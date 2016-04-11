---
layout: post
title: Map.prototype.availableTargets & Friends
category: doomball
tags: [doomball, javascript, games]
---


![Sample Attack Range]({{ site.baseurl }}/public/images/doomball-attack-range.png){: .float-left width="30%"}

A major part of the Doomball project is the ability to attack enemy units. This is a pretty big part of a lot of games, of course, and I guess I could have just stripped something out of someone else's game but how boring is that, right?

In Doomball a lot of pieces have a range of greater than 1, so it can't just be adjacent spaces, and then terrain effects the range measurements too. A unit on a hill can fire over friendly units, you can fire at a unit in a forest, but you can't draw line of site through a forest. You can't fire through mountains at all. So I started with the most complicated and important function, ~Map.prototype.spacesInRangeOf(y,x)~, which returns a set of objects representing the spaces that are in range of the originating unit, taking into account the unit's range and the properties of both the terrain it's on and the terrain between itself and the spaces.

~~~javascript
Map.prototype.spacesInRangeOf = function(y, x){
  var space = this.spaces[y][x];
    if (space.contains){
      var spacesInRange = [space];
      var range = space.contains.range.value;
      var elevated = space.isElevated();
      var showStoppers = [];
      while (range > 0) {
        var nextRing = spacesInRange.forEach(function(tempSpace){
          var adjacentSpaces = this.adjacentSpaces(tempSpace.y, tempSpace.x);
          adjacentSpaces.forEach(function(candidate){
            if (spacesInRange.indexOf(candidate) == -1) {
              if (candidate.terrain.dropsLOS) {
                showStoppers.push(candidate)
              } else if (!candidate.terrain.blocksLOS) {
                if (!candidate.contains || (space.isElevated() && candidate.contains.player == space.contains.player)) {
                  spacesInRange.push(candidate); 
                } else if (candidate.contains.player != space.contains.player) {
                  showStoppers.push(candidate)
                }
              }
            }
          })
        }, this)
      range -= 1
    }
  spacesInRange.shift();
  spacesInRange = spacesInRange.concat(showStoppers);
  return spacesInRange
}
}
~~~

The showStoppers set is important, because when a unit stops further line of site from being drawn past it, for example enemy units or a forest space, they're still added to the set of spaces in range but are no longer taken into consideration for the purposes of drawing further line of site. This worked out well in practice. ~Space.prototype.isElevated()~ is a nice little utility function that checks if the unit has the Special characteristic for its Range attribute, or if it's on a hill. Or both I suppose but they're redundant in that case. ~Map.prototype.adjacentSpaces()~ uses the prototype function ~isAdjacentTo()~ to give a set of spaces adjacent to a given space, and then the spacesInRange set is shuttled into the availableTarget space which returns the spaces that contain enemy units.

~~~javascript
var spacesInRange = activeGame.availableTargets(y, x);
console.log(spacesInRange);
spacesInRange.forEach(function(space){
	$(".row" + space.y + ".col" + space.x).addClass("targetable")
})
~~~

Then I added this bit to the ~$(document).ready()~ section of the index.js file to make the whole thing work, and through it into the part for when you click on a unit. This is a lot more terse than the current code I've got put together for the movement section, which I need to go back and tidy up. A big part of the tightening of this thing is going to involve pulling out sections of code and turning them into separate functions. Clean Code concepts and such.

This was a big prototype project for me. I found it was more useful to throw prototype methods onto the ~Map~ objects instead of the ~Space~ or ~Unit~ objects because it let me go through all the spaces without having to do any mathematical iteration. I used a lot of forEach(), too.

Next thing to work on is letting dudes actually attack each other. I'd also like to show all potential spaces in movement range instead of moving your guys one space at a time, but I'm not sure how to handle forests. They use an extra movement point when you're going through them so it's going to have to be a different approach than this range thing.