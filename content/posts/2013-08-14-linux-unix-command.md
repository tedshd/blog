---
layout: post
title: 'Linux/unix command'
date: 2013-08-14
comments: true
categories: [mac Linux]
---
## command

### User
```sh
su / sudo
# 最高權限使用者

su -u <user name> bash
# 切換使用者

exit
# 跳出最高權限使用者

shutdown
# 關機
shutdown -h now 立即關機
shutdown -h +m m分鐘後關機
shutdown -h hh:mm 幾點幾分關機

reboot
# 重開機

login
# 登入使用者

logout / exit
# 登出

passwd
# 修改密碼
useradd / adduser
# 新增帳號

passwd
# 修改密碼

sudo -u <user name> <shell>
# 切換使用者

date
# 顯示時間
date 月日時分(root修改)

history
# 顯示輸入過的指令

ps
# 顯示目前執行的工作

chmod <777>
# 修改權限
# rwx
# 2*2 2 1

chown <user>:<user> <file>
# 修改該 file owner

uname -a
# 確認 system OS

uanme -r
# linux kernel

df
# 確認硬碟空間

```

### File Management
```sh
ls
# 列出檔案
ls -a 列出以.開頭的檔案
ls -l 列出檔案詳細
ls -- directory 查看該目錄內容

cd
# 切換目錄
cd .. 回上一層
cd / 切換到系統根目錄
cd 目錄
cd 路徑

pwd
# 顯示目前所在目錄

clear
# 清空畫面

info / man
# 查詢指令

tab
# 同DOS的tab功用,切換下一個選擇的項目

mkdir
# 建立目錄

rmdir
# 刪除目錄

touch
# 建立檔案

cp
# 複製檔案
cp -v 顯示複製過程
cp -r <folder> <directory> 把資料夾複製到某目錄
cp <file> <path>

rm
# 刪除檔案或目錄
rm -f 強制刪除檔案
rm -rf 強制刪除目錄

mv
# 搬移或更名檔案或目錄
mv <file> <path>
mv <舊檔名> <新檔名>

cat
# 瀏覽檔案內容

less
# 分頁瀏覽檔案內容
q 離開

find / locate
# 尋找檔案
# find -name "php.ini"

more
# 顯示畫面暫停

|
# 管線
將指令結果輸出給另一個指令

>
# 重導
將指令結果輸出到檔案中檔案原有內容被刪除

>>
# 重導
將指令結果輸出到檔案中檔案原有內容不被刪除

grep -r 'XXX' *
# 找內含XXX的檔案

scp
# ssh copy
scp <username@tohostname>:<remote file> <local path>
scp <local file> <username@tohostname>:<remote path>
scp -r <username@tohostname>:<remote directory> <local path>
scp -r <local directory> <username@tohostname>:<remote path>
scp -i <key> <local directory> <username@tohostname>:<remote path>
```

tar -zcvf <archive-name>.tar.gz <directory-name>
# 壓縮資料夾

tar -zxvf <archive-name>.tar.gz <directory-name>
# 解壓縮資料夾

sudo lsof -i -P -n | grep LISTEN
netstat -tulpn | grep LISTEN
# 確認開啟的port
lsof -n -i | grep LISTEN **(for Mac)**

### apt

```sh
apt --installed list
# 列出已安裝套件

sudo aptitude update
# 修復損毀的相依性

sudo aptitude safe-upgrade
# 較為安全的升級方式
sudo aptitude full-upgrade
# 針對整個系統做升級, 可能會更動系統核心的版號
sudo aptitude dist-upgrade
# 同於 full-upgrade
```

### Mail server
```sh
host -t mx <mail domain>
# 查詢是否已紀錄此 mail domain
```
