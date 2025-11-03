-- MASSIVE BLACK LAYER LOCK SYSTEM (sem pausas)
local N = 900000 -- cuidado: valor grande pode travar MUITO
local correctKey = "minhaKey123"

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ThickDarkLayers"
screenGui.ResetOnSpawn = false
screenGui.DisplayOrder = 999999
screenGui.Parent = playerGui

local function freeze()
	local char = player.Character or player.CharacterAdded:Wait()
	local humanoid = char:WaitForChild("Humanoid")
	local root = char:WaitForChild("HumanoidRootPart")
	humanoid.WalkSpeed = 0
	humanoid.JumpPower = 0
	root.Anchored = true
	workspace.CurrentCamera.CameraType = Enum.CameraType.Scriptable
end

local function unfreeze()
	local char = player.Character or player.CharacterAdded:Wait()
	local humanoid = char:WaitForChild("Humanoid")
	local root = char:WaitForChild("HumanoidRootPart")
	humanoid.WalkSpeed = 16
	humanoid.JumpPower = 50
	root.Anchored = false
	workspace.CurrentCamera.CameraType = Enum.CameraType.Custom
end

freeze()

for i = 1, N do
	local frame = Instance.new("Frame")
	frame.Name = "Layer_" .. i
	frame.Size = UDim2.new(1, 0, 1, 0)
	frame.Position = UDim2.new(0, 0, 0, 0)
	frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
	frame.BorderSizePixel = 8
	frame.BorderColor3 = Color3.fromRGB(10, 10, 10)
	frame.BackgroundTransparency = 0
	frame.ZIndex = 1000000 + i
	frame.Active = true
	frame.Selectable = true
	frame.Parent = screenGui
end

-- tela da key
local keyFrame = Instance.new("Frame")
keyFrame.Size = UDim2.new(1, 0, 1, 0)
keyFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
keyFrame.BackgroundTransparency = 0
keyFrame.ZIndex = 1000000 + N + 10
keyFrame.Parent = screenGui

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 60)
title.Position = UDim2.new(0, 0, 0.25, 0)
title.BackgroundTransparency = 1
title.Text = "🔒 SISTEMA DE KEY 🔒"
title.Font = Enum.Font.GothamBold
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextSize = 30
title.ZIndex = keyFrame.ZIndex + 1
title.Parent = keyFrame

local keyBox = Instance.new("TextBox")
keyBox.Size = UDim2.new(0, 400, 0, 50)
keyBox.Position = UDim2.new(0.5, -200, 0.45, 0)
keyBox.PlaceholderText = "Digite a Key..."
keyBox.Font = Enum.Font.Gotham
keyBox.TextSize = 22
keyBox.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
keyBox.BorderSizePixel = 3
keyBox.BorderColor3 = Color3.fromRGB(60, 60, 60)
keyBox.TextColor3 = Color3.fromRGB(255, 255, 255)
keyBox.ZIndex = keyFrame.ZIndex + 1
keyBox.Parent = keyFrame

local confirm = Instance.new("TextButton")
confirm.Size = UDim2.new(0, 200, 0, 50)
confirm.Position = UDim2.new(0.5, -100, 0.55, 60)
confirm.Text = "Confirmar Key"
confirm.Font = Enum.Font.GothamBold
confirm.TextSize = 20
confirm.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
confirm.TextColor3 = Color3.fromRGB(255, 255, 255)
confirm.ZIndex = keyFrame.ZIndex + 1
confirm.Parent = keyFrame

confirm.MouseButton1Click:Connect(function()
	if keyBox.Text == correctKey then
		unfreeze()
		screenGui:Destroy()
	else
		confirm.Text = "❌ Key Errada"
		task.wait(1.5)
		confirm.Text = "Confirmar Key"
	end
end)# Teste-100
