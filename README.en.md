<!-- README language switch -->
[![中文](https://img.shields.io/badge/%E4%B8%AD%E6%96%87-555555?style=for-the-badge)](README.md) [![English](https://img.shields.io/badge/English-1677ff?style=for-the-badge)](README.en.md)
<!-- /README language switch -->

# 📜 plugin_jinriyunshi | NoneBot Daily Fortune Plugin

An entertainment plugin for NoneBot 2 that provides a daily fortune reading. It combines fortune levels with traditional divination-style text, automatic caching, and a daily reset.

---

## ✨ Features

- Generate a daily fortune with a star rating, a written reading, and an image.
- Automatically fetch images using the Wallhaven API.
- Expand the image pool with duplicate detection using `imagehash` and `md5`.
- Refresh the image pool automatically each night or manually as an administrator.
- Allow each user to trigger a fortune only once per day to reduce chat spam.
- Support image pool refresh commands through private chat.

---

## 🖼 Examples

Examples of the plugin in use:

![Example 1](demo/demo1.png)
![Example 2](demo/demo2.png)

These show the text and image returned after a user sends `.今日运势`.

---

## 📥 Commands

The command keywords are Chinese and should be entered exactly as shown.

### User commands

| Command | Description |
| --- | --- |
| `.今日运势` or `.今日人品` | Generate a daily fortune level from 0 to 8, with a reading and a random image; available once per day |

### Administrator commands (private chat only)

| Command | Description |
| --- | --- |
| `.扩充图池` | Refresh the image pool by fetching from Wallhaven; runs asynchronously without blocking the main thread |

---

## 🧠 How it works

### Fortune generation

- With a 70% probability, calculate a score from four dimensions: wealth, relationships, career, and character, each ranging from 0 to 2.
- Otherwise, choose a level at random and derive a valid combination of scores.
- Each level from 0 to 8 has three predefined readings; one is selected randomly.
- Star ratings use `★` and `☆`.

### Image pool

- Refresh automatically at 3 AM each day.
- Source: the Wallhaven API.
- Tags include genshin-impact, honkai-star-rail, and other anime-style games.
- Fetch 5 images per tag and check for duplicates using `imagehash` and `md5`.
- Save downloaded images in `cache/wallhaven_download/`.

### Caching

- Cache daily fortunes in `cache/daily_cache.json`.
- Each user can receive a fortune at most once per day.
- Clear old cache data automatically each day.

### Image deduplication

- Compute aHash using `PIL` and `imagehash`.
- Generate an MD5 hash of the image bytes using `hashlib`.
- Skip duplicate images instead of adding them to the pool.

---

## 🗂 Project structure

```text
plugin_jinriyunshi/
├── __init__.py
├── cache/
│   ├── daily_cache.json          # Daily fortune cache
│   ├── wallhaven_download/       # Downloaded image pool
│   └── .hash_cache.json          # Image deduplication records
├── demo/
│   ├── demo1.png                 # Usage example 1
│   └── demo2.png                 # Usage example 2
└── README.md                    # Original README
```

---

## ⚙ Usage tips

- Add the administrators' QQ numbers to `ADMIN_QQ_LIST`.
- Users receive a notification if the image pool is empty. Populate it beforehand or run `.扩充图池` manually.
- Periodically remove old images from `wallhaven_download`, either manually or through automation.

---

## 📌 Disclaimer

- Images come from the public image library [wallhaven.cc](https://wallhaven.cc). Follow its terms of use.
- Fortune readings are for entertainment only. Do not treat them as factual predictions.

---

## 📮 Feedback

Issues and pull requests with feedback or suggestions are welcome!
