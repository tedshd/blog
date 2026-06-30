---
title: "如何自己建立 mcp 服務"
date: 2026-06-30T23:51:33+08:00
draft: false
categories: []
---

## Intro

因為 RD 常用 markdown 格式來記錄
但是有時要交付給其他非開發的人或是要提供出去
就得轉成 PDF
很麻煩
所以想了一下
乾脆寫了一個處理 markdown 轉成 pdf 的程式
然後再包成 mcp

## MCP 的連接方式

MCP 目前主要有兩種連接方式：**Local MCP** 和 **Remote MCP**

### Local MCP

透過 `stdio`（標準輸入輸出）在本機執行，AI client 直接啟動一個子程序來溝通。

**優點：**
- 設定簡單，不需要架伺服器
- 可以直接存取本機檔案系統和資源
- 不需要網路連線
- 安全性較高，資料不會離開本機

**缺點：**
- 只能在本機使用，無法共享給其他人
- 每個使用者都要自己安裝和設定
- 不適合需要多人協作或雲端使用的情境

### Remote MCP

透過 HTTP + SSE（Server-Sent Events）或 WebSocket 連接到遠端伺服器。

**優點：**
- 可以共享給團隊成員，統一管理
- 不需要在每台機器上安裝
- 可以部署到雲端，隨時隨地使用
- 適合整合需要後端服務的工具

**缺點：**
- 需要架設並維護伺服器
- 需要處理認證和安全性問題
- 有網路延遲，效能不如 local
- 資料會經過網路傳輸，需要注意隱私

### 選擇建議

個人開發工具、需要存取本機資源的情境 → **Local MCP**

團隊共用工具、需要整合雲端服務的情境 → **Remote MCP**

---

## md2pdf 開發說明

### 技術選型

- **Node.js** 作為執行環境
- **Puppeteer**（Headless Chrome）負責將 HTML 渲染成 PDF
- **highlight.js** 處理程式碼語法高亮
- **Mermaid** 支援流程圖、sequence diagram 等圖表渲染

轉換流程是先將 Markdown 轉成 HTML，再交給 Puppeteer 渲染輸出 A4 PDF。

### Local MCP 開發方式

本機版透過 `stdio` 通訊，tool 接收的是**檔案路徑**，由 server 直接讀取本機檔案轉換，Markdown 內容不會進入 Claude context，**token 消耗少**。

安裝與設定：

```bash
# clone 專案並安裝相依套件
git clone https://github.com/<your-username>/md2pdf.git
cd md2pdf
npm install
```

加入 Claude Code CLI：

```bash
claude mcp add md2pdf node /path/to/md2pdf/src/mcp-server.js
```

加入 Claude Desktop，編輯 `~/Library/Application Support/Claude/claude_desktop_config.json`：

```json
{
  "mcpServers": {
    "md2pdf": {
      "command": "node",
      "args": ["/path/to/md2pdf/src/mcp-server.js"]
    }
  }
}
```

設定完成後直接用自然語言觸發：

> 幫我把 /Users/yourname/docs/report.md 轉成 PDF

### Remote MCP 開發方式

遠端版透過 HTTP 部署，tool 接收的是**完整 Markdown 內容字串**，server 轉換完成後儲存 PDF 並回傳下載連結。

運作流程：
1. 使用者傳送 Markdown 內容給 server
2. Server 轉換成 PDF 並儲存
3. 回傳下載連結（`GET /files/<id>.pdf`）
4. 使用者點連結下載

本機測試：

```bash
npm start

# 健康檢查
curl http://localhost:3000/health
```

部署推薦使用 **Render** 或 **Railway**，兩者都支援 Docker 部署，有免費方案可以先測試。

Docker 部署：

```bash
docker build -t md2pdf-mcp .
docker run -p 3000:3000 -e BASE_URL=https://your-domain.com md2pdf-mcp
```

加入 Claude Code CLI（遠端版）：

```bash
claude mcp add --transport http md2pdf https://<your-app>.onrender.com/mcp
```

---

## 注意事項

### 中文字型問題

部署到 Linux 環境（Render、Railway、Docker）時，容器預設不含中文字型，PDF 中文字會變成方塊或亂碼。

解法是在 Dockerfile 安裝 `fonts-noto-cjk`（Google 思源黑體）：

```dockerfile
RUN apt-get install -y fonts-noto-cjk
```

> 注意：`fonts-noto-cjk` 約 400 MB，會讓 image 變大、首次部署時間較長，但字型品質最完整。

### CI / Docker 環境需要停用 sandbox

Puppeteer 預設會啟用 Chrome sandbox，在 Docker 或 CI 環境通常沒有對應的 kernel 權限，需要加上 `--no-sandbox` 參數，否則轉換會失敗。

```bash
node src/cli.js docs/README.md --no-sandbox
```

或設定環境變數：

```bash
PUPPETEER_NO_SANDBOX=true
```

### Remote MCP 的 token 消耗

遠端版需要把完整 Markdown 內容傳給 server，這些內容同時也會進入 Claude context，文件越長消耗的 token 越多。如果主要是自己使用、文件又有隱私疑慮，建議選 local 版本。

### Render Free 方案的冷啟動

Render Free 方案閒置 15 分鐘後會休眠，冷啟動需要 30-60 秒。如果需要穩定使用，升級到 Starter 方案（$7/月）或改用 Railway。

---

## 實測比較：Remote MCP vs Local MCP

以一份 15,674 bytes（6,846 字元）的 Markdown 文件做實測，結果如下。

### 耗時比較

| 測試 | 環境 | 耗時 | 備註 |
|---|---|---|---|
| Remote 第一次 | Render（冷啟動） | **158 秒**（約 2.6 分鐘） | 含 server cold start + 渲染 |
| Remote 第二次 | Render（已熱機） | **10.45 秒** | 服務已啟動，速度大幅提升 |
| Local | 本機 stdio | **10 秒** | 穩定，無冷啟動問題 |

### Token 消耗比較

| 環境 | 傳入內容 | 估算 Token 數 |
|---|---|---|
| Remote MCP | 完整 Markdown 內容字串 | **~7,800 tokens**（5,300–10,300）|
| Local MCP | 檔案路徑（絕對路徑字串） | 極少，幾乎可忽略 |

### 結論

- **Remote 冷啟動很痛**：Render Free 方案閒置後首次呼叫要等將近 3 分鐘，不適合需要即時轉換的情境
- **熱機後 Remote 和 Local 速度差不多**：兩者都在 10 秒左右完成渲染
- **Local MCP token 消耗遠低於 Remote**：Remote 每次轉換要額外消耗約 7,800 tokens，文件越長差距越大
- **自己用選 Local 最划算**：速度相當、token 省、資料不離開本機
