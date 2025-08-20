
<header>Optical UI Lib Documentation</header>

<main>
<section>
<h2>Getting Started</h2>
<p>Include this code in a LocalScript to initialize the PlatWare UI:</p>
<pre><code>local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local UIS = game:GetService("UserInputService")

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "Optical"-- your screenGui's name
screenGui.Parent = player:WaitForChild("PlayerGui")
screenGui.ResetOnSpawn = false

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 500, 0, 300)
mainFrame.Position = UDim2.new(0.5, -250, 0.5, -150)
mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
mainFrame.BorderSizePixel = 0
mainFrame.ClipsDescendants = true
mainFrame.Parent = screenGui
Instance.new("UICorner", mainFrame).CornerRadius = UDim.new(0, 8)
Instance.new("UIStroke", mainFrame).Color = Color3.fromRGB(80, 80, 80)

local topPanel = Instance.new("Frame", mainFrame)
topPanel.Size = UDim2.new(1, 0, 0, 35)
topPanel.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Instance.new("UICorner", topPanel).CornerRadius = UDim.new(0, 8)
Instance.new("UIStroke", topPanel).Color = Color3.fromRGB(60, 60, 60)

local title = Instance.new("TextLabel", topPanel)
title.Size = UDim2.new(1, -80, 1, 0)
title.Position = UDim2.new(0, 10, 0, 0)
title.BackgroundTransparency = 1
title.Text = "Optical"-- your script's title
title.TextColor3 = Color3.fromRGB(200, 200, 200)
title.TextSize = 18
title.Font = Enum.Font.GothamBold
title.TextXAlignment = Enum.TextXAlignment.Left

local minimizeBtn = Instance.new("TextButton", topPanel)
minimizeBtn.Size = UDim2.new(0, 35, 0, 25)
minimizeBtn.Position = UDim2.new(1, -70, 0.5, -12)
minimizeBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
minimizeBtn.Text = "-"
minimizeBtn.TextSize = 20
minimizeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
minimizeBtn.Font = Enum.Font.GothamBold
Instance.new("UICorner", minimizeBtn).CornerRadius = UDim.new(0, 5)

local closeBtn = Instance.new("TextButton", topPanel)
closeBtn.Size = UDim2.new(0, 35, 0, 25)
closeBtn.Position = UDim2.new(1, -35, 0.5, -12)
closeBtn.BackgroundColor3 = Color3.fromRGB(100, 40, 40)
closeBtn.Text = "X"
closeBtn.TextSize = 18
closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
closeBtn.Font = Enum.Font.GothamBold
Instance.new("UICorner", closeBtn).CornerRadius = UDim.new(0, 5)

local contentFrame = Instance.new("Frame", mainFrame)
contentFrame.Size = UDim2.new(1, 0, 1, -35)
contentFrame.Position = UDim2.new(0, 0, 0, 35)
contentFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Instance.new("UICorner", contentFrame).CornerRadius = UDim.new(0, 8)

local sidebar = Instance.new("Frame", contentFrame)
sidebar.Size = UDim2.new(0, 120, 1, 0)
sidebar.Position = UDim2.new(0, 0, 0, 0)
sidebar.BackgroundTransparency = 1
local sideLayout = Instance.new("UIListLayout", sidebar)
sideLayout.FillDirection = Enum.FillDirection.Vertical
sideLayout.SortOrder = Enum.SortOrder.LayoutOrder
sideLayout.Padding = UDim.new(0,5)

local categoryContentParent = Instance.new("Frame", contentFrame)
categoryContentParent.Size = UDim2.new(1, -120, 1, 0)
categoryContentParent.Position = UDim2.new(0, 120, 0, 0)
categoryContentParent.BackgroundTransparency = 1
local contentLayout = Instance.new("UIListLayout", categoryContentParent)
contentLayout.FillDirection = Enum.FillDirection.Vertical
contentLayout.SortOrder = Enum.SortOrder.LayoutOrder
contentLayout.Padding = UDim.new(0,5)

local tweenInfo = TweenInfo.new(0.4, Enum.EasingStyle.Quint, Enum.EasingDirection.Out)
local minimized = false

minimizeBtn.MouseButton1Click:Connect(function()
	if minimized then
		TweenService:Create(mainFrame, tweenInfo, {Size = UDim2.new(0, 500, 0, 300)}):Play()
	else
		TweenService:Create(mainFrame, tweenInfo, {Size = UDim2.new(0, 500, 0, 35)}):Play()
	end
	minimized = not minimized
end)

closeBtn.MouseButton1Click:Connect(function()
	local tween1 = TweenService:Create(mainFrame, tweenInfo, {Size = UDim2.new(mainFrame.Size.X.Scale, mainFrame.Size.X.Offset, 0, 35)})
	tween1:Play()
	tween1.Completed:Wait()
	local tween2 = TweenService:Create(mainFrame, tweenInfo, {Size = UDim2.new(0, 0, 0, 35), Position = UDim2.new(0.5, 0, mainFrame.Position.Y.Scale, mainFrame.Position.Y.Offset)})
	tween2:Play()
	tween2.Completed:Wait()
	screenGui:Destroy()
end)

do
	local dragging = false
	local dragInput, dragStart, startPos
	local function update(input)
		local delta = input.Position - dragStart
		mainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X,
			startPos.Y.Scale, startPos.Y.Offset + delta.Y)
	end

	topPanel.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 then
			dragging = true
			dragStart = input.Position
			startPos = mainFrame.Position
			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
				end
			end)
		end
	end)

	topPanel.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement then
			dragInput = input
		end
	end)

	UIS.InputChanged:Connect(function(input)
		if input == dragInput and dragging then
			update(input)
		end
	end)
end

local UI = {}
UI.Categories = {}

function UI:MakeCat(opts)
	local cat = {}
	local name = opts.Name or "Category"

	cat.Frame = Instance.new("Frame", categoryContentParent)
	cat.Frame.Size = UDim2.new(1, 0, 0, 0)
	cat.Frame.BackgroundTransparency = 1
	cat.Frame.Visible = false
	local catLayout = Instance.new("UIListLayout", cat.Frame)
	catLayout.FillDirection = Enum.FillDirection.Vertical
	catLayout.SortOrder = Enum.SortOrder.LayoutOrder
	catLayout.Padding = UDim.new(0,5)

	cat.Button = Instance.new("TextButton", sidebar)
	cat.Button.Size = UDim2.new(1, 0, 0, 35)
	cat.Button.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
	cat.Button.Text = name
	cat.Button.TextColor3 = Color3.fromRGB(220, 220, 220)
	cat.Button.Font = Enum.Font.Gotham
	cat.Button.TextSize = 16
	Instance.new("UICorner", cat.Button).CornerRadius = UDim.new(0, 6)

	cat.Button.MouseButton1Click:Connect(function()
		for _,c in pairs(UI.Categories) do
			c.Frame.Visible = false
			c.Button.BackgroundColor3 = Color3.fromRGB(60,60,60)
		end
		cat.Frame.Visible = true
		cat.Button.BackgroundColor3 = Color3.fromRGB(100,100,100)
	end)

	function cat:AddLabel(text)
		local lbl = Instance.new("TextLabel", cat.Frame)
		lbl.Size = UDim2.new(1,0,0,25)
		lbl.BackgroundTransparency = 1
		lbl.Text = text
		lbl.TextColor3 = Color3.fromRGB(200,200,200)
		lbl.Font = Enum.Font.Gotham
		lbl.TextSize = 14
	end

	function cat:AddButton(opts)
		local btn = Instance.new("TextButton", cat.Frame)
		btn.Size = UDim2.new(1,0,0,30)
		btn.BackgroundColor3 = Color3.fromRGB(60,60,60)
		btn.TextColor3 = Color3.fromRGB(255,255,255)
		btn.Font = Enum.Font.Gotham
		btn.TextSize = 16
		btn.Text = opts.Name or "Button"
		Instance.new("UICorner", btn).CornerRadius = UDim.new(0,6)
		btn.MouseButton1Click:Connect(function()
			if opts.Callback then opts.Callback() end
		end)
	end

	function cat:AddToggle(opts)
		local toggleBtn = Instance.new("TextButton", cat.Frame)
		toggleBtn.Size = UDim2.new(1,0,0,30)
		toggleBtn.BackgroundColor3 = Color3.fromRGB(60,60,60)
		toggleBtn.TextColor3 = Color3.fromRGB(255,255,255)
		toggleBtn.Font = Enum.Font.Gotham
		toggleBtn.TextSize = 16
		local state = opts.Default or false
		toggleBtn.Text = opts.Name.." ["..(state and "ON" or "OFF").."]"
		toggleBtn.MouseButton1Click:Connect(function()
			state = not state
			toggleBtn.Text = opts.Name.." ["..(state and "ON" or "OFF").."]"
			if opts.Callback then opts.Callback(state) end
		end)
	end

	function cat:AddSlider(opts)
		local sliderFrame = Instance.new("Frame", cat.Frame)
		sliderFrame.Size = UDim2.new(1,0,0,40)
		sliderFrame.BackgroundTransparency = 1

		local label = Instance.new("TextLabel", sliderFrame)
		label.Size = UDim2.new(1,0,0,15)
		label.BackgroundTransparency = 1
		label.Text = opts.Name.." ["..(opts.Default or 0).."]"
		label.TextColor3 = Color3.fromRGB(200,200,200)
		label.Font = Enum.Font.Gotham
		label.TextSize = 14
		label.TextXAlignment = Enum.TextXAlignment.Left

		local barBackground = Instance.new("Frame", sliderFrame)
		barBackground.Size = UDim2.new(1,0,0,15)
		barBackground.Position = UDim2.new(0,0,0,20)
		barBackground.BackgroundColor3 = Color3.fromRGB(60,60,60)
		Instance.new("UICorner", barBackground).CornerRadius = UDim.new(0,6)

		local barFill = Instance.new("Frame", barBackground)
		barFill.Size = UDim2.new((opts.Default or 0)/ (opts.Max or 100),0,1,0)
		barFill.BackgroundColor3 = Color3.fromRGB(100,100,255)
		Instance.new("UICorner", barFill).CornerRadius = UDim.new(0,6)

		local dragging = false
		barBackground.InputBegan:Connect(function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 then
				dragging = true
			end
		end)

		barBackground.InputEnded:Connect(function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 then
				dragging = false
			end
		end)

		UIS.InputChanged:Connect(function(input)
			if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
				local mousePos = input.Position.X
				local relativePos = math.clamp(mousePos - barBackground.AbsolutePosition.X, 0, barBackground.AbsoluteSize.X)
				local value = math.floor((relativePos / barBackground.AbsoluteSize.X) * (opts.Max or 100))
				barFill.Size = UDim2.new(relativePos / barBackground.AbsoluteSize.X, 0, 1, 0)
				label.Text = opts.Name.." ["..value.."]"
				if opts.Callback then opts.Callback(value) end
			end
		end)
	end

	table.insert(UI.Categories, cat)
	return cat
end
</code></pre>
</section>

<section>
<h2>Creating Categories</h2>
<p>Use <code>UI:MakeCat()</code> to create sidebar categories:</p>
<pre><code>local Cat = UI:MakeCat({ Name = "Characters" })</code></pre>
</section>

<section>
<h2>Adding Labels</h2>
<p>Add simple text labels inside a category:</p>
<pre><code>Cat:AddLabel("Player Options")</code></pre>
</section>

<section>
<h2>Adding Buttons</h2>
<p>Create interactive buttons with a callback function:</p>
<pre><code>Cat:AddButton({
    Name = "Reset Character",
    Callback = function()
        print("Button clicked!")
    end
})</code></pre>
</section>

<section>
<h2>Adding Toggles</h2>
<p>Add a toggle switch:</p>
<pre><code>Cat:AddToggle({
    Name = "Enable Fly",
    Default = false,
    Callback = function(state)
        print("Toggle is now", state and "ON" or "OFF")
    end
})</code></pre>
<p>The button automatically shows <code>[ON]</code> or <code>[OFF]</code> based on the state.</p>
</section>

<section>
<h2>Adding Sliders</h2>
<p>Use sliders for numeric input:</p>
<pre><code>Cat:AddSlider({
    Name = "Speed",
    Default = 50,
    Max = 100,
    Callback = function(value)
        print("Slider value:", value)
    end
})</code></pre>
</section>

<section>
<h2>Adding Dropdowns</h2>
<p>Use Dropdowns for selection:</p>
<pre><code>Cat:AddDropdown({
    Name = "Select",
    Options = {"Option1", "Option2", "Option3"},
    Default = "Option1",
    Callback = function(selectedOption)
        print("Selected:", selectedOption)
    end
})</code></pre>
</section>

<<section>
<h2>Ending Lib</h2>
<p>Put this at the end of your script when youre done coding</p>
<pre><code>return UI</code></pre>
<p>This is REQUIRED for the code to work</p>
</section>

</main>
</body>
</html>
