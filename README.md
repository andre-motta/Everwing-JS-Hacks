# Everwing-Hacks
Hacks for the everwing game

## Apply the hacks
To apply the hacks you have to open the developer console of your browser.
To do that:
 - Click F12 on the everwing game page (or, right click the page and select "inspect element")
 - Click the "Console" tab if you are not already there
 - Click the down arrow next to the "top"
 - On the drop down, sellect "index.html" (it should be on the bottom)

## Hack Codes
Now paste any of the codes bollow to hack the game.

### Unlock All Players

```javascript
var names = ["fiona", "sophia", "coin", "magnet", "lenore", "jade", "arcana"];
for (var i = 0; i < names.length; i++) {
  if(GC.app.mvc.models.CharactersModel.characters[names[i]].state == "locked")
    GC.app.client.runFunction("unlockCharacter",{characterName: names[i], isFree: true});
}
```

### Get a sidekick

Get a random sidekick
```javascript
var types = ["smart", "common", "bronze", "silver", "gold", "magical", "legendary", "bossraid"];
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : types[Math.floor(Math.random() * types.length)]});
```

Get a smart sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "smart"});
```

Get a common sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "common"});
```

Get a bronze sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "bronze"});
```

Get a silver sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "silver"});
```

Get a gold sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "gold"});
```

Get a magical sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "magical"});
```

Get a legendary sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "legendary"});
```

Get a bossraid sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "bossraid"});
```

### Get Energy

First apply this function
```javascript
var getFreeEnergy = function(x){
  if(GC.app.client.schemaManager.models[17]._frozen)
    GC.app.client.schemaManager.models[17]._frozen = false;
  if (GC.app.client.schemaAPI.getTable("raidEnergyShop").rows.length == 6) {
    GC.app.client.schemaManager.models[17].rows = JSON.parse(JSON.stringify(GC.app.client.schemaManager.models[17].rows));
    for(var i = 0; i < GC.app.client.schemaManager.models[17].rows.length; i++){
      if(GC.app.client.schemaManager.models[17].rows[i].count == x)
        break;
    }
    GC.app.client.schemaManager.models[17].rows.splice(i, 0, {
      "id" : "item-free",
      "icon" : "resources/images/game/base/item_energy.png",
      "count" : x,
      "cost" : 0,
      "currency" : "trophies",
      "bonus" : 0
    });
  } else {
    GC.app.client.schemaAPI.getTable("raidEnergyShop").getRow("item-free").count = x;
  }
  GC.app.mvc.sendNotification("PurchaseEnergyCommand",{id: "item-free"});
}
```
Then call it with any ammount you want, for example, if you want 10 energy, write
```javascript
getFreeEnergy(10);
```

### Fake a game run

First apply this function
```javascript
var playFakeGame = function(data) {
	// Fake game data
	var data = data || {};
	data.score = data.score || 10 + Math.round(Math.random()*10);
	data.seconds = data.seconds || 10 + Math.round(Math.random()*10);
	data.coins = data.coins || 0;
	data.trophies = data.trophies || 0;
	data.energy = data.energy || 0;
	data.xp = data.xp || 0;
	data.sidekick_xp = data.sidekick_xp || 0;
	// Get sidekicks
	var sidekicks = {};
	var sidekicks_db = window.GC.app.gameView.sidekicksModel.sidekicksList;
	for(var i=0; i<sidekicks_db.length; i++){
		if(sidekicks_db[i].state == "equippedLeft"){sidekicks.left = sidekicks_db[i];}
		else if(sidekicks_db[i].state == "equippedRight"){sidekicks.right = sidekicks_db[i];}
	}
	// App reference
	var app = window.GC.app;
	// Send command
	app.mvc.commandMap.GamePlayedCommand.prototype.execute.apply({mvc :app.mvc,finishCommand : function(e, $){}},
	[{
		playerID : app.gameModel.player.id,
		secondsElapsed : data.seconds,
		killedBy : "Meteor SINGLE " + (Math.round(Math.random()*3) + 1),
		background : "ocean",
		score : data.score,
		commonEarned : data.coins,
		premiumEarned : data.trophies,
		energyEarned : data.energy,
		playerXP : data.xp,
		sidekickXP : data.sidekick_xp,
		sidekickLeftID : (sidekicks.left) ? sidekicks.left.id : null,
		sidekickRightID : (sidekicks.right) ? sidekicks.right.id : null,
	}]);
}
```

Then call it with the amount of resources you need.

Get 15.000 coints
```javascript
playFakeGame({coins : 15000});
```
Get 1.500 trophies
```javascript
playFakeGame({trophies : 1500});
```
Get 9.999 player XP points
```javascript
playFakeGame({xp : 9999});
```
Get 9.999 sideckick XP points
```javascript
playFakeGame({sidekick_xp : 9999});
```
