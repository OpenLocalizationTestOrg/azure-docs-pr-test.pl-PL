---
title: "Rozwiązywanie problemów z wdrożenia maszyny Wirtualnej systemu Linux-RM | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: aea5db05843b0175b8ef8b713944e12262e33010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="674ac-103">Rozwiązywanie problemów wdrożenia usługi Resource Manager z Tworzenie nowej maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="674ac-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="674ac-104">Najważniejsze problemy</span><span class="sxs-lookup"><span data-stu-id="674ac-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="674ac-105">Inne problemy z wdrażaniem maszyny Wirtualnej i pytania, zobacz [Rozwiązywanie problemów z wdrażanie problemy dotyczące maszyny wirtualnej systemu Linux na platformie Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="674ac-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="674ac-106">Rejestruje działania zbieranie</span><span class="sxs-lookup"><span data-stu-id="674ac-106">Collect activity logs</span></span>
<span data-ttu-id="674ac-107">Zacząć Rozwiązywanie problemów zbierać dzienniki działania, aby zidentyfikować ten błąd skojarzone z problem.</span><span class="sxs-lookup"><span data-stu-id="674ac-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="674ac-108">Poniższe łącza zawierają szczegółowe informacje dla procesu, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="674ac-108">The following links contain detailed information on the process to follow.</span></span>

[<span data-ttu-id="674ac-109">Wyświetlanie operacji wdrażania</span><span class="sxs-lookup"><span data-stu-id="674ac-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="674ac-110">Wyświetl dzienniki aktywności do zarządzania zasobami Azure</span><span class="sxs-lookup"><span data-stu-id="674ac-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="674ac-111">**/ Y:** Jeśli system operacyjny Linux uogólniony i jest przekazany lub przechwycone z ustawieniem uogólniony, wówczas nie będzie błędów.</span><span class="sxs-lookup"><span data-stu-id="674ac-111">**Y:** If the OS is Linux generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="674ac-112">Podobnie w przypadku systemu operacyjnego Linux specjalizowany, jest przekazywane lub przechwycić ustawienia specjalne, a następnie nie będzie błędów.</span><span class="sxs-lookup"><span data-stu-id="674ac-112">Similarly, if the OS is Linux specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="674ac-113">**Przekazywanie błędów:**</span><span class="sxs-lookup"><span data-stu-id="674ac-113">**Upload Errors:**</span></span>

<span data-ttu-id="674ac-114">**N<sup>1</sup>:** Jeśli system operacyjny Linux uogólniony, a jest przekazywany jako wyspecjalizowane, otrzymasz inicjowania obsługi administracyjnej błąd upływu limitu czasu, ponieważ maszyna wirtualna jest zablokowana w fazie inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="674ac-114">**N<sup>1</sup>:** If the OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because the VM is stuck at the provisioning stage.</span></span>

<span data-ttu-id="674ac-115">**N<sup>2</sup>:** w przypadku systemu operacyjnego Linux specjalizowany, a przesłaniem jako uogólniony, otrzymasz inicjowania obsługi administracyjnej błąd niepowodzenie, ponieważ nowa maszyna wirtualna jest uruchomiona z oryginalnej nazwy komputera, nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="674ac-115">**N<sup>2</sup>:** If the OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="674ac-116">**Rozwiązanie:**</span><span class="sxs-lookup"><span data-stu-id="674ac-116">**Resolution:**</span></span>

<span data-ttu-id="674ac-117">Aby rozwiązać oba te błędy, Przekaż oryginalny dysk VHD, dostępne lokalnych, jak to samo ustawienie dla systemu operacyjnego (uogólniony/specjalizowany).</span><span class="sxs-lookup"><span data-stu-id="674ac-117">To resolve both these errors, upload the original VHD, available on-prem, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="674ac-118">Można przekazać jako uogólniony, pamiętaj, aby uruchomić - anulowanie zastrzeżenia najpierw.</span><span class="sxs-lookup"><span data-stu-id="674ac-118">To upload as generalized, remember to run -deprovision first.</span></span>

<span data-ttu-id="674ac-119">**Zapisz błędy:**</span><span class="sxs-lookup"><span data-stu-id="674ac-119">**Capture Errors:**</span></span>

<span data-ttu-id="674ac-120">**N<sup>3</sup>:** Jeśli system operacyjny Linux uogólniony, a jest przechwytywany jako wyspecjalizowane, otrzymasz inicjowania obsługi administracyjnej błąd upływu limitu czasu, ponieważ oryginalna maszyna wirtualna nie jest używany, ponieważ jest oznaczony jako uogólniony.</span><span class="sxs-lookup"><span data-stu-id="674ac-120">**N<sup>3</sup>:** If the OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="674ac-121">**N<sup>4</sup>:** w przypadku systemu operacyjnego Linux specjalizowany i jest przechwytywany jako uogólniony, otrzymasz inicjowania obsługi administracyjnej błąd niepowodzenie, ponieważ nowa maszyna wirtualna jest uruchomiona z oryginalnej nazwy komputera, nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="674ac-121">**N<sup>4</sup>:** If the OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span> <span data-ttu-id="674ac-122">Ponadto oryginalna maszyna wirtualna nie jest używany ponieważ jest oznaczony jako specjalne.</span><span class="sxs-lookup"><span data-stu-id="674ac-122">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="674ac-123">**Rozwiązanie:**</span><span class="sxs-lookup"><span data-stu-id="674ac-123">**Resolution:**</span></span>

<span data-ttu-id="674ac-124">Usuń oba te błędy, Usuń bieżący obraz z portalu, i [je ponownie przechwycić z bieżącym wirtualnych dysków twardych](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to samo ustawienie, jak te dla systemu operacyjnego (uogólniony/specjalizowany).</span><span class="sxs-lookup"><span data-stu-id="674ac-124">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="674ac-125">Problem: Niestandardowy / galerii / obrazu z witryny marketplace; Błąd alokacji</span><span class="sxs-lookup"><span data-stu-id="674ac-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="674ac-126">Ten błąd pojawia się w sytuacjach, gdy nowe żądanie maszyna wirtualna jest przypięta do klastra, która nie obsługuje żądanej rozmiaru maszyny Wirtualnej, lub nie ma dostępnego wolnego miejsca, aby zmieścił się w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="674ac-126">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span></span>

<span data-ttu-id="674ac-127">**Przyczyna 1:** klastra nie może obsługiwać żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="674ac-127">**Cause 1:** The cluster cannot support the requested VM size.</span></span>

<span data-ttu-id="674ac-128">**Rozwiązanie 1:**</span><span class="sxs-lookup"><span data-stu-id="674ac-128">**Resolution 1:**</span></span>

* <span data-ttu-id="674ac-129">Ponów żądanie przy użyciu mniejszego rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="674ac-129">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="674ac-130">Jeśli nie można zmienić rozmiar żądanej maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="674ac-130">If the size of the requested VM cannot be changed:</span></span>
  * <span data-ttu-id="674ac-131">Zatrzymanie wszystkich maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="674ac-131">Stop all the VMs in the availability set.</span></span>
    <span data-ttu-id="674ac-132">Kliknij przycisk **grup zasobów** > *grupie zasobów* > **zasobów** > *zestawu dostępności* > **maszyn wirtualnych** > *maszyny wirtualnej* > **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="674ac-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="674ac-133">Po zatrzymanie wszystkich maszyn wirtualnych, należy utworzyć nową maszynę Wirtualną w wymagany rozmiar.</span><span class="sxs-lookup"><span data-stu-id="674ac-133">After all the VMs stop, create the new VM in the desired size.</span></span>
  * <span data-ttu-id="674ac-134">Najpierw należy uruchomić nową maszynę Wirtualną, a następnie wybierz poszczególne zatrzymania maszyn wirtualnych i kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="674ac-134">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span></span>

<span data-ttu-id="674ac-135">**Przyczyny 2:** klastra nie ma wolnego zasobów.</span><span class="sxs-lookup"><span data-stu-id="674ac-135">**Cause 2:** The cluster does not have free resources.</span></span>

<span data-ttu-id="674ac-136">**Rozdzielczość 2:**</span><span class="sxs-lookup"><span data-stu-id="674ac-136">**Resolution 2:**</span></span>

* <span data-ttu-id="674ac-137">Ponów żądanie w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="674ac-137">Retry the request at a later time.</span></span>
* <span data-ttu-id="674ac-138">Jeśli nowa maszyna wirtualna może być częścią zestawu dostępności różnych</span><span class="sxs-lookup"><span data-stu-id="674ac-138">If the new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="674ac-139">Utwórz nową maszynę Wirtualną w różnych dostępności, ustawić (w tym samym regionie).</span><span class="sxs-lookup"><span data-stu-id="674ac-139">Create a new VM in a different availability set (in the same region).</span></span>
  * <span data-ttu-id="674ac-140">Dodaj nową maszynę Wirtualną do tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="674ac-140">Add the new VM to the same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="674ac-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="674ac-141">Next steps</span></span>
<span data-ttu-id="674ac-142">Jeśli wystąpią problemy podczas uruchamiania zatrzymanej maszyny Wirtualnej systemu Linux lub zmień rozmiar istniejącej maszyny Wirtualnej systemu Linux na platformie Azure, zobacz [problemy z wdrażaniem Rozwiązywanie problemów z Menedżera zasobów z ponownym uruchomieniem lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Linux na platformie Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="674ac-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

