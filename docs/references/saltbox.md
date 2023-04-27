---
tags:
  - SALTBOX
---

# Saltbox

## Wordpress

```yaml
wordpress_docker_envs_default:
  TZ: "{{ tz }}"
  WORDPRESS_DB_HOST: "mariadb:3306" <-- edit that
  WORDPRESS_DB_USER: "root"
  WORDPRESS_DB_PASSWORD: "password321"
  WORDPRESS_DB_NAME: "{{ wordpress_name }}"
```

to install another instance of mariadb, you'd run: `#!bash sb install mariadb -e mariadb_name=mariadb2`

## Homeassistant

So this link to a [Homeassistant] tutorial is going to be super helpful I think.

  [Homeassistant]: https://sequr.be/blog/2022/09/home-assistant-container-part-3-mariadb-and-influxdb/
