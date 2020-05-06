# rails + MySQLのDockerアプリケーション
## 新規にアプリケーションを作成する
初期ディレクトリ構成
```
$ tree
.
├── Dockerfile
├── README.md
├── docker-compose.yml
└── src
    ├── Gemfile
    └── Gemfile.lock
```
rails newを実行すると、src下にファイル群が生成される
```
$  docker-compose run web rails new . --force --database=mysql --skip-bundles
```