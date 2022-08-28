---
marp: true
paginate: true
theme: default
---

<style>
section {
    background-color: #030303;
    color: #FFF;
    padding-left: 150px; 
    padding-right: 150px;
}
h1 {
    color: #00ff00
}
h2 {
    color: #00ff00

}
</style>

# メモ

- CMS/ headlessCMS
- バックエンド/フロントエンド
- データベース、サーバ
- NodeJS の説明消す？
- web フレームワークの説明を増やしたい
- HTML/CSS の説明を飛ばす
- アイコン画像挿入
- 文章を体言止め箇条書きに直す
- ビジュアルを増やす

---

# Web サイトの作り方を調べてみた

LT 会のサンプル
written by tomoyahiroe

---

## お題目

0. 自己紹介
1. はじめに
2. 静的な WEB ページの作成
3. リッチな WEB ページの作成
4. HTML ファイルの自動生成
5. Node.js について
6. WEB 開発フレームワーク
7. まとめ
8. 今後の課題
9. 参考文献

---

## 0. 自己紹介

- 横国経済 2 年、廣江友哉(ひろえ ともや)
- 趣味はソフテニ、ベース
- TypeScript を学習中。

  <img src="./images/intro_myself.JPG" width="400">

---

## 1. はじめに

### 目的

- 常盤祭企画 Lumos Lightening talks の発表例を提示すること
- モダンな WEB フレームワーク(特に NuxtJS)に入門するための知識を補強すること

### 想定読者

- HTML/CSS を書いたことがある人

### 注意事項

- 不備は Lumos ではなく tomoyahiroe に帰属
- 親切な方からのご指摘に期待(TwitterID: @yudetamageta)
- 本旨に影響を与えない知識はあえて雑に説明

---

## 2. 静的な WEB ページの作成

- あらかじめ用意された HTML と CSS(と JS)を WEB サーバが配信し、私たちの PC 上のブラウザに表示する形式をとるサイト

  - WEB サーバ ... 作成した HTML/CSS ファイルを配信してくれるもの
  - ブラウザ ... ウェブサイトを表示してくれるアプリケーション(Google Chrome,Firefox, Microsoft Edge)

---

## JavaScript による DOM 操作

- DOM ... HTML/CSS の要素のこと(正確には違う)

[DOM の説明記事]('https://eng -entrance.com/what-is-dom')

---

### HTML/CSS 要素の操作(DOM 操作)でこんなことができる

- 昔の CSS はそんな機能豊富じゃなかったらしい
  - ダークモード/ライトモードの切り替え
  - 見出しのフェードイン
  - 現在時刻の表示
  - スライダーの表示
  - ハンバーガーメニューの実装

...

---

### JavaScript によるページ要素の操作

- 具体的に JavaScript で書かれるコードの簡易的な例

```js
// 架空JSのコード
button.onclick = function () {
  const defined_name = document.getElementsByClassName(
    "class_name_of_html_element"
  )[0];
  defined_name.innerText = "Lumosに入会する";
};
```

---

## 3.5 静的サイトでできないこと

- できないこと
  - HTML ファイルの自動生成
  - ユーザ毎に異なる画面を表示
  - 機能毎にファイルを分けられない
- 死ぬほどめんどくさいこと
  - 画面遷移(リンクの移動)を伴わない画面表示の変更
  - (上の例のように)HTML ファイルに JS で定義した変数の値を埋め込むこと(データバインド)
- 不便なこと
  - 繰り返し使用される表示(ヘッダー/フッター)を HTML ファイル全部に書かなければならない

<p style="text-align:center"><strong>WEBフレームワークなら全部簡単にできる!</strong></p>

---

## 4. HTML ファイルの自動生成(動的な WEB サイトの作成)

---

---

### どうやって生成するのか

- いくつかの方法はありますが、ほぼ共通しているのは私たちのブラウザ側(Google Chrome, Firefox 等)ではなく、**サーバ**(世界のどこかにあるでかい PC みたいなもん)側で何かしらの処理が動くことです。
- 例えば、ブログサイトだったら１つの記事のタイトルや本文のデータをデータベース(その名の通り必要な情報群)から取ってきて、サーバで HTML ファイルにそのデータをぶち込み通信します。その HTML をブラウザが受け取って私たちはサイトを見ているわけです。
- この例で言うところの、データを取ってきて HTML ファイルにデータをぶち込む作業を前ページに登場した各々の言語が行います。

---

- 超超超ざっくりとしたイメージ
  <img src="./images/image.png" width="900">

---

## 5. Node.js について

---

### JavaScript はサーバで動かない!?

- 実のところ、JavaScript は Chrome や Firefox といったブラウザで実行することのできる言語で、私たちの手元にある PC 上では動作しない言語です。これは、サーバでも同じことが言えます。
- サーバとは常に動いている PC のようなもので、サーバ上でも本来 JavaScript は動作しません。これはつまり、JavaScript ではサーバ上でデータを HTML ファイルにぶち込む作業などができないことを意味します。
- この問題を解決するのが、**Node.js** です。

---

### Node.js とは??

- Node.js とは、本来 JavaScript が動作しない、PC 上で JavaScript のプログラムを実行するための**実行環境**です。
- 実行環境ってなんぞや？とよくわからないかもしれませんが、Node.js の公式サイトからダウンロードすれば誰の PC にだって JS の実行環境(つまり Node.js)ができます。
- 英語を覚えたら、英語の命令を理解して行動できるのと同じように、PC に Node.js をインストールすると、PC は JavaScript を理解して命令を実行できるようになります。つまり、サーバに Node.js をインストールすれば良いわけです。
- Node.js のおかげで、JavaScript はサーバ上でさまざまな処理を走らせることができます。

---

## 6. WEB 開発フレームワーク

動的ページの生成や状態管理など、素の言語だと面倒な処理を簡単にしてくれる便利なテンプレートフォルダのようなもの。これ以降の説明は私の知識不足と記述の簡単化のためより雑な説明となります。ご容赦を。

---

### JS 以外のフレームワーク

WEB 開発のためのフレームワークはいろいろな種類があり、言語ごとに複数個有名なフレームワークがあります。ここではその一例を取り上げます。

- Python
  - **Django**
  - **Flusk**
- PHP
  - **Laravel**
- Ruby
  - **Ruby on rails**

---

### ナウイ JS フレームワーク(フロントエンドフレームワーク)

- **Vue.js**
  - Vue.js をより便利にした **Nuxt.js** がある。
- **React.js**
  - React.js をより便利にした **Next.js** がある。
- **Gatsby.js**
  - React.js ベースのフレームワークらしい。(SSG 専門らしい??)

---

- 例えば、Nuxt.js を使うと、`create nuxt-app [your project name]` と打つだけでこんなフォルダが生成されます。
  <img src="./images/nuxt_folder.png" height="600">

---

- サイトを立ち上げると、すでに...
  <img src="./images/default_nuxt.png" width="900">

---

## 7. まとめ

- WEB サイトを作る方法はたくさんある。
- それぞれ違ったメリットがあり、サイトの目的や必要な機能によって使用する技術も変わってくると思う。
- ググれば意外と情報が出てくる。ただ、ブラウザで開くタブの量がエグいことになる。

---

## 8. 今後の課題

- SSG, SSR, SPA についても解説できるように理解したい。
- ライブラリーの説明を端折ってしまったのが悔しい。(ライブラリーとフレームワークの違いはよく聞かれるので説明できるようにしたい。)
- JS のパッケージ管理ツールについて時間的に説明できなかった。
- JS フレームワークについてもっと掘り下げたかった。
- テスティングフレームワークについても調べたい。

---

## 9. 参考文献

- JavaScript の歴史(https://www.jetbrains.com/ja-jp/lp/javascript-25/)
- Node.js について(https://qiita.com/non_cal/items/a8fee0b7ad96e67713eb)
- WEB フレームワーク(https://kaopiz.com/ja-news-best-10-web-framework-2020/)
