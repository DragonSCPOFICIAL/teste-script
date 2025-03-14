print("https://discord.gg/aUd8umqUKu8888")
toclipboard("https://discord.gg/aUd8umqUKu88888")

-- Remover efeitos indesejados
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Effects = ReplicatedStorage.Effect.Container

for _, effectName in ipairs({"Death", "Respawn"}) do
    if Effects:FindFirstChild(effectName) then
        Effects[effectName]:Destroy()
    end
end

-- Configurações principais
_G.Settings = {
    Main = {
        ["Auto Farm Level"] = false,
        ["Fast Auto Farm Level"] = false,

        -- [Mob Aura]
        ["Distance Mob Aura"] = 1000, -- {Max: 5000}
        ["Mob Aura"] = false,

        -- [World 1]
        ["Auto New World"] = false,
        ["Auto Saber"] = false,
        ["Auto Pole"] = false,
        ["Auto Buy Ability"] = false,

        -- [World 2]
        ["Auto Third Sea"] = false,
        ["Auto Factory"] = false,
        ["Auto Factory Hop"] = false,
        ["Auto Bartilo Quest"] = false,
        ["Auto True Triple Katana"] = false,
        ["Auto Rengoku"] = false,
        ["Auto Swan Glasses"] = false,
        ["Auto Dark Coat"] = false,
        ["Auto Ectoplasm"] = false,
        ["Auto Buy Legendary Sword"] = false,
        ["Auto Buy Enchantment Haki"] = false,

        -- [World 3]
        ["Auto Holy Torch"] = false,
        ["Auto Buddy Swords"] = false,
        ["Auto Farm Boss Hallow"] = false,
        ["Auto Rainbow Haki"] = false,
        ["Auto Elite Hunter"] = false,
        ["Auto Musketeer Hat"] = false,
        ["Auto Buddy Sword"] = false,
        ["Auto Farm Bone"] = false,
        ["Auto Ken-Haki V2"] = false,
        ["Auto Cavander"] = false,
        ["Auto Yama Sword"] = false,
        ["Auto Tushita Sword"] = false,
        ["Auto Serpent Bow"] = false,
        ["Auto Dark Dagger"] = false,
        ["Auto Cake Prince"] = false,
        ["Auto Dough V2"] = false,
        ["Auto Random Bone"] = false,

        -- [For God Human]
        ["Auto Fish Tail Sea 1"] = false,
        ["Auto Fish Tail Sea 3"] = false,
        ["Auto Magma Ore Sea 2"] = false,
        ["Auto Magma Ore Sea 1"] = false,
        ["Auto Mystic Droplet"] = false,
        ["Auto Dragon Scales"] = false,
    },

    FightingStyle = {
        ["Auto God Human"] = false,
        ["Auto Superhuman"] = false,
        ["Auto Electric Claw"] = false,
        ["Auto Death Step"] = false,
        ["Auto Fully Death Step"] = false,
        ["Auto SharkMan Karate"] = false,
        ["Auto Fully SharkMan Karate"] = false,
        ["Auto Dragon Talon"] = false,
    },

    Boss = {
        ["Auto All Boss"] = false,
        ["Auto Boss Select"] = false,
        ["Select Boss"] = {},
        ["Auto Quest"] = false,
    },

    Mastery = {
        ["Select Multi Sword"] = {},
        ["Farm Mastery SwordList"] = false,
        ["Auto Farm Fruit Mastery"] = false,
        ["Auto Farm Gun Mastery"] = false,
        ["Mob Health (%)"] = 15,
    },

    Configs = {
        ["Double Quest"] = false,
        ["Bypass TP"] = false,
        ["Select Team"] = {"Pirate"}, -- {Pirate, Marine}

        ["Fast Attack"] = true,
        ["Fast Attack Type"] = {"Fast"}, -- {Normal, Fast, Slow}

        ["Select Weapon"] = {},

        -- [Misc Configs]
        ["Auto Haki"] = true,
        ["Distance Auto Farm"] = 20, -- {Max: 50}
        ["Camera Shaker"] = false,

        -- [Skill Configs]
        ["Skill Z"] = true,
        ["Skill X"] = true,
        ["Skill C"] = true,
        ["Skill V"] = true,

        -- [Mob Configs]
        ["Show Hitbox"] = false,
        ["Bring Mob"] = true,
        ["Disabled Damage"] = false,
    },

    Stat = {
        -- [Auto Stats]
        ["Enabled Auto Stats"] = false,
        ["Auto Stats Kaitun"] = false,
        ["Select Stats"] = {"Melee"}, -- {Max Stats, Melee, Defense, Sword, Devil Fruit, Gun}
        ["Point Select"] = 3, -- {Recommended, Max: 9}

        -- [Auto Redeem Code]
        ["Enabled Auto Redeem Code"] = false,
        ["Select Level Redeem Code"] = 1, -- {Max: 2400}
    },

    Misc = {
        ["No Soru Cooldown"] = false,
        ["No Dash Cooldown"] = false,
        ["Infinite Geppo"] = false,
        ["Infinite Energy"] = false,
        ["No Fog"] = false,
        ["Wall-TP"] = false,
        ["Fly"] = false,
        ["Fly Speed"] = 1,

        -- [Server]
        ["Auto Rejoin"] = true,
    },

    Teleport = {
        ["Teleport to Sea Beast"] = false,
    },

    Fruits = {
        ["Auto Buy Random Fruits"] = false,
        ["Auto Store Fruits"] = false,
        ["Select Devil Fruits"] = {}, -- Lista de frutas completa corrigida
        ["Auto Buy Devil Fruits Sniper"] = false,
    },

    Raids = {
        ["Auto Raids"] = false,
        ["Kill Aura"] = false,
        ["Auto Awakened"] = false,
        ["Auto Next Place"] = false,
        ["Select Raids"] = {}, -- Tipos de raids corrigidos
    },

    Combat = {
        ["Fov Size"] = 200,
        ["Show Fov"] = false,
        ["Aimbot Skill"] = false,
    },

    HUD = {
        ["FPS"] = 60,
        ["LockFPS"] = true,
        ["Boost FPS Windows"] = false,
        ['White Screen'] = false,
    },

    ConfigsUI = {
        ColorUI = Color3.fromRGB(255, 0, 127), -- {Color UI}
    }
}
-- [Require Module Optimized]

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Workspace = game:GetService("Workspace")

-- Cached references
local LocalPlayer = Players.LocalPlayer
local RigControllerEvent = ReplicatedStorage.RigControllerEvent
local Validator = ReplicatedStorage.Remotes.Validator
local CombatFramework = require(LocalPlayer.PlayerScripts:WaitForChild("CombatFramework"))
local CombatFrameworkR = getupvalues(CombatFramework)[2]
local RigController = require(LocalPlayer.PlayerScripts.CombatFramework.RigController)
local RigControllerR = getupvalues(RigController)[2]
local realbhit = require(ReplicatedStorage.CombatFramework.RigLib)

-- Attack constants
local BASE_ATTACK_RANGE = 60
local HITBOX_OFFSET = 5
local ATTACK_MULTIPLIERS = {727595, 798405}
local MAX_32BIT = 1099511627776
local COLOR_DIVISOR = 16777215

local cooldownfastattack = tick()

-- Optimized enemy collection
local function getAllBladeHits(range)
    local hits = {}
    local character = LocalPlayer.Character
    local enemies = Workspace.Enemies:GetChildren()
    
    if not character then return hits end
    
    local humanoidRoot = character:FindFirstChild("HumanoidRootPart")
    if not humanoidRoot then return hits end
    
    local checkDistance = range + HITBOX_OFFSET
    local rootPosition = humanoidRoot.Position

    for _, enemy in ipairs(enemies) do
        local human = enemy:FindFirstChildOfClass("Humanoid")
        local rootPart = human and human.RootPart
        
        if rootPart and human.Health > 0 then
            local distance = (rootPart.Position - rootPosition).Magnitude
            if distance < checkDistance then
                table.insert(hits, rootPart)
            end
        end
    end
    
    return hits
end

-- Weapon caching system
local weaponCache = {
    lastChecked = 0,
    value = nil
}

local function CurrentWeapon()
    local now = tick()
    if now - weaponCache.lastChecked < 0.1 then
        return weaponCache.value
    end

    weaponCache.lastChecked = now
    local ac = CombatFrameworkR.activeController
    local blade = ac and ac.blades[1]

    if blade then
        pcall(function()
            while blade.Parent ~= LocalPlayer.Character do
                blade = blade.Parent
            end
        end)
        weaponCache.value = blade
        return blade
    end

    weaponCache.value = LocalPlayer.Character:FindFirstChildOfClass("Tool") and 
                       LocalPlayer.Character:FindFirstChildOfClass("Tool").Name
    return weaponCache.value
end

-- Optimized attack sequence
local attackState = {
    AcAttack7 = nil,
    AcAttack8 = nil,
    AcAttack9 = nil,
    AcAttack10 = nil
}

local function UpdateAttackState(ac)
    attackState.AcAttack8 = debug.getupvalue(ac.attack, 5)
    attackState.AcAttack9 = debug.getupvalue(ac.attack, 6)
    attackState.AcAttack7 = debug.getupvalue(ac.attack, 4)
    attackState.AcAttack10 = debug.getupvalue(ac.attack, 7)
end

local function CalculateAttackValues()
    local numberAc12 = (attackState.AcAttack8 * ATTACK_MULTIPLIERS[2] + 
                       attackState.AcAttack7 * ATTACK_MULTIPLIERS[1]) % attackState.AcAttack9
    local numberAc13 = attackState.AcAttack7 * ATTACK_MULTIPLIERS[2]
    
    numberAc12 = (numberAc12 * attackState.AcAttack9 + numberAc13) % MAX_32BIT
    attackState.AcAttack8 = math.floor(numberAc12 / attackState.AcAttack9)
    attackState.AcAttack7 = numberAc12 - attackState.AcAttack8 * attackState.AcAttack9
    attackState.AcAttack10 += 1
    
    return numberAc12
end

local function ExecuteAttack(ac, bladehit, numberAc12)
    RigControllerEvent:FireServer("weaponChange", tostring(CurrentWeapon()))
    Validator:FireServer(
        math.floor(numberAc12 / MAX_32BIT * COLOR_DIVISOR),
        attackState.AcAttack10
    )
    RigControllerEvent:FireServer("hit", bladehit, 2, "")
end

local function PlayAttackAnimations(animator)
    for _, anim in pairs(animator.anims.basic) do
        anim:Play(0.01, 0.01, 0.01)
    end
end

function AttackFunction()
    local ac = CombatFrameworkR.activeController
    if not (ac and ac.equipped) then return end

    local bladehit = getAllBladeHits(BASE_ATTACK_RANGE)
    if #bladehit == 0 then return end

    UpdateAttackState(ac)
    local numberAc12 = CalculateAttackValues()
    
    debug.setupvalue(ac.attack, 5, attackState.AcAttack8)
    debug.setupvalue(ac.attack, 6, attackState.AcAttack9)
    debug.setupvalue(ac.attack, 4, attackState.AcAttack7)
    debug.setupvalue(ac.attack, 7, attackState.AcAttack10)

    PlayAttackAnimations(ac.animator)
    
    if LocalPlayer.Character:FindFirstChildOfClass("Tool") and ac.blades and ac.blades[1] then
        ExecuteAttack(ac, bladehit, numberAc12)
    end
end
local EnemySpawns = Instance.new("Folder")
EnemySpawns.Name = "EnemySpawns"
EnemySpawns.Parent = workspace

-- Helper function to clean enemy names
local function cleanEnemyName(name)
    local result = name:gsub("Lv. ", "")
                      :gsub("[%[%]]", "")
                      :gsub("%d+", "")
                      :gsub("%s+", "")
    return result
end

-- Process existing enemy spawns
for _, v in pairs(workspace._WorldOrigin.EnemySpawns:GetChildren()) do
    if v:IsA("Part") then
        local EnemySpawnsX2 = v:Clone()
        EnemySpawnsX2.Name = cleanEnemyName(v.Name)
        EnemySpawnsX2.Parent = EnemySpawns
        EnemySpawnsX2.Anchored = true
    end
end

-- Process active enemies in workspace
for _, v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
    if v:IsA("Model") and v:FindFirstChild("HumanoidRootPart") then
        print(v.HumanoidRootPart.Parent)
        local EnemySpawnsX2 = v.HumanoidRootPart:Clone()
        local cleanName = cleanEnemyName(v.Name)
        print(cleanName)
        EnemySpawnsX2.Name = cleanName
        EnemySpawnsX2.Parent = EnemySpawns
        EnemySpawnsX2.Anchored = true
    end
end

-- Process enemies in ReplicatedStorage
for _, v in pairs(game.ReplicatedStorage:GetChildren()) do
    if v:IsA("Model") and v:FindFirstChild("HumanoidRootPart") then
        local EnemySpawnsX2 = v.HumanoidRootPart:Clone()
        local cleanName = cleanEnemyName(v.Name)
        print(cleanName)
        EnemySpawnsX2.Name = cleanName
        EnemySpawnsX2.Parent = EnemySpawns
        EnemySpawnsX2.Anchored = true
    end
end

-- Paths for settings
local SETTINGS_FOLDER = "Silver Hub Premium Scripts"
local GAME_FOLDER = SETTINGS_FOLDER.."/Blox Fruits/"
local PLAYER_SETTINGS_FILE = GAME_FOLDER..game.Players.LocalPlayer.Name..".json"

-- Load settings from file
function LoadSettings()
    if readfile and writefile and isfile and isfolder then
        -- Create folders if they don't exist
        if not isfolder(SETTINGS_FOLDER) then
            makefolder(SETTINGS_FOLDER)
        end
        
        if not isfolder(GAME_FOLDER) then
            makefolder(GAME_FOLDER)
        end
        
        -- Create or load settings file
        if not isfile(PLAYER_SETTINGS_FILE) then
            writefile(PLAYER_SETTINGS_FILE, game:GetService("HttpService"):JSONEncode(_G.Settings))
        else
            local success, decodedSettings = pcall(function()
                return game:GetService("HttpService"):JSONDecode(readfile(PLAYER_SETTINGS_FILE))
            end)
            
            if success and type(decodedSettings) == "table" then
                for i, v in pairs(decodedSettings) do
                    _G.Settings[i] = v
                end
            else
                warn("Settings file corrupted. Creating new file.")
                writefile(PLAYER_SETTINGS_FILE, game:GetService("HttpService"):JSONEncode(_G.Settings))
            end
        end
    else
        return warn("Status: Undetected Executor")
    end
end

-- Save settings to file
function SaveSettings()
    if readfile and writefile and isfile and isfolder then
        if not isfile(PLAYER_SETTINGS_FILE) then
            LoadSettings()
        else
            local currentSettings = {}
            for i, v in pairs(_G.Settings) do
                currentSettings[i] = v
            end
            
            local success, encodedSettings = pcall(function()
                return game:GetService("HttpService"):JSONEncode(currentSettings)
            end)
            
            if success then
                writefile(PLAYER_SETTINGS_FILE, encodedSettings)
            else
                warn("Failed to encode settings")
            end
        end
    else
        return warn("Status: Undetected Executor")
    end
end
LoadSettings()
------------ // AutoUpdate \\ ------------
spawn(function()
    while wait() do
        if _G.AutoFarmLevelReal then
            FastAttack = true
        else
            FastAttack = false
        end
    end
end)

local function QuestCheck()
    local Lvl = game:GetService("Players").LocalPlayer.Data.Level.Value
    
    -- Helper function to find mob spawn locations
    local function GetMobSpawnLocations(mobName)
        local cleanName = mobName:gsub("Lv. ", ""):gsub("[%[%]]", ""):gsub("%d+", ""):gsub("%s+", "")
        local matchingCFrames = {}
        
        for _, v in pairs(game.workspace.EnemySpawns:GetChildren()) do
            if v.Name == cleanName then
                table.insert(matchingCFrames, v.CFrame)
            end
        end
        
        return matchingCFrames
    end
    
    -- Quest data structure
    local questData = {
        QuestLevel = 1,
        NPCPosition = CFrame.new(0, 0, 0),
        MobName = "",
        QuestName = "",
        LevelRequire = 1,
        Mon = "",
        MobCFrame = {}
    }
    
    -- Level 1-9 quests
    if Lvl >= 1 and Lvl <= 9 then
        if tostring(game.Players.LocalPlayer.Team) == "Marines" then
            questData.MobName = "Trainee [Lv. 5]"
            questData.QuestName = "MarineQuest"
            questData.QuestLevel = 1
            questData.Mon = "Trainee"
            questData.NPCPosition = CFrame.new(-2709.67944, 24.5206585, 2104.24585, -0.744724929, -3.97967455e-08, -0.667371571, 4.32403588e-08, 1, -1.07884304e-07, 0.667371571, -1.09201515e-07, -0.744724929)
        elseif tostring(game.Players.LocalPlayer.Team) == "Pirates" then
            questData.MobName = "Bandit [Lv. 5]"
            questData.Mon = "Bandit"
            questData.QuestName = "BanditQuest1"
            questData.QuestLevel = 1
            questData.NPCPosition = CFrame.new(1059.99731, 16.9222069, 1549.28162, -0.95466274, 7.29721794e-09, 0.297689587, 1.05190106e-08, 1, 9.22064114e-09, -0.297689587, 1.19340022e-08, -0.95466274)
        end
        
        questData.MobCFrame = GetMobSpawnLocations(questData.MobName)
        return {
            [1] = questData.QuestLevel,
            [2] = questData.NPCPosition,
            [3] = questData.MobName,
            [4] = questData.QuestName,
            [5] = questData.LevelRequire,
            [6] = questData.Mon,
            [7] = questData.MobCFrame
        }
    end
    
    -- Level 210-249 quests
    if Lvl >= 210 and Lvl <= 249 then
        questData.MobName = "Dangerous Prisoner [Lv. 210]"
        questData.QuestName = "PrisonerQuest"
        questData.QuestLevel = 2
        questData.Mon = "Dangerous Prisoner"
        questData.NPCPosition = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
        questData.MobCFrame = GetMobSpawnLocations(questData.MobName)
        
        return {
            [1] = questData.QuestLevel,
            [2] = questData.NPCPosition,
            [3] = questData.MobName,
            [4] = questData.QuestName,
            [5] = questData.LevelRequire,
            [6] = questData.Mon,
            [7] = questData.MobCFrame
        }
    end
--game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
    local GuideModule = require(game:GetService("ReplicatedStorage").GuideModule)
    local Quests = require(game:GetService("ReplicatedStorage").Quests)
    
    -- Process quest data from GuideModule
    for i, v in pairs(GuideModule["Data"]["NPCList"]) do
        for i1, v1 in pairs(v["Levels"]) do
            if Lvl >= v1 then
                if not LevelRequire then
                    LevelRequire = 0
                end
                if v1 > LevelRequire then
                    NPCPosition = i["CFrame"]
                    QuestLevel = i1
                    LevelRequire = v1
                end
                -- Special case for NPCs with 3 levels
                if #v["Levels"] == 3 and QuestLevel == 3 then
                    NPCPosition = i["CFrame"]
                    QuestLevel = 2
                    LevelRequire = v["Levels"][2]
                end
            end
        end
    end
    
    -- Special case for teleporting to Fishman area
    local function TeleportToFishmanArea()
        if _G.StartFarm and (MobCFrame.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
            return true
        end
        return false
    end
    
    -- Specific level ranges for mobs
    if Lvl >= 375 and Lvl <= 399 then -- Fishman Warrior
        MobCFrame = CFrame.new(61122.5625, 18.4716396, 1568.16504, 0.893533468, 3.95251609e-09, 0.448996574, -2.34327455e-08, 1, 3.78297464e-08, -0.448996574, -4.43233645e-08, 0.893533468)
        if TeleportToFishmanArea() then
            return
        end
    end
    
    if Lvl >= 400 and Lvl <= 449 then -- Fishman Commando
        MobCFrame = CFrame.new(61122.5625, 18.4716396, 1568.16504, 0.893533468, 3.95251609e-09, 0.448996574, -2.34327455e-08, 1, 3.78297464e-08, -0.448996574, -4.43233645e-08, 0.893533468)
        if TeleportToFishmanArea() then
            return
        end
    end
    
    -- Find quest details from Quests module
    for i, v in pairs(Quests) do
        for i1, v1 in pairs(v) do
            if v1["LevelReq"] == LevelRequire and i ~= "CitizenQuest" then
                QuestName = i
                for i2, v2 in pairs(v1["Task"]) do
                    MobName = i2
                    Mon = string.split(i2, " [Lv. ".. v1["LevelReq"] .. "]")[1]
                end
            end
        end
    end
    
    -- Special case quests that need manual adjustments
    local questOverrides = {
        ["MarineQuest2"] = function()
            QuestName = "MarineQuest2"
            QuestLevel = 1
            MobName = "Chief Petty Officer [Lv. 120]"
            Mon = "Chief Petty Officer"
            LevelRequire = 120
        end,
        ["ImpelQuest"] = function()
            QuestName = "PrisonerQuest"
            QuestLevel = 2
            MobName = "Dangerous Prisoner [Lv. 190]"
            Mon = "Dangerous Prisoner"
            LevelRequire = 210
            NPCPosition = CFrame.new(5310.60547, 0.350014925, 474.946594, 0.0175017118, 0, 0.999846935, 0, 1, 0, -0.999846935, 0, 0.0175017118)
        end,
        ["SkyExp1Quest"] = function()
            if QuestLevel == 1 then
                NPCPosition = CFrame.new(-4721.88867, 843.874695, -1949.96643, 0.996191859, -0, -0.0871884301, 0, 1, -0, 0.0871884301, 0, 0.996191859)
            elseif QuestLevel == 2 then
                NPCPosition = CFrame.new(-7859.09814, 5544.19043, -381.476196, -0.422592998, 0, 0.906319618, 0, 1, 0, -0.906319618, 0, -0.422592998)
            end
        end,
        ["Area2Quest"] = function()
            if QuestLevel == 2 then
                QuestName = "Area2Quest"
                QuestLevel = 1
                MobName = "Swan Pirate [Lv. 775]"
                Mon = "Swan Pirate"
                LevelRequire = 775
            end
        end
    }
    
    -- Apply quest overrides if needed
    if questOverrides[QuestName] then
        questOverrides[QuestName]()
    end
    
    -- Clean up mob name
    MobName = MobName:sub(1, #MobName)
    
    -- Find appropriate mob level if not specified
    if not MobName:find("Lv") then
        -- Check workspace enemies
        for i, v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
            local MonLV = string.match(v.Name, "%d+")
            if MonLV and v.Name:find(MobName) and #v.Name > #MobName and tonumber(MonLV) <= Lvl + 50 then
                MobName = v.Name
            end
        end
        
        -- Check replicated storage if not found in workspace
        if not MobName:find("Lv") then
            for i, v in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
                local MonLV = string.match(v.Name, "%d+")
                if MonLV and v.Name:find(MobName) and #v.Name > #MobName and tonumber(MonLV) <= Lvl + 50 then
                    MobName = v.Name
                    Mon = MobName:match("^([^[]+)") -- Extract name without level
                    if Mon then Mon = Mon:gsub("%s+$", "") end -- Remove trailing spaces
                end
            end
        end
    end
local function GetMobCFrames(MobName)
    local matchingCFrames = {}
    local cleanName = string.gsub(MobName, "Lv. ", "")
    cleanName = string.gsub(cleanName, "[%[%]]", "")
    cleanName = string.gsub(cleanName, "%d+", "")
    cleanName = string.gsub(cleanName, "%s+", "")
    
    for _, v in pairs(game.workspace.EnemySpawns:GetChildren()) do
        if v.Name == cleanName then
            table.insert(matchingCFrames, v.CFrame)
        end
    end
    
    return matchingCFrames
end

local function QuestCheck()
    -- Rest of the QuestCheck function code...
    
    -- Get mob spawn locations
    MobCFrame = GetMobCFrames(MobName)
    
    return {
        [1] = QuestLevel,
        [2] = NPCPosition,
        [3] = MobName,
        [4] = QuestName,
        [5] = LevelRequire,
        [6] = Mon,
        [7] = MobCFrame,
        [8] = MonQ,
        [9] = MobCFrameNuber
    }
end

function Bypass(Point)
    toposition(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
    wait(1.5)
    _G.StopTween = true
    _G.StertScript = false

    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
    
    local hrp = game.Players.LocalPlayer.Character.HumanoidRootPart
    
    -- Teleport sequence
    game.Players.LocalPlayer.Character.Head:Destroy()
    hrp.CFrame = Point * CFrame.new(0, 50, 0)
    wait(.2)
    hrp.CFrame = Point
    wait(.1)
    hrp.CFrame = Point * CFrame.new(0, 50, 0)
    hrp.Anchored = true
    wait(.1)
    hrp.CFrame = Point
    wait(0.5)
    hrp.Anchored = false
    hrp.CFrame = Point * CFrame.new(900, 900, 900)
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")

    -- Reset global variables
    _G.StopTween = false
    _G.StertScript = false
    _G.Clip = false
    
    -- Remove BodyClip if it exists
    if game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
        game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
    end
end

local function toTarget(...)
    local RealtargetPos = {...}
    local targetPos = RealtargetPos[1]
    local RealTarget
    
    -- Determine target type and convert to CFrame
    if type(targetPos) == "vector" then
        RealTarget = CFrame.new(targetPos)
    elseif type(targetPos) == "userdata" then
        RealTarget = targetPos
    elseif type(targetPos) == "number" then
        RealTarget = CFrame.new(unpack(RealtargetPos))
    end

    -- Wait for player to respawn if dead
    if game.Players.LocalPlayer.Character:WaitForChild("Humanoid").Health == 0 then 
        if tween then tween:Cancel() end 
        repeat wait() until game.Players.LocalPlayer.Character:WaitForChild("Humanoid").Health > 0
        wait(0.2) 
    end

    -- Adjust speed based on distance
    local Distance = (RealTarget.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).Magnitude
    local Speed = Distance < 1000 and 315 or 300

    -- Handle bypass teleport for long distances
    if _G.Settings.Configs["Bypass TP"] then
        local shouldBypass = Distance > 3000 and 
                            not AutoFarmMaterial and 
                            not _G.Settings.FightingStyle["Auto God Human"] and 
                            not _G.Settings.Raids["Auto Raids"] and
                            not HasSpecialItems() and
                            not IsFishman(Name)
        
        if shouldBypass then
            pcall(function()
                if tween then tween:Cancel() end
                local fkwarp = false
                local playerData = game:GetService("Players")["LocalPlayer"].Data
                local targetIsland = GetIsLand(RealTarget)
                
                -- Teleport based on spawn point
                if playerData:FindFirstChild("SpawnPoint").Value == tostring(targetIsland) then
                    wait(.1)
                    Com("F_", "TeleportToSpawn")
                elseif playerData:FindFirstChild("LastSpawnPoint").Value == tostring(targetIsland) then
                    game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid"):ChangeState(15)
                    wait(0.1)
                    repeat wait() until game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid").Health > 0
                else
                    if game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid").Health > 0 then
                        if not fkwarp then
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = RealTarget
                        end
                        fkwarp = true
                    end
                    wait(.08)
                    game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid"):ChangeState(15)
                    repeat wait() until game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid").Health > 0
                    wait(.1)
                    Com("F_", "SetSpawnPoint")
                end
                
                return
            end)
        end
    end
    
    -- Helper functions for condition checks
    function HasSpecialItems()
        local items = {
            "Special Microchip",
            "God's Chalice",
            "Hallow Essence",
            "Sweet Chalice"
        }
        
        for _, item in pairs(items) do
            if game.Players.LocalPlayer.Backpack:FindFirstChild(item) or 
               game.Players.LocalPlayer.Character:FindFirstChild(item) then
                return true
            end
        end
        return false
    end
    
    function IsFishman(Name)
        return Name == "Fishman Commando [Lv. 400]" or Name == "Fishman Warrior [Lv. 375]"
    end
    
    -- Return the tweenfunc table (seems to be incomplete in the original code)
    return tweenfunc
end

local tween_s = game:GetService("TweenService") -- Using GetService is more reliable than service shortcut
local tweenfunc = {} -- Missing declaration of tweenfunc table

function tweenfunc:Create(RealTarget, Speed)
    local info = TweenInfo.new(
        (RealTarget.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).Magnitude/Speed, 
        Enum.EasingStyle.Linear
    )
    
    local tween
    local tweenw, err = pcall(function()
        tween = tween_s:Create(game.Players.LocalPlayer.Character["HumanoidRootPart"], info, {CFrame = RealTarget})
        tween:Play()
    end)
    
    if not tweenw then
        warn("Tween creation failed: " .. tostring(err))
        return nil
    end
    
    function tweenfunc:Stop()
        if tween then
            tween:Cancel()
        end
    end 
    
    function tweenfunc:Wait()
        if tween then
            tween.Completed:Wait()
        end
    end 
    
    return tweenfunc
end

function InMyNetWork(object)
    if object and object:IsA("BasePart") then
        if isnetworkowner then
            return isnetworkowner(object)
        else
            if game.Players.LocalPlayer.Character and 
               game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") and
               (object.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 350 then 
                return true
            end
            return false
        end
    end
    return false
end

-- SimulationRadius handling
task.spawn(function()
    while true do 
        task.wait()
        pcall(function() -- Added pcall to handle errors
            if setscriptable then
                setscriptable(game.Players.LocalPlayer, "SimulationRadius", true)
            end
            if sethiddenproperty then
                sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
            end
        end)
    end
end)

local SetCFarme = 1
local function GetIsLand(...)
    local RealtargetPos = {...}
    local targetPos = RealtargetPos[1]
    local RealTarget
    
    if type(targetPos) == "vector" then
        RealTarget = targetPos
    elseif type(targetPos) == "userdata" then
        RealTarget = targetPos.Position
    elseif type(targetPos) == "number" then
        RealTarget = CFrame.new(unpack(RealtargetPos))
        RealTarget = RealTarget.p
    end
    
    local ReturnValue
    local CheckInOut = math.huge
    
    if game.Players.LocalPlayer.Team then
        local teamSpawns = game.Workspace._WorldOrigin.PlayerSpawns:FindFirstChild(tostring(game.Players.LocalPlayer.Team))
        if teamSpawns then
            for i, v in pairs(teamSpawns:GetChildren()) do 
                if v:IsA("Model") then
                    local modelCFrame = v:GetModelCFrame()
                    if modelCFrame then
                        local ReMagnitude = (RealTarget - modelCFrame.p).Magnitude
                        if ReMagnitude < CheckInOut then
                            CheckInOut = ReMagnitude
                            ReturnValue = v.Name
                        end
                    end
                end
            end
        end
    end
    
    return ReturnValue
end

-- Mob farming
task.spawn(function()
    while task.wait() do
        pcall(function()
            if _G.AutoFarmLevelReal and BringMobFarm and PosMon then
                for i, v in pairs(game.Workspace.Enemies:GetChildren()) do
                    if v:IsA("Model") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and
                       not string.find(v.Name, "Boss") and 
                       (v.HumanoidRootPart.Position - PosMon.Position).magnitude <= 400 then
                        
                        if InMyNetWork(v.HumanoidRootPart) then
                            v.HumanoidRootPart.CFrame = PosMon
                            v.Humanoid.JumpPower = 0
                            v.Humanoid.WalkSpeed = 0
                            v.HumanoidRootPart.Size = Vector3.new(60, 60, 60)
                            v.HumanoidRootPart.Transparency = 1
                            v.HumanoidRootPart.CanCollide = false
                            
                            if v:FindFirstChild("Head") then
                                v.Head.CanCollide = false
                            end
                            
                            if v.Humanoid:FindFirstChild("Animator") then
                                v.Humanoid.Animator:Destroy()
                            end
                            
                            v.Humanoid:ChangeState(11)
                            v.Humanoid:ChangeState(14)
                            
                            pcall(function()
                                sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
                            end)
                        end
                    end
                end
            end
        end)
    end
end)

function EquipWeapon(Tool)
    pcall(function()
        if game.Players.LocalPlayer.Backpack:FindFirstChild(Tool) and
           game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") then
            local ToolHumanoid = game.Players.LocalPlayer.Backpack:FindFirstChild(Tool) 
            game.Players.LocalPlayer.Character.Humanoid:EquipTool(ToolHumanoid) 
        end
    end)
end

function UnEquipWeapon(Weapon)
    pcall(function()
        if game.Players.LocalPlayer.Character:FindFirstChild(Weapon) then
            _G.NotAutoEquip = true
            task.wait(.5)
            game.Players.LocalPlayer.Character:FindFirstChild(Weapon).Parent = game.Players.LocalPlayer.Backpack
            task.wait(.1)
            _G.NotAutoEquip = false
        end
    end)
end

spawn(function()
    while wait(0.1) do -- Improved wait time for better performance
        if _G.AutoFarmLevelReal then
            local MyLevel = game.Players.LocalPlayer.Data.Level.Value
            local QuestC = game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest
            
            if QuestC.Visible == true then
                -- Check distance to quest and bypass if too far
                if QuestCheck() and (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude >= 3000 then
                    Bypass(QuestCheck()[2])
                end
                
                -- Check if enemies exist
                if QuestCheck() and game:GetService("Workspace").Enemies:FindFirstChild(QuestCheck()[3]) then
                    for i, v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                        if v and v.Name == QuestCheck()[3] then
                            if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                repeat task.wait()
                                    if not QuestCheck() or not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, QuestCheck()[6]) then
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                                    else
                                        PosMon = v.HumanoidRootPart.CFrame
                                        v.HumanoidRootPart.Size = Vector3.new(60, 60, 60)
                                        v.HumanoidRootPart.CanCollide = false
                                        v.Humanoid.WalkSpeed = 0
                                        v.Head.CanCollide = false
                                        BringMobFarm = true
                                        EquipWeapon(_G.Settings.Configs["Select Weapon"])
                                        v.HumanoidRootPart.Transparency = 1
                                        toTarget(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 5))
                                    end
                                until not _G.AutoFarmLevelReal or not v.Parent or v.Humanoid.Health <= 0 or QuestC.Visible == false or not v:FindFirstChild("HumanoidRootPart")
                            end
                        end
                    end
                else
                    -- No enemies found, move to spawn location
                    if QuestCheck() then
                        UnEquipWeapon(_G.Settings.Configs["Select Weapon"])
                        toTarget(QuestCheck()[7][SetCFarme] * CFrame.new(0, 30, 5))
                        
                        if (QuestCheck()[7][SetCFarme].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 50 then
                            -- Reset or increment SetCFarme
                            if SetCFarme == nil or SetCFarme == '' or SetCFarme >= #QuestCheck()[7] then
                                SetCFarme = 1
                            else
                                SetCFarme = SetCFarme + 1
                            end
                            
                            task.wait(0.5)
                        end
                    end
                end
            else
                -- Quest not visible, get a quest
                task.wait(0.5)
                
                if QuestCheck() and GetIsLand and game:GetService("Players").LocalPlayer.Data.LastSpawnPoint.Value == tostring(GetIsLand(QuestCheck()[7][1])) then
                    -- Already at the right island
                    game:GetService('ReplicatedStorage').Remotes.CommF_:InvokeServer("StartQuest", QuestCheck()[4], QuestCheck()[1]) 
                    task.wait(0.5)
                    toTarget(QuestCheck()[7][1] * CFrame.new(0, 30, 20))
                else
                    if QuestCheck() then
                        if (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude >= 3000 then
                            -- Too far, use bypass
                            Bypass(QuestCheck()[2])
                        else
                            -- Move to quest giver
                            repeat 
                                task.wait() 
                                if QuestCheck() then
                                    toTarget(QuestCheck()[2]) 
                                end
                            until not QuestCheck() or (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 20 or not _G.StartFarm
                            
                            -- Additional check to ensure we're at quest giver
                            if QuestCheck() and (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1 then
                                BringMobFarm = false
                                task.wait(0.2)
                                game:GetService('ReplicatedStorage').Remotes.CommF_:InvokeServer("StartQuest", QuestCheck()[4], QuestCheck()[1]) 
                                task.wait(0.5)
                                toTarget(QuestCheck()[7][1] * CFrame.new(0, 30, 20))
                            end
                        end
                    end
                end
            end
        end
    end
end)

-- UI Library
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/minhhau207/SilverHub/main/obfuscated-3788.lua"))()

local Main = Library.xova()

-- Create tabs
local Tab1 = Main.create("เมนูหลัก")
local Tab2 = Main.create("ผู้เล่น/สเเตก")
local Tab3 = Main.create("วาป/ดันเจี้ยน")
local Tab4 = Main.create("ร้านค้า")
local Tab5 = Main.create("อื่น ๆ")

-------------[Tab1]-------------
local Page1 = Tab1.xovapage(1)
local Page2 = Tab1.xovapage(1)
local Page3 = Tab1.xovapage(2)
local Page8 = Tab1.xovapage(2)
local Page4 = Tab1.xovapage(2)
local Page5 = Tab1.xovapage(2)
local Page6 = Tab1.xovapage(1)
local Page7 = Tab1.xovapage(2)

-------------[Tab2]-------------
local Page9 = Tab2.xovapage(1)
local Page15 = Tab2.xovapage(2)

-------------[Tab3]-------------
local Page10 = Tab3.xovapage(1)
local Page11 = Tab3.xovapage(2)

-------------[Tab4]-------------
local Page12 = Tab4.xovapage(1)
local Page13 = Tab4.xovapage(2)

-------------[Tab5]-------------
local Page14 = Tab5.xovapage(1)
local Page16 = Tab5.xovapage(2)

Page1.Label({
    Title = "Main",
})

Page1.Toggle({
             Title = "Auto Farm Level",
    Mode = 2,
    Default = _G.Settings.Main["Auto Farm Level"],
    Desc = "Select Farm Type First",
    callback = function(value)
        _G.AutoFarmLevelReal = value
        Auto_Farm_Level = value
        if value == false then
            toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame)
        end
        SaveSettings()
    end,
})

Page3.Toggle({
    Title = "Fast Attack",
    Default = _G.Settings.Configs["Fast Attack"],
    callback = function(value)
        _G.Settings.Configs["Fast Attack"] = value
        SaveSettings()
    end,
})

Page3.Dropdown({
    Title = "Fast Attack Type",
    Item = {"Fast","Normal","Slow"},
    callback = function(value)
        _G.Settings.Configs["Fast Attack Type"] = value
        SaveSettings()
    end,
})

-- Improved attack system using coroutine
coroutine.wrap(function()
    local cooldownfastattack = tick()
    while task.wait(.1) do
        pcall(function()
            local ac = CombatFrameworkR.activeController
            if ac and ac.equipped then
                if FastAttack and _G.Settings.Configs["Fast Attack"] then
                    AttackFunction()
                    local attackDelay = 0.9  -- Default delay
                    local waitTime = 0.1     -- Default wait time
                    
                    if _G.Settings.Configs["Fast Attack Type"] == "Fast" then
                        attackDelay = 1.5
                        waitTime = 0.01
                    elseif _G.Settings.Configs["Fast Attack Type"] == "Slow" then
                        attackDelay = 0.3
                        waitTime = 0.7
                    end
                    
                    if tick() - cooldownfastattack > attackDelay then 
                        wait(waitTime) 
                        cooldownfastattack = tick() 
                    end
                elseif FastAttack and _G.Settings.Configs["Fast Attack"] == false then
                    if ac.hitboxMagnitude ~= 55 then
                        ac.hitboxMagnitude = 55
                    end
                    ac:attack()
                end
            end
        end)
    end
end)()

Page3.Line()

Page3.Toggle({
    Title = "Auto Haki",
    Default = _G.Settings.Configs["Auto Haki"],
    callback = function(value)
        _G.Settings.Configs["Auto Haki"] = value
        SaveSettings()
    end,
})

-- Auto Haki system
task.spawn(function()
    while task.wait(1) do  -- Reduced frequency for better performance
        pcall(function()
            if _G.Settings.Configs["Auto Haki"] then
                if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
                end
            end
        end)
    end
end)

-- [Table Weapon]
Weapon = {
    "Melee",
    "Sword",
    "Fruit"
}

Page3.Line()

Page3.Dropdown({
    Title = "Select Weapon",
    Item = Weapon,
    callback = function(value)
        SelectWeapon = value
    end,
})

-- Weapon selection system with optimization
task.spawn(function()
    while task.wait(0.5) do  -- Reduced frequency for better performance
        pcall(function()
            if not SelectWeapon then SelectWeapon = "Melee" end
            
            local backpack = game.Players.LocalPlayer.Backpack
            if not backpack then return end
            
            -- More efficient weapon search
            local foundWeapon = false
            for _, v in pairs(backpack:GetChildren()) do
                if v:IsA("Tool") and v.ToolTip == (SelectWeapon == "Fruit" and "Blox Fruit" or SelectWeapon) then
                    _G.Settings.Configs["Select Weapon"] = v.Name
                    foundWeapon = true
                    break  -- Exit loop once found
                end
            end
            
            -- Fallback to Melee if nothing found
            if not foundWeapon and SelectWeapon ~= "Melee" then
                for _, v in pairs(backpack:GetChildren()) do
                    if v:IsA("Tool") and v.ToolTip == "Melee" then
                        _G.Settings.Configs["Select Weapon"] = v.Name
                        break
                    end
                end
            end
        end)
    end
end)

-- Character movement optimization
task.spawn(function()
    while task.wait(0.1) do  -- Better performance with task.wait
        pcall(function()
            if _G.AutoFarmLevelReal then
                local character = game.Players.LocalPlayer.Character
                if not character then return end
                
                local humanoid = character:FindFirstChild("Humanoid")
                local rootPart = character:FindFirstChild("HumanoidRootPart")
                
                if not humanoid or not rootPart then return end
                
                if syn then
                    -- Synapse X optimization
                    setfflag("HumanoidParallelRemoveNoPhysics", "False")
                    setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                    humanoid:ChangeState(11)
                    if humanoid.Sit == true then
                        humanoid.Sit = false
                    end
                else
                    -- Non-Synapse optimization
                    if humanoid.Sit == true then
                        humanoid.Sit = false
                    end
                    
                    if not rootPart:FindFirstChild("BodyVelocity1") then
                        local bodyVelocity = Instance.new("BodyVelocity")
                        bodyVelocity.Name = "BodyVelocity1"
                        bodyVelocity.Parent = rootPart
                        bodyVelocity.MaxForce = Vector3.new(10000, 10000, 10000)
                        bodyVelocity.Velocity = Vector3.new(0, 0, 0)
                    end
                    
                    -- Disable collisions for all parts
                    for _, v in pairs(character:GetDescendants()) do
                        if v:IsA("BasePart") then
                            v.CanCollide = false    
                        end
                    end
                end
            else
                -- Clean up when not farming
                local character = game.Players.LocalPlayer.Character
                if character and character:FindFirstChild("HumanoidRootPart") then
                    local bodyVelocity = character.HumanoidRootPart:FindFirstChild("BodyVelocity1")
                    if bodyVelocity then
                        bodyVelocity:Destroy()
                    end
                end
            end
        end)
    end
end)
