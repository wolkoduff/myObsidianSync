Часть 1
```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local towers = require(ReplicatedStorage:WaitForChild("TowerShop"))

local gui = script.Parent
local container = gui.Container

local exit = container.Exit
local gems = container.Gems
local limits = container.Limits
local itemFrame = container.ItemsFrame

local function toggleShop()
	container.Visible = not container.Visible
end

local function setupShop()
	local prompt = Instance.new("ProximityPrompt")
	prompt.RequiresLineOfSight = false
	prompt.ActionText = "Shop"
	prompt.Parent = workspace:WaitForChild("ShopPart")
	
	prompt.Triggered:Connect(toggleShop)
	exit.Activated:Connect(toggleShop)
end

setupShop()
```