local Player = game:GetService("Players").LocalPlayer
local insert = game:GetService("InsertService")
local RS = game:GetService("ReplicatedStorage")

local SKIN = "Milestone100Slasher"
local CHAR = "Slasher"

local function import(link, name)
  if not isfile(name) then
    writefile(name, game:HttpGet(link))
  end
  return getcustomasset(name)
end

local function importinstance(asset, parent)
  local ok, imported = pcall(insert.LoadLocalAsset, insert, asset)
  if ok and imported then
    imported.Parent = parent
    return imported
  end
end

local JasonRBXM = import("https://github.com/bn9266705-code/Jason/raw/refs/heads/main/Jason.rbxm", "Jason_M4.rbxm")
local LMS_Guest = import("https://github.com/bn9266705-code/Jason/raw/refs/heads/main/lv_0_20261004210806%20(online-audio-converter.com).mp3", "LMS_Guest1337.mp3")
local LMS_Default = import("https://github.com/bn9266705-code/LMS/raw/refs/heads/main/A%20BRAVE%20SOUL%20-%20Forsaken%20UST%20MS%204%20Killer%20VS%20MS%204%20Survivor.mp3", "LMS_BraveSoul.mp3")
local VictorySFX = import("https://github.com/bn9266705-code/Jason/raw/refs/heads/main/Forsaken%20-%20Unusedscrapped%20jason%20win%20animation%20forsaken%20roblo.mp3", "Jason_Victory.mp3")

pcall(function()
  local f = RS.Assets.Skins.Killers.Slasher:FindFirstChild("Milestone100Slasher")
  local VIPCon = f and require(f.Config)
  if VIPCon then
    VIPCon.DisplayName = "Milestone IV"
    VIPCon.RenderImage = "rbxassetid://98225822061072"
    VIPCon.Sounds = VIPCon.Sounds or {}
    VIPCon.Sounds.TerrorRadiusThemes = {
      [60] = { ID = "rbxassetid://132410957705890", BPM = 150 },
      [40] = { ID = "rbxassetid://110159320385013", BPM = 150 },
      [20] = { ID = "rbxassetid://88809604073112", BPM = 150 },
      [18] = { ID = "rbxassetid://72775647208451", BPM = 150, Chase = true },
    }
    VIPCon.Sounds.Execution = "rbxassetid://133920638799807"
    VIPCon.Sounds.Victory = VictorySFX
  end
end)

pcall(function()
  local SBeh = require(RS.Assets.Killers.Slasher.Behavior)
  local JBeh = require(RS.Assets.Killers.Jason.Behavior)
  SBeh.Abilities.Slash.Icon = JBeh.Abilities.Slash.Icon
  SBeh.Abilities.Behead.Icon = JBeh.Abilities.Behead.Icon
  SBeh.Abilities.GashingWound.Icon = JBeh.Abilities.GashingWound.Icon
  SBeh.Abilities.RagingPace.Icon = JBeh.Abilities.RagingPace.Icon
end)

local function CreatePart(name, parent, weld, offset)
  local Part = Instance.new("Part")
  Part.Name = name
  Part.Massless = true
  Part.Anchored = false
  Part.CanCollide = false
  Part.CanTouch = false
  Part.CanQuery = false
  if weld then
    local Weld = Instance.new("Weld")
    Weld.C0 = offset or CFrame.new(0, 0, 0)
    Weld.Part0 = Part
    Weld.Part1 = weld
    Weld.Parent = Part
  end
  Part.Parent = parent
  return Part
end

local function Accs(AccsName, parent, Mesh, Texture, Scale, CF, Welded, Angle)
  Scale = Scale or Vector3.new(1, 1, 1)
  Angle = Angle or CFrame.Angles(0, 0, 0)
  CF = CF or CFrame.new(0, 0, 0)
  local var_2 = CreatePart(AccsName, parent)
  var_2.Size = Vector3.new(1, 1, 1)
  local var_3 = Instance.new("SpecialMesh")
  var_3.Name = "Mesh"
  var_3.MeshId = Mesh
  var_3.TextureId = Texture
  var_3.Scale = Scale
  var_3.Parent = var_2
  local var_4 = Instance.new("Weld")
  var_4.C0 = CF * Angle
  var_4.Part0 = var_2
  var_4.Part1 = Welded
  var_4.Parent = var_2
  return var_2
end

local function D(...)
  for _, v in ipairs({...}) do
    if v then pcall(function() v:Destroy() end) end
  end
end

local function isTarget(P)
  if not P or P.Name ~= CHAR then return false end
  return (P:GetAttribute("SkinName") or "") == SKIN
end

local function stripSlasher(P)
  D(
    P:FindFirstChild("M4 slasher"),
    P:FindFirstChild("M4 Slasher"),
    P:FindFirstChild("M4Slasher"),
    P:FindFirstChild("Slasher Export"),
    P:FindFirstChild("Mask"),
    P:FindFirstChild("Knife"),
    P:FindFirstChild("Necrobloxian")
  )
  local ll = P:FindFirstChild("Left Leg")
  local rl = P:FindFirstChild("Right Leg")
  if ll then D(ll:FindFirstChild("LShoe")) end
  if rl then D(rl:FindFirstChild("RShoe")) end
  local cs = P:FindFirstChild("Chainsaw")
  if cs then D(cs:FindFirstChild("Note")) end
  for _, v in ipairs(P:GetChildren()) do
    if v:IsA("Shirt") or v:IsA("Pants") or v:IsA("ShirtGraphic") or v:IsA("Accessory") or v:IsA("Hat") or v:IsA("CharacterMesh") then
      D(v)
    end
    local n = string.lower(v.Name)
    if (n:find("m4") or n:find("export") or n:find("necro") or n:find("mask") or n:find("shoe")) and v.Name ~= "JasonM4Rig" and v.Name ~= "OldMachete" then
      if v.Name ~= "Head" and v.Name ~= "Torso" and v.Name ~= "Machete" and v.Name ~= "Chainsaw" and v.Name ~= "HumanoidRootPart" and not v.Name:find("Arm") and not v.Name:find("Leg") then
        D(v)
      end
    end
  end
  for _, v in ipairs(P:GetDescendants()) do
    if P:FindFirstChild("JasonM4Rig") and v:IsDescendantOf(P.JasonM4Rig) then
    else
      if v:IsA("ParticleEmitter") or v:IsA("Fire") or v:IsA("Smoke") or v:IsA("Beam") then
        pcall(function() v:Destroy() end)
      end
    end
  end
end

local function hideBody(P)
  for _, n in ipairs({"Head", "Torso", "Right Leg", "Left Leg", "Right Arm", "Left Arm"}) do
    local L = P:FindFirstChild(n)
    if L and L:IsA("BasePart") then
      L.Transparency = 1
    end
  end
end

local function cleanJasonRig(Model)
  D(Model:FindFirstChild("AnimSaves"), Model:FindFirstChild("Machete"), Model:FindFirstChild("Manchete"), Model:FindFirstChild("Chainsaw"))
  for _, v in ipairs(Model:GetDescendants()) do
    if v.Name == "AnimSaves" or v.Name == "Machete" or v.Name == "Manchete" or v.Name == "Chainsaw" then
      D(v)
    end
    if v:IsA("Script") or v:IsA("LocalScript") then
      D(v)
    end
  end
end

local function weldModel(Model, P)
  pcall(function()
    local hum = Model:FindFirstChildOfClass("Humanoid")
    if hum then
      hum.EvaluateStateMachine = false
    end
  end)
  for _, v in ipairs(Model:GetDescendants()) do
    if v:IsA("Motor6D") then
      if v.Part1 and P:FindFirstChild(v.Part1.Name) then
        v.Enabled = false
        D(v)
      end
    elseif v:IsA("BasePart") then
      v.Transparency = 0
      v.LocalTransparencyModifier = 0
      v.Massless = true
      v.CanCollide = false
      v.CanTouch = false
      v.Anchored = false
      local host = P:FindFirstChild(v.Name)
      if host and host:IsA("BasePart") then
        local w = Instance.new("Weld")
        w.Part0 = v
        w.Part1 = host
        w.Parent = host
      end
    end
  end
  local hrp = Model:FindFirstChild("HumanoidRootPart")
  local phrp = P:FindFirstChild("HumanoidRootPart") or P.PrimaryPart
  if hrp and phrp then
    hrp.Transparency = 1
    hrp.Massless = true
    hrp.CanCollide = false
    hrp.Anchored = false
    local w = Instance.new("Weld")
    w.Part0 = hrp
    w.Part1 = phrp
    w.Parent = phrp
  end
end

local function GetFarthestSurv(c)
  local Survs = workspace:FindFirstChild("Players") and workspace.Players:FindFirstChild("Survivors")
  if not Survs then return nil end
  local furthest
  local max = -1
  for _, v in ipairs(Survs:GetChildren()) do
    local root = v:FindFirstChild("HumanoidRootPart")
    local myRoot = c:FindFirstChild("HumanoidRootPart")
    if root and myRoot then
      local dis = (myRoot.Position - root.Position).Magnitude
      if dis > max then
        max = dis
        furthest = v
      end
    end
  end
  return furthest
end

local themesDone = false
local function setupThemes(P)
  if themesDone then return end
  local Themes = workspace:FindFirstChild("Themes")
  if not Themes then
    task.spawn(function()
      Themes = workspace:WaitForChild("Themes", 60)
      if Themes then
        themesDone = false
        setupThemes(P)
      end
    end)
    return
  end
  themesDone = true

  Themes.ChildAdded:Connect(function(v)
    if not v:IsA("Sound") then return end
    task.wait(0.08)

    if v.Name == "LastSurvivor" or tostring(v.SoundId):find("80564889711353") then
      local FS = GetFarthestSurv(P)
      if FS and FS.Name == "Guest1337" then
        v.SoundId = LMS_Guest
        v.Volume = 1
      else
        v.SoundId = LMS_Default
        v.Volume = 0.9
      end
      v:Play()
    end
  end)
end

local function setupVictory()
  local function onSound(v)
    if not v:IsA("Sound") then return end
    local id = tostring(v.SoundId)
    local n = string.lower(v.Name)
    if n:find("victory") or n:find("win") or id:find("victory") then
      v:Stop()
      v.SoundId = VictorySFX
      v.Volume = 1
      v:Play()
    end
  end

  workspace.DescendantAdded:Connect(function(v)
    if v:IsA("Sound") then
      task.wait()
      onSound(v)
    end
  end)
end

local function DoMorph(P)
  if not isTarget(P) then return end
  if P:GetAttribute("JasonM4Done") then return end
  P:SetAttribute("JasonM4Done", true)
  task.wait(0.5)

  stripSlasher(P)
  hideBody(P)

  if P:FindFirstChild("Machete") then
    P.Machete.Transparency = 1
    for _, c in ipairs(P.Machete:GetDescendants()) do
      if c:IsA("BasePart") then
        c.Transparency = 1
      end
    end
    Accs("OldMachete", P.Machete, "rbxassetid://441575918", "rbxassetid://441575955", Vector3.new(0.016, 0.016, 0.016), nil, P.Machete, CFrame.Angles(0, -math.pi / 2, 0))
  end

  local Model = importinstance(JasonRBXM, P)
  if not Model then
    warn("[JasonM4] falha rbxm")
    return
  end
  Model.Name = "JasonM4Rig"
  cleanJasonRig(Model)

  pcall(function()
    if Model.PrimaryPart then
      Model:PivotTo(P:GetPivot())
    elseif Model:FindFirstChild("HumanoidRootPart") then
      Model.HumanoidRootPart.CFrame = P.HumanoidRootPart.CFrame
    end
  end)

  weldModel(Model, P)
  stripSlasher(P)
  setupThemes(P)
  setupVictory()
end

local function try(r)
  task.wait(0.8)
  DoMorph(r)
end

if Player.Character then
  task.spawn(try, Player.Character)
end
Player.CharacterAdded:Connect(try)

task.spawn(function()
  local k = workspace:FindFirstChild("Players") and workspace.Players:FindFirstChild("Killers")
  if not k then
    local pf = workspace:WaitForChild("Players", 30)
    if pf then
      k = pf:WaitForChild("Killers", 30)
    end
  end
  if not k then return end
  for _, c in ipairs(k:GetChildren()) do
    try(c)
  end
  k.ChildAdded:Connect(try)
end)
