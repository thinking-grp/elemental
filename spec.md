# Elemental v2 仕様書

Elemental v2は、主にカスタムエレメント（Web Components）を活用した、軽量で一貫性のあるデザインを提供するUIコンポーネントライブラリです。

---
[assets/Elemental-v1.pdf](https://github.com/thinking-grp/elemental/blob/main/assets/Elemental-v1.pdf)

## 1. 導入方法

### 1.1 必要なリソース
以下の外部フォントおよび最低限のスタイルシートを `<head>` 内で読み込む必要があります。

```html
<link rel="preconnect" href="[https://fonts.googleapis.com](https://fonts.googleapis.com)">
<link rel="preconnect" href="[https://fonts.gstatic.com](https://fonts.gstatic.com)" crossorigin>
<link href="[https://fonts.googleapis.com/css2?family=Barlow:wght@100..900&family=Noto+Sans+JP:wght@100..900&display=swap](https://fonts.googleapis.com/css2?family=Barlow:wght@100..900&family=Noto+Sans+JP:wght@100..900&display=swap)" rel="stylesheet">

<link href="styles/color.css" rel="stylesheet">
<link href="styles/main.css" rel="stylesheet">

```

---

## 2. コンポーネント詳細

### 2.1 ボタン `<elm2-button>`

標準的なアクション用ボタンです。

| 属性 | 説明 |
| --- | --- |
| `primary` | 強調表示（プライマリカラー）。 |
| `big` | ボタンサイズを大きくします。 |
| `disabled` | ボタンを無効化します。 |
| `carousel` | カルーセル内アイテムとして使用する場合に付与します。 |

#### **サンプルコード**

```html
<elm2-button primary>Primaryボタン</elm2-button>
<elm2-button>通常ボタン</elm2-button>
<elm2-button disabled>無効化</elm2-button>

<elm2-button big primary>Primaryボタン</elm2-button>
<elm2-button big>Bigボタン</elm2-button>

```

---

### 2.2 カルーセル `<elm2-carousel>`

横スクロール可能なコンテンツコンテナです。内部には主に `elm2-button` を配置します。

| 属性 | 説明 |
| --- | --- |
| `scale-effect` | スクロールアイテムに拡大エフェクトを適用します。 |
| `image` | 画像表示モード。内部ボタンの `--src-url` 変数から画像を読み込みます。 |

#### **サンプルコード**

```html
<elm2-carousel scale-effect>
    <elm2-button carousel>アイテム1</elm2-button>
    <elm2-button carousel>アイテム2</elm2-button>
</elm2-carousel>

<elm2-carousel image scale-effect>
    <elm2-button carousel style="--src-url:url(image1.png);"></elm2-button>
    <elm2-button carousel style="--src-url:url(image2.png);"></elm2-button>
</elm2-carousel>

```

---

### 2.3 テキスト入力 `<elm2-input>`

カスタマイズされたテキスト入力フィールドです。

#### **仕様**

* タグ内のテキストは自動的に `placeholder` として処理されます。
* `autocomplete="off"` が自動的に適用されます。

#### **サンプルコード**

```html
<elm2-input id="search">何か入力してください...</elm2-input>
<elm2-input id="search" disabled>入力は不可能です...</elm2-input>

```

---

### 2.4 リスト `<elm2-list-ul>`, `<elm2-list-li>`

構造化されたリストを表示します。

#### **サンプルコード**

```html
<elm2-list-ul>
    <elm2-list-li>リスト項目1</elm2-list-li>
    <elm2-list-li>
        技術発展<br>
        <small>2024年10月10日に獲得</small>
    </elm2-list-li>
</elm2-list-ul>

```

---

### 2.5 スナックバー表示 `snackbar` 属性

ボタンクリック時に画面下部に通知を表示します。

| 属性 | 説明 |
| --- | --- |
| `snackbar` | 表示するメッセージを指定。 |
| `bg` | スナックバーの背景色（CSS変数名または色コード）。 |

#### **サンプルコード**

```html
<elm2-button snackbar="こんにちは！">デフォルト</elm2-button>
<elm2-button snackbar="青い通知です" bg="--elm2-blue-50">青色通知</elm2-button>

```

---

### 2.6 スイッチ `<elm2-switch>`

トグル形式のスイッチです。

#### **サンプルコード**

```html
<elm2-switch id="setting1" name="notifications" checked></elm2-switch>

```

---

### 2.7 確率・バトル `<elm2-battle>`

2つの値の比率をプログレスバーのように表示します。

| 属性 | 説明 |
| --- | --- |
| `value` | カンマ区切りで2つの数値を入力（例: `"160,80"`）。 |
| `text` | 数値の後ろに表示するラベル文字列。 |

#### **サンプルコード**

```html
<elm2-battle value="160,80" text="人の投票"></elm2-battle>

```

---

## 3. JavaScript API

### `Elm2Snackbar.show(message, duration, bgColor)`

プログラムから直接スナックバーを表示します。

* `message` (string): 表示内容
* `duration` (number): 表示時間（ミリ秒）
* `bgColor` (string): 背景色

---

## 4. 技術的留意点

* **ブラウザ互換性**: `corner-shape: super-ellipse` をサポートしていないブラウザでは、自動的に代替のスタイル（角丸）が適用されます。
* **動的生成**: JavaScriptによって、カスタムタグ内部に適切なHTML構造（`button` や `input` 等）が自動生成されます。
仕様書の中には書いていなかったんですが、ボタンのデザインについてここで述べておきます。
ボタンは、以下の画像のような設計になっています。
背景は`#bbbbbb1e`(強調色2)、枠線は`#a1a1a1`(境界線)、影は`#bfbfbf55`(影)に指定してください。ダークモードの場合も同じように、強調色2、境界線、影、としてください。

![](https://raw.githubusercontent.com/Sorakime/Sorakime.github.io/7290967327ff7b7c08d3ef19d3a3f6662411503d/mncr/project/elemental/button.jpg)
