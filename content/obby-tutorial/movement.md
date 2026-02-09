# Movement in Roblox Studio: Holding Shift to Sprint Tutorial

https://github.com/user-attachments/assets/f6deec26-8567-4605-a783-d45530abf60e

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
      Humanoid.WalkSpeed = 32	
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
      Humanoid.WalkSpeed = 16	
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
		Humanoid.WalkSpeed = 32
	end
end)

UserInputService.InputEnded:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
		Humanoid.WalkSpeed = 16
	end
end)
```

# Movement Animation

We are going to edit this code:

```luau
local UserInputService = game:GetService("UserInputService")

local Character = script.Parent
local Humanoid = Character:WaitForChild("Humanoid")

UserInputService.InputBegan:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
		Humanoid.WalkSpeed = 32
	end
end)

UserInputService.InputEnded:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
		Humanoid.WalkSpeed = 16
	end
end)
```

so that it plays different animation for **run**, **walk** and **jump**

## Step 1.

Add this code to our script so that it disables the default animation so that it doesn't interfere with our new animations

```luau
local animate = character:FindFirstChild("Animate")
if animate then
	animate.Disabled = true
end
```

## Step 2. 

### Step 2a. 
Create an **Animation object** for walk

```luau
local walkAnim = Instance.new("Animation") 
```

### Step 2b. 
Then set the **asset ID** of the animation you want to use for walk

```luau
walkAnim.AnimationId = "rbxassetid://616122287"
```

### Step 2c. 
Load the animation so you can play/stop it in the code

```luau
local walkTrack = humanoid:LoadAnimation(walkAnim)
```

### Step 2d. 
Then do the same thing for **run** asnd **jump**

## Full code for animations

```luau
local walkAnim = Instance.new("Animation")
walkAnim.AnimationId = "rbxassetid://616122287"
local walkTrack = humanoid:LoadAnimation(walkAnim)

local runAnim = Instance.new("Animation")
runAnim.AnimationId = "rbxassetid://656118852"
local runTrack = humanoid:LoadAnimation(runAnim)

local jumpAnim = Instance.new("Animation")
jumpAnim.AnimationId = "rbxassetid://616115533"
local jumpTrack = humanoid:LoadAnimation(jumpAnim)
```

## Step 3.

### Step 3a.

Create a variable `isRunning` and set to a `false` initially

```luau
local isRunning = false
```

This variable tracks whether the player is currently sprinting.

### Step 3b.

Keep checking for running by adding this code

```luau
RunService.RenderStepped:Connect(function

end)
```

> **Note:** 
> RenderStepped will run every frame before any rendering.

### Step 3c.

Create a variable that tracks whether if the player is moving or not

```luau
RunService.RenderStepped:Connect(function
	local moving = humanoid.MoveDirection.Magnitude > 0
end)
```

### Step 3d.
Ignore walk/run animation when the player is in the falling or jumping

```luau
RunService.RenderStepped:Connect(function
	local moving = humanoid.MoveDirection.Magnitude > 0

	if humanoid:GetState() == Enum.HumanoidStateType.Jumping 
	   or humanoid:GetState() == Enum.HumanoidStateType.Freefall then
	    return
	end
end)
```

### Step 3e.

Play the **run animation** if the character is **moving** and **running**

```luau
RunService.RenderStepped:Connect(function()
	local moving = humanoid.MoveDirection.Magnitude > 0

	if humanoid:GetState() == Enum.HumanoidStateType.Jumping 
	   or humanoid:GetState() == Enum.HumanoidStateType.Freefall then
	    return
	end

	if moving then
		if isRunning then
			if not runTrack.IsPlaying then
				walkTrack:Stop()
				runTrack:Play()
			end
		end
	end
end)
```

### Step 3f.

If the character is **moving** but **not running**, then play the **walking animation**

```luau
RunService.RenderStepped:Connect(function()
	local moving = humanoid.MoveDirection.Magnitude > 0

	if humanoid:GetState() == Enum.HumanoidStateType.Jumping 
	   or humanoid:GetState() == Enum.HumanoidStateType.Freefall then
	    return
	end

	if moving then
		if isRunning then
			if not runTrack.IsPlaying then
				walkTrack:Stop()
				runTrack:Play()
			end
		else
			if not walkTrack.IsPlaying then
				runTrack:Stop()
				walkTrack:Play()
			end
		end
	end
end)
```

### Step 3g.

If the character isn't **moving**, then the character stops the animation for running and walking

```luau
RunService.RenderStepped:Connect(function()
	local moving = humanoid.MoveDirection.Magnitude > 0

	if humanoid:GetState() == Enum.HumanoidStateType.Jumping or humanoid:GetState() == Enum.HumanoidStateType.Freefall then
		return
	end

	if moving then
		if isRunning then
			if not runTrack.IsPlaying then
				walkTrack:Stop()
				runTrack:Play()
			end
		else
			if not walkTrack.IsPlaying then
				runTrack:Stop()
				walkTrack:Play()
			end
		end
	else
		walkTrack:Stop()
		runTrack:Stop()
	end
end)
```

## Step 4

Run the **jumping animation** when the player jumps and stop the animation when the character lands

```luau
humanoid.Jumping:Connect(function()
	walkTrack:Stop()
	runTrack:Stop()
	jumpTrack:Play()
end)

humanoid.StateChanged:Connect(function(_, newState)
	if newState == Enum.HumanoidStateType.Landed then
		jumpTrack:Stop()
	end
end)
```

# Full Code

```luau
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local character = script.Parent
local humanoid = character:WaitForChild("Humanoid")

local animate = character:FindFirstChild("Animate")
if animate then
	animate.Disabled = true
end

local walkAnim = Instance.new("Animation")
walkAnim.AnimationId = "rbxassetid://616122287"
local walkTrack = humanoid:LoadAnimation(walkAnim)

local runAnim = Instance.new("Animation")
runAnim.AnimationId = "rbxassetid://656118852"
local runTrack = humanoid:LoadAnimation(runAnim)

local jumpAnim = Instance.new("Animation")
jumpAnim.AnimationId = "rbxassetid://616115533"
local jumpTrack = humanoid:LoadAnimation(jumpAnim)

local isRunning = false

UserInputService.InputBegan:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
		isRunning = true
		humanoid.WalkSpeed = 25
	end
end)

UserInputService.InputEnded:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.LeftShift then
		isRunning = false
		humanoid.WalkSpeed = 16
	end
end)

RunService.RenderStepped:Connect(function()
	local moving = humanoid.MoveDirection.Magnitude > 0

	if humanoid:GetState() == Enum.HumanoidStateType.Jumping or humanoid:GetState() == Enum.HumanoidStateType.Freefall then
		return
	end

	if moving then
		if isRunning then
			if not runTrack.IsPlaying then
				walkTrack:Stop()
				runTrack:Play()
			end
		else
			if not walkTrack.IsPlaying then
				runTrack:Stop()
				walkTrack:Play()
			end
		end
	else
		walkTrack:Stop()
		runTrack:Stop()
	end
end)

-- Jump animation
humanoid.Jumping:Connect(function()
	walkTrack:Stop()
	runTrack:Stop()
	jumpTrack:Play()
end)

humanoid.StateChanged:Connect(function(_, newState)
	if newState == Enum.HumanoidStateType.Landed then
		jumpTrack:Stop()
	end
end)
```
