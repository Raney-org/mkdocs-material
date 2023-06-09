---
tags:
  - DOCKER
---

# Pihole + Unbound Compose File + `.env`

## Pihole compose

=== "docker-compose.yml"

    ```yaml
    version: '3.0'

    #volumes:
    #  etc_pihole-unbound:
    #  etc_pihole_dnsmasq-unbound:

    services:
    pihole:
        container_name: pihole
        image: cbcrowe/pihole-unbound:latest
        hostname: ${HOSTNAME}
        domainname: ${DOMAIN_NAME}
        ports:
        # # - 443:443/tcp
        - 53:53/tcp
        - 53:53/udp
        # - ${PIHOLE_WEBPORT:-80}:80/tcp #Allows use of different port to access pihole web interface when other docker containers use port 80
        - 5335:5335/tcp # Uncomment to enable unbound access on local server
        - 22/tcp # Uncomment to enable SSH
        environment:
        - FTLCONF_LOCAL_IPV4=${FTLCONF_LOCAL_IPV4}
        - TZ=${TZ:-UTC}
        - WEBPASSWORD=${WEBPASSWORD}
        - WEBTHEME=${WEBTHEME:-default-light}
        - REV_SERVER=${REV_SERVER:-false}
        - REV_SERVER_TARGET=${REV_SERVER_TARGET}
        - REV_SERVER_DOMAIN=${REV_SERVER_DOMAIN}
        - REV_SERVER_CIDR=${REV_SERVER_CIDR}
        - PIHOLE_DNS_=127.0.0.1#5335
        - DNSSEC="true"
        - DNSMASQ_LISTENING=single
        - PUID=1001
        - PGID=1002
        labels:
        traefik.enable: true
        traefik.http.routers.pihole-http.entrypoints: web
        traefik.http.routers.pihole-http.middlewares: globalHeaders@file,redirect-to-https,gzip
        traefik.http.routers.pihole-http.rule: Host(`pihole.domain.com`)
        traefik.http.routers.pihole-http.service: pihole
        traefik.http.routers.pihole.entrypoints: websecure
        traefik.http.routers.pihole.middlewares: globalHeaders@file,secureHeaders@file
        traefik.http.routers.pihole.rule: Host(`pihole.domain.com`)
        traefik.http.routers.pihole.service: pihole
        traefik.http.routers.pihole.tls.certresolver: cfdns
        traefik.http.routers.pihole.tls.options: securetls@file
        traefik.http.services.pihole.loadbalancer.server.port: 80
    #   volumes:
    #     - etc_pihole-unbound:/etc/pihole:rw
    #     - etc_pihole_dnsmasq-unbound:/etc/dnsmasq.d:rw
        # network_mode: host
        networks:
        - saltbox
        cap_add:
        - NET_ADMIN
        volumes:
        - /opt/pihole:/etc/pihole:rw
        - /opt/pihole/dnsmasq:/etc/dnsmasq.d:rw
        - /etc/localtime:/etc/localtime:ro
        restart: unless-stopped
    networks:
    saltbox:
        external: true
    ```

=== ".env"

    ```toml
    FTLCONF_LOCAL_IPV4=192.168.1.92
    TZ=America/Chicago
    WEBPASSWORD=Chingala1@
    REV_SERVER=true
    REV_SERVER_DOMAIN=localdomain
    REV_SERVER_TARGET=192.168.1.1
    REV_SERVER_CIDR=192.168.1.0/16
    HOSTNAME=pihole
    DOMAIN_NAME=pihole.localdomain
    #PIHOLE_WEBPORT=80
    WEBTHEME=default-dark
    ```

## Pihole `.env`

The PiHole container requires a .env file to compliment the `docker-compose.yml` this is with. Current set up that WORKED was as follows
