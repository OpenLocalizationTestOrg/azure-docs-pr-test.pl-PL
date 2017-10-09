---
title: aaaRedeploy maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Jak problemy z maszyn wirtualnych systemu Linux tooredeploy w Azure toomitigate połączenia SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a><span data-ttu-id="9c02d-103">Należy ponownie wdrożyć toonew maszyny wirtualnej systemu Linux platformy Azure węzła</span><span class="sxs-lookup"><span data-stu-id="9c02d-103">Redeploy Linux virtual machine toonew Azure node</span></span>
<span data-ttu-id="9c02d-104">Ponowne rozmieszczanie hello maszyny Wirtualnej może pomóc w pokonywaniu trudności Rozwiązywanie problemów z SSH lub aplikacja dostęp do maszyny wirtualnej systemu Linux tooa (VM) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9c02d-104">If you face difficulties troubleshooting SSH or application access tooa Linux virtual machine (VM) in Azure, redeploying hello VM may help.</span></span> <span data-ttu-id="9c02d-105">Podczas ponownego wdrażania maszyny Wirtualnej przenosi do nowego węzła tooa hello maszyny Wirtualnej w ramach hello infrastruktury platformy Azure i uprawnień go ponownie.</span><span class="sxs-lookup"><span data-stu-id="9c02d-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="9c02d-106">Opcje konfiguracji i skojarzonych zasobów są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="9c02d-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="9c02d-107">W tym artykule opisano sposób tooredeploy a maszyny Wirtualnej przy użyciu wiersza polecenia platformy Azure lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c02d-107">This article shows you how tooredeploy a VM using Azure CLI or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="9c02d-108">Po ponownego wdrażania maszyny Wirtualnej, dysku tymczasowym hello zostaną utracone i dynamicznych adresów IP skojarzonych z interfejsu sieci wirtualnej zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="9c02d-108">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="9c02d-109">Można wdrożyć ponownie Maszynę wirtualną przy użyciu jednej z hello następujące opcje.</span><span class="sxs-lookup"><span data-stu-id="9c02d-109">You can redeploy a VM using one of hello following options.</span></span> <span data-ttu-id="9c02d-110">Wystarczy tylko jeden tooredeploy opcji toochoose maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="9c02d-110">You only need toochoose one option tooredeploy your VM:</span></span>

- [<span data-ttu-id="9c02d-111">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9c02d-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="9c02d-112">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9c02d-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="9c02d-113">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9c02d-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="9c02d-114">Użyj hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9c02d-114">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="9c02d-115">Najnowsza wersja hello instalacji [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="9c02d-115">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="9c02d-116">Wdrożenie maszyny Wirtualnej z [ponownego wdrażania maszyny wirtualnej az](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="9c02d-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="9c02d-117">powitania po wdraża ponownie przykład Witaj maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9c02d-117">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="9c02d-118">Użyj hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="9c02d-118">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="9c02d-119">Zainstaluj hello [najnowsze Azure CLI 1.0](../../cli-install-nodejs.md), zaloguj się za tooan konto platformy Azure i upewnij się, że jesteś w trybie Menedżera zasobów (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="9c02d-119">Install hello [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in tooan Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="9c02d-120">powitania po wdraża ponownie przykład Witaj maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9c02d-120">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="9c02d-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9c02d-121">Next steps</span></span>
<span data-ttu-id="9c02d-122">Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, można znaleźć pomoc w [Rozwiązywanie problemów z połączeniami SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [szczegółowe kroki rozwiązywania problemów SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9c02d-122">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9c02d-123">Jeśli nie można uzyskać dostęp do aplikacji działających na maszynie Wirtualnej, możesz przeczytać [aplikacji Rozwiązywanie problemów z](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9c02d-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

