local v0 = loadstring(game:HttpGet("https://raw.githubusercontent.com/jensonhirst/Orion/main/source"))()

local v1 = v0:MakeWindow({
    Name = "InfinityCore Hub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "InfinityCoreConfig"
})

v0:MakeNotification({
    Name = "Notificação",
    Content = "InfinityCore Hub Executado!",
    Image = "rbxassetid://7733954760",
    Time = 8
})

-- Variáveis
local v2 = false  -- Auto Orb
local v3 = false  -- Auto Pet
local v4 = false  -- Auto Gem
local v5 = false  -- Auto Hoop
local v6 = 0.1    -- Velocidade Hoop
local v7 = "Jungle Crystal"
local v8 = 0.01   -- Velocidade Pet
local v9 = 0.01   -- Velocidade Orb
local v10 = 0.01  -- Velocidade Gem
local v11 = false

-- Cor do Hub
local corAtual = Color3.fromRGB(85, 170, 255)

-- Funções
function coletarOrb(v19, v20)
    local v22 = {"collectOrb", v19, v20}
    game:GetService("ReplicatedStorage"):WaitForChild("rEvents"):WaitForChild("orbEvent"):FireServer(unpack(v22))
end

function coletarGem(v23, v24)
    local v26 = {"collectOrb", v23, v24}
    game:GetService("ReplicatedStorage"):WaitForChild("rEvents"):WaitForChild("orbEvent"):FireServer(unpack(v26))
end

function abrirCrystal(v27)
    local v29 = {"openCrystal", v27}
    game:GetService("ReplicatedStorage"):WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer(unpack(v29))
end

-- Tab Info Logs
local v12 = v1:MakeTab({
    Name = "Info Logs",
    Icon = "rbxassetid://7734075797",
    PremiumOnly = false
})

v12:AddLabel("📜 Info Logs")
v12:AddParagraph("📲 Log De Atualização", [[
Versão: 2.2.0
Desenvolvedor: Rchard
Hub: InfinityCore Hub
Última atualização: 04/12/2025 - 15:00

• Adicionado
    - Botão de configuração de cor
    - Novo nome: InfinityCore Hub

• Removido
    Nenhuma Atualização.
]])

-- Tab Main
local v13 = v1:MakeTab({
    Name = "Main",
    Icon = "rbxassetid://7733960981",
    PremiumOnly = false
})

v13:AddLabel("🏠 Main")

v13:AddToggle({
    Name = "Auto - Orb",
    Default = false,
    Callback = function(v30)
        v2 = v30
        spawn(function()
            while v2 do
                coletarOrb("Blue Orb", "City")
                coletarOrb("Red Orb", "City")
                coletarOrb("Yellow Orb", "City")
                coletarOrb("Orange Orb", "City")
                coletarOrb("Blue Orb", "Snow City")
                coletarOrb("Red Orb", "Snow City")
                coletarOrb("Yellow Orb", "Snow City")
                coletarOrb("Orange Orb", "Snow City")
                coletarOrb("Blue Orb", "Magma City")
                coletarOrb("Red Orb", "Magma City")
                coletarOrb("Yellow Orb", "Magma City")
                coletarOrb("Orange Orb", "Magma City")
                wait(v9)
            end
        end)
    end
})

v13:AddToggle({
    Name = "Auto - Hoop",
    Default = false,
    Callback = function(v32)
        v5 = v32
        if v5 then
            task.spawn(function()
                while v5 do
                    local hoopPositions = {
                        CFrame.new(-11096.9756, 200.85762, 4465.38623, 0, 0.0200170279, 0.999799609, -1, 0, 0.0000085532665, -0.0000085532665, -0.999799609, 0.0200170279),
                        CFrame.new(-13140.8779, 200.85762, 4465.38623, 0, 0.0200170279, 0.999799609, -1, 0, 0.0000085532665, -0.0000085532665, -0.999799609, 0.0200170279),
                        CFrame.new(-15156.4043, 355.120056, 4141.85889, 0, 0.0200170279, 0.999799609, -1, 0, 0.0000085532665, -0.0000085532665, -0.999799609, 0.0200170279)
                    }
                    for _, pos in pairs(hoopPositions) do
                        if not v5 then break end
                        local char = game.Players.LocalPlayer.Character
                        if char and char:FindFirstChild("HumanoidRootPart") then
                            char.HumanoidRootPart.CFrame = pos
                        end
                        task.wait(v6)
                    end
                end
            end)
        end
    end
})

v13:AddToggle({
    Name = "Auto - Gem",
    Default = false,
    Callback = function(v35)
        v4 = v35
        spawn(function()
            while v4 do
                coletarGem("Gem", "City")
                wait(v10)
            end
        end)
    end
})

v13:AddParagraph("⚠️ AVISO! ⚠️", [[
Não use o "Auto - Hoop" em servidores públicos!
Risco de denúncias e banimento.

Use velocidades acima de 0.1s para evitar lag.
]])

-- Tab Pet
local v14 = v1:MakeTab({
    Name = "Pet",
    Icon = "rbxassetid://7734068321",
    PremiumOnly = false
})

v14:AddLabel("🐾 Pet")

v14:AddDropdown({
    Name = "Selecionar Crystal",
    Default = "Jungle Crystal",
    Options = {"Jungle Crystal", "Electro Legends Crystal"},
    Callback = function(v37)
        v7 = v37
    end
})

v14:AddToggle({
    Name = "Auto - Pet",
    Default = false,
    Callback = function(v38)
        v3 = v38
        spawn(function()
            while v3 do
                abrirCrystal(v7)
                wait(v8)
            end
        end)
    end
})

v14:AddSection({Name = "⚙️ Configuração Auto - Pet"})

v14:AddDropdown({
    Name = "⏱️ Velocidade",
    Default = "0.1",
    Options = {"0.01", "0.1", "0.5", "1"},
    Callback = function(v40)
        v8 = tonumber(v40)
    end
})

v14:AddParagraph("🔮 SISTEMA DE PETS", [[
1. Selecione o crystal
2. Ajuste a velocidade
3. Ative o Auto Pet
]])

-- Tab Configurações
local v15 = v1:MakeTab({
    Name = "Configurações",
    Icon = "rbxassetid://7734053495",
    PremiumOnly = false
})

v15:AddLabel("⚙️ Configuração")

-- ===== BOTÃO DE COR ADICIONADO =====
v15:AddSection({Name = "🎨 Personalização"})

v15:AddColorpicker({
    Name = "🎨 Cor do Hub",
    Default = Color3.fromRGB(85, 170, 255),
    Callback = function(cor)
        corAtual = cor
        v0:MakeNotification({
            Name = "🎨 Cor Alterada",
            Content = "Cor do hub atualizada com sucesso!",
            Image = "rbxassetid://7733942651",
            Time = 3
        })
        -- Aplicar cor nos elementos do hub (se suportado)
        pcall(function()
            for _, obj in pairs(game:GetService("CoreGui"):GetDescendants()) do
                if obj:IsA("Frame") and obj.Name == "TopBar" then
                    obj.BackgroundColor3 = cor
                end
            end
        end)
    end
})

v15:AddButton({
    Name = "🔄 Resetar Cor Padrão",
    Callback = function()
        corAtual = Color3.fromRGB(85, 170, 255)
        v0:MakeNotification({
            Name = "🔄 Cor Resetada",
            Content = "Cor padrão restaurada!",
            Image = "rbxassetid://7733942651",
            Time = 3
        })
    end
})

-- Seções de Velocidade
v15:AddSection({Name = "Auto - Orb"})
v15:AddTextbox({
    Name = "⏱️ Velocidade",
    Default = "0.01",
    TextDisappear = false,
    Callback = function(v41)
        v9 = tonumber(v41)
    end
})

v15:AddSection({Name = "Auto - Hoop"})
v15:AddTextbox({
    Name = "⏱️ Velocidade",
    Default = "0.01",
    TextDisappear = false,
    Callback = function(v42)
        v6 = tonumber(v42)
    end
})

v15:AddSection({Name = "Auto - Gem"})
v15:AddTextbox({
    Name = "⏱️ Velocidade",
    Default = "0.01",
    TextDisappear = false,
    Callback = function(v43)
        v10 = tonumber(v43)
    end
})

v15:AddParagraph("⚙️ CONFIGURAÇÕES", [[
Ajuste as velocidades dos farms.
Valores muito baixos podem causar lag.
]])

-- Tab Features
local v17 = v1:MakeTab({
    Name = "Features",
    Icon = "rbxassetid://7734068495",
    PremiumOnly = false
})

v17:AddLabel("🔧 Features")

v17:AddButton({
    Name = "Anti Afk",
    Callback = function()
        v0:MakeNotification({
            Name = "Notificação",
            Content = "Anti Afk Ativado!",
            Image = "rbxassetid://7733942651",
            Time = 5
        })
        spawn(function()
            while true do
                game:GetService("VirtualUser"):CaptureController()
                wait(30)
            end
        end)
    end
})

v17:AddButton({
    Name = "Force Reset",
    Callback = function()
        game.Players.LocalPlayer.Character:BreakJoints()
    end
})

v17:AddParagraph("🔧 FERRAMENTAS", [[
Utilidades para melhorar
sua experiência no jogo.
]])

-- Tab Links
local v18 = v1:MakeTab({
    Name = "Links",
    Icon = "rbxassetid://7733978098",
    PremiumOnly = false
})

v18:AddButton({
    Name = "📋 Copiar Discord",
    Callback = function()
        setclipboard("https://discord.gg/fHBxYqVG")
        v0:MakeNotification({
            Name = "Notificação",
            Content = "Discord copiado para área de transferência",
            Image = "rbxassetid://7733779668",
            Time = 3
        })
    end
})

v18:AddButton({
    Name = "🎥 Canal do Youtube",
    Callback = function()
        setclipboard("www.youtube.com/@richard75e")
        v0:MakeNotification({
            Name = "Notificação",
            Content = "Link copiado para área de transferência",
            Image = "rbxassetid://7733779668",
            Time = 3
        })
    end
})

v18:AddButton({
    Name = "👤 Copiar Seu User ID",
    Callback = function()
        local userId = game.Players.LocalPlayer.UserId
        setclipboard(tostring(userId))
        v0:MakeNotification({
            Name = "📋 ID Copiado",
            Content = "Seu ID: " .. userId,
            Time = 4
        })
    end
})

v18:AddParagraph("🔗 LINKS ÚTEIS", [[
Links para contato e suporte.
]])

v0:Init()
