local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Anime X hub v1", "BloodTheme")
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("FastAttack")
Section:NewToggle("FastAttack", "Click to use FastAttack", function(state)
local Fast = require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework)
local CameraShaker = require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework.CameraShaker)
_G.Fastattack = state -- true\false
game:GetService("RunService").RenderStepped:Connect(function()
    pcall(function()
        if _G.Fastattack then
Fast.activeController.timeToNextAttack = 0
Fast.activeController.hitboxMagnitude = 50
game:GetService'VirtualUser':CaptureController()
game:GetService'VirtualUser':Button1Down(Vector2.new(686, 352))
CameraShaker.CameraShakeInstance.CameraShakeState = {FadingIn = 3, FadingOut = 2, Sustained = 0, Inactive = 1}
end
end)
end)
end)
Section:NewLabel("Bringmob")
Section:NewToggle("Bringmob", "Click to use bringmob", function(state)
_G.bringmob = state
while _G.bringmob do wait()
    pcall(function()
for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
for x,y in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
if v.Name == "Bandit [Lv. 5]" then
    if y.Name == "Bandit [Lv. 5]" then
   v.HumanoidRootPart.CFrame = y.HumanoidRootPart.CFrame
   v.HumanoidRootPart.Size = Vector3.new(60,60,60)
   y.HumanoidRootPart.Size = Vector3.new(60,60,60)
   v.HumanoidRootPart.Transparency = 1
   v.HumanoidRootPart.CanCollide = false
   y.HumanoidRootPart.CanCollide = false
   v.Humanoid.WalkSpeed = 0
   y.Humanoid.WalkSpeed = 0
   v.Humanoid.JumpPower = 0
   y.Humanoid.JumpPower = 0
   if sethiddenproperty then
     sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
end
end
end
end
end
end)
end
end)
Section:NewKeybind("KeybindText", "KeybindInfo", Enum.KeyCode.RightControl, function()
	Library:ToggleUI()
end)

local Section = Tab:NewSection("Auto Equip")

local Weaponlist = {}
local Weapon = nil

for i,v in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
    table.insert(Weaponlist,v.Name)
end

Section:NewDropdown("select weapon", " ", Weaponlist, function(currentOption)
    Weapon = currentOption
end)

Section:NewToggle("Auto Equip", " ", function(a)
AutoEquiped = a
end)

spawn(function()
while wait() do
if AutoEquiped then
pcall(function()
game.Players.LocalPlayer.Character.Humanoid:EquipTool(game:GetService("Players").LocalPlayer.Backpack:FindFirstChild(Weapon))
end)
end
end
end)

local Tab = Window:NewTab("TP")
local Section = Tab:NewSection("Tp")
Section:NewButton("TP1", "", function()
 local CFrameEnd = CFrame.new(1046.54431, 16.2735653, 1426.11328, 0.00888089277, 4.00218632e-08, 0.999960542, -9.50167589e-08, 1, -3.91795751e-08, -0.999960542, -9.46650616e-08, 0.00888089277) --ใส่CFrame
local Time = 5 --ใส่เวลาที่จะไปถึง
local tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart, TweenInfo.new(Time), {CFrame = CFrameEnd}) tween:Play()
end)

Section:NewButton("TP2", "", function()
 local CFrameEnd = CFrame.new(-676.812073, 7.85225534, 1578.31421, 0.22935541, -6.67799895e-08, -0.973342717, -4.83182454e-08, 1, -7.99944715e-08, 0.973342717, 6.53773782e-08, 0.22935541) --ใส่CFrame
local Time = 5 --ใส่เวลาที่จะไปถึง
local tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart, TweenInfo.new(Time), {CFrame = CFrameEnd}) tween:Play()
end)

local Tab = Window:NewTab("Setting")
local Section = Tab:NewSection("Level Lock")
Section:NewToggle("Level Lock kick", "", function(state)
if state then
        print("Toggle On")
    else
        print("Toggle Off")
    end
end)
Section:NewSlider("Level Lock", "", 2200, 0, function(s) -- 500 (MaxValue) | 0 (MinValue)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = s
end)
