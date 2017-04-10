---
layout: post
title: Mythotopia, An introduction
category: mythotopia
tags: [mythotopia, javascript, games]
---

## The game

Kelly and I went to Foam Brain games in Troy and they had this brown bag sale where you spent $25 and just got whatever was in the bag, which was pretty much guaranteed to have an MSRP of greater than $25. I was so happy with the first one that I got that I got two more, plus I love the thrill of the unknown purchase.

One of the games we picked up was called Mythotopia. It uses a combination of card-drafting/deckbuilding mechanics and map-based maneuvering. It doesn't have any really out-of-turn actions which I think makes it an excellent candidate for my first attempt at a Node-served asynchronous multiplayer game, since full turn resolution can occur without the interjection of opposing players.

## First pass

So I've been thinking about how to structure this. Since it's all Node-y instead of the purely client side javascript approach I've taken with Doomball, I think it's important to more effectively differentiate between the different concerns. So we're going MVC on this one, or as close as I can get with my weird incomplete understanding of the approach.

### Model

The main and most important model is going to be the game as a whole. This is going to include information about the map (more complicated since I want to make it so you can play custom maps) and the state of the game on that map, including tokens in reserve and the board state that the players have. It's also going to include objects for the players in the game, and those object will include subobjects for the hand of cards the player has, the cards the player has in reserve, the cards in the players' decks, that sort of thing. 

These are going to be straight objects because I want to handle the various gamestate manipulations through functions in the controller. That way, instead of using methods like I used in Doomball, I can use separate functions and leave the game state as a pure object with no prototype functions which should make it easier to pull it out of the database and load it up.

### Controller

This is going to be where I hold the functions that change the game state, I'll probably have it so they get passed the objects they need to manipulate directly. Not sure how to pull the functions out of the modules they're in yet, that's something I'll have to figure out.

### View

This is going to be the Node/Express part of the thing but since I'm doing gamestate manipulation serverside it's going to be totally focussed on presenting an effective GUI to the player without handling gamestate changes. Doomball has a lot of gameplay functional stuff being handled by class changes to HTML elements which I guess is ok (I don't like it) for a totally clientside program but I think it'll be more graceful if the view is just passed the game object and then displays it. Obviously it'll have to detect the player accessing the game and hide the information of the other players though. 

I want to use like jquery type stuff to use elements as input options and then they're going to feed information to an action object that gets passed back to the controller, which turns it into an actual game state change, reflects it in the game object, and then sends the game object back to the user.

## Next steps

I think this is going to be a pretty effective approach. There's also the problems of like user authentication and profile/save game management but those seem like more vanilla Node tasks and things I can look up stuff on how to do but making Mythotopia into an online game is a little more unique and interesting.

The next thing I want to do is produce a mocked-up object to represent a game that is about to begin. I think this'll give me a good idea on how to approach further steps and set up my server effectively.