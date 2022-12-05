# featuresディレクトリ
要するにドメインモデルをベースにディレクトリを切り分ける方法です。
[bulletproof-react](https://github.com/alan2207/bulletproof-react) のディレクトリ構成を参考にしています。

## ドメインとは
ドメインに関してはこちらを参考に↓
- [ドメインモデルとは(「現場で役立つシステム設計の原則」より) - Qiita](https://qiita.com/jimpei/items/93671b4b09407f9d4111)
- [ドメイン駆動設計における「良いモデル」と「悪いモデル」とは - ログミーTech](https://logmi.jp/tech/articles/322831)

(**厳密に言うと違うけど**、ざっくりいうとデータベースのテーブル単位で分けられたオブジェクトくらいの認識で良いです。)

## ディレクトリ構成
``
```
src/
├─ features/
│  ├─ domain name/
│  │  ├─ api/
│  │  ├─ components/
│  │  ├─ domain/
│  │  ├─ schema/
│  │  ├─ validation/
│  │  ├─ index.ts
├─ schemas/ // zodiosで自動生成される場所
│  ├─ index.ts
```

## api
ドメインに紐づく api 通信するモジュールを格納する

## validation
バリデーションロジックを書く

## schema
schemas から該当する schema を取得する

## components
ドメインに紐づくコンポーネント。
schema を props に受け取る UI を格納する。

## domain
schema の値を引数に受け取り任意の処理をするドメインロジックを書く場所

例：User の firstName と lastName が API のレスポンスから返ってきてそれを fullName として出力したい

## index.ts
各 feature のエントリポイント。
feature 下のモジュールをまとめて export する。(Barrel パターンと呼ばれれてるやつ→[参考](https://basarat.gitbook.io/typescript/main-1/barrel))
