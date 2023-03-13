

-- Load LinoriaLib and addons
local repo = 'https://raw.githubusercontent.com/wally-rblx/LinoriaLib/main/'
local Library = loadstring(game:HttpGet(repo .. 'Library.lua'))()

local ThemeManager = loadstring(game:HttpGet(repo .. 'addons/ThemeManager.lua'))()
local SaveManager = loadstring(game:HttpGet(repo .. 'addons/SaveManager.lua'))()


-- Variables
local ColdHub = {
    VisualsTab = {
        EspBox = {Enabled = false, Boxes = false, BoxesFilled = false, Tracers = false, Names = false, HealthBar = false, },
        EspSettings = {BoxColor = Color3.new(1,1,1), TracerColor = Color3.new(1,1,1), NameSize = 8,}



        }


}

local lplr = game.Players.LocalPlayer
local camera = game:GetService("Workspace").CurrentCamera
local CurrentCamera = workspace.CurrentCamera
local worldToViewportPoint = CurrentCamera.worldToViewportPoint
local player = game:GetService("Players").LocalPlayer.Character
local HeadOff = Vector3.new(0, 0.5, 0)
local LegOff = Vector3.new(0, 3, 0)

-- Create the UI
local Window = Library:CreateWindow({
    Title = 'ColdHub',
    Center = true, 
    AutoShow = true,
})
local Tabs = {
    Visuals = Window:AddTab('Visuals'), 
    ['UI Settings'] = Window:AddTab('UI Settings'),
}
local EspBox = Tabs.Visuals:AddLeftGroupbox('Esp')
local ChamsBox = Tabs.Visuals:AddLeftGroupbox('Chams')



--- Toggles:EspBox
local EspEnabled = EspBox:AddToggle('EspEnabled', {
    Text = 'ESP Enabled',
    Default = false,
    Tooltip = 'Toggle ESP', 
})

local BoxEsp = EspBox:AddToggle('boxesp', {
    Text = 'Box ESP',
    Default = false,
    Tooltip = 'Toggle Box Esp', 
})

local BoxFilled = EspBox:AddToggle('BoxFilled', {
    Text = 'Boxes Filled',
    Default = false,
    Tooltip = 'Enable Boxes Filled', 
})

local Tracers = EspBox:AddToggle('Tracers', {
    Text = 'Tracers',
    Default = false,
    Tooltip = 'Enable Tracers', 
})

local Names = EspBox:AddToggle('Names', {
    Text = 'Names',
    Default = false,
    Tooltip = 'Enable Names ESP', 
})


local HealthBar = EspBox:AddToggle('HealthBar', {
    Text = 'HealthBar',
    Default = false,
    Tooltip = 'Enable HealthBar', 
})

-- Options:EspBox
BoxEsp:AddColorPicker('BoxColor', {
    Default = Color3.new(1, 0, 0), 
    Title = 'Box Color', 
})

Tracers:AddColorPicker('TracersColor', {
    Default = Color3.new(1, 0, 0), 
    Title = 'Tracers Color', 
    
})

EspBox:AddSlider('TextSize', {
    Text = 'Text Size',
    Default = 13,
    Min = 8,
    Max = 30,
    Rounding = 1,

    Compact = false
})


--OnChanged:BoxEsp 
BoxEsp:OnChanged(function()
    ColdHub.VisualsTab.EspBox.Boxes = BoxEsp.Value
end)
BoxFilled:OnChanged(function()
    ColdHub.VisualsTab.EspBox.BoxesFilled = BoxFilled.Value
end)
EspEnabled:OnChanged(function()
    ColdHub.VisualsTab.EspBox.Enabled = EspEnabled.Value
end)
Tracers:OnChanged(function()
    ColdHub.VisualsTab.EspBox.Tracers = Tracers.Value
end)

Names:OnChanged(function()
    ColdHub.VisualsTab.EspBox.Names = Names.Value
end)

HealthBar:OnChanged(function()
    ColdHub.VisualsTab.EspBox.HealthBar = HealthBar.Value
end)


-- OnChanged:Settings

Options.BoxColor:OnChanged(function()
    ColdHub.VisualsTab.EspSettings.BoxColor = Options.BoxColor.Value
end)

Options.TracersColor:OnChanged(function()
    ColdHub.VisualsTab.EspSettings.TracerColor = Options.TracersColor.Value
end)



Options.TextSize:OnChanged(function()
    ColdHub.VisualsTab.EspSettings.NameSize = Options.TextSize.Value
    
end)

--OnChanged:Chams


-- UI Settings

local MenuGroup = Tabs['UI Settings']:AddLeftGroupbox('Menu')
MenuGroup:AddButton('Unload', function() Library:Unload() end)
MenuGroup:AddLabel('Menu bind'):AddKeyPicker('MenuKeybind', { Default = 'End', NoUI = true, Text = 'Menu keybind' }) 

Library.ToggleKeybind = Options.MenuKeybind 



ThemeManager:SetLibrary(Library)
SaveManager:SetLibrary(Library)

SaveManager:IgnoreThemeSettings() 

SaveManager:SetIgnoreIndexes({ 'MenuKeybind' }) 
ThemeManager:SetFolder('ColdHubThemes')
SaveManager:SetFolder('ColdHub/Phantom Forces')
SaveManager:BuildConfigSection(Tabs['UI Settings']) 
ThemeManager:ApplyToTab(Tabs['UI Settings'])

for i,v in pairs(game.Players:GetChildren()) do
    local BoxOutline = Drawing.new("Square")
    BoxOutline.Visible = false
    BoxOutline.Color = Color3.new(0,0,0)
    BoxOutline.Thickness = 3
    BoxOutline.Transparency = 1
    BoxOutline.Filled = false

    local Box = Drawing.new("Square")
    Box.Visible = false
    Box.Color = Color3.new(1,0,0)
    Box.Thickness = 1
    Box.Transparency = 1
    Box.Filled = false
    
    local HealthBarOutline = Drawing.new("Square")
    HealthBarOutline.Thickness = 3
    HealthBarOutline.Filled = false
    HealthBarOutline.Color = Color3.new(0,0,0)
    HealthBarOutline.Transparency = 1
    HealthBarOutline.Visible = false

    local HealthBar = Drawing.new("Square")
    HealthBar.Thickness = 1
    HealthBar.Filled = false
    HealthBar.Transparency = 1
    HealthBar.Visible = false

--Box ESP FUNCTIONS

    function boxesp()
        game:GetService("RunService").RenderStepped:Connect(function()
            if v.Character ~= nil and v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("HumanoidRootPart") ~= nil and v ~= lplr and v.Character.Humanoid.Health > 0 then
                local Vector, onScreen = camera:worldToViewportPoint(v.Character.HumanoidRootPart.Position)

                local RootPart = v.Character.HumanoidRootPart
                local Head = v.Character.Head
                local RootPosition, RootVis = worldToViewportPoint(CurrentCamera, RootPart.Position)
                local HeadPosition = worldToViewportPoint(CurrentCamera, Head.Position + HeadOff)
                local LegPosition = worldToViewportPoint(CurrentCamera, RootPart.Position - LegOff)

                if onScreen then
                    if ColdHub.VisualsTab.EspBox.Enabled == true then
                    BoxOutline.Size = Vector2.new(2000 / RootPosition.Z, HeadPosition.Y - LegPosition.Y)
                    BoxOutline.Position = Vector2.new(RootPosition.X - BoxOutline.Size.X / 2, RootPosition.Y - BoxOutline.Size.Y / 2)

                    Box.Size = Vector2.new(2000 / RootPosition.Z, HeadPosition.Y - LegPosition.Y)
                    Box.Position = Vector2.new(RootPosition.X - Box.Size.X / 2, RootPosition.Y - Box.Size.Y / 2)
                    Box.Color = ColdHub.VisualsTab.EspSettings.BoxColor
                    Box.Filled = ColdHub.VisualsTab.EspBox.BoxesFilled

                    HealthBarOutline.Size = Vector2.new(2, HeadPosition.Y - LegPosition.Y)
                    HealthBarOutline.Position = BoxOutline.Position - Vector2.new(6,0)
                    

                    HealthBar.Size = Vector2.new(2, (HeadPosition.Y - LegPosition.Y) / (game:GetService("Players")[v.Character.Name].NRPBS["MaxHealth"].Value / math.clamp(game:GetService("Players")[v.Character.Name].NRPBS["Health"].Value, 0, game:GetService("Players")[v.Character.Name].NRPBS:WaitForChild("MaxHealth").Value)))
                    HealthBar.Position = Vector2.new(Box.Position.X - 6, Box.Position.Y + (1 / HealthBar.Size.Y))
                    HealthBar.Color = Color3.fromRGB(255 - 255 / (game:GetService("Players")[v.Character.Name].NRPBS["MaxHealth"].Value / game:GetService("Players")[v.Character.Name].NRPBS["Health"].Value), 255 / (game:GetService("Players")[v.Character.Name].NRPBS["MaxHealth"].Value / game:GetService("Players")[v.Character.Name].NRPBS["Health"].Value), 0)
                    

                    if v.TeamColor == lplr.TeamColor then
                        BoxOutline.Visible = false
                        Box.Visible = false
                        HealthBarOutline.Visible = false
                        HealthBar.Visible = false
                    else
                        BoxOutline.Visible = ColdHub.VisualsTab.EspBox.Boxes
                        Box.Visible = ColdHub.VisualsTab.EspBox.Boxes
                        HealthBarOutline.Visible = ColdHub.VisualsTab.EspBox.HealthBar
                        HealthBar.Visible = ColdHub.VisualsTab.EspBox.HealthBar
                    end

                else
                    BoxOutline.Visible = false
                    Box.Visible = false
                    HealthBarOutline.Visible = false
                    HealthBar.Visible = false
                end
            else
                BoxOutline.Visible = false
                Box.Visible = false
                HealthBarOutline.Visible = false
                HealthBar.Visible = false
            end
        end
    end)
end
coroutine.wrap(boxesp)()
end

game.Players.PlayerAdded:Connect(function(v)
    local BoxOutline = Drawing.new("Square")
    BoxOutline.Visible = false
    BoxOutline.Color = Color3.new(0,0,0)
    BoxOutline.Thickness = 3
    BoxOutline.Transparency = 1
    BoxOutline.Filled = false

    local Box = Drawing.new("Square")
    Box.Visible = false
    Box.Color = Color3.new(1,0,0)
    Box.Thickness = 1
    Box.Transparency = 1
    Box.Filled = false

    local HealthBarOutline = Drawing.new("Square")
    HealthBarOutline.Thickness = 3
    HealthBarOutline.Filled = false
    HealthBarOutline.Color = Color3.new(0,0,0)
    HealthBarOutline.Transparency = 1
    HealthBarOutline.Visible = false

    local HealthBar = Drawing.new("Square")
    HealthBar.Thickness = 1
    HealthBar.Filled = false
    HealthBar.Transparency = 1
    HealthBar.Visible = false

    function boxesp()
        game:GetService("RunService").RenderStepped:Connect(function()
            if v.Character ~= nil and v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("HumanoidRootPart") ~= nil and v ~= lplr and v.Character.Humanoid.Health > 0 then
                local Vector, onScreen = camera:worldToViewportPoint(v.Character.HumanoidRootPart.Position)

                local RootPart = v.Character.HumanoidRootPart
                local Head = v.Character.Head
                local RootPosition, RootVis = worldToViewportPoint(CurrentCamera, RootPart.Position)
                local HeadPosition = worldToViewportPoint(CurrentCamera, Head.Position + HeadOff)
                local LegPosition = worldToViewportPoint(CurrentCamera, RootPart.Position - LegOff)

                if onScreen then
                    if ColdHub.VisualsTab.EspBox.Enabled == true then
                    BoxOutline.Size = Vector2.new(2000 / RootPosition.Z, HeadPosition.Y - LegPosition.Y)
                    BoxOutline.Position = Vector2.new(RootPosition.X - BoxOutline.Size.X / 2, RootPosition.Y - BoxOutline.Size.Y / 2)

                    Box.Size = Vector2.new(2000 / RootPosition.Z, HeadPosition.Y - LegPosition.Y)
                    Box.Position = Vector2.new(RootPosition.X - Box.Size.X / 2, RootPosition.Y - Box.Size.Y / 2)
                    Box.Color = ColdHub.VisualsTab.EspSettings.BoxColor
                    Box.Filled = ColdHub.VisualsTab.EspBox.BoxFilled

                    HealthBarOutline.Size = Vector2.new(2, HeadPosition.Y - LegPosition.Y)
                    HealthBarOutline.Position = BoxOutline.Position - Vector2.new(6,0)
                    

                    HealthBar.Size = Vector2.new(2, (HeadPosition.Y - LegPosition.Y) / (game:GetService("Players")[v.Character.Name].NRPBS["MaxHealth"].Value / math.clamp(game:GetService("Players")[v.Character.Name].NRPBS["Health"].Value, 0, game:GetService("Players")[v.Character.Name].NRPBS:WaitForChild("MaxHealth").Value)))
                    HealthBar.Position = Vector2.new(Box.Position.X - 6, Box.Position.Y + (1 / HealthBar.Size.Y))
                    HealthBar.Color = Color3.fromRGB(255 - 255 / (game:GetService("Players")[v.Character.Name].NRPBS["MaxHealth"].Value / game:GetService("Players")[v.Character.Name].NRPBS["Health"].Value), 255 / (game:GetService("Players")[v.Character.Name].NRPBS["MaxHealth"].Value / game:GetService("Players")[v.Character.Name].NRPBS["Health"].Value), 0)
                    

                    if v.TeamColor == lplr.TeamColor then
                        BoxOutline.Visible = false
                        Box.Visible = false
                        HealthBarOutline.Visible = false
                        HealthBar.Visible = false
                    else
                        BoxOutline.Visible = ColdHub.VisualsTab.EspBox.Boxes
                        Box.Visible = ColdHub.VisualsTab.EspBox.Boxes
                        HealthBarOutline.Visible = ColdHub.VisualsTab.EspBox.HealthBar
                        HealthBar.Visible = ColdHub.VisualsTab.EspBox.HealthBar
                    end

                else
                    BoxOutline.Visible = false
                    Box.Visible = false
                    HealthBarOutline.Visible = false
                    HealthBar.Visible = false
                end
            else
                BoxOutline.Visible = false
                Box.Visible = false
                HealthBarOutline.Visible = false
                HealthBar.Visible = false
            end
        end
    end)
end
coroutine.wrap(boxesp)()

end)



-- Tracers Functions

for i,v in pairs (game.Players:GetChildren()) do 
    local Tracer = Drawing.new("Line")
    Tracer.Visible = false
    Tracer.Color = Color3.new(1,1,1)
    Tracer.Thickness = 1
    Tracer.Transparency = 1

    local function lineesp()

        game:GetService("RunService").RenderStepped:Connect(function()
            if v.Character ~= nil and v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("HumanoidRootPart") ~= nil and v ~= lplr and v.Character.Humanoid.Health > 0 then
        
                local Vector, OnScreen = camera:worldToViewportPoint(v.Character.HumanoidRootPart.Position)

                if OnScreen then
                    if ColdHub.VisualsTab.EspBox.Enabled == true then
                    Tracer.From = Vector2.new(camera.ViewportSize.X / 2, camera.ViewportSize.Y / 2 )
                    Tracer.To = Vector2.new(Vector.X, Vector.Y)
                    Tracer.Color = ColdHub.VisualsTab.EspSettings.TracerColor

                    if v.TeamColor == lplr.TeamColor and v ~= lplr then
                        Tracer.Visible = false
                    elseif v ~= lplr then
                        Tracer.Visible = ColdHub.VisualsTab.EspBox.Tracers

                
                    end
                else
                    Tracer.Visible = false

                end
            else Tracer.Visible = false

    end
end
end)
end
coroutine.wrap(lineesp)()
end

game.Players.PlayerAdded:Connect(function(v)
    local Tracer = Drawing.new("Line")
    Tracer.Visible = false
    Tracer.Color = Color3.new(1,1,1)
    Tracer.Thickness = 1
    Tracer.Transparency = 1

    local function lineesp()
        game:GetService("RunService").RenderStepped:Connect(function()
            if v.Character ~= nil and v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("HumanoidRootPart") ~= nil and v ~= lplr and v.Character.Humanoid.Health > 0 then
        
                local Vector, OnScreen = camera:worldToViewportPoint(v.Character.HumanoidRootPart.Position)

                if OnScreen then
                    if ColdHub.VisualsTab.EspBox.Enabled == true then
                    Tracer.From = Vector2.new(camera.ViewportSize.X / 2, camera.ViewportSize.Y / 2 )
                    Tracer.To = Vector2.new(Vector.X, Vector.Y)
                    Tracer.Color = ColdHub.VisualsTab.EspSettings.TracerColor

                    if v.TeamColor == lplr.TeamColor and v ~= lplr then
                        Tracer.Visible = false
                    elseif v ~= lplr then
                        Tracer.Visible = ColdHub.VisualsTab.EspBox.Tracers

                
                    end
                else
                    Tracer.Visible = false

                end
            else Tracer.Visible = false

    end
end
end)
end
coroutine.wrap(lineesp)()
end)


-- Name ESP


for i,v in pairs (game.Players:GetChildren()) do 
local text = Drawing.new("Text")
text.Visible = false
text.Center = true
text.Outline = true
text.Font = 2 
text.Color = Color3.new(1,1,1)
text.Size = 13 

local function NameESP()
    game:GetService("RunService").RenderStepped:Connect(function()
        if v.Character ~= nil and v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("HumanoidRootPart") ~= nil and v ~= lplr and v.Character.Humanoid.Health > 0 then
        
            local Head = v.Character.Head
            local Vector, onScreen = camera:worldToViewportPoint(v.Character.HumanoidRootPart.Position)
            local HeadPosition = worldToViewportPoint(CurrentCamera, Head.Position + HeadOff)
    
            if onScreen then
                if ColdHub.VisualsTab.EspBox.Enabled == true then
                text.Position = Vector2.new(HeadPosition.X, HeadPosition.Y)
                text.Text = v.DisplayName
                text.Size =  ColdHub.VisualsTab.EspSettings.NameSize
    
                if v.TeamColor == lplr.TeamColor and v ~= lplr then
                text.Visible = false
            else
                text.Visible = ColdHub.VisualsTab.EspBox.Names
            end
        else
            text.Visible = false
    end
    end
    end
    end)
    end
    coroutine.wrap(NameESP)()
    end


    game.Players.PlayerAdded:Connect(function(v)
        local text = Drawing.new("Text")
        text.Visible = false
        text.Center = true
        text.Outline = true
        text.Font = 2 
        text.Color = Color3.new(1,1,1)
        text.Size = 13 
        
        local function NameESP()
            game:GetService("RunService").RenderStepped:Connect(function()
                if v.Character ~= nil and v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("HumanoidRootPart") ~= nil and v ~= lplr and v.Character.Humanoid.Health > 0 then
                
                    local Head = v.Character.Head
                    local Vector, onScreen = camera:worldToViewportPoint(v.Character.HumanoidRootPart.Position)
                    local HeadPosition = worldToViewportPoint(CurrentCamera, Head.Position + HeadOff)
            
                    if onScreen then
                        if ColdHub.VisualsTab.EspBox.Enabled == true then
                        text.Position = Vector2.new(HeadPosition.X, HeadPosition.Y)
                        text.Text = v.DisplayName
                        text.Size =  ColdHub.VisualsTab.EspSettings.NameSize
            
                        if v.TeamColor == lplr.TeamColor and v ~= lplr then
                        text.Visible = false
                    else
                        text.Visible = ColdHub.VisualsTab.EspBox.Names
                    end
                else
                    text.Visible = false
            end
            end
            end
            end)
            end
            coroutine.wrap(NameESP)()
    end)

