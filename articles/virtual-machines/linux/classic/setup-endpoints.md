---
title: "Konfigurowanie punktów końcowych w klasycznym maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować punktów końcowych dla maszyny Wirtualnej systemu Linux w klasycznym portalu Azure, aby umożliwić komunikację z maszyny wirtualnej systemu Linux na platformie Azure"
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
ms.openlocfilehash: 4fd8b847b0f60648d1661ce5a8667c641e616ed4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="7bacf-103">Jak skonfigurować punkty końcowe w klasycznym maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="7bacf-103">How to set up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="7bacf-104">Wszystkie maszyny wirtualne systemu Linux utworzone na platformie Azure przy użyciu klasycznego modelu wdrażania można automatycznie komunikują się za pośrednictwem kanału między maszynami wirtualnymi w tej samej usługi w chmurze lub sieci wirtualnej sieci prywatnej.</span><span class="sxs-lookup"><span data-stu-id="7bacf-104">All Linux virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="7bacf-105">Jednak komputery w Internecie lub innych sieci wirtualnych wymagają punktów końcowych, aby skierować ruch sieciowy przychodzący do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7bacf-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="7bacf-106">W tym artykule jest również dostępny do [maszyn wirtualnych Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7bacf-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7bacf-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7bacf-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7bacf-108">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="7bacf-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7bacf-109">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7bacf-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="7bacf-110">W **Resource Manager** model wdrażania, punkty końcowe są skonfigurowane przy użyciu **grup zabezpieczeń sieci (NSG)**.</span><span class="sxs-lookup"><span data-stu-id="7bacf-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="7bacf-111">Aby uzyskać więcej informacji, zobacz [Otwieranie portów i punkty końcowe](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7bacf-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7bacf-112">Po utworzeniu maszyny wirtualnej systemu Linux w portalu Azure, punkt końcowy dla protokołu Secure Shell (SSH) jest zwykle tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="7bacf-112">When you create a Linux virtual machine in the Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="7bacf-113">Dodatkowe punkty końcowe można skonfigurować podczas tworzenia maszyny wirtualnej lub po jego zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="7bacf-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="7bacf-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7bacf-114">Next steps</span></span>
* <span data-ttu-id="7bacf-115">Punkt końcowy maszyny Wirtualnej można również utworzyć za pomocą [interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="7bacf-115">You can also create a VM endpoint by using the [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="7bacf-116">Uruchom **utworzyć punktu końcowego maszyny wirtualnej azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="7bacf-116">Run the **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="7bacf-117">Jeśli utworzono maszynę wirtualną w modelu wdrażania usługi Resource Manager, można użyć wiersza polecenia platformy Azure w trybie Menedżera zasobów, aby [Utwórz grupy zabezpieczeń sieci](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) sterujących ruchem do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7bacf-117">If you created a virtual machine in the Resource Manager deployment model, you can use the Azure CLI in Resource Manager mode to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) to control traffic to the VM.</span></span>
