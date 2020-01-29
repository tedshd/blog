---
layout: post
title: 'web - mobile web on iPhone X first preview'
date: 2017-10-02
comments: true
categories: [iOS, Apple]
---
## web - mobile web on iPhone X first preview

### Intro

On 2017 9/12.

Apple published iPhone X.

And this device has so special screen.

<img src="https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-10-02%20%E4%B8%8A%E5%8D%8811.23.11.png?alt=media&amp;token=2072f272-5d9a-4d36-9552-ea68113a4afe">

So many web & iOS developer worry about some case like.

<img src="https://www.apple.com/newsroom/videos/iphone-x-ar/posters/iPhone_X_AR_The_Machines_571x321.jpg.large.jpg">

(form Apple)

OMG!

It can effect app show on full screen.

So Apple has provide guideline about iPhone X.

[iPhone X - Overview - iOS Human Interface Guidelines](https://developer.apple.com/ios/human-interface-guidelines/overview/iphone-x/)

It is great change for web & iOS developer.

For web developer, we need this design guideline

[Designing Websites for iPhone X | WebKit](https://webkit.org/blog/7929/designing-websites-for-iphone-x/)

Apple provide new CSS function handle this problem.

And it is in W3C [working group](https://github.com/w3c/csswg-drafts/issues/1693#issuecomment-330909067)

### Preview iPhone X

But we can preview iPhone X in Xcode.

1. Update your Xcode to Xcode 9.

2. Open a new Project and set build iOS simulator as iPhone X.

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-10-02%20%E4%B8%8A%E5%8D%8811.51.49.png?alt=media&token=df8b38b8-add6-4a49-812b-8a65d5cc2a2a)

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-10-02%20%E4%B8%8A%E5%8D%8811.52.03.png?alt=media&token=dff6a51f-979d-415e-ad37-fff7c01fcb83)

3. Xcode > Open Developer Tool > iOS Simulator

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-10-02%20%E4%B8%8A%E5%8D%8811.52.46.png?alt=media&token=a3318002-8d07-47b8-9c2b-05960bc3c356)

4. we can use Safari test web now.

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-10-02%20%E4%B8%8B%E5%8D%8812.11.24.png?alt=media&token=05515073-1ba1-4b98-a1d1-be3b08587fc2)

### Result

Some case

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-10-02%20%E4%B8%8B%E5%8D%8812.14.15.png?alt=media&token=c91ea97a-e1ac-4ee6-9b7e-ab06ad0e0d42)

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-10-02%20%E4%B8%8B%E5%8D%8812.13.27.png?alt=media&token=c43337d7-fec7-4e5a-a6d1-951b8aed1228)

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-10-02%20%E4%B8%8B%E5%8D%8812.14.41.png?alt=media&token=bf6b3221-45a6-4c14-afa1-c353e9aa485c)

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-10-02%20%E4%B8%8B%E5%8D%8812.14.57.png?alt=media&token=5a6a397d-d109-4d9e-8720-2e7d72f79125)

Safari App has handle safe area & follow iPhone X design.

So we maybe don't worry about this problem on Safari.

But maybe we need worry about chrome on iOS and other webview in App.
