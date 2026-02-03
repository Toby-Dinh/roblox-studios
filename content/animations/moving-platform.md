## Set Up

## 1. Create Your Parts
- **Moving Platform**: This is the part that will move.
- **End Points**: Create two separate parts to mark the start and end positions of the platform.

<img width="1520" height="776" alt="image" src="https://github.com/user-attachments/assets/98bcd053-fad3-4cd0-894b-6b091aaafaf3" />
<img width="340" height="185" alt="image" src="https://github.com/user-attachments/assets/18195af1-bfd9-46fc-b740-d6cf883538b2" />

## 2. Configure the Parts
- **Anchor the end points** so they stay in place.
- **Unanchor the moving platform** so it can move.
- Optionally, set the **transparency of the end points to 1** to make them invisible in-game.

https://github.com/user-attachments/assets/a50177ab-4ea0-40ef-8992-77914dcca15e

## 3. Scripting: Add Movement

Add a script to your moving platform

<img width="295" height="207" alt="image" src="https://github.com/user-attachments/assets/42311938-c9dc-4bba-9fd1-743e564ac30d" />

### 1. Get the Moving Platform

```lua
local movingPlatform = script.Parent
```
> Note:
> `movingPlatform` refers to the platform this script is attached to.
> `script.Parent` means the script controls the part it is a child of.

### 2. Get the Start and End Positions

```lua
local StartPart = game.Workspace:WaitForChild("StartPos")
local EndPart = game.Workspace:WaitForChild("EndPos")
```

> Note:
> `StartPart` and `EndPart` are the invisible parts that mark the start and end positions.
> `WaitForChild` ensures the script waits until the parts exist before continuing.

### 3. Create a BodyPosition

1. `local bodyPosition = Instance.new("BodyPosition")` – Create a new BodyPosition object.  
2. `bodyPosition.Parent = movingPlatform` – Attach it to the platform you want to move.  
3. `bodyPosition.MaxForce = Vector3.new(5000, 5000, 5000)` – Set how strongly it pulls the platform toward the target position.

```lua
local bodyPosition = Instance.new("BodyPosition")
bodyPosition.Parent = movingPlatform
bodyPosition.MaxForce = Vector3.new(5000, 5000, 5000)
```

This creates a `BodyPosition` object that allows the part to move smoothly to a target position.

### 4. Lock the starting and ending positions
```lua
local startPos = StartPart.Position
local endPos = EndPart.Position
```

### 5. Movement loop

```lua
while true do
	bodyPosition.Position = endPos
	task.wait(2)

	bodyPosition.Position = startPos
	task.wait(2)
end
```
