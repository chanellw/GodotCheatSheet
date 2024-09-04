Sure\! Here's a list of common physics-related functions in Godot with descriptions and examples:

\#\#\# 1\. \*\*\`apply\_impulse(offset: Vector2, impulse: Vector2)\`\*\*  
   \- \*\*Description:\*\* Applies an impulse at a specific offset from the body's origin. This is useful for creating instant reactions, like a jump or a sudden push.  
   \- \*\*Example:\*\*  
     \`\`\`gdscript  
     \# Assuming this script is attached to a RigidBody2D node  
     func \_on\_jump():  
         var jump\_force \= Vector2(0, \-300) \# Upward impulse  
         apply\_impulse(Vector2.ZERO, jump\_force) \# Apply impulse at the center  
     \`\`\`

\#\#\# 2\. \*\*\`add\_force(offset: Vector2, force: Vector2)\`\*\*  
   \- \*\*Description:\*\* Adds a continuous force at a specific offset, making the body accelerate in a certain direction. This is used for applying ongoing forces like wind or gravity.  
   \- \*\*Example:\*\*  
     \`\`\`gdscript  
     \# Applying a force to the right  
     func \_apply\_wind\_force():  
         var wind\_force \= Vector2(200, 0\)  
         add\_force(Vector2.ZERO, wind\_force) \# Apply force at the center  
     \`\`\`

\#\#\# 3\. \*\*\`set\_linear\_velocity(velocity: Vector2)\`\*\*  
   \- \*\*Description:\*\* Directly sets the linear velocity of the body. This is useful for overriding the current movement speed or giving an object an initial velocity.  
   \- \*\*Example:\*\*  
     \`\`\`gdscript  
     \# Set a constant speed to the right  
     func \_ready():  
         var speed \= Vector2(150, 0\)  
         set\_linear\_velocity(speed)  
     \`\`\`

\#\#\# 4\. \*\*\`set\_angular\_velocity(angular\_velocity: float)\`\*\*  
   \- \*\*Description:\*\* Sets the angular velocity of the body, which controls how fast it rotates. Useful for spinning objects.  
   \- \*\*Example:\*\*  
     \`\`\`gdscript  
     \# Set a constant spin to the object  
     func \_ready():  
         set\_angular\_velocity(3.14) \# Rotate at 180 degrees per second  
     \`\`\`

\#\#\# 5\. \*\*\`move\_and\_slide(velocity: Vector2, up\_direction: Vector2 \= Vector2(0, \-1)) \-\> Vector2\`\*\*  
   \- \*\*Description:\*\* Moves the body along a velocity vector, and slides along surfaces. This is commonly used in kinematic bodies for platformer-style movement.  
   \- \*\*Example:\*\*  
     \`\`\`gdscript  
     \# Assuming this script is attached to a KinematicBody2D  
     var velocity \= Vector2()  
     var speed \= 200

     func \_physics\_process(delta):  
         velocity.x \= Input.get\_action\_strength("ui\_right") \- Input.get\_action\_strength("ui\_left")  
         velocity.y \+= 20 \# Gravity effect  
         velocity \= velocity.normalized() \* speed  
         move\_and\_slide(velocity, Vector2.UP)  
     \`\`\`

\#\#\# 6\. \*\*\`move\_and\_collide(velocity: Vector2) \-\> KinematicCollision2D\`\*\*  
   \- \*\*Description:\*\* Moves the body along a velocity vector, but stops when a collision occurs. This is used when you want to manually handle collisions.  
   \- \*\*Example:\*\*  
     \`\`\`gdscript  
     \# Assuming this script is attached to a KinematicBody2D  
     var velocity \= Vector2(100, 0\)

     func \_physics\_process(delta):  
         var collision \= move\_and\_collide(velocity \* delta)  
         if collision:  
             print("Collision detected with: ", collision.collider.name)  
     \`\`\`

\#\#\# 7\. \*\*\`apply\_central\_impulse(impulse: Vector2)\`\*\*  
   \- \*\*Description:\*\* Similar to \`apply\_impulse\`, but applies the impulse directly at the center of mass.  
   \- \*\*Example:\*\*  
     \`\`\`gdscript  
     \# Applying an upward impulse to make the object jump  
     func \_on\_jump():  
         var jump\_impulse \= Vector2(0, \-300)  
         apply\_central\_impulse(jump\_impulse)  
     \`\`\`

\#\#\# 8\. \*\*\`\_integrate\_forces(state: Physics2DDirectBodyState)\`\*\*  
   \- \*\*Description:\*\* Custom integration of physics forces. This function allows for advanced physics calculations and control over the physics simulation.  
   \- \*\*Example:\*\*  
     \`\`\`gdscript  
     \# Custom gravity  
     func \_integrate\_forces(state):  
         var custom\_gravity \= Vector2(0, 98\)  
         state.linear\_velocity \+= custom\_gravity \* state.step  
     \`\`\`

\#\#\# 9\. \*\*\`add\_central\_force(force: Vector2)\`\*\*  
   \- \*\*Description:\*\* Adds a continuous force at the center of mass. Similar to \`add\_force\`, but it's applied centrally.  
   \- \*\*Example:\*\*  
     \`\`\`gdscript  
     \# Applying a constant force downward (custom gravity)  
     func \_ready():  
         add\_central\_force(Vector2(0, 500))  
     \`\`\`

\#\#\# 10\. \*\*\`set\_mode(mode: int)\`\*\*  
   \- \*\*Description:\*\* Sets the mode of the physics body, which can be static, kinematic, rigid, or character. This is useful for dynamically changing how an object interacts with the physics world.  
   \- \*\*Example:\*\*  
     \`\`\`gdscript  
     \# Switching to kinematic mode  
     func \_on\_switch\_mode():  
         set\_mode(RigidBody2D.MODE\_KINEMATIC)  
     \`\`\`

These functions are essential for handling physics in 2D games within Godot. Each one serves a different purpose, from applying instantaneous forces to handling continuous movement and collisions.  
