# 🧟 Roblox Tower Defense – Creating Enemy Pathing

This guide shows how to create a **basic path system** for enemies in a tower defense game using **waypoints**.

---

# 1. Create the Path

First, build the **path that enemies will follow** in your map.

Make sure to **anchor** your path so it doesn't move

<img width="1728" height="1117" alt="Screenshot 2026-03-10 at 7 48 43 am" src="https://github.com/user-attachments/assets/d905fd64-6634-40fc-83c8-7e55a6630c05" />

---

# 2. Add an Enemy Model

Insert an enemy model (for example a **Zombie**) into the game.

![Enemy Model](https://github.com/user-attachments/assets/9787ec51-2e47-4c2d-badc-92b8e7d56959)

---

# 3. Create Waypoints

Waypoints tell the enemy **where to walk**.

1. Create a **Folder** in `Workspace`
2. Name it: waypoints
3. Inside the folder, add **Parts** along the path.
4. Anchor the waypoints and disable the collision

<img width="1728" height="1117" alt="Screenshot 2026-03-10 at 11 55 28 am" src="https://github.com/user-attachments/assets/287e0570-ec6a-48bd-8c31-f124b33dd49e" />

---

# 4. Number each part from the beginning to the end

<img width="373" height="244" alt="image" src="https://github.com/user-attachments/assets/3c8b735c-e103-4e46-92dc-e250929b0f3e" />

---

# 5. Create a script in the enemy model

<img width="390" height="61" alt="image" src="https://github.com/user-attachments/assets/d870ce12-c1b1-4f51-9c9f-1049d490ae43" />

---

# 6. Enemy Movement Script

### Getting the Zombie and Waypoints

```lua
local zombie = script.Parent
local waypoints = workspace.waypoints
```

### Loop through each waypoint and make the zombie go to each waypoint from 1 to the last number

```lua
for waypoint = 1, #waypoints:GetChildren() do
	zombie.Humanoid:MoveTo(waypoints[waypoint].Position)
	zombie.Humanoid.MoveToFinished:Wait()
end
```

# 🧟 Roblox Tower Defense – Creating Enemy Pathing Part 2

# 1. Add a Script and a Module Script inside of that Script

## Rename the Script to Main and the Module Script to Mob

<img width="205" height="61" alt="image" src="https://github.com/user-attachments/assets/25c1e5b5-f963-4025-9b86-302bf5109068" />

# 2. Make a new folder and rename it to what you want your map to be called

<img width="300" height="66" alt="image" src="https://github.com/user-attachments/assets/ad2d7349-e75d-47a2-a42b-e31dc3144ec3" />

# 3. Decorate your map

<img width="857" height="813" alt="image" src="https://github.com/user-attachments/assets/1db01107-efa1-4133-b214-a41e8ffc27e1" />

# 4. Make a starting position

### Rename it to Start
### Anchor and Disable Collision

<img width="1728" height="1117" alt="image" src="https://github.com/user-attachments/assets/a30bdbc4-075c-4c70-a709-71f263e714ae" />

### Make sure that it is facing the right way

You can check this by: Right Clicking on **Start** and clicking **Show Orientation Indictator**

<img width="1728" height="1117" alt="image" src="https://github.com/user-attachments/assets/f27e1035-6265-4d3b-bf3e-8a6b12f28e25" />


# 5. Spawn the Mob

In the **mob script**

Make a function for spawning the mob

```lua
local ServerStorage = game:GetService("ServerStorage")
local mob = {}

function mob.Spawn(name, map)
	local mobExists = ServerStorage.Mobs:FindFirstChild(name)
	
	if mobExists then
		local newMob = mobExists:Clone()
		newMob.HumanoidRootPart.CFrame = map.Start.CFrame
		newMob.Parent = workspace
	end
end

return mob
```

# 6. Call the Function

In **Main Script**
Write the code to call the function that will spawn in the mob

```
local mob = require(script.Mob)
local map = workspace.grassland

mob.Spawn("Zombie", map)
```

# 7. Write a movement function for the mob

### In the **Mob Script**, create a function for movement
```lua
function mob.Spawn(name, map)

end
```

### Copy the code from the zombie script 

```lua
function mob.Move(mob, map)
	local zombie = script.Parent
	local waypoints = workspace.waypoints

	for waypoint=1, #waypoints:GetChildren() do 
		zombie.Humanoid:MoveTo(waypoints[waypoint].Position)
		zombie.Humanoid.MoveToFinished:Wait()
	end
end
```

### Update the Script

Instead of using script.Parent, use the mob parameter so the function works for any mob.

```lua
function mob.Move(mob, map)
	local humanoid = mob:WaitForChild("Humanoid")
	local waypoints = map.waypoints

	for waypoint=1, #waypoints:GetChildren() do 
		humanoid:MoveTo(waypoints[waypoint].Position)
		humanoid.MoveToFinished:Wait()
	end
end
```
<img width="405" height="688" alt="image" src="https://github.com/user-attachments/assets/c8afd9d3-a559-4653-9d07-53c56ba78c37" />

### Call the move function every time the mob has been spawned

```lua
function mob.Spawn(name, map)
	local mobExists = ServerStorage.Mobs:FindFirstChild(name)
	
	if mobExists then
		local newMob = mobExists:Clone()
		newMob.HumanoidRootPart.CFrame = map.Start.CFrame
		newMob.Parent = workspace
		
		mob.Move(newMob, map) --Add this line here
	else 
		warn("Requested Mob does not exist:", name)
	end
end
```

# 8. Use a loop to continuously spawn in a zombie

