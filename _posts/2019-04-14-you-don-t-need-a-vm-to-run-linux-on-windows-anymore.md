---
categories:
- kubernetes
tags:
- featured
layout: post
title: Do yourself a favour , install WSL
author: vamsi
image: "/assets/images/wsl.jpeg"
date: 2019-04-14 12:45:45 +0000

---
**Y**ou have Windows 10. You setup VMs within Windows to execute Linux native commands. You ❤ Docker, Kubernetes and Minikube and you don’t have Hyper-V and don’t like the cumbersome setup process and is highly unreliable. You ❤ Power shell + Chocolatey but you simply can’t get over Bash !!. Your Linux VMs are really slow and consume a lot of resources

![](https://cdn-images-1.medium.com/max/2600/0*kCNAv6hizyb5bO2d)

Do yourself a favor , enable Linux Subsystems for Windows.

#### **Step 1:** Open Powershell as an administrator and run this command

    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

    and Restart your system when prompted !!

#### **Step 2:** Check OS Build Version

    systeminfo | Select-String "^OS Name","^OS Version"

    if (build version >= Windows build 16215):
    Open Microsoft Store;
    Search for "Linux"
    Select Distro and Install:
    proceed to Step 3

![](https://cdn-images-1.medium.com/max/1000/1*J3s3CsXdCK7gUiGngjKvNw.png)

#### **Step 3:** Download Distros based on your requirement. I downloaded Ubuntu 18.04 Links Below

    Ubuntu 18.04Ubuntu 18.04 ARMUbuntu 16.04Debian GNU/LinuxKali LinuxOpenSUSESLES

#### **Step 4:** Extract the Archive and Install it

    1) -------------Open Powershell----------------
    cd C:\mkdir Distroscd Distros
    2) Copy file from Downloads folder to this folder
    -----------------Open Powershell-------------------
    Rename-Item ~/Ubuntu.appx ~/Ubuntu.zip Expand-Archive ~/Ubuntu.zip ~/Ubuntu
    Run Ubuntu.exe and enter your username and password 

> !!! Note: Sometimes you may have to rename and unzip the appx file inside the appx archive to see the actual .exe

#### **Step 5**: Once the installation is done

    Open Powershell and add to path variable (or) do it manually------------------------------------------------------------
    $userenv = [System.Environment]::GetEnvironmentVariable("Path", "User") [System.Environment]::SetEnvironmentVariable("PATH", $userenv + "C:\Distros\Ubuntu", "User")

### **How do I exchange files between the Windows system and Linux Subsystem ?**

> !!! Don’t Modify them, instead work on a copy. Unless you want to get stuck in the rabbit-hole of file metadata corruption

#### Linux Files on Windows

    %userprofile%\AppData\Local\Packages
    C:\ ----------/mnt/c/
    D:\----------/mnt/d/

**Windows Files on Linux**

Yes you may run multiple Linux distros on the same machine :)