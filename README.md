local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")# sdfsdfdslocal Flying = false
local Speed = 50ocal BodyGyro = Instance.new("BodyGyro")
local BodyVelocity = Instance.new("BodyVelocity")
ocal BodyGyro = Instance.new("BodyGyro")
local BodyVelocity = Instance.new("BodyVelocity") else  Flying = true
        local Character = LocalPlayer.Character
        if Character and Character:FindFirstChild("HumanoidRootPart") then
            local HRP = Character.HumanoidRootPartBodyGyro = Instance.new("BodyGyro")
            BodyGyro.Parent = HRP
            BodyGyro.MaxTorque = Vector3.new(9e9, 9e9, 9e9)
            BodyGyro.CFrame = HRP.CFrame
            
            BodyVelocity = Instance.new("BodyVelocity")
            BodyVelocity.Parent = HRP
            BodyVelocity.Velocity = Vector3.new(0, 0, 0)
            BodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9)
            
            RunService.RenderStepped:Connect(function()
                if Flying and Character and HRP then
                    BodyGyro.CFrame = HRP.CFrame
                    BodyVelocity.Velocity = HRP.CFrame.LookVector * Speed
                end
            end)
        end
    end
endUserInputService.InputBegan:Connect(function(input, gameProcessed)
    if not gameProcessed and input.KeyCode == Enum.KeyCode.Z then
        ToggleFly()
    end
end)

-- Função para teleportar para peças de armas
function TeleportToParts()
    for _, part in pairs(workspace:GetDescendants()) do
        if part:IsA("Part") and string.find(part.Name:lower(), "peça") then
            LocalPlayer.Character:MoveTo(part.Position + Vector3.new(0, 3, 0))
            wait(0.5) -- Pequena pausa para garantir a coleta
        end
    end
endUserInputService.InputBegan:Connect(function(input, gameProcessed)
    if not gameProcessed and input.KeyCode == Enum.KeyCode.X then
        TeleportToParts()
    end
end)

