---
title: Kubernetes Playground on your laptop
date: 2019-04-14 13:21:00 Z
categories:
- kubernetes
tags:
- featured
layout: post
author: vamsi
image: "/assets/images/playground.jpeg"
---

Getting started with Kubernetes on a vanilla linux installation can be overwhelming considering the number of steps and the repetitions involved in setting up master and worker nodes. In this post I intend to explain how to set up Minikube with Hyper-V on your windows 10 laptop so you can play around with it easily.

#### Minikube

![Image result for minikube](https://cdn-images-1.medium.com/max/675/1*UBwQRP_HpjawvPzlvdHfWw.jpeg)

Source: Kubernetes

**_Minikube_** _is a tool that makes it easy to run Kubernetes locally. Minikube runs a single-node Kubernetes cluster inside a VM on your laptop for users looking to try out Kubernetes._

#### Hyper-V

![](https://cdn-images-1.medium.com/max/675/0*HrUd-EN4jEsisM_n.png)

Source: Wikipedia

_A component of Windows Server **Microsoft Hyper-V**, codenamed Viridian and formerly known as Windows Server Virtualization, is a native hypervisor. It can create virtual machines on x86–64 systems running Windows._

#### Pre-requisites:

* **Hyper-V** : [How to get Hyper-V Installed](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)
* **Chocolatey**: [How to install Chocolatey Package Manager](https://medium.com/@JockDaRock/installing-the-chocolatey-package-manager-for-windows-3b1bdd0dbb49)

**Step 1:** Open Windows Power Shell with Admin Privileges ( Right Click -> Run as Administrator )

**Step 2:** Install the package minikube using chocolatey package manager

    ##Minikube has a kubernetes-cli dependency which will get auto-installed along with Minikube ##

    choco install minikube

**Step 4:** Post Successful installation verify if your Powershell prints an output like this

![](https://cdn-images-1.medium.com/max/900/1*HYIrZ2o3UxBSbPeFQSr1Yw.png)

**Step 5:** Install the Kubernetes Command Line Interface that will help you access any kubernetes cluster ( Local or otherwise )

    choco install kubernetes-cli

![](https://cdn-images-1.medium.com/max/675/1*QIE-e8SWaMnjbaMaMMBTnw.png)

**Step 6:** Change settings of Hyper-V to work around a bug of minikube.

![](https://cdn-images-1.medium.com/max/675/1*R_rQ-R3bT53arPY0vn9ddA.png)

**Step 7:** Open Hyper-V and go to Virtual Switch

**Step 8:** Click on **New virtual network switch** on the right hand side, select **External** for the network type, and then click the **Create Virtual Switch**button.

![](https://cdn-images-1.medium.com/max/900/1*s13PahCGGzv7HVD08nq8Uw.png)

**Step 9:** Name the network Minikube v switch and then set it as an external network

![](https://cdn-images-1.medium.com/max/900/1*s0zfwR_RKvfb47ekPX1eKA.png)

**Step 10:** Run the following command in command prompt with admin privileges to start the minikube VM and configure it to be used with kubectl

    minikube start --vm-driver hyperv --hyperv-virtual-switch "minikube v switch"

![](https://cdn-images-1.medium.com/max/900/1*yeYK9MtfESStuVLlzgWirQ.png)

**Step 11**: Open a new command window, this time as a normal user and run the following command

    kubectl get pods -n kube-system

You should see the following result

![](https://cdn-images-1.medium.com/max/900/1*o5QzKsoHEy4ZBRRCDMAvNA.png)

**Step 12**: If you are a kubernetes dashboard person, you can open that up by typing in the following command in the command line window with the same privileges that you started minikube

    minikube dashboard