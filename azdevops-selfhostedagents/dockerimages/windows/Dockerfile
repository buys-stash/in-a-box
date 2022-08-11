# Specifies that the latest microsoft/iis image will be used as the base image
FROM mcr.microsoft.com/windows/servercore:ltsc2019

# Restore the default Windows shell for correct batch processing.
SHELL ["cmd", "/S", "/C"]

# Run some PowerShell commands within the new container to set up the image
RUN powershell -Command "Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))"

RUN powershell -Command "choco feature enable -n allowGlobalConfirmation"
RUN powershell -Command "choco install pwsh -y"

## Required reg key to install edge 
RUN powershell -Command "REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\EdgeUpdate /v Allowsxs /t REG_DWORD /d 1"
RUN powershell -Command "choco install microsoft-edge"

WORKDIR /azp

COPY start.ps1 .

CMD ["powershell.exe", "C:\\azp\\start.ps1"]