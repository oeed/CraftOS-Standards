# UpdateTool file
#### MIME: install/updatetool
#### extension: .update or .ut

UpdateTool uses a unique type of file to track differences between the local copy of a program and the github copy of a program. It uses
a file with a serialized table, which may contain up to 3 tables, named "mod" and "del", both optional, and a required string named "tag". 
  
The "mod" table contains strings, which are urls to download, with the key being the file path it needs to download to. This is used for modified files and added files being updated.
  
The "del" table is a table of strings with no names, who contains paths to DELETE.  
  
The "tag" string is a simple string saying what the new github release/commit of the update contained in the file is.

Here is an example of an update from swiftOS/swiftOS release dev-2 to commit d2c446a:
```
{
  mod = {
    [ "swift/api/json" ] = "https://github.com/swiftOS/swiftOS/raw/d2c446a77c10d406518d029e7bf287a0ecdb2751/swift/api/json",
    [ "swift/digitalarmor/rednet" ] = "https://github.com/swiftOS/swiftOS/raw/d2c446a77c10d406518d029e7bf287a0ecdb2751/swift/digitalarmor/rednet",
    [ "README.md" ] = "https://github.com/swiftOS/swiftOS/raw/d2c446a77c10d406518d029e7bf287a0ecdb2751/README.md",
    startup = "https://github.com/swiftOS/swiftOS/raw/d2c446a77c10d406518d029e7bf287a0ecdb2751/startup",
    [ "swift/api/swift" ] = "https://github.com/swiftOS/swiftOS/raw/d2c446a77c10d406518d029e7bf287a0ecdb2751/swift/api/swift",
    [ "swift/api/hmeta" ] = "https://github.com/swiftOS/swiftOS/raw/d2c446a77c10d406518d029e7bf287a0ecdb2751/swift/api/hmeta",
    [ "boot.lua" ] = "https://github.com/swiftOS/swiftOS/raw/d2c446a77c10d406518d029e7bf287a0ecdb2751/boot.lua",
    [ "swift/updatetool" ] = "https://github.com/swiftOS/swiftOS/raw/d2c446a77c10d406518d029e7bf287a0ecdb2751/swift/updatetool",
  },
  tag = "d2c446a",
  del = {},
}
```
