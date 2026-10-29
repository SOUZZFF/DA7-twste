--[[
    omk driver | Versão Completa
    Compatível com PC e Mobile
]]

-- ==================== ANTI AFK ====================
warn("Anti afk running")
game:GetService("Players").LocalPlayer.Idled:Connect(function()
    warn("Anti afk ran")
    game:GetService("VirtualUser"):CaptureController()
    game:GetService("VirtualUser"):ClickButton2(Vector2.new())
end)

-- ==================== MENU ====================
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Orion/main/source"))()

local Window = OrionLib:MakeWindow({
    Name = "omk driver",
    HidePremium = true,
    SaveConfig = false,
    IntroEnabled = false
})

local MainTab = Window:MakeTab({
    Name = "Main",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- ==================== SPEED ====================
getfenv().speed = 500
getfenv().boostMultiplier = 1

MainTab:AddTextbox({
    Name = "Enter Vehicle Speed",
    Default = "500",
    TextDisappear = false,
    Callback = function(Value)
        local num = tonumber(Value)
        if num then
            getfenv().speed = num
            warn("Speed setada para: " .. num)
        end
    end
})

-- ==================== SPEED BOOST EXTRA ====================
MainTab:AddToggle({
    Name = "Speed Boost Extra",
    Default = false,
    Callback = function(state)
        getfenv().speedBoost = state
        getfenv().boostMultiplier = state and 2.2 or 1
        warn(state and "Speed Boost Extra ATIVADO" or "Speed Boost Extra DESATIVADO")
    end
})

-- ==================== INFINITE NITRO ====================
MainTab:AddToggle({
    Name = "Infinite Nitro",
    Default = false,
    Callback = function(state)
        getfenv().infNitro = state
        warn(state and "Infinite Nitro ATIVADO" or "Infinite Nitro DESATIVADO")
    end
})

task.spawn(function()
    local teclas = {"LeftShift", "LeftControl", "E", "Q", "F"}
    while true do
        task.wait(0.12)
        if getfenv().infNitro then
            for _, tecla in pairs(teclas) do
                pcall(function()
                    game:GetService("VirtualInputManager"):SendKeyEvent(true, tecla, false, game)
                end)
            end
        end
    end
end)

-- ==================== AUTO DRIVE ====================
MainTab:AddToggle({
    Name = "Auto Drive",
    Default = false,
    Callback = function(state)
        getfenv().auto = state
        if state then
            local car = game.Players.LocalPlayer.ReplicationFocus
            if car then
                pcall(function()
                    game.Players.LocalPlayer:RequestStreamAroundAsync(Vector3.new(-3531.84521, 36.217411, 1262.63647))
                    task.wait()
                    car:PivotTo(CFrame.new(-3531.84521, 36.217411, 1262.63647, -0.929316938, -7.24218182e-07, 0.36928311, 8.97509338e-08, 1, 2.18700848e-06, -0.36928311, 2.06556751e-06, -0.929316938))
                    task.wait(1)
                    getfenv().btp = car.CFrame
                end)
            end
        end

        while getfenv().auto do
            local car = game.Players.LocalPlayer.ReplicationFocus
            if car and getfenv().btp then
                pcall(function()
                    game:GetService("VirtualInputManager"):SendKeyEvent(true, "W", false, game)
                    local speed = (getfenv().speed or 500) * (getfenv().boostMultiplier or 1)
                    car:PivotTo(getfenv().btp)
                    local dist = (car.Position - CFrame.new(-4049.48584, car.Position.Y, 1018.12622, -0.903568566, 3.80430015e-06, 0.428443521, 2.83321583e-06, 1, -2.90422236e-06, -0.428443521, -1.41029113e-06, -0.903568566).Position).Magnitude
                    local TweenService = game:GetService("TweenService")
                    local TweenInfoToUse = TweenInfo.new(dist / speed, Enum.EasingStyle.Linear, Enum.EasingDirection.InOut, 0, false, 0)
                    local TweenValue = Instance.new("CFrameValue")
                    TweenValue.Value = car.CFrame
                    TweenValue.Changed:Connect(function()
                        car:PivotTo(TweenValue.Value)
                    end)
                    local OnTween = TweenService:Create(TweenValue, TweenInfoToUse, {
                        Value = CFrame.new(-4049.48584, car.Position.Y, 1018.12622, -0.903568566, 3.80430015e-06, 0.428443521, 2.83321583e-06, 1, -2.90422236e-06, -0.428443521, -1.41029113e-06, -0.903568566)
                    })
                    OnTween:Play()
                    OnTween.Completed:Wait()
                    game:GetService("VirtualInputManager"):SendKeyEvent(false, "W", false, game)
                end)
            end
            task.wait()
        end
    end
})

-- ==================== AUTO FARM RACE ====================
getfenv().raceName = "Bridge_Trail"

MainTab:AddTextbox({
    Name = "Nome da Race",
    Default = "Bridge_Trail",
    TextDisappear = false,
    Callback = function(Value)
        getfenv().raceName = Value
        warn("Race setada para: " .. Value)
    end
})

MainTab:AddToggle({
    Name = "Auto Farm Race",
    Default = false,
    Callback = function(state)
        getfenv().autorace = state
        local plr = game.Players.LocalPlayer
        local success, CarSerivce = pcall(function()
            return require(plr.PlayerScripts.TS.CarService.CarService_Client).CarSerivce
        end)
        if not success or not CarSerivce then return end
        local CarInfo = CarSerivce.ActiveCar
        if not CarInfo then return end

        local maxSpeed = 300 * (getfenv().boostMultiplier or 1)

        while getfenv().autorace do
            task.wait()
            if not workspace:FindFirstChild("RaceCheckpoints") then continue end

            if not workspace.RaceCheckpoints:FindFirstChildOfClass("Model") then
                pcall(function()
                    game:GetService("ReplicatedStorage")["events-shared/Definations/Networking/RaceDefinations@GeneralEvents"].EnterRaceQueue:FireServer(getfenv().raceName or "Bridge_Trail", true)
                end)
                task.wait(1)
            else
                for _, v in pairs(workspace.RaceCheckpoints:GetChildren()) do
                    if v:IsA("Model") and v:FindFirstChild("Ring") and v.Ring.Transparency < 1 then
                        pcall(function()
                            local dist = (CarInfo.Body.Position - v.WorldPivot.Position).Magnitude
                            local TweenService = game:GetService("TweenService")
                            local TweenInfoToUse = TweenInfo.new(dist / maxSpeed, Enum.EasingStyle.Linear, Enum.EasingDirection.InOut, 0, false, 0)
                            local TweenValue = Instance.new("CFrameValue")
                            TweenValue.Value = CarInfo.Body.CFrame
                            TweenValue.Changed:Connect(function()
                                CarInfo.Body.CFrame = TweenValue.Value
                                CarInfo.Body.AssemblyLinearVelocity = Vector3.zero
                            end)
                            local tween = TweenService:Create(TweenValue, TweenInfoToUse, {Value = v.WorldPivot})
                            tween:Play()
                            tween.Completed:Wait()
                        end)
                    end
                end
            end
        end
    end
})

-- ==================== BOTÃO FLY MOBILE ====================
local function criarBotaoMobile()
    local PlayerGui = game.Players.LocalPlayer:WaitForChild("PlayerGui")
    if PlayerGui:FindFirstChild("OmkFlyButton") then
        PlayerGui.OmkFlyButton:Destroy()
    end

    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Name = "OmkFlyButton"
    ScreenGui.ResetOnSpawn = false
    ScreenGui.Parent = PlayerGui

    local Button = Instance.new("TextButton")
    Button.Size = UDim2.new(0, 75, 0, 75)
    Button.Position = UDim2.new(0.82, 0, 0.42, 0)
    Button.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    Button.TextColor3 = Color3.fromRGB(255, 255, 255)
    Button.Text = "FLY\nOFF"
    Button.TextScaled = true
    Button.Font = Enum.Font.GothamBold
    Button.Parent = ScreenGui

    local UICorner = Instance.new("UICorner")
    UICorner.CornerRadius = UDim.new(1, 0)
    UICorner.Parent = Button

    local UIStroke = Instance.new("UIStroke")
    UIStroke.Color = Color3.fromRGB(255, 60, 60)
    UIStroke.Thickness = 2.5
    UIStroke.Parent = Button

    local dragging, dragStart, startPos
    Button.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            dragStart = input.Position
            startPos = Button.Position
        end
    end)
    Button.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = false
        end
    end)
    game:GetService("UserInputService").InputChanged:Connect(function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseMovement) then
            local delta = input.Position - dragStart
            Button.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)

    Button.MouseButton1Click:Connect(function()
        getfenv().flyVehicle = not getfenv().flyVehicle
        if getfenv().flyVehicle then
            Button.Text = "FLY\nON"
            Button.BackgroundColor3 = Color3.fromRGB(0, 160, 0)
            UIStroke.Color = Color3.fromRGB(0, 255, 120)
        else
            Button.Text = "FLY\nOFF"
            Button.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
            UIStroke.Color = Color3.fromRGB(255, 60, 60)
        end
    end)
end

criarBotaoMobile()

-- ==================== FLY VEHICLE ====================
MainTab:AddToggle({
    Name = "Fly Vehicle (Mouse/Mobile)",
    Default = false,
    Callback = function(state)
        getfenv().flyVehicle = state
        warn(state and "Fly ATIVADO" or "Fly DESATIVADO")
    end
})

task.spawn(function()
    while true do
        task.wait(0.02)
        if getfenv().flyVehicle then
            local car = game.Players.LocalPlayer.ReplicationFocus
            local cam = workspace.CurrentCamera
            if car and cam then
                pcall(function()
                    local speed = (getfenv().speed or 160) * (getfenv().boostMultiplier or 1)
                    local look = cam.CFrame.LookVector
                    local newPos = car.Position + (look * (speed * 0.155)) + Vector3.new(0, 3.4, 0)
                    car:PivotTo(CFrame.new(newPos, newPos + look))
                    car.AssemblyLinearVelocity = look * speed + Vector3.new(0, 50, 0)
                    car.AssemblyAngularVelocity = Vector3.zero
                end)
            end
        end
    end
end)

OrionLib:Init()
