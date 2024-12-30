-- Variáveis globais
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

-- Função para identificar o assassino
local function identificarAssassino()
    local assassino = nil

    -- Procura o assassino no jogo
    for _, player in pairs(Players:GetPlayers()) do
        if player.Character and player.Character:FindFirstChild("Humanoid") then
            local humanoid = player.Character.Humanoid
            if humanoid.Health > 0 and player.Name ~= game.Players.LocalPlayer.Name then
                -- Verifica se o jogador é o assassino (alterar lógica conforme necessário)
                if humanoid:FindFirstChild("IsMurderer") then
                    assassino = player
                    break
                end
            end
        end
    end

    return assassino
end

-- Função que altera a visão do jogador (detetive)
local function ativarVisaoDoDetetive()
    while true do
        wait(1)
        local assassino = identificarAssassino()
        if assassino then
            -- Aqui, você pode alterar a aparência do assassino para destacar ele
            assassino.Character:FindFirstChild("Head").BrickColor = BrickColor.new("Bright red")
            print("O assassino é: " .. assassino.Name)
        end
    end
end

-- Inicia a função de visão do detetive
if game.Players.LocalPlayer.Team and game.Players.LocalPlayer.Team.Name == "Detetive" then
    ativarVisaoDoDetetive()
end
