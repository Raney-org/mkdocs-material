---
tags:
  - PYTHON
---

# Youtube DL

Here is the compose `.yaml` I used to initially set up ytdl. It worked well with my system until I created an ansible role for it!

???+ success "docker-compose.yml"

    ```yaml
    version: "3"
    services:
        ytdl:
        restart: unless-stopped
        container_name: ytdl
        image: ghcr.io/jmbannon/ytdl-sub:latest
        hostname: ytdl
        environment:
          - PUID=1001
          - PGID=1002
          - TZ=Etc/UTC
        networks:
          - saltbox
        labels:
            traefik.enable: true
            traefik.http.routers.ytdl-http.entrypoints: web
            traefik.http.routers.ytdl-http.middlewares: globalHeaders@file,redirect-to-https,gzip
            traefik.http.routers.ytdl-http.rule: Host(`ytdl.domain.tld`)
            traefik.http.routers.ytdl-http.service: ytdl
            traefik.http.routers.ytdl.entrypoints: websecure
            traefik.http.routers.ytdl.middlewares: globalHeaders@file,secureHeaders@file
            traefik.http.routers.ytdl.rule: Host(`ytdl.domain.tld`)
            traefik.http.routers.ytdl.service: ytdl
            traefik.http.routers.ytdl.tls.certresolver: cfdns
            traefik.http.routers.ytdl.tls.options: securetls@file
            traefik.http.services.ytdl.loadbalancer.server.port: 80
        volumes:
          - /opt/ytdl:/config
          - /etc/localtime:/etc/localtime:ro
          - /mnt/local/Media/TV:/tv_shows
          - /mnt/local/Media/Movies:/movies
          - /mnt/local/Media/MusicVideos:/music_videos
          - /mnt/local/Media/Music:/music

    networks:
        saltbox:
        external: true
    ```
