---
layout: post
title: "Streamlining Azure Automation DSC Node Onboarding"
date: 2017-04-16
tags:
    - azureautomation
    - dsc
    - powershell
    - automation
    - azure
---

A simple example on getting started with Azure Automation DSC— registering your on-prem servers.

One of the biggest pain points when managing an on-prem DSC pull server is the cumbersome process of onboarding a new server. There are a series of hoops to jump through with certificates and registration in order to ensure the workflow is secure (using only HTTPS). This onboarding experience, coupled with the lack of a front-end really position the solution as a framework, to which something like Puppet Enterprise or a similar automation engine would sit on top of to bring the experience full circle. Over the last few months I worked with the Azure Automation team on their Azure Automation DSC (AA DSC) service while it was in private and public preview to provide feedback and test various scenarios. Now that the service is GA, it really feels like an enterprise ready solution, and continues to evolve and get better almost weekly.

##  Azure VMs
The onboarding experience for Azure IaaS VM’s is very straightforward. From within your automation account, you select “Add Azure VM”, select a single server from a list of eligible VMs, and you’re done. The machine is now ready to start pulling down DSC configurations which have been applied to it in the portal.