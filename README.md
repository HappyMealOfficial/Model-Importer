# Model-Importer
A simple model importer script for roblox lol, thanks to hazel for inspiration

# Why have I made it open source?
Simple, so you can steal it :D

# Usage
```
loadstring(game:HttpGet("https://raw.githubusercontent.com/mcKTS/Model-Importer/main/modelimporter.lua"))()
```

https://youtu.be/dggt_2ut-oM (Watch this and use your brain to think if you don't know how to use)

Code used in the video:
```
local HttpService = game:GetService("HttpService")
local partsInModel = {}
local modelPart = script.Parent

for index,part in pairs(modelPart:GetDescendants()) do
    part.Name = "Part"..index
end

for i, part in modelPart:GetDescendants() do
    if part:IsA("Part") then
        local properties = {}
        properties["Type"] = "Part"
        properties["Color"] = tostring(part.Color)
        properties["Material"] = tostring(part.Material.Name)
        properties["CFrame"] = tostring(part.CFrame)
        properties["Size"] = tostring(part.Size)
        properties["Reflectance"] = part.Reflectance
        properties["Transparency"] = part.Transparency
        properties["Shape"] = tostring(part.Shape.Name)

        partsInModel[part.Name] = properties
    end
end

local json = HttpService:JSONEncode(partsInModel)
print(json)
```
# Credit
GreenDeno - Venyx-UI-Library
