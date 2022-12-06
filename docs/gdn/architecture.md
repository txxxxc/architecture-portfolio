# アーキテクチャ

モジュラーモノリスみたいな感じでやっていきたい。

- src
  - handler
  - constants
  - svc
    - workspace
      - domain
      - posts
        - members
        - overview
        - integration
      - usecase
      - repository
    - slack
      - domain
        - message
      - usecase
      - repository
  - lib
    - slack
    - firestore
    - setupTest(vitest のセットアップ)
    - firebase fucntion test
