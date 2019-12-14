```powershell
function Set-SearchBoxTaskbar {
  [CmdletBinding()]
  param ()
  $regpath = "HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\Search"
  try {
    if ((Get-ItemProperty -Path $regpath).SearchboxTaskbarMode -eq 0) {
      Set-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\Search -Name "SearchboxTaskbarMode" -Value 1 -Force
      Write-Host "search box toggled on"
    }
    else {
      Set-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\Search -Name "SearchboxTaskbarMode" -Value 0 -Force
      Write-Host "search box toggled off"
    }
    Get-Process explorer | Stop-Process
  }
  catch {
    Write-Error $_.Exception.Message
  }
}
```
