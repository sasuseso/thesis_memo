# MIT Exokernel
**why legacy architecture inefficient**
- no advantages of domain-specific optimizations  

## 特徴
- exokernelはアプリケーションレベルのlow-level resource managementを実現する
- アプリケーションプログラマは一般的に抽象化された資源の代わりに専門化された抽象化を自分で作れる
- exokernelはハードウェア資源を安全にmultiplexする
- libOSはExokernelの最上位にあってkernelの情報にアクセスできる  

**Exokernel Principles**
- Exokernelの目的は効率的なリソースコントロールをuntrustedなアプリケーションにsecureに与えるマルチユーザシステム
- resource managementを避け必要な保護だけする(allocation, revocation, ownership)

- exokernelはセキュアにハードウェアをexportする
  - secureなバインドを使えばアプリケーションはセキュアにハードウェアをバインド・イベントハンドルできる
  - 明示的なリソース解放を用いることでアプリケーションリソース解放プロトコルに参加できる
  - abort protocolをを使って非協力なアプリケーションを強制的に中止できる

- exokernelはlibOSに互いから保護された上で最大限に自由なresource managementを実現する
- １つのlibOSのエラーが他のものに影響を与えてはいけない  
  - リソースのownershipを追跡
  - すべてのリソースもしくはbinding pointsを監視し，アクセスを取り消す(revoke accsess)ことによって保護(protection)を保証

- *secure binding*はauthorizationをリソースの利用から切り離す保護機構  

**Multiplexing the CPU**
- Xokではprocessは*enviroment*
  - accounting information
  - ページテーブル
  - 特定のイベント発生時に実行するコード(upcalls)
  - custom data(libOSの作者による)
- traditional OSのように例外によって通知される
- 普通にラウンドロビン法によってスケジュールされmultiplexされる

**Multiplexing Main Memory**
- 単純にlibOSがメモリをallocateするとXokはownerとpermissionをチェックしlibOSが互いに干渉しないようにアクセスを制限する
- exokernelがpage fault(どんな種類でも)を受け取るとlibOSに通達しlibOS上のハンドラに処理が行く

**Multiplexing the Stable Storage**
- XNとかゆうやつを使っとる
- ↑はbuffer cache registryとかfree mapを含んだdisk構造体をlibOSにexportする
- libOSは1つ以上のLibFSをもつ（同じファイルを違う用途で使うのに複数のLibFSが使える）
- exokernelはLibFSに不正なアクセスが発生しない限りファイル管理以上の操作を提供する
- Xok/ExOSのデフォルトのLibFSはC-FFSとかゆーやつ
- C-FFSはXNの機能をコードをダウロードしてきて拡張
  - exokernelの機能をつかってinodeをディレクトリに挿入
  - 関連するファイルを近くに配置

## Advantages
- kernel内の構造体にアクセスできるのはアプリケーション自身のリソース管理を行う上で非常に強力
- exokernelはハードウェア資源へのアクセスを調停しているので従来のOSのような保護ポリシーも強制することができる
- アプリケーションはCPUを得た(取り上げられた)ときに通知されるので以前はkernelしかできなかったスケジューリングに依存した操作ができる
- ライブラリはOS kernelをより開発が楽
- libOSのバグはExokernel全体に影響しない

## Disadvantages
- 設計が複雑
- 保護ポリシーによるパフォーマンスの低下との兼ね合い
- resource-managementタスクにアプリケーションレベルでの情報不足
  - libOSがVirtual MemoryをhandleしたあとにはもうXokはどのpageがblock cacheかvirtual memoryか分からない

