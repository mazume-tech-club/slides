# slides

mazume-tech-club の勉強会スライド集です。資料はテーマごとに1ディレクトリの静的 HTML で、ビルドしません。

## 資料一覧

| 資料 | パス | 内容 |
| --- | --- | --- |
| DOMと仮想DOMを体系的に理解する | [dom-virtual-dom/](dom-virtual-dom/) | DOMの木、レンダリングパイプライン、仮想DOMの差分と key、ミニ実装、Svelte / Solid / Vue Vapor との比較 |

公開時の想定URLは <https://mazume-tech-club.github.io/slides/dom-virtual-dom/> です。一覧は <https://mazume-tech-club.github.io/slides/> です。

### DOMと仮想DOMを体系的に理解する

対象は、フロントエンドを触ったことはあるが DOM / 仮想DOMを体系的には追っていない人です。

1. DOMとは（パース、ノード、API、イベント）
2. レンダリングパイプライン（レイアウトスラッシングまで）
3. 素のDOM操作の課題
4. 仮想DOM、key、O(n) のヒューリスティック
5. ミニ仮想DOM（`h`、初回描画、diff / patch）と、key の有無を見比べるデモ
6. 「仮想DOMは速い」が正確でない理由
7. Svelte、Solid、Vue Vapor との比較

スライド内のボタンはページ内のデモです。矢印キーでスライドを進めます。

## ローカルで見る

```bash
python3 -m http.server 4173
```

- 一覧: <http://127.0.0.1:4173/>
- 資料: <http://127.0.0.1:4173/dom-virtual-dom/>

reveal.js とフォントは CDN から読むので、閲覧中はネットワークが要ります。

## 新しい資料を追加する

1. `your-topic/index.html` を作る。ディレクトリ名が GitHub Pages のパスになる。英小文字とハイフンだけにする。
2. 下の骨組みをコピーし、`section` を足す。`assets/theme.css` を使うと既存資料と見た目が揃う。
3. ルートの `index.html` の「資料」にカードを足す。
4. この README の表に1行足す。
5. `main` にマージする。GitHub Actions が静的ファイルを Pages に出す。ワークフローは `.git` と `.github` 以外を配信するので、新しいディレクトリをワークフローへ登録し直す必要はない。

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>タイトル — mazume-tech-club</title>
    <link rel="icon" href="../assets/favicon.svg" type="image/svg+xml" />
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@6.0.2/dist/reveal.css" />
    <link rel="stylesheet" href="../assets/theme.css" />
  </head>
  <body class="deck">
    <div class="reveal">
      <div class="slides">
        <section>
          <h1>タイトル</h1>
        </section>
      </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/reveal.js@6.0.2/dist/reveal.js"></script>
    <script>
      Reveal.initialize({ hash: true, hashOneBasedIndex: true, slideNumber: "c/t" });
    </script>
  </body>
</html>
```

コードを載せる資料は、reveal.js の highlight プラグイン（同じバージョンの `dist/plugin/highlight.js`）を足すとシンタックスハイライトが付く。

## 公開

`.github/workflows/pages.yml` が `main` への push と手動実行で、リポジトリの静的ファイルを GitHub Pages にデプロイする。

Pages の公開元は GitHub Actions にする。この設定はリポジトリの Settings → Pages で行う。ワークフローファイルだけではサイトは有効にならない。
