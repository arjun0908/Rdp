name: Cl

on: [push, workflow_dispatch]

Jobs:

build:

runs-on: windows-latest

steps:

- name: Download

run: Invoke-WebRequest

https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-windows- amd64.zip-OutFile ngrok.zip

- name: Extract

run: Expand-Archive ngrok.zip

- name: Auth

run: Ingrokingrok.exe authtoken $Env:NGROK_AUTH_TOKEN

env:

NGROK_AUTH_TOKEN: ${{ secrets.NGROK_AUTH_TOKEN })
- name: Enable TS.

run: Set-ItemProperty -Path "HKLM\System\CurrentControlSet\Control\Terminal Server'- name "DenyTSConnections-Value 0

- run: Enable-NetFirewall Rule-Display Group "Remote Desktop"

- run: Set-ItemProperty -Path 'HKLM\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" - Value 1

- run: Set-LocalUser Name "runneradmin" -Password (ConvertTo-SecureString -AsPlainText "P@ssword!" -Force)

- name: Create Tunnel

run: Ingrokingrok.exe tcp 3389
