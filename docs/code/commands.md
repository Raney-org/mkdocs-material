---
tags:
  - COMMANDS
  - SNIPPETS
---

# Cli commands

Here is one for finding your timezone. How cool is that.

``` sh
curl http://ip-api.com/line?fields=timezone
```

Here is one for showing all the traefik rules attached to containers. Helpful for finding other things using jq.

``` sh
docker inspect $(docker ps -aq) | jq -r '.[].Config.Labels' | grep ".rule"
```
