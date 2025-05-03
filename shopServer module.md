Допиливаем shopServer, добавляя новую функцию загрузки данных игроков

```lua
local DataStoreService = game:GetService("DataStoreService")

local database = DataStoreService:GetDataStore("database")

local data = {}

-- Загрузка данных игроков
-- Сохранение данных игроков

local function getItemStatus(player: Player, itemName: string)
```

После активации апилок, пишем следующую функцию:
```lua
-- Загрузка данных игроков
local function LoadData(player)
	local success = nil
	local playerData = nil
	local attempt = 1

	repeat
		success, playerData = pcall(function()
			return database:GetAsync(player.UserId)
		end)

		attempt += 1
	until success or attempt == 3
	if not success then 
		warn(playerData)
		task.wait()
	end
	if success then
		print("Connection success")
		if not playerData then
			print("New player, giving default data")
			playerData = {
				defaultData
			}
		end 
		data[player.UserId] = playerData
	else
		warn("Unable to get data for player", player.UserId)
		player:Kick("There was a problem getting your data")
	end
end
Players.PlayerAdded:Connect(LoadData)
```
Допишем функцию сохранения данных игроков
```lua
Players.PlayerAdded:Connect(LoadData)
-- Сохранение данных игроков
local function SaveData(player)
	if data[player.UserId] then
		local success = nil
		local playerData = nil
		local attempt = 1
	
		repeat
			success, playerData = pcall(function()
				return database:UpdateAsync(player.UserId, function()
					return data[player.UserId]
				end)
			end)
	
			attempt += 1
		until success or attempt == 3
		if not success then 
			warn(playerData)
			task.wait()
		end
		if success then
			print("Data saved successfully")
		else
			warn("Unable to save data for", player.UserId)
		end
	else
		warn("No session data for", player.UserId)
	end
end
Players.PlayerRemoving:Connect(SaveData)
```

Обновление данных при закрытии игры (дабы не потерялось всё)
```lua
Players.PlayerRemoving:Connect(function(player)
	SaveData(player)
	data[player.UserId] = nil
end)

game:BindToClose(function() 
	for index, player in pairs(Players:GetPlayers())
		task.spawn(function() 
			SaveData(player)
		end)
	end
end)
```