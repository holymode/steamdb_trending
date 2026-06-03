# steamdb_trending

A daily-updated dataset of trending and upcoming Steam games, sourced from SteamDB. Available in both **JSON** and **HTML** formats.

## Overview

This repository automatically scrapes and saves SteamDB trending game data every day at `01:00 UTC`. It tracks games gaining follower traction as well as upcoming releases ranked by various metrics. Both SFW and NSFW (adult content) variants are provided for each dataset.

## Files

| File | Description |
|------|-------------|
| `trending_followers.json` | Games trending by follower growth (SFW) |
| `trending_followers_nsfw.json` | Games trending by follower growth (includes adult content) |
| `upcoming_latest.json` | Upcoming games sorted by latest additions (SFW) |
| `upcoming_latest_nsfw.json` | Upcoming games sorted by latest additions (includes adult content) |
| `upcoming_peak_desc.json` | Upcoming games sorted by peak players descending (SFW) |
| `upcoming_peak_desc_nsfw.json` | Upcoming games sorted by peak players descending (includes adult content) |
| `html/` | HTML-rendered versions of the above datasets |

## JSON Format

Each JSON file contains an array of game objects:

```json
[
  { "appid": 1118520, "name": "Paralives" },
  { "appid": 3768760, "name": "007 First Light" },
  ...
]
```

| Field | Type | Description |
|-------|------|-------------|
| `appid` | `number` | Steam App ID — use to construct store links or query the Steam API |
| `name` | `string` | Display name of the game |

You can link directly to a game's Steam store page using:
```
https://store.steampowered.com/app/{appid}
```

## Usage Examples

**Fetch the latest trending games (JSON):**
```bash
curl https://raw.githubusercontent.com/holymode/steamdb_trending/main/trending_followers.json
```

**Fetch upcoming games (HTML view):**
```
https://raw.githubusercontent.com/holymode/steamdb_trending/main/html/upcoming_latest.html
```

**Parse with Python:**
```python
import json, urllib.request

url = "https://raw.githubusercontent.com/holymode/steamdb_trending/main/trending_followers.json"
with urllib.request.urlopen(url) as r:
    games = json.loads(r.read())

for game in games[:10]:
    print(game["appid"], game["name"])
```

## Update Schedule

Data is committed automatically once per day. The last commit timestamp reflects the freshness of the data.

## Data Source

All data originates from [SteamDB](https://steamdb.info/), a third-party site that tracks Steam catalog metadata, pricing, and player statistics.

## License

This repository contains data aggregated from SteamDB for informational and research purposes.
