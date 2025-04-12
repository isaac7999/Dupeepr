local player = game.Players.LocalPlayer
local gui = player:WaitForChild("PlayerGui")

-- Anti-Ban aprimorado (apenas observa passivamente)
pcall(function()
    local palavrasSuspeitas = {"anticheat", "log", "ban", "report", "kick", "monitor"}

    game.DescendantAdded:Connect(function(obj)
        for _, palavra in ipairs(palavrasSuspeitas) do
            if obj.Name:lower():find(palavra) then
                warn("Sistema suspeito detectado: " .. obj:GetFullName())
                -- Apenas notifica, não chuta
            end
        end
    end)
end)

-- Interface de botão pequeno e discreto
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = gui
screenGui.Name = "DupeBtnGui"
screenGui.ResetOnSpawn = false

local btn = Instance.new("TextButton")
btn.Parent = screenGui
btn.Size = UDim2.new(0, 35, 0, 35)
btn.Position = UDim2.new(0.95, -40, 0.95, -40)
btn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
btn.BorderSizePixel = 0
btn.Text = ""
btn.AutoButtonColor = false

local circulo = Instance.new("UICorner", btn)
circulo.CornerRadius = UDim.new(1, 0)

-- Duplicar Tool do Slot1 (apenas quando clicado)
btn.MouseButton1Click:Connect(function()
    pcall(function()
        local slot = gui:FindFirstChild("BackpackNova")
            and gui.BackpackNova:FindFirstChild("Inventario")
            and gui.BackpackNova.Inventario:FindFirstChild("MyInv")
            and gui.BackpackNova.Inventario.MyInv:FindFirstChild("counteudo")
            and gui.BackpackNova.Inventario.MyInv.counteudo:FindFirstChild("Slot1")

        if slot and slot:FindFirstChild("In") and slot.In:FindFirstChildOfClass("Tool") then
            local tool = slot.In:FindFirstChildOfClass("Tool")
            local clone = tool:Clone()
            task.wait(math.random(1, 2)) -- Espera aleatória
            clone.Parent = slot.In
            print("Tool duplicada (modo stealth).")
        else
            warn("Tool não localizada.")
        end
    end)
end)
