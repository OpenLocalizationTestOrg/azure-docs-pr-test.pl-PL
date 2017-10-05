---
title: "Dyski maszyn wirtualnych IaaS platformy Azure — często zadawane pytania (FAQ) | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące dysków maszyny Wirtualnej Azure IaaS i dysków w warstwie premium (zarządzanych i niezarządzanych)"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 9e5eed35334f1b95441b8181c8e90645be78b389
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="b1704-103">Często zadawane pytania dotyczące dyski maszyny Wirtualnej Azure IaaS i zarządzane i niezarządzane — wersja premium</span><span class="sxs-lookup"><span data-stu-id="b1704-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="b1704-104">Ten artykuł zawiera odpowiedzi na niektóre często zadawane pytania dotyczące dysków zarządzanych Azure i usługa Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="b1704-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="b1704-105">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="b1704-105">Managed Disks</span></span>

<span data-ttu-id="b1704-106">**Co to jest Azure zarządzane dyski?**</span><span class="sxs-lookup"><span data-stu-id="b1704-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="b1704-107">Dyski zarządzane jest funkcja, która ułatwia zarządzanie dyskami dla maszyn wirtualnych IaaS platformy Azure dzięki obsłudze Zarządzanie kontem magazynu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="b1704-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="b1704-108">Aby uzyskać więcej informacji, zobacz [omówienie dysków zarządzanych](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1704-108">For more information, see the [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="b1704-109">**Jeśli utworzyć standardowych dysków zarządzanych z istniejącego dysku VHD, 80 GB, ile będzie tego koszt mnie?**</span><span class="sxs-lookup"><span data-stu-id="b1704-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="b1704-110">Standardowa dysków zarządzanych utworzone na podstawie wirtualny dysk twardy 80 GB jest traktowany jako dalej rozmiar dostępnych dysków w warstwie standardowa, który jest dyskiem s10 w warstwie.</span><span class="sxs-lookup"><span data-stu-id="b1704-110">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="b1704-111">Są naliczane opłaty zgodnie z s10 w warstwie cenowej dysku.</span><span class="sxs-lookup"><span data-stu-id="b1704-111">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="b1704-112">Aby uzyskać więcej informacji, odwiedź [stronę cennika](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="b1704-112">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="b1704-113">**Czy istnieją kosztów transakcji dla standardowych dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="b1704-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="b1704-114">Tak.</span><span class="sxs-lookup"><span data-stu-id="b1704-114">Yes.</span></span> <span data-ttu-id="b1704-115">W przypadku naliczona opłata za każdą transakcję.</span><span class="sxs-lookup"><span data-stu-id="b1704-115">You're charged for each transaction.</span></span> <span data-ttu-id="b1704-116">Aby uzyskać więcej informacji, odwiedź [stronę cennika](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="b1704-116">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="b1704-117">**Dla standardowych dysków zarządzanych I obciążymy rzeczywisty rozmiar danych na dysku lub elastycznie pojemność dysku?**</span><span class="sxs-lookup"><span data-stu-id="b1704-117">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="b1704-118">Są naliczane opłaty oparte na elastycznie pojemność dysku.</span><span class="sxs-lookup"><span data-stu-id="b1704-118">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="b1704-119">Aby uzyskać więcej informacji, odwiedź [stronę cennika](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="b1704-119">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="b1704-120">**Jak jest inny niż dyski niezarządzane cennik dysków zarządzanych w warstwie premium?**</span><span class="sxs-lookup"><span data-stu-id="b1704-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="b1704-121">Cennik dysków zarządzanych w warstwie premium jest taka sama jak dyski premium niezarządzane.</span><span class="sxs-lookup"><span data-stu-id="b1704-121">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="b1704-122">**Można zmienić typu (standardowy lub Premium) konta magazynu z dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="b1704-122">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="b1704-123">Tak.</span><span class="sxs-lookup"><span data-stu-id="b1704-123">Yes.</span></span> <span data-ttu-id="b1704-124">Można zmienić typu konta magazynu dysków zarządzanych za pomocą portalu Azure, programu PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b1704-124">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="b1704-125">**Czy istnieje sposób, aby I skopiuj lub wyeksportować dysków zarządzanych do konta magazynu prywatnej?**</span><span class="sxs-lookup"><span data-stu-id="b1704-125">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="b1704-126">Tak.</span><span class="sxs-lookup"><span data-stu-id="b1704-126">Yes.</span></span> <span data-ttu-id="b1704-127">Dyski zarządzane można wyeksportować za pomocą portalu Azure, programu PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b1704-127">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="b1704-128">**Aby utworzyć dysków zarządzanych za pomocą innej subskrypcji można użyć pliku VHD na koncie magazynu platformy Azure?**</span><span class="sxs-lookup"><span data-stu-id="b1704-128">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="b1704-129">Nie.</span><span class="sxs-lookup"><span data-stu-id="b1704-129">No.</span></span>

<span data-ttu-id="b1704-130">**Aby utworzyć dysków zarządzanych w innym regionie można użyć pliku VHD na koncie magazynu platformy Azure?**</span><span class="sxs-lookup"><span data-stu-id="b1704-130">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="b1704-131">Nie.</span><span class="sxs-lookup"><span data-stu-id="b1704-131">No.</span></span>

<span data-ttu-id="b1704-132">**Czy istnieją jakiekolwiek ograniczenia skali dla klientów korzystających z zarządzanego dyski?**</span><span class="sxs-lookup"><span data-stu-id="b1704-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="b1704-133">Dyski zarządzane eliminuje limity skojarzonego z kontami magazynu.</span><span class="sxs-lookup"><span data-stu-id="b1704-133">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="b1704-134">Jednak liczbę zarządzanych dysków dla subskrypcji jest ograniczona do 2000 domyślnie.</span><span class="sxs-lookup"><span data-stu-id="b1704-134">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="b1704-135">Możesz wywołać pomocy technicznej, aby zwiększyć ten numer.</span><span class="sxs-lookup"><span data-stu-id="b1704-135">You can call support to increase this number.</span></span>

<span data-ttu-id="b1704-136">**Czy można wykonać przyrostowej migawki dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="b1704-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="b1704-137">Nie.</span><span class="sxs-lookup"><span data-stu-id="b1704-137">No.</span></span> <span data-ttu-id="b1704-138">Pełną kopię dysków zarządzanych sprawia, że bieżąca funkcja migawki.</span><span class="sxs-lookup"><span data-stu-id="b1704-138">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="b1704-139">Jednak firma Microsoft planuje obsługuje przyrostowe migawek w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="b1704-139">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="b1704-140">**Maszyny wirtualne w zestawie dostępności może zawierać kombinację dysków zarządzane i niezarządzane?**</span><span class="sxs-lookup"><span data-stu-id="b1704-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="b1704-141">Nie.</span><span class="sxs-lookup"><span data-stu-id="b1704-141">No.</span></span> <span data-ttu-id="b1704-142">Maszyn wirtualnych w zestawie dostępności muszą używać wszystkich zarządzanych dysków lub wszystkie dyski niezarządzane.</span><span class="sxs-lookup"><span data-stu-id="b1704-142">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="b1704-143">Podczas tworzenia zestawu dostępności można wybrać typu dysków, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="b1704-143">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="b1704-144">**Jest domyślną opcją w portalu Azure zarządzane dyski?**</span><span class="sxs-lookup"><span data-stu-id="b1704-144">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="b1704-145">Aktualnie nie ale stanie się domyślnie w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="b1704-145">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="b1704-146">**Można utworzyć pusty dysk zarządzany?**</span><span class="sxs-lookup"><span data-stu-id="b1704-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="b1704-147">Tak.</span><span class="sxs-lookup"><span data-stu-id="b1704-147">Yes.</span></span> <span data-ttu-id="b1704-148">Możesz utworzyć pusty dysk.</span><span class="sxs-lookup"><span data-stu-id="b1704-148">You can create an empty disk.</span></span> <span data-ttu-id="b1704-149">Dysk zarządzany można tworzyć niezależnie od maszyny Wirtualnej, na przykład bez dołączeniu go do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b1704-149">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="b1704-150">**Co to liczba domen błędów obsługiwanych dostępności ustawiono używającym dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="b1704-150">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="b1704-151">W zależności od regionu, w którym znajduje się zestaw dostępności, który używa dysków zarządzanych liczba domen błędów obsługiwanych jest 2 lub 3.</span><span class="sxs-lookup"><span data-stu-id="b1704-151">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="b1704-152">**Jak jest to konto magazynu w warstwie standardowa dla diagnostyki Konfigurowanie?**</span><span class="sxs-lookup"><span data-stu-id="b1704-152">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="b1704-153">Skonfiguruj konto magazynu prywatne dla diagnostyki maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b1704-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="b1704-154">W przyszłości firma Microsoft planuje także przełącznik diagnostyki do zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="b1704-154">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="b1704-155">**Jakiego rodzaju obsługi kontroli dostępu opartej na rolach jest dostępna dla dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="b1704-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="b1704-156">Zarządzane dysków obsługuje trzy kluczowe domyślne role:</span><span class="sxs-lookup"><span data-stu-id="b1704-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="b1704-157">Właściciel: Mogą zarządzać wszystkim łącznie z dostępem</span><span class="sxs-lookup"><span data-stu-id="b1704-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="b1704-158">Współautor: Mogą zarządzać wszystkim poza dostępem</span><span class="sxs-lookup"><span data-stu-id="b1704-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="b1704-159">Czytnik: Można przeglądać wszystko, ale nie można wprowadzić zmian</span><span class="sxs-lookup"><span data-stu-id="b1704-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="b1704-160">**Czy istnieje sposób, aby I skopiuj lub wyeksportować dysków zarządzanych do konta magazynu prywatnej?**</span><span class="sxs-lookup"><span data-stu-id="b1704-160">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="b1704-161">Można pobrać sygnatury dostępu współdzielonego tylko do odczytu identyfikatora URI dla dysków zarządzanych i go użyć do kopiowania zawartości do magazynu konta lub lokalnego magazynu prywatnych.</span><span class="sxs-lookup"><span data-stu-id="b1704-161">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="b1704-162">**Można utworzyć kopię dysku zarządzanego?**</span><span class="sxs-lookup"><span data-stu-id="b1704-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="b1704-163">Klienci mogą migawki dysków zarządzanych, a następnie użyj migawki do tworzenia dysków zarządzanych w innym.</span><span class="sxs-lookup"><span data-stu-id="b1704-163">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="b1704-164">**Niezarządzane dyski nadal są obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="b1704-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="b1704-165">Tak.</span><span class="sxs-lookup"><span data-stu-id="b1704-165">Yes.</span></span> <span data-ttu-id="b1704-166">Firma Microsoft obsługuje dyski niezarządzane i zarządzane.</span><span class="sxs-lookup"><span data-stu-id="b1704-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="b1704-167">Zalecamy dysków zarządzanych dla nowych obciążeń, a migracja bieżącego obciążeń do zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="b1704-167">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="b1704-168">**Jeśli I Utwórz dysk 128 GB i dopiero potem zwiększyć rozmiar 130 GB I obciążymy dla następnego rozmiar dysku (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="b1704-168">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="b1704-169">Tak.</span><span class="sxs-lookup"><span data-stu-id="b1704-169">Yes.</span></span>

<span data-ttu-id="b1704-170">**Magazyn lokalnie nadmiarowy, Magazyn geograficznie nadmiarowy, można utworzyć i dyskach zarządzanych przez Magazyn strefowo nadmiarowy?**</span><span class="sxs-lookup"><span data-stu-id="b1704-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="b1704-171">Dyskach zarządzanych platformy Azure obsługuje obecnie tylko lokalnie nadmiarowego magazynu zarządzane dyski.</span><span class="sxs-lookup"><span data-stu-id="b1704-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="b1704-172">**Można zmniejszyć lub downsize dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="b1704-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="b1704-173">Nie.</span><span class="sxs-lookup"><span data-stu-id="b1704-173">No.</span></span> <span data-ttu-id="b1704-174">Ta funkcja nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="b1704-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="b1704-175">**Właściwość Nazwa komputera można zmienić po specjalistycznej (nie utworzone przy użyciu narzędzia przygotowywania systemu lub uogólniony) dysku systemu operacyjnego jest używany do udostępnienia maszyny Wirtualnej?**</span><span class="sxs-lookup"><span data-stu-id="b1704-175">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="b1704-176">Nie.</span><span class="sxs-lookup"><span data-stu-id="b1704-176">No.</span></span> <span data-ttu-id="b1704-177">Nie można zaktualizować właściwości Nazwa komputera.</span><span class="sxs-lookup"><span data-stu-id="b1704-177">You can't update the computer name property.</span></span> <span data-ttu-id="b1704-178">Nowa maszyna wirtualna dziedziczy z elementu nadrzędnego maszyny Wirtualnej, który został użyty do utworzenia dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b1704-178">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="b1704-179">**Gdzie można znaleźć przykładowych szablonów usługi Azure Resource Manager do tworzenia maszyn wirtualnych z dyskami zarządzanych**</span><span class="sxs-lookup"><span data-stu-id="b1704-179">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="b1704-180">Lista szablonów przy użyciu dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="b1704-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="b1704-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="b1704-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="b1704-182">Zarządzane dysków i szyfrowanie usługi magazynu</span><span class="sxs-lookup"><span data-stu-id="b1704-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="b1704-183">**Jest szyfrowanie usługi Magazyn Azure domyślnie podczas tworzenia dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="b1704-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="b1704-184">Tak.</span><span class="sxs-lookup"><span data-stu-id="b1704-184">Yes.</span></span>

<span data-ttu-id="b1704-185">**Kto zarządza klucze szyfrowania?**</span><span class="sxs-lookup"><span data-stu-id="b1704-185">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="b1704-186">Firma Microsoft zarządza kluczy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="b1704-186">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="b1704-187">**Do zarządzanych dysków można wyłączyć szyfrowanie usługi Magazyn?**</span><span class="sxs-lookup"><span data-stu-id="b1704-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="b1704-188">Nie.</span><span class="sxs-lookup"><span data-stu-id="b1704-188">No.</span></span>

<span data-ttu-id="b1704-189">**Jest szyfrowanie usługi Magazyn dostępna tylko w określonych regionach?**</span><span class="sxs-lookup"><span data-stu-id="b1704-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="b1704-190">Nie.</span><span class="sxs-lookup"><span data-stu-id="b1704-190">No.</span></span> <span data-ttu-id="b1704-191">Jest dostępna we wszystkich regionach, gdzie dostępna jest opcja dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="b1704-191">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="b1704-192">Dyski zarządzane jest dostępna we wszystkich regionach publicznego i Niemczech.</span><span class="sxs-lookup"><span data-stu-id="b1704-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="b1704-193">**Jak można sprawdzić w przypadku zarządzanych dysku są szyfrowane?**</span><span class="sxs-lookup"><span data-stu-id="b1704-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="b1704-194">Można ustalić czas utworzenia dysków zarządzanych w portalu Azure, interfejsu wiersza polecenia Azure i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1704-194">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="b1704-195">Gdy czas po 9 czerwca 2017 dysku są szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="b1704-195">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="b1704-196">**Jak można zaszyfrować Moje istniejących dysków, które zostały utworzone przed 10 czerwca 2017 r.**</span><span class="sxs-lookup"><span data-stu-id="b1704-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="b1704-197">Począwszy od 10 czerwca 2017 nowych danych istniejących dysków zarządzanych jest szyfrowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b1704-197">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="b1704-198">Możemy również planowania szyfrowania istniejących danych i szyfrowanie nastąpi asynchronicznie w tle.</span><span class="sxs-lookup"><span data-stu-id="b1704-198">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="b1704-199">Jeśli musi teraz zaszyfrować dane, należy utworzyć kopię dysku.</span><span class="sxs-lookup"><span data-stu-id="b1704-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="b1704-200">Nowe dyski zostaną zaszyfrowane.</span><span class="sxs-lookup"><span data-stu-id="b1704-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="b1704-201">Kopiowanie dysków zarządzanych przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b1704-201">Copy managed disks by using the Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="b1704-202">Kopiowanie dysków zarządzanych za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1704-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="b1704-203">**Są zarządzane migawki i obrazy szyfrowane?**</span><span class="sxs-lookup"><span data-stu-id="b1704-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="b1704-204">Tak.</span><span class="sxs-lookup"><span data-stu-id="b1704-204">Yes.</span></span> <span data-ttu-id="b1704-205">Wszystkie zarządzane migawki i obrazy utworzone po 9 czerwca 2017 r są szyfrowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b1704-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="b1704-206">**Czy mogę przekonwertować maszyny wirtualne z dyskami niezarządzane, które znajdują się na kontach magazynu, które są lub wcześniej były szyfrowane do zarządzanych dysków**</span><span class="sxs-lookup"><span data-stu-id="b1704-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="b1704-207">Tak</span><span class="sxs-lookup"><span data-stu-id="b1704-207">Yes</span></span>

<span data-ttu-id="b1704-208">**Wyeksportowane wirtualnego dysku twardego z zarządzanego dysku lub migawka także będą zaszyfrowane?**</span><span class="sxs-lookup"><span data-stu-id="b1704-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="b1704-209">Nie.</span><span class="sxs-lookup"><span data-stu-id="b1704-209">No.</span></span> <span data-ttu-id="b1704-210">Ale jeśli możesz wyeksportować do konta magazynu zaszyfrowanego dysku VHD z zaszyfrowanego zarządzane dysku lub migawki, a następnie jest on zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="b1704-210">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="b1704-211">Dyski Premium: zarządzanych i niezarządzanych</span><span class="sxs-lookup"><span data-stu-id="b1704-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="b1704-212">**Jeśli maszyna wirtualna używa rozmiar serii, która obsługuje magazyn w warstwie Premium, takich jak DSv2, można dołączyć zarówno premium i dyski standardowe danych?**</span><span class="sxs-lookup"><span data-stu-id="b1704-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="b1704-213">Tak.</span><span class="sxs-lookup"><span data-stu-id="b1704-213">Yes.</span></span>

<span data-ttu-id="b1704-214">**Do rozmiaru serii, która nie obsługuje usługi Premium Storage, takich jak seria D, Dv2, G lub F można podłączyć zarówno premium i dyski standardowe danych?**</span><span class="sxs-lookup"><span data-stu-id="b1704-214">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="b1704-215">Nie.</span><span class="sxs-lookup"><span data-stu-id="b1704-215">No.</span></span> <span data-ttu-id="b1704-216">Tylko dyski standardowe danych można dołączyć do maszyn wirtualnych, które nie używają serii rozmiar, który obsługuje magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="b1704-216">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="b1704-217">**Jeśli dysk danych — warstwa premium można utworzyć z istniejącego dysku VHD, który był 80 GB, ile będzie tego koszt?**</span><span class="sxs-lookup"><span data-stu-id="b1704-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="b1704-218">Dysk z danymi premium utworzone na podstawie wirtualny dysk twardy 80 GB jest traktowany jako rozmiaru dysku premium dostępne dalej, który jest dyskiem P10.</span><span class="sxs-lookup"><span data-stu-id="b1704-218">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="b1704-219">Są naliczane opłaty zgodnie z cennik P10 dysku.</span><span class="sxs-lookup"><span data-stu-id="b1704-219">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="b1704-220">**Czy istnieją koszty transakcji do użycia magazyn w warstwie Premium?**</span><span class="sxs-lookup"><span data-stu-id="b1704-220">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="b1704-221">Brak koszt stały rozmiar każdego dysku, które pojawia się z określonym limity udostępnionym IOPS i przepustowość.</span><span class="sxs-lookup"><span data-stu-id="b1704-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="b1704-222">Inne koszty są przepustowości wychodzącej i pojemność migawki, jeśli ma to zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="b1704-222">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="b1704-223">Aby uzyskać więcej informacji, odwiedź [stronę cennika](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="b1704-223">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="b1704-224">**Jakie są limity dla IOPS i przepływność, którą można pobrać z pamięci podręcznej dysku?**</span><span class="sxs-lookup"><span data-stu-id="b1704-224">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="b1704-225">Łączne limity dla pamięci podręcznej i lokalny dysk SSD dla serii DS są 4000 IOPS na podstawowe i 33 MB na sekundę na podstawowe.</span><span class="sxs-lookup"><span data-stu-id="b1704-225">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="b1704-226">Serii GS oferuje 5000 IOPS na podstawowe i 50 MB na sekundę na podstawowe.</span><span class="sxs-lookup"><span data-stu-id="b1704-226">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="b1704-227">**Lokalny dysk SSD jest obsługiwana dla maszyny Wirtualnej, zarządzane dyski?**</span><span class="sxs-lookup"><span data-stu-id="b1704-227">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="b1704-228">Lokalny dysk SSD jest tymczasowego magazynu, który jest dołączony do maszyny Wirtualnej dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="b1704-228">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="b1704-229">Jest nie żadnymi dodatkowymi kosztami dla tego magazynu tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="b1704-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="b1704-230">Firma Microsoft zaleca, aby używać tego lokalny dysk SSD do przechowywania danych aplikacji, ponieważ nie jest on utrwalane w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b1704-230">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="b1704-231">**Czy istnieją żadnych skutków PRZYCINANIE do użytku na dyski premium?**</span><span class="sxs-lookup"><span data-stu-id="b1704-231">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="b1704-232">Nie ma żadnych wadą interfejsu użyciem PRZYCINANIE na dyskach platformy Azure w warstwie premium albo lub dyski standardowe.</span><span class="sxs-lookup"><span data-stu-id="b1704-232">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="b1704-233">Nowy rozmiar dysku: zarządzanych i niezarządzanych</span><span class="sxs-lookup"><span data-stu-id="b1704-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="b1704-234">**Co to jest największy rozmiar dysku systemu operacyjnego i dysków z danymi obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="b1704-234">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="b1704-235">Typ partycji, który Azure obsługuje dla dysku systemu operacyjnego jest główny rekord rozruchowy (MBR).</span><span class="sxs-lookup"><span data-stu-id="b1704-235">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="b1704-236">Obsługuje format MBR dysk rozmiar do 2 TB.</span><span class="sxs-lookup"><span data-stu-id="b1704-236">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="b1704-237">Największy rozmiar, który Azure obsługuje dla dysku systemu operacyjnego jest 2 TB.</span><span class="sxs-lookup"><span data-stu-id="b1704-237">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="b1704-238">Azure obsługuje do 4 TB dla dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="b1704-238">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="b1704-239">**Co to jest największy rozmiar strony obiektu blob jest obsługiwana?**</span><span class="sxs-lookup"><span data-stu-id="b1704-239">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="b1704-240">Największy rozmiar strony obiektu blob Azure obsługuje jest 8 TB (8191 GB).</span><span class="sxs-lookup"><span data-stu-id="b1704-240">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="b1704-241">Nie obsługujemy stronicowe obiekty BLOB większych niż 4 TB (4,095 GB) dołączona do maszyny Wirtualnej jako dane lub dysków systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b1704-241">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="b1704-242">**Należy użyć nowej wersji narzędzi platformy Azure do tworzenia, Dołącz, zmienianie rozmiaru i przekaż dysków większych niż 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="b1704-242">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="b1704-243">Nie trzeba uaktualnić Azure istniejących narzędzi do tworzenia, Dołącz lub zmieniać rozmiar dysków większych niż 1 TB.</span><span class="sxs-lookup"><span data-stu-id="b1704-243">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="b1704-244">Aby przesłać plik wirtualnego dysku twardego z lokalnymi bezpośrednio na platformie Azure jako stronicowy obiekt blob lub niezarządzane dysku, należy użyć najnowszej zestawów narzędzia:</span><span class="sxs-lookup"><span data-stu-id="b1704-244">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="b1704-245">Narzędzia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b1704-245">Azure tools</span></span>      | <span data-ttu-id="b1704-246">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="b1704-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="b1704-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1704-247">Azure PowerShell</span></span> | <span data-ttu-id="b1704-248">Numer wersji 4.1.0: czerwiec 2017 wersji lub nowszy</span><span class="sxs-lookup"><span data-stu-id="b1704-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="b1704-249">Interfejs wiersza polecenia platformy Azure w wersji 1</span><span class="sxs-lookup"><span data-stu-id="b1704-249">Azure CLI v1</span></span>     | <span data-ttu-id="b1704-250">Numer wersji 0.10.13: 2017 może zwolnić lub nowszy</span><span class="sxs-lookup"><span data-stu-id="b1704-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="b1704-251">Narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="b1704-251">AzCopy</span></span>           | <span data-ttu-id="b1704-252">Numer wersji 6.1.0: czerwiec 2017 wersji lub nowszy</span><span class="sxs-lookup"><span data-stu-id="b1704-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="b1704-253">Obsługa interfejsu wiersza polecenia Azure w wersji 2 i Eksploratora usługi Storage platformy Azure będzie dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="b1704-253">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="b1704-254">**P4 i P6 rozmiary dysków są obsługiwane dla niezarządzanego dysków lub stronicowych obiektów blob?**</span><span class="sxs-lookup"><span data-stu-id="b1704-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="b1704-255">Nie.</span><span class="sxs-lookup"><span data-stu-id="b1704-255">No.</span></span> <span data-ttu-id="b1704-256">P4 (32 GB) i P6 rozmiary dysków (64 GB) są obsługiwane tylko w przypadku dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="b1704-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="b1704-257">Obsługa dysków niezarządzane i stronicowe obiekty BLOB będzie dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="b1704-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="b1704-258">**Jeśli Mój istniejący premium zarządzane na dysku z mniej niż 64 GB został utworzony przed włączeniem małego dysku (około 15 czerwca 2017 r), jak jest on rozliczany?**</span><span class="sxs-lookup"><span data-stu-id="b1704-258">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="b1704-259">Istniejące premium małe dyski mniej niż 64 GB nadal będą naliczane opłaty zgodnie z warstwy cenowej P10.</span><span class="sxs-lookup"><span data-stu-id="b1704-259">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="b1704-260">**Jak można zmienić warstwy dysków premium małe dyski, mniejsze niż 64 GB z P10 P4 lub P6?**</span><span class="sxs-lookup"><span data-stu-id="b1704-260">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="b1704-261">Można utworzyć migawkę małe dyski, a następnie utwórz dysk, aby automatycznie Zmień warstwę cenową P4 lub P6 zależnie od rozmiaru elastycznie.</span><span class="sxs-lookup"><span data-stu-id="b1704-261">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="b1704-262">Co zrobić, jeśli mojego pytania nie ma odpowiedzi w tym miejscu?</span><span class="sxs-lookup"><span data-stu-id="b1704-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="b1704-263">Jeśli Twoje pytanie nie ma na liście w tym miejscu, Daj nam znać, a pomożemy Ci znaleźć odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="b1704-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="b1704-264">W komentarzach można Zadaj pytanie na końcu tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="b1704-264">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="b1704-265">Aby współpracować z zespołu usługi Magazyn Azure i innymi członkami społeczności informacje w tym artykule, należy użyć MSDN [forum usługi Azure Storage](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="b1704-265">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="b1704-266">Aby poprosić o funkcje, przesłać żądania i pomysłami, które [forum opinii usługi Azure Storage](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="b1704-266">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
