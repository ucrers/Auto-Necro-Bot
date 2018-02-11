#SingleInstance Force

Gui, Add, Button, x22 y10 w280 h40 gOPEN_CHATLOG, START
Gui, Add, Button, x22 y60 w280 h40 gSTOP, STOP

Gui, Show, x348 y432 h125 w329, Auto Necro Bot
Return

GuiClose:
ExitApp
Return

STOP:
Exitapp
return

OPEN_CHATLOG:
FileSelectFile, AuthFile, 3, , Open a Auth file, Auth Datei (*.json)
if AuthFile !=
{
	FileRead, AuthFileText, %AuthFile%
	FileSelectFile, APIFile, 3, , Open a API file, API Datei (*.txt)
	
	if APIFile !=
	{
		
		FileSelectFolder, NecroFolder
	
		if NecroFolder !=
		{
			SetWorkingDir, %NecroFolder%
			
			; Program burda basliyor
			Loop, Read, %APIFile%
			{
				;Sil
				FileDelete %AuthFile%
				;Degistir
				NewStr := RegExReplace(AuthFileText,  "[A-Z0-9]{20}", A_LoopReadLine)
				FileAppend, %NewStr%, %AuthFile%
				Run, NecroBot2.exe
				Sleep, 10000
				WinClose, NecroBot2 Loading
				Sleep, 1500
				
				Loop, Logs\*.txt
					FileRead, LogFileText, %A_LoopFileFullPath%
				
				if !InStr(LogFileText, "The HashKey is invalid or has expired") && !InStr(LogFileText, "Expires in: -1")
				{
					MsgBox, 64, Found, Found API Key!`n%A_LoopReadLine%
					SoundBeep
				}
				if InStr(LogFileText, "Expires in: -1")
				{
					;FormatTime, TimeString,, [dd-MM-yyyy HH:mm:ss]
					FileAppend, %A_LoopReadLine%`n, %A_ScriptDir%\expired_apis.txt
				}
			}
			MsgBox, 64, API List, The API List is end!
		}
	}

}
return