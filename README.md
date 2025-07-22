local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "BrainrotStealer"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local Button = Instance.new("TextButton")
Button.Size = UDim2.new(0, 160, 0, 50)
Button.Position = UDim2.new(0, 20, 0, 100)
Button.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
Button.TextColor3 = Color3.fromRGB(255, 255, 255)
Button.Text = "Auto Steal [OFF]"
Button.Parent = ScreenGui

local autoSteal = false
local Players = game:GetService("Players")
local player = Players.LocalPlayer

Button.MouseButton1Click:Connect(function()
	autoSteal = not autoSteal
	Button.Text = "Auto Steal [" .. (autoSteal and "ON" or "OFF") .. "]"
end)

-- Função principal
task.spawn(function()
	while true do
		task.wait(1)
		if autoSteal then
			local char = player.Character
			if not char or not char:FindFirstChild("HumanoidRootPart") then continue end
			
			local root = char:FindFirstChild("HumanoidRootPart")
			local brainrot = workspace:FindFirstChild("Brainrot")
			local base = workspace:FindFirstChild("Base")

			if brainrot and base then
				-- Teleporta até o Brainrot
				root.CFrame = brainrot.CFrame + Vector3.new(0, 3, 0)
				task.wait(0.4)

				-- Pega o Brainrot
				brainrot.Parent = char
				brainrot.CFrame = root.CFrame

				task.wait(0.4)

				-- Vai pra base
				root.CFrame = base.CFrame + Vector3.new(0, 3, 0)
				task.wait(0.4)

				-- Solta o Brainrot
				brainrot.Parent = workspace
				brainrot.CFrame = base.CFrame + Vector3.new(0, 2, 0)
			end
		end
	end
end)
