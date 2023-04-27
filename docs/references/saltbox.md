---
tags:
  - SALTBOX
---

# Saltbox

```yaml
wordpress_docker_envs_default:
  TZ: "{{ tz }}"
  WORDPRESS_DB_HOST: "mariadb:3306" <-- edit that
  WORDPRESS_DB_USER: "root"
  WORDPRESS_DB_PASSWORD: "password321"
  WORDPRESS_DB_NAME: "{{ wordpress_name }}"
```
