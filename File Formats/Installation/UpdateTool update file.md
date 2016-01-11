# UpdateTool file
#### MIME: install/updatetool
#### extension: .update or .ut

UpdateTool uses a unique type of file to track differences between the local copy of a program and the github copy of a program. It uses
a file with a serialized table, which may contain up to 3 tables, named "res" and "del", both optional, and a required string named "tag". 
  
The "res" table contains strings, which are urls to download, with the key being the file path it needs to download to. This is used for modified files and added files being updated.
  
The "del" table is a table of strings with no names, who contains paths to DELETE.  
  
The "tag" string is a simple string saying what the new github release/commit of the update contained in the file is.
