# *COS 7:* Temporary Directory

## Quick information
| Information |                                                                 |
| ----------- | --------------------------------------------------------------- |
| Version     | 2.0.0                                                           |
| Type        | Path / Directory                                                |
| MIME        | `application/directory`                                         |
| Location    | Temporary Directory is located in `settings.get("tempdir")`     |

### Technical Details
A standard temp directory exists at `settings.get("tempdir")`

This directory is used for storing files temporarily. The point of this directory is to be able to have a standard place
to store "junk" files, where the program doesn't have to worry about accidentally overriding another file created by the
user. It is NOT a place to store any files that need to be accurately recalled later on.

#### Proper Usage in Supporting Programs
To use it properly, a program can (through normal non-interrupted execution) store files in the `settings.get("tempdir")` directory while
it is running, and then should promptly delete the file from this directory as soon as possible.

#### Proper Support in Supporting OSes (and other systems)
The `settings.get("tempdir")` folder should be deleted then recreated at the startup of the system. Access to this directory should be open
and unprotected. It can however be hidden by the operating system, however, this is at the discretion of the OS creator
(and hopefully a user-modifiable config setting as well). **Ensure that you are only hiding `settings.get("tempdir")` and not other folders
called tmp**

### Examples

#### Usage (In a Program)
```lua
local tempdir = settings.get("tempdir")
local junkFile = fs.open(fs.combine(tempdir,"blah"), "w")
junkFile.write("So since I can write here, I'm not at risk of messing a user's stuff up.")
junkFile.close()

if fs.exists(fs.combine(tempdir,"blah")) then
    local junkFile = fs.open(fs.combine(tempdir,"blah"), "r")
    -- junkFile could be nil, so you will want to check for that. There is no guarentee the file still exists - the temp
    -- directory is not persistent.
    local var = junkFile.readAll()
    junkFile.close()
end
```

#### Usage (In an Operating System or Other Booting System)
```lua
-- This is a startup file. Append this code to the top of your startup file (or close to it) to adhere to the standard.

-- Get tempdir, or fall back to "/tmp"
local tempdir = settings.get("/tmp")
fs.delete(tempdir)
fs.makeDir(tempdir)

-- Additionally, it is permissible to hide the folder from the user. The tmp directory might not need to be seen on
every OS depending on your target userbase. PLEASE ENSURE YOU ARE ONLY HIDING "/tmp" AND NOT OTHER FOLDERS CALLED "tmp"
IF YOU ARE LOOKING TO ONLY FOLLOW THIS STANDARD. This standard doesn't cover program-specific temp folders.
```
