## What’s the difference?

I updated the name and icon, and installed two separate GitHub clients to manage multiple accounts.

```shell
nvm install v20.18.1
nvm use v20.18.1
npm install -g yarn
yarn -v
conda create -n github-desktop python=3.9
conda activate github-desktop
yarn
yarn build:dev
yarn start
yarn build:prod
yarn package
```

## Known Issues

>These preferences will edit your global Git config file.

As a result, switching between different accounts can overwrite your user information.
My solution is to manually edit the config file and toggle comment lines using the command line.

It’s a simple workaround—but it works.

```
[user]
	name = git
	email = @mail
# [user]
	# name = hub
	# email = @mail
```

## Windows

Windows is untested and too much of a hassle to set up — feel free to submit a pull request.

## Hammerspoon

On Mac, I use Hammerspoon with custom hotkeys to switch users—it works really well.



```lua
local obj = {}
obj.__index = obj

local CFG_PATH     = os.getenv("HOME") .. "/.gitconfig"
local BACKUP_SUFX  = ".bak"

local function trimComment(line)  return line:gsub("^%s*#%s*", "") end
local function addComment(line)   return line:match("^%s*#") and line or ("# "..line) end

local function switchAccount(target)
  local lines = {}
  for ln in io.lines(CFG_PATH) do lines[#lines+1] = ln end

  local inUser, current = false, nil
  for i, ln in ipairs(lines) do
    if ln:match("^%s*#?%s*%[user%]") then
      inUser, current = true, nil
    elseif inUser and ln:match("^%s*%[") then
      inUser = false
    end

    if inUser then
      if not current then
        current = trimComment(ln):match("name%s*=%s*(%S+)")
      end
      if current then
        lines[i] = (current == target) and trimComment(ln) or addComment(ln)
      end
    end
  end

  os.rename(CFG_PATH, CFG_PATH .. BACKUP_SUFX)
  local f = assert(io.open(CFG_PATH, "w"))
  f:write(table.concat(lines, "\n"))
  f:close()
end

function obj.toggle(target)
  switchAccount(target)
  hs.alert.show("Git user → "..target, 1)
end

function obj:bindHotkeys(map)
  for key, name in pairs(map) do
    hs.hotkey.bind({"ctrl","alt"}, key, function() obj.toggle(name) end)
  end
end

return obj
```

Load

```lua
hs.loadSpoon("SwitchGitUser")
spoon.SwitchGitUser:bindHotkeys{
  a = "git",   -- Ctrl + Alt + A  →  name = git
  s = "hub",   -- Ctrl + Alt + S  →  name = hub
  -- add more  d = "work", …
}
