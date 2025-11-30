# Elemental仕様書

## はじめに

Elementalは、thinking元代表であるSorakimeが考案しました。

## 理念

「より自然に、わかりやすく、誰が見ても同じように。」
コンピューター上のデザインは、現実の制約に縛られない。特徴のある動きと、白と黒の濃さだけの極限までシンプルな色使いを採用した。

## 基本設計 / Foundations

### 単位
基本単位として、px（ピクセル）を使用します。
ただし、CSSを使用する場合は、必要に応じてrem、emを使用してよい。

前提知識

px（ピクセル）は1つのドット（画素）あたる単位である。しかし、ディスプレイの高解像度化により、小さく表示されてしまう問題が発生した。ここで、ソフトウェア上で表示サイズを調整するスケーリングという仕組みでが導入された。これにより、どのディスプレイで表示をしても適切なサイズ見やすく表示できるようになった。
以上のように、物理的なドットを「ハードウェアピクセル」、ソフトウェア上で論理的に扱うドットを「ソフトウェアピクセル」という。

### カラー

Elementalでは、色を白黒モノクロームで表現します。

#### カラーパレット

基本色として、以下のカラーパレットに示す色を使用します。
このカラーパレットは彩度、明度が同じになるよう、色相を変えています。

- 無彩色

<table>
	<tr>
		<th>カラー名</th>
		<th>色（RGB・16進）</th>
	</tr>
	<tr>
		<td>Black</td>
		<td>#000000</td>
	</tr>
	<tr>
		<td>Black (Light)</td>
		<td>#0F0F0F</td>
	</tr>
	<tr>
		<td>Gray (Darker)</td>
		<td>#3F3F3F</td>
	</tr>
	<tr>
		<td>Glay (Dark)</td>
		<td>#5F5F5F</td>
	</tr>
	<tr>
		<td>Gray</td>
		<td>#7F7F7F</td>
	</tr>
	<tr>
		<td>Gray (Light)</td>
		<td>#9F9F9F</td>
	</tr>
	<tr>
		<td>Gray (Lighter)</td>
		<td>#BFBFBF</td>
	</tr>
	<tr>
		<td>White (Dark)</td>
		<td>#EFEFEF</td>
	</tr>
	<tr>
		<td>White</td>
		<td>#FFFFFF</td>
	</tr>
</table>

- 有彩色

<table>
	<tr>
		<th>カラー名</th>
		<th>色（RGB・16進）</th>
	</tr>
	<tr>
		<td>Red</td>
		<td>#ED1A3D</td>
	</tr>
	<tr>
		<td>Yellow</td>
		<td>#FFD400</td>
	</tr>
	<tr>
		<td>Green</td>
		<td>#00B06B</td>
	</tr>
	<tr>
		<td>Blue</td>
		<td>#2063F1</td>
	</tr>
</table>

#### 主に使用する色

カラーパレットから選択しています。

確実に心地よいUXを提供するため、窮屈な印象を与えないように、Elementalでは背景色と文字色のコントラストを少し低めに選びました。

ライトモードは白を基調とするのに対し、ダークモードは黒を基調としたもので、対称的な印象を与えます。

色がきつすぎる場合があるので、通常はライトモードとダークモードのみを使用してください。

<table>
	<tr>
		<th colspan="2"></th>
		<th>ライトモード（白）</th>
		<th>ライトモード</th>
		<th>ダークモード</th>
		<th>ダークモード（黒）</th>
	</tr>
	<tr>
		<th rowspan="2">基底色</th>
		<th>背景色</th>
		<td>White</td>
		<td>White (Dark)</td>
		<td>Black (Light)</td>
		<td>Black</td>
	</tr>
	<tr>
		<th>文字色</th>
		<td>Black (Light)</td>
		<td>Black</td>
		<td>White</td>
		<td>White (Dark)</td>
	</tr>
	<tr>
		<th rowspan="2">第一色</th>
		<th>背景色</th>
		<td>Black (Light)</td>
		<td>Black</td>
		<td>White</td>
		<td>White (Dark)</td>
	</tr>
	<tr>
		<th>文字色</th>
		<td>White</td>
		<td>White (Dark)</td>
		<td>Black (Light)</td>
		<td>Black</td>
	</tr>
	<tr>
		<th rowspan="2">第二色</th>
		<th>背景色</th>
		<td>Gray</td>
		<td>Gray</td>
		<td>Gray</td>
		<td>Gray</td>
	</tr>
	<tr>
		<th>文字色</th>
		<td>White</td>
		<td>White (Dark)</td>
		<td>White</td>
		<td>White (Dark)</td>
	</tr>
	<tr>
		<th rowspan="2">第三色</th>
		<th>背景色</th>
		<td>Gray (Lighter)</td>
		<td>Gray (Lighter)</td>
		<td>Gray (Darker)</td>
		<td>Gray (Darker)</td>
	</tr>
	<tr>
		<th>文字色</th>
		<td>Black (Light)</td>
		<td>Black</td>
		<td>White</td>
		<td>White (Dark)</td>
	</tr>
</table>

### ベース（Bases）

ベースには、色、文字、図形、アニメーションが含まれます。

#### 文字

```
フォント:
欧文: Barlow
和文: Noto Sans JP

太さ:
Light
Regular
Medium
Bold

---

テキスト
見出し
h1: 40px
h2: 36px
h3: 32px
h4: 28px
h5: 24px
h6: 20px
ウェイト: Bold

本文
16px
ウェイト: Regular

強調
元のサイズ
ウェイト: Medium
```

指定されたフォントは必要に応じて変更が可能です。

#### 図形

主に四角形と円を使用します。
なお、四角形はそれぞれの角に8pxの丸みをもたせます。

影は、xy原点中心、ブラー16pxとします。


```
使用する図形:
四角形
円

共通:
影:
なし
角の丸み:
8px
```

### 余白

各要素は、子要素の外側に最低8pxの余白を持つものとします。

#### アニメーション

イーズインアウト
0.2秒

最も優雅でスムーズに動作するアニメーションです。


### コンポーネント（Components）

コンポーネントには、各種ボタンと二種類の検索ボックスなどが含まれます。

#### ボタン（Button）




#### 検索ボックス（）





### レイアウト（Layouts）

二つのレイアウトが決められています。
それぞれ、機能を決められた場所にすべて収納することで、潔く、使いやすくしています。

Vertical Layout と Horizon Layoutを組み合わせてデザインすることも可能です。

#### Vertical Layout

Vertical Layoutは、垂直に配置するタブや目次を表示することに適しています。

Vertical Layoutは、Sidebar（サイドバー）とItems（項目）の、2つの要素から構成されています。


```
+++++++++++++++++++++++++++++++++
+         +                     +
+         +                     +
+         +                     +
+         +                     +
+ Sidebar +        Items        +
+         +                     +
+         +                     +
+         +                     +
+         +                     +
+++++++++++++++++++++++++++++++++
```

Sidebarは、内側の余白を8px、子要素間の余白を8pxとります。

Itemでは、内側の余白を8px、子要素間の余白を8pxとります。

Itemでは、外側余白を、要素間の余白をうんたらpxとります。

#### Horizontal Layout

Horizontal Layoutは、目次を使わずナビゲーションバーを固定して配置するウェブブラウザやテキストエディタなどのデザインに最適です。

Horizontal Layoutは、Navigation (ナビゲーション)とContents (内容)の、2つの要素によって構成されています。

```
+++++++++++++++++++++++++++++++++
+          Navigation           +
+++++++++++++++++++++++++++++++++
+                               +
+                               +
+                               +
+           Contents            +
+                               +
+                               +
+                               +
+++++++++++++++++++++++++++++++++
```
Navigationは、内側の余白を8px、子要素間の間隔を8pxとります。

Contentsでは、内側の余白を8px、子要素間の余白を8pxとります。

他の要素は、「ベース（Bases）」、「コンポーネント（Components）」を元に実装してください。



## UI部品 / Components

基本的にこの部品を組み合わせて配置することになります。

### ボタン

ボタンは押下されるものに対してのみ使用します。


通常状態
第一色

ホバー状態

無効状態


背景はbbbbbb1e(強調色2)、枠線はa1a1a1(境界線)、影はbfbfbf55(影)に指定してください。ダークモードの場合も同じように、強調色2、境界線、影、としてください。

### 入力欄

### チェックボックス

### ラジオボタン



---

## 終わりに

Elementalの仕様書は以上です。

不明な点などがある場合、私たちにご連絡ください。

ウェブサイト: https://thinking-grp.github.io/project/elemental/

## バージョン履歴

v.1.0.0 thinking元代表Sorakimeが初版を公開。monochrome Project.のMonontなど、UIデザインの基礎となる。

v.1.1.0 *正式公開時に記入*

## ライセンス
Copyright 2021―2025 thinking All rights reserved.
