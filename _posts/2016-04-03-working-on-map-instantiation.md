---
layout: post
title: Working on Map Instantiation
category: doomball
tags: [doomball, javascript, games]
---

 I've got a function up and running that returns a two dimensional array with space objects that can contain a unit. It can pass the unit to the `renderUnitCard` function and can be easily traversed. Very satisfying.

~~~javascript
["......",
 "--..--",
 ".-^--.",
 "=.##..",
 "..##.#",
 ".--^-.",
 "--..--",
 "......"]
~~~
 
 The Space class doesn't need to be any more complicated, it's really just a container though it's one that should have a prototype output method that returns itself as a string, complete with any contained units. The game only allows one real token on the space at any given time which simplifes things. The Token class is going to need a prototype method that returns a string <div> version of itself so that the css can render the unit on top of the card.
 
 I have to find some good backgrounds for the spaces too.
 
 I'm thinking about the option of turning the game into a grid instead of having hexes, just for simplicity of rendering, but then you'd either have four facing with no diagonal movement/attack or you'd have eight facing, both of which just feel so different than having six facings which is of course the world's most perfect number for faces of a polygon.
 
 Oh yeah and it makes the map from sexy ASCII drawings like the one on the top.