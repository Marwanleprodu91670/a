-- Load the Fluent library from GitHub
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()

-- Create the main window (Slash Hub)
local window = Fluent:Window({
    Title = "Slash Hub",
    Size = UDim2.new(0, 400, 0, 300),
    Position = UDim2.new(0.5, -200, 0.5, -150),
    Draggable = true,
    Resizable = true
})

-- Create a Home Tab
local homeTab = Fluent:Tab({
    Name = "Home",
    Parent = window,
})

-- Create a Label that says "Discord Server Link:"
local discordLabel = Fluent:Label({
    Text = "Discord Server Link:",
    Parent = homeTab,
    Position = UDim2.new(0.5, -100, 0.2, 0), -- Centers the label
    Size = UDim2.new(0, 200, 0, 50),
})

-- Function to copy the link to clipboard (Roblox does not have direct clipboard access, so we use a TextBox)
local function copyLink()
    local textBox = Instance.new("TextBox")
    textBox.Text = "https://discord.gg/QEy2hTHc"
    textBox.TextButton = true
    textBox.Size = UDim2.new(0, 1, 0, 1)  -- Minimized so it's invisible
    textBox.BackgroundTransparency = 1
    textBox.Parent = game.CoreGui

    -- Focus the TextBox to copy to clipboard
    textBox:CaptureFocus()
    textBox.TextButton = true
    game:GetService("GuiService"):SetCore("SendNotification", {
        Title = "Success",
        Text = "Link copied to clipboard!",
        Duration = 2,
    })

    -- After a short time, remove the textBox from CoreGui
    delay(0.1, function()
        textBox:Destroy()
    end)
end

-- Create the Copy Link Button
local copyButton = Fluent:Button({
    Text = "Copy Link",
    Parent = homeTab,
    Position = UDim2.new(0.5, -75, 0.4, 0), -- Centers the button
    Size = UDim2.new(0, 150, 0, 50),
    OnClick = copyLink,
})

-- Show the window
window:Show()
