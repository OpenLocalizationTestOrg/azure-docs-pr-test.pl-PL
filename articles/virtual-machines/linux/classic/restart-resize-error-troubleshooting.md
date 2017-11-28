---
title: "Maszyny Wirtualnej, ponownego uruchamiania lub zmiana rozmiaru problemów | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów wdrożenie klasyczne z ponownym uruchomieniem lub zmieniania rozmiaru istniejącej maszyny wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: c6d4ed45133dc3f4b1f3d17fb5a87d3bf77aa3f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="0edab-103">Rozwiązywanie problemów wdrożenie klasyczne z ponownym uruchomieniem lub zmieniania rozmiaru istniejącej maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0edab-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0edab-104">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="0edab-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="0edab-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0edab-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="0edab-106">Podczas uruchamiania zatrzymanej maszyny wirtualnej Azure (VM), lub zmień rozmiar istniejącej maszyny Wirtualnej Azure, wystąpią typowych błędów jest błąd alokacji.</span><span class="sxs-lookup"><span data-stu-id="0edab-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="0edab-107">Ten błąd powoduje klastra lub regionie nie ma dostępu do zasobów lub nie może obsługiwać żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0edab-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0edab-108">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0edab-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0edab-109">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0edab-109">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0edab-110">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0edab-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="0edab-111">Wersja Menedżera zasobów dla [tutaj](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0edab-111">For the Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="0edab-112">Dzienniki inspekcji zbieranie</span><span class="sxs-lookup"><span data-stu-id="0edab-112">Collect audit logs</span></span>
<span data-ttu-id="0edab-113">Zacząć Rozwiązywanie problemów, zbierz dzienniki inspekcji, aby określić błąd skojarzone z problem.</span><span class="sxs-lookup"><span data-stu-id="0edab-113">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="0edab-114">W portalu Azure kliknij **Przeglądaj** > **maszyn wirtualnych** > *maszyny wirtualnej systemu Linux*  >   **Ustawienia** > **dzienniki inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="0edab-114">In the Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="0edab-115">Problem: Błąd podczas uruchamiania zatrzymanej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0edab-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="0edab-116">Próby uruchomienia zatrzymanej maszyny Wirtualnej, ale awaria alokacji.</span><span class="sxs-lookup"><span data-stu-id="0edab-116">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="0edab-117">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="0edab-117">Cause</span></span>
<span data-ttu-id="0edab-118">Żądania uruchomienia zatrzymanej maszyny Wirtualnej musi podjąć w oryginalnego klastra, który jest hostem usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0edab-118">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="0edab-119">Jednak klaster nie ma wolnego miejsca do spełnienia żądania.</span><span class="sxs-lookup"><span data-stu-id="0edab-119">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="0edab-120">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="0edab-120">Resolution</span></span>
* <span data-ttu-id="0edab-121">Utwórz nową usługę w chmurze i skojarzyć go z jednego regionu lub sieci wirtualnej region, ale nie grupy koligacji.</span><span class="sxs-lookup"><span data-stu-id="0edab-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="0edab-122">Usuń zatrzymanej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0edab-122">Delete the stopped VM.</span></span>
* <span data-ttu-id="0edab-123">Utwórz ponownie maszynę Wirtualną w nowej usługi w chmurze przy użyciu dysków.</span><span class="sxs-lookup"><span data-stu-id="0edab-123">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="0edab-124">Uruchom ponownie utworzyć maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="0edab-124">Start the re-created VM.</span></span>

<span data-ttu-id="0edab-125">Jeśli wystąpi błąd podczas próby utworzenia nowej usługi w chmurze, spróbuj ponownie później lub zmienić regionu dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0edab-125">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0edab-126">Nowa usługa w chmurze będzie miała nowej nazwy i adresu VIP, dlatego należy zmieniać te informacje dla wszystkich zależności, korzystających z tych informacji do istniejącej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0edab-126">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="0edab-127">Problem: Błąd podczas zmiany rozmiaru istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0edab-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="0edab-128">Spróbuj zmienić rozmiar istniejącej maszyny Wirtualnej, ale jest wyświetlany błąd alokacji.</span><span class="sxs-lookup"><span data-stu-id="0edab-128">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="0edab-129">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="0edab-129">Cause</span></span>
<span data-ttu-id="0edab-130">Żądanie zmiany rozmiaru maszyny Wirtualnej musi podjąć w oryginalnego klastra, który jest hostem usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0edab-130">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="0edab-131">Klaster nie obsługuje jednak żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0edab-131">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="0edab-132">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="0edab-132">Resolution</span></span>
<span data-ttu-id="0edab-133">Zmniejsz żądany rozmiar maszyny Wirtualnej i ponów żądanie zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="0edab-133">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="0edab-134">Kliknij przycisk **Przeglądaj wszystkie** > **maszyn wirtualnych (klasyczne)** > *maszyny wirtualnej* > **ustawienia**  >  **Rozmiar**.</span><span class="sxs-lookup"><span data-stu-id="0edab-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="0edab-135">Aby uzyskać szczegółowe instrukcje, zobacz [zmienić rozmiaru maszyny wirtualnej](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="0edab-135">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="0edab-136">Jeśli nie jest możliwe zmniejszenie rozmiaru maszyny Wirtualnej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0edab-136">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="0edab-137">Utwórz nową usługę w chmurze, zapewniając jest nie jest połączony z grupą koligacji i nie jest skojarzona z siecią wirtualną, która jest połączona z grupą koligacji.</span><span class="sxs-lookup"><span data-stu-id="0edab-137">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="0edab-138">Utwórz nowy, o większym rozmiarze maszyny Wirtualnej w nim.</span><span class="sxs-lookup"><span data-stu-id="0edab-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="0edab-139">Umożliwiającej obsługę wszystkich maszyn wirtualnych w tej samej usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0edab-139">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="0edab-140">Jeśli istniejącą usługę w chmurze jest skojarzone z sieci wirtualnej na podstawie regionu, możesz połączyć nową usługę w chmurze do istniejącej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0edab-140">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="0edab-141">Jeśli istniejącą usługę w chmurze nie jest powiązana z siecią wirtualną regionu, następnie należy usunąć maszyn wirtualnych w istniejącej usługi w chmurze i utwórz je ponownie w nowej usługi w chmurze z ich dysków.</span><span class="sxs-lookup"><span data-stu-id="0edab-141">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="0edab-142">Jest jednak należy pamiętać, że nowa usługa w chmurze będzie są nowej nazwy i adresu VIP, więc należy zaktualizować te zależności, których te informacje jest obecnie używana dla istniejącej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0edab-142">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0edab-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0edab-143">Next steps</span></span>
<span data-ttu-id="0edab-144">Jeśli wystąpią problemy podczas tworzenia nowej maszyny Wirtualnej systemu Linux na platformie Azure, zobacz [Rozwiązywanie problemów dotyczących wdrożenia z Tworzenie nowej maszyny wirtualnej systemu Linux na platformie Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0edab-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

