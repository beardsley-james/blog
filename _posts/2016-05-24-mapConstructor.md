---
layout: post
title: Map Construction and Savegame Structure, Alpha Release
category: doomball
tags: [doomball, javascript, games]
---

## mapConstructor(attacker, defender)

This is a function that takes as its input the names of the two sides, an attacker and defender, and outputs a renderable game object that pits the two sides against each other. I need to revise it, though, so that it takes a different sort of object so that I can use it to load save games and attach the right prototype functions to the different object types, and I also need to write a function to strip certain information out of the game state and turn it into an object that can be passed into the constructor.

I like this one, I think it's tidy and does what it's supposed to, though I might prefer to iterate through the two lists and cut five or six lines out of the thing.

~~~javascript
var mapConstructor = function(attacker, defender){
	var attArmy = armyList[attacker]["attacker"];
	var defArmy = armyList[defender]["defender"];
	var map = defArmy["map"].concat(attArmy.map);
	var board = new Map(map);
	attArmy["army"].forEach(function(item){
		var unit = item.split(" ");
		var type = unit[0];
		var y = unit[1];
		var x = unit[2];
		board.spaces[y][x].contains = new Unit(units[attacker][type]);
		board.spaces[y][x].contains.player = "player1"
	});
	defArmy["army"].forEach(function(item){
		var unit = item.split(" ");
		var type = unit[0];
		var y = unit[1];
		var x = unit[2];
		
		board.spaces[y][x].contains = new Unit(units[defender][type]);
		board.spaces[y][x].contains.player = "player2"
	});
	return board
}
~~~

This is the format in `units.js`, which puts all the army lists from the separate files into one big object that contains all the different armies. So far there are six, because that's as far as I got with my art assets.

~~~json
"undead": {
	"attacker": {
		"map": [
			"^.....",
			"^^..=.",
			"^.....",
			"......"],
		"army": [
			"ghosts 5 2",
			"ghosts 5 3",
			"ghosts 5 4",
			"ghosts 5 5"...]
	},
	"defender": {
		"map": [
			"......",
			"#....#",
			"^#..#^",
			"^.##.^"],
		"army": [
			"zombies 2 1",
			"zombies 2 2",
			"zombies 2 3",
			"zombies 2 4"...]
	}
}
~~~

I've also got the turn order mechanic working, I'll write that up in a future post. It's a little sloppy but it seems to work out so far. You can run a simple match between two sides, but the game objective isn't in place yet and half the special abilities don't do anything so plenty of work to do there.

That said, I plan on releasing the current build as 0.0.1 since it is playable. Super alpha but a release nonetheless.