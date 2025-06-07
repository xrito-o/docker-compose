```yml
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      # These ports are in format <host-port>:<container-port>
      - '8080:80' # Public HTTP Port
      - '4430:443' # Public HTTPS Port
      - '8100:81' # Admin Web Port
      # Add any other Stream port you want to expose
      # - '21:21' # FTP

    volumes:
      - /root/docker/nginx-proxy-manager/data:/data
      - /root/docker/nginx-proxy-manager/letsencrypt:/etc/letsencrypt
```