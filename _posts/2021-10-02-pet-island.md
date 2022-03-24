---
layout: post
title: "Pet Island"
date: 2021-10-13
tags: [game, professional, Lua]
comments: true
game: true
pagetype: 1
figure: pet_figure.png
excerpt_separator: <!--more-->
---
Collect pets and dig mines

<b>Role:</b> Sole Programmer and designer

<b>Platform:</b> Lua + in-house game engines

Company: Lilith Games
<!--more-->

## Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/QvPPOupOO20" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

I did all programming parts and collaborated with Artist and Designer Jerry Liu from September 2020 to Janurary 2021.


## Set data structure of stat inflation for the designer
<p>· Pet properties such as the model, rarity, egg region, levels, and stats, etc. The designer can make a new pet by add a new line on pet's propertoies sheet.</p>
<p>· Item and potion properties such as the price, the time it can effect and its function. The designer can make a new item by add a new line on item design sheet.</p>
<p>· Mines properties such as model, time refresh, zoning, and money player receives, etc.</p>
<p>· Bag system and Pet collection handbook.</p>

## Animation tool for the artist
<p>· UI animation tool such as where should the UI pop up and the way the UI pop up.</p>
<p>· Pet spawn animation tool such as camera angle, animation length, etc.</p>

## Pet simple AI by FSM

{% highlight c %}
        function FsmBase:NewFSM(allState)
            self.allState = allState    
            self.curState = nil
        end

        function FsmBase:RunFSM()
            local curState = self.allState[self.curState]
            if curState and curState.OnUpdate then
                curState.OnUpdate(self)
            end
        end

        function FsmBase:ChangeState(_nextState)
            local curState = self.allState[self.curState]
        	if curState and curState.OnLeave then
        		curState.OnLeave(self)
        	end
        	local nextState = self.allState[_nextState]
        	self.curState = _nextState
        	if nextState and nextState.OnEnter then
        		nextState.OnEnter(self)
        	end
        end

        function FsmBase:ProcessLocalEvent(event,...)
        	local args = {...}
        	local curState = self.allState[self.curState]
        	if curState and curState.OnEvent then
        		curState.OnEvent(self,event,table.unpack(args))
        	end
        end

        function FsmBase:IsInState(state)
        	if self.curState == state then
        		return true
        	end
        	return false
        end
{% endhighlight %}

<p>Above is the base function of FSM. Specifically, FSM has OnEnter, OnLeave, OnUpdate, OnEvent. </p>
<p>I used FSM to make pet follow, idle, dig mine and play around.</p>

## Data security
Most of data calculation happens in server-sided to insure data security. And server pass the calculation result to client.

## Contribute design to trade-up system
Briefly, player can put five pets in incubator and get a new pet randomly.