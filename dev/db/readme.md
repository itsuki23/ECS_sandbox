# MySQL

- 本番RDSの代わりなのでapp/webのcomposeには含めず構成

```
..
├── docker-compose.yml(app+web)
└── db
    ├── docker-compose.yml(db)
    ├── .env
    ├── mysqsl-data(mount用)
    └── .gitignore
```


- docker-compose.yml(db)
```sh
version: '3'
services:
  db:
    # --------------------
    #  Mysql 8.0
    # --------------------
    image: mysql:8.0
    # 8.0で認証プラグインが変わったので、mysql_native_passwordに戻す設定
    command: --default-authentication-plugin=mysql_native_password
    # --------------------
    #  Mysql 5.7
    # --------------------
    # image: mysql:5.7

    # restart: always
    # hostname: db-host
    # container_name: db-container

    environment:
      MYSQL_USER: root
      MYSQL_DATABASE: db_test
      TZ: "Asia/Tokyo"
      BIND-ADDRESS: 0.0.0.0
    env_file:
      - .env # MYSQL_PASSWORD=<password>

    ports:
      - "3306:3306" # localとも接続する際は、競合するので3306以外を使う
    volumes:
      - ./_mysql:/var/lib/mysql
      # 設定ファイル
      # - ./conf/my.cnf:/etc/my.cnf
      # 初期データを投入するSQLが格納されているdir
      # - ./db/mysql_init:/docker-entrypoint-initdb.d
    tty: true

    # 他のコンテナと接続するために以下を接続先にも追記
    networks:
      - test-network
networks:
    test-network:
        external: true
```


- .env
```
MYSQL_ROOT_PASSWORD=password
```


- docker-compose.yml(app+web)
```sh
version: "3"
services:
  app:
    ...
    networks:
      - test-network
  web:
    ...
networks:
    test-network:
        external: true
```

- 実行

```
# コンテナ間接続設定 (docker-composeは使わない場合)
$ docker network create test-network

# docker-compose.ymlにtest-networkの接続設定を追記

# コンテナ起動
$ docker-compose up -d --build

# 別コンテナから接続
$ mysql -u root -h db -p

# ホストOSから接続
$ mysql -u root -h localhost -P 3306 --protocol=tcp -p

# 外部のサーバーから接続
$ mysql -u root -h <hostname> -P 3306 --protocol=tcp -p
```

参考: https://qiita.com/Esfahan/items/70047ea2e4fecab4e2cc