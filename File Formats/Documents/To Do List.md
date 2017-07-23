# _To Do List_
| Information	|																						                                            |
|-------------|---------------------------------------------------------------------------------------|
| Version     | 0.3.0                                                                                 |
| Type		  	| Document file format														                                      |
| MIME		  	| `text/tdl`																			                                      |
| Extensions	| `.tdl`	                                                                              |

### Technical Details

A TDL file has some requirements:
* It must be a serialized table.
* Each item in that table must be a table containing a string (to be used as the name of the task) and a number between 0 and 1 (the percent of completion, divided by 100) OR a table where each item in that table must be a table containing a string (to be used as the name of the task) and a number between 0 and 1 (the percent of completion, divided by 100).

Programs should check to make sure the table meets the standard while or before using the contents of said table.

#### Available Utilities
* TDLClient (discontinued) - For manipulating TDL files.
* TDLViewer - For viewing the contents of a TDL file.

### Examples
#### Installation
Use `pastebin run Hpum9P5F` and choose "y" when prompted. This will install TDLViewer. If you wish, you can then enter "y" again to install the outdated TDLCLient. TDLClient will not render tasks with subtasks. 

#### Usage
```Lua
{
  {"Show off how minimalistic this looks.",1,},
  {"Find out the Doctor's name.",
      {"Track down the Doctor", 1,},
      {"Ask the Doctor what their name is", 0,},
  },
}
```

(example courtesy of Lyqyd)
