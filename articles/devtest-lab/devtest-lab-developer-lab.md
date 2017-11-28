---
title: "aaaUse Azure DevTest Labs dla deweloperów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Azure DevTest Labs dla deweloperów."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: 16a3ef47c9fcbca3050dd50db5b472a9a1e3c62c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="b9e5d-103">Użyj Azure DevTest Labs dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="b9e5d-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="b9e5d-104">Azure DevTest Labs mogą być używane tooimplement wiele kluczowych scenariuszy, ale jeden z hello podstawowe scenariusze polega na użyciu DevTest Labs toohost programowanie maszyny dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-104">Azure DevTest Labs can be used tooimplement many key scenarios, but one of hello primary scenarios involves using DevTest Labs toohost development machines for developers.</span></span> <span data-ttu-id="b9e5d-105">W tym scenariuszu DevTest Labs zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b9e5d-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="b9e5d-106">Deweloperzy mogą szybko ustanowić maszynami programowanie na żądanie.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="b9e5d-107">Deweloperzy można łatwo dostosować ich maszyn rozwój w miarę potrzeby.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="b9e5d-108">Administratorzy mogą kontrolować koszty przez zapewnienie, że:</span><span class="sxs-lookup"><span data-stu-id="b9e5d-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="b9e5d-109">Deweloperzy nie można pobrać więcej maszyn wirtualnych, niż jest to wymagane do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="b9e5d-110">Maszyny wirtualne są zamknięte podczas nieużywany.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-110">VMs are shut down when not in use.</span></span> 

![Użyć do trenowania DevTest Labs](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="b9e5d-112">W tym artykule dowiesz się o różnych funkcjach Azure DevTest Labs, które można toomeet używane developer wymagania i hello szczegółowy opis kroków, wykonać tooset się laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-112">In this article, you learn about various Azure DevTest Labs features that can be used toomeet developer requirements and hello detailed steps that you can follow tooset up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="b9e5d-113">Implementowanie środowiska dewelopera z Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b9e5d-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="b9e5d-114">**Tworzenie laboratorium hello**</span><span class="sxs-lookup"><span data-stu-id="b9e5d-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="b9e5d-115">Laboratoria są hello punkt początkowy w usłudze Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="b9e5d-116">Po utworzeniu laboratorium, można wykonać zadania, takie jak dodawanie laboratorium toohello użytkowników (deweloperzy), ustawienia zasad toocontrol kosztów, definiowanie obrazów maszyn wirtualnych, które można szybko utworzyć i inne.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-116">Once you create a lab, you can perform tasks such as adding users (developers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="b9e5d-117">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b9e5d-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b9e5d-118">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b9e5d-118">Task</span></span> | <span data-ttu-id="b9e5d-119">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b9e5d-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b9e5d-120">Tworzenie laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b9e5d-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="b9e5d-121">Dowiedz się, jak toocreate a laboratorium w usłudze Azure DevTest Labs w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="b9e5d-122">**Tworzenie maszyn wirtualnych w kilka minut przy użyciu gotowych marketplace obrazów i niestandardowych obrazów**</span><span class="sxs-lookup"><span data-stu-id="b9e5d-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="b9e5d-123">Możesz pobrania gotowych obrazów z szerokiej gamy obrazów w portalu Azure Marketplace hello i udostępnić je w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="b9e5d-124">Jeśli obrazy gotowe hello nie spełniają wymagań, można utworzyć niestandardowy obraz przez utworzenie maszyny Wirtualnej przy użyciu gotowych obrazu z portalu Azure Marketplace, instalowanie całe oprogramowanie hello, które są potrzebne, i zapisywanie hello maszyny Wirtualnej jako obraz niestandardowy w laboratorium hello laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="b9e5d-125">Jeśli będziesz używać niestandardowych obrazów, należy rozważyć użycie toocreate fabryki obrazu i dystrybucji obrazów.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="b9e5d-126">Fabryka obrazu jest rozwiązanie konfiguracji jako kod, który regularnie tworzy i rozpowszechnia obrazy skonfigurowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="b9e5d-127">Ta zapisuje hello czas toomanually skonfigurować system powitania po utworzeniu maszyny Wirtualnej z hello podstawowego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="b9e5d-128">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b9e5d-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b9e5d-129">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b9e5d-129">Task</span></span> | <span data-ttu-id="b9e5d-130">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b9e5d-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b9e5d-131">Konfigurowanie portalu Azure Marketplace obrazów</span><span class="sxs-lookup"><span data-stu-id="b9e5d-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="b9e5d-132">Informacje na temat dozwolonych obrazów Azure Marketplace, udostępniając wybór tylko hello obrazów interesujące dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello developers.</span></span>|
   | [<span data-ttu-id="b9e5d-133">Tworzenie niestandardowego obrazu</span><span class="sxs-lookup"><span data-stu-id="b9e5d-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="b9e5d-134">Tworzenie niestandardowego obrazu wstępnie instalując oprogramowanie hello, które są potrzebne, dzięki czemu deweloperzy mogą szybko tworzyć Maszynę wirtualną przy użyciu niestandardowego obrazu hello.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-134">Create a custom image by pre-installing hello software you need so that developers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="b9e5d-135">Więcej informacji na temat fabryki obrazu</span><span class="sxs-lookup"><span data-stu-id="b9e5d-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="b9e5d-136">Obejrzyj klip wideo, który opisuje sposób tooset Konfigurowanie i użyj fabrykę obrazu.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="b9e5d-137">**Tworzenie szablonów wielokrotnego użytku na komputerach deweloperów**</span><span class="sxs-lookup"><span data-stu-id="b9e5d-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="b9e5d-138">Formuła w usłudze Azure DevTest Labs jest lista domyślnych wartości właściwości używanych toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="b9e5d-139">Wybieranie obrazu, rozmiar maszyny Wirtualnej (kombinacja Procesora i pamięci RAM) i sieć wirtualną można utworzyć formuły w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="b9e5d-140">Każdy deweloper można Zobacz hello formuły w laboratorium hello i użyć toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-140">Each developer can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="b9e5d-141">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b9e5d-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b9e5d-142">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b9e5d-142">Task</span></span> | <span data-ttu-id="b9e5d-143">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b9e5d-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b9e5d-144">Zarządzanie DevTest Labs formuły toocreate maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="b9e5d-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="b9e5d-145">Dowiedz się, jak utworzyć formuły przez przechwycenie obrazu, rozmiar maszyny Wirtualnej (kombinację procesora CPU i pamięci RAM) i sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="b9e5d-146">**Tworzenie artefaktów tooenable elastyczne dostosowanie maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="b9e5d-146">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="b9e5d-147">Artefakty są używane toodeploy i konfigurowania aplikacji po zainicjowaniu obsługi maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-147">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="b9e5d-148">Artefaktami mogą być:</span><span class="sxs-lookup"><span data-stu-id="b9e5d-148">Artifacts can be:</span></span>

   - <span data-ttu-id="b9e5d-149">Narzędzia, które mają tooinstall na powitania maszyny Wirtualnej — np. agenci, program Fiddler i program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-149">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="b9e5d-150">Akcje, które mają toorun na powitania maszyny Wirtualnej — np. klonowanie repozytorium.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-150">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="b9e5d-151">Aplikacje, które mają tootest.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-151">Applications that you want tootest.</span></span>

   <span data-ttu-id="b9e5d-152">Wiele artefakty są już dostępne out-of--box.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="b9e5d-153">Można utworzyć własne niestandardowe artefakty, jeśli chcesz więcej dostosowania do określonych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="b9e5d-154">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b9e5d-154">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b9e5d-155">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b9e5d-155">Task</span></span> | <span data-ttu-id="b9e5d-156">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b9e5d-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b9e5d-157">Tworzenie niestandardowych artefaktów dla maszyny Wirtualnej DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b9e5d-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="b9e5d-158">Tworzenie własnych niestandardowych artefaktów dla maszyn wirtualnych hello w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-158">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="b9e5d-159">Dodaj Git artefakty niestandardowych toostore repozytorium i szablony usługi Azure Resource Manager do użycia w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b9e5d-159">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="b9e5d-160">Dowiedz się, jak toostore Twojego niestandardowe artefakty w własne prywatne repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-160">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="b9e5d-161">**Kontrolę kosztów**</span><span class="sxs-lookup"><span data-stu-id="b9e5d-161">**Control costs**</span></span>
   
    <span data-ttu-id="b9e5d-162">Azure DevTest Labs umożliwia tooset zasady w hello laboratorium toospecify hello maksymalną liczbę maszyn wirtualnych, które mogą być tworzone przez deweloperów w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-162">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a developer in hello lab.</span></span> 
   
    <span data-ttu-id="b9e5d-163">Jeśli zespół deweloperów ma zestaw harmonogram pracy i mają toostop wszystkich hello maszyn wirtualnych o określonej godzinie dnia hello, a następnie automatycznie uruchomić je ponownie hello dnia, można łatwo wykonywać który przez ustawienie automatyczne zamykanie automatyczne uruchamianie zasad i w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-163">If your developer team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="b9e5d-164">Na koniec po zakończeniu tworzenia aplikacji można usunąć wszystkich hello maszyn wirtualnych jednocześnie za pomocą jednego skryptu środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-164">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="b9e5d-165">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b9e5d-165">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b9e5d-166">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b9e5d-166">Task</span></span> | <span data-ttu-id="b9e5d-167">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b9e5d-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b9e5d-168">Definiowanie zasad laboratorium</span><span class="sxs-lookup"><span data-stu-id="b9e5d-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="b9e5d-169">Kontrolę kosztów przez ustawienie zasad w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-169">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="b9e5d-170">Usuń wszystkie laboratorium hello maszyn wirtualnych za pomocą skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9e5d-170">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="b9e5d-171">Po zakończeniu tworzenia, należy usunąć wszystkie laboratoria hello w jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-171">Delete all hello labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="b9e5d-172">**Dodaj tooa sieci wirtualnej maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="b9e5d-172">**Add a virtual network tooa VM**</span></span> 
   
    <span data-ttu-id="b9e5d-173">DevTest Labs tworzy nową sieć wirtualną (VNET), przy każdym utworzeniu laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="b9e5d-174">Jeśli skonfigurowano własnych sieci Wirtualnej — np. za pomocą programu ExpressRoute lub sieci VPN typu lokacja lokacja — można dodać tej sieci Wirtualnej laboratorium tooyour ustawień sieci wirtualnej, aby była dostępna podczas tworzenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="b9e5d-175">Ponadto jest dostępny, który będzie przyłączyć się do domeny tooa maszyny Wirtualnej po utworzeniu maszyny Wirtualnej hello artefaktu sprzężenia domeny usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="b9e5d-176">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b9e5d-176">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b9e5d-177">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b9e5d-177">Task</span></span> | <span data-ttu-id="b9e5d-178">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b9e5d-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b9e5d-179">Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b9e5d-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="b9e5d-180">Dowiedz się, jak tooconfigure sieci wirtualnej w usłudze Azure DevTest Labs przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-180">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="b9e5d-181">**Udostępnij laboratorium hello wszystkich deweloperów**</span><span class="sxs-lookup"><span data-stu-id="b9e5d-181">**Share hello lab with each developer**</span></span>
   
    <span data-ttu-id="b9e5d-182">Laboratoria są bezpośrednio dostępne przy użyciu łącza, które są udostępniane deweloperów.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="b9e5d-183">Ich nie muszą nawet być toohave konta platformy Azure, jak długo mają [konta Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="b9e5d-183">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="b9e5d-184">Deweloperzy nie widzi tworzone przez innych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="b9e5d-185">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b9e5d-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b9e5d-186">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b9e5d-186">Task</span></span> | <span data-ttu-id="b9e5d-187">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b9e5d-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b9e5d-188">Dodawanie laboratorium tooa deweloperów w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b9e5d-188">Add a developer tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="b9e5d-189">Użyj hello Azure tooadd portalu deweloperów tooyour laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-189">Use hello Azure portal tooadd developers tooyour lab.</span></span>|
   | [<span data-ttu-id="b9e5d-190">Dodawanie laboratorium toohello deweloperzy przy użyciu skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9e5d-190">Add developers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="b9e5d-191">Użyj Dodawanie laboratorium tooyour deweloperzy tooautomate środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-191">Use PowerShell tooautomate adding developers tooyour lab.</span></span> |
   | [<span data-ttu-id="b9e5d-192">Uzyskaj link toohello laboratorium</span><span class="sxs-lookup"><span data-stu-id="b9e5d-192">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="b9e5d-193">Dowiedz się, jak deweloperzy mogą bezpośrednio uzyskać dostępu do laboratorium za pośrednictwem hiperłącza.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="b9e5d-194">**Zautomatyzować tworzenie laboratorium więcej zespołów**</span><span class="sxs-lookup"><span data-stu-id="b9e5d-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="b9e5d-195">Można zautomatyzować tworzenie laboratorium, ustawienia niestandardowe, w tym tworzenia szablonu usługi Resource Manager i używając jej labs identyczne toocreate wielokrotnie.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="b9e5d-196">Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="b9e5d-196">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="b9e5d-197">Zadanie</span><span class="sxs-lookup"><span data-stu-id="b9e5d-197">Task</span></span> | <span data-ttu-id="b9e5d-198">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="b9e5d-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="b9e5d-199">Tworzenie laboratorium przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b9e5d-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="b9e5d-200">Utwórz laboratoriów w usłudze Azure DevTest Labs za pomocą szablonów usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b9e5d-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

