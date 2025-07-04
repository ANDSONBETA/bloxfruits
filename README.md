--[[
    Monarch AFK - Anti-AFK Tool
    Por ANDSONBETA + Copilot
    Interface moderna, arrastável, compacta, com créditos em destaque.
    Coloque este LocalScript no StarterGui.
]]

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer

-- GUI Setup
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MonarchAFK_UI"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

-- Botão de abrir/fechar (logo)
local LogoFrame = Instance.new("Frame")
LogoFrame.Name = "LogoFrame"
LogoFrame.Size = UDim2.new(0, 54, 0, 54)
LogoFrame.Position = UDim2.new(0.02, 0, 0.36, 0)
LogoFrame.BackgroundColor3 = Color3.fromRGB(80, 40, 150)
LogoFrame.BackgroundTransparency = 0.47
LogoFrame.BorderSizePixel = 0
LogoFrame.Active = true
LogoFrame.Parent = ScreenGui
local LogoCorner = Instance.new("UICorner")
LogoCorner.CornerRadius = UDim.new(1, 0)
LogoCorner.Parent = LogoFrame

local MLabel = Instance.new("TextLabel")
MLabel.Name = "MLabel"
MLabel.Parent = LogoFrame
MLabel.AnchorPoint = Vector2.new(0.5,0.5)
MLabel.Position = UDim2.new(0.5,0,0.5,1)
MLabel.Size = UDim2.new(1, -12, 1, -12)
MLabel.BackgroundTransparency = 1
MLabel.Text = "M"
MLabel.Font = Enum.Font.FredokaOne
MLabel.TextSize = 40
MLabel.TextColor3 = Color3.fromRGB(190, 80, 255)
MLabel.TextStrokeTransparency = 0.25

-- Botão real transparente para clicar toda área
local LogoBtn = Instance.new("ImageButton")
LogoBtn.Name = "LogoBtn"
LogoBtn.Size = UDim2.new(1,0,1,0)
LogoBtn.Position = UDim2.new(0,0,0,0)
LogoBtn.BackgroundTransparency = 1
LogoBtn.Image = ""
LogoBtn.Parent = LogoFrame

-- Main UI
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.BackgroundColor3 = Color3.fromRGB(32, 24, 48)
MainFrame.BackgroundTransparency = 0.18
MainFrame.Position = UDim2.new(0, 80, 0.34, 0)
MainFrame.Size = UDim2.new(0, 220, 0, 140)
MainFrame.Visible = false
MainFrame.AnchorPoint = Vector2.new(0,0)
MainFrame.Active = true
MainFrame.Selectable = true
MainFrame.Parent = ScreenGui
local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 26)
MainCorner.Parent = MainFrame
local MainStroke = Instance.new("UIStroke")
MainStroke.Thickness = 2
MainStroke.Color = Color3.fromRGB(190, 80, 255)
MainStroke.Transparency = 0.25
MainStroke.Parent = MainFrame

-- Título
local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.Text = "Monarch AFK"
Title.Font = Enum.Font.FredokaOne
Title.TextColor3 = Color3.fromRGB(190, 80, 255)
Title.TextStrokeTransparency = 0.28
Title.TextSize = 28
Title.BackgroundTransparency = 1
Title.Size = UDim2.new(1, 0, 0, 38)
Title.Position = UDim2.new(0, 0, 0, 4)
Title.Parent = MainFrame

-- Botão AFK
local AFKBtn = Instance.new("TextButton")
AFKBtn.Name = "AFKBtn"
AFKBtn.Text = "Ativar Anti-AFK"
AFKBtn.Font = Enum.Font.GothamBold
AFKBtn.TextSize = 17
AFKBtn.TextColor3 = Color3.fromRGB(255,255,255)
AFKBtn.BackgroundColor3 = Color3.fromRGB(140, 65, 205)
AFKBtn.BackgroundTransparency = 0.13
AFKBtn.BorderSizePixel = 0
AFKBtn.Size = UDim2.new(1, -36, 0, 38)
AFKBtn.Position = UDim2.new(0, 18, 0, 48)
local BtnCorner = Instance.new("UICorner")
BtnCorner.CornerRadius = UDim.new(0, 14)
BtnCorner.Parent = AFKBtn
AFKBtn.Parent = MainFrame

-- Status
local Status = Instance.new("TextLabel")
Status.Name = "Status"
Status.Text = "Evite ser kickado por inatividade!"
Status.Font = Enum.Font.Gotham
Status.TextSize = 13
Status.TextColor3 = Color3.fromRGB(210,180,255)
Status.BackgroundTransparency = 1
Status.Size = UDim2.new(1, -20, 0, 18)
Status.Position = UDim2.new(0, 10, 0, 92)
Status.TextXAlignment = Enum.TextXAlignment.Center
Status.Parent = MainFrame

-- Créditos
local Credits = Instance.new("TextLabel")
Credits.Text = "Feito por monarch (andson)"
Credits.Font = Enum.Font.GothamBlack
Credits.TextSize = 13
Credits.TextColor3 = Color3.fromRGB(255, 255, 255)
Credits.BackgroundTransparency = 1
Credits.Size = UDim2.new(1, 0, 0, 16)
Credits.Position = UDim2.new(0, 0, 1, -22)
Credits.TextXAlignment = Enum.TextXAlignment.Center
Credits.TextStrokeTransparency = 0.5
Credits.Parent = MainFrame

-- Função de abrir/fechar
LogoBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

-- Drag Logo
local draggingLogo, dragInputLogo, dragStartLogo, startPosLogo
LogoFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        draggingLogo = true
        dragStartLogo = input.Position
        startPosLogo = LogoFrame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then draggingLogo = false end
        end)
    end
end)
LogoFrame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then dragInputLogo = input end
end)
UserInputService.InputChanged:Connect(function(input)
    if input == dragInputLogo and draggingLogo then
        local delta = input.Position - dragStartLogo
        LogoFrame.Position = UDim2.new(startPosLogo.X.Scale, startPosLogo.X.Offset + delta.X, startPosLogo.Y.Scale, startPosLogo.Y.Offset + delta.Y)
    end
end)

-- Drag MainFrame
local draggingMain, dragInputMain, dragStartMain, startPosMain
MainFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        draggingMain = true
        dragStartMain = input.Position
        startPosMain = MainFrame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then draggingMain = false end
        end)
    end
end)
MainFrame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then dragInputMain = input end
end)
UserInputService.InputChanged:Connect(function(input)
    if input == dragInputMain and draggingMain then
        local delta = input.Position - dragStartMain
        MainFrame.Position = UDim2.new(startPosMain.X.Scale, startPosMain.X.Offset + delta.X, startPosMain.Y.Scale, startPosMain.Y.Offset + delta.Y)
    end
end)

-- Anti-AFK
local antiAFKEnabled = false
local antiAFKConnection = nil
AFKBtn.MouseButton1Click:Connect(function()
    antiAFKEnabled = not antiAFKEnabled
    AFKBtn.Text = antiAFKEnabled and "Desativar Anti-AFK" or "Ativar Anti-AFK"
    Status.Text = antiAFKEnabled and "Anti-AFK ATIVADO!" or "Anti-AFK DESATIVADO."
    if antiAFKEnabled then
        if antiAFKConnection then antiAFKConnection:Disconnect() end
        antiAFKConnection = RunService.RenderStepped:Connect(function()
            if tick() % 60 < 0.05 then
                local char = LocalPlayer.Character
                if char and char:FindFirstChild("HumanoidRootPart") then
                    char.HumanoidRootPart.CFrame = char.HumanoidRootPart.CFrame * CFrame.new(0.1,0,0)
                end
            end
        end)
    else
        if antiAFKConnection then antiAFKConnection:Disconnect() end
    end
end)
