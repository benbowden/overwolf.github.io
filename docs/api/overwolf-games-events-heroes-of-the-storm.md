---
id: overwolf-games-events-hots
title: Heroes of the Storm Game Events
sidebar_label: Heroes of the Storm
---

Please read the [overwolf.games.events](overwolf-games-events) documentation page to learn how to use Overwolf game events.

:::important Game ID
10624
:::

## Sample Apps
* [HOTS game events sample app](https://github.com/overwolf/events-sample-apps)

## Available Features

* [match_info](#match_info)
* [me](#me)
* [game_info](#game_info)
* [roster](#roster)
* [death](#death)
* [kill](#kill)

## Game events status

It's highly recommended to communicate errors and warnings to your app users. Check game event status [here](../status/all) or easily check game event status from your app [using our API](../topics/howto-check-events-status-from-app).

## `me`

### Info Updates

key          | Category    | Values                    | Notes                 | Since GEP Ver. |
------------ | ------------| ------------------------- | --------------------- | ------------- | 
battletag    | me          | Battletag of local player | See [notes](#battletag-note)|    134.0|

#### *battletag* note

Data Example:

```json
{"feature":"me", "category":"me", "key":"battletag", "value":"Shargaas#2430"}
```

## `match_info`

### Info Updates

key          | Category    | Values                    | Notes                 | Since GEP Ver. |
------------ | ------------| ------------------------- | --------------------- | ------------- | 
pseudo_match_id| match_info| Current session’s ID code. | See [notes](#pseudo_match_id-note)|  134.0  |
teams_level  | match_info  | Current level of both teams| See [notes](#teams_level-note)|  134.0  |
score        | match_info  | Current kill-score of both teams. | See [notes](#score-note)|  134.0  |
match_state  | match_info  | Is a match in progress - true/false. | See [notes](#match_state-note)|  134.0  |

### Events

Event  | Event Data        | Fired When   | Notes      | Since GEP Ver. |
-------| ------------------| -------------| ---------- | --------------|
match_start| null          | Match starts |See [notes](#match_start-note)|    134.0      |
match_end  | victory/defeat| Match ends   |See [notes](#match_end-note)|    134.0      |
talent_available  | null | A skill point is available for use.  |See [notes](#talent_available-note)|    134.0      |
gates_opened  | null | When pregame preparation countdown has ended and the match begins.  |See [notes](#gates_opened-note)|    134.0      |

#### *pseudo_match_id* note

The reason that pseudo_match_id is different for each player is that its internal Overwolf info that created for highlights recording capabilities. You should not use it to determine that individual players are playing in the same match. For that, you should use the [roster](#roster) info.

Data Example:

```json
{"info":{"match_info":{"pseudo_match_id":"055accd3-5948-4444-903a-12400d484d4b"}}, "feature":"match_info"}
```

#### *teams_level* note:

Data Example:

```json
{"info":{"match_info":{"teams_level":{"order":1, "chaos":1}}}, "feature":"match_info"}
```

#### *score* note:

Data Example:

```json
{"info":{"match_info":{"score":{"order":8, "chaos":19}}}, "feature":"match_info"}
```

#### *match_state* note:

Data Example:

```json
{"info":{"match_info":{"match_state":{"in_progress":true}}}, "feature":"match_info"}
```

##### *match_start* note:

Data Example:

```json
{"events":[{"name":"match_start", "data":""}]}
```

##### *match_end* note:

Data Example:

```json
{"events":[{"name":"match_end", "data":"victory"}]}
```

#### *talent_available* note:

Data Example:

```json
{"events":[{"name":"talent_available", "data":""}]}
```

#### *gates_opened* note:

Data Example:

```json
{"events":[{"name":"gates_opened", "data":""}]}
```

## `game_info`

### Info Updates

key          | Category    | Values                    | Notes                 | Since GEP Ver. |
------------ | ------------| ------------------------- | --------------------- | ------------- | 
scene        | game_info   | Current menu state    | See [notes](#scene-note)|    134.0    |

#### *scene* note:

Data Examples:

```json
{"info":{"game_info":{"scene":"loading_screen"}},"feature":"game_info"}
{"info":{"game_info":{"scene":"hero_select"}}, "feature":"game_info"}
{"info":{"game_info":{"scene":"unranked_preparing"}}, "feature":"game_info"}
{"info":{"game_info":{"scene":"collection"}}, "feature":"game_info"}
{"info":{"game_info":{"scene":"home"}}, "feature":"game_info"}
{"info":{"game_info":{"scene":"unranked_preparing"}}, "feature":"game_info"}
```

## `roster`

### Info Updates

key          | Category    | Values                    | Notes                 | Since GEP Ver. |
------------ | ------------| ------------------------- | --------------------- | ------------- | 
roster       | game_info   | Full player roster   | See [notes](#roster-note)|    134.0    |

#### *roster* note:

Provided data:

* player_level
* battletag
* if local = true/false
* team - chaos/order
* hero_name

Data Example:

```json
{ 
   "info":{ 
      "roster":{ 
         "roster":"{"Cerese":{ 
            "player_name":"Cerese",
            "battletag":"Cerese#2249",
            "player_level":"811",
            "hero_name":"Ana",
            "local":false,
            "team":"order"
         },
         "DREADr":{ 
            "player_name":"DREADr",
            "battletag":"DREADr#2716",
            "player_level":"1001",
            "hero_name":"Falstad",
            "local":false,
            "team":"chaos"
         },
         "Devastator":{ 
            "player_name":"Devastator",
            "battletag":"Devastator#22538",
            "player_level":"454",
            "hero_name":"Valla",
            "local":false,
            "team":"order"
         },
         "Hostik":{ 
            "player_name":"Hostik",
            "battletag":"Hostik#2133",
            "player_level":"975",
            "hero_name":"Abathur",
            "local":false,
            "team":"order"
         },
         "Kafei":{ 
            "player_name":"Kafei",
            "battletag":"Kafei#2771",
            "player_level":"250",
            "hero_name":"Nova",
            "local":false,
            "team":"order"
         },
         "Monomax":{ 
            "player_name":"Monomax",
            "battletag":"Monomax#2130",
            "player_level":"813",
            "hero_name":"Artanis",
            "local":false,
            "team":"chaos"
         },
         "SouthernUral":{ 
            "player_name":"SouthernUral",
            "battletag":"SouthernUral#2738",
            "player_level":"1379",
            "hero_name":"Rehgar",
            "local":false,
            "team":"chaos"
         },
         "ladyboner":{ 
            "player_name":"ladyboner",
            "battletag":"ladyboner#2168",
            "player_level":"519",
            "hero_name":"Zarya",
            "local":false,
            "team":"chaos"
         },
         "moustacho":{ 
            "player_name":"moustacho",
            "battletag":"moustacho#21261",
            "player_level":"264",
            "hero_name":"Imperius",
            "local":false,
            "team":"order"
         },
         "?????????":{ 
            "player_name":"?????????",
            "battletag":"?????????#2698",
            "player_level":"40",
            "hero_name":"Butcher",
            "local":true,
            "team":"chaos"
         }
      }      "
    }
  },
  "      feature":"roster"
   }
```

## `kill`

### Events

Event  | Event Data        | Fired When   | Notes      | Since GEP Ver. |
-------| ------------------| -------------| ---------- | --------------|
kill   | null              | Local player kills an opponent. |See [notes](#kill-note)|    134.0      |
assist | null              | Local player takes part in the killing of an opponent. |See [notes](#assist-note)|    134.0      |
minion_kill| null          | Local player kills a minion. |See [notes](#minion_kill-note)|    134.0      |
takedown| null             | Local player kills an opponent. |See [notes](#takedown-note)|    134.0      |


#### *kill* note:

Data Example:

```json
{"events":[{"name":"kill", "data":""}]}
```

#### *assist* note:

Data Example:

```json
{"events":[{"name":"assist", "data":""}]}
```

#### *minion_kill* note:

Data Example:

```json
{"events":[{"name":"minion_kill", "data":""}]}
```

#### *takedown* note:

Data Example:

```json
{"events":[{"name":"takedown" ,"data":""}]}
```

## `death`

### Events

Event  | Event Data        | Fired When   | Notes      | Since GEP Ver. |
-------| ------------------| -------------| ---------- | --------------|
death  | null              | Local player dies. |See [notes](#death-note)|    134.0      |

#### *death* note:

Data Example:

```json
{"events":[{"name":"death", "data":""}]}
```
