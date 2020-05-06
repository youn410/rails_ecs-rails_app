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
$ docker-compose run web rails new . --force --database=mysql --skip-bundles
```
`src/config/database.yml` を環境変数から設定値を読み込めるように修正し、イメージをビルド
```
$ docker-compose build
```
イメージが作成されている
```
$ docker images
REPOSITORY                                                        TAG                 IMAGE ID            CREATED             SIZE
rails_app_web                                                     latest              f7f3af0a7fef        41 seconds ago      1.04GB
```
rails webコンテナを起動
```
$ docker-compose up -d
```
dbコンテナ(run rails newの時生成された)とwebコンテナが起動
```
 docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                               NAMES
38726bffdfab        rails_app_web       "rails s -p 3000 -b …"   6 seconds ago       Up 5 seconds        0.0.0.0:3000->3000/tcp              rails_web
c6d18acd5535        mysql:5.7           "docker-entrypoint.s…"   16 minutes ago      Up 16 minutes       0.0.0.0:3306->3306/tcp, 33060/tcp   rails_mysql
```
databaseを作成する
```
$ docker-compose run --rm web rails db:create
Starting rails_mysql ... done
Created database 'app_development'
Created database 'app_test
```
ブラウザで`http://localhost:3000/`にアクセスすると「Yay! You’re on Rails!」ページが表示されている