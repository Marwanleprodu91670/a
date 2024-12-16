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

-- Auto Farm Toggles (Already defined above)
-- Skipping these as they are unchanged in the updated code

-- Auto Kill Toggle
local AutoKillToggle = Tabs.Killing:AddToggle("AutoKillToggle", {Title = "Auto Kill", Default = false })

-- Whitelist Dropdown
local WhitelistPlayers = {}
local WhitelistPlayerDropdown = Tabs.Killing:AddDropdown("WhitelistPlayerDropdown", {
    Title = "Whitelist Player",
    Values = {},
    Multi = true,
    Default = {}
})

-- Kill Player Dropdown
local KillPlayerDropdown = Tabs.Killing:AddDropdown("KillPlayerDropdown", {
    Title = "Choose Player to Kill",
    Values = {},
    Multi = false,
    Default = {}
})

local KillPlayerToggle = Tabs.Killing:AddToggle("KillPlayerToggle", {Title = "Kill Player", Default = false })

-- Function to equip and use a tool continuously
local function EquipAndUseTool(toolName)
    local player = game.Players.LocalPlayer
    local character = player.Character
    if character then
        local tool = character:FindFirstChild(toolName)
        if tool then
            -- Equip the tool if not already equipped
            if not character:FindFirstChild(toolName) then
                tool.Parent = character
            end
            -- Use the tool continuously by simulating a click
            while true do
                if character and character:FindFirstChild(toolName) then
                    tool:Activate()
                end
                wait(0.1) -- Use a short wait to avoid too many activations per frame
            end
        end
    end
end

-- Auto Kill Toggle Action
AutoKillToggle:OnChanged(function(State)
    if State then
        -- Create grey part 10,000 studs up as a "floor"
        local floor = Instance.new("Part")
        floor.Size = Vector3.new(100, 1, 100) -- Size for the "floor"
        floor.Position = Vector3.new(0, 10000, 0) -- Position it 10,000 studs up
        floor.Anchored = true
        floor.Color = Color3.fromRGB(169, 169, 169) -- Grey color
        floor.Parent = game.Workspace
        
        -- Teleport the player to the floor
        local character = game.Players.LocalPlayer.Character
        if character then
            character:MoveTo(floor.Position + Vector3.new(0, 5, 0)) -- Move slightly above the floor
        end
        
        -- Equip and use the "Punch" tool continuously
        spawn(function()
            EquipAndUseTool("Punch")
        end)

        -- Teleport all players' heads to the player's right hand (except whitelist players)
        spawn(function()
            while AutoKillToggle.Value do
                for _, player in pairs(game.Players:GetPlayers()) do
                    if player ~= game.Players.LocalPlayer and not table.find(WhitelistPlayers, player.Name) then
                        local character = player.Character
                        if character and character:FindFirstChild("Head") then
                            local head = character.Head
                            local rightHand = game.Players.LocalPlayer.Character:FindFirstChild("RightHand")
                            if rightHand then
                                head.CFrame = rightHand.CFrame
                            end
                        end
                    end
                end
                wait(1) -- Update every second
            end
        end)
    else
        -- Logic to stop Auto Kill (you can handle removal of floor or cleanup here if necessary)
    end
end)

-- Whitelist Update Function
local function UpdateWhitelist()
    local playerNames = {}
    for _, player in pairs(game.Players:GetPlayers()) do
        table.insert(playerNames, player.Name)
    end
    WhitelistPlayerDropdown:SetValues(playerNames)
end

-- Kill Player Dropdown Update
local function UpdateKillPlayerDropdown()
    local playerNames = {}
    for _, player in pairs(game.Players:GetPlayers()) do
        table.insert(playerNames, player.Name)
    end
    KillPlayerDropdown:SetValues(playerNames)
end

-- Call the functions to update dropdowns every second
spawn(function()
    while true do
        UpdateWhitelist()
        UpdateKillPlayerDropdown()
        wait(1) -- Update every second
    end
end)

-- Kill Player Toggle Action
KillPlayerToggle:OnChanged(function(State)
    local selectedPlayerName = KillPlayerDropdown.SelectedValue
    if State and selectedPlayerName then
        -- Create grey part 10,000 studs up as a "floor"
        local floor = Instance.new("Part")
        floor.Size = Vector3.new(100, 1, 100) -- Size for the "floor"
        floor.Position = Vector3.new(0, 10000, 0) -- Position it 10,000 studs up
        floor.Anchored = true
        floor.Color = Color3.fromRGB(169, 169, 169) -- Grey color
        floor.Parent = game.Workspace
        
        -- Teleport the player to the floor
        local character = game.Players.LocalPlayer.Character
        if character then
            character:MoveTo(floor.Position + Vector3.new(0, 5, 0)) -- Move slightly above the floor
        end
        
        -- Equip and use the "Punch" tool continuously
        spawn(function()
            EquipAndUseTool("Punch")
        end)

        -- Teleport the selected player's head to the player's right hand
        spawn(function()
            while KillPlayerToggle.Value do
                local player = game.Players:FindFirstChild(selectedPlayerName)
                if player and player.Character then
                    local head = player.Character:FindFirstChild("Head")
                    local rightHand = game.Players.LocalPlayer.Character:FindFirstChild("RightHand")
                    if head and rightHand then
                        head.CFrame = rightHand.CFrame
                    end
                end
                wait(1) -- Update every second
            end
        end)
    end
end)

