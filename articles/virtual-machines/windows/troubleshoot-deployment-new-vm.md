---
title: "aaaTroubleshoot wdrożenia maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Menedżer zasobów Rozwiązywanie problemów dotyczących wdrożenia podczas tworzenia nowej maszyny wirtualnej systemu Windows na platformie Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c27d4f63b67db2d1c9f117f05a2eba9ef130ef37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a><span data-ttu-id="53716-103">Rozwiązywanie problemów dotyczących wdrożenia podczas tworzenia nowej maszyny Wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="53716-103">Troubleshoot deployment issues when creating a new Windows VM in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="53716-104">Najważniejsze problemy</span><span class="sxs-lookup"><span data-stu-id="53716-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="53716-105">Inne problemy z wdrażaniem maszyny Wirtualnej i pytania, zobacz [rozwiązać wdrażanie systemu Windows maszyny wirtualnej na platformie Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="53716-105">For other VM deployment issues and questions, see [Troubleshoot deploying Windows virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>

## <a name="collect-activity-logs"></a><span data-ttu-id="53716-106">Rejestruje działania zbieranie</span><span class="sxs-lookup"><span data-stu-id="53716-106">Collect activity logs</span></span>
<span data-ttu-id="53716-107">toostart rozwiązywania problemów, zbieranie hello działania rejestruje błąd hello tooidentify skojarzone z hello problem.</span><span class="sxs-lookup"><span data-stu-id="53716-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="53716-108">Witaj poniższe łącza zawierają szczegółowe informacje na powitania toofollow procesu.</span><span class="sxs-lookup"><span data-stu-id="53716-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="53716-109">Wyświetlanie operacji wdrażania</span><span class="sxs-lookup"><span data-stu-id="53716-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="53716-110">Wyświetl toomanage Dzienniki aktywności Azure zasobów</span><span class="sxs-lookup"><span data-stu-id="53716-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="53716-111">**/ Y:** Jeśli hello systemu operacyjnego Windows uogólniony i jest przekazany lub przechwycone z hello uogólniony ustawienie, wówczas nie będzie błędów.</span><span class="sxs-lookup"><span data-stu-id="53716-111">**Y:** If hello OS is Windows generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="53716-112">Podobnie jeśli hello systemu operacyjnego jest specjalizowany systemu Windows i jest przekazany lub przechwycone z hello specjalizowany ustawienie, nie będzie błędów, a następnie.</span><span class="sxs-lookup"><span data-stu-id="53716-112">Similarly, if hello OS is Windows specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="53716-113">**Przekazywanie błędów:**</span><span class="sxs-lookup"><span data-stu-id="53716-113">**Upload Errors:**</span></span>

<span data-ttu-id="53716-114">**N<sup>1</sup>:** Jeśli hello systemu operacyjnego Windows uogólniony, a jest przekazywany jako wyspecjalizowane, wystąpi błąd limitu czasu inicjowania obsługi administracyjnej z maszyny Wirtualnej jest zablokowany na ekranie OOBE hello hello.</span><span class="sxs-lookup"><span data-stu-id="53716-114">**N<sup>1</sup>:** If hello OS is Windows generalized, and it is uploaded as specialized, you will get a provisioning timeout error with hello VM stuck at hello OOBE screen.</span></span>

<span data-ttu-id="53716-115">**N<sup>2</sup>:** Jeśli hello systemu operacyjnego jest specjalizowany systemu Windows, a przesłaniem jako uogólniony, otrzyma inicjowania obsługi administracyjnej błąd awarii z maszyny Wirtualnej jest zablokowany na ekranie OOBE hello ponieważ hello nowej maszyny Wirtualnej został uruchomiony z oryginalnego komputera hello hello Nazwa, nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="53716-115">**N<sup>2</sup>:** If hello OS is Windows specialized, and it is uploaded as generalized, you will get a provisioning failure error with hello VM stuck at hello OOBE screen because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="53716-116">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="53716-116">**Resolution**</span></span>

<span data-ttu-id="53716-117">użyć obu tych błędów, tooresolve [tooupload AzureRmVhd Dodaj hello oryginalny dysk VHD](https://msdn.microsoft.com/library/mt603554.aspx), dostępnych na lokalnym, hello samo ustawienie jak dla hello systemu operacyjnego (uogólniony/specjalizowany).</span><span class="sxs-lookup"><span data-stu-id="53716-117">tooresolve both these errors, use [Add-AzureRmVhd tooupload hello original VHD](https://msdn.microsoft.com/library/mt603554.aspx), available on-premises, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="53716-118">tooupload jako uogólniony, najpierw należy pamiętać toorun programu sysprep.</span><span class="sxs-lookup"><span data-stu-id="53716-118">tooupload as generalized, remember toorun sysprep first.</span></span>

<span data-ttu-id="53716-119">**Zapisz błędy:**</span><span class="sxs-lookup"><span data-stu-id="53716-119">**Capture Errors:**</span></span>

<span data-ttu-id="53716-120">**N<sup>3</sup>:** Jeśli hello systemu operacyjnego Windows uogólniony, a jest przechwytywany jako wyspecjalizowane, otrzymasz inicjowania obsługi administracyjnej błąd upływu limitu czasu, ponieważ oryginalne hello maszyny Wirtualnej nie jest używany jako jest oznaczony jako uogólniony.</span><span class="sxs-lookup"><span data-stu-id="53716-120">**N<sup>3</sup>:** If hello OS is Windows generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="53716-121">**N<sup>4</sup>:** w przypadku hello systemu operacyjnego Windows specjalizowany i jest przechwytywany jako uogólniony, otrzymasz błędem błąd inicjowania obsługi administracyjnej, ponieważ hello nowej maszyny Wirtualnej został uruchomiony z hello oryginalną nazwę komputera, nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="53716-121">**N<sup>4</sup>:** If hello OS is Windows specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username, and password.</span></span> <span data-ttu-id="53716-122">Ponadto oryginalne hello maszyny Wirtualnej nie jest używany, ponieważ jest on oznaczony jako specjalne.</span><span class="sxs-lookup"><span data-stu-id="53716-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="53716-123">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="53716-123">**Resolution**</span></span>

<span data-ttu-id="53716-124">tooresolve obu tych błędów, Usuń hello bieżącego obrazu z portalu hello i [je ponownie przechwycić z hello bieżącego wirtualne dyski twarde](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) z hello sam, jak ustawienie hello systemu operacyjnego (uogólniony/specjalizowany).</span><span class="sxs-lookup"><span data-stu-id="53716-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a><span data-ttu-id="53716-125">Problem: Niestandardowy/galerii/obrazu witryny marketplace; Błąd alokacji</span><span class="sxs-lookup"><span data-stu-id="53716-125">Issue: Custom/gallery/marketplace image; allocation failure</span></span>
<span data-ttu-id="53716-126">Ten błąd pojawia się w sytuacjach, gdy hello nowe żądanie maszyny Wirtualnej jest przypięty tooa klastra, który nie obsługuje żądanej rozmiar maszyny Wirtualnej hello albo nie ma wolnego miejsca tooaccommodate hello żądania.</span><span class="sxs-lookup"><span data-stu-id="53716-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="53716-127">**Przyczyna 1:** hello klastra nie może obsługiwać hello żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53716-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="53716-128">**Rozwiązanie 1:**</span><span class="sxs-lookup"><span data-stu-id="53716-128">**Resolution 1:**</span></span>

* <span data-ttu-id="53716-129">Ponów żądanie hello przy użyciu mniejszego rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53716-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="53716-130">Jeśli hello żądany rozmiar hello się, że nie można zmienić maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="53716-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="53716-131">Zatrzymaj wszystkie hello maszyn wirtualnych w zestawie dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="53716-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="53716-132">Kliknij przycisk **grup zasobów** > *grupie zasobów* > **zasobów** > *zestawu dostępności* > **maszyn wirtualnych** > *maszyny wirtualnej* > **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="53716-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="53716-133">Po hello wszystkich stopu maszyn wirtualnych, należy utworzyć hello nowej maszyny Wirtualnej w hello żądanego rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="53716-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="53716-134">Uruchom najpierw hello nowej maszyny Wirtualnej, a następnie wybierz każdego z hello zatrzymane maszyn wirtualnych i kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="53716-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="53716-135">**Przyczyny 2:** hello klastra nie ma wolnego zasobów.</span><span class="sxs-lookup"><span data-stu-id="53716-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="53716-136">**Rozdzielczość 2:**</span><span class="sxs-lookup"><span data-stu-id="53716-136">**Resolution 2:**</span></span>

* <span data-ttu-id="53716-137">Ponów żądanie hello w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="53716-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="53716-138">Jeśli hello nowej maszyny Wirtualnej można ustawić część różnych dostępności</span><span class="sxs-lookup"><span data-stu-id="53716-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="53716-139">Tworzenie nowej maszyny Wirtualnej w innym zestawem dostępności (w hello tego samego regionu).</span><span class="sxs-lookup"><span data-stu-id="53716-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="53716-140">Dodaj nowe toohello wirtualna hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53716-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53716-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="53716-141">Next steps</span></span>
<span data-ttu-id="53716-142">Jeśli wystąpią problemy podczas uruchamiania zatrzymanej maszyny Wirtualnej systemu Windows lub zmień rozmiar istniejącej maszyny Wirtualnej systemu Windows na platformie Azure, zobacz [problemy z wdrażaniem Rozwiązywanie problemów z Menedżera zasobów z ponownym uruchomieniem lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Windows na platformie Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="53716-142">If you encounter issues when you start a stopped Windows VM or resize an existing Windows VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

