# I’m Not Dead Yet! The Role of the Operating System in a Kernel-Bypass Era
- カーネルバイパスの出現とデータセンターでの多用によってOSが必要なくなるのでは
  ないかという予想がある
- しかしカーネルバイパスによってOSの抽象化が排除されるためデバイスをアプリケー
  ションが統一的に扱えるインタフェースがない

- Demikernel: カーネルバイパスのため新しいlibOSアーキテクチャ
    - カーネルバイパスのためのデバイスに依存しないI/Oの抽象化を提供
- Demikernel Architecture
    - 汎用OSの機能を二つに分ける
        - *control path operations*(kernel)
            - I/O毎に行われない(頻繁に呼ばれない)処理
            - 仮想化されたカーネルバイパスアクセサレーターのアプリケーションへ
              の割り当て, ネットワークの確立, ファイルの作成など
        - *data path operations*(libOS)
            - I/Oほハンドルするすべての処理
            - ストレージの読み書き, ネットワーク処理など
            - I/O毎に実行される為CPUバウンドな処理やperf-criticalな処理
        - libOSとしてカーネルバイパスアクセサレーターとのインタフェースを実装

