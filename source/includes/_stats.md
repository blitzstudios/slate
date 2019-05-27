# Stats

## Stats and Projections

```shell
curl "https://api.sleeper.app/v1/stats/nfl/regular/2018"
curl "https://api.sleeper.app/v1/stats/nfl/regular/2018/1"
curl "https://api.sleeper.app/v1/projections/nfl/regular/2018"
curl "https://api.sleeper.app/v1/projections/nfl/regular/2018/1"
```

> The above commands return JSON structured like this:

```javascript
{
  "1001": { /* player_id */
    "xpm": 2.7,
    "xpa": 2.7,
    "pts_std": 7.17,
    "pts_ppr": 7.17,
    "pts_half_ppr": 7.2,
    "gs": 1,
    "gp": 1,
    "gms_active": 1,
    "fgmiss": 0.2,
    "fgm_yds_over_30": 12,
    "fgm_yds": 42,
    "fgm_pct": 100,
    "fgm_50p": 0.22,
    "fgm_40_49": 0.52,
    "fgm_30_39": 0.53,
    "fgm_20_29": 0.49,
    "fgm_0_19": 0.01,
    "fgm": 1.8,
    "fga": 2
  },
  "MIA": {  /* player_id */
    "rush_ypa": 4.48,
    "rush_yd": 22.77,
    "rush_td": 0.12,
    "rush_att": 5.66,
    "pts_std": 16.85,
    "pts_ppr": 16.85,
    "pts_half_ppr": 16.9,
    "pass_ypc": 9.41,
    "pass_ypa": 6.05,
    "pass_yd": 216.97,
    "pass_td_40p": 1,
    "pass_td": 1.85,
    "pass_rtg": 92.13,
    "pass_int": 0.7,
    "pass_inc": 10.75,
    "pass_fd": 8,
    "pass_cmp_40p": 2,
    "pass_cmp": 19.32,
    "pass_att": 30.07,
    "gs": 1,
    "gp": 1,
    "gms_active": 1,
    "fum_lost": 0.16,
    "fum": 0.16,
    "cmp_pct": 63.9
  },
  ...
```

<aside class="notice">
If you are using these stats for commercial purposes, please contact [sportsdata.io](https://sportsdata.io) regarding pricing.
</aside>

The following endpoints return season and weekly stats as well as projections.  

The result is a map of `player_id` to stat maps.

### HTTP Request

`GET https://api.sleeper.app/v1/stats/<sport>/<season_type>/<season>`

`GET https://api.sleeper.app/v1/stats/<sport>/<season_type>/<season>/<week>`

`GET https://api.sleeper.app/v1/projections/<sport>/<season_type>/<season>`

`GET https://api.sleeper.app/v1/projections/<sport>/<season_type>/<season>/<week>`

### URL Parameters

Parameter   | Description
---------   | -----------
sport       | We only support "nfl" right now.
season_type | `regular`, `pre`, `post` are supported
season      | Season can be 2017, 2018, etc...
week        | Week can be 1, 2, 3, etc.
