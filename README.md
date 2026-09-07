# AR ありがとうカード

カメラをかざすと、目印になっている絵の上にキャラクターが浮かび上がり、「ありがとな〜」の吹き出しが出るWeb ARコンテンツです。専用アプリのインストールは不要で、スマホのブラウザ（Safari / Chrome）だけで動きます。

使用ライブラリ: [MindAR](https://hiukim.github.io/mind-ar-js-doc/) (画像認識AR) + [A-Frame](https://aframe.io/)

## フォルダ構成

```
index.html            ← ARページ本体（リポジトリ直下。このままGitHub Pagesで公開できます）
assets/
  target-image.png    ← 目印（マーカー）にする元画像
  character.png       ← 浮かび上がらせるキャラクター（背景を透過済み）
  targets.mind        ← ★マーカー認識用データ（下記手順で作成が必要）
```

## 1. マーカーファイル（targets.mind）について

`assets/targets.mind` は作成済みで、このリポジトリに含まれています。

マーカー画像（`assets/target-image.png`）を差し替えたときだけ、作り直しが必要です。その場合は [MindAR Image Target Compiler](https://hiukim.github.io/mind-ar-js-doc/tools/compile/) を開き、「Choose File」で新しい `assets/target-image.png` をアップロード →「Start」→ 完了したら「Download」で `targets.mind` を取得し、`assets/targets.mind` を上書きしてpushしてください。

> 補足: 今回のキャラクターイラストは色の塗りつぶしが多く、写真に比べると認識の「目印」になる特徴点が少なめです。屋外や明るい場所で、印刷した絵にまっすぐ近づける・遠すぎない距離（15〜30cm目安）で試すと安定します。もし認識が不安定な場合は、絵の周りに柄や模様のある台紙・フレームを足すと精度が上がります。

## 2. GitHubにアップロードする

まだGitHubリポジトリを作っていない場合:

1. https://github.com/new で新しいリポジトリを作成（例: `ar-arigatou-card`）。Public / Privateどちらでも可（GitHub Pagesを使う場合、Privateだと有料プラン以外では公開ページが使えないためPublic推奨）
2. パソコンのターミナル（またはClaude Code）で、このプロジェクトフォルダに移動して以下を実行:

```bash
git init
git add .
git commit -m "ARありがとうカードを追加"
git branch -M main
git remote add origin https://github.com/【あなたのユーザー名】/ar-arigatou-card.git
git push -u origin main
```

(すでにリポジトリがある場合は `git remote add origin ...` の部分だけ、そのリポジトリのURLに置き換えてください)

## 3. GitHub Pagesで公開する

1. GitHub上のリポジトリページで `Settings` → `Pages` を開く
2. 「Build and deployment」の `Source` を `Deploy from a branch` にする
3. `Branch` を `main`、フォルダを `/(root)` に設定して `Save`
4. 数分待つと `https://ibekari.github.io/IBERI-AR/` のようなURLが発行されます

このURLをQRコードにして印刷し、目印の絵と並べて設置すると、当日はお客様がスマホでQRを読み取ってカメラをかざすだけで体験できます。

## 4. 当日の使い方

1. 発行されたURLをスマホのブラウザで開く（QRコード経由が便利）
2. 「カメラをはじめる」をタップ → カメラの使用を許可
3. 目印の絵（`target-image.png` を印刷したもの）にカメラをゆっくり近づける
4. 絵の上にキャラクターが浮かび上がり、「ありがとな〜」の吹き出しが表示される

## カスタマイズしたい場合

- 吹き出しの文言: `index.html` 内の `buildBubbleTexture("ありがとな〜")` の文字列を変更
- 吹き出しの色: 同じ関数内の `#fff7ec`（背景色）・`#c2793a`（枠線）・`#a85a25`（文字色）を変更
- 浮き上がる高さやスピード: `showContent()` 内の `duration`（ミリ秒）や `-0.25 + e * 0.25` の数値を調整
- マーカー画像やキャラクター画像を差し替える場合は、`assets/target-image.png` と `assets/character.png` を入れ替えたうえで、targets.mind を作り直してください（画像を変えたら再生成が必須です）
