# Ansible+Vagrantでローカル開発環境

## 構成

* CentOS 7.2
* Nginx 1.12.1
* PHP(FPM) 7.1.5
* MySQL 5.6.37

## 使い方

### 基本
```
$ git clone git@github.com:egapool/centos72-ansible.git
$ cd centos72-ansible

// Vagrantfileを環境に合わせて変更 （下記参照
$ vi Vagrantfile

$ vagrant up
```

### 環境によって調整
#### Vagrantfile
ローカルのIPは任意です
```
config.vm.network :private_network, ip: "192.168.44.38"
```

開発ソースのディレクトリ対して相対パスを変更
```
config.vm.synced_folder "./public_html", "/var/www/html"
↓
config.vm.synced_folder "./your/source/dirctory", "/var/www/html"
```

#### playbook/site.yml
local.example.jp -> 任意のドメインに変更
```
server_name: "local.example.jp"
↓
server_name: "[任意のドメイン]"
```

Vagrantfileのsynced_folderで指定した開発ソースがあるディレクトリに変更
```
root: "/var/www/html/example"
↓
root: "/var/www/html/[ローカルのソースがあるディレクトリ名]"
```

## 主な設定ファイルの場所
#### nginx
`/etc/nginx/nginx.conf`,`/etc/nginx/conf.d/*.conf`
#### php
`/usr/local/lib/php.ini`,`/usr/local/etc/php-fpm.conf`,`/usr/local/etc/php-fpm.d/*.conf`
#### mysql
`/etc/my.cnf`,`/root/.my.cnf`
