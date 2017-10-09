---
title: "aaaSet się punkty końcowe w klasycznym maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooset się punktów końcowych dla maszyny Wirtualnej systemu Linux w hello Azure classic portal tooallow komunikacji z maszyny wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="5d9ba-103">Jak tooset się punkty końcowe w klasycznym maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5d9ba-103">How tooset up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="5d9ba-104">Wszystkie maszyny wirtualne systemu Linux utworzone na platformie Azure przy użyciu hello klasycznego modelu wdrażania może komunikować się automatycznie kanałem sieci prywatnej innym maszynom wirtualnym w hello się, że takie same w chmurze, usługi lub wirtualnych sieci.</span><span class="sxs-lookup"><span data-stu-id="5d9ba-104">All Linux virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="5d9ba-105">Jednak komputery na powitania Internet lub innych sieci wirtualnych wymagają punkty końcowe toodirect hello ruchu przychodzącego ruchu tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5d9ba-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="5d9ba-106">W tym artykule jest również dostępny do [maszyn wirtualnych Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d9ba-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d9ba-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5d9ba-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5d9ba-108">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="5d9ba-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="5d9ba-109">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5d9ba-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="5d9ba-110">W hello **Resource Manager** model wdrażania, punkty końcowe są skonfigurowane przy użyciu **grup zabezpieczeń sieci (NSG)**.</span><span class="sxs-lookup"><span data-stu-id="5d9ba-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="5d9ba-111">Aby uzyskać więcej informacji, zobacz [Otwieranie portów i punkty końcowe](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d9ba-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="5d9ba-112">Po utworzeniu maszyny wirtualnej systemu Linux w portalu Azure hello punkt końcowy dla protokołu Secure Shell (SSH) jest zwykle tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="5d9ba-112">When you create a Linux virtual machine in hello Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="5d9ba-113">Podczas tworzenia maszyny wirtualnej hello lub później w razie potrzeby można skonfigurować dodatkowe punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="5d9ba-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="5d9ba-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d9ba-114">Next steps</span></span>
* <span data-ttu-id="5d9ba-115">Punkt końcowy maszyny Wirtualnej można również utworzyć za pomocą hello [interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="5d9ba-115">You can also create a VM endpoint by using hello [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="5d9ba-116">Uruchom hello **utworzyć punktu końcowego maszyny wirtualnej azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="5d9ba-116">Run hello **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="5d9ba-117">Jeśli utworzono maszynę wirtualną w modelu wdrażania usługi Resource Manager hello hello wiersza polecenia platformy Azure w trybie Menedżera zasobów można użyć zbyt[Utwórz grupy zabezpieczeń sieci](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol toohello ruch maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5d9ba-117">If you created a virtual machine in hello Resource Manager deployment model, you can use hello Azure CLI in Resource Manager mode too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffic toohello VM.</span></span>
