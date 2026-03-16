# Unity Scripting Reference

## 1. Transform & Positioning

The **Transform** component determines where an object sits in the world.

### `transform.position`

* **Purpose:** Gets or sets the $(x, y, z)$ coordinates.
* **Note:** You cannot modify a single axis directly (e.g., `transform.position.x = 10` is invalid). You must assign a new Vector.
* **Example:**
```csharp
// Teleport to a specific coordinate
transform.position = new Vector3(10f, 5f, 0f);

```



### `Vector2` & `Vector3`

* **Purpose:** Data structures for positions and directions.
* **Usage:** Use `Vector2` for movement math and `Vector3` for anything interacting with `transform.position`.
* **Example:**
```csharp
Vector2 movement = new Vector2(1f, 0f); // Representing "Right"

```



---

## 2. Input Handling

Capturing player intent via the keyboard.

### `Input.GetAxisRaw()`

* **Purpose:** Returns `-1`, `0`, or `1` based on input ($W, A, S, D$ or Arrows).
* **Usage:** "Raw" input is used for snappy, grid-like movement perfect for puzzles.
* **Example:**
```csharp
float x = Input.GetAxisRaw("Horizontal"); // Left = -1, Right = 1
float y = Input.GetAxisRaw("Vertical");   // Down = -1, Up = 1

```



---

## 3. Physics & Interaction

Determining what happens when the player touches something.

### `OnTriggerEnter2D(Collider2D other)`

* **Purpose:** Runs code when the player overlaps with a "Trigger" (like a pressure plate or treasure).
* **Example:**
```csharp
private void OnTriggerEnter2D(Collider2D other) {
    if (other.CompareTag("Goal")) {
        Debug.Log("Level Complete!");
    }
}

```



### `OnCollisionEnter2D(Collision2D collision)`

* **Purpose:** Runs code when the player hits a solid object (like a wall or a damaging trap).
* **Example:**
```csharp
private void OnCollisionEnter2D(Collision2D collision) {
    if (collision.gameObject.CompareTag("Spikes")) {
        RestartLevel();
    }
}

```



---

## 4. Time & Smoothness

Ensuring the game runs the same on every computer.

### `Time.deltaTime`

* **Purpose:** The time in seconds it took to complete the last frame.
* **Usage:** Multiply your movement speed by this to prevent players with faster PCs from moving faster.
* **Example:**
```csharp
float speed = 5f;
transform.position += direction * speed * Time.deltaTime;

```



---

## 5. Animation Control

Linking code logic to the visual 4-directional animations.

### `Animator.SetBool()` / `Animator.SetFloat()`

* **Purpose:** Sends data to the Animator window to trigger transitions.
* **Example:**
```csharp
// Logic for walking up
if (y > 0) {
    animator.SetFloat("MoveY", 1);
    animator.SetBool("isWalking", true);
}

```



---

## 6. Script Communication

How one object talks to another.

### `GetComponent<T>()`

* **Purpose:** Accesses other components (like the SpriteRenderer or a custom script) on a GameObject.
* **Example:**
```csharp
// Change the player's color when they hit a powerup
GetComponent<SpriteRenderer>().color = Color.blue;

```



---

## 7. Object Management

Creating and identifying objects at runtime.

### `Instantiate()`

* **Purpose:** Spawns a **Prefab** (blueprint) into the scene.
* **Example:**
```csharp
public GameObject puffOfSmoke;
// Spawn smoke at the player's position
Instantiate(puffOfSmoke, transform.position, Quaternion.identity);

```



### `CompareTag()`

* **Purpose:** A high-performance way to check what an object is.
* **Example:**
```csharp
if (gameObject.CompareTag("Player")) { /* Do something */ }

```



---

## 8. Scene & Game Flow

Transitioning between rooms or restarting.

### `SceneManager.LoadScene()`

* **Purpose:** Loads a specific level. Requires `using UnityEngine.SceneManagement;` at the top of the script.
* **Example:**
```csharp
// Reload the current level
SceneManager.LoadScene(SceneManager.GetActiveScene().name);

```

---

## 9. Object Lifetime

### `Destroy()`

* **Purpose:** Removes a GameObject, component, or asset from the game permanently.
* **Usage:** Use this for items the player picks up, enemies that are defeated, or projectiles that hit a wall. You can also add an optional delay in seconds.
* **Example:**
```csharp
// Destroy the coin when the player touches it
Destroy(gameObject);

// Destroy an object after a 3-second delay
Destroy(gameObject, 3f);

```
