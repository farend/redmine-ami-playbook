# Redmine Ver.3.3 AMIの作り方

**AWS上で公開している Farend-Redmine AMI の構成情報を明らかにするために公開しております。**

## インスタンス作成

AWSコンソール等にてAmazon Linuxのmicroインスタンスを作成する。

## OSを最新状態にする（この内容のみインスタンスで実行）

* 一度インスタンスにログインし、 `sudo yum -y update` を実施する。
* 再起動する。

## 使用インスタンスの特定

* `hosts.sample` を `hosts` として複製する。

### hosts

* ホストのIPアドレスを設定する。
* `ansible_ssh_private_key_file` を正規のファイルパスにする。

## バージョン及び設定等の定義

* `group_vars/redmine.sample` を `groups_vars/redmine` として複製する。

### redmine

* `mysql_root_password` に **MySQLのrootのパスワード** を設定する。
* `redmine_db_pass` に **db_redmineデータベースのuser_redmineアカウントのパスワード** を設定する。
* `ruby_major` に **rubyのメジャーバージョン（小数点1位まで）** を設定する。
* `ruby_version` に **rubyのバージョンのruby_major以外** を設定する。

## インストール実行

**`ansible-playbook -i hosts main.yml`** で実行

## Redmine設定

*<u>Ansibleの実行が終わったら</u>*、Redmineにadminでログインし、デフォルトのテーマを **farend_basic** に変更。

## 操作ログ等の削除

インスタンスにログインし、下記を実行。

```
$ export HISTSIZE=0
$ history -c
$ sudo su -
# cd
# sh delete.sh
# rm delete.sh
# export HISTSIZE=0
# history -c
```

## イメージ作成

ログなどが削除されたか確認し、この状態でAMIを作成
