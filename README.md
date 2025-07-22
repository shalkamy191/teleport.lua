-- main.lua (this is what gets loaded after key check)
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local ScreenGui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
ScreenGui.Name = "GodGui"

local Toggle = Instance.new("TextButton", ScreenGui)
Toggle.Size = UDim2.new(0, 100, 0, 30)
Toggle.Position = UDim2.new(0, 10, 0, 10)
Toggle.Text = "ESP: OFF"

local enabled = false
local boxes = {}

function updateESP()
    for i, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local box = Drawing.new("Text")
            box.Text = player.Name
            box.Position = Vector2.new(300, 300)
            box.Color = Color3.new(1, 1, 1)
            box.Visible = enabled
            boxes[player.Name] = box
        end
    end
end

Toggle.MouseButton1Click:Connect(function()
    enabled = not enabled
    Toggle.Text = "ESP: " .. (enabled and "ON" or "OFF")
    updateESP()
end)
