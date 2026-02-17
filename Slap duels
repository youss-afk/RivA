
local LP = game.Players.LocalPlayer
local UIS = game:GetService("UserInputService")
local CoreGui = game:GetService("CoreGui")
local StarterGui = game:GetService("StarterGui")

local CorrectKey = "OP BON" 
local KeyLink = "Https://link-target.net/3632059/aOK5gdpopPx4" 

-- تنظيف النسخ السابقة
for _, v in pairs(CoreGui:GetChildren()) do
    if v.Name == "SlapUltimateFinal" then v:Destroy() end
end

local Gui = Instance.new("ScreenGui", CoreGui)
Gui.Name = "SlapUltimateFinal"

_G.HSize = 15
_G.LockX = false
_G.LockDash = false
local SelectedLang = "AR"

-- وظيفة السحب
local function MakeDraggable(frame, lockVar)
    local dragging, dragInput, dragStart, startPos
    frame.InputBegan:Connect(function(input)
        if (not lockVar or not _G[lockVar]) and (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
            dragging = true; dragStart = input.Position; startPos = frame.Position
            input.Changed:Connect(function() if input.UserInputState == Enum.UserInputState.End then dragging = false end end)
        end
    end)
    frame.InputChanged:Connect(function(input)
        if (not lockVar or not _G[lockVar]) and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then dragInput = input end
    end)
    game:GetService("RunService").RenderStepped:Connect(function()
        if dragging and dragInput and (not lockVar or not _G[lockVar]) then
            local delta = dragInput.Position - dragStart
            frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)
end

-- [ دالة السكربت الرئيسي بعد المفتاح واللغة ]
local function Launch(lang)
    SelectedLang = lang
    
    local ExternalBtn = Instance.new("TextButton", Gui)
    ExternalBtn.Size = UDim2.new(0, 60, 0, 60); ExternalBtn.Position = UDim2.new(0.05, 0, 0.2, 0)
    ExternalBtn.Text = "X"; ExternalBtn.BackgroundColor3 = Color3.fromRGB(200, 0, 0); ExternalBtn.TextColor3 = Color3.new(1, 1, 1)
    ExternalBtn.Font = Enum.Font.GothamBold; ExternalBtn.TextSize = 30; Instance.new("UICorner", ExternalBtn); MakeDraggable(ExternalBtn, "LockX")

    local DashBtn = Instance.new("TextButton", Gui)
    DashBtn.Size = UDim2.new(0, 85, 0, 85); DashBtn.Position = UDim2.new(0.75, 0, 0.1, 0)
    DashBtn.Text = "DASH"; DashBtn.BackgroundColor3 = Color3.fromRGB(255, 0, 0); DashBtn.TextColor3 = Color3.new(1, 1, 1)
    DashBtn.Font = Enum.Font.GothamBold; DashBtn.TextSize = 20; DashBtn.Visible = false; DashBtn.BackgroundTransparency = 0.2
    Instance.new("UICorner", DashBtn); MakeDraggable(DashBtn, "LockDash")

    local Main = Instance.new("Frame", Gui)
    Main.Size = UDim2.new(0, 280, 0, 550); Main.Position = UDim2.new(0.5, -140, 0.25, 0)
    Main.BackgroundColor3 = Color3.fromRGB(20, 20, 20); Main.Visible = true; Main.Active = true
    Instance.new("UICorner", Main); local MStroke = Instance.new("UIStroke", Main); MStroke.Color = Color3.fromRGB(255, 0, 0); MStroke.Thickness = 2
    MakeDraggable(Main)

    local MTitle = Instance.new("TextLabel", Main)
    MTitle.Size = UDim2.new(1, 0, 0, 55); MTitle.BackgroundColor3 = Color3.fromRGB(255, 0, 0); MTitle.TextColor3 = Color3.new(1,1,1)
    MTitle.TextSize = 22; MTitle.Font = Enum.Font.GothamBold; MTitle.Text = lang == "AR" and "سكربت سلب ديولز" or "SLAP DUELS SCRIPT"
    Instance.new("UICorner", MTitle)

    local Container = Instance.new("ScrollingFrame", Main)
    Container.Size = UDim2.new(1, 0, 1, -60); Container.Position = UDim2.new(0, 0, 0, 60); Container.BackgroundTransparency = 1; Container.ScrollBarThickness = 3
    local Layout = Instance.new("UIListLayout", Container); Layout.Padding = UDim.new(0, 10); Layout.HorizontalAlignment = Enum.HorizontalAlignment.Center

    ExternalBtn.MouseButton1Click:Connect(function() Main.Visible = not Main.Visible end)

    -- [[ برمجة زر الداش بقوة 70 ]]
    DashBtn.MouseButton1Click:Connect(function()
        if _G.DashEnabled and LP.Character and LP.Character:FindFirstChild("HumanoidRootPart") then
            local v = Instance.new("BodyVelocity", LP.Character.HumanoidRootPart)
            v.MaxForce = Vector3.new(1e6, 1e6, 1e6); v.Velocity = LP.Character.HumanoidRootPart.CFrame.LookVector * 70
            task.wait(0.12); v:Destroy()
        end
    end)

    local function AddToggle(nameAr, nameEn, callback)
        local btn = Instance.new("TextButton", Container)
        btn.Size = UDim2.new(0.9, 0, 0, 45); btn.BackgroundColor3 = Color3.fromRGB(40, 40, 40); btn.TextColor3 = Color3.new(1,1,1)
        btn.Font = Enum.Font.GothamBold; btn.TextSize = 18; Instance.new("UICorner", btn)
        local enabled = false
        local function updateText() btn.Text = (SelectedLang == "AR" and nameAr or nameEn) .. (enabled and " [ON]" or " [OFF]") end
        btn.MouseButton1Click:Connect(function()
            enabled = not enabled
            btn.BackgroundColor3 = enabled and Color3.fromRGB(180, 0, 0) or Color3.fromRGB(40, 40, 40)
            updateText(); callback(enabled)
        end)
        updateText()
    end

    -- المميزات
    AddToggle("تفعيل الهيتبوكس", "Enable Hitbox", function(state)
        _G.HitEnabled = state
        if state then
            task.spawn(function()
                while _G.HitEnabled do
                    for _, v in pairs(game.Players:GetPlayers()) do
                        if v ~= LP and v.Character and v.Character:FindFirstChild("HumanoidRootPart") then
                            v.Character.HumanoidRootPart.Size = Vector3.new(_G.HSize, _G.HSize, _G.HSize)
                            v.Character.HumanoidRootPart.Transparency = 0.7
                        end
                    end
                    task.wait(0.5)
                end
            end)
        end
    end)

    local HitboxSizeInput = Instance.new("TextBox", Container)
    HitboxSizeInput.Size = UDim2.new(0.9, 0, 0, 40); HitboxSizeInput.BackgroundColor3 = Color3.fromRGB(30, 30, 30); HitboxSizeInput.TextColor3 = Color3.new(1, 1, 1)
    HitboxSizeInput.Font = Enum.Font.GothamBold; HitboxSizeInput.TextSize = 16
    HitboxSizeInput.PlaceholderText = lang == "AR" and "حجم الهيتبوكس" or "Hitbox Size"
    HitboxSizeInput.Text = tostring(_G.HSize); Instance.new("UICorner", HitboxSizeInput)
    HitboxSizeInput.FocusLost:Connect(function() local val = tonumber(HitboxSizeInput.Text) if val then _G.HSize = val end end)

    AddToggle("انتقال لمنصة الخصم", "TP Win Enemy", function(state)
        _G.TPWin = state
        task.spawn(function()
            while _G.TPWin do
                pcall(function()
                    local furthest, maxDist = nil, 0
                    local myPos = LP.Character.HumanoidRootPart.Position
                    for _, v in pairs(game.Workspace:GetDescendants()) do
                        if v:IsA("BasePart") and v.Color == Color3.fromRGB(0, 255, 0) and v.Size.X > 5 then
                            local d = (v.Position - myPos).Magnitude
                            if d > maxDist then maxDist = d; furthest = v end
                        end
                    end
                    if furthest then LP.Character.HumanoidRootPart.CFrame = furthest.CFrame + Vector3.new(0, 5, 0) end
                end)
                task.wait(0.5)
            end
        end)
    end)

    AddToggle("سرعة اللاعب", "Speed Hack", function(state)
        _G.Speed = state
        task.spawn(function()
            while _G.Speed do if LP.Character then LP.Character.Humanoid.WalkSpeed = 85 end task.wait(0.1) end
            if LP.Character then LP.Character.Humanoid.WalkSpeed = 16 end
        end)
    end)
    AddToggle("قفز لا نهائي", "Infinite Jump", function(state)
        _G.Jump = state
        UIS.JumpRequest:Connect(function() if _G.Jump then LP.Character.Humanoid:ChangeState("Jumping") end end)
    end)
    AddToggle("تفعيل زر الاندفاع", "Enable Dash", function(state) _G.DashEnabled = state; DashBtn.Visible = state end)
    AddToggle("قفل تحريك زر X", "Lock X Button", function(state) _G.LockX = state end)
    AddToggle("قفل تحريك زر الاندفاع", "Lock Dash Button", function(state) _G.LockDash = state end)
end

-- [ نافذة اختيار اللغة ]
local function ShowLanguageLoader()
    local Loader = Instance.new("Frame", Gui)
    Loader.Size = UDim2.new(0, 320, 0, 180); Loader.Position = UDim2.new(0.5, -160, 0.4, 0)
    Loader.BackgroundColor3 = Color3.fromRGB(15, 15, 15); Instance.new("UICorner", Loader)

    local LoaderTitle = Instance.new("TextLabel", Loader)
    LoaderTitle.Size = UDim2.new(1, 0, 0, 40); LoaderTitle.Text = "Choose Language / اختر اللغة"; LoaderTitle.TextColor3 = Color3.new(1,1,1)
    LoaderTitle.BackgroundTransparency = 1; LoaderTitle.Font = Enum.Font.GothamBold; LoaderTitle.TextSize = 16

    local ArBtn = Instance.new("TextButton", Loader)
    ArBtn.Size = UDim2.new(0.4, 0, 0, 50); ArBtn.Position = UDim2.new(0.07, 0, 0.45, 0); ArBtn.Text = "العربية"
    ArBtn.BackgroundColor3 = Color3.fromRGB(180, 0, 0); ArBtn.TextColor3 = Color3.new(1, 1, 1); ArBtn.Font = Enum.Font.GothamBold; ArBtn.TextSize = 20
    Instance.new("UICorner", ArBtn)
    ArBtn.MouseButton1Click:Connect(function() Loader:Destroy(); Launch("AR") end)

    local EnBtn = Instance.new("TextButton", Loader)
    EnBtn.Size = UDim2.new(0.4, 0, 0, 50); EnBtn.Position = UDim2.new(0.53, 0, 0.45, 0); EnBtn.Text = "English"
    EnBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40); EnBtn.TextColor3 = Color3.new(1, 1, 1); EnBtn.Font = Enum.Font.GothamBold; EnBtn.TextSize = 20
    Instance.new("UICorner", EnBtn)
    EnBtn.MouseButton1Click:Connect(function() Loader:Destroy(); Launch("EN") end)
end

-- [ نافذة المفتاح ]
local AuthFrame = Instance.new("Frame", Gui)
AuthFrame.Size = UDim2.new(0, 320, 0, 240); AuthFrame.Position = UDim2.new(0.5, -160, 0.4, 0)
AuthFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25); Instance.new("UICorner", AuthFrame)

local TTitle = Instance.new("TextLabel", AuthFrame)
TTitle.Size = UDim2.new(1, 0, 0, 50); TTitle.Text = "SLAP DUELS | AUTH"; TTitle.TextColor3 = Color3.new(1,1,1)
TTitle.Font = Enum.Font.GothamBold; TTitle.BackgroundTransparency = 1; TTitle.TextSize = 18

local Box = Instance.new("TextBox", AuthFrame)
Box.Size = UDim2.new(0.9, 0, 0, 50); Box.Position = UDim2.new(0.05, 0, 0.35, 0)
Box.PlaceholderText = "Enter Key..."; Box.Text = ""; Box.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Box.TextColor3 = Color3.new(1,1,1); Box.TextScaled = true; Instance.new("UICorner", Box)

local BtnCheck = Instance.new("TextButton", AuthFrame)
BtnCheck.Size = UDim2.new(0.43, 0, 0, 45); BtnCheck.Position = UDim2.new(0.05, 0, 0.7, 0)
BtnCheck.Text = "CHECK"; BtnCheck.BackgroundColor3 = Color3.fromRGB(0, 150, 0); BtnCheck.TextColor3 = Color3.new(1,1,1)
BtnCheck.Font = Enum.Font.GothamBold; Instance.new("UICorner", BtnCheck)

local BtnGet = Instance.new("TextButton", AuthFrame)
BtnGet.Size = UDim2.new(0.43, 0, 0, 45); BtnGet.Position = UDim2.new(0.52, 0, 0.7, 0)
BtnGet.Text = "GET KEY"; BtnGet.BackgroundColor3 = Color3.fromRGB(180, 0, 0); BtnGet.TextColor3 = Color3.new(1,1,1)
BtnGet.Font = Enum.Font.GothamBold; Instance.new("UICorner", BtnGet)

BtnCheck.MouseButton1Click:Connect(function()
    if Box.Text == CorrectKey then
        StarterGui:SetCore("SendNotification", {Title = "Success", Text = "Key Verified!", Duration = 5})
        AuthFrame:Destroy(); ShowLanguageLoader()
    else
        Box.Text = ""; Box.PlaceholderText = "WRONG KEY! ❌"
    end
end)

BtnGet.MouseButton1Click:Connect(function()
    setclipboard(KeyLink); Box.Text = KeyLink; BtnGet.Text = "COPIED!"
    task.wait(2); BtnGet.Text = "GET KEY"
end)

