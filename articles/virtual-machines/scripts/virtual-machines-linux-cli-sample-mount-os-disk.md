---
title: "Przykładowy skrypt interfejsu wiersza polecenia — dysk systemu operacyjnego instalacji aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="76799-103">Rozwiązywanie problemów z dyskiem systemu operacyjnego maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="76799-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="76799-104">Ten skrypt instaluje hello dysku systemu operacyjnego maszyny wirtualnej nie powiodło się lub problemem jako dane dysku tooa drugiej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="76799-104">This script mounts hello operating system disk of a failed or problematic virtual machine as a data disk tooa second virtual machine.</span></span> <span data-ttu-id="76799-105">Może to być przydatne podczas rozwiązywania problemów z dysku problemy lub odzyskiwania danych.</span><span class="sxs-lookup"><span data-stu-id="76799-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="76799-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="76799-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a><span data-ttu-id="76799-107">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="76799-107">Script explanation</span></span>

<span data-ttu-id="76799-108">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="76799-108">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="76799-109">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="76799-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="76799-110">Polecenie</span><span class="sxs-lookup"><span data-stu-id="76799-110">Command</span></span> | <span data-ttu-id="76799-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="76799-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="76799-112">Pokaż wirtualna az</span><span class="sxs-lookup"><span data-stu-id="76799-112">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="76799-113">Zwraca listę maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="76799-113">Return a list of virtual machines.</span></span> <span data-ttu-id="76799-114">W takim przypadku hello opcja zapytania jest dysk systemu operacyjnego maszyny wirtualnej hello tooreturn używane.</span><span class="sxs-lookup"><span data-stu-id="76799-114">In this case, hello query option is used tooreturn hello virtual machine operating system disk.</span></span> <span data-ttu-id="76799-115">Ta wartość jest następnie dodawana tooa nazwę zmiennej "uri".</span><span class="sxs-lookup"><span data-stu-id="76799-115">This value is then added tooa variable name ‘uri’.</span></span> |
| [<span data-ttu-id="76799-116">AZ usuwania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="76799-116">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="76799-117">Usuwa maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="76799-117">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="76799-118">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="76799-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="76799-119">Tworzy maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="76799-119">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="76799-120">Dołącz az dysku maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="76799-120">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="76799-121">Dołącza maszynę wirtualną tooa dysku.</span><span class="sxs-lookup"><span data-stu-id="76799-121">Attaches a disk tooa virtual machine.</span></span> |
| [<span data-ttu-id="76799-122">AZ vm--adresy ip</span><span class="sxs-lookup"><span data-stu-id="76799-122">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="76799-123">Zwraca hello adresów IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="76799-123">Returns hello IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="76799-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="76799-124">Next steps</span></span>

<span data-ttu-id="76799-125">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="76799-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="76799-126">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="76799-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
