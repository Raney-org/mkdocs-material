---
tags:
  - QBITTORRENT
  - SCRIPTS
---

# qBit scripts

## qBittorrent Ratio Analyzer

[qBit Average Ratio](https://github.com/s0up4200/scripts/blob/main/qbit-avg-ratio.py)

This script calculates the average ratio of torrents in each category and tag in qBittorrent. The results can be displayed in the console and optionally saved to a CSV file.

Good for min-maxers that want to see how their tactics perform.

### Requirements

- python 3
- qbittorrent-api library: pip3 install qbittorrent-api

### Usage

1. Set your qBittorrent credentials (host, username, and password) in the script file or call them as arguments.
2. Run the script using python3 qbit_ratio.py
3. Use optional command-line arguments as needed.

Available command-line arguments:

```sh
--host - qBittorrent Web UI host (default: value set in script)
--username - qBittorrent Web UI username (default: value set in script)
--password - qBittorrent Web UI password (default: value set in script)
--tags-only - Only export tags
--categories-only - Only export categories
--exclude-tags "Tag1" "Tag2" "Tag3"
--exclude-categories "Category1" "Category2" "Category3"
```

### Example output

```json
python3 qbit_ratio.py --exclude-tags "noHL"

Average Ratios for Categories:
Category: tv, Average Ratio: 3.94
Category: music, Average Ratio: 1.05

Average Ratios for Tags:
Tag: Omegabrr - Popular TV, Average Ratio: 4.02
Tag: Omegabrr - Anticipated TV, Average Ratio: 2.97
Tag: Music - Upcoming albums, Average Ratio: 1.13
Tag: Music - New albums, Average Ratio: 0.51
```
