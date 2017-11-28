---
title: "Utwórz nazwę FQDN dla maszyny Wirtualnej systemu Windows, w portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć w pełni kwalifikowaną nazwę domeny lub nazwę FQDN dla Menedżera zasobów na podstawie maszyny wirtualnej w portalu Azure."
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
ms.openlocfilehash: 2d5a555cd873222efcdb29e8eb3aaf128a24414b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-windows-vm"></a><span data-ttu-id="a8798-103">Utwórz w pełni kwalifikowaną nazwą domeny w portalu Azure dla maszyny Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a8798-103">Create a fully qualified domain name in the Azure portal for a Windows VM</span></span>

<span data-ttu-id="a8798-104">Po utworzeniu maszyny wirtualnej (VM) w [portalu Azure](https://portal.azure.com), zasób publicznego adresu IP dla maszyny wirtualnej jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="a8798-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="a8798-105">Ten adres IP umożliwia zdalny dostęp do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8798-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="a8798-106">Mimo że nie tworzy portalu [pełną nazwę domeny](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), lub w pełni kwalifikowaną nazwę domeny, można utworzyć po utworzeniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8798-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once the VM is created.</span></span> <span data-ttu-id="a8798-107">W tym artykule przedstawiono kroki, aby utworzyć nazwę DNS lub nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="a8798-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="a8798-108">Utwórz nazwę FQDN</span><span class="sxs-lookup"><span data-stu-id="a8798-108">Create a FQDN</span></span>
<span data-ttu-id="a8798-109">W tym artykule przyjęto założenie, że utworzono już maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8798-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="a8798-110">W razie potrzeby można [tworzenie maszyny Wirtualnej w portalu](quick-create-portal.md) lub [przy użyciu programu Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a8798-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="a8798-111">Po skonfigurowaniu i uruchomieniu maszyny Wirtualnej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a8798-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="a8798-112">Teraz można podłączyć zdalnego do maszyny Wirtualnej przy użyciu tej nazwy DNS takich jak dla protokołu RDP (Remote Desktop).</span><span class="sxs-lookup"><span data-stu-id="a8798-112">You can now connect remotely to the VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8798-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a8798-113">Next steps</span></span>
<span data-ttu-id="a8798-114">Teraz, gdy maszyna wirtualna ma nazwę publicznego adresu IP i DNS, można wdrożyć wspólnej struktury aplikacji lub usług, takich jak IIS, SQL i programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a8798-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="a8798-115">Można również uzyskać więcej informacji [za pomocą Menedżera zasobów](../../azure-resource-manager/resource-group-overview.md) porady na temat budowania Azure wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="a8798-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

