## gulpを利用するためのステップ
* node.jsのインストール（初回のみ）
* gulpをグローバルインストール（初回のみ）
* gulpを各プロジェクトにインストール  
<br><br><br>


## 将来的にvccwやその他の開発系フレームワークとか使うならhomebrewとnodebrewでnode.jsのインストールを強くお勧めします。
[nodeのインストール](https://github.com/mamimu-tetau/vccw)
こちらでnodeのインストールまでを済ませてください。
<br><br><br>


## gulpをグローバルにインストール（初回のみ）
```
npm install -g gulp
```  
<br><br><br>



# 　ここからはプロジェクトごとに行う作業
<br><br><br>

## npmのバージョンを最新にしておく
できる限りこちは時間がある時に最新版にアップデートしておいてください。
```
npm install -g npm
```
<br><br><br>


今回はこのリポジトリにサンプルを用意したいのでgit cloneかzipとかでダウンロードしてください。
<br><br>
## 静的サイトのディレクトリ構成はこんな感じ
```
project
  ├── node_modules
  ├── public_html（納品用）
  ├── src（開発用）
  │   ├── scss/*.scss
  │   ├── **/*.html
  │   └── assets
  │       ├── css
  │       ├── images
  │       ├── js
  │       ├── scss
  ├── gulpfile.js
  ├── package.json
```
<br><br><br>


## プロジェクトフォルダに移動
ターミナルを立ち上げて上記でダウンロードしたディレクトリに移動します。
```
cd C:\hoge\fuga\piyo\project
```
ターミナルにそのフォルダをドロップするとパス勝手に入ります。便利
<br><br><br>


## package.jsonの作成
インストールしたパッケージとか一覧で見れるから作っておいた方が便利ですが簡単なプロジェクトならスルーでOK。
プロジェクト名やらなんやら設定が出てくるから必要なら設定
```
npm init
```
プロジェクト名やらなんやら設定が出てくるから必要なら設定。
enterで進んでいく。で最後にyes
```
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (desktop) 
version: (1.0.0) 
description: 
entry point: (index.js) 
test command: 
git repository: 
keywords: 
author: 
license: (ISC) 
About to write to /Users/hacca/Desktop/package.json:

{
  "name": "desktop",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this OK? (yes) 
```
こんな感じの出る。
<br><br><br>



## gulpのローカルインストール

```
npm install gulp --save-dev
```
できる限りバージョンはCLIと合わせる。
毎回プロジェクトごとに最新版をインストールしているとグローバルのgulpとバージョンがあわなくなるのでその時はグローバルもアップデート。

##### --saveと--save-dev
違いはようわからんすのでgoogleさんに聞いて。  
で、なんで付けるかというとnpm install で --save をつけると、 package.json にインストールしたパッケージ名とそのバージョンが自動的に保存され、他で同じ環境を作ることが出来る。  
[参考:面倒な作業も発狂しない！Web制作を超効率化するgulp.jsの始め方考](https://www.webprofessional.jp/introduction-gulp-js/)
<br><br><br>


## gulpプラグインをインストール

##### Sassコンパイル + browser-sync
```
npm install gulp-sass gulp-autoprefixer gulp-sourcemaps gulp-filter gulp-notify gulp-plumber browser-sync --save-dev
```  

* gulp-sass Sassのコンパイル
* gulp-autoprefixer PostCSSのベンダープレフィクス自動化　だれかPostCSSでの書き方教えて
* gulp-sourcemaps　CSSのソースマップ作成　他にもいいのあればアップデートしたい
* gulp-filter　ストリームの中身をグロブパターンによって抽出したファイルだけに
* gulp-notify　デスクトップ通知
* gulp-plumber エラーが発生しても落ちないように  
* browser-sync ファイル変更を監視し、自動でブラウザリロードを行ってくれる  
<br><br><br>

##### + Minify
sassのコンパイルだけが目的ならこちらはスルーでOK

```
npm install gulp-cssmin gulp-imagemin imagemin-mozjpeg gulp-uglify imagemin-pngquant --save-dev
```  

* gulp-cssmin CSS Minify
* gulp-imagemin 画像圧縮
* imagemin-mozjpeg jpg圧縮（要検討）
* imagemin-pngquant png圧縮（要検討）
* gulp-uglify js圧縮（要検討） 
<br><br><br>


# 実際に動かしてみましょう。

macのapacheの設定がまだなら↓を行ってください。
[macのapacheとかもろもrも](https://github.com/mamimu-tetau/mac-apache)
<br><br>
で上記URLのバーチャルホストを記入するところで今回のやつを追記
```
<VirtualHost *:80>
    serverName localhost.mamimu.div
    #作業フォルダ
    DocumentRoot "/Users/あんたのユーザー名/ダウンロードしたフォルダ/project/src"
	<Directory "/Users/あんたのユーザー名/ダウンロードしたフォルダ/project/src">
		Require all granted
	</Directory>
</VirtualHost>
npm install gulp-sass gulp-autoprefixer gulp-sourcemaps gulp-filter gulp-notify gulp-plumber browser-sync --save-dev
```  
さらに

browserSyncも使うので今回はhostsファイル




# 余談

## Gulpバージョン変更
##### グローバル
```
npm uninstall -g gulp
npm install -g gulp
```
<br><br><br>

##### ローカル
```
npm uninstall gulp --save-dev
npm install gulp --save-dev
```
<br><br><br>

## BrowserSync
はまりどころbodyタグ抜けてるとダメす
