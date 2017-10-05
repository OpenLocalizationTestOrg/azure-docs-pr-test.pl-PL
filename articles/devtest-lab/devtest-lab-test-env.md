---
title: "Użyj Azure DevTest Labs dla maszyny Wirtualnej i PaaS środowisk testowania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać Azure DevTest Labs dla maszyny Wirtualnej i PaaS scenariuszy środowiska testowego."
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
ms.openlocfilehash: a556cee9d7b665cd7df23c97e7e2c8c2afabbe58
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="88d21-103">Użyj Azure DevTest Labs dla maszyny Wirtualnej i PaaS test środowisk</span><span class="sxs-lookup"><span data-stu-id="88d21-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="88d21-104">Azure DevTest Labs umożliwia wdrożenie wielu kluczowych scenariuszy, ale podstawowego scenariusza polega na użyciu DevTest Labs na komputerach hosta dla testerów.</span><span class="sxs-lookup"><span data-stu-id="88d21-104">You can use Azure DevTest Labs to implement many key scenarios, but a primary scenario involves using DevTest Labs to host machines for testers.</span></span> 

<span data-ttu-id="88d21-105">W tym scenariuszu DevTest Labs zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="88d21-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="88d21-106">Testerów można przetestować najnowszej wersji aplikacji przez szybkie Inicjowanie obsługi środowisk systemu Windows i Linux za pomocą szablonów wielokrotnego użytku i artefaktów.</span><span class="sxs-lookup"><span data-stu-id="88d21-106">Testers can test the latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="88d21-107">Testerów można zwiększać ich przez Inicjowanie obsługi wielu agentów testowych do testowania obciążenia.</span><span class="sxs-lookup"><span data-stu-id="88d21-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="88d21-108">Administratorzy mogą kontrolować koszty przez zapewnienie, że:</span><span class="sxs-lookup"><span data-stu-id="88d21-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="88d21-109">Testerów nie można pobrać więcej maszyn wirtualnych, niż jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="88d21-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="88d21-110">Maszyny wirtualne są zamknięte podczas nieużywany.</span><span class="sxs-lookup"><span data-stu-id="88d21-110">VMs are shut down when not in use.</span></span>

![Użyć do trenowania DevTest Labs](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="88d21-112">W tym artykule dowiesz się o różnych funkcjach Azure DevTest Labs użyć, aby spełnić wymagania tester i szczegółowy opis kroków wykonaj skonfigurować laboratorium.</span><span class="sxs-lookup"><span data-stu-id="88d21-112">In this article, you learn about various Azure DevTest Labs features used to meet tester requirements and the detailed steps to follow to set up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="88d21-113">Implementowanie środowiska testowego o usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="88d21-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="88d21-114">**Tworzenie laboratorium**</span><span class="sxs-lookup"><span data-stu-id="88d21-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="88d21-115">Laboratoria stanowią punkt początkowy w usłudze Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="88d21-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="88d21-116">Po utworzeniu laboratorium, można wykonywać zadania, takie jak dodawanie użytkowników (testerów) do laboratorium, ustawienie zasad w celu kontrolowania kosztów, definiowanie obrazów maszyn wirtualnych, które można szybko utworzyć i inne.</span><span class="sxs-lookup"><span data-stu-id="88d21-116">Once you create a lab, you can perform tasks such as adding users (testers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="88d21-117">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="88d21-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="88d21-118">Zadanie</span><span class="sxs-lookup"><span data-stu-id="88d21-118">Task</span></span> | <span data-ttu-id="88d21-119">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="88d21-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="88d21-120">Tworzenie laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="88d21-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="88d21-121">Dowiedz się, jak tworzenie laboratorium w usłudze Azure DevTest Labs w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="88d21-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="88d21-122">**Tworzenie maszyn wirtualnych w kilka minut przy użyciu gotowych marketplace obrazów i niestandardowych obrazów**</span><span class="sxs-lookup"><span data-stu-id="88d21-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="88d21-123">Możesz pobrania gotowych obrazów z szerokiej gamy obrazów w portalu Azure Marketplace i udostępnić je w środowisku laboratoryjnym.</span><span class="sxs-lookup"><span data-stu-id="88d21-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="88d21-124">Jeśli gotowe do użycia obrazy nie spełniają wymagań, można utworzyć niestandardowego obrazu, tworząc laboratorium maszyny Wirtualnej przy użyciu gotowych obrazu z portalu Azure Marketplace, instalacja oprogramowania, które są potrzebne, i zapisywanie maszyny Wirtualnej jako obraz niestandardowy w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="88d21-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="88d21-125">Jeśli będziesz używać niestandardowych obrazów, rozważ użycie fabrykę obrazu do tworzenia i rozpowszechniania obrazów.</span><span class="sxs-lookup"><span data-stu-id="88d21-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="88d21-126">Fabryka obrazu jest rozwiązanie konfiguracji jako kod, który regularnie tworzy i rozpowszechnia obrazy skonfigurowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="88d21-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="88d21-127">Spowoduje to zapisanie czasu, należy ręcznie skonfigurować system po utworzeniu maszyny Wirtualnej z podstawowego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="88d21-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="88d21-128">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="88d21-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="88d21-129">Zadanie</span><span class="sxs-lookup"><span data-stu-id="88d21-129">Task</span></span> | <span data-ttu-id="88d21-130">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="88d21-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="88d21-131">Konfigurowanie portalu Azure Marketplace obrazów</span><span class="sxs-lookup"><span data-stu-id="88d21-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="88d21-132">Informacje na temat dozwolonych portalu Azure Marketplace obrazów, określ, co do wyboru dostępne tylko obrazy dla testerów.</span><span class="sxs-lookup"><span data-stu-id="88d21-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the testers.</span></span>|
   | [<span data-ttu-id="88d21-133">Tworzenie niestandardowego obrazu</span><span class="sxs-lookup"><span data-stu-id="88d21-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="88d21-134">Tworzenie niestandardowego obrazu za pomocą wstępnie instalacji oprogramowania, które są potrzebne, aby testerów może szybko utworzyć Maszynę wirtualną przy użyciu niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="88d21-134">Create a custom image by pre-installing the software you need so that testers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="88d21-135">Więcej informacji na temat fabryki obrazu</span><span class="sxs-lookup"><span data-stu-id="88d21-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="88d21-136">Obejrzyj klip wideo, który opisuje sposób konfigurowania i używania fabrykę obrazu.</span><span class="sxs-lookup"><span data-stu-id="88d21-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="88d21-137">**Tworzenie szablonów wielokrotnego użytku dla maszyny testowe**</span><span class="sxs-lookup"><span data-stu-id="88d21-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="88d21-138">Formuła w usłudze Azure DevTest Labs znajduje się lista domyślnych wartości właściwości używany do tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88d21-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="88d21-139">Wybieranie obrazu, rozmiar maszyny Wirtualnej (kombinacja Procesora i pamięci RAM) i sieć wirtualną można utworzyć formuły w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="88d21-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="88d21-140">Każdy tester można formuła w laboratorium i go użyć do utworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88d21-140">Each tester can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="88d21-141">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="88d21-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="88d21-142">Zadanie</span><span class="sxs-lookup"><span data-stu-id="88d21-142">Task</span></span> | <span data-ttu-id="88d21-143">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="88d21-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="88d21-144">Zarządzanie DevTest Labs formuły można utworzyć maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="88d21-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="88d21-145">Dowiedz się, jak utworzyć formuły przez przechwycenie obrazu, rozmiar maszyny Wirtualnej (kombinację procesora CPU i pamięci RAM) i sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88d21-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="88d21-146">**Tworzenie wielu maszyn wirtualnych środowisk testowych.**</span><span class="sxs-lookup"><span data-stu-id="88d21-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="88d21-147">Szablony usługi Azure Resource Manager służy do definiowania infrastrukturze i konfiguracji rozwiązania Azure i wielokrotnie wdrażać testu wiele maszyn wirtualnych w spójnym stanie.</span><span class="sxs-lookup"><span data-stu-id="88d21-147">You can use Azure Resource Manager templates to define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="88d21-148">Zasoby platformy Azure PaaS można udostępnić w środowisku z szablonem usługi Resource Manager i widoczny w śledzenie kosztów.</span><span class="sxs-lookup"><span data-stu-id="88d21-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="88d21-149">Jednak maszyna wirtualna automatycznego zamykania nie ma zastosowania do zasobów typu PaaS.</span><span class="sxs-lookup"><span data-stu-id="88d21-149">However, VM auto shutdown does not apply to PaaS resources.</span></span>

    <span data-ttu-id="88d21-150">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="88d21-150">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="88d21-151">Zadanie</span><span class="sxs-lookup"><span data-stu-id="88d21-151">Task</span></span> | <span data-ttu-id="88d21-152">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="88d21-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="88d21-153">Tworzenie środowisk z wieloma maszynami wirtualnymi i zasobów PaaS za pomocą szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="88d21-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="88d21-154">Dowiedz się, jak można wdrożyć wiele maszyn wirtualnych w spójnym stanie dla danego środowiska testowego.</span><span class="sxs-lookup"><span data-stu-id="88d21-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="88d21-155">**Tworzenie artefaktów, aby umożliwić elastyczne dostosowanie maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="88d21-155">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="88d21-156">Artefakty służą do wdrażania i konfigurowania aplikacji po zainicjowaniu obsługi maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88d21-156">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="88d21-157">Artefaktami mogą być:</span><span class="sxs-lookup"><span data-stu-id="88d21-157">Artifacts can be:</span></span>

   - <span data-ttu-id="88d21-158">Narzędzia, które chcesz zainstalować na maszynie Wirtualnej — np. agenci, program Fiddler i program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88d21-158">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="88d21-159">Akcje, które chcesz uruchomić na maszynie Wirtualnej — np. klonowanie repozytorium.</span><span class="sxs-lookup"><span data-stu-id="88d21-159">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="88d21-160">Aplikacje, które chcesz przetestować.</span><span class="sxs-lookup"><span data-stu-id="88d21-160">Applications that you want to test.</span></span>

   <span data-ttu-id="88d21-161">Wiele artefakty są już dostępne out-of--box.</span><span class="sxs-lookup"><span data-stu-id="88d21-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="88d21-162">Ale jeśli chcesz więcej dostosowania do określonych potrzeb, możesz utworzyć własne niestandardowe artefakty.</span><span class="sxs-lookup"><span data-stu-id="88d21-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="88d21-163">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="88d21-163">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="88d21-164">Zadanie</span><span class="sxs-lookup"><span data-stu-id="88d21-164">Task</span></span> | <span data-ttu-id="88d21-165">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="88d21-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="88d21-166">Tworzenie niestandardowych artefaktów dla maszyny Wirtualnej DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="88d21-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="88d21-167">Tworzenie własnych niestandardowych artefaktów dla maszyn wirtualnych w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="88d21-167">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="88d21-168">Dodaj repozytorium Git do przechowywania niestandardowych artefaktów i szablony usługi Azure Resource Manager do użycia w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="88d21-168">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="88d21-169">Dowiedz się, jak zapisać Twoje niestandardowe artefakty w własne prywatne repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="88d21-169">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="88d21-170">**Kontrolę kosztów**</span><span class="sxs-lookup"><span data-stu-id="88d21-170">**Control costs**</span></span>
   
    <span data-ttu-id="88d21-171">Azure DevTest Labs umożliwia ustawienie zasad w środowisku laboratoryjnym, aby określić maksymalną liczbę maszyn wirtualnych, które mogą być tworzone przez tester w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="88d21-171">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a tester in the lab.</span></span> 
   
    <span data-ttu-id="88d21-172">Jeśli zespół testu zawiera zestaw pracy harmonogramu i chcesz zatrzymanie wszystkich maszyn wirtualnych o określonej godzinie dnia, a następnie automatycznie uruchomić je ponownie następnego dnia, można łatwo realizacji tego przez ustawienie zasad automatycznego zamykania i automatycznego uruchamiania w środowisku laboratoryjnym.</span><span class="sxs-lookup"><span data-stu-id="88d21-172">If your test team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="88d21-173">Na koniec po zakończeniu tworzenia aplikacji, można usunąć wszystkich maszyn wirtualnych jednocześnie za pomocą jednego skryptu środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88d21-173">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="88d21-174">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="88d21-174">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="88d21-175">Zadanie</span><span class="sxs-lookup"><span data-stu-id="88d21-175">Task</span></span> | <span data-ttu-id="88d21-176">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="88d21-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="88d21-177">Definiowanie zasad laboratorium</span><span class="sxs-lookup"><span data-stu-id="88d21-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="88d21-178">Kontrolę kosztów przez ustawienie zasad w środowisku laboratoryjnym.</span><span class="sxs-lookup"><span data-stu-id="88d21-178">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="88d21-179">Usuń wszystkie laboratorium maszyn wirtualnych za pomocą skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="88d21-179">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="88d21-180">Po zakończeniu testowania, należy usunąć wszystkie laboratoriów w ramach jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="88d21-180">Delete all the labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="88d21-181">**Dodaj sieć wirtualną w laboratorium**</span><span class="sxs-lookup"><span data-stu-id="88d21-181">**Add a virtual network to a Lab**</span></span> 
   
    <span data-ttu-id="88d21-182">DevTest Labs tworzy nową sieć wirtualną (VNET), przy każdym utworzeniu laboratorium.</span><span class="sxs-lookup"><span data-stu-id="88d21-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="88d21-183">Jeśli skonfigurowano własnych sieci Wirtualnej — np. za pomocą programu ExpressRoute lub sieci VPN typu lokacja lokacja — można dodać tej sieci Wirtualnej do ustawień sieci wirtualnej środowiska laboratoryjnego, aby była dostępna podczas tworzenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="88d21-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="88d21-184">Ponadto jest usługa Azure Active Directory domeny sprzężenia artefaktu dostępne której jest przyłączany do domeny maszyny Wirtualnej, po utworzeniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88d21-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="88d21-185">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="88d21-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="88d21-186">Zadanie</span><span class="sxs-lookup"><span data-stu-id="88d21-186">Task</span></span> | <span data-ttu-id="88d21-187">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="88d21-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="88d21-188">Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="88d21-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="88d21-189">Dowiedz się, jak skonfigurować sieć wirtualną w usłudze Azure DevTest Labs przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="88d21-189">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="88d21-190">**Udostępnij każdego tester laboratorium**</span><span class="sxs-lookup"><span data-stu-id="88d21-190">**Share the lab with each tester**</span></span>
   
    <span data-ttu-id="88d21-191">Laboratoria są bezpośrednio dostępne przy użyciu łącza, które są udostępniane z testerów.</span><span class="sxs-lookup"><span data-stu-id="88d21-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="88d21-192">Nie nawet muszą oni mieć konto platformy Azure, jak długo mają [konta Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="88d21-192">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="88d21-193">Testerów nie widzi maszyny wirtualne utworzone przez inne testerów.</span><span class="sxs-lookup"><span data-stu-id="88d21-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="88d21-194">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="88d21-194">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="88d21-195">Zadanie</span><span class="sxs-lookup"><span data-stu-id="88d21-195">Task</span></span> | <span data-ttu-id="88d21-196">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="88d21-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="88d21-197">Dodaj tester do laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="88d21-197">Add a tester to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="88d21-198">Użyj portalu Azure, aby dodać testerów do laboratorium.</span><span class="sxs-lookup"><span data-stu-id="88d21-198">Use the Azure portal to add testers to your lab.</span></span>|
   | [<span data-ttu-id="88d21-199">Dodaj testerów do laboratorium za pomocą skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="88d21-199">Add testers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="88d21-200">Za pomocą programu PowerShell można zautomatyzować Dodawanie testerów do laboratorium.</span><span class="sxs-lookup"><span data-stu-id="88d21-200">Use PowerShell to automate adding testers to your lab.</span></span> |
   | [<span data-ttu-id="88d21-201">Uzyskaj link do laboratorium</span><span class="sxs-lookup"><span data-stu-id="88d21-201">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="88d21-202">Dowiedz się, jak testerów bezpośrednio uzyskać dostęp za pośrednictwem hiperłącze laboratorium.</span><span class="sxs-lookup"><span data-stu-id="88d21-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="88d21-203">**Zautomatyzować tworzenie laboratorium więcej zespołów**</span><span class="sxs-lookup"><span data-stu-id="88d21-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="88d21-204">Można zautomatyzować tworzenie laboratorium, m.in. przez tworzenie szablonu usługi Resource Manager i używanie go ponownie i ponownie utworzyć labs identyczne ustawienia niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="88d21-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="88d21-205">Dowiedz się więcej, klikając łącza w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="88d21-205">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="88d21-206">Zadanie</span><span class="sxs-lookup"><span data-stu-id="88d21-206">Task</span></span> | <span data-ttu-id="88d21-207">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="88d21-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="88d21-208">Tworzenie laboratorium przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="88d21-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="88d21-209">Utwórz laboratoriów w usłudze Azure DevTest Labs za pomocą szablonów usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="88d21-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

