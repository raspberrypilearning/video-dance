## Getting the player to dance

Now it's time for the player to try and have a go at dancing, and give them some clues as to what moves they need to do.

--- task ---
Add some blocks to tell the player that it is their turn to play and then add in a `broadcast`{:class="block3events"} to signal this to other sprites.

![dance sprite](images/dance_sprite.png)
```blocks3
when flag clicked
wait (1) seconds
set [level v] to (1)
set [beats v] to (1)
forever
delete all of [moves v]
repeat (level)
add (pick random (1) to (4)) to [moves v]
set [move v] to (item (length of [moves v]) of [moves v])
switch costume to (move)
play drum (move) for (beats) beats
end
+say [now it's your turn] for (1) seconds
+broadcast [start dancing v]
```
--- /task ---


Now you need to add some code that will keep the dancer sprite waiting until the player has finished their turn. The idea is that the players actions are stored in another list called `actions`{:class="block3variables"}. The `actions`{:class="block3variables"} list should be the same length as the `moves`{:class="block3variables"} list by the end of the player's turn

--- task ---
Create a new list called `actions`{:class="block3variables"}. This is where all the player's actions will be stored as they dance.
--- /task ---

--- task ---
Add in a `wait until`{:class="block3control"} that compares the length of the two lists.
![dance sprite](images/dance_sprite.png)
```blocks3
when flag clicked
wait (1) seconds
set [level v] to (1)
set [beats v] to (1)
forever
delete all of [moves v]
repeat (level)
add (pick random (1) to (4)) to [moves v]
set [move v] to (item (length of [moves v]) of [moves v])
switch costume to (move)
play drum (move) for (beats) beats
end
say [now it's your turn] for (1) seconds
broadcast [start dancing v]
+wait until <(length of [actions v]) = (length of [moves v])>
```
--- /task ---
The next set of code blocks will be added to the circle sprite you made at the start.

--- task ---
Begin by starting the script by receiving the broadcast.

![pad](images/pad.png)
```blocks3
when I receive [start dancing v]
```
--- /task ---

Variables in Scratch come in two varieties. One that is a variable that all Sprites can use, and the other is a variable that only the sprite it was created for can use.

--- task ---
Create a variable called `pad`{:class="block3variables"}, and make sure it is `For this Sprite only`

![create a variable](images/create_variable.png)

The variable can be set to a value of `1`{:class="block3variables"}

![pad](images/pad.png)
```blocks3
when I receive [start dancing v]
+set [pad v] to (1)
```
--- /task ---

At the moment, the `moves`{:class="block3variables"} list contains only one random number. As the game gets more difficult though, more random numbers will be added.

If the players actions are being stored in the `actions`{:class="block3variables"} list, then we know that when the two lists are the same size, the player has finished that round of dancing.

--- task ---
Use a `repeat until`{:class="block3control"} block to keep the script running until the two lists are of equal length.

![pad](images/pad.png)
```blocks3
when I receive [start dancing v]
set [pad v] to (1)
+ repeat until <(length of [actions v]) = (length of [moves v])>
```
--- /task ---

The Video sensing extension lets you detect if there is movement over a sprite.

--- task ---
Add the Video sensing extension in the same way you added the Music extension
--- /task ---

--- task ---
Create a new variable called `sensitivity`{:class="block3variables"}. (This should be for all sprites). This will be used to adjust how sensitive your sprites are to the video motion.
--- /task ---

--- task ---
Now you can check to see if the `video motion`{:class="block3extension"} is greater than the `sensitivity`{:class="block3variables"}

![pad](images/pad.png)
```blocks3
when I receive [start dancing v]
set [pad v] to (1)
repeat until <(length of [actions v]) = ()>
+if  <(video [motion v] on [sprite v]) > (length of [moves v])> then
```
--- /task ---

--- task ---
If this `if then`{:class="block3control"} is true, then the player has "touched" the sprite and so you can add the `pad`{:class="block3variables"} value into the `actions`{:class="block3variables"} list, and then play a drum beat.

![pad](images/pad.png)
```blocks3
when I receive [start dancing v]
set [pad v] to (1)
repeat until <(length of [actions v]) = ()>
if  <(video [motion v] on [sprite v]) > (length of [moves v])> then
+add (pad) to [actions v]
+play drum (pad) for (beats) beats
```
--- /task ---

--- task ---
Click the green flag and wait for the sprite to tell you to start dancing. Then wave a hand so that it passes over the pad sprite. You should hear a drumbeat.
--- /task ---
