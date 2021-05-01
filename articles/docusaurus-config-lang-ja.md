---
title: "Docusaurus v2 を日本語化"
emoji: "🦕"
type: "tech"
topics: ["docusaurus"]
published: true
---

:::message
Docusaurus 2.0.0-alpha.75 で確認しています。
:::

[多言語対応で記事を作成し、ヘッダーから言語選択する UI も標準で用意されている Docusaurus](https://docusaurus.io/docs/i18n/introduction) ですが、セットアップした状態（多言語対応化していない状態）では英語 `lang="en"` がデフォルトの言語となっています。

```html
<!DOCTYPE html>
<html lang="en" data-theme="light" dir="ltr" data-react-helmet="lang,dir">
```

日本語のみで利用したい場合は、以下のように **多言語対応設定を追加しつつ、`ja` のみを利用する** 形にします。

```js:docusaurus.config.js
module.exports = {
  i18n: {
    defaultLocale: 'ja',
    locales: ['ja'],
    localeConfigs: {
      ja: {
        label: '日本語',
        direction: 'ltr',
      },
    },
  },
};
```

参考: [docs/docusaurus.config.js#i18n](https://docusaurus.io/docs/docusaurus.config.js#i18n)

`localeConfigs` は今回利用されないため、省略可能です。

これで、出力される HTML の `lang` 属性が `ja` になります。

```html
<!DOCTYPE html>
<html lang="ja" data-theme="light" dir="ltr" data-react-helmet="lang,dir">
```

コンテンツ本体も、デフォルトの `docs`, `blog` などのディレクトリの中身を単純に日本語で作成します。

もちろん日本語以外でも、デフォルトにしたい言語が１つで良い場合はこの方法で対応可能です。
