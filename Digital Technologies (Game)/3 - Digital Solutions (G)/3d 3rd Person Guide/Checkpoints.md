# Checkpoints 

Steps:
1. Create the checkpoint flag scene
2. Checkpoint script on Flag
3. Add checkpoint functionality to Player
4. Dying and resetting

### Making a Flag
Not too complex! Here's my basic flag that I made, I just added some basic materials to the shapes
- Flagpole is a CSG Cylinder
- Flag is a CSG Box
- I added the CSG Sphere for a ballpoint at the top of the flag

![[Pasted image 20260504104757.png]]
![[Pasted image 20260504104921.png]]
I then added the extra nodes that we will use when programming the functionality. 
- The Area3D and collision shape are for detecting the player. I gave it a cylindrical collision shape.
- The Marker3D is for specifying the exact position the player is going to spawn to. In my case it's just at the bottom of the flagpole. The handy thing is that you will be able to change it on specific checkpoints, you'll just need to open the "editable children"

### Checkpoint Script
```gdscript
extends Node3D

@export var unclaimed_mat: StandardMaterial3D
@export var claimed_mat: StandardMaterial3D

@onready var flag : CSGBox3D = $Flag

var claimed = false

func _ready():
	flag.material = unclaimed_mat

func _on_area_3d_body_entered(body):
	if body is Player and claimed == false:
		claimed = true
		flag.material = claimed_mat
		body.set_checkpoint($Spawnpoint)

```
Not a wild script by any means, but it adds a few things to the to-do list from here:
- Since I've exported two materials you'll just need to set them up in the Checkpoint Scene editor; I've just left my "unclaimed" as the default white, and set my claimed to be a basic red.
- The flag variable is to reference the actual flag object that will change colour, make sure your object name matches the script
- The script assumes two things
	- The player has a class_name of "Player"
	- The player has a function called "set_checkpoint" - We're about to go and write that now!

### Checkpoint functionality on the Player
Let's edit the default Player.gd script that controls our player's State Machine.
```gdscript
var checkpoint : Node3D

...

func _take_damage(dmg:int):
	hp -= dmg
	if hp <= 0:
		changeState(StateName.DEAD)
		await get_tree().create_timer(2.0).timeout

		respawn()
	else:
		changeState(StateName.DAMAGED)
		
...
#Add these two new functions at the bottom of the script
func set_checkpoint(cp:Node3D):
	checkpoint = cp
	
func respawn():
	hp = 3
	global_position = checkpoint.global_position
	changeState(StateName.SPAWN)

```

- Add the checkpoint variable at the top of your script, that's going to store the position for the player to respawn to
- Edit the `take_damage` function so it now will pause for two seconds when the player dies, and then runs the new `respawn` function 
- The set checkpoint function simply assigns the sent checkpoint node
	- This is one of those instances where you could probably do this just by setting the variable from the other script, but there are system design reasons why this is considered bad practice, and doing it with a function is a better design choice
- The Respawn function resets the HP variable to 3, set's the player position to the checkpoint's position, and then moves the player to the SPAWN state.

### Dying and Resetting
Finally, we need to test the player's ability to die and reset to the checkpoint!
Everything should actually already work here - If you add a checkpoint flag to the test_scene, you can check!
![[Checkpoint_Test.gif]]