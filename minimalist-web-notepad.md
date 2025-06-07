```yml
version: "2.4"
services:
    minimalist-web-notepad:
        container_name: minimalist-web-notepad
        restart: always
        ports:
         - "8065:80"
        environment:
            - TZ=Asia/Shanghai
            - PUID=1000
            - PGID=1000
        volumes:
         - /root/docker/minimalist-web-notepad/data:/app/web/_tmp
        image: ddsderek/minimalist-web-notepad:latest
```