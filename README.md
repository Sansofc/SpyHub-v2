SpyBub
-- Serviços
local Players = game:GetService("Players")
local StarterGui = game:GetService("StarterGui")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

-- Criar GUI principal
local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.Name = "CustomUI"
screenGui.ResetOnSpawn = false

-- Botão móvel principal (emoji 🤓)
local mainButton = Instance.new("TextButton", screenGui)
mainButton.Size = UDim2.new(0, 60, 0, 60)
mainButton.Position = UDim2.new(0.1, 0, 0.5, 0)
mainButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
mainButton.BackgroundTransparency = 0.1
mainButton.Text = "🤓"
mainButton.Font = Enum.Font.SourceSansBold
mainButton.TextSize = 36
mainButton.TextColor3 = Color3.fromRGB(0, 0, 0)
mainButton.Draggable = true

-- Frame de funções
local frame = Instance.new("Frame", screenGui)
frame.Size = UDim2.new(0, 200, 0, 250)
frame.Position = UDim2.new(0.2, 0, 0.4, 0)
frame.Visible = false
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.BorderSizePixel = 0
frame.BackgroundTransparency = 0.2

-- Função de criação de botão
local function criarBotao(nome, ordem, callback)
	local btn = Instance.new("TextButton", frame)
	btn.Size = UDim2.new(1, -10, 0, 40)
	btn.Position = UDim2.new(0, 5, 0, (ordem - 1) * 45 + 5)
	btn.Text = nome
	btn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
	btn.TextColor3 = Color3.new(1, 1, 1)
	btn.BorderSizePixel = 0
	btn.Font = Enum.Font.SourceSans
	btn.TextSize = 20
	btn.MouseButton1Click:Connect(callback)
end

-- Alternar visibilidade da interface
mainButton.MouseButton1Click:Connect(function()
	frame.Visible = not frame.Visible
end)

-- Botões
criarBotao("Ender tp", 1, function()
	-- Código será adicionado futuramente
	print("Ender tp ativado")
end)

criarBotao("Ender tp test", 2, function()
	-- Código será adicionado futuramente
	print("Ender tp test ativado")
end)

-- ESP: borda branca em todos os players
criarBotao("ESP", 3, function()
	for _, targetPlayer in pairs(Players:GetPlayers()) do
		if targetPlayer ~= player and targetPlayer.Character then
			for _, part in pairs(targetPlayer.Character:GetDescendants()) do
				if part:IsA("BasePart") and not part:FindFirstChild("ESP") then
					local espBox = Instance.new("BoxHandleAdornment")
					espBox.Name = "ESP"
					espBox.Adornee = part
					espBox.Size = part.Size
					espBox.AlwaysOnTop = true
					espBox.ZIndex = 10
					espBox.Transparency = 0.5
					espBox.Color3 = Color3.fromRGB(255, 255, 255)
					espBox.Parent = part
				end
			end
		end
	end
end)

-- Fly (a função ainda será colocada por você)
criarBotao("Fly", 4, function()
	print("Fly ativado")
end)

-- Speed (aumenta a velocidade)
criarBotao("Speed", 5, function()
	humanoid.WalkSpeed = 100 -- Altere o valor como quiser
	print("Speed ativado")
end)
