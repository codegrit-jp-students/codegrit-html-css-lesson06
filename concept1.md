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

例ではCodeGritのロゴに変化を加えていきます。

![ロゴマーク](./images/mark.png)

### Transformsの2つのプロパティ

Transformsには以下の2つのプロパティがあります。

#### 1. transform

`transform`はどのような変化を起こしたいか指定するために利用します。

例えば、画像を横の長さはそのまま、縦の長さを半分の大きさにし、45度右回りに回転してみます。

```html
<img class="logo-mark" src="./images/mark.png">
```

```css
.logo-mark {
  transform: scale(1, 0.5) rotate(45deg);
}
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/Lj6ns4q2/3/embedded/html,css,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

また、画像の位置を画像の横幅の半分の長さだけ左に移動したいという場合以下のようにします。

```css
.logo-mark {
  transform: translate(-50%, 0);
}
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/785e24hq/1/embedded/html,css,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

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

この画像の左底を起点に90度回転したいという場合は、以下のようにします。

```css
.logo-mark {
  transform-origin: bottom left;
  transform: rotate(90deg);
}
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/jbag7vmp/1/embedded/html,css,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

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