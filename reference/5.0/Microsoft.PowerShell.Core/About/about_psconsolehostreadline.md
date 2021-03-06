---
title: about_PSConsoleHostReadLine
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dba9aa0c-53af-401a-91d0-e8381ed4f133
---
# about_PSConsoleHostReadLine
## TOPIC  
 about\_PSConsoleHostReadLine  
  
## SHORT DESCRIPTION  
 Explains how to create a customize how Windows PowerShellÂ® reads input at the console prompt.  
  
## LONG DESCRIPTION  
 Starting in Windows PowerShell V3, you can write a function named PSConsoleHostReadLine that overrides the default way that console input is processed.  
  
### EXAMPLES  
 The following example launches Notepad and gets input from a text File that the user creates:  
  
```  
         function PSConsoleHostReadLine  
         {  
             $inputFile = Join-Path $env:TEMP PSConsoleHostReadLine  
             Set-Content $inputFile "PS > "  
  
             ## Notepad opens. Enter your command in it, save the file,  
             ## and then exit.  
             notepad $inputFile | Out-Null  
             $userInput = Get-Content $inputFile  
             $resultingCommand = $userInput.Replace("PS >", "")  
             $resultingCommand  
         }  
```  
  
### REMARKS  
 By default, Windows PowerShell reads input from the console in what is known as “Cooked Mode”—in which the Windows console subsystem handles all the keypresses, F7 menus, and other input. When you press Enter or Tab, Windows PowerShell gets the text that you have typed up to that point. There is no way for it to know that you pressed Ctrl\-R, Ctrl\-A, Ctrl\-E, or any other keys before pressing Enter or Tab. In Windows PowerShell version 3, the PSConsoleHostReadLine function solves this issue. When you define a function named PSConsoleHostReadline in the Windows PowerShell console host, Windows PowerShell calls that function instead of the “Cooked Mode” input mechanism.  
  
### SEE ALSO  
 about\_Prompts
