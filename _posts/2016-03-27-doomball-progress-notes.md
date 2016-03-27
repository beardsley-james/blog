---
layout: post
title: Unit generator progress notes
category: javascript
tags: [doomball, html, games]
---

## Unit Generator

```javascript
var Unit = function(unit) {
	this.race = unit.race; this.name = unit.name;
	
	if (unit.level) {this.level = unit.level} 
	else {this.level = 1}
	
	this.range = setStat(unit, "range");
	this.attack = setStat(unit, "attack");
	this.defense = setStat(unit, "defense");
	this.move = setStat(unit, "move");
	
	if (unit.special) {this.special = unit.special}
	
	this.tokens = [];
	
	this.graphic = unit.graphic;
}
```

This is what I'm working with so far. setStat() is a simple utility function that sets a default stat and handles the availability of special characteristics. I think there's a little bit more logic in here I could rip out but I can roll with this so far. Having defaults values (1 range, 2 attack, 1 defense, and 1 move) means that I can create unit definitions that simply state how they differ from the default instead of typing out each characteristic every time. That feels programmatic. It feels like a good solution.

## Human Units

```json
var humanUnits = {
	"spearmen": {
		"race": "human",
		"name": "Spearmen",
		"special": "Steadfast",
		"graphic": "./images/spearmen.png"	
	},
	"archers": {
		"race": "human",
		"name": "Archers",
		"special": "Pinning",
		"graphic": "./images/archers.png",
		"range": {
			"value": 2
		},
		"move": {
			"special": true
		}
	},
	"horsemen": {
		"race": "human",
		"name": "Horsemen",
		"special": "Overrun",
		"graphic": "./images/horsemen.png",
		"defense": {
			"special": true
		},
		"move": {
			"value": 2
		}
	},
...
```

There's four more like this, some more or less complicated, works out fine. I have another function that makes HTML strings that display these as the blocks I previewed in the last post, feels good. Have to throw together some transparent unit graphics and then get started on the next army I think - having functions that can display each faction with nothing more than a change in JSON archive is central to the design concept I'm working with here.

## What's next

- I need to make sure that it changes the background image based on the faction. In the original design for the game each faction had a specific and different background image. I don't know if it's something I'm going to stick with but it's something I want to at least work into the spec. I'm thinking each will have a specific class to throw onto the divs with a different background image - .unit-human, .unit-orc, .unit-hive, that sort of thing.

- I'm still thinking about how to display these suckers responsively and how to give them a nice hex grid to get thrown onto. I think I can set up the actual display on the board with some judicious div use and a .staggered class that pops everything over 100 pixels. Getting the hexes to lock into each other will be tough, though. Have to figure out the right size to make them so that they can have the pieces on top and you can still see what the space is underneath. Each is going to have to be identifiable from its margins.

- Haven't even started on the game logic yet.

- The tokens could be part of the tile generation. Throw some conditional .divs into the package and make sure they display on different places on the tile - the whole of the inside is claimable territory for tokens, but you wouldn't want them to overlap by any means.