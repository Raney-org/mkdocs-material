---
tags:
  - TUNE
  - QBITTORRENT
---

# qBittorrent Tuning for 4.3.9-4.5.2 on 1gbps LT 1.2

Thank you to Imabee for writing this up! Hes the tuniest Canadian I know.

## Speed

Unlimited on all, rate limit utp and lan

## Connection

``` yaml
Peer connection protocol: TCP
Global max: off
Max num per torrent: off
Global max number upload slots: off
Max number of upload slots: off
```
![]
## Advanced

``` yaml
Interface: put it on whatever interface you want the torrent client to bind to
File Pool Size: 5000
Outstanding Mem: 128
Disk Cache: 1024 (or -1 if you feel ballsy, 0 if you experience memory leaks)
Disk cache expiry: 60
Disk IO Type: Default
Disk IO Read Mode: Enable OS Cache
Disk IO Write Mode: Enable OS Cache
Coalesce reads and writes: OFF
Use piece extent affinity: ON
Send Upload Piece Suggestions: ON
Send Buffer Watermark: 5120
Send Buffer Low Watermark: 512
Send buffer watermark factor: Between 200-250, adjust as needed
Outgoing connections per second: 50
Socket Backlog: 1000
Peer TOS: 128
utp-tcp mixed mode algo: Prefer TCP
Support IDN: ON
Allow Multiple Connections from the same IP address: ON
Validate HTTPS: OFF
SSRF Mitigation: ON
Upload Slots Behaviour: Fixed Slots
Upload choking alogrithm: Fastest Upload
Always announce to all tiers: ON
Max concurrent HTTP Announces: 50-75 (only increase if experiencing announce issues with very high amount of torrents loaded in client)
Peer turnover disconnect Percentage: 0
Peer turnover threshold percentage: 90
Peer turnover disconnect interval: 30
Max outstanding requests to a single peer: Leave as is
```
