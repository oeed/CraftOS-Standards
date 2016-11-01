## *COS 2:* Logs

|Information |                |
|------------|----------------|
|Type        |Log File        |
|MIME        |'text/log'      |
|Extensions  |'.log'          |

##Technical Details
.log files should contain valid logged data, including the type of the written data,
the written data and the time when the data was written. As of Version 1.0.0.0 there are
4 types, which are the following:
'[INFO]' - For the information of the User 
'[SEVERE]' - For the indication that a non-critical problem existed
'[ERROR]' - For the indication that a critical problem although it didn't crash the program existed
'[CRITICAL]' - For the indication that a critical problem that crashed the program existed

*Avaiable Utilities*
As of version 1.0.0.0 no Utilities come with this standard.

##Examples
*Installation*
A Universal Parser and Creator of the log files defined here can be found at https://github.com/MrObsidy/CC-LogParserAPI .
(It is obtainable in-game via lyqyd's packman as mrobsidy/logparser)

*Usage*
A example file, 'log1.log', would be this:
'[23:21][INFO]: Booted TestOS'
