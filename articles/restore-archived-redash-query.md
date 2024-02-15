---
title: "Redash でアーカイブしたクエリを元に戻す"
emoji: "🚯"
type: "tech"
topics: ["redash"]
publication_name: "socialplus"
published: true
---

Redash では UI 上からクエリのアーカイブが可能だが、アーカイブしたクエリを復元することはできません。  
アーカイブしたクエリを復元したい場合は Redash API を利用する必要があります。

- [Redash - Integrations and API](https://redash.io/help/user-guide/integrations-and-api/api)

API の実行に必要な API キーは２種類ありますが、どちらでも実行可能です。

- User API Key
- Query API Key

恒久的な自動化などで利用する場合は `Query API Key` を利用したほうがいいですが、以下のような curl コマンドでさっと実行するのであれば個人のアカウントごとに発行されている `User API Key` の利用で充分かと思います。

`User API Key` は Redash UI の［Settings］>［Account］のページにあります。

念のため、先にデータを確認しましょう。

```curl
curl -L -X GET "https://redash.example.com/api/queries/{Query ID}" \
 -H "Content-Type: application/json" \
 -H "Authorization: Key {API Key}"
```

`is_archived` というデータがあるので、その値を更新します。  
`true` がアーカイブ中で、`false` がアーカイブ解除です。


```curl
curl -L -X POST "https://redash.example.com/api/queries/{Query ID}" \
 -H "Content-Type: application/json" \
 -H "Authorization: Key {API Key}" \
 --data-raw '{
   "is_archived": false
 }'
```

API リクエストが正常に通ればアーカイブ状態が解除され、UI 上でも `Archived` マークが消えます。

アーカイブ状態が解除されたクエリは `Unpublished`（非公開）状態になっているので、必要に応じて UI 上から Publish などを行ってください。
