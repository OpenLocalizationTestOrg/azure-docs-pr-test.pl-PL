---
title: "Azure CLI przykładowym skrypcie - dysk systemu operacyjnego instalacji | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - instalacji dysk systemu operacyjnego"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b54a94d833644ebfae4c1fac59e4753ab723ced4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="d7a9b-103">Rozwiązywanie problemów z dyskiem systemu operacyjnego maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="d7a9b-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="d7a9b-104">Ten skrypt instaluje dysk systemu operacyjnego maszyny wirtualnej nie powiodło się lub problemem jako dysku danych do drugiej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d7a9b-104">This script mounts the operating system disk of a failed or problematic virtual machine as a data disk to a second virtual machine.</span></span> <span data-ttu-id="d7a9b-105">Może to być przydatne podczas rozwiązywania problemów z dysku problemy lub odzyskiwania danych.</span><span class="sxs-lookup"><span data-stu-id="d7a9b-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d7a9b-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d7a9b-106">Sample script</span></span>

<span data-ttu-id="d7a9b-107">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "szybkie tworzenie maszyn wirtualnych")]</span><span class="sxs-lookup"><span data-stu-id="d7a9b-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="d7a9b-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d7a9b-108">Script explanation</span></span>

<span data-ttu-id="d7a9b-109">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, maszyny wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="d7a9b-109">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d7a9b-110">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="d7a9b-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d7a9b-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d7a9b-111">Command</span></span> | <span data-ttu-id="d7a9b-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d7a9b-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d7a9b-113">Pokaż wirtualna az</span><span class="sxs-lookup"><span data-stu-id="d7a9b-113">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="d7a9b-114">Zwraca listę maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d7a9b-114">Return a list of virtual machines.</span></span> <span data-ttu-id="d7a9b-115">W takim przypadku opcji zapytania służy do zwracania dysku systemu operacyjnego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d7a9b-115">In this case, the query option is used to return the virtual machine operating system disk.</span></span> <span data-ttu-id="d7a9b-116">Ta wartość jest następnie dodawana do nazwy zmiennej "uri".</span><span class="sxs-lookup"><span data-stu-id="d7a9b-116">This value is then added to a variable name ‘uri’.</span></span> |
| [<span data-ttu-id="d7a9b-117">AZ usuwania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d7a9b-117">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="d7a9b-118">Usuwa maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="d7a9b-118">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="d7a9b-119">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="d7a9b-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d7a9b-120">Tworzy maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="d7a9b-120">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="d7a9b-121">Dołącz az dysku maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d7a9b-121">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="d7a9b-122">Dołącza dysk do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d7a9b-122">Attaches a disk to a virtual machine.</span></span> |
| [<span data-ttu-id="d7a9b-123">AZ vm--adresy ip</span><span class="sxs-lookup"><span data-stu-id="d7a9b-123">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="d7a9b-124">Zwraca adresów IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d7a9b-124">Returns the IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d7a9b-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d7a9b-125">Next steps</span></span>

<span data-ttu-id="d7a9b-126">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d7a9b-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d7a9b-127">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7a9b-127">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
