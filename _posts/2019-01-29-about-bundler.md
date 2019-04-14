---
layout: post
title: DevOps on Steroids with Oracle Kubernetes Engine, Oracle Developer Cloud Service,
  Wercker/Spinnaker, Helm and Monocular — Setup Pre-reqs (2/3)
author: vamsi
categories:
- Devops
- OCI
- Cloudnative
image: "/uploads/containers.jpeg"

---
This post we primarily focus on setting up of pre-requisites for the end to end DevOps environment using Oracle Cloud. [Link to Part 1](https://medium.com/jsonlovesyaml/devops-on-steroids-with-oracle-kubernetes-engine-oke-oracle-developer-cloud-service-wercker-4eb7d45be6be)(TL;DR)

**Definition of Terms**

* [**Oracle Kubernetes Engine**](https://cloud.oracle.com/containers/kubernetes-engine) is a managed service for running Production Grade Highly Available Kubernetes Clusters
* [**Oracle Developer Cloud Service**](https://cloud.oracle.com/en_US/developer-service) is a managed service to streamline software development and delivery
* [**Wercker**](http://www.wercker.com/) aka [**Oracle Container Pipelines**](https://cloud.oracle.com/en_US/containers/pipelines) is a managed container native continuous integration and delivery platform
* [**Helm**](https://helm.sh/) and Tiller are Client-Side and Server-Side Package Management tools for Kubernetes through abstractions called Charts
* [**Monocular**](https://github.com/helm/monocular) is a Web-UI for Helm and Tiller.
* [**Spinnaker**](https://www.spinnaker.io/) is a battle-tested Continuous Deployment Platform

### Initial Setup

#### Setup Oracle Kubernetes Engine

    --> Through Console ( Involves Button Clicks ) Tutorial --> Through a Terraform Script Link

#### Setup Oracle Developer Cloud Service (Dev-CS) / Github

    --> Here's an interactive tutorial to setup Dev-CS Link--> Just to setup Github-HelloWorld

#### Setup Oracle Container Pipelines / Wercker Account It’s Free!!

    --> Here's a detailed tutorial on setting up your first Container Native Pipeline

#### Setting up Helm

**Windows**

1. Install Choco — Package Manager [Tutorial](https://medium.com/@JockDaRock/installing-the-chocolatey-package-manager-for-windows-3b1bdd0dbb49)
2. Open Powershell as Administrator and run the following commands

   choco install kubernetes-clichoco install kubernetes-helm

3\. Setup the “**_kubeconfig_**” env variable to point to the directory where the file is downloaded.

    1) Right Click My Computer → Properties → Advanced System Settings → Environment Variables → System variables → “KUBECONFIG” 2) Right Click My Computer → Properties → Advanced System Settings → Environment Variables → User variables → “KUBECONFIG”

If you don't have the kubeconfig file of Oracle Kubernetes Engine and don’t know how to download it please use this [**link**](https://docs.cloud.oracle.com/iaas/Content/ContEng/Tasks/contengdownloadkubeconfigfile.htm)

The [Oracle Kubernetes Engine](https://cloud.oracle.com/containers/kubernetes-engine) comes installed with Tiller, hence there is no need to install it separately, however, to ensure that the tiller pod is up to date

    helm inithelm init --upgrade --service-account tiller

**Linux**

Install and configure kubectl and helm on linux

    Kubectl : LinkHelm : Link

**Post Installation**

    helm inithelm init --upgrade --service-account tiller

#### Make Kubernetes Cloud Infrastructure Aware

**Flex Volume Drivers and Provisioners:** The FlexVolume Plugins and Provisioners provide Kubernetes the capability to become infrastructure aware, this usually comes pre-configured in the Oracle Kubernetes Engine. In case you don’t use the managed service and you’ve set it up the hard way, use links below to make Kubernetes, Cloud Infrastructure Aware

    OCI Flex Volume Driver Install - LinkOCI Flex Volume Provisioner Install - Link

#### Set up Monocular

Monocular provides a Search and Discovery UI for Helm Repositories, Releases and Deployments and comes with a few simple and easy to use features. To install Monocular simply run the command

Read More about [Monocular](https://github.com/helm/monocular)

![](https://cdn-images-1.medium.com/max/750/0*yujOOiV6Cu_Oe_1k.gif)

    1)Install an NGINX Ingresshelm install stable/nginx-ingress
    
    2)Install Monocularhelm repo add monocular https://helm.github.io/monocularhelm install monocular/monocular

#### Setup Spinnaker

To be precise, Spinnaker would be a centralized task runner across all your Kubernetes clusters and the container pipelines and git repos. The best practice is to run spinnaker on a separate cluster and all other workloads in another cluster.

    helm install --name spinnaker-test --namespace spinnaker stable/spinnaker --timeout 600

Spinnaker installation and setup could take quite sometime and hence timeout is specified to handle a fall back.

The methodology to tie all these tools together will be discussed in detail on the next post.