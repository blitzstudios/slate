# Drafts

## Get all drafts for user

```shell
curl "https://api.sleeper.app/v1/user/<user_id>/drafts/nfl/2018"
```

> The above command returns JSON structured like this:

```javascript
[
  {
    "type": "snake",
    "status": "complete",
    "start_time": 1515700800000,
    "sport": "nfl",
    "settings": {
      "teams": 6,
      "slots_wr": 2,
      "slots_te": 1,
      "slots_rb": 2,
      "slots_qb": 1,
      "slots_k": 1,
      "slots_flex": 2,
      "slots_def": 1,
      "slots_bn": 5,
      "rounds": 15,
      "pick_timer": 120
    },
    "season_type": "regular",
    "season": "2017",
    "metadata": {
      "scoring_type": "ppr",
      "name": "My Dynasty",
      "description": ""
    },
    "league_id": "257270637750382592",
    "last_picked": 1515700871182,
    "last_message_time": 1515700942674,
    "last_message_id": "257272036450111488",
    "draft_order": null,
    "draft_id": "257270643320426496",
    "creators": null,
    "created": 1515700610526
  },
  ...
]
```

This endpoint retrieves all drafts by a user.

### HTTP Request

`GET https://api.sleeper.app/v1/user/<user_id>/drafts/<sport>/<season>`

### URL Parameters

Parameter | Description
--------- | -----------
user_id   | The numerical ID of the user.
sport     | We only support "nfl" right now.
season    | Season can be 2017, 2018, etc...



## Get all drafts for a league

```shell
curl "https://api.sleeper.app/v1/league/<league_id>/drafts"
```

> The above command returns JSON structured like this:

```javascript
[
  {
    "type": "snake",
    "status": "complete",
    "start_time": 1515700800000,
    "sport": "nfl",
    "settings": {
      "teams": 6,
      "slots_wr": 2,
      "slots_te": 1,
      "slots_rb": 2,
      "slots_qb": 1,
      "slots_k": 1,
      "slots_flex": 2,
      "slots_def": 1,
      "slots_bn": 5,
      "rounds": 15,
      "pick_timer": 120
    },
    "season_type": "regular",
    "season": "2017",
    "metadata": {
      "scoring_type": "ppr",
      "name": "My Dynasty",
      "description": ""
    },
    "league_id": "257270637750382592",
    "last_picked": 1515700871182,
    "last_message_time": 1515700942674,
    "last_message_id": "257272036450111488",
    "draft_order": null,
    "draft_id": "257270643320426496",
    "creators": null,
    "created": 1515700610526
  },
  ...
]
```

This endpoint retrieves all drafts for a league.  Keep in mind that a league can have multiple drafts, especially dynasty leagues.  

Drafts are sorted by most recent to earliest.  Most leagues should only have one draft.

### HTTP Request

`GET https://api.sleeper.app/v1/league/<league_id>/drafts`

### URL Parameters

Parameter | Description
--------- | -----------
league_id | The ID of the league for which you are trying to retrieve drafts.


## Get a specific draft

```shell
curl "https://api.sleeper.app/v1/draft/<draft_id>"
```

> The above command returns JSON structured like this:

```javascript
{
  "type": "snake",
  "status": "complete",
  "start_time": 1515700800000,
  "sport": "nfl",
  "settings": {
    "teams": 6,
    "slots_wr": 2,
    "slots_te": 1,
    "slots_rb": 2,
    "slots_qb": 1,
    "slots_k": 1,
    "slots_flex": 2,
    "slots_def": 1,
    "slots_bn": 5,
    "rounds": 15,
    "pick_timer": 120
  },
  "season_type": "regular",
  "season": "2017",
  "metadata": {
    "scoring_type": "ppr",
    "name": "My Dynasty",
    "description": ""
  },
  "league_id": "257270637750382592",
  "last_picked": 1515700871182,
  "last_message_time": 1515700942674,
  "last_message_id": "257272036450111488",

  // this is the user_id to draft slot mapping
  "draft_order": {
    "12345678": 1,
    "23434332": 2,
    ...
  },

  // this is the draft slot to roster_id mapping
  // leagues have rosters, which have roster_ids
  // this means draft slot 1 (column 1) will go to roster 10, slot 2 will go to roster_id 3, etc
  "slot_to_roster_id": {
    "1": 10,
    "2": 3,
    "3": 5
  },

  "draft_id": "257270643320426496",
  "creators": null,
  "created": 1515700610526
}
```

This endpoint retrieves a specific draft.

### HTTP Request

`GET https://api.sleeper.app/v1/draft/<draft_id>`

### URL Parameters

Parameter | Description
--------- | -----------
draft_id  | The ID of the draft to retrieve




## Get all picks in a draft

```shell
curl "https://api.sleeper.app/v1/draft/<draft_id>/picks"
```

> The above command returns JSON structured like this:

```javascript
[
  {
    "player_id": "2391",
    "picked_by": "234343434", // user_id this pick will go to (not all leagues have users in every slot, this can be "")
    "roster_id": "1", // roster_id this pick will go to
    "round": 5,
    "draft_slot": 5, // which column this is on the draftboard
    "pick_no": 1,
    "metadata": {
      "team": "ARI",
      "status": "Injured Reserve",
      "sport": "nfl",
      "position": "RB",
      "player_id": "2391",
      "number": "31",
      "news_updated": "1513007102037",
      "last_name": "Johnson",
      "injury_status": "Out",
      "first_name": "David"
    },
    "is_keeper": null,
    "draft_id": "257270643320426496"
  },
  {
    "player_id": "1408",
    "picked_by": "234343434", // user_id this pick will go to (not all leagues have users in every slot, this can be "")
    "roster_id": "1", // roster_id this pick will go to
    "round": 5,
    "draft_slot": 6,
    "pick_no": 2,
    "metadata": {
      "team": "PIT",
      "status": "Active",
      "sport": "nfl",
      "position": "RB",
      "player_id": "1408",
      "number": "26",
      "news_updated": "1515698101257",
      "last_name": "Bell",
      "injury_status": "",
      "first_name": "Le'Veon"
    },
    "is_keeper": null,
    "draft_id": "257270643320426496"
  },
  {
    "player_id": "536",
    "picked_by": "667279356739584",
    "pick_no": 3,
    "metadata": {
      "team": "PIT",
      "status": "Active",
      "sport": "nfl",
      "position": "WR",
      "player_id": "536",
      "number": "84",
      "news_updated": "1515673801292",
      "last_name": "Brown",
      "injury_status": "Probable",
      "first_name": "Antonio"
    },
    "is_keeper": null,
    "draft_id": "257270643320426496"
  },
  ...
]
```

This endpoint retrieves all picks in a draft.

### HTTP Request

`GET https://api.sleeper.app/v1/draft/<draft_id>/picks`

### URL Parameters

Parameter | Description
--------- | -----------
draft_id  | The ID of the draft to retrieve picks for



## Get traded picks in a draft

```shell
curl "https://api.sleeper.app/v1/draft/<draft_id>/traded_picks"
```

> The above command returns JSON structured like this:

```javascript
[
  {
    "season": "2019",
    "round": 5,              // which round the pick is
    "roster_id": 1,          // roster_id of ORIGINAL owner
    "previous_owner_id": 1,  // roster_id of the previous owner
    "owner_id": 2,           // roster_id of current owner
  },
  {
    "season": "2019",
    "round": 3,              // which round the pick is
    "roster_id": 2,          // roster_id of original owner
    "previous_owner_id": 2,  // roster_id of previous owner
    "owner_id": 1,           // roster_id of current owner
  },
  ...
]
```

This endpoint retrieves all traded picks in a draft.

### HTTP Request

`GET https://api.sleeper.app/v1/draft/<draft_id>/traded_picks`

### URL Parameters

Parameter | Description
--------- | -----------
draft_id  | The ID of the draft to retrieve picks for
