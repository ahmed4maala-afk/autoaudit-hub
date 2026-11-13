# AutoAudit Hub

Public assets and the link-in-bio page for the **AutoAudit** channel.

- YouTube — https://www.youtube.com/@AutoAudit
- Instagram — https://www.instagram.com/autoauditofficial/

## Why this repo exists

Instagram's Content Publishing API does not accept a file upload. It accepts
a **public URL** and fetches the media from it, so anything published to
Instagram has to be hosted somewhere public first. That is `media/`.

Instagram captions are also never clickable — links only work from the bio.
So `index.html` is the one page that bio link points at, and it lists every
published video. It is generated from `data/videos.json`, never edited by
hand.

## Layout

```
index.html          generated — do not edit directly
data/videos.json    source of truth for the page
media/              images and video served to the Instagram API
```

## Generating the page

```python
from core import hub
entries = hub.load()
entries.append(hub.Entry(
    slug="e90-specs",
    title="BMW E90 3-Series: Should You Buy It?",
    youtube_id="...",
    car="BMW 3-Series (E90) 2006–2011",
    published="2026-11-13",
    kind="specs",
))
hub.save(entries)
hub.render(entries)
hub.publish()
```

## Sources

Vehicle reliability figures come from the NHTSA Office of Defects
Investigation (`api.nhtsa.gov`). Photography is licence-filtered to CC0,
public domain and CC-BY only; credits travel with each image.
