
<h2>Optical UI Lib Documentation</h2>

<main>
<section>
<h2>Getting Started</h2>
<p>Include this code in a LocalScript to initialize the PlatWare UI:</p>
<pre><code>local UI = loadstring(game:HttpGet("https://raw.githubusercontent.com/ZaHando15/Optical-UI-Lib-Documentation/refs/heads/main/Base"))()
</code></pre>
</section>

<section>
<h2>Creating Categories</h2>
<p>Use <code>UI:MakeCat()</code> to create sidebar categories:</p>
<pre><code>local Cat = UI:MakeCat({ Name = "Category" })</code></pre>
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
</section>

</main>
</body>
</html>
