---
tags:
  - DROPBOX
--- 

# Dropbox Notes

???+ quote

    We have had good success maxing out both a 2GB and a 10GB upload to dropbox using the following:

```yml
rclone copy local:/mnt/local/Media dropbox:/Media -vP --dropbox-chunk-size=128m --transfers=16 --size-only --ignore-checksum
Read what --size-only and --ignore-checksum 
```

flags do, as they may not suit your use case. Speeds are almost but not quite as fast omitting those two flags.  move should be as fast as copy
