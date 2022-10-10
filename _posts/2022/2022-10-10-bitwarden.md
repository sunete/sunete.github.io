---
title: "Bitwarden 安装教程"
categories:
  - tutorial
tags:
  - 教程
toc: true
toc_sticky: true
toc_label: ""
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---

## 一、安装 docker
```
wget -qO- https://get.docker.com/ | bash
```

## 二、安装 docker-compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

运行 `docker-compose --version` 以检查安装是否成功。

## 二、创建 docker-compose 配置文件
在 `/var/www/vaultwarden` 目录下创建 `docker-compose` 文件

```shell
vi /var/www/vaultwarden/docker-compose.yml
```
配置文件内容
```dockerfile
version: '3'
services:
  vaultwarden:
    image: vaultwarden/server:latest
    container_name: vaultwarden
    restart: always
    ports:
      - "3080:80"
      - "3012:3012"
    environment:
      DOMAIN: 'https://vw.231111.xyz/'
      SIGNUPS_ALLOWED: 'true'
      WEB_VAULT_ENABLED: 'true'
      WEBSOCKET_ENABLED: 'true'
    volumes:
      - ./data:/data
```
这里配置文件内开启了注册，在网站启动后先注册，之后修改配置文件为 `SIGNUPS_ALLOWED: 'true'` 关闭注册。
## 三、启动 Vaultwarden
在 `docker-compose.yml` 所在文件夹执行命令
```dockerfile
docker-compose  up -d
```
查看日志
```dockerfile
docker logs vaultwarden
```
## 四、创建 Nginx 配置文件
```shell
nano /etc/nginx/conf.d/vaultwarden.conf
```
Nginx 配置文件内容
​

注意修改域名、证书路径。**acme 申请的泛域名证书必须使用 fullchain.cer ，否则安卓客户端无法连接。**
```nginx
server{
        listen 443 ssl http2;
        listen [::]:443 ssl http2;
        server_name  vw.231111.xyz;

        #SSL
        ssl_certificate /root/.acme.sh/231111.xyz/fullchain.cer;
        ssl_certificate_key /root/.acme.sh/231111.xyz/231111.xyz.key;
        ssl_session_cache        shared:SSL:10m;
        ssl_session_timeout      10m;
        ssl_session_tickets      on;
        resolver                 8.8.4.4 8.8.8.8  valid=300s;
        resolver_timeout         10s;
        ssl_session_cache builtin:1000 shared:SSL:10m;

        ssl_prefer_server_ciphers on;

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3;

        add_header X-Frame-Options "SAMEORIGIN";
        add_header X-XSS-Protection "1; mode=block";
        add_header X-Content-Type-Options "nosniff";

        charset utf-8;
        
        location / {
                proxy_pass http://127.0.0.1:3080;
                proxy_http_version    1.1;
                proxy_cache_bypass    $http_upgrade;
                proxy_set_header Upgrade            $http_upgrade;
                proxy_set_header Connection         "upgrade";
                proxy_set_header Host               $host;
                proxy_set_header X-Real-IP          $remote_addr;
                proxy_set_header X-Forwarded-For    $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto  $scheme;
                proxy_set_header X-Forwarded-Host   $host;
                proxy_set_header X-Forwarded-Port   $server_port;
        }

        location /notifications/hub {
                proxy_pass http://127.0.0.1:3012;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
        }

        location /notifications/hub/negotiate {
                proxy_pass http://127.0.0.1:3080;
        }

        location /admin {
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_pass http://127.0.0.1:3080;
        }
}

server
{
        listen          80;
        server_name vw.231111.xyz;
        location / {
                rewrite ^/(.*)$ https://vw.231111.xyz/$1 permanent;
        }
}
```
重载 Nginx 配置文件
```shell
nginx -s reload
```
## 五、注册使用
访问网站，注册账号使用。如果只是个人使用，一定要在注册完成后，编辑 `docker-compose.yml` 关闭注册。

---

最后，数据无价，记得备份！
