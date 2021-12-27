# steam-db
## :calendar: last update : __dec. 26, 2021__
steam-db is a skimmed data dump of the [Steam](https://store.steampowered.com/) products.  *It doesn't include soundtracks, films, and some outlier products type are omitted as well.*  

It is meant to fuel the steam-game-finder web-app & browser extension, but since all the data is publicly accessible I made it available.

# Fetching individual app data
Note that while you should not point directly to this repo to fetch data, a copy of it is cached in github pages :
```js
`https://nebukam.github.io/steam-db/app/${appid}/infos.json`
```

### Shout-out to Co-optimus
__A bit short of 2500 products info include data fetched from [Co-optimus](https://www.co-optimus.com/), namely the known number of players allowed in different game-modes and some others goodies.__  
A massive thank you to their team, without which the Steam game finder app would have much less immediate value as a tool to find relevant multiplayer games within a group of friends :)

---

# Repo content

The git is split in three main data bits :
## [applist.json](https://github.com/Nebukam/steam-db/blob/main/applist.json)
Is a direct dump of the steam API call `http://api.steampowered.com/ISteamApps/GetAppList/v0002/?key=API_KEY&format=json` at the time of update.
  
## [db.json](https://github.com/Nebukam/steam-db/blob/main/db.json)
Is the whole database in a single rather huge file, formatted as follow :
```js
{
    "appid":{
        // app data
    }
}
```
Each entry is what you can otherwise be individually found through `app/appid/infos.json`
  
## [Individual app infos](https://github.com/Nebukam/steam-db/tree/main/app)
Each file contains some skimmed game infos in the following format:
```js
{
    // Steam app ID
    "appid": 359550,
    // Game verbose title
    "name": "Tom Clancy's Rainbow Six Siege", 
    // Parent appid if DLC, otherwise empty string
    "parentappid": "", 
    // Features flags
    "flags": [2,36,38,29,35,18,41,42,1,9,20], 
    // App tags
    "tags": [ 
        "FPS",
        "Hero Shooter",
        "Multiplayer",
        "Tactical",
        "Shooter",
        "Team-Based",
        "Action",
        "First-Person",
        "Competitive",
        "Co-op",
        "Strategy",
        "Realistic",
        "Online Co-Op",
        "Destruction",
        "Physics",
        "Atmospheric",
        "Singleplayer",
        "Massively Multiplayer",
        "Casual",
        "Simulation"
    ],
    // Co-optimus data (false if couldn't be found)
    "cooptimus": { 
        "url": "https://www.co-optimus.com/game/3480/PC/tom-clancy-s-rainbow-six-siege.html",
        // Max nmber of players in local play
        "local": "0", 
        // Max number of players in online play
        "online": "5", 
        // Max number of players in lan
        "lan": "0", 
        // Support splitscreen
        "splitscreen": "0", 
        // Support drop-in drop-out
        "dropindropout": "0", 
        // Support coop campaign
        "campaign": "0", 
        // List of notable features
        "featurelist": [ 
            "Co-Op Modes"
        ]
    }
}
```

The flag list matches the following map  
*(they're the most common flags I've gathered)* :
> :warning: Some flag are inconsistently used by steam admin and are marked as such. (e.g the absence of such flag doesn't mean the game doesn't have the related features. i.e CS:GO is not flagged with any multiplayer features.)   
*I try to flag games based on existing tags as a fail safe, but this is not a rock-solid method.*

```js
[
    { flag: 21, id: `dlc` },
    // Unreliable
    { flag: 1,  id: `multiplayer` },
    { flag: 2,  id: `single_player` },
    // Unreliable
    { flag: 49, id: `pvp` },
    // Unreliable
    { flag: 9,  id: `coop` }, 
    { flag: 20, id: `mmo` },
    { flag: 36, id: `online_pvp` },
    { flag: 38, id: `online_coop` },
    { flag: 47, id: `lan_pvp` },
    { flag: 48, id: `lan_coop` },
    { flag: 37, id: `shared_split_pvp` },
    { flag: 39, id: `shared_split_coop` },
    { flag: 27, id: `cross_platform_mp` },
    { flag: 29, id: `trading_cards` },
    { flag: 35, id: `in_app_purchase` },
    { flag: 18, id: `partial_controller_support` },
    { flag: 28, id: `full_controller_support` },
    { flag: 22, id: `achievements` },
    { flag: 22, id: `steam_cloud` },
    { flag: 13, id: `captions` },
    { flag: 42, id: `remote_play_tablet` },
    { flag: 43, id: `remote_play_tv` },
    { flag: 44, id: `remote_play_together` },
    { flag: 30, id: `steam_workshop` },
    { flag: 32, id: `steam_turn_notification` },
    // A few more, unlisted
]
```
---
# Some statistics

### Steam

Total number of products : `132959`  

Number of games with tags : `117410`  

Total number of unique tags : `426` [full list :eye_speech_bubble:](https://github.com/Nebukam/steam-db/blob/main/tags.json)

Number of games with flags : `119194`  
Unique flags : `1,10,13,14,15,16,17,18,18,19,2,2,20,20,21,22,22,23,23,25,25,27,28,28,29,29,30,32,35,35,36,36,37,37,38,38,39,40,41,42,43,44,47,47,48,49,50,6,8,9,990,992,993,994`

Number of games with errors : `11`  
<sup><sup>*(When the script failed to fetch a unique appid data)*</sup></sup>

### Co-optimus

Number of games with co-optimus data : `2287`  

Local player count values : `0,1,2,3,4,5,6,7,8,9,10,12`

Online player count values : `0,2,3,4,5,6,7,8,9,10,11,12,14,16,20,24,26,30,32,35,64,100,255,500`

LAN player count values : `0,2,3,4,5,6,7,8,10,11,12,14,16,20,24,30,32,35,64,255,256,500`

