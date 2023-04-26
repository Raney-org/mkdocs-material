---
tags:
  - RADARR
---

# Radarr

So I migrated from sqlite to postgresql today on my radarr4k container. It seemed to go pretty well! I'll just monitor it for a while I suppose.

[Here](https://wiki.servarr.com/radarr/postgres-setup) is the link to the setup/tutorial, I'll probably make my own as that assumes that you know more than you do IMO. I fiddle fucked with it for forever until I got it to work.

[This](https://github.com/Radarr/Radarr/issues/7387) issue has more info on how someone did some trouble shooting as well, if you have any questions about it.

A saltbox specific reference for the pgloader command is here:

=== ":octicons-file-code-16: `docker-run`"

    ```docker
    docker run --rm -v /opt/radarr4k/radarr.db:/radarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /radarr.db "postgresql://radarr4k:password1234@postgres2/radarr4k-main"
    ```

=== ":octicons-file-code-16: `docker-run 2`"

    ```docker
    docker run --rm -v /opt/radarr4k/radarr.db:/radarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" --with "prefetch rows = 100" --with "batch size = 1MB"  /radarr.db "postgresql://radarr4k:password1234@postgres2/radarr4k-main"
    ```
