# difference between Azure Private Link and Service Endpoint

|Azure Private Link<br>Private Endpoint|-|Service Endpoint|
|---|---|---|
|Datalake以外同左、他にもたくさん|対応リソース|Azure Storage<br>Azure SQL<br>Azure Synapse Analytics<br>Azure KeyVault<br>Azure Cosmos DB<br>Azure Event Hub<br>Azure Service Bus<br>Azure Data Lake Storage V1|
|Private Endpointが従量|料金|無料|
|OK（NATする前提）|ERやVPNGW超えの接続|NG<br>※NATとかFWルールに書いたりすればOK|
|OK|AADテナント超えできるか|NG<br>※**Azure StorageとAzure Kye VaultならOK**<br>※VNet,サブスクリプション超えできる|
|OK|リージョン超えできるか|NG|
|NATする機器を置く|両端でIPレンジが被った場合|NOTHING to do|

## Private Link

* N Private Endpoints/Private Link
* 1 Private Link/Private Endpoints
* リージョン障害時は別リージョンにPEを立てればok
    * **std SKUのLB&バックエンドのリソースが同じVNetにいる必要あり**
    * max 8 Links/LB
* inbound/outboundのルールは書かなくていいというか今は書けない。(preview) <https://docs.microsoft.com/ja-jp/azure/private-link/private-endpoint-overview#limitations>

## Service Endpoint

* 

## common

* 同一VNet内に複数Endpointを置ける
* 専用Subnetが不要
* Endpoint間は閉域接続（MSバックボーン）
