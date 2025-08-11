-- MASTER HUB Básico Compacto (Versão Corrigida)

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Função para criar botões
local function criarBotao(nome, parent, posY)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 180, 0, 40)
    btn.Position = UDim2.new(0, 10, 0, posY)
    btn.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    btn.TextColor3 = Color3.fromRGB(0, 170, 255)
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 18
    btn.Text = nome
    btn.Parent = parent
    btn.AutoButtonColor = true
    return btn
end

-- Criar ScreenGui e Frame principal
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "MasterHubGui"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 200, 0, 170)
frame.Position = UDim2.new(0.5, -100, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
frame.BorderSizePixel = 0
frame.Parent = screenGui

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 30)
title.BackgroundTransparency = 1
title.Text = "MASTER HUB"
title.TextColor3 = Color3.fromRGB(0, 170, 255)
title.Font = Enum.Font.GothamBold
title.TextSize = 22
title.Parent = frame

-- Frame de TP
local tpFrame = Instance.new("Frame")
tpFrame.Size = UDim2.new(0, 180, 0, 80)
tpFrame.Position = UDim2.new(0.5, -90, 0.3, 180)
tpFrame.BackgroundColor3 = Color3.fromRGB(22, 22, 22)
tpFrame.BorderSizePixel = 0
tpFrame.Visible = false
tpFrame.Parent = screenGui

local tpLabel = Instance.new("TextLabel")
tpLabel.Size = UDim2.new(1, 0, 0, 30)
tpLabel.BackgroundTransparency = 1
tpLabel.Text = "TP"
tpLabel.TextColor3 = Color3.fromRGB(0, 170, 255)
tpLabel.Font = Enum.Font.GothamBold
tpLabel.TextSize = 20
tpLabel.Parent = tpFrame

local tpBtn = Instance.new("TextButton")
tpBtn.Size = UDim2.new(0, 100, 0, 30)
tpBtn.Position = UDim2.new(0.5, -50, 0, 40)
tpBtn.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
tpBtn.TextColor3 = Color3.new(1, 1, 1)
tpBtn.Font = Enum.Font.GothamBold
tpBtn.TextSize = 18
tpBtn.Text = "Confirmar TP"
tpBtn.Parent = tpFrame

local tpCloseBtn = Instance.new("TextButton")
tpCloseBtn.Size = UDim2.new(0, 30, 0, 30)
tpCloseBtn.Position = UDim2.new(1, -35, 0, 5)
tpCloseBtn.BackgroundColor3 = Color3.fromRGB(170, 0, 0)
tpCloseBtn.TextColor3 = Color3.new(1, 1, 1)
tpCloseBtn.Font = Enum.Font.GothamBold
tpCloseBtn.TextSize = 18
tpCloseBtn.Text = "X"
tpCloseBtn.Parent = tpFrame

-- Função tela preta
local function telaPretaFade()
    local blackScreen = Instance.new("Frame")
    blackScreen.Size = UDim2.new(1, 0, 1, 0)
    blackScreen.BackgroundColor3 = Color3.new(0, 0, 0)
    blackScreen.Parent = playerGui
    blackScreen.ZIndex = 999
    blackScreen.BackgroundTransparency = 1

    for i = 0, 1, 0.1 do
        blackScreen.BackgroundTransparency = 1 - i
        wait(0.05)
    end
    wait(0.7)
    for i = 0, 1, 0.1 do
        blackScreen.BackgroundTransparency = i
        wait(0.05)
    end
    blackScreen:Destroy()
end

-- Função de teleporte
local function teleportarBase()
    local character = player.Character
    if not character or not character:FindFirstChild("HumanoidRootPart") then return end

    local baseModel = workspace:FindFirstChild(player.Name)
    if not baseModel then
        warn("Base do jogador não encontrada")
        return
    end

    local hrp = character.HumanoidRootPart
    local basePos = baseModel:GetModelCFrame().p + Vector3.new(0, 5, 0)
    hrp.CFrame = CFrame.new(basePos)
end

-- Botões
local posY = 40
local btnTP = criarBotao("Abrir TP", frame, posY)
posY = posY + 45
local btnSpeed = criarBotao("Alternar Velocidade", frame, posY)
posY = posY + 45
local btnSuperJump = criarBotao("Alternar Super Pulo", frame, posY)

-- Variáveis de estado
local speedOn = false
local jumpOn = false

-- Eventos
btnSpeed.MouseButton1Click:Connect(function()
    speedOn = not speedOn
    local humanoid = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
    if speedOn and humanoid then
        humanoid.WalkSpeed = 250
        btnSpeed.Text = "Velocidade: ON"
    elseif humanoid then
        humanoid.WalkSpeed = 16
        btnSpeed.Text = "Velocidade: OFF"
    end
end)

btnSuperJump.MouseButton1Click:Connect(function()
    jumpOn = not jumpOn
    local humanoid = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
    if jumpOn and humanoid then
        humanoid.JumpPower = 90
        btnSuperJump.Text = "Super Pulo: ON"
    elseif humanoid then
        humanoid.JumpPower = 50
        btnSuperJump.Text = "Super Pulo: OFF"
    end
end)

btnTP.MouseButton1Click:Connect(function()
    tpFrame.Visible = not tpFrame.Visible
end)

tpCloseBtn.MouseButton1Click:Connect(function()
    tpFrame.Visible = false
end)

tpBtn.MouseButton1Click:Connect(function()
    tpFrame.Visible = false
    telaPretaFade()
    teleportarBase()
end)

