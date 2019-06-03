## CSS Transitonを利用したアニメーション

CSS Transitionを利用すると、最初の状態から最後の状態への変化に対して、いつ変化し始めるのか、どの程度時間をかけて変化するのか、変化はどのように起こるのか、どのプロパティ(フォント、色、要素のプロパティ全てなど)に対して変化を起こすのか、などを指定することが出来ます。

詳しい説明の前に実際に例を見てみましょう。ここでは以下の条件を満たすボタンを作ってみます。

- ホバーすると`transform: scale(1.2)`が適用され、サイズが拡大する。
- ホバーするとバックグラウンドとフォントの色が変わる。
- ボタンがホバーされてから0.5秒後に変化が開始される。
- 上の2つの変化が1秒かけて起こる。
- 変化は一定の速さで起こる。

これは以下のように書くことで実現出来ます。

```css
.btn {
  font-size: 12px;
  margin: 0;
  padding: 10px 20px;
  background-color: gray;
  transition-property: all; /* ボタン全体に変化を与える */
  transition-duration: 1s; /* 1秒間(second)かけて変化を起こす */
  transition-delay: 0.5s; /* ホバーから0.5秒後に変化が開始する */
  transition-timing-function: linear; /* 一定のスピードで変化させる */
}
.btn:hover {
  transform: scale(1.2); /* サイズを1.2倍にする */
  background-color: black;
  color: #fff;
}
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/sqwp2Lhj/1/embedded/html,css,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

[サンプルコード](https://github.com/codegrit-jp-students/codegrit-html-css-lesson06-sample-transition)

以降では、この例を基にTransitionのプロパティをそれぞれ解説していきます。

### Transitionのプロパティ

#### transition-property

`transtion-property`は変化をさせたいプロパティを指定するために利用します。デフォルトでは`all`が設定されています。例えば上記のボタンで、ボタンのサイズだけにtransitionを適用させたい場合は`transition-property: transform`のように指定します。

#### transition-duration

`transition-duration`は変化をどの程度の時間をかけて起こしたいのかをしていします。ボタンの例では`transition-duration: 1s;`と設定することで1秒かけて変化を起こしています。`s`を使うと秒単位で、`ms`を使うとミリ秒単位で指定が可能です。

#### transition-delay

`transition-delay`は変化の開始を遅らせるために使います。ボタンの例では`0.5s`と指定することで、ホバーしてから0.5秒経ってから変化が開始するようにしました。`transition-duration`と同様に秒単位、ミリ秒単位での指定が出来ます。

#### transition-timing-function

`transition-timing-function`は変化をどのように起こすのかを指定することが出来るプロパティです。デフォルトでは`ease`が指定されています。よく利用するのは`ease`、`ease-in`、`ease-in-out`などです。例えば、デフォルトの`ease`ではゆっくりとスタートした後に、変化が早くなり、またゆっくりとなり変化を終えます。`transition-duration`が十分長くないと、各変化方法の違いは認識しづらいので普段はデフォルトの`ease`を使用すれば良いでしょう。

#### transition

`transition`は上の`transition-property`、`transition-duration`、`transition-delay`、`transition-timing-function`を1行で書くためのショートハンドです。transitionは以下のようなシンタックスで指定します。一つずつプロパティを書くと冗長になるため、特に理由がないのであれば常にこのショートハンドを利用するようにしましょう。

`transition: <property> <duration> <delay> <timing-function>;`

例えば、ボタンの例で指定した各プロパティは以下のように書き直すことが出来ます。

```css
/* transitionプロパテイ未使用 */

.btn {
  transition-property: all; /* ボタン全体に変化を与える */
  transition-duration: 1s; /* 1秒間(second)かけて変化を起こす */
  transition-delay: 0.5s; /* ホバーから0.5秒後に変化が開始する */
  transition-timing-function: linear; /* 一定のスピードで変化させる */
}

/* transitionプロパティ使用 */

.btn {
  transition: all 1s 0.5s linear;
}
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/athLus96/embedded/html,css,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>