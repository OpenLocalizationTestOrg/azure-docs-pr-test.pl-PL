---
title: "aaaCreate i zarządzania maszynami wirtualnymi w usłudze DevTest Labs z wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Azure DevTest Labs toouse i zarządzania maszynami wirtualnymi Azure CLI 2.0"
services: devtest-lab,virtual-machines
documentationcenter: na
author: lisawong19
manager: douge
editor: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: liwong
ms.openlocfilehash: 98ea3aa7b2489bff61971573aaf584984cd811e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a><span data-ttu-id="58835-103">Tworzenie i zarządzanie maszynami wirtualnymi z DevTest Labs przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="58835-103">Create and manage virtual machines with DevTest Labs using hello Azure CLI</span></span>
<span data-ttu-id="58835-104">To szybki start przeprowadzi użytkownika przez proces tworzenia, uruchamiania, połączenie, aktualizowanie i czyszczenia komputera Programowanie w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="58835-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="58835-105">Przed rozpoczęciem:</span><span class="sxs-lookup"><span data-stu-id="58835-105">Before you begin:</span></span>

* <span data-ttu-id="58835-106">Jeśli laboratorium nie został utworzony, można znaleźć instrukcje [tutaj](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="58835-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="58835-107">[Zainstaluj interfejs wiersza polecenia 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="58835-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="58835-108">toostart, uruchom az toocreate logowania połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="58835-108">toostart, run az login toocreate a connection with Azure.</span></span> 

## <a name="create-and-verify-hello-virtual-machine"></a><span data-ttu-id="58835-109">Tworzenie i sprawdź hello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="58835-109">Create and verify hello virtual machine</span></span> 
<span data-ttu-id="58835-110">Utwórz maszynę Wirtualną z obrazu z witryny marketplace z ssh uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="58835-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="58835-111">Umieść hello **grupy zasobów w laboratorium** nazwie w hello — parametr grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="58835-111">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="58835-112">Toocreate Maszynę wirtualną przy użyciu formuły, należy użyć hello — parametr formuły w [tworzenia maszyny wirtualnej laboratorium az](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="58835-112">If you want toocreate a VM using a formula, use hello --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="58835-113">Sprawdź, czy ten hello maszyny Wirtualnej jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="58835-113">Verify that hello VM is available.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-toohello-virtual-machine"></a><span data-ttu-id="58835-114">Rozpoczęcie i połączenie toohello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="58835-114">Start and connect toohello virtual machine</span></span>
<span data-ttu-id="58835-115">Uruchom Maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="58835-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="58835-116">Umieść hello **grupy zasobów w laboratorium** nazwie w hello — parametr grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="58835-116">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="58835-117">Połącz tooa maszyny Wirtualnej: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) lub [pulpitu zdalnego](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="58835-117">Connect tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a><span data-ttu-id="58835-118">Maszyna wirtualna hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="58835-118">Update hello virtual machine</span></span>
<span data-ttu-id="58835-119">Zastosuj tooa artefaktów maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="58835-119">Apply artifacts tooa VM.</span></span>
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

<span data-ttu-id="58835-120">Lista dostępnych w laboratorium hello artefaktów.</span><span class="sxs-lookup"><span data-stu-id="58835-120">List artifacts available in hello lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a><span data-ttu-id="58835-121">Zatrzymaj i Usuń maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="58835-121">Stop and delete hello virtual machine</span></span>    
<span data-ttu-id="58835-122">Zatrzymaj Maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="58835-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="58835-123">Usuń Maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="58835-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]