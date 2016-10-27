# _Basic To Do List_
| Information	|																						                                            |
|-------------|---------------------------------------------------------------------------------------|
| Version     | 0.2.0                                                                                 |
| Type		  	| Document file format														                                      |
| MIME		  	| `text/tdl`																			                                      |
| Extensions	| `.tdl`	                                                                              |

### Technical Details

A TDL file has some requirements:
* It must be a serialized table.
* Each item in that table must be a table containing a string (to be used as the name of the task) and a number between 0 and 1 (the percent of completion, divided by 100).

Even though the standard states that the number must be between 0 and 1, programs should add a case for if the table is malformed.

#### Available Utilities
* TDLClient - For manipulating TDL files.
* TDLViewer - For viewing the contents of a TDL file.

### Examples
#### Installation
Use `pastebin run Hpum9P5F` and choose "y" when prompted. This will install TDLClient and TDLViewer.

#### Usage
```Lua
{
  {"Show off how minimalistic this looks.",1,},
  {"Find out the Doctor's name.",0,}
}
```
