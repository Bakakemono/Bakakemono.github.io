---
layout: post
title:  "Aiming Aid"
date:   2020-04-17 01:00:00 +0200
---

Before starting, a small reminder seems essential. The game that I am currently working on is a Star Fox Like. 

<div style="text-align: center"><img src="/assets/data/gifs/starfox_64.gif" width="600"></div>
<p>&nbsp;</p>

One of the main feature of this type of game is shooting elements that can be enemies or just some random objects of the decor while moving in front of a camera that is moving on a rail.

<div style="text-align: center"><img src="/assets/data/images/basicSetup.png" width="600"></div>
<p>&nbsp;</p>

But some trouble appear when it comes to deal with the shooting mechanics.

First trouble, the shooting mechanics.

<div style="text-align: center"><img src="/assets/data/images/playerFrontCamera.png" width="600"></div>
<p>&nbsp;</p>

The player is on a 2D space in front of the camera while this one is moving around in a 3D space. It’s hard to tell the distance the player is from the camera just by looking. Even with some reference elements around like asteroid, it’s still hard to be sure.

Second trouble, the direction the player is going to fire.

<div style="text-align: center"><img src="/assets/data/images/firePlayer.png" width="600"></div>
<p>&nbsp;</p>

Because of the perspective due to the 3D view and the fact that the player is mainly going to fire at the same direction as the camera is looking at, the accuracy is reduce.

Third and last trouble (at the moment) we are going to solve is that like the player, the enemies are also troublesome to estimate their position from the camera and from the player. 

<div style="text-align: center"><img src="/assets/data/images/enemyMove.png" width="600"></div>
<p>&nbsp;</p>

The enemies will mainly come in front of the camera to face the player and fire at him. Like explain for the player, the perspective make the estimation of their current and future position  hard and boring, mainly when you can hit something that you were sure you were going to hit. The other fact is that the camera is moving and make everything even harder.

So we need a way to increase the experience of the player by removing the trajectory calculation for him.

It was at this moment that the aiming aid system was imagine and the implementation started.

The first element of this feature that need to be implemented is a small debug draw to help visualize which way the player is currently aiming at.

<div style="text-align: center"><img src="/assets/data/images/cible.png" width="600"></div>
<p>&nbsp;</p>

Even if this seems false in the first, the player will be able to estimate more efficiently in which direction he will fire.

<div style="text-align: center"><img src="/assets/data/images/aimFront.png" width="600"></div>
<p>&nbsp;</p>

But it is not good enough to make easier the player’s gameplay. A precise aiming like this is still too hard and too troublesome, While the player is firing at enemies, they will move and the player will also move because of the camera, making any sort of precise positioning almost impossible. That’s why if an object that can be firing at is not far away from the initial fire’s direction, a small correction will be apply to make him touche the target.

<div style="text-align: center"><img src="/assets/data/images/AimFrontReoriented.png" width="600"></div>
<p>&nbsp;</p>

That’s what this feature need to be and the implementation will now begin.

The first element that I have implemented was a sight in front of the player. At the beginning, I didn’t have the sight that was make by the art team, so I use a debug gizmos to represent it. As expected, it was already better to estimate the current fire direction.

<div style="text-align: center"><img src="/assets/data/images/addGizmoTarget.png" width="600"></div>
<p>&nbsp;</p>

After the sight implemented, I need to get all the current drawn entities. The programmer team that make the game engine have implement a simple method to easily get all entities currently drawn.

<div style="text-align: center"><img src="/assets/data/images/getDrawedTarget.png" width="600"></div>
<p>&nbsp;</p>

All those entity aren’t necessary for the aiming aid system. Only entities that can take damage like asteroids or enemies will be taken but we will obviously avoid the player. The type of entity that the player need is a destructible element that all entity that can be destroy have and we register in an array all the entities that the player is be able to destroy.

<div style="text-align: center"><img src="/assets/data/images/possibleTarget.png" width="600"></div>
<p>&nbsp;</p>

Once the first sort done, it was time to make another more accurate, which is the most important. By taking the view of that from the camera position to the sight, we are able to calculate a field of aim and we can check if one of the previously registered entity is in the field of aim of the player. To check if it is or not in the field of aim, we check if the angle obtained by a dot product from the current aim direction and the current target direction is bigger from the maximum angle that we have set. If it is smaller, we register it in an other array for the target that we can fire at.

<div style="text-align: center"><img src="/assets/data/images/preciseTarget.png" width="600"></div>
<p>&nbsp;</p>

Once those entity registered, we just need now to check which on have the smaller angle from the current fire direction and lock it by telling the player that his target is this entity and in which direction it is.

<div style="text-align: center"><img src="/assets/data/images/bestTarget.png" width="600"></div>
<p>&nbsp;</p>

Of course, if there is an entity that can be targeted exactly in the middle of the field of aim, the aiming aid will not be that relevant to have.

<div style="text-align: center"><img src="/assets/data/images/centralTarget.png" width="600"></div>
<p>&nbsp;</p>

But if the target is far from the middle, the player will be grateful that he can shoot at it even if he doesn’t fire at it precisely.

<div style="text-align: center"><img src="/assets/data/images/desaxedTarget.png" width="600"></div>
<p>&nbsp;</p>

But since this rustic version of the aiming aid, many changes and improvement have been made to it.

Almost at the end of the implementation, the target that was provided by the art team was ready so I was implement them with a new feature. When the player have no entity lock, the sight is in neutral mod and de sight sprite at the left is display. But when one is lock, it is the other one.

<div style="text-align: center"><img src="/assets/data/images/reticule_neutral.png" width="300"><img src="/assets/data/images/reticule_lock.png" width="300"></div>
<p>&nbsp;</p>

An adjustment was quickly imposed as necessary. The player missed almost no targets and it spoiled the gaming experience. The reason was quickly found. The angle that defined the cone in which entities can be targeted was too high and had to be reduced.

<div style="text-align: center"><img src="/assets/data/images/angleReduction.png" width="600"></div>
<p>&nbsp;</p>

But the player was still too powerful and the reason was one more time obvious, he have an unlimited range.  As any entity that entered the screen was potentially targeted, a maximum range had to be set up. So that it’s not too heavy for the cpu, I decided, instead of calculating the distance in a “classic” way with the pythagorean theorem that requires a square root, to calculate the Manhattan distance which contains only an addition of the distances on the X and the Y axis. it is certainly less accurate but also cost less performance.

<div style="text-align: center"><img src="/assets/data/images/lengthLimitation.png" width="600"></div>
<p>&nbsp;</p>

Even if it is not that much, this system is one of the most performance cost of all game system.


Further research will be required but there is some possibility to optimize parts such as angles calculations or the part where the positions of the targetable entities are recovered.


It is not impossible, however, that the aiming aid will be abandoned afterwards or that the system will be readapted if the current version does not match the final vision of the game and the feeling that we want to give to it.