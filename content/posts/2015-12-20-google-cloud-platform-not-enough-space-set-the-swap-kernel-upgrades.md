---
layout: post
title: 'Google Cloud Platform - 空間不足, 設定 swap, kernel 升級'
date: 2015-12-20
comments: true
categories: [google cloud platform]
---
## Google Cloud Platform - 空間不足, 設定 swap, kernel 升級

### kernel 升級, 設定 swap

最近強者我朋友在 Google Cloud Platform 上的 computer engine 上的 VM 升級 kernel 時發現升一升就 GG 了

連不進去了

用快照再開一台試驗還是如此

最後跟另一位大大研究了一下發現說原來是升級時記憶體不足導致整個系統卡住了, 然後又可能剛好 kernel 升級失敗所以就進不去 Lunix

因為是開最小的機器(f1-micro (vCPUs: shared, RAM: 0.60 GB) * does not support local SSD - 10GB storage)

我朋友又有跑許多 service 在上面, 所以記憶體會不足, 所以大大建議掛 swap 上去, 但 computer engine 在開 VM 時沒設 swap 的選項啊, 沒有切 partition 給 swap 的選項啊

大大就說了可以用 file 的方式建 swap 出來, 所以強者我朋友就建好後在升級就過了, 成功升級 kernel

因為我也是開同等級的 VM 所以我朋友也建議我也做一下這機制

大大的建議怎麼可以忽視呢

所以就來記錄一下步驟吧

```shell
# count 依自己的設定設置
sudo dd if=/dev/zero of=/swapfile bs=1M count=512
# 格式化 swap
sudo mkswap /swapfile
# 啟動 swap
swapon /swapfile
```

為了在開機時掛載 swap

要做以下處理

```shell
vim /etc/fstab

# 加入
/swapfile    swap    swap    defaults    0 0
```

這時就好了

有裝 htop 可用 htop 看一下就會發現有 swap 了

![螢幕快照 2015-12-21 上午12.13.22.png](http://user-image.logdown.io/user/3170/blog/3202/post/379436/4H5o7kFbSQCXK2KRdihI_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-12-21%20%E4%B8%8A%E5%8D%8812.13.22.png)

但是強者我朋友又發現一個問題

就是明明開 10G 了, 空間卻不夠用?

### 空間不足的問題

經過強者我朋友經過一番地找查

總算找到原因了

就是 kernel 的問題!

他在 `/boot` 底下發現一卡車的 kernel

原來是這一卡車的 kernel 佔掉一堆空間

所以其實只要做 `sudo apt-get autoremove` 就可以移掉無用的 kernel

移除前

![螢幕快照 2015-12-21 上午12.27.46.png](http://user-image.logdown.io/user/3170/blog/3202/post/379436/rKWHb6ETTdyssTBjdZZM_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-12-21%20%E4%B8%8A%E5%8D%8812.27.46.png)

移除後

![螢幕快照 2015-12-21 上午12.26.27.png](http://user-image.logdown.io/user/3170/blog/3202/post/379436/lcw6zUl5TGukhWZXNxsZ_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-12-21%20%E4%B8%8A%E5%8D%8812.26.27.png)

**省了一半空間!**

且發現一個現象

VM 在重啟時會自動升級 kernel

所以機器開小沒掛 swap 或空間不足

在重開 VM 就可能會 GG

[refer - CentOS 建立 Swap File](http://iammic.pixnet.net/blog/post/6204976-centos-%E5%BB%BA%E7%AB%8B-swap-file)

[refer - Aptitude - Ubuntu 正體中文 Wiki](http://wiki.ubuntu-tw.org/index.php?title=Aptitude)
