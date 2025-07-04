--[[
    MonarcK - Anti-AFK Tool + Hit-Me + ESP-Gays (Box) + Rafael Jumpscare
    Por monarch
    Interface moderna, arrastável, compacta, com créditos em destaque.
    Coloque este LocalScript no StarterGui.
    Créditos limpos!
]]

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer

-- GUI Setup
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MonarcK_UI"
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
MainFrame.Size = UDim2.new(0, 220, 0, 242)
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
Title.Text = "MonarcK"
Title.Font = Enum.Font.Arcade -- Minecraft-like font
Title.TextColor3 = Color3.fromRGB(190, 80, 255)
Title.TextStrokeTransparency = 0.18
Title.TextStrokeColor3 = Color3.fromRGB(0,0,0)
Title.TextSize = 28
Title.BackgroundTransparency = 1
Title.Size = UDim2.new(1, 0, 0, 38)
Title.Position = UDim2.new(0, 0, 0, 4)
Title.Parent = MainFrame

-- Função para criar botões de função bonitos e destacados
local function createFunctionButton(name, text, yPos, color, font, parent)
    local btn = Instance.new("TextButton")
    btn.Name = name
    btn.Text = text
    btn.Font = font or Enum.Font.FredokaOne
    btn.TextSize = 20
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.TextStrokeTransparency = 0.2
    btn.TextStrokeColor3 = Color3.fromRGB(100,0,100)
    btn.BackgroundColor3 = color
    btn.BackgroundTransparency = 0.10
    btn.BorderSizePixel = 0
    btn.Size = UDim2.new(1, -36, 0, 36)
    btn.Position = UDim2.new(0, 18, 0, yPos)
    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0, 14)
    btnCorner.Parent = btn
    btn.Parent = parent
    return btn
end

-- Botão AFK (Fonte FredokaOne, destacado)
local AFKBtn = createFunctionButton(
    "AFKBtn", "Ativar Anti-AFK", 48, 
    Color3.fromRGB(140, 65, 205), Enum.Font.FredokaOne, MainFrame
)

-- Botão Hit-Me (reset) (Fonte GothamBlack, destacado)
local HitMeBtn = createFunctionButton(
    "HitMeBtn", "Hit-Me (Resetar)", 92, 
    Color3.fromRGB(200, 65, 120), Enum.Font.GothamBlack, MainFrame
)

-- Botão ESP-Gays (Fonte FredokaOne, destacado)
local EspGaysBtn = createFunctionButton(
    "EspGaysBtn", "ESP-Gays", 136, 
    Color3.fromRGB(255, 30, 30), Enum.Font.FredokaOne, MainFrame
)

-- Botão Rafael (Fonte Arcade, destacado)
local RafaelBtn = createFunctionButton(
    "Rafael", "Rafael", 180, 
    Color3.fromRGB(60,0,0), Enum.Font.Arcade, MainFrame
)
RafaelBtn.TextStrokeTransparency = 0.08
RafaelBtn.TextSize = 22

-- Status
local Status = Instance.new("TextLabel")
Status.Name = "Status"
Status.Text = "Evite ser kickado por inatividade!"
Status.Font = Enum.Font.Gotham
Status.TextSize = 13
Status.TextColor3 = Color3.fromRGB(210,180,255)
Status.BackgroundTransparency = 1
Status.Size = UDim2.new(1, -20, 0, 18)
Status.Position = UDim2.new(0, 10, 0, 220)
Status.TextXAlignment = Enum.TextXAlignment.Center
Status.Parent = MainFrame

-- Créditos (GothamBlack, tradicional, sem nada atrás)
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

-- Hit-Me: Resetar personagem
HitMeBtn.MouseButton1Click:Connect(function()
    local char = LocalPlayer.Character
    if char and char:FindFirstChildOfClass("Humanoid") then
        char:FindFirstChildOfClass("Humanoid").Health = 0
        Status.Text = "Personagem resetado!"
    else
        Status.Text = "Não foi possível resetar."
    end
end)

-- ESP-Gays (BOX: nome branco pequeno + box em todos os parts do personagem)
local espEnabled = false
local ESPFolder = Instance.new("Folder")
ESPFolder.Name = "ESPFolder"
ESPFolder.Parent = ScreenGui

local function clearESP()
    for _,v in pairs(ESPFolder:GetChildren()) do
        v:Destroy()
    end
end

local function createESPBox(part)
    local adorn = Instance.new("BoxHandleAdornment")
    adorn.Name = "ESPBox"
    adorn.Adornee = part
    adorn.AlwaysOnTop = true
    adorn.ZIndex = 10
    adorn.Size = part.Size
    adorn.Color3 = Color3.fromRGB(255,0,0)
    adorn.Transparency = 0.7
    adorn.Parent = ESPFolder
end

local function createESPForPlayer(plr)
    if plr == LocalPlayer then return end
    local char = plr.Character
    if not char then return end
    -- Nome branco e menor acima da cabeça
    if char:FindFirstChild("Head") then
        local billboard = Instance.new("BillboardGui")
        billboard.Name = "MonarchESP"
        billboard.Adornee = char.Head
        billboard.Size = UDim2.new(0, 70, 0, 13)
        billboard.StudsOffset = Vector3.new(0, 2, 0)
        billboard.AlwaysOnTop = true
        billboard.Parent = ESPFolder

        local nameLabel = Instance.new("TextLabel")
        nameLabel.BackgroundTransparency = 1
        nameLabel.Size = UDim2.new(1, 0, 1, 0)
        nameLabel.Text = plr.Name
        nameLabel.Font = Enum.Font.GothamBold
        nameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        nameLabel.TextStrokeTransparency = 0.6
        nameLabel.TextScaled = true
        nameLabel.Parent = billboard
    end
    -- Box vermelha em todas as hitboxes (Parts)
    for _,p in ipairs(char:GetChildren()) do
        if p:IsA("BasePart") then
            createESPBox(p)
        end
    end
end

local function updateESP()
    clearESP()
    for _,plr in ipairs(Players:GetPlayers()) do
        createESPForPlayer(plr)
    end
end

EspGaysBtn.MouseButton1Click:Connect(function()
    espEnabled = not espEnabled
    EspGaysBtn.Text = espEnabled and "ESP-Gays (ON)" or "ESP-Gays"
    Status.Text = espEnabled and "ESP-Gays Ativado!" or "ESP-Gays Desativado."
    if not espEnabled then
        clearESP()
    else
        updateESP()
    end
end)
Players.PlayerAdded:Connect(function() if espEnabled then updateESP() end end)
Players.PlayerRemoving:Connect(function() if espEnabled then updateESP() end end)
Players.PlayerAdded:Connect(function(plr) plr.CharacterAdded:Connect(function() if espEnabled then updateESP() end end) end)

-- Rafael: jumpscare, trava tela e fecha script
RafaelBtn.MouseButton1Click:Connect(function()
    -- Jumpscare overlay
    local jumpscareFrame = Instance.new("Frame")
    jumpscareFrame.BackgroundColor3 = Color3.fromRGB(255,0,0)
    jumpscareFrame.BackgroundTransparency = 0
    jumpscareFrame.Size = UDim2.new(1,0,1,0)
    jumpscareFrame.Position = UDim2.new(0,0,0,0)
    jumpscareFrame.Parent = ScreenGui
    jumpscareFrame.ZIndex = 9999

    local jumpscareLabel = Instance.new("TextLabel")
    jumpscareLabel.Text = "RAFAEL!!!!"
    jumpscareLabel.Font = Enum.Font.Arcade
    jumpscareLabel.TextSize = 85
    jumpscareLabel.TextColor3 = Color3.new(1,1,1)
    jumpscareLabel.TextStrokeColor3 = Color3.new(0,0,0)
    jumpscareLabel.TextStrokeTransparency = 0.3
    jumpscareLabel.BackgroundTransparency = 1
    jumpscareLabel.Size = UDim2.new(1,0,1,0)
    jumpscareLabel.Position = UDim2.new(0,0,0,0)
    jumpscareLabel.ZIndex = 10000
    jumpscareLabel.Parent = jumpscareFrame

    -- Congela tela (Remove tudo)
    wait(1.1)
    ScreenGui:Destroy()
    if ESPFolder then pcall(function() ESPFolder:Destroy() end) end
end)
