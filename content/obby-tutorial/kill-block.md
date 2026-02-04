---
title: Lava / Kill blocks
description: Creating a basic script that makes a kills a player when touched
---

https://github.com/user-attachments/assets/d30b2c9f-9006-4f0b-82c9-7fac9e1bd6d5

## Set Up

1. Insert a Part and move it into place in your world. Name it **LavaFloor** or any name you think would suit.

2. Make sure that the part is **anchored** and rize it so it covers the floor of the enclosing space.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f09694c2-99b3-4cbf-bba8-8da35bf7e1bc" />

### Adding the lava
3. Make the floor look more like lava by setting the Material property to Neon and the Color to an orange shade.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/051cb008-7b07-46e8-a83a-1ea5f5c2924c" />

<img width="640" height="282" alt="image" src="https://github.com/user-attachments/assets/8dcef2cf-d1e0-4f75-a631-bb193c8e9b8a" />

## Scripting 
### First Variable

Start by creating a variable for the platform. In Luau, variables are written as local name = value and are usually in camel case.

Copy the code below to create a variable called platform with the value script.Parent:

```luau
local lava = script.Parent
```
### Creating a function

> **Note:**  
> A **function** is a named block of code that performs a specific task.  
> You can run the same code multiple times by calling the function instead of writing it again.

Declare a new function and call it `kill` (or any name of your choice). 

```luau
local lava = script.Parent

local function kill()

end
```
### Get the touching part

To make the lava kill a player, the function needs to know which object touched it.  

We use a **parameter** for this — a variable the function receives when it’s called. In this case, we create a parameter called `otherPart` for the `kill` function:

> **Note:**  
> A **parameter** is a value you pass to a function so it knows what to work with.  
> Here, `otherPart` represents the part that touched the lava, letting the function affect the correct player.

```luau
local lava = script.Parent

local function kill(otherPart)

end
```

### Finding the Player Character

To affect the player, we first need to get the character that owns the part that touched the lava.  

1. **Get the character model**  
Create a variable called `character` to store the parent of the part that touched the lava.

This gives you access to the player’s entire character model.

```luau
local lava = script.Parent

local function kill(otherPart)
    local character = otherPart.Parent
end
```

2. **Get the Humanoid of the character model** 
Create a variable called `humanoid` by using `FindFirstChild("Humanoid")` on the character.

This lets you access the player’s health and other properties.

```luau
local lava = script.Parent

local function kill(otherPart)
    local character = otherPart.Parent
    local humanoid = character:FindFirstChild("Humanoid")
end
```

### Check the humanoid

> **Note:**
> An if statement runs the code inside it only when a certain condition is true.

You can check if the humanoid exists using an ** if statement** 

The code inside the if statement only runs if the condition is true. 

```luau
local lava = script.Parent

local function kill(otherPart)
  local character = otherPart.Parent
  local humanoid = character:FindFirstChild("Humanoid")
  if humanoid then
  
  end
end
```

If there is a `humanoid`, we're going to change the health to 0 to kill the player

```luau
local lava = script.Parent

local function kill(otherPart)
  local character = otherPart.Parent
  local humanoid = character:FindFirstChild("Humanoid")
  if humanoid then
    humanoid.Health = 0
  end
end
```

### Call the `kill` function when something touches the lava!

Add `lava.Touched:Connect(kill)` **below the function**. This makes the `kill` function run automatically whenever something touches the lava.

```luau
local lava = script.Parent

local function kill(otherPart)
  local character = otherPart.Parent
  local humanoid = character:FindFirstChild("Humanoid")
  if humanoid then
    humanoid.Health = 0
  end
end

lava.Touched:Connect(kill)
```

## Test Your Code
With that, your lava floor is complete! Test your experience and you should find that your deadly lava successfully kills users on contact. Try using your lava as an extra challenge in an obby, or as a boundary for a world.

You can also make kill blocks instead of lava like the one below or make up your own ideas! 

https://github.com/user-attachments/assets/83852746-2ae8-47d8-b1c1-42ce6961857b
