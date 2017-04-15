---
layout: post
title: "Modernizing SCCM Application Approval"
date: 2017-01-30
tags:
    - azure
    - ARM
author: marcus
---

Addinig an automation workflow to SCCM application requests

As it stands, there are no native options within SCCM to allow for seamless application approval workflows. The ability to approve or deny an application request is surfaced within the SCCM console, and is traditionally managed by the SCCM administrator(s). A [3rd party solution existed](http://blog.coretech.dk/kea/coretech-application-e-mail-approval-tool/ "CoreTech") which helped fulfill this need, allowing a user’s manager to navigate to an internal (corp) website and approve or deny the request. The solution required the manager to be on the corp network, and was only customizable if the admin had a fairly decent understanding of asp.net programming.

![Azure VM Onboarding Experience](/assets/posts/2017-01-30-SCCM-App-Approval/01.png)
##### *Figure: Approval email a user’s manager will receive, which clearly identifies the request, and how to take action.*

To bring a modern approach to this workflow, I put together a solution which leverages Azure Logic Apps, an Azure SQL database, and PowerShell script which provides [mobile friendly] secure email based approval of SCCM application requests. At a high level, the user requests an application from the app catalog, which creates a new request in the Azure SQL database, spawning a Logic App run, which sends an approval email to user’s manager (or pre-defined mailbox/distribution list), waits for an approve or deny response, and ultimately approves or denies the request within SCCM. Once the request has been approved or denied, the user will receive an email notification, updating them with the request status. By putting the engine in an Azure Logic App, this solution can easily be extended or tailored to hook into [any] service which has a documented API or pre-built Microsoft connector (the [current list of connectors](
https://docs.microsoft.com/en-us/azure/connectors/apis-list "Logic App Connectors") is fairly long, and grows weekly). The code is available on [GitHub](https://github.com/marcusclayton/SCCM_App_Approval "Repo").