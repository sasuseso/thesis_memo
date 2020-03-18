# Glider: A GPU Library Driver for Improved System Security
- デバイスドライバはリソースの分配と管理を単独で行うため,TCBが大きくなり脆弱性
  の温床となる
- リソースの管理と分配を分けることで解決｡リソース管理を(untrustedな)アプリケー
  ションレベルにライブラリとして持ち込む｡
- Exokernelの*untrusted resource management*より着想
- isolationをカーネルで実現(*device kernel*)
- key benefits
    - application間のisolation
    - TCBがdriver kernelだけのため*small attack surface*
    - kernel空間とユーザー間でデータコピーが発生しない為高速
