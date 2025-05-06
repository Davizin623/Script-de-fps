--// Interface
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local MinimizeButton = Instance.new("TextButton")
local FPSBoostButton = Instance.new("TextButton")

--// Configuração da Interface
ScreenGui.Parent = game.CoreGui
ScreenGui.Name = "ScriptDoKauanHzz"

Frame.Name = "Main"
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Frame.Position = UDim2.new(0.05, 0, 0.1, 0)
Frame.Size = UDim2.new(0, 250, 0, 150)
Frame.Active = true
Frame.Draggable = true

Title.Name = "Title"
Title.Parent = Frame
Title.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Font = Enum.Font.SourceSansBold
Title.Text = "Script do KauanHzz"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 18

MinimizeButton.Name = "Minimize"
MinimizeButton.Parent = Title
MinimizeButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
MinimizeButton.Position = UDim2.new(1, -30, 0, 0)
MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
MinimizeButton.Font = Enum.Font.SourceSansBold
MinimizeButton.Text = "-"
MinimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeButton.TextSize = 18

FPSBoostButton.Name = "FPSBoost"
FPSBoostButton.Parent = Frame
FPSBoostButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
FPSBoostButton.Position = UDim2.new(0.1, 0, 0.4, 0)
FPSBoostButton.Size = UDim2.new(0.8, 0, 0, 40)
FPSBoostButton.Font = Enum.Font.SourceSansBold
FPSBoostButton.Text = "Ativar FPS Boost"
FPSBoostButton.TextColor3 = Color3.fromRGB(255, 255, 255)
FPSBoostButton.TextSize = 16

--// Funções
local minimized = false
local originalSize = Frame.Size

MinimizeButton.MouseButton1Click:Connect(function()
    minimized = not minimized
    for _, v in pairs(Frame:GetChildren()) do
        if v ~= Title and v ~= MinimizeButton then
            v.Visible = not minimized
        end
    end
    if minimized then
        Frame.Size = UDim2.new(0, 250, 0, 30)
        MinimizeButton.Text = "+"
    else
        Frame.Size = originalSize
        MinimizeButton.Text = "-"
    end
end)

FPSBoostButton.MouseButton1Click:Connect(function()
    -- FPS BOOST
    sethiddenproperty(game:GetService("Lighting"), "Technology", Enum.Technology.Compatibility)
    game:GetService("Lighting").GlobalShadows = false
    game:GetService("Lighting").FogEnd = 9e9
    settings().Rendering.QualityLevel = "Level01"

    for _, v in pairs(workspace:GetDescendants()) do
        if v:IsA("BasePart") then
            v.Material = Enum.Material.SmoothPlastic
            v.Reflectance = 0
        elseif v:IsA("Decal") or v:IsA("Texture") then
            v:Destroy()
        end
    end

    FPSBoostButton.Text = "FPS Boost Ativado!"
end)
