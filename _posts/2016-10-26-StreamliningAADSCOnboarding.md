---
layout: post
title: "Streamlining Azure Automation DSC Node Onboarding"
date: 2016-10-26
tags:
    - azureautomation
    - dsc
    - powershell
    - automation
    - azure
---

A simple example on getting started with Azure Automation DSC— registering your on-prem servers.

One of the biggest pain points when managing an on-prem DSC pull server is the cumbersome process of onboarding a new server. There are a series of hoops to jump through with certificates and registration in order to ensure the workflow is secure (using only HTTPS). This onboarding experience, coupled with the lack of a front-end really position the solution as a framework, to which something like Puppet Enterprise or a similar automation engine would sit on top of to bring the experience full circle. Over the last few months I worked with the Azure Automation team on their Azure Automation DSC (AA DSC) service while it was in private and public preview to provide feedback and test various scenarios. Now that the service is GA, it really feels like an enterprise ready solution, and continues to evolve and get better almost weekly.

###  Azure VM Onboarding
The onboarding experience for Azure IaaS VM’s is very straightforward. From within your automation account, you select “Add Azure VM”, select a single server from a list of eligible VMs, and you’re done. The machine is now ready to start pulling down DSC configurations which have been applied to it in the portal.

![Azure VM Onboarding Experience](/assets/posts/2016-10-26-StreamliningAADSCOnboarding/01.png)
###### *Figure:Assigning a node configuration which installs the OMS agent and registers the server with your OMS workspace.*

### On-Prem Servers
To get your on-prem servers onboarded takes a little bit more effort. This article outlines the process in depth, but essentially boils down to you running a few scripts to generate a configuration file which is manually applied to your target server to make it aware of AA DSC. While not as arduous as a traditional DSC pull server, it still requires a little bit of leg work for each new host. I wanted to put together a more seamless workflow to enable all DSC management to take place within the portal. The solution I came up with is an Azure Automation Runbook, which provides a comparable experience to onboarding Azure IaaS VMs, only requiring you to enter the on-prem server name (FQDN preferred).

![Onboarding with runbook](/assets/posts/2016-10-26-StreamliningAADSCOnboarding/02.png)
###### *Figure: Providing a computer name input as a parameter, which tells the runbook the server to target/onboard.*

### The workflow and next steps
The initial setup to get the framework established will only need to be done once, and [should] provide enough value long term to justify the upfront work. A high level overview of the steps can be found in my Azure GitHub repo [here](https://github.com/marcusclayton/azure/tree/master/AA-DSC/ConnectTo-AADSCPullServer "Repo"). The end result of executing the runbook is an on-premise server ready to receive DSC configuration MOFs, such as the OMS agent installation and registration DSC resource. A second version of the runbook is set up to consume Webhook data, and is also available in my [GitHub Repo](https://github.com/marcusclayton/azure/tree/master/AA-DSC/ConnectTo-AADSCPullServer-Webhook "Repo").