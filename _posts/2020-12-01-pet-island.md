---
layout: post
title: "Pet_Island"
date: 7/2020-1/2020
excerpt: "Professional metaverse game"
tags: [game, professional, Lua]
comments: true
game: true
pagetype: 1
figure: pet-figure.png

---

## Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/QvPPOupOO20" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

I did all programming parts.


## Set data structure of stat inflation for the designer
· Pet properties such as the model, rarity, egg region, levels, and stats, etc. The designer can make a new pet by add a new line on pet's propertoies sheet.
· Item and potion properties such as the price, the time it can effect and its function. The designer can make a new item by add a new line on item design sheet.
· Mines properties such as model, time refresh, zoning, and money player receives, etc.
· Bag system and Pet collection handbook.

## Animation tool for the artist
· UI animation tool such as where should the UI pop up and the way the UI pop up.
· Pet spawn animation tool such as camera angle, animation length, etc.

## Pet simple AI by FSM

<pre>
    <code>
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
    </code>
</pre>

Above is the base function of FSM. Specifically, FSM has OnEnter, OnLeave, OnUpdate, OnEvent. 
I used FSM to make pet follow, idle, dig mine and play around.

## Data security
Most of data calculation happens in server-sided to insure data security. And server pass the calculation result to client.

## Contribute design to trade-up system
Briefly, player can put five pets in incubator and get a new pet randomly.