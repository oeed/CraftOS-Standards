# *COS 1:* Configuration File

## Quick information

| Information |                           |
| ----------- | ------------------------- |
| Type        | Plain text file format    |
| MIME        | `text/config`             |
| Extensions  | `.cfg` or `.config`       |

## Technical Details
This format is based upon plain text and as such technical details that apply to plain text also apply to this format.

##Config data

Config data is saved in the following way:

```
Key1: Value1
Key2: Value2
```

Values are saved in the normal Lua way(Strings are enclosed with "", tables are enclosed with {},...)

Every entry has to have it's own line, the following is __wrong__:
```
Key1:{Hello="World",
World="Hello"}
```
Correct way:
```
Key1:{Hello="World",World="Hello"}
```
##API to Convert config format to table and vice versa:
http://pastebin.com/1GGq3fyw
##Code for making a table from a config:
```lua
if type("config") ~= "string" then
  return nil,"Config must be a string"
end
local lines = {}
for line in (config.."\n"):gmatch("([^\n]*)\n") do
  table.insert(lines,line)
end
local result = {}
for i,v in pairs(lines) do
  local t = {}
  for a in (v..":"):gmatch("([^:]*):") do
    table.insert(t,a)
  end
  if #t ~= 2 then
    return nil,"Line "..i.." is invalid!"
  else
    result[t[1]] = loadstring("return "..t[2])()
  end
end
return result
```
##Code for making a config from a table:
```lua
local s = ""
local tk, tv
for k, v in pairs(configTable) do
  tk, tv = type(k), type(v)
  if tk == "string" or tk == "number" then
    if tv ~= "string" and tv ~= "nubmer" and tv ~= "boolean" and tv ~= "table" then
      error("Invalid type for value: Expected string, number, boolean, table; got "..tv)
    end
    if tv == "table" then
      tv = tostring(textutils.serialize(tv)):gsub("\n", "")
    end
    s = s .. tk .. ": " ..tostring(tv) .. "\n"
  else
    error("Invalid type for key: Expected string, number; got "..tk)
  end
end
return s
```
