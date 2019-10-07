# docker-for-mysql

Docker + MySQL で開発環境用 DB の作成

## docker-compose ビルド

```
# /docker/localhost ディレクトリに移動して
$ docker-compose build --no-cache
```

## docker-compose 起動

```
$ docker-compose up -d
```

## コンテナ接続

```
$ docker ps

CONTAINER ID  IMAGE  COMMAND  CREATED STATUS  PORTS NAMES
000000000000  docker_mysql_mysql "docker-entrypoint.s…" 39 seconds ago  Up 44 seconds 3306/tcp  docker_mysql_mysql_1

#コンテナに接続
$ docker exec -it 000000000000 bash

#コンテナ内のMySQLに接続
root@000000000000:/# mysql -u root -p

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sample_db          |
| sys                |
+--------------------+
5 rows in set (0.01 sec)

mysql> use sample_db;

mysql> show tables;
+---------------------+
| Tables_in_sample_db |
+---------------------+
| users               |
+---------------------+
1 row in set (0.00 sec)
```

## docker-compose シャットダウン

```
$ docker-compose down
```

## ディレクトリ構成

```
├─ mysql
│  ├─ Dockerfile (Dockerイメージやポートの設定)
│  ├─ db
│  │  └─ init.sql (DBの初期値データとして実行するSQL)
│  ├─ data/ (永続的ファイル一式))
│  └─ my.cnf (MySQLの設定)
├─ docker-compose.yml (Dockerの起動設定)
└─ README.md
```
