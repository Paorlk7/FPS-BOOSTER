-- ANTI-LAG ULTRA MAX — GitHub Version
local RunService, Players, Lighting, player = game:GetService("RunService"), game:GetService("Players"), game:GetService("Lighting"), game.Players.LocalPlayer

setfpscap(999)
Lighting.GlobalShadows = false
Lighting.FogEnd = 100000
Lighting.FogStart = 100000
Lighting.Brightness = 0.5
Lighting.Ambient = Color3.fromRGB(100, 100, 100)
settings().Rendering.QualityLevel = 1

for _, effect in ipairs(Lighting:GetChildren()) do
    if effect:IsA("BlurEffect") or effect:IsA("SunRaysEffect") or effect:IsA("ColorCorrectionEffect") or effect:IsA("BloomEffect") or effect:IsA("DepthOfFieldEffect") then
        effect:Destroy()
    end
end

local function removeAllEffects(parent)
    for _, obj in ipairs(parent:GetDescendants()) do
        if obj:IsA("ParticleEmitter") or obj:IsA("Smoke") or obj:IsA("Fire") or obj:IsA("Sparkles") or obj:IsA("Trail") or obj:IsA("Decal") or obj:IsA("Texture") or obj:IsA("SpecialMesh") then
            obj.Enabled = false
            obj.Transparency = 1
            if obj:IsA("SpecialMesh") then obj.TextureId = "" end
        end
    end
end

removeAllEffects(workspace)
removeAllEffects(player.Character)

for _, part in ipairs(workspace:GetDescendants()) do
    if part:IsA("BasePart") then part.LOD = 0 end
end

for _, model in ipairs(workspace:GetDescendants()) do
    if model:IsA("Model") then
        for _, part in ipairs(model:GetDescendants()) do
            if part:IsA("BasePart") then part.CastShadow = false end
        end
    end
end

workspace.DescendantAdded:Connect(function(obj)
    if obj:IsA("ParticleEmitter") or obj:IsA("Smoke") or obj:IsA("Fire") or obj:IsA("Sparkles") or obj:IsA("Trail") or obj:IsA("Decal") or obj:IsA("Texture") then
        obj.Enabled = false
        obj.Transparency = 1
    end
end)

workspace.StreamingEnabled = false
player.CameraMaxZoomDistance = 50

print("[ANTI-LAG ULTRA MAX] TUDO removido! FPS otimizado ao máximo.")
