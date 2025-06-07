### Portainer using Docker Compose

#### 1. Create a Directory for Portainer

```bash
mkdir -p ~/docker/portainer
cd ~/docker/portainer
```

#### 2. Create the `docker-compose.yml` File

```bash
nano docker-compose.yml
```

Paste the following content:

```yaml
version: '3.8'

services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: unless-stopped
    ports:
      - "9000:9000"
      - "9443:9443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /root/docker/portainer/portainer_data:/data
```



#### 3. Start Portainer

```bash
docker compose up -d
```

---