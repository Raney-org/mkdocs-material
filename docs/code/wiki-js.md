---
tags:
  - DOCKER
---

# Wiki JS Docker Compose

[Here](https://github.com/requarks/wiki) is their github!

???+ success "docker-compose.yml"

    ```yaml
    version: "3"
    services:
    wiki:
        image: ghcr.io/requarks/wiki:2
        container_name: wikijs
        networks:
        - saltbox
        environment:
        DB_TYPE: postgres
        DB_HOST: postgres # or whatever you want
        DB_PORT: 5432
        DB_USER: your_user_here
        DB_PASS: 'password4321'
        DB_NAME: wiki
        labels:
        traefik.enable: true
        com.github.saltbox.saltbox_managed: true
        traefik.http.routers.wikijs-http.entrypoints: web
        traefik.http.routers.wikijs-http.middlewares: globalHeaders@file,redirect-to-https,gzip
        traefik.http.routers.wikijs-http.rule: Host(`wikijs.domain.com`)
        traefik.http.routers.wikijs-http.service: wikijs
        traefik.http.routers.wikijs.entrypoints: websecure
        traefik.http.routers.wikijs.middlewares: globalHeaders@file,secureHeaders@file,authelia@docker
        traefik.http.routers.wikijs.rule: Host(`wikijs.domain.com`)
        traefik.http.routers.wikijs.service: wikijs
        traefik.http.routers.wikijs.tls.certresolver: cfdns
        traefik.http.routers.wikijs.tls.options: securetls@file
        traefik.http.services.wikijs.loadbalancer.server.port: 3000
        restart: unless-stopped
        volumes:
        - /opt/wiki-js:/config
        - /etc/localtime:/etc/localtime:ro
        - /opt/wiki-js/config.yml:/config.yml
        - /opt/wiki-js/data:/data

    networks:
    saltbox:
        external: true
    ```

## Image test

<figure markdown>
  ![Image title](https://dummyimage.com/600x400/){ width="300" }
  <figcaption>Image caption</figcaption>
</figure>
