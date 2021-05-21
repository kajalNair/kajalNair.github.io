---
title: State of Different IaC Tools 
description: Static Analysis of Infrastructure as Code
---


> TL;DR
> 
> This blog will address the current state of IaC tools starting with Terraform. We will discuss about an analysis performed on the open source Terraform modules, and vulnerable cloud environments to measure the working of different infrastructure-as-code static analysis tools. The data in this blog is collected by scanning public resources within Terraform modules and popular projects like CloudGoat, TerraGoat, etc. 
The work discussed below has been done by [Ashwath](https://twitter.com/ka3hk), [Rashika](https://www.linkedin.com/in/rashika-singh-7529b4137), [Niket](https://www.linkedin.com/in/masterniketyadav/), [Kajal](https://twitter.com/kajalN6) and training project developed by [Anand Gupta](https://www.linkedin.com/in/anand-gupta-8495aa43/) along with interns'20. 



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
What is Terraform then?
+ an open source IaC provisioning tool written in Go.
+ supports multiple cloud providers. 
+ the code is written in Harshicorp Configuration Language and source code files that contains these definitions have .tf extension.

![Terraform]({{ '/static/assets/terraform-code-block-file.png' | prepend: site.baseurl | replace: '//', '/' }})

> The sample Terraform code above shows that an AWS cloud provider has been configured and a VPC is created with some attribute. 


In IaC, Terraform’s role is to ensure that the state of resources in the cloud(any provider of your choice) is equal to the state expressed in code (tf file).



## Terraform Security - Statistics
According to an analysis done by [Bridgecrew](https://bridgecrew.io/wp-content/uploads/state-of-open-source-terraform-security-2020.pdf), stated that 
+ nearly 44% of Terraform modules used to provision different cloud providers were misconfigured 
+ these modules have been downloaded over 15M times
+ Most of the misconfigurations are in Backup and Recovery, Logging, and Encryption categories. 

Networking or compute instances exposed on the Internet can be hacked by malicious actors that can attempt to use them to infiltrate into privately hosted cloud networks and, from there, obtain access to sensitive data. 

![Terraform-misconfig-1]({{ '/static/assets/T-Misconfig-Stats-1.png' | prepend: site.baseurl | replace: '//', '/' }}) ![Terraform-misconfig-2]({{ '/static/assets/T-Misconfig-Stats-2.png' | prepend: site.baseurl | replace: '//', '/' }})



## How did we setup our experiment?
In the beginning, we decided to look for different IaC tools like tfscan, terrascan, checkov, tflint, etc., available for Terraform code scanning and find out the best project. For this, we had to gather information on these tools like 
* which cloud providers are supported?
* how many rule sets are in place?
* True/False positive analysis
* Detection rate, no. of missed findings
* if the tools are well maintained and well-documented

Once we had the list (having information gathered above), our next steps were as followed:
1. Search the internet (start with github) for Terraform files
2. Download all the Terraform files onto local disk
3. Run it against different tools
4. Compare results

For step one, we used URL below to find all the Terraform files: 
```link
https://github.com/search?q=.tf+extension%3Atf+filename%3Amain&type=Code&ref=advsearch&l=&l=
```

The search identified more than 15k files.
![github-search]({{ '/static/assets/github-search-for-tf-files.png' | prepend: site.baseurl | replace: '//', '/' }})

We also developed an intentionally vulnerable cloud environment, Synopsys VCE, a training project to learn how to identify and avoid infrastructure as code misconfigurations and security risks. Though there are plenty of projects like SadCloud, Terragoat, Cloudgoat etc., out there to learn how common configuration errors can find their way into production cloud environments. The image below shows the common misconfigurations present in these learning projects.

![vce]({{ '/static/assets/vulnerable-cloud-env.png' | prepend: site.baseurl | replace: '//', '/' }})

We then scanned the data set for known misconfigurations and risk, and this is what we found. 

![scan-analysis]({{ '/static/assets/scan-analysis.png' | prepend: site.baseurl | replace: '//', '/' }})



## Result of our analysis

![result-analysis]({{ '/static/assets/result-analysis.png' | prepend: site.baseurl | replace: '//', '/' }})

Our observations so far concluded that:
- the reason for these misconfigurations is that as Terraform modules come pre-built with standardized configurations and variable templates, these modules do not include best practices/policies as default, rather left as an option for the developers to use.
- Most of the tools do not have proper security checks in place for different cloud providers.
- Tfsec and checkov can be considered as reliable tools for Terraform code scanning. 
- While finding the detection rate, we observed that the number for false positives flagged by these tools were quite high. 
- If you have an assessment where you have to audit infrastructure related configurations, then [checkov](https://github.com/bridgecrewio/checkov) is the best option to go with.
It has over 300 compliance and security checks across AWS, Azure, and Google Cloud. These security checks are based on policies defined by Center of Internet Security (CIS), AWS Foundations, SOC2, PCI, and additional best practices.



## Afterwords
Terraform security is becoming an increasingly important area for DevOps engineers to learn and implement. Throughout this adventure, we gained useful experience, and learned about working for different IaC tools. We hope this research helps you get started with right IaC static analysis tools. :)











