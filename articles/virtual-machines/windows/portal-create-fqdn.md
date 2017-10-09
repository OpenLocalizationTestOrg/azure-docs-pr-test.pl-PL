---
title: Nazwa FQDN maszyny Wirtualnej systemu Windows, w portalu Azure hello aaaCreate | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate w pełni kwalifikowana nazwa domeny lub nazwę FQDN dla Menedżera zasobów na podstawie maszyny wirtualnej w hello portalu Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a><span data-ttu-id="063ee-103">Tworzenie w pełni kwalifikowaną nazwą domeny na powitania portalu Azure dla maszyny Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="063ee-103">Create a fully qualified domain name in hello Azure portal for a Windows VM</span></span>

<span data-ttu-id="063ee-104">Po utworzeniu maszyny wirtualnej (VM) hello [portalu Azure](https://portal.azure.com), publicznego adresu IP zasobu hello maszyny wirtualnej jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="063ee-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="063ee-105">Możesz użyć tego adresu IP adres tooremotely dostępu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="063ee-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="063ee-106">Mimo że nie tworzy hello portal [pełną nazwę domeny](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), lub nazwę FQDN, możesz ją utworzyć utworzone hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="063ee-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once hello VM is created.</span></span> <span data-ttu-id="063ee-107">W tym artykule przedstawiono hello kroki toocreate nazwy DNS lub nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="063ee-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="063ee-108">Utwórz nazwę FQDN</span><span class="sxs-lookup"><span data-stu-id="063ee-108">Create a FQDN</span></span>
<span data-ttu-id="063ee-109">W tym artykule przyjęto założenie, że utworzono już maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="063ee-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="063ee-110">W razie potrzeby można [tworzenie maszyny Wirtualnej w portalu hello](quick-create-portal.md) lub [przy użyciu programu Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="063ee-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="063ee-111">Po skonfigurowaniu i uruchomieniu maszyny Wirtualnej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="063ee-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="063ee-112">Teraz można podłączyć zdalnie toohello maszyny Wirtualnej przy użyciu tej nazwy DNS takich jak dla protokołu RDP (Remote Desktop).</span><span class="sxs-lookup"><span data-stu-id="063ee-112">You can now connect remotely toohello VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="063ee-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="063ee-113">Next steps</span></span>
<span data-ttu-id="063ee-114">Teraz, gdy maszyna wirtualna ma nazwę publicznego adresu IP i DNS, można wdrożyć wspólnej struktury aplikacji lub usług, takich jak IIS, SQL i programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="063ee-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="063ee-115">Można również uzyskać więcej informacji [za pomocą Menedżera zasobów](../../azure-resource-manager/resource-group-overview.md) porady na temat budowania Azure wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="063ee-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

