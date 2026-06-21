---
title: "{{ replace .File.ContentBaseName "-" " " | title }}"
date: {{ .Date }}
draft: false
# --- Artist fields ---
status: "active"   # active or legacy
weight: 99         # lower = higher on roster; legacy artists can omit
website: ""        # the band's own site, if any
bandcamp: ""       # Bandcamp URL (merch / listening)
instagram: ""
spotify: ""
---

Short bio goes here.
