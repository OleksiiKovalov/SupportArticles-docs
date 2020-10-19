---
title: The uptime value of the Hyper-V Management console changes to the resume time of the last pause
description: Describes an issue that occurs when you back up a virtual machine that is running on a Hyper-V host operating system.
ms.date: 09/14/2020
author: Deland-Han
ms.author: delhan 
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: Integration components
ms.technology: HyperV
---
# The uptime value of the Hyper-V Management console changes to the resume time of the last pause

This article describes an issue that occurs when you back up a virtual machine that is running on a Hyper-V host operating system.

_Original product version:_ &nbsp; Windows Server 2012 R2  
_Original KB number:_ &nbsp; 2981479

## Symptom

Consider the following scenario:
- You have a virtual machine that is running on a Hyper-V host operating system.
- The host operating system is Windows Server 2012 or Windows Server 2012 R2.
- You back up the virtual machine.  

In this scenario, the uptime value of the Hyper-V Management console changes to the resume time of the last pause instead of the time when backup completed. 

When the virtual machine pauses, the uptime value changes to the time when the virtual machine paused. If the virtual machine never pauses, the uptime value changes to the time when the virtual machine was in a stopped state. That is, the uptime value changes to **00:00:00**. And, no save or reset logs are created when the backup starts.

## Workaround

To work around this issue, restart the Virtual Machine Management service  (VMMS). The Hyper-V Management console will display a correct operating system uptime value after you restart VMMS.