Стартуем!
```lua
Добавляем тут вызов функции getData
...
local function SetupGameGui()
...
	gui.Towers.Title.Text = ""...""
	local playerData = getDataFunction:InvokeServer()
	for i, tower in pairs(playerData.SelectedTowers) do -- заменяем старый код на новый
		local tower = towers:FindFirstChild(tower)
		-- проверку на модельку упрощаем
		if tower then ...
	...
```