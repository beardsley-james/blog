---
layout: post
title: Doomball&colon; the Genesis
category: javascript
tags: [doomball, javascript, games]
---

## This game used to be called Artifact War

![Hive Warriors]({{ site.baseurl }}/public/images/hive_warriors.png){: .float-right height="150px"}

I made a board game last year, loosely based on American football, where two armies of fantasy races try to snag an artifact in the middle and run it past the opponent's side of the board. I wrote up some rules, I wrote down some pseudocode logic because I wanted to turn it into a computer game, I made up some nine different races and hand drew the armies for them, I made custom pixel art to represent the pieces, I drew up templates and started researching how to be better at pixel art so that I could make it look better - I guess I kind of got into it.

Then I stepped away.

I haven't sat down with this project for like a year, it was a fun one too. Now I think I'm going to try to leave my dream and turn my weird little board game into a computer game.

Tonight I started thinking about the constructors I'm going to need.

```javascript
var Unit = function() {
	this.race = "string"; 
	this.name = "string";
	this.id = 0;
	this.level = 1;
	
	this.range = {
		"value": 1,
		"special": false
	};
	
	this.attack = {
		"value": 2,
		"special": false
	};
	
	this.defense = {
		"value": 1,
		"special": false
	};
	
	this.move = {
		"value": 1,
		"special": false
	};
	
	this.special = "string";
	this.tokens = [];
	
	this.url = "string"
}

// Special abilities: Steadfast, Pinning, Overrun, Armor Piercing, Charging, Explosive, Cowardly, Leadership
```

This is going to have to be some kind of construction function, possibly taking an object as an argument and filling in default values if not specified, so parts will have to be replaced with more useful defaults. This might be a good place to add some	prototype actions to let the characters move on the field.

```javascript
var Space = function(){
	this.x = 0;
	this.y = 0;
	this.terrain = "Plains"
}
```

I'm probably going to want to structure this so that it can be used in a gameboard constructing function, so the arguments are going to have to be like (x, y, terrain) and then the terrain will probably be a one letter thing so that I can specify maps pretty easily.

```javascript
var Token = function(){
	this.name = "string";
	this.unique = true;

	this.url = "string"
}
```

Was considering adding an x, y locator object and an owner object but I don't know now, since I'm probably just going to push tokens into an array on the individual units anyway. Seems like the easier way to	do it. Maybe add a prototype .effect() function that checks the string and then applies the appropriate effect to the character.
	
A lot is going to have to happen in the game logic, though, with various functions checking for the presence of certain tokens and then applying different effects as a matter of course. Some tokens will also be looking for the presence of other tokens, and I'm not sure how to do that.