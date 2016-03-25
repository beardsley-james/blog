---
layout: post
title: Pure HTML Unit Cards for Doomball
category: html
tags: [doomball, html, games]
---

## I whipped this up


<div style = "height: 200px; width: 200px; background-color: green; position: relative; border: 4px brown solid; font-size: 35px; background-image: url('{{ site.baseurl }}/public/images/grass.png'); float: left; margin-right: 15px; color: black">
	<div style="text-align: center; position: absolute; width: 200px; font-size: 20px">Spearmen</div>
	<div style="height: 40px; width: 40px; background-color: orange; text-align: center; position: absolute; line-height: 40px">1</div>
	<div style="height: 40px; width: 40px; background-color: black; color: white; text-align: center; position: absolute; right: 0; line-height: 40px">S</div>
	<img src="{{ site.baseurl }}/public/images/spearmen.png" style="position: absolute; top: 40px">
	<div style="height: 40px; width: 40px; background-color: red; text-align: center; position: absolute; bottom: 0; line-height: 40px">2</div>
	<div style="height: 40px; width: 40px; background-color: blue; text-align: center; position: absolute; bottom: 0; left: 80px; line-height: 40px">1</div>
	<div style="height: 40px; width: 40px; background-color: green; text-align: center; position: absolute; bottom: 0; right: 0; line-height: 40px">1</div>
</div>

Frankly, it's ugly as sin. The colors are HTML generic, the styling is all done in-line for testing purposes, the graphics could be a little better - should I code in multiple instances of individual soldier graphics and plug them in? They're all based on a universal sizing template per size so it should theoretically be a thing, but I don't know if it'd be better than using these basic png transparencies for it. Need to make sure the text can display dynamically so it's visible on whatever size screen is looking at it, too. Do I want to set this up to be responsive from the get go or would I be better off keeping it simple at first and revising it later? Or never, and just making it for desktop? Everyone's on phones these days, probably best to make it responsive, but it's going to be awfule finicky to position in the first place.

As a proof of concept this is an ugly success.