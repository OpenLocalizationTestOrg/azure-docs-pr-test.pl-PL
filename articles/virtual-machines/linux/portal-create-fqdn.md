---
title: Nazwa FQDN maszyny Wirtualnej systemu Linux, w portalu Azure hello aaaCreate | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate w pełni kwalifikowana nazwa domeny lub nazwę FQDN dla Menedżera zasobów na podstawie maszyny wirtualnej w hello portalu Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a><span data-ttu-id="b2daf-103">Tworzenie w pełni kwalifikowaną nazwą domeny na powitania portalu Azure dla maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b2daf-103">Create a fully qualified domain name in hello Azure portal for a Linux VM</span></span>

<span data-ttu-id="b2daf-104">Po utworzeniu maszyny wirtualnej (VM) hello [portalu Azure](https://portal.azure.com), publicznego adresu IP zasobu hello maszyny wirtualnej jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b2daf-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="b2daf-105">Możesz użyć tego adresu IP adres tooremotely dostępu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b2daf-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="b2daf-106">Mimo że nie tworzy hello portal [pełną nazwę domeny](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), lub w pełni kwalifikowaną nazwę domeny, możesz dodać kategorię, po hello zostanie utworzona maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="b2daf-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once hello VM is created.</span></span> <span data-ttu-id="b2daf-107">W tym artykule przedstawiono hello kroki toocreate nazwy DNS lub nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="b2daf-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="b2daf-108">Utwórz nazwę FQDN</span><span class="sxs-lookup"><span data-stu-id="b2daf-108">Create a FQDN</span></span>
<span data-ttu-id="b2daf-109">W tym artykule przyjęto założenie, że utworzono już maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b2daf-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="b2daf-110">W razie potrzeby można [tworzenie maszyny Wirtualnej w portalu hello](quick-create-portal.md) lub [z hello Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b2daf-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with hello Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="b2daf-111">Po skonfigurowaniu i uruchomieniu maszyny Wirtualnej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b2daf-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="b2daf-112">Teraz można podłączyć zdalnie toohello maszyny Wirtualnej przy użyciu tego DNS nazwa takich jak z `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="b2daf-112">You can now connect remotely toohello VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2daf-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2daf-113">Next steps</span></span>
<span data-ttu-id="b2daf-114">Teraz, gdy maszyna wirtualna ma nazwę publicznego adresu IP i DNS, można wdrożyć wspólnej struktury aplikacji lub usług, takich jak nginx, bazy danych MongoDB, Docker, itp.</span><span class="sxs-lookup"><span data-stu-id="b2daf-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="b2daf-115">Można również uzyskać więcej informacji [za pomocą Menedżera zasobów](../../azure-resource-manager/resource-group-overview.md) porady na temat budowania Azure wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="b2daf-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

