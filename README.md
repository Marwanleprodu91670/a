local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Slash Hub " .. Fluent.Version,
    SubTitle = "",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Aqua",
    MinimizeKey = Enum.KeyCode.LeftControl -- Used when there's no MinimizeKeybind
})

-- Fluent provides Lucide Icons, they are optional
local Tabs = {
    Home = Window:AddTab({ Title = "Home", Icon = "" }),
    AutoFarm = Window:AddTab({ Title = "AutoFarm", Icon = "" }),
    Killing = Window:AddTab({ Title = "Killing", Icon = "" })
}

-- Home Tab Code (Same as before)
local HomeTab = Tabs.Home
local Section = HomeTab:AddSection("Local player:")

HomeTab:AddSlider({
    Title = "WalkSpeed",
    Min = 16,
    Max = 1000,
    Default = 16,
    Callback = function(value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
    end
})

HomeTab:AddSlider({
    Title = "JumpPower",
    Min = 50,
    Max = 1000,
    Default = 50,
    Callback = function(value)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
    end
})

HomeTab:AddToggle({
    Title = "Infinite Jumps",
    Default = false,
    Callback = function(state)
        local player = game.Players.LocalPlayer
        local humanoid = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.Changed:Connect(function()
                if humanoid:GetState() == Enum.HumanoidStateType.Physics then
                    humanoid:ChangeState(Enum.HumanoidStateType.Seated)
                end
            end)
            humanoid.Jumping = state
        end
    end
})

-- Killing Tab Code
local KillingTab = Tabs.Killing

local whitelistPlayer = nil
local playersInServer = {}
local allPlayers = game.Players:GetPlayers()

-- Populate the list of players in the server
for _, player in ipairs(allPlayers) do
    table.insert(playersInServer, player.Name)
end

-- Whitelist Player Section
local KillingSection1 = KillingTab:AddSection("Whitelist A Player")

KillingTab:AddDropdown({
    Title = "Select Player to Whitelist",
    Options = playersInServer,
    Default = "",
    Callback = function(selectedPlayer)
        whitelistPlayer = selectedPlayer
    end
})

-- Auto Kill Section
local KillingSection2 = KillingTab:AddSection("Kill Farming")

local function teleportLegToRightHand(player)
    local character = player.Character
    if character and character:FindFirstChild("RightHand") then
        local leg = character:FindFirstChild("LeftLeg") or character:FindFirstChild("RightLeg")
        if leg then
            leg.CFrame = game.Players.LocalPlayer.Character.RightHand.CFrame
            leg.Transparency = 1
        end
    end
end

KillingTab:AddToggle({
    Title = "Auto Kill",
    Default = false,
    Callback = function(state)
        while state do
            for _, player in ipairs(game.Players:GetPlayers()) do
                if player.Name ~= whitelistPlayer then
                    teleportLegToRightHand(player)
                end
            end
            wait(0.1)  -- Adjust this delay as needed
        end
    end
})

-- Target Player Section
local KillingSection3 = KillingTab:AddSection("Target Player")

KillingTab:AddDropdown({
    Title = "Select Player",
    Options = playersInServer,
    Default = "",
    Callback = function(selectedPlayer)
        targetPlayer = game.Players:FindFirstChild(selectedPlayer)
    end
})

KillingTab:AddToggle({
    Title = "Kill Players",
    Default = false,
    Callback = function(state)
        while state do
            if targetPlayer then
                teleportLegToRightHand(targetPlayer)
            end
            wait(0.1)  -- Adjust this delay as needed
        end
    end
})

-- Spying Section
local KillingSection4 = KillingTab:AddSection("Spying")

local function spyOnPlayer(selectedPlayer)
    local player = game.Players:FindFirstChild(selectedPlayer)
    if player then
        local camera = game.Workspace.CurrentCamera
        camera.CameraSubject = player.Character.Humanoid
        camera.CameraType = Enum.CameraType.Custom
    end
end

KillingTab:AddToggle({
    Title = "Spy on Player",
    Default = false,
    Callback = function(state)
        while state do
            if targetPlayer then
                spyOnPlayer(targetPlayer.Name)
            end
            wait(0.1)  -- Adjust this delay as needed
        end
    end
})

-- Auto Punching Section (New)
local AutoPunchSection = KillingTab:AddSection("Auto Punching")

-- Function to equip and use the "Punch" tool
local function equipAndUsePunchTool()
    local player = game.Players.LocalPlayer
    local character = player.Character
    if character then
        local punchTool = character:FindFirstChild("Punch")
        if punchTool then
            punchTool.Parent = character
            punchTool:Activate()
        end
    end
end

-- Auto Punch Toggle
KillingTab:AddToggle({
    Title = "Auto Punch",
    Default = false,
    Callback = function(state)
        while state do
            equipAndUsePunchTool()
            wait(0.1)  -- Adjust this delay as needed
        end
    end
})

-- Update playersInServer when new players join or leave
game.Players.PlayerAdded:Connect(function(player)
    table.insert(playersInServer, player.Name)
end)

game.Players.PlayerRemoving:Connect(function(player)
    for i, name in ipairs(playersInServer) do
        if name == player.Name then
            table.remove(playersInServer, i)
            break
        end
    end
end)
