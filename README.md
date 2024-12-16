local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = library:CreateWindow("Slash Hub [Muscle Legends]")

-- Main Tab
local MainTab = Window:CreateTab("Main")
MainTab:CreateLabel("Features", {TextSize = 18, TextColor = Color3.fromRGB(255, 255, 255)})

-- Adding a House Icon to Main Tab
MainTab:CreateIcon("House", "rbxassetid://1234567890", function() -- Replace the asset id with an actual icon ID if available
    print("House Icon Clicked")
end)

-- WalkSpeed Slider
MainTab:CreateSlider("WalkSpeed", {Min = 16, Max = 1000, Default = 16, Color = Color3.fromRGB(0, 255, 0), Increment = 1, ValueName = "WalkSpeed"}, function(value)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
end)

-- JumpPower Slider
MainTab:CreateSlider("JumpPower", {Min = 16, Max = 1000, Default = 50, Color = Color3.fromRGB(0, 255, 0), Increment = 1, ValueName = "JumpPower"}, function(value)
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
end)

-- Infinite Jump Toggle
MainTab:CreateToggle("Infinite Jump", {Default = false, Text = "Enable Infinite Jump", Callback = function(state)
    local humanoid = game.Players.LocalPlayer.Character:WaitForChild("Humanoid")
    
    if state then
        humanoid.Changed:Connect(function()
            if humanoid:GetState() == Enum.HumanoidStateType.Physics then
                humanoid:ChangeState(Enum.HumanoidStateType.Physics)
                humanoid:Move(Vector3.new(0, 50, 0))
            end
        end)
    end
end})

-- Max Zoom Slider
MainTab:CreateSlider("Max Zoom", {Min = 0, Max = 1000, Default = 50, Color = Color3.fromRGB(0, 255, 0), Increment = 1, ValueName = "Max Zoom"}, function(value)
    game:GetService("Workspace").CurrentCamera.FieldOfView = value
end)

-- Auto Farm Tab
local AutoFarmTab = Window:CreateTab("Auto Farm")
AutoFarmTab:CreateLabel("Farming", {TextSize = 18, TextColor = Color3.fromRGB(255, 255, 255)})

-- Auto Weight
AutoFarmTab:CreateToggle("Auto Weight", {Default = false, Text = "Enable Auto Weight", Callback = function(state)
    local weightTool = game.Players.LocalPlayer.Backpack:FindFirstChild("Weight")
    
    if state then
        while state do
            if weightTool then
                game.Players.LocalPlayer.Character.Humanoid:EquipTool(weightTool)
                weightTool:Activate()
            end
            wait(0.5)
        end
    end
end})

-- Auto Pushups
AutoFarmTab:CreateToggle("Auto Pushups", {Default = false, Text = "Enable Auto Pushups", Callback = function(state)
    local pushupsTool = game.Players.LocalPlayer.Backpack:FindFirstChild("Pushups")
    
    if state then
        while state do
            if pushupsTool then
                game.Players.LocalPlayer.Character.Humanoid:EquipTool(pushupsTool)
                pushupsTool:Activate()
            end
            wait(0.5)
        end
    end
end})

-- Auto Situps
AutoFarmTab:CreateToggle("Auto Situps", {Default = false, Text = "Enable Auto Situps", Callback = function(state)
    local situpsTool = game.Players.LocalPlayer.Backpack:FindFirstChild("Situps")
    
    if state then
        while state do
            if situpsTool then
                game.Players.LocalPlayer.Character.Humanoid:EquipTool(situpsTool)
                situpsTool:Activate()
            end
            wait(0.5)
        end
    end
end})

-- Auto Handsstands
AutoFarmTab:CreateToggle("Auto Handsstands", {Default = false, Text = "Enable Auto Handsstands", Callback = function(state)
    local handsstandsTool = game.Players.LocalPlayer.Backpack:FindFirstChild("Handsstands")
    
    if state then
        while state do
            if handsstandsTool then
                game.Players.LocalPlayer.Character.Humanoid:EquipTool(handsstandsTool)
                handsstandsTool:Activate()
            end
            wait(0.5)
        end
    end
end})

-- Killing Tab
local KillingTab = Window:CreateTab("Killing")
KillingTab:CreateLabel("Kill Chosen Players", {TextSize = 18, TextColor = Color3.fromRGB(255, 255, 255)})

-- Auto Kill Toggle
KillingTab:CreateToggle("Auto Kill", {Default = false, Text = "Enable Auto Kill", Callback = function(state)
    local playerList = game.Players:GetPlayers()
    local localPlayer = game.Players.LocalPlayer
    
    while state do
        for _, player in pairs(playerList) do
            if player ~= localPlayer then
                local char = player.Character
                if char and char:FindFirstChild("HumanoidRootPart") then
                    char.HumanoidRootPart.CFrame = localPlayer.Character.RightHand.CFrame
                    char:FindFirstChild("Humanoid").HipWidth = 0
                    char:FindFirstChild("Humanoid").HipHeight = 0
                    char:FindFirstChild("HumanoidRootPart").Transparency = 1
                    for _, part in pairs(char:GetChildren()) do
                        if part:IsA("BasePart") then
                            part.LocalTransparencyModifier = 1
                        end
                    end
                end
            end
        end
        wait(0.5)
    end
end})

-- Whitelist Players Dropdown
local whitelist = {}
KillingTab:CreateDropdown("Whitelist Players", {Options = game.Players:GetPlayers(), MultiSelect = true}, function(selectedPlayers)
    whitelist = selectedPlayers
end)

-- Select Players Dropdown
KillingTab:CreateDropdown("Select Players", {Options = game.Players:GetPlayers(), MultiSelect = true}, function(selectedPlayers)
    local killPlayerList = selectedPlayers
    
    -- Kill Players Toggle
    KillingTab:CreateToggle("Kill Players", {Default = false, Text = "Enable Kill Players", Callback = function(state)
        local localPlayer = game.Players.LocalPlayer
        
        while state do
            for _, playerName in pairs(killPlayerList) do
                local player = game.Players:FindFirstChild(playerName)
                if player and player.Character then
                    if not table.find(whitelist, player.Name) then
                        local char = player.Character
                        if char and char:FindFirstChild("HumanoidRootPart") then
                            char.HumanoidRootPart.CFrame = localPlayer.Character.RightHand.CFrame
                            char:FindFirstChild("Humanoid").HipWidth = 0
                            char:FindFirstChild("Humanoid").HipHeight = 0
                            char:FindFirstChild("HumanoidRootPart").Transparency = 1
                            for _, part in pairs(char:GetChildren()) do
                                if part:IsA("BasePart") then
                                    part.LocalTransparencyModifier = 1
                                end
                            end
                        end
                    end
                end
            end
            wait(0.5)
        end
    end})
end)
