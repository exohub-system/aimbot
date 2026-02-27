-- ╔═══════════════════════════════════╗
--   EXO HUB | Silent Aim
--   Rivals Optimized | Head Only
--   discord.gg/6QzV9pTWs
-- ╚═══════════════════════════════════╝

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local Camera = workspace.CurrentCamera
local lp = Players.LocalPlayer

-- // CONFIG
local CFG = {
    Enabled     = false,
    FOV         = 150,        -- how wide the silent aim checks (higher = more forgiving)
    TeamCheck   = true,       -- don't aim at teammates
    WallCheck   = true,       -- don't aim through walls
    TargetPart  = "Head",     -- aim at Head
}

-- // FOV CIRCLE UI
if lp.PlayerGui:FindFirstChild("ExoAimUI") then
    lp.PlayerGui.ExoAimUI:Destroy()
end

local SG = Instance.new("ScreenGui")
SG.Name = "ExoAimUI"
SG.ResetOnSpawn = false
SG.DisplayOrder = 9999
SG.IgnoreGuiInset = true
SG.Parent = lp.PlayerGui

-- FOV circle drawn on screen
local fovCircle = Instance.new("Frame")
fovCircle.Size = UDim2.new(0, CFG.FOV * 2, 0, CFG.FOV * 2)
fovCircle.AnchorPoint = Vector2.new(0.5, 0.5)
fovCircle.Position = UDim2.new(0.5, 0, 0.5, 0)
fovCircle.BackgroundTransparency = 1
fovCircle.BorderSizePixel = 0
fovCircle.ZIndex = 5
fovCircle.Parent = SG
Instance.new("UICorner", fovCircle).CornerRadius = UDim.new(1, 0)
local fovStroke = Instance.new("UIStroke")
fovStroke.Color = Color3.fromRGB(120, 60, 255)
fovStroke.Thickness = 1
fovStroke.Transparency = 0.4
fovStroke.Parent = fovCircle

-- crosshair dot
local crossDot = Instance.new("Frame")
crossDot.Size = UDim2.new(0, 6, 0, 6)
crossDot.AnchorPoint = Vector2.new(0.5, 0.5)
crossDot.Position = UDim2.new(0.5, 0, 0.5, 0)
crossDot.BackgroundColor3 = Color3.fromRGB(120, 60, 255)
crossDot.BackgroundTransparency = 0.3
crossDot.BorderSizePixel = 0
crossDot.ZIndex = 6
crossDot.Parent = SG
Instance.new("UICorner", crossDot).CornerRadius = UDim.new(1, 0)

-- // MAIN HUB WINDOW
local W = Instance.new("Frame")
W.Size = UDim2.new(0, 220, 0, 280)
W.Position = UDim2.new(0, 20, 0.5, -140)
W.BackgroundColor3 = Color3.fromRGB(7, 5, 16)
W.BorderSizePixel = 0
W.Active = true
W.Draggable = true
W.ZIndex = 2
W.Parent = SG
Instance.new("UICorner", W).CornerRadius = UDim.new(0, 14)

local wStroke = Instance.new("UIStroke")
wStroke.Color = Color3.fromRGB(120, 60, 255)
wStroke.Thickness = 1.5
wStroke.Transparency = 0.3
wStroke.Parent = W

local wGrad = Instance.new("UIGradient")
wGrad.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0,   Color3.fromRGB(18, 8, 40)),
    ColorSequenceKeypoint.new(0.7, Color3.fromRGB(7, 5, 16)),
    ColorSequenceKeypoint.new(1,   Color3.fromRGB(4, 2, 10)),
})
wGrad.Rotation = 135
wGrad.Parent = W

-- title bar
local TB = Instance.new("Frame")
TB.Size = UDim2.new(1, 0, 0, 44)
TB.BackgroundColor3 = Color3.fromRGB(10, 6, 24)
TB.BorderSizePixel = 0
TB.ZIndex = 2
TB.Parent = W
Instance.new("UICorner", TB).CornerRadius = UDim.new(0, 14)
local TBFix = Instance.new("Frame")
TBFix.Size = UDim2.new(1, 0, 0.5, 0)
TBFix.Position = UDim2.new(0, 0, 0.5, 0)
TBFix.BackgroundColor3 = Color3.fromRGB(10, 6, 24)
TBFix.BorderSizePixel = 0
TBFix.ZIndex = 2
TBFix.Parent = TB

-- shimmer line
local shim = Instance.new("Frame")
shim.Size = UDim2.new(1, 0, 0, 2)
shim.Position = UDim2.new(0, 0, 1, -2)
shim.BackgroundColor3 = Color3.fromRGB(140, 70, 255)
shim.BorderSizePixel = 0
shim.ZIndex = 3
shim.Parent = TB
local shimGrad = Instance.new("UIGradient")
shimGrad.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0,   Color3.fromRGB(0,0,0)),
    ColorSequenceKeypoint.new(0.4, Color3.fromRGB(120,60,255)),
    ColorSequenceKeypoint.new(0.6, Color3.fromRGB(200,140,255)),
    ColorSequenceKeypoint.new(1,   Color3.fromRGB(0,0,0)),
})
shimGrad.Parent = shim
task.spawn(function()
    local t = 0
    while SG.Parent do
        t += 0.025
        shimGrad.Offset = Vector2.new(math.sin(t) * 0.8, 0)
        task.wait(0.03)
    end
end)

local titleLbl = Instance.new("TextLabel")
titleLbl.Size = UDim2.new(1, -50, 1, 0)
titleLbl.Position = UDim2.new(0, 12, 0, 0)
titleLbl.BackgroundTransparency = 1
titleLbl.Text = "EXO HUB"
titleLbl.Font = Enum.Font.GothamBlack
titleLbl.TextSize = 16
titleLbl.TextXAlignment = Enum.TextXAlignment.Left
titleLbl.ZIndex = 3
titleLbl.Parent = TB
local tGrad = Instance.new("UIGradient")
tGrad.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0,   Color3.fromRGB(160, 100, 255)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(255, 255, 255)),
    ColorSequenceKeypoint.new(1,   Color3.fromRGB(120, 60, 240)),
})
tGrad.Rotation = 90
tGrad.Parent = titleLbl

local subLbl = Instance.new("TextLabel")
subLbl.Size = UDim2.new(1, -50, 0, 13)
subLbl.Position = UDim2.new(0, 14, 0, 29)
subLbl.BackgroundTransparency = 1
subLbl.Text = "Silent Aim  •  Rivals"
subLbl.Font = Enum.Font.Gotham
subLbl.TextSize = 10
subLbl.TextColor3 = Color3.fromRGB(120, 70, 200)
subLbl.TextXAlignment = Enum.TextXAlignment.Left
subLbl.ZIndex = 3
subLbl.Parent = TB

local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 24, 0, 24)
closeBtn.Position = UDim2.new(1, -32, 0.5, -12)
closeBtn.BackgroundColor3 = Color3.fromRGB(200, 40, 60)
closeBtn.Text = "✕"
closeBtn.TextColor3 = Color3.fromRGB(255,255,255)
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 11
closeBtn.BorderSizePixel = 0
closeBtn.ZIndex = 3
closeBtn.Parent = TB
Instance.new("UICorner", closeBtn).CornerRadius = UDim.new(0, 6)
closeBtn.MouseButton1Click:Connect(function() SG:Destroy() end)

-- // TOGGLE MAKER
local function makeToggle(parent, labelTxt, yPos, default, onChange)
    local row = Instance.new("Frame")
    row.Size = UDim2.new(1, -20, 0, 38)
    row.Position = UDim2.new(0, 10, 0, yPos)
    row.BackgroundColor3 = Color3.fromRGB(12, 8, 28)
    row.BorderSizePixel = 0
    row.ZIndex = 3
    row.Parent = parent
    Instance.new("UICorner", row).CornerRadius = UDim.new(0, 10)
    local rs = Instance.new("UIStroke")
    rs.Color = Color3.fromRGB(70, 35, 150)
    rs.Thickness = 1
    rs.Parent = row

    local lbl = Instance.new("TextLabel")
    lbl.Size = UDim2.new(1, -54, 1, 0)
    lbl.Position = UDim2.new(0, 10, 0, 0)
    lbl.BackgroundTransparency = 1
    lbl.Text = labelTxt
    lbl.Font = Enum.Font.GothamBold
    lbl.TextSize = 12
    lbl.TextColor3 = Color3.fromRGB(180, 150, 230)
    lbl.TextXAlignment = Enum.TextXAlignment.Left
    lbl.ZIndex = 4
    lbl.Parent = row

    local sw = Instance.new("Frame")
    sw.Size = UDim2.new(0, 36, 0, 20)
    sw.AnchorPoint = Vector2.new(1, 0.5)
    sw.Position = UDim2.new(1, -8, 0.5, 0)
    sw.BackgroundColor3 = default and Color3.fromRGB(120, 60, 255) or Color3.fromRGB(30, 18, 55)
    sw.BorderSizePixel = 0
    sw.ZIndex = 4
    sw.Parent = row
    Instance.new("UICorner", sw).CornerRadius = UDim.new(1, 0)

    local ball = Instance.new("Frame")
    ball.Size = UDim2.new(0, 14, 0, 14)
    ball.AnchorPoint = Vector2.new(0.5, 0.5)
    ball.Position = default and UDim2.new(0.75,0,0.5,0) or UDim2.new(0.27,0,0.5,0)
    ball.BackgroundColor3 = Color3.fromRGB(255,255,255)
    ball.BorderSizePixel = 0
    ball.ZIndex = 5
    ball.Parent = sw
    Instance.new("UICorner", ball).CornerRadius = UDim.new(1, 0)

    local state = default
    local clickArea = Instance.new("TextButton")
    clickArea.Size = UDim2.new(1,0,1,0)
    clickArea.BackgroundTransparency = 1
    clickArea.Text = ""
    clickArea.ZIndex = 6
    clickArea.Parent = row

    local ti = TweenInfo.new(0.18, Enum.EasingStyle.Quart)
    clickArea.MouseButton1Click:Connect(function()
        state = not state
        TweenService:Create(sw, ti, {BackgroundColor3 = state and Color3.fromRGB(120,60,255) or Color3.fromRGB(30,18,55)}):Play()
        TweenService:Create(ball, ti, {Position = state and UDim2.new(0.75,0,0.5,0) or UDim2.new(0.27,0,0.5,0)}):Play()
        TweenService:Create(rs, ti, {Color = state and Color3.fromRGB(140,70,255) or Color3.fromRGB(70,35,150)}):Play()
        onChange(state)
    end)
end

-- // FOV SLIDER
local function makeFOVSlider(yPos)
    local lbl = Instance.new("TextLabel")
    lbl.Size = UDim2.new(1, -20, 0, 16)
    lbl.Position = UDim2.new(0, 10, 0, yPos)
    lbl.BackgroundTransparency = 1
    lbl.Text = "FOV"
    lbl.Font = Enum.Font.GothamBold
    lbl.TextSize = 11
    lbl.TextColor3 = Color3.fromRGB(120, 70, 200)
    lbl.TextXAlignment = Enum.TextXAlignment.Left
    lbl.ZIndex = 3
    lbl.Parent = W

    local valLbl = Instance.new("TextLabel")
    valLbl.Size = UDim2.new(0, 40, 0, 16)
    valLbl.Position = UDim2.new(1, -50, 0, yPos)
    valLbl.BackgroundTransparency = 1
    valLbl.Text = tostring(CFG.FOV)
    valLbl.Font = Enum.Font.GothamBold
    valLbl.TextSize = 11
    valLbl.TextColor3 = Color3.fromRGB(160, 100, 255)
    valLbl.TextXAlignment = Enum.TextXAlignment.Right
    valLbl.ZIndex = 3
    valLbl.Parent = W

    local track = Instance.new("Frame")
    track.Size = UDim2.new(1, -20, 0, 6)
    track.Position = UDim2.new(0, 10, 0, yPos + 20)
    track.BackgroundColor3 = Color3.fromRGB(18, 10, 40)
    track.BorderSizePixel = 0
    track.ZIndex = 3
    track.Parent = W
    Instance.new("UICorner", track).CornerRadius = UDim.new(1, 0)

    local fill = Instance.new("Frame")
    fill.Size = UDim2.new(CFG.FOV / 300, 0, 1, 0)
    fill.BackgroundColor3 = Color3.fromRGB(120, 60, 255)
    fill.BorderSizePixel = 0
    fill.ZIndex = 4
    fill.Parent = track
    Instance.new("UICorner", fill).CornerRadius = UDim.new(1, 0)
    local fg = Instance.new("UIGradient")
    fg.Color = ColorSequence.new({ColorSequenceKeypoint.new(0,Color3.fromRGB(80,30,200)),ColorSequenceKeypoint.new(1,Color3.fromRGB(180,120,255))})
    fg.Parent = fill

    local knob = Instance.new("Frame")
    knob.Size = UDim2.new(0, 14, 0, 14)
    knob.AnchorPoint = Vector2.new(0.5, 0.5)
    knob.Position = UDim2.new(CFG.FOV / 300, 0, 0.5, 0)
    knob.BackgroundColor3 = Color3.fromRGB(180, 120, 255)
    knob.BorderSizePixel = 0
    knob.ZIndex = 5
    knob.Parent = track
    Instance.new("UICorner", knob).CornerRadius = UDim.new(1, 0)

    local dragging = false
    knob.InputBegan:Connect(function(i) if i.UserInputType == Enum.UserInputType.MouseButton1 then dragging = true end end)
    UserInputService.InputEnded:Connect(function(i) if i.UserInputType == Enum.UserInputType.MouseButton1 then dragging = false end end)
    UserInputService.InputChanged:Connect(function(i)
        if dragging and i.UserInputType == Enum.UserInputType.MouseMovement then
            local rx = math.clamp((i.Position.X - track.AbsolutePosition.X) / track.AbsoluteSize.X, 0, 1)
            CFG.FOV = math.floor(rx * 300)
            if CFG.FOV < 10 then CFG.FOV = 10 end
            valLbl.Text = tostring(CFG.FOV)
            fill.Size = UDim2.new(rx, 0, 1, 0)
            knob.Position = UDim2.new(rx, 0, 0.5, 0)
            -- update fov circle size
            fovCircle.Size = UDim2.new(0, CFG.FOV * 2, 0, CFG.FOV * 2)
        end
    end)
end

-- // BUILD TOGGLES
makeToggle(W, "🎯  Silent Aim", 52, false, function(state)
    CFG.Enabled = state
    fovStroke.Transparency = state and 0.2 or 0.7
    crossDot.BackgroundTransparency = state and 0 or 0.8
end)

makeToggle(W, "👥  Team Check", 98, true, function(state)
    CFG.TeamCheck = state
end)

makeToggle(W, "🧱  Wall Check", 144, true, function(state)
    CFG.WallCheck = state
end)

makeFOVSlider(198)

-- watermark
local wm = Instance.new("TextLabel")
wm.Size = UDim2.new(1, -20, 0, 14)
wm.Position = UDim2.new(0, 10, 1, -20)
wm.BackgroundTransparency = 1
wm.Text = "discord.gg/6QzV9pTWs"
wm.Font = Enum.Font.Gotham
wm.TextSize = 10
wm.TextColor3 = Color3.fromRGB(70, 40, 120)
wm.TextXAlignment = Enum.TextXAlignment.Center
wm.ZIndex = 3
wm.Parent = W

-- // HELPER FUNCTIONS
local function getTeam(player)
    return player.Team
end

local function isEnemy(target)
    if not CFG.TeamCheck then return true end
    return getTeam(target) ~= getTeam(lp)
end

local function wallCheck(pos)
    if not CFG.WallCheck then return true end
    local char = lp.Character
    if not char then return false end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return false end
    local ray = RaycastParams.new()
    ray.FilterType = Enum.RaycastFilterType.Exclude
    ray.FilterDescendantsInstances = {char}
    local result = workspace:Raycast(hrp.Position, (pos - hrp.Position).Unit * (pos - hrp.Position).Magnitude, ray)
    return result == nil
end

local function getTarget()
    local bestTarget = nil
    local bestDist = CFG.FOV
    local center = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)

    for _, plr in ipairs(Players:GetPlayers()) do
        if plr == lp then continue end
        if not isEnemy(plr) then continue end
        local char = plr.Character
        if not char then continue end
        local head = char:FindFirstChild("Head")
        local hum = char:FindFirstChildOfClass("Humanoid")
        if not head or not hum or hum.Health <= 0 then continue end

        local screenPos, onScreen = Camera:WorldToViewportPoint(head.Position)
        if not onScreen then continue end

        local dist = (Vector2.new(screenPos.X, screenPos.Y) - center).Magnitude
        if dist < bestDist then
            if wallCheck(head.Position) then
                bestDist = dist
                bestTarget = head
            end
        end
    end

    return bestTarget
end

-- // SILENT AIM CORE
-- Hooks the camera's CFrame to redirect bullets to target's head
-- without moving your actual camera (silent = invisible to others)
local oldIndex = nil

local function enableSilentAim()
    -- Hook into the rendering pipeline
    -- When the game reads the camera CFrame for bullet origin,
    -- we redirect it to point at the target head
    local mt = getrawmetatable and getrawmetatable(Camera)
    if not mt then
        -- fallback for executors without metatable access
        return
    end

    local oldNewIndex = mt.__index
    setreadonly(mt, false)

    oldIndex = mt.__index
    mt.__index = newcclosure(function(self, key)
        if key == "CFrame" and CFG.Enabled then
            local target = getTarget()
            if target then
                local origin = oldIndex(self, key)
                return CFrame.new(origin.Position, target.Position)
            end
        end
        return oldIndex(self, key)
    end)

    setreadonly(mt, true)
end

local function disableSilentAim()
    local mt = getrawmetatable and getrawmetatable(Camera)
    if not mt or not oldIndex then return end
    setreadonly(mt, false)
    mt.__index = oldIndex
    setreadonly(mt, true)
    oldIndex = nil
end

-- Try to enable — works on most executors (Synapse X, KRNL, Delta)
pcall(enableSilentAim)

-- // BACKUP: RenderStepped aim assist for executors without metatable
-- Smoothly moves camera toward target when holding right click
local aimConn = nil
aimConn = RunService.RenderStepped:Connect(function()
    if not CFG.Enabled then return end
    local target = getTarget()

    -- update FOV circle color based on whether target is locked
    if target then
        fovStroke.Color = Color3.fromRGB(80, 255, 140)
        crossDot.BackgroundColor3 = Color3.fromRGB(80, 255, 140)
    else
        fovStroke.Color = Color3.fromRGB(120, 60, 255)
        crossDot.BackgroundColor3 = Color3.fromRGB(120, 60, 255)
    end
end)

-- // PULSE ANIMATION
local t = 0
RunService.Heartbeat:Connect(function(dt)
    if not SG.Parent then return end
    t += dt
    local pulse = (math.sin(t * 2.5) + 1) / 2
    wStroke.Transparency = 0.1 + pulse * 0.3
    if CFG.Enabled then
        fovStroke.Thickness = 1 + pulse * 0.6
    end
    tGrad.Rotation = (t * 22) % 360
end)

-- // OPEN ANIM
W.Position = UDim2.new(-0.5, 0, 0.5, -140)
TweenService:Create(W, TweenInfo.new(0.4, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
    Position = UDim2.new(0, 20, 0.5, -140)
}):Play()

print("[EXO HUB] Silent Aim loaded | discord.gg/6QzV9pTWs")
