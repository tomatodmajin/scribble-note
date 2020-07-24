# equivalent-objectstorage_AWS-vs-Azure

* なんとなく並べなおしてみた。
* が、Azureの場合は各ストレージサービス（機能）の上位に「ストレージアカウント」という概念がいるイメージ。
    * ストレージアカウント > Blob（オブジェクトストレージ）, File, Table, Queue
    * ストレージアカウントの種類 <https://docs.microsoft.com/ja-jp/azure/storage/common/storage-account-overview#types-of-storage-accounts>
    * が、「特に理由がなければ汎用v2を使え」という圧がすごい

|detail|suitable storage-class name(AWS)|min. storage days|suitable storage-class name(Azure)|spec|
|---|---|---|---|---|
|高アクセス|S3 Standard|-|Blob-ホット層|-|
|長期保存・低アクセス|S3 Standard-IA|30days|Blob-クール層|30days|
|長期保存・不定アクセス|S3 Intelligent-Tiering|30days|-|-|
|長期保存・低アクセス・低重要|S3 1Zone-IA|30days|-|-|
|長期保存・数分-数時間で取り出し|S3 Glacier|90days|Blob-アーカイブ層(rehydrate:high)|180days|
|低アクセス・12hで取り出し|Blob-アーカイブ層(rehydrate:standard)|180days|

* 参考
    * AWS <https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/dev/storage-class-intro.html>
    * Azure <https://docs.microsoft.com/ja-jp/azure/storage/blobs/storage-blob-storage-tiers?tabs=azure-portal#comparing-block-blob-storage-options>
    * Azure-blob archive <https://docs.microsoft.com/ja-jp/azure/storage/blobs/storage-blob-rehydration?tabs=azure-portal>
* Blob-アーカイブ層の「rehydrate:high/standard」をGlacierのequivalentとして書いてみたが、単純equivalentではない感ある。
* Blob-PremiumパフォーマンスのAWS equivalentが無さそうな