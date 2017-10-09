---
title: "kod zarządzany platformy Azure na dysku dla kopii zapasowej aaaCopy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate kopię toouse Azure zarządzanych dysku dla dysku z powrotem się lub rozwiązywania problemów problemy."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="4c801-103">Utwórz kopię plik VHD przechowywany jako dysk zarządzane Azure przy użyciu migawek zarządzane</span><span class="sxs-lookup"><span data-stu-id="4c801-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="4c801-104">Migawki zarządzane dysku do utworzenia kopii zapasowej lub tworzenie dysku zarządzanego z migawki hello i dołącz je tooa test maszyny wirtualnej tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="4c801-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="4c801-105">Zarządzane migawki jest kopią pełnej w momencie zarządzane dysku maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4c801-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="4c801-106">Tworzy kopię tylko do odczytu z wirtualnego dysku twardego i, domyślnie zapisuje go jako dysk standardowy zarządzane.</span><span class="sxs-lookup"><span data-stu-id="4c801-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="4c801-107">Aby uzyskać informacje o cenach, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="4c801-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link tootopic or blog post that explains managed disks. -->

<span data-ttu-id="4c801-108">Użyj albo hello Azure portalu lub hello Azure CLI 2.0 tootake migawkę hello dysku zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="4c801-108">Use either hello Azure portal or hello Azure CLI 2.0 tootake a snapshot of hello Managed Disk.</span></span>

## <a name="use-azure-cli-20-tootake-a-snapshot"></a><span data-ttu-id="4c801-109">Użyj tootake Azure CLI 2.0 migawki</span><span class="sxs-lookup"><span data-stu-id="4c801-109">Use Azure CLI 2.0 tootake a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="4c801-110">Witaj poniższy przykład wymaga hello Azure CLI 2.0 zainstalowany, a zalogowany do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4c801-110">hello following example requires hello Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="4c801-111">Witaj poniższej procedurze pokazano, jak tooobtain i wykonaj migawkę zarządzanych systemu operacyjnego na dysku za pomocą hello `az snapshot create` z hello `--source-disk` parametru.</span><span class="sxs-lookup"><span data-stu-id="4c801-111">hello following steps show how tooobtain and take a snapshot of a managed OS disk using hello `az snapshot create` command with hello `--source-disk` parameter.</span></span> <span data-ttu-id="4c801-112">Hello poniższym przykładzie założono, że istnieje maszyna wirtualna o nazwie `myVM` utworzone za pomocą zarządzanego dysku systemu operacyjnego w hello `myResourceGroup` grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4c801-112">hello following example assumes that there is a VM called `myVM` created with a managed OS disk in hello `myResourceGroup` resource group.</span></span>

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="4c801-113">dane wyjściowe Hello powinny wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="4c801-113">hello output should look something like:</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="4c801-114">Użyj tootake portalu Azure migawki</span><span class="sxs-lookup"><span data-stu-id="4c801-114">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="4c801-115">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c801-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4c801-116">Począwszy od lewej górnej powitania kliknij **nowy** i wyszukaj **migawki**.</span><span class="sxs-lookup"><span data-stu-id="4c801-116">Starting in hello upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="4c801-117">W bloku migawki powitania kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4c801-117">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="4c801-118">Wprowadź **nazwa** hello migawki.</span><span class="sxs-lookup"><span data-stu-id="4c801-118">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="4c801-119">Wybierz istniejący [grupy zasobów](../../azure-resource-manager/resource-group-overview.md#resource-groups) lub nazwa typu hello nowej.</span><span class="sxs-lookup"><span data-stu-id="4c801-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="4c801-120">Wybierz centrum danych Azure lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="4c801-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="4c801-121">Aby uzyskać **dysku źródłowego**, wybierz hello toosnapshot dysku zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="4c801-121">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="4c801-122">Wybierz hello **typ konta** toouse toostore hello migawki.</span><span class="sxs-lookup"><span data-stu-id="4c801-122">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="4c801-123">Firma Microsoft zaleca **Standard_LRS** chyba że ma być przechowywane na dysku wysokiej wydajności.</span><span class="sxs-lookup"><span data-stu-id="4c801-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="4c801-124">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4c801-124">Click **Create**.</span></span>

<span data-ttu-id="4c801-125">Jeśli planujesz toouse hello migawki toocreate dysku zarządzanego dołączyć maszynę Wirtualną, która wymaga wydajnych toobe, użyj parametru hello `--sku Premium_LRS` z hello `az snapshot create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="4c801-125">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `--sku Premium_LRS` with hello `az snapshot create` command.</span></span> <span data-ttu-id="4c801-126">Spowoduje to utworzenie migawki hello tak, aby była przechowywana jako dysk zarządzane Premium.</span><span class="sxs-lookup"><span data-stu-id="4c801-126">This creates hello snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="4c801-127">Dysków zarządzanych w warstwie Premium działać lepiej, ponieważ są dysków półprzewodnikowych (SSD), ale są droższe niż dyski standardowe (HDD).</span><span class="sxs-lookup"><span data-stu-id="4c801-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


