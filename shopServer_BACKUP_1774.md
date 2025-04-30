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

ReplicatedStorage.GetData.OnServerInvoke = function(player: Player)
	return defaultData
end
```

<<<<<<< HEAD
<<<<<<< HEAD
Итоговый скрипт
=======
Полный скрипт
>>>>>>> origin/main
=======
Полный скрипт
>>>>>>> ec56f089b3a47df03e80a742caafd15c528800f8
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

local function getItemStatus(player: Player, itemName: string)
	local playerData = defaultData
	if table.find(playerData.SelectedTowers, itemName) then
		return "Equipped"
	elseif table.find(playerData.OwnedTowers, itemName) then
		return "Owned"
	else
		return "For Sale"
	end
end


ReplicatedStorage.InteractItem.OnServerInvoke = function(player: Player, itemName: string)
	local shopItem = towers[itemName]
	local playerData = defaultData
	if shopItem and playerData then
		local status = getItemStatus(player, itemName)
		
		if status == "For Sale" and shopItem.Price <= playerData.Gems then
			-- purshare
			playerData.Gems -= shopItem.Price
			table.insert(playerData.OwnedTowers, shopItem.Name)
			
		elseif status == "Owned" then
			-- equip the tower
			table.insert(playerData.SelectedTowers, shopItem.Name)
			if #playerData.SelectedTowers > MAX_SELECTED_TOWERS then
				table.remove(playerData.SelectedTowers, 1)
			end
		elseif status == "Equipped" then
			-- unselect the tower (if more than 1 selected)
			if #playerData.SelectedTowers > 1 then
				local towerToRemove = table.find(playerData.SelectedTowers, itemName)
				table.remove(playerData.SelectedTowers, towerToRemove)
			end
		end
		
		return playerData
	else
		warn("Башна/данные игрока не найдены")
		
		return false
	end
end

ReplicatedStorage.GetData.OnServerInvoke = function(player: Player)
	return defaultData
end
```