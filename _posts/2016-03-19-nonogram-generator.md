---
layout: post
title: Nonogram Generator
categories: [projects, nonogram, codepen, javascript]
---

[![Nonogram screenshot]({{ site.baseurl }}/public/images/nonogram_generator.jpg)]
(http://beardsley-james.github.io/griddler2/)

The Nonogram generator is my biggest project to date, and the one I've got the most significant plans for.

Last year I started playing a game called [Griddlers Plus][1] on my telephone, it's a pretty simple Nonogram game with colors and triangles spaces which is pretty great. I have a couple of strategies I've figured out for solving the puzzles, and I was looking into transferring them into a javascript program I would use to solve the puzzles for me or at least give me a head start.

In the process of looking into doing so, I realized quickly that I would essentially have to reinvent the game in order to program the solving algorithm, and I started working on an engine to render the grid as a usable artifact on Codepen.

<p data-height="268" data-theme-id="0" data-slug-hash="pgRvgw" data-default-tab="result" data-user="beardsley-james" class="codepen">See the Pen <a href="http://codepen.io/beardsley-james/pen/pgRvgw/">Nonogram</a> by James Beardsley (<a href="http://codepen.io/beardsley-james">@beardsley-james</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

I ran into a couple of headaches and realized I didn't necessarily have the capacity to work this out on Codepen. I think the main problem was that I thought I should be able to have a function that could traverse both columns and rows to output the binary value representing activated cells. I started working on other projects and got more comfortable using github to host my online content.

At this point I began work on the [next iteration][2] of the nonogram software, mostly working on setting up the form that would be used to input the values and get it set up. I started working with jQuery and worked out the basic structure I wanted on notepaper at work before I took it home and started working with it. 

```javascript
function generateBinaryString(element){};

function generateClue(binaryString){};

function generateClassFromValue(val){
	switch (val){
		case "0":
			return "white";
			break;
		case "1":
			return "black";
			break;
		case "2":
			return "flag"
	}
};
```

I was also reading [Clean Code][3] by Robert Martin at the time so I was thinking a lot about how to name functions and using little functions to do every damn kind of thing.

I ran into basically the same problem, though, especially when I tried accessing classes in freshly made DOM nodules with jQuery. I decided to try something a little different and looked up how to set up a table using straight javascript DOM manipulation.

```javascript
function tableMaker(tableId, puzzle) {
	var table = document.getElementById(tableId);
	table.innerHTML = ("");
	var	tbody = document.createElement('tbody');
	
	var	width = puzzle.width;
	var	height = puzzle.height;
		
	table.appendChild(tbody);

	for (var i = 0; i <= height-1; i++) {
		tbody.insertRow(i);
		for (var j = 0; j <= width-1; j++) {
			tbody.rows[i].insertCell(j);
			tbody.rows[i].cells[j].addClassName("row" + i);
			tbody.rows[i].cells[j].addClassName("cell" + j);
		};
	}

	tbody.insertRow(0);
	for (var j = 0; j <= width-1; j++) {
		var th = document.createElement('th');
		th.addClassName("cell" + j)
		tbody.rows[0].appendChild(th);
	}

	tbody.rows[0].insertBefore(
		document.createElement('td'), tbody.rows[0].cells[0]
	).addClassName("empty");

	for (var i = 1; i <= height; i++) {
		var th = document.createElement('th');
		th.addClassName("row" + (i - 1))
		tbody.rows[i].insertBefore(th, tbody.rows[i].cells[0])
	}
	
	table.createCaption().innerHTML = puzzle.name;
	return true;
}
```

Of course this didn't work out right away and I had to tweak stuff but suddenly I had an appropriate DOM object to work with, consistent across instances importantly, since prepending the table headers in front of the rows was one of the things throwing me off with jQuery. What I originally referred to as "TableMaker" became [Griddler 2][4], and I think is the most usable bit of programming I've done to date. You can go in, you can make objects that could theoretically be exported into the program as solvable puzzles, you can solve puzzles and it tells you when you win. I think the clue verification is still a bit wonky, and there's nowhere to input your created puzzles to make them usable, but it's a start.

The plan going forward is to put in some kind of backend so that people can use their Facebook profiles or whatever to jump on and save their puzzles. Nothing big, it's really a practice project, but it's nice to have something I kind of ran at and conquered of my own volition.



[1]: https://play.google.com/store/apps/details?id=com.ally.griddlersplus
[2]: http://beardsley-james.github.io/griddler/
[3]: http://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882
[4]: http://beardsley-james.github.io/griddler2/