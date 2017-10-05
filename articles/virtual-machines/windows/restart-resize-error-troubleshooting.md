---
title: Problemy z maszyny Wirtualnej, ponownego uruchamiania lub zmiana rozmiaru na platformie Azure | Dokumentacja firmy Microsoft
description: "Rozwiązywanie problemów wdrożenia usługi Resource Manager z ponownego uruchamiania lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Windows na platformie Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 0756b52d-4f5a-4503-ae45-c00a6a2edcdf
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.workload: required
ms.date: 06/13/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 078c4666f047604b1732e828d27e7e26383aa616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-windows-vm-in-azure"></a><span data-ttu-id="192fd-103">Rozwiązywanie problemów dotyczących wdrożenia z ponownym uruchomieniem lub zmiana rozmiaru istniejącej maszyny Wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="192fd-103">Troubleshoot deployment issues with restarting or resizing an existing Windows VM in Azure</span></span>
<span data-ttu-id="192fd-104">Podczas uruchamiania zatrzymanej maszyny wirtualnej Azure (VM), lub zmień rozmiar istniejącej maszyny Wirtualnej Azure, wystąpią typowych błędów jest błąd alokacji.</span><span class="sxs-lookup"><span data-stu-id="192fd-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="192fd-105">Ten błąd powoduje klastra lub regionie nie ma dostępu do zasobów lub nie może obsługiwać żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="192fd-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="192fd-106">Rejestruje działania zbieranie</span><span class="sxs-lookup"><span data-stu-id="192fd-106">Collect activity logs</span></span>
<span data-ttu-id="192fd-107">Zacząć Rozwiązywanie problemów zbierać dzienniki działania, aby zidentyfikować ten błąd skojarzone z problem.</span><span class="sxs-lookup"><span data-stu-id="192fd-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="192fd-108">Poniższe łącza zawierają szczegółowe informacje na temat procesu:</span><span class="sxs-lookup"><span data-stu-id="192fd-108">The following links contain detailed information on the process:</span></span>

[<span data-ttu-id="192fd-109">Wyświetlanie operacji wdrażania</span><span class="sxs-lookup"><span data-stu-id="192fd-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="192fd-110">Wyświetl dzienniki aktywności do zarządzania zasobami Azure</span><span class="sxs-lookup"><span data-stu-id="192fd-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="192fd-111">Problem: Błąd podczas uruchamiania zatrzymanej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="192fd-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="192fd-112">Próby uruchomienia zatrzymanej maszyny Wirtualnej, ale awaria alokacji.</span><span class="sxs-lookup"><span data-stu-id="192fd-112">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="192fd-113">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="192fd-113">Cause</span></span>
<span data-ttu-id="192fd-114">Żądania uruchomienia zatrzymanej maszyny Wirtualnej musi podjąć w oryginalnego klastra, który jest hostem usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="192fd-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="192fd-115">Jednak klaster nie ma wolnego miejsca do spełnienia żądania.</span><span class="sxs-lookup"><span data-stu-id="192fd-115">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="192fd-116">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="192fd-116">Resolution</span></span>
* <span data-ttu-id="192fd-117">Zatrzymanie wszystkich maszyn wirtualnych w zestawie dostępności i uruchom ponownie każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="192fd-117">Stop all the VMs in the availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="192fd-118">Kliknij przycisk **grup zasobów** > *grupie zasobów* > **zasobów** > *zestawu dostępności* > **maszyn wirtualnych** > *maszyny wirtualnej* > **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="192fd-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="192fd-119">Po zatrzymanie wszystkich maszyn wirtualnych, wybierz poszczególne zatrzymania maszyn wirtualnych, a następnie kliknij przycisk Uruchom.</span><span class="sxs-lookup"><span data-stu-id="192fd-119">After all the VMs stop, select each of the stopped VMs and click Start.</span></span>
* <span data-ttu-id="192fd-120">Ponów żądanie ponownego uruchomienia w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="192fd-120">Retry the restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="192fd-121">Problem: Błąd podczas zmiany rozmiaru istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="192fd-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="192fd-122">Spróbuj zmienić rozmiar istniejącej maszyny Wirtualnej, ale jest wyświetlany błąd alokacji.</span><span class="sxs-lookup"><span data-stu-id="192fd-122">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="192fd-123">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="192fd-123">Cause</span></span>
<span data-ttu-id="192fd-124">Żądanie zmiany rozmiaru maszyny Wirtualnej musi podjąć w oryginalnego klastra, który jest hostem usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="192fd-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="192fd-125">Klaster nie obsługuje jednak żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="192fd-125">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="192fd-126">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="192fd-126">Resolution</span></span>
* <span data-ttu-id="192fd-127">Ponów żądanie przy użyciu mniejszego rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="192fd-127">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="192fd-128">Jeśli nie można zmienić rozmiar żądanej maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="192fd-128">If the size of the requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="192fd-129">Zatrzymanie wszystkich maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="192fd-129">Stop all the VMs in the availability set.</span></span>
     
     * <span data-ttu-id="192fd-130">Kliknij przycisk **grup zasobów** > *grupie zasobów* > **zasobów** > *zestawu dostępności* > **maszyn wirtualnych** > *maszyny wirtualnej* > **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="192fd-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="192fd-131">Po zatrzymanie wszystkich maszyn wirtualnych, Zmień rozmiar odpowiednią maszynę Wirtualną na większy rozmiar.</span><span class="sxs-lookup"><span data-stu-id="192fd-131">After all the VMs stop, resize the desired VM to a larger size.</span></span>
  3. <span data-ttu-id="192fd-132">Wybierz po zmianie rozmiaru maszyny Wirtualnej, a następnie kliknij przycisk **Start**, a następnie ponowne uruchomienie wszystkich zatrzymania maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="192fd-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="192fd-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="192fd-133">Next steps</span></span>
<span data-ttu-id="192fd-134">Jeśli wystąpią problemy podczas tworzenia nowej maszyny Wirtualnej systemu Windows na platformie Azure, zobacz [Rozwiązywanie problemów dotyczących wdrożenia z Tworzenie nowej maszyny wirtualnej systemu Windows na platformie Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="192fd-134">If you encounter issues when you create a new Windows VM in Azure, see [Troubleshoot deployment issues with creating a new Windows virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

