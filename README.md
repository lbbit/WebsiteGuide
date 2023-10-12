# WebDockerfile

基于`WebsiteGuide`项目，支持docker-compose + Dockerfile本地一键部署

## 部署方式

```bash
# 一键部署
docker-compose up -d

# 修改代码后重新部署
docker-compose up --build -d

```

## 数据和迁移

docker-compose文件中已经将系统数据挂载到volumes
```yml
    volumes:
     - website-db:/WebsiteGuide
     - website-media:/WebsiteGuide/websiteapp/media

volumes:
  website-db:  # 这是数据库文件的卷
  website-media:  # 这是media文件的卷
    driver: local
```
默认路径为：`/var/lib/docker/volumes/webdockerfile_website-db/_data`和`/var/lib/docker/volumes/webdockerfile_website-media/_data`

迁移步骤：
1. 新服务器下载最新代码使用`docker-compose up -d`启动
2. 将旧服务器`webdockerfile_website-db/_data/db.sqlite3`文件和`/var/lib/docker/volumes/webdockerfile_website-media/_data`目录所有文件复制到新服务器对应文件夹中
3. 重启容器