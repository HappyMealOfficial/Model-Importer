--Roblox Model Importer v1.1
--Made by Loco_CTO with Venyx UI Library
repeat task.wait() until game:IsLoaded()

--Required Services
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/RegularVynixu/UI-Libraries/main/Venyx/Source.lua"))()
local venyx = library.new("Model Importer v1.1")
local HttpService = game:GetService("HttpService")
local models = {}

--Define Value
local modelImportJson = ''
local selectedModelInImporterFolder = ''
local importedModelsTable = {}

--Workspace Folder Handle
makefolder("ModelsImporter")

--In Game Asset Folder 
modelsImporterFolder = Instance.new("Folder")
modelsImporterFolder.Name = "ModelsImporter"
modelsImporterFolder.Parent = game.Workspace

--String decoder
local function searchImporterModels()
        table.clear(models)
        for i, model in pairs(modelsImporterFolder:GetChildren()) do
                table.insert(models, model.Name)
        end
        importedModelsTable = models
        return models
end
      
local function decodeCFrame(CFrameString)
        local splitString = string.split(CFrameString,",")
        local newCFrame = CFrame.new(
                splitString[1],
                splitString[2],
                splitString[3],
                splitString[4],
                splitString[5],
                splitString[6],
                splitString[7],
                splitString[8],
                splitString[9],
                splitString[10],
                splitString[11],
                splitString[12]
        )
        return newCFrame
end
      
local function decodeColor3(Color3String)
        local splitString = string.split(Color3String,",")
        local newColor3 = Color3.new(
                splitString[1],
                splitString[2],
                splitString[3]
        )
        return newColor3
end
      
local function decodeSize(SizeString)
        local splitString = string.split(SizeString,",")
        local newSize = Vector3.new(
                splitString[1],
                splitString[2],
                splitString[3]
        )
        return newSize
end
      
local function decodeShape(ShapeString)
        local newShape = Enum.PartType[ShapeString]
        return newShape
end
      
local function decodeMaterial(MaterialString)
        local newShape = Enum.Material[MaterialString]
        return newShape
end

--Model importer page
local modelimporter = venyx:addPage("Importer", 5012544693)
local modelimporterSectionImported = modelimporter:addSection("Imported Models")

local modelimporterSectionImportedDropDown = modelimporterSectionImported:addDropdown("Search", searchImporterModels())
local modelimporterSectionImportNew = modelimporter:addSection("Import new")

local function modelImport(json)
        modelName = string.gsub(modelImportJson, "ModelsImporter\\", "")
        modelName = string.gsub(modelName, ".json", "")
        local model = Instance.new('Model')
        model.Name = modelName
        model.Parent = modelsImporterFolder
        local decode = HttpService:JSONDecode(json)
        for i, partDecode in pairs(decode) do
                if partDecode.Type == 'Part' then
                        local part = Instance.new("Part")
                        part.CFrame = decodeCFrame(partDecode.CFrame)
                        part.Reflectance = partDecode.Reflectance
                        part.Transparency = partDecode.Transparency
                        part.Material = decodeMaterial(partDecode.Material)
                        part.Color = decodeColor3(partDecode.Color)
                        part.Shape = decodeShape(partDecode.Shape)
                        part.Size = decodeSize(partDecode.Size)
                        part.Parent = model
                        part.Anchored = true
                end
        end
        venyx:Notify("Model Importer", "Imported model from "..modelImportJson.."!")
        searchImporterModels()
        modelimporterSectionImported:updateDropdown(modelimporterSectionImportedDropDown, "Search", importedModelsTable)
end

local modelimporterSectionImportNewDropDown = modelimporterSectionImportNew:addDropdown("Select Model", listfiles("ModelsImporter"), function(Selection)
        modelImportJson = Selection
end)

modelimporterSectionImportNew:addButton("Import", function()
        pcall(function()
                modelImport(readfile(modelImportJson))
        end)
end)

modelimporterSectionImportNew:addButton("Refresh Files", function()
        modelimporterSectionImportNew:updateDropdown(modelimporterSectionImportNewDropDown, "Select Model", listfiles("ModelsImporter"))
end)

--Others
local others = venyx:addPage("Others", 5012544693)
local othersSection1 = others:addSection("Others")
othersSection1:addKeybind("Toggle Keybind", Enum.KeyCode.RightShift, function()
	venyx:toggle()
end)

local othersSection1 = others:addSection("How to use?")

local othersSection1 = others:addSection("Scripted by Loco_CTO with Venyx UI Lib")

--UI themes
local themes = {
	Background = Color3.fromRGB(10, 10, 10),
	Glow = Color3.fromRGB(208, 0, 255),
	Accent = Color3.fromRGB(0, 0, 0),
	LightContrast = Color3.fromRGB(49, 26, 63),
	DarkContrast = Color3.fromRGB(5, 5, 5),
	TextColor = Color3.fromRGB(242, 234, 255)
}


for theme, color in pairs(themes) do
	venyx:setTheme(theme, color)
end

venyx:SelectPage(venyx.pages[1], true)
