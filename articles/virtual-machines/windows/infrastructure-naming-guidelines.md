---
title: "Zasady — Windows nazewnictwa infrastruktury platformy Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat klucza projekt i implementację wskazówki dotyczące nazewnictwa w usług infrastruktury platformy Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a595d5c2f0316b5214af7b8939f1af8da187ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="d43e5-103">Zasady nazewnictwa dla maszyn wirtualnych systemu Windows infrastruktury platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d43e5-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="d43e5-104">Ten artykuł koncentruje się na sposób podejścia konwencje nazewnictwa dla wszystkich różnych zasobów platformy Azure można utworzyć logicznych i identyfikację zestaw zasobów w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="d43e5-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="d43e5-105">Implementacja — wskazówki dla konwencje nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="d43e5-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="d43e5-106">Decyzje:</span><span class="sxs-lookup"><span data-stu-id="d43e5-106">Decisions:</span></span>

* <span data-ttu-id="d43e5-107">Co to są konwencji nazewnictwa dla zasobów platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="d43e5-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="d43e5-108">Zadania:</span><span class="sxs-lookup"><span data-stu-id="d43e5-108">Tasks:</span></span>

* <span data-ttu-id="d43e5-109">Zdefiniuj afiksów służące do zapewniania spójności między zasobami.</span><span class="sxs-lookup"><span data-stu-id="d43e5-109">Define the affixes to use across your resources to maintain consistency.</span></span>
* <span data-ttu-id="d43e5-110">Zdefiniuj podane wymagania dla nich być globalnie unikatowe nazwy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d43e5-110">Define storage account names given the requirement for them to be globally unique.</span></span>
* <span data-ttu-id="d43e5-111">Następnie należy udokumentować konwencji nazewnictwa, można użyć do rozpowszechniania wśród wszystkich uczestniczących w celu zapewnienia spójności we wszystkich wdrożeniach.</span><span class="sxs-lookup"><span data-stu-id="d43e5-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="d43e5-112">Konwencje nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="d43e5-112">Naming conventions</span></span>
<span data-ttu-id="d43e5-113">Przed utworzeniem jakichkolwiek na platformie Azure, powinien mieć dobrą konwencji nazewnictwa w miejscu.</span><span class="sxs-lookup"><span data-stu-id="d43e5-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="d43e5-114">Konwencja nazewnictwa gwarantuje, że wszystkie zasoby przewidywalną nazwy, co pomaga zmniejszyć obciążenie administracyjne związane z zarządzaniem tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d43e5-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="d43e5-115">Można wykonać określonych konwencji nazewnictwa zdefiniowane dla całej organizacji lub dla określonej subskrypcji Azure lub konta.</span><span class="sxs-lookup"><span data-stu-id="d43e5-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="d43e5-116">Chociaż jest łatwe dla użytkowników indywidualnych w ramach organizacji ustanowienie reguł niejawnych podczas pracy z zasobów platformy Azure, gdy zespół wymaga do pracy nad projektem na platformie Azure, modelu trudności w kontekście skalowania.</span><span class="sxs-lookup"><span data-stu-id="d43e5-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, when a team needs to work on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="d43e5-117">Zgodę na zestawie konwencji nazewnictwa na początku.</span><span class="sxs-lookup"><span data-stu-id="d43e5-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="d43e5-118">Istnieją pewne kwestie dotyczące konwencji nazewnictwa Wytnij przez ten zestaw reguł.</span><span class="sxs-lookup"><span data-stu-id="d43e5-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="d43e5-119">Umieszcza</span><span class="sxs-lookup"><span data-stu-id="d43e5-119">Affixes</span></span>
<span data-ttu-id="d43e5-120">Jak wyglądają na definiowanie konwencji nazewnictwa, jeden decyzji pochodzi czy Afiks znajduje się na:</span><span class="sxs-lookup"><span data-stu-id="d43e5-120">As you look to define a naming convention, one decision comes whether the affix is at:</span></span>

* <span data-ttu-id="d43e5-121">Na początku nazwy (prefiks)</span><span class="sxs-lookup"><span data-stu-id="d43e5-121">The beginning of the name (prefix)</span></span>
* <span data-ttu-id="d43e5-122">Końcowa kropka (sufiks)</span><span class="sxs-lookup"><span data-stu-id="d43e5-122">The end of the name (suffix)</span></span>

<span data-ttu-id="d43e5-123">Na przykład poniżej przedstawiono dwa możliwe nazwy grupy zasobów przy użyciu `rg` umieścić:</span><span class="sxs-lookup"><span data-stu-id="d43e5-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span></span>

* <span data-ttu-id="d43e5-124">Aplikacja zarządcy zasobów sieci Web (prefiks)</span><span class="sxs-lookup"><span data-stu-id="d43e5-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="d43e5-125">Aplikacja sieci Web zarządcy zasobów (sufiks)</span><span class="sxs-lookup"><span data-stu-id="d43e5-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="d43e5-126">Afiksów mogą odwoływać się do różnych aspektów, które opisują określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d43e5-126">Affixes can refer to different aspects that describe the particular resources.</span></span> <span data-ttu-id="d43e5-127">W poniższej tabeli przedstawiono kilka przykładów zwykle używane.</span><span class="sxs-lookup"><span data-stu-id="d43e5-127">The following table shows some examples typically used.</span></span>

| <span data-ttu-id="d43e5-128">Aspekt</span><span class="sxs-lookup"><span data-stu-id="d43e5-128">Aspect</span></span> | <span data-ttu-id="d43e5-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="d43e5-129">Examples</span></span> | <span data-ttu-id="d43e5-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d43e5-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d43e5-131">Środowisko</span><span class="sxs-lookup"><span data-stu-id="d43e5-131">Environment</span></span> |<span data-ttu-id="d43e5-132">deweloperów, stg, produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="d43e5-132">dev, stg, prod</span></span> |<span data-ttu-id="d43e5-133">W zależności od przeznaczenia i nazwa każdego środowiska.</span><span class="sxs-lookup"><span data-stu-id="d43e5-133">Depending on the purpose and name of each environment.</span></span> |
| <span data-ttu-id="d43e5-134">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="d43e5-134">Location</span></span> |<span data-ttu-id="d43e5-135">usw (zachodnie stany USA), użyj (wschodnie stany USA 2)</span><span class="sxs-lookup"><span data-stu-id="d43e5-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="d43e5-136">W zależności od regionu centrum danych lub regionu, w organizacji.</span><span class="sxs-lookup"><span data-stu-id="d43e5-136">Depending on the region of the datacenter or the region of the organization.</span></span> |
| <span data-ttu-id="d43e5-137">Składnik Azure, usługi lub produktu</span><span class="sxs-lookup"><span data-stu-id="d43e5-137">Azure component, service, or product</span></span> |<span data-ttu-id="d43e5-138">Grupy zasobów dla grupy zasobów, sieci wirtualnej dla sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d43e5-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="d43e5-139">W zależności od produktu, którego zasobu zapewnia obsługę.</span><span class="sxs-lookup"><span data-stu-id="d43e5-139">Depending on the product for which the resource provides support.</span></span> |
| <span data-ttu-id="d43e5-140">Rola</span><span class="sxs-lookup"><span data-stu-id="d43e5-140">Role</span></span> |<span data-ttu-id="d43e5-141">SQL, ora, sp, usługi iis</span><span class="sxs-lookup"><span data-stu-id="d43e5-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="d43e5-142">W zależności od roli maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d43e5-142">Depending on the role of the virtual machine.</span></span> |
| <span data-ttu-id="d43e5-143">Wystąpienie</span><span class="sxs-lookup"><span data-stu-id="d43e5-143">Instance</span></span> |<span data-ttu-id="d43e5-144">01, 02, 03, itp.</span><span class="sxs-lookup"><span data-stu-id="d43e5-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="d43e5-145">Dla zasobów, które mają więcej niż jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="d43e5-145">For resources that have more than one instance.</span></span> <span data-ttu-id="d43e5-146">Na przykład serwery sieci web w usłudze w chmurze zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="d43e5-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="d43e5-147">Podczas ustanawiania konwencji nazewnictwa, upewnij się, czy one wyraźnie określają, które afiksów do użycia dla każdego typu zasobu, w jakim położeniu (prefiks vs sufiks).</span><span class="sxs-lookup"><span data-stu-id="d43e5-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="d43e5-148">daty</span><span class="sxs-lookup"><span data-stu-id="d43e5-148">Dates</span></span>
<span data-ttu-id="d43e5-149">Często jest to ważne jest określenie daty utworzenia od nazwy zasobu.</span><span class="sxs-lookup"><span data-stu-id="d43e5-149">It is often important to determine the date of creation from the name of a resource.</span></span> <span data-ttu-id="d43e5-150">Zalecamy format daty RRRRMMDD.</span><span class="sxs-lookup"><span data-stu-id="d43e5-150">We recommend the YYYYMMDD date format.</span></span> <span data-ttu-id="d43e5-151">Ten format gwarantuje, że nie tylko pełną datę jest rejestrowane, ale również tego dwa zasoby których nazwy różnią się tylko w dniu jest sortowana alfabetycznie, w porządku chronologicznym w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="d43e5-151">This format ensures that not only the full date is recorded, but also that two resources whose names differ only on the date is sorted alphabetically and chronologically at the same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="d43e5-152">Nadawanie nazw zasobów</span><span class="sxs-lookup"><span data-stu-id="d43e5-152">Naming resources</span></span>
<span data-ttu-id="d43e5-153">Zdefiniuj każdego typu zasobu w konwencji nazewnictwa, która ma reguł określających, jak przypisać nazwy do każdego zasobu, która jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="d43e5-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span></span> <span data-ttu-id="d43e5-154">Te reguły stosuje się do wszystkich typów zasobów, na przykład:</span><span class="sxs-lookup"><span data-stu-id="d43e5-154">These rules should apply to all types of resources, for example:</span></span>

* <span data-ttu-id="d43e5-155">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="d43e5-155">Subscriptions</span></span>
* <span data-ttu-id="d43e5-156">Konta</span><span class="sxs-lookup"><span data-stu-id="d43e5-156">Accounts</span></span>
* <span data-ttu-id="d43e5-157">Konta magazynu</span><span class="sxs-lookup"><span data-stu-id="d43e5-157">Storage accounts</span></span>
* <span data-ttu-id="d43e5-158">Sieci wirtualne</span><span class="sxs-lookup"><span data-stu-id="d43e5-158">Virtual networks</span></span>
* <span data-ttu-id="d43e5-159">Podsieci</span><span class="sxs-lookup"><span data-stu-id="d43e5-159">Subnets</span></span>
* <span data-ttu-id="d43e5-160">Zestawy dostępności</span><span class="sxs-lookup"><span data-stu-id="d43e5-160">Availability sets</span></span>
* <span data-ttu-id="d43e5-161">Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="d43e5-161">Resource groups</span></span>
* <span data-ttu-id="d43e5-162">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="d43e5-162">Virtual machines</span></span>
* <span data-ttu-id="d43e5-163">Punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="d43e5-163">Endpoints</span></span>
* <span data-ttu-id="d43e5-164">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="d43e5-164">Network security groups</span></span>
* <span data-ttu-id="d43e5-165">Role</span><span class="sxs-lookup"><span data-stu-id="d43e5-165">Roles</span></span>

<span data-ttu-id="d43e5-166">Aby upewnić się, że nazwa zawiera wystarczających informacji do ustalenia, do którego odnosi się zasobu, należy używać nazwy opisowej.</span><span class="sxs-lookup"><span data-stu-id="d43e5-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="d43e5-167">Nazwy komputerów</span><span class="sxs-lookup"><span data-stu-id="d43e5-167">Computer names</span></span>
<span data-ttu-id="d43e5-168">Podczas tworzenia maszyny wirtualnej (VM), Microsoft Azure wymaga nazwę maszyny Wirtualnej z maksymalnie 15 znaków używany dla nazwy zasobu.</span><span class="sxs-lookup"><span data-stu-id="d43e5-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up to 15 characters which is used for the resource name.</span></span> <span data-ttu-id="d43e5-169">Azure korzysta z tej samej nazwy dla system operacyjny zainstalowany na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d43e5-169">Azure uses the same name for the operating system installed in the VM.</span></span> <span data-ttu-id="d43e5-170">Jednak te nazwy może nie zawsze być takie same.</span><span class="sxs-lookup"><span data-stu-id="d43e5-170">However, these names might not always be the same.</span></span>

<span data-ttu-id="d43e5-171">W przypadku maszyny Wirtualnej jest tworzona na podstawie pliku obrazu vhd zawierającego system operacyjny, nazwę maszyny Wirtualnej na platformie Azure mogą się różnić od nazwy komputera systemu operacyjnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d43e5-171">In case a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span></span> <span data-ttu-id="d43e5-172">Do maszyny Wirtualnej zarządzania, dlatego nie zaleca się takiej sytuacji można dodać stopień trudności.</span><span class="sxs-lookup"><span data-stu-id="d43e5-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span></span> <span data-ttu-id="d43e5-173">Przydziel zasób maszyny Wirtualnej Azure taką samą nazwę jak nazwa komputera, przypisane do tej maszyny Wirtualnej systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d43e5-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span></span>

<span data-ttu-id="d43e5-174">Zaleca się, że nazwa maszyny Wirtualnej platformy Azure jest taka sama jak nazwa komputera źródłowego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d43e5-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="d43e5-175">Nazwy kont magazynu</span><span class="sxs-lookup"><span data-stu-id="d43e5-175">Storage account names</span></span>
<span data-ttu-id="d43e5-176">Ta sekcja nie ma zastosowania do [dysków zarządzanych Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ponieważ nie należy tworzyć oddzielnego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d43e5-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="d43e5-177">Dla niezarządzanego dysków kont magazynu ma specjalne zasady dotyczące ich nazw.</span><span class="sxs-lookup"><span data-stu-id="d43e5-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="d43e5-178">Można używać tylko małe litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="d43e5-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="d43e5-179">Aby uzyskać więcej informacji, zobacz [Utwórz konto magazynu](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d43e5-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="d43e5-180">Ponadto nazwa konta magazynu, wraz z core.windows.net, należy globalnie prawidłową, unikatową nazwę DNS.</span><span class="sxs-lookup"><span data-stu-id="d43e5-180">Additionally, the storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="d43e5-181">Na przykład jeśli konto magazynu jest nazywane mojekontomagazynu, wynikowy poniższe nazwy DNS powinien być unikatowy:</span><span class="sxs-lookup"><span data-stu-id="d43e5-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="d43e5-182">mystorageaccount.blob.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="d43e5-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="d43e5-183">mystorageaccount.TABLE.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="d43e5-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="d43e5-184">mystorageaccount.Queue.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="d43e5-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="d43e5-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d43e5-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

