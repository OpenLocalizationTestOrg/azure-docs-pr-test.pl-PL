---
title: "aaaResize maszyny Wirtualnej systemu Windows w hello klasycznego modelu wdrażania - Azure | Dokumentacja firmy Microsoft"
description: "Zmień rozmiar maszyny wirtualnej systemu Windows utworzonej w hello klasycznego modelu wdrażania, przy użyciu programu Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a><span data-ttu-id="617e9-103">Zmień rozmiar maszyny Wirtualnej systemu Windows utworzonych w hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="617e9-103">Resize a Windows VM created in hello classic deployment model</span></span>
<span data-ttu-id="617e9-104">W tym artykule opisano, jak tooresize maszyny Wirtualnej systemu Windows, utworzonej w hello klasycznego modelu wdrażania przy użyciu programu Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="617e9-104">This article shows you how tooresize a Windows VM, created in hello classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="617e9-105">Podczas określania hello tooresize możliwości maszyny Wirtualnej, istnieją dwa pojęcia kontrolujące hello zakres maszyny wirtualnej hello tooresize dostępne rozmiary.</span><span class="sxs-lookup"><span data-stu-id="617e9-105">When considering hello ability tooresize a VM, there are two concepts which control hello range of sizes available tooresize hello virtual machine.</span></span> <span data-ttu-id="617e9-106">koncepcja pierwszy Hello jest hello regionu, w którym wdrożonej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="617e9-106">hello first concept is hello region in which your VM is deployed.</span></span> <span data-ttu-id="617e9-107">Witaj listę dostępnych rozmiarów maszyny Wirtualnej w regionie jest karcie usług hello strony sieci web hello regiony platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="617e9-107">hello list of VM sizes available in region is under hello Services tab of hello Azure Regions web page.</span></span> <span data-ttu-id="617e9-108">koncepcja drugi Hello jest sprzętem fizycznym hello obecnie udostępnia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="617e9-108">hello second concept is hello physical hardware currently hosting your VM.</span></span> <span data-ttu-id="617e9-109">serwery fizyczne Hello hostingu maszyn wirtualnych są grupowane w klastrach wspólnej sprzętu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="617e9-109">hello physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="617e9-110">Metoda Hello zmiany rozmiaru maszyny Wirtualnej różni się w zależności od, jeśli hello żądany nowy rozmiar maszyny Wirtualnej jest obsługiwany przez hello sprzętu klastra aktualnie obsługujący hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="617e9-110">hello method of changing a VM size differs depending on if hello desired new VM size is supported by hello hardware cluster currently hosting hello VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="617e9-111">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="617e9-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="617e9-112">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="617e9-112">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="617e9-113">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="617e9-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="617e9-114">Możesz również [Zmień rozmiar maszyny Wirtualnej utworzonej w modelu wdrażania usługi Resource Manager hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="617e9-114">You can also [resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="617e9-115">Dodaj swoje konto</span><span class="sxs-lookup"><span data-stu-id="617e9-115">Add your account</span></span>
<span data-ttu-id="617e9-116">Należy skonfigurować toowork programu Azure PowerShell z klasycznym zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="617e9-116">You must configure Azure PowerShell toowork with classic Azure resources.</span></span> <span data-ttu-id="617e9-117">Wykonaj kroki hello poniżej tooconfigure zasoby klasyczne toomanage programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="617e9-117">Follow hello steps below tooconfigure Azure PowerShell toomanage classic resources.</span></span>

1. <span data-ttu-id="617e9-118">W wierszu polecenia programu PowerShell hello, wpisz `Add-AzureAccount` i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="617e9-118">At hello PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="617e9-119">Wpisz adres e-mail hello skojarzone z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="617e9-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="617e9-120">Wpisz hasło powitania dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="617e9-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="617e9-121">Kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="617e9-121">Click **Sign in**.</span></span> 

## <a name="resize-in-hello-same-hardware-cluster"></a><span data-ttu-id="617e9-122">Zmiana rozmiaru w hello sam sprzętu klastra</span><span class="sxs-lookup"><span data-stu-id="617e9-122">Resize in hello same hardware cluster</span></span>
<span data-ttu-id="617e9-123">tooresize rozmiar tooa maszyny Wirtualnej dostępne w klastrze sprzętu hello hosting hello maszyny Wirtualnej, wykonaj hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="617e9-123">tooresize a VM tooa size available in hello hardware cluster hosting hello VM, perform hello following steps.</span></span>

1. <span data-ttu-id="617e9-124">Uruchom hello następującego polecenia programu PowerShell dostępnych w klastrze sprzętu hello hosting usługi hello w chmurze, który zawiera rozmiarów maszyn wirtualnych hello toolist hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="617e9-124">Run hello following PowerShell command toolist hello VM sizes available in hello hardware cluster hosting hello cloud service which contains hello VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="617e9-125">Witaj uruchom następujące polecenia hello tooresize maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="617e9-125">Run hello following commands tooresize hello VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="617e9-126">Zmiana rozmiaru w nowym klastrze sprzętu</span><span class="sxs-lookup"><span data-stu-id="617e9-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="617e9-127">tooresize rozmiar tooa maszyny Wirtualnej nie jest dostępna w hello sprzętu klastra hostingu hello maszyny Wirtualnej, hello usługa w chmurze i wszystkich maszyn wirtualnych w usłudze w chmurze hello muszą zostać ponownie utworzone.</span><span class="sxs-lookup"><span data-stu-id="617e9-127">tooresize a VM tooa size not available in hello hardware cluster hosting hello VM, hello cloud service and all VMs in hello cloud service must be recreated.</span></span> <span data-ttu-id="617e9-128">Każdą usługę w chmurze jest hostowanych w klastrze pojedynczego sprzętu, więc wszystkie maszyny wirtualne w usłudze w chmurze hello musi mieć rozmiar, który jest obsługiwany w klastrze sprzętu.</span><span class="sxs-lookup"><span data-stu-id="617e9-128">Each cloud service is hosted on a single hardware cluster so all VMs in hello cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="617e9-129">Witaj następujące kroki opisano, jak tooresize maszyn wirtualnych przez usunięcie i ponowne utworzenie następnie hello chmury usługi.</span><span class="sxs-lookup"><span data-stu-id="617e9-129">hello following steps will describe how tooresize a VM by deleting and then recreating hello cloud service.</span></span>

1. <span data-ttu-id="617e9-130">Uruchom hello następującego środowiska PowerShell polecenie toolist hello rozmiarów maszyn wirtualnych dostępne w regionie hello.</span><span class="sxs-lookup"><span data-stu-id="617e9-130">Run hello following PowerShell command toolist hello VM sizes available in hello region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="617e9-131">Zanotuj wszystkie ustawienia konfiguracji dla każdej maszyny Wirtualnej w usłudze w chmurze hello zawierającą hello wirtualna toobe zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="617e9-131">Make note of all configuration settings for each VM in hello cloud service which contains hello VM toobe resized.</span></span> 
3. <span data-ttu-id="617e9-132">Usuń wszystkie maszyny wirtualne w usłudze w chmurze hello wybór hello opcja tooretain hello dysków dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="617e9-132">Delete all VMs in hello cloud service selecting hello option tooretain hello disks for each VM.</span></span>
4. <span data-ttu-id="617e9-133">Utwórz ponownie hello wirtualna toobe zmiany rozmiaru przy użyciu hello żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="617e9-133">Recreate hello VM toobe resized using hello desired VM size.</span></span>
5. <span data-ttu-id="617e9-134">Utwórz ponownie wszystkich innych maszyn wirtualnych będących hello w usłudze w chmurze przy użyciu rozmiaru maszyny Wirtualnej dostępne w klastrze sprzętu hello teraz hosting hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="617e9-134">Recreate all other VMs which were in hello cloud service using a VM size available in hello hardware cluster now hosting hello cloud service.</span></span>

<span data-ttu-id="617e9-135">Przykładowy skrypt do usuwania i ponowne utworzenie usługi w chmurze przy użyciu nowego rozmiaru maszyny Wirtualnej można znaleźć [tutaj](https://github.com/Azure/azure-vm-scripts).</span><span class="sxs-lookup"><span data-stu-id="617e9-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="617e9-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="617e9-136">Next steps</span></span>
* <span data-ttu-id="617e9-137">[Zmień rozmiar maszyny Wirtualnej utworzonej w modelu wdrażania usługi Resource Manager hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="617e9-137">[Resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

