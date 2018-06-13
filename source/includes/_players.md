# Players

> To fetch a user object, use this code:

```shell
curl "https://api.sleeper.app/v1/players/nfl"
```

> You will get a JSON response that looks something like this:

```javascript
{
  "3086": {
    "hashtag": "#TomBrady-NFL-NE-12",
    "depth_chart_position": 1,
    "status": "Active",
    "sport": "nfl",
    "fantasy_positions": ["QB"],
    "number": 12,
    "search_last_name": "brady",
    "injury_start_date": null,
    "weight": "220",
    "position": "QB",
    "practice_participation": null,
    "sportradar_id": "",
    "team": "NE",
    "last_name": "Brady",
    "college": "Michigan",
    "fantasy_data_id":17836,
    "injury_status":null,
    "player_id":"3086",
    "height": "6'4\"",
    "search_full_name": "tombrady",
    "age": 40,
    "stats_id": "",
    "birth_country": "United States",
    "espn_id": "",
    "search_rank": 24,
    "first_name": "Tom",
    "depth_chart_order": 1,
    "years_exp": 14,
    "rotowire_id": null,
    "rotoworld_id": 8356,
    "search_first_name": "tom",
    "yahoo_id": null
  },
  ...
}
```

<aside class="notice">
Please use this call sparingly, as it is intended only to be used once per day at most to keep your player IDs updated.  The average size of this query is <code>5MB</code>.
</aside>

Since rosters and draft picks contain `Player IDs` which look like `"1042"`, `"2403"`, `"CAR"`, etc, you will need to know what those IDs map to.  The `/players` call provides you the map necessary to look up any player.

You should **save this information on your own servers** as this is not intended to be called every time you need to look up players due to the filesize being close to 5MB in size.  You do not need to call this endpoint more than once per day.

`GET https://api.sleeper.app/v1/players/nfl`
