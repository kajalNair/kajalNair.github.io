---
title: State of different Open Source Tools 
description: Static Analysis of Infrastructure as Code

---

> write something here too.

## Traditional way of doing it?
Traditionally, IT people would put servers in place and configure them manually. Now suppose you want to deploy an application, you would spin up a VM and configure it to correct settings required by the OS and application. You would install softwares and packages needed to get your application up and running. Now imagine that you want to run few more instances and to do all that manually, is gonna take hell lot of time. As the scale of infrastructure continues to expand, it is imperative to change the way infrastructure is designed, developed, configured, managed, and maintained. This is where Infrastructure as Code comes into play.

So the real idea behind infrastructure as code is: How do we take this whole process in some sense and capture that in a codified way? So if you need to do it as many times as you want, you can automate that. Every morning, you can hit a script that brings up a thousand machines, and every evening, hit the same script to bring it back down to required size.



## Infrastructure as Code
> According to Wikipedia, Infrastructure as code is the process of managing and provisioning computer data centers through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools. 

##
Simply put, it lets you manage your infrastructure by just using configuration files.

But how does IaC streamline all these processes?


## Choosing an Infrastructure as Code tool
The IaC approach is widely used in modern deployment, configuration management, virtualization and orchestration software. And you would have heard of tools like ansible, chef, puppet, docker and kubernetes and wondered what these are and how Terraform, (which we'll discuss shortly) differs from them?

+ Ansible, chef, puppets are mainly used for provisioning, configuration management and application deployment.
+ Docker and Kubernetes, the leading tools used for container creation and orchestration.
+ Terraform's strength lies in provisioning hardware resources, rather than installing softwares and managing configurations.


## Role of Terraform
Terraform is an open source IaC provisioning tool written in Go and developed by Harshicorp. It supports multiple cloud providers. The code that defines the infra is written in in Harshicorp Configuration Language and source code files that contains these definations have .tf extension.


