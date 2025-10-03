# Tap Next PWA

超シンプルな PWA です。画像を表示し、指定エリアのタップで **次の画像** に切り替わります。
- デフォルトでは左右半分どちらをタップしても「次へ」
- 長押しで「前へ」
- 画像リストは `index.html` の `IMAGES` 配列を編集してください
- 画像ごとに当たり判定を変えたい場合は `CUSTOM_HOTSPOTS` を使ってください

## ローカルで動かす（Service Worker要件のため http(s)で）
### Node.js を使う場合
```bash
npx serve .
# または
npx http-server -p 5173
```
→ 表示されたURL（http://localhost:5173 など）を iPhone の Safari で開く

### Python を使う場合
```bash
# Windows (Pythonインストール済み)
py -m http.server 5173
```
→ http://localhost:5173 を開く

## ホーム画面に追加（iPhone）
1. Safari で上のURLを開く
2. 共有ボタン → 「ホーム画面に追加」

## 画像の差し替え
- `images/` フォルダに画像を入れ、ファイル名を `index.html` の IMAGES 配列に記述
- 例:
```js
const IMAGES = ["./images/a.jpg", "./images/b.jpg", "./images/c.jpg"];
```

## 任意の座標にホットスポットを置きたい
`CUSTOM_HOTSPOTS` を使うと、画像インデックスごとに任意の矩形エリアを登録できます。
例（0枚目に2つのホットスポットを追加）:
```js
const CUSTOM_HOTSPOTS = {
  0: [
    { left: "10%", top: "10%", width: "30%", height: "30%", action: "next" },
    { left: "60%", top: "60%", width: "30%", height: "30%", action: "next" }
  ]
};
```
- `action` は `next` または `prev`
- 単位は `%` のほか `px` などCSSが使えます

## デプロイ（例）
- GitHub Pages, Cloudflare Pages, Netlify など **静的ホスティング** に `index.html` 等をアップロードするだけ
