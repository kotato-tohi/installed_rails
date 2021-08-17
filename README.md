## EC2の初期状態に対して実行しRailsの環境構築まで完了させるPlayBook

## 実行方法

### hostsファイルの編集
対象ホストと、秘密鍵のパスを指定

```
[target]
<IP ADDR>

[target:vars]
ansible_ssh_port=22
ansible_ssh_user=ec2-user
ansible_ssh_private_key_file=<PRIVATE KEY PATH>

```

### 各種変数
デフォルトでは下記の通りになっているので必要であれば適宜変更してください。

/ruby/vars/main.yml
インストールするrubyのバージョン指定
```
__ruby_version: 3.0.2
e.g.)__ruby_version: 2.6.8
```

/mysql/vars/main.yml
mysqlのリポジトリなど

```
# MySQL version setting
__repo_url: https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
__mysql_version: 8.0
__mysql_new_repo: mysql80-community
__mysql_current_repo: mysql57-community

```

/js/vars/main.yml
nodejsのソース
version16以外の場合変更
```
__nodejs_source_url: https://rpm.nodesource.com/setup_16.x
```


### 実行コマンド

```
$ ansible-playbool -i hosts site.yml
```


## roles
### init
- リポジトリが最新である
- 必要な前提パッケージがインストール済みである
- bash_profileテンプレートが配置されている
- sshd_configの編集(タイムアウト防止)がされている

### js
- nodejsがインストールされている
- yarnがインストールされている

### mysql
- mysql-clientがインストールされている

### nginx
- ~~nginxがインストールされている~~
- rails環境構築では不要なので削除(プロジェクトデプロイのplaybookに追加)

### ruby
- rbenvがインストールされている
- ruby-buildがインストールされている
- 指定したバージョンのrubyがインストールされている


```

.
├── README.md
├── hosts
├── roles
│   ├── init
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── tasks
│   │   │   └── main.yml
│   │   ├── templates
│   │   └── vars
│   │       └── main.yml
│   ├── js
│   │   ├── tasks
│   │   │   └── main.yml
│   │   ├── templates
│   │   └── vars
│   │       └── main.yml
│   ├── mysql
│   │   ├── tasks
│   │   │   └── main.yml
│   │   ├── templates
│   │   └── vars
│   │       └── main.yml
│   ├── rails
│   │   ├── tasks
│   │   ├── templates
│   │   └── vars
│   └── ruby
│       ├── tasks
│       │   └── main.yml
│       ├── templates
│       │   └── 001_rbenv.sh
│       └── vars
│           └── main.yml
└── site.yml
