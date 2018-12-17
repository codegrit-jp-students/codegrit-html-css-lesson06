# CSSを利用したアニメーション

## 目的

- CSS TransitionとTransformの基礎を学ぶ
- CSS Animationの基礎を学ぶ

## CSSを利用したアニメーション

Webサイトを見ている時に、画面から透明な状態から現れてくる文字や、マウスをホバーすると動くボタンやカードなど動きのあるパーツを見たことがあるでしょうか？こうした動きを出すには、以前はブラウザの対応の問題でJavascriptを使うのが主流でした。しかし近年では、ほぼ全ての主要ブラウザでCSSのみを利用してアニメーションを表現することが出来るようになっています。今回は、CSSを利用してアニメーションを作る方法を学びましょう。


## CSS TransitionとCSS Animationモジュール

CSSによって動的なコンテンツを作成するには、Transitionプロパティを利用する方法と、CSS Animationモジュールを利用した方法の２つがあります。それぞれの特徴は以下の通りです。

- CSS Transtion

最初の状態と最後の状態の2つのポイントの間の変化を指定することが出来ます。単純な変化を簡単に書くことが出来るためボタンのホバー時の色変化や形の変化など1つのエレメントの単純なアニメーションを表現するのに向いています。

- CSS Animationモジュール

Transitionとは異なり、変化のポイントを複数作ることが出来ます。そのため、CSS Transitoinに比べてより複雑なアニメーションを表現するのに向いています。

## CSS Transforms

CSS Transitionの説明に入る前に、CSS Transformsについて説明していきます。Transformsを利用すると、例えばあるHTML要素を拡大、拡大させたり、斜めに表示したり、上下反転させたりというふうに要素を変化させることが出来ます。

ここでは、例と一緒にTransformsの使い方を見ていきましょう。

### Transformsの2つのプロパティ

Transformsには以下の2つのプロパティがあります。

#### 1. transform

`transform`はどのような変化を起こしたいか指定するために利用します。

例えば、先ほどの画像を横の長さはそのまま、縦の長さを半分の大きさにし、45度右回りに回転してみます。

```html
<img class="logo-mark" src="./images/logo-mark.png">
```
```css
.logo-mark {
  transform: scale(1, 0.5) rotate(45deg)
}
```

また、画像の位置を画像の横幅の半分の長さだけ左に移動したいという場合以下のようにします。

```css
.logo-mark {
  transform: translate(-50%, 0)
}
```

**transformのシンタックス**

上の例の`translate()`や`scale()`のように変化を起こすために呼び出すものを**transform関数**と呼びます。transformはこのtansform関数を複数組み合わせて表現します。

transform関数は、例で出てきた3つの他にも横幅のみを拡大するscaleXや縦幅のみ拡大するscaleYなど多数あります。最もよく使うのが例で挙げた3つです。

- `scale(横幅の拡大割合、縦幅の拡大割合)`

`scale()`は要素を拡大縮小するために利用します。拡大割合には0以上の任意の数値が入ります。また数字を1つだけ書いた場合横軸、縦軸が同じ割合拡大されます。例えば縦横ともに50%の大きさにしたい場合`scale(0.5)`と書きます。

- `translate()`

`translate()`は要素の位置を移動するための関数です。px単位での指定と%単位での指定の両方が可能です。scale関数と同様で値を1つだけ書いた場合は縦横両方とも同じ値の分だけ移動します。

- `rotate(角度)`

`rotate()`は要素を回転するための関数です。角度の指定方法は複数ありますが最も一般的なものは`deg`を利用する方法です。degreeは角度の略で一周で360度で右回りで考えます。例のように要素を45度右回りに回転したい場合は`rotate(45deg)`と入力します。

transformに利用できるtransform関数は現在全部で21あります。ここで全部は紹介出来ないため、例えば3Dで要素を扱いたい場合などはMDNの公式ドキュメントを参照して下さい。

[transform - MDN](https://developer.mozilla.org/ja/docs/Web/CSS/transform)


#### 2. transform-origin

`transform-origin`は要素に変化を与える際の基準になる位置を決めるために利用します。。デフォルトでは`transform-origin: 50%, 50%, 0`と設定されており、これは要素の中心を意味しています。

例えば、以下のCodeGritのロゴに変化を加えるとしましょう。

![ロゴマーク](./images/mark.png)

この画像の左底を起点に90度回転したいという場合は、以下のようにします。

```css
.logo-mark {
  transform-origin: bottom left;
  transform: rotate(90deg);
}
```

**transform-originのシンタックス**

transform-originでは横軸をx軸、縦軸をy軸、そしてx軸とy軸と垂直に交わる軸をz軸としています。z軸は3Dとして要素を扱いたい場合に利用します。それぞれx軸は左端が0、y軸は上端が0、z軸はx軸とy軸が存在する平面を0とします。平面の奥を指定してしたい時は-10pxのようにマイナスの値を入れ、手前を指定したい場合は10pxのようにプラスの値を入れます。

`transform-origin`は以下のような指定方法が出来ます。

1. 3つの値で指定する

3つの値でしていする場合は、以下のように書きます。

`x軸上の位置 y軸上の位置 z軸上の位置`

デフォルトでは`50% 50% 0`が指定されており、これは要素の中心を意味します。

2. 2つの値で指定する

3D要素を扱わない場合は2つの値のみを指定します。

`x軸上の位置 y軸上の位置`

x軸とy軸の値は、px、em、%などで指定出来る他、left、right、center、bottom、topなどのワードでも指定が出来ます。ワードを使う場合は`left top`のように指定します。

3. １つの値で指定する

x軸とy軸上それぞれ同一の数値を指定したい場合は1つの値のみで定義出来ます。

例えば、`transform-origin: 50% 50%;`と`transform-origin: 50%;`は同一の意味となります。

[サンプルコード](https://github.com/codegrit-jp-students/codegrit-html-css-lesson06-sample-transform)

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

## CSS Animationモジュールを利用したアニメーション

CSS Transitionでは2つのポイントしか指定できませんでした。それに対して、CSS Animationモジュールでは`@keyframe`プロパティを利用することで複数の変化ポイントを作る事ができます。

まずは例を見てみましょう。ここでは以下のようなアニメーションを作ってみます。

- 最初は50px四方の正方形
- 1秒かけて円に変わったあと、また1秒かけて正方形に戻る
- 色は最初は赤色で最後は青色に変わる。

```css
@keyframes to-circle { /* アニメーションにto-circleという名前を付けています */
  0% { /* 背景色は最初と最後は赤です */
    background-color: red;
  }
  50% {
    border-radius: 50%; /* 正方形から円へと変化させます。 */
  }
  100% {
    background-color: blue;
    border-radius: 0;
  }
}

.square {
  height: 50px;
  width: 50px;
  margin: 0;
  padding: 0;
  border: 0;
  animation-name: to-circle; /* animationにto-circleを利用 */
  animation-duration: 2s;
  animation-iteration-count: infinite;
}
```

[サンプルコード](https://github.com/codegrit-jp-students/codegrit-html-css-lesson06-sample-css-animation)

いかがでしょうか、アニメーションというと難しそうですが書き方自体は直感的にも分かりやすいのではないでしょうか？ これ以降の項目ではCSS Animationモジュールの各プロパティと、アニメーションを指定するための`@keyframes`プロパティについて詳しく見ていきましょう。

### @keyframes

@keyframesは**at-rule**というCSSルールの一つです。このプロパティを利用することで変化ポイントそれぞれの状態を指定することが出来ます。例えば最初のボタンの例は以下のように書き換えることが出来ます。

@keyframesのシンタックスは以下の通りです。

```css
@keyframes アニメーション名 {
  各ポイント { /* 0%から100%で指定 */
    プロパティ
  }
}
```

### CSS Animationモジュールのプロパティ

CSS Ainmationモジュールで利用するプロパティは、`animation-delay`や`animation-duration`のように`Transitions`と似ているものと、CSS Animation独自のものとがあります。以下ではそれぞれ見ていきましょう。注意すべき点は、CSS Animationモジュールを利用する場合、Transitionsとは異なりプロパティごとの指定が出来ず、アニメーションが要素全体に適用される点です。

#### animation-name

`animation-name`はその名の通り、利用するアニメーション(@keyframes)の名前を指定します。

#### animation-duration

`animation-duration`は`transition-duration`と同様にアニメーション全体でどの程度の時間をかけて変化を起こすかを指定します。

#### animation-delay

`animation-delay`は`transition-delay`と同様にアニメーション開始のタイミングを遅らせるために利用します。

#### animation-timing-function

`animation-timing-function`は`transition-timing-function`と同様に変化の起こり方を指定します。

#### animation-iteration-count

`animation-iteration-count`は指定のアニメーションを何度繰り返すかを指定します。値には数字または`infinite`が入ります。

#### animation-direction

`animation-direction`はアニメーションの順序を指定出来ます。

- normal(デフォルト): 0%から100%へとアニメーションが再生されます。
- reverse: 100%から0%へとアニメーションが逆に再生されます。
- alternate: 0%から100%と100%から0%への再生が交互に起こります。

#### animation-fill-mode

`animation-fill-mode`では何も再生されていない状態で、100%の状態か0%の状態どちらを表示しておくかを指定できます。

- none(デフォルト): 再生し終えるとアニメーションが消えます。
- forwards: 再生し終えると、再生終了時の状態のままとなります。
- backwards: 再生前の状態でも、0%のときの状態が表示された状態となります。
- both: forwardsとbackwardsの両方が適用されます。

#### animation-play-state

アニメーションの再生中、停止中を指定出来ます。Javascriptを利用することでボタンを押すと、このプロパティを変更し再生するというようなことが出来ます。デフォルトでは
`running`(再生中)となっています。

#### animation

`transition`と同様に、animation関連のプロパティを1行で指定するためのショートハンドです。基本的にこのショートハンドを利用するのが推奨されています。

**animationのシンタックス**

`animation: <duration> <timing-function> <delay> <iteration-count> <direction> <fill-mode> <play-state> <name>;`

animationプロパティを利用すると最初の例は次のように書くことが出来ます。

## ベンダープレフィックス

Transform、Animationを利用する際には以下のようにベンダープレフィックスを設定する必要があります。


```css
.transform-prefixes {
  -webkit-transform: rotate(30deg);
  -ms-transform: rotate(30deg);
  transform: rotate(30deg);
}
.animation-prefixes {
  -webkit-animation: (指定内容);
  animation:         (指定内容);
}

@-webkit-keyframes 名前 {...}
@keyframes 名前 {...}

```

## チャレンジ

[チャレンジ6](./challenge/README.md)

## さらに学ぼう

### 記事で学ぶ

[CSS Transforms - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transforms)
[CSS Transitions- MDN](https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Transitions)
[CSS Animations - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations)

### 動画で学ぶ

[transformで要素を変形させてみよう - ドットインストール](https://dotinstall.com/lessons/basic_css3_v2/31915)
[transitionを使ってみよう - ドットインストール](https://dotinstall.com/lessons/basic_css3_v2/31917)
[animationを使ってみよう](https://dotinstall.com/lessons/basic_css3_v2/31918)
