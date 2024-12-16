local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Slash Hub [Muscle Legends] " .. Fluent.Version,
    SubTitle = "",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl
})

-- Tabs
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "" }),
    AutoFarm = Window:AddTab({ Title = "AutoFarm", Icon = "Auto Farm" }),
    Killing = Window:AddTab({ Title = "Killing", Icon = "Auto Farm" })
}

-- WalkSpeed Slider
local WalkSpeedSlider = Tabs.Main:AddSlider("WalkSpeedSlider", {
    Title = "WalkSpeed",
    Description = "Adjust the player's walk speed",
    Default = 16,
    Min = 16,
    Max = 1000,
    Rounding = 1,
    Callback = function(Value)
        if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
        end
    end
})

-- JumpPower Slider
local JumpPowerSlider = Tabs.Main:AddSlider("JumpPowerSlider", {
    Title = "Jump Power",
    Description = "Adjust the player's jump power",
    Default = 40,
    Min = 40,
    Max = 1000,
    Rounding = 1,
    Callback = function(Value)
        if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") then
            game.Players.LocalPlayer.Character.Humanoid.JumpPower = Value
        end
    end
})

local Players = game:GetService("Players")

-- Auto Kill Toggle
local ToggleAutoKill = Tabs.Killing:AddToggle("AutoKillToggle", {Title = "Auto Kill", Default = false})

-- Kill Player Toggle
local ToggleKillPlayer = Tabs.Killing:AddToggle("KillPlayerToggle", {Title = "Kill Player", Default = false})

-- Whitelist Player Dropdown
local WhitelistDropdown = Tabs.Killing:AddDropdown("WhitelistPlayerDropdown", {
    Title = "Whitelist Player",
    Values = {},  -- This will be populated dynamically
    Multi = false,
    Default = 1,
})

-- Select Player Dropdown
local SelectPlayerDropdown = Tabs.Killing:AddDropdown("SelectPlayerDropdown", {
    Title = "Select Player",
    Values = {},  -- This will be populated dynamically
    Multi = false,
    Default = 1,
})

-- Function to update player lists in dropdowns
local function updatePlayerLists()
    local playerNames = {}
    for _, player in pairs(Players:GetPlayers()) do
        table.insert(playerNames, player.Name)
    end

    -- Update both dropdowns with the latest player list
    WhitelistDropdown:SetOptions(playerNames)
    SelectPlayerDropdown:SetOptions(playerNames)
end

-- Update the player lists every second
game:GetService("RunService").Heartbeat:Connect(function()
    updatePlayerLists()
end)

-- Function to teleport and make the torso invisible
local function teleportAndMakeInvisible(targetPlayer)
    -- Assuming you want to teleport the player's torso to your right hand
    local torso = targetPlayer.Character and targetPlayer.Character:FindFirstChild("Torso")
    if torso then
        -- Teleport torso to the player's right hand (assuming you have a reference to your right hand part)
        local rightHand = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("RightHand")
        if rightHand then
            torso.CFrame = rightHand.CFrame
        end
        -- Make torso invisible
        torso.Transparency = 1
    end
end

-- Auto Kill Logic: Infinite teleportation of all players' torsos (except whitelisted)
ToggleAutoKill:OnChanged(function()
    local isAutoKillEnabled = ToggleAutoKill.Value
    local whitelistedPlayers = {}

    -- Gather all whitelisted players from the dropdown
    if WhitelistDropdown.Selected then
        for _, playerName in pairs(WhitelistDropdown.Selected) do
            table.insert(whitelistedPlayers, playerName)
        end
    end

    -- Infinite teleportation of all players' torsos except whitelisted
    while isAutoKillEnabled do
        for _, player in pairs(Players:GetPlayers()) do
            -- Skip if the player is whitelisted
            if not table.find(whitelistedPlayers, player.Name) then
                teleportAndMakeInvisible(player)
            end
        end
        wait(0.1)  -- Adjust delay as necessary for performance
    end
end)

-- Kill Player Logic: Teleport and make the selected player's torso invisible
ToggleKillPlayer:OnChanged(function()
    local isKillPlayerEnabled = ToggleKillPlayer.Value
    local selectedPlayerName = SelectPlayerDropdown.Selected and SelectPlayerDropdown.Selected[1]

    if selectedPlayerName then
        local selectedPlayer = Players:FindFirstChild(selectedPlayerName)
        if selectedPlayer then
            if isKillPlayerEnabled then
                teleportAndMakeInvisible(selectedPlayer)
            end
        end
    end
end)

-- Initial update of player lists
updatePlayerLists()

-- Add a paragraph titled "Auto Punching"
Tabs.Killing:AddParagraph({
    Title = "Auto Punching",
    Content = "Enables automatic punching using the Punch tool."
})

-- Add a toggle called "Auto Punch"
local ToggleAutoPunch = Tabs.Killing:AddToggle("AutoPunchToggle", {Title = "Auto Punch", Default = false})

-- Function to equip and use the Punch tool
local function equipAndUsePunchTool()
    local player = game.Players.LocalPlayer
    local character = player.Character
    local backpack = player.Backpack

    -- Try to find the "Punch" tool in the player's Backpack
    local punchTool = backpack:FindFirstChild("Punch")

    if punchTool then
        -- Equip the Punch tool if it's not already equipped
        if character and not character:FindFirstChild("Punch") then
            punchTool.Parent = character  -- Equip the Punch tool to the character
        end

        -- Use the Punch tool (assuming it has an activation method like Fire)
        if punchTool:FindFirstChild("Activate") then
            punchTool.Activate:Fire()  -- Trigger the punch tool's activation
        end
    end
end

-- Auto Punch Logic: Infinite equip and use of the "Punch" tool
ToggleAutoPunch:OnChanged(function()
    local isAutoPunchEnabled = ToggleAutoPunch.Value

    -- Infinite loop to equip and use Punch tool when Auto Punch is enabled
    while isAutoPunchEnabled do
        equipAndUsePunchTool()
        wait(0.1)  -- Adjust delay to prevent too rapid execution (optional)
    end
end)

-- Auto Punch [No Animation] Toggle
local ToggleAutoPunchNoAnim = Tabs.Killing:AddToggle("AutoPunchNoAnimToggle", {Title = "Auto Punch [No Animation]", Default = false})

-- Fast Punch Toggle
local ToggleFastPunch = Tabs.Killing:AddToggle("FastPunchToggle", {Title = "Fast Punch", Default = false})

-- Auto Punch [No Animation] Logic
ToggleAutoPunchNoAnim:OnChanged(function()
    local isAutoPunchEnabled = ToggleAutoPunchNoAnim.Value
    local player = game.Players.LocalPlayer
    local playerName = player.Name
    local punchTool = player.Backpack:FindFirstChild("Punch") or game.Workspace:FindFirstChild(playerName):FindFirstChild("Punch")

    _G.autoPunchanim = true -- Global control variable

    -- Infinite loop while Auto Punch is enabled
    while _G.autoPunchanim do
        if isAutoPunchEnabled then
            if punchTool then
                -- Equip the Punch tool to the player's character if not already equipped
                if punchTool.Parent ~= game.Workspace:FindFirstChild(playerName) then
                    punchTool.Parent = game.Workspace:FindFirstChild(playerName)
                end
                
                -- Fire punch events for both right and left hand
                game.Players.LocalPlayer.muscleEvent:FireServer("punch", "rightHand")
                game.Players.LocalPlayer.muscleEvent:FireServer("punch", "leftHand")
                
                wait(0.1) -- Adjust the delay as needed for timing between punches
            else
                warn("Punch tool not found")
                _G.autoPunchanim = false -- Stop the loop if the tool is not found
            end
        else
            _G.autoPunchanim = false
        end
        wait() -- Prevent a busy wait loop
    end
end)

-- Fast Punch Logic
ToggleFastPunch:OnChanged(function()
    local isFastPunchEnabled = ToggleFastPunch.Value
    local player = game.Players.LocalPlayer
    local punchTool = player.Backpack:FindFirstChild("Punch") or player.Character:FindFirstChild("Punch")
    
    if isFastPunchEnabled and punchTool and punchTool:FindFirstChild("attackTime") then
        punchTool.attackTime.Value = 0 -- Set the attack time to 0 for fast punching
    end
end)
