---
layout: post
title: "Safari Snap"
date: 2021-07-22
excerpt: "Professional Metaverse Game"
tags: [game, Professional]
comments: true
game: true
pagetype: 1
figure: safari_figure.png

---

## Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/87jT2Cp5-4U" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Worked in an 8-people team at Lilith Games.

## Behavior Tree for animal AI
<p>· Behavior Tree contains Sequence, Selector, Condition, Decoration.</p>
<p>· Designer designed animals' behavior. I broke the behavior mode into behavior tree diagram.</p>
![image](https://user-images.githubusercontent.com/49530505/137403888-e12175ce-b501-41e9-96cd-08eac58ea4ae.png "Behavior Tree Design")
<span class="caption">screenshot of Behavior Tree Design</span>
<p> Other programmer can create behavior nodes by my codes.</p>
<pre>
<code>
function BTMgr.CreateSequence(_name,_owner)
	local newNode = CreateNewNode()
	newNode:Init(_name, newNode.Type.Sequence,_owner)
	return newNode
end

function BTMgr.CreateSelector(_name,_owner)
	local newNode = CreateNewNode()
	newNode:Init(_name, newNode.Type.Selector,_owner)
	return newNode
end

function BTMgr.CreateAction(_name,_action,_owner,...)
	local args = {...}
	local newNode = CreateNewNode()
	newNode:Init(_name, newNode.Type.Action,_owner,args)
	newNode:SetAction(_action)
	return newNode
end
</code>
</pre>

## Different types of anmial FSM inherited from base FSM.
<p>· The game has many types of animals: bird, herbivore, carnivore, etc. So I made modules for different types of animal FSM, which improves code efficiency and work efficieny.</p>

## Cooperated with other programmers to build path finding system.
<p>· Understood the basic tool of pathfinding produced by the engine and taught other programmers.
<p>· Wrote methods of pathfinding in different situations for animal ai, such as animal being chased.

## Contributed Design to camera system and photo editing system. Built these two systems and made them very customizable for designers.
<p>· The customizable camera and photo system includes filter, sticker, selfi gesture, etc.