First, let's get a NPC model from the toolbox. Since I'm going to use an R15 animation, I have to get an R15 character.

> **Note:**  
> R6 animations only work on R6 characters, and R15 animations only work on R15 characters.  
> Since this NPC uses an R15 animation, make sure the NPC model is **R15**

https://github.com/user-attachments/assets/e4bb4f74-cb7b-43c8-99c4-1cc03840ffd7

We’re going to create a script that makes an NPC humanoid follow the player. First, create a Script.

https://github.com/user-attachments/assets/c7b86964-b5d5-4cc5-9d0e-769274a57ce7

# NPC Follow Player Script (R15)

---

## Step 1: Define Variables

```lua
--- Reference the NPC model
local NPC = script.Parent
-- HumanoidRootPart: the invisible part that controls a humanoid's movement
local HumanoidRootPart = NPC.HumanoidRootPart

-- Maximum distance at which the NPC can detect players
local MaxDistance = math.huge  -- unlimited for now, can be changed
-- Debounce to prevent dealing damage too fast
local debounce = false
