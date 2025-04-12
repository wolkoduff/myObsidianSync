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

Часть 2
```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local towers = require(ReplicatedStorage:WaitForChild("TowerShop"))

local getDataFunction = ReplicatedStorage:WaitForChild("GetData")

local gui = script.Parent
local container = gui.Container

local exit = container.Exit
local gems = container.Gems
local limit = container.Limits
local itemsFrame = container.ItemsFrame

local playerData = {}

local function updateItems()
	gems.Text = "💎" .. playerData.Gems
	limit.Text = #playerData.SelectedTowers .. "/3" -- Предельное количество доступных башен для выбора
	
	for i, tower in pairs(towers) do
		local newButton = itemsFrame.TemplateButton:Clone()
		newButton.Name = tower.Name
		newButton.TowerName.Text = tower.Name
		newButton.Image = tower.ImageAsset
		newButton.Visible = true
		newButton.Parent = itemsFrame
	end
end

local function toggleShop()
	container.Visible = not container.Visible
	if container.Visible then
		playerData = getDataFunction:InvokeServer()
		updateItems()
	end
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