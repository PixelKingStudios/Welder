#### [<-- Home](https://pixelkingstudios.github.io/Home/)

## Welder - Lightweight Module for Model and Tool Welding

### What is Welder?

Welder is an open-source module that makes it extremely easy to weld every `BasePart` in a model to it's `PrimaryPart`, or every '`BasePart` in a tool to it's Handle. It only takes two lines of code from another script and it's done! Welder can also "un-weld" if you want to undo the welding.

### How to get Welder?

Welder can be required from another script using it's AssetID (5718676928) or can be purchased for free from Roblox's asset library [here](https://www.roblox.com/library/5718676928/Welder). To `require()` Welder from another script, use the following code bellow:

````lua
local Welder = require(5718676928)
````

### How do I use Welder?

#### Welding

To weld every `BasePart` of a model to it's `PrimaryPart`, use the following code:

````lua
Welder:Weld(PATH_TO_MODEL)
````

Similarly, to weld every `BasePart` of a tool to it's Handle, use the following code:

````lua
Welder:Weld(PATH_TO_TOOL)
````

#### Un-welding

To un-weld every `BasePart` of a model from it's `PrimaryPart`, use the following code:

````lua
Welder:Unweld(PATH_TO_MODEL)
````

Similarly, to un-weld every `BasePart` of a tool from it's Handle, use the following code:

````lua
Welder:Unweld(PATH_TO_TOOL)
````

#### Welding without changing the `BasePart`'s anchored state

Welder will unanchor every `BasePart` it welds. To weld without changing the `BasePart`'s anchored state, use the following code:

````lua
Welder:WeldKeepAnchoredState(PATH_TO_MODEL_OR_TOOL)
````

### Important things to note

#### Object must be a Model or a Tool

Welder will only weld the descendants of a model or a tool, and will throw a warning in the output widow if it isn't. Welder may be updated in the future to work with other objects, but for now only models and tools are supported.

#### `PrimaryPart` for a model and Handle for a tool is required

Welder will throw a warning in the output window if the model's `PrimaryPart` is equal to `nil`. Welder needs to know what to weld everything to, so it uses the model's `PrimaryPart` as it's main part.

Similarly, a tool must have a `BasePart` named "Handle" in order for the tool to be welded.

#### Welding will unanchor

Unless you're using `WeldKeepAnchoredState()`, Welder will unanchor everything you weld. To prevent this, use the `WeldKeepAnchoredState()` method instead.

#### Old methods no longer supported

Methods such as `Welder.weld()` and `Welder.unweld()` are no longer supported, and have been replaced with methods such as `Welder:Weld()` and `Welder:Unweld()`. Using these old methods will throw an error.

### Code samples

Weld, then after 10 seconds Unweld:

````lua
local Welder = require(5718676928)
local model = PATH_TO_MODEL

Welder:Weld(model)
wait(10)
Welder:Unweld(model)
````

Loop through every model in a folder and weld their `BasePart` descendants:

````lua
local Welder = require(5718676928)
local folder = PATH_TO_FOLDER

for _, child in pairs(folder:GetChildren()) do
  if child:IsA("Model") then
    Welder:Weld(child)
  end
end)
````

Weld a model without changing its `BasePart` descendants' anchored states:

````lua
local Welder = require(5718676928)
local model = PATH_TO_MODEL

Welder:WeldKeepAnchoredState(model)
````

Weld, then when `PrimaryPart` touched Unweld:

````lua
local Welder = require(5718676928)
local model = PATH_TO_MODEL

Welder:Weld(model)
local welded = true

model.PrimaryPart.Touched:Connect(function(hit)
  if welded then
    Welder:Unweld(model)
    welded = false
  end
end)
````

Weld every `BasePart` of a tool to it's Handle:

````lua
local Welder = require(5718676928)
local tool = PATH_TO_TOOL

Welder:Weld(tool)
````
