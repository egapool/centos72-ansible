# Ansible+Vagrantでローカル開発環境

## 構成

* CentOS 7.2
* Nginx 1.12.1
* PHP(FPM) 7.1.5
* MySQL 5.6.37

## 使い方

### 基本
```
// すでに同様のCentOS7.2のboxがある場合は不要
$ vagrant box add centos72 https://github.com/CommanderK5/packer-centos-template/releases/download/0.7.2/vagrant-centos-7.2.box

$ git clone git@github.com:egapool/centos72-ansible.git
$ cd centos72-ansible

// Vagrantfileを環境に合わせて変更 （下記参照
$ vi Vagrantfile

$ vagrant up
```

### 環境によって調整
#### Vagrantfile
CentOS7.2のboxが予めローカルにある場合は`config.vm.box`にそのboxの名前を記載
```
config.vm.box = "your-name-of-centos7.2"
```

ローカルのIPは任意です
```
config.vm.network :private_network, ip: "192.168.44.38"
```

ソースのディレクトリ対して相対パスを変更
```
config.vm.synced_folder "./public_html", "/var/www/html"
↓
config.vm.synced_folder "./your/source/dirctory", "/var/www/html"
```

#### playbook/site.yml
local.example.jp -> 任意のドメインに変更

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
