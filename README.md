-- Hikari Hub Beta
-- by rineunebebe
if game.CoreGui:FindFirstChild("HikariHub") then
    game.CoreGui.HikariHub:Destroy()
end

local gui = Instance.new("ScreenGui")
gui.Parent = game.CoreGui
gui.Name = "HikariHub"
gui.ResetOnSpawn = false

local frame = Instance.new("Frame")
frame.Parent = gui
frame.Size = UDim2.new(0, 260, 0, 240)
frame.Position = UDim2.new(0.1,0,0.2,0)
frame.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
frame.Active = true
frame.Draggable = true

local corner = Instance.new("UICorner", frame)
corner.CornerRadius = UDim.new(0, 8)

local stroke = Instance.new("UIStroke", frame)
stroke.Thickness = 2
stroke.Color = Color3.fromRGB(180, 0, 0)

local title = Instance.new("TextLabel")
title.Parent = frame
title.Size = UDim2.new(1,0,0,30)
title.Text = "HIKARI HUB"
title.Font = Enum.Font.GothamBold
title.TextSize = 18
title.BackgroundTransparency = 1
title.TextColor3 = Color3.fromRGB(200,0,0)

local player = game.Players.LocalPlayer
local UIS = game:GetService("UserInputService")

local function getHumanoid()
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        return player.Character.Humanoid
    end
end

local function MakeButton(text, Y, func)
    local btn = Instance.new("TextButton")
    btn.Parent = frame
    btn.Size = UDim2.new(1, -20, 0, 35)
    btn.Position = UDim2.new(0, 10, 0, Y)
    btn.BackgroundColor3 = Color3.fromRGB(25,0,0)
    btn.Text = text
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.Font = Enum.Font.Gotham
    btn.TextScaled = true
    
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0,6)

    btn.MouseButton1Click:Connect(func)
end

-- ✅ Speed
MakeButton("Speed", 40, function()
    local h = getHumanoid()
    if h then h.WalkSpeed = 32 end
end)

-- ✅ Jump Boost
MakeButton("Jump Boost", 80, function()
    local h = getHumanoid()
    if h then h.JumpPower = 120 end
end)

 -- ✅ Infinite Jump
MakeButton("Infinite Jump", 120, function()
    UIS.JumpRequest:Connect(function()
        local h = getHumanoid()
        if h then
            h:ChangeState(Enum.HumanoidStateType.Jumping)
        end
    end)
end)

-- ✅ Reset
MakeButton("Reset", 160, function()
    local h = getHumanoid()
    if h then
        h.WalkSpeed = 16
        h.JumpPower = 50
    end
end)

-- ✅ Fechar Hub
MakeButton("Close", 200, function()
    gui:Destroy()
end)
