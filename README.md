-- Load Fluent and its dependencies
local Fluent = loadstring(game:HttpGet("https://github.com/ActualMasterOogway/Fluent-Renewed/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

-- Create the main window
local Window = Fluent:CreateWindow({
    Title = "Slash Hub [Muscle Legends] " .. Fluent.Version,
    SubTitle = "",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl,
    OnMinimize = function() -- Add the minimize functionality here
        Window:Minimize() -- Minimize the window when the minimize button is clicked
    end
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
    local torso = targetPlayer.Character and targetPlayer.Character:FindFirstChild("Torso")
    if torso then
        local rightHand = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("RightHand")
        if rightHand then
            torso.CFrame = rightHand.CFrame
        end
        torso.Transparency = 1
    end
end

-- Auto Kill Logic: Infinite teleportation of all players' torsos (except whitelisted)
ToggleAutoKill:OnChanged(function()
    local isAutoKillEnabled = ToggleAutoKill.Value
    local whitelistedPlayers = {}

    if WhitelistDropdown.Selected then
        for _, playerName in pairs(WhitelistDropdown.Selected) do
            table.insert(whitelistedPlayers, playerName)
        end
    end

    while isAutoKillEnabled do
        for _, player in pairs(Players:GetPlayers()) do
            if not table.find(whitelistedPlayers, player.Name) then
                teleportAndMakeInvisible(player)
            end
        end
        wait(0.1)
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

    local punchTool = backpack:FindFirstChild("Punch")

    if punchTool then
        if character and not character:FindFirstChild("Punch") then
            punchTool.Parent = character
        end

        if punchTool:FindFirstChild("Activate") then
            punchTool.Activate:Fire()
        end
    end
end

-- Auto Punch Logic: Infinite equip and use of the "Punch" tool
ToggleAutoPunch:OnChanged(function()
    local isAutoPunchEnabled = ToggleAutoPunch.Value

    while isAutoPunchEnabled do
        equipAndUsePunchTool()
        wait(0.1)
    end
end)

-- Fast Punch Logic
local ToggleFastPunch = Tabs.Killing:AddToggle("FastPunchToggle", {Title = "Fast Punch", Default = false})

ToggleFastPunch:OnChanged(function()
    local isFastPunchEnabled = ToggleFastPunch.Value
    local player = game.Players.LocalPlayer
    local punchTool = player.Backpack:FindFirstChild("Punch") or player.Character:FindFirstChild("Punch")
    
    if isFastPunchEnabled and punchTool and punchTool:FindFirstChild("attackTime") then
        punchTool.attackTime.Value = 0
    end
end)

