# ECS container training


- 実行
```s
root/db/$ docker-compose up

root/$ docker-compose up
```
http://localhost:80



- 構成図
```s
$ tree
.                          # App contaienr create -> docker-compose up (--build)
├── .cercleci                     
│   └── config.yml
├── dev
│   ├── app
│   │    ├── _rails        # Mount data
│   │    ├── Dockerfile
│   │    ├── gemrc
│   │    ├── web
│   │    │   ├── app.conf
│   │    │   └── nginx.conf
│   │    └── supervisor
│   │         └── app.conf
│   ├── db                  # DB  container create -> docker-compose up (--build)
│   │    ├── _mysql         # Mount data
│   │    └── docker-compose.yml
│   └── docker-compose.yml
├── dev.sh
├── stg
│   └── app
│       ├── Dockerfile
│       ├── gemrc
│       ├── web
│       │   ├── app.conf
│       │   └── nginx.conf
│       └── supervisor
│           └── app.conf
└── stg.sh
```

