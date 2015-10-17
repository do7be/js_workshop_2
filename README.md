# js workshop #2

## 概要

### 日時

2015/10/xx 19:30〜20:30

### 目的

package.jsonを書くことでNPMを気軽に使えるようにする。js,cssを縮小処理をgulpで自動化してみることで、タスクランナーの基礎をつかむ。

### 想定参加者

* Node.jsを触ったことがある
  * ない場合はjs workshop #1をやってみてください


### 内容

* git clone
* npm init
* npm script
* npm install to gulp
* gulpで縮小化してみる
* gulpでファイル監視して縮小処理を自動化してみる


### 持ち物

ノートPC

* Mac推奨
* WinでもいいがVM構築必須
* Git環境


## workshop前の基本知識

* NPMとは
  * Node.js Package Manager
  * Node.jsで使用するパッケージやライブラリやツールのダウンロード・インストール・設定などを簡単に実現するツール
  * 最近だと、Node.jsを使わないプロダクトでも必須
    * 例えばjsファイル、cssファイルの縮小化。様々なタスクの自動化など。（タスクランナーを使うため）
  * Gitとものすごく相性が良い
    * リポジトリをcloneして`$ npm install`をするだけで基本的に実行環境が整う
    * 開発環境を整えるには`$ npm install -dev`


## workshop本題

### 準備
