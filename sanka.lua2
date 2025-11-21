-- Dark Neon Menu completo
-- Colar este LocalScript em StarterPlayerScripts

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer

-- Preset colors para ESP
local presetColors = {
	Color3.fromRGB(255,0,0),
	Color3.fromRGB(0,255,0),
	Color3.fromRGB(0,0,255),
	Color3.fromRGB(255,255,0),
	Color3.fromRGB(255,0,255),
	Color3.fromRGB(0,255,255),
	Color3.fromRGB(255,255,255),
}

-- ---------- GUI PRINCIPAL ----------
local gui = Instance.new("ScreenGui")
gui.Name = "DarkNeonMenu"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local frame = Instance.new("Frame", gui)
frame.Name = "MainFrame"
frame.Size = UDim2.new(0, 380, 0, 330)
frame.Position = UDim2.new(0.05, 0, 0.18, 0)
frame.BackgroundColor3 = Color3.fromRGB(12,12,12)
frame.BorderSizePixel = 0
frame.ClipsDescendants = true

-- border neon
local stroke = Instance.new("UIStroke", frame)
stroke.Thickness = 3
stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

task.spawn(function()
	while true do
		stroke.Color = Color3.fromHSV((tick() % 5) / 5, 1, 1)
		task.wait(0.05)
	end
end)

-- Title
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, -20, 0, 30)
title.Position = UDim2.new(0, 10, 0, 6)
title.BackgroundTransparency = 1
title.Text = "Dark Neon Menu"
title.TextColor3 = Color3.new(1,1,1)
title.Font = Enum.Font.GothamSemibold
title.TextSize = 18
title.TextXAlignment = Enum.TextXAlignment.Left

-- Close (minimize) button
local btnClose = Instance.new("TextButton", frame)
btnClose.Size = UDim2.new(0, 28, 0, 28)
btnClose.Position = UDim2.new(1, -36, 0, 6)
btnClose.BackgroundColor3 = Color3.fromRGB(25,25,25)
btnClose.Text = "X"
btnClose.TextColor3 = Color3.new(1,1,1)
btnClose.Font = Enum.Font.GothamBold
btnClose.TextSize = 18
btnClose.BorderSizePixel = 0
btnClose.Name = "MinimizeBtn"

-- Tabs bar
local tabsBar = Instance.new("Frame", frame)
tabsBar.Size = UDim2.new(1, 0, 0, 44)
tabsBar.Position = UDim2.new(0, 0, 0, 40)
tabsBar.BackgroundTransparency = 1

local pages = Instance.new("Frame", frame)
pages.Size = UDim2.new(1, 0, 1, -44-40)
pages.Position = UDim2.new(0, 0, 0, 84)
pages.BackgroundTransparency = 1

local function makeTabButton(text, xpos)
	local b = Instance.new("TextButton", tabsBar)
	b.Size = UDim2.new(0, 110, 1, 0)
	b.Position = UDim2.new(xpos, 0, 0, 0)
	b.BackgroundColor3 = Color3.fromRGB(20,20,20)
	b.TextColor3 = Color3.new(1,1,1)
	b.BorderSizePixel = 0
	b.Text = text
	b.Font = Enum.Font.Gotham
	b.TextSize = 14
	return b
end

local flyTabBtn = makeTabButton("FLY", 0)
local tpTabBtn   = makeTabButton("TELEPORT", 0.29)
local espTabBtn  = makeTabButton("ESP", 0.58)

local flyPage = Instance.new("Frame", pages); flyPage.Size = UDim2.new(1,0,1,0); flyPage.BackgroundTransparency = 1
local tpPage   = Instance.new("Frame", pages); tpPage.Size = UDim2.new(1,0,1,0); tpPage.BackgroundTransparency = 1; tpPage.Visible = false
local espPage  = Instance.new("Frame", pages); espPage.Size = UDim2.new(1,0,1,0); espPage.BackgroundTransparency = 1; espPage.Visible = false

local function openPage(page)
	for _,p in pairs(pages:GetChildren()) do
		if p:IsA("Frame") then p.Visible = false end
	end
	page.Visible = true
end

flyTabBtn.MouseButton1Click:Connect(function() openPage(flyPage) end)
tpTabBtn.MouseButton1Click:Connect(function() openPage(tpPage) end)
espTabBtn.MouseButton1Click:Connect(function() openPage(espPage) end)

-- ---------- ICON MINIMIZADO (RETÂNGULO MINIMALISTA "SANKA SCRIPT" AZUL NEON) ----------
local minimizedIcon = Instance.new("ImageButton", gui)
minimizedIcon.Name = "MinIcon"
minimizedIcon.Size = UDim2.new(0, 160, 0, 40)
minimizedIcon.Position = UDim2.new(0, 10, 0.9, -60)
minimizedIcon.AnchorPoint = Vector2.new(0,0)
minimizedIcon.BackgroundTransparency = 0
minimizedIcon.BackgroundColor3 = Color3.fromRGB(22,22,22)
minimizedIcon.BorderSizePixel = 0
minimizedIcon.Visible = false

-- border neon for icon
local iconStroke = Instance.new("UIStroke", minimizedIcon)
iconStroke.Thickness = 2
iconStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
task.spawn(function()
	while true do
		iconStroke.Color = Color3.fromHSV(((tick()+2) % 5) / 5, 1, 1)
		task.wait(0.06)
	end
end)

local iconText = Instance.new("TextLabel", minimizedIcon)
iconText.Size = UDim2.new(1, -12, 1, 0)
iconText.Position = UDim2.new(0, 6, 0, 0)
iconText.BackgroundTransparency = 1
iconText.Text = "SANKA SCRIPT"
-- azul neon escolhido
iconText.TextColor3 = Color3.fromRGB(0,170,255)
iconText.Font = Enum.Font.GothamBold
iconText.TextSize = 16
iconText.TextXAlignment = Enum.TextXAlignment.Left

-- ---------- DRAGGABLE ----------
local dragging = false
local dragInput, dragStart, startPos

local function updateDrag(input)
	local delta = input.Position - dragStart
	frame.Position = UDim2.new(
		math.clamp(startPos.X.Scale, 0, 1),
		math.clamp(startPos.X.Offset + delta.X, -1000, 1000),
		math.clamp(startPos.Y.Scale, 0, 1),
		math.clamp(startPos.Y.Offset + delta.Y, -1000, 1000)
	)
end

frame.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = true
		dragStart = input.Position
		startPos = frame.Position
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

frame.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement then
		dragInput = input
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if dragging and input == dragInput then
		updateDrag(input)
	end
end)

-- Minimize & Restore
btnClose.MouseButton1Click:Connect(function()
	frame.Visible = false
	minimizedIcon.Visible = true
end)

minimizedIcon.MouseButton1Click:Connect(function()
	frame.Visible = true
	minimizedIcon.Visible = false
end)

-- ---------- ABA 1: FLY (tapete) ----------
do
	local label = Instance.new("TextLabel", flyPage)
	label.Size = UDim2.new(1, -20, 0, 22)
	label.Position = UDim2.new(0, 10, 0, 6)
	label.BackgroundTransparency = 1
	label.Text = "FLY (Tapete flutuante)"
	label.TextColor3 = Color3.new(1,1,1)
	label.Font = Enum.Font.GothamBold
	label.TextSize = 16
	label.TextXAlignment = Enum.TextXAlignment.Left

	local flyToggle = Instance.new("TextButton", flyPage)
	flyToggle.Size = UDim2.new(0, 220, 0, 44)
	flyToggle.Position = UDim2.new(0, 10, 0, 36)
	flyToggle.Text = "Ativar Fly"
	flyToggle.BackgroundColor3 = Color3.fromRGB(20,20,20)
	flyToggle.TextColor3 = Color3.new(1,1,1)
	flyToggle.BorderSizePixel = 0

	local speedLabel = Instance.new("TextLabel", flyPage)
	speedLabel.Size = UDim2.new(0, 200, 0, 20)
	speedLabel.Position = UDim2.new(0, 240, 0, 42)
	speedLabel.BackgroundTransparency = 1
	speedLabel.Text = "Velocidade: 50"
	speedLabel.TextColor3 = Color3.new(1,1,1)
	speedLabel.Font = Enum.Font.Gotham
	speedLabel.TextSize = 12
	speedLabel.TextXAlignment = Enum.TextXAlignment.Left

	local increase = Instance.new("TextButton", flyPage)
	increase.Size = UDim2.new(0, 24, 0, 24)
	increase.Position = UDim2.new(0, 340, 0, 36)
	increase.Text = "+"
	increase.BackgroundColor3 = Color3.fromRGB(30,30,30)
	increase.TextColor3 = Color3.new(1,1,1)
	increase.BorderSizePixel = 0

	local decrease = increase:Clone()
	decrease.Parent = flyPage
	decrease.Position = UDim2.new(0, 310, 0, 36)
	decrease.Text = "-"

	local flying = false
	local carpet = nil
	local speed = 50

	local function createCarpet()
		if carpet and carpet.Parent then return end
		carpet = Instance.new("Part")
		carpet.Size = Vector3.new(6,1,6)
		carpet.Color = Color3.fromRGB(10,10,10)
		carpet.Material = Enum.Material.Neon
		carpet.Anchored = true
		carpet.CanCollide = true
		carpet.Name = "FlyingCarpet"
		carpet.Parent = workspace
	end

	local function updateCarpet()
		while flying and carpet do
			local char = player.Character
			if not char then task.wait(0.1); continue end
			local root = char:FindFirstChild("HumanoidRootPart")
			if not root then task.wait(0.1); continue end

			carpet.Position = root.Position - Vector3.new(0,3,0)

			local move = Vector3.zero
			if UserInputService:IsKeyDown(Enum.KeyCode.W) then move += root.CFrame.LookVector end
			if UserInputService:IsKeyDown(Enum.KeyCode.S) then move -= root.CFrame.LookVector end
			if UserInputService:IsKeyDown(Enum.KeyCode.A) then move -= root.CFrame.RightVector end
			if UserInputService:IsKeyDown(Enum.KeyCode.D) then move += root.CFrame.RightVector end

			local dt = task.wait(0.03)
			if move.Magnitude > 0 then
				carpet.Position = carpet.Position + move.Unit * speed * dt
			end
		end
	end

	flyToggle.MouseButton1Click:Connect(function()
		flying = not flying
		if flying then
			flyToggle.Text = "Desativar Fly"
			if not carpet then createCarpet() end
			task.spawn(updateCarpet)
		else
			flyToggle.Text = "Ativar Fly"
			if carpet then carpet:Destroy(); carpet = nil end
		end
	end)

	increase.MouseButton1Click:Connect(function()
		speed = speed + 10
		speedLabel.Text = "Velocidade: " .. tostring(speed)
	end)
	decrease.MouseButton1Click:Connect(function()
		speed = math.max(10, speed - 10)
		speedLabel.Text = "Velocidade: " .. tostring(speed)
	end)
end

-- ---------- ABA 2: TELEPORT ----------
do
	local label = Instance.new("TextLabel", tpPage)
	label.Size = UDim2.new(1, -20, 0, 22)
	label.Position = UDim2.new(0, 10, 0, 6)
	label.BackgroundTransparency = 1
	label.Text = "TELEPORT - clique em um jogador para ir até ele"
	label.TextColor3 = Color3.new(1,1,1)
	label.Font = Enum.Font.GothamBold
	label.TextSize = 16
	label.TextXAlignment = Enum.TextXAlignment.Left

	local scroll = Instance.new("ScrollingFrame", tpPage)
	scroll.Size = UDim2.new(1, -20, 1, -40)
	scroll.Position = UDim2.new(0, 10, 0, 36)
	scroll.BackgroundTransparency = 1
	scroll.ScrollBarThickness = 6

	local layout = Instance.new("UIListLayout", scroll)
	layout.Padding = UDim.new(0,6)
	layout.SortOrder = Enum.SortOrder.LayoutOrder

	local function refresh()
		for _,c in pairs(scroll:GetChildren()) do
			if c:IsA("TextButton") then c:Destroy() end
		end
		for _,pl in pairs(Players:GetPlayers()) do
			if pl ~= player then
				local btn = Instance.new("TextButton", scroll)
				btn.Size = UDim2.new(1, -10, 0, 36)
				btn.Text = "Teleportar -> " .. pl.Name
				btn.BackgroundColor3 = Color3.fromRGB(20,20,20)
				btn.TextColor3 = Color3.new(1,1,1)
				btn.BorderSizePixel = 0
				btn.Font = Enum.Font.Gotham
				btn.TextSize = 14

				btn.MouseButton1Click:Connect(function()
					local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
					local target = pl.Character and pl.Character:FindFirstChild("HumanoidRootPart")
					if root and target then
						root.CFrame = target.CFrame + Vector3.new(0,2,0)
					end
				end)
			end
		end
		scroll.CanvasSize = UDim2.new(0,0,0, layout.AbsoluteContentSize.Y + 10)
	end

	refresh()
	Players.PlayerAdded:Connect(refresh)
	Players.PlayerRemoving:Connect(refresh)
end

-- ---------- ABA 3: ESP (Highlight, Line, Box 3D) ----------
do
	local label = Instance.new("TextLabel", espPage)
	label.Size = UDim2.new(1, -20, 0, 22)
	label.Position = UDim2.new(0, 10, 0, 6)
	label.BackgroundTransparency = 1
	label.Text = "ESP - Highlight / Line / Box 3D"
	label.TextColor3 = Color3.new(1,1,1)
	label.Font = Enum.Font.GothamBold
	label.TextSize = 16
	label.TextXAlignment = Enum.TextXAlignment.Left

	-- Buttons & color pickers (preset cycling)
	local btnHighlight = Instance.new("TextButton", espPage)
	btnHighlight.Size = UDim2.new(0, 160, 0, 36)
	btnHighlight.Position = UDim2.new(0, 10, 0, 36)
	btnHighlight.Text = "ESP Highlight"
	btnHighlight.BackgroundColor3 = Color3.fromRGB(20,20,20)
	btnHighlight.TextColor3 = Color3.new(1,1,1)
	btnHighlight.BorderSizePixel = 0

	local colorHLBtn = Instance.new("TextButton", espPage)
	colorHLBtn.Size = UDim2.new(0, 36, 0, 36)
	colorHLBtn.Position = UDim2.new(0, 180, 0, 36)
	colorHLBtn.Text = ""
	colorHLBtn.BackgroundColor3 = presetColors[3] -- default blue
	colorHLBtn.BorderSizePixel = 0

	local btnLine = Instance.new("TextButton", espPage)
	btnLine.Size = UDim2.new(0, 160, 0, 36)
	btnLine.Position = UDim2.new(0, 10, 0, 86)
	btnLine.Text = "ESP Line"
	btnLine.BackgroundColor3 = Color3.fromRGB(20,20,20)
	btnLine.TextColor3 = Color3.new(1,1,1)
	btnLine.BorderSizePixel = 0

	local colorLineBtn = colorHLBtn:Clone(); colorLineBtn.Parent = espPage
	colorLineBtn.Position = UDim2.new(0, 180, 0, 86)
	colorLineBtn.BackgroundColor3 = presetColors[2]

	local btnBox = Instance.new("TextButton", espPage)
	btnBox.Size = UDim2.new(0, 160, 0, 36)
	btnBox.Position = UDim2.new(0, 10, 0, 136)
	btnBox.Text = "ESP Box 3D"
	btnBox.BackgroundColor3 = Color3.fromRGB(20,20,20)
	btnBox.TextColor3 = Color3.new(1,1,1)
	btnBox.BorderSizePixel = 0

	local colorBoxBtn = colorHLBtn:Clone(); colorBoxBtn.Parent = espPage
	colorBoxBtn.Position = UDim2.new(0, 180, 0, 136)
	colorBoxBtn.BackgroundColor3 = presetColors[1]

	local statusHL = Instance.new("TextLabel", espPage)
	statusHL.Size = UDim2.new(0, 180, 0, 20)
	statusHL.Position = UDim2.new(0, 10, 0, 180)
	statusHL.BackgroundTransparency = 1
	statusHL.Text = "Highlight: OFF"
	statusHL.TextColor3 = Color3.new(1,1,1)
	statusHL.Font = Enum.Font.Gotham
	statusHL.TextSize = 12
	statusHL.TextXAlignment = Enum.TextXAlignment.Left

	local statusLine = statusHL:Clone(); statusLine.Parent = espPage
	statusLine.Position = UDim2.new(0, 10, 0, 200)
	statusLine.Text = "Line: OFF"

	local statusBox = statusHL:Clone(); statusBox.Parent = espPage
	statusBox.Position = UDim2.new(0, 10, 0, 220)
	statusBox.Text = "Box: OFF"

	-- States and tables
	local highlightEnabled = false
	local highlights = {}

	local lineEnabled = false
	local lines = {}

	local boxEnabled = false
	local boxes = {}

	-- helpers
	local function applyHighlightToPlayer(plr, color)
		if not plr.Character then return end
		if highlights[plr] then highlights[plr]:Destroy(); highlights[plr] = nil end
		local hl = Instance.new("Highlight")
		hl.Name = "ESP_Highlight"
		hl.FillColor = color
		hl.OutlineColor = Color3.new(1,1,1)
		hl.FillTransparency = 0.5
		hl.Parent = plr.Character
		highlights[plr] = hl
	end

	local function removeHighlightFromPlayer(plr)
		if highlights[plr] then highlights[plr]:Destroy(); highlights[plr] = nil end
	end

	local function createLineForPlayer(plr, color)
		if lines[plr] then lines[plr]:Destroy(); lines[plr] = nil end
		local p = Instance.new("Part")
		p.Name = "ESP_Line_"..plr.Name
		p.Anchored = true
		p.CanCollide = false
		p.Material = Enum.Material.Neon
		p.Color = color
		p.Size = Vector3.new(0.12, 0.12, 1)
		p.Parent = workspace
		lines[plr] = p
	end

	local function removeLineForPlayer(plr)
		if lines[plr] then lines[plr]:Destroy(); lines[plr] = nil end
	end

	local function createBoxForPlayer(plr, color)
		if boxes[plr] then boxes[plr]:Destroy(); boxes[plr] = nil end
		if not plr.Character then return end
		local head = plr.Character:FindFirstChild("Head") or plr.Character:FindFirstChild("HumanoidRootPart")
		if not head then return end
		local box = Instance.new("BoxHandleAdornment")
		box.Name = "ESP_Box_"..plr.Name
		box.Adornee = head
		box.AlwaysOnTop = true
		box.ZIndex = 5
		box.Color3 = color
		box.Transparency = 0.4
		box.Size = Vector3.new(2.5, 4, 1.5)
		box.Parent = workspace
		boxes[plr] = box
	end

	local function removeBoxForPlayer(plr)
		if boxes[plr] then boxes[plr]:Destroy(); boxes[plr] = nil end
	end

	-- enable/disable all
	local function enableAllHighlights(color)
		highlightEnabled = true
		for _,pl in pairs(Players:GetPlayers()) do
			if pl ~= player and pl.Character then
				applyHighlightToPlayer(pl, color)
			end
		end
	end
	local function disableAllHighlights()
		highlightEnabled = false
		for pl,_ in pairs(highlights) do
			if highlights[pl] then highlights[pl]:Destroy() end
		end
		highlights = {}
	end

	local function enableAllLines(color)
		lineEnabled = true
		for _,pl in pairs(Players:GetPlayers()) do
			if pl ~= player and pl.Character then
				createLineForPlayer(pl, color)
			end
		end
	end
	local function disableAllLines()
		lineEnabled = false
		for pl,_ in pairs(lines) do
			if lines[pl] then lines[pl]:Destroy() end
		end
		lines = {}
	end

	local function enableAllBoxes(color)
		boxEnabled = true
		for _,pl in pairs(Players:GetPlayers()) do
			if pl ~= player and pl.Character then
				createBoxForPlayer(pl, color)
			end
		end
	end
	local function disableAllBoxes()
		boxEnabled = false
		for pl,_ in pairs(boxes) do
			if boxes[pl] then boxes[pl]:Destroy() end
		end
		boxes = {}
	end

	-- update lines each frame
	RunService.RenderStepped:Connect(function()
		if lineEnabled then
			for pl,part in pairs(lines) do
				if pl.Character and pl.Character.Parent then
					local head = pl.Character:FindFirstChild("Head")
					local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
					if head and root then
						local dir = head.Position - root.Position
						local dist = dir.Magnitude
						part.Size = Vector3.new(0.12, 0.12, dist)
						part.CFrame = CFrame.new(root.Position, head.Position) * CFrame.new(0,0,-dist/2)
					else
						removeLineForPlayer(pl)
					end
				else
					removeLineForPlayer(pl)
				end
			end
		end
	end)

	-- react to players joining/leaving
	Players.PlayerAdded:Connect(function(pl)
		pl.CharacterAdded:Connect(function()
			task.wait(0.2)
			if highlightEnabled then applyHighlightToPlayer(pl, colorHLBtn.BackgroundColor3) end
			if lineEnabled then createLineForPlayer(pl, colorLineBtn.BackgroundColor3) end
			if boxEnabled then createBoxForPlayer(pl, colorBoxBtn.BackgroundColor3) end
		end)
	end)

	Players.PlayerRemoving:Connect(function(pl)
		removeHighlightFromPlayer(pl)
		removeLineForPlayer(pl)
		removeBoxForPlayer(pl)
	end)

	-- cycle color helper
	local function cycleColor(btn)
		local cur = btn.BackgroundColor3
		local idx = 1
		for i,c in ipairs(presetColors) do
			if c == cur then idx = i; break end
		end
		local nexti = (idx % #presetColors) + 1
		btn.BackgroundColor3 = presetColors[nexti]
	end

	colorHLBtn.MouseButton1Click:Connect(function()
		cycleColor(colorHLBtn)
		if highlightEnabled then
			for pl,_ in pairs(highlights) do
				applyHighlightToPlayer(pl, colorHLBtn.BackgroundColor3)
			end
		end
	end)

	colorLineBtn.MouseButton1Click:Connect(function()
		cycleColor(colorLineBtn)
		if lineEnabled then
			for pl,_ in pairs(lines) do
				removeLineForPlayer(pl)
				createLineForPlayer(pl, colorLineBtn.BackgroundColor3)
			end
		end
	end)

	colorBoxBtn.MouseButton1Click:Connect(function()
		cycleColor(colorBoxBtn)
		if boxEnabled then
			for pl,_ in pairs(boxes) do
				removeBoxForPlayer(pl)
				createBoxForPlayer(pl, colorBoxBtn.BackgroundColor3)
			end
		end
	end)

	-- buttons on/off
	btnHighlight.MouseButton1Click:Connect(function()
		if highlightEnabled then
			disableAllHighlights()
			btnHighlight.Text = "ESP Highlight"
			statusHL.Text = "Highlight: OFF"
		else
			enableAllHighlights(colorHLBtn.BackgroundColor3)
			btnHighlight.Text = "Desativar Highlight"
			statusHL.Text = "Highlight: ON"
		end
	end)

	btnLine.MouseButton1Click:Connect(function()
		if lineEnabled then
			disableAllLines()
			btnLine.Text = "ESP Line"
			statusLine.Text = "Line: OFF"
		else
			enableAllLines(colorLineBtn.BackgroundColor3)
			btnLine.Text = "Desativar Line"
			statusLine.Text = "Line: ON"
		end
	end)

	btnBox.MouseButton1Click:Connect(function()
		if boxEnabled then
			disableAllBoxes()
			btnBox.Text = "ESP Box 3D"
			statusBox.Text = "Box: OFF"
		else
			enableAllBoxes(colorBoxBtn.BackgroundColor3)
			btnBox.Text = "Desativar Box"
			statusBox.Text = "Box: ON"
		end
	end)
end

-- Done
print("[DarkNeonMenu] Carregado com sucesso.")
