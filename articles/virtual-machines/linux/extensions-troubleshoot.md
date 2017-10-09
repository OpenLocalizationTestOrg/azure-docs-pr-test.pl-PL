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
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="afaae-103">Rozwiązywanie problemów z błędami rozszerzenia maszyny Wirtualnej systemu Linux platformy Azure</span><span class="sxs-lookup"><span data-stu-id="afaae-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="afaae-104">Wyświetlanie stanu rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="afaae-104">Viewing extension status</span></span>
<span data-ttu-id="afaae-105">Szablony usługi Azure Resource Manager można wykonać z hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afaae-105">Azure Resource Manager templates can be executed from hello  Azure CLI.</span></span> <span data-ttu-id="afaae-106">Po szablonu hello jest wykonywane, można wyświetlić stan rozszerzenia hello z Eksploratora zasobów Azure lub hello narzędzi wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="afaae-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="afaae-107">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="afaae-107">Here is an example:</span></span>

<span data-ttu-id="afaae-108">Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="afaae-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="afaae-109">Oto hello przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="afaae-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="afaae-110">]</span><span class="sxs-lookup"><span data-stu-id="afaae-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="afaae-111">Rozwiązywanie problemów z błędami Extenson:</span><span class="sxs-lookup"><span data-stu-id="afaae-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="afaae-112">Ponowne uruchomienie rozszerzenia hello na powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="afaae-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="afaae-113">Jeśli używasz skryptów na powitania maszyny Wirtualnej przy użyciu niestandardowe rozszerzenie skryptu, można uruchomić czasami wystąpił błąd, gdy maszyna wirtualna została utworzona pomyślnie, ale hello skryptu nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="afaae-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="afaae-114">W obszarze tych warunków hello zalecany sposób toorecover tego błędu jest rozszerzeniem hello tooremove i ponownie hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="afaae-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="afaae-115">Uwaga: W przyszłości, ta funkcja będzie rozszerzone tooremove hello potrzebę odinstalowywanie hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="afaae-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-cli"></a><span data-ttu-id="afaae-116">Usuń rozszerzenie hello z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="afaae-116">Remove hello extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="afaae-117">Gdzie "publsher-name" odpowiada typu rozszerzenia toohello z danych wyjściowych hello "azure get widok wystąpienia maszyny wirtualnej-", a nazwa jest nazwą hello hello rozszerzenie zasobu z hello szablonu</span><span class="sxs-lookup"><span data-stu-id="afaae-117">Where "publsher-name" corresponds toohello extension type from hello output of "azure vm get-instance-view" and name is hello name of hello extension resource from hello template</span></span>

<span data-ttu-id="afaae-118">Po usunięciu rozszerzenia hello hello szablon może być ponowne wykonanie toorun hello skryptów na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afaae-118">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

