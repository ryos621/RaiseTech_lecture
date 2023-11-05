# 第4回課題
## 1.VPCの作成
![VPC](img/vpc.png)

## 2.EC2とRDSの構築
### EC2
![EC2](img/ap.png)

#### サブネット（パブリックサブネット）
![ap_subnet](img/ap_publicsubnet_route.png)

#### セキュリティグループ
- インバウンド
  ![sg_ap_inbound](img/sg_ap_inbound.png)

- アウトバウンド
  ![sg_ap_outbound](img/sg_ap_outbound.png)

### RDS
![RDS](img/db.png)
#### サブネット（プライベートサブネット）
![db_subnet1](img/db_privatesubnet_1_route.png)
![db_subnet2](img/db_privatesubnet_2_route.png)

#### セキュリティグループ
- インバウンド
  ![sg_db_inbound](img/sg_db_inbound.png)

- アウトバウンド
  ![sg_db_outbound](img/sg_db_outbound.png)

## 3.EC2→RDSへの疎通確認
### EC2 Instance Connectより、RDS上のMySQLにログイン
![EC2toRDS](img/EC2toRDS.png)