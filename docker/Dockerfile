# syntax=docker/dockerfile:1.3

# Define base images for different architectures
ARG POWERSHELL_AMD64=mcr.microsoft.com/powershell:mariner-2.0
ARG POWERSHELL_ARM64=mcr.microsoft.com/powershell:mariner-2.0-arm64

# Base setup for amd64
FROM --platform=linux/amd64 ${POWERSHELL_AMD64} AS build-amd64
SHELL ["pwsh", "-Command"]
RUN IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing); \
    Install-AtomicRedTeam -getAtomics
RUN New-Item $PROFILE -Force
COPY ./setup.ps1 .
RUN ./setup.ps1

# Base setup for arm64
FROM --platform=linux/arm64 ${POWERSHELL_ARM64} AS build-arm64
SHELL ["pwsh", "-Command"]
RUN IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing); \
    Install-AtomicRedTeam -getAtomics
RUN New-Item $PROFILE -Force
COPY ./setup.ps1 .
RUN ./setup.ps1

# Final image
FROM build-$BUILDARCH
