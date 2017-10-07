---
title: "aaaCreate klasyczne maszyny Wirtualnej systemu Linux przy użyciu hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate maszyny wirtualnej systemu Linux przy użyciu hello Azure CLI 1.0 hello klasycznego modelu wdrożenia"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a><span data-ttu-id="aac1b-103">Jak tooCreate a klasyczne maszyny Wirtualnej systemu Linux z hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="aac1b-103">How tooCreate a Classic Linux VM with hello Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="aac1b-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="aac1b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="aac1b-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="aac1b-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="aac1b-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aac1b-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="aac1b-107">Wersja hello Menedżera zasobów dla [tutaj](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aac1b-107">For hello Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="aac1b-108">W tym temacie opisano, jak toocreate maszyny wirtualnej systemu Linux (VM) z hello Azure CLI 1.0 za pomocą hello klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="aac1b-108">This topic describes how toocreate a Linux virtual machine (VM) with hello Azure CLI 1.0 using hello Classic deployment model.</span></span> <span data-ttu-id="aac1b-109">Używamy obrazu systemu Linux, z hello dostępne **obrazów** na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="aac1b-109">We use a Linux image from hello available **IMAGES** on Azure.</span></span> <span data-ttu-id="aac1b-110">polecenia Hello Azure CLI 1.0 podać hello następujące opcje konfiguracji, między innymi:</span><span class="sxs-lookup"><span data-stu-id="aac1b-110">hello Azure CLI 1.0 commands give hello following configuration choices, among others:</span></span>

* <span data-ttu-id="aac1b-111">Łączenie sieci wirtualnej tooa hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="aac1b-111">Connecting hello VM tooa virtual network</span></span>
* <span data-ttu-id="aac1b-112">Dodawanie hello wirtualna tooan istniejącą usługę w chmurze</span><span class="sxs-lookup"><span data-stu-id="aac1b-112">Adding hello VM tooan existing cloud service</span></span>
* <span data-ttu-id="aac1b-113">Dodawanie hello wirtualna tooan istniejącego konta magazynu</span><span class="sxs-lookup"><span data-stu-id="aac1b-113">Adding hello VM tooan existing storage account</span></span>
* <span data-ttu-id="aac1b-114">Dodawanie zestawu dostępności tooan wirtualna hello lub lokalizacji</span><span class="sxs-lookup"><span data-stu-id="aac1b-114">Adding hello VM tooan availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aac1b-115">Jeśli chcesz toouse Twojego wirtualna sieć wirtualną do połączenia się tooit bezpośrednio przez hosta lub konfigurowanie połączeń między różnymi lokalizacjami, upewnij się, że hello sieci wirtualnej można określić podczas tworzenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="aac1b-115">If you want your VM toouse a virtual network so you can connect tooit directly by hostname or set up cross-premises connections, make sure you specify hello virtual network when you create hello VM.</span></span> <span data-ttu-id="aac1b-116">Maszyny Wirtualnej może być skonfigurowany toojoin sieci wirtualnej wyłącznie w przypadku utworzenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="aac1b-116">A VM can be configured toojoin a virtual network only when you create hello VM.</span></span> <span data-ttu-id="aac1b-117">Aby uzyskać szczegółowe informacje w sieciach wirtualnych, zobacz [omówienie sieci wirtualnych Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="aac1b-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a><span data-ttu-id="aac1b-118">Jak toocreate a maszyny Wirtualnej systemu Linux przy użyciu hello klasycznego modelu wdrożenia</span><span class="sxs-lookup"><span data-stu-id="aac1b-118">How toocreate a Linux VM using hello Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

