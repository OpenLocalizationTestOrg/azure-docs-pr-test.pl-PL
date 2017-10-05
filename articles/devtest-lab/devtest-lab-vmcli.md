---
title: "Tworzenie i zarządzanie maszynami wirtualnymi w usłudze DevTest Labs z wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure DevTest Labs umożliwia tworzenie i zarządzanie maszynami wirtualnymi Azure CLI 2.0"
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
ms.openlocfilehash: 42b0448c1bcdfa909715abd5075353d63cab8389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-the-azure-cli"></a><span data-ttu-id="fdd2b-103">Tworzenie i zarządzanie maszynami wirtualnymi z DevTest Labs przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fdd2b-103">Create and manage virtual machines with DevTest Labs using the Azure CLI</span></span>
<span data-ttu-id="fdd2b-104">To szybki start przeprowadzi użytkownika przez proces tworzenia, uruchamiania, połączenie, aktualizowanie i czyszczenia komputera Programowanie w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="fdd2b-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="fdd2b-105">Przed rozpoczęciem:</span><span class="sxs-lookup"><span data-stu-id="fdd2b-105">Before you begin:</span></span>

* <span data-ttu-id="fdd2b-106">Jeśli laboratorium nie został utworzony, można znaleźć instrukcje [tutaj](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="fdd2b-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="fdd2b-107">[Zainstaluj interfejs wiersza polecenia 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fdd2b-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="fdd2b-108">Aby rozpocząć, uruchom az logowania, aby utworzyć połączenie z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="fdd2b-108">To start, run az login to create a connection with Azure.</span></span> 

## <a name="create-and-verify-the-virtual-machine"></a><span data-ttu-id="fdd2b-109">Tworzenie i sprawdź maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fdd2b-109">Create and verify the virtual machine</span></span> 
<span data-ttu-id="fdd2b-110">Utwórz maszynę Wirtualną z obrazu z witryny marketplace z ssh uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="fdd2b-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="fdd2b-111">Umieść **grupy zasobów w laboratorium** nazwę w parametrze--grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="fdd2b-111">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="fdd2b-112">Jeśli chcesz utworzyć Maszynę wirtualną przy użyciu formuły, użyj formuły parametru w [tworzenia maszyny wirtualnej laboratorium az](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fdd2b-112">If you want to create a VM using a formula, use the --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="fdd2b-113">Sprawdź, czy maszyna wirtualna jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="fdd2b-113">Verify that the VM is available.</span></span>
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

## <a name="start-and-connect-to-the-virtual-machine"></a><span data-ttu-id="fdd2b-114">Rozpoczęcie i połączenie z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="fdd2b-114">Start and connect to the virtual machine</span></span>
<span data-ttu-id="fdd2b-115">Uruchom Maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="fdd2b-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="fdd2b-116">Umieść **grupy zasobów w laboratorium** nazwę w parametrze--grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="fdd2b-116">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="fdd2b-117">Połączenie z maszyną wirtualną: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) lub [pulpitu zdalnego](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="fdd2b-117">Connect to a VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-the-virtual-machine"></a><span data-ttu-id="fdd2b-118">Zaktualizuj maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="fdd2b-118">Update the virtual machine</span></span>
<span data-ttu-id="fdd2b-119">Zastosuj artefakty do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fdd2b-119">Apply artifacts to a VM.</span></span>
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

<span data-ttu-id="fdd2b-120">Na liście artefaktów związanych dostępne w środowisku laboratoryjnym.</span><span class="sxs-lookup"><span data-stu-id="fdd2b-120">List artifacts available in the lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-the-virtual-machine"></a><span data-ttu-id="fdd2b-121">Zatrzymaj i Usuń maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="fdd2b-121">Stop and delete the virtual machine</span></span>    
<span data-ttu-id="fdd2b-122">Zatrzymaj Maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="fdd2b-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="fdd2b-123">Usuń Maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="fdd2b-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]