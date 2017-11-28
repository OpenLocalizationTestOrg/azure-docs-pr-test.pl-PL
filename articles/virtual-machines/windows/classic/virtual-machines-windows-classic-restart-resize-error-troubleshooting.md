---
title: "aaaVM ponownego uruchamiania lub zmiana rozmiaru problemów | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów wdrożenie klasyczne z ponownego uruchamiania lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Windows na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="135f1-103">Rozwiązywanie problemów wdrożenie klasyczne z ponownego uruchamiania lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="135f1-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="135f1-104">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="135f1-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="135f1-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="135f1-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="135f1-106">Spróbuj toostart zatrzymania maszyny wirtualnej Azure (VM), lub zmień rozmiar istniejącej maszyny Wirtualnej Azure, hello typowym błędem występujących po błąd alokacji.</span><span class="sxs-lookup"><span data-stu-id="135f1-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="135f1-107">Ten błąd powoduje hello klastra lub regionie nie ma dostępnych zasobów lub nie hello Obsługa żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="135f1-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="135f1-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="135f1-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="135f1-109">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="135f1-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="135f1-110">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="135f1-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="135f1-111">Dzienniki inspekcji zbieranie</span><span class="sxs-lookup"><span data-stu-id="135f1-111">Collect audit logs</span></span>
<span data-ttu-id="135f1-112">Rozwiązywanie problemów, toostart hello zbierania danych inspekcji rejestruje błąd hello tooidentify skojarzone z hello problem.</span><span class="sxs-lookup"><span data-stu-id="135f1-112">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="135f1-113">W portalu Azure hello, kliknij przycisk **Przeglądaj** > **maszyn wirtualnych** > *maszyny wirtualnej systemu Windows*  >   **Ustawienia** > **dzienniki inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="135f1-113">In hello Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="135f1-114">Problem: Błąd podczas uruchamiania zatrzymanej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="135f1-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="135f1-115">Spróbuj toostart zatrzymanej maszyny Wirtualnej, ale jest wyświetlany błąd alokacji.</span><span class="sxs-lookup"><span data-stu-id="135f1-115">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="135f1-116">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="135f1-116">Cause</span></span>
<span data-ttu-id="135f1-117">Żądanie hello toostart hello zatrzymana maszyna wirtualna ma toobe podjęto na powitania oryginalnego klastra obsługującego hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="135f1-117">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="135f1-118">Witaj klaster nie ma jednak żądania hello toofulfill dostępne wolne miejsce.</span><span class="sxs-lookup"><span data-stu-id="135f1-118">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="135f1-119">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="135f1-119">Resolution</span></span>
* <span data-ttu-id="135f1-120">Utwórz nową usługę w chmurze i skojarzyć go z jednego regionu lub sieci wirtualnej region, ale nie grupy koligacji.</span><span class="sxs-lookup"><span data-stu-id="135f1-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="135f1-121">Usuń hello zatrzymana maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="135f1-121">Delete hello stopped VM.</span></span>
* <span data-ttu-id="135f1-122">Utwórz ponownie hello maszyny Wirtualnej w hello nową usługę w chmurze przy użyciu hello dysków.</span><span class="sxs-lookup"><span data-stu-id="135f1-122">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="135f1-123">Uruchom hello ponownie utworzyć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="135f1-123">Start hello re-created VM.</span></span>

<span data-ttu-id="135f1-124">Jeśli wystąpi błąd podczas próby toocreate nową usługę w chmurze, spróbuj ponownie później lub zmienić regionu hello hello usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="135f1-124">If you get an error when trying toocreate a new cloud service, either retry later or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="135f1-125">Hello nową usługę w chmurze będzie miała nowej nazwy i adresu VIP, dlatego należy toochange te informacje dla wszystkich zależności hello korzystających z tych informacji w celu hello istniejącą usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="135f1-125">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="135f1-126">Problem: Błąd podczas zmiany rozmiaru istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="135f1-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="135f1-127">Spróbuj tooresize istniejącej maszyny Wirtualnej, ale jest wyświetlany błąd alokacji.</span><span class="sxs-lookup"><span data-stu-id="135f1-127">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="135f1-128">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="135f1-128">Cause</span></span>
<span data-ttu-id="135f1-129">żądania Hello hello tooresize maszyna wirtualna ma toobe nastąpiła w oryginalnym klastrze hello danej usługi w chmurze hello hostów.</span><span class="sxs-lookup"><span data-stu-id="135f1-129">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="135f1-130">Witaj klastra nie obsługuje jednak hello żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="135f1-130">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="135f1-131">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="135f1-131">Resolution</span></span>
<span data-ttu-id="135f1-132">Zmniejsz hello żądany rozmiar maszyny Wirtualnej i ponów próbę hello rozmiaru żądania.</span><span class="sxs-lookup"><span data-stu-id="135f1-132">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="135f1-133">Kliknij przycisk **Przeglądaj wszystkie** > **maszyn wirtualnych (klasyczne)** > *maszyny wirtualnej* > **ustawienia**  >  **Rozmiar**.</span><span class="sxs-lookup"><span data-stu-id="135f1-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="135f1-134">Aby uzyskać szczegółowe instrukcje, zobacz [zmienić rozmiaru maszyny wirtualnej hello](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="135f1-134">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="135f1-135">Jeśli nie jest możliwe tooreduce hello rozmiar maszyny Wirtualnej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="135f1-135">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="135f1-136">Utwórz nową usługę w chmurze, zapewnienie, że nie jest połączona grupa koligacji tooan i nie są skojarzone z sieci wirtualnej jest tooan połączonej grupy koligacji.</span><span class="sxs-lookup"><span data-stu-id="135f1-136">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="135f1-137">Utwórz nowy, o większym rozmiarze maszyny Wirtualnej w nim.</span><span class="sxs-lookup"><span data-stu-id="135f1-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="135f1-138">Umożliwiającej obsługę wszystkich maszyn wirtualnych w hello sama usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="135f1-138">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="135f1-139">Jeśli istniejącą usługę w chmurze jest skojarzone z sieci wirtualnej na podstawie regionu, możesz połączyć hello nowe chmury usługi toohello istniejącej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="135f1-139">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="135f1-140">Jeśli hello istniejącej usługi chmury nie jest skojarzony z sieci wirtualnej na podstawie regionu, następnie należy mieć toodelete hello maszyn wirtualnych w hello istniejącą usługę w chmurze i utwórz je ponownie hello nowego w usłudze w chmurze z ich dysków.</span><span class="sxs-lookup"><span data-stu-id="135f1-140">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="135f1-141">Jest jednak ważne tooremember hello nową usługę w chmurze że nowej nazwy i adresu VIP, dlatego należy tooupdate tych opcji dla wszystkich zależności hello, które obecnie korzystanie z tej informacji hello istniejącą usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="135f1-141">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="135f1-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="135f1-142">Next steps</span></span>
<span data-ttu-id="135f1-143">Jeśli wystąpią problemy podczas tworzenia maszyny Wirtualnej systemu Windows na platformie Azure, zobacz [Rozwiązywanie problemów dotyczących wdrożenia z tworzenia maszyny wirtualnej systemu Windows na platformie Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="135f1-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

