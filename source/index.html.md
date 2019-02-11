---
title: Sleeper API

language_tabs:
  - shell

toc_footers:
  - <a href='https://sleeper.app'>Go to sleeper.app</a>

includes:
  - user
  - avatars
  - leagues
  - drafts
  - players
  - stats
  - errors

search: true
---

# Introduction

The Sleeper API is a read-only HTTP API that is free to use and allows access to a user's leagues, drafts, and rosters.

No API Token is necessary, as you **cannot modify** contents via this API.

Be mindful of the frequency of calls.  A general rule is to stay under 1000 API calls per minute, otherwise, you risk being IP-blocked.
