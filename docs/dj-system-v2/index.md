# DJ System v2

DJ System v2 のアーキテクチャです。

## 使用するフレームワーク

このアプリケーションでは主に以下の技術をベースに構築します。
- Nuxt3
- TypeScript

## 目的

今回のアーキテクチャを構築する際に意識した部分は以下です。
- 出来るだけ Nuxt3 の標準 API を活かす
- 型安全に API を叩く
- アプリの規模がそんな大きくないので複雑さを回避して開発スピードを上げる

## 全体像

特筆すべきディレクトリだけピックアップしています。
```
src/
├─ components
├─ composables
├─ layouts
├─ middleware
├─ pages
├─ plugins
├─ utils

// 独自に生やしたディレクトリ
├─ features // ドメインに紐づく部分をまとめる。
├─ libs // ライブラリに依存する部分を隠蔽する。
├─ schemas // スキーマを保存する。zodiosで自動生成する。
```

## 標準で提供されているディレクトリ

Nuxt3 によってデフォルトで提供されているディレクトリとその役割です。

### components

このディレクトリには以下のようなコンポーネントを格納する
- ページで横断して利用されるライブラリ
- ドメインに紐付かないライブラリ
	- footer, header など
今回は UI ライブラリとして Vuetify を使用するので基本的にはあまり使わない予定。

[components/ · Nuxt Directory Structure](https://nuxt.com/docs/guide/directory-structure/components)

### composables

このディレクトリには以下のようなモジュールを格納する
- ドメインに紐付かないロジック
	- useRouter を使ったページ遷移のロジック
- 共通で使われるロジック
	- cookie の取得
- libs にあるモジュールをアクセスするモジュール
	- API Client の初期化
[composables/ · Nuxt Directory Structure](https://nuxt.com/docs/guide/directory-structure/composables)

### layouts

ページの枠組みとなるレイアウトを格納します。
[layouts/ · Nuxt Directory Structure](https://nuxt.com/docs/guide/directory-structure/layouts)

### middleware

画面遷移時に発動するルーティング処理を記述するミドルウェアを格納します。
[middleware/ · Nuxt Directory Structure](https://nuxt.com/docs/guide/directory-structure/middleware)

### pages

ページを格納します。
[pages/ · Nuxt Directory Structure](https://nuxt.com/docs/guide/directory-structure/pages)

### plugins

アプリケーションの初期化時に起動するプラグインを格納します。
[plugins/ · Nuxt Directory Structure](https://nuxt.com/docs/guide/directory-structure/plugins)

### utils

便利関数を生やします。
例：スネークケースをキャメルケースに変換するなど
[utils/ · Nuxt Directory Structure](https://nuxt.com/docs/guide/directory-structure/utils)

## 独自に生やしたディレクトリ

独自に生やしたディレクトリその理由です。

### libs

外部ライブラリに依存するモジュールをラップして隠蔽するディレクトリです。
例としては以下です。
- ofetch をラップした API Client
- Sentry

### features

ドメインと紐づくロジックを格納するディレクトリです。
このディレクトリに関しては [featuresディレクトリ](./features.md) を参照してください。

### schemas

[zodios](https://github.com/astahmer/openapi-zod-client) によって自動生成される部分。

## Q&A

## 使用するライブラリ

使用するライブラリとその理由です。

### Vuetify

管理画面側の UI フレームワークとして [Vuetify](https://vuetifyjs.com/en/) を利用しています。
今回のアプリケーションは大きく分けて、管理画面とユーザーが触る画面の 2 つの画面があります。

管理画面の目的は一般的で見やすい UI でアプリケーションの関わる情報を整理することです。
Vuetify を使うことの利点として以下の 2 点が挙げられます。

- インストールするだけでシンプルで分かりやすい UI を表現できる。
- 複雑な UI のロジックが用意されているので工数を大幅に削減できる。

管理画面の目的と Vuetify の利点がマッチしていると考え今回は Vuetify を採用しました。

### Zod

Zod は TypeScript バリデーションライブラリです。
フォームのバリデーションやその他にも方のついていないオブジェクトを型安全に扱えるということで採用しました。
あとで紹介する Zodios に依存ライブラリです。

### Zodios

Zodios は Zod を使ったスキーマ定義を使って型安全な API クライアントです。
Zodios を使うことによって型安全で快適に API 通信周りのコードを書けるので採用しました。

## その他規約

細かいコーディング規約は [こちら](./coding-rules.md)
