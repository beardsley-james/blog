---
layout: post
title: freeCodeCamp Random Quote Machine
category: javascript
tags: [projects, quotemachine, freecodecamp, javascript, codepen]
---
## The Challenge

One of the early front-end challenges in the freeCodeCamp curriculum is to make a little app that gives you a random quote when you click a button. You're also supposed to make it so that you can tweet the quote if it's a good one, but that was optional when I did the challenge. I think I'm going to have to go back and add that on though because they took out optional User Stories and made them all mandatory, I guess we'll see.

## The Archive

I started by looking for a solid API to provide random quotes and I found quite a mess. Lots of websites that wanted to be like "you can only do so many quotes" or gave instructions I didn't really get at the time, so I decided to skip that mess and do it myself. I split it up into three parts - [the first part][1] was a simple array containing the quotes I'd picked out as what were coincidentally JSON objects. I don't think I totally understood JSON objects at the time.

```javascript
{'id': 0, 'quote': 'string', 'author': 'string', 'source': 'string'}
```

So that worked out pretty well. I could generate a random number between 1 and the number of quotes and use that to snag the quote I wanted to render on the page.

## The Collector

Once I started grabbing quotes online and throwing them into the page, though, I realized that it was tedious and I hated it, so I threw together a quick page that gave me a form I could put the info into to get a nicely formatted object to copy-paste into the database. Obviously a full stack program would submit it directly, but this is Codepen so it's all front end stuff.

<p data-height="266" data-theme-id="22892" data-slug-hash="PqyJGP" data-default-tab="result" data-user="beardsley-james" class="codepen">See the Pen <a href="http://codepen.io/beardsley-james/pen/PqyJGP/">QuoteForm</a> by James Beardsley (<a href="http://codepen.io/beardsley-james">@beardsley-james</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

```javascript
$('#id').val(quotes.length);
```

This part sets the ID number as the next one higher than the highest one in use so I don't have to figure it out manually.

```javascript
$('#quoteGen').on('click', function(){
  $('#result').text('{id: ' + $('#id').val() + ', quote: "' + $('#quote').val() + '", author: "' + $('#author').val() + '", source: "' + $('#source').val() + '"\} ');
})
```

This is the meat, this snags values out of all the form sections and tosses them together into a juicy javascript object. I think now I would probably pull in some variables to gussy it up a bit but honestly this is so clean and functional I don't think it'd be an improvement. Also note the use of single quotes - I like double quotes usually since I'm an American but all the quotes I was inputting had double quotes too, so I had to use single quotes to not break the scripting.

```javascript
for (i = quotes.length - 1; i > 0; i--) {
  document.write("</br><p>ID: " + quotes[i].id);
  document.write("</br>Quote: " + quotes[i].quote);
  document.write("</br>Author: " + quotes[i].author);
  document.write("</br>Source: " + quotes[i].source)
}
```

And this part prints all the existing quotes onto the page when it loads, which is a nice feature. It's not totally necessary I suppose, but it doesn't hurt.

I didn't think to throw everything into the mandatory `$(document).ready()` jQuery handler, but it doesn't seem to have hurt the functionality any so no worries on that front.

## The Product

Finally I threw together the actual random quote generator which wasn't really as inspired as the pseudo back end I don't think.

<p data-height="266" data-theme-id="22892" data-slug-hash="GJBerd" data-default-tab="result" data-user="beardsley-james" class="codepen">See the Pen <a href="http://codepen.io/beardsley-james/pen/GJBerd/">Random Quote Generator</a> by James Beardsley (<a href="http://codepen.io/beardsley-james">@beardsley-james</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

I made one in yellow.

<p data-height="266" data-theme-id="22892" data-slug-hash="RPeEWy" data-default-tab="result" data-user="beardsley-james" class="codepen">See the Pen <a href="http://codepen.io/beardsley-james/pen/RPeEWy/">RQG Candy Apple Green</a> by James Beardsley (<a href="http://codepen.io/beardsley-james">@beardsley-james</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

And I made this one called candy apple green for some reason. I don't really know why. It doesn't have any actual green on it but that's what it's called. I really don't remember where the name came from.

```javascript
var previous;

$(document).ready(function() {
  $('#button').on('click', function() {
    var i = Math.floor((Math.random() * quotes.length) + 1);
    if (i === previous) {
      i++
    };
    if (i > quotes.length) {
      i = 1
    };
    previous = i;
    $('#quote').html(quotes[i].quote);
    $('#author').text(quotes[i].author);
    $('#source').text(quotes[i].source)
  })
});
```

One of the big things that bothered me about the original version of this was that sometime you would click on it and it would just show you the same quote as the one you already had. No big deal if there were a lot of quotes, since the chances of getting a duplicate were pretty low, but my enthusiasm for digging up appropriately pretentious quotes flagged pretty quickly. Nice and easy, though, just saves whatever the ID of the current quote is and adds one if it's a duplicate. Then I ended up with blank pages when it ran into the ceiling, so I made it reset back to 1 if it hit the end. Other than that it's just filling in some variables and throwing them onto the page.

I put this sucker together like a year ago but I think it holds up pretty well. Someone in the freeCodeCamp chatroom yesterday said they liked how clean the javascript was and so do I. It's a good indication of my proclivity for modulization, which I hope to explore going forward.

[1]: http://codepen.io/beardsley-james/pen/MwPyKO.js