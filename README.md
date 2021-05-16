local ui = game:GetService("CoreGui"):FindFirstChild("FluxLib")
if ui then
    ui:Destroy()
end
local Flux = loadstring(game:HttpGet"https://raw.githubusercontent.com/DookDekDEE/gui/main/fairyhub.txt")()

local win = Flux:Window("Nitrogen X", "Glue Piece ( Free Beta )", Color3.fromRGB(0, 255, 255) ,Enum.KeyCode.RightControl)
local tab = win:Tab("Farm Option", "http://www.roblox.com/asset/?id=6034989568")
local plr = game.Players.LocalPlayer
local VirtualUser = game:GetService("VirtualUser")
local self = game.Players.LocalPlayer.Character.HumanoidRootPart
local TOOLS = {}
        for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
            if v:IsA("Tool") then
                table.insert(TOOLS,v.Name)
            end
        end

tab:Dropdown("Select Mob",{"Thug","Evil Thug","Slime","Runny","Unknown Boss [Fake Yoru]","Sneaky","Elite Noob","Cutie Noob","Cutie [Boss Raid]","King Noob","Sword Master","Sans","Nooby","Kyo","Chara"}, function(a)
    namemobs = a
end)

tab:Dropdown("Method",{"Over","Under","Behind"},function(a)
  Method =  a
end)

tab:Toggle("Start Farm", "", false , function(f)
  _G.farm = f
  end)

game:GetService("RunService").Stepped:Connect(function()
    if _G.farm then
        for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
          pcall(function()
            if v.Name == namemobs  and v.Humanoid.Health > 0 then
                if Method == "Behind" then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,0,distance)
                game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
                VirtualUser:CaptureController()
                VirtualUser:ClickButton1(Vector2.new(851, 158), CFrame.new(Vector3.new(0, 0, 0)))
                elseif Method == "Over" then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,distance,0) * CFrame.Angles(math.rad(-90), 0, 0)
                game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
                VirtualUser:CaptureController()
                VirtualUser:ClickButton1(Vector2.new(851, 158), CFrame.new(Vector3.new(0, 0, 0)))
                elseif Method == "Under" then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.Angles(math.rad(90), 0, 0) - Vector3.new(0,distance,0)
                game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
                VirtualUser:CaptureController()
                VirtualUser:ClickButton1(Vector2.new(851, 158), CFrame.new(Vector3.new(0, 0, 0)))
              end
            end
        end)
    end
  end
  end)

tab:Slider("Distance","",0,20,0,function(t)
    distance = t
end)

local  rdropdwon = tab:Dropdown("Select Weapon",TOOLS,function(t)
    SelectedWeapon = t
end)


tab:Button("Refresh Weapon","",function()
    rdropdwon:Clear()
        TOOLS = {}
    for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
        if v:IsA("Tool") then
            rdropdwon:Add(v.Name)
        end
    end
end)

tab:Toggle("Auto Equip","",false,function(t)
    spawn(function()
    _G.Equip = t
end)
    while wait() do
        if _G.Equip then
            for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                if v.Name == SelectedWeapon then
                    game.Players.LocalPlayer.Character.Humanoid:EquipTool(v)
                end
            end
        end
    end
end)


local tab = win:Tab("Auto-Stat", "http://www.roblox.com/asset/?id=6034989568")

tab:Toggle("Melee","",false,function (Value)
    melee = Value
end)
spawn(function()
    while wait() do
        if melee then
    local number_1 = 1;
    local string_1 = "Strength";
    local Target = game:GetService("ReplicatedStorage").RemoteEvent.Stats.Add;
    Target:FireServer(number_1, string_1);
end
end
end)

tab:Toggle("Defense","",false,function (Value)
    defense = Value
end)
spawn(function()
    while wait() do
        if defense then
    local number_1 = 1;
    local string_1 = "Defense";
    local Target = game:GetService("ReplicatedStorage").RemoteEvent.Stats.Add;
    Target:FireServer(number_1, string_1);
end
end
end)

tab:Toggle("Sword","",false,function (Value)
    sword = Value
end)
spawn(function()
    while wait() do
        if sword then
    local number_1 = 1;
    local string_1 = "Melee";
    local Target = game:GetService("ReplicatedStorage").RemoteEvent.Stats.Add;
    Target:FireServer(number_1, string_1);
end
end
end)

tab:Toggle("DevilFruit","",false,function (Value)
    devil = Value
end)
spawn(function()
    while wait() do
        if devil then
    local number_1 = 1;
    local string_1 = "DevilFruit";
    local Target = game:GetService("ReplicatedStorage").RemoteEvent.Stats.Add;
    Target:FireServer(number_1, string_1);
end
end
end)

local tab = win:Tab("Teleports", "http://www.roblox.com/asset/?id=6034989568")

tab:Button("Server-Hop","",function ()
    repeat wait() until game:IsLoaded() and game.Players.LocalPlayer
local HttpService, TPService = game:GetService"HttpService", game:GetService"TeleportService";
local OtherServers = HttpService:JSONDecode(game:HttpGet("https://games.roblox.com/v1/games/"..game.PlaceId.."/servers/Public?sortOrder=Asc&limit=100"))
function joinNew()
    if not isfile('servers.sss') then
        writefile('servers.sss',HttpService:JSONEncode({}))
    end
    local dontJoin = readfile('servers.sss')
    dontJoin = HttpService:JSONDecode(dontJoin)

    for Index, Server in next, OtherServers["data"] do
        if Server ~= game.JobId then
            local j = true
            for a,c in pairs(dontJoin) do
               if c == Server.id then
                   j = false
               end
            end
            if j then
                table.insert(dontJoin,Server["id"])
                writefile("servers.sss",HttpService:JSONEncode(dontJoin))
                wait()
                return Server['id']


            end
        end
    end
end

local server = joinNew()
if not server then
    writefile("servers.sss",HttpService:JSONEncode({}))
    local server = joinNew()
    TPService:TeleportToPlaceInstance(game.PlaceId, server)
else
TPService:TeleportToPlaceInstance(game.PlaceId, server)
end
end)

tab:Line()

tab:Button("Thug"," ",function ()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-120.424217, 13, -11.257144)
end)
tab:Button("Slime"," ",function ()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-50.4214783, 12.9000034, -872.822327)
end)
tab:Button("Sneaky"," ",function ()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-646.527771, 13, -1715.22498)
end)
tab:Button("Elite"," ",function ()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1607.97998, 13, -1828.66406)
end)
tab:Button("WaterFall"," ",function ()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-2603.198, 13, -119.838692)
end)
tab:Button("Cutie"," ",function ()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-2639.70239, 48.0000153, 959.031006)
end)
tab:Button("Grave"," ",function ()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(10.0521564, 13.9999962, 569.868896)
end)
tab:Button("Snow"," ",function ()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-515.607788, 13, 1843.6687)
end)
tab:Button("Snow2"," ",function ()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(475.685883, 13, 2317.07568)
end)
tab:Button("Sky","",function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1718.3717, 438, -1176.56018)
end)
tab:Button("Hall","",function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(530.143982, 11.5736389, 375.021545)
end)
tab:Button("RandowFruit"," ",function ()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1127.45752, 0, -1020.15417, -0.014595747, 0, -0.999893427, 0, 1, 0, 0.999893427, 0, -0.014595747) * CFrame.new(0,5,0)
end)

local tab = win:Tab("Misc", "http://www.roblox.com/asset/?id=6034989568")

tab:Slider("Walkspeed", "",16,2000,0,function(value)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
end)
tab:Slider("JumpPower", "",50,2000,0,function(value)
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
end)

tab:Button("Random Fruit","",function()
    -- Script generated by SimpleSpy - credits to exx#9394

local args = {
    [1] = "Random DF",
    [2] = "Money"
}

game:GetService("ReplicatedStorage").RemoteEvent.Reset.Reset:FireServer(unpack(args))
end)

tab:Button("Reset Stat","",function()
    -- Script generated by SimpleSpy - credits to exx#9394

local args = {
    [1] = "Reset Stats",
    [2] = "Money"
}

game:GetService("ReplicatedStorage").RemoteEvent.Reset.Reset:FireServer(unpack(args))
end)
tab:Button("Reset DevilFruit","",function()
    -- Script generated by SimpleSpy - credits to exx#9394

local args = {
    [1] = "Reset DF",
    [2] = "Money"
}

game:GetService("ReplicatedStorage").RemoteEvent.Reset.Reset:FireServer(unpack(args))
end)
tab:Toggle("Ctrl + Click = TP","",false,function(vu)
    CTRL = vu
 end)
 local Plr = game:GetService("Players").LocalPlayer
 local Mouse = Plr:GetMouse()
 Mouse.Button1Down:connect(
    function()
       if not game:GetService("UserInputService"):IsKeyDown(Enum.KeyCode.LeftControl) then
          return
       end
       if not Mouse.Target then
          return
       end
       if CTRL then
          Plr.Character:MoveTo(Mouse.Hit.p)
       end
    end)
    tab:Toggle("Teleport DevilFruits", "XDDDDD",false,function(t)
            TPF = t
            while wait() do
                if TPF then
            for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
            if v:IsA ("Tool") then
                firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart,v.Handle,0)
            end
            end
        end
        end
        end)
local tab = win:Tab("Credit", "http://www.roblox.com/asset/?id=6034989568")
     tab:Button("Made By sHi#5390","",function()
    rdropdwon:Clear()
        TOOLS = {}
    for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
        if v:IsA("Tool") then
            rdropdwon:Add(v.Name)
        end
    end
end)
    tab:Button("Edit By I'm So Cute 💗#5436","",function()
    rdropdwon:Clear()
        TOOLS = {}
    for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
        if v:IsA("Tool") then
            rdropdwon:Add(v.Name)
        end
    end
end)
    
