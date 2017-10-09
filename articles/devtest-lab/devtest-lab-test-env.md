---
title: "aaaUse Azure DevTest Labs dla maszyny Wirtualnej i PaaS test środowisk | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Azure DevTest Labs dla maszyny Wirtualnej i PaaS przetestować scenariusze środowiska."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="b7d91-103">Użyj Azure DevTest Labs dla maszyny Wirtualnej i PaaS test środowisk</span><span class="sxs-lookup"><span data-stu-id="b7d91-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="b7d91-104">Azure DevTest Labs tooimplement można używać wielu różnych kluczowych scenariuszy, ale podstawowego scenariusza polega na użyciu DevTest Labs toohost maszyny dla testerów.</span><span class="sxs-lookup"><span data-stu-id="b7d91-104">You can use Azure DevTest Labs tooimplement many key scenarios, but a primary scenario involves using DevTest Labs toohost machines for testers.</span></span> 

<span data-ttu-id="b7d91-105">W tym scenariuszu DevTest Labs zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b7d91-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="b7d91-106">Testerów przetestować najnowszą wersję aplikacji hello szybkie Inicjowanie obsługi środowisk systemu Windows i Linux za pomocą szablonów wielokrotnego użytku i artefaktów.</span><span class="sxs-lookup"><span data-stu-id="b7d91-106">Testers can test hello latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="b7d91-107">Testerów można zwiększać ich przez Inicjowanie obsługi wielu agentów testowych do testowania obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b7d91-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="b7d91-108">Administratorzy mogą kontrolować koszty przez zapewnienie, że:</span><span class="sxs-lookup"><span data-stu-id="b7d91-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="b7d91-109">Testerów nie można pobrać więcej maszyn wirtualnych, niż jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="b7d91-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="b7d91-110">Maszyny wirtualne są zamknięte podczas nieużywany.</span><span class="sxs-lookup"><span data-stu-id="b7d91-110">VMs are shut down when not in use.</span></span>

![Użyć do trenowania DevTest Labs](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="b7d91-112">W tym artykule informacje o różnych wymaganiach tester toomeet funkcji Azure DevTest Labs i hello tooset toofollow szczegółowy opis kroków, tworząc laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b7d91-112">In this article, you learn about various Azure DevTest Labs features used toomeet tester requirements and hello detailed steps toofollow tooset up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="b7d91-113">Implementowanie środowiska testowego o usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b7d91-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="b7d91-114">**Tworzenie laboratorium hello**</span><span class="sxs-lookup"><span data-stu-id="b7d91-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="b7d91-115">Laboratoria są hello punkt początkowy w usłudze Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="b7d91-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="b7d91-116">Po utworzeniu laboratorium, można wykonać zadania, takie jak dodawanie laboratorium toohello użytkowników (testerów), ustawienia zasad toocontrol kosztów, definiowanie obrazów maszyn wirtualnych, które można szybko utworzyć i inne.</span><span class="sxs-lookup"><span data-stu-id="b7d91-116">Once you create a lab, you can perform tasks such as adding users (testers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="b7d91-117">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b7d91-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b7d91-118">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b7d91-118">Task</span></span> | <span data-ttu-id="b7d91-119">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b7d91-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b7d91-120">Tworzenie laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b7d91-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="b7d91-121">Dowiedz się, jak toocreate a laboratorium w usłudze Azure DevTest Labs w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b7d91-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="b7d91-122">**Tworzenie maszyn wirtualnych w kilka minut przy użyciu gotowych marketplace obrazów i niestandardowych obrazów**</span><span class="sxs-lookup"><span data-stu-id="b7d91-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="b7d91-123">Możesz pobrania gotowych obrazów z szerokiej gamy obrazów w portalu Azure Marketplace hello i udostępnić je w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="b7d91-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="b7d91-124">Jeśli obrazy gotowe hello nie spełniają wymagań, można utworzyć niestandardowy obraz przez utworzenie maszyny Wirtualnej przy użyciu gotowych obrazu z portalu Azure Marketplace, instalowanie całe oprogramowanie hello, które są potrzebne, i zapisywanie hello maszyny Wirtualnej jako obraz niestandardowy w laboratorium hello laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b7d91-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="b7d91-125">Jeśli będziesz używać niestandardowych obrazów, należy rozważyć użycie toocreate fabryki obrazu i dystrybucji obrazów.</span><span class="sxs-lookup"><span data-stu-id="b7d91-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="b7d91-126">Fabryka obrazu jest rozwiązanie konfiguracji jako kod, który regularnie tworzy i rozpowszechnia obrazy skonfigurowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b7d91-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="b7d91-127">Ta zapisuje hello czas toomanually skonfigurować system powitania po utworzeniu maszyny Wirtualnej z hello podstawowego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b7d91-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="b7d91-128">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b7d91-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b7d91-129">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b7d91-129">Task</span></span> | <span data-ttu-id="b7d91-130">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b7d91-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b7d91-131">Konfigurowanie portalu Azure Marketplace obrazów</span><span class="sxs-lookup"><span data-stu-id="b7d91-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="b7d91-132">Informacje na temat dozwolonych obrazów Azure Marketplace, udostępniając wybór tylko hello obrazów dla testerów hello.</span><span class="sxs-lookup"><span data-stu-id="b7d91-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello testers.</span></span>|
   | [<span data-ttu-id="b7d91-133">Tworzenie niestandardowego obrazu</span><span class="sxs-lookup"><span data-stu-id="b7d91-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="b7d91-134">Tworzenie niestandardowego obrazu wstępnie instalując oprogramowanie hello, potrzebne, aby testerów może szybko utworzyć Maszynę wirtualną przy użyciu hello niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="b7d91-134">Create a custom image by pre-installing hello software you need so that testers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="b7d91-135">Więcej informacji na temat fabryki obrazu</span><span class="sxs-lookup"><span data-stu-id="b7d91-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="b7d91-136">Obejrzyj klip wideo, który opisuje sposób tooset Konfigurowanie i użyj fabrykę obrazu.</span><span class="sxs-lookup"><span data-stu-id="b7d91-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="b7d91-137">**Tworzenie szablonów wielokrotnego użytku dla maszyny testowe**</span><span class="sxs-lookup"><span data-stu-id="b7d91-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="b7d91-138">Formuła w usłudze Azure DevTest Labs jest lista domyślnych wartości właściwości używanych toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b7d91-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="b7d91-139">Wybieranie obrazu, rozmiar maszyny Wirtualnej (kombinacja Procesora i pamięci RAM) i sieć wirtualną można utworzyć formuły w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="b7d91-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="b7d91-140">Każdy tester można Zobacz hello formuły w laboratorium hello i użyć toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b7d91-140">Each tester can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="b7d91-141">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b7d91-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b7d91-142">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b7d91-142">Task</span></span> | <span data-ttu-id="b7d91-143">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b7d91-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b7d91-144">Zarządzanie DevTest Labs formuły toocreate maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="b7d91-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="b7d91-145">Dowiedz się, jak utworzyć formuły przez przechwycenie obrazu, rozmiar maszyny Wirtualnej (kombinację procesora CPU i pamięci RAM) i sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b7d91-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="b7d91-146">**Tworzenie wielu maszyn wirtualnych środowisk testowych.**</span><span class="sxs-lookup"><span data-stu-id="b7d91-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="b7d91-147">Można użyć usługi Azure Resource Manager szablony toodefine hello infrastrukturze i konfiguracji rozwiązania Azure i wielokrotnie wdrażać testu wiele maszyn wirtualnych w spójnym stanie.</span><span class="sxs-lookup"><span data-stu-id="b7d91-147">You can use Azure Resource Manager templates toodefine hello infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="b7d91-148">Zasoby platformy Azure PaaS można udostępnić w środowisku z szablonem usługi Resource Manager i widoczny w śledzenie kosztów.</span><span class="sxs-lookup"><span data-stu-id="b7d91-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="b7d91-149">Jednak maszyna wirtualna automatycznego zamykania nie ma zastosowania tooPaaS zasobów.</span><span class="sxs-lookup"><span data-stu-id="b7d91-149">However, VM auto shutdown does not apply tooPaaS resources.</span></span>

    <span data-ttu-id="b7d91-150">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b7d91-150">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b7d91-151">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b7d91-151">Task</span></span> | <span data-ttu-id="b7d91-152">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b7d91-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b7d91-153">Tworzenie środowisk z wieloma maszynami wirtualnymi i zasobów PaaS za pomocą szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b7d91-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="b7d91-154">Dowiedz się, jak można wdrożyć wiele maszyn wirtualnych w spójnym stanie dla danego środowiska testowego.</span><span class="sxs-lookup"><span data-stu-id="b7d91-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="b7d91-155">**Tworzenie artefaktów tooenable elastyczne dostosowanie maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="b7d91-155">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="b7d91-156">Artefakty są używane toodeploy i konfigurowania aplikacji po zainicjowaniu obsługi maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b7d91-156">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="b7d91-157">Artefaktami mogą być:</span><span class="sxs-lookup"><span data-stu-id="b7d91-157">Artifacts can be:</span></span>

   - <span data-ttu-id="b7d91-158">Narzędzia, które mają tooinstall na powitania maszyny Wirtualnej — np. agenci, program Fiddler i program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b7d91-158">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="b7d91-159">Akcje, które mają toorun na powitania maszyny Wirtualnej — np. klonowanie repozytorium.</span><span class="sxs-lookup"><span data-stu-id="b7d91-159">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="b7d91-160">Aplikacje, które mają tootest.</span><span class="sxs-lookup"><span data-stu-id="b7d91-160">Applications that you want tootest.</span></span>

   <span data-ttu-id="b7d91-161">Wiele artefakty są już dostępne out-of--box.</span><span class="sxs-lookup"><span data-stu-id="b7d91-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="b7d91-162">Ale jeśli chcesz więcej dostosowania do określonych potrzeb, możesz utworzyć własne niestandardowe artefakty.</span><span class="sxs-lookup"><span data-stu-id="b7d91-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="b7d91-163">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b7d91-163">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b7d91-164">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b7d91-164">Task</span></span> | <span data-ttu-id="b7d91-165">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b7d91-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b7d91-166">Tworzenie niestandardowych artefaktów dla maszyny Wirtualnej DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b7d91-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="b7d91-167">Tworzenie własnych niestandardowych artefaktów dla maszyn wirtualnych hello w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b7d91-167">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="b7d91-168">Dodaj Git artefakty niestandardowych toostore repozytorium i szablony usługi Azure Resource Manager do użycia w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b7d91-168">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="b7d91-169">Dowiedz się, jak toostore Twojego niestandardowe artefakty w własne prywatne repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="b7d91-169">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="b7d91-170">**Kontrolę kosztów**</span><span class="sxs-lookup"><span data-stu-id="b7d91-170">**Control costs**</span></span>
   
    <span data-ttu-id="b7d91-171">Azure DevTest Labs umożliwia tooset zasady w hello laboratorium toospecify hello maksymalną liczbę maszyn wirtualnych, które mogą być tworzone przez tester w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="b7d91-171">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a tester in hello lab.</span></span> 
   
    <span data-ttu-id="b7d91-172">Jeśli zespół testu ma zestaw harmonogram pracy i mają toostop wszystkich hello maszyn wirtualnych o określonej godzinie dnia hello, a następnie automatycznie uruchomić je ponownie hello dnia, można łatwo wykonywać który przez ustawienie automatyczne zamykanie automatyczne uruchamianie zasad i w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="b7d91-172">If your test team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="b7d91-173">Na koniec po zakończeniu tworzenia aplikacji można usunąć wszystkich hello maszyn wirtualnych jednocześnie za pomocą jednego skryptu środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7d91-173">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="b7d91-174">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b7d91-174">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b7d91-175">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b7d91-175">Task</span></span> | <span data-ttu-id="b7d91-176">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b7d91-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b7d91-177">Definiowanie zasad laboratorium</span><span class="sxs-lookup"><span data-stu-id="b7d91-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="b7d91-178">Kontrolę kosztów przez ustawienie zasad w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="b7d91-178">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="b7d91-179">Usuń wszystkie laboratorium hello maszyn wirtualnych za pomocą skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7d91-179">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="b7d91-180">Po zakończeniu testowania, należy usunąć wszystkie laboratoria hello w jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="b7d91-180">Delete all hello labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="b7d91-181">**Dodaj tooa sieci wirtualnej laboratorium**</span><span class="sxs-lookup"><span data-stu-id="b7d91-181">**Add a virtual network tooa Lab**</span></span> 
   
    <span data-ttu-id="b7d91-182">DevTest Labs tworzy nową sieć wirtualną (VNET), przy każdym utworzeniu laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b7d91-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="b7d91-183">Jeśli skonfigurowano własnych sieci Wirtualnej — np. za pomocą programu ExpressRoute lub sieci VPN typu lokacja lokacja — można dodać tej sieci Wirtualnej laboratorium tooyour ustawień sieci wirtualnej, aby była dostępna podczas tworzenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b7d91-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="b7d91-184">Ponadto jest usługa Azure Active Directory domeny sprzężenia artefaktu dostępne której jest przyłączany do domeny tooa maszyny Wirtualnej po utworzeniu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b7d91-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="b7d91-185">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b7d91-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b7d91-186">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b7d91-186">Task</span></span> | <span data-ttu-id="b7d91-187">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b7d91-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b7d91-188">Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b7d91-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="b7d91-189">Dowiedz się, jak tooconfigure sieci wirtualnej w usłudze Azure DevTest Labs przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b7d91-189">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="b7d91-190">**Udostępnij laboratorium hello każdego tester**</span><span class="sxs-lookup"><span data-stu-id="b7d91-190">**Share hello lab with each tester**</span></span>
   
    <span data-ttu-id="b7d91-191">Laboratoria są bezpośrednio dostępne przy użyciu łącza, które są udostępniane z testerów.</span><span class="sxs-lookup"><span data-stu-id="b7d91-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="b7d91-192">Ich nie muszą nawet być toohave konta platformy Azure, jak długo mają [konta Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="b7d91-192">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="b7d91-193">Testerów nie widzi maszyny wirtualne utworzone przez inne testerów.</span><span class="sxs-lookup"><span data-stu-id="b7d91-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="b7d91-194">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b7d91-194">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b7d91-195">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b7d91-195">Task</span></span> | <span data-ttu-id="b7d91-196">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b7d91-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b7d91-197">Dodawanie laboratorium tooa tester w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b7d91-197">Add a tester tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="b7d91-198">Użyj hello Azure tooadd portalu testerów tooyour laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b7d91-198">Use hello Azure portal tooadd testers tooyour lab.</span></span>|
   | [<span data-ttu-id="b7d91-199">Dodawanie laboratorium toohello testerów przy użyciu skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7d91-199">Add testers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="b7d91-200">Za pomocą programu PowerShell tooautomate Dodawanie laboratorium tooyour testerów.</span><span class="sxs-lookup"><span data-stu-id="b7d91-200">Use PowerShell tooautomate adding testers tooyour lab.</span></span> |
   | [<span data-ttu-id="b7d91-201">Uzyskaj link toohello laboratorium</span><span class="sxs-lookup"><span data-stu-id="b7d91-201">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="b7d91-202">Dowiedz się, jak testerów bezpośrednio uzyskać dostęp za pośrednictwem hiperłącze laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b7d91-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="b7d91-203">**Zautomatyzować tworzenie laboratorium więcej zespołów**</span><span class="sxs-lookup"><span data-stu-id="b7d91-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="b7d91-204">Można zautomatyzować tworzenie laboratorium, ustawienia niestandardowe, w tym tworzenia szablonu usługi Resource Manager i używając jej labs identyczne toocreate wielokrotnie.</span><span class="sxs-lookup"><span data-stu-id="b7d91-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="b7d91-205">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b7d91-205">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b7d91-206">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b7d91-206">Task</span></span> | <span data-ttu-id="b7d91-207">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b7d91-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b7d91-208">Tworzenie laboratorium przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b7d91-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="b7d91-209">Utwórz laboratoriów w usłudze Azure DevTest Labs za pomocą szablonów usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b7d91-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

