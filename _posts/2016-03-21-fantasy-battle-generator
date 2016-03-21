---
layout: post
title: The Fantasy Battle Generator
---

Like, I'm sure, many of my readers, I frequently read 300 page rulebooks for games I never intend on playing simply for the pleasure of studying irrelevant minutiae. In the course of reading the latest version of [Warhammer Fantasy Roleplay][1], a really gritty and fun roleplaying game for people that have a keen dislike for the characters they're roleplaying, I found myself wondering how some of the combat mechanics might play out if they were automated.

At this point I was basically just messing around on Codepen. I came up with this:

<p data-height="264" data-theme-id="22892" data-slug-hash="BovRop" data-default-tab="result" data-user="beardsley-james" class="codepen">See the Pen <a href="http://codepen.io/beardsley-james/pen/BovRop/">Warhammer Adventure</a> by James Beardsley (<a href="http://codepen.io/beardsley-james">@beardsley-james</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Basically you can click on a couple buttons, come up with some semi-randomized Warhammer Fantasy critters, and then make them fight to the death for fun, with a nice little adventure read out that tells you how hard they're hitting each other.

Now there are some serious balance issues with this "game", specifically that there's this whole system of avoiding combat that only applies to opponents that are using ranged weapons, which means nine times out of ten your orc buddy is going to stomp whatever poor halfling archer you're sending his way. 

I had to make some tough choices about what kinds of characters I was going to include, too, and I haven't even put in a magical system or any kind of way of keeping a range value between the character to make bows and arrows more effective.

I'd like to put in some kind of ammo counter too, so that guns are more of a thing. Tighten up a bit. It's tough to feel that motivated to, though, since as far as I can tell the major consumer category for this program consists of me and I'm not even that interested in running it a bunch of times. Fun exercise, though, and it's really the first time I tried to stretch my legs out with object oriented programming concepts.

The latest version is [here][2], which I moved over from Codepen when I decided to host on Github for now. The main thing I did in the move was separate the parts of the Javascript code bank into their own separate files which isn't at all best practice at this point, and make the form to pick characters a bit more robust and interesting.

I also added an ability for the game to store and serve pre-generated characters types, which is something I might revisit when I start hooking some of these things up to backend software.

[1]: https://www.fantasyflightgames.com/en/products/warhammer-fantasy-roleplay/
[2]: http://beardsley-james.github.io/fantasybattlegenerator/