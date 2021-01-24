# equivalent vmtype AWS vs Azure

色々ありすぎてよく分からないので並べてみる。（2021/1/24時点）

* 参考
    * AWS
        * <https://aws.amazon.com/jp/ec2/instance-types/>
        * <https://pages.awscloud.com/rs/112-TZM-766/images/C2-07.pdf>
    * Azure
        * <https://docs.microsoft.com/ja-jp/azure/virtual-machines/sizes?toc=https%3A%2F%2Fdocs.microsoft.com%2Fja-jp%2Fazure%2Fvirtual-machine-scale-sets%2Ftoc.json&bc=https%3A%2F%2Fdocs.microsoft.com%2Fja-jp%2Fazure%2Fbread%2Ftoc.json>
* 共通
    * AWS
        * *.metal = AWS Nitro System上に構築されるベアメタルインスタンス
        * EC2インスタンスストア + 物理ホスト = EC2インスタンス
            * インスタンスストアは一時領域としての利用が推奨

|AWS|EC2インスタンスタイプ名|概要|Azure|VMタイプ名|概要|
|-|-|-|-|-|-|
|汎用|mac1<br>t4g<br>t3<br>t3a<br>t2<br>m6g<br>m5a<br>m5n<br>m5zn<br>m4<br>a1|・万能<br>・ex. `ウェブサーバーやコードリポジトリなど、インスタンスのリソースを同じ割合で使用するアプリケーション`<br>・CPU性能の安定　：t ＜ m<br>・t　：バースト可能パフォーマンスインスタンス（cf. CPUクレジット）<br>・a　：AWS Gravitonプロセッサ（64-bit Arm arch：安いやつ）|汎用|B<br>Dsv3<br>Dv3<br>Dasv4<br>Dav4<br>DSv2、Dv2、Av2、DC、DCv2、Dv4、Dsv4<br>Ddv4<br>Ddsv4|ex. `テストと開発、小～中規模のデータベース、および低～中程度のトラフィックの Web サーバー`|
|コンピューティング最適化|c6g<br>c6gn<br>c5<br>c5a<br>c5n<br>c4|・処理性能で押していくワークロード<br>・ex. `バッチ処理ワークロード、メディアトランスコード、高性能ウェブサーバー、ハイパフォーマンスウェブサーバー、ハイパフォーマンスコンピューティング (HPC)、科学モデリング、専用ゲームサーバーおよび広告サーバーエンジン、機械学習推論などのコンピューティング集約型アプリケーション`|コンピューティングの最適化|F<br>Fs<br>Fsv2|・こっちに書いたけどほぼm<br>・ex. `トラフィックが中程度の Web サーバー、ネットワーク アプライアンス、バッチ処理、アプリケーション サーバー`|
|高速コンピューティング（アクセラレーテッド）|p4<br>p3<br>p2<br>inf1<br>g4dn<br>g4ad<br>g3<br>f1|・↑のバカでかい利用バージョン<br>・GPU/FPGA有<br>・ex. `浮動小数点計算、グラフィックス処理、データパターン照合などの機能`|GPU|NC<br>NCv2<br>NCv3<br>NCasT4_v3 (プレビュー)<br>ND<br>NDv2 (プレビュー)<br>NV<br>NVv3<br>NVv4|・GPU有<br>・ex. `負荷の高いグラフィックスのレンダリングやビデオ編集、ディープ ラーニングを使用したモデル トレーニングと推論 (ND) `|
||||ハイ パフォーマンス コンピューティング|HB<br>HBv2<br>HC<br>H|・vCPUやらなんやらとにかくデカい|
|メモリ最適化|r6g<br>r5<br>r5a<br>r5b<br>r5n<br>r4<br>x1e<br>x1<br>u-*tb1<br>z1d|・メモリがたくさん必要なワークロード<br>・EBS帯域幅多め|メモリの最適化|Esv3<br>Ev3<br>Easv4<br>Eav4<br>Ev4<br>Esv4<br>Edv4<br>Edsv4<br>Mv2<br>M<br>DSv2<br>Dv2|ex. `リレーショナル データベース サーバー、中～大規模のキャッシュ、およびメモリ内分析`|
|ストレージ最適化|i3<br>i3en<br>d2<br>d3<br>d3en<br>h1|・読み書きが多いワークロード<br>・ローカルストレージが他タイプより大きい|ストレージの最適化|Lsv2|ex. `ビッグ データ、SQL、NoSQL データベース、データ ウェアハウス、および大規模なトランザクション データベース`|
