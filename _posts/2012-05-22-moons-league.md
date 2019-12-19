---
layout: post
title: "Moon's League"
date: 2019-05-22
excerpt: "Group Project: a strategy game"
tags: [group, strategy]
comments: true
game: true
pagetype: 1
figure: strategy-figure.png
---

[Install Moon's League](https://muruc.itch.io/moons-league){: .btn}


{: .center}
![image](https://user-images.githubusercontent.com/49530505/69022293-d72e6180-09f5-11ea-92c0-be14255ae1d5.png "map")
{% capture images %}
{% endcapture %}
{% include gallery images=images caption="Screenshots of Moon's League" cols=2 %}
	

	
Moon’s League is a strategy game made by Unity. It's
a two-player game. They could find a place to build the
kingdom and buy different constructions. They could hire
heroes in the tavern construction and each turn the tavern
produce different hero. Every hero has unique skills that
may have impact on terrain or other effects. 

I did the
design of characters’ skill, value design and all coding. All graphs were designed by Dayoon Lee.

## Demo

<iframe width="560" height="315" src="https://www.youtube.com/embed/PiBjiLdneK0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Game Mechanism

{: .center}
![image](https://user-images.githubusercontent.com/49530505/69022302-df869c80-09f5-11ea-9245-bb8d8b3b6a39.png "screenshots")
{% include gallery images=images caption="Screenshots of Moon's League" cols=2 %}

At the beginning of the game, players will follow the tutorial. They will
move the icon of the king (randomly spawned on the map) and build the
kindom.

In the kingdom, players can buy constructions and find grids to build
them.

After players buy tavern, they can recruit heroes. Moveing hero can
eliminate the fog of war. Hero can attack opponent's hero, heal other
player's hero or have special function like destroy barriers.
When player's hero arrive the opponent's kingdom, player win.

{: .center}
![image](https://user-images.githubusercontent.com/49530505/69022303-df869c80-09f5-11ea-91eb-0b2aa618b833.png "screenshots")
{: .center}
![image](https://user-images.githubusercontent.com/49530505/69022301-deee0600-09f5-11ea-9757-059f51870760.png "screenshots")
{% capture images %}
{% endcapture %}
{% include gallery images=images caption="Screenshots of Moon's League" cols=2 %}

In Each turn, player can recruit hero in "tavern". The maximum
number of hero that one player can have is five (with farm it is six).
Hero's death or selling hero will reduce the current hero number.
There are 21 heroes in the public hero pool in total. Each turn
there will be three heroes that are randomly picked from the public
hero pool. Recruiting hero will cost money.

Each player can buy up to two contrustrtions after the kingdom
has been built.
In tavern, player can recruit heroes. The workshop can produce
miner who can dig gold and add wealth. If player has farm, the
maximum number of heroes will be six.

## Character Design

There are 21 heroes in total:

{% capture images %}
	https://user-images.githubusercontent.com/49530505/69045678-4f1a7d00-0a32-11ea-8e01-ca0f9df46b37.png
	https://user-images.githubusercontent.com/49530505/69045679-4f1a7d00-0a32-11ea-89b0-d63dc4453569.png
{% endcapture %}
{% include gallery images=images caption="Graphic designs of characters by Dayoon Lee" cols=2 %}

* <b>Paladin</b>: Dash towards a direction and spend all current move steps. Do damage on all enemies on that line. If the heroes have three current move steps, dash three grids.

* <b>Witch Doctor</b>: Double the Buff on one teammate. The effect lasts in one turn.

* <b>Bard</b>: Add power up Buff on one teammate, lasting in one turn

* <b>Snaker</b>: Give an enemy ten-layer poisoned Debuff. In every following turn the poisoned Debuff lower down one layer

* <b>Snow</b>:  If an enemy has any Debuff, turn that Debuff into stun for one turn

* <b>SandShaper</b>: Spend all current move steps to build obstacles on grids. The obstacles can be destroyed. They automatically disappear after three turns.

* <b>Mole</b>: Destroy any construction on the map. Construction will restore after three turns.

* <b>Monk</b>: Give an enemy 50% vulnerability and 30% weakness

* <b>Flame</b>: Attack all enemies around and give them three-layer burning debuff

* <b>Lich</b>: Double all debuffs on an enemy, lasting one turn

* <b>Silencer</b>: Cause an enemy silenced in next turn.

* <b>Elf Archer</b>: Long-distance attack. Ignore defense and obstacles.

* <b>Berserker</b>: High single-enemy attack and causing 30% Vulnerability lasting one turn.

* <b>Cleric</b>: Heal a hero.

* <b>Purifier</b>: Relieve all debuffs on a hero

* <b>Goblin Techies</b>: Burry a mine.

* <b>Land Guardian</b>: Give a hero shield, lasting for one turn.

* <b>Rogue</b>: Steal all Buffs of an enemy and shifts them on a teammate.

* <b>Death Alchemist</b>: Burry a bomb on a teammate. Three turns later the bomb kills that teammate and cause high and large-range damage to all characters (enemies and teammates) within that range.

* <b>Lord of Time</b>: Mark the current position grid. After three turns teleports the character back to that position and cause AOE 

* <b>Master of Circus</b>: Switch the positions of an enemy and a teammate

[Install Moon's League](https://muruc.itch.io/moons-league){: .btn}