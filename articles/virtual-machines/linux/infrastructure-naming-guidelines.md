---
title: "zasady — Linux nazewnictwa infrastruktury aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello klucza projekt i implementację zasady nazewnictwa w usług infrastruktury platformy Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="36e66-103">Zasady nazewnictwa dla maszyn wirtualnych systemu Linux infrastruktury platformy Azure</span><span class="sxs-lookup"><span data-stu-id="36e66-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="36e66-104">Ten artykuł koncentruje się na konfiguracji tooapproach konwencje nazewnictwa dla wszystkich sieci różnych zasobów Azure toobuild a logicznych i identyfikację zasobów w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="36e66-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="36e66-105">Implementacja — wskazówki dla konwencje nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="36e66-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="36e66-106">Decyzje:</span><span class="sxs-lookup"><span data-stu-id="36e66-106">Decisions:</span></span>

* <span data-ttu-id="36e66-107">Co to są konwencji nazewnictwa dla zasobów platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="36e66-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="36e66-108">Zadania:</span><span class="sxs-lookup"><span data-stu-id="36e66-108">Tasks:</span></span>

* <span data-ttu-id="36e66-109">Zdefiniuj toouse afiksów hello między spójności toomaintain Twojego zasobów.</span><span class="sxs-lookup"><span data-stu-id="36e66-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="36e66-110">Zdefiniuj konto magazynu, że podane nazwy hello wymaganie dla nich toobe globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="36e66-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="36e66-111">Dokument hello toobe konwencji nazewnictwa używane i rozpowszechniają spójności tooensure uczestniczących stron tooall wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="36e66-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="36e66-112">Konwencje nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="36e66-112">Naming conventions</span></span>
<span data-ttu-id="36e66-113">Przed utworzeniem jakichkolwiek na platformie Azure, powinien mieć dobrą konwencji nazewnictwa w miejscu.</span><span class="sxs-lookup"><span data-stu-id="36e66-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="36e66-114">Konwencja nazewnictwa gwarantuje, że wszystkie zasoby hello przewidywalną nazwy, która pomaga w dolnym hello nakładu prac administracyjnych związane z zarządzaniem tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="36e66-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="36e66-115">Możesz wybrać toofollow określonych konwencji nazewnictwa zdefiniowane dla całej organizacji lub dla określonej subskrypcji Azure lub konta.</span><span class="sxs-lookup"><span data-stu-id="36e66-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="36e66-116">Chociaż jest łatwy do osób w organizacji tooestablish niejawne reguł podczas pracy z zasobami Azure, należy tooscale stanie toobe dla zespołów pracujących razem na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="36e66-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, you need toobe able tooscale for teams working together in Azure.</span></span>

<span data-ttu-id="36e66-117">Zgodę na zestawie konwencji nazewnictwa na początku.</span><span class="sxs-lookup"><span data-stu-id="36e66-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="36e66-118">Istnieją pewne kwestie dotyczących konwencji nazewnictwa Wytnij między które ustawia zasady.</span><span class="sxs-lookup"><span data-stu-id="36e66-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="36e66-119">Umieszcza</span><span class="sxs-lookup"><span data-stu-id="36e66-119">Affixes</span></span>
<span data-ttu-id="36e66-120">Jak wyglądają toodefine konwencji nazewnictwa, decyzji co jest czy Afiks hello na:</span><span class="sxs-lookup"><span data-stu-id="36e66-120">As you look toodefine a naming convention, one decision is whether hello affix is at:</span></span>

* <span data-ttu-id="36e66-121">Witaj na początku nazwy hello (prefiks)</span><span class="sxs-lookup"><span data-stu-id="36e66-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="36e66-122">Witaj na końcu nazwy hello (sufiks)</span><span class="sxs-lookup"><span data-stu-id="36e66-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="36e66-123">Na przykład poniżej przedstawiono dwa możliwe nazwy grupy zasobów, przy użyciu hello `rg` umieścić:</span><span class="sxs-lookup"><span data-stu-id="36e66-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="36e66-124">Aplikacja zarządcy zasobów sieci Web (prefiks)</span><span class="sxs-lookup"><span data-stu-id="36e66-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="36e66-125">Aplikacja sieci Web zarządcy zasobów (sufiks)</span><span class="sxs-lookup"><span data-stu-id="36e66-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="36e66-126">Afiksów mogą odwoływać się toodifferent aspektów, które opisują hello określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="36e66-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="36e66-127">Witaj poniższej tabeli przedstawiono kilka przykładów zwykle używane.</span><span class="sxs-lookup"><span data-stu-id="36e66-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="36e66-128">Aspekt</span><span class="sxs-lookup"><span data-stu-id="36e66-128">Aspect</span></span> | <span data-ttu-id="36e66-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="36e66-129">Examples</span></span> | <span data-ttu-id="36e66-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="36e66-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="36e66-131">Środowisko</span><span class="sxs-lookup"><span data-stu-id="36e66-131">Environment</span></span> |<span data-ttu-id="36e66-132">deweloperów, stg, produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="36e66-132">dev, stg, prod</span></span> |<span data-ttu-id="36e66-133">W zależności od celu hello i nazwa każdego środowiska.</span><span class="sxs-lookup"><span data-stu-id="36e66-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="36e66-134">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="36e66-134">Location</span></span> |<span data-ttu-id="36e66-135">usw (zachodnie stany USA), użyj (wschodnie stany USA 2)</span><span class="sxs-lookup"><span data-stu-id="36e66-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="36e66-136">W zależności od regionu hello hello centrum danych lub regionu hello hello organizacji.</span><span class="sxs-lookup"><span data-stu-id="36e66-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="36e66-137">Składnik Azure, usługi lub produktu</span><span class="sxs-lookup"><span data-stu-id="36e66-137">Azure component, service, or product</span></span> |<span data-ttu-id="36e66-138">Grupy zasobów dla grupy zasobów, sieci wirtualnej dla sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="36e66-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="36e66-139">W zależności od produktu hello, dla których hello zasobów zapewnia obsługę.</span><span class="sxs-lookup"><span data-stu-id="36e66-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="36e66-140">Rola</span><span class="sxs-lookup"><span data-stu-id="36e66-140">Role</span></span> |<span data-ttu-id="36e66-141">bazy danych, aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="36e66-141">db, app, web</span></span> |<span data-ttu-id="36e66-142">W zależności od roli hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e66-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="36e66-143">Wystąpienie</span><span class="sxs-lookup"><span data-stu-id="36e66-143">Instance</span></span> |<span data-ttu-id="36e66-144">01, 02, 03, itp.</span><span class="sxs-lookup"><span data-stu-id="36e66-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="36e66-145">Dla zasobów, które mają więcej niż jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="36e66-145">For resources that have more than one instance.</span></span> <span data-ttu-id="36e66-146">Na przykład serwery sieci web w usłudze w chmurze zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="36e66-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="36e66-147">Podczas ustanawiania konwencji nazewnictwa, upewnij się, że ich wyraźnie określają, które umieszcza toouse dla każdego typu zasobu, w jakim położeniu (prefiks vs sufiks).</span><span class="sxs-lookup"><span data-stu-id="36e66-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="36e66-148">daty</span><span class="sxs-lookup"><span data-stu-id="36e66-148">Dates</span></span>
<span data-ttu-id="36e66-149">Często jest ważne toodetermine hello Data utworzenia z hello nazwy zasobu.</span><span class="sxs-lookup"><span data-stu-id="36e66-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="36e66-150">Zalecamy format daty hello RRRRMMDD.</span><span class="sxs-lookup"><span data-stu-id="36e66-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="36e66-151">Format ten zapewnia nie tylko hello pełna data jest rejestrowane, ale również tego dwa zasoby których nazwy różnią się tylko w dniu hello są posortowane alfabetycznie, w porządku chronologicznym.</span><span class="sxs-lookup"><span data-stu-id="36e66-151">This format ensures that not only is hello full date is recorded, but also that two resources whose names differ only on hello date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="36e66-152">Nadawanie nazw zasobów</span><span class="sxs-lookup"><span data-stu-id="36e66-152">Naming resources</span></span>
<span data-ttu-id="36e66-153">Każdy typ zasobu w konwencji nazewnictwa hello, który powinien mieć reguł określających sposób tooassign nazwy zasobu tooeach który jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="36e66-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="36e66-154">Te reguły stosowania tooall typów zasobów, na przykład:</span><span class="sxs-lookup"><span data-stu-id="36e66-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="36e66-155">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="36e66-155">Subscriptions</span></span>
* <span data-ttu-id="36e66-156">Konta</span><span class="sxs-lookup"><span data-stu-id="36e66-156">Accounts</span></span>
* <span data-ttu-id="36e66-157">Konta magazynu</span><span class="sxs-lookup"><span data-stu-id="36e66-157">Storage accounts</span></span>
* <span data-ttu-id="36e66-158">Sieci wirtualne</span><span class="sxs-lookup"><span data-stu-id="36e66-158">Virtual networks</span></span>
* <span data-ttu-id="36e66-159">Podsieci</span><span class="sxs-lookup"><span data-stu-id="36e66-159">Subnets</span></span>
* <span data-ttu-id="36e66-160">Zestawy dostępności</span><span class="sxs-lookup"><span data-stu-id="36e66-160">Availability sets</span></span>
* <span data-ttu-id="36e66-161">Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="36e66-161">Resource groups</span></span>
* <span data-ttu-id="36e66-162">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="36e66-162">Virtual machines</span></span>
* <span data-ttu-id="36e66-163">Punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="36e66-163">Endpoints</span></span>
* <span data-ttu-id="36e66-164">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="36e66-164">Network security groups</span></span>
* <span data-ttu-id="36e66-165">Role</span><span class="sxs-lookup"><span data-stu-id="36e66-165">Roles</span></span>

<span data-ttu-id="36e66-166">tooensure, który hello nazwa zawiera za mało informacji toodetermine toowhich zasób, który odwołuje się, należy użyć nazwy opisowe.</span><span class="sxs-lookup"><span data-stu-id="36e66-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="36e66-167">Nazwy komputerów</span><span class="sxs-lookup"><span data-stu-id="36e66-167">Computer names</span></span>
<span data-ttu-id="36e66-168">Podczas tworzenia maszyny wirtualnej (VM) na platformie Azure wymaga nazwę maszyny Wirtualnej z zapasowej too64 znaków używany do hello Nazwa zasobu.</span><span class="sxs-lookup"><span data-stu-id="36e66-168">When you create a virtual machine (VM), Azure requires a VM name of up too64 characters that is used for hello resource name.</span></span> <span data-ttu-id="36e66-169">Platforma Azure hello tej samej nazwy dla hello system operacyjny zainstalowany na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e66-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="36e66-170">Jednak te nazwy może nie zawsze być hello tego samego.</span><span class="sxs-lookup"><span data-stu-id="36e66-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="36e66-171">Jeśli maszyna wirtualna została utworzona z pliku obrazu vhd zawierającego system operacyjny, hello nazwę maszyny Wirtualnej na platformie Azure mogą się różnić od hello nazwa komputera systemu operacyjnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e66-171">If a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="36e66-172">Takiej sytuacji można dodać stopień trudności tooVM zarządzania, które w związku z tym nie jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="36e66-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="36e66-173">Przypisz hello hello zasobu maszyny Wirtualnej Azure takie same nazwy jako nazwy komputera hello przypisanie toohello system operacyjny tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e66-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="36e66-174">Firma Microsoft zaleca tę nazwę maszyny Wirtualnej Azure hello jest hello taki sam jak hello bazowy nazwa komputera systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="36e66-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="36e66-175">Nazwy kont magazynu</span><span class="sxs-lookup"><span data-stu-id="36e66-175">Storage account names</span></span>
<span data-ttu-id="36e66-176">Ta sekcja nie ma zastosowania zbyt[dysków zarządzanych Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ponieważ nie należy tworzyć oddzielnego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="36e66-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="36e66-177">Dla niezarządzanego dysków kont magazynu ma specjalne zasady dotyczące ich nazw.</span><span class="sxs-lookup"><span data-stu-id="36e66-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="36e66-178">Można używać tylko małe litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="36e66-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="36e66-179">Aby uzyskać więcej informacji, zobacz [Utwórz konto magazynu](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="36e66-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="36e66-180">Ponadto hello nazwy konta magazynu, z core.windows.net, należy globalnie prawidłową, unikatową nazwę DNS.</span><span class="sxs-lookup"><span data-stu-id="36e66-180">Additionally, hello storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="36e66-181">Na przykład jeśli konto magazynu hello jest nazywane mojekontomagazynu, hello poniższe nazwy DNS wynikowy powinna być unikatowa:</span><span class="sxs-lookup"><span data-stu-id="36e66-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="36e66-182">mystorageaccount.blob.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="36e66-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="36e66-183">mystorageaccount.TABLE.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="36e66-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="36e66-184">mystorageaccount.Queue.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="36e66-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="36e66-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36e66-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

