---
layout: post
title: "Adding an Existing ARM VM to Availability Set"
date: 2017-01-29
tags:
    - azure
    - ARM
author: marcus
---

Add ARM VM to an availability set.

In certain scenarios, Azure Resource Manager (ARM) virtual machines are required to be deployed into an availability set. One such scenario is the use of load balancers. One of more VM’s can exist in the availability set, but this option is only exposed in the portal during the initial VM deployment. If a VM was deployed without specifying an availability set, the only [traditional] option was to delete and recreate it. Using the script (linked below) will allow you to preserve the VM’s settings and VHD, delete the VM, and reprovision into an availability set. This is important for VM’s which have already been fully configured, joined to a domain, and are actively being used (i.e. a SCOM server). The process requires minimal downtime, and allows for a more seamless fix. The code is available on [GitHub](https://github.com/marcusclayton/azure/blob/master/Management/Add-AzureRMtoAvailabilitySet.ps1 "Repo").