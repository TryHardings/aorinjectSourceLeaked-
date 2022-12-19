-- Skidded Script by 6akan / aori


--- Leaked By Rizy and Tokyo

getgenv().keybind = "q"
getgenv().prediction = 0.1258
getgenv().ballistics = 0.35
getgenv().smoothness = 11
getgenv().fovradius = 60
getgenv().Notifications = false
getgenv().SmoothnessValue = true
getgenv().PredictionState = true
getgenv().CamUndergroundResolver = true
getgenv().UnlockWhenTargetDies = false
getgenv().UnlockWhenPlayerDies = false
getgenv().TracerRadius = false
getgenv().GrabbedCheck = true
getgenv().KoCheck = true
getgenv().loaded = false
getgenv().AorinjectSettings = {
    SilentAim = true,
    Prediction = 0.1281,
}
Drawing = Drawing
mousemoverel = mousemoverel

local Settings = {
    Head = "HumanoidRootPart",
    Humanoid = "Humanoid",
    NeckOffSet = Vector3.new(0, tonumber(getgenv().ballistics), 0)
};

local Locking = false
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local Workspace = game:GetService("Workspace")
local GuiService = game:GetService("GuiService")
local RunService = game:GetService("RunService")
local Heartbeat = RunService.Heartbeat
local CurrentCamera = Workspace.CurrentCamera
local Drawingnew, Color3fromRGB, Vector2new = Drawing.new
local Color3fromRGB = Color3.fromRGB
local Vector2new = Vector2.new
local GetGuiInset = GuiService.GetGuiInset
local CharacterAdded = LocalPlayer.CharacterAdded
local CharacterAddedWait = CharacterAdded.Wait
local WorldToViewportPoint = CurrentCamera.WorldToViewportPoint
local RaycastParamsnew = RaycastParams.new
local EnumRaycastFilterTypeBlacklist = Enum.RaycastFilterType.Blacklist
local Raycast = Workspace.Raycast
local GetPlayers = Players.GetPlayers
local Instancenew = Instance.new
local IsDescendantOf = Instancenew("Part").IsDescendantOf
local FindFirstChildWhichIsA = Instancenew("Part").FindFirstChildWhichIsA
local FindFirstChild = Instancenew("Part").FindFirstChild
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local Camera = game:GetService("Workspace").CurrentCamera
local Enemy
local Render_Lock = nil
local FOV_Circle = Drawing.new("Circle")
FOV_Circle.Filled = false
FOV_Circle.Color = Color3.fromRGB(170, 255, 255)
FOV_Circle.Radius = getgenv().fovradius
FOV_Circle.Thickness = 1
FOV_Circle.Visible = false
FOV_Circle.Position = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)
local Move_Circle = nil
local accomidationfactor = 0.1
local aorinjectbase = function(a) 
    rconsoleprint("@@LIGHT_MAGENTA@@") 
    rconsoleprint(a) 
end
local aori, aoricammisc, aorisilmisc = nil, nil, nil
local smoothnessstatus, notifstatus, unlockwhendeadstatus, unlockwhenlocalplayerknockedstatus, tracewhentargetradiusstatus, fovcirclestatus, silentfovcirclestatus  = "false", "false", "false", "false", "false", "false", "false"
local smoothnessvalue, predictionvalue, silpredictionvalue = "Default", "Default", "Default"
local predictionstatus, undergroundresolverstatus, silgrabbedvalue, silkodcheckstatus = "true", "true", "true", "true"
local aorinjectstatus = "Not Loaded"
local silpredictionstatus, silentaimstatus = "Enabled", "Enabled"
local fovvalue = "60"
local silentfovvalue = "40"
local keybindvalue = "q"

getgenv().Aorinject = {
    Enabled = true,
    ShowFOV = false,
    FOV = 40,
    FOVSides = 25,
    FOVColour = Color3fromRGB(255, 255, 255),
    VisibleCheck = true,
    HitChance = 100,
    Selected = nil,
    SelectedPart = nil,
    TargetPart = {"Head", "UpperTorso", "HumanoidRootPart", "LowerTorso", "LeftLowerArm", "RightLowerArm", "LeftUpperArm", "RightUpperArm", "LeftLowerLeg",  "LeftUpperLeg", "RightLowerLeg", "RightUpperLeg"},
}

local circle = Drawingnew("Circle")
circle.Transparency = 0.4
circle.Thickness = 0.8
circle.Color = Aorinject.FOVColour
circle.Filled = false
Aorinject.FOVCircle = circle

function Aorinject.UpdateFOV()
    if not (circle) then
        return
    end
    circle.Visible = Aorinject.ShowFOV
    circle.Radius = Aorinject.FOV
    circle.Position = Vector2new(Mouse.X, Mouse.Y + GetGuiInset(GuiService).Y)
    circle.NumSides = Aorinject.FOVSides
    circle.Color = Aorinject.FOVColour
    return circle
end

function Aorinject.IsPartVisible(Part, PartDescendant)
    local Character = LocalPlayer.Character or CharacterAddedWait(CharacterAdded)
    local Origin = CurrentCamera.CFrame.Position
    local _, OnScreen = WorldToViewportPoint(CurrentCamera, Part.Position)
    if (OnScreen) then
        local raycastParams = RaycastParamsnew()
        raycastParams.FilterType = EnumRaycastFilterTypeBlacklist
        raycastParams.FilterDescendantsInstances = {Character, CurrentCamera}
        local Result = Raycast(Workspace, Origin, Part.Position - Origin, raycastParams)
        if (Result) then
            local PartHit = Result.Instance
            local Visible = (not PartHit or IsDescendantOf(PartHit, PartDescendant))
            return Visible
        end
    end
    return false
end

function Aorinject.Raycast(Origin, Destination, UnitMultiplier)
    if (typeof(Origin) == "Vector3" and typeof(Destination) == "Vector3") then
        if (not UnitMultiplier) then UnitMultiplier = 1 end
        local Direction = (Destination - Origin).Unit * UnitMultiplier
        local Result = Raycast(Workspace, Origin, Direction)
        if (Result) then
            local Normal = Result.Normal
            local Material = Result.Material
            return Direction, Normal, Material
        end
    end
    return nil
end

function Aorinject.Character(Player)
    return Player.Character
end

function Aorinject.CheckHealth(Player)
    local Character = Aorinject.Character(Player)
    local Humanoid = FindFirstChildWhichIsA(Character, "Humanoid")
    local Health = (Humanoid and Humanoid.Health or 0)
    return Health > 0
end

function Aorinject.Check()
    return (Aorinject.Enabled == true and Aorinject.Selected ~= LocalPlayer and Aorinject.SelectedPart ~= nil)
end
Aorinject.checkSilentAim = Aorinject.Check

function Aorinject.GetClosestTargetPartToCursor(Character)
    local TargetParts = Aorinject.TargetPart

    local ClosestPart = nil
    local ClosestPartPosition = nil
    local ClosestPartOnScreen = false
    local ClosestPartMagnitudeFromMouse = nil
    local ShortestDistance = 1/0
    local function CheckTargetPart(TargetPart)
        if (typeof(TargetPart) == "string") then
            TargetPart = FindFirstChild(Character, TargetPart)
        end
        if not (TargetPart) then
            return
        end
        local PartPos, onScreen = WorldToViewportPoint(CurrentCamera, TargetPart.Position)
        local GuiInset = GetGuiInset(GuiService)
        local Magnitude = (Vector2new(PartPos.X, PartPos.Y - GuiInset.Y) - Vector2new(Mouse.X, Mouse.Y)).Magnitude
        if (Magnitude < ShortestDistance) then
            ClosestPart = TargetPart
            ClosestPartPosition = PartPos
            ClosestPartOnScreen = onScreen
            ClosestPartMagnitudeFromMouse = Magnitude
            ShortestDistance = Magnitude
        end
    end
    if (typeof(TargetParts) == "string") then
        if (TargetParts == "All") then
            for _, v in ipairs(Character:GetChildren()) do
                if not (v:IsA("BasePart")) then
                    continue
                end
                CheckTargetPart(v)
            end
        else
            CheckTargetPart(TargetParts)
        end
    end
    if (typeof(TargetParts) == "table") then
        for _, TargetPartName in ipairs(TargetParts) do
            CheckTargetPart(TargetPartName)
        end
    end
    return ClosestPart, ClosestPartPosition, ClosestPartOnScreen, ClosestPartMagnitudeFromMouse
end

function Aorinject.GetClosestPlayerToCursor()
    local TargetPart = nil
    local ClosestPlayer = nil
    local ShortestDistance = 1/0
    for _, Player in ipairs(GetPlayers(Players)) do
        local Character = Aorinject.Character(Player)
        if Character then
            local TargetPartTemp, _, _, Magnitude = Aorinject.GetClosestTargetPartToCursor(Character)
            if (TargetPartTemp and Aorinject.CheckHealth(Player)) then
                if (circle.Radius > Magnitude and Magnitude < ShortestDistance) then
                    if (Aorinject.VisibleCheck and not Aorinject.IsPartVisible(TargetPartTemp, Character)) then continue end
                    ClosestPlayer = Player
                    ShortestDistance = Magnitude
                    TargetPart = TargetPartTemp
                end
            end
        end
    end
    Aorinject.Selected = ClosestPlayer
    Aorinject.SelectedPart = TargetPart
end

Heartbeat:Connect(function()
    Aorinject.UpdateFOV()
    Aorinject.GetClosestPlayerToCursor()
    if Aorinject.Selected and Aorinject.Selected ~= game.Players.LocalPlayer and Aorinject.Selected.Character:WaitForChild("BodyEffects")["K.O"].Value == false and Aorinject.Selected.Character:FindFirstChild("GRABBING_CONSTRAINT") == false then
        Aorinject.SelectedPart.Velocity = Vector3.new(Aorinject.SelectedPart.Velocity.X, 0, Aorinject.SelectedPart.Velocity.Z)
        Aorinject.SelectedPart.AssemblyLinearVelocity = Vector3.new(Aorinject.SelectedPart.Velocity.X, 0, Aorinject.SelectedPart.Velocity.Z)
    end
end) 

Move_Circle = RunService.RenderStepped:Connect(function()
    FOV_Circle.Position = Vector2.new(UserInputService:GetMouseLocation().X, UserInputService:GetMouseLocation().Y)
end)

function InRadius()
    local Target = nil
    local Distance = 9e9
    local Camera = game:GetService("Workspace").CurrentCamera
    for _, v in pairs(Players:GetPlayers()) do
        if v ~= LocalPlayer and v.Character and v.Character[Settings.Head] and v.Character[Settings.Humanoid] and v.Character.BodyEffects['K.O'].Value == false and
            v.Character[Settings.Humanoid].Health > 0 then
            local Enemy = v.Character
            local CastingFrom = CFrame.new(Camera.CFrame.Position, Enemy[Settings.Head].CFrame.Position) *
                                    CFrame.new(0, 0, -4)
            local RayCast = Ray.new(CastingFrom.Position, CastingFrom.LookVector * 9000)
            local World, ToSpace = game:GetService("Workspace"):FindPartOnRayWithIgnoreList(RayCast,
                {LocalPlayer.Character[Settings.Head]});
            local RootWorld = (Enemy[Settings.Head].CFrame.Position - ToSpace).magnitude
            if RootWorld < 4 then
                local RootPartPosition, Visible = Camera:WorldToViewportPoint(Enemy[Settings.Head].Position)
                if Visible then
                    local Real_Magnitude = (Vector2.new(Mouse.X, Mouse.Y) -
                                               Vector2.new(RootPartPosition.X, RootPartPosition.Y)).Magnitude
                    if Real_Magnitude < Distance and Real_Magnitude < FOV_Circle.Radius then
                        Distance = Real_Magnitude
                        Target = Enemy
                    end
                end
            end
        end
    end
    return Target
end
function Aorinject.Check()
    if not (Aorinject.Enabled == true and Aorinject.Selected ~= LocalPlayer and Aorinject.SelectedPart ~= nil) then
        return false
    end
    local Character = Aorinject.Character(Aorinject.Selected)
    local KOd = Character:WaitForChild("BodyEffects")["K.O"].Value
    local Grabbed = Character:FindFirstChild("GRABBING_CONSTRAINT") ~= nil
    if getgenv().GrabbedCheck then
        if Grabbed then
            return false
        end
    end
    if getgenv().KoCheck then
        if KOd then
            return false
        end
    end
    return true
end
function Aimbot()
    pcall(function()
        if Locking then
            local Camera = game:GetService("Workspace").CurrentCamera
            local Predicted_Position = nil
            local GetPositionsFromVector3 = nil
            local Distance = 9e9
            if Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health > 0 and
                getgenv().SmoothnessValue and getgenv().PredictionState then
                Render_Lock = RunService.Stepped:Connect(function()
                    pcall(function()
                        if getgenv().TracerRadius then
                            local RootPartPosition = Camera:WorldToViewportPoint(Enemy[Settings.Head].Position)
                            local Real_Magnitude = (Vector2.new(Mouse.X, Mouse.Y) -
                                                       Vector2.new(RootPartPosition.X, RootPartPosition.Y)).Magnitude
                            if Real_Magnitude < Distance and Real_Magnitude < FOV_Circle.Radius then
                                if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and
                                    Enemy[Settings.Humanoid].Health > 0 and getgenv().CamUndergroundResolver then
                                    local hrp = Enemy.HumanoidRootPart
                                    hrp.Velocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                    hrp.AssemblyLinearVelocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                end
                                if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and
                                    Enemy[Settings.Humanoid].Health > 0 then
                                    Predicted_Position = Enemy[Settings.Head].Position +
                                                             (Enemy[Settings.Head].AssemblyLinearVelocity *
                                                                 getgenv().prediction + Settings.NeckOffSet)
                                    GetPositionsFromVector3 = Camera:WorldToScreenPoint(Predicted_Position)
                                    mousemoverel((GetPositionsFromVector3.X - Mouse.X) / getgenv().smoothness,
                                        (GetPositionsFromVector3.Y - Mouse.Y) / getgenv().smoothness)
                                elseif Locking == false then
                                    Enemy = nil
                                elseif Enemy == nil then
                                    Locking = false
                                end
                            end
                        elseif getgenv().TracerRadius == false then
                            if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health >
                                0 and getgenv().CamUndergroundResolver then
                                local hrp = Enemy.HumanoidRootPart
                                hrp.Velocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                hrp.AssemblyLinearVelocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                            end
                            if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health >
                                0 then
                                Predicted_Position = Enemy[Settings.Head].Position +
                                                         (Enemy[Settings.Head].AssemblyLinearVelocity *
                                                             getgenv().prediction + Settings.NeckOffSet)
                                GetPositionsFromVector3 = Camera:WorldToScreenPoint(Predicted_Position)
                                mousemoverel((GetPositionsFromVector3.X - Mouse.X) / getgenv().smoothness,
                                    (GetPositionsFromVector3.Y - Mouse.Y) / getgenv().smoothness)
                            elseif Locking == false then
                                Enemy = nil
                            elseif Enemy == nil then
                                Locking = false
                            end
                        end
                    end)
                end)
            elseif Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health > 0 and
                getgenv().SmoothnessValue == false and getgenv().PredictionState then
                Render_Lock = RunService.Stepped:Connect(function()
                    pcall(function()
                        if getgenv().TracerRadius then
                            local RootPartPosition = Camera:WorldToViewportPoint(Enemy[Settings.Head].Position)
                            local Real_Magnitude = (Vector2.new(Mouse.X, Mouse.Y) -
                                                       Vector2.new(RootPartPosition.X, RootPartPosition.Y)).Magnitude
                            if Real_Magnitude < Distance and Real_Magnitude < FOV_Circle.Radius then
                                if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and
                                    Enemy[Settings.Humanoid].Health > 0 and getgenv().CamUndergroundResolver then
                                    local hrp = Enemy.HumanoidRootPart
                                    hrp.Velocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                    hrp.AssemblyLinearVelocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                end
                                if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and
                                    Enemy[Settings.Humanoid].Health > 0 then
                                    Predicted_Position = Enemy[Settings.Head].Position +
                                                             (Enemy[Settings.Head].AssemblyLinearVelocity *
                                                                 getgenv().prediction + Settings.NeckOffSet)
                                    GetPositionsFromVector3 = Camera:WorldToScreenPoint(Predicted_Position)
                                    mousemoverel((GetPositionsFromVector3.X - Mouse.X) / 0.55,
                                        (GetPositionsFromVector3.Y - Mouse.Y) / 0.55)
                                elseif Locking == false then
                                    Enemy = nil
                                elseif Enemy == nil then
                                    Locking = false
                                end
                            end
                        elseif getgenv().TracerRadius == false then
                            if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health >
                                0 and getgenv().CamUndergroundResolver then
                                local hrp = Enemy.HumanoidRootPart
                                hrp.Velocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                hrp.AssemblyLinearVelocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                            end
                            if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health >
                                0 then
                                Predicted_Position = Enemy[Settings.Head].Position +
                                                         (Enemy[Settings.Head].AssemblyLinearVelocity *
                                                             getgenv().prediction + Settings.NeckOffSet)
                                GetPositionsFromVector3 = Camera:WorldToScreenPoint(Predicted_Position)
                                mousemoverel((GetPositionsFromVector3.X - Mouse.X) / 0.55,
                                    (GetPositionsFromVector3.Y - Mouse.Y) / 0.55)
                            elseif Locking == false then
                                Enemy = nil
                            elseif Enemy == nil then
                                Locking = false
                            end
                        end
                    end)
                end)
            elseif Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health > 0 and
                getgenv().SmoothnessValue and getgenv().PredictionState == false then
                Render_Lock = RunService.Stepped:Connect(function()
                    pcall(function()
                        if getgenv().TracerRadius then
                            local RootPartPosition = Camera:WorldToViewportPoint(Enemy[Settings.Head].Position)
                            local Real_Magnitude = (Vector2.new(Mouse.X, Mouse.Y) -
                                                       Vector2.new(RootPartPosition.X, RootPartPosition.Y)).Magnitude
                            if Real_Magnitude < Distance and Real_Magnitude < FOV_Circle.Radius then
                                if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and
                                    Enemy[Settings.Humanoid].Health > 0 and getgenv().CamUndergroundResolver then
                                    local hrp = Enemy.HumanoidRootPart
                                    hrp.Velocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                    hrp.AssemblyLinearVelocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                end
                                if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and
                                    Enemy[Settings.Humanoid].Health > 0 then
                                    Predicted_Position = Enemy[Settings.Head].Position
                                    GetPositionsFromVector3 = Camera:WorldToScreenPoint(Predicted_Position)
                                    mousemoverel((GetPositionsFromVector3.X - Mouse.X) / getgenv().smoothness,
                                        (GetPositionsFromVector3.Y - Mouse.Y) / getgenv().smoothness)
                                elseif Locking == false then
                                    Enemy = nil
                                elseif Enemy == nil then
                                    Locking = false
                                end
                            end
                        elseif getgenv().TracerRadius == false then
                            if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health >
                                0 and getgenv().CamUndergroundResolver then
                                local hrp = Enemy.HumanoidRootPart
                                hrp.Velocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                hrp.AssemblyLinearVelocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                            end
                            if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health >
                                0 then
                                Predicted_Position = Enemy[Settings.Head].Position
                                GetPositionsFromVector3 = Camera:WorldToScreenPoint(Predicted_Position)
                                mousemoverel((GetPositionsFromVector3.X - Mouse.X) / getgenv().smoothness,
                                    (GetPositionsFromVector3.Y - Mouse.Y) / getgenv().smoothness)
                            elseif Locking == false then
                                Enemy = nil
                            elseif Enemy == nil then
                                Locking = false
                            end
                        end
                    end)
                end)
            elseif Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health > 0 and
                getgenv().SmoothnessValue == false and getgenv().PredictionState == false then
                Render_Lock = RunService.Stepped:Connect(function()
                    pcall(function()
                        if getgenv().TracerRadius then
                            local RootPartPosition = Camera:WorldToViewportPoint(Enemy[Settings.Head].Position)
                            local Real_Magnitude = (Vector2.new(Mouse.X, Mouse.Y) -
                                                       Vector2.new(RootPartPosition.X, RootPartPosition.Y)).Magnitude
                            if Real_Magnitude < Distance and Real_Magnitude < FOV_Circle.Radius then
                                if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and
                                    Enemy[Settings.Humanoid].Health > 0 and getgenv().CamUndergroundResolver then
                                    local hrp = Enemy.HumanoidRootPart
                                    hrp.Velocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                    hrp.AssemblyLinearVelocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                end
                                if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and
                                    Enemy[Settings.Humanoid].Health > 0 then
                                    Predicted_Position = Enemy[Settings.Head].Position
                                    GetPositionsFromVector3 = Camera:WorldToScreenPoint(Predicted_Position)
                                    mousemoverel((GetPositionsFromVector3.X - Mouse.X) / 0.6,
                                        (GetPositionsFromVector3.Y - Mouse.Y) / 0.6)
                                elseif Locking == false then
                                    Enemy = nil
                                elseif Enemy == nil then
                                    Locking = false
                                end
                            end
                        elseif getgenv().TracerRadius == false then
                            if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health >
                                0 and getgenv().CamUndergroundResolver then
                                local hrp = Enemy.HumanoidRootPart
                                hrp.Velocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                                hrp.AssemblyLinearVelocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
                            end
                            if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] and Enemy[Settings.Humanoid].Health >
                                0 then
                                Predicted_Position = Enemy[Settings.Head].Position
                                GetPositionsFromVector3 = Camera:WorldToScreenPoint(Predicted_Position)
                                mousemoverel((GetPositionsFromVector3.X - Mouse.X) / 0.6,
                                    (GetPositionsFromVector3.Y - Mouse.Y) / 0.6)
                            elseif Locking == false then
                                Enemy = nil
                            elseif Enemy == nil then
                                Locking = false
                            end
                        end
                    end)
                end)
            end
        end
    end)
end

RunService.Stepped:Connect(function()
    if getgenv().UnlockWhenTargetDies then
        if Locking and Enemy ~= nil and Enemy[Settings.Humanoid] then
            if Enemy.BodyEffects['K.O'].Value == true and Enemy[Settings.Humanoid] then
                Locking = false
                Render_Lock:Disconnect()
            end
        end
    end
    if getgenv().UnlockWhenPlayerDies then
        if game.Players.LocalPlayer.Character.BodyEffects['K.O'].Value == true or
            game.Players.LocalPlayer.Character.Humanoid.Health <= 0 then
            Locking = false
            Render_Lock:Disconnect()
        end
    end
end)

rconsolename("aorinject")
function aorimain()
aorinjectbase([[
                                                    .                                                    s    
                                                   @88>                   ..                            :8    
                               u.      .u    .     %8P      u.    u.     888>                          .88    
                  u      ...ue888b   .d88B :@8c     .     x@88k u@88c.   "8P        .u          .     :888ooo 
               us888u.   888R Y888r ="8888f8888r  .@88u  ^"8888""8888"    .      ud8888.   .udR88N  -*8888888 
            .@88 "8888"  888R I888>   4888>'88"  ''888E`   8888  888R   u888u. :888'8888. <888'888k   8888    
            9888  9888   888R I888>   4888> '      888E    8888  888R  `'888E  d888 '88%" 9888 'Y"    8888    
            9888  9888   888R I888>   4888>        888E    8888  888R    888E  8888.+"    9888        8888    
            9888  9888  u8888cJ888   .d888L .+     888E    8888  888R    888E  8888L      9888       .8888Lu= 
            9888  9888   "*888*P"    ^"8888*"      888&   "*88*" 8888"   888E  '8888c. .+ ?8888u../  ^%888*   
            "888*""888"    'Y"          "Y"        R888"    ""   'Y"     888E   "88888%    "8888P'     'Y"    
             ^Y"   ^Y'                              ""                   888E     "YP'       "P'              
                                                                         888E                                 
                                                                         888P                                 
                                                                       .J88"                            

        Made by delusional#7743 & aori#0001 / discord.gg/aorinject


                                [1] Load Aorinject []] ..aorinjectstatus ..[[]
                                [2] Camlock Settings
                                [3] Silent-Aim Settings

                                [X] Exit
]])
aori = rconsoleinput("")
aoriresponse()
end

function aoricammiscs()
aorinjectbase([[
                                                    .                                                    s    
                                                   @88>                   ..                            :8    
                               u.      .u    .     %8P      u.    u.     888>                          .88    
                  u      ...ue888b   .d88B :@8c     .     x@88k u@88c.   "8P        .u          .     :888ooo 
               us888u.   888R Y888r ="8888f8888r  .@88u  ^"8888""8888"    .      ud8888.   .udR88N  -*8888888 
            .@88 "8888"  888R I888>   4888>'88"  ''888E`   8888  888R   u888u. :888'8888. <888'888k   8888    
            9888  9888   888R I888>   4888> '      888E    8888  888R  `'888E  d888 '88%" 9888 'Y"    8888    
            9888  9888   888R I888>   4888>        888E    8888  888R    888E  8888.+"    9888        8888    
            9888  9888  u8888cJ888   .d888L .+     888E    8888  888R    888E  8888L      9888       .8888Lu= 
            9888  9888   "*888*P"    ^"8888*"      888&   "*88*" 8888"   888E  '8888c. .+ ?8888u../  ^%888*   
            "888*""888"    'Y"          "Y"        R888"    ""   'Y"     888E   "88888%    "8888P'     'Y"    
             ^Y"   ^Y'                              ""                   888E     "YP'       "P'              
                                                                         888E                                 
                                            [Camlock Settings]           888P                                 
                                                                       .J88"                                                                 

                                        [0] Change FOV Radius []] ..fovvalue ..[[]
                                        [1] Notifications []] ..notifstatus ..[[]
                                        [2] Smoothness []] ..smoothnessstatus ..[[]
                                        [3] Smoothness Value []] ..smoothnessvalue ..[[]
                                        [4] Prediction []] ..predictionstatus ..[[]
                                        [5] Prediction Value []] ..predictionvalue ..[[]
                                        [6] Unlock when target dies []] ..unlockwhendeadstatus ..[[]
                                        [7] Unlock when you die []] ..unlockwhenlocalplayerknockedstatus ..[[]
                                        [8] Trace only if target is in radius []] ..tracewhentargetradiusstatus ..[[]
                                        [9] Show FOV Circle []] ..fovcirclestatus ..[[]
                                        [10] Keybind []] ..keybindvalue ..[[]

                                        [X] Go back to main menu
]])
aoricammisc = rconsoleinput("")
aoricammiscresponse()
end

function aorisilmiscs()
aorinjectbase([[
                                                    .                                                    s    
                                                   @88>                   ..                            :8    
                               u.      .u    .     %8P      u.    u.     888>                          .88    
                  u      ...ue888b   .d88B :@8c     .     x@88k u@88c.   "8P        .u          .     :888ooo 
               us888u.   888R Y888r ="8888f8888r  .@88u  ^"8888""8888"    .      ud8888.   .udR88N  -*8888888 
            .@88 "8888"  888R I888>   4888>'88"  ''888E`   8888  888R   u888u. :888'8888. <888'888k   8888    
            9888  9888   888R I888>   4888> '      888E    8888  888R  `'888E  d888 '88%" 9888 'Y"    8888    
            9888  9888   888R I888>   4888>        888E    8888  888R    888E  8888.+"    9888        8888    
            9888  9888  u8888cJ888   .d888L .+     888E    8888  888R    888E  8888L      9888       .8888Lu= 
            9888  9888   "*888*P"    ^"8888*"      888&   "*88*" 8888"   888E  '8888c. .+ ?8888u../  ^%888*   
            "888*""888"    'Y"          "Y"        R888"    ""   'Y"     888E   "88888%    "8888P'     'Y"    
             ^Y"   ^Y'                              ""                   888E     "YP'       "P'              
                                                                         888E                                 
                                            [Silent-Aim Settings]        888P                                 
                                                                       .J88"                            

                                        [0] Enable / Disable Silent-Aim []] ..silentaimstatus ..[[]
                                        [1] Prediction Value []] ..silpredictionvalue ..[[]
                                        [2] Prediction []] ..silpredictionstatus ..[[]
                                        [3] Grabbed Check []] ..silgrabbedvalue ..[[]
                                        [4] K.O Check []] ..silkodcheckstatus ..[[]
                                        [5] Change FOV Radius []] ..silentfovvalue ..[[]
                                        [6] Show FOV Circle []] ..silentfovcirclestatus ..[[]
                                
                                        [X] Go back to main menu
]])
aorisilmisc = rconsoleinput("")
aorisilmiscresponse()
end

function aoriresponse()
    if aori == "1" and getgenv().loaded == false then
        Mouse.KeyDown:Connect(function(KeyPressed)
            if KeyPressed == string.lower(getgenv().keybind) then
                pcall(function()
                    if Locking == false then
                        Locking = true
                        Aimbot()
                        Enemy = InRadius()
                        if getgenv().Notifications then
                            game.StarterGui:SetCore("SendNotification", {
                                Title = "aorinject",
                                Text = "Target:  " .. tostring(Enemy.Humanoid.DisplayName .. ".")
                            })
                        end
                        if Enemy == nil then
                            Locking = false
                        end
                    elseif Locking == true then
                        if getgenv().Notifications then
                            game.StarterGui:SetCore("SendNotification", {
                                Title = "aorinject",
                                Text = "Unlocked."
                            })
                        end
                        Locking = false
                        Render_Lock:Disconnect()
                    end
                end)
            end
        end)
        AorinjectSettings.SilentAim = true
        getgenv().loaded = true
        aorinjectstatus = "Loaded"
        rconsoleclear()
        aorimain()
    elseif aori == "1" and getgenv().loaded == true then
        rconsoleprint([[Already Loaded
]])
        aori = rconsoleinput("")
        aoriresponse()
    elseif aori == "X" or aori == "x" then
        game.Players.LocalPlayer:Kick("AorInject Kick")
    elseif aori == "2" then
        rconsoleclear()
        aoricammiscs()
    elseif aori == "3" then
        rconsoleclear()
        aorisilmiscs()
    else
        rconsoleprint([[Unknown Command
]])
        aori = rconsoleinput("")
        aoriresponse()
    end
end

function aoricammiscresponse()
    if aoricammisc == "1" then
        if getgenv().Notifications == true then
            getgenv().Notifications = false
            notifstatus = "false"
        elseif getgenv().Notifications == false then
            getgenv().Notifications = true
            notifstatus = "true"
        end
        rconsoleclear()
        aoricammiscs()
    elseif aoricammisc == "2" then
        if getgenv().SmoothnessValue == true then
            getgenv().SmoothnessValue = false
            smoothnessstatus = "false"
        elseif getgenv().SmoothnessValue == false then
            getgenv().SmoothnessValue = true
            smoothnessstatus = "true"
        end
        rconsoleclear()
        aoricammiscs()
    elseif aoricammisc == "3" then
        rconsoleprint("Smoothness: ")
        smoothnessvalue = rconsoleinput("")
        getgenv().smoothness = tonumber(smoothnessvalue)
        rconsoleclear()
        aoricammiscs()
    elseif aoricammisc == "4" then
        if getgenv().PredictionState == true then
            getgenv().PredictionState = false
            predictionstatus = "false"
        elseif getgenv().PredictionState == false then
            getgenv().PredictionState = true
            predictionstatus = "true"
        end
        rconsoleclear()
        aoricammiscs()
    elseif aoricammisc == "5" then
        rconsoleprint("Prediction: ")
        predictionvalue = rconsoleinput("")
        getgenv().prediction = tonumber(predictionvalue)
        rconsoleclear()
        aoricammiscs()
    elseif aoricammisc == "6" then
        if getgenv().UnlockWhenTargetDies == true then
            getgenv().UnlockWhenTargetDies = false
            unlockwhendeadstatus = "false"
        elseif getgenv().UnlockWhenTargetDies == false then
            getgenv().UnlockWhenTargetDies = true
            unlockwhendeadstatus = "true"
        end
        rconsoleclear()
        aoricammiscs()
    elseif aoricammisc == "7" then
        if getgenv().UnlockWhenPlayerDies == true then
            getgenv().UnlockWhenPlayerDies = false
            unlockwhenlocalplayerknockedstatus = "false"
        elseif getgenv().UnlockWhenPlayerDies == false then
            getgenv().UnlockWhenPlayerDies = true
            unlockwhenlocalplayerknockedstatus = "true"
        end
        rconsoleclear()
        aoricammiscs()
    elseif aoricammisc == "8" then
        if getgenv().TracerRadius == true then
            getgenv().TracerRadius = false
            tracewhentargetradiusstatus = "false"
        elseif getgenv().TracerRadius == false then
            getgenv().TracerRadius = true
            tracewhentargetradiusstatus = "true"
        end
        rconsoleclear()
        aoricammiscs()
    elseif aoricammisc == "9" then
        if FOV_Circle.Visible == true then
            FOV_Circle.Visible = false
            fovcirclestatus = "false"
        elseif FOV_Circle.Visible == false then
            FOV_Circle.Visible = true
            fovcirclestatus = "true"
        end
        rconsoleclear()
        aoricammiscs()
    elseif aoricammisc == "10" then
        rconsoleprint("Keybind: ")
        keybindvalue = rconsoleinput("")
        getgenv().keybind = keybindvalue
        rconsoleclear()
        aoricammiscs()
    elseif aoricammisc == "0" then
        rconsoleprint("FOV: ")
        fovvalue = rconsoleinput("")
        FOV_Circle.Radius = tonumber(fovvalue)
        rconsoleclear()
        aoricammiscs()
    elseif aoricammisc == "X" or aoricammisc == "x" then
        rconsoleclear()
        aorimain()
    else
        rconsoleprint([[Unknown Command
]])
        aoricammisc = rconsoleinput("")
        aoricammiscresponse()
    end
end

function aorisilmiscresponse()
    if aorisilmisc == "0" then
        if getgenv().AorinjectSettings.SilentAim == true then
            getgenv().AorinjectSettings.SilentAim = false
            silentaimstatus = "Disabled"
        elseif getgenv().AorinjectSettings.SilentAim == false then
            getgenv().AorinjectSettings.SilentAim = true
            silentaimstatus = "Enabled"
        end
        rconsoleclear()
        aorisilmiscs()
    elseif aorisilmisc == "1" then
        rconsoleprint("Prediction: ")
        silpredictionvalue = rconsoleinput("")
        getgenv().AorinjectSettings.Prediction = tonumber(silpredictionvalue)
        rconsoleclear()
        aorisilmiscs()
    elseif aorisilmisc == "2" then
        if getgenv().AorinjectSettings.PredictionStatus == true then
            getgenv().AorinjectSettings.PredictionStatus = false
            silpredictionstatus = "Disabled"
        elseif getgenv().AorinjectSettings.PredictionStatus == false then
            getgenv().AorinjectSettings.PredictionStatus = true
            silpredictionstatus = "Enabled"
        end
        rconsoleclear()
        aorisilmiscs()
    elseif aorisilmisc == "3" then
        if getgenv().GrabbedCheck == true then
            getgenv().GrabbedCheck = false
            silgrabbedvalue = "false"
        elseif getgenv().GrabbedCheck == false then
            getgenv().GrabbedCheck = true
            silgrabbedvalue = "true"
        end
        rconsoleclear()
        aorisilmiscs()
    elseif aorisilmisc == "4" then
        if getgenv().KoCheck == true then
            getgenv().KoCheck = false
            silkodcheckstatus = "false"
        elseif getgenv().KoCheck == false then
            getgenv().KoCheck = true
            silkodcheckstatus = "true"
        end
        rconsoleclear()
        aorisilmiscs()
    elseif aorisilmisc == "5" then
        rconsoleprint("FOV: ")
        silentfovvalue = rconsoleinput("")
        getgenv().Aorinject.FOV = tonumber(silentfovvalue)
        rconsoleclear()
        aorisilmiscs()
    elseif aorisilmisc == "6" then
        if getgenv().Aorinject.ShowFOV == true then
            getgenv().Aorinject.ShowFOV = false
            silentfovcirclestatus = "false"
        elseif getgenv().Aorinject.ShowFOV == false then
            getgenv().Aorinject.ShowFOV = true
            silentfovcirclestatus = "true"
        end
        rconsoleclear()
        aorisilmiscs()()
    elseif aorisilmisc == "X" or aorisilmisc == "x" then
        rconsoleclear()
        aorimain()
    else
        rconsoleprint([[Unknown Command
]])
        aorisilmisc = rconsoleinput("")
        aorisilmiscresponse()
    end
end

local __index
__index = hookmetamethod(game, "__index", function(t, k)
    if (t:IsA("Mouse") and (k == "Hit" or k == "Target") and Aorinject.Check()) then
        local SelectedPart = Aorinject.SelectedPart
        if (getgenv().AorinjectSettings.SilentAim and (k == "Hit" or k == "Target")) then
            local Hit = SelectedPart.CFrame + (SelectedPart.Velocity * getgenv().AorinjectSettings.Prediction)
            return (k == "Hit" and Hit or SelectedPart)
        end
    end
    return __index(t, k)
end)

rconsoleclear()
aorimain()
