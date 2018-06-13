# Leagues

## Get all leagues for user

```shell
curl "https://api.sleeper.app/v1/user/<user_id>/leagues/nfl/2018"
```

> The above command returns JSON structured like this:

```javascript
[
  {
    "total_rosters": 12,
    "status": "pre_draft", // can also be "drafting", "in_season", or "complete"
    "sport": "nfl",
    "settings": { settings object },
    "season_type": "regular",
    "season": "2018",
    "scoring_settings": { scoring_settings object },
    "roster_positions": [ roster positions array ],
    "previous_league_id": "198946952535085056",
    "name": "Sleeperbot Friends League",
    "league_id": "289646328504385536",
    "draft_id": "289646328508579840",
    "avatar": "efaefa889ae24046a53265a3c71b8b64"
  },
  {
    "total_rosters": 12,
    "status": "in_season",
    "sport": "nfl",
    "settings": { settings object },
    "season_type": "regular",
    "season": "2018",
    "scoring_settings": { scoring_settings object },
    "roster_positions": [ roster positions array ],
    "previous_league_id": "198946952535085056",
    "name": "Sleeperbot Dynasty",
    "league_id": "289646328504385536",
    "draft_id": "289646328508579840",
    "avatar": "efaefa889ae24046a53265a3c71b8b64"
  },
]
```

This endpoint retrieves all leagues.

### HTTP Request

`GET https://api.sleeper.app/v1/user/<user_id>/leagues/<sport>/<season>`

### URL Parameters

Parameter | Description
--------- | -----------
user_id   | The numerical ID of the user.
sport     | We only support "nfl" right now.
season    | Season can be 2017, 2018, etc...

## Get a specific league

```shell
curl "https://api.sleeper.app/v1/league/<league_id>"
```

> The above command returns JSON structured like this:

```javascript
{
  "total_rosters": 12,
  "status": "in_season",
  "sport": "nfl",
  "settings": { settings object },
  "season_type": "regular",
  "season": "2018",
  "scoring_settings": { scoring_settings object },
  "roster_positions": [ roster positions array ],
  "previous_league_id": "198946952535085056",
  "name": "Sleeperbot Dynasty",
  "league_id": "289646328504385536",
  "draft_id": "289646328508579840",
  "avatar": "efaefa889ae24046a53265a3c71b8b64"
}
```

This endpoint retrieves a specific league.

### HTTP Request

`GET https://api.sleeper.app/v1/league/<league_id>`

### URL Parameters

Parameter | Description
--------- | -----------
league_id | The ID of the league to retrieve

## Getting rosters in a league

```shell
curl "https://api.sleeper.app/v1/league/<league_id>/rosters"
```

> The above command returns JSON structured like this:

```javascript
[
  {
    "starters": ["2307", "2257", "4034", "147", "642", "4039", "515", "4149", "DET"],
    "settings": {
      "wins": 5,
      "waiver_position": 7,
      "waiver_budget_used": 0,
      "total_moves": 0,
      "ties": 0,
      "losses": 9,
      "fpts_decimal": 78,
      "fpts_against_decimal": 32,
      "fpts_against": 1670,
      "fpts": 1617
    },
    "roster_id": 1,
    "reserve": [],
    "players": ["1046", "138", "147", "2257", "2307", "2319", "4034", "4039", "4040", "4149", "421", "515", "642", "745", "DET"],
    "owner_id": "188815879448829952",
    "league_id": "206827432160788480"
  },
  ...
]
```

This endpoint retrieves all rosters in a league.

### HTTP Request

`GET https://api.sleeper.app/v1/league/<league_id>/rosters`

### URL Parameters

Parameter | Description
--------- | -----------
league_id | The ID of the league to retrieve rosters from
