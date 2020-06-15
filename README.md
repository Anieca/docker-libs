# docker-libs

個人用に Dockerfile をまとめたリポジトリ.

- ubuntu
  - Ubuntu 18.04 + Python の環境

## build

Docker Image の作成.

`docker-compose.yml` の記述を変更して以下を実施.

```
docker-compose build
```

## run

Docker Container の起動.

```
docker-compose [-p <project_name>] up -d
```

## remove

起動している Docker Container の削除.

```
docker-compose [-p <project_name>] down
```
