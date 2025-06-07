###  FileBrowser Docker Compose Setup

#### 📁 Recommended Directory Structure:

```bash
mkdir -p docker/filebrowser
cd docker/filebrowser
```

```bash
touch docker/filebrowser/filebrowser.db
touch docker/filebrowser/settings.json
```
#### ✏️ `docker-compose.yml`:

```yaml
version: "3"
services:
  filebrowser:
    image: filebrowser/filebrowser:latest
    container_name: filebrowser
    ports:
      - "8280:80"
    volumes:
      - /:/srv
      - /root/docker/filebrowser/filebrowser.db:/database/filebrowser.db
      - /root/docker/filebrowser/settings.json:/config/settings.json
    environment:
      - PUID=1000
      - PGID=1000
    restart: unless-stopped
```

---


### 🚀 Run It:

```bash
docker compose up -d
```

---


