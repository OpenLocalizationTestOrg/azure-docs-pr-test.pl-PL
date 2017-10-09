---
title: "błędy rozszerzenia maszyny Wirtualnej systemu Windows aaaTroubleshooting | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat rozwiązywania problemów z błędami rozszerzenia maszyny Wirtualnej systemu Windows Azure"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a>Rozwiązywanie problemów z błędami rozszerzenia maszyny Wirtualnej systemu Windows Azure
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Wyświetlanie stanu rozszerzenia
Szablony usługi Azure Resource Manager można wykonać z programu Azure PowerShell. Po szablonu hello jest wykonywane, można wyświetlić stan rozszerzenia hello z Eksploratora zasobów Azure lub hello narzędzi wiersza polecenia.

Oto przykład:

Program Azure PowerShell:

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

Oto hello przykładowe dane wyjściowe:

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  ]

## <a name="troubleshooting-extension-failures"></a>Rozwiązywanie problemów z błędami rozszerzenia
### <a name="re-running-hello-extension-on-hello-vm"></a>Ponowne uruchomienie rozszerzenia hello na powitania maszyny Wirtualnej
Jeśli używasz skryptów na powitania maszyny Wirtualnej przy użyciu niestandardowe rozszerzenie skryptu, można uruchomić czasami wystąpił błąd, gdy maszyna wirtualna została utworzona pomyślnie, ale hello skryptu nie powiodło się. W obszarze tych warunków hello zalecany sposób toorecover tego błędu jest rozszerzeniem hello tooremove i ponownie hello szablonu.
Uwaga: W przyszłości, ta funkcja będzie rozszerzone tooremove hello potrzebę odinstalowywanie hello rozszerzenia.

#### <a name="remove-hello-extension-from-azure-powershell"></a>Usuń rozszerzenie hello z programu Azure PowerShell
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

Po usunięciu rozszerzenia hello hello szablon może być ponowne wykonanie toorun hello skryptów na powitania maszyny Wirtualnej.

