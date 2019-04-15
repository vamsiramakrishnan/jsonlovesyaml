---
layout: post
title: Custom Steps with Wercker
author: vamsi
categories:
- cicd
- devops
- oci
- wercker
image: "/assets/images/cicdcustomstep.jpeg"
tags: featured

---
If you cannot find a pre-defined step in the Wercker Step store that satisfies your requirement, and if you want these steps defined as custom-code to be consistent and be executed in the same order every single time, you can write your own step.

    -----------  History-----------
    * Oracle completed the acquisition of Wercker in 2017 and added it to their rich CI/CD offerings. 
    * In this article you may find Oracle Container Pipelines being used interchangeably with Wercker!!

If you are new to Wercker, here is some suggested reading

[**CI-CD simplified with Wercker + Kubernetes on Oracle Cloud Infrastructure**  
_Step up and modernize your integration and deployment pipeline with Wercker and Kubernetes_medium.com](https://medium.com/jsonlovesyaml/ci-cd-simplified-with-wercker-kubernetes-on-oracle-cloud-infrastructure-a2332497d36f "https://medium.com/jsonlovesyaml/ci-cd-simplified-with-wercker-kubernetes-on-oracle-cloud-infrastructure-a2332497d36f")

This article relies on the example step for helm that I published on Wercker. Improvements and Contributions welcome!!

#### Address of Repo

[**vamsiramakrishnan/step-helm**  
_Wercker Custom Step to execute helm on Wercker. Contribute to vamsiramakrishnan/step-helm development by creating an…_github.com](https://github.com/vamsiramakrishnan/step-helm "https://github.com/vamsiramakrishnan/step-helm")

### How to

1. Writing a step on Wercker is no different from using them as a part of your pipeline.

   \--------Concepts--------
   A custom Wercker step is a sequence of Wercker steps A custom Wercker step is a container published into the Step Store

2\. You will need the following

    1. A Step Manifest File 
    2. A Wercker.yml File
    3. A run.sh File

#### Step manifest

The step manifest contains the following information

    ----------------------------Anatomy of the Step manifest----------------------------
    1. Name of your step 
    2. Version of your step 
    3. Summary
    4. Configurable Parameters

#### How does the step manifest file look ?

    ----GIST----
    1) Has Kubeconfig parameters 
    2) Has Helm parameters

#### Wercker.yml File

    1. Define your step build like any other build
    2. Add a Publish Step in the end. 

#### How does a Publish Step Look ?

#### The run.sh file

The run.sh file is the container-entrypoint of the step when it is invoked. Once wercker executes the code in the run.sh file , it moves on to the next step.

#### How does a Run.Sh Look

    -----------Pseudo-Code-----------#
    !/bin/sh
    # Use the Packages defined in Wercker.yml
    # Do Something using Property Variables defined in Step Manifest
    # Echo Something for the user's benefit
    # End of Script

**Code:**

### Import it into Wercker

> Building Step== Building Application

> * in Wercker :)

    ---------Workflow ---------
    1) Create New Application
    2) Connect it with your SCM in Oracle Developer Cloud Service/ Github/Gitlab
    3) Select the repository
    4) Add the defined Wercker.yml from repo 
    5) Define Pipelines as written in the wercker.yml6) Trigger Build , by updating 

#### Go to the Steps store

Voila!! use it!!