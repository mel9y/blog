---
title: ブログとポートフォリオ
publish_date: 2023-03-03
---

やっとこさ重い腰を上げて放置していたポートフォリオとZennには書けない技術的じゃないことを書くブログを完成させました。めっちゃくちゃ Nextra とかで楽したけど。

せっかくなので、ブログの最初の記事はこのブログとポートフォリオのことを書こうと思います。

(ブログを作る理由にもなった [ぼっち・ざ・ろっく！](https://bocchi.rocks/) のことも別記事として書きます。まだ見てないならこんなブログ記事より、先に見てくれ　いいアニメだから...)

## ポートフォリオ

ポートフォリオは実は今までも作ってはいましたが、なんせフロントの知識がミジンコ以下なので不細工なものしか作れませんでした。

Next.js を勉強するために作るのもありだったんですが、先述の通りまた不細工ができてもすぐに消しそうなのでたまには楽しようということで、静的サイトジェネレーター [Nextra](https://nextra.site/) を使って作ることにしました。 (これなら Next.js 使ってるからギリセーフ)

この Nextra , Next.js の恩恵を受けながらドキュメントサイトやブログサイトを作ることができる優れもので、私が参加しているプロジェクトのドキュメントにも使っているものになります。

Nextra はブログとドキュメントでテーマが変わっていますが、 ブログテーマを見ていたらポートフォリオにしたときのイメージが湧いてきたので、そのままポートフォリオにしちゃいました。

ただ、 Next.js の恩恵を受けるには受けるんですが、私のような運用は Lighthouse の Performance を下げがちなので気をつけてください。(多分1ページにいろいろ詰めすぎているのが原因)

![Lighthouse が報告したレポート](https://pbs.twimg.com/media/FqS91QQaMAAXINO?format=jpg&name=medium)

### Nextra のすごいところ (抜粋)

#### Next.js の恩恵を受けることができる

Nextra は Vercel の社員が作っているライブラリで、 Next.js との連携が凄まじいです。

今まで静的サイトジェネレーターといと VuePress とかが選択肢に出てくると思いますが、 Next.js の恩恵が受けれるなら Nextra を選択肢に入れるのもいいくらいに体験がいいです。

#### リンクや画像が常に最適化

Nextra は Markdown (mdx) に書かれたリンクや画像を可能な限り Next.js Link や Next.js Image を使うよう自動変換してくれます。

VuePress たちが出来ない芸当ですよほんと

#### ダークモードのサポート

何もしなくてもダークモードがサポートされています。

#### i18n のサポート

i18n がサポートされています。これは VuePress とかもそうですが、 Nextra の i18n は非常に簡単に設定できるよう設計されています。

### 歌詞の引用

[とある方](https://yude.jp) のポートフォリオに歌詞が引用される機能があり、この機能を見てから自分もやりたいという強い感情に駆られ作りました。 Nextra でできた素朴なポートフォリオに花を添えてくれています。

![歌詞の引用](https://pbs.twimg.com/media/FqPNnEZaYAAJAAb?format=jpg&name=900x900)

この歌詞の情報は `public/assets/quotes.json` で記録していて、これをランダムに出しています。ページをリロードするたびに変わります。(あまりやると Cloudflare に怒られます)

```json
  {
    "lyrics": "君と集まって星座になれたら",
    "title": "星座になれたら",
    "artist": "結束バンド"
  },
  {
    "lyrics": "遥か彼方 僕らは出会ってしまった",
    "title": "星座になれたら",
    "artist": "結束バンド"
  },
  {
    "lyrics": "いいな 君は みんなから愛されて",
    "title": "星座になれたら",
    "artist": "結束バンド"
  },
  {
    "lyrics": "僕は何処へ向かえばいい?",
    "title": "なにが悪い",
    "artist": "結束バンド"
  },
  {
    "lyrics": "ぶちまけちゃおうか 星に",
    "title": "ギターと孤独と青い惑星",
    "artist": "結束バンド"
  },
```

## ブログ

今回から初めて作ったブログです。これも先述の理由により、楽してます。

Node.js に変わる新しい JavaScript / TypeScript のランタイム実行環境 Deno が提供している [deno_blog](https://github.com/denoland/deno_blog) で作成、デプロイは Deno Deploy を使っています。ちゃんと優良顧客になろうとしています。

これ、シンプルでありながら作成からデプロイまでとても簡単です。(裏を返せばあまりカスタマイズができません。Nextra のほうがいいかなぁとはなり始めています。)


### deno_blog の使い方

deno_blog は タイトル等共通する設定を `main.ts` 等に書き込み、それを `deno run` すると `posts` にあるマークダウンファイルから静的サイトを生成してくれます。

```js
import blog from "https://deno.land/x/blog@0.5.0/blog.tsx";

blog({
  title: "mel9y blog",
  author: "mel9y",
  avatar: "",
  avatarClass: "full",
  links: [
    { title: "WebSite", url: "https://mel9y.dev" },
    { title: "GitHub", url: "https://github.com/mel9y/blog" },
  ],
});
```

## 困ったこと

### 相変わらず Vercel と Cloudflare の相性が悪い

Vercel で指定したカスタムドメインを Cf のプロキシに通すとうまく開通しませんでした。

Vercel 側がドキュメントを公開してはいますが、何してもうまく行かん....

[How do I use a Cloudflare domain with Vercel? - Vercel Docs](https://vercel.com/guides/using-cloudflare-with-vercel)

プロキシを切って、DNSだけのルートにすればうまくいきます。マジでこれ難しすぎる。

ちなみに Deno Deploy もちょっと挙動怪しかったです。慣れてないときはやめておいたほうがよさそう

### 新しく取ったドメインは NextDNS の Allowlist に入れたほうがいい

新しく取ったドメインに対して設定次第ですが、 NextDNS はブロック対象にして堂々と弾いてきます。

これに気づかないと一生 `DNS_PROBE_FINISHED_NXDOMAIN` などで躓きます。私は躓きました。
