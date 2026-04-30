# Laser State Machine

Today, we're going to be making a basic FSM based on a timed laser that our player will need to navigate around. This is basically the goal:

![[laser_eg.gif]]

So let's break down the requirements:
1. Basic 2D Player
2. Laser Node Setup
3. Scripting the State Machine

### Basic 2D Player
Today, we're just going to use the Godot logo for the player image, and we're keeping it very simple in terms of node structure:
![[Pasted image 20260429122331.png]]
After the screenshot I renamed the CharacterBody2D to "Player" - this is important for programming later!
Here's the script you'll need to pop onto the Player. It's built on the default CharacterBody2D script, but altered to make it top-down rather than platformer (with X and Y movement, and no gravity)

I've also included a function to make the player respawn; our lasers are going to call that function if they hit the player.
```gdscript
extends CharacterBody2D

const SPEED = 300.0
var spawn_point

func _ready():
	spawn_point = position

func _physics_process(delta):
	var direction = Input.get_vector("ui_left","ui_right", "ui_up", "ui_down")
	if direction:
		velocity = direction * SPEED
	else:
		velocity = Vector2.ZERO

	move_and_slide()

func respawn():
	position = spawn_point


```

### Laser Node Setup
Next, let's setup our Laser system. 
We need a couple visual elements; first the "Laser Emitter", and then the physical laser that comes out.
Take a look at the Node structure I've used here, and what it looks like
![[Pasted image 20260429124812.png]]![[Pasted image 20260429125217.png]]
The Node2D is just to hold everything and control the positions easily, the ColorRect is just the easiest way to show the laser emitter (it feels important to have it!), and the Line 2D is set up with the following properties:
![[Pasted image 20260429123736.png]]

The Area2D is given a CollisionShape2D, but the key element here is the CollisionShape2D is set up with a *SegmentShape2D*. This is going to let us set the laser's collision to match the visual laser!
![[Pasted image 20260429124924.png]]

Throw in a timer for good measure!

### Programming the Laser State Machine
We've got a few things to do here, the first is making the laser work!

```gdscript
extends Node2D

@onready var line_2d = $Line2D
@onready var collision_shape_2d = $Area2D/CollisionShape2D
@onready var timer = $Timer

enum states {OFF, WARMUP, ON, COOL}
var current_state = null

# Called when the node enters the scene tree for the first time.
func _ready():
	collision_shape_2d.shape.a = line_2d.points[0]
	change_state(states.OFF)

# Called every frame. 'delta' is the elapsed time since the previous frame.
func _process(delta):
	
	match current_state:
		states.OFF:
			pass
		states.WARMUP:
			laser_warmup(delta)
		states.ON:
			pass
		states.COOL:
			laser_cool(delta)

func change_state(new_state):
	current_state = new_state
	print("moving to " + states.keys()[current_state])
	# Handle "Entry" logic for specific states
	match current_state:
		states.OFF:
			timer.start(1.0)
		states.WARMUP:
			timer.stop()
		states.ON:
			timer.start(2.0)
		states.WARMUP:
			timer.stop()

func laser_warmup(delta):
	line_2d.points[1].y += 100*delta
	collision_shape_2d.shape.b = line_2d.points[1]
	if line_2d.points[1].y > 200:
		change_state(states.ON)

func laser_cool(delta):
	line_2d.points[1].y -= 50*delta
	collision_shape_2d.shape.b = line_2d.points[1]
	if line_2d.points[1].y <= 0:
		change_state(states.OFF)
	
func _on_timer_timeout():
	print("TIME")
	
	if current_state == states.OFF:
		change_state(states.WARMUP)
	elif current_state == states.ON:
		change_state(states.COOL)
		
func _on_area_2d_body_entered(body):
	if body.name == "Player":
		print("HIT")
		body.respawn()

```