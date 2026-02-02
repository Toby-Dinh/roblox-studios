---
title: Disappearing Platform
description: Creating a basic script that makes a platform disappear.
---

# Designing 
## Create Your Platforms

First, create two platforms like the ones shown below.

https://github.com/user-attachments/assets/138c35b5-51db-44f8-af2d-d6d6e58bbe10

Make sure to **anchor** the platforms so they don’t fall when the game starts.

https://github.com/user-attachments/assets/1afd3ffd-2d58-4e0c-85e8-0c9fb846d107

Next, add a **SpawnLocation** from the Toolbox and place another platform between the two platforms.

<img width="1377" height="706" alt="image" src="https://github.com/user-attachments/assets/dea314f8-ffba-4fd0-885b-cf0ada357360" />

Rename this middle platform to **DisappearingPlatform** (or any name you think fits).

https://github.com/user-attachments/assets/72525bda-4a0e-43fb-8ea0-b547888cbbfe

---

# Scripting
## First Variable

Start by creating a variable for the platform. In Luau, variables are written as `local name = value` and are usually in camel case.

Copy the code below to create a variable called `platform` with the value `script.Parent`:

```luau
local platform = script.Parent
```

> **Note:**  
> `script.Parent` refers to the object the script is inside.  
> `script` means the script you’re writing, and `Parent` is the object that contains it.

## Disappear Function
Time to make the platform disappear. To keep code organized, we use a **function**, which is a named block of code you can reuse.

Create a function in the script and call it `disappear`.

```luau
local platform = script.Parent

local function disappear()

end
```

### Making the Platform Invisible and Non-Solid

This function makes the platform disappear by changing two important properties.

- In the `disappear` function, set the `CanCollide` property of the platform to `false`. This makes it so the player can't step on the platform and will fall through.  
- Set `Transparency = 1` to make the platform fully invisible.

```luau
local platform = script.Parent

local function disappear()
    platform.CanCollide = false
    platform.Transparency = 1
end
```

### Call the function 

Once you've declared a function, you can run it by writing its name with parentheses next to it. For example, disappear() will run the disappear function. This is known as **calling** a function.

```luau
local platform = script.Parent

local function disappear()
    platform.CanCollide = false
    platform.Transparency = 1
end

disappear()
```

### Test your code
If your platform has disappeared, that means your code has worked.

## Appear function 
You can easily make the platform reappear by writing a function that does the exact opposite of the disappear function.

1. Delete the `disappear()` line from the script.

2. Declare a new function called `appear`.

3. In the function body, set the `CanCollide` property to **true** and the `Transparency` property to **0**.

```luau
local platform = script.Parent

local function disappear()
    platform.CanCollide = false
    platform.Transparency = 1
end

local function appear()
    platform.CanCollide = true
    platform.Transparency = 0
end
```

## Loops

A **loop** lets you repeat a block of code multiple times.  

We can use this to make the platform appear and disappear with a few seconds between each change

```luau
while true do

end
```

> **Note:**  
> `while true do` creates an infinite loop, so the code inside will keep repeating until the game stops or you break the loop.

### Making the Platform Disappear and Reappear

Use a **while loop** to make the platform disappear and reappear. Always include `task.wait()` to avoid freezing your game.  

1. Call `task.wait(3)` to pause for 3 seconds.  
2. Call the `disappear()` function to make the platform vanish.  
3. Call `task.wait(3)` again to pause for 3 seconds.  
4. Call the `appear()` function to make the platform reappear.

```luau
while true do
    task.wait(3)      -- Wait 3 seconds
    disappear()       -- Make platform disappear
    task.wait(3)      -- Wait 3 seconds
    appear()          -- Make platform reappear
end
```

## Test your code!
Your code is complete now! Test your code now and you should find that the platform disappears after 3 seconds then reappears three seconds later.

You can add more features to the disappearing platform and experiment with the script to make your obby better

https://github.com/user-attachments/assets/dd835d37-6e56-49e4-955f-3933ab35ead7


