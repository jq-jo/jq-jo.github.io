---
layout: post
title: "asset-pipeline"
date: 2016-08-10 16:42:54 +0900
comments: true
categories:
---
<small>
# Assetとは
RailsにはJavaScriptやCSS、Imageなどの要素をアセットと呼びます。アセットはそれぞれに 'app/assets/javascripts/'、 'app/assets/stylesheets/'、 'app/assets/images' フォルダーで管理します。
Railsは基本的にJavaScriptとCSSの拡張言語のCoffeeScriptとSCSSを提供します。
# Asset Pipelineとは
JavaScriptやCSS、Imageなどのアセットを最小化(minify)または圧縮して連結するフレイムワーク
# Asset Pipelineの役割
##### 1.アセットファイルのパスの管理
##### 2.アセットのコンパイル
##### 3.アセットの依存関係の整理
## アセットファイルのパスの管理
Assetsの中のパスの管理をします。
<div class="colorscripter-code" style="color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#272727; border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0"><div style="margin:0; padding:0; color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">/assets/javascript/user.js</div><div style="padding:0 6px; white-space:pre; line-height:130%">/assets/stylesheet/user.css</div></div></td></tr></table></div>
というファイルを
<div class="colorscripter-code" style="color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#272727; border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0"><div style="margin:0; padding:0; color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">/assets/user.js</div><div style="padding:0 6px; white-space:pre; line-height:130%">/assets/user.css</div></div></td></tr></table></div>
のように1つのディレクトリで管理されているようにアクセスさせてくれます。
## アセットのコンパイル
Javascript、CSSのかわりに、CoffeeScript、SCSSを使うことも多いと思います。browserはCoffeeScriptとSCSSを読めないのでCoffeeScriptとSCSSをJavaScriptとCSSにコンパイルしなきゃいけないです。このように、ファイルを適当な形式に変換してくれる機能をAsset Pipelineと言います。<br>
必要となるgemは以下です。
<div class="colorscripter-code" style="color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#272727; border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0"><div style="margin:0; padding:0; color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">gem&nbsp;&nbsp;<span style="color:#68ec68">'sprockets'</span>&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">gem&nbsp;&nbsp;<span style="color:#68ec68">'coffee_script'</span>&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">gem&nbsp;&nbsp;<span style="color:#68ec68">'scss'</span></div></div></td></tr></table></div><br>
### sprockets
Asset Pipelineの基盤の機能を提供してくれます。
### coffee_script && scss
それぞれCoffeeScript、SCSSを使うためです。
## アセットの依存関係の整理
Asset間の依存関係を整理します。このようにファイルの読み込みの順番を管理します。他のファイルに影響を与えないためにコメントアウトの形式で書きます。<br>
<small>app/assets/javascript/application.js</small>
<div class="colorscripter-code" style="color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#272727; border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0"><div style="margin:0; padding:0; color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#999999">//&nbsp;=&nbsp;require&nbsp;jquery&nbsp;</span></div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#999999">//&nbsp;=&nbsp;require&nbsp;jquery_ujs&nbsp;</span></div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#999999">//&nbsp;=&nbsp;require_tree.</span></div></div></td></tr></table></div>
Railsのアプリケーションでは複数のCSS、Javascriptを1つのファイルにまとめて提供することが主流となっています。それは複数ファイルが存在すればリクエストの数が増えてページの読み込みが遅くなるからです。アプリケーションの内の依存関係をまとめて提供するための仲介になるファイルを「manifest file」と呼び、デフォルトでは application.js、application.css になります。
# Asset Pipelineをコントロールする
## develpment/productionの設定
設定は/config/environments/ファイルに書きます。
### config.assets.js_compressor
Javascriptの圧縮ライブラリの設定。productionではuglifierというgemを利用しているが nilの設定にして無効にすることも出来る。
default設定
development: nil
production: :uglifier
### config.assets.css_compressor
CSSの圧縮ライブラリの設定。
default設定
development: nil
production: :uglifier
### config.assets.compile
動的にcompileするかの設定。trueだとprecompileしていないファイルを動的にコンパイルするのでproductionではfalseが良さそうです。
default設定
development: true
production: false
### config.assets.digest
pipelineを通した後のファイルにつく数字をつけるかどうかです。
default設定
development: false
production: true
### config.assets.debug
debugするかの設定。
default設定
development: true
production: false
## precompileの設定
<small>config/initializers/asset.rb</small>
<div class="colorscripter-code" style="color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#272727; border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0"><div style="margin:0; padding:0; color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#999999">#&nbsp;Precompile&nbsp;additional&nbsp;assets.&nbsp;</span></div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#999999">#&nbsp;application.js,&nbsp;application.css,&nbsp;and&nbsp;all&nbsp;non-JS&nbsp;/&nbsp;CSS&nbsp;in&nbsp;app&nbsp;/&nbsp;assets&nbsp;folder&nbsp;are&nbsp;already&nbsp;added.&nbsp;</span></div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#999999">#&nbsp;Rails.application.config.assets.precompile&nbsp;+&nbsp;=&nbsp;%&nbsp;w&nbsp;(search.js)&nbsp;</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">Rails&nbsp;.&nbsp;application&nbsp;.&nbsp;config&nbsp;.&nbsp;assets&nbsp;.&nbsp;precompile&nbsp;&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">+</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;&nbsp;%&nbsp;w&nbsp;(<span style="color:#0086b3"></span><span style="color:#ff3399">*</span>&nbsp;.js&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">*</span>&nbsp;application.css)</div></div></td><td style="vertical-align:bottom; padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none; color:white"><span style="font-size:9px; word-break:normal; background-color:#4f4f4f; color:white; border-radius:10px; padding:1px">cs</span></a></td></tr></table></div>
## Asset Pipelineの流れ
### production
例えば、下記設定の場合。<br>
<small>/config/environments/production.rb</small>
<div class="colorscripter-code" style="color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#272727; border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0"><div style="margin:0; padding:0; color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">config&nbsp;.&nbsp;assets&nbsp;.&nbsp;js_compressor&nbsp;&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;&nbsp;:&nbsp;uglifier&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">config&nbsp;.&nbsp;assets&nbsp;.&nbsp;css_compressor&nbsp;&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;&nbsp;:&nbsp;sass&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">config&nbsp;.&nbsp;assets&nbsp;.&nbsp;compile&nbsp;&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;&nbsp;<span style="color:#c10aff">false</span>&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">config&nbsp;.&nbsp;assets&nbsp;.&nbsp;digest&nbsp;&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;&nbsp;<span style="color:#c10aff">true</span>&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#999999">#&nbsp;config.assets.debug&nbsp;=&nbsp;false</span></div></div></td></tr></table></div>
1.assetにあるソースコードをコンパイル(coffee -> js、 scss -> css)<br>
2.コンパイルしたソースコードを合わせる (複数のファイルのコードをまとめる）<br>
3.ファイルを圧縮する（uglifier、sass)<br>
4.ファイルにダイジェストを付与する（ファイル名につくハッシュ)<br><br>
これでブラウザに送られます。<br><br>
### development
例えば、下記設定の場合。
<div class="colorscripter-code" style="color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#272727; border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0"><div style="margin:0; padding:0; color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#999999">#&nbsp;config.assets.js_compressor&nbsp;=&nbsp;nil&nbsp;</span></div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#999999">#&nbsp;config.assets.css_compressor&nbsp;=&nbsp;nil&nbsp;</span></div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#999999">#&nbsp;config.assets.compile&nbsp;=&nbsp;true&nbsp;</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">config&nbsp;.&nbsp;assets&nbsp;.&nbsp;digest&nbsp;&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;&nbsp;<span style="color:#c10aff">false</span>&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">config&nbsp;.&nbsp;assets&nbsp;.&nbsp;debug&nbsp;&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;&nbsp;<span style="color:#c10aff">true</span></div></div></td></tr></table></div>
1.assetにあるソースコードをコンパイル(coffee -> js、 scss -> css)<br><br>
これだけでブラウザへ送られます。
</small>
##参照
<small>
http://qiita.com/shizuma/items/1980bf885906c73238b6
</small>
