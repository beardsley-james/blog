---
layout: post
title: Boring Status Update
category: personal
tags: 
---

Things have been going a bit slow because the whole family just got over being sick all at the same time. Haven't had a lot of time to stay up late and work on stuff, plus I download Kerbal Space Program which is a fascinating and educational time sink. It's amazing how many people are talking about rocket mechanics for no reason other than accomplishing goals in a make believe sandbox video game space program. So far I've killed a lot of kerbals and made some explosions, and had a couple of falling with style types of situations.

I've been thinking about how to handle map movement for my game. I think the first thing to do is to get a working demo where a virtual table top, with an array of objects representing the spaces, is shown on the screen, and a guy can move around on the map. Maybe with some terrain, maybe worry about the terrain later.

Nah, I should worry about the terrain now.

So it's going to look something like this:

```javascript
var map = [
	[ {
		x: 0,
		y: 0,
		terrain: "Plains",
		contains: {
			"spearmen 1": {
				"name": "spearmen",
				"tokens": [
					hit, hit, entrenched
				]
			}
		}
	]
]
```

Or something like that. And then it goes through it and renders it on the screen. And then you can click on the guy and it shows you where he can move and then you can click on one of those spaces and he moves there. And you can't click on spaces where he can't move.

Attacking is more complicated because of range. I also have to decide if I want the player to be able to course out a whole turn's worth of movement or if I want everyone to pop around one space at a time. Rivers require a coin flip to cross so you wouldn't be able to plan a route across a river because you don't know if the ford will be successful or not.