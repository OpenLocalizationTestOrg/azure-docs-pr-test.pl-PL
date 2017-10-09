---
title: "aaaSet się punkty końcowe w klasycznym maszyny Wirtualnej systemu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooset się punktów końcowych dla maszyny Wirtualnej systemu Windows w hello Azure classic portal tooallow komunikację z maszyną wirtualną systemu Windows na platformie Azure."
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
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="f7030-103">Jak tooset się punkty końcowe w klasycznym maszyny wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f7030-103">How tooset up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="f7030-104">Wszystkich maszyn wirtualnych tworzonych na platformie Azure przy użyciu hello klasycznego modelu wdrażania można automatycznie komunikują się za pośrednictwem kanału między maszynami wirtualnymi w sieci prywatnej systemu Windows hello tej samej usługi w chmurze lub sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f7030-104">All Windows virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="f7030-105">Jednak komputery na powitania Internet lub innych sieci wirtualnych wymagają punkty końcowe toodirect hello ruchu przychodzącego ruchu tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f7030-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="f7030-106">W tym artykule jest również dostępny do [maszyn wirtualnych systemu Linux](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="f7030-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7030-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f7030-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f7030-108">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="f7030-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f7030-109">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f7030-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="f7030-110">W hello **Resource Manager** model wdrażania, punkty końcowe są skonfigurowane przy użyciu **grup zabezpieczeń sieci (NSG)**.</span><span class="sxs-lookup"><span data-stu-id="f7030-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="f7030-111">Aby uzyskać więcej informacji, zobacz [Zezwalaj dostępu zewnętrznego tooyour maszynę Wirtualną przy użyciu hello portalu Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7030-111">For more information, see [Allow external access tooyour VM using hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f7030-112">Po utworzeniu maszyny wirtualnej systemu Windows w portalu Azure hello typowych punktów końcowych, takich jak te dotyczące usług pulpitu zdalnego i komunikacji zdalnej programu Windows PowerShell są zazwyczaj tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="f7030-112">When you create a Windows virtual machine in hello Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="f7030-113">Podczas tworzenia maszyny wirtualnej hello lub później w razie potrzeby można skonfigurować dodatkowe punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="f7030-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="f7030-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7030-114">Next steps</span></span>
* <span data-ttu-id="f7030-115">toouse tooset polecenia cmdlet programu Azure PowerShell się punkt końcowy maszyny Wirtualnej, zobacz [AzureEndpoint Dodaj](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="f7030-115">toouse an Azure PowerShell cmdlet tooset up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="f7030-116">toouse toomanage polecenia cmdlet programu Azure PowerShell listy ACL punktu końcowego, zobacz [Zarządzanie listy kontroli dostępu (ACL) dla punktów końcowych przy użyciu programu PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f7030-116">toouse an Azure PowerShell cmdlet toomanage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="f7030-117">Jeśli utworzono maszynę wirtualną w modelu wdrażania usługi Resource Manager hello, możesz użyć programu Azure PowerShell zbyt[Utwórz grupy zabezpieczeń sieci](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol toohello ruch maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f7030-117">If you created a virtual machine in hello Resource Manager deployment model, you can use Azure PowerShell too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffic toohello VM.</span></span>
