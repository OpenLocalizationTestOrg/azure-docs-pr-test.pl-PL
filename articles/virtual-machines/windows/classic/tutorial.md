---
title: aaaCreate maszyny Wirtualnej w portalu Azure hello | Dokumentacja firmy Microsoft
description: "Utwórz maszynę wirtualną systemu Windows w hello portalu Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a><span data-ttu-id="abd2d-103">Utwórz maszynę wirtualną z systemem Windows w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="abd2d-103">Create a virtual machine running Windows in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="abd2d-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="abd2d-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="abd2d-105">Środowiska PowerShell: Wdrożenia klasycznego</span><span class="sxs-lookup"><span data-stu-id="abd2d-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="abd2d-106">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="abd2d-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="abd2d-107">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="abd2d-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="abd2d-108">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="abd2d-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="abd2d-109">Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu wdrażania usługi Resource Manager hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przy użyciu hello **portalu Azure**.</span><span class="sxs-lookup"><span data-stu-id="abd2d-109">Learn how too[perform these steps using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using hello **Azure portal**.</span></span>

<span data-ttu-id="abd2d-110">W tym samouczku przedstawiono sposób toocreate Azure maszyny wirtualnej (VM) z systemem Windows w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="abd2d-110">This tutorial shows you how toocreate an Azure virtual machine (VM) running Windows in hello Azure portal.</span></span> <span data-ttu-id="abd2d-111">Na przykład użyjemy obrazu systemu Windows Server, ale jest to tylko jeden z hello wiele obrazów oferty Azure.</span><span class="sxs-lookup"><span data-stu-id="abd2d-111">We'll use a Windows Server image as an example, but that's just one of hello many images Azure offers.</span></span> <span data-ttu-id="abd2d-112">Należy pamiętać, że obrazy dostępne do wyboru zależą subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="abd2d-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="abd2d-113">Na przykład obrazy pulpitu systemu Windows mogą być dostępne tooMSDN subskrybentów.</span><span class="sxs-lookup"><span data-stu-id="abd2d-113">For example, Windows desktop images may be available tooMSDN subscribers.</span></span>

<span data-ttu-id="abd2d-114">W tej sekcji opisano sposób toouse hello **pulpitu nawigacyjnego** w hello tooselect portalu Azure, a następnie utwórz hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="abd2d-114">This section shows you how toouse hello **Dashboard** in hello Azure portal tooselect and then create hello virtual machine.</span></span>

<span data-ttu-id="abd2d-115">Można również tworzyć maszyny wirtualne przy użyciu [własnych obrazów](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="abd2d-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="abd2d-116">toolearn dotyczących tego i innych metod, zobacz [toocreate różne sposoby maszyny wirtualnej systemu Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="abd2d-116">toolearn about this and other methods, see [Different ways toocreate a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <span data-ttu-id="abd2d-117"><a id="createvirtualmachine"></a>Utworzyć hello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="abd2d-117"><a id="createvirtualmachine"> </a>Create hello virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="abd2d-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="abd2d-118">Next steps</span></span>
* <span data-ttu-id="abd2d-119">Dowiedz się, jak za[utworzyć Maszynę wirtualną przy użyciu modelu wdrażania usługi Resource Manager hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="abd2d-119">Learn how too[create a VM using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure portal.</span></span>
* <span data-ttu-id="abd2d-120">Zaloguj się na toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="abd2d-120">Log on toohello virtual machine.</span></span> <span data-ttu-id="abd2d-121">Aby uzyskać instrukcje, zobacz [logowania tooa maszyny wirtualnej z systemem Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="abd2d-121">For instructions, see [Log on tooa virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="abd2d-122">Dołącz dane toostore dysku.</span><span class="sxs-lookup"><span data-stu-id="abd2d-122">Attach a disk toostore data.</span></span> <span data-ttu-id="abd2d-123">Możesz dołączyć zarówno puste dyski i dyski, które zawierają dane.</span><span class="sxs-lookup"><span data-stu-id="abd2d-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="abd2d-124">Aby uzyskać instrukcje, zobacz hello [dołączanie danych dysku tooa systemu Windows maszyny wirtualnej utworzonej z hello klasycznego modelu wdrażania](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="abd2d-124">For instructions, see hello [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](attach-disk.md).</span></span>
