---
layout: post
title: "Hybrid, Native, Responsive"
date: 2016-08-31 16:02:03 +0900
comments: true
categories:
---
<small>
# Mobile Applicationの種類
<img src="/images/threeApps.jpg"><br>
1. Native Application<br>
2. Hybrid Application<br>
3. Responsive Web Application<br>
## Native Application
Native Appの開発でアプリはios, androidなどの特定のMobile Platformに合わせて作成することになり、一般的にはPlatform会社の開発道具を使用して作られます。他のPlatformにはコードの再使用はできません。<br><br>
####メリット
• 性能が高い（特にゲームの場合）<br>
<small>- グラフィックユーザーインターフェース、速度など</small><br>
• デバイスの全ての機能を使える（センサー、カメラ、連絡先など）<br>
• Appleのアップストア、GooglePlayなどの公開アップストアを通して配布<br>
####デメリット
• 開発者不足<br>
• Platform別にそれぞれアプリを作るため費用を使う<br>
• Platform別にコードベースを管理するため費用と時間を使う<br>
• 長い開発期間<br>
• 開発のかかる時間で各Platformのバージョンがそれぞれになる可能性がある<br>
• 各アップストアの承認手順を待たなきゃいけないのでアプリの配布が遅くなる可能性がある<br>
####開発道具
• Apple: XCode<br>
• Android: Android Studio, eclipse<br>
## Responsive
HTML 5, CSS, JSなどを使用して作るWeb Application。デバイスのブラウザーを通して接近できます。デバイスの機能を使用することが難しいです。<br>
####メリット
• 既存Web開発者を活用して作れる<br>
• 費用が一番安い<br>
• 一つのコードベースだけ管理する<br>
• 早く編集、アップデートや配布が可能<br>
####デメリット
• インターフェースが標準Native Appと違う可能性がある<br>
• マルチメディアの性能がよくない<br>
• デバイスの機能を使うことが難しい<br>
####開発道具
HTML 5, JS, CSSを使ってWebを作ることに使用される全ての開発道具はResponsive Web Applicationを作ることができます。<br>
• AngularJS - Googleが管理しているopen source web application framework<br>
• Ember.js - open source javascript web application framework<br>
• React - facebookが管理しているopen source javascript library<br>
• JQuery - javascript library<br>
• Bootstrap - Responsiveを優先するCSS framework<br>
## Hybrid Application
Hybrid ApplicationはResponsive AppをMobile Platformで実行するAppになります。ウェブ標準を使用するが最終アプリはデバイスでnative appで実行されます。Native AppとResponsive Appのメリットだけ合わせるように誕生した。<br>
####メリット
• ウェブ標準を使用して作る（APIやデバイスの機能に接近するためコーディングが必要<br>
• 既存ウェブ開発者を活用して開発可能<br>
• 早く編集、アップデートや配布が可能<br>
• 各PlatformでNative Appで実行する<br>
####デメリット
• インターフェースが標準Native Appと違う可能性がある<br>
• Native Appよりは性能がよくない<br>
• 一般的にデバイスの全ての機能が使えるが新たな機能は少し時間がかかる<br>
• Platformによってそれぞれ違うコードベースにしなきゃいけない<br>
####開発道具
• Apache Cordova - HTML 5, CSS, javascriptを使用しているResponsive Appを基盤にしてNative Appをbuildするopen source platform<br>
• Adobe PhoneGap - Adobeが作ったApache Cordovaの変形<br>
• Alpha Anywhere - Responsive Appを作ってそれをNative Appに配布するようにしてくれる開発環境<br>
• Ionic Framework - AngularJSやCordovaと連携してResponsive Appを基盤にしてNative Appをbuildするユーザーインターフェース中心のframework<br>
#b#まとめ
<img src="/images/chart_apps.png">

</small>
##参照
<small>
http://www.itworld.co.kr/news/95791


</small>
