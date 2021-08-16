## EC2の初期状態に対して実行しRailsの環境構築まで完了させるPlayBook


## roles
### init
- yum update
- gitのインストール
- bash_profileテンプレートの配置

### js
- nodejsのインストール
- yarnのインストール

### mysql
- mysql-clientのインストール

### nginx
- nginxのインストール

### ruby
- rbenvのインストール
- ruby-buildのインストール
- rubyのインストール

### rails
- railsのインストール
- bundlerのインストール
- プロジェクトのpull
- bundle install --path vendor/bundle
- nginxの再起動
- unicoenの起動

```

instaled_rails
├── README.md
├── hosts
├── roles
│   ├── init
│   │   ├── tasks
│   │   ├── templates
│   │   └── vars
│   ├── js
│   │   ├── tasks
│   │   ├── templates
│   │   └── vars
│   ├── mysql
│   │   ├── tasks
│   │   ├── templates
│   │   └── vars
│   ├── nginx
│   │   ├── tasks
│   │   ├── templates
│   │   └── vars
│   ├── rails
│   │   ├── tasks
│   │   ├── templates
│   │   └── vars
│   └── ruby
│       ├── tasks
│       ├── templates
│       └── vars
└── site.yml

```