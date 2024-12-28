-- Whitelist for specific usernames 
local whitelistedUsers = {
   "Sub2LeopardGod",
   "Mrbignewcoming3",
   "Hi_dorihi",  --whitelisted
    “EpicDeevv”,
    “EpicDeevvIV999”,
    “robloxlovejonathan2”,
}

-- Function to check if player is whitelisted
local function isWhitelisted(username)
   for _, whitelisted in ipairs(whitelistedUsers) do
       if username == whitelisted then
           return true
       end
   end
   return false
end

-- Get the local player's username
local player = game.Players.LocalPlayer
local username = player.Name

-- Kick the player if they are not whitelisted
if not isWhitelisted(username) then
   game.Players.LocalPlayer:Kick("Not WhiteListed L")
   return
else

--Main Script
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/memejames/elerium-v2-ui-library//main/Library", true))()


local window = library:AddWindow("KT4Mz Clan Private Script", {
    main_color = Color3.fromRGB(128,128,128), -- Color
    min_size = Vector2.new(420, 440), -- Size of the gui
    can_resize = false, -- true or false
})

local Maintab = window:AddTab("Main")

-- Anti Crash Button
Maintab:AddButton("Anti Crash", function()
    wait(0.5)
    local ba = Instance.new("ScreenGui")
    local ca = Instance.new("TextLabel")
    local da = Instance.new("Frame")
    local _b = Instance.new("TextLabel")
    local ab = Instance.new("TextLabel")

    ba.Parent = game.CoreGui
    ba.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

    ca.Parent = ba
    ca.Active = true
    ca.BackgroundColor3 = Color3.new(0.176471, 0.176471, 0.176471)
    ca.Draggable = true
    ca.Position = UDim2.new(0.698610067, 0, 0.098096624, 0)
    ca.Size = UDim2.new(0, 370, 0, 52)
    ca.Font = Enum.Font.SourceSansSemibold
    ca.Text = "Anti Afk"
    ca.TextColor3 = Color3.new(0, 1, 1)
    ca.TextSize = 22

    da.Parent = ca
    da.BackgroundColor3 = Color3.new(0.196078, 0.196078, 0.196078)
    da.Position = UDim2.new(0, 0, 1.0192306, 0)
    da.Size = UDim2.new(0, 370, 0, 107)

    _b.Parent = da
    _b.BackgroundColor3 = Color3.new(0.176471, 0.176471, 0.176471)
    _b.Position = UDim2.new(0, 0, 0.800455689, 0)
    _b.Size = UDim2.new(0, 370, 0, 21)
    _b.Font = Enum.Font.Arial
    _b.Text = "Made by luca#5432"
    _b.TextColor3 = Color3.new(0, 1, 1)
    _b.TextSize = 20

    ab.Parent = da
    ab.BackgroundColor3 = Color3.new(0.176471, 0.176471, 0.176471)
    ab.Position = UDim2.new(0, 0, 0.158377, 0)
    ab.Size = UDim2.new(0, 370, 0, 44)
    ab.Font = Enum.Font.ArialBold
    ab.Text = "Status: Active"
    ab.TextColor3 = Color3.new(0, 1, 1)
    ab.TextSize = 20

    local bb = game:GetService("VirtualUser")
    game:GetService("Players").LocalPlayer.Idled:Connect(function()
        bb:CaptureController()
        bb:ClickButton2(Vector2.new())
        ab.Text = "Roblox tried kicking you, but I didn’t let them!"  -- Fixed encoding issue
        wait(2)
        ab.Text = "Status: Active"
    end)
end)

-- Destroy Ad teleport Button
Maintab:AddButton("Destroy Ad teleport", function()
    local part = workspace:FindFirstChild("RobloxForwardPortals")
    if part then
        part:Destroy()
        print("Part 'RobloxForwardPortals' has been destroyed.")
    else
        print("Part 'RobloxForwardPortals' not found.")
    end
end)

-- Create folder "Islands Teleports"
local folder = Maintab:AddFolder("Islands Teleports")

-- Beach Teleport
folder:AddButton("Beach", function()
    if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-11, 5, -178)
    end
end)

-- Legends Teleport
folder:AddButton("Legends", function()
    if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(4603, 989, -3898)
    end
end)

-- Muscle Teleport
folder:AddButton("Muscle", function()
    if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-8626, 15, -5730)
    end
end)

-- Tiny Teleport
folder:AddButton("Tiny", function()
    if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-38, 5, 1884)
    end
end)

-- Secret Teleport
folder:AddButton("Secret", function()
    if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-2596, -1, 5738)
    end
end)

-- Inferno Teleport
folder:AddButton("Inferno", function()
    if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-6759, 5, -1285)
    end
end)

-- Frost Teleport
folder:AddButton("Frost", function()
    if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-2623, 5, -409)
    end
end)

-- Mythical Teleport
folder:AddButton("Mythical", function()
    if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2251, 5, 1073)
    end
end)

-- Rock Farming v1 Section
local folder2 = Maintab:AddFolder("Rock Farming v1")
folder2:AddLabel("Coming Soon")

-- Brawl Things
local folder3 = Maintab:AddFolder("Brawl")

-- God Mode Toggle
folder3:AddSwitch("God Mode (Brawl)", function(State)
    godModeToggle = State
    if godModeToggle then
        -- Repeat the joinBrawl event every 0.1 seconds to simulate God Mode
        task.spawn(function()
            while godModeToggle do
                local args = { [1] = "joinBrawl" }
                game:GetService("ReplicatedStorage"):WaitForChild("rEvents"):WaitForChild("brawlEvent"):FireServer(unpack(args))
                task.wait()  -- Repeat the event every 0 seconds
            end
        end)
    end
end)

-- Auto Join Brawl
folder3:AddSwitch("Auto Join Brawl", function(State)
    godModeToggle = State
    if godModeToggle then
        task.spawn(function()
            while godModeToggle do
                local args = { [1] = "joinBrawl" }
                game:GetService("ReplicatedStorage"):WaitForChild("rEvents"):WaitForChild("brawlEvent"):FireServer(unpack(args))
                task.wait(2)  -- Repeat the event every 2 seconds
            end
        end)
    end
end)



local Killtab = window:AddTab("Kill")
local AutoPunchToggle = false
local targetPlayerName = ""
local teleporting = false
local playerToSpyOn = nil
local godModeToggle = false
local autoEquipPunchToggle = false
local whitelist = {}  -- Table to store whitelisted player names
local punchEquipped = false  -- Variable to track whether the "Punch" tool is equipped or not
local currentKillPlayer = nil  -- Variable to store the player whose model is being 
local autoKillActive = false
local originalTransparency = {}  -- Table to store original transparency values
local originalCanCollide = {}  -- Table to store original CanCollide values

-- Create Whitelist [Player] Textbox
Killtab:AddTextBox("Whitelist [Player]", function(text)
    -- Add the player name to the whitelist
    if text ~= "" and game.Players:FindFirstChild(text) then
        whitelist[text] = true
        print(text .. " has been whitelisted.")
    else
        print("Invalid player name.")
    end
end)

-- Create Unwhitelist [Player] Textbox
Killtab:AddTextBox("Unwhitelist [Player]", function(text)
    -- Remove the player name from the whitelist
    if text ~= "" and whitelist[text] then
        whitelist[text] = nil
        print(text .. " has been unwhitelisted.")
    else
        print("Player not found in whitelist.")
    end
end)

local folder5 = Killtab:AddFolder("Choose the Auto Kill you want") -- Folder name should be descriptive

-- Auto Kill Toggle
folder5:AddSwitch("Auto Kill", function(State)
    autoKillActive = State  -- Toggle the state of autoKill

    -- If AutoKill is enabled, start the autoKill process
    if autoKillActive then
        local function autoKill()
            while autoKillActive do
                wait(0.1)  -- Wait to avoid performance issues

                -- Get the local player and their right hand
                local player = game.Players.LocalPlayer
                local character = player.Character
                local rightHand = character and character:FindFirstChild("RightHand")

                -- Ensure that the right hand exists
                if rightHand then
                    -- Iterate through all models in the Workspace
                    for _, obj in pairs(game.Workspace:GetChildren()) do
                        -- Check if the object is a model and if its parent is a player
                        if obj:IsA("Model") and game.Players:FindFirstChild(obj.Name) then
                            -- Check if the object is not the local player's character and is not whitelisted
                            if obj.Name ~= player.Name and not whitelist[obj.Name] then
                                -- Save the original transparency and CanCollide values if they haven't been saved already
                                if not originalTransparency[obj.Name] then
                                    originalTransparency[obj.Name] = {}
                                    originalCanCollide[obj.Name] = {}
                                    for _, part in pairs(obj:GetDescendants()) do
                                        if part:IsA("BasePart") then
                                            originalTransparency[obj.Name][part] = part.Transparency
                                            originalCanCollide[obj.Name][part] = part.CanCollide
                                        end
                                    end
                                end

                                -- Make the model invisible by setting transparency to 1 and disabling collisions
                                for _, part in pairs(obj:GetDescendants()) do
                                    if part:IsA("BasePart") then
                                        part.Transparency = 1
                                        part.CanCollide = false
                                    end
                                end

                                -- Teleport the model to the player's right hand
                                local humanoidRootPart = obj:FindFirstChild("HumanoidRootPart")
                                if humanoidRootPart then
                                    humanoidRootPart.CFrame = rightHand.CFrame
                                end
                            end
                        end
                    end
                end
            end
        end

        -- Start the autoKill loop in a coroutine so it runs independently
        coroutine.wrap(autoKill)()
    else
        -- If AutoKill is turned off, reset transparency and collisions
        for _, obj in pairs(game.Workspace:GetChildren()) do
            if obj:IsA("Model") and game.Players:FindFirstChild(obj.Name) and not whitelist[obj.Name] then
                -- Restore original transparency and CanCollide values
                if originalTransparency[obj.Name] then
                    for part, transparency in pairs(originalTransparency[obj.Name]) do
                        part.Transparency = transparency
                        part.CanCollide = originalCanCollide[obj.Name][part]
                    end
                end
            end
        end
        -- Clear the saved data for next time
        originalTransparency = {}
        originalCanCollide = {}
    end
end)


-- Auto Kill Aura v2 Toggle
folder5:AddSwitch("Auto Kill Aura v2", function(State)
    autoKillEnabled = State
end)

game:GetService('RunService').RenderStepped:Connect(function()
    if autoKillEnabled then
        for _, player in pairs(game:GetService("Players"):GetPlayers()) do
            if player.Name ~= game.Players.LocalPlayer.Name then
                if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    local rootPart = player.Character.HumanoidRootPart
                    -- Modify the root part properties for players that are not the local player
                    rootPart.Size = Vector3.new(hitboxSize, hitboxSize, hitboxSize)  -- Set hitbox size to 600
                    rootPart.Transparency = 1  -- Make the red thing invisible
                    rootPart.Material = Enum.Material.Neon
                    rootPart.CanCollide = false
                end
            end
        end

        -- Modify the local player's HumanoidRootPart properties (optional)
        local localPlayer = game.Players.LocalPlayer
        if localPlayer.Character and localPlayer.Character:FindFirstChild("HumanoidRootPart") then
            local rootPart = localPlayer.Character.HumanoidRootPart
            rootPart.Transparency = 1  -- Make the local player's root part invisible
            rootPart.CanCollide = false
        end
    end
end)

-- Optional function to reset the player's character
local function resetPlayer()
    local player = game.Players.LocalPlayer
    if player.Character then
        player.Character:BreakJoints()  -- Break joints to reset the character (if necessary)
    end
end

-- Call the function to reset the character (if required by the script's logic)
resetPlayer()


-- Create Equip Punch Toggle
Killtab:AddSwitch("Equip Punch", function(State)
    punchEquipped = State  -- Toggle whether the "Punch" tool should be equipped or not

    -- If Equip Punch is enabled, continuously equip the "Punch" tool
    local player = game.Players.LocalPlayer
    local character = player.Character
    local backpack = player.Backpack

    if punchEquipped then
        -- Equip "Punch" tool continuously
        local punchTool = character:FindFirstChild("Punch") or backpack:FindFirstChild("Punch")
        if punchTool then
            -- Equip the tool if it's found in the character or backpack
            backpack:EquipTool(punchTool)
        end
    else
        -- If Equip Punch is off, stop equipping the "Punch" tool
        local punchTool = backpack:FindFirstChild("Punch")
        if punchTool then
            -- Unequip the "Punch" tool
            punchTool.Parent = character
        end
    end
end)


-- Create Kill Player [Name] Textbox
Killtab:AddTextBox("Kill Player [Name]", function(text)
    -- Store the player's name to be used for teleportation
    currentKillPlayer = text
end)

-- Create Start Kill Button
Killtab:AddButton("Start Kill", function()
    if currentKillPlayer then
        local player = game.Players:FindFirstChild(currentKillPlayer)
        if player then
            -- Start teleporting the specified player's model
            local function startTeleporting()
                local character = player.Character
                local rightHand = game.Players.LocalPlayer.Character:FindFirstChild("RightHand")

                -- Check if the player's character and right hand exist
                if character and rightHand then
                    while currentKillPlayer == player.Name do
                        wait(0.1)  -- Wait to avoid performance issues
                        -- Check if the player is not whitelisted
                        if not whitelist[player.Name] then
                            -- Teleport the model to the player's right hand
                            local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
                            if humanoidRootPart then
                                humanoidRootPart.CFrame = rightHand.CFrame
                            end
                        end
                    end
                end
            end

            -- Start teleporting the player's model in a coroutine
            coroutine.wrap(startTeleporting)()
        else
            print("Player not found.")
        end
    else
        print("No player name specified.")
    end
end)

-- Create Stop Kill Button
Killtab:AddButton("Stop Kill", function()
    if currentKillPlayer then
        local player = game.Players:FindFirstChild(currentKillPlayer)
        if player then
            -- Stop teleporting the specified player's model
            print("Stopped teleporting " .. currentKillPlayer)
            currentKillPlayer = nil  -- Stop teleporting
        else
            print("Player not found.")
        end
    else
        print("No player name specified.")
    end
end)

-- Speed Punch (Optional Speed Increase for Punch)
Killtab:AddButton("Speed Punch", function()
    local player = game.Players.LocalPlayer
    local punch = player.Backpack:FindFirstChild("Punch") or player.Character:FindFirstChild("Punch")
    if punch and punch:FindFirstChild("attackTime") then
        punch.attackTime.Value = 0
    end
end)

-- Auto Punch Toggle
Killtab:AddSwitch("Auto Punch", function(State)
    AutoPunchToggle = State
    if AutoPunchToggle then
        task.spawn(function()
            while AutoPunchToggle do
                local player = game.Players.LocalPlayer
                local tool = player.Backpack:FindFirstChild("Punch") or player.Character:FindFirstChild("Punch")
                if tool and tool.Parent ~= player.Character then
                    tool.Parent = player.Character
                end
                if tool then
                    tool:Activate()
                end
                task.wait(0.01)  -- Trigger every 0.01 seconds
            end
        end)
    end
end)

Killtab:AddSwitch("Auto Punch [No Animation]", function(state)
    if state then
        local player = game.Players.LocalPlayer
        local playerName = player.Name
        local punchTool =
            player.Backpack:FindFirstChild("Punch") or
            game.Workspace:FindFirstChild(playerName):FindFirstChild("Punch")
        
        _G.autoPunchanim = true -- Global control variable

        while _G.autoPunchanim do
            if punchTool then
                if punchTool.Parent ~= game.Workspace:FindFirstChild(playerName) then
                    punchTool.Parent = game.Workspace:FindFirstChild(playerName) -- Equip the tool
                end
                
                -- Fire punch events for both right and left hand
                game.Players.LocalPlayer.muscleEvent:FireServer("punch", "rightHand")
                game.Players.LocalPlayer.muscleEvent:FireServer("punch", "leftHand")
                
                wait() -- Adjust the delay as needed for timing between punches
            else
                warn("Punch tool not found")
                _G.autoPunchanim = false -- Optional: Stop the loop if tool is not found
            end
        end
    else
        _G.autoPunchanim = false
    end
end)

Killtab:AddLabel("Spy")

-- Textbox for Spy target player
Killtab:AddTextBox("Spy on Player (Name)", function(text)
    playerToSpyOn = text
end)

-- Spy Toggle
Killtab:AddSwitch("Spy", function(State)
    if State then
        local player = game.Players.LocalPlayer
        local spying = true -- Variable to control the spying state
        task.spawn(function()
            while spying do
                task.wait(0.1)  -- Check every 0.1 seconds
                if playerToSpyOn then
                    local targetPlayer = game.Players:FindFirstChild(playerToSpyOn)
                    if targetPlayer and targetPlayer.Character then
                        -- Teleport the LocalPlayer to the target player's head (or wherever you want)
                        local targetHead = targetPlayer.Character:FindFirstChild("Head")
                        if targetHead then
                            player.Character:MoveTo(targetHead.Position)
                        end
                    end
                end
            end
        end)
    else
        -- Stop spying when toggle is turned off
        spying = false
    end
end)









local rebirthAmount = 0
local currentRebirths = 0
local autoRebirthEnabled = false

-- Create a function for auto rebirth
local function autoRebirth()
    spawn(function()
        while autoRebirthEnabled do
            local rebirthevent = game.ReplicatedStorage.rEvents:FindFirstChild("rebirthRemote")
            if rebirthevent then
                if rebirthAmount == 0 or currentRebirths < rebirthAmount then
                    rebirthevent:FireServer()
                    currentRebirths = currentRebirths + 1
                else
                    autoRebirthEnabled = false
                    print("Reached the desired rebirth amount.")
                end
            end
            wait(0.1)
        end
    end)
end

-- Assuming 'window' is the UI library you're using, and it has an AddTab method
local RebirthTab = window:AddTab("Rebirth")

-- Add a switch for auto rebirth
RebirthTab:AddSwitch("Auto Rebirth", {
    Default = false,
    Callback = function(state)
        autoRebirthEnabled = state
        if state then
            autoRebirth()
        end
    end
})



-- Add a textbox to set the rebirth amount
RebirthTab:AddTextBox("Select Rebirth Amount", function(text)
    local inputNumber = tonumber(text)
    if inputNumber and inputNumber >= 0 then
        rebirthAmount = inputNumber
        currentRebirths = 0
        print("Rebirth amount set to:", rebirthAmount)
    else
        print("Invalid input. Please enter a positive number.")
    end
end)


local AutoFarmTab = window:AddTab("Auto Farm")
local AutoWeightToggle = false
local AutoPushupsToggle = false
local SitupsToggle = false
local MuscleKingFarmToggle = false

-- Helper functions for auto actions
local function AutoWeight()
    while AutoWeightToggle do
        local player = game.Players.LocalPlayer
        local weightTool = player.Backpack:FindFirstChild("Weight") or player.Character:FindFirstChild("Weight")
        if weightTool then
            player.Character.Humanoid:EquipTool(weightTool)
            weightTool:Activate()
        end
        wait(0.1)
    end
end

local function AutoPushups()
    while AutoPushupsToggle do
        local player = game.Players.LocalPlayer
        local pushupTool = player.Backpack:FindFirstChild("Pushup") or player.Character:FindFirstChild("Pushup")
        if pushupTool then
            player.Character.Humanoid:EquipTool(pushupTool)
            pushupTool:Activate()
        end
        wait(0.1)
    end
end

local function AutoSitups()
    while SitupsToggle do
        local player = game.Players.LocalPlayer
        local situpTool = player.Backpack:FindFirstChild("Situp") or player.Character:FindFirstChild("Situp")
        if situpTool then
            player.Character.Humanoid:EquipTool(situpTool)
            situpTool:Activate()
        end
        wait(0.1)
    end
end

local function MuscleKingFarm()
    while MuscleKingFarmToggle do
        local player = game.Players.LocalPlayer
        local muscleKingTool = player.Backpack:FindFirstChild("MuscleKing") or player.Character:FindFirstChild("MuscleKing")
        if muscleKingTool then
            player.Character.Humanoid:EquipTool(muscleKingTool)
            muscleKingTool:Activate()
        end
        wait(0.1)
    end
end

AutoFarmTab:AddSwitch("Auto Weight", function(State)
    AutoWeightToggle = State
    if AutoWeightToggle then
        AutoWeight()
    end
end)

AutoFarmTab:AddSwitch("Auto Pushups", function(value)
    AutoPushupsToggle = value
    if AutoPushupsToggle then
        AutoPushups()
    end
end)

AutoFarmTab:AddSwitch("Situps", function(value)
    SitupsToggle = value
    if SitupsToggle then
        AutoSitups()
    end
end)

AutoFarmTab:AddSwitch("Muscle King Farm", function(value)
    MuscleKingFarmToggle = value
    if MuscleKingFarmToggle then
        MuscleKingFarm()
    end
end)



-- View Stats Tab
local ViewStatsTab = window:AddTab("ViewStats")

local playerData = {}
local currentSelectedPlayer = nil
local notFoundLabel = nil
local selectedPlayerName = nil

-- Helper function to abbreviate large numbers
local function abbreviateNumber(value)
    if value >= 1e15 then
        return string.format("%.1fQa", value / 1e15)
    elseif value >= 1e12 then
        return string.format("%.1fT", value / 1e12)
    elseif value >= 1e9 then
        return string.format("%.1fB", value / 1e9)
    elseif value >= 1e6 then
        return string.format("%.1fM", value / 1e6)
    elseif value >= 1e3 then
        return string.format("%.1fK", value / 1e3)
    else
        return tostring(value)
    end
end

-- Function to create labels for the selected player's stats
local function createPlayerLabels(player)
    local playerName = player.Name
    local leaderstats = player:FindFirstChild("leaderstats")
    local equippedPets = player:FindFirstChild("equippedPets")
    local ownedGamepasses = player:FindFirstChild("ownedGamepasses")

    -- Create labels for stats
    local labels = {
        StrengthLabel = ViewStatsTab:AddLabel("Strength: " .. abbreviateNumber(leaderstats.Strength.Value or 0)),
        DurabilityLabel = ViewStatsTab:AddLabel("Durability: " .. abbreviateNumber(player.Durability.Value or 0)),
        KillsLabel = ViewStatsTab:AddLabel("Kills: " .. abbreviateNumber(leaderstats.Kills.Value or 0)),
        BrawlsLabel = ViewStatsTab:AddLabel("Brawls: " .. abbreviateNumber(leaderstats.Brawls.Value or 0)),
        AgilityLabel = ViewStatsTab:AddLabel("Agility: " .. abbreviateNumber(player.Agility.Value or 0)),
        EvilKarmaLabel = ViewStatsTab:AddLabel("evilKarma: " .. abbreviateNumber(player.evilKarma.Value or 0)),
        GoodKarmaLabel = ViewStatsTab:AddLabel("goodKarma: " .. abbreviateNumber(player.goodKarma.Value or 0)),
        MapLabel = ViewStatsTab:AddLabel("Map: " .. (player.currentMap.Value or "N/A")),
        KingTimeLabel = ViewStatsTab:AddLabel("KingTime: " .. abbreviateNumber(player.muscleKingTime.Value or 0)),
        PremiumLabel = ViewStatsTab:AddLabel("Premium: " .. (player.MembershipType == Enum.MembershipType.Premium and "true" or "false")),
    }

    -- Add pet labels
    for i = 1, 5 do
        local petValue = equippedPets:FindFirstChild("pet" .. i) and equippedPets["pet" .. i].Value or "N/A"
        labels["Pet" .. i .. "Label"] = ViewStatsTab:AddLabel("Pet" .. i .. ": " .. tostring(petValue))
    end

    -- Add owned gamepasses
    local gamepassList = {}
    if ownedGamepasses then
        for _, gamepass in ipairs(ownedGamepasses:GetChildren()) do
            table.insert(gamepassList, gamepass.Name)
        end
    end

    local gamepassesText = #gamepassList > 0 and table.concat(gamepassList, ", ") or "N/A"
    labels.GamepassesLabel = ViewStatsTab:AddLabel("ownedGamepasses: " .. gamepassesText)

    playerData[playerName] = labels

    -- Connect value change events to update the labels
    leaderstats.Kills.Changed:Connect(function()
        labels.KillsLabel.Text = "Kills: " .. abbreviateNumber(leaderstats.Kills.Value or 0)
    end)

    leaderstats.Strength.Changed:Connect(function()
        labels.StrengthLabel.Text = "Strength: " .. abbreviateNumber(leaderstats.Strength.Value or 0)
    end)

    leaderstats.Brawls.Changed:Connect(function()
        labels.BrawlsLabel.Text = "Brawls: " .. abbreviateNumber(leaderstats.Brawls.Value or 0)
    end)

    player.Durability.Changed:Connect(function()
        labels.DurabilityLabel.Text = "Durability: " .. abbreviateNumber(player.Durability.Value or 0)
    end)

    player.Agility.Changed:Connect(function()
        labels.AgilityLabel.Text = "Agility: " .. abbreviateNumber(player.Agility.Value or 0)
    end)

    player.evilKarma.Changed:Connect(function()
        labels.EvilKarmaLabel.Text = "evilKarma: " .. abbreviateNumber(player.evilKarma.Value or 0)
    end)

    player.goodKarma.Changed:Connect(function()
        labels.GoodKarmaLabel.Text = "goodKarma: " .. abbreviateNumber(player.goodKarma.Value or 0)
    end)
end

-- Function to remove player labels (cleanup)
local function removePlayerLabels(playerName)
    if playerData[playerName] then
        for _, label in pairs(playerData[playerName]) do
            label:Remove()
        end
        playerData[playerName] = nil
    end
end

-- Adding a textbox for player name input
local textbox = ViewStatsTab:AddTextBox("Player Name", function(playerName)
    selectedPlayerName = playerName
    if notFoundLabel then
        notFoundLabel:Remove()
        notFoundLabel = nil
    end

    local player = game.Players:FindFirstChild(playerName)
    if player then
        if currentSelectedPlayer then
            removePlayerLabels(currentSelectedPlayer)
        end
        createPlayerLabels(player)
        currentSelectedPlayer = playerName
    else
        notFoundLabel = ViewStatsTab:AddLabel("Player not found!")
    end
end)

--The credit tab because yes
local Credittab = window:AddTab("Credit")  -- Adding the "Credit" tab

-- Adding the labels
Credittab:AddLabel("Script Made By Adopt And EpicDeevv")
Credittab:AddLabel("Discord Server: https://discord.gg/ZgDYgKa2")

-- Show the window
window:Show()
