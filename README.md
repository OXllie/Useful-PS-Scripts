# Useful-PS-Scripts
Assortment of commands

#### Hash contents of folder
```powershell
Get-ChildItem | ForEach-Object {Get-FileHash $_.FullName -Algorithm MD5}
```
