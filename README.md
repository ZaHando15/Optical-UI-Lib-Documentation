<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Optical UI Library – Docs</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    :root {
      --bg: #0d1117;
      --card: #161b22;
      --border: #30363d;
      --text: #c9d1d9;
      --accent: #58a6ff;
      --green: #3fb950;
    }
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    body {
      background: var(--bg);
      color: var(--text);
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
      line-height: 1.6;
    }
    a {
      color: var(--accent);
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }
    header {
      padding: 3rem 1rem;
      text-align: center;
      border-bottom: 1px solid var(--border);
    }
    header h1 {
      font-size: 2.5rem;
      letter-spacing: -1px;
    }
    header p {
      font-size: 1.1rem;
      opacity: .8;
      margin-top: .5rem;
    }
    .container {
      max-width: 900px;
      margin: auto;
      padding: 2rem 1rem;
    }
    .snippet {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1rem;
      margin: 1rem 0;
      position: relative;
      overflow-x: auto;
    }
    .snippet code {
      color: var(--green);
      font-family: "SFMono-Regular", Consolas, "Liberation Mono", Menlo, monospace;
      font-size: .9rem;
    }
    .snippet::before {
      content: "Lua";
      position: absolute;
      top: .5rem;
      right: .75rem;
      background: var(--border);
      color: var(--text);
      padding: .15rem .4rem;
      border-radius: 4px;
      font-size: .75rem;
      font-weight: 600;
    }
    h2 {
      margin-top: 2.5rem;
      margin-bottom: 1rem;
      font-size: 1.75rem;
      border-left: 4px solid var(--accent);
      padding-left: .75rem;
    }
    h3 {
      margin-top: 2rem;
      margin-bottom: .5rem;
      font-size: 1.25rem;
    }
    ul {
      padding-left: 1.25rem;
    }
    li {
      margin: .25rem 0;
    }
    .install-box {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1.25rem;
      margin-bottom: 2rem;
    }
    .install-box code {
      display: block;
      color: var(--green);
      font-size: 1rem;
      white-space: pre;
      overflow-x: auto;
    }
    footer {
      text-align: center;
      padding: 2rem 1rem;
      font-size: .9rem;
      opacity: .7;
      border-top: 1px solid var(--border);
      margin-top: 3rem;
    }
  </style>
</head>

<body>
  <header>
    <h1>Optical UI Library</h1>
    <p>Lightweight, drop-in Roblox UI library – no dependencies, full feature set.</p>
  </header>

  <div class="container">
    <!-- Installation -->
    <h2>⚙️ Installation</h2>
    <div class="install-box">
      <code>local UI = loadstring(game:HttpGet("YOUR_RAW_GITHUB_LINK"))()</code>
    </div>

    <!-- Quick Start -->
    <h2>🚀 Quick Start</h2>
    <div class="snippet">
      <code>local Main = UI:MakeCat({Name = "Main"})

Main:AddToggle({
    Name = "God Mode",
    Default = false,
    Callback = function(on)
        -- Function
    end
})</code>
    </div>

    <!-- Controls -->
    <h2>📦 Controls</h2>
    <ul>
      <li><strong>Label</strong> – <code>AddLabel(text)</code></li>
      <li><strong>Button</strong> – <code>AddButton(opts)</code></li>
      <li><strong>Checkbox Toggle</strong> – <code>AddToggle(opts)</code></li>
      <li><strong>Keybind</strong> – <code>AddKeybind(opts)</code></li>
      <li><strong>Slider</strong> – <code>AddSlider(opts)</code></li>
      <li><strong>Dropdown</strong> – <code>AddDropdown(opts)</code></li>
      <li><strong>Color Picker</strong> – <code>AddColorPicker(opts)</code></li>
    </ul>

    <!-- Label -->
    <h3>1. Label</h3>
    <div class="snippet"><code>Cat:AddLabel("Information text")</code></div>

    <!-- Button -->
    <h3>2. Button</h3>
    <div class="snippet"><code>Cat:AddButton({
    Name = "Kill All",
    Callback = function()
        -- Function
    end
})</code></div>

    <!-- Toggle -->
    <h3>3. Checkbox Toggle <small>(left-side decal)</small></h3>
    <div class="snippet"><code>Cat:AddToggle({
    Name = "ESP",
    Default = false,
    Callback = function(state) -- bool
        -- Function
    end
})</code></div>

    <!-- Keybind -->
    <h3>4. Keybind <small>(left-side decal)</small></h3>
    <div class="snippet"><code>Cat:AddKeybind({
    Name = "Toggle Fly",
    Callback = function()
        -- Function
    end
})</code></div>

    <!-- Slider -->
    <h3>5. Slider</h3>
    <div class="snippet"><code>Cat:AddSlider({
    Name = "WalkSpeed",
    Default = 16,
    Max = 200,
    Callback = function(value) -- integer 0-200
        -- Function
    end
})</code></div>

    <!-- Dropdown -->
    <h3>6. Dropdown <small>(multi-select)</small></h3>
    <div class="snippet"><code>Cat:AddDropdown({
    Name = "Teleports",
    Options = {"Spawn", "Base", "Shop"},
    Default = {"Spawn"},
    Callback = function(selected) -- table of strings
        -- Function
    end
})</code></div>

    <!-- Color Picker -->
    <h3>7. Color Picker <small>(HSV square + hue bar)</small></h3>
    <div class="snippet"><code>Cat:AddColorPicker({
    Name = "ESP Colour",
    Default = Color3.fromRGB(255,0,0),
    Callback = function(color) -- Color3
        -- Function
    end
})</code></div>

    <!-- Window Controls -->
    <h2>🪟 Window Controls</h2>
    <ul>
      <li><strong>Drag</strong> – grab top bar</li>
      <li><strong>Minimize</strong> – <kbd>-</kbd> button</li>
      <li><strong>Close</strong> – <kbd>X</kbd> button (smooth destroy)</li>
    </ul>

    <!-- Global Keybind Table -->
    <h2>🧪 Global Keybind Table</h2>
    <p>All binds live in <code>UI.Keybinds</code> (array):</p>
    <div class="snippet"><code>for _,k in pairs(UI.Keybinds) do
    print(k.Name, k.Key.Name)
end</code></div>

    <!-- Full Example -->
    <h2>📄 Full Example Tab</h2>
    <div class="snippet"><code>local Visuals = UI:MakeCat({Name = "Visuals"})

Visuals:AddToggle({Name = "ESP", Default = false, Callback = function(v)
    -- Function
end})

Visuals:AddKeybind({Name = "Toggle Fly", Callback = function()
    -- Function
end})

Visuals:AddColorPicker({Name = "ESP Colour", Default = Color3.new(1,0,0), Callback = function(c)
    -- Function
end})

Visuals:AddSlider({Name = "Transparency", Default = 0, Max = 100, Callback = function(v)
    -- Function
end})</code></div>

    <!-- Assets -->
    <h2>🎨 Built-in Assets</h2>
    <ul>
      <li>Empty square: <code>rbxassetid://6031068420</code></li>
      <li>White check: <code>rbxassetid://6031068421</code></li>
      <li>Hue strip: <code>rbxassetid://6998583936</code></li>
      <li>Saturation mask: <code>rbxassetid://6998583760</code></li>
    </ul>
  </div>

  <footer>
    MIT License – do whatever you want, just keep the credit line.
  </footer>
</body>
</html>
