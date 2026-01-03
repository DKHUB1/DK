local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local player = Players.LocalPlayer

-- =========================
-- VARIÁVEIS DE POSIÇÃO
-- =========================
local lastMainPosition = UDim2.new(0.5, -325, 0.5, -190)
local lastMiniPosition = UDim2.new(0.5, -30, 0.5, -30)

-- =========================
-- SCREEN GUI
-- =========================
local gui = Instance.new("ScreenGui")
gui.Name = "DK_HUB"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

-- =========================
-- HUB PRINCIPAL
-- =========================
local main = Instance.new("Frame")
main.Size = UDim2.new(0, 650, 0, 380)
main.Position = lastMainPosition
main.BackgroundColor3 = Color3.fromRGB(18,18,18)
main.BorderSizePixel = 0
main.Active = true
main.Draggable = true
main.Parent = gui
Instance.new("UICorner", main).CornerRadius = UDim.new(0,14)

-- Salvar posição ao mover
main:GetPropertyChangedSignal("Position"):Connect(function()
	lastMainPosition = main.Position
end)

-- =========================
-- SIDEBAR
-- =========================
local sidebar = Instance.new("Frame")
sidebar.Size = UDim2.new(0, 70, 1, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(14,14,14)
sidebar.BorderSizePixel = 0
sidebar.Parent = main
Instance.new("UICorner", sidebar).CornerRadius = UDim.new(0,14)

for i = 1, 6 do
	local icon = Instance.new("Frame")
	icon.Size = UDim2.new(0, 40, 0, 40)
	icon.Position = UDim2.new(0, 15, 0, 20 + (i-1)*55)
	icon.BackgroundColor3 = Color3.fromRGB(30,30,30)
	icon.BorderSizePixel = 0
	icon.Parent = sidebar
	Instance.new("UICorner", icon).CornerRadius = UDim.new(1,0)
end

-- =========================
-- TOP BAR
-- =========================
local top = Instance.new("Frame")
top.Size = UDim2.new(1, -70, 0, 60)
top.Position = UDim2.new(0, 70, 0, 0)
top.BackgroundColor3 = Color3.fromRGB(22,22,22)
top.BorderSizePixel = 0
top.Parent = main

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -120, 1, 0)
title.Position = UDim2.new(0, 15, 0, 0)
title.BackgroundTransparency = 1
title.Text = "DK | HUB"
title.TextColor3 = Color3.fromRGB(255,255,255)
title.Font = Enum.Font.GothamBold
title.TextSize = 22
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = top

-- Botão minimizar
local minimize = Instance.new("TextButton")
minimize.Size = UDim2.new(0, 40, 0, 40)
minimize.Position = UDim2.new(1, -50, 0.5, -20)
minimize.Text = "—"
minimize.Font = Enum.Font.GothamBold
minimize.TextSize = 22
minimize.TextColor3 = Color3.fromRGB(255,255,255)
minimize.BackgroundColor3 = Color3.fromRGB(40,40,40)
minimize.BorderSizePixel = 0
minimize.Parent = top
Instance.new("UICorner", minimize).CornerRadius = UDim.new(1,0)

-- =========================
-- CONTEÚDO
-- =========================
local content = Instance.new("Frame")
content.Size = UDim2.new(1, -90, 1, -80)
content.Position = UDim2.new(0, 80, 0, 70)
content.BackgroundColor3 = Color3.fromRGB(20,20,20)
content.BorderSizePixel = 0
content.Parent = main
Instance.new("UICorner", content).CornerRadius = UDim.new(0,12)

-- =========================
-- MINI HUB (DK)
-- =========================
local mini = Instance.new("Frame")
mini.Size = UDim2.new(0, 60, 0, 60)
mini.Position = lastMiniPosition
mini.BackgroundColor3 = Color3.fromRGB(20,20,20)
mini.BorderSizePixel = 0
mini.Visible = false
mini.Active = true
mini.Draggable = true
mini.Parent = gui
Instance.new("UICorner", mini).CornerRadius = UDim.new(1,0)

-- Salvar posição do mini
mini:GetPropertyChangedSignal("Position"):Connect(function()
	lastMiniPosition = mini.Position
end)

local dkText = Instance.new("TextLabel")
dkText.Size = UDim2.new(1, 0, 1, 0)
dkText.BackgroundTransparency = 1
dkText.Text = "DK"
dkText.TextColor3 = Color3.fromRGB(255,255,255)
dkText.Font = Enum.Font.GothamBlack
dkText.TextSize = 26
dkText.Parent = mini

-- =========================
-- FUNÇÕES
-- =========================
minimize.MouseButton1Click:Connect(function()
	main.Visible = false
	mini.Position = lastMiniPosition
	mini.Visible = true
end)

mini.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		mini.Visible = false
		main.Position = lastMainPosition
		main.Visible = true
	end
end)
