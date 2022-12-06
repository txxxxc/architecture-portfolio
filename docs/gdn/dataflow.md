# データフロー

1. GitHub Discussions で質問が作られる
2. GitHub Actions が起動して Firebase Functions をトリガーする
3. Slack に通知が行く


## Firebase FunctionsのURLをSecretで管理するのめんどい

Firebase Functions の URL を Secret から読んでるけど環境構築の容易性を確保するために、もっと別の方法でやりたい。

### Secretでやっていた理由
- 実装的にエンドポイントにリクエストできてしまったら Slack の通知飛ばせまくりだったので

### 解決案
- サーバーの URL は普通に公開する&discussion の id が含まれる workspace が無かったら何もしないという仕様にする