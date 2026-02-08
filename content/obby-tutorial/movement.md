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
