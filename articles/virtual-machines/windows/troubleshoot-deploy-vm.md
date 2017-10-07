---
title: "aaaTroubleshoot wdrażanie problemy dotyczące maszyny wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Wdrażanie systemu Windows maszyny wirtualnej Rozwiązywanie problemów z w modelu wdrażania Azurethe Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="ebf87-103">Rozwiązywanie problemów z wdrażanie problemy dotyczące maszyny wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ebf87-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="ebf87-104">problemy z wdrażaniem tootroubleshoot maszyny wirtualnej (VM) na platformie Azure, przejrzyj hello [Najważniejsze problemy](#top-issues) dla typowych błędów i rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ebf87-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="ebf87-105">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="ebf87-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="ebf87-106">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf87-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="ebf87-107">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz **uzyskać obsługuje**.</span><span class="sxs-lookup"><span data-stu-id="ebf87-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="ebf87-108">Najważniejsze problemy</span><span class="sxs-lookup"><span data-stu-id="ebf87-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="ebf87-109">Witaj klastra nie może obsługiwać hello żądany rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ebf87-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="ebf87-110">Ponów żądanie hello przy użyciu mniejszego rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ebf87-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="ebf87-111">Jeśli hello żądany rozmiar hello się, że nie można zmienić maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="ebf87-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="ebf87-112">Zatrzymaj wszystkie hello maszyn wirtualnych w zestawie dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="ebf87-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="ebf87-113">Kliknij przycisk **grup zasobów** > grupy zasobów > **zasobów** > zestawu dostępności > **maszyn wirtualnych** > maszyny wirtualnej > **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="ebf87-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="ebf87-114">Po wszystkich hello zatrzymywania maszyn wirtualnych, należy utworzyć hello maszyny Wirtualnej w hello żądanego rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="ebf87-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="ebf87-115">Uruchom najpierw hello nowej maszyny Wirtualnej, a następnie wybierz każdego z hello zatrzymana maszyn wirtualnych i kliknij przycisk Start.</span><span class="sxs-lookup"><span data-stu-id="ebf87-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="ebf87-116">Witaj klastra nie ma wolnego zasobów</span><span class="sxs-lookup"><span data-stu-id="ebf87-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="ebf87-117">Ponów żądanie hello później.</span><span class="sxs-lookup"><span data-stu-id="ebf87-117">Retry hello request later.</span></span>
- <span data-ttu-id="ebf87-118">Jeśli hello nowej maszyny Wirtualnej można ustawić część różnych dostępności</span><span class="sxs-lookup"><span data-stu-id="ebf87-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="ebf87-119">Tworzenie maszyny Wirtualnej w innym zestawem dostępności (w hello tego samego regionu).</span><span class="sxs-lookup"><span data-stu-id="ebf87-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="ebf87-120">Dodaj nowe toohello wirtualna hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ebf87-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="ebf87-121">Jak używać i wdrażanie obrazu klienta systemu windows na platformie Azure?</span><span class="sxs-lookup"><span data-stu-id="ebf87-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="ebf87-122">Służy Windows 7, Windows 8 lub Windows 10 w usłudze Azure scenariusze tworzenia/testowania Jeśli masz odpowiednie subskrypcji programu Visual Studio (dawniej MSDN).</span><span class="sxs-lookup"><span data-stu-id="ebf87-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="ebf87-123">To [artykułu](client-images.md) przedstawiono hello kwalifikujących się wymagania dotyczące uruchamiania klienta systemu Windows Azure i używa hello obrazów w galerii Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf87-123">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and uses of hello Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a><span data-ttu-id="ebf87-124">Jak można wdrożyć maszyny wirtualnej z wykorzystaniem hello korzyści Użyj hybrydowych (KONCENTRATOR)</span><span class="sxs-lookup"><span data-stu-id="ebf87-124">How can I deploy a virtual machine using hello Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="ebf87-125">Istnieje kilka różnych sposobów toodeploy Windows maszynom wirtualnym hello Azure hybrydowego Użyj korzyści.</span><span class="sxs-lookup"><span data-stu-id="ebf87-125">There are a couple of different ways toodeploy Windows virtual machines with hello Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="ebf87-126">Dla subskrypcji Enterprise Agreement:</span><span class="sxs-lookup"><span data-stu-id="ebf87-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="ebf87-127">• Wdrażanie maszyn wirtualnych z określonych obrazów Marketplace, które są wstępnie skonfigurowane z korzyści Użyj hybrydowe platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf87-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="ebf87-128">Dla umowy Enterprise agreement:</span><span class="sxs-lookup"><span data-stu-id="ebf87-128">For Enterprise agreement:</span></span>

<span data-ttu-id="ebf87-129">• Przekazywanie niestandardowych maszyny Wirtualnej i wdrażanie za pomocą szablonu usługi Resource Manager lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ebf87-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="ebf87-130">Aby uzyskać więcej informacji zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="ebf87-130">For more information, see hello following resources:</span></span>

 - [<span data-ttu-id="ebf87-131">Omówienie usługi Azure korzyści Użyj hybrydowego</span><span class="sxs-lookup"><span data-stu-id="ebf87-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="ebf87-132">Do pobrania — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="ebf87-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="ebf87-133">[Korzyści Użyj hybrydowe platformy Azure dla systemu Windows Server i klienta systemu Windows](hybrid-use-benefit-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="ebf87-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="ebf87-134">Jak używać hello korzyści Użyj hybrydowe na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ebf87-134">How can I use hello Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="ebf87-135">Jak aktywować Moje miesięczny kredyt dla programu Visual studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="ebf87-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="ebf87-136">tooactivate miesięcznych Twojej karty kredytowej, zobacz ten [artykułu](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="ebf87-136">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a><span data-ttu-id="ebf87-137">Jak tooadd przedsiębiorstwa: tworzenie i testowanie toomy Enterprise Agreement (EA) tooget uzyskują dostęp do obrazów klientów tooWindow?</span><span class="sxs-lookup"><span data-stu-id="ebf87-137">How tooadd Enterprise Dev/Test toomy Enterprise Agreement (EA) tooget access tooWindow client images?</span></span>

<span data-ttu-id="ebf87-138">Subskrypcje toocreate możliwości Hello oparte na powitania przedsiębiorstwa i testowania oferty jest ograniczone tooAccount właścicieli, którzy otrzymali uprawnienia toodo tak przez administratora przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="ebf87-138">hello ability toocreate subscriptions based on hello Enterprise Dev/Test offer is restricted tooAccount Owners who have been given permission toodo so by an Enterprise Administrator.</span></span> <span data-ttu-id="ebf87-139">Hello właściciela konta tworzy subskrypcji za pośrednictwem portalu konta usługi Azure hello i następnie należy dodać aktywnych subskrybentów usługi Visual Studio jako współadministratorów.</span><span class="sxs-lookup"><span data-stu-id="ebf87-139">hello Account Owner creates subscriptions via hello Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="ebf87-140">Aby mogli zarządzać i użyj hello zasobów niezbędnych do projektowania i testowania.</span><span class="sxs-lookup"><span data-stu-id="ebf87-140">So that they can manage and use hello resources needed for development and testing.</span></span> <span data-ttu-id="ebf87-141">Aby uzyskać więcej informacji, zobacz [przedsiębiorstwa: tworzenie i testowanie](https://azure.microsoft.com/offers/ms-azr-0148p/).</span><span class="sxs-lookup"><span data-stu-id="ebf87-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="ebf87-142">Brak sterowników, dla moich wirtualna N-Series systemu Windows</span><span class="sxs-lookup"><span data-stu-id="ebf87-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="ebf87-143">Sterowniki dla maszyn wirtualnych z systemem Windows znajdują się [tutaj](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="ebf87-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="ebf87-144">Nie można znaleźć wystąpienia procesora GPU w mojej wirtualna N serii</span><span class="sxs-lookup"><span data-stu-id="ebf87-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="ebf87-145">tootake korzystać z funkcji GPU hello Azure N-series maszyny wirtualne z systemami Windows Server 2016 lub Windows Server 2012 R2, należy zainstalować sterowniki grafiki NVIDIA na każdej maszynie Wirtualnej po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="ebf87-145">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="ebf87-146">Sterownik instalacji informacje są dostępne dla [maszyn wirtualnych systemu Windows](n-series-driver-setup.md) i [maszyn wirtualnych systemu Linux](../linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="ebf87-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="ebf87-147">Obrazy klienta są obsługiwane dla serii N?</span><span class="sxs-lookup"><span data-stu-id="ebf87-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="ebf87-148">Azure obsługuje obecnie tylko N serii na maszynach wirtualnych z systemami operacyjnymi Windows Server i Linux.</span><span class="sxs-lookup"><span data-stu-id="ebf87-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="ebf87-149">N-Series maszyn wirtualnych jest dostępny w moim regionie?</span><span class="sxs-lookup"><span data-stu-id="ebf87-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="ebf87-150">Możesz sprawdzić dostępność hello z hello [produkty dostępne przez tabelę region](https://azure.microsoft.com/regions/services)i cenach [tutaj](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="ebf87-150">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a><span data-ttu-id="ebf87-151">Jakie obrazy klienta I użycia i wdrożyć w Azure i sposobu tooI je uzyskać?</span><span class="sxs-lookup"><span data-stu-id="ebf87-151">What client images can I use and deploy in Azure, and how tooI get them?</span></span>

<span data-ttu-id="ebf87-152">Można użyć systemu Windows 7, Windows 8 lub Windows 10 w usłudze Azure scenariusze tworzenia/testowania, pod warunkiem, że masz odpowiednie subskrypcji programu Visual Studio (dawniej MSDN).</span><span class="sxs-lookup"><span data-stu-id="ebf87-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="ebf87-153">Obrazy systemu Windows 10 są dostępne w galerii Azure hello w [oferuje kwalifikujących się tworzenie/testowanie](client-images.md#eligible-offers).</span><span class="sxs-lookup"><span data-stu-id="ebf87-153">Windows 10 images are available from hello Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="ebf87-154">Subskrybentów usługi Visual Studio w obrębie dowolnego typu oferty może również [odpowiednio przygotować i utworzyć](prepare-for-upload-vhd-image.md) 64-bitowego obrazu systemu Windows 7, Windows 8 lub Windows 10, a następnie [przekazać tooAzure](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="ebf87-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload tooAzure](upload-generalized-managed.md).</span></span> <span data-ttu-id="ebf87-155">Użyj Hello pozostaje toodev i testowanie ograniczone przez aktywnych subskrybentów usługi Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebf87-155">hello use remains limited toodev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="ebf87-156">To [artykułu](client-images.md) przedstawiono hello kwalifikujących się wymagania dotyczące uruchamiania klienta systemu Windows Azure i użyj hello obrazów w galerii Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf87-156">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and use of hello Azure Gallery images.</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="ebf87-157">Nie mam stanie toosee rodziny rozmiar maszyny Wirtualnej, która przy zmianie rozmiaru Moja maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="ebf87-157">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="ebf87-158">Kiedy maszyna wirtualna jest uruchomiona, jest tooa wdrożonego serwera fizycznego.</span><span class="sxs-lookup"><span data-stu-id="ebf87-158">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="ebf87-159">serwerów fizycznych Hello w regionach platformy Azure są pogrupowane w klastrach wspólnej sprzętu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="ebf87-159">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="ebf87-160">Zmiana rozmiaru maszyny Wirtualnej, który wymaga hello wirtualna toobe przenieść toodifferent sprzętu klastrów różni się w zależności od modelu wdrażania został hello toodeploy używane maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ebf87-160">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="ebf87-161">Maszyn wirtualnych wdrożonych w klasycznym modelu wdrażania, wdrożenie usługi chmury hello muszą zostać usunięte i wdrożone toochange hello maszyn wirtualnych tooa rozmiar innej rodziny.</span><span class="sxs-lookup"><span data-stu-id="ebf87-161">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="ebf87-162">Maszyn wirtualnych wdrożonych w modelu wdrażania usługi Resource Manager, należy zatrzymać wszystkie maszyny wirtualne w zestawie przed zmianą rozmiaru hello żadnej maszyny Wirtualnej w zestawie dostępności hello dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="ebf87-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="ebf87-163">Witaj wymienionych rozmiar maszyny Wirtualnej nie jest obsługiwana podczas wdrażania w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="ebf87-163">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="ebf87-164">Wybierz rozmiar, który jest obsługiwany w zestawie dostępności hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ebf87-164">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="ebf87-165">Zaleca się podczas tworzenia zestawu dostępności toochoose hello największy rozmiar maszyny Wirtualnej przez uważasz, że należy, i mieć stosowania Twojego pierwszego toohello wdrożenia zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="ebf87-165">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="ebf87-166">Można dodać istniejącego zestawu dostępności tooan klasyczne maszyny Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="ebf87-166">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="ebf87-167">Tak.</span><span class="sxs-lookup"><span data-stu-id="ebf87-167">Yes.</span></span> <span data-ttu-id="ebf87-168">Można dodać istniejącego klasycznego wirtualna tooa nowego lub istniejącego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="ebf87-168">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="ebf87-169">Aby uzyskać więcej informacji, zobacz [Dodawanie istniejącego zestawu dostępności maszyny wirtualnej tooan](classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="ebf87-169">For more information see [Add an existing virtual machine tooan availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="ebf87-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ebf87-170">Next steps</span></span>
<span data-ttu-id="ebf87-171">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="ebf87-171">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="ebf87-172">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf87-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="ebf87-173">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz **uzyskać obsługuje**.</span><span class="sxs-lookup"><span data-stu-id="ebf87-173">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
