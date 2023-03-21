# equivalent_instance-storage_AWS-vs-Azure

なんとなく並べなおしてみた。

|workload|suitable service name(AWS)|spec|service name(Azure)|spec|
|---|---|---|---|---|
|高スループット・高IOPS（ミッションクリティカルな本番環境向け）|プロビジョンドIOPS SSD(io1,io2,io2Express)<br>※ExpressはI/Oが25.6万まで爆上がりする|4GB-16TB(Exは64TB),<br>64,000IOPS(Exは256,000)|Ultraディスク|4GB-70TB, 2GB/sec, 16KB I/O|
|低～中スループット・高IOPS, AWSさん的には「汎用：開発・テスト環境向け」|汎用SSD(gp2,gp3)|1GB-16TB,<br>16,000IOPS|Premium SSD|4GB-35TB, 900MB/sec, 20KB I/O
|高スループット・低IOPS|スループット最適化 HDD(st1)|125GB-16TB,<br>500IOPS|Standard SSD|4GB-35TB, 750MB/sec, 6MB I/O|
|バックアップ|Cold HDD(sc1)|536GB-16TB, 262MB/sec, 1MB I/O|Standard HDD|34GB-35TB, 500MB/sec, 2MB I/O|

※XiB→XBは小数点以下切り捨て

* 参考
    * AWS <https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/ebs-volume-types.html>
    * Azure <https://docs.microsoft.com/ja-jp/azure/virtual-machines/windows/disks-types#disk-comparison>
* 「スループット」と「IOPS」の関係性について <https://blog.ryukiy.net/2015/06/12/premium-storage-part2/>
* gp2とPremium SSDは単純equivalentではない気もする。。