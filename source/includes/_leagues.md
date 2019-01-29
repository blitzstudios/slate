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

## Getting users in a league

```shell
curl "https://api.sleeper.app/v1/league/<league_id>/users"
```

> The above command returns JSON structured like this:

```javascript
[
  {
    "user_id": "<user_id>",
    "username": "<username>",
    "display_name": "<display_name>",
    "avatar": "1233456789",
    "metadata": {
      "team_name": "Dezpacito"
    },
    "is_owner": true   // is commissioner (there can be multiple commissioners)
  },
  ...
]
```

This endpoint retrieves all users in a league.

This also includes each user's **display_name**, **avatar**, and their **metadata** which sometimes includes a nickname they gave their team.

### HTTP Request

`GET https://api.sleeper.app/v1/league/<league_id>/users`

### URL Parameters

Parameter | Description
--------- | -----------
league_id | The ID of the league to retrieve rosters from



## Getting matchups in a league

```shell
curl "https://api.sleeper.app/v1/league/<league_id>/matchups/<week>"
```

> The above command returns JSON structured like this:

```javascript
[
  {
    "starters": ["421", "4035", "3242", "2133", "2449", "4531", "2257", "788", "PHI"],
    "roster_id": 1,
    "players": ["1352", "1387", "2118", "2133", "2182", "223", "2319", "2449", "3208", "4035", "421", "4881", "4892", "788", "CLE"],
    "matchup_id": 2
  },
  ...
]
```

This endpoint retrieves all matchups in a league for a given week.  Each object in the list represents one team.  The two teams with the same `matchup_id` match up against each other.

The `starters` is in an ordered list of player_ids, and `players` is a list of all player_ids in this matchup.

The bench can be deduced by removing the `starters` from the `players` field.

### HTTP Request

`GET https://api.sleeper.app/v1/league/<league_id>/matchups/<week>`

### URL Parameters

Parameter | Description
--------- | -----------
league_id | The ID of the league to retrieve matchups from
week      | The week these matchups take place



## Getting the playoff bracket

```shell
curl "https://api.sleeper.app/v1/league/<league_id>/winners_bracket"
curl "https://api.sleeper.app/v1/league/<league_id>/losers_bracket"
```

> The above command returns JSON structured like this:

```javascript
[
  {r: 1, m: 1,   t1: 3,       t2: 6,       w: null, l: null},
  {r: 1, m: 2,   t1: 4,       t2: 5,       w: null, l: null},

  {r: 2, m: 3,   t1: 1,       t2: {w: 1},  w: null, l: null},
  {r: 2, m: 4,   t1: 2,       t2: {w: 2},  w: null, l: null},
  {r: 2, m: 5,   t1: {l: 1},  t2: {l: 2},  w: null, l: null, p: 5},

  {r: 3, m: 6,   t1: {w: 3},  t2: {w: 4},  w: null, l: null, p: 1},
  {r: 3, m: 7,   t1: {l: 3},  t2: {l: 4},  w: null, l: null, p: 3}
]
```

This endpoint retrieves the playoff bracket for a league for 4, 6, and 8 team playoffs.

Each row represents a matchup between 2 teams.

Field | Type          | Description
----- | ------------- | -----
r     | int           | The round for this matchup, 1st, 2nd, 3rd round, etc.
m     | int           | The match `id` of the matchup, unique for all matchups within a bracket.
t1    | int or object | The `roster_id` of a team in this matchup OR `{w: 1}` which means the winner of match id `1`
t2    | int or object | The `roster_id` of the other team in this matchup OR `{l: 1}` which means the loser of match id `1`
w     | int           | The `roster_id` of the winning team, if the match has been played.
l     | int           | The `roster_id` of the losing team, if the match has been played.


### HTTP Request

`GET https://api.sleeper.app/v1/league/<league_id>/winners_bracket`

`GET https://api.sleeper.app/v1/league/<league_id>/loses_bracket`

### URL Parameters

Parameter | Description
--------- | -----------
league_id | The ID of the league to retrieve matchups from