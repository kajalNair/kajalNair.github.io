---
title: State of different Open Source Tools 
description: Static Analysis of Infrastructure as Code

---

> This post includes an analysis done by @ka3hk, Rashika, Niket, @kajalN6 and training project developed by Anand Gupta along with interns'20. 

## Traditional way of doing it?
Traditionally, IT people would put servers in place and configure them manually. Now suppose you want to deploy an application, you would spin up a VM and configure it to correct settings required by the OS and application. You would install softwares and packages needed to get your application up and running. Now imagine that you want to run few more instances and to do all that manually, is gonna take hell lot of time. As the scale of infrastructure continues to expand, it is imperative to change the way infrastructure is designed, developed, configured, managed, and maintained. This is why term IaC was coined.

So the real idea behind infrastructure as code is: How do we take this whole process in some sense and capture that in a codified way? So if you need to do it as many times as you want, you can automate that. Every morning, you can hit a script that scales up during high peak at daytime, and every evening, hit the same script to bring it back down to required size.



## Infrastructure as Code
> According to Wikipedia, Infrastructure as code is the process of managing and provisioning computer data centers through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools. 


Simply put, it lets you manage your infrastructure by just using configuration files.

But how does IaC streamline all these processes?


## Choosing an Infrastructure as Code tool
The IaC approach is widely used in modern deployment, configuration management, virtualization and orchestration software. And you would have heard of tools like ansible, chef, puppet, docker and kubernetes and wondered what these are and how Terraform, (which we'll discuss shortly) differs from them?

+ Ansible, chef, puppets are mainly used for provisioning, configuration management and application deployment.
+ Docker and Kubernetes, the leading tools used for container creation and orchestration.
+ Terraform's strength lies in provisioning hardware resources, rather than installing softwares and managing configurations.


## Role of Terraform
Terraform is an open source IaC provisioning tool written in Go and developed by Harshicorp. It supports multiple cloud providers. The code that defines the infra is written in in Harshicorp Configuration Language and source code files that contains these definations have .tf extension.

![Terraform]({{ '/static/assets/terraform-code-block-file.png' | prepend: site.baseurl | replace: '//', '/' }})

> The sample terraform code above shows that an AWS cloud provider has been configured and a VPC is created with some attribute. 

In IaC, Terraform’s role is to ensure that the state of resources in the cloud(any provider of your choice) is equal to the state expressed in code (tf file).

## Terraform Security - Statistics
Few months back, we at Synopsys did an analysis where we tried to find out different open source static analysis tools available for infra-as-code, particularly terraform code scanning and how they work.
We also developed an intentionally vulnerable cloud environment, Synopsys VCE, a training project to learn about how to identify and avoid infrastructure as code misconfigurations and security risks. Though there are plenty of projects like SadCloud, Terragoat, Cloudgoat etc., out there to learn how common configuration errors can find their way into production cloud environments. 

![vce]({{ '/static/assets/vulnerable-cloud-env.png' | prepend: site.baseurl | replace: '//', '/' }})

To gather this data, we analyzed the public resources within more than 1k open source terraform modules used to provision cloud resources alongside other vulnerable cloud environments, by using these tools to find out more about their security coverage and to understand how they work. 

![iac-tools]({{ '/static/assets/comparison-of-iac-tools.png' | prepend: site.baseurl | replace: '//', '/' }})


According to a fantastic analysis done by Bridecrew and [shown here](https://bridgecrew.io/wp-content/uploads/state-of-open-source-terraform-security-2020.pdf), stated that nearly 44% of terraform modules used to provision different cloud providers were misconfigured and these modules have been downloaded over 15M times. Most of the misconfigurations are in Backup and Recovery, Logging, and Encryption categories. Networking or compute instances exposed on the Internet can be hacked by malicious actors that can attempt to use them to infiltrate into privately hosted cloud networks and, from there, obtain access to sensitive data. 


![Terraform-misconfig-1]({{ '/static/assets/T-Misconfig-Stats-1.png' | prepend: site.baseurl | replace: '//', '/' }}) ![Terraform-misconfig-2]({{ '/static/assets/T-Misconfig-Stats-2.png' | prepend: site.baseurl | replace: '//', '/' }})

We also found that the reason for these misconfigurations is that as Terraform modules come pre-built with standardized configurations and variable templates, these modules do not include best practices/policies as default, rather left as an option for the developers to use.


We scanned the data set for known misconfigurations and risk, and this is what we found.

![scan-analysis]({{ '/static/assets/scan-analysis.png' | prepend: site.baseurl | replace: '//', '/' }})

## Result of our analysis

![result-analysis]({{ '/static/assets/result-analysis.png' | prepend: site.baseurl | replace: '//', '/' }})

Checkov proved to be best iac tool out of all. It has over 300 compliance and security checks across AWS, Azure, and Google Cloud. These security checks are based on policies defined by Center of Internet Security (CIS), AWS Foundations, SOC2, PCI, and additional best practices.  

Terraform security is becoming an increasingly important area for DevOps engineers to learn and implement. We hope this helps you to get started with right tools.


### References
https://www.hashicorp.com/resources/what-is-infrastructure-as-code

https://bridgecrew.io/wp-content/uploads/state-of-open-source-terraform-security-2020.pdf

https://github.com/bridgecrewio/terragoat 

https://github.com/RhinoSecurityLabs/cloudgoat

https://github.com/appsecco/attacking-cloudgoat2

https://github.com/bridgecrewio/checkov

https://github.com/accurics/terrascan

https://github.com/terraform-linters/tflint

https://www.terraform.io/

https://github.com/nccgroup/ScoutSuite/



