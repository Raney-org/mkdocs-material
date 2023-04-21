---
tags:
  - DOCKER
---

# Audiobookshelf Docker Compose

If you've looked over some of my other compose examples here, you'll notice that this guy is a little different, but it still works the same! It will still get the saltbox docker network, be "managed" by saltbox, etc. Its a fantastic app if you haven't used it before. [Here](https://github.com/advplyr/audiobookshelf) is their GitHub!!

???+ success "docker-compose.yml"

    ```yaml
    version: '3.3'
    services:
        advplyr:
            container_name: audiobookshelf
            restart: unless-stopped
            environment:
                - PGID=1000
                - PUID=1001
                - TZ=America/Chicago
            volumes:
                - '/mnt:/mnt'
                - '/opt/audiobookshelf:/config'
                - '/opt/audiobookshelf/metadata:/metadata'
                - '/etc/localtime:/etc/localtime:ro'
            network_mode: saltbox
            labels:
                - com.github.saltbox.saltbox_managed=true
                - traefik.enable=true
                - traefik.http.routers.audiobookshelf-http.entrypoints=web
                - 'traefik.http.routers.audiobookshelf-http.middlewares=globalHeaders@file,redirect-to-https,gzip'
                - traefik.http.routers.audiobookshelf-http.rule=Host\(\`audiobookshelf.domain.com\`\)
                - traefik.http.routers.audiobookshelf-http.service=audiobookshelf
                - traefik.http.routers.audiobookshelf.entrypoints=websecure
                - 'traefik.http.routers.audiobookshelf.middlewares=globalHeaders@file,secureHeaders@file'
                - traefik.http.routers.audiobookshelf.rule=Host\(\`audiobookshelf.domain.com\`\)
                - traefik.http.routers.audiobookshelf.service=audiobookshelf
                - traefik.http.routers.audiobookshelf.tls.certresolver=cfdns
                - traefik.http.routers.audiobookshelf.tls.options=securetls@file
                - traefik.http.services.audiobookshelf.loadbalancer.server.port=80
            image: ghcr.io/advplyr/audiobookshelf
    ```
