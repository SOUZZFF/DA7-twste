--[[
    VENOM HAVEN
    Brookhaven RP Hub
    Criado do zero - Novembro 2026
]]

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local Lighting = game:GetService("Lighting")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera
local Mouse = LocalPlayer:GetMouse()

-- Estado
local States = {
    ESP = false,
    Fly = false,
    Speed = false,
    Noclip = false,
    InfJump = false,
    AntiFling = false,
    Fullbright = false
}

local FlySpeed = 50
local WalkSpeed = 50
local ESPObjects = {}
local Connections = {}

-- Limpar
local function ClearESP()
    for _, v in pairs(ESPObjects) do
        if v and v.Parent then v:Destroy() end
    end
    ESPObjects = {}
end

-- ESP
local function CreateESP(player)
    if player == LocalPlayer then return end
    local character = player.Character
    if not character then return end
    local root = character:FindFirstChild("HumanoidRootPart")
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    if not root or not humanoid then return end

    local billboard = Instance.new("BillboardGui")
    billboard.Name = "VenomESP"
    billboard.Adornee = root
    billboard.Size = UDim2.new(0, 200, 0, 50)
    billboard.StudsOffset = Vector3.new(0, 3, 0)
    billboard.AlwaysOnTop = true
    billboard.Parent = character

    local nameLabel = Instance.new("TextLabel")
    nameLabel.Size = UDim2.new(1, 0, 0.5, 0)
    nameLabel.BackgroundTransparency = 1
    nameLabel.Text = player.Name
    nameLabel.TextColor3 = Color3.fromRGB(180, 100, 255)
    nameLabel.TextStrokeTransparency = 0.5
    nameLabel.Font = Enum.Font.GothamBold
    nameLabel.TextSize = 14
    nameLabel.Parent = billboard

    local distLabel = Instance.new("TextLabel")
    distLabel.Size = UDim2.new(1, 0, 0.5, 0)
    distLabel.Position = UDim2.new(0, 0, 0.5, 0)
    distLabel.BackgroundTransparency = 1
    distLabel.TextColor3 = Color3.fromRGB(200, 200, 255)
    distLabel.TextStrokeTransparency = 0.6
    distLabel.Font = Enum.Font.Gotham
    distLabel.TextSize = 12
    distLabel.Parent = billboard

    local box = Instance.new("BoxHandleAdornment")
    box.Name = "VenomBox"
    box.Adornee = root
    box.AlwaysOnTop = true
    box.ZIndex = 5
    box.Size = character:GetExtentsSize()
    box.Transparency = 0.6
    box.Color3 = Color3.fromRGB(160, 80, 255)
    box.Parent = character

    table.insert(ESPObjects, billboard)
    table.insert(ESPObjects, box)

    local conn
    conn = RunService.RenderStepped:Connect(function()
        if not States.ESP or not character.Parent or not root.Parent then
            if conn then conn:Disconnect() end
            return
        end
        local dist = (LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") and (LocalPlayer.Character.HumanoidRootPart.Position - root.Position).Magnitude) or 0
        distLabel.Text = math.floor(dist) .. "m | HP: " .. math.floor(humanoid.Health)
        box.Size = character:GetExtentsSize()
    end)
    table.insert(Connections, conn)
end

local function ToggleESP(state)
    States.ESP = state
    ClearESP()
    if state then
        for _, plr in pairs(Players:GetPlayers()) do
            CreateESP(plr)
        end
        table.insert(Connections, Players.PlayerAdded:Connect(function(plr)
            plr.CharacterAdded:Connect(function()
                task.wait(1)
                if States.ESP then CreateESP(plr) end
            end)
        end))
    end
end

-- Fly
local BodyGyro, BodyVelocity
local function ToggleFly(state)
    States.Fly = state
    local char = LocalPlayer.Character
    if not char then return end
    local root = char:FindFirstChild("HumanoidRootPart")
    local humanoid = char:FindFirstChildOfClass("Humanoid")
    if not root or not humanoid then return end

    if state then
        humanoid.PlatformStand = true
        BodyGyro = Instance.new("BodyGyro")
        BodyGyro.P = 9e4
        BodyGyro.MaxTorque = Vector3.new(9e9, 9e9, 9e9)
        BodyGyro.CFrame = root.CFrame
        BodyGyro.Parent = root

        BodyVelocity = Instance.new("BodyVelocity")
        BodyVelocity.Velocity = Vector3.new(0, 0, 0)
        BodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9)
        BodyVelocity.Parent = root

        table.insert(Connections, RunService.RenderStepped:Connect(function()
            if not States.Fly then return end
            local camCF = Camera.CFrame
            local direction = Vector3.new()
            if UserInputService:IsKeyDown(Enum.KeyCode.W) then direction = direction + camCF.LookVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.S) then direction = direction - camCF.LookVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.A) then direction = direction - camCF.RightVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.D) then direction = direction + camCF.RightVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.Space) then direction = direction + Vector3.new(0, 1, 0) end
            if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then direction = direction - Vector3.new(0, 1, 0) end
            BodyVelocity.Velocity = direction.Unit * FlySpeed
            if direction.Magnitude < 0.1 then BodyVelocity.Velocity = Vector3.new(0, 0, 0) end
            BodyGyro.CFrame = camCF
        end))
    else
        if BodyGyro then BodyGyro:Destroy() end
        if BodyVelocity then BodyVelocity:Destroy() end
        humanoid.PlatformStand = false
    end
end

-- Speed
local function ToggleSpeed(state)
    States.Speed = state
    local humanoid = LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
    if humanoid then
        humanoid.WalkSpeed = state and WalkSpeed or 16
    end
end

-- Noclip
local function ToggleNoclip(state)
    States.Noclip = state
    if state then
        table.insert(Connections, RunService.Stepped:Connect(function()
            if not States.Noclip then return end
            local char = LocalPlayer.Character
            if char then
                for _, part in pairs(char:GetDescendants()) do
                    if part:IsA("BasePart") then
                        part.CanCollide = false
                    end
                end
            end
        end))
    end
end

-- Infinite Jump
UserInputService.JumpRequest:Connect(function()
    if States.InfJump and LocalPlayer.Character then
        local humanoid = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        end
    end
end)

-- Fullbright
local function ToggleFullbright(state)
    States.Fullbright = state
    if state then
        Lighting.Brightness = 2
        Lighting.ClockTime = 14
        Lighting.FogEnd = 100000
        Lighting.GlobalShadows = false
        Lighting.OutdoorAmbient = Color3.fromRGB(128, 128, 128)
    else
        Lighting.Brightness = 1
        Lighting.ClockTime = 14
        Lighting.FogEnd = 1000
        Lighting.GlobalShadows = true
    end
end

-- UI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "VenomHaven"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = game:GetService("CoreGui")

local Main = Instance.new("Frame")
Main.Name = "Main"
Main.Size = UDim2.new(0, 320, 0, 420)
Main.Position = UDim2.new(0.5, -160, 0.5, -210)
Main.BackgroundColor3 = Color3.fromRGB(18, 18, 24)
Main.BorderSizePixel = 0
Main.Parent = ScreenGui
Main.Active = true
Main.Draggable = true

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 12)
UICorner.Parent = Main

local Stroke = Instance.new("UIStroke")
Stroke.Color = Color3.fromRGB(140, 70, 255)
Stroke.Thickness = 1.5
Stroke.Transparency = 0.3
Stroke.Parent = Main

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 40)
Title.BackgroundTransparency = 1
Title.Text = "VENOM HAVEN"
Title.Font = Enum.Font.GothamBlack
Title.TextSize = 20
Title.TextColor3 = Color3.fromRGB(180, 120, 255)
Title.Parent = Main

local Sub = Instance.new("TextLabel")
Sub.Size = UDim2.new(1, 0, 0, 20)
Sub.Position = UDim2.new(0, 0, 0, 32)
Sub.BackgroundTransparency = 1
Sub.Text = "Brookhaven • Criado do zero"
Sub.Font = Enum.Font.Gotham
Sub.TextSize = 11
Sub.TextColor3 = Color3.fromRGB(140, 140, 160)
Sub.Parent = Main

local function CreateToggle(name, y, callback)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, -30, 0, 36)
    frame.Position = UDim2.new(0, 15, 0, y)
    frame.BackgroundColor3 = Color3.fromRGB(28, 28, 36)
    frame.Parent = Main

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 8)
    corner.Parent = frame

    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(0.7, 0, 1, 0)
    label.Position = UDim2.new(0, 12, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = name
    label.Font = Enum.Font.GothamMedium
    label.TextSize = 14
    label.TextColor3 = Color3.fromRGB(220, 220, 240)
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = frame

    local toggle = Instance.new("TextButton")
    toggle.Size = UDim2.new(0, 44, 0, 22)
    toggle.Position = UDim2.new(1, -56, 0.5, -11)
    toggle.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
    toggle.Text = ""
    toggle.Parent = frame

    local tCorner = Instance.new("UICorner")
    tCorner.CornerRadius = UDim.new(1, 0)
    tCorner.Parent = toggle

    local circle = Instance.new("Frame")
    circle.Size = UDim2.new(0, 16, 0, 16)
    circle.Position = UDim2.new(0, 3, 0.5, -8)
    circle.BackgroundColor3 = Color3.fromRGB(180, 180, 200)
    circle.Parent = toggle

    local cCorner = Instance.new("UICorner")
    cCorner.CornerRadius = UDim.new(1, 0)
    cCorner.Parent = circle

    local on = false
    toggle.MouseButton1Click:Connect(function()
        on = not on
        local goalPos = on and UDim2.new(1, -19, 0.5, -8) or UDim2.new(0, 3, 0.5, -8)
        local goalColor = on and Color3.fromRGB(140, 70, 255) or Color3.fromRGB(50, 50, 60)
        local circleColor = on and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(180, 180, 200)
        TweenService:Create(circle, TweenInfo.new(0.2), {Position = goalPos, BackgroundColor3 = circleColor}):Play()
        TweenService:Create(toggle, TweenInfo.new(0.2), {BackgroundColor3 = goalColor}):Play()
        callback(on)
    end)
end

CreateToggle("ESP", 70, ToggleESP)
CreateToggle("Fly", 112, ToggleFly)
CreateToggle("Speed", 154, ToggleSpeed)
CreateToggle("Noclip", 196, ToggleNoclip)
CreateToggle("Infinite Jump", 238, function(s) States.InfJump = s end)
CreateToggle("Anti Fling", 280, function(s) States.AntiFling = s end)
CreateToggle("Fullbright", 322, ToggleFullbright)

local Close = Instance.new("TextButton")
Close.Size = UDim2.new(0, 28, 0, 28)
Close.Position = UDim2.new(1, -36, 0, 8)
Close.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
Close.Text = "×"
Close.Font = Enum.Font.GothamBold
Close.TextSize = 18
Close.TextColor3 = Color3.fromRGB(200, 200, 220)
Close.Parent = Main

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 6)
closeCorner.Parent = Close

Close.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
    for _, c in pairs(Connections) do pcall(function() c:Disconnect() end) end
    ClearESP()
    ToggleFly(false)
end)

print("VENOM HAVEN carregado • Brookhaven")
