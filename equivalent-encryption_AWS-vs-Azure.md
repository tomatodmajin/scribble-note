# equivalent-encryption_AWS-vs-Azure

|what encrypt_lv.1|what encrypt_lv.2|function name(AWS)|detail|function name(Azure)|detail|
|---|---|---|---|---|---|
|data in transit||-|AWSリソースとの通信をSSL/TLSでやる|||
|||Site-to-Site VPN||||
|||Direct Connect||||
|data in rest|storage|SSE-S3|データの上げ先で暗号化 with S3のキー <https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/dev/UsingServerSideEncryption.html>|||
|||SSE-KMS|データの上げ先で暗号化 with KMSのキー <https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/dev/UsingKMSEncryption.html>|||
|||SSE-C|データの上げ先で暗号化 with 独自キー <https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/dev/ServerSideEncryptionCustomerKeys.html>|||
|||CSE-KMS|データの送信前に暗号化 with KMS <https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/dev/UsingClientSideEncryption.html>|||
|data in rest|storage|S3/EBS暗号化|with KMS-CMK <https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/EBSEncryption.html>|Storage Service Encryption|with Key Vault-CMK,etc. <https://docs.microsoft.com/ja-jp/azure/storage/common/storage-service-encryption#about-encryption-key-management>|
|||||Blob-client side encryption|with Key Vault-CEK,etc. <https://docs.microsoft.com/ja-jp/azure/storage/blobs/storage-encrypt-decrypt-blobs-key-vault>|
|||||Disk Encryption-SSE|with Key Vault-CMK <https://docs.microsoft.com/ja-jp/azure/virtual-machines/windows/disk-encryption#about-encryption-key-management>|
||DBinstance|RDS/Transparent Data Encryption (TDE)|RDSで独自に証明書を生成、暗号化 <https://docs.aws.amazon.com/ja_jp/AmazonRDS/latest/UserGuide/Appendix.SQLServer.Options.TDE.html>|Transparent Data Encryption (TDE)|with Key Vault or BYOK <https://docs.microsoft.com/ja-jp/azure/azure-sql/database/transparent-data-encryption-tde-overview?tabs=azure-portal>
||DBinstance|RDS/ [Enable encryption]|with KMS <https://docs.aws.amazon.com/ja_jp/AmazonRDS/latest/UserGuide/Overview.Encryption.html#Overview.Encryption.Enabling>|||
||DBdata|Dynamo/AWS所有のCMK|暗号化with Dynamo独自のキー <https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/encryption.howitworks.html>|||
||DBdata|Dynamo・DocumentDB・Aurora・Redshift/AWS管理のCMK|暗号化with KMS-CMK <https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/encryption.howitworks.html> <https://docs.aws.amazon.com/ja_jp/documentdb/latest/developerguide/encryption-at-rest.html> <https://docs.aws.amazon.com/ja_jp/AmazonRDS/latest/AuroraUserGuide/Overview.Encryption.html#Overview.Encryption.Enabling> <https://docs.aws.amazon.com/ja_jp/redshift/latest/mgmt/working-with-db-encryption.html#working-with-aws-kms>|||
||DBdata|Dynamo・ElastiCache/カスタマー管理のCMK|暗号化with 独自キー <https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/encryption.howitworks.html> <https://docs.aws.amazon.com/ja_jp/AmazonElastiCache/latest/red-ug/at-rest-encryption.html#using-customer-managed-keys-for-elasticache-security>|||
||DBdata|Redshift/CloudHSM Classic|暗号化with ハードウェアセキュリティモジュール <https://docs.aws.amazon.com/ja_jp/redshift/latest/mgmt/working-with-db-encryption.html#working-with-HSM>|||
||key|KMS|xx|Key Vault|xx|

* 「セキュリティ」でドキュメント1セクション作れるのすごい <https://docs.aws.amazon.com/ja_jp/security/?id=docs_gateway>
    * たぶんこれも参考になりそう <https://d0.awsstatic.com/whitepapers/Security/AWS_Security_Whitepaper.pdf>
* S3の暗号化おまけ　：デフォルト暗号化 <https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/dev/bucket-encryption.html>
* 転送時の暗号化をいろいろ書ききってない
* compute/storage/DB以外のサービスデータの暗号化については省略　：結局KMS使う話