local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Slash Hub [Muscle Legends] " .. Fluent.Version,
    SubTitle = "",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl -- Used when theres no MinimizeKeybind
})

--tabs
local Tabs = {
    Main = Window:AddTab({ Title = "Home", Icon = "Home" }),
    Settings = Window:AddTab({ Title = "Auto Farm", Icon = "" })
}

Tabs.Home:AddParagraph({
        Title = "DiscordParagraph",
        Content = "Discord Server:"
    })

Tabs.Home:AddButton({
    Title = "Copy Discord Server Link",
    Description = "",
    Callback = function()
        setclipboard("https://discord.gg/QEy2hTHc")
    end
})
