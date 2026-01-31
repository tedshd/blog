---
title: "Claude MCP 瀏覽器自動化：Playwright 與 Chrome DevTools 指南"
date: 2026-01-31T22:53:03+08:00
draft: false
categories: ["Claude", "MCP", "Playwright", "Chrome DevTools", "Browser Automation"]
---

# Claude MCP 安裝與使用指南

## 什麼是 MCP

MCP（Model Context Protocol）是一個開放協議，讓 Claude 能夠連接外部工具和資料來源，例如瀏覽器自動化、檔案系統存取、API 整合等。

---

## 確認已安裝的 MCP

### Claude Code（命令列）

```bash
# 列出所有已設定的 MCP 伺服器
claude mcp list

# 查看特定伺服器的詳細資訊
claude mcp get <server-name>

# 在 Claude Code 互動模式中檢查伺服器狀態
/mcp
```

### Claude Desktop（桌面應用程式）

設定檔位置：
- **macOS**：`~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**：`%APPDATA%\Claude\claude_desktop_config.json`

成功連線後，在對話輸入框的右下角會看到 MCP 伺服器指示器。

---

## MCP 安裝範圍

| 範圍 | 說明 | 參數 |
|------|------|------|
| **local** | 僅當前專案目錄可用（預設） | 無需參數 |
| **project** | 專案層級，可與團隊共享 | `-s project` |
| **user** | 全域，所有專案都可用 | `-s user` |

### 安裝為全域

```bash
claude mcp add -s user <server-name> <command>
```

---

## 安裝 Playwright MCP

Playwright MCP 提供瀏覽器自動化功能，適合 UI 測試、截圖、填表單、網頁爬取等任務。

### Claude Code

```bash
# 本地安裝（僅當前專案）
claude mcp add playwright npx @playwright/mcp@latest

# 全域安裝（所有專案可用）
claude mcp add -s user playwright npx @playwright/mcp@latest
```

這種通用的工具建議使用全域安裝。

### Claude Desktop

編輯設定檔，加入：

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
}
```

儲存後完全關閉並重啟 Claude Desktop。

### 前置需求

**Chrome DevTools MCP 需要 Node.js v20.19 以上：**

1. 安裝 Node.js（從 [nodejs.org](https://nodejs.org) 下載 LTS 版本）
2. 瀏覽器會在首次使用時自動安裝

```bash
node --version
```

---

## 安裝 Chrome DevTools MCP

Chrome DevTools MCP 提供深度調試和性能分析功能。

### Claude Code

```bash
# 全域安裝
claude mcp add -s user chrome-devtools npx chrome-devtools-mcp@latest

# 或使用 headless 模式
claude mcp add -s user chrome-devtools -- npx chrome-devtools-mcp@latest --headless
```

### 連線失敗的解決方法

Chrome DevTools MCP 需要連接到正在運行的 Chrome 瀏覽器。

**啟動帶有遠端調試的 Chrome：**

Windows：
```bash
"C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222
```

macOS：
```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222
```

---

## Playwright vs Chrome DevTools MCP 比較

| 特性 | Playwright MCP | Chrome DevTools MCP |
|------|----------------|---------------------|
| **主要用途** | 瀏覽器自動化、UI 測試 | 深度調試、性能分析 |
| **瀏覽器支援** | Chrome、Firefox、WebKit | 僅 Chromium 系列 |
| **工具數量** | 21 個工具 | 26 個工具 |
| **Token 消耗** | ~13.7k tokens | ~18k tokens |
| **需要手動啟動瀏覽器** | 否（自動管理） | 是 |
| **適合場景** | 截圖、填表單、爬資料、E2E 測試 | Console 監控、網路請求分析、性能追蹤 |

### 建議

**大多數情況下，Playwright MCP 就夠用了**，除非你需要：
- 深度性能分析（Performance traces）
- Heap snapshots
- 詳細網路請求監控

---

## Claude 如何選擇使用哪個 MCP

### 可用性優先

Claude 只會使用**連線成功**的 MCP。如果 Chrome DevTools 連線失敗，會自動使用 Playwright。

### 任務類型

如果兩個都可用，Claude 會根據任務選擇：

| 任務 | 選擇 |
|------|------|
| 截圖、填表單、點擊 | Playwright |
| 性能分析、網路請求監控 | Chrome DevTools |
| 讀取 console | 兩者皆可 |

### 明確指定

你也可以在提示中指定使用哪個工具：

```
用 Playwright 幫我打開 example.com 並截圖
```

---

## 常用指令彙整

```bash
# 列出所有 MCP
claude mcp list

# 新增 MCP（本地）
claude mcp add <name> <command>

# 新增 MCP（全域）
claude mcp add -s user <name> <command>

# 查看特定 MCP
claude mcp get <name>

# 移除 MCP
claude mcp remove <name>

# 在互動模式中檢查狀態
/mcp
```

---

## 疑難排解

| 問題 | 解決方法 |
|------|----------|
| MCP 連線失敗 | 確認 Node.js 已安裝（`node --version`） |
| Chrome DevTools 連不上 | 手動啟動帶 `--remote-debugging-port=9222` 的 Chrome |
| 設定沒生效 | 完全重啟 Claude Desktop（包括背景程序） |
| JSON 格式錯誤 | 檢查設定檔的 JSON 語法是否正確 |