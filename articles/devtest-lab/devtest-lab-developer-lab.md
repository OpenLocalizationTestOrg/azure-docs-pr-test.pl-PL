---
title: "Użyj Azure DevTest Labs dla deweloperów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi Azure DevTest Labs dla deweloperów."
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
ms.openlocfilehash: c187819e9392908c8979556f80e8c94739eb14d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="a3757-103">Użyj Azure DevTest Labs dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="a3757-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="a3757-104">Azure DevTest Labs umożliwia wdrożenie wielu kluczowych scenariuszy, ale jednego ze scenariuszy głównej polega na użyciu DevTest Labs umożliwiający przechowywanie tam maszyn programowanie dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="a3757-104">Azure DevTest Labs can be used to implement many key scenarios, but one of the primary scenarios involves using DevTest Labs to host development machines for developers.</span></span> <span data-ttu-id="a3757-105">W tym scenariuszu DevTest Labs zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a3757-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="a3757-106">Deweloperzy mogą szybko ustanowić maszynami programowanie na żądanie.</span><span class="sxs-lookup"><span data-stu-id="a3757-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="a3757-107">Deweloperzy można łatwo dostosować ich maszyn rozwój w miarę potrzeby.</span><span class="sxs-lookup"><span data-stu-id="a3757-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="a3757-108">Administratorzy mogą kontrolować koszty przez zapewnienie, że:</span><span class="sxs-lookup"><span data-stu-id="a3757-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="a3757-109">Deweloperzy nie można pobrać więcej maszyn wirtualnych, niż jest to wymagane do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a3757-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="a3757-110">Maszyny wirtualne są zamknięte podczas nieużywany.</span><span class="sxs-lookup"><span data-stu-id="a3757-110">VMs are shut down when not in use.</span></span> 

![Użyć do trenowania DevTest Labs](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="a3757-112">W tym artykule informacje o różnych funkcji Azure DevTest Labs, które mogą służyć do wymagań deweloperów i szczegółowy opis kroków, które można wykonać, aby skonfigurować laboratorium.</span><span class="sxs-lookup"><span data-stu-id="a3757-112">In this article, you learn about various Azure DevTest Labs features that can be used to meet developer requirements and the detailed steps that you can follow to set up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="a3757-113">Implementowanie środowiska dewelopera z Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a3757-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="a3757-114">**Tworzenie laboratorium**</span><span class="sxs-lookup"><span data-stu-id="a3757-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="a3757-115">Laboratoria stanowią punkt początkowy w usłudze Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="a3757-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="a3757-116">Po utworzeniu laboratorium, można wykonywać zadania, takie jak dodawanie użytkowników (deweloperzy) do laboratorium, ustawienie zasad w celu kontrolowania kosztów, definiowanie obrazów maszyn wirtualnych, które można szybko utworzyć i inne.</span><span class="sxs-lookup"><span data-stu-id="a3757-116">Once you create a lab, you can perform tasks such as adding users (developers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="a3757-117">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="a3757-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="a3757-118">Zadanie</span><span class="sxs-lookup"><span data-stu-id="a3757-118">Task</span></span> | <span data-ttu-id="a3757-119">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="a3757-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="a3757-120">Tworzenie laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a3757-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="a3757-121">Dowiedz się, jak tworzenie laboratorium w usłudze Azure DevTest Labs w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a3757-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="a3757-122">**Tworzenie maszyn wirtualnych w kilka minut przy użyciu gotowych marketplace obrazów i niestandardowych obrazów**</span><span class="sxs-lookup"><span data-stu-id="a3757-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="a3757-123">Możesz pobrania gotowych obrazów z szerokiej gamy obrazów w portalu Azure Marketplace i udostępnić je w środowisku laboratoryjnym.</span><span class="sxs-lookup"><span data-stu-id="a3757-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="a3757-124">Jeśli gotowe do użycia obrazy nie spełniają wymagań, można utworzyć niestandardowego obrazu, tworząc laboratorium maszyny Wirtualnej przy użyciu gotowych obrazu z portalu Azure Marketplace, instalacja oprogramowania, które są potrzebne, i zapisywanie maszyny Wirtualnej jako obraz niestandardowy w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="a3757-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="a3757-125">Jeśli będziesz używać niestandardowych obrazów, rozważ użycie fabrykę obrazu do tworzenia i rozpowszechniania obrazów.</span><span class="sxs-lookup"><span data-stu-id="a3757-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="a3757-126">Fabryka obrazu jest rozwiązanie konfiguracji jako kod, który regularnie tworzy i rozpowszechnia obrazy skonfigurowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="a3757-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="a3757-127">Spowoduje to zapisanie czasu, należy ręcznie skonfigurować system po utworzeniu maszyny Wirtualnej z podstawowego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="a3757-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="a3757-128">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="a3757-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="a3757-129">Zadanie</span><span class="sxs-lookup"><span data-stu-id="a3757-129">Task</span></span> | <span data-ttu-id="a3757-130">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="a3757-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="a3757-131">Konfigurowanie portalu Azure Marketplace obrazów</span><span class="sxs-lookup"><span data-stu-id="a3757-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="a3757-132">Informacje na temat dozwolonych portalu Azure Marketplace obrazów, określ, co do wyboru dostępne tylko obrazy dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="a3757-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the developers.</span></span>|
   | [<span data-ttu-id="a3757-133">Tworzenie niestandardowego obrazu</span><span class="sxs-lookup"><span data-stu-id="a3757-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="a3757-134">Tworzenie niestandardowego obrazu za pomocą wstępnie instalacji oprogramowania, które są potrzebne, dzięki czemu deweloperzy mogą szybko utworzyć Maszynę wirtualną przy użyciu niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="a3757-134">Create a custom image by pre-installing the software you need so that developers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="a3757-135">Więcej informacji na temat fabryki obrazu</span><span class="sxs-lookup"><span data-stu-id="a3757-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="a3757-136">Obejrzyj klip wideo, który opisuje sposób konfigurowania i używania fabrykę obrazu.</span><span class="sxs-lookup"><span data-stu-id="a3757-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="a3757-137">**Tworzenie szablonów wielokrotnego użytku na komputerach deweloperów**</span><span class="sxs-lookup"><span data-stu-id="a3757-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="a3757-138">Formuła w usłudze Azure DevTest Labs znajduje się lista domyślnych wartości właściwości używany do tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a3757-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="a3757-139">Wybieranie obrazu, rozmiar maszyny Wirtualnej (kombinacja Procesora i pamięci RAM) i sieć wirtualną można utworzyć formuły w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="a3757-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="a3757-140">Każdy deweloper może formuła w laboratorium i go użyć do utworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a3757-140">Each developer can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="a3757-141">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="a3757-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="a3757-142">Zadanie</span><span class="sxs-lookup"><span data-stu-id="a3757-142">Task</span></span> | <span data-ttu-id="a3757-143">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="a3757-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="a3757-144">Zarządzanie DevTest Labs formuły można utworzyć maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="a3757-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="a3757-145">Dowiedz się, jak utworzyć formuły przez przechwycenie obrazu, rozmiar maszyny Wirtualnej (kombinację procesora CPU i pamięci RAM) i sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a3757-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="a3757-146">**Tworzenie artefaktów, aby umożliwić elastyczne dostosowanie maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="a3757-146">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="a3757-147">Artefakty służą do wdrażania i konfigurowania aplikacji po zainicjowaniu obsługi maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a3757-147">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="a3757-148">Artefaktami mogą być:</span><span class="sxs-lookup"><span data-stu-id="a3757-148">Artifacts can be:</span></span>

   - <span data-ttu-id="a3757-149">Narzędzia, które chcesz zainstalować na maszynie Wirtualnej — np. agenci, program Fiddler i program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3757-149">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="a3757-150">Akcje, które chcesz uruchomić na maszynie Wirtualnej — np. klonowanie repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a3757-150">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="a3757-151">Aplikacje, które chcesz przetestować.</span><span class="sxs-lookup"><span data-stu-id="a3757-151">Applications that you want to test.</span></span>

   <span data-ttu-id="a3757-152">Wiele artefakty są już dostępne out-of--box.</span><span class="sxs-lookup"><span data-stu-id="a3757-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="a3757-153">Można utworzyć własne niestandardowe artefakty, jeśli chcesz więcej dostosowania do określonych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="a3757-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="a3757-154">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="a3757-154">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="a3757-155">Zadanie</span><span class="sxs-lookup"><span data-stu-id="a3757-155">Task</span></span> | <span data-ttu-id="a3757-156">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="a3757-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="a3757-157">Tworzenie niestandardowych artefaktów dla maszyny Wirtualnej DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a3757-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="a3757-158">Tworzenie własnych niestandardowych artefaktów dla maszyn wirtualnych w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="a3757-158">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="a3757-159">Dodaj repozytorium Git do przechowywania niestandardowych artefaktów i szablony usługi Azure Resource Manager do użycia w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a3757-159">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="a3757-160">Dowiedz się, jak zapisać Twoje niestandardowe artefakty w własne prywatne repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="a3757-160">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="a3757-161">**Kontrolę kosztów**</span><span class="sxs-lookup"><span data-stu-id="a3757-161">**Control costs**</span></span>
   
    <span data-ttu-id="a3757-162">Azure DevTest Labs umożliwia ustawienie zasad w środowisku laboratoryjnym, aby określić maksymalną liczbę maszyn wirtualnych, które mogą zostać utworzone przez dewelopera w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="a3757-162">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a developer in the lab.</span></span> 
   
    <span data-ttu-id="a3757-163">Jeśli zespół deweloperów zawiera zestaw pracy harmonogramu i chcesz zatrzymanie wszystkich maszyn wirtualnych o określonej godzinie dnia, a następnie automatycznie uruchomić je ponownie następnego dnia, można łatwo realizacji tego przez ustawienie zasad automatycznego zamykania i automatycznego uruchamiania w środowisku laboratoryjnym.</span><span class="sxs-lookup"><span data-stu-id="a3757-163">If your developer team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="a3757-164">Na koniec po zakończeniu tworzenia aplikacji, można usunąć wszystkich maszyn wirtualnych jednocześnie za pomocą jednego skryptu środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3757-164">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="a3757-165">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="a3757-165">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="a3757-166">Zadanie</span><span class="sxs-lookup"><span data-stu-id="a3757-166">Task</span></span> | <span data-ttu-id="a3757-167">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="a3757-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="a3757-168">Definiowanie zasad laboratorium</span><span class="sxs-lookup"><span data-stu-id="a3757-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="a3757-169">Kontrolę kosztów przez ustawienie zasad w środowisku laboratoryjnym.</span><span class="sxs-lookup"><span data-stu-id="a3757-169">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="a3757-170">Usuń wszystkie laboratorium maszyn wirtualnych za pomocą skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3757-170">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="a3757-171">Po zakończeniu tworzenia, należy usunąć wszystkie laboratoriów w ramach jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="a3757-171">Delete all the labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="a3757-172">**Dodawanie sieci wirtualnej do maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="a3757-172">**Add a virtual network to a VM**</span></span> 
   
    <span data-ttu-id="a3757-173">DevTest Labs tworzy nową sieć wirtualną (VNET), przy każdym utworzeniu laboratorium.</span><span class="sxs-lookup"><span data-stu-id="a3757-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="a3757-174">Jeśli skonfigurowano własnych sieci Wirtualnej — np. za pomocą programu ExpressRoute lub sieci VPN typu lokacja lokacja — można dodać tej sieci Wirtualnej do ustawień sieci wirtualnej środowiska laboratoryjnego, aby była dostępna podczas tworzenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a3757-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="a3757-175">Ponadto jest dostępny, które zostaną dołączone Maszynę wirtualną do domeny po utworzeniu maszyny Wirtualnej artefaktu sprzężenia domeny usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a3757-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="a3757-176">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="a3757-176">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="a3757-177">Zadanie</span><span class="sxs-lookup"><span data-stu-id="a3757-177">Task</span></span> | <span data-ttu-id="a3757-178">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="a3757-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="a3757-179">Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a3757-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="a3757-180">Dowiedz się, jak skonfigurować sieć wirtualną w usłudze Azure DevTest Labs przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a3757-180">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="a3757-181">**Udostępnij laboratorium wszystkich deweloperów**</span><span class="sxs-lookup"><span data-stu-id="a3757-181">**Share the lab with each developer**</span></span>
   
    <span data-ttu-id="a3757-182">Laboratoria są bezpośrednio dostępne przy użyciu łącza, które są udostępniane deweloperów.</span><span class="sxs-lookup"><span data-stu-id="a3757-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="a3757-183">Nie nawet muszą oni mieć konto platformy Azure, jak długo mają [konta Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="a3757-183">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="a3757-184">Deweloperzy nie widzi tworzone przez innych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a3757-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="a3757-185">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="a3757-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="a3757-186">Zadanie</span><span class="sxs-lookup"><span data-stu-id="a3757-186">Task</span></span> | <span data-ttu-id="a3757-187">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="a3757-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="a3757-188">Dodawanie projektanta do laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a3757-188">Add a developer to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="a3757-189">Użyj portalu Azure, aby dodać deweloperów do laboratorium.</span><span class="sxs-lookup"><span data-stu-id="a3757-189">Use the Azure portal to add developers to your lab.</span></span>|
   | [<span data-ttu-id="a3757-190">Dodawanie do laboratorium za pomocą skryptu programu PowerShell deweloperów</span><span class="sxs-lookup"><span data-stu-id="a3757-190">Add developers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="a3757-191">Za pomocą programu PowerShell można zautomatyzować Dodawanie deweloperom laboratorium.</span><span class="sxs-lookup"><span data-stu-id="a3757-191">Use PowerShell to automate adding developers to your lab.</span></span> |
   | [<span data-ttu-id="a3757-192">Uzyskaj link do laboratorium</span><span class="sxs-lookup"><span data-stu-id="a3757-192">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="a3757-193">Dowiedz się, jak deweloperzy mogą bezpośrednio uzyskać dostępu do laboratorium za pośrednictwem hiperłącza.</span><span class="sxs-lookup"><span data-stu-id="a3757-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="a3757-194">**Zautomatyzować tworzenie laboratorium więcej zespołów**</span><span class="sxs-lookup"><span data-stu-id="a3757-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="a3757-195">Można zautomatyzować tworzenie laboratorium, m.in. przez tworzenie szablonu usługi Resource Manager i używanie go ponownie i ponownie utworzyć labs identyczne ustawienia niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="a3757-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="a3757-196">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="a3757-196">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="a3757-197">Zadanie</span><span class="sxs-lookup"><span data-stu-id="a3757-197">Task</span></span> | <span data-ttu-id="a3757-198">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="a3757-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="a3757-199">Tworzenie laboratorium przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a3757-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="a3757-200">Utwórz laboratoriów w usłudze Azure DevTest Labs za pomocą szablonów usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a3757-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

