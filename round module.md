Следующие функции подвергаются аннигиляции или инквизиции в скрипте round
```lua
toggleVoting

for name, map in pairs(votes) do
...
end 

if not winVote then 
	local n = math.random(#maps)
	winVote = maps[n].Name
end 
```