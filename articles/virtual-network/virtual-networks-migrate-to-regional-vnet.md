---
title: "aaaMigrate sieci wirtualnej platformy Azure (klasyczną) z grupą koligacji regionu tooa | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomigrate sieci wirtualnej (wdrożenia klasyczne) z koligacji grupy tooa regionu."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a><span data-ttu-id="c6d9c-103">Migracja sieci wirtualnej (klasyczne) z regionu tooa grupy koligacji</span><span class="sxs-lookup"><span data-stu-id="c6d9c-103">Migrate a virtual network (classic) from an affinity group tooa region</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6d9c-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6d9c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="c6d9c-105">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="c6d9c-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="c6d9c-107">Grupy koligacji upewnij się, że zasoby są tworzone w ramach tej samej grupie koligacji fizycznie są obsługiwane przez serwery, które są blisko siebie włączenie tych zasobów toocommunicate szybsze hello.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-107">Affinity groups ensure that resources created within hello same affinity group are physically hosted by servers that are close together, enabling these resources toocommunicate quicker.</span></span> <span data-ttu-id="c6d9c-108">W ciągu ostatnich hello grupy koligacji były wymagane do tworzenia sieci wirtualnych (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="c6d9c-108">In hello past, affinity groups were a requirement for creating virtual networks (classic).</span></span> <span data-ttu-id="c6d9c-109">W tym czasie hello usługi Menedżera sieci, zarządzaną sieciami wirtualnymi (klasyczne) może pracować tylko w ramach zestawu serwerów fizycznych lub jednostki skalowania.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-109">At that time, hello network manager service that managed virtual networks (classic) could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="c6d9c-110">Ulepszenia architektury nastąpiło nasilenie zakresu hello sieci zarządzania tooa regionu.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-110">Architectural improvements have increased hello scope of network management tooa region.</span></span>

<span data-ttu-id="c6d9c-111">W wyniku tych usprawnień architektury grup koligacji nie jest już zalecane lub wymagane dla sieci wirtualnych (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="c6d9c-111">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks (classic).</span></span> <span data-ttu-id="c6d9c-112">Użyj Hello grup koligacji dla sieci wirtualnych (klasyczne) zastępuje regionów.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-112">hello use of affinity groups for virtual networks (classic) is replaced by regions.</span></span> <span data-ttu-id="c6d9c-113">Sieci wirtualne (klasyczne) skojarzonych z regiony są nazywane regionalnych sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-113">Virtual networks (classic) that are associated with regions are called regional virtual networks.</span></span>

<span data-ttu-id="c6d9c-114">Zaleca się, że grupy koligacji nie używaj ogólnie.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-114">We recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="c6d9c-115">Oprócz wymagań sieci wirtualnej hello grupy koligacji były również ważne toouse tooensure zasoby, takie jak zasobów obliczeniowych (klasyczne) i magazynu (klasyczne), zostały umieszczone obok siebie.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-115">Aside from hello virtual network requirement, affinity groups were also important toouse tooensure resources, such as compute (classic) and storage (classic), were placed near each other.</span></span> <span data-ttu-id="c6d9c-116">Jednak z hello bieżącej architektury sieci platformy Azure, tych wymagań umieszczania nie są już wymagane.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-116">However, with hello current Azure network architecture, these placement requirements are no longer necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6d9c-117">Chociaż jest technicznie możliwe, toocreate sieci wirtualnej, która jest skojarzona z grupą koligacji, nie istnieje żadne atrakcyjnych toodo Przyczyna tak.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-117">Although it is still technically possible toocreate a virtual network that is associated with an affinity group, there is no compelling reason toodo so.</span></span> <span data-ttu-id="c6d9c-118">Wiele funkcji sieci wirtualnej, takich jak grupy zabezpieczeń sieciowych, są dostępne tylko po użyciu regionalną sieć wirtualną, a nie są dostępne dla sieci wirtualnych, które są skojarzone z grup koligacji.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-118">Many virtual network features, such as network security groups, are only available when using a regional virtual network, and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

## <a name="edit-hello-network-configuration-file"></a><span data-ttu-id="c6d9c-119">Edytowanie pliku konfiguracji sieci hello</span><span class="sxs-lookup"><span data-stu-id="c6d9c-119">Edit hello network configuration file</span></span>

1. <span data-ttu-id="c6d9c-120">Eksportowanie pliku konfiguracji sieci hello.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-120">Export hello network configuration file.</span></span> <span data-ttu-id="c6d9c-121">toolearn jak tooexport konfiguracji sieci przy użyciu programu PowerShell lub plik hello Azure interfejsu wiersza polecenia (CLI) 1.0, zobacz [skonfigurować sieć wirtualną przy użyciu pliku konfiguracji sieci](virtual-networks-using-network-configuration-file.md#export).</span><span class="sxs-lookup"><span data-stu-id="c6d9c-121">toolearn how tooexport a network configuration file using PowerShell or hello Azure command-line interface (CLI) 1.0, see [Configure a virtual network using a network configuration file](virtual-networks-using-network-configuration-file.md#export).</span></span>
2. <span data-ttu-id="c6d9c-122">Edytowanie pliku konfiguracji sieci hello, zastępując **AffinityGroup** z **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-122">Edit hello network configuration file, replacing **AffinityGroup** with **Location**.</span></span> <span data-ttu-id="c6d9c-123">Określ Azure [region](https://azure.microsoft.com/regions) dla **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-123">You specify an Azure [region](https://azure.microsoft.com/regions) for **Location**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c6d9c-124">Witaj **lokalizacji** to region hello, określony dla hello grupie koligacji, która jest skojarzona z sieci wirtualnej (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="c6d9c-124">hello **Location** is hello region that you specified for hello affinity group that is associated with your virtual network (classic).</span></span> <span data-ttu-id="c6d9c-125">Na przykład, jeśli w Twojej sieci wirtualnej (klasyczne) jest skojarzona z grupą koligacji znajdującego się w zachodnie stany USA, podczas migracji Twoje **lokalizacji** musi wskazywać tooWest Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-125">For example, if your virtual network (classic) is associated with an affinity group that is located in West US, when you migrate, your **Location** must point tooWest US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="c6d9c-126">Edytuj hello następujące wiersze w pliku konfiguracji sieci, zastępując wartości hello własnych:</span><span class="sxs-lookup"><span data-stu-id="c6d9c-126">Edit hello following lines in your network configuration file, replacing hello values with your own:</span></span> 
   
    <span data-ttu-id="c6d9c-127">**Stara wartość:** \<VirtualNetworkSitename = AffinityGroup "VNetUSWest" = "VNetDemoAG"\></span><span class="sxs-lookup"><span data-stu-id="c6d9c-127">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="c6d9c-128">**Nowa wartość:** \<VirtualNetworkSitename = "VNetUSWest" Lokalizacja = "Zachodnie stany USA"\></span><span class="sxs-lookup"><span data-stu-id="c6d9c-128">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="c6d9c-129">Zapisz zmiany i [zaimportować](virtual-networks-using-network-configuration-file.md#import) hello tooAzure konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-129">Save your changes and [import](virtual-networks-using-network-configuration-file.md#import) hello network configuration tooAzure.</span></span>

> [!NOTE]
> <span data-ttu-id="c6d9c-130">Ta migracja nie powoduje żadnych przestojów tooyour usług.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-130">This migration does NOT cause any downtime tooyour services.</span></span>
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a><span data-ttu-id="c6d9c-131">Jakie toodo, jeśli masz maszyny Wirtualnej (klasyczne) w grupie koligacji</span><span class="sxs-lookup"><span data-stu-id="c6d9c-131">What toodo if you have a VM (classic) in an affinity group</span></span>
<span data-ttu-id="c6d9c-132">Maszyny wirtualne (klasyczne) są obecnie w grupie koligacji nie ma potrzeby toobe usunięte z grupy koligacji hello.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-132">VMs (classic) that are currently in an affinity group do not need toobe removed from hello affinity group.</span></span> <span data-ttu-id="c6d9c-133">Po wdrożeniu maszyny Wirtualnej jest jednostką skalowania pojedynczego tooa wdrożone.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-133">Once a VM is deployed, it is deployed tooa single scale unit.</span></span> <span data-ttu-id="c6d9c-134">Grupy koligacji, można ograniczyć zestaw hello dostępnych rozmiarów maszyn wirtualnych do nowego wdrożenia maszyny Wirtualnej, ale istniejącej maszyny Wirtualnej, które zostało wdrożone już jest ograniczony zestaw toohello maszyny wirtualnej rozmiarów dostępnych w jednostce skalowania hello, w których hello maszyna wirtualna jest wdrożona.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-134">Affinity groups can restrict hello set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted toohello set of VM sizes available in hello scale unit in which hello VM is deployed.</span></span> <span data-ttu-id="c6d9c-135">Ponieważ powitalne maszyna wirtualna jest już wdrożony tooa jednostki skalowania, usuwanie maszyny Wirtualnej z grupy koligacji nie ma wpływu na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c6d9c-135">Because hello VM is already deployed tooa scale unit, removing a VM from an affinity group has no effect on hello VM.</span></span>
