# 第5回課題
## 課題で学ぶこと
### 1.EC2を利用した、アプリ動作環境構築
### 2.ELB(ALB)を利用した、アプリ動作環境の冗長化
### 3.S3サービスの活用
### 4.AWS構成図の作成

## 1-1.組み込みサーバアプリ(Puma)単体でのアプリ動作環境構築
### ・Pumaの設定
#### /var/www/raisetech-live8-sample-app/config/puma.rb
![puma_config](img/puma_config.png)
### (1)bin/devでアプリケーション実行後、サーバのIPアドレス:3000(Pumaで利用しているポート番号)にアクセスし、アプリが動作していることを確認
![bin/dev](img/bin_dev.png)
![puma_web](img/puma_web.png)

## 1-2.Webサーバアプリ(Nginx)とAPサーバアプリ(Unicorn)に分割した環境でのアプ動作環境構築
### ・Nginxの設定
#### /etc/nginx/nginx.conf
![nginx_config](img/nginx_config.png)
### ・Unicornの設定
#### /var/www/raisetech-live8-sample-app/config/unicorn.rb
![unicorn_config](img/unicorn_config.png)
### (1)Nginxの起動
![nginx_boot](img/nginx_boot.png)
### (2)Unicornの起動
![unicorn_boot](img/unicorn_boot.png)
### (3)サーバのIPアドレス:81(Nginxで利用しているポート番号)にアクセスし、アプリが動作していることを確認
![nginx_web](img/nginx_web.png)

## 2.ELB(ALB)を利用した、アプリ動作環境の冗長化
### ・冗長化のためのサーバの作成
#### 1-2で作成した環境(Nginx-Unicorn-lecture05)をもとに、冗長化のためのサーバ(Nginx-Unicorn-lecture05-2)を作成
![ami](img/ami.png)
### ・ターゲットグループの作成
#### 2つのサーバをターゲットグループに指定
![tg](img/tg.png)
### ・ロードバランサー(ALB)の作成
#### 作成したターゲットグループを設定したロードバランサーを作成
![lb](img/lb.png)
### ・動作確認のために、アプリTOPページの文言を変更
#### サーバ1(Nginx-Unicorn-lecture05)
##### /var/www/raisetech-live8-sample-app/app/views/fruits/index.html.slim
![server1_top](img/server1_top.png)
#### サーバ2(Nginx-Unicorn-lecture05-2)
##### /var/www/raisetech-live8-sample-app/app/views/fruits/index.html.slim
![server2_top](img/server2_top.png)
### (1)ロードバランサーのDNS名:81(Nginxで利用しているポート番号)にアクセスし、アプリが動作していることを確認
![elb_web](img/elb_web.png)
### (2)現在アクセスしているサーバを停止し、ページを更新することで、冗長化されていることを確認
![server1_stop](img/server1_stop.png)
![elb_web2](img/elb_web2.png)
## 3.S3サービスの活用
### 1〜2で作成したアプリの環境において、画像投稿時のファイルの保存先を、サーバ内→S3に変更する。
### ・S3バケットの作成
![s3bucket](img/s3bucket.png)
### ・ストレージの設定を変更
#### /var/www/raisetech-live8-sample-app/config/environments/development.rb
![localtos3](img/localtos3.png)
#### /var/www/raisetech-live8-sample-app/config/storage.yml
![storage](img/storage.png)
#### 環境変数(/home/ec2-user/.bashrc)
![bashrc](img/bashrc.png)
### (1)アプリ上で画像を投稿
#### 保存前
![post_before](img/post_before.png)
#### 保存後
![post_after](img/post_after.png)

#### 保存後のS3バケット内のオブジェクト
![s3bucket_2](img/s3bucket_2.png)

## 4.AWS構成図の作成
### 1~3で作成したアプリ動作環境のAWS構成図を作成
![lecture05](img/lecture05.png)