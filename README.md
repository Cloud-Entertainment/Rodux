<h1 align="center">Rodux</h1>
<div align="center">
	<a href="https://github.com/Roblox/rodux/actions">
		<img src="https://github.com/Roblox/rodux/workflows/CI/badge.svg" alt="GitHub Actions Build Status" />
	</a>
	<a href="https://coveralls.io/github/Roblox/rodux?branch=master">
		<img src="https://coveralls.io/repos/github/Roblox/rodux/badge.svg?branch=master" alt="Coveralls Coverage" />
	</a>
	<a href="https://roblox.github.io/rodux">
		<img src="https://img.shields.io/badge/docs-website-green.svg" alt="Documentation" />
	</a>
</div>

<div align="center">
	A state management library for Roblox Lua inspired by <a href="https://redux.js.org">Redux</a>.
</div>

<div>&nbsp;</div>

## Installation

### Method 1: Model File (Roblox Studio)
* Download the `rbxm` model file attached to the latest release from the [GitHub releases page](https://github.com/Roblox/rodux/releases).
* Insert the model into Studio into a place like `ReplicatedStorage`

### Method 2: Filesystem
* Copy the `src` directory into your codebase
* Rename the folder to `Rodux`
* Use a plugin like [Rojo](https://github.com/LPGhatguy/rojo) to sync the files into a place

## Usage
Rodux works just like [Redux](https://redux.js.org)'s base API.

See the official [Rodux Documentation](https://roblox.github.io/rodux/) for more details.

```lua
local Rodux = require(script.Parent.Rodux)

local function reducer(state, action)
	state = state or {
		frobulations = 0,
	}

	if action.type == "frobulate" then
		return {
			frobulations = state.frobulations + 1,
		}
	end

	return state
end

local store = Rodux.Store.new(reducer)

store:getState() -- { frobulations = 0 }

store:dispatch({
	type = "frobulate",
})

store:getState() -- { frobulations = 1 }
```

## Contributing
Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for information.

## License
Rodux is available under the Apache 2.0 license. See [LICENSE](LICENSE) for details.

## Cloud Entertainment API

**Store:bindToValueChanged**

Binds the given callback function to the store changed event, but only runs when the specified value has changed. Returns a handle to be used in Store:unbindFromValueChanged(handle) to unbind this callback.

`Store:bindToValueChanged(callback, ...)`

**Parameters**
- **callback [function]:** The function you want to run when then specified value changes.
- **... [tuple]:** The dictionary path of the value you want to listen for changes to (e.g. (callback, "liveOps", "worlds", "world1") will listen for when the world1 table changes in live ops).

<br>


**Store:unbindFromValueChanged**

Unbinds the given handle which is returned from Store:bindToValueChanged().

`Store:unbindFromValueChanged(handle)`

**Parameters**
- **handle [function]:** The handle to be unbinded.

<br>


**Store:waitForValue**

Unbinds the given handle which is returned from Store:bindToValueChanged().

`Store:waitForValue(...)`

**Parameters**
- **... [tuple]:** The dictionary path for the value you want to wait for. Will yield until this value exists, and will return the value (e.g. :waitForValue("liveOps") will yield until the live ops table has been added to Rodux)