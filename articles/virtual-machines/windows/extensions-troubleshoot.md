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
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="c0fa7-103">Rozwiązywanie problemów z błędami rozszerzenia maszyny Wirtualnej systemu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="c0fa7-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="c0fa7-104">Wyświetlanie stanu rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="c0fa7-104">Viewing extension status</span></span>
<span data-ttu-id="c0fa7-105">Szablony usługi Azure Resource Manager można wykonać z programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c0fa7-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="c0fa7-106">Po szablonu hello jest wykonywane, można wyświetlić stan rozszerzenia hello z Eksploratora zasobów Azure lub hello narzędzi wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c0fa7-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="c0fa7-107">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="c0fa7-107">Here is an example:</span></span>

<span data-ttu-id="c0fa7-108">Program Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c0fa7-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="c0fa7-109">Oto hello przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c0fa7-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="c0fa7-110">]</span><span class="sxs-lookup"><span data-stu-id="c0fa7-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="c0fa7-111">Rozwiązywanie problemów z błędami rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="c0fa7-111">Troubleshooting extension failures</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="c0fa7-112">Ponowne uruchomienie rozszerzenia hello na powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c0fa7-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="c0fa7-113">Jeśli używasz skryptów na powitania maszyny Wirtualnej przy użyciu niestandardowe rozszerzenie skryptu, można uruchomić czasami wystąpił błąd, gdy maszyna wirtualna została utworzona pomyślnie, ale hello skryptu nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="c0fa7-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="c0fa7-114">W obszarze tych warunków hello zalecany sposób toorecover tego błędu jest rozszerzeniem hello tooremove i ponownie hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="c0fa7-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="c0fa7-115">Uwaga: W przyszłości, ta funkcja będzie rozszerzone tooremove hello potrzebę odinstalowywanie hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="c0fa7-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-powershell"></a><span data-ttu-id="c0fa7-116">Usuń rozszerzenie hello z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0fa7-116">Remove hello extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="c0fa7-117">Po usunięciu rozszerzenia hello hello szablon może być ponowne wykonanie toorun hello skryptów na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c0fa7-117">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

