## Welder - Lightweight Module For Model Welding

### What is Welder?

Welder is an open-source module that makes it extremely easy to weld every `BasePart` in a model to it's `PrimaryPart`. It only takes two lines of code from another script and it's done! Welder can also "un-weld" if you want to undo the welding.

### How do get Welder?

Welder can be required from another script using it's AssetID (5718676928) or can be purchased for free from Roblox's asset library [here](https://www.roblox.com/library/5718676928/Welder). To `require()` Welder from another script, use the following code bellow:

````lua
local Welder = require(5718676928)
````

### How do I use Welder?

#### Welding

To weld every `BasePart` of a model to it's `PrimaryPart`, use the following code:

````lua
Welder:Weld(script.Parent) -- Assuming that the script is located inside of the model itself.
````

#### Un-welding

To un-weld every `BasePart` of a model from it's `PrimaryPart`, use the following code:

````lua
Welder:Unweld(script.Parent) -- Assuming that the script is located inside of the model itself.
````

#### Welding without changing the `BasePart`'s anchored state

Welder will unanchor every `BasePart` it welds. To weld without changing the `BasePart`'s anchored state, use the following code:

````lua
Welder:WeldKeepAnchoredState(script.Parent) -- Assuming that the script is located inside of the model itself.
````

### Important things to note

#### Object must be a Model

Welder will only weld the descendants of a model, and will throw a warning in the output widow if it isn't. Welder may be updated in the future to work with other objects, but for now only models are supported.

#### `PrimaryPart` is required

Welder will throw a warning in the output window if the model's `PrimaryPart` is equal to `nil`. Welder needs to know what to weld everything to, so it uses the model's `PrimaryPart` as it's main part.

#### Welding will unanchor

Unless you're using `WeldKeepAnchoredState()`, Welder will unanchor everything you weld. To prevent this, use the `WeldKeepAnchoredState()` method instead.

### Code samples

Weld, then after 10 seconds un-weld:

````lua
local Welder = require(5718676928)
local model = script.Parent -- path to model

Welder:Weld(model)
wait(10)
Welder:Unweld(model)
````

Loop through every model in a folder and weld their `BasePart` descendants:

````lua
local Welder = require(5718676928)
local folder = script.Parent -- path to folder

for _, model in pairs(folder:GetChildren()) do
  if model:IsA("Model") then
    Welder:Weld(model)
  end
end)
````
