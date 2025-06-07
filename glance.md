# Glance Dashboard Setup & Configuration

## Docker Compose Service

This configuration runs the Glance app as a Docker container:

```yaml
services:
  glance:
    container_name: glance
    image: glanceapp/glance
    restart: unless-stopped
    volumes:
      - /root/docker/glance/config:/app/config
    ports:
      - 8980:8080
```

* **container\_name**: `glance`
* **image**: `glanceapp/glance` (official Glance Docker image)
* **restart**: `unless-stopped` (auto-restarts unless manually stopped)
* **volumes**: Mounts local config directory `/root/docker/glance/config` into container at `/app/config`
* **ports**: Maps host port `8980` to container port `8080`

---

## Editing Glance Configuration

To customize your Glance dashboard, edit the `glance.yml` config file:

```bash
cd /root/docker/glance/config
nano glance.yml
```


```yml
pages:
#-------------------------------- tab 1 ---------------------------------------
  - name: Home
    columns:
      - size: small
        widgets:
          - type: calendar
            first-day-of-week: saturday

      - size: full
        widgets:
          # - type: bookmarks
          #   groups:
          #     - title: My Services
          #       color: 50 50 50
          #       links:
          #         - title: Portainer
          #           url: https://portainer.xrito.xyz
          #           icon: di:portainer
          #         - title: Wireguard
          #           url: https://vpn.xrito.xyz
          #           icon: di:wireguard
          #         - title: Nginx Proxy Manager
          #           url: https://proxy.xrito.xyz
          #           icon: si:nginxproxymanager
          - type: monitor
            cache: 1m
            title: Services
            sites:
             - title: Portainer
               url: https://portainer.xrito.xyz
               icon: di:portainer
             - title: Wireguard
               url: https://vpn.xrito.xyz
               icon: di:wireguard
             - title: Nginx Proxy Manager
               url: https://proxy.xrito.xyz
               icon: si:nginxproxymanager
             - title: Filebrowser
               url: https://file.xrito.xyz
               icon: di:filebrowser
             - title: Blog
               url: https://blog.xrito.xyz/
               icon: si:filebrowser
      - size: small
        widgets:
          - type: weather
            units: metric
            location: Dhaka, Bangladesh
            hour-format: 12h
#-------------------------------- tab 2 ---------------------------------------
  - name: Feeds
    columns:
      - size: full
        widgets:
          - type: rss
            limit: 100
            collapse-after: 15
            style: detailed-list
            cache: 3h
            feeds:
              - url: https://www.cnx-software.com/feed/ # CNX Software
              - url: https://newsroom.churchofjesuschrist.org/rss # Church Newsroom
              - url: https://liliputing.com/feed #Liliputing
              - url: https://9to5google.com/guides/google/feed/ # 9 to 5 Google
              - url: https://www.ksl.com/rss/news/news\_utah #KSL UTAH News
              - url: https://www.hackster.io/news/ # Hackster.io
              - url: https://www.neowin.net/news/rss/ # Neowin
              - url: https://goodereader.com/blog/feed # good e-reader
#-------------------------------- tab 3 ---------------------------------------
  - name: Reddit
    columns:
      - size: full
        widgets:
          - type: reddit
            subreddit: selfhosted
            show-thumbnails: true
            limit: 25
          - type: reddit
            subreddit: homeassistant
            show-thumbnails: true
            limit: 25
          - type: reddit
            subreddit: Xpenology
            show-thumbnails: true
            limit: 25
          - type: reddit
            subreddit: synology
            show-thumbnails: true
            limit: 25
          - type: reddit
            subreddit: immich
            show-thumbnails: true
            limit: 25
          - type: reddit
            subreddit: smoking
            show-thumbnails: true
            limit: 25
          - type: reddit
            subreddit: OffsetSmokers
            show-thumbnails: true
            limit: 25
          - type: reddit
            subreddit: opendirectories
            show-thumbnails: true
            limit: 25


#-------------------------------- tab 4 ---------------------------------------
  - name: Youtube Channels
    columns:
      - size: full
        widgets:
          #- title: BBQ Channels
          #  type: video
          #  channels:
            #  - UCsLTjOX249AJsrl9iJh4CSw # ChudsBBQ
            #  - UCselvHbb5ah0sEqZrFa-7nA # Mad Scientist BBQ
            #  - UCfx_bnkuHaJeQMgchdNvQDw # Smoker Builder
          - title: Tech Channels
            type: videos
            channels:
               - UC3ECq823SyuR1Is4zhxfuOA
               - UCngn7SVujlvskHRvRKc1cTw
            #  - UCR-DXc1voovS8nhAvccRZhg # Jeff Geerling
            #  - UCv6J_jJa8GJqFwQNgNrMuww # ServeTheHome
            #  - UCOk-gHyjcWZNj3Br4oxwh0A # Techno Tim
            #  - UCOJJM6kvbqc5vytWR-TGu0w # AuxXxilium Tech
            #  - UC_81EVeTVFtqe2FYMPOuJLw # VolumeData21
            #  - UCwFpzG5MK5Shg_ncAhrgr9g # Awesome Open Source
          #- title: Health Channels
          #  type: videos
          #  channels:
            #  - UC_yUeH8TsG5pxqvkOxBtsFA # Snake Diet
            #  - UCAohrrjG-3gEp5QF1WlM9_w # Siim Land
#-------------------------------- tab 5 ---------------------------------------
  - name: test
    # Optionally, if you only have a single page you can hide the desktop navigation for a cleaner look
    # hide-desktop-navigation: true
    columns:
      - size: small
        widgets:
          - type: calendar
            first-day-of-week: monday

          - type: rss
            limit: 10
            collapse-after: 3
            cache: 12h
            feeds:
              - url: https://selfh.st/rss/
                title: selfh.st
                limit: 4
              - url: https://ciechanow.ski/atom.xml
              - url: https://www.joshwcomeau.com/rss.xml
                title: Josh Comeau
              - url: https://samwho.dev/rss.xml
              - url: https://ishadeed.com/feed.xml
                title: Ahmad Shadeed

          - type: twitch-channels
            channels:
              - theprimeagen
              - j_blow
              - piratesoftware
              - cohhcarnage
              - christitustech
              - EJ_SA

      - size: full
        widgets:
          - type: group
            widgets:
              - type: hacker-news
              - type: lobsters

          - type: videos
            channels:
              - UCXuqSBlHAE6Xw-yeJA0Tunw # Linus Tech Tips
              - UCR-DXc1voovS8nhAvccRZhg # Jeff Geerling
              - UCsBjURrPoezykLs9EqgamOA # Fireship
              - UCBJycsmduvYEL83R_U4JriQ # Marques Brownlee
              - UCHnyfMqiRRG1u-2MsSQLbXA # Veritasium

          - type: group
            widgets:
              - type: reddit
                subreddit: technology
                show-thumbnails: true
              - type: reddit
                subreddit: selfhosted
                show-thumbnails: true

      - size: small
        widgets:
          - type: weather
            location: London, United Kingdom
            units: metric # alternatively "imperial"
            hour-format: 12h # alternatively "24h"
            # Optionally hide the location from being displayed in the widget
            # hide-location: true

          - type: markets
            markets:
              - symbol: SPY
                name: S&P 500
              - symbol: BTC-USD
                name: Bitcoin
              - symbol: NVDA
                name: NVIDIA
              - symbol: AAPL
                name: Apple
              - symbol: MSFT
                name: Microsoft

          - type: releases
            cache: 1d
            # Without authentication the Github API allows for up to 60 requests per hour. You can create a
            # read-only token from your Github account settings and use it here to increase the limit.
            # token: ...
            repositories:
              - glanceapp/glance
              - go-gitea/gitea
              - immich-app/immich
              - syncthing/syncthing
```