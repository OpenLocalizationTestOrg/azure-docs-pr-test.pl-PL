---
title: "Ustaw aaaCreate dostępności maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak ustawić toocreate dostępności zarządzane lub niezarządzane dostępności dla maszyn wirtualnych przy użyciu programu Azure PowerShell lub hello portalu w modelu wdrażania usługi Resource Manager hello."
keywords: "Zestaw dostępności"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="de071-104">Zwiększenie dostępności maszyny Wirtualnej przez utworzenie zestawu dostępności Azure</span><span class="sxs-lookup"><span data-stu-id="de071-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="de071-105">Zestawy dostępności zapewniają nadmiarowość tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de071-105">Availability sets provide redundancy tooyour application.</span></span> <span data-ttu-id="de071-106">Zalecamy grupowanie co najmniej dwie maszyny wirtualne w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="de071-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="de071-107">Taka konfiguracja powoduje, że podczas albo planowanego lub nieplanowanego zdarzenia konserwacji, co najmniej jedna maszyna wirtualna będzie dostępna i spełniają hello 99,95% umowy SLA platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de071-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet hello 99.95% Azure SLA.</span></span> <span data-ttu-id="de071-108">Aby uzyskać więcej informacji, zobacz hello [umowy SLA dla maszyn wirtualnych](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="de071-108">For more information, see hello [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de071-109">Maszyny wirtualne muszą zostać utworzone w hello sam grupie zasobów co hello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="de071-109">VMs must be created in hello same resource group as hello availability set.</span></span>
> 

<span data-ttu-id="de071-110">Jeśli chcesz, aby maszyna wirtualna z toobe częścią zestawu dostępności, należy toocreate hello dostępności ustawić pierwszego lub podczas tworzenia pierwszej maszyny Wirtualnej w zestawie hello.</span><span class="sxs-lookup"><span data-stu-id="de071-110">If you want your VM toobe part of an availability set, you need toocreate hello availability set first or while you are creating your first VM in hello set.</span></span> <span data-ttu-id="de071-111">Jeśli maszyna wirtualna zostanie używa dysków zarządzanych, zestaw dostępności hello należy utworzyć jako zestaw dostępności zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="de071-111">If your VM will be using Managed Disks, hello availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="de071-112">Aby uzyskać więcej informacji na temat tworzenia i używania zestawów dostępności, zobacz [Zarządzanie hello dostępność maszyn wirtualnych](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de071-112">For more information about creating and using availability sets, see [Manage hello availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="de071-113">Użyj portalu toocreate hello zestaw dostępności przed Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="de071-113">Use hello portal toocreate an availability set before creating your VMs</span></span>
1. <span data-ttu-id="de071-114">W menu centralnym powitania kliknij **Przeglądaj** i wybierz **zestawy dostępności**.</span><span class="sxs-lookup"><span data-stu-id="de071-114">In hello hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="de071-115">Na powitania **bloku zestawy dostępności**, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="de071-115">On hello **Availability sets blade**, click **Add**.</span></span>
   
    ![Zrzut ekranu pokazujący hello Dodawanie przycisku do tworzenia nowego zestawu dostępności.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="de071-117">Na powitania **tworzenia zestawu dostępności** bloku, hello kompletne informacje dla zestawu.</span><span class="sxs-lookup"><span data-stu-id="de071-117">On hello **Create availability set** blade, complete hello information for your set.</span></span>
   
    ![Zrzut ekranu, że pokazuje hello informacje dotyczące dostępności hello toocreate tooenter ustawiony.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="de071-119">**Nazwa** -hello nazwa powinna być 1 – 80 znaków składają się z liczb, liter, kropki, podkreślenia i łączniki.</span><span class="sxs-lookup"><span data-stu-id="de071-119">**Name** - hello name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="de071-120">Witaj pierwszy znak musi być literą lub cyfrą.</span><span class="sxs-lookup"><span data-stu-id="de071-120">hello first character must be a letter or number.</span></span> <span data-ttu-id="de071-121">Witaj ostatni znak musi być literą, cyfrą lub znakiem podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="de071-121">hello last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="de071-122">**Odporność domen** -hello grupy maszyn wirtualnych, które współużytkują wspólne przełącznik źródła i sieci zasilania Definiowanie domen błędów.</span><span class="sxs-lookup"><span data-stu-id="de071-122">**Fault domains** - fault domains define hello group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="de071-123">Domyślnie maszyny wirtualne hello są rozdzielone przez się toothree domen błędów i może być zmienione toobetween 1 i 3.</span><span class="sxs-lookup"><span data-stu-id="de071-123">By default, hello VMs  are separated across up toothree fault domains and can be changed toobetween 1 and 3.</span></span>
   * <span data-ttu-id="de071-124">**Aktualizowanie domeny** — są domyślnie przypisane pięć domen aktualizacji i można go ustawić toobetween 1 do 20.</span><span class="sxs-lookup"><span data-stu-id="de071-124">**Update domains** -  five update domains are assigned by default and this can be set toobetween 1 and 20.</span></span> <span data-ttu-id="de071-125">Aktualizacja domen wskazują grupy maszyn wirtualnych i podstawowym sprzętem fizycznym, który może zostać uruchomiony ponownie na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="de071-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="de071-126">Na przykład jeśli określono domen, gdy więcej niż pięć maszyny wirtualne są skonfigurowane w ramach jednego zestawu dostępności, hello szóstego maszyny wirtualnej zostaną umieszczone w pięciu aktualizacji hello tej samej domenie aktualizacji pierwszej maszyny wirtualnej hello hello siódme w hello takie same UD jako hello drugiej maszyny wirtualnej i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="de071-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, hello sixth virtual machine will be placed into hello same update domain as hello first virtual machine, hello seventh in hello same UD as hello second virtual machine, and so on.</span></span> <span data-ttu-id="de071-127">kolejność Hello hello ponownych uruchomień komputera nie może być sekwencyjnych, ale tylko jedna aktualizacja domeny zostanie uruchomiony ponownie w czasie.</span><span class="sxs-lookup"><span data-stu-id="de071-127">hello order of hello reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="de071-128">**Subskrypcja** — wybierz hello toouse subskrypcji, jeśli masz więcej niż jeden.</span><span class="sxs-lookup"><span data-stu-id="de071-128">**Subscription** - select hello subscription toouse if you have more than one.</span></span>
   * <span data-ttu-id="de071-129">**Grupa zasobów** — wybierz istniejącą grupę zasobów, klikając strzałkę hello i wybierając grupy zasobów z hello listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="de071-129">**Resource group** - select an existing resource group by clicking hello arrow and selecting a resource group from hello drop down.</span></span> <span data-ttu-id="de071-130">Można również utworzyć nową grupę zasobów, wpisując nazwę.</span><span class="sxs-lookup"><span data-stu-id="de071-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="de071-131">Witaj nazwa może zawierać żadnego z następujących znaków hello: litery, cyfry, kropki, łączniki, podkreślenia i otwierający i zamykający nawias okrągły.</span><span class="sxs-lookup"><span data-stu-id="de071-131">hello name can contain any of hello following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="de071-132">Nazwa Hello nie może kończyć się kropką.</span><span class="sxs-lookup"><span data-stu-id="de071-132">hello name cannot end in a period.</span></span> <span data-ttu-id="de071-133">Wszystkie hello maszyn wirtualnych w grupie dostępności hello muszą toobe utworzone w hello tej samej grupie zasobów co hello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="de071-133">All of hello VMs in hello availability group need toobe created in hello same resource group as hello availability set.</span></span>
   * <span data-ttu-id="de071-134">**Lokalizacja** — wybrać lokalizację z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="de071-134">**Location** - select a location from hello drop-down.</span></span>
   * <span data-ttu-id="de071-135">**Zarządzane** — wybierz tę opcję *tak* toocreate zarządzanych dostępności ustawić toouse z maszynami wirtualnymi, które jako magazynu używały dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="de071-135">**Managed** - select *Yes* toocreate a managed availability set toouse with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="de071-136">Wybierz **nr** Jeśli hello maszyn wirtualnych, które będą znajdować się w zestawie hello dysków niezarządzanego na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="de071-136">Select **No** if hello VMs that will be in hello set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="de071-137">Po zakończeniu wprowadzania informacji powitania kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="de071-137">When you are done entering hello information, click **Create**.</span></span> 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a><span data-ttu-id="de071-138">Użyj hello toocreate portalu maszynę wirtualną i dostępności ustawioną hello sam czas</span><span class="sxs-lookup"><span data-stu-id="de071-138">Use hello portal toocreate a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="de071-139">W przypadku tworzenia nowej maszyny Wirtualnej za pomocą portalu hello, można również utworzyć nowy zbiór dostępności dla maszyny Wirtualnej hello podczas tworzenia hello pierwsza maszyna wirtualna w zestawie hello.</span><span class="sxs-lookup"><span data-stu-id="de071-139">If you are creating a new VM using hello portal, you can also create a new availability set for hello VM while you create hello first VM in hello set.</span></span> <span data-ttu-id="de071-140">Jeśli wybierzesz toouse zarządzane dysków dla maszyny Wirtualnej, zostanie utworzony zestaw dostępności zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="de071-140">If you choose toouse Managed Disks for your VM, a managed availability set will be created.</span></span>

![Zrzut ekranu pokazujący hello proces tworzenia dostępność nowych ustawić podczas tworzenia hello maszyny Wirtualnej.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a><span data-ttu-id="de071-142">Dodawanie nowej maszyny Wirtualnej tooan istniejącego zestawu dostępności w portalu hello</span><span class="sxs-lookup"><span data-stu-id="de071-142">Add a new VM tooan existing availability set in hello portal</span></span>
<span data-ttu-id="de071-143">Dla każdej dodatkowe maszyny Wirtualnej tworzonej powinien należeć w zestawie hello, upewnij się, że tworzenie w hello sam **grupy zasobów** , a następnie wybierz hello istniejących zestawem dostępności w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="de071-143">For each additional VM that you create that should belong in hello set, make sure that you create it in hello same **resource group** and then select hello existing availability set in Step 3.</span></span> 

![Zrzut ekranu przedstawiający tooselect dostępności istniejącej konfiguracji toouse dla maszyny Wirtualnej.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a><span data-ttu-id="de071-145">Użyj programu PowerShell toocreate dostępności ustawić</span><span class="sxs-lookup"><span data-stu-id="de071-145">Use PowerShell toocreate an availability set</span></span>
<span data-ttu-id="de071-146">W tym przykładzie tworzy zbiór nazwanego dostępności **myAvailabilitySet** w hello **myResourceGroup** grupy zasobów w hello **zachodnie stany USA** lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="de071-146">This example creates an availability set named **myAvailabilitySet** in hello **myResourceGroup** resource group in hello **West US** location.</span></span> <span data-ttu-id="de071-147">Musi to zrobić przed utworzeniem hello toobe pierwsza maszyna wirtualna, która będzie hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="de071-147">This needs toobe done before you create hello first VM that will be in hello set.</span></span>

<span data-ttu-id="de071-148">Przed rozpoczęciem upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="de071-148">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="de071-149">Uruchom hello następujących tooinstall polecenia.</span><span class="sxs-lookup"><span data-stu-id="de071-149">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="de071-150">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="de071-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="de071-151">Jeśli korzystasz z zarządzanego dyski dla maszyn wirtualnych, wpisz:</span><span class="sxs-lookup"><span data-stu-id="de071-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="de071-152">Jeśli używasz konta magazynu dla maszyn wirtualnych, wpisz:</span><span class="sxs-lookup"><span data-stu-id="de071-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="de071-153">Aby uzyskać więcej informacji, zobacz [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="de071-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="de071-154">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="de071-154">Troubleshooting</span></span>
* <span data-ttu-id="de071-155">Podczas tworzenia maszyny Wirtualnej, jeśli zestaw dostępności hello nie jest na liście rozwijanej hello w portalu hello może utworzono go w innej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="de071-155">When you create a VM, if hello availability set you want isn't in hello drop-down list in hello portal you may have created it in a different resource group.</span></span> <span data-ttu-id="de071-156">Jeśli nie znasz hello grupy zasobów dla jego dostępność ustawić, przejdź menu centralnym toohello i kliknij przycisk Przeglądaj > toosee ustawia listę dostępności sieci i grupy zasobów, które należą do zestawy dostępności.</span><span class="sxs-lookup"><span data-stu-id="de071-156">If you don't know hello resource group for your availability set, go toohello hub menu and click Browse > Availability sets toosee a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de071-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de071-157">Next steps</span></span>
<span data-ttu-id="de071-158">Dodaj tooyour dodatkowego magazynu maszyny Wirtualnej przez dodanie dodatkowych [dysku danych](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de071-158">Add additional storage tooyour VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

