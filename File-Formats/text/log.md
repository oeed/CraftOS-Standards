## *COS 2:* Logs

|Information |                |
|------------|----------------|
|Type        |Log File        |
|MIME        |`text/log`      |
|Extensions  |`.log`          |

##Technical Details
.log files should contain valid logged data, including the type of the written data,
the written data and the time when the data was written. As of Version 1.0.0.0 there are
4 types, which are the following:

`[INFO]` - For the information of the User 

`[ERROR]` - For the indication that a non-critical problem existed

`[SEVERE]` - For the indication that a critical problem although it didn't crash the program existed

`[CRITICAL]` - For the indication that a critical problem that crashed the program existed

*Avaiable Utilities*
As of version 1.0.0.0 no Utilities come with this standard.

##Examples
*Installation*

A Universal Parser and Creator of the log files defined here can be found at https://github.com/MrObsidy/CC-LogParserAPI
(It is obtainable in-game via lyqyd's packman as mrobsidy/logparser)

*Syntax*

The Timestamp has to be obtained using this (or a similar) way:
`textutils.formatTime(os.time(), true)`
```
Please note that the time is given in 24-Hour-Clock. This should stay that way to avoid 
confusion and make reading the log by external programs a lot easier.
```
A log entry is terminated by the end of a line. A valid log entry is built up like this:

`
[time in 24-Hour][INFO/SEVERE/ERROR/CRITICAL]: log content
`

The log content is not further defined and can be freely chosen, however, there are some recommendations:

A `[CRITICAL]` tag in a log should _only_ be used to display a critical error with a resulting crash of the program and the following crash-report

A `[SEVERE]` tag in a log should _only_ be used to display a severe error that may limit the usage of the program, although not closing/crashing it

A `[ERROR]` tag in a log should _only_ be used to display a minor error that has no furhter effects on the program

A `[INFO]` tag in a log should be used for everything that is not a error, Wrong user inputs (like for example a wrong password entered or a number was expected and a string given) or general information.

*Usage*

A example file, 'log1.log', would be this:

```
[23:21][INFO]: Booted TestOS
[23:23][ERROR]: No rednet modem found
[23:27][INFO]: User(testuser) entered wrong password
[23:28][INFO]: User(testuser) logged in Succesfully
[23:29][SEVERE]: Desktop could not be generated, falling back to text mode
[23:30][CRITICAL]: Fallback failed! TestOS has crashed, this is the crash report: (also saved to crash-report.txt)
[23:30][CRITICAL]: failed to call displayTerminal() in kernel.lua, syntax error on line 274
[23:30][CRITICAL]: desktopFail() in display.lib tried calling _G[ kernel.lua ].displayTerminal()
```
