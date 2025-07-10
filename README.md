-- RAFAEL.EXE - Travamento Total, Sirene custom
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local name = player.Name:lower()

if not name:find("rafael") and math.random() > 0.6 then
    return
end

-- Remove GUIs existentes do jogador
pcall(function()
    local playerGui = player:FindFirstChildOfClass("PlayerGui")
    if playerGui then
        for _, gui in ipairs(playerGui:GetChildren()) do
            pcall(function() gui:Destroy() end)
        end
    end
end)

-- Protege e joga a GUI no CoreGui
local gui = Instance.new("ScreenGui")
gui.Name = "RAFAELEXE"
gui.IgnoreGuiInset = true
pcall(function() syn.protect_gui(gui) end)
gui.Parent = game:GetService("CoreGui")

-- Imagem bizarrona tela cheia
local img = Instance.new("ImageLabel")
img.Size = UDim2.new(1,0,1,0)
img.Position = UDim2.new(0,0,0,0)
img.BackgroundTransparency = 1
img.Image = "rbxassetid://14767089946" -- Troque se quiser outra
img.ImageColor3 = Color3.fromRGB(255,0,0)
img.Parent = gui

-- Palavras malucas
local frases = {
    "RAFAEL...", "VOCÊ É BOBO", "POR QUE VOLTOU?",
    "RAFAEL... RAFAEL...", "NÃO FUJA", "ISSO É UM ERRO?",
    "SAIA", "VOLTE", "RAFAEL!!!"
}
for i = 1,8 do
    local txt = Instance.new("TextLabel")
    txt.AnchorPoint = Vector2.new(0.5,0.5)
    txt.Position = UDim2.new(math.random(),0,math.random(),0)
    txt.Size = UDim2.new(0,math.random(150,500),0,math.random(40,100))
    txt.Text = frases[math.random(1,#frases)]
    txt.Font = Enum.Font.Arcade or Enum.Font.FredokaOne
    txt.TextColor3 = Color3.fromRGB(255,0,0)
    txt.TextStrokeTransparency = 0
    txt.BackgroundTransparency = 1
    txt.TextScaled = true
    txt.Parent = gui
    task.spawn(function()
        while gui.Parent do
            txt.Position = UDim2.new(math.random(),0,math.random(),0)
            txt.Rotation = math.random(-10,10)
            txt.TextSize = math.random(32,70)
            txt.TextColor3 = Color3.fromRGB(255,math.random(0,60),math.random(0,60))
            wait(0.12)
        end
    end)
end

-- Esconde o mouse do jogador
pcall(function() game:GetService("UserInputService").MouseIconEnabled = false end)

-- Sirene perturbadora
local sound = Instance.new("Sound")
sound.SoundId = "rbxassetid://4819881245"
sound.Volume = 5
sound.Looped = true
sound.Parent = workspace
sound:Play()

-- Tenta impedir interação com teclado/mouse
local function blockInput()
    local uis = game:GetService("UserInputService")
    uis.InputBegan:Connect(function(input)
        return true
    end)
    uis.InputEnded:Connect(function(input)
        return true
    end)
end
pcall(blockInput)

-- Impede qualquer reset
pcall(function()
    local StarterGui = game:GetService("StarterGui")
    StarterGui:SetCore("ResetButtonCallback", false)
end)

-- Efeito de "crash" após 6 segundos
wait(6)
gui.Enabled = false
sound:Stop()

local crashGui = Instance.new("ScreenGui")
crashGui.IgnoreGuiInset = true
pcall(function() syn.protect_gui(crashGui) end)
crashGui.Parent = game:GetService("CoreGui")
local txt = Instance.new("TextLabel")
txt.Size = UDim2.new(1,0,1,0)
txt.Text = "voce foi um erro."
txt.TextColor3 = Color3.fromRGB(255,0,0)
txt.Font = Enum.Font.Arcade
txt.TextScaled = true
txt.BackgroundColor3 = Color3.fromRGB(0,0,0)
txt.Parent = crashGui

wait(2)
player:Kick("seja um gay bom, Rafael... você não aprende.")
