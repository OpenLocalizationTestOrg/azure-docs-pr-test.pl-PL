---
title: "Konfigurowanie punktów końcowych w klasycznym maszyny Wirtualnej systemu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się skonfigurować punktów końcowych dla maszyny Wirtualnej systemu Windows w klasycznym portalu Azure, aby umożliwić komunikację z maszyny wirtualnej systemu Windows na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 60861819a7e437bb715b14c0e8eaf74f13b33ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="1ee16-103">Jak skonfigurować punkty końcowe w klasycznym maszyny wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1ee16-103">How to set up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="1ee16-104">Wszystkie okna, które maszyn wirtualnych, które tworzenia na platformie Azure przy użyciu klasycznego modelu wdrażania można automatycznie komunikują się za pośrednictwem prywatnej kanał sieciowy między maszynami wirtualnymi w tej samej usługi w chmurze lub sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1ee16-104">All Windows virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="1ee16-105">Jednak komputery w Internecie lub innych sieci wirtualnych wymagają punktów końcowych, aby skierować ruch sieciowy przychodzący do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1ee16-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="1ee16-106">W tym artykule jest również dostępny do [maszyn wirtualnych systemu Linux](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="1ee16-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ee16-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1ee16-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1ee16-108">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="1ee16-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="1ee16-109">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1ee16-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="1ee16-110">W **Resource Manager** model wdrażania, punkty końcowe są skonfigurowane przy użyciu **grup zabezpieczeń sieci (NSG)**.</span><span class="sxs-lookup"><span data-stu-id="1ee16-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="1ee16-111">Aby uzyskać więcej informacji, zobacz [dostęp do zewnętrznych sieci maszyny Wirtualnej przy użyciu portalu Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1ee16-111">For more information, see [Allow external access to your VM using the Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="1ee16-112">Po utworzeniu maszyny wirtualnej systemu Windows w portalu Azure, typowe punkty końcowe, takich jak te dotyczące usług pulpitu zdalnego i komunikacji zdalnej programu Windows PowerShell są zazwyczaj tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="1ee16-112">When you create a Windows virtual machine in the Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="1ee16-113">Dodatkowe punkty końcowe można skonfigurować podczas tworzenia maszyny wirtualnej lub po jego zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="1ee16-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="1ee16-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1ee16-114">Next steps</span></span>
* <span data-ttu-id="1ee16-115">Aby użyć polecenia cmdlet programu Azure PowerShell do konfigurowania punktu końcowego maszyny Wirtualnej, zobacz [AzureEndpoint Dodaj](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ee16-115">To use an Azure PowerShell cmdlet to set up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="1ee16-116">Aby użyć polecenia cmdlet programu Azure PowerShell do zarządzania listy ACL punktu końcowego, zobacz [Zarządzanie listy kontroli dostępu (ACL) dla punktów końcowych przy użyciu programu PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1ee16-116">To use an Azure PowerShell cmdlet to manage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="1ee16-117">Jeśli utworzono maszynę wirtualną w modelu wdrażania usługi Resource Manager, możesz użyć programu Azure PowerShell do [Utwórz grupy zabezpieczeń sieci](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) sterujących ruchem do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1ee16-117">If you created a virtual machine in the Resource Manager deployment model, you can use Azure PowerShell to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) to control traffic to the VM.</span></span>
