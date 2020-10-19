---
title: File Server Resource Manager could not load WMI objects on Windows Server 2012
description: Fixes an error that occurs when starting the File Server Resource Manager on Windows Server 2012.
ms.date: 09/14/2020
author: Deland-Han
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: File Server Resource Manager (FSRM)
ms.technology: BackupStorage
---
# File Server Resource Manager could not load WMI objects on Windows Server 2012

This article helps fix an error that occurs when starting the File Server Resource Manager on Windows Server 2012.

_Original product version:_ &nbsp;Windows Server 2012 R2  
_Original KB number:_ &nbsp;2831687

## Symptoms

When starting the File Server Resource Manager on Windows Server 2012, you may receive the following error message:

> File Server Resource Manager could not load WMI objects on "Server Name".

If you query the MSFT_FSRMSettings WMI class under root\Microsoft\Windows\FSRM while having the described error reported, you may then receive the following WMI error:

> Error 0x80041001 (Generic failure).

## Cause

This problem occurs because the Windows Management Instrumentation service is restarted after the FSRM Service and a new provider load/registration for the FSRM provider is needed.

## Resolution

To resolve this problem, restart the FSRM Service. 

If you notice this is a reoccurring issue, there are two actions needed:


- Verify and investigate the Windows Management Instrumentation Service is restart issue to solve the behavior.
- Add a dependency for the FSRM Service in the registry, so that it gets restarted when the WMI service is restarted. To add the dependency in the registry, follow the steps:
    1. On the Start screen, click the Search tile.
    2. Type regedit in the Search window and then double-click regedit.exe 
    3. Locate the following registry entry:
     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\srmsvc` 

    4. From the right-side pane, right-click DependOnService, and then click Modify 
    5. Add WINMGMT to the Multi-String Value
    6. Click on OK and then exit the registry editor
    7. Reboot the computer.

## More information

In a particular case, the Windows Management Instrumentation is restarted as part of a WMI Repository Rebuild action. In that case, an investigation would be needed as to why the WMI Repository is being rebuilt. 

If you're running SCCM 2012, ensure that you're not running in the behavior described in the following article:

 [2796086](https://support.microsoft.com/help/2796086) Configuration Manager Management Points collocated with clients fail after installing Windows Management Framework 3.0 and running Client Health Evaluation