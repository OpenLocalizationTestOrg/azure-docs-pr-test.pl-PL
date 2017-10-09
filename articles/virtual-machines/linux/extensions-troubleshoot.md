---
title: "aaaTroubleshooting maszyny Wirtualnej systemu Linux błędy rozszerzenia | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat rozwiązywania problemów z błędami rozszerzenia maszyny Wirtualnej systemu Linux platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Rozwiązywanie problemów z błędami rozszerzenia maszyny Wirtualnej systemu Linux platformy Azure
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Wyświetlanie stanu rozszerzenia
Szablony usługi Azure Resource Manager można wykonać z hello wiersza polecenia platformy Azure. Po szablonu hello jest wykonywane, można wyświetlić stan rozszerzenia hello z Eksploratora zasobów Azure lub hello narzędzi wiersza polecenia.

Oto przykład:

Azure CLI:

      azure vm get-instance-view


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

## <a name="troubleshooting-extenson-failures"></a>Rozwiązywanie problemów z błędami Extenson:
### <a name="re-running-hello-extension-on-hello-vm"></a>Ponowne uruchomienie rozszerzenia hello na powitania maszyny Wirtualnej
Jeśli używasz skryptów na powitania maszyny Wirtualnej przy użyciu niestandardowe rozszerzenie skryptu, można uruchomić czasami wystąpił błąd, gdy maszyna wirtualna została utworzona pomyślnie, ale hello skryptu nie powiodło się. W obszarze tych warunków hello zalecany sposób toorecover tego błędu jest rozszerzeniem hello tooremove i ponownie hello szablonu.
Uwaga: W przyszłości, ta funkcja będzie rozszerzone tooremove hello potrzebę odinstalowywanie hello rozszerzenia.

#### <a name="remove-hello-extension-from-azure-cli"></a>Usuń rozszerzenie hello z wiersza polecenia platformy Azure
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

Gdzie "publsher-name" odpowiada typu rozszerzenia toohello z danych wyjściowych hello "azure get widok wystąpienia maszyny wirtualnej-", a nazwa jest nazwą hello hello rozszerzenie zasobu z hello szablonu

Po usunięciu rozszerzenia hello hello szablon może być ponowne wykonanie toorun hello skryptów na powitania maszyny Wirtualnej.

