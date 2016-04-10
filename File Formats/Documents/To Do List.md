# _To Do List_
| Information	|																						                                            |
|-------------|---------------------------------------------------------------------------------------|
| Version     | 0.1.0                                                                                 |
| Type		  	| Document file format														                                      |
| MIME		  	| `basic/tdl`																			                                      |
| Extensions	| `.tdl`	                                                                              |

### Technical Details
This format is an attempt to create one united standard for to-do lists.

A TDL file has some requirements:
* It must be a serialized table.
* Each item in that table must be a table containing a string and a boolean.

Regarding the last bullet, the string is the name of the task, and the boolean is whether it is finished or not.
#### Available Utilities
* TDLClient - For manipulating TDL files.
* TDLViewer - For viewing the contents of a TDL file.

### Examples
#### Installation
Use `pastebin run Hpum9P5F` and choose "y" when prompted. This will install TDLClient and TDLViewer.

#### Usage
```Lua
-- example of TDL file
{
  {"Show off how minimalistic this looks.",true,},
  {"Find out the Doctor's name.",false,}
}
```
