# CS381MyTowerDefenseProject

A 3D tower defense game for Unity, where enemies walk a winding road in waves, and I place towers beside it to stop them before they reach the end. Towers aim at where an enemy will be, not where it is now.

I start with 260 coins, 1 life and 8 tower placements.
Destroying enemies earns coins and score. Clearing a wave gives a bonus of 20 + 10 × wave coins.
If any enemy reaches the end of the road, the game ends. Click Restart to play again.

Waves and difficulty
- Wave n spawns 5 + 2 × (n − 1) enemies.
- The gap between spawns shrinks each wave, down to a minimum of 0.42 seconds.
- Enemy health grows 15% per wave. Enemy speed grows 2% per wave, capped at +50%.
- The next wave starts a short time after the previous one is fully cleared.

Project structure
Script	                      Purpose
TowerDefenseStartup.cs - Starts the bootstrap on every scene load, so Restart works
TowerDefenseBootstrap.cs - Builds the camera, ground, road, towers, enemies, projectile and UI
GameManager.cs - Lives, coins, score, wave number, game over and restart
EnemySpawner.cs - Runs the waves and chooses which enemy type to spawn
Enemy.cs - Walks the waypoints, takes damage, rewards coins or costs lives
Tower.cs - Finds targets, predicts their position, rotates the barrel and fires
Projectile.cs - Flies straight and damages the first enemy it hits
TowerPlacement.cs - Handles clicks, placement rules and the placement limit
UIManager.cs - HUD, instructions, messages and the game-over panel
GameInput.cs - Mouse input that works with the old or new Input System

How it works
- Predictive aiming: Tower.GetPredictedPosition solves for the time at which a projectile of the tower's speed meets the enemy moving at its current velocity. The tower fires at that point.
- Target choice: a tower targets the in-range enemy that has travelled furthest along the road.
- Placement rules: towers cannot be built within 2 units of the road or too close to another tower. Clicking a tower counts as an occupied spot.
- Projectile hits: projectiles move in code and test each frame's path against active enemies. They do not rely on physics trigger events. They still have a Rigidbody (no gravity) and a trigger collider.

Known limitations
- There is no sound and no start menu.
- Towers, enemies and the projectile are created in code at startup, so they do not appear as prefabs in the Project window.
- startingLives is 1 (set in GameManager), so one escaped enemy ends the game.
- Colors use material.color, which works in the Built-In Render Pipeline but shows pink in URP.

Credits
Planned assets, all CC0 by Kenney:

Tower Defense Kit: towers, tiles and UFO enemies
Sci-Fi Sounds: shots and explosions

Crediting Kenney is not required, but is appreciated.
