# Players

## Fetch all players

> To fetch all players, use this code:

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

## Trending Players

> To get a list of trending players based on add/drop activity:

```shell
curl "https://api.sleeper.app/v1/players/nfl/trending/add"
```

> You will get a JSON response that looks something like this:

```javascript
[
  {
    "player_id": "1111", // the player_id
    "count": 45         // number or adds
  },
  ...
]
```

> Want to embed this on your app? Copy the code below:

```
<iframe src="https://sleeper.app/embed/players/nfl/trending/add?lookback_hours=24&limit=25" width="350" height="500" allowtransparency="true" frameborder="0"></iframe>
```

<aside class="notice">
Please give attribution to Sleeper you are using our trending data.  If you'd like to embed our trending list on your website or blog, please use the embed code on the right.
</aside>

You can use this endpoint to get a list of trending players based on adds or drops in the past 24 hours.

`GET https://api.sleeper.app/v1/players/<sport>/trending/<type>?lookback_hours=<hours>&limit=<int>`

### URL Parameters

Parameter | Description
--------- | -----------
sport     | The sport, such as `nfl`
type      | Either `add` or `drop`
lookback_hours | Number of hours to look back (default is 24) - optional
limit     | Number of results you want, (default is 25) - optional
