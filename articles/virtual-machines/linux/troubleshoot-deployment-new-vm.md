---
title: "aaaTroubleshoot wdrożenia maszyny Wirtualnej systemu Linux-RM | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów dotyczących wdrożenia usługi Resource Manager podczas tworzenia nowej maszyny wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="d54d7-103">Rozwiązywanie problemów wdrożenia usługi Resource Manager z Tworzenie nowej maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d54d7-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="d54d7-104">Najważniejsze problemy</span><span class="sxs-lookup"><span data-stu-id="d54d7-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="d54d7-105">Inne problemy z wdrażaniem maszyny Wirtualnej i pytania, zobacz [Rozwiązywanie problemów z wdrażanie problemy dotyczące maszyny wirtualnej systemu Linux na platformie Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="d54d7-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="d54d7-106">Rejestruje działania zbieranie</span><span class="sxs-lookup"><span data-stu-id="d54d7-106">Collect activity logs</span></span>
<span data-ttu-id="d54d7-107">toostart rozwiązywania problemów, zbieranie hello działania rejestruje błąd hello tooidentify skojarzone z hello problem.</span><span class="sxs-lookup"><span data-stu-id="d54d7-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="d54d7-108">Witaj poniższe łącza zawierają szczegółowe informacje na powitania toofollow procesu.</span><span class="sxs-lookup"><span data-stu-id="d54d7-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="d54d7-109">Wyświetlanie operacji wdrażania</span><span class="sxs-lookup"><span data-stu-id="d54d7-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="d54d7-110">Wyświetl toomanage Dzienniki aktywności Azure zasobów</span><span class="sxs-lookup"><span data-stu-id="d54d7-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="d54d7-111">**/ Y:** Jeśli hello systemu operacyjnego Linux uogólniony i jest przekazany lub przechwycone z hello uogólniony ustawienie, wówczas nie będzie żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="d54d7-111">**Y:** If hello OS is Linux generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="d54d7-112">Podobnie jeśli jest hello systemu operacyjnego Linux specjalizowany i jest przekazany lub przechwycić przy hello specjalizowany ustawienie, nie będzie błędów, a następnie.</span><span class="sxs-lookup"><span data-stu-id="d54d7-112">Similarly, if hello OS is Linux specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="d54d7-113">**Przekazywanie błędów:**</span><span class="sxs-lookup"><span data-stu-id="d54d7-113">**Upload Errors:**</span></span>

<span data-ttu-id="d54d7-114">**N<sup>1</sup>:** Jeśli hello systemu operacyjnego Linux uogólniony, a jest przekazywany jako wyspecjalizowane, otrzymasz inicjowania obsługi administracyjnej błąd upływu limitu czasu ponieważ hello maszyny Wirtualnej jest zablokowany na powitania inicjowania obsługi administracyjnej etapu.</span><span class="sxs-lookup"><span data-stu-id="d54d7-114">**N<sup>1</sup>:** If hello OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because hello VM is stuck at hello provisioning stage.</span></span>

<span data-ttu-id="d54d7-115">**N<sup>2</sup>:** w przypadku hello systemu operacyjnego Linux specjalizowany, a przesłaniem jako uogólniony, otrzymasz błędem błąd inicjowania obsługi administracyjnej, ponieważ hello nowej maszyny Wirtualnej został uruchomiony z hello oryginalną nazwę komputera, nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="d54d7-115">**N<sup>2</sup>:** If hello OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="d54d7-116">**Rozwiązanie:**</span><span class="sxs-lookup"><span data-stu-id="d54d7-116">**Resolution:**</span></span>

<span data-ttu-id="d54d7-117">tooresolve obu tych błędów, Przekaż hello oryginalny dysk VHD, dostępnych na lokalnym, z hello takie same jak ustawienie hello systemu operacyjnego (uogólniony/specjalizowany).</span><span class="sxs-lookup"><span data-stu-id="d54d7-117">tooresolve both these errors, upload hello original VHD, available on-prem, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="d54d7-118">tooupload jako uogólniony, pamiętaj toorun-anulowanie zastrzeżenia najpierw.</span><span class="sxs-lookup"><span data-stu-id="d54d7-118">tooupload as generalized, remember toorun -deprovision first.</span></span>

<span data-ttu-id="d54d7-119">**Zapisz błędy:**</span><span class="sxs-lookup"><span data-stu-id="d54d7-119">**Capture Errors:**</span></span>

<span data-ttu-id="d54d7-120">**N<sup>3</sup>:** Jeśli hello systemu operacyjnego Linux uogólniony, a jest przechwytywany jako wyspecjalizowane, otrzymasz inicjowania obsługi administracyjnej błąd upływu limitu czasu, ponieważ oryginalne hello maszyny Wirtualnej nie jest używany jako jest oznaczony jako uogólniony.</span><span class="sxs-lookup"><span data-stu-id="d54d7-120">**N<sup>3</sup>:** If hello OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="d54d7-121">**N<sup>4</sup>:** w przypadku hello systemu operacyjnego Linux specjalizowany i jest przechwytywany jako uogólniony, otrzymasz błędem błąd inicjowania obsługi administracyjnej, ponieważ hello nowej maszyny Wirtualnej został uruchomiony z hello oryginalną nazwę komputera, nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="d54d7-121">**N<sup>4</sup>:** If hello OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span> <span data-ttu-id="d54d7-122">Ponadto oryginalne hello maszyny Wirtualnej nie jest używany, ponieważ jest on oznaczony jako specjalne.</span><span class="sxs-lookup"><span data-stu-id="d54d7-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="d54d7-123">**Rozwiązanie:**</span><span class="sxs-lookup"><span data-stu-id="d54d7-123">**Resolution:**</span></span>

<span data-ttu-id="d54d7-124">tooresolve obu tych błędów, Usuń hello bieżącego obrazu z portalu hello i [je ponownie przechwycić z hello bieżącego wirtualne dyski twarde](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) z hello sam, jak ustawienie hello systemu operacyjnego (uogólniony/specjalizowany).</span><span class="sxs-lookup"><span data-stu-id="d54d7-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="d54d7-125">Problem: Niestandardowy / galerii / obrazu z witryny marketplace; Błąd alokacji</span><span class="sxs-lookup"><span data-stu-id="d54d7-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="d54d7-126">Ten błąd pojawia się w sytuacjach, gdy hello nowe żądanie maszyny Wirtualnej jest przypięty tooa klastra, który nie obsługuje żądanej rozmiar maszyny Wirtualnej hello albo nie ma wolnego miejsca tooaccommodate hello żądania.</span><span class="sxs-lookup"><span data-stu-id="d54d7-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="d54d7-127">**Przyczyna 1:** hello klastra nie może obsługiwać hello żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d54d7-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="d54d7-128">**Rozwiązanie 1:**</span><span class="sxs-lookup"><span data-stu-id="d54d7-128">**Resolution 1:**</span></span>

* <span data-ttu-id="d54d7-129">Ponów żądanie hello przy użyciu mniejszego rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d54d7-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="d54d7-130">Jeśli hello żądany rozmiar hello się, że nie można zmienić maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="d54d7-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="d54d7-131">Zatrzymaj wszystkie hello maszyn wirtualnych w zestawie dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="d54d7-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="d54d7-132">Kliknij przycisk **grup zasobów** > *grupie zasobów* > **zasobów** > *zestawu dostępności* > **maszyn wirtualnych** > *maszyny wirtualnej* > **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="d54d7-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="d54d7-133">Po hello wszystkich stopu maszyn wirtualnych, należy utworzyć hello nowej maszyny Wirtualnej w hello żądanego rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="d54d7-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="d54d7-134">Uruchom najpierw hello nowej maszyny Wirtualnej, a następnie wybierz każdego z hello zatrzymane maszyn wirtualnych i kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="d54d7-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="d54d7-135">**Przyczyny 2:** hello klastra nie ma wolnego zasobów.</span><span class="sxs-lookup"><span data-stu-id="d54d7-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="d54d7-136">**Rozdzielczość 2:**</span><span class="sxs-lookup"><span data-stu-id="d54d7-136">**Resolution 2:**</span></span>

* <span data-ttu-id="d54d7-137">Ponów żądanie hello w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="d54d7-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="d54d7-138">Jeśli hello nowej maszyny Wirtualnej można ustawić część różnych dostępności</span><span class="sxs-lookup"><span data-stu-id="d54d7-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="d54d7-139">Tworzenie nowej maszyny Wirtualnej w innym zestawem dostępności (w hello tego samego regionu).</span><span class="sxs-lookup"><span data-stu-id="d54d7-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="d54d7-140">Dodaj nowe toohello wirtualna hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d54d7-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d54d7-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d54d7-141">Next steps</span></span>
<span data-ttu-id="d54d7-142">Jeśli wystąpią problemy podczas uruchamiania zatrzymanej maszyny Wirtualnej systemu Linux lub zmień rozmiar istniejącej maszyny Wirtualnej systemu Linux na platformie Azure, zobacz [problemy z wdrażaniem Rozwiązywanie problemów z Menedżera zasobów z ponownym uruchomieniem lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Linux na platformie Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d54d7-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

