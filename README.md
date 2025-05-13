-- Speed Hack GUI com TextBox RGB (Simples, arrastável, sem Kavo UI)

-- Cria a GUI
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "SpeedGUI"

local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 200, 0, 120)
Frame.Position = UDim2.new(0.5, -100, 0.5, -60)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.Active = true
Frame.Draggable = true

local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Text = "Speed Hack"
Title.TextColor3 = Color3.new(1, 1, 1)
Title.BackgroundTransparency = 1
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 20

local TextBox = Instance.new("TextBox", Frame)
TextBox.Position = UDim2.new(0, 10, 0, 40)
TextBox.Size = UDim2.new(1, -20, 0, 25)
TextBox.PlaceholderText = "Digite a velocidade"
TextBox.Text = ""
TextBox.Font = Enum.Font.SourceSans
TextBox.TextSize = 18
TextBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
TextBox.TextColor3 = Color3.new(1, 1, 1)
TextBox.BorderSizePixel = 2

-- RGB Effect na TextBox
task.spawn(function()
	local hue = 0
	while true do
		hue = (hue + 0.01) % 1
		local color = Color3.fromHSV(hue, 1, 1)
		TextBox.TextColor3 = color
		TextBox.BorderColor3 = color
		task.wait(0.03)
	end
end)

local Button = Instance.new("TextButton", Frame)
Button.Position = UDim2.new(0, 10, 0, 75)
Button.Size = UDim2.new(1, -20, 0, 30)
Button.Text = "Aplicar Speed"
Button.Font = Enum.Font.SourceSansBold
Button.TextSize = 18
Button.BackgroundColor3 = Color3.fromRGB(70, 130, 180)
Button.TextColor3 = Color3.new(1, 1, 1)

-- Função do botão
Button.MouseButton1Click:Connect(function()
	local speed = tonumber(TextBox.Text)
	if speed then
		local char = game.Players.LocalPlayer.Character or game.Players.LocalPlayer.CharacterAdded:Wait()
		local humanoid = char:FindFirstChildOfClass("Humanoid")
		if humanoid then
			humanoid.WalkSpeed = speed
		end
	end
end)
