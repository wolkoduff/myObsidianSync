```lua
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local towers = require(ReplicatedStorage:WaitForChild("TowerShop"))

local MAX_SELECTED_TOWERS = 3


local data = {}
local defaultData = {
	["Gems"] = 400,
	["SelectedTowers"] = {"Cannon"},
	["OwnedTowers"] = {"Cannon", "Killer"}
}
```