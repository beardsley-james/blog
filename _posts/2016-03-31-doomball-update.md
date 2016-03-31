---
layout: post
title: Progress with Doomball
category: doomball
tags: [javascript, html, games]
---

<img src="{{ site.baseurl }}/public/images/doomball.png" style="width:100%">

Kind of an excellent bit of prograss on the Doomball engine. I've got the unit renderer working, I made a way to work with the grid, and I've been putting some solid thought into the way to handle gameplay mechanics. Found a cool little game that does some similar things to what I'm thinking about, though it handles them in different ways. I think a big part of it is that I've been working with front end stuff so the simple way to handle things for me seems to be with jQuery and lots of `div` classes and I think it could be handled more smoothly with pure JS and some canvas elements, but I don't know how to use canvas elements honestly.

[There's a gallery of units up right now](http://beardsley-james.github.io/doomball/) though that's on the index.html file so if it changes that link will go to something different, and I think they're all looking pretty good. I have art done for a few more races but I've gotten better at pixel art since I started so I kind of want to go back and revisit these old units. One benefit to this project, even if I don't actually get it working as a video game, is that this is a way easier way to customize and revise these pieces than trying to keep up with the dramatic system of paint.net layers I was using before. 

The [grid system](http://beardsley-james.github.io/doomball/testGrid.html) is a bit messy but the spacing is basically right. There was something weird that happened where the inline-block div elements that hold the units were dipping on the last line when it wrapped around the window, so I switched the display to regular block and just floated the things and that cleared it up. Didn't really have to be inline-block anyway, there was nothing inline about the design.

I also wrote a kind of sloppy little function that checks for adjacency.

```javascript
Space.prototype.isAdjacentTo = function(space){
	if (this.x == space.x || this.x == space.x-1 || this.x == space.x+1) {
		if (this.x % 2 == 0) {
			if (this.y == space.y-1 || this.y == space.y) {
				return true}
		} else {
			if (this.y == space.y || this.y == space.y+1) {
				return true
	}}}
	
	return false
}
```

I wrote some grids down longhand and tried to figure out a good test to see if spaces were adjacent when you were dealing with hexagons and this is basically what I came up with. I thought it was too rough and I figured, since I didn't really have any tests to run on it yet, I'd shelve it and see how it worked when I got to it but when I went looking for a good way to generate hex maps in html, I found [this game](http://www.h3xed.com/pc-gaming/turn-based-strategy-hexagon-risk-like-javascript-canvas-game) and jumped into the source code. It basically uses the same algorithm to check adjacency, but it uses arrays of values to add or subtract from the values of the hex in question instead of a simple test like this. I'm not sure if it's better or not. I guess you could use those values in more than one place, with the other guy's example.

```javascript
GridMath.neighbors = {
    'even': [[-1, 0],[+1, 0],[0, -1],[0, +1],[-1, +1],[-1, -1]],
    'odd': [[-1, 0],[+1, 0],[0, -1],[0, +1],[+1, +1],[+1, -1]]
};
GridMath.isNeighbor = function(x, y, x2, y2) {
    var neighbors = y % 2 == 0 ? GridMath.neighbors.even : GridMath.neighbors.odd;
    for (var i = 0; i < neighbors.length; i++) {
        if (x + neighbors[i][0] == x2 && y + neighbors[i][1] == y2) {
            return true
        }
    }
    return false
};
```

See? Basically the same thing.