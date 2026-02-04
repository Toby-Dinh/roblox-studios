# Movement in Roblox Studio: Holding Shift to Sprint Tutorial

To add movement mechanics to our players (like sprinting, walking, sliding), we need to start scripting in `StarterCharacterScripts`.

> **Note:**  
> `StarterCharacterScripts` runs scripts inside the player’s character and resets every time they respawn.
> `StarterPlayerScripts`, on the other hand, runs scripts once per player and does not reset on respawn.

## Step 1. 

Create a `LocalScript` in `StarterPlayer`/`StarterCharacterScripts`

> **Note:**  
> `LocalScript` is an object that contains and runs Luau code on the client (player's device) instead of the server.
> `Script` on the otherhand, contains and runs Luau code on the server 

<img width="243" height="62" alt="image" src="https://github.com/user-attachments/assets/874befad-cee4-441b-8354-82e11f841659" />

## Step 2. 

To detect any input from the player, first get the UserInputService:

```luau
local UserInputService = game:GetService("UserInputService")
```

This service allows your script to listen for any type of input, such as keyboard presses, mouse clicks, or touch events.

## Step 3. 

We now need to get the `Character` and the `Humanoid` so that we can modify things like speed, jump or animations

```luau
local Character = script.Parent
local Humanoid = Character:WaitForChild("Humanoid")
```

## Step 4. 

Now, we need to make a function that make the player **sprint** when they hold **Left Shift**

```luau
UserInputService.InputBegan:Connect(function(input)
	
end)
```

This line of code runs then function when the player starts an input (like pressing key)

> **Note:**  
> `UserInputService.InputBegan` runs code whenever the player starts an input (like pressing **shift**)
> `:Connect(function(input) ... end)` runs the code inside the function whenever the input starts
> the **input** parameter is used to pass information on which key or mouse button was clicked

## Step 5.

We then need to check if the user is holding the **Left Shift** key

We can do this by using an **if statement to check if the user is pressing the **Left Shift** key

```luau
UserInputService.InputBegan:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then

	end
end)
```

The code inside runs only if Left Shift is pressed.

If any other key is pressed, nothing happens.

## Step 6.

Add this line of code inside the **If statement**

```luau
UserInputService.InputBegan:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
      Humanoid.WalkSpeed = 50	
	end
end)
```

This makes the player's speed faster when they hold shift now!

## Step 7.

To stop the player from sprinting when they releases **Left Shift**, we can use `InputEnded` 

> **Note:**
> Fires when a user stops interacting with an input device such as a mouse or gamepad.

```luau
UserInputService.InputEnded:Connect(function(input)

end)
```

This event fires when the player stops using an input, like releasing a key, letting go of a mouse button, or lifting a finger from the screen.

## Step 8. 

Check if the user has let go of **Left Shift** and and if they do, then change the `WalkSpeed` to the walking speed

```luau
UserInputService.InputEnded:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
      Humanoid.WalkSpeed = 20	
	end
end)
```

This stops the sprint as soon as **Left Shift** is let go and sets the player's speed to 20 instead of 50

## Test your code
Hold the **Left Shift** key to see if the player's speed gets faster and let go of the key to check if the player's speed resets to default!

## Full Code
```luau
local UserInputService = game:GetService("UserInputService")

local Character = script.Parent
local Humanoid = Character:WaitForChild("Humanoid")

UserInputService.InputBegan:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
		Humanoid.WalkSpeed = 50	
		isRunning = true
	end
end)

UserInputService.InputEnded:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
		Humanoid.WalkSpeed = 20	
		isRunning = false
	end
end)
```

# Movement in Roblox Studio: Adding Run, Walk and Idle Animations

Before writing the script for your animations, you need to first create or import the animations you want to use.

This means you should have walking, running, and idle animations ready so the script can control them properly.

You can get the animations by creating them yourself or finding them in the Roblox Toolbox

## Step 1.

Create a new `instance` for each animation. 

> **Note:**
> An instance is an object in Roblox, like a part, script or animation.
> Anything you add to the game, like parts, scripts, or animations, is an Instance.

Use cases: 
If we wanted to:

- spawn parts or models
- play animations on a character 
- add tools and effects

we can do this in a script by using `Instance.new()` which creates new objects while the game is running.

```luau
local walkAnimation = Instance.new("Animation")
local runAnimation = Instance.new("Animation")
local idleAnimation = Instance.new("Animation")
```

## Step 2.

Assign the Animation ID to each animation 

```luau
local walkAnimation = Instance.new("Animation")
local runAnimation = Instance.new("Animation")
local idleAnimation = Instance.new("Animation")

walkAnimation.AnimationId = "rbxassetid://750785693"
runAnimation.AnimationId = "rbxassetid://98682628049286"
idleAnimation.AnimationId = "rbxassetid://657595757"
```

## Step 3.

Load each animtion so they're ready to play

```luau
local walkAnimTrack = Humanoid:LoadAnimation(walkAnimation)
local runAnimTrack = Humanoid:LoadAnimation(runAnimation)
local idleAnimTrack = Humanoid:LoadAnimation(idleAnimation)
```

## Step 4.

Create a variable `isRunning` to store whether the player is running.

```luau
local isRunning = false 
```

## Step 5.

Set `isRunning` to `true` if the user is holding **Left Shift**

```luau
UserInputService.InputBegan:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
		Humanoid.WalkSpeed = 50	
		isRunning = true
	end
end)
```

and `false` if the user is not holding **Left Shift**

```luau
UserInputService.InputEnded:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
		Humanoid.WalkSpeed = 20	
		isRunning = false
	end
end)
```

## Step 6. 

Listen for movement

```luau
Humanoid.Running:Connect(function(speed)

end)
```

This code calls the function whenever the character’s running speed changes.

## Step 7. 

Check if the character is moving by using the comparison operator

```luau
Humanoid.Running:Connect(function(speed)
	if speed > 0 then

	end
end)
```

If the speed is greater than 0, the character is moving

## Step 8. 

Check if the character is running

```luau
Humanoid.Running:Connect(function(speed)
	if speed > 0 then
		if isRunning then
			runAnimTrack:Play()
			walkAnimTrack:Stop()
		end
	end
end)
```

If `isRunning = true`, then it runs the code inside which makes the **run animation plays** and the **walk animation stops**.

## Step 9. 

Add an **else statement** to run code if the character is **not running**

```luau
Humanoid.Running:Connect(function(speed)
	if speed > 0 then
		if isRunning then
			runAnimTrack:Play()
			walkAnimTrack:Stop()
		else 
			walkAnimTrack:Play()
			runAnimTrack:Stop()
		end
	end
end)
```

If the **speed** is **more** than **0** but the character is not running, this means the character is walking.
Thus, the **walk animation plays** but the **run animation stops**

## Step 10.

If the speed is not more than 0, that means the character is idle!

So we need to make an **else statement** to play the **idle animation** and stop the other movement animations

```luau
	Humanoid.Running:Connect(function(speed)
		if speed > 0 then
			if isRunning then
				runAnimTrack:Play()
				walkAnimTrack:Stop()
			else 
				walkAnimTrack:Play()
				runAnimTrack:Stop()
			end
		else
			walkAnimTrack:Stop()
			runAnimTrack:Stop()
			idleAnimTrack:Play()
		end
	end)
```

## Test your Code
Your code is now complete, test your code by running, walking and staying idle to see if the animations play properly

## Complete Code

```luau
local UserInputService = game:GetService("UserInputService")

local Character = script.Parent
local Humanoid = Character:WaitForChild("Humanoid")

-- Animations
local walkAnimation = Instance.new("Animation")
walkAnimation.AnimationId = "rbxassetid://750785693"

local runAnimation = Instance.new("Animation")
runAnimation.AnimationId = "rbxassetid://98682628049286"

local idleAnimation = Instance.new("Animation")
idleAnimation.AnimationId = "rbxassetid://657595757"

local walkAnimTrack = Humanoid:LoadAnimation(walkAnimation)
local runAnimTrack = Humanoid:LoadAnimation(runAnimation)
local idleAnimTrack = Humanoid:LoadAnimation(idleAnimation)

-- Start idle
idleAnimTrack:Play()

local isRunning = false 

UserInputService.InputBegan:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
		Humanoid.WalkSpeed = 50	
		isRunning = true
	end
end)

UserInputService.InputEnded:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
		Humanoid.WalkSpeed = 20	
		isRunning = false
	end
end)

Humanoid.Running:Connect(function(speed)
	if speed > 0 then
		if isRunning then
			runAnimTrack:Play()
			walkAnimTrack:Stop()
		else 
			walkAnimTrack:Play()
			runAnimTrack:Stop()
		end
	else
		walkAnimTrack:Stop()
		runAnimTrack:Stop()
		idleAnimTrack:Play()
	end
end)
```
