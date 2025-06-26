-- GUI principal
local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", game.CoreGui)
gui.Name = "VatoxScriptGUI"
gui.ResetOnSpawn = false

-- Função para obter senha baseada no tempo
local function getSenhaAtual()
    local tempo = tick() -- Tempo atual em segundos
    local tempoInicial = 0 -- Pode ser salvo externamente se quiser manter entre sessões
    if tempo - tempoInicial < 18000 then
        return "hakaigay"
    else
        return "vatoxlindo"
    end
end

-- Tela de senha
local senhaFrame = Instance.new("Frame", gui)
senhaFrame.Size = UDim2.new(0, 250, 0, 140)
senhaFrame.Position = UDim2.new(0.5, -125, 0.5, -70)
senhaFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
senhaFrame.Active = true
senhaFrame.Draggable = true

local senhaCorner = Instance.new("UICorner", senhaFrame)
senhaCorner.CornerRadius = UDim.new(0, 10)

local senhaLabel = Instance.new("TextLabel", senhaFrame)
senhaLabel.Size = UDim2.new(1, 0, 0, 40)
senhaLabel.Position = UDim2.new(0, 0, 0, 0)
senhaLabel.Text = "Digite a Senha"
senhaLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
senhaLabel.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
senhaLabel.TextSize = 18
senhaLabel.Font = Enum.Font.SourceSansBold

local senhaBox = Instance.new("TextBox", senhaFrame)
senhaBox.Size = UDim2.new(0.9, 0, 0, 40)
senhaBox.Position = UDim2.new(0.05, 0, 0, 50)
senhaBox.PlaceholderText = "Senha"
senhaBox.Text = ""
senhaBox.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
senhaBox.TextColor3 = Color3.fromRGB(255, 255, 255)
senhaBox.Font = Enum.Font.SourceSans
senhaBox.TextSize = 18

local senhaBtn = Instance.new("TextButton", senhaFrame)
senhaBtn.Size = UDim2.new(0.9, 0, 0, 30)
senhaBtn.Position = UDim2.new(0.05, 0, 0, 100)
senhaBtn.Text = "Entrar"
senhaBtn.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
senhaBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
senhaBtn.Font = Enum.Font.SourceSansBold
senhaBtn.TextSize = 16

local senhaBtnCorner = Instance.new("UICorner", senhaBtn)
senhaBtnCorner.CornerRadius = UDim.new(0, 6)

senhaBtn.MouseButton1Click:Connect(function()
    if senhaBox.Text == getSenhaAtual() then
        senhaFrame.Visible = false
    else
        gui:Destroy() -- Encerra tudo se errar a senha
    end
end)

-- Painel principal (inicialmente oculto até passar a senha)
local panel = Instance.new("Frame")
panel.Size = UDim2.new(0, 200, 0, 160)
panel.Position = UDim2.new(0, 140, 0, 40)
panel.BackgroundColor3 = Color3.fromRGB(20, 50, 180)
panel.Visible = true
panel.Active = true
panel.Draggable = true
panel.Parent = gui

local panelCorner = Instance.new("UICorner", panel)
panelCorner.CornerRadius = UDim.new(0, 10)

local title = Instance.new("TextLabel", panel)
title.Size = UDim2.new(1, 0, 0, 30)
title.Position = UDim2.new(0, 0, 0, 0)
title.Text = "Vatox Script"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.BackgroundColor3 = Color3.fromRGB(40, 40, 90)
title.TextSize = 18
title.Font = Enum.Font.SourceSansBold

local titleCorner = Instance.new("UICorner", title)
titleCorner.CornerRadius = UDim.new(0, 8)

-- Botão imagem
local toggleButton = Instance.new("ImageButton", gui)
toggleButton.Size = UDim2.new(0, 100, 0, 100)
toggleButton.Position = UDim2.new(0, 20, 0, 20)
toggleButton.Image = "http://www.roblox.com/asset/?id=14267946435"
toggleButton.BackgroundTransparency = 1
toggleButton.Name = "ToggleButton"

-- Função botão
local function createButton(icon, posY, callback, color)
    local btn = Instance.new("TextButton", panel)
    btn.Size = UDim2.new(0.9, 0, 0, 40)
    btn.Position = UDim2.new(0.05, 0, 0, posY)
    btn.Text = icon
    btn.BackgroundColor3 = color
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Font = Enum.Font.SourceSansBold
    btn.TextSize = 24
    btn.BorderSizePixel = 0

    local corner = Instance.new("UICorner", btn)
    corner.CornerRadius = UDim.new(0, 6)

    btn.MouseButton1Click:Connect(callback)
end

-- Botões
createButton("⬆", 40, function()
    local char = player.Character
    if char and char:FindFirstChild("HumanoidRootPart") then
        char.HumanoidRootPart.CFrame += Vector3.new(0, 200, 0)
    end
end, Color3.fromRGB(0, 200, 0))

createButton("⬇", 90, function()
    local char = player.Character
    if char and char:FindFirstChild("HumanoidRootPart") then
        char.HumanoidRootPart.CFrame += Vector3.new(0, -200, 0)
    end
end, Color3.fromRGB(200, 0, 0))

-- Mostrar/esconder painel
toggleButton.MouseButton1Click:Connect(function()
    panel.Visible = not panel.Visible
end)
