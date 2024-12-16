local Library = loadstring(game:HttpGetAsync("https://github.com/ActualMasterOogway/Fluent-Renewed/releases/latest/download/Fluent.luau"))()
local SaveManager = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/ActualMasterOogway/Fluent-Renewed/master/Addons/SaveManager.luau"))()
local InterfaceManager = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/ActualMasterOogway/Fluent-Renewed/master/Addons/InterfaceManager.luau"))()
 
local Window = Library:CreateWindow{
    Title = `Slash Hub`,
    SubTitle = "",
    TabWidth = 160,
    Size = UDim2.fromOffset(830, 525),
    Resize = true, -- Resize this ^ Size according to a 1920x1080 screen, good for mobile users but may look weird on some devices
    MinSize = Vector2.new(470, 380),
    Acrylic = true, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.RightControl -- Used when theres no MinimizeKeybind
}

local Tabs = {
    Home = Window:CreateTab{
        Title = "Home",
        Icon = ""
    }

local Options = Library.Options

Library:Notify{
    Title = "Notification",
    Content = "Welcome To Slash Hub",
    SubContent = "SubContent", -- Optional
    Duration = 5 
}

local Paragraph = Tabs.Home:CreateParagraph("Paragraph", {
    Title = "DiscordParagraph",
    Content = "Discord Server Link:"
})

Tabs.Home:CreateButton{
    Title = "Copy Discord Server Link",
    Description = "",
    Callback = function()
        setclipboard(https://discord.gg/QEy2hTHc)
}
