---
title: "aaaComparing niestandardowych obrazów i formuły w usłudze DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello różnice między niestandardowych obrazów i formuły jako baz maszyn wirtualnych może zdecydować, który najlepiej odpowiada środowisku."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="3cf22-103">Porównywanie niestandardowych obrazów i formuły w usłudze DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3cf22-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="3cf22-104">Zarówno [niestandardowych obrazów](devtest-lab-create-template.md) i [formuły](devtest-lab-manage-formulas.md) mogą być używane jako podstawy [utworzone nowe maszyny wirtualne](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="3cf22-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="3cf22-105">Jednak rozróżnienia klucza hello niestandardowych obrazów i formuły jest obraz niestandardowy po prostu obraz oparty na dysku VHD, gdy formuła jest obraz oparty na dysku VHD *oprócz* wstępnie skonfigurowane ustawienia — takich jak rozmiar maszyny Wirtualnej, sieci wirtualnej podsieć, a artefaktów.</span><span class="sxs-lookup"><span data-stu-id="3cf22-105">However, hello key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="3cf22-106">Te wstępnie skonfigurowane ustawienia są skonfigurowane z wartościami domyślnymi, które mogą zostać zastąpione w czasie hello tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3cf22-106">These preconfigured settings are set up with default values that can be overridden at hello time of VM creation.</span></span> <span data-ttu-id="3cf22-107">W tym artykule opisano niektóre zalety hello (specjalistów) wady i zalety (wad) toousing niestandardowych obrazów i przy użyciu formuły.</span><span class="sxs-lookup"><span data-stu-id="3cf22-107">This article explains some of hello advantages (pros) and disadvantages (cons) toousing custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="3cf22-108">Obraz niestandardowy zalet i wad</span><span class="sxs-lookup"><span data-stu-id="3cf22-108">Custom image pros and cons</span></span>
<span data-ttu-id="3cf22-109">Niestandardowe obrazy zapewniają toocreate statycznych, niezmienne sposób maszyn wirtualnych z wymagane środowisko.</span><span class="sxs-lookup"><span data-stu-id="3cf22-109">Custom images provide a static, immutable way toocreate VMs from a desired environment.</span></span> 

<span data-ttu-id="3cf22-110">**Specjaliści**</span><span class="sxs-lookup"><span data-stu-id="3cf22-110">**Pros**</span></span>

* <span data-ttu-id="3cf22-111">Obsługi z niestandardowego obrazu maszyny Wirtualnej jest szybkie, ponieważ nic nie zmieni się po powitalne przejścia maszyny Wirtualnej z obrazu hello.</span><span class="sxs-lookup"><span data-stu-id="3cf22-111">VM provisioning from a custom image is fast as nothing changes after hello VM is spun up from hello image.</span></span> <span data-ttu-id="3cf22-112">Innymi słowy nie ma żadnych tooapply ustawienia jako obraz niestandardowy hello jest tylko obraz bez ustawień.</span><span class="sxs-lookup"><span data-stu-id="3cf22-112">In other words, there are no settings tooapply as hello custom image is just an image without settings.</span></span> 
* <span data-ttu-id="3cf22-113">Maszyny wirtualne utworzone za pomocą pojedynczego obrazu niestandardowego są identyczne.</span><span class="sxs-lookup"><span data-stu-id="3cf22-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="3cf22-114">**Cons**</span><span class="sxs-lookup"><span data-stu-id="3cf22-114">**Cons**</span></span>

* <span data-ttu-id="3cf22-115">Należy tooupdate pewien aspekt niestandardowy obraz powitania obraz powitania muszą zostać ponownie utworzone.</span><span class="sxs-lookup"><span data-stu-id="3cf22-115">If you need tooupdate some aspect of hello custom image, hello image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="3cf22-116">Formuły zalet i wad</span><span class="sxs-lookup"><span data-stu-id="3cf22-116">Formula pros and cons</span></span>
<span data-ttu-id="3cf22-117">Formuły zapewniają toocreate dynamiczny sposób maszyn wirtualnych z ustawienia konfiguracji hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="3cf22-117">Formulas provide a dynamic way toocreate VMs from hello desired configuration/settings.</span></span>

<span data-ttu-id="3cf22-118">**Specjaliści**</span><span class="sxs-lookup"><span data-stu-id="3cf22-118">**Pros**</span></span>

* <span data-ttu-id="3cf22-119">Zmiany w środowisku hello można przechwycić na bieżąco hello za pośrednictwem artefaktów.</span><span class="sxs-lookup"><span data-stu-id="3cf22-119">Changes in hello environment can be captured on hello fly via artifacts.</span></span> <span data-ttu-id="3cf22-120">Na przykład, jeśli mają zainstalowane najnowsze bitów hello z potoku sieci wersji maszyny Wirtualnej lub zarejestrować hello najnowsze kodu z repozytorium, można po prostu określić artefaktu, który wdraża bitów najnowsze hello lub rejestruje hello najnowsze kodu w formule hello razem z docelowy obrazu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="3cf22-120">For example, if you want a VM installed with hello latest bits from your release pipeline or enlist hello latest code from your repository, you can simply specify an artifact that deploys hello latest bits or enlists hello latest code in hello formula together with a target base image.</span></span> <span data-ttu-id="3cf22-121">Zawsze, gdy w tej formule jest używany toocreate maszyn wirtualnych, hello najnowsze bity/kodu są wdrożone pozyskać toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3cf22-121">Whenever this formula is used toocreate VMs, hello latest bits/code are deployed/enlisted toohello VM.</span></span> 
* <span data-ttu-id="3cf22-122">Formuły można zdefiniować ustawienia domyślne, których nie może dostarczyć niestandardowe obrazy — takich jak ustawienia sieci wirtualnej i rozmiarów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3cf22-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="3cf22-123">Ustawienia Hello zapisane w formule są wyświetlane jako wartości domyślne, ale można zmodyfikować po utworzeniu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3cf22-123">hello settings saved in a formula are shown as default values, but can be modified when hello VM is created.</span></span> 

<span data-ttu-id="3cf22-124">**Cons**</span><span class="sxs-lookup"><span data-stu-id="3cf22-124">**Cons**</span></span>

* <span data-ttu-id="3cf22-125">Tworzenie maszyny Wirtualnej na podstawie formuły może zająć więcej czasu niż tworzenia maszyny Wirtualnej z obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="3cf22-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="3cf22-126">Wpisy na blogu pokrewne</span><span class="sxs-lookup"><span data-stu-id="3cf22-126">Related blog posts</span></span>
* [<span data-ttu-id="3cf22-127">Niestandardowe obrazy lub formuł?</span><span class="sxs-lookup"><span data-stu-id="3cf22-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="3cf22-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3cf22-128">Next steps</span></span>
- [<span data-ttu-id="3cf22-129">DevTest Labs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="3cf22-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)