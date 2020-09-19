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
    "matchup_id": 2,
    "points": 20.0 // total points for team based on league settings
    "custom_points": null // if commissioner overrides points manually
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
  {r: 1, m: 1,   t1: 3,    t2: 6,     w: null, l: null},
  {r: 1, m: 2,   t1: 4,    t2: 5,     w: null, l: null},

  {r: 2, m: 3,   t1: 1,    t2: null,  t2_from: {w: 1},  w: null, l: null},
  {r: 2, m: 4,   t1: 2,    t2: null,  t2_from: {w: 2},  w: null, l: null},
  {r: 2, m: 5,   t1: null, t2: null,  t1_from: {l: 1},  t2_from: {l: 2},  w: null, l: null, p: 5},

  {r: 3, m: 6,   t1: null, t2: null,  t1_from: {w: 3},  t2_from: {w: 4},  w: null, l: null, p: 1},
  {r: 3, m: 7,   t1: null, t2: null,  t1_from: {l: 3},  t2_from: {l: 4},  w: null, l: null, p: 3}
]
```

This endpoint retrieves the playoff bracket for a league for 4, 6, and 8 team playoffs.

Each row represents a matchup between 2 teams.

Field   | Type   | Description
------- | ------ | -----
r       | int    | The round for this matchup, 1st, 2nd, 3rd round, etc.
m       | int    | The match `id` of the matchup, unique for all matchups within a bracket.
t1      | int    | The `roster_id` of a team in this matchup OR `{w: 1}` which means the winner of match id `1`
t2      | int    | The `roster_id` of the other team in this matchup OR `{l: 1}` which means the loser of match id `1`
w       | int    | The `roster_id` of the winning team, if the match has been played.
l       | int    | The `roster_id` of the losing team, if the match has been played.
t1_from | object | Where t1 comes from, either winner or loser of the match `id`, necessary to show bracket progression.
t2_from | object | Where t2 comes from, either winner or loser of the match `id`, necessary to show bracket progression.


### HTTP Request

`GET https://api.sleeper.app/v1/league/<league_id>/winners_bracket`

`GET https://api.sleeper.app/v1/league/<league_id>/loses_bracket`

### URL Parameters

Parameter | Description
--------- | -----------
league_id | The ID of the league to retrieve matchups from



## Get transactions

```shell
curl "https://api.sleeper.app/v1/league/<league_id>/transactions/<round>"
```

> The above command returns JSON structured like this:

```javascript
[
  {
    "type": "trade",
    "transaction_id": "434852362033561600",
    "status_updated": 1558039402803,
    "status": "complete",
    "settings": null,     // trades do not use this field
    "roster_ids": [2, 1], // roster_ids involved in this transaction
    "metadata": null,
    "leg": 1,         // in football, this is the week
    "drops": null,
    "draft_picks": [  // picks that were traded
      {
        "season": "2019",// the season this draft pick belongs to
        "round": 5,      // which round this draft pick is
        "roster_id": 1,  // original owner's roster_id
        "previous_owner_id": 1,  // previous owner's roster id (in this trade)
        "owner_id": 2,   // the new owner of this pick after the trade
      },
      {
        "season": "2019",
        "round": 3,
        "roster_id": 2,
        "previous_owner_id": 2,
        "owner_id": 1,
      }
    ],
    "creator": "160000000000000000",  // user id who initiated the transaction
    "created": 1558039391576,
    "consenter_ids": [2, 1], // roster_ids of the people who agreed to this transaction
    "adds": null
    "waiver_budget": [   // roster_id 2 sends 55 FAAB dollars to roster_id 3
      {
        "sender": 2,
        "receiver": 3,
        "amount": 55
      }
    ],
  },
  {
    "type": "free_agent",  // could be waiver or trade as well
    "transaction_id": "434890120798142464",
    "status_updated": 1558048393967,
    "status": "complete",
    "settings": null,   // could be {'waiver_bid': 44} if it's FAAB waivers
    "roster_ids": [1],  // roster_ids involved in this transaction
    "metadata": null,   // can contain notes in waivers like why it didn't go through
    "leg": 1,
    "drops": {
      "1736": 1         // player id 1736 dropped from roster_id 1
    },
    "draft_picks": [],
    "creator": "160000000000000000",
    "created": 1558048393967,
    "consenter_ids": [1], // the roster_ids who agreed to this transaction
    "adds": {
      "2315": 1   // player id 2315 added to roster_id 1
      ...
    },
    "waiver_budget": []  // this used for trades only involving FAAB
  },
  ...
]
```

This endpoint retrieves all traded picks in a league, including future picks.

### HTTP Request

`GET https://api.sleeper.app/v1/league/<league_id>/transactions/<round>`

### URL Parameters

Parameter | Description
--------- | -----------
league_id | The ID of the draft to retrieve picks for
round     | The week you want to pull from



## Get traded picks

```shell
curl "https://api.sleeper.app/v1/league/<league_id>/traded_picks"
```

> The above command returns JSON structured like this:

```javascript
[
  {
    "season": "2019",        // which season the pick is for
    "round": 5,              // which round the pick is
    "roster_id": 1,          // roster_id of ORIGINAL owner
    "previous_owner_id": 1,  // roster_id of the previous owner
    "owner_id": 2,           // roster_id of current owner
  },
  {
    "season": "2020",        // which season the pick is for
    "round": 3,              // which round the pick is
    "roster_id": 2,          // roster_id of original owner
    "previous_owner_id": 2,  // roster_id of previous owner
    "owner_id": 1,           // roster_id of current owner
  },
  ...
]
```

This endpoint retrieves all traded picks in a league, including future picks.

### HTTP Request

`GET https://api.sleeper.app/v1/league/<league_id>/traded_picks`

### URL Parameters

Parameter | Description
--------- | -----------
league_id | The ID of the league to retrieve traded picks for