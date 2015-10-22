# js workshop #2

## 概要

### 日時

2015/10/xx 19:30〜20:30

### 目的

package.jsonを書くことでNPMを気軽に使えるようにする。jsファイルの縮小処理をgulpで自動化してみることで、タスクランナーの基礎をつかむ。

### 想定参加者

* Node.jsを触ったことがある
  * ない場合は[js workshop #1](https://github.com/do7be/js_workshop_1)をやってみてください


### 内容

* git clone
* npmの初期化
* npmでscriptをつくる
* npmでgulpをインストールする
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

ワークショップ用リポジトリをクローンする

```
$ cd ${適当なディレクトリ}
$ git clone https://github.com/do7be/js_workshop_2.git
$ cd js_workshop_2
```

### npmの初期化

```
$ npm init

対話式でプロダクトの情報を設定していく。今回はEnterを押していくだけでいい。
```

対話が終わるとpackage.jsonというファイルが作られている。

```
$ less package.json
```

### npmでscriptをつくる

```
$ vi package.json

// 下記部分のように書き換える
"scripts": {
    "start": "node index.js"
},
```

```
$ npm start

index.jsが実行される。
```

このように、簡単なスクリプト（実行、コンパイルなど）を登録することができる。

### npmでgulpをインストールする

```
$ npm install --save-dev gulp
```

* `--save-dev`をつけると、package.jsonのdevDependenciesにパッケージ名が書き込まれる
    * これは、開発環境にて使用するパッケージであることを明確にしている
    * devDependenciesに書かれたパッケージは`npm install -dev`でインストールされる。
* `--save`でインストールすると、package.jsonのdependenciesに追記される
    * ここに書かれたパッケージは動作自体に必要なものであることを明記している
    * こちらは`npm install`でインストールされる
* `-g`というのもよく使う。`--global`の略
    * このオプションをつけると、現在のホームディレクトリ直下にNPMパッケージがインストールされるため、今後同じパッケージを別のプロダクトでインストールする必要がなくなる
    * ツール系やコマンドライン系はグローバルで入れると良い
    * `-g`をつけない場合はカレントディレクトリ直下にパッケージがインストールされる


### gulpとは

* タスクランナー
* プログラムの実行、コンパイル、縮小化などのタスクを管理し、簡単に実行できるように扱うツール
* ファイル監視ができるため、「ファイルの内容を変更し保存したら自動的にコンパイルしてテストしてブラウザリロードする」までを自動化することもできる
* ちょっと前まではgruntというタスクランナーが主流だったが、記述の自由度などからgulpが使われることが多い
* 最近ではFlyというものもでてきた


### gulpで縮小化してみる

gulpfileで使用するパッケージをインストールする。

```
$ npm install --save-dev gulp-uglify gulp-rename gulp-plumber
```


```
$ vi gulpfile.js

// 使用するパッケージを宣言
var gulp    = require("gulp"),
    uglify  = require("gulp-uglify"),
    rename  = require('gulp-rename'),
    plumber = require("gulp-plumber");

// タスクの登録
gulp.task('uglify', function() {
  return gulp.src('src/program.js')
    .pipe(plumber())
    .pipe(uglify())
    .pipe(rename('program.min.js'))
    .pipe(gulp.dest('./'));
});

// gulpとだけ打った時にuglifyが実行されるように
gulp.task('default', ['uglify']);
```

gulpはJavaScriptで記述することができ、gulp.srcで読み込んだファイルをpipeで次の処理に渡していく。

```
$ gulp uglify
```
もしくは
```
$gulp
```

src/program.jsが縮小化され、program.min.jsが作成される。


### gulpでファイル監視して縮小処理を自動化してみる

```
$ vi gulpfile.js

// 下記を追加
gulp.task('watch', function(){
  gulp.watch(['src/*.js'], ['uglify']);
});
```

```
$ gulp watch
```

別のシェルを立ち上げる。

```
$ vi src/program.js

// 下記を追加
console.log('Nice! gulp!!!!!');
```

保存すると、自動で縮小化され、index.min.jsが作成される。

```
$ node program.min.js
```

これで毎回手動で縮小化とかコンパイルしなくてよくなった！

### cssの圧縮

以下をインストールしてやってみる。

https://www.npmjs.com/package/gulp-minify-css


以上でjs workshop #2は終了です。

### （時間が余ったら）learnyounode

Node.js入門者用workshopper

http://nodeschool.io/

```
$ npm install -g learnyounode-jp
$ cd ${適当なディレクトリ}
$ learnyounode
```


## LICENSE

Thanks to https://github.com/gulpjs/gulp
