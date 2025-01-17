---
id: overwolf-games
title: overwolf.games API
sidebar_label: overwolf.games
---

Provides information about the currently running game.

## Methods Reference

* [overwolf.games.getRunningGameInfo()](#getrunninggameinfocallback)
* [overwolf.games.getGameInfo()](#getgameinfogameclassid-callback)
* [overwolf.games.getGameDBInfo()](#getgamedbinfogameclassid-callback)
* [overwolf.games.getRecentlyPlayedGames()](#getrecentlyplayedgamesmaxnumofgames-callback)

## Events Reference

* [overwolf.games.onGameInfoUpdated](#ongameinfoupdated)
* [overwolf.games.onGameLaunched](#ongamelaunched)
* [overwolf.games.onMajorFrameRateChange](#onmajorframeratechange)
* [overwolf.games.onGameRendererDetected](#ongamerendererdetected)

## Types Reference

* [GameInfo](#gameinfo-object)
* [GameInfoChangeData](#gameinfochangedata-object)

## getRunningGameInfo(callback)

#### Version added: 0.78 

> Returns an object with information about the currently running game or games, if more than one is running, or returns null if no game is running.

Parameter | Type     | Description                                                              |
----------| -------- | ------------------------------------------------------------------------ |
callback  | function | Called with the currently running [GameInfo](#gameinfo-object) |

#### Callback argument: Success

```json
{
    "isInFocus": true,
    "isRunning": true,
    "allowsVideoCapture": true,
    "title": "Counter-Strike: Global Offensive",
    "id": 77641,
    "width": 1920,
    "height": 1080,
    "logicalWidth": 1920,
    "logicalHeight": 1080,
    "renderers": [
        "D3D9"
    ],
    "detectedRenderer": "D3D9",
    "executionPath": "D://Steam/steamapp/scommon/Counter-Strike Global Offensive/csgo.exe",
    "sessionId": "1a1b96a9d8bb439d8f21abc21faa1184",
    "commandLine": "D://Steam/steamapps/common/Counter-Strike Global Offensive/csgo.exe" -steam -novid +mat_vignette_enable 0"
}
```

#### Usage Example

```javascript
overwolf.games.getRunningGameInfo(function(){console.log(JSON.stringify(arguments))})
```

## getGameInfo(gameClassId,callback)

#### Version added: 0.93 

> Returns information about a game with a given game ID.

**Note**: Game info will be returned only if the game is installed on the local machine.

Parameter   | Type     | Description                                                              |
------------| -------- | ------------------------------------------------------------------------ |
gameClassId | int      | Class ID of the game                                                  |
callback    | function | Returns info about the game                                      |

#### Callback argument: Success

```json
{
    "status": "success",
    "gameInfo": {
        "GameInfoClassID": 7764,
        "GameInfoID": 77641,
        "ProcessPath": "D:SteamSteamAppscommonCounter-Strike Global Offensivecsgo.exe",
        "LauncherPath": "D:Steamsteam.exe",
        "LauncherCommandLineParams": "-applaunch 730",
        "LastTimeVerified": "2016-04-25T06:56:18.180Z",
        "ManuallyAdded": false,
        "WasAutoAddedByProcessDetection": false,
        "GameInfo": {
            "ID": 77641,
            "GameTitle": "Counter-Strike: Global Offensive",
            "DisplayName": "CS: GO",
            "ProcessNames": [
                "SteamApps*Counter-Strike Global Offensivecsgo.exe"
            ],
            "LuancherNames": [
                "steam.exe"
            ],
            "CommandLine": null,
            ...
        }
    }
}
```

## getGameDBInfo(gameClassId,callback)

#### Version added: 0.112 

> Returns information about a game with a given game ID.

:::note
This method is similar to [getGameInfo()](#getgameinfogameclassid-callback) except that it can return two different results:

* If the game is detected as installed, then the `installedGameInfo` member of the result will be set and the `gameInfo` member will be null.
* If the game is NOT detected as installed, then the returned JSON status will be `error`.
:::

Parameter   | Type     | Description                                                              |
------------| -------- | ------------------------------------------------------------------------ |
gameClassId | int      |The class ID of the game                                                  |
callback    | function |Called with the info about the game                                       |

#### Callback argument: Success

```json
{  
   "status":"success",
   "gameInfo":null,
   "installedGameInfo":{  
      "GameInfoClassID":10906,
      "GameInfoID":109062,
      "ProcessPath":"E:/Steam Games/steamapps/common/PUBG/TslGame/Binaries/Win64/TslGame.exe",
      "LauncherPath":"c:/program files (x86)/steam/Steam.exe",
      "LauncherCommandLineParams":"-applaunch 578080",
      "LastTimeVerified":"2018-03-14T12:02:06.686Z",
      "ManuallyAdded":false,
      "WasAutoAddedByProcessDetection":true,
      "GameInfo":{  
         "ID":109062,
         "NativeID":10906,
         "Type":0,
         "LauncherGameClassId":0,
         "GameTitle":"PLAYERUNKNOWN'S BATTLEGROUNDS",
         "ShortTitle":null,
         "DisplayName":"PUBG",
         "ProcessNames":[  
            "TslGame.exe"
         ],
         "LauncherNames":[  
            "Steam.exe"
         ],
         "CommandLine":null,
         "GameRenderers":82,
         "ActualDetectedRenderers":0,
         "FirstGameResolutionHeight":null,
         "FirstGameResolutionWidth":null,
         "GameGenres":"Action_Survival-Horror",
         "InjectionDecision":1,
         "SupportedScheme":null,
         "UnsupportedScheme":"5/1",
         "LauncherDirectoryRegistryKey":"HKEY_LOCAL_MACHINESOFTWAREValveSteamInstallPath",
         "LaunchParams":"-applaunch 578080",
		 ...
      }
   }
}
```
#### Callback argument: Failure

```json
{"status":"error","reason":"game not found"}
```
## getRecentlyPlayedGames(maxNumOfGames, callback)

#### Version added: 0.122 

> Returns an array of the most recently played game IDs. An empty array will be returned if none have been recorded.

Parameter     | Type     | Description                                                                       |
--------------| -------- | --------------------------------------------------------------------------------- |
maxNumOfGames | int      | Maximum number of games to receive. Currently we support a maximum of 3 games |
callback      | function | Called with the array of game IDs                                                 |

#### Callback argument: Success

```json
{  
   "status":"success",
   "games":[  
      54261,
      11361,
      77641
   ]
}
```

## onGameInfoUpdated

> Fired when game info is updated, including game name, game running, game terminated, game changing focus, etc. Passes a [GameInfoChangeData](#gameinfochangedata-object) object.

#### Event data example:

```json
{
    "gameInfo": {
        "isInFocus": true,
        "isRunning": true,
        "allowsVideoCapture": true,
        "title": "Dota 2",
        "id": 73143,
        "width": 1920,
        "height": 1080,
        "logicalWidth": 1920,
        "logicalHeight": 1080,
        "renderers": [
            "D3D9",
            "D3D11"
        ],
        "detectedRenderer": "D3D9",
        "executionPath": "D:/Steam/steamapps/common/dota2/game/bin/win64/dota2.exe",
        "sessionId": "9b163a0c0ca74d2c8f01f85d4fade07f",
        "commandLine": "D:/Steam/steamapps/common/dota2/game/bin/win64/dota2.exe -steam"
    },
    "resolutionChanged": false,
    "focusChanged": true,
    "runningChanged": false,
    "gameChanged": false
}
```

## onGameLaunched

> Fired when a game is launched.

#### Event data example:

```json
{
    "isInFocus": false,
    "isRunning": true,
    "allowsVideoCapture": true,
    "title": "Dota 2",
    "id": 73143,
    "width": 1920,
    "height": 1080,
    "logicalWidth": 1920,
    "logicalHeight": 1080,
    "renderers": [
        "D3D9",
        "D3D11"
    ],
    "detectedRenderer": "Unknown",
    "executionPath": "D:/Steam/steamapps/common/dota2/game/bin/win64/dota2.exe",
    "sessionId": "9b163a0c0ca74d2c8f01f85d4fade07f",
    "commandLine": "D:/Steam/steamapps/common/dota2/game/bin/win64/dota2.exe -steam"
}
```

## onMajorFrameRateChange

> Fired when the rendering frame-rate of the currently injected game changes dramatically.

#### Event data example:

```json
{
    "fps_status": "Increase", // can be “None”, “Stable”, “Drop” and “Increase”.
    "fps": 35
}
```

## onGameRendererDetected

> Fired when the rendering method of the game has been detected.

#### Event data example:

```json
{
    "detectedRenderer": "D3D9"
}
```

## GameInfo object

#### Version added: 0.78 

Contains information about a game.

| Name               | Type     | Description                                                                                         | Since |
|--------------------| ---------|-----------------------------------------------------------------------------------------------------|------ |
| isInFocus          | bool     | Returns whether the game is currently in focus                                                      | 0.78  |
| isRunning          | bool     | Returns whether the game is currently running                                                       | 0.78  |
| allowsVideoCapture | bool     | Returns whether the game allows video to be captured                                                | 0.78  |
| title              | string   | Returns the title of the game                                                                       | 0.78  |
| id                 | int      | Returns the ID of the game                                                                          | 0.78  |
| width              | int      | Returns the pixel width of the game window                                                          | 0.78  |
| height             | int      | Returns the pixel height of the game window                                                         | 0.78  |
| logicalWidth       | int      | Returns the game-reported (logical) pixel width of the game window                                  | 0.78  |
| logicalHeight      | int      | Returns the game-reported (logical) pixel height of the game window                                 | 0.78  |
| renderers          | string[] | Returns an array of the rendering technology names supported by the running game                    | 0.78  |
| detectedRenderer   | string   | Returns the rendering technology detected by the running game                                       | 0.78  |
| commandLine        | string   | Returns the game process commandline                                                                | 0.78  |
| monitorHandle      | object   | Returns the current monitor handle                                                                  | 0.135 |
| windowHandle       | object   | Returns the current app window handle                                                               | 0.135 |

#### Example data

```json
{ 
   "isInFocus":false,
   "isRunning":true,
   "allowsVideoCapture":true,
   "title":"Guild Wars",
   "displayName":"",
   "shortTitle":"",
   "id":11361,
   "classId":1136,
   "width":1920,
   "height":1080,
   "logicalWidth":1920,
   "logicalHeight":1080,
   "renderers":["D3D9"],
   "detectedRenderer":"D3D9",
   "executionPath":"D:/Games/Guild Wars/Gw.exe",
   "sessionId":"96879a3f7545472194ae86eb5a8fd64a",
   "commandLine":"\"D:/Games/Guild Wars/Gw.exe\"",
   "type":0,
   "typeAsString":"Game",
   "windowHandle":{"value":592562},
   "monitorHandle":{"value":329731}
}
```

## GameInfoChangeData object

#### Version added: 0.78 

An object containing the game info object in addition to a set of flags indicating the changes from the last time that data was updated.

| Name               | Type     | Description                                                                                         | Since |
|--------------------| ---------|-----------------------------------------------------------------------------------------------------|------ |
| gameInfo           | [GameInfo](#gameinfo-object) object     | The new game info data                                               | 0.78  |
| resolutionChanged  | bool     | Indicates if there was a change in resolution (i.e. the width or height properties were changed)    | 0.78  |
| focusChanged       | bool     | Indicates if there was a change in the game focus status                                            | 0.78  |
| runningChanged     | bool     | Indicates if there was a change in the game running status                                          | 0.78  |
| gameChanged        | bool     | Indicates if the gameInfo property represents a different game than before                          | 0.78  |
