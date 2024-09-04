Sure! Here's a list of common physics-related functions in Godot with descriptions and examples:

### 1. **`apply_impulse(offset: Vector2, impulse: Vector2)`**  
   - **Description:** Applies an impulse at a specific offset from the body's origin. This is useful for creating instant reactions, like a jump or a sudden push.  
   - **Example:**  
     ```gdscript  
     # Assuming this script is attached to a RigidBody2D node  
     func _on_jump():  
         var jump_force = Vector2(0, -300) # Upward impulse  
         apply_impulse(Vector2.ZERO, jump_force) # Apply impulse at the center  
     ```

### 2. **`add_force(offset: Vector2, force: Vector2)`**  
   - **Description:** Adds a continuous force at a specific offset, making the body accelerate in a certain direction. This is used for applying ongoing forces like wind or gravity.  
   - **Example:**  
     ```gdscript  
     # Applying a force to the right  
     func _apply_wind_force():  
         var wind_force = Vector2(200, 0)  
         add_force(Vector2.ZERO, wind_force) # Apply force at the center  
     ```

### 3. **`set_linear_velocity(velocity: Vector2)`**  
   - **Description:** Directly sets the linear velocity of the body. This is useful for overriding the current movement speed or giving an object an initial velocity.  
   - **Example:**  
     ```gdscript  
     # Set a constant speed to the right  
     func _ready():  
         var speed = Vector2(150, 0)  
         set_linear_velocity(speed)  
     ```

### 4. **`set_angular_velocity(angular_velocity: float)`**  
   - **Description:** Sets the angular velocity of the body, which controls how fast it rotates. Useful for spinning objects.  
   - **Example:**  
     ```gdscript  
     # Set a constant spin to the object  
     func _ready():  
         set_angular_velocity(3.14) # Rotate at 180 degrees per second  
     ```

### 5. **`move_and_slide(velocity: Vector2, up_direction: Vector2 = Vector2(0, -1)) -> Vector2`**  
   - **Description:** Moves the body along a velocity vector, and slides along surfaces. This is commonly used in kinematic bodies for platformer-style movement.  
   - **Example:**  
     ```gdscript  
     # Assuming this script is attached to a KinematicBody2D  
     var velocity = Vector2()  
     var speed = 200

     func _physics_process(delta):  
         velocity.x = Input.get_action_strength("ui_right") - Input.get_action_strength("ui_left")  
         velocity.y += 20 # Gravity effect  
         velocity = velocity.normalized() * speed  
         move_and_slide(velocity, Vector2.UP)  
     ```

### 6. **`move_and_collide(velocity: Vector2) -> KinematicCollision2D`**  
   - **Description:** Moves the body along a velocity vector, but stops when a collision occurs. This is used when you want to manually handle collisions.  
   - **Example:**  
     ```gdscript  
     # Assuming this script is attached to a KinematicBody2D  
     var velocity = Vector2(100, 0)

     func _physics_process(delta):  
         var collision = move_and_collide(velocity * delta)  
         if collision:  
             print("Collision detected with: ", collision.collider.name)  
     ```

### 7. **`apply_central_impulse(impulse: Vector2)`**  
   - **Description:** Similar to `apply_impulse`, but applies the impulse directly at the center of mass.  
   - **Example:**  
     ```gdscript  
     # Applying an upward impulse to make the object jump  
     func _on_jump():  
         var jump_impulse = Vector2(0, -300)  
         apply_central_impulse(jump_impulse)  
     ```

### 8. **`_integrate_forces(state: Physics2DDirectBodyState)`**  
   - **Description:** Custom integration of physics forces. This function allows for advanced physics calculations and control over the physics simulation.  
   - **Example:**  
     ```gdscript  
     # Custom gravity  
     func _integrate_forces(state):  
         var custom_gravity = Vector2(0, 98)  
         state.linear_velocity += custom_gravity * state.step  
     ```

### 9. **`add_central_force(force: Vector2)`**  
   - **Description:** Adds a continuous force at the center of mass. Similar to `add_force`, but it's applied centrally.  
   - **Example:**  
     ```gdscript  
     # Applying a constant force downward (custom gravity)  
     func _ready():  
         add_central_force(Vector2(0, 500))  
     ```

### 10. **`set_mode(mode: int)`**  
   - **Description:** Sets the mode of the physics body, which can be static, kinematic, rigid, or character. This is useful for dynamically changing how an object interacts with the physics world.  
   - **Example:**  
     ```gdscript  
     # Switching to kinematic mode  
     func _on_switch_mode():  
         set_mode(RigidBody2D.MODE_KINEMATIC)  
     ```

These functions are essential for handling physics in 2D games within Godot. Each one serves a different purpose, from applying instantaneous forces to handling continuous movement and collisions.  
