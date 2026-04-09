# AWS Networking Study

AWSのネットワーク基礎（VPC/Subnet/IGW/RouteTable）を構築し、インフラの構造を理解するためのリポジトリ。

## 1. ネットワーク構成図
graph TD
    subnet[Public Subnet] -- Route Table --> igw(Internet Gateway)
    igw -- Internet --> User

## 2. 構築ログ
### ステップ1：VPCの作成
- **CIDR:** 10.0.0.0/16
- **名前:** my-first-vpc
- **メモ:** 仮想ネットワークの土台を作成。

### ステップ2：パブリックサブネットの作成
- **CIDR:** 10.0.1.0/24
- **名前:** public-subnet-1
- **AZ:** ap-northeast-1a
- **メモ:** VPCを小分けにした区画。

### ステップ3：インターネットゲートウェイ (IGW) の作成
- **名前:** my-igw
- **状態:** Attached (my-first-vpcへアタッチ済み)
- **メモ:** これをVPCにアタッチしないと外と通信できない。

### ステップ4：ルートテーブルの設定
- **名前:** public-rt
- **設定内容:** 0.0.0.0/0 -> my-igw
- **サブネットの関連付け:** public-subnet-1
- **メモ:** サブネットからインターネットへの出口を定義。

### ステップ5：セキュリティグループ (Security Group) の作成
- **名前:** my-web-sg
- **インバウンドルール:** - **タイプ:** SSH (22)
  - **ソース:** マイIP (自分の接続環境のみ)
- **メモ:** サーバーを守る門番を配置。自分のIPからのみSSHを許可。
