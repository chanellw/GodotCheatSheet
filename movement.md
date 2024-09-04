Sure! Here’s a list of helpful GDScript functions for character or object movement in Godot, along with descriptions and examples:

### 1. **`move_toward(target_position: Vector2, speed: float) -> Vector2`**
   - **Description:** Moves an object toward a target position at a constant speed. This function calculates the new position by interpolating between the current position and the target.
   - **Example:**
     ```gdscript
     func move_toward_target(delta):
         var current_position = position
         var target_position = Vector2(500, 300)
         var speed = 200
         
         position = current_position.move_toward(target_position, speed * delta)
     ```

### 2. **`look_at(target_position: Vector2)`**
   - **Description:** Rotates the object to face the target position. This is useful for making characters or objects face the direction they're moving or aiming at.
   - **Example:**
     ```gdscript
     func _process(delta):
         var target_position = get_global_mouse_position()
         look_at(target_position)
     ```

### 3. **`lerp(start: float, end: float, weight: float) -> float`**
   - **Description:** Linearly interpolates between two values based on a weight (0 to 1). This is commonly used for smooth transitions, like movement or animation blending.
   - **Example:**
     ```gdscript
     var speed = 100

     func _process(delta):
         position.x = lerp(position.x, target_position.x, 0.1)
     ```

### 4. **`lerp_angle(from: float, to: float, weight: float) -> float`**
   - **Description:** Similar to `lerp`, but for angles. It smoothly interpolates between two angles and is used for smooth rotation transitions.
   - **Example:**
     ```gdscript
     func _process(delta):
         rotation = lerp_angle(rotation, target_rotation, 0.1)
     ```

### 5. **`clamp(value: float, min: float, max: float) -> float`**
   - **Description:** Clamps a value between a minimum and maximum. This is useful to restrict movement within certain bounds, like keeping a player within the screen limits.
   - **Example:**
     ```gdscript
     func _process(delta):
         position.x = clamp(position.x, 0, screen_width)
     ```

### 6. **`move_and_slide_with_snap(velocity: Vector2, snap: Vector2, stop_on_slope: bool = false, max_slides: int = 4, floor_max_angle: float = 0.785398, infinite_inertia: bool = true) -> Vector2`**
   - **Description:** Similar to `move_and_slide`, but allows snapping to surfaces, which is useful for slopes and stairs.
   - **Example:**
     ```gdscript
     var velocity = Vector2()
     var snap_vector = Vector2(0, 16) # Snap downwards

     func _physics_process(delta):
         velocity.y += 20 # Gravity
         velocity = move_and_slide_with_snap(velocity, snap_vector, Vector2.UP)
     ```

### 7. **`move_and_collide(velocity: Vector2) -> KinematicCollision2D`**
   - **Description:** Moves the body along a velocity vector and stops when a collision occurs. This is useful for precise movement and collision detection.
   - **Example:**
     ```gdscript
     func _physics_process(delta):
         var velocity = Vector2(100, 0)
         var collision = move_and_collide(velocity * delta)
         
         if collision:
             print("Collided with:", collision.collider.name)
     ```

### 8. **`distance_to(target: Vector2) -> float`**
   - **Description:** Returns the distance between the current position and the target position. Useful for determining proximity or triggering events based on distance.
   - **Example:**
     ```gdscript
     func _process(delta):
         if position.distance_to(target_position) < 10:
             print("Close to target")
     ```

### 9. **`direction_to(target: Vector2) -> Vector2`**
   - **Description:** Returns the normalized direction vector pointing from the current position to the target position. Useful for moving toward a target.
   - **Example:**
     ```gdscript
     func _process(delta):
         var direction = position.direction_to(target_position)
         position += direction * speed * delta
     ```

### 10. **`move_and_slide(velocity: Vector2, up_direction: Vector2 = Vector2(0, -1)) -> Vector2`**
   - **Description:** Moves the object along a velocity vector, sliding along surfaces. Ideal for kinematic bodies, especially in platformers.
   - **Example:**
     ```gdscript
     var velocity = Vector2()

     func _physics_process(delta):
         velocity.y += 20 # Gravity effect
         velocity.x = Input.get_action_strength("ui_right") - Input.get_action_strength("ui_left") * speed
         velocity = move_and_slide(velocity, Vector2.UP)
     ```

These functions can greatly help with various movement and positioning needs in your Godot projects. Whether you're controlling a player character, moving objects around, or creating smooth transitions, these examples should give you a solid foundation.