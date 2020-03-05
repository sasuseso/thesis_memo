# Virtual Gang based Scheduling of Real-Time Tasks on Multicore Platform

## Gang Schedulingとは
並列システムにおけるスケジューリングアルゴリズムの１つ。Ousterhout Matrixが基底にある。Ousterhout Matrixでは行をtime slice列をプロセッサとして表現される。ジョブは１つの行として表現される。Context Switchをジョブ間で調整する。

## Abstract
virtual-gangの概念をベースとした並列計算スケジューリングアルゴリズムの提案。virtual-gangとは互いにgang-scheduledかつ静的にリンクされた並列リアルタイムタスクの集合。  
ギャング内での同期的フレームワークと強力なtemporal isorationをhigh real-time schedulability を提供するvirtual-gang間でのフォーメーションアルゴリズムの提案

- one-gang-at-a-time
  - 優先度が高いタスクが来るとすべてのコアがプリエンプトされる

### virtual-gang
- 複数のタスクをまとめてgang-schedulingする
- 始点が同じタスクをまとめてgang-schedulingさせる
- 始点が揃わないと最初より悪くなることもある
- virtual-gang内のスケジューリングも考える(gang-formation problem)
