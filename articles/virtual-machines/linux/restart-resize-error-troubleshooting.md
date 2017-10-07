---
title: problemy z aaaVM ponownego uruchamiania lub zmiana rozmiaru na platformie Azure | Dokumentacja firmy Microsoft
description: "Rozwiązywanie problemów wdrożenia usługi Resource Manager z ponownego uruchamiania lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="f4754-103">Rozwiązywanie problemów dotyczących wdrożenia z ponownym uruchomieniem lub zmiana rozmiaru istniejącej maszyny Wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f4754-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="f4754-104">Spróbuj toostart zatrzymania maszyny wirtualnej Azure (VM), lub zmień rozmiar istniejącej maszyny Wirtualnej Azure, hello typowym błędem występujących po błąd alokacji.</span><span class="sxs-lookup"><span data-stu-id="f4754-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="f4754-105">Ten błąd powoduje hello klastra lub regionie nie ma dostępnych zasobów lub nie hello Obsługa żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f4754-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="f4754-106">Rejestruje działania zbieranie</span><span class="sxs-lookup"><span data-stu-id="f4754-106">Collect activity logs</span></span>
<span data-ttu-id="f4754-107">toostart rozwiązywania problemów, zbieranie hello działania rejestruje błąd hello tooidentify skojarzone z hello problem.</span><span class="sxs-lookup"><span data-stu-id="f4754-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="f4754-108">Hello następującego łącza zawierają szczegółowe informacje na temat procesu hello:</span><span class="sxs-lookup"><span data-stu-id="f4754-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="f4754-109">Wyświetlanie operacji wdrażania</span><span class="sxs-lookup"><span data-stu-id="f4754-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="f4754-110">Wyświetl toomanage Dzienniki aktywności Azure zasobów</span><span class="sxs-lookup"><span data-stu-id="f4754-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="f4754-111">Problem: Błąd podczas uruchamiania zatrzymanej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f4754-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="f4754-112">Spróbuj toostart zatrzymanej maszyny Wirtualnej, ale jest wyświetlany błąd alokacji.</span><span class="sxs-lookup"><span data-stu-id="f4754-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="f4754-113">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="f4754-113">Cause</span></span>
<span data-ttu-id="f4754-114">Żądanie hello toostart hello zatrzymana maszyna wirtualna ma toobe podjęto na powitania oryginalnego klastra obsługującego hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f4754-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="f4754-115">Witaj klaster nie ma jednak żądania hello toofulfill dostępne wolne miejsce.</span><span class="sxs-lookup"><span data-stu-id="f4754-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="f4754-116">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="f4754-116">Resolution</span></span>
* <span data-ttu-id="f4754-117">Zatrzymaj hello wszystkich maszyn wirtualnych w dostępności hello wartość i ponownie uruchom każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f4754-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="f4754-118">Kliknij przycisk **grup zasobów** > *grupie zasobów* > **zasobów** > *zestawu dostępności* > **maszyn wirtualnych** > *maszyny wirtualnej* > **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="f4754-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="f4754-119">Po wszystkich hello zatrzymania maszyny wirtualne, wybierz poszczególne maszyny wirtualne hello zatrzymana i kliknij przycisk Start.</span><span class="sxs-lookup"><span data-stu-id="f4754-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="f4754-120">Ponów żądanie ponownego uruchomienia hello w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="f4754-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="f4754-121">Problem: Błąd podczas zmiany rozmiaru istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f4754-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="f4754-122">Spróbuj tooresize istniejącej maszyny Wirtualnej, ale jest wyświetlany błąd alokacji.</span><span class="sxs-lookup"><span data-stu-id="f4754-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="f4754-123">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="f4754-123">Cause</span></span>
<span data-ttu-id="f4754-124">żądania Hello hello tooresize maszyna wirtualna ma toobe nastąpiła w oryginalnym klastrze hello danej usługi w chmurze hello hostów.</span><span class="sxs-lookup"><span data-stu-id="f4754-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="f4754-125">Witaj klastra nie obsługuje jednak hello żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f4754-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="f4754-126">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="f4754-126">Resolution</span></span>
* <span data-ttu-id="f4754-127">Ponów żądanie hello przy użyciu mniejszego rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f4754-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="f4754-128">Jeśli hello żądany rozmiar hello się, że nie można zmienić maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="f4754-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="f4754-129">Zatrzymaj wszystkie hello maszyn wirtualnych w zestawie dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="f4754-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="f4754-130">Kliknij przycisk **grup zasobów** > *grupie zasobów* > **zasobów** > *zestawu dostępności* > **maszyn wirtualnych** > *maszyny wirtualnej* > **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="f4754-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="f4754-131">Po wszystkich hello zatrzymania maszyny wirtualne, Zmień rozmiar hello potrzeby maszyny Wirtualnej tooa większy rozmiar.</span><span class="sxs-lookup"><span data-stu-id="f4754-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="f4754-132">Wybierz hello zmiany rozmiaru maszyny Wirtualnej i kliknij przycisk **Start**, a następnie uruchom każdą hello zatrzymane maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f4754-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4754-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f4754-133">Next steps</span></span>
<span data-ttu-id="f4754-134">Jeśli wystąpią problemy podczas tworzenia nowej maszyny Wirtualnej systemu Linux na platformie Azure, zobacz [Rozwiązywanie problemów dotyczących wdrożenia z Tworzenie nowej maszyny wirtualnej systemu Linux na platformie Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f4754-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

