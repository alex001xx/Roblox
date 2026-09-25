local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

-- 🎨 ROSA PASTEL TRANSPARENTE
local COLOR_FONDO = Color3.fromRGB(255, 230, 240)
local COLOR_BARRA = Color3.fromRGB(255, 200, 220)
local COLOR_TEXTO = Color3.fromRGB(100, 50, 75)
local TRANSPARENCIA = 0.45

local COLOR_BOTON_ON = Color3.fromRGB(255, 180, 210)
local COLOR_BOTON_OFF = Color3.fromRGB(255, 150, 150)
local COLOR_BOTON_OTROS = Color3.fromRGB(245, 210, 225)
local TRANSPARENCIA_BOTON_ONOFF = TRANSPARENCIA * 0.4
local TRANSPARENCIA_BOTON_BLANCO = TRANSPARENCIA * 0.35

local COLOR_FONDO_LISTA = Color3.fromRGB(255, 240, 245)
local COLOR_SELECCIONADO = Color3.fromRGB(255, 180, 210)
local COLOR_ENTRY = Color3.fromRGB(255, 225, 235)
local COLOR_TU = Color3.fromRGB(200, 220, 255)

-- Función para agregar barra con nombre y minimizar
local function agregarBarraMinimizable(frame, anchoOriginal, altoOriginal, nombreVentana)
    local barra = Instance.new("Frame")
    barra.Size = UDim2.new(1, 0, 0, 22)
    barra.Position = UDim2.new(0, 0, 0, 0)
    barra.BackgroundColor3 = COLOR_BARRA
    barra.BackgroundTransparency = TRANSPARENCIA
    barra.BorderSizePixel = 1
    barra.BorderColor3 = Color3.fromRGB(255, 150, 190)
    barra.ZIndex = 10
    barra.Parent = frame

    local titulo = Instance.new("TextLabel")
    titulo.Size = UDim2.new(0.8, -5, 1, 0)
    titulo.Position = UDim2.new(0, 5, 0, 0)
    titulo.BackgroundTransparency = 1
    titulo.Text = nombreVentana
    titulo.TextColor3 = COLOR_TEXTO
    titulo.Font = Enum.Font.GothamBold
    titulo.TextSize = 11
    titulo.TextXAlignment = Enum.TextXAlignment.Left
    titulo.ZIndex = 11
    titulo.Parent = barra

    local btnMin = Instance.new("TextButton")
    btnMin.Size = UDim2.new(0, 22, 0, 22)
    btnMin.Position = UDim2.new(1, -22, 0, 0)
    btnMin.BackgroundColor3 = Color3.fromRGB(255, 180, 210)
    btnMin.BackgroundTransparency = TRANSPARENCIA * 0.6
    btnMin.Text = "-"
    btnMin.TextColor3 = Color3.fromRGB(90, 40, 65)
    btnMin.Font = Enum.Font.GothamBold
    btnMin.TextSize = 13
    btnMin.ZIndex = 11
    btnMin.Parent = barra

    for _, hijo in pairs(frame:GetChildren()) do
        if hijo ~= barra then
            hijo.Position = hijo.Position + UDim2.new(0, 0, 0, 22)
            hijo.ZIndex = 9
        end
    end

    local minimizado = false
    frame.Size = UDim2.new(0, anchoOriginal, 0, altoOriginal + 22)

    btnMin.MouseButton1Click:Connect(function()
        minimizado = not minimizado
        if minimizado then
            for _, hijo in pairs(frame:GetChildren()) do
                if hijo ~= barra then hijo.Visible = false end
            end
            frame.Size = UDim2.new(0, anchoOriginal, 0, 22)
            btnMin.Text = "+"
        else
            for _, hijo in pairs(frame:GetChildren()) do
                if hijo ~= barra then hijo.Visible = true end
            end
            frame.Size = UDim2.new(0, anchoOriginal, 0, altoOriginal + 22)
            btnMin.Text = "-"
        end
    end)
end

-- 🅰️ Letra A abajo
local function agregarLetraA(frame, anchoOriginal, altoOriginal)
    local letraA = Instance.new("TextLabel")
    letraA.Name = "LetraA"
    letraA.Size = UDim2.new(1, 0, 0, 16)
    letraA.Position = UDim2.new(0, 0, 1, -16)
    letraA.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    letraA.BackgroundTransparency = 0.6
    letraA.Text = "A"
    letraA.TextColor3 = Color3.fromRGB(255, 105, 180)
    letraA.Font = Enum.Font.GothamBold
    letraA.TextSize = 12
    letraA.TextTransparency = 0.2
    letraA.ZIndex = 12
    letraA.Parent = frame
    return letraA
end

-- ==================================================
-- VENTANA 1: TELETRANSPORTE GUARDADO
-- ==================================================
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")
screenGui.ResetOnSpawn = false

local frame = Instance.new("Frame")
frame.Parent = screenGui
frame.BackgroundColor3 = COLOR_FONDO
frame.BackgroundTransparency = TRANSPARENCIA
frame.Size = UDim2.new(0, 180, 0, 136)
frame.Position = UDim2.new(0.5, -90, 0.5, -68)
frame.Active = true
frame.Draggable = true

local onButton = Instance.new("TextButton")
onButton.Parent = frame
onButton.BackgroundColor3 = COLOR_BOTON_ON
onButton.BackgroundTransparency = TRANSPARENCIA_BOTON_ONOFF
onButton.Size = UDim2.new(0, 50, 0, 26)
onButton.Position = UDim2.new(0, 15, 0, 37)
onButton.Text = "On"
onButton.TextColor3 = Color3.fromRGB(80, 35, 55)
onButton.TextScaled = true

local offButton = Instance.new("TextButton")
offButton.Parent = frame
offButton.BackgroundColor3 = COLOR_BOTON_OFF
offButton.BackgroundTransparency = TRANSPARENCIA_BOTON_ONOFF
offButton.Size = UDim2.new(0, 50, 0, 26)
offButton.Position = UDim2.new(0, 105, 0, 37)
offButton.Text = "Off"
offButton.TextColor3 = Color3.fromRGB(80, 35, 55)
offButton.TextScaled = true

local teleportButton = Instance.new("TextButton")
teleportButton.Parent = frame
teleportButton.BackgroundColor3 = COLOR_BOTON_OTROS
teleportButton.BackgroundTransparency = TRANSPARENCIA_BOTON_BLANCO
teleportButton.Size = UDim2.new(0, 150, 0, 26)
teleportButton.Position = UDim2.new(0, 15, 0, 67)
teleportButton.Text = "Teleport"
teleportButton.TextColor3 = COLOR_TEXTO
teleportButton.TextScaled = true

local destroyButton = Instance.new("TextButton")
destroyButton.Parent = frame
destroyButton.BackgroundColor3 = COLOR_BOTON_OTROS
destroyButton.BackgroundTransparency = TRANSPARENCIA_BOTON_BLANCO
destroyButton.Size = UDim2.new(0, 150, 0, 26)
destroyButton.Position = UDim2.new(0, 15, 0, 97)
destroyButton.Text = "Destroy"
destroyButton.TextColor3 = COLOR_TEXTO
destroyButton.TextScaled = true

local statusLabel = Instance.new("TextLabel")
statusLabel.Parent = frame
statusLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
statusLabel.BackgroundTransparency = 0.6
statusLabel.Size = UDim2.new(0, 180, 0, 26)
statusLabel.Position = UDim2.new(0, 0, 0, 7)
statusLabel.Text = "Status: Off"
statusLabel.TextColor3 = COLOR_TEXTO
statusLabel.TextScaled = true

local isActive = false
local lastPosition = nil
local DISTANCIA_TP = -500

local function hacerTeletransporte()
    if not isActive then
        statusLabel.Text = "❌ Activa primero!"
        task.delay(1.5, function() statusLabel.Text = "Status: On" end)
        return
    end
    if not lastPosition then
        statusLabel.Text = "❌ Sin posición guardada"
        task.delay(1.5, function() statusLabel.Text = "Status: On" end)
        return
    end
    local character = LocalPlayer.Character
    if not character then
        statusLabel.Text = "❌ Sin personaje"
        return
    end
    local nuevaPosicion = lastPosition + Vector3.new(0, DISTANCIA_TP, 0)
    character:PivotTo(CFrame.new(nuevaPosicion))
    statusLabel.Text = "✅ ¡Cuerpo completo TP!"
    task.delay(1.2, function() statusLabel.Text = "Status: On" end)
end

onButton.MouseButton1Click:Connect(function()
    isActive = true
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        lastPosition = LocalPlayer.Character.HumanoidRootPart.Position
    end
    statusLabel.Text = "✅ ACTIVO - Posición guardada"
    statusLabel.TextColor3 = Color3.fromRGB(50, 120, 50)
end)

offButton.MouseButton1Click:Connect(function()
    statusLabel.Text = "Status: Off"
    statusLabel.TextColor3 = Color3.fromRGB(180, 60, 60)
    isActive = false
end)

teleportButton.MouseButton1Click:Connect(hacerTeletransporte)

destroyButton.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

RunService.Heartbeat:Connect(function()
    if isActive and LocalPlayer.Character then
        local root = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if root then
            lastPosition = root.Position
        end
    end
end)

local function onCharacterAdded(character)
    character:WaitForChild("Humanoid").Died:Connect(function()
        task.wait(0.5)
        if lastPosition then
            character:WaitForChild("HumanoidRootPart", 10)
            character:PivotTo(CFrame.new(lastPosition))
        end
    end)
end

LocalPlayer.CharacterAdded:Connect(onCharacterAdded)
if LocalPlayer.Character then onCharacterAdded(LocalPlayer.Character) end

agregarBarraMinimizable(frame, 180, 136, "Teleport Guardado")
agregarLetraA(frame, 180, 136)

-- ==================================================
-- VENTANA 2: PUNTO DE CONTROL
-- ==================================================
local screenGui2 = Instance.new("ScreenGui")
screenGui2.Name = "PuntoDeControl_GUI"
screenGui2.Parent = PlayerGui
screenGui2.ResetOnSpawn = false

local frame2 = Instance.new("Frame")
frame2.Parent = screenGui2
frame2.BackgroundColor3 = COLOR_FONDO
frame2.BackgroundTransparency = TRANSPARENCIA
frame2.Size = UDim2.new(0, 180, 0, 106)
frame2.Position = UDim2.new(0.5, -90, 0.5, -53)
frame2.Active = true
frame2.Draggable = true

local onButton2 = Instance.new("TextButton")
onButton2.Parent = frame2
onButton2.BackgroundColor3 = COLOR_BOTON_ON
onButton2.BackgroundTransparency = TRANSPARENCIA_BOTON_ONOFF
onButton2.Size = UDim2.new(0, 50, 0, 26)
onButton2.Position = UDim2.new(0, 15, 0, 37)
onButton2.Text = "On"
onButton2.TextColor3 = Color3.fromRGB(80, 35, 55)
onButton2.TextScaled = true

local offButton2 = Instance.new("TextButton")
offButton2.Parent = frame2
offButton2.BackgroundColor3 = COLOR_BOTON_OFF
offButton2.BackgroundTransparency = TRANSPARENCIA_BOTON_ONOFF
offButton2.Size = UDim2.new(0, 50, 0, 26)
offButton2.Position = UDim2.new(0, 105, 0, 37)
offButton2.Text = "Off"
offButton2.TextColor3 = Color3.fromRGB(80, 35, 55)
offButton2.TextScaled = true

local destroyButton2 = Instance.new("TextButton")
destroyButton2.Parent = frame2
destroyButton2.BackgroundColor3 = COLOR_BOTON_OTROS
destroyButton2.BackgroundTransparency = TRANSPARENCIA_BOTON_BLANCO
destroyButton2.Size = UDim2.new(0, 150, 0, 26)
destroyButton2.Position = UDim2.new(0, 15, 0, 67)
destroyButton2.Text = "Destroy"
destroyButton2.TextColor3 = COLOR_TEXTO
destroyButton2.TextScaled = true

local statusLabel2 = Instance.new("TextLabel")
statusLabel2.Parent = frame2
statusLabel2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
statusLabel2.BackgroundTransparency = 0.6
statusLabel2.Size = UDim2.new(0, 180, 0, 26)
statusLabel2.Position = UDim2.new(0, 0, 0, 7)
statusLabel2.Text = "Status: Off"
statusLabel2.TextColor3 = COLOR_TEXTO
statusLabel2.TextScaled = true

local checkpoint = nil
local checkpointEnabled = false
local character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
local initialCheckpointY = humanoidRootPart.Position.Y - character.Humanoid.HipHeight - 1

local function createCheckpoint()
    if checkpoint then checkpoint:Destroy() end
    checkpoint = Instance.new("Part")
    checkpoint.Size = Vector3.new(6, 1, 6)
    checkpoint.Anchored = true
    checkpoint.CanCollide = false
    checkpoint.Transparency = 0.75
    checkpoint.BrickColor = BrickColor.new("Hot pink")
    checkpoint.Position = Vector3.new(humanoidRootPart.Position.X, initialCheckpointY, humanoidRootPart.Position.Z)
    checkpoint.Parent = workspace
end

local function updateCheckpointPosition()
    if checkpointEnabled and checkpoint then
        checkpoint.Position = Vector3.new(humanoidRootPart.Position.X, initialCheckpointY, humanoidRootPart.Position.Z)
    end
end

local function teleportToCheckpoint(newCharacter)
    if checkpointEnabled and checkpoint then
        local newHRP = newCharacter:WaitForChild("HumanoidRootPart", 2)
        if newHRP then
            newHRP.CFrame = CFrame.new(checkpoint.Position + Vector3.new(0, 3, 0))
        end
    end
end

onButton2.MouseButton1Click:Connect(function()
    checkpointEnabled = true
    initialCheckpointY = humanoidRootPart.Position.Y - character.Humanoid.HipHeight - 1
    createCheckpoint()
    statusLabel2.Text = "Status: On"
    statusLabel2.TextColor3 = Color3.fromRGB(50, 120, 50)
end)

offButton2.MouseButton1Click:Connect(function()
    checkpointEnabled = false
    if checkpoint then checkpoint:Destroy() end
    statusLabel2.Text = "Status: Off"
    statusLabel2.TextColor3 = Color3.fromRGB(180, 60, 60)
end)

destroyButton2.MouseButton1Click:Connect(function()
    if checkpoint then checkpoint:Destroy() end
    screenGui2:Destroy()
end)

RunService.Heartbeat:Connect(updateCheckpointPosition)

LocalPlayer.CharacterAdded:Connect(function(newChar)
    character = newChar
    humanoidRootPart = newChar:WaitForChild("HumanoidRootPart", 3)
    teleportToCheckpoint(newChar)
end)

agregarBarraMinimizable(frame2, 180, 106, "Punto de Control")
agregarLetraA(frame2, 180, 106)

-- ==================================================
-- VENTANA 3: LISTA DE JUGADORES + TELETRANSPORTE
-- ==================================================
local UserInputService = game:GetService("UserInputService")

local jugadorSeleccionado = nil
local teleportEnabled = false
local originalPositions = {}

-- Ventana 3a: Lista de Jugadores
local screenGuiLista = Instance.new("ScreenGui")
screenGuiLista.Parent = LocalPlayer:WaitForChild("PlayerGui")
screenGuiLista.ResetOnSpawn = false

local frameLista = Instance.new("Frame")
frameLista.Parent = screenGuiLista
frameLista.BackgroundColor3 = COLOR_FONDO
frameLista.BackgroundTransparency = TRANSPARENCIA
frameLista.Size = UDim2.new(0, 220, 0, 316)
frameLista.Position = UDim2.new(0, 20, 0, 20)
frameLista.Active = true
frameLista.Draggable = true

agregarBarraMinimizable(frameLista, 220, 316, "Lista de Jugadores")

local scrollingFrame = Instance.new("ScrollingFrame")
scrollingFrame.Name = "PlayerList"
scrollingFrame.Size = UDim2.new(1, -20, 1, -76)
scrollingFrame.Position = UDim2.new(0, 10, 0, 50)
scrollingFrame.BackgroundColor3 = COLOR_FONDO_LISTA
scrollingFrame.BackgroundTransparency = 0.5
scrollingFrame.BorderSizePixel = 0
scrollingFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
scrollingFrame.ScrollBarThickness = 4
scrollingFrame.ScrollBarImageColor3 = Color3.fromRGB(255, 150, 190)
scrollingFrame.Parent = frameLista

local uiListLayout = Instance.new("UIListLayout")
uiListLayout.FillDirection = Enum.FillDirection.Vertical
uiListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
uiListLayout.SortOrder = Enum.SortOrder.Name
uiListLayout.Padding = UDim.new(0, 6)
uiListLayout.Parent = scrollingFrame

local function actualizarListaJugadores()
    for _, child in ipairs(scrollingFrame:GetChildren()) do
        if child:IsA("Frame") then child:Destroy() end
    end
    local listaJugadores = Players:GetPlayers()
    for _, plr in ipairs(listaJugadores) do
        local playerEntry = Instance.new("Frame")
        playerEntry.Size = UDim2.new(1, -10, 0, 38)
        playerEntry.BackgroundColor3 = (jugadorSeleccionado == plr) and COLOR_SELECCIONADO or COLOR_ENTRY
        playerEntry.BackgroundTransparency = 0.3
        playerEntry.BorderSizePixel = 0
        playerEntry.Parent = scrollingFrame
        local entryCorner = Instance.new("UICorner")
        entryCorner.CornerRadius = UDim.new(0, 4)
        entryCorner.Parent = playerEntry
        local nameLabel = Instance.new("TextLabel")
        nameLabel.Size = UDim2.new(1, -20, 1, 0)
        nameLabel.Position = UDim2.new(0, 10, 0, 0)
        nameLabel.BackgroundTransparency = 1
        nameLabel.Text = plr.DisplayName .. " (@" .. plr.Name .. ")"
        nameLabel.TextColor3 = COLOR_TEXTO
        nameLabel.Font = Enum.Font.GothamSemibold
        nameLabel.TextSize = 14
        nameLabel.TextXAlignment = Enum.TextXAlignment.Left
        nameLabel.Parent = playerEntry
        if plr == LocalPlayer then
            playerEntry.BackgroundColor3 = COLOR_TU
            nameLabel.Text = nameLabel.Text .. "  • TÚ"
        end
        playerEntry.InputBegan:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
                jugadorSeleccionado = plr
                actualizarListaJugadores()
                if statusLabel3 then
                    statusLabel3.Text = "Objetivo: " .. jugadorSeleccionado.Name
                    statusLabel3.TextColor3 = Color3.fromRGB(80, 140, 220)
                end
            end
        end)
    end
    scrollingFrame.CanvasSize = UDim2.new(0, 0, 0, #listaJugadores * 44)
end

Players.PlayerAdded:Connect(actualizarListaJugadores)
Players.PlayerRemoving:Connect(actualizarListaJugadores)

-- Ventana 3b: Teletransportar al Jugador Seleccionado
local screenGui3 = Instance.new("ScreenGui")
screenGui3.Parent = LocalPlayer:WaitForChild("PlayerGui")
screenGui3.ResetOnSpawn = false

local frame3 = Instance.new("Frame")
frame3.Parent = screenGui3
frame3.BackgroundColor3 = COLOR_FONDO
frame3.BackgroundTransparency = TRANSPARENCIA
frame3.Size = UDim2.new(0, 180, 0, 146)
frame3.Position = UDim2.new(0.5, -90, 0.5, -73)
frame3.Active = true
frame3.Draggable = true

agregarBarraMinimizable(frame3, 180, 146, "Teleportar Jugador")

local btnSeleccionarCercano = Instance.new("TextButton")
btnSeleccionarCercano.Parent = frame3
btnSeleccionarCercano.BackgroundColor3 = COLOR_BOTON_OTROS
btnSeleccionarCercano.BackgroundTransparency = TRANSPARENCIA_BOTON_BLANCO
btnSeleccionarCercano.Size = UDim2.new(0, 150, 0, 26)
btnSeleccionarCercano.Position = UDim2.new(0, 15, 0, 37)
btnSeleccionarCercano.Text = "Seleccionar Cercano"
btnSeleccionarCercano.TextColor3 = COLOR_TEXTO
btnSeleccionarCercano.TextScaled = true

local onButton3 = Instance.new("TextButton")
onButton3.Parent = frame3
onButton3.BackgroundColor3 = COLOR_BOTON_ON
onButton3.BackgroundTransparency = TRANSPARENCIA_BOTON_ONOFF
onButton3.Size = UDim2.new(0, 50, 0, 26)
onButton3.Position = UDim2.new(0, 15, 0, 67)
onButton3.Text = "On"
onButton3.TextColor3 = Color3.fromRGB(80, 35, 55)
onButton3.TextScaled = true

local offButton3 = Instance.new("TextButton")
offButton3.Parent = frame3
offButton3.BackgroundColor3 = COLOR_BOTON_OFF
offButton3.BackgroundTransparency = TRANSPARENCIA_BOTON_ONOFF
offButton3.Size = UDim2.new(0, 50, 0, 26)
offButton3.Position = UDim2.new(0, 105, 0, 67)
offButton3.Text = "Off"
offButton3.TextColor3 = Color3.fromRGB(80, 35, 55)
offButton3.TextScaled = true

local destroyButton3 = Instance.new("TextButton")
destroyButton3.Parent = frame3
destroyButton3.BackgroundColor3 = COLOR_BOTON_OTROS
destroyButton3.BackgroundTransparency = TRANSPARENCIA_BOTON_BLANCO
destroyButton3.Size = UDim2.new(0, 150, 0, 26)
destroyButton3.Position = UDim2.new(0, 15, 0, 97)
destroyButton3.Text = "Destroy"
destroyButton3.TextColor3 = COLOR_TEXTO
destroyButton3.TextScaled = true

local statusLabel3 = Instance.new("TextLabel")
statusLabel3.Parent = frame3
statusLabel3.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
statusLabel3.BackgroundTransparency = 0.6
statusLabel3.Size = UDim2.new(0, 180, 0, 26)
statusLabel3.Position = UDim2.new(0, 0, 0, 7)
statusLabel3.Text = "Status: Off | Objetivo: Ninguno"
statusLabel3.TextColor3 = COLOR_TEXTO
statusLabel3.TextScaled = true

local function obtenerJugadorMasCercano()
    local miCaracter = LocalPlayer.Character
    if not miCaracter or not miCaracter:FindFirstChild("HumanoidRootPart") then return nil end
    local miPos = miCaracter.HumanoidRootPart.Position
    local distanciaMinima = math.huge
    local jugadorCercano = nil
    for _, plr in pairs(Players:GetPlayers()) do
        if plr ~= LocalPlayer and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
            local dist = (miPos - plr.Character.HumanoidRootPart.Position).Magnitude
            if dist < distanciaMinima then
                distanciaMinima = dist
                jugadorCercano = plr
            end
        end
    end
    return jugadorCercano
end

local function teleportarJugadorSeleccionado()
    local char = LocalPlayer.Character
    if not char or not char:FindFirstChild("HumanoidRootPart") then return end
    local myHRP = char.HumanoidRootPart
    local target = jugadorSeleccionado
    if not target or not target.Character or not target.Character:FindFirstChild("HumanoidRootPart") then return end
    local tHRP = target.Character.HumanoidRootPart
    if not originalPositions[target] then originalPositions[target] = tHRP.CFrame end
    local nuevaPosicion = myHRP.CFrame * CFrame.new(0, 0, -3)
    tHRP.CFrame = CFrame.lookAt(nuevaPosicion.Position, myHRP.Position) * CFrame.Angles(0, math.rad(180), 0)
end

local function restaurarPosicionOriginal()
    local target = jugadorSeleccionado
    if target and originalPositions[target] and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
        target.Character.HumanoidRootPart.CFrame = originalPositions[target]
    end
end

spawn(function()
    while true do
        if teleportEnabled and jugadorSeleccionado then
            teleportarJugadorSeleccionado()
        end
        wait(0.1)
    end
end)

btnSeleccionarCercano.MouseButton1Click:Connect(function()
    jugadorSeleccionado = obtenerJugadorMasCercano()
    actualizarListaJugadores()
    if jugadorSeleccionado then
        statusLabel3.Text = "Objetivo: " .. jugadorSeleccionado.Name
        statusLabel3.TextColor3 = Color3.fromRGB(80, 140, 220)
    else
        statusLabel3.Text = "No se encontró jugador"
        statusLabel3.TextColor3 = Color3.fromRGB(180, 60, 60)
    end
end)

onButton3.MouseButton1Click:Connect(function()
    if not jugadorSeleccionado then
        statusLabel3.Text = "¡Selecciona un jugador primero!"
        return
    end
    teleportEnabled = true
    statusLabel3.Text = "Status: On | Objetivo: " .. jugadorSeleccionado.Name
    statusLabel3.TextColor3 = Color3.fromRGB(50, 120, 50)
end)

offButton3.MouseButton1Click:Connect(function()
    teleportEnabled = false
    statusLabel3.Text = "Status: Off | Objetivo: " .. (jugadorSeleccionado and jugadorSeleccionado.Name or "Ninguno")
    statusLabel3.TextColor3 = Color3.fromRGB(180, 60, 60)
    restaurarPosicionOriginal()
end)

destroyButton3.MouseButton1Click:Connect(function()
    if teleportEnabled then restaurarPosicionOriginal() end
    screenGuiLista:Destroy()
    screenGui3:Destroy()
end)

agregarLetraA(frame3, 180, 146)
agregarLetraA(frameLista, 220, 316)

task.wait(0.5)
actualizarListaJugadores()

print("✅ ¡Rosa Pastel cargado! 🩷")

