# A Secure and Formally Verified Linux KVMHypervisor

## Abstract

- 背景: ハイパーバイザーのコード多くね？これってセキュリティリスクってｺﾄ!?
- アプローチ: 形式手法を使おう！でもコードがデカい...
  - _microverification_: ハイパーバイザーを小さなコア部分と untrusted なサービ
    スの集合に分割し,コア部分の検証をすれば全体のセキュリティ特性を証明可能に
    する
  - security-preserving layers: 証明をモジュライズするために,複数のレイヤに分割しそれぞれを証明していく｡
  - data oracles: 動的に変化する情報を扱うハイパーバイザーのために意図的な部分を隠す

## 成果物

- KVM を改造して試した(変更は少ない)
- Coq を使って VM データの confidentiality, integrity を証明(perf や functionality も増えたよ)
- MicroV: デカいシステムのセキュリティ特性を証明
