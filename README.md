# ジェットコースター・エネルギーラボ

ジェットコースターを走らせて、**運動エネルギー K・位置エネルギー U・熱など T の入れかわり**を棒グラフで確かめる、高校物理基礎「力学的エネルギー」のシミュレーションです。単一のHTMLファイルで動きます。画面右上のボタンで**日本語／English**と**ライト／ダーク**を切り替えられます。

*English: see [below](#english).*

👉 **[https://coaster.meetupsensei.com/](https://coaster.meetupsensei.com/)**

---

## つくった理由

力学的エネルギー保存は「mgh = ½mv²」の式で覚えて終わりになりがちですが、実際には

- 高いところの U が、下りで K に入れかわる
- 摩擦や空気抵抗があると K+U は減る。でも減った分は熱 T になっていて、**K+U+T はいつも一定**
- だからコースターはスタートより高い丘を越えられないし、ループの頂上では「止まらない」だけでなく「ある速さ」が必要

というように、**エネルギーの行き先を追いかけると、コースターの動きがすべて説明できます**。走らせる前に予想し、走らせて棒グラフで確かめる、をくり返すことで、生徒が自分で気づく形を目指しました。

---

## 6つの区間

画面上部の路線図から区間を選びます。各区間にクイズがついていて、「この条件をセットする」ボタンで問題の条件をそのまま再現できます。

| 区間 | 内容 |
|------|------|
| 1. エネルギーの基本 | 高さ・質量・摩擦の有無を変えて、U が K に入れかわる様子を見る。v = √(2gh) が質量によらないことも確かめる |
| 2. 丘を越えられる？ | 2つめの丘の高さ（スタートに対する％）を変えて、越えられる限界を探す |
| 3. 摩擦のちがい | 氷・雪・芝生の坂を比べる。ハーフパイプで往復させ、届く高さが下がっていく様子を見る |
| 4. ループに挑戦 | ループの半径と位置を変えて、落ちずに一回転できる一番大きなループを探す |
| 5. 計算チャレンジ | 4つの地点の K・U・K+U・T を計算して入力し、答え合わせする（入力値は棒グラフに反映） |
| 6. オリジナル設計 | 丘・ループなどのパーツを組み合わせ、条件（敷地の幅・落下しない・ブレーキゾーンで止まる）を満たしながらスリルポイントを競う |

画面の右側には、K・U・K+U・T の棒グラフと、時間変化のグラフが常に表示されます。

---

## 授業での使いどころ

- **導入**：区間1で「高さが速さに変わる」を見せ、K と U の棒が入れかわるところで止めて問いかける
- **予想→実験**：区間2・4のクイズは「予想してから走らせる」形式。班ごとに予想を出させてから一斉に走らせる
- **計算演習**：区間5で、教科書の問題と同じ形の計算を自分で確かめる
- **探究・まとめ**：区間6で設計コンテスト。うまくいかない原因をエネルギーの言葉で説明させる
- **自習**：生徒が自分のスマホ・iPadから開いて触る（ログイン不要。進み具合はブラウザに保存されます）

---

## 技術的なこと

- HTML・CSS・JavaScript の単一ファイル。ビルド不要、フレームワーク不要
- 外部依存は Google Fonts のみ（読み込めない環境でもシステムフォントで動作します）
- レールに沿った1次元の運動方程式を細かい時間刻みで解き、摩擦（一定の大きさ）と空気抵抗（速さの2乗に比例）で失われたエネルギーを T として積算しています
- ループでは垂直抗力が負になった時点でレールから離れ、放物運動で落下します
- 日本語／英語の切り替えに対応（選んだ言語はブラウザに保存されます）。区間の説明・クイズ・解説・結果メッセージまで英語になります
- ライト／ダークの両方に対応（OSの設定に従い、右上のボタンで切り替えも可能）
- 区間のデータはコード内の `STAGES` 配列、英語の文言は `EN_STAGES`（区間ごと）と `UI.en`（画面の文言）にまとまっています

### 区間やクイズを足す・直す

クイズは `STAGES` の各区間の `quiz` に1行ずつ書かれています。

```js
{q:'速さが2倍になると、運動エネルギーは何倍になる？',
 o:['2倍','4倍','変わらない','½倍'],  // 選択肢
 a:1,                                  // 正解の番号（0から数える）
 e:'K は v² に比例するので…',          // 解説
 preset:{mu:0}}                        // 任意：「この条件をセットする」で設定する値
```

英語版にも表示するときは、`EN_STAGES` の同じ区間・同じ位置に `q` / `o` / `e`（必要なら `hint`）を書きます。**選択肢 `o` は日本語と同じ順番・同じ数**にしてください（正解は番号 `a` で共有しています）。

---

## 公開の手順

1. このリポジトリの `index.html` をそのまま使う
2. Settings → Pages → Source を「Deploy from a branch」、Branch を `main` / `(root)` に設定
3. 1〜2分で `https://<ユーザー名>.github.io/<リポジトリ名>/` が開きます

---

## ライセンス

[MIT License](LICENSE)

授業でそのまま使う、自校向けにクイズを足す、コードを参考に別のシミュレーションをつくる、といった利用を自由にどうぞ。コードをコピー・改変して配布・公開するときは、著作権表示とライセンス文（`LICENSE`）を残してください。公開中のページをそのまま授業で使うだけなら、手続きは不要です。

## つくった人

のざたん

---

## English

**Roller Coaster Energy Lab** is a single-file web app for high school physics. Run a roller coaster and watch kinetic energy K, potential energy U and heat T trade places on a live bar chart.

👉 **[https://coaster.meetupsensei.com/](https://coaster.meetupsensei.com/)**: switch to English with the button at the top right. Light and dark themes are supported.

Six sections, each with a short quiz whose conditions can be loaded into the simulation with one tap:

- **Energy basics**: change the height, mass and friction, and see U turn into K. The speed at the bottom does not depend on mass.
- **Over the hill?**: find the tallest second hill the coaster can clear. It can never go higher than the start.
- **Friction**: compare ice, snow and grass, and watch a sled lose height on each pass of a half-pipe.
- **Loop challenge**: find the biggest loop it can get around without falling off at the top.
- **Calculation challenge**: calculate K, U, K+U and T at four points and check your answers.
- **Your own design**: combine hills and loops into a safe, thrilling coaster that stops in the brake zone.

No build step, no framework, no login. Released under the [MIT License](LICENSE). Made by Nozatan ([meetupsensei.com](https://meetupsensei.com)).
