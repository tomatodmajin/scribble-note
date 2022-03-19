# difference between Azure Private Link and Service Endpoint

|Azure Private Link<br>Private Endpoint|-|Service Endpoint|
|---|---|---|
|Datalake以外同左、他にもたくさん|対応リソース|Azure Storage<br>Azure SQL<br>Azure Synapse Analytics<br>Azure KeyVault<br>Azure Cosmos DB<br>Azure Event Hub<br>Azure Service Bus<br>Azure Data Lake Storage V1|
|Private Endpointが従量|料金|無料|
|閉域(MSバックボーン)|接続|Internet|
|プライベートIP|割り当てられるIP|パブリックIP<br>※後ろのリソースのパブリックIPはオフにする|
|OK|AADテナント超えできるか|NG<br>※**Azure StorageとAzure Kye VaultならOK**<br>※VNet,サブスクリプション超えできる|
|NATする機器を置く|両端でIPレンジが被った場合|NOTHING to do|

## Private Link

* N Private Endpoints/Private Link
* 1 Private Link/Private Endpoints
* リージョン障害時は別リージョンにPEを立てればok
    * **std SKUのLB&バックエンドのリソースが同じVNetにいる必要あり**
    * max 8 Links/LB

## Service Endpoint

* 

## common

* 同一VNet内に複数Endpointを置ける
* 専用Subnetが不要
* リージョン超えが可能
    * Service Endpointは、Storage&SQLの組み合わせだとリージョン超えできない
