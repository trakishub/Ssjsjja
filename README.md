-- =====================================================================
-- SCRIPT DE RESET AUTOMÁTICO DE SKIN - BROOKHAVEN (DELTA EXECUTOR)
-- =====================================================================

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local LocalPlayer = Players.LocalPlayer

print("[Brookhaven] Iniciando reset automático de skin...")

-- Método 1: Tenta encontrar os remotes de avatar/roupas do Brookhaven para limpar a skin
pcall(function()
    for _, obj in ipairs(ReplicatedStorage:GetDescendants()) do
        if obj:IsA("RemoteEvent") and (obj.Name:lower():find("avatar") or obj.Name:lower():find("skin") or obj.Name:lower():find("cloth") or obj.Name:lower():find("reset")) then
            -- Tenta disparar o evento de reset/limpeza se o nome bater com padrões comuns do jogo
            obj:FireServer("Clear")
            obj:FireServer("Reset")
        end
    end
end)

-- Método 2: Força o recarregamento do personagem (Respawn limpo que remove roupas customizadas presas)
pcall(function()
    local humanoid = LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
    if humanoid then
        -- Redefine a saúde para 0 para forçar o respawn limpo no jogo
        humanoid.Health = 0
    end
end)

print("[Brookhaven] Comando de reset executado com sucesso!")
