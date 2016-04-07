---
layout: post
title: Fixing Multiple Unit Selection Bug in Doomball
category: doomball
tags: [doomball, javascript, games, debug]
---

![Multiple Unit Selection Bug]({{ site.baseurl }}/public/images/04-06-2016-doomball-bug-screenshot.png){: .float-right width="25%"}

So I linked Kelly to the work I did last night and she sent me back this screenshot. That's a nasty little gap in the middle there, and it's a big problem. I clicked around myself and found that you can actually select several units at a time and have them possess the ~activeSpace~ class, which is not good since they will all move to the target space you pick and their empty spaces will be whatever the first one in the stack was sitting on, which throws off the display of the grid and makes more than one unit disappear.

~~~javascript
if (activeGame.spaces[y][x].contains) {
	$(this).addClass("activeSpace");
	$("div#grid .gridSpace").each(function(){
		$(this).removeClass("movable");
		var targetClasses = $(this).attr("class").split(" ");
		var targetX = targetClasses[2].charAt(3);
		var targetY = targetClasses[1].charAt(3);
		if (activeGame.spaces[y][x].canMoveTo(activeGame.spaces[targetY][targetX])) {
			$(this).addClass("movable")
		}
	})
}
~~~		

So what I need to do is take out the activeSpace class from whatever space has it from the get go. 

~~~javascript
if ($(".activeSpace")) {
	$(".activeSpace").removeClass("activeSpace")
}
~~~

Nice and easy. Let's see if it works.

Yeah, that did it. Nice.