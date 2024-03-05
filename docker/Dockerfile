# Define arguments for base images
ARG BASE_IMAGE_AMD64=mcr.microsoft.com/powershell:mariner-2.0
ARG BASE_IMAGE_ARM64=mcr.microsoft.com/powershell:mariner-2.0-arm64

# Use build argument to select the appropriate base image
ARG TARGETPLATFORM
ARG BASE_IMAGE=$BASE_IMAGE_AMD64
FROM ${BASE_IMAGE} AS builder

# Common build steps
SHELL ["pwsh", "-Command"]
RUN IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing); \
    Install-AtomicRedTeam -getAtomics
RUN New-Item $PROFILE -Force
COPY ./setup.ps1 .
RUN ./setup.ps1
