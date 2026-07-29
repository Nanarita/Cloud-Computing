# Environment Setup — IKB42603 Lab0

This document provides a concise, step-by-step environment setup for Windows following the guide [IKB42603_Lab0_Environment_Setup_Cheatsheet.pdf](IKB42603_Lab0_Environment_Setup_Cheatsheet.pdf).

Prerequisites
- Administrative access on the machine
- PowerShell or an elevated Command Prompt

1) Install Docker Desktop
- Download & install Docker Desktop for Windows and enable WSL2 or Hyper-V as prompted.
- Start Docker Desktop and ensure it is running.
  ```powershell
  docker --version
  ```
- Evidence: [Evidence/Docker.PNG](Evidence/Docker.PNG)

2) Install AWS CLI v2
- Download the AWS CLI v2 MSI for Windows and run the installer.
- Verify:
  ```powershell
  aws --version
  ```
- Evidence: [Evidence/AWS CLI v2.PNG](Evidence/AWS%20CLI%20v2.PNG)

3) Install kind and kubectl
- Download the kind Windows binary or use Go if available. Example with curl (PowerShell):
  ```powershell
  curl -Lo kind.exe https://kind.sigs.k8s.io/dl/v0.20.0/kind-windows-amd64
  chmod +x ./kind && sudo mv ./kind /usr/local/bin/kind
  kind --version
  ```
- Download the kubectl binary for Windows and place it in a directory on your PATH.
- Verify kubectl:
  ```powershell
  kubectl version --client
  ```
- Evidence: [Evidence/Kind.PNG](Evidence/Kind.PNG)
- Evidence: [Evidence/Kubectl.PNG](Evidence/Kubectl.PNG)

4) Install OpenSSL and oathtool
- OpenSSL (for certs): install it from the official Windows build or Git for Windows bundle, then verify:
  ```powershell
  openssl version
  ```
- Oathtool (for OTP generation): install the Windows build and verify:
  ```powershell
  oathtool --version
  ```
- Evidence: [Evidence/OpenSSL.PNG](Evidence/OpenSSL.PNG)
- Evidence: [Evidence/Oathtool.PNG](Evidence/Oathtool.PNG)

5) Start and stop the lab environment
- Install LocalStack (for AWS service emulation) using pip or Docker:
  ```powershell
  sudo docker run --rm -p 4566:4566 localstack/localstack:3.0
  localstack --version
  ```
- Or run via Docker Compose as shown in the guide.
- Evidence: [Evidence/LocalStack.PNG](Evidence/LocalStack.PNG)

- Create the Kubernetes cluster with kind
- Create the cluster:
  ```powershell
  kind create cluster --name ccse
  kubectl cluster-info --context kind-ccse
  kubectl get nodes
  ```
- Evidence: [Evidence/Kubernetes cluster KIND.PNG](Evidence/Kubernetes%20cluster%20KIND.PNG)

6) One-time / Final checks
- Ensure all CLIs are on `PATH` and show expected versions:
  ```powershell
  EP='--endpoint-url=http://localhost:4566'
  aws $EP sts get-caller-identity
  ```