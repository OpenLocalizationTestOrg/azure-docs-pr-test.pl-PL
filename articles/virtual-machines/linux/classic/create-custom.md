---
title: "Tworzenie klasycznej maszyny Wirtualnej systemu Linux przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć maszyny wirtualnej systemu Linux z 1.0 interfejsu wiersza polecenia platformy Azure przy użyciu klasycznego modelu wdrożenia"
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
ms.openlocfilehash: 8ddbacbbb70c0cf1a2537fab4d981a316610a4d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-classic-linux-vm-with-the-azure-cli-10"></a><span data-ttu-id="373fb-103">Tworzenie klasycznej maszyny Wirtualnej systemu Linux z Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="373fb-103">How to Create a Classic Linux VM with the Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="373fb-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="373fb-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="373fb-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="373fb-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="373fb-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="373fb-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="373fb-107">Wersja Menedżera zasobów dla [tutaj](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="373fb-107">For the Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="373fb-108">W tym temacie opisano sposób tworzenia maszyny wirtualnej systemu Linux (VM) z 1.0 interfejsu wiersza polecenia platformy Azure przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="373fb-108">This topic describes how to create a Linux virtual machine (VM) with the Azure CLI 1.0 using the Classic deployment model.</span></span> <span data-ttu-id="373fb-109">Używamy obrazu systemu Linux, spośród dostępnych **obrazów** na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="373fb-109">We use a Linux image from the available **IMAGES** on Azure.</span></span> <span data-ttu-id="373fb-110">Polecenia interfejsu wiersza polecenia platformy Azure w wersji 1.0 zapewniają następujące opcje konfiguracji, między innymi:</span><span class="sxs-lookup"><span data-stu-id="373fb-110">The Azure CLI 1.0 commands give the following configuration choices, among others:</span></span>

* <span data-ttu-id="373fb-111">Połączenie z maszyną Wirtualną do sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="373fb-111">Connecting the VM to a virtual network</span></span>
* <span data-ttu-id="373fb-112">Dodawanie maszyny Wirtualnej do istniejącej usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="373fb-112">Adding the VM to an existing cloud service</span></span>
* <span data-ttu-id="373fb-113">Dodawanie maszyny Wirtualnej do istniejącego konta magazynu</span><span class="sxs-lookup"><span data-stu-id="373fb-113">Adding the VM to an existing storage account</span></span>
* <span data-ttu-id="373fb-114">Dodawanie maszyny Wirtualnej do zestawu dostępności lub lokalizacji</span><span class="sxs-lookup"><span data-stu-id="373fb-114">Adding the VM to an availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="373fb-115">Jeśli chcesz użyć sieci wirtualnej do połączenia się do niego bezpośrednio przez hosta lub konfigurowanie połączeń między różnymi lokalizacjami maszyny Wirtualnej upewnij się, że sieci wirtualnej można określić podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="373fb-115">If you want your VM to use a virtual network so you can connect to it directly by hostname or set up cross-premises connections, make sure you specify the virtual network when you create the VM.</span></span> <span data-ttu-id="373fb-116">Maszyny Wirtualnej można skonfigurować do przyłączenia sieci wirtualnej wyłącznie w przypadku utworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="373fb-116">A VM can be configured to join a virtual network only when you create the VM.</span></span> <span data-ttu-id="373fb-117">Aby uzyskać szczegółowe informacje w sieciach wirtualnych, zobacz [omówienie sieci wirtualnych Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="373fb-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-to-create-a-linux-vm-using-the-classic-deployment-model"></a><span data-ttu-id="373fb-118">Tworzenie maszyny Wirtualnej systemu Linux przy użyciu klasycznego modelu wdrożenia</span><span class="sxs-lookup"><span data-stu-id="373fb-118">How to create a Linux VM using the Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

