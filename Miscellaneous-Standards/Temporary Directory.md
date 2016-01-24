# _Temporary Directory_
| Information	|																						                                            |
|-------------|---------------------------------------------------------------------------------------|
| Version 		|1.0.0											                        |	
| Type		  	| Path / Directory																	                                      |
| MIME		  	| `path/temp`																			                                      |
| Location	| Temporary Directory is located in `/.temp`	|
| Deprecates	| No standards have been made for this yet.				                  			|

### Technical Details
A standard temp directory exists at `/.temp`

This directory is used for storing files temporarily. The point of this directory is to be able to have a standard place to store "junk" files, where the program doesn't have to worry about accidentally overriding another file created by the user. It is NOT a place to store any files that need to be accurately recalled later on.

**Proper Usage in Supporting Programs**

To use it properly, a program can (through normal non-interrupted execution) store files in the `/.temp` directory while it is running, and then should promptly delete the file from this directory as soon as possible.

**Proper Support in Supporting OSes (and other systems)**

The `/.temp` folder should be deleted then recreated at the startup of the system. Access to this directory should be open and unprotected.

### Examples

#### Usage (In a Program)
```Lua
local junkFile = fs.open("/.temp/blah", "w")
junkFile.write("So since I can write here, I'm not at risk of messing a user's stuff up.")
junkFile.close()

sleep(0)

if fs.exists("/.temp/blah") then
	local junkFile = fs.open("/.temp/blah", "r")
	-- junkFile could be nil, so you will want to check for that. There is no guarentee the file still exists - the temp directory is not persistent.
    local var = junkFile.readAll()
end
```

#### Usage (In an Operating System or Other Booting System)
```
-- This is a startup file. Append this code to the top of your startup file (or close to it) to adhere to the standard.

fs.delete("/.temp")
fs.makeDir("/.temp")
```
