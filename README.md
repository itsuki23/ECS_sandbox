# ECS container training
- 20200819　予想構成図
```s
$ tree
.                          # App contaienr create -> docker-compose up -d --build
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
│   ├── db                  # DB  container create -> docker-compose up -d --build
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

