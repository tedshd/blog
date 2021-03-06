---
layout: post
title: 'Computer Science - 作業系統'
date: 2013-08-27
comments: true
categories: [Computer Science]
---
## 作業系統

指令集複雜度之所以不重要,是因為有副程式.副程式可以讓一串指令在程式中被無限使用.事實上,程式設計師可以用呼叫副程式的方式將原有的指令定義為新的指令.利用 Jump 指令把副程式的位址載入程式計數器中,將執行順序轉移到副程式中,但轉移之前,電腦會將之前程式計數器的內容儲存在特定記憶體中,當副程式執行完時,會有另一個指令讀取到這個返回位址(return address),而讓順序跳回到原先呼叫副程式時的位置繼續執行.

這種呼叫副程式的過程可以遞迴的執行,某個副程式本身可以跳到另一個副程式裡執行,然後這個副程式在跳到別的副程式,依此類推,在遞迴函數中,副程式本身亦可以呼叫自己.為了紀錄這種成層疊加的副程式呼叫過程,電腦必須用一種有系統的方式儲存返回位址,當每個副程式執行完畢時才知道該回到哪裡去.但不能把所有的返回位址都紀錄在同一地方,因為一但副程式成層疊加起來,電腦就必須記住一個以上的返回位址.通常,電腦會將返回位址循序儲存在一群記憶體位置中,稱為堆疊(stack),最後一個返回位址會放在[堆疊頂端(top of the stack)].堆疊記憶體的運作方式就好像疊在一起的盤子一樣,總是從頂端加入或取出東西.這種後進先出(last-in,first-out)的儲存方式,對於儲存一疊疊副程式的返回位址來說確實完美,因為每個副程式都必須等它自己所呼叫的副程式執行完成後才會結束.

電腦中總是裝有一些很有用的副程式,它們統稱為作業系統(operating system).

作業系統包含了能讀寫鍵入字元或是在螢幕上畫線條的副程式,不然就是其他與使用者互動的副程式.作業系統決定使用者所看到的界面,也掌控了電腦與所執行程式之間的界面,這是由於作業系統提供了一套比機械語言指令更豐富且更複雜的指令.

事實上,程式設計師並不在乎他所謂的功能是以電腦硬體或是由作業系統軟體所執行,只要它們能產生同樣的效果就好了.同樣的程式在兩種不同的電腦上運作時,可能其中一個是透過硬體的算術運算執行,而另一個則是以作業系統的副程式來執行.同樣的,電腦的作業系統也會仿效它型電腦的指令集.有時電腦製造商會利用這種模仿方式,讓新型電腦像舊型一樣操作,如此一來就可以不經過任何修改而讓舊有的軟體在新型電腦上運作.

作業系統通常包含執行基本輸入輸出的副程式,也就是能讓程式和外界互動的副程式.其運作方式是將電腦記憶體中某特定位置與鍵盤或滑鼠等輸入設備連接在一起,或是與顯示器之類的輸出設備連接. EX.鍵盤上的空白鍵可能接到記憶暫存器23號,當按下空白鍵時就可以在位址 23 中讀到資料 1,反之讀到資料 0.另一個記憶暫存器可能控制螢幕上的某個點的顏色,假設螢幕上的每一點所顯示的資料都儲存再不同的記憶體位置中,那只要將適當的位元資料寫入記憶體中,電腦就可以在螢幕上畫出任何圖案.

除了這些輸出入機制外,我們所描述的電腦其實只是一部接了記憶體的有限狀態機,而這兩者都可以用暫存器和布林邏輯區組建構出來,控制電腦的有限狀態機相當複雜,設計這樣的機器其實是就是經過一連串記憶體資料,位址和狀態順序等細節,以執行每一個指令,然後再將它的狀態轉換成布林邏輯的過程.既然有限狀態機和記憶體是由暫存器和邏輯區組所組成的,那這些東西就可以用各種技術加以實作, EX.電子電路 液壓管路 滑桿.
