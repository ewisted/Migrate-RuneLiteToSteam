# Migrate-RuneLiteToSteam
A Powershell script that lets you launch RuneLite through Steam

## Getting Started
All you need to get up and running is to [download a zip of the repo](https://github.com/ewisted/Migrate-RuneLiteToSteam/archive/refs/heads/main.zip), a [RuneLite installation](https://runelite.net/), an [OSRS Steam client installation](https://store.steampowered.com/app/1343370/Old_School_RuneScape/), and Powershell. Once you have those, just follow these steps:
1. Extract the `Migrate-RuneliteToSteam.ps1` file from the downloaded zip to wherever you wish to keep it.
2. Open up a Powershell window as administrator in the directory you extracted the script to. The easiest way to do this is to navigate to the folder containing the script to in File Explorer, click `File` in the top-left corner then hover over `Open Windows Powershell` and click `Open Windows Powershell as administrator`.
3. Enter the following commands in the Powershell window. Make sure to replace the placeholder variables with your installation/script paths.
  ```
  Unblock-File -Path "path-to-downloaded script"
  .\Migrate-RuneliteToSteam.ps1 -RuneLiteInstallPath "path-to-runelite-files" -SteamClientInstallPath "path-to-steam-client-files"
  ```
As long as there were no errors, launching OSRS through Steam should now launch RuneLite.

### Reverting back to the Steam client
Reverting back is simple. Just run the migration script again with the `-Revert` switch:
  ```
  .\Migrate-RuneliteToSteam.ps1 -RuneLiteInstallPath "path-to-runelite-files" -SteamClientInstallPath "path-to-steam-client-files" -Revert
  ```
  
## Run at Startup/Logon
Eventually Steam is going to update OSRS and overwrite RuneLite or RuneLite could be updated from its orginal install location. The script takes these cases into account and keeps track of RuneLite's MD5 hash in order to be idempotent. Therefore, it is recommended to schedule to run the script at startup or logon. To do so just follow these steps:
1. Run Powershell as admin in the directory containing the script.
3. Run the script with the `-Schedule` parameter. It accepts either `Startup` or `Logon`.
  ```
  .\Migrate-RuneliteToSteam.ps1 -RuneLiteInstallPath "path-to-runelite-files" -SteamClientInstallPath "path-to-steam-client-files" -Schedule "schedule-type"
  ```
The `-Schedule` parameter also works with the `-Revert` switch, so using both will remove the scheduled task.
  ```
  .\Migrate-RuneliteToSteam.ps1 -RuneLiteInstallPath "path-to-runelite-files" -SteamClientInstallPath "path-to-steam-client-files" -Schedule "schedule-type" -Revert
  ```
