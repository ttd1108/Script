getgenv().Toggle = not getgenv().Toggle 

local plr = game.Players.LocalPlayer

if not getgenv().NoclipRun then
    function Noclip()
        for i, v in ipairs(plr.Character:GetDescendants()) do
            if v:IsA("BasePart") and v.CanCollide == true then
                v.CanCollide = false
            end
        end
    end
    game:GetService("RunService").Stepped:Connect(function()
        if getgenv().noclip then
            if plr.Character ~= nil then
                Noclip()
            end
        end
    end)
    spawn(function()
        while wait() do
            pcall(function()
                if noclip and not plr.Character.HumanoidRootPart:FindFirstChild("coems") then
                    local BV = Instance.new("BodyVelocity", plr.Character.HumanoidRootPart)
                    BV.Name = "coems"
                    BV.Velocity = Vector3.new(0, 0, 0)
                    BV.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                end
                repeat wait()
                until not plr.Character.HumanoidRootPart:FindFirstChild("coems") or not noclip
                if not noclip and plr.Character.HumanoidRootPart:FindFirstChild("coems") then
                    plr.Character.HumanoidRootPart.coems:Destroy()
                end
            end)
        end
    end)
    getgenv().NoclipRun = true
end

local GetPointNumber = function()
    for _, v in pairs(plr.PlayerGui:GetChildren()) do
        if string.find(v.Name, "Waypoint") and v.Enabled then
            return v.Name:gsub("Waypoint", "")
        end
    end
end
local function GetShelf()
    return workspace["Shelf" .. GetPointNumber()]
end
local function GetBox()
    for _, v in pairs(plr.Backpack:GetChildren()) do
        if v:IsA("Tool") and string.find(v.Name, "Box") then
            return v
        end
    end
    for _, v in pairs(plr.Character:GetChildren()) do
        if v:IsA("Tool") and string.find(v.Name, "Box") then
            return v
        end
    end
end

local function GetGrabPos()
    for i, v in pairs(workspace:GetChildren()) do
        if v.Name == "Team Changer (Change Part Color)" and v.CFrame == CFrame.new(-371.601349, 0.148784548, 457.317017, 1, 0, 0, 0, 1, 0, 0, 0, 1) then
            return v
        end
    end
end

getgenv().noclip = Toggle

while getgenv().Toggle do wait()
    local s, e = pcall(function()
        if tostring(plr.Team) == "Grab" then
            local Box = GetBox()
            if Box and plr.Character:FindFirstChild(Box.Name) then
                local v = GetShelf()
                if plr:DistanceFromCharacter(v.Deliver.Position) > v.Deliver.ProximityPrompt.MaxActivationDistance then
                    local Pos = v.Deliver.Position
                    plr.Character.HumanoidRootPart.CFrame = CFrame.new(Pos.X, Pos.Y - v.Deliver.ProximityPrompt.MaxActivationDistance, Pos.Z)
                else
                    fireproximityprompt(v.Deliver.ProximityPrompt, .5)
                end
            elseif Box then
                plr.Character.Humanoid:EquipTool(Box)
            else
                local v = workspace.Boxes
                if plr:DistanceFromCharacter(v.Position) > v.Attachment.ProximityPrompt.MaxActivationDistance then
                    v.CanCollide = false
                    local Pos = v.Position
                    plr.Character.HumanoidRootPart.CFrame = CFrame.new(Pos.X, Pos.Y - v.Attachment.ProximityPrompt.MaxActivationDistance, Pos.Z)
                else
                    fireproximityprompt(v.Attachment.ProximityPrompt, .5)
                    wait(1)
                end
            end
        else
            local Grab = GetGrabPos()
            firetouchinterest(plr.Character.HumanoidRootPart, Grab, 0)
            firetouchinterest(plr.Character.HumanoidRootPart, Grab, 1)
        end
    end)
    print(e)
    if e then
        plr.Character.Humanoid.Health = 0
        wait(6)
    end
end
