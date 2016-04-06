---
layout: post
title: Successful Implementation of Move Mechanic
category: doomball
tags: [doomball, javascript, games]
---

If you visit the [testGrid](http://beardsley-james.github.io/doomball.testGrid.html) you'll see that you can now click on dudes and move them around at will. There isn't currently anything preventing you from moving around all over the damn place and the thing is faction agnostic at this point, so it doesn't have any attacking functions or anything, but it's a pretty good start. Very happy, kind of tired.

The separate .render() function is important to how this works, because it replaces the HTML of the updated spaces with a fresh render of each space. Since the transfer of the Unit object occurs before the render takes place, it's an adequate representation, and it should transfer clean with whatever temporary effects there are in play.

Right now the movability of the space is only represented in the rendered page and has no analog in the actual object code, which I think works fine. I suppose if I wanted to present the game as like an ASCII telnet thing I'd want to transfer that functionality into something a little more hard-coded, but I suppose it'd basically return true or false in reaction to like a "3,0 to 2,0" kind of query. It wouldn't be that hard to do.

A telnet client would actually be a fun way to make this thing multiplayer without having to worry about handshaking or anything like that. How would you do a grid in ASCII?

~~~
 _   _   _
/S\_/W\_/ \
\_/O\_/L\_/
/ \_/ \_/ \
\_/ \_/ \_/
~~~

Yeah I guess that would work fine. You'd want to pop it up a bit and have a little more room for characters so that you could show more information but no biggie.