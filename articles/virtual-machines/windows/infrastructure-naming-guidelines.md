---
title: "zasady — Windows nazewnictwa infrastruktury aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello klucza projekt i implementację zasady nazewnictwa w usług infrastruktury platformy Azure."
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
ms.openlocfilehash: 9b4a16ce99cf1cac5804c77675e24590ac2e2b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="5147e-103">Zasady nazewnictwa dla maszyn wirtualnych systemu Windows infrastruktury platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5147e-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="5147e-104">Ten artykuł koncentruje się na konfiguracji tooapproach konwencje nazewnictwa dla wszystkich sieci różnych zasobów Azure toobuild a logicznych i identyfikację zasobów w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="5147e-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="5147e-105">Implementacja — wskazówki dla konwencje nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="5147e-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="5147e-106">Decyzje:</span><span class="sxs-lookup"><span data-stu-id="5147e-106">Decisions:</span></span>

* <span data-ttu-id="5147e-107">Co to są konwencji nazewnictwa dla zasobów platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="5147e-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="5147e-108">Zadania:</span><span class="sxs-lookup"><span data-stu-id="5147e-108">Tasks:</span></span>

* <span data-ttu-id="5147e-109">Zdefiniuj toouse afiksów hello między spójności toomaintain Twojego zasobów.</span><span class="sxs-lookup"><span data-stu-id="5147e-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="5147e-110">Zdefiniuj konto magazynu, że podane nazwy hello wymaganie dla nich toobe globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="5147e-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="5147e-111">Dokument hello toobe konwencji nazewnictwa używane i rozpowszechniają spójności tooensure uczestniczących stron tooall wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="5147e-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="5147e-112">Konwencje nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="5147e-112">Naming conventions</span></span>
<span data-ttu-id="5147e-113">Przed utworzeniem jakichkolwiek na platformie Azure, powinien mieć dobrą konwencji nazewnictwa w miejscu.</span><span class="sxs-lookup"><span data-stu-id="5147e-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="5147e-114">Konwencja nazewnictwa gwarantuje, że wszystkie zasoby hello przewidywalną nazwy, która pomaga w dolnym hello nakładu prac administracyjnych związane z zarządzaniem tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="5147e-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="5147e-115">Możesz wybrać toofollow określonych konwencji nazewnictwa zdefiniowane dla całej organizacji lub dla określonej subskrypcji Azure lub konta.</span><span class="sxs-lookup"><span data-stu-id="5147e-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="5147e-116">Chociaż jest łatwy do osób w organizacji tooestablish niejawne reguł podczas pracy z zasobami Azure, gdy zespół musi toowork projektu na platformie Azure, modelu trudności w kontekście skalowania.</span><span class="sxs-lookup"><span data-stu-id="5147e-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, when a team needs toowork on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="5147e-117">Zgodę na zestawie konwencji nazewnictwa na początku.</span><span class="sxs-lookup"><span data-stu-id="5147e-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="5147e-118">Istnieją pewne kwestie dotyczące konwencji nazewnictwa Wytnij przez ten zestaw reguł.</span><span class="sxs-lookup"><span data-stu-id="5147e-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="5147e-119">Umieszcza</span><span class="sxs-lookup"><span data-stu-id="5147e-119">Affixes</span></span>
<span data-ttu-id="5147e-120">Jak wyglądają toodefine konwencji nazewnictwa, decyzji co wiąże się czy Afiks hello znajduje się na:</span><span class="sxs-lookup"><span data-stu-id="5147e-120">As you look toodefine a naming convention, one decision comes whether hello affix is at:</span></span>

* <span data-ttu-id="5147e-121">Witaj na początku nazwy hello (prefiks)</span><span class="sxs-lookup"><span data-stu-id="5147e-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="5147e-122">Witaj na końcu nazwy hello (sufiks)</span><span class="sxs-lookup"><span data-stu-id="5147e-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="5147e-123">Na przykład poniżej przedstawiono dwa możliwe nazwy grupy zasobów, przy użyciu hello `rg` umieścić:</span><span class="sxs-lookup"><span data-stu-id="5147e-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="5147e-124">Aplikacja zarządcy zasobów sieci Web (prefiks)</span><span class="sxs-lookup"><span data-stu-id="5147e-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="5147e-125">Aplikacja sieci Web zarządcy zasobów (sufiks)</span><span class="sxs-lookup"><span data-stu-id="5147e-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="5147e-126">Afiksów mogą odwoływać się toodifferent aspektów, które opisują hello określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="5147e-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="5147e-127">Witaj poniższej tabeli przedstawiono kilka przykładów zwykle używane.</span><span class="sxs-lookup"><span data-stu-id="5147e-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="5147e-128">Aspekt</span><span class="sxs-lookup"><span data-stu-id="5147e-128">Aspect</span></span> | <span data-ttu-id="5147e-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="5147e-129">Examples</span></span> | <span data-ttu-id="5147e-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5147e-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5147e-131">Środowisko</span><span class="sxs-lookup"><span data-stu-id="5147e-131">Environment</span></span> |<span data-ttu-id="5147e-132">deweloperów, stg, produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="5147e-132">dev, stg, prod</span></span> |<span data-ttu-id="5147e-133">W zależności od celu hello i nazwa każdego środowiska.</span><span class="sxs-lookup"><span data-stu-id="5147e-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="5147e-134">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="5147e-134">Location</span></span> |<span data-ttu-id="5147e-135">usw (zachodnie stany USA), użyj (wschodnie stany USA 2)</span><span class="sxs-lookup"><span data-stu-id="5147e-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="5147e-136">W zależności od regionu hello hello centrum danych lub regionu hello hello organizacji.</span><span class="sxs-lookup"><span data-stu-id="5147e-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="5147e-137">Składnik Azure, usługi lub produktu</span><span class="sxs-lookup"><span data-stu-id="5147e-137">Azure component, service, or product</span></span> |<span data-ttu-id="5147e-138">Grupy zasobów dla grupy zasobów, sieci wirtualnej dla sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5147e-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="5147e-139">W zależności od produktu hello, dla których hello zasobów zapewnia obsługę.</span><span class="sxs-lookup"><span data-stu-id="5147e-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="5147e-140">Rola</span><span class="sxs-lookup"><span data-stu-id="5147e-140">Role</span></span> |<span data-ttu-id="5147e-141">SQL, ora, sp, usługi iis</span><span class="sxs-lookup"><span data-stu-id="5147e-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="5147e-142">W zależności od roli hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5147e-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="5147e-143">Wystąpienie</span><span class="sxs-lookup"><span data-stu-id="5147e-143">Instance</span></span> |<span data-ttu-id="5147e-144">01, 02, 03, itp.</span><span class="sxs-lookup"><span data-stu-id="5147e-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="5147e-145">Dla zasobów, które mają więcej niż jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="5147e-145">For resources that have more than one instance.</span></span> <span data-ttu-id="5147e-146">Na przykład serwery sieci web w usłudze w chmurze zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="5147e-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="5147e-147">Podczas ustanawiania konwencji nazewnictwa, upewnij się, że ich wyraźnie określają, które umieszcza toouse dla każdego typu zasobu, w jakim położeniu (prefiks vs sufiks).</span><span class="sxs-lookup"><span data-stu-id="5147e-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="5147e-148">daty</span><span class="sxs-lookup"><span data-stu-id="5147e-148">Dates</span></span>
<span data-ttu-id="5147e-149">Często jest ważne toodetermine hello Data utworzenia z hello nazwy zasobu.</span><span class="sxs-lookup"><span data-stu-id="5147e-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="5147e-150">Zalecamy format daty hello RRRRMMDD.</span><span class="sxs-lookup"><span data-stu-id="5147e-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="5147e-151">Ten format gwarantuje, że nie tylko pełną datę hello jest rejestrowane, ale również tego dwa zasoby których nazwy różnią się tylko w dniu hello jest sortowana alfabetycznie, w porządku chronologicznym w hello tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="5147e-151">This format ensures that not only hello full date is recorded, but also that two resources whose names differ only on hello date is sorted alphabetically and chronologically at hello same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="5147e-152">Nadawanie nazw zasobów</span><span class="sxs-lookup"><span data-stu-id="5147e-152">Naming resources</span></span>
<span data-ttu-id="5147e-153">Każdy typ zasobu w konwencji nazewnictwa hello, który powinien mieć reguł określających sposób tooassign nazwy zasobu tooeach który jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="5147e-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="5147e-154">Te reguły stosowania tooall typów zasobów, na przykład:</span><span class="sxs-lookup"><span data-stu-id="5147e-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="5147e-155">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="5147e-155">Subscriptions</span></span>
* <span data-ttu-id="5147e-156">Konta</span><span class="sxs-lookup"><span data-stu-id="5147e-156">Accounts</span></span>
* <span data-ttu-id="5147e-157">Konta magazynu</span><span class="sxs-lookup"><span data-stu-id="5147e-157">Storage accounts</span></span>
* <span data-ttu-id="5147e-158">Sieci wirtualne</span><span class="sxs-lookup"><span data-stu-id="5147e-158">Virtual networks</span></span>
* <span data-ttu-id="5147e-159">Podsieci</span><span class="sxs-lookup"><span data-stu-id="5147e-159">Subnets</span></span>
* <span data-ttu-id="5147e-160">Zestawy dostępności</span><span class="sxs-lookup"><span data-stu-id="5147e-160">Availability sets</span></span>
* <span data-ttu-id="5147e-161">Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="5147e-161">Resource groups</span></span>
* <span data-ttu-id="5147e-162">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="5147e-162">Virtual machines</span></span>
* <span data-ttu-id="5147e-163">Punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="5147e-163">Endpoints</span></span>
* <span data-ttu-id="5147e-164">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="5147e-164">Network security groups</span></span>
* <span data-ttu-id="5147e-165">Role</span><span class="sxs-lookup"><span data-stu-id="5147e-165">Roles</span></span>

<span data-ttu-id="5147e-166">tooensure, który hello nazwa zawiera za mało informacji toodetermine toowhich zasób, który odwołuje się, należy użyć nazwy opisowe.</span><span class="sxs-lookup"><span data-stu-id="5147e-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="5147e-167">Nazwy komputerów</span><span class="sxs-lookup"><span data-stu-id="5147e-167">Computer names</span></span>
<span data-ttu-id="5147e-168">Podczas tworzenia maszyny wirtualnej (VM), Microsoft Azure wymaga nazwę maszyny Wirtualnej z zapasowej too15 znaków używany dla nazwy zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="5147e-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up too15 characters which is used for hello resource name.</span></span> <span data-ttu-id="5147e-169">Platforma Azure hello tej samej nazwy dla hello system operacyjny zainstalowany na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5147e-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="5147e-170">Jednak te nazwy może nie zawsze być hello tego samego.</span><span class="sxs-lookup"><span data-stu-id="5147e-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="5147e-171">W przypadku maszyny Wirtualnej jest tworzona na podstawie pliku obrazu vhd zawierającego system operacyjny, hello nazwę maszyny Wirtualnej na platformie Azure mogą się różnić od hello nazwa komputera systemu operacyjnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5147e-171">In case a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="5147e-172">Takiej sytuacji można dodać stopień trudności tooVM zarządzania, które w związku z tym nie jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="5147e-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="5147e-173">Przypisz hello hello zasobu maszyny Wirtualnej Azure takie same nazwy jako nazwy komputera hello przypisanie toohello system operacyjny tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5147e-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="5147e-174">Firma Microsoft zaleca tę nazwę maszyny Wirtualnej Azure hello jest hello taki sam jak hello bazowy nazwa komputera systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="5147e-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="5147e-175">Nazwy kont magazynu</span><span class="sxs-lookup"><span data-stu-id="5147e-175">Storage account names</span></span>
<span data-ttu-id="5147e-176">Ta sekcja nie ma zastosowania zbyt[dysków zarządzanych Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ponieważ nie należy tworzyć oddzielnego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5147e-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="5147e-177">Dla niezarządzanego dysków kont magazynu ma specjalne zasady dotyczące ich nazw.</span><span class="sxs-lookup"><span data-stu-id="5147e-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="5147e-178">Można używać tylko małe litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="5147e-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="5147e-179">Aby uzyskać więcej informacji, zobacz [Utwórz konto magazynu](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5147e-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="5147e-180">Ponadto hello nazwy konta magazynu, wraz z core.windows.net, należy globalnie prawidłową, unikatową nazwę DNS.</span><span class="sxs-lookup"><span data-stu-id="5147e-180">Additionally, hello storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="5147e-181">Na przykład jeśli konto magazynu hello jest nazywane mojekontomagazynu, hello poniższe nazwy DNS wynikowy powinna być unikatowa:</span><span class="sxs-lookup"><span data-stu-id="5147e-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="5147e-182">mystorageaccount.blob.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="5147e-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="5147e-183">mystorageaccount.TABLE.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="5147e-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="5147e-184">mystorageaccount.Queue.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="5147e-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="5147e-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5147e-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

