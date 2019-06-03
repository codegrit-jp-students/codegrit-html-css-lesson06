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

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/cqL318kz/1/embedded/html,css,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

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

## さらに学ぼう

### 記事で学ぶ

[CSS Transforms - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transforms)
[CSS Transitions- MDN](https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Transitions)
[CSS Animations - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations)

### 動画で学ぶ

[transformで要素を変形させてみよう - ドットインストール](https://dotinstall.com/lessons/basic_css3_v2/31915)
[transitionを使ってみよう - ドットインストール](https://dotinstall.com/lessons/basic_css3_v2/31917)
[animationを使ってみよう](https://dotinstall.com/lessons/basic_css3_v2/31918)
