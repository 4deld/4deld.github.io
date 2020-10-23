---
title: Development Log {Gangle}
date: 2020-08-09 16:50:30 +0900
categories: [Development Log, Gangle]
tags: [development log, competition]    # TAG names should always be lowercase
seo:
  date_modified: 2020-08-24 11:33:04 +0900
---

# Development log - Gangle

First Development log is Gangle.

## The Date

2019/12/8 ~ 2019/12/24

After the final exam, I developed Gangle.

## Title(What is it)

Gangle(Running game)

## Description(Give your future self a break, help them remember)

This won the silver prize in the DIGITAL CONTENTS COMPETITION 2019.

Gangle is a web running game developed with the concept of an office worker wandering around the city looking for Wi-Fi.

The format of the game, which avoids obstacles through jumps, is no different from the traditional running games. 

However, it was developed by differentiating itself with unusual manipulations that are not in other games.

The types of cards are REROLL, JUMP1, JUMP2, and WIFI DISCONNECTED.

Three cards are randomly displayed with the directional key each time.

Pressing the direction key activates *the effect of the card*.

*REROLL* - updates the three cards randomly.

*JUMP1,2* - the character jumps. (The height that the character jumps is higher when pressing JUMP2 than when pressing JUMP1.)

*WIFI DISCONNECTED* - game over

## Tech Stack

GCP, javascript, Node.js, Phaser3, lowdb

## What you were in charge of

I was in charge of frontend, backend except phaser

## What was the problem(How was it solved? or unsolved?)

The problem was in *Ranking*.

I thought this logic would be worked. First, receive *the username* and *id value* from the client and save them in the database. Second, after the game is over, *the game score* is put where *the matching id* exists. 

However, the id value *changed* whenever other users came in from the server, so the score became other users'(-UNSOLVED).

it became *gameover* by pressing the JUMP card ↑ on the third .

I don't know why. Because it's the problem of the Phaser developer (-UNSOLVED).

## Feelings(what you felt)

To be honest, I doubted a little if my team could pass the preliminary round with the project developed by my colleagues.

The preliminary announcement came out during the final exam period and I used to say that I would die if I couldn't develop a server after the end of the final exam.

I learned node.js in the club, but I didn't understand well. However, with the thought of doing it, I felt it somehow worked out.

I think the fact that the bug in ranking was caused by using the database without knowing well the interaction between the server and the client.

I developed the server for the first time and won an award with it, so I think it's a project with a lot of *affection*.

I was absorbed in developing server, used to stay up all night *coding*. The exam was over and it was more fun because it was a work to participate in the competition. 

But it was such a shame. Phaser and server were combined and distributed for a day or two, there were many bugs, errors, and points to modify *(details)*.

It was almost incomplete because we had to go through the judging process without fixing that part.

It would have been better if I had distributed it for a week after the exam with fixed bugs, errors, and additions.

That's too bad. The server seems to be fixed well if you fix the foundations first.

I think it was possible because my *senior* helped me even though he was participating in the competition.  I think senior is really important in our school.

## Desired things & Future plans

- Change Ranking Style ( TOP3 color )

- Make button that can control the volume or ON/OFF the sound

- Allow game to start by pressing Enter

- Enable player to view scores while playing a game

- Bug that becomes gameover by pressing the JUMP card ↑ on the third

- Let cards float with player

- Fix Ranking bug

- Change DataBase from lowdb to MongoDB

- Add various obstacles and add a system to raise the tempo of the game

- The goal is to add various cards so that can show various plays that were not seen in the running game