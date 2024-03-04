FROM mcr.microsoft.com/powershell:7.1.3-ubuntu-20.04

SHELL ["pwsh", "-Command"]

# Install Atomic Red Team from pwsh
RUN IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing); \
    Install-AtomicRedTeam -getAtomics

RUN New-Item $PROFILE -Force

COPY ./setup.ps1 .
RUN ./setup.ps1
