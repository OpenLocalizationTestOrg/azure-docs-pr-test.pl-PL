---
title: "aaaTroubleshoot wdrażanie problemy dotyczące maszyny wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z wdrażanie problemy dotyczące maszyny wirtualnej systemu Linux w modelu wdrażania Menedżera zasobów Azurethe."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="36579-103">Rozwiązywanie problemów z wdrażanie problemy dotyczące maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="36579-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="36579-104">problemy z wdrażaniem tootroubleshoot maszyny wirtualnej (VM) na platformie Azure, przejrzyj hello [Najważniejsze problemy](#top-issues) dla typowych błędów i rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="36579-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="36579-105">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="36579-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="36579-106">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36579-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="36579-107">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz **uzyskać obsługuje**.</span><span class="sxs-lookup"><span data-stu-id="36579-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="36579-108">Najważniejsze problemy</span><span class="sxs-lookup"><span data-stu-id="36579-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="36579-109">Witaj klastra nie może obsługiwać hello żądany rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="36579-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="36579-110">Ponów żądanie hello przy użyciu mniejszego rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36579-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="36579-111">Jeśli hello żądany rozmiar hello się, że nie można zmienić maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="36579-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="36579-112">Zatrzymaj wszystkie hello maszyn wirtualnych w zestawie dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="36579-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="36579-113">Kliknij przycisk **grup zasobów** > grupy zasobów > **zasobów** > zestawu dostępności > **maszyn wirtualnych** > maszyny wirtualnej > **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="36579-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="36579-114">Po wszystkich hello zatrzymywania maszyn wirtualnych, należy utworzyć hello maszyny Wirtualnej w hello żądanego rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="36579-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="36579-115">Uruchom najpierw hello nowej maszyny Wirtualnej, a następnie wybierz każdego z hello zatrzymana maszyn wirtualnych i kliknij przycisk Start.</span><span class="sxs-lookup"><span data-stu-id="36579-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="36579-116">Witaj klastra nie ma wolnego zasobów</span><span class="sxs-lookup"><span data-stu-id="36579-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="36579-117">Ponów żądanie hello później.</span><span class="sxs-lookup"><span data-stu-id="36579-117">Retry hello request later.</span></span>
- <span data-ttu-id="36579-118">Jeśli hello nowej maszyny Wirtualnej można ustawić część różnych dostępności</span><span class="sxs-lookup"><span data-stu-id="36579-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="36579-119">Tworzenie maszyny Wirtualnej w innym zestawem dostępności (w hello tego samego regionu).</span><span class="sxs-lookup"><span data-stu-id="36579-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="36579-120">Dodaj nowe toohello wirtualna hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36579-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="36579-121">Jak aktywować Moje miesięczny kredyt dla programu Visual studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="36579-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="36579-122">tooactivate miesięcznych Twojej karty kredytowej, zobacz ten [artykułu](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="36579-122">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="36579-123">Dlaczego I nie można zainstalować sterownik procesora GPU powitania dla maszyny Wirtualnej systemu Ubuntu wirtualizacją sieci?</span><span class="sxs-lookup"><span data-stu-id="36579-123">Why can I not install hello GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="36579-124">Obecnie Obsługa Linux GPU jest dostępna tylko na maszynach wirtualnych NC Azure systemem Ubuntu Server 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="36579-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="36579-125">Aby uzyskać więcej informacji, zobacz [Konfigurowanie wersji sterowników procesora GPU dla maszyn wirtualnych N-series systemem Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="36579-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="36579-126">Brak sterowników, dla mojej wirtualna N-Series systemu Linux</span><span class="sxs-lookup"><span data-stu-id="36579-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="36579-127">Sterowniki dla maszyn wirtualnych w systemie Linux znajdują się [tutaj](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="36579-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="36579-128">Nie można znaleźć wystąpienia procesora GPU w mojej wirtualna N serii</span><span class="sxs-lookup"><span data-stu-id="36579-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="36579-129">tootake korzystać z funkcji GPU hello Azure N-series maszyny wirtualne z systemami Windows Server 2016 lub Windows Server 2012 R2, należy zainstalować sterowniki grafiki NVIDIA na każdej maszynie Wirtualnej po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="36579-129">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="36579-130">Sterownik instalacji informacje są dostępne dla [maszyn wirtualnych systemu Windows](../windows/n-series-driver-setup.md) i [maszyn wirtualnych systemu Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="36579-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="36579-131">N-Series maszyn wirtualnych jest dostępny w moim regionie?</span><span class="sxs-lookup"><span data-stu-id="36579-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="36579-132">Możesz sprawdzić dostępność hello z hello [produkty dostępne przez tabelę region](https://azure.microsoft.com/regions/services)i cenach [tutaj](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="36579-132">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="36579-133">Nie mam stanie toosee rodziny rozmiar maszyny Wirtualnej, która przy zmianie rozmiaru Moja maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="36579-133">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="36579-134">Kiedy maszyna wirtualna jest uruchomiona, jest tooa wdrożonego serwera fizycznego.</span><span class="sxs-lookup"><span data-stu-id="36579-134">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="36579-135">serwerów fizycznych Hello w regionach platformy Azure są pogrupowane w klastrach wspólnej sprzętu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="36579-135">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="36579-136">Zmiana rozmiaru maszyny Wirtualnej, który wymaga hello wirtualna toobe przenieść toodifferent sprzętu klastrów różni się w zależności od modelu wdrażania został hello toodeploy używane maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36579-136">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="36579-137">Maszyn wirtualnych wdrożonych w klasycznym modelu wdrażania, wdrożenie usługi chmury hello muszą zostać usunięte i wdrożone toochange hello maszyn wirtualnych tooa rozmiar innej rodziny.</span><span class="sxs-lookup"><span data-stu-id="36579-137">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="36579-138">Maszyn wirtualnych wdrożonych w modelu wdrażania usługi Resource Manager, należy zatrzymać wszystkie maszyny wirtualne w zestawie przed zmianą rozmiaru hello żadnej maszyny Wirtualnej w zestawie dostępności hello dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="36579-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="36579-139">Witaj wymienionych rozmiar maszyny Wirtualnej nie jest obsługiwana podczas wdrażania w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="36579-139">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="36579-140">Wybierz rozmiar, który jest obsługiwany w zestawie dostępności hello klastra.</span><span class="sxs-lookup"><span data-stu-id="36579-140">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="36579-141">Zaleca się podczas tworzenia zestawu dostępności toochoose hello największy rozmiar maszyny Wirtualnej przez uważasz, że należy, i mieć stosowania Twojego pierwszego toohello wdrożenia zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="36579-141">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="36579-142">Dystrybucje systemu Linux/wersji są obsługiwane na platformie Azure?</span><span class="sxs-lookup"><span data-stu-id="36579-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="36579-143">Listę hello w systemie Linux można znaleźć na [dystrybucje Azure-Endorsed](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="36579-143">You can find hello list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="36579-144">Można dodać istniejącego zestawu dostępności tooan klasyczne maszyny Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="36579-144">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="36579-145">Tak.</span><span class="sxs-lookup"><span data-stu-id="36579-145">Yes.</span></span> <span data-ttu-id="36579-146">Można dodać istniejącego klasycznego wirtualna tooa nowego lub istniejącego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="36579-146">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="36579-147">Aby uzyskać więcej informacji, zobacz [Dodawanie istniejącego zestawu dostępności maszyny wirtualnej tooan](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="36579-147">For more information see [Add an existing virtual machine tooan availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="36579-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36579-148">Next steps</span></span>
<span data-ttu-id="36579-149">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="36579-149">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="36579-150">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36579-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="36579-151">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz **uzyskać obsługuje**.</span><span class="sxs-lookup"><span data-stu-id="36579-151">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
