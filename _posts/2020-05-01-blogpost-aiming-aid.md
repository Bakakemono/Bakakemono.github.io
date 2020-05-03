---
layout: post
title:  "Aiming Aid"
date:   2020-05-01 01:00:00 +0200
---

<p style="color: red; font-weight: bold">>>>>>  gd2md-html alert:  ERRORs: 0; WARNINGs: 0; ALERTS: 19.</p>
<ul style="color: red; font-weight: bold"><li>See top comment block for details on ERRORs and WARNINGs. <li>In the converted Markdown or HTML, search for inline alerts that start with >>>>>  gd2md-html alert:  for specific instances that need correction.</ul>

<p style="color: red; font-weight: bold">Links to alert messages:</p><a href="#gdcalert1">alert1</a>
<a href="#gdcalert2">alert2</a>
<a href="#gdcalert3">alert3</a>
<a href="#gdcalert4">alert4</a>
<a href="#gdcalert5">alert5</a>
<a href="#gdcalert6">alert6</a>
<a href="#gdcalert7">alert7</a>
<a href="#gdcalert8">alert8</a>
<a href="#gdcalert9">alert9</a>
<a href="#gdcalert10">alert10</a>
<a href="#gdcalert11">alert11</a>
<a href="#gdcalert12">alert12</a>
<a href="#gdcalert13">alert13</a>
<a href="#gdcalert14">alert14</a>
<a href="#gdcalert15">alert15</a>
<a href="#gdcalert16">alert16</a>
<a href="#gdcalert17">alert17</a>
<a href="#gdcalert18">alert18</a>
<a href="#gdcalert19">alert19</a>

<p style="color: red; font-weight: bold">>>>>> PLEASE check and correct alert issues and delete this message and the inline alerts.<hr></p>


Aiming Aid

Technical Blogpost

Robin Alves

Before starting, a small reminder seems essential. The game that I am currently working on is a Star Fox Like. 


![GIF of Starfox 64 gameplay](../data/gifs/starfox_64.gif "starfox 64 gif")

One of the main feature of this type of game is shooting elements that can be enemies or just some random objects of the decor while moving in front of a camera that is moving on a rail.

 \


<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique1.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique1.png "image_tooltip")


But some trouble appear when it comes to deal with the shooting mechanics. \
 \
First trouble, the shooting mechanics.



<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique2.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique2.png "image_tooltip")


The player is on a 2D space in front of the camera while this one is moving around in a 3D space. It’s hard to tell the distance the player is from the camera just by looking. Even with some reference elements around like asteroid, it’s still hard to be sure.



Second trouble, the direction the player is going to fire.



<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique3.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique3.png "image_tooltip")


Because of the perspective due to the 3D view and the fact that the player is mainly going to fire at the same direction as the camera is looking at, the accuracy is reduce.

Third and last trouble (at the moment) we are going to solve is that like the player, the enemies are also troublesome to estimate their position from the camera and from the player. 



<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique4.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique4.png "image_tooltip")


The enemies will mainly come in front of the camera to face the player and fire at him. Like explain for the player, the perspective make the estimation of their current and future position  hard and boring, mainly when you can hit something that you were sure you were going to hit. The other fact is that the camera is moving and make everything even harder.



So we need a way to increase the experience of the player by removing the trajectory calculation for him. \
 \
It was at this moment that the aiming aid system was imagine and the implementation started.

The first element of this feature that need to be implemented is a small debug draw to help visualize which way the player is currently aiming at.



<p id="gdcalert6" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique5.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert7">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique5.png "image_tooltip")


Even if this seems false in the first, the player will be able to estimate more efficiently in which direction he will fire.



<p id="gdcalert7" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique6.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert8">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique6.png "image_tooltip")




But it is not good enough to make easier the player’s gameplay. A precise aiming like this is still too hard and too troublesome, While the player is firing at enemies, they will move and the player will also move because of the camera, making any sort of precise positioning almost impossible. That’s why if an object that can be firing at is not far away from the initial fire’s direction, a small correction will be apply to make him touche the target.



<p id="gdcalert8" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique7.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert9">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique7.png "image_tooltip")




That’s what this feature need to be and the implementation will now begin.

The first element that I have implemented was a sight in front of the player. At the beginning, I didn’t have the sight that was make by the art team, so I use a debug gizmos to represent it. As expected, it was already better to estimate the current fire direction.



<p id="gdcalert9" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique8.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert10">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique8.png "image_tooltip")


After the sight implemented, I need to get all the current drawn entities. The programmer team that make the game engine have implement a simple method to easily get all entities currently drawn.



<p id="gdcalert10" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique9.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert11">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique9.png "image_tooltip")




All those entity aren’t necessary for the aiming aid system. Only entities that can take damage like asteroids or enemies will be taken but we will obviously avoid the player. The type of entity that the player need is a destructible element that all entity that can be destroy have and we register in an array all the entities that the player is be able to destroy.



<p id="gdcalert11" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique10.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert12">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique10.png "image_tooltip")


Once the first sort done, it was time to make another more accurate, which is the most important. By taking the view of that from the camera position to the sight, we are able to calculate a field of aim and we can check if one of the previously registered entity is in the field of aim of the player. To check if it is or not in the field of aim, we check if the angle obtained by a dot product from the current aim direction and the current target direction is bigger from the maximum angle that we have set. If it is smaller, we register it in an other array for the target that we can fire at.

 \




<p id="gdcalert12" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique11.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert13">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique11.png "image_tooltip")




Once those entity registered, we just need now to check which on have the smaller angle from the current fire direction and lock it by telling the player that his target is this entity and in which direction it is.



<p id="gdcalert13" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique12.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert14">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique12.png "image_tooltip")


Of course, if there is an entity that can be targeted exactly in the middle of the field of aim, the aiming aid will not be that relevant to have.



<p id="gdcalert14" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique13.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert15">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique13.png "image_tooltip")


But if the target is far from the middle, the player will be grateful that he can shoot at it even if he doesn’t fire at it precisely.



<p id="gdcalert15" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique14.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert16">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique14.png "image_tooltip")




But since this rustic version of the aiming aid, many changes and improvement have been made to it.

Almost at the end of the implementation, the target that was provided by the art team was ready so I was implement them with a new feature. When the player have no entity lock, the sight is in neutral mod and de sight sprite at the left is display. But when one is lock, it is the other one.



<p id="gdcalert16" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique15.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert17">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique15.png "image_tooltip")


<p id="gdcalert17" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique16.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert18">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique16.png "image_tooltip")


An adjustment was quickly imposed as necessary. The player missed almost no targets and it spoiled the gaming experience. The reason was quickly found. The angle that defined the cone in which entities can be targeted was too high and had to be reduced.



<p id="gdcalert18" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique17.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert19">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique17.png "image_tooltip")




But the player was still too powerful and the reason was one more time obvious, he have an unlimited range.  As any entity that entered the screen was potentially targeted, a maximum range had to be set up. So that it’s not too heavy for the cpu, I decided, instead of calculating the distance in a “classic” way with the pythagorean theorem that requires a square root, to calculate the Manhattan distance which contains only an addition of the distances on the X and the Y axis. it is certainly less accurate but also cost less performance.



<p id="gdcalert19" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Blogpost-technique18.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert20">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Blogpost-technique18.png "image_tooltip")




Even if it is not that much, this system is one of the most performance cost of all game system.

Further research will be required but there is some possibility to optimize parts such as angles calculations or the part where the positions of the targetable entities are recovered.

It is not impossible, however, that the aiming aid will be abandoned afterwards or that the system will be readapted if the current version does not match the final vision of the game and the feeling that we want to give to it.