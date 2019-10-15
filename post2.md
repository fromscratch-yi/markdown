## はじめに
<div class="section_inner">

`Firebase` 、 `Contentful` というサービスと、 `Nuxt.js` という技術を使ってこのポートフォリオ兼ブログサイトを作成しました。
これらのサービス・技術の概要と、個人的なメリット・デメリットをまとめたいと思います。
</div>

## <a class="refer" href="https://firebase.google.com/?hl=ja" target="_blank" rel="noopener">Firebaseとは？</a>
<div class="section_inner">
<p class="img_wrap"><img src="//images.ctfassets.net/eebw0y2sorkq/5eYNXBz3UMPu1oeXQil07p/9b8e6c7b960094ea555975c171fef6d0/firebase.jpg" alt="firebase"></p>

GCP(Google Cloud Pratform)の一部で、高品質のアプリを素早く開発できるよう用意されたプラットフォームです。
Real Time DatabaseやFunctions, Hostingなどの開発に必要な機能が数多く用意されております。
今回はHostingというサービスを使用して、このサイトを公開しています。

<div class="memo">
<p class="memo_ttl"><a class="refer decoration" href="https://firebase.google.com/docs/hosting/" target="_blank" rel="noopener">Firebase Hosting</a></p>
<p class="memo_desc">Firebase Hosting は、ウェブアプリ、静的コンテンツ、動的コンテンツ向けの高速で安全性の高いホスティングを提供します。<br>また、デフォルトでSSLが組み込まれるため、証明書の取得なしにhttpsの通信となります！</p>
</div>

### メリット

- 今どきの技術に触れられる。
- サーバサイドの知識なしにWebページを公開でき、簡単なアプリくらいなら作れる。
- コマンド一つで簡単にデプロイ（本番公開）できる。
- 証明書の取得などなしにSSL対応（https通信）してくれる。
- 無料でもそこそこ使える。

### デメリット

- 新しく覚えないといけないこともある。（私の場合、NodeやNuxt.js、Vue.js）
- Nodeの環境のみっぽい？
- FunctionsでのNodeのバージョンはFirebase次第（今現在はNode.js 8.14.0）
- Nuxt.jsのアプリでSSR（サーバサイドレンダリング）対応した際にいろいろ大変。
</div>

## <a class="refer" href="https://www.contentful.com/" target="_blank" rel="noopener">Contentfulとは？</a>
<div class="section_inner">
<p class="img_wrap"><img src="//images.ctfassets.net/eebw0y2sorkq/1vh9td29835MtJ8lgyeIRO/437b2b60dc9b5197fdcfb98cdb47b987/contentful.jpg" alt="contentful"></p>

ContentfulはヘッダレスCMSや、APIベースCMSなどと言われています。
今までCMSといわれると、WordPressをイメージする人も多いかと思います。
しかし、ContentfulはAPIベースのため、WordPressのようにフロントとバックエンドが密結合せず、分離されており、フロントの自由度も高まります。

### メリット

- 今どきのサービスに触れられる。
- APIベースで取得できるため、見た目（CSS）部分のカスタマイズは自由。
- アプリ側と別管理となるため、モバイルアプリやその他サービスからから参照したい場合も容易。

### デメリット

- <a class="refer decoration" href="https://firebase.google.com/docs/functions/get-started" target="_blank" rel="noopener">FirebaseでSSRしようとしたときに無料プランではサードパーティのAPIはうまく叩けない。</a>
- 記事取得、検索、次の記事へボタンなどの実装が必要。
</div>

## <a class="refer" href="https://ja.nuxtjs.org/" target="_blank" rel="noopener">Nuxt.jsとは？</a>
<div class="section_inner">
<p class="img_wrap"><img src="//images.ctfassets.net/eebw0y2sorkq/4ydos3mBHF4Yqfv47DlRNb/b728c397fc7dab2ab3615ef7e91a4510/nuxt.jpg" alt="nuxtjs"></p>

まず、クライアントサイドjavascriptのフレームワークである<a class="refer decoration" href="https://jp.vuejs.org/v2/guide/index.html" target="_blank" rel="noopener">Vue.js</a>があります。
Vue.jsはSPA（Single Page Application）のWebアプリを容易に実装することが可能です。

しかし、SPAは一つのページの中で、遷移先のページなども取得するため、ページ遷移やアプリの動きが軽快でUXは向上しますが、致命的なデメリットとして初期ロード（初期表示）が遅い、SEOに向いていないという欠点があります。
その問題を解決するために、SSR（サーバサイドレンダリング）という技術があり、SSRを用いたVue.jsアプリケーションを簡単に作成するためのフレームワークがNuxt.jsです。

### メリット

- SPAやSSRの技術に触れられる。
- WebアプリやWebサイトを簡単に作成できる。
- 高品質、高UXなWebアプリを作成できる。

### デメリット

- Nuxt.js + Vue.jsの学習コストが必要
</div>

## 最後に
<div class="section_inner">

今回はFirebase、Contentful、Nuxt.jsについて説明でした。
僕も今年に入ってからVue.js含め、初めて触れてみたものなので間違った解釈もあるかもですが、気になることがあれば、DMいただければと思います。
</div>