---
title: "{{ replace .File.ContentBaseName "-" " " | title }}"
date: {{ .Date }}
draft: false
# --- Release fields ---
artist: ""         # band name (match an artist title)
catalog: ""        # catalog number, e.g. DS-001
format: ""         # e.g. LP / Cassette / Digital
released: ""       # e.g. September 5, 2025
coverart: ""       # path to cover art, e.g. /covers/ds-001.jpg
bandcamp: ""       # link to buy / listen
spotify: ""        # Spotify album URL, e.g. https://open.spotify.com/album/ID
bandcamp_embed: "" # paste the full Bandcamp iframe embed code here
---

Liner notes / description goes here.
