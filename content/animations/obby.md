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

## First Variable

Start by creating a variable for the platform. In Luau, variables are written as `local name = value` and are usually in camel case.

Copy the code below to create a variable called `platform` with the value `script.Parent`:

```luau
local platform = script.Parent
```

> **Note:**  
> `script.Parent` refers to the object the script is inside.  
> `script` means the script you’re writing, and `Parent` is the object that contains it.
