First, let's get a NPC model from the toolbox. Since I'm going to use an R15 animation, I have to get an R15 character.

> **Note:**  
> R6 animations only work on R6 characters, and R15 animations only work on R15 characters.  
> Since this NPC uses an R15 animation, make sure the NPC model is **R15**

https://github.com/user-attachments/assets/e4bb4f74-cb7b-43c8-99c4-1cc03840ffd7

We’re going to create a script that makes an NPC humanoid follow the player. First, create a Script.

https://github.com/user-attachments/assets/c7b86964-b5d5-4cc5-9d0e-769274a57ce7

### NPC Follow Player Script (R15)

---

### Step 1: Define Variables

```lua
--- Reference the NPC model
local NPC = script.Parent
-- HumanoidRootPart: the invisible part that controls a humanoid's movement
local HumanoidRootPart = NPC.HumanoidRootPart

-- Maximum distance at which the NPC can detect players
local MaxDistance = math.huge  -- unlimited for now, can be changed
-- Variable to prevent dealing damage too fast
local hitReady = true
```

### Step 2: Create a function

> **Functions**  
> Functions are blocks of code that you can execute multiple times on command
> You can also connect them to events or assign them as callbacks.

We're going to create a function that attack the player!

```lua
NPC.Humanoid.Touched:Connect(function(hit)

end)
```

Create a conditional to check if the NPC model has hit another humanoid (another NPC or player)
and only proceed if the NPC is ready to deal damage by making sure hitReady = true

```lua
NPC.Humanoid.Touched:Connect(function(hit)
  if hit.Parent:FindFirstChild("Humanoid") and hitReady then
  
  end
end)
```

When the NPC is touching another humanoid, set hitReady to false so that the NPC cannot hit again immediately

```lua
NPC.Humanoid.Touched:Connect(function(hit)
  if hit.Parent:FindFirstChild("Humanoid") and hitReady then
    hitReady = false
  end
end)
```

Deals damage to another humanoid by 20

```lua
NPC.Humanoid.Touched:Connect(function(hit)
  if hit.Parent:FindFirstChild("Humanoid") and not hitReady then
    hitReady = false
    hit.Parent.Humanoid.Health -= 20
  end
end)
```

Add a cooldown for 1 second then set hitReady to true
This makes the NPC wait 1 second before attacking again

```lua
NPC.Humanoid.Touched:Connect(function(hit)
  if hit.Parent:FindFirstChild("Humanoid") and not hitReady then
    hitReady = false
    hit.Parent.Humanoid.Health -= 20
    wait(1)
    hitReady = true
  end
end)
```
