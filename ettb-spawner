local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

local players = game:GetService("Players")
local cs = game:GetService("CollectionService")
local lp = players.LocalPlayer

-- used an AI to list down pets lol losakldlskablkdaskl
local petdata = {
    Secret = {
        "Matteo", "Gattatino Neonino", "Statutino Libertino", "Unclito Samito",
        "Gatattino Donutino", "Espresso Signora", "Los Tungtungtungcitos", "Los Combinasionas",
        "Aura Farma", "Rainbow 67", "Fragola La La La", "Eek Eek Eek Sahur",
        "Bambooini Bombini", "Mastodontico Telepiedone", "La Vacca Black Hole Goat",
        "Tractoro Dinosauro", "Capybara Monitora", "Patatino Astronauta", "Patito Dinerito",
        "Onionello Penguini", "Sausaggini Sanitario", "Marietti Frigo",
        "Tartarughi Attrezzini", "Kissarini Heartini", "Scaldarino Derpino"
    },
    Celestial = {
        "Job Job Job Sahur", "Dug Dug Dug", "Bisonte Giuppitere", "Alessio",
        "Esok Sekolah", "Diamantusa", "Caffe Trinity", "Avocadini Antilopini",
        "Los Orcaleritos", "Zung Zung Zung Lazur", "La Malita", "Money Elephant",
        "Capuccino Policia", "Rattini Machini", "Polpo Semaforini",
        "Cioccolatone Draghettone", "Ketupastro Infernetto"
    },
    Divine = {
        "Bulbito Bandito Traktorito", "Burgerini Bearini", "Strawberry Elephant",
        "Martino Gravitino", "Galactio Fantasma", "Grappellino D'Oro", "Din Din Vaultero",
        "Rubichetto Cubini", "Glacierello Infernetti", "Freezeti Cobretti",
        "Biscotti Macarotti", "Cupitron Consoletron", "Explodini Cataclismi",
        "Pastapot Infernotto", "Draculini Meowlini", "Don Magmito"
    },
}

local mutations = {
    "None", "Emerald", "Gold", "Blood", "Electric", "Admin",
    "Diamond", "Radioactive", "UFO", "Money", "Candy", "Doom",
    "Gamer", "Hacker", "Lucky"
}

local state = {
    rarity   = "Secret",
    pet      = petdata["Secret"][1],
    mutation = "None",
    level    = 100,
    scale    = 1.2,
}

-- functions
local function getmybase()
    local bf = workspace:FindFirstChild("Bases")
    if not bf then return nil end
    for _, base in pairs(bf:GetChildren()) do
        local tp = base:FindFirstChild("Title")
        if tp then
            local tg = tp:FindFirstChild("TitleGui")
            if tg then
                local fr = tg:FindFirstChild("Frame")
                if fr then
                    local pn = fr:FindFirstChild("PlayerName")
                    if pn and (string.find(pn.Text, lp.Name) or string.find(pn.Text, lp.DisplayName)) then
                        return base
                    end
                end
            end
        end
    end
end

local function getfirstemptyslot(base)
    for i = 1, 50 do
        local s = base:FindFirstChild("slot " .. i .. " brainrot")
        if s and not s:FindFirstChild("VisualPetContainer") and not s:FindFirstChildWhichIsA("Model") then
            return s
        end
    end
end

local function spawnpet()
    local base = getmybase()
    if not base then warn("[sillycopper] base not found!") return end
    local slot = getfirstemptyslot(base)
    if not slot then warn("[sillycopper] no empty slot!") return end

    local cont = Instance.new("Folder")
    cont.Name = "VisualPetContainer"
    cont.Parent = slot

    local root = Instance.new("Part")
    root.Name = "Root"
    root.Transparency = 1
    root.Anchored = true
    root.CFrame = (slot:IsA("BasePart") and slot.CFrame) or slot.PrimaryPart.CFrame
    root.Parent = cont

    cont:SetAttribute("BrainrotName", state.pet)
    cont:SetAttribute("Scale", state.scale)
    cont:SetAttribute("Level", state.level)
    cont:SetAttribute("StatsOverhead", true)
    cont:SetAttribute("Mutation", state.mutation)
    cs:AddTag(cont, "RenderBrainrot")

    print(("[sillycopper] spawned: %s | %s | lv%d | x%.1f"):format(state.pet, state.mutation, state.level, state.scale))
end


-- rayfield components
local window = Rayfield:CreateWindow({
    Name = "sillycopper spawner ez",
    LoadingTitle = "sillycopper",
    LoadingSubtitle = "spawner ez",
    Theme = "Default",
    DisableRayfieldPrompts = true,
    DisableBuildWarnings = true,
    ConfigurationSaving = { Enabled = false },
    KeySystem = false,
})

local tabsecret = window:CreateTab("Secret", "star")
tabsecret:CreateSection("select pet")

local secretpetnames = {}
for _, p in ipairs(petdata.Secret) do table.insert(secretpetnames, p) end

tabsecret:CreateDropdown({
    Name = "pet",
    Options = secretpetnames,
    CurrentOption = { secretpetnames[1] },
    MultipleOptions = false,
    Flag = "SecretPet",
    Callback = function(val)
        state.rarity = "Secret"
        state.pet = val[1]
    end,
})

local tabcelestial = window:CreateTab("Celestial", "sparkles")
tabcelestial:CreateSection("select pet")

local celestialpetnames = {}
for _, p in ipairs(petdata.Celestial) do table.insert(celestialpetnames, p) end

tabcelestial:CreateDropdown({
    Name = "pet",
    Options = celestialpetnames,
    CurrentOption = { celestialpetnames[1] },
    MultipleOptions = false,
    Flag = "CelestialPet",
    Callback = function(val)
        state.rarity = "Celestial"
        state.pet = val[1]
    end,
})

local tabdivine = window:CreateTab("Divine", "crown")
tabdivine:CreateSection("select pet")

local divinepetnames = {}
for _, p in ipairs(petdata.Divine) do table.insert(divinepetnames, p) end

tabdivine:CreateDropdown({
    Name = "pet",
    Options = divinepetnames,
    CurrentOption = { divinepetnames[1] },
    MultipleOptions = false,
    Flag = "DivinePet",
    Callback = function(val)
        state.rarity = "Divine"
        state.pet = val[1]
    end,
})

local tabsettings = window:CreateTab("Settings", "settings")
tabsettings:CreateSection("pet options")

tabsettings:CreateDropdown({
    Name = "mutation",
    Options = mutations,
    CurrentOption = { "None" },
    MultipleOptions = false,
    Flag = "Mutation",
    Callback = function(val)
        state.mutation = val[1]
    end,
})

tabsettings:CreateSlider({
    Name = "level",
    Range = { 1, 1000 },
    Increment = 1,
    Suffix = "",
    CurrentValue = 100,
    Flag = "Level",
    Callback = function(val)
        state.level = val
    end,
})

tabsettings:CreateSlider({
    Name = "scale",
    Range = { 0.1, 5 },
    Increment = 0.1,
    Suffix = "x",
    CurrentValue = 1.2,
    Flag = "Scale",
    Callback = function(val)
        state.scale = val
    end,
})

tabsettings:CreateSection("spawn")

tabsettings:CreateButton({
    Name = "Spawn pet",
    Callback = function()
        spawnpet()
        Rayfield:Notify({
            Title = "sillycopper",
            Content = "spawned: " .. state.pet,
            Duration = 3,
            Image = "check",
        })
    end,
})

tabsecret:CreateSection("spawn")
tabsecret:CreateButton({
    Name = "Spawn selected pet",
    Callback = function()
        state.rarity = "Secret"
        spawnpet()
        Rayfield:Notify({ Title = "sillycopper", Content = "spawned: " .. state.pet, Duration = 3, Image = "check" })
    end,
})

tabcelestial:CreateSection("spawn")
tabcelestial:CreateButton({
    Name = "Spawn selected pet",
    Callback = function()
        state.rarity = "Celestial"
        spawnpet()
        Rayfield:Notify({ Title = "sillycopper", Content = "spawned: " .. state.pet, Duration = 3, Image = "check" })
    end,
})

tabdivine:CreateSection("spawn")
tabdivine:CreateButton({
    Name = "Spawn selected pet",
    Callback = function()
        state.rarity = "Divine"
        spawnpet()
        Rayfield:Notify({ Title = "sillycopper", Content = "spawned: " .. state.pet, Duration = 3, Image = "check" })
    end,
})

Rayfield:LoadConfiguration()
