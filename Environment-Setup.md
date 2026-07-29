# Environment Setup — IKB42603 Lab0

This document provides a concise, step-by-step environment setup for Windows following the guide [IKB42603_Lab0_Environment_Setup_Cheatsheet.pdf](IKB42603_Lab0_Environment_Setup_Cheatsheet.pdf).

Prerequisites
- Administrative access on the machine
- PowerShell or an elevated Command Prompt
- (Optional) Chocolatey (`choco`) for easy installs

1) Install Docker Desktop
- Download & install Docker Desktop for Windows and enable WSL2 or Hyper-V as prompted.
- Start Docker Desktop and ensure it is running.
  ```powershell
  docker --version
  ```
- Evidence: <img width="351" height="68" alt="1  Docker" src="https://github.com/user-attachments/assets/f8cfa18e-b498-4260-80e9-d9ac5c9fc8eb" />


2) Install AWS CLI v2
- Download the AWS CLI v2 MSI for Windows and run the installer, or use Chocolatey:
  ```powershell
  choco install awscli -y
  ```
- Verify:
  ```powershell
  aws --version
  ```
- Evidence: [Evidence/AWS CLI v2.PNG](Evidence/AWS%20CLI%20v2.PNG)

3) Install kubectl
- Recommended via Chocolatey or curl:
  ```powershell
  choco install kubernetes-cli -y
  kubectl version --client
  ```
- Evidence: [Evidence/Kubectl.PNG](Evidence/Kubectl.PNG)

4) Install kind (Kubernetes IN Docker)
- Download the Windows binary or use Go if available. Example with curl (PowerShell):
  ```powershell
  curl -Lo kind.exe https://kind.sigs.k8s.io/dl/v0.20.0/kind-windows-amd64
  Move-Item .\kind.exe C:\Windows\System32\kind.exe
  kind --version
  ```
- Evidence: [Evidence/Kind.PNG](Evidence/Kind.PNG)

5) Create a local Kubernetes cluster with kind
  ```powershell
  kind create cluster --name lab0
  kubectl cluster-info --context kind-lab0
  kubectl get nodes
  ```
- Evidence: [Evidence/Kubernetes cluster KIND.PNG](Evidence/Kubernetes%20cluster%20KIND.PNG)

6) Install LocalStack (for AWS service emulation)
- Using pip (recommended in a venv) or Docker image:
  ```powershell
  pip install localstack
  localstack --version
  ```
- Or run via Docker Compose as shown in the guide.
- Evidence: [Evidence/LocalStack.PNG](Evidence/LocalStack.PNG)

7) Install OpenSSL and oathtool
- OpenSSL (for certs): use Chocolatey or Git for Windows bundles. Example:
  ```powershell
  choco install openssl.light -y
  openssl version
  ```
- Oathtool (for OTP generation):
  ```powershell
  choco install oathtool -y
  oathtool --version
  ```
- Evidence: [Evidence/OpenSSL.PNG](Evidence/OpenSSL.PNG)
- Evidence: [Evidence/Oathtool.PNG](Evidence/Oathtool.PNG)

8) One-time / Final checks
- Ensure all CLIs are on `PATH` and show expected versions:
  ```powershell
  docker --version; kind --version; kubectl version --client; aws --version; localstack --version
  ```
