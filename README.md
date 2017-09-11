# Ansible+Vagrantでローカル開発環境

## 構成

* CentOS 7.2
* Nginx *
* PHP(FPM) 7.1.5
* MySQL 5.6.*

## 使い方

### 基本
```
$ git clone git@github.com:egapool/centos72-ansible.git
$ cd centos72-ansible
$ vagrant up
```

### 環境によって調整
CentOS7.2のboxが予めローカルにある場合は`config.vm.box`にそのboxの名前を記載
```
config.vm.box = "your-name-of-centos7.2"
```

ソースのディレクトリ対して相対パスを変更
```
config.vm.synced_folder "./public_html", "/var/www/html"
↓
config.vm.synced_folder "./your/source/dirctory", "/var/www/html"
```
