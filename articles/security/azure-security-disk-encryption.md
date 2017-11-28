---
title: "Szyfrowanie dysków Azure dla systemu Windows i maszyn wirtualnych systemu Linux IaaS | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie programu Microsoft Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: a4f20fc19ae40561d042d5cff744a030014f75c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="c7536-103">Szyfrowanie dysków Azure dla systemu Windows i maszyn wirtualnych systemu Linux IaaS</span><span class="sxs-lookup"><span data-stu-id="c7536-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="c7536-104">Microsoft Azure jest silnie zobowiązane do zapewnienia prywatności danych, suwerenności danych i umożliwia sterowanie platformy Azure hostowanej danych za pomocą wielu zaawansowanych technologii szyfrowania, sterowania i zarządzania kluczami szyfrowania, inspekcji i kontroli dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="c7536-104">Microsoft Azure is strongly committed to ensuring your data privacy, data sovereignty and enables you to control your Azure hosted data through a range of advanced technologies to encrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="c7536-105">Klienci Azure zapewnia elastyczność wyboru rozwiązania, które będzie najlepiej odpowiadać ich potrzeb biznesowych.</span><span class="sxs-lookup"><span data-stu-id="c7536-105">This provides Azure customers the flexibility to choose the solution that best meets their business needs.</span></span> <span data-ttu-id="c7536-106">W tym dokumencie firma Microsoft podstawowe informacje na temat nowego rozwiązania technologii "Szyfrowania dysków Azure dla systemu Windows i Linux IaaS maszyny Wirtualnej na" Aby chronić i ochrony danych w celu spełnienia organizacji bezpieczeństwa i zgodności zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="c7536-106">In this paper, we will introduce you to a new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” to help protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="c7536-107">Papieru zapewnia napotka szczegółowe wskazówki dotyczące sposobu używania funkcji szyfrowania dysków Azure w tym obsługiwane scenariusze i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c7536-107">The paper provides detailed guidance on how to use the Azure disk encryption features including the supported scenarios and the user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-108">Zastosowanie niektórych zaleceń zamieszczonych może zwiększyć danych, sieci i użycia zasobów obliczeniowych, co powoduje dodatkowych kosztów licencji lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c7536-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="c7536-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c7536-109">Overview</span></span>
<span data-ttu-id="c7536-110">Szyfrowanie dysków Azure jest nową możliwość, która pomaga szyfrowania dysków maszyny wirtualnej systemu Windows i Linux IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7536-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="c7536-111">Szyfrowanie dysków Azure korzysta ze standardu branżowego [funkcji BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funkcji systemu Windows i [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) funkcji systemu Linux w celu zapewnienia szyfrowania woluminów systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="c7536-111">Azure Disk Encryption leverages the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks.</span></span> <span data-ttu-id="c7536-112">Rozwiązanie jest zintegrowany z [usługi Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) ułatwiają kontrolowanie i zarządzanie nimi klucze szyfrowania dysku i kluczy tajnych w magazynie kluczy subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c7536-112">The solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="c7536-113">Rozwiązanie zapewnia również, że wszystkie dane na dyskach maszyny wirtualnej są szyfrowane, gdy w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-113">The solution also ensures that all data on the virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="c7536-114">Szyfrowanie dysków Azure dla systemu Windows i maszyn wirtualnych systemu Linux IaaS, jest teraz w **ogólnej dostępności** we wszystkich regionach publicznej platformy Azure i regiony AzureGov standardowe maszyn wirtualnych i maszyn wirtualnych z magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="c7536-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="c7536-115">Scenariusze szyfrowania</span><span class="sxs-lookup"><span data-stu-id="c7536-115">Encryption scenarios</span></span>
<span data-ttu-id="c7536-116">Rozwiązanie szyfrowania dysków Azure obsługuje następujących scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="c7536-116">The Azure Disk Encryption solution supports the following customer scenarios:</span></span>

* <span data-ttu-id="c7536-117">Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS utworzone na podstawie wstępnie zaszyfrowany dysk VHD i kluczy szyfrowania</span><span class="sxs-lookup"><span data-stu-id="c7536-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="c7536-118">Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS utworzone z obrazów obsługiwane galerii Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-118">Enable encryption on new IaaS VMs created from the supported Azure Gallery images</span></span>
* <span data-ttu-id="c7536-119">Włącz szyfrowanie dla istniejących maszyn wirtualnych IaaS działające na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="c7536-120">Wyłącz szyfrowanie na maszynach wirtualnych IaaS systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c7536-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="c7536-121">Wyłącz szyfrowanie dysków danych dla maszyn wirtualnych systemu Linux IaaS</span><span class="sxs-lookup"><span data-stu-id="c7536-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="c7536-122">Włącz szyfrowanie dysków zarządzanych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="c7536-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="c7536-123">Aktualizowanie ustawień szyfrowania istniejących zaszyfrowanych inne niż premium magazynu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c7536-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="c7536-124">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych, zaszyfrowane za pomocą klucza szyfrowania</span><span class="sxs-lookup"><span data-stu-id="c7536-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="c7536-125">Rozwiązanie obsługuje następujące scenariusze dla maszyn wirtualnych IaaS, jeśli są włączone w systemie Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="c7536-125">The solution supports the following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="c7536-126">Integracja z usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c7536-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="c7536-127">Maszyny wirtualne warstwy standardowa: [A, D DS, G, GS, F i itp szeregów maszyn wirtualnych IaaS](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="c7536-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="c7536-128">Włącz szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS i maszyn wirtualnych dysków zarządzanych z obsługiwanych obrazów w galerii Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from the supported Azure Gallery images</span></span>
* <span data-ttu-id="c7536-129">Wyłącz szyfrowanie dysków systemu operacyjnego i danych dla maszyn wirtualnych IaaS systemu Windows i dysków zarządzanych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="c7536-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="c7536-130">Wyłącz szyfrowanie dysków danych dla maszyn wirtualnych systemu Linux IaaS i dysków zarządzanych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="c7536-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="c7536-131">Włącz szyfrowanie dla maszyn wirtualnych IaaS systemem kliencki system operacyjny Windows</span><span class="sxs-lookup"><span data-stu-id="c7536-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="c7536-132">Włącz szyfrowanie dla woluminów przy użyciu ścieżki instalacji</span><span class="sxs-lookup"><span data-stu-id="c7536-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="c7536-133">Włącz szyfrowanie dla maszyn wirtualnych systemu Linux skonfigurowany z dysku przy użyciu mdadm zastosowanie rozkładania (RAID)</span><span class="sxs-lookup"><span data-stu-id="c7536-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="c7536-134">Włącz szyfrowanie dla maszyn wirtualnych systemu Linux przy użyciu LVM dla dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="c7536-135">Włącz szyfrowanie dla maszyn wirtualnych systemu Windows skonfigurowane z funkcją miejsca do magazynowania</span><span class="sxs-lookup"><span data-stu-id="c7536-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="c7536-136">Aktualizowanie ustawień szyfrowania istniejących zaszyfrowanych inne niż premium magazynu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c7536-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="c7536-137">Wszystkie publiczne Azure i AzureGov regiony są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c7536-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="c7536-138">Rozwiązanie nie obsługuje następujące scenariusze, funkcje i technologie:</span><span class="sxs-lookup"><span data-stu-id="c7536-138">The solution does not support the following scenarios, features, and technology:</span></span>

* <span data-ttu-id="c7536-139">Maszyny wirtualne IaaS warstwa podstawowa</span><span class="sxs-lookup"><span data-stu-id="c7536-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="c7536-140">Wyłączenie szyfrowania na dysku systemu operacyjnego dla maszyn wirtualnych systemu Linux IaaS</span><span class="sxs-lookup"><span data-stu-id="c7536-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="c7536-141">Wyłączenie szyfrowania na dysku danych, jeśli dysk systemu operacyjnego jest szyfrowany dla maszyn wirtualnych systemu Linux Iaas</span><span class="sxs-lookup"><span data-stu-id="c7536-141">Disabling encryption on a data drive if the OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="c7536-142">Maszyny wirtualne IaaS, które są tworzone za pomocą klasycznego metodę tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c7536-142">IaaS VMs that are created by using the classic VM creation method</span></span>
* <span data-ttu-id="c7536-143">Włącz szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS niestandardowych obrazów klienta nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="c7536-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="c7536-144">Włącz enccryption w systemie operacyjnym Linux LVM dysk nie jest obsługiwany obecnie.</span><span class="sxs-lookup"><span data-stu-id="c7536-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="c7536-145">Ta obsługa rozpocznie się wkrótce.</span><span class="sxs-lookup"><span data-stu-id="c7536-145">This support will come soon.</span></span>
* <span data-ttu-id="c7536-146">Integracja z lokalnej usługi zarządzania kluczami</span><span class="sxs-lookup"><span data-stu-id="c7536-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="c7536-147">Usługa pliki Azure (udostępnionego systemu plików), sieciowego systemu plików (NFS), dynamiczne woluminy i maszyn wirtualnych systemu Windows, które są skonfigurowane przy użyciu systemów opartych na oprogramowaniu RAID</span><span class="sxs-lookup"><span data-stu-id="c7536-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="c7536-148">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych, szyfrowane bez klucza szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="c7536-149">Zaktualizuj ustawienia szyfrowania istniejącego magazynu premium zaszyfrowanych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-150">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych jest obsługiwana tylko dla maszyn wirtualnych, które są szyfrowane przy użyciu konfiguracji KEK.</span><span class="sxs-lookup"><span data-stu-id="c7536-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="c7536-151">Nie jest obsługiwana na maszynach wirtualnych, które są szyfrowane bez KEK.</span><span class="sxs-lookup"><span data-stu-id="c7536-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="c7536-152">KEK jest opcjonalnym parametrem, który włącza szyfrowanie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="c7536-153">Ta obsługa zostanie wkrótce uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="c7536-153">This support is coming soon.</span></span>
> <span data-ttu-id="c7536-154">Aktualizuj ustawienia szyfrowania istniejący magazyn w warstwie premium zaszyfrowanych maszyny Wirtualnej nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c7536-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="c7536-155">Ta obsługa zostanie wkrótce uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="c7536-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="c7536-156">Funkcji szyfrowania</span><span class="sxs-lookup"><span data-stu-id="c7536-156">Encryption features</span></span>
<span data-ttu-id="c7536-157">Po włączeniu i wdrożeniu szyfrowania dysków Azure dla maszyn wirtualnych IaaS platformy Azure, następujące funkcje są włączone, w zależności od Podana konfiguracja:</span><span class="sxs-lookup"><span data-stu-id="c7536-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, the following capabilities are enabled, depending on the configuration provided:</span></span>

* <span data-ttu-id="c7536-158">Szyfrowania woluminu systemu operacyjnego, aby chronić wolumin rozruchowy magazynowane w magazynie</span><span class="sxs-lookup"><span data-stu-id="c7536-158">Encryption of the OS volume to protect the boot volume at rest in your storage</span></span>
* <span data-ttu-id="c7536-159">Szyfrowanie ilości danych, aby chronić woluminy danych przechowywanych w magazynie</span><span class="sxs-lookup"><span data-stu-id="c7536-159">Encryption of data volumes to protect the data volumes at rest in your storage</span></span>
* <span data-ttu-id="c7536-160">Wyłączenie szyfrowania dysków systemu operacyjnego i danych dla maszyn wirtualnych IaaS systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c7536-160">Disabling encryption on the OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="c7536-161">Wyłączenie szyfrowania danych dyski dla maszyn wirtualnych systemu Linux IaaS (tylko wtedy, gdy nie jest zaszyfrowany to dysk systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="c7536-161">Disabling encryption on the data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="c7536-162">Ochrona kluczy szyfrowania i kluczy tajnych w magazynie kluczy subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c7536-162">Safeguarding the encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="c7536-163">Raportowanie stanu szyfrowania zaszyfrowanej maszyn wirtualnych IaaS</span><span class="sxs-lookup"><span data-stu-id="c7536-163">Reporting the encryption status of the encrypted IaaS VM</span></span>
* <span data-ttu-id="c7536-164">Usuwanie ustawień konfiguracji szyfrowania dysku od maszyny wirtualnej IaaS</span><span class="sxs-lookup"><span data-stu-id="c7536-164">Removal of disk-encryption configuration settings from the IaaS virtual machine</span></span>
* <span data-ttu-id="c7536-165">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych za pomocą usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-165">Backup and restore of encrypted VMs by using the Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-166">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych jest obsługiwana tylko dla maszyn wirtualnych, które są szyfrowane przy użyciu konfiguracji KEK.</span><span class="sxs-lookup"><span data-stu-id="c7536-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="c7536-167">Nie jest obsługiwana na maszynach wirtualnych, które są szyfrowane bez KEK.</span><span class="sxs-lookup"><span data-stu-id="c7536-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="c7536-168">KEK jest opcjonalnym parametrem, który włącza szyfrowanie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="c7536-169">Szyfrowanie dysków Azure maszyny Wirtualne IaaS dla systemu Windows i Linux rozwiązanie obejmuje:</span><span class="sxs-lookup"><span data-stu-id="c7536-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="c7536-170">Rozszerzenie szyfrowania dysku dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c7536-170">The disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="c7536-171">Rozszerzenie szyfrowania dysku dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c7536-171">The disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="c7536-172">Szyfrowanie dysków poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7536-172">The disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="c7536-173">Dysk szyfrowania poleceń cmdlet Azure interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="c7536-173">The disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="c7536-174">Szyfrowanie dysków szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7536-174">The disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="c7536-175">Rozwiązanie szyfrowania dysków Azure jest obsługiwane na maszynach wirtualnych IaaS, które korzystają z systemu Windows lub systemu operacyjnego Linux.</span><span class="sxs-lookup"><span data-stu-id="c7536-175">The Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="c7536-176">Aby uzyskać więcej informacji o obsługiwanych systemach operacyjnych zobacz sekcję "Wymagania wstępne".</span><span class="sxs-lookup"><span data-stu-id="c7536-176">For more information about the supported operating systems, see the "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-177">Brak bez dodatkowych opłat szyfrowanie dysków maszyny Wirtualnej przy użyciu szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="c7536-178">Opis korzyści</span><span class="sxs-lookup"><span data-stu-id="c7536-178">Value proposition</span></span>
<span data-ttu-id="c7536-179">Po zastosowaniu rozwiązania zarządzania szyfrowania dysków Azure mogą spełniać następujące wymagania biznesowe:</span><span class="sxs-lookup"><span data-stu-id="c7536-179">When you apply the Azure Disk Encryption-management solution, you can satisfy the following business needs:</span></span>

* <span data-ttu-id="c7536-180">Maszyny wirtualne IaaS są zabezpieczone magazynowane, ponieważ można użyć technologii szyfrowania standardowych do organizacji wymagania dotyczące zabezpieczeń i zgodności.</span><span class="sxs-lookup"><span data-stu-id="c7536-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology to address organizational security and compliance requirements.</span></span>
* <span data-ttu-id="c7536-181">Maszyny wirtualne IaaS rozruchu w obszarze klucze kontrolowane przez klienta i zasad, a można inspekcji ich użycia w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="c7536-182">Szyfrowanie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="c7536-182">Encryption workflow</span></span>
<span data-ttu-id="c7536-183">Aby włączyć szyfrowanie dysku dla systemu Windows i maszyn wirtualnych systemu Linux, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-183">To enable disk encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="c7536-184">Wybierz scenariusz szyfrowania spośród powyższych scenariuszy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-184">Choose an encryption scenario from among the preceding encryption scenarios.</span></span>
2. <span data-ttu-id="c7536-185">Zgódź się na włączenie szyfrowania za pomocą Menedżera zasobów szyfrowania dysków Azure szablonu, poleceń cmdlet programu PowerShell lub polecenia interfejsu wiersza polecenia na dysku, a następnie określ konfiguracji szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-185">Opt in to enabling disk encryption via the Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify the encryption configuration.</span></span>

   * <span data-ttu-id="c7536-186">W scenariuszu wirtualnego dysku twardego szyfrowane klienta przekazać zaszyfrowanego dysku VHD do konta magazynu i materiału klucza szyfrowania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-186">For the customer-encrypted VHD scenario, upload the encrypted VHD to your storage account and the encryption key material to your key vault.</span></span> <span data-ttu-id="c7536-187">Następnie podaj w konfiguracji szyfrowania, aby włączyć szyfrowanie na nowej maszyny Wirtualnej IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7536-187">Then, provide the encryption configuration to enable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="c7536-188">W przypadku nowych maszyn wirtualnych, które są tworzone z witryny Marketplace, a istniejące maszyny wirtualne, które zostały już uruchomione na platformie Azure Podaj konfiguracji szyfrowania, aby włączyć szyfrowanie na Maszynie wirtualnej IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7536-188">For new VMs that are created from the Marketplace and existing VMs that are already running in Azure, provide the encryption configuration to enable encryption on the IaaS VM.</span></span>

3. <span data-ttu-id="c7536-189">Udziel dostępu do platformy Azure do odczytu z magazynu kluczy, aby włączyć szyfrowanie na Maszynie wirtualnej IaaS materiału klucza szyfrowania (klucze szyfrowania funkcji BitLocker dla systemów Windows) i hasło dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c7536-189">Grant access to the Azure platform to read the encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault to enable encryption on the IaaS VM.</span></span>

4. <span data-ttu-id="c7536-190">Podaj tożsamość aplikacji usługi Azure Active Directory (Azure AD) można zapisać klucza szyfrowania materiały do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-190">Provide the Azure Active Directory (Azure AD) application identity to write the encryption key material to your key vault.</span></span> <span data-ttu-id="c7536-191">Dzięki temu włącza szyfrowanie na maszynie Wirtualnej IaaS w scenariuszach wspomnianego w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="c7536-191">Doing so enables encryption on the IaaS VM for the scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="c7536-192">Azure aktualizuje modelu usług maszyny Wirtualnej przy użyciu szyfrowania i konfiguracji magazynu kluczy i konfiguruje zaszyfrowanych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-192">Azure updates the VM service model with encryption and the key vault configuration, and sets up your encrypted VM.</span></span>

 ![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="c7536-194">Odszyfrowywanie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="c7536-194">Decryption workflow</span></span>
<span data-ttu-id="c7536-195">Aby wyłączyć szyfrowanie dysku dla maszyn wirtualnych IaaS, wykonaj następujące czynności ogólne:</span><span class="sxs-lookup"><span data-stu-id="c7536-195">To disable disk encryption for IaaS VMs, complete the following high-level steps:</span></span>

1. <span data-ttu-id="c7536-196">Wybierz umożliwia wyłączenie szyfrowania (odszyfrowywania) na uruchomionych maszyn wirtualnych IaaS na platformie Azure za pośrednictwem szablon Menedżera zasobów szyfrowania dysków Azure lub poleceń cmdlet programu PowerShell i określić konfigurację odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="c7536-196">Choose to disable encryption (decryption) on a running IaaS VM in Azure via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify the decryption configuration.</span></span>

 <span data-ttu-id="c7536-197">Ten krok powoduje wyłączenie szyfrowania systemu operacyjnego ilość danych i/lub na Maszynie wirtualnej uruchomionej IaaS systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c7536-197">This step disables encryption of the OS or the data volume or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="c7536-198">Jednakże jak wspomniano w poprzedniej sekcji, wyłączenie szyfrowania dysku systemu operacyjnego Linux nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c7536-198">However, as mentioned in the previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="c7536-199">Krok odszyfrowywania jest dozwolone tylko w przypadku dysków z danymi na maszynach wirtualnych systemu Linux, tak długo, jak dysk systemu operacyjnego nie jest zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="c7536-199">The decryption step is allowed only for data drives on Linux VMs as long as the OS disk is not encrypted.</span></span>
2. <span data-ttu-id="c7536-200">Azure aktualizacji modelu usług maszyny Wirtualnej, a IaaS maszyny Wirtualnej jest oznaczony jako odszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="c7536-200">Azure updates the VM service model, and the IaaS VM is marked decrypted.</span></span> <span data-ttu-id="c7536-201">Zawartość maszyny Wirtualnej nie są szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="c7536-201">The contents of the VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-202">Operacja disable szyfrowania nie powoduje usunięcia magazynu kluczy i materiału klucza szyfrowania (klucze szyfrowania funkcji BitLocker dla systemów Windows) lub hasło dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c7536-202">The disable-encryption operation does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="c7536-203">Wyłączenie szyfrowania dysku systemu operacyjnego Linux nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c7536-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="c7536-204">Krok odszyfrowywania jest dozwolone tylko w przypadku dysków z danymi na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c7536-204">The decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="c7536-205">Wyłączenie szyfrowania dysku danych dla systemu Linux nie jest obsługiwane, jeśli dysk systemu operacyjnego jest zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="c7536-205">Disabling data disk encryption for Linux is not supported if the OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7536-206">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c7536-206">Prerequisites</span></span>
<span data-ttu-id="c7536-207">Przed włączeniem szyfrowania dysków Azure na maszynach wirtualnych Azure IaaS dla obsługiwane scenariusze, które zostały omówione w sekcji "Przegląd", zobacz następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="c7536-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for the supported scenarios that were discussed in the "Overview" section, see the following prerequisites:</span></span>

* <span data-ttu-id="c7536-208">Musi mieć prawidłową aktywną subskrypcją platformy Azure na tworzenie zasobów Azure w obsługiwanych regionów.</span><span class="sxs-lookup"><span data-stu-id="c7536-208">You must have a valid active Azure subscription to create resources in Azure in the supported regions.</span></span>
* <span data-ttu-id="c7536-209">Szyfrowanie dysków Azure jest obsługiwane w następujących wersjach systemu Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 i Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c7536-209">Azure Disk Encryption is supported on the following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="c7536-210">Szyfrowanie dysków Azure jest obsługiwane w następujących wersjach klientów systemu Windows: Windows 10 i Windows 8 klienta.</span><span class="sxs-lookup"><span data-stu-id="c7536-210">Azure Disk Encryption is supported on the following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-211">Dla systemu Windows Server 2008 R2 musisz mieć zainstalowany przed włączeniem szyfrowania na platformie Azure programu .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="c7536-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="c7536-212">Można zainstalować z witryny Windows Update, instalując opcjonalną aktualizację programu Microsoft .NET Framework 4.5.2 dla systemów opartych na x64 systemu Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="c7536-212">You can install it from Windows Update by installing the optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="c7536-213">Szyfrowanie dysków Azure jest obsługiwane na następujących galerii Azure na podstawie dystrybucje systemu Linux serwera i wersji:</span><span class="sxs-lookup"><span data-stu-id="c7536-213">Azure Disk Encryption is supported on the following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="c7536-214">Dystrybucja systemu Linux</span><span class="sxs-lookup"><span data-stu-id="c7536-214">Linux Distribution</span></span> | <span data-ttu-id="c7536-215">Wersja</span><span class="sxs-lookup"><span data-stu-id="c7536-215">Version</span></span> | <span data-ttu-id="c7536-216">Typ woluminu obsługiwany w przypadku szyfrowania</span><span class="sxs-lookup"><span data-stu-id="c7536-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="c7536-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c7536-217">Ubuntu</span></span> | <span data-ttu-id="c7536-218">16.04 — CODZIENNIE LTS</span><span class="sxs-lookup"><span data-stu-id="c7536-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="c7536-219">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="c7536-219">OS and Data disk</span></span> |
| <span data-ttu-id="c7536-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c7536-220">Ubuntu</span></span> | <span data-ttu-id="c7536-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="c7536-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="c7536-222">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="c7536-222">OS and Data disk</span></span> |
| <span data-ttu-id="c7536-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c7536-223">Ubuntu</span></span> | <span data-ttu-id="c7536-224">12.10</span><span class="sxs-lookup"><span data-stu-id="c7536-224">12.10</span></span> | <span data-ttu-id="c7536-225">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-225">Data disk</span></span> |
| <span data-ttu-id="c7536-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c7536-226">Ubuntu</span></span> | <span data-ttu-id="c7536-227">12.04</span><span class="sxs-lookup"><span data-stu-id="c7536-227">12.04</span></span> | <span data-ttu-id="c7536-228">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-228">Data disk</span></span> |
| <span data-ttu-id="c7536-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="c7536-229">RHEL</span></span> | <span data-ttu-id="c7536-230">7.3</span><span class="sxs-lookup"><span data-stu-id="c7536-230">7.3</span></span> | <span data-ttu-id="c7536-231">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="c7536-231">OS and Data disk</span></span> |
| <span data-ttu-id="c7536-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="c7536-232">RHEL</span></span> | <span data-ttu-id="c7536-233">7.2</span><span class="sxs-lookup"><span data-stu-id="c7536-233">7.2</span></span> | <span data-ttu-id="c7536-234">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="c7536-234">OS and Data disk</span></span> |
| <span data-ttu-id="c7536-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="c7536-235">RHEL</span></span> | <span data-ttu-id="c7536-236">6.8</span><span class="sxs-lookup"><span data-stu-id="c7536-236">6.8</span></span> | <span data-ttu-id="c7536-237">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="c7536-237">OS and Data disk</span></span> |
| <span data-ttu-id="c7536-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="c7536-238">RHEL</span></span> | <span data-ttu-id="c7536-239">6.7</span><span class="sxs-lookup"><span data-stu-id="c7536-239">6.7</span></span> | <span data-ttu-id="c7536-240">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-240">Data disk</span></span> |
| <span data-ttu-id="c7536-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7536-241">CentOS</span></span> | <span data-ttu-id="c7536-242">7.3</span><span class="sxs-lookup"><span data-stu-id="c7536-242">7.3</span></span> | <span data-ttu-id="c7536-243">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="c7536-243">OS and Data disk</span></span> |
| <span data-ttu-id="c7536-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7536-244">CentOS</span></span> | <span data-ttu-id="c7536-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="c7536-245">7.2n</span></span> | <span data-ttu-id="c7536-246">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="c7536-246">OS and Data disk</span></span> |
| <span data-ttu-id="c7536-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7536-247">CentOS</span></span> | <span data-ttu-id="c7536-248">6.8</span><span class="sxs-lookup"><span data-stu-id="c7536-248">6.8</span></span> | <span data-ttu-id="c7536-249">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="c7536-249">OS and Data disk</span></span> |
| <span data-ttu-id="c7536-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7536-250">CentOS</span></span> | <span data-ttu-id="c7536-251">7.1</span><span class="sxs-lookup"><span data-stu-id="c7536-251">7.1</span></span> | <span data-ttu-id="c7536-252">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-252">Data disk</span></span> |
| <span data-ttu-id="c7536-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7536-253">CentOS</span></span> | <span data-ttu-id="c7536-254">7.0</span><span class="sxs-lookup"><span data-stu-id="c7536-254">7.0</span></span> | <span data-ttu-id="c7536-255">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-255">Data disk</span></span> |
| <span data-ttu-id="c7536-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7536-256">CentOS</span></span> | <span data-ttu-id="c7536-257">6.7</span><span class="sxs-lookup"><span data-stu-id="c7536-257">6.7</span></span> | <span data-ttu-id="c7536-258">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-258">Data disk</span></span> |
| <span data-ttu-id="c7536-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7536-259">CentOS</span></span> | <span data-ttu-id="c7536-260">6.6</span><span class="sxs-lookup"><span data-stu-id="c7536-260">6.6</span></span> | <span data-ttu-id="c7536-261">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-261">Data disk</span></span> |
| <span data-ttu-id="c7536-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7536-262">CentOS</span></span> | <span data-ttu-id="c7536-263">6.5</span><span class="sxs-lookup"><span data-stu-id="c7536-263">6.5</span></span> | <span data-ttu-id="c7536-264">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-264">Data disk</span></span> |
| <span data-ttu-id="c7536-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="c7536-265">openSUSE</span></span> | <span data-ttu-id="c7536-266">13.2</span><span class="sxs-lookup"><span data-stu-id="c7536-266">13.2</span></span> | <span data-ttu-id="c7536-267">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-267">Data disk</span></span> |
| <span data-ttu-id="c7536-268">SLES</span><span class="sxs-lookup"><span data-stu-id="c7536-268">SLES</span></span> | <span data-ttu-id="c7536-269">12 Z DODATKIEM SP1</span><span class="sxs-lookup"><span data-stu-id="c7536-269">12 SP1</span></span> | <span data-ttu-id="c7536-270">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-270">Data disk</span></span> |
| <span data-ttu-id="c7536-271">SLES</span><span class="sxs-lookup"><span data-stu-id="c7536-271">SLES</span></span> | <span data-ttu-id="c7536-272">12 dodatku SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="c7536-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="c7536-273">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-273">Data disk</span></span> |
| <span data-ttu-id="c7536-274">SLES</span><span class="sxs-lookup"><span data-stu-id="c7536-274">SLES</span></span> | <span data-ttu-id="c7536-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="c7536-275">HPC 12</span></span> | <span data-ttu-id="c7536-276">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-276">Data disk</span></span> |
| <span data-ttu-id="c7536-277">SLES</span><span class="sxs-lookup"><span data-stu-id="c7536-277">SLES</span></span> | <span data-ttu-id="c7536-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="c7536-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="c7536-279">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-279">Data disk</span></span> |
| <span data-ttu-id="c7536-280">SLES</span><span class="sxs-lookup"><span data-stu-id="c7536-280">SLES</span></span> | <span data-ttu-id="c7536-281">11 Z DODATKIEM SP4</span><span class="sxs-lookup"><span data-stu-id="c7536-281">11 SP4</span></span> | <span data-ttu-id="c7536-282">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="c7536-282">Data disk</span></span> |

* <span data-ttu-id="c7536-283">Szyfrowanie dysków Azure wymaga, aby magazyn kluczy i maszyny wirtualne znajdowały się w tym samym regionie Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c7536-283">Azure Disk Encryption requires that your key vault and VMs reside in the same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-284">Konfigurowanie zasobów w oddzielnych regionach powoduje to niepowodzenie w włączenie funkcji szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-284">Configuring the resources in separate regions causes a failure in enabling the Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="c7536-285">Do instalowania i konfigurowania magazynu kluczy do szyfrowania dysków Azure, zobacz sekcję **ustawiony w górę i konfigurowania magazynu kluczy szyfrowania dysków Azure** w *wymagania wstępne* sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="c7536-285">To set up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="c7536-286">Do instalowania i konfigurowania aplikacji usługi Azure AD w usłudze Azure Active directory szyfrowanie dysków Azure, zobacz sekcję **Konfigurowanie aplikacji usługi Azure AD w usłudze Azure Active Directory** w *wymagania wstępne* sekcji w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="c7536-286">To set up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up the Azure AD application in Azure Active Directory** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="c7536-287">Do instalowania i konfigurowania zasad dostępu do magazynu kluczy dla aplikacji usługi Azure AD, zobacz sekcję **skonfigurować zasady dostępu do magazynu kluczy dla aplikacji usługi Azure AD** w *wymagania wstępne* sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="c7536-287">To set up and configure the key vault access policy for the Azure AD application, see section **Set up the key vault access policy for the Azure AD application** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="c7536-288">Aby przygotować wstępnie zaszyfrowanego dysku VHD systemu Windows, zobacz sekcję **przygotować wstępnie zaszyfrowanego dysku VHD systemu Windows** w *dodatku*.</span><span class="sxs-lookup"><span data-stu-id="c7536-288">To prepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="c7536-289">Aby przygotować wstępnie zaszyfrowanego dysku VHD systemu Linux, zobacz sekcję **przygotować wstępnie zaszyfrowanego dysku VHD systemu Linux** w *dodatku*.</span><span class="sxs-lookup"><span data-stu-id="c7536-289">To prepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="c7536-290">Platforma Azure wymaga dostępu do kluczy szyfrowania lub kluczy tajnych w magazynie kluczy, aby były dostępne dla maszyny wirtualnej podczas rozruchu i odszyfrowuje wolumin systemu operacyjnego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-290">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the virtual machine when it boots and decrypts the virtual machine OS volume.</span></span> <span data-ttu-id="c7536-291">Aby udzielić uprawnień do platformy Azure, należy ustawić **EnabledForDiskEncryption** właściwość w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-291">To grant permissions to Azure platform, set the **EnabledForDiskEncryption** property in the key vault.</span></span> <span data-ttu-id="c7536-292">Aby uzyskać więcej informacji, zobacz **ustawiony w górę i konfigurowania magazynu kluczy szyfrowania dysków Azure** w dodatku.</span><span class="sxs-lookup"><span data-stu-id="c7536-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in the Appendix.</span></span>
* <span data-ttu-id="c7536-293">Klucz tajny magazynu kluczy, a adresy URL KEK musi być numerów wersji.</span><span class="sxs-lookup"><span data-stu-id="c7536-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="c7536-294">Azure wymusza to ograniczenie wersji.</span><span class="sxs-lookup"><span data-stu-id="c7536-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="c7536-295">Nieprawidłowy klucz tajny i KEK adresów URL zobacz następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="c7536-295">For valid secret and KEK URLs, see the following examples:</span></span>

  * <span data-ttu-id="c7536-296">Przykład prawidłowego adresu URL tajny: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c7536-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="c7536-297">Przykład prawidłowy adres URL KEK: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c7536-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="c7536-298">Szyfrowanie dysków Azure nie obsługuje określania numery portów, jako część adresy URL KEK i kluczy tajnych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="c7536-299">Przykłady adresów URL magazynu kluczy obsługiwanych i nieobsługiwanych zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="c7536-299">For examples of non-supported and supported key vault URLs, see the following:</span></span>

  * <span data-ttu-id="c7536-300">Adres URL magazynu kluczy można zaakceptować *https://contosovault.vault.azure.net:443/klucze tajne/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c7536-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="c7536-301">Adres URL magazynu kluczy dopuszczalne: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c7536-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="c7536-302">Aby włączyć szyfrowanie dysków Azure funkcji, maszyny wirtualne IaaS musi spełniać następujące wymagania dotyczące konfiguracji punktu końcowego sieci:</span><span class="sxs-lookup"><span data-stu-id="c7536-302">To enable the Azure Disk Encryption feature, the IaaS VMs must meet the following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="c7536-303">Aby uzyskać token, aby połączyć się z magazynu kluczy, musi być można nawiązać połączenia z punktem końcowym usługi Azure Active Directory, maszyn wirtualnych IaaS \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="c7536-303">To get a token to connect to your key vault, the IaaS VM must be able to connect to an Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="c7536-304">Do zapisu kluczy szyfrowania magazynu kluczy, maszyn wirtualnych IaaS musi mieć możliwość połączenia z punktem końcowym magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-304">To write the encryption keys to your key vault, the IaaS VM must be able to connect to the key vault endpoint.</span></span>
  * <span data-ttu-id="c7536-305">Maszyn wirtualnych IaaS musi mieć możliwość nawiązania połączenia usługi Azure storage punktu końcowego, który obsługuje repozytorium rozszerzenie Azure i konto magazynu platformy Azure obsługującym pliki wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="c7536-305">The IaaS VM must be able to connect to an Azure storage endpoint that hosts the Azure extension repository and an Azure storage account that hosts the VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c7536-306">Jeśli zasady zabezpieczeń ogranicza dostęp do Internetu z maszyn wirtualnych platformy Azure, można rozwiązać poprzedni identyfikator URI i skonfigurować określona Reguła zezwalająca na łączności wychodzącego adresy IP.</span><span class="sxs-lookup"><span data-stu-id="c7536-306">If your security policy limits access from Azure VMs to the Internet, you can resolve the preceding URI and configure a specific rule to allow outbound connectivity to the IPs.</span></span>
  >
  ><span data-ttu-id="c7536-307">Konfigurowanie i dostępu do usługi Azure Key Vault za zaporą (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="c7536-307">To configure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="c7536-308">Użyj najnowszej wersji zestawu SDK programu PowerShell Azure w wersji, aby skonfigurować szyfrowanie dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-308">Use the latest version of Azure PowerShell SDK version to configure Azure Disk Encryption.</span></span> <span data-ttu-id="c7536-309">Pobierz najnowszą wersję [wersji programu Azure PowerShell](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="c7536-309">Download the latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="c7536-310">Szyfrowanie dysków Azure nie jest obsługiwana w [zestawu SDK usługi Azure PowerShell w wersji 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="c7536-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="c7536-311">Jeśli wyświetlany błąd związany z przy użyciu programu Azure PowerShell 1.1.0, zobacz [Azure dysku szyfrowania błędów związanych z programu Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7536-311">If you are receiving an error related to using Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related to Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="c7536-312">Aby uruchomić polecenia wiersza polecenia platformy Azure i skojarzyć go z subskrypcją platformy Azure, należy najpierw zainstalować wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="c7536-312">To run any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="c7536-313">Aby zainstalować wiersza polecenia platformy Azure i skojarzyć go z subskrypcją platformy Azure, zobacz [jak instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c7536-313">To install Azure CLI and associate it with your Azure subscription, see [How to install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="c7536-314">Aby użyć wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows za pomocą Menedżera zasobów Azure, zobacz [polecenia wiersza polecenia platformy Azure w trybie Menedżera zasobów](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="c7536-314">To use Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="c7536-315">Podczas szyfrowania dysków zarządzanych, jest wymagane wstępnie wymaganego do wykonania migawki dysków zarządzanych lub kopii zapasowej dysku poza szyfrowania dysków Azure przed włączeniem szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-315">When encrypting a managed disk, it is mandatory prerequisite to take a snapshot of the managed disk or a backup of the disk outside of Azure Disk Encryption prior to enabling encryption.</span></span>  <span data-ttu-id="c7536-316">Bez kopii zapasowej w miejscu wszelkie nieoczekiwany błąd podczas szyfrowania może spowodować dysku i wirtualna niedostępna bez opcji odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c7536-316">Without a backup in place, any unexpected failure during encryption may render the disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="c7536-317">Zestaw AzureRmVMDiskEncryptionExtension nie jest obecnie kopii dysków zarządzanych i zostanie błąd, jeśli użyty przed dysków zarządzanych, chyba że został określony parametr - skipVmBackup.</span><span class="sxs-lookup"><span data-stu-id="c7536-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless the -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="c7536-318">Ten parametr jest niebezpieczne używać, chyba że już wykonano kopię zapasową poza szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-318">This parameter is unsafe to use unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="c7536-319">Jeśli nie określono parametru - skipVmBackup, polecenie cmdlet nie dokona kopii zapasowej dysków zarządzanych przed szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-319">When the -skipVmBackup parameter is specified, the cmdlet will not make a backup of the managed disk prior to encryption.</span></span>  <span data-ttu-id="c7536-320">Z tego powodu uważa się wymagane wstępnie wymagana do upewnij się, że kopia zapasowa dysków zarządzanych się, że maszyna wirtualna ma miejsce przed włączeniem szyfrowania dysków Azure w przypadku odzyskiwania później jest potrzebny.</span><span class="sxs-lookup"><span data-stu-id="c7536-320">For this reason, it is considered a mandatory prerequisite to make sure a backup of the managed disk VM is in place prior to enabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="c7536-321">Parametr - skipVmBackup nigdy nie powinien być używany, chyba że migawka lub kopia zapasowa została już dokonana poza szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-321">The -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="c7536-322">Rozwiązania szyfrowania dysków Azure używa zewnętrznego ochrony klucza funkcji BitLocker dla maszyn wirtualnych IaaS systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c7536-322">The Azure Disk Encryption solution uses the BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="c7536-323">Dla domeny dołączonego do maszyn wirtualnych, nie należy wypchnąć żadnych zasad grupy, które wymuszania funkcji ochrony Moduł TPM.</span><span class="sxs-lookup"><span data-stu-id="c7536-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="c7536-324">Aby uzyskać informacje dotyczące zasad grupy "Zezwalaj na funkcję BitLocker bez zgodny moduł TPM", zobacz [dokumentacja zasad grupy funkcji BitLocker](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="c7536-324">For information about the group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="c7536-325">Zasady funkcji BitLocker na maszynach wirtualnych przyłączony do domeny z zasad grupy niestandardowe musi zawierać następujące ustawienie: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` szyfrowania dysków Azure zakończy się niepowodzeniem, jeśli ustawienia zasad niestandardowych grup do używania funkcji Bitlocker są niezgodne.</span><span class="sxs-lookup"><span data-stu-id="c7536-325">Bitlocker policy on domain joined virtual machines with custom group policy must include the following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="c7536-326">Na komputerach, które nie ma prawidłowe zasady może być wymagane ustawienia, stosowanie nowych zasad, wymuszanie nowych zasad w celu aktualizacji (gpupdate.exe/Force) i ponowne uruchomienie.</span><span class="sxs-lookup"><span data-stu-id="c7536-326">On machines that did not have the correct policy setting, applying the new policy, forcing the new policy to update (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="c7536-327">Aby utworzyć aplikację usługi Azure AD, utworzyć magazyn kluczy, lub skonfigurować istniejący magazyn kluczy i włączenia szyfrowania, zobacz [skrypt programu PowerShell wymagań wstępnych szyfrowania dysków Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="c7536-327">To create an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see the [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="c7536-328">Aby skonfigurować wymagań wstępnych szyfrowania dysków za pomocą interfejsu wiersza polecenia Azure, zobacz [ten skrypt Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c7536-328">To configure disk-encryption prerequisites using the Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="c7536-329">Aby korzystać z usługi Kopia zapasowa Azure kopii zapasowej i przywracanie zaszyfrowanych maszyn wirtualnych, po włączeniu szyfrowania z szyfrowania dysków Azure, szyfrowania maszyn wirtualnych przy użyciu konfiguracji klucza szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-329">To use the Azure Backup service to back up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using the Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="c7536-330">Usługa kopii zapasowej obsługuje maszyny wirtualne, które są szyfrowane za pomocą KEK tylko konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c7536-330">The Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="c7536-331">Zobacz [jak wykonać kopię zapasową i przywrócić szyfrowane maszyn wirtualnych przy użyciu szyfrowania usługi Kopia zapasowa Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="c7536-331">See [How to back up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="c7536-332">Podczas szyfrowania woluminu systemu operacyjnego Linux, należy pamiętać, że ponowne uruchomienie maszyny Wirtualnej jest obecnie wymagane na koniec procesu.</span><span class="sxs-lookup"><span data-stu-id="c7536-332">When encrypting a Linux OS volume, note that a VM restart is currently required at the end of the process.</span></span> <span data-ttu-id="c7536-333">Można to zrobić za pomocą portalu, programu powershell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c7536-333">This can be done via the portal, powershell, or CLI.</span></span>   <span data-ttu-id="c7536-334">Aby śledzić postęp szyfrowania, okresowo sondować komunikatu o stanie zwracanych przez https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus Get AzureRmVMDiskEncryptionStatus.</span><span class="sxs-lookup"><span data-stu-id="c7536-334">To track the progress of encryption, periodically poll the status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="c7536-335">Po zakończeniu szyfrowania komunikatu o stanie zwracanych przez to polecenie będzie tę informację.</span><span class="sxs-lookup"><span data-stu-id="c7536-335">Once encryption is complete, the the status message returned by this command will indicate this.</span></span>  <span data-ttu-id="c7536-336">Na przykład "postępu: dysk systemu operacyjnego zostały pomyślnie zaszyfrowane, wykonaj ponowny rozruch maszyny Wirtualnej" w tym punkcie maszyny Wirtualnej może być uruchomiona ponownie oraz używane.</span><span class="sxs-lookup"><span data-stu-id="c7536-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot the VM"  At this point the VM can be restarted and used.</span></span>  

* <span data-ttu-id="c7536-337">Azure szyfrowanie dysku dla systemu Linux wymaga dysków z danymi ma zainstalowany system plików w systemie Linux przed szyfrowania</span><span class="sxs-lookup"><span data-stu-id="c7536-337">Azure Disk Encryption for Linux requires data disks to have a mounted file system in Linux prior to encryption</span></span>

* <span data-ttu-id="c7536-338">Rekursywnie zainstalowanego dane, które dyski nie są obsługiwane przez szyfrowanie dysków Azure dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c7536-338">Recursively mounted data disks are not supported by the Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="c7536-339">Na przykład, jeśli system docelowy ma zainstalowany dysk paska/foo/i następnie w /foo/bar/baz, szyfrowanie /foo/bar/baz powiedzie się, ale szyfrowania paska/foo/zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="c7536-339">For example, if the target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, the encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="c7536-340">Szyfrowanie dysków Azure jest obsługiwana tylko w przypadku obrazów obsługiwane galerii Azure, które spełniają wymagania wstępne wymienione wyżej.</span><span class="sxs-lookup"><span data-stu-id="c7536-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet the aforementioned prerequisites.</span></span> <span data-ttu-id="c7536-341">Niestandardowe obrazy klienta nie są obsługiwane z powodu schemat partycji niestandardowych i zachowania procesu, które mogą występować w tych obrazów.</span><span class="sxs-lookup"><span data-stu-id="c7536-341">Customer custom images are not supported due to custom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="c7536-342">Co więcej, nawet galerii opartej na obrazie maszyny Wirtualnej, która początkowo spełnione wymagania wstępne zostały zmienione po utworzeniu mogą być niezgodne.</span><span class="sxs-lookup"><span data-stu-id="c7536-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="c7536-343">W tym powodem, sugerowane procedury szyfrowania Maszynę wirtualną systemu Linux jest uruchomić z czystą galerii, szyfrowanie maszyny Wirtualnej, a następnie dodaj niestandardowe oprogramowania lub dane do maszyny Wirtualnej, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="c7536-343">For that reason, the suggested procedure for encrypting a Linux VM is to start from a clean gallery image, encrypt the VM, and then add custom software or data to the VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="c7536-344">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych jest obsługiwana tylko dla maszyn wirtualnych, które są szyfrowane przy użyciu konfiguracji KEK.</span><span class="sxs-lookup"><span data-stu-id="c7536-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="c7536-345">Nie jest obsługiwana na maszynach wirtualnych, które są szyfrowane bez KEK.</span><span class="sxs-lookup"><span data-stu-id="c7536-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="c7536-346">KEK jest opcjonalnym parametrem, który umożliwia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-the-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="c7536-347">Konfigurowanie aplikacji usługi Azure AD w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7536-347">Set up the Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="c7536-348">Jeśli potrzebujesz szyfrowanie można włączyć na maszynie Wirtualnej uruchomionej w usłudze Azure szyfrowania dysków Azure generuje i zapisuje klucze szyfrowania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-348">When you need encryption to be enabled on a running VM in Azure, Azure Disk Encryption generates and writes the encryption keys to your key vault.</span></span> <span data-ttu-id="c7536-349">Zarządzanie kluczy szyfrowania w magazynie kluczy, wymaga uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7536-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="c7536-350">W tym celu należy utworzyć aplikację usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7536-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="c7536-351">Szczegółowy opis kroków można znaleźć rejestrowania aplikacji w sekcji "Pobierz tożsamości dla aplikacji" w blogu [usługi Azure Key Vault - krok po kroku](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7536-351">You can find detailed steps for registering an application in the “Get an Identity for the Application” section of the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="c7536-352">Ten wpis zawiera również liczbę przykłady przydatne do instalowania i konfigurowania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="c7536-353">Na potrzeby uwierzytelniania można użyć uwierzytelniania opartego na klucz tajny klienta i uwierzytelnianie klienta oparte na certyfikatach usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7536-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="c7536-354">Uwierzytelnianie oparte na protokole klucz tajny klienta dla usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7536-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="c7536-355">W kolejnych sekcjach ułatwiają konfigurowanie uwierzytelniania opartego na klucz tajny klienta dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7536-355">The sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="c7536-356">Tworzenie aplikacji usługi Azure AD przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7536-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="c7536-357">Aby utworzyć aplikację usługi Azure AD, należy użyć następującego polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c7536-357">Use the following PowerShell cmdlet to create an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="c7536-358">$azureAdApplication.ApplicationId jest Azure AD ClientID i $aadClientSecret ze klucza tajnego klienta należy używać później można włączyć szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-358">$azureAdApplication.ApplicationId is the Azure AD ClientID and $aadClientSecret is the client secret that you should use later to enable Azure Disk Encryption.</span></span> <span data-ttu-id="c7536-359">Odpowiednio Chroń klucz tajny klienta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7536-359">Safeguard the Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-the-azure-ad-client-id-and-secret-from-the-azure-classic-portal"></a><span data-ttu-id="c7536-360">Konfigurowanie usługi Azure AD identyfikator klienta i klucz tajny z klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-360">Setting up the Azure AD client ID and secret from the Azure classic portal</span></span>
<span data-ttu-id="c7536-361">Można również ustawić zapasowej identyfikator klienta usługi Azure AD i klucz tajny przy użyciu [klasycznego portalu Azure]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c7536-361">You can also set up your Azure AD client ID and secret by using the [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="c7536-362">Aby wykonać to zadanie, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-362">To perform this task, do the following:</span></span>

1. <span data-ttu-id="c7536-363">Kliknij przycisk **usługi Active Directory** kartę.</span><span class="sxs-lookup"><span data-stu-id="c7536-363">Click the **Active Directory** tab.</span></span>

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="c7536-365">Kliknij przycisk **Dodawanie aplikacji**, a następnie wpisz nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c7536-365">Click **Add Application**, and then type the application name.</span></span>

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="c7536-367">Kliknij przycisk strzałki, a następnie skonfigurować właściwości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c7536-367">Click the arrow button, and then configure the application properties.</span></span>

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="c7536-369">Kliknij znacznik wyboru, w lewym dolnym rogu, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="c7536-369">Click the check mark in the lower left corner to finish.</span></span> <span data-ttu-id="c7536-370">Zostanie wyświetlona strona konfiguracji aplikacji, a identyfikator klienta usługi Azure AD są wyświetlane u dołu strony.</span><span class="sxs-lookup"><span data-stu-id="c7536-370">The application configuration page appears, and the Azure AD client ID is displayed at the bottom of the page.</span></span>

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="c7536-372">Zapisz klucz tajny klienta usługi Azure AD, klikając **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c7536-372">Save the Azure AD client secret by clicking the **Save** button.</span></span> <span data-ttu-id="c7536-373">Należy pamiętać, klucz tajny klienta usługi Azure AD w polu tekstowym kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-373">Note the Azure AD client secret in the keys text box.</span></span> <span data-ttu-id="c7536-374">Chroń odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="c7536-374">Safeguard it appropriately.</span></span>

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="c7536-376">Poprzedni przepływ nie jest obsługiwane w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-376">The preceding flow is not supported on the Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="c7536-377">Użyj istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="c7536-377">Use an existing application</span></span>
<span data-ttu-id="c7536-378">Do wykonania poniższych poleceń, uzyskiwał i wykorzystywał [modułu Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7536-378">To execute the following commands, obtain and use the [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-379">Należy wykonać następujące polecenia z nowe okno programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7536-379">The following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="c7536-380">Nie należy używać programu Azure PowerShell lub w oknie usługi Azure Resource Manager można wykonać polecenia.</span><span class="sxs-lookup"><span data-stu-id="c7536-380">Do not use Azure PowerShell or the Azure Resource Manager window to execute the commands.</span></span> <span data-ttu-id="c7536-381">Firma Microsoft zaleca takie podejście, ponieważ te polecenia cmdlet w MSOnline module lub Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7536-381">We recommend this approach because these cmdlets are in the MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="c7536-382">Uwierzytelnianie oparte na certyfikatach dla usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7536-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="c7536-383">Uwierzytelnianie oparte na certyfikatach AD Azure aktualnie nie jest obsługiwane na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c7536-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="c7536-384">W kolejnych sekcjach pokazano, jak skonfigurować uwierzytelnianie oparte na certyfikatach dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7536-384">The sections that follow show how to configure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="c7536-385">Tworzenie aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7536-385">Create an Azure AD application</span></span>
<span data-ttu-id="c7536-386">Aby utworzyć aplikację usługi Azure AD, wykonaj następujące polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c7536-386">To create an Azure AD application, execute the following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-387">Zastąp następujące `yourpassword` ciągu bezpiecznego hasła i ochrony hasłem.</span><span class="sxs-lookup"><span data-stu-id="c7536-387">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="c7536-388">Po zakończeniu tego kroku, Przekaż plik PFX do magazynu kluczy i włącz zasady dostępu, wymagane do wdrożenia tego certyfikatu do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-388">After you finish this step, upload a PFX file to your key vault and enable the access policy needed to deploy that certificate to a VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="c7536-389">Użyj istniejącej aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7536-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="c7536-390">W przypadku konfigurowania uwierzytelniania opartego na certyfikatach dla istniejącej aplikacji, użyj polecenia cmdlet programu PowerShell pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c7536-390">If you are configuring certificate-based authentication for an existing application, use the PowerShell cmdlets shown here.</span></span> <span data-ttu-id="c7536-391">Pamiętaj wykonać je z nowe okno programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7536-391">Be sure to execute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="c7536-392">Po zakończeniu tego kroku, Przekaż plik PFX do magazynu kluczy i włącz zasady dostępu, które ma potrzebne do wdrożenia certyfikatów do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-392">After you finish this step, upload a PFX file to your key vault and enable the access policy that's needed to deploy the certificate to a VM.</span></span>

##### <a name="upload-a-pfx-file-to-your-key-vault"></a><span data-ttu-id="c7536-393">Przekaż plik PFX do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="c7536-393">Upload a PFX file to your key vault</span></span>
<span data-ttu-id="c7536-394">Aby uzyskać szczegółowy opis tego procesu, zobacz [oficjalny Azure klucza magazynu Blog zespołu](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7536-394">For a detailed explanation of this process, see [The Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="c7536-395">Następujące polecenia cmdlet programu PowerShell są jednak potrzebne dla zadania.</span><span class="sxs-lookup"><span data-stu-id="c7536-395">However, the following PowerShell cmdlets are all you need for the task.</span></span> <span data-ttu-id="c7536-396">Należy je wykonać z konsoli programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7536-396">Be sure to execute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-397">Zastąp następujące `yourpassword` ciągu bezpiecznego hasła i ochrony hasłem.</span><span class="sxs-lookup"><span data-stu-id="c7536-397">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-to-an-existing-vm"></a><span data-ttu-id="c7536-398">Wdróż certyfikat w magazynie kluczy, istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c7536-398">Deploy a certificate in your key vault to an existing VM</span></span>
<span data-ttu-id="c7536-399">Po zakończeniu przekazywania plik PFX, Wdróż certyfikat w magazynie kluczy istniejącej maszyny Wirtualnej z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-399">After you finish uploading the PFX, deploy a certificate in the key vault to an existing VM with the following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-the-key-vault-access-policy-for-the-azure-ad-application"></a><span data-ttu-id="c7536-400">Konfigurowanie zasad dostępu do magazynu kluczy dla aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7536-400">Set up the key vault access policy for the Azure AD application</span></span>
<span data-ttu-id="c7536-401">Aplikacja Azure AD wymaga praw dostępu do kluczy lub kluczy tajnych w magazynie.</span><span class="sxs-lookup"><span data-stu-id="c7536-401">Your Azure AD application needs rights to access the keys or secrets in the vault.</span></span> <span data-ttu-id="c7536-402">Użyj [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) polecenia cmdlet, aby udzielić uprawnień do aplikacji, przy użyciu Identyfikatora klienta (który został wygenerowany, gdy aplikacja została zarejestrowana) jako _— ServicePrincipalName_ wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="c7536-402">Use the [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet to grant permissions to the application, using the client ID (which was generated when the application was registered) as the _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="c7536-403">Aby dowiedzieć się więcej, zobacz wpis w blogu [usługi Azure Key Vault - krok po kroku](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7536-403">To learn more, see the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="c7536-404">Oto przykład sposobu wykonania tego zadania za pomocą programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c7536-404">Here is an example of how to perform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="c7536-405">Szyfrowanie dysków Azure, musisz skonfigurować następujące zasady dostępu do aplikacji klienta usługi Azure AD: _WrapKey_ i _ustawić_ uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="c7536-405">Azure Disk Encryption requires you to configure the following access policies to your Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="c7536-406">Terminologia</span><span class="sxs-lookup"><span data-stu-id="c7536-406">Terminology</span></span>
<span data-ttu-id="c7536-407">Aby poznać niektóre typowe terminy używane przez tę technologię, skorzystaj z poniższej tabeli terminologią:</span><span class="sxs-lookup"><span data-stu-id="c7536-407">To understand some of the common terms used by this technology, use the following terminology table:</span></span>

| <span data-ttu-id="c7536-408">Terminologia</span><span class="sxs-lookup"><span data-stu-id="c7536-408">Terminology</span></span> | <span data-ttu-id="c7536-409">Definicja</span><span class="sxs-lookup"><span data-stu-id="c7536-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="c7536-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7536-410">Azure AD</span></span> | <span data-ttu-id="c7536-411">Usługa Azure AD [usługi Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="c7536-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="c7536-412">Konto usługi Azure AD jest wymagane do uwierzytelniania, przechowywania i pobierania kluczy tajnych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="c7536-413">W usłudze Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c7536-413">Azure Key Vault</span></span> | <span data-ttu-id="c7536-414">Key Vault jest usługą zarządzania kryptograficznych, klucza opartego na zweryfikowane FIPS Federal Information Processing standardów sprzętowych modułów zabezpieczeń, które pomagają w ochronie z kluczy kryptograficznych i kluczy tajnych poufnych.</span><span class="sxs-lookup"><span data-stu-id="c7536-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="c7536-415">Aby uzyskać więcej informacji, zobacz [Key Vault](https://azure.microsoft.com/services/key-vault/) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="c7536-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="c7536-416">ARM</span><span class="sxs-lookup"><span data-stu-id="c7536-416">ARM</span></span> | <span data-ttu-id="c7536-417">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7536-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="c7536-418">Funkcja BitLocker</span><span class="sxs-lookup"><span data-stu-id="c7536-418">BitLocker</span></span> |<span data-ttu-id="c7536-419">[Funkcja BitLocker](https://technet.microsoft.com/library/hh831713.aspx) jest branży Windows woluminu szyfrowania technologia, która jest używana do włączenia szyfrowania dysków na maszynach wirtualnych IaaS systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c7536-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used to enable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="c7536-420">KSB</span><span class="sxs-lookup"><span data-stu-id="c7536-420">BEK</span></span> | <span data-ttu-id="c7536-421">Klucze szyfrowania funkcji BitLocker są używane do szyfrowania woluminu rozruchowego systemu operacyjnego i woluminów danych.</span><span class="sxs-lookup"><span data-stu-id="c7536-421">BitLocker encryption keys are used to encrypt the OS boot volume and data volumes.</span></span> <span data-ttu-id="c7536-422">Klucze funkcji BitLocker są chronione w magazynie kluczy jako kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="c7536-422">The BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="c7536-423">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c7536-423">CLI</span></span> | <span data-ttu-id="c7536-424">Zobacz [interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c7536-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="c7536-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="c7536-425">DM-Crypt</span></span> |<span data-ttu-id="c7536-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) podsystem opartych na systemie Linux lub przezroczystego szyfrowania dysku, który jest używany do Włącz szyfrowanie dysku dla maszyn wirtualnych systemu Linux IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7536-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is the Linux-based, transparent disk-encryption subsystem that's used to enable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="c7536-427">KEK</span><span class="sxs-lookup"><span data-stu-id="c7536-427">KEK</span></span> | <span data-ttu-id="c7536-428">Klucz szyfrowania jest klucza asymetrycznego (RSA 2048), który służy do ochrony lub opakuj klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="c7536-428">Key encryption key is the asymmetric key (RSA 2048) that you can use to protect or wrap the secret.</span></span> <span data-ttu-id="c7536-429">Możesz podać zabezpieczeń sprzętowych modułów (HSM)-chronione klucza lub klucza chronionego przez oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="c7536-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="c7536-430">Aby uzyskać więcej informacji, zobacz [usługi Azure Key Vault](https://azure.microsoft.com/services/key-vault/) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="c7536-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="c7536-431">PS polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7536-431">PS cmdlets</span></span> | <span data-ttu-id="c7536-432">Zobacz [poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c7536-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="c7536-433">Instalowanie i Konfigurowanie magazynu kluczy do szyfrowania dysków Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="c7536-434">Szyfrowanie dysków Azure ułatwia zabezpieczenie szyfrowanie dysków kluczy i kluczy tajnych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-434">Azure Disk Encryption helps safeguard the disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="c7536-435">Aby skonfigurować szyfrowanie dysków Azure magazynu kluczy, wykonać kroki opisane w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="c7536-435">To set up your key vault for Azure Disk Encryption, complete the steps in each of the following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="c7536-436">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="c7536-436">Create a key vault</span></span>
<span data-ttu-id="c7536-437">Aby utworzyć magazyn kluczy, użyj jednej z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="c7536-437">To create a key vault, use one of the following options:</span></span>

* [<span data-ttu-id="c7536-438">"101-klucza-magazynu-Create" Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7536-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="c7536-439">Polecenia cmdlet magazynu kluczy Azure programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7536-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="c7536-440">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7536-440">Azure Resource Manager</span></span>
* <span data-ttu-id="c7536-441">Jak [bezpiecznego magazynu kluczy](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="c7536-441">How to [Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-442">Jeśli magazyn kluczy zostały już skonfigurowane dla Twojej subskrypcji, przejdź do następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c7536-442">If you have already set up a key vault for your subscription, skip to the next section.</span></span>

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="c7536-444">Konfigurowanie klucza szyfrowania (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="c7536-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="c7536-445">Jeśli chcesz użyć KEK dla dodatkową warstwę zabezpieczeń dla kluczy szyfrowania funkcją BitLocker, należy dodać KEK do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-445">If you want to use a KEK for an additional layer of security for the BitLocker encryption keys, add a KEK to your key vault.</span></span> <span data-ttu-id="c7536-446">Użyj [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) polecenia cmdlet, aby utworzyć klucz szyfrowania kluczy w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-446">Use the [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to create a key encryption key in the key vault.</span></span> <span data-ttu-id="c7536-447">Można także zaimportować KEK z lokalnymi Zarządzanie klucza HSM.</span><span class="sxs-lookup"><span data-stu-id="c7536-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="c7536-448">Aby uzyskać więcej informacji, zobacz [klucza magazynu dokumentacji](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="c7536-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="c7536-449">Można dodać klucza KEK, przechodząc do usługi Azure Resource Manager lub przy użyciu interfejsu magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-449">You can add the KEK by going to Azure Resource Manager or by using your key vault interface.</span></span>

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="c7536-451">Ustaw uprawnienia magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="c7536-451">Set key vault permissions</span></span>
<span data-ttu-id="c7536-452">Platforma Azure wymaga dostępu do kluczy szyfrowania lub kluczy tajnych w magazynie kluczy, aby udostępnić je do maszyny Wirtualnej do rozruchu i odszyfrowywania woluminów.</span><span class="sxs-lookup"><span data-stu-id="c7536-452">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span></span> <span data-ttu-id="c7536-453">Aby udzielić uprawnień do platformy Azure, należy ustawić **EnabledForDiskEncryption** właściwości klucza magazynu za pomocą polecenia cmdlet programu PowerShell magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="c7536-453">To grant permissions to the Azure platform, set the **EnabledForDiskEncryption** property in the key vault by using the key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="c7536-454">Można również ustawić **EnabledForDiskEncryption** właściwości odwiedzając [Eksploratora zasobów Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c7536-454">You can also set the **EnabledForDiskEncryption** property by visiting the [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="c7536-455">Jak wspomniano wcześniej, musisz ustawić **EnabledForDiskEncryption** właściwości magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-455">As mentioned earlier, you must set the **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="c7536-456">W przeciwnym razie wdrażanie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="c7536-456">Otherwise, the deployment will fail.</span></span>

<span data-ttu-id="c7536-457">Jak pokazano poniżej, można skonfigurować zasady dostępu dla aplikacji usługi Azure AD z interfejsu magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="c7536-457">You can set up access policies for your Azure AD application from the key vault interface, as shown here:</span></span>

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="c7536-460">Na **zasady dostępu zaawansowane** i upewnij się, że magazynu kluczy jest włączona obsługa szyfrowania dysków Azure:</span><span class="sxs-lookup"><span data-stu-id="c7536-460">On the **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Usługi Azure key vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="c7536-462">Scenariusze wdrażania szyfrowanie dysków oraz możliwości użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c7536-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="c7536-463">Aby umożliwić wiele scenariuszy szyfrowania dysków i kroki mogą się różnić w zależności od scenariusza.</span><span class="sxs-lookup"><span data-stu-id="c7536-463">You can enable many disk-encryption scenarios, and the steps may vary according to the scenario.</span></span> <span data-ttu-id="c7536-464">W poniższych częściach omówiono scenariusze większej liczby szczegółów.</span><span class="sxs-lookup"><span data-stu-id="c7536-464">The following sections cover the scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-the-marketplace"></a><span data-ttu-id="c7536-465">Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS utworzony z witryny Marketplace</span><span class="sxs-lookup"><span data-stu-id="c7536-465">Enable encryption on new IaaS VMs that are created from the Marketplace</span></span>
<span data-ttu-id="c7536-466">Można włączyć szyfrowanie dysków na nowej maszyny Wirtualnej systemu Windows IaaS z witryny Marketplace na platformie Azure przy użyciu [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="c7536-466">You can enable disk encryption on new IaaS Windows VM from the Marketplace in Azure by using the  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="c7536-467">W szablonie szybki start Azure, kliknij polecenie **wdrażanie na platformie Azure**, wprowadź konfiguracji szyfrowania **parametry** bloku, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7536-467">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c7536-468">Wybierz subskrypcję, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** Aby włączyć szyfrowanie na nowej maszyny Wirtualnej IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7536-468">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-469">Ten szablon umożliwia tworzenie nowych zaszyfrowanych Windows maszynę Wirtualną, która używa obrazu galerii systemu Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="c7536-469">This template creates a new encrypted Windows VM that uses the Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="c7536-470">Można włączyć szyfrowanie dysków na nowe IaaS RedHat Linux 7.2 maszynę Wirtualną za pomocą macierzy RAID-0 200 GB, za pomocą tego [szablonu usługi Resource Manager](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="c7536-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="c7536-471">Po wdrożeniu szablonu, sprawdź stan szyfrowania maszyny Wirtualnej za pomocą `Get-AzureRmVmDiskEncryptionStatus` polecenia cmdlet, zgodnie z opisem w [OS szyfrowania dysków na uruchomionej maszyny Wirtualnej systemu Linux](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="c7536-471">After you deploy the template, verify the VM encryption status by using the `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="c7536-472">Gdy komputer zwraca stan _VMRestartPending_, uruchom ponownie maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="c7536-472">When the machine returns a status of _VMRestartPending_, restart the VM.</span></span>

<span data-ttu-id="c7536-473">W poniższej tabeli wymieniono parametrów szablonu usługi Resource Manager dla nowych maszyn wirtualnych z scenariusza Marketplace przy użyciu Identyfikatora klienta usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c7536-473">The following table lists the Resource Manager template parameters for new VMs from the Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="c7536-474">Parametr</span><span class="sxs-lookup"><span data-stu-id="c7536-474">Parameter</span></span> | <span data-ttu-id="c7536-475">Opis</span><span class="sxs-lookup"><span data-stu-id="c7536-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7536-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="c7536-476">adminUserName</span></span> | <span data-ttu-id="c7536-477">Nazwa użytkownika administratora dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-477">Admin user name for the virtual machine.</span></span> |
| <span data-ttu-id="c7536-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="c7536-478">adminPassword</span></span> | <span data-ttu-id="c7536-479">Hasło użytkownika administratora dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-479">Admin user password for the virtual machine.</span></span> |
| <span data-ttu-id="c7536-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="c7536-480">newStorageAccountName</span></span> | <span data-ttu-id="c7536-481">Nazwa konta magazynu do przechowywania systemu operacyjnego i danych wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="c7536-481">Name of the storage account to store OS and data VHDs.</span></span> |
| <span data-ttu-id="c7536-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="c7536-482">vmSize</span></span> | <span data-ttu-id="c7536-483">Rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-483">Size of the VM.</span></span> <span data-ttu-id="c7536-484">Obecnie obsługiwane są tylko standardowe A, D i G serii.</span><span class="sxs-lookup"><span data-stu-id="c7536-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="c7536-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="c7536-485">virtualNetworkName</span></span> | <span data-ttu-id="c7536-486">Nazwa sieci wirtualnej, której maszyna wirtualna karta sieciowa powinna należeć.</span><span class="sxs-lookup"><span data-stu-id="c7536-486">Name of the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="c7536-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="c7536-487">subnetName</span></span> | <span data-ttu-id="c7536-488">Nazwa podsieci w sieci wirtualnej, której maszyna wirtualna karta sieciowa powinna należeć.</span><span class="sxs-lookup"><span data-stu-id="c7536-488">Name of the subnet in the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="c7536-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="c7536-489">AADClientID</span></span> | <span data-ttu-id="c7536-490">Identyfikator klienta aplikacji usługi Azure AD, które ma uprawnienia do zapisu kluczy tajnych magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-490">Client ID of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="c7536-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="c7536-491">AADClientSecret</span></span> | <span data-ttu-id="c7536-492">Klucz tajny klienta aplikacji usługi Azure AD, które ma uprawnienia do zapisu kluczy tajnych magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-492">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="c7536-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="c7536-493">keyVaultURL</span></span> | <span data-ttu-id="c7536-494">Adres URL magazynu kluczy, który powinien być przekazywane klucza funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7536-494">URL of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="c7536-495">Możesz pobrać go za pomocą polecenia cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="c7536-495">You can get it by using the cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="c7536-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="c7536-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="c7536-497">Adres URL klucza szyfrowania klucza, który jest używany do szyfrowania klucza funkcji BitLocker wygenerowanego (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="c7536-497">URL of the key encryption key that's used to encrypt the generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="c7536-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c7536-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="c7536-499">Grupa zasobów magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-499">Resource group of the key vault.</span></span> |
| <span data-ttu-id="c7536-500">vmName</span><span class="sxs-lookup"><span data-stu-id="c7536-500">vmName</span></span> | <span data-ttu-id="c7536-501">Nazwa maszyny Wirtualnej, można wykonać w operacji szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-501">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="c7536-502">_KeyEncryptionKeyURL_ jest parametrem opcjonalnym.</span><span class="sxs-lookup"><span data-stu-id="c7536-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="c7536-503">Będzie można przełączyć własne KEK do dalszego zabezpieczenie klucza szyfrowania danych (klucz tajny hasło) w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-503">You can bring your own KEK to further safeguard the data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="c7536-504">Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS, które są tworzone na podstawie klienta systemu szyfrowania plików VHD i kluczy szyfrowania</span><span class="sxs-lookup"><span data-stu-id="c7536-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="c7536-505">W tym scenariuszu można włączyć szyfrowanie przy użyciu szablonu usługi Resource Manager, poleceń cmdlet programu PowerShell lub polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c7536-505">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="c7536-506">W poniższych sekcjach opisano szczegółowo szablonu usługi Resource Manager i polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c7536-506">The following sections explain in greater detail the Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="c7536-507">Postępuj zgodnie z instrukcjami z jednego z tych sekcji przygotowania zaszyfrowane wstępnie obrazy, których można użyć w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-507">Follow the instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="c7536-508">Po utworzeniu obrazu służy kroki opisane w następnej sekcji można utworzyć zaszyfrowanego maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-508">After the image is created, you can use the steps in the next section to create an encrypted Azure VM.</span></span>

* [<span data-ttu-id="c7536-509">Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c7536-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="c7536-510">Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Linux</span><span class="sxs-lookup"><span data-stu-id="c7536-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="c7536-511">Przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7536-511">Using the Resource Manager template</span></span>
<span data-ttu-id="c7536-512">Można włączyć szyfrowanie dysków na zaszyfrowany dysk VHD za pomocą [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="c7536-512">You can enable disk encryption on your encrypted VHD by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="c7536-513">W szablonie szybki start Azure, kliknij polecenie **wdrażanie na platformie Azure**, wprowadź konfiguracji szyfrowania **parametry** bloku, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7536-513">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c7536-514">Wybierz subskrypcję, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** Aby włączyć szyfrowanie na nowej maszyny Wirtualnej IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7536-514">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the new IaaS VM.</span></span>

<span data-ttu-id="c7536-515">W poniższej tabeli wymieniono parametrów szablonu usługi Resource Manager z zaszyfrowanego dysku VHD:</span><span class="sxs-lookup"><span data-stu-id="c7536-515">The following table lists the Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="c7536-516">Parametr</span><span class="sxs-lookup"><span data-stu-id="c7536-516">Parameter</span></span> | <span data-ttu-id="c7536-517">Opis</span><span class="sxs-lookup"><span data-stu-id="c7536-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7536-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="c7536-518">newStorageAccountName</span></span> | <span data-ttu-id="c7536-519">Nazwa konta magazynu do przechowywania zaszyfrowanego dysku VHD systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7536-519">Name of the storage account to store the encrypted OS VHD.</span></span> <span data-ttu-id="c7536-520">To konto magazynu należy już został utworzony w tej samej grupie zasobów i tej samej lokalizacji co maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-520">This storage account should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="c7536-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="c7536-521">osVhdUri</span></span> | <span data-ttu-id="c7536-522">Identyfikator URI dysku VHD systemu operacyjnego z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c7536-522">URI of the OS VHD from the storage account.</span></span> |
| <span data-ttu-id="c7536-523">osType</span><span class="sxs-lookup"><span data-stu-id="c7536-523">osType</span></span> | <span data-ttu-id="c7536-524">Typ produktu systemu operacyjnego (Windows/Linux).</span><span class="sxs-lookup"><span data-stu-id="c7536-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="c7536-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="c7536-525">virtualNetworkName</span></span> | <span data-ttu-id="c7536-526">Nazwa sieci wirtualnej, której maszyna wirtualna karta sieciowa powinna należeć.</span><span class="sxs-lookup"><span data-stu-id="c7536-526">Name of the VNet that the VM NIC should belong to.</span></span> <span data-ttu-id="c7536-527">Nazwa powinna już został utworzony w tej samej grupie zasobów i tej samej lokalizacji co maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-527">The name should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="c7536-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="c7536-528">subnetName</span></span> | <span data-ttu-id="c7536-529">Nazwa podsieci w sieci wirtualnej, której maszyna wirtualna karta sieciowa powinna należeć.</span><span class="sxs-lookup"><span data-stu-id="c7536-529">Name of the subnet on the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="c7536-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="c7536-530">vmSize</span></span> | <span data-ttu-id="c7536-531">Rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-531">Size of the VM.</span></span> <span data-ttu-id="c7536-532">Obecnie obsługiwane są tylko standardowe A, D i G serii.</span><span class="sxs-lookup"><span data-stu-id="c7536-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="c7536-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="c7536-533">keyVaultResourceID</span></span> | <span data-ttu-id="c7536-534">Identyfikator zasobu, który identyfikuje zasobu magazynu kluczy Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7536-534">The ResourceID that identifies the key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="c7536-535">Możesz pobrać go za pomocą polecenia cmdlet programu PowerShell `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="c7536-535">You can get it by using the PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="c7536-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="c7536-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="c7536-537">Adres URL klucza szyfrowania dysków, który został skonfigurowany w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-537">URL of the disk-encryption key that's set up in the key vault.</span></span> |
| <span data-ttu-id="c7536-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="c7536-538">keyVaultKekUrl</span></span> | <span data-ttu-id="c7536-539">Adres URL klucz szyfrowania kluczy do szyfrowania klucza wygenerowanego szyfrowanie dysków.</span><span class="sxs-lookup"><span data-stu-id="c7536-539">URL of the key encryption key for encrypting the generated disk-encryption key.</span></span> |
| <span data-ttu-id="c7536-540">vmName</span><span class="sxs-lookup"><span data-stu-id="c7536-540">vmName</span></span> | <span data-ttu-id="c7536-541">Nazwa maszyny Wirtualnej IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7536-541">Name of the IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="c7536-542">Za pomocą poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7536-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="c7536-543">Można włączyć szyfrowanie dysków na zaszyfrowany dysk VHD za pomocą polecenia cmdlet programu PowerShell [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="c7536-543">You can enable disk encryption on your encrypted VHD by using the PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="c7536-544">Za pomocą polecenia interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c7536-544">Using CLI commands</span></span>
<span data-ttu-id="c7536-545">Aby włączyć szyfrowanie dysku dla tego scenariusza za pomocą polecenia interfejsu wiersza polecenia, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-545">To enable disk encryption for this scenario by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="c7536-546">Ustawianie zasad dostępu w magazynie kluczy:</span><span class="sxs-lookup"><span data-stu-id="c7536-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="c7536-547">Ustaw **EnabledForDiskEncryption** flagi:</span><span class="sxs-lookup"><span data-stu-id="c7536-547">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="c7536-548">Ustaw uprawnienia do aplikacji usługi Azure AD do zapisu kluczy tajnych magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="c7536-548">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="c7536-549">Aby włączyć szyfrowanie na istniejących lub uruchomionej maszyny Wirtualnej, wpisz:</span><span class="sxs-lookup"><span data-stu-id="c7536-549">To enable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="c7536-550">Pobierz stan szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="c7536-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="c7536-551">Aby włączyć szyfrowanie na nowej maszyny Wirtualnej z zaszyfrowany dysk VHD, należy użyć poniższych parametrów z `azure vm create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="c7536-551">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="c7536-552">Włącz szyfrowanie dla istniejących lub uruchomione maszyny Wirtualnej systemu Windows IaaS na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="c7536-553">W tym scenariuszu można włączyć szyfrowanie przy użyciu szablonu usługi Resource Manager, poleceń cmdlet programu PowerShell lub polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c7536-553">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="c7536-554">W poniższych sekcjach opisano szczegółowo, jak je włączyć za pomocą szablonu usługi Resource Manager i polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c7536-554">The following sections explain in greater detail how to enable it by using the Resource Manager template and CLI commands.</span></span>

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="c7536-555">Przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7536-555">Using the Resource Manager template</span></span>
<span data-ttu-id="c7536-556">Można włączyć szyfrowanie dysku na istniejących lub uruchomione maszyny wirtualne IaaS systemu Windows na platformie Azure przy użyciu [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="c7536-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="c7536-557">W szablonie szybki start Azure, kliknij polecenie **wdrażanie na platformie Azure**, wprowadź konfiguracji szyfrowania **parametry** bloku, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7536-557">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c7536-558">Wybierz subskrypcję, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** Aby włączyć szyfrowanie na Maszynie wirtualnej IaaS istniejących lub nie działają.</span><span class="sxs-lookup"><span data-stu-id="c7536-558">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="c7536-559">Poniższa tabela zawiera listę parametrów szablonu usługi Resource Manager dla istniejących lub działających maszyn wirtualnych, które mają identyfikator klienta usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c7536-559">The following table lists the Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="c7536-560">Parametr</span><span class="sxs-lookup"><span data-stu-id="c7536-560">Parameter</span></span> | <span data-ttu-id="c7536-561">Opis</span><span class="sxs-lookup"><span data-stu-id="c7536-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7536-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="c7536-562">AADClientID</span></span> | <span data-ttu-id="c7536-563">Identyfikator klienta aplikacji usługi Azure AD, które ma uprawnienia do zapisu kluczy tajnych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-563">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="c7536-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="c7536-564">AADClientSecret</span></span> | <span data-ttu-id="c7536-565">Klucz tajny klienta aplikacji usługi Azure AD, które ma uprawnienia do zapisu kluczy tajnych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-565">Client secret of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="c7536-566">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c7536-566">keyVaultName</span></span> | <span data-ttu-id="c7536-567">Nazwa magazynu kluczy, który powinien być przekazywane klucza funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7536-567">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="c7536-568">Możesz pobrać go za pomocą polecenia cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="c7536-568">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="c7536-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="c7536-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="c7536-570">Adres URL klucza szyfrowania klucza, który jest używany do szyfrowania wygenerowanego klucza funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7536-570">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="c7536-571">Ten parametr jest opcjonalny w przypadku wybrania **nokek** na liście rozwijanej UseExistingKek.</span><span class="sxs-lookup"><span data-stu-id="c7536-571">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="c7536-572">W przypadku wybrania **kek** na liście rozwijanej UseExistingKek należy wprowadzić _keyEncryptionKeyURL_ wartości.</span><span class="sxs-lookup"><span data-stu-id="c7536-572">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="c7536-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="c7536-573">volumeType</span></span> | <span data-ttu-id="c7536-574">Typ operacji szyfrowania jest wykonywana na wolumin.</span><span class="sxs-lookup"><span data-stu-id="c7536-574">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="c7536-575">Prawidłowe wartości to _OS_, _danych_, i _wszystkich_.</span><span class="sxs-lookup"><span data-stu-id="c7536-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="c7536-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="c7536-576">sequenceVersion</span></span> | <span data-ttu-id="c7536-577">Wersja sekwencji operacji funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7536-577">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="c7536-578">Zwiększ numer wersji, za każdym razem, gdy operacja szyfrowania dysków jest wykonywana na tej samej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-578">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="c7536-579">vmName</span><span class="sxs-lookup"><span data-stu-id="c7536-579">vmName</span></span> | <span data-ttu-id="c7536-580">Nazwa maszyny Wirtualnej, można wykonać w operacji szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-580">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="c7536-581">_KeyEncryptionKeyURL_ jest parametrem opcjonalnym.</span><span class="sxs-lookup"><span data-stu-id="c7536-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="c7536-582">Własne KEK może doprowadzić do dalszych zabezpieczenie klucza szyfrowania danych (funkcji BitLocker Szyfrowanie klucz tajny) w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-582">You can bring your own KEK to further safeguard the data encryption key (BitLocker encryption secret) in the key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="c7536-583">Za pomocą poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7536-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="c7536-584">Aby uzyskać informacje na temat włączania szyfrowania z szyfrowania dysków Azure za pomocą poleceń cmdlet programu PowerShell, zobacz wpisy blogu [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) i [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7536-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="c7536-585">Za pomocą polecenia interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c7536-585">Using CLI commands</span></span>
<span data-ttu-id="c7536-586">Aby włączyć szyfrowanie na istniejących lub uruchomione maszyny Wirtualnej systemu Windows IaaS na platformie Azure przy użyciu polecenia interfejsu wiersza polecenia, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-586">To enable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do the following:</span></span>

1. <span data-ttu-id="c7536-587">Aby ustawić zasady dostępu w magazynie kluczy:</span><span class="sxs-lookup"><span data-stu-id="c7536-587">To set access policies in the key vault:</span></span>
   * <span data-ttu-id="c7536-588">Ustaw **EnabledForDiskEncryption** flagi:</span><span class="sxs-lookup"><span data-stu-id="c7536-588">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="c7536-589">Ustaw uprawnienia do aplikacji usługi Azure AD do zapisu kluczy tajnych magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="c7536-589">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="c7536-590">Aby włączyć szyfrowanie na istniejących lub uruchomionej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="c7536-590">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="c7536-591">Można pobrać stanu szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="c7536-591">To get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="c7536-592">Aby włączyć szyfrowanie na nowej maszyny Wirtualnej z zaszyfrowany dysk VHD, należy użyć poniższych parametrów z `azure vm create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="c7536-592">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="c7536-593">Włącz szyfrowanie dla istniejących lub nie działają IaaS maszyny Wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="c7536-594">Można włączyć szyfrowanie dysków na istniejące lub nie działają IaaS maszyny Wirtualnej systemu Linux na platformie Azure przy użyciu [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="c7536-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="c7536-595">Kliknij przycisk **wdrażanie na platformie Azure** na szablonie szybki start Azure, wprowadź konfiguracji szyfrowania na **parametry** bloku, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7536-595">Click **Deploy to Azure** on the Azure quick-start template, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c7536-596">Wybierz subskrypcję, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** Aby włączyć szyfrowanie na Maszynie wirtualnej IaaS istniejących lub nie działają.</span><span class="sxs-lookup"><span data-stu-id="c7536-596">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="c7536-597">Poniższa tabela zawiera listę parametrów szablonu usługi Resource Manager dla istniejących lub działających maszyn wirtualnych, które mają identyfikator klienta usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c7536-597">The following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="c7536-598">Parametr</span><span class="sxs-lookup"><span data-stu-id="c7536-598">Parameter</span></span> | <span data-ttu-id="c7536-599">Opis</span><span class="sxs-lookup"><span data-stu-id="c7536-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7536-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="c7536-600">AADClientID</span></span> | <span data-ttu-id="c7536-601">Identyfikator klienta aplikacji usługi Azure AD, które ma uprawnienia do zapisu kluczy tajnych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-601">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="c7536-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="c7536-602">AADClientSecret</span></span> | <span data-ttu-id="c7536-603">Klucz tajny klienta aplikacji usługi Azure AD, które ma uprawnienia do zapisu kluczy tajnych magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-603">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="c7536-604">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c7536-604">keyVaultName</span></span> | <span data-ttu-id="c7536-605">Nazwa magazynu kluczy, który powinien być przekazywane klucza funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7536-605">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="c7536-606">Możesz pobrać go za pomocą polecenia cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="c7536-606">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="c7536-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="c7536-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="c7536-608">Adres URL klucza szyfrowania klucza, który jest używany do szyfrowania wygenerowanego klucza funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7536-608">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="c7536-609">Ten parametr jest opcjonalny w przypadku wybrania **nokek** na liście rozwijanej UseExistingKek.</span><span class="sxs-lookup"><span data-stu-id="c7536-609">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="c7536-610">W przypadku wybrania **kek** na liście rozwijanej UseExistingKek należy wprowadzić _keyEncryptionKeyURL_ wartości.</span><span class="sxs-lookup"><span data-stu-id="c7536-610">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="c7536-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="c7536-611">volumeType</span></span> | <span data-ttu-id="c7536-612">Typ operacji szyfrowania jest wykonywana na wolumin.</span><span class="sxs-lookup"><span data-stu-id="c7536-612">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="c7536-613">Nieprawidłowy obsługiwane wartości to _OS_ lub _wszystkie_ (dla RHEL 7.2, CentOS 7.2 i Ubuntu 16.04), i _danych_ (dla wszystkich innych dystrybucji).</span><span class="sxs-lookup"><span data-stu-id="c7536-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="c7536-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="c7536-614">sequenceVersion</span></span> | <span data-ttu-id="c7536-615">Wersja sekwencji operacji funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7536-615">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="c7536-616">Zwiększ numer wersji, za każdym razem, gdy operacja szyfrowania dysków jest wykonywana na tej samej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-616">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="c7536-617">vmName</span><span class="sxs-lookup"><span data-stu-id="c7536-617">vmName</span></span> | <span data-ttu-id="c7536-618">Nazwa maszyny Wirtualnej, można wykonać w operacji szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-618">Name of the VM that the encryption operation is to be performed on.</span></span> |
| <span data-ttu-id="c7536-619">Hasło</span><span class="sxs-lookup"><span data-stu-id="c7536-619">passPhrase</span></span> | <span data-ttu-id="c7536-620">Wpisz silne hasło klucza szyfrowania danych.</span><span class="sxs-lookup"><span data-stu-id="c7536-620">Type a strong passphrase as the data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="c7536-621">_KeyEncryptionKeyURL_ jest parametrem opcjonalnym.</span><span class="sxs-lookup"><span data-stu-id="c7536-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="c7536-622">Będzie można przełączyć własne KEK do dalszego zabezpieczenie klucza szyfrowania danych (klucz tajny hasło) w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-622">You can bring your own KEK to further safeguard the data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="c7536-623">Polecenia interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c7536-623">CLI commands</span></span>
<span data-ttu-id="c7536-624">Można włączyć szyfrowanie dysków na zaszyfrowany dysk VHD przez zainstalowanie i używanie [polecenia interfejsu wiersza polecenia](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c7536-624">You can enable disk encryption on your encrypted VHD by installing and using the [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="c7536-625">Aby włączyć szyfrowanie na istniejących lub działających maszyn wirtualnych systemu Linux IaaS na platformie Azure przy użyciu polecenia interfejsu wiersza polecenia, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-625">To enable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="c7536-626">Ustawianie zasad dostępu w magazynie kluczy:</span><span class="sxs-lookup"><span data-stu-id="c7536-626">Set access policies in the key vault:</span></span>

 * <span data-ttu-id="c7536-627">Ustaw **EnabledForDiskEncryption** flagi:</span><span class="sxs-lookup"><span data-stu-id="c7536-627">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="c7536-628">Ustaw uprawnienia do aplikacji usługi Azure AD do zapisu kluczy tajnych magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="c7536-628">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="c7536-629">Aby włączyć szyfrowanie na istniejących lub uruchomionej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="c7536-629">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="c7536-630">Pobierz stan szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="c7536-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="c7536-631">Aby włączyć szyfrowanie na nowej maszyny Wirtualnej z zaszyfrowany dysk VHD, należy użyć poniższych parametrów z `azure vm create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="c7536-631">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-the-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="c7536-632">Pobieranie stanu szyfrowania zaszyfrowanej maszyn wirtualnych IaaS</span><span class="sxs-lookup"><span data-stu-id="c7536-632">Get the encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="c7536-633">Przy użyciu usługi Azure Resource Manager można uzyskać stanu szyfrowania [poleceń cmdlet programu PowerShell](/powershell/azure/overview), lub polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c7536-633">You can get the encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="c7536-634">W poniższych sekcjach opisano sposób korzystania z klasycznego portalu Azure i poleceń interfejsu wiersza polecenia można pobrać stanu szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-634">The following sections explain how to use the Azure classic portal and CLI commands to get the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="c7536-635">Pobieranie stanu szyfrowania zaszyfrowanej maszyny Wirtualnej systemu Windows za pomocą usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7536-635">Get the encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="c7536-636">Z usługi Azure Resource Manager można uzyskać stanu szyfrowania maszyn wirtualnych IaaS w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c7536-636">You can get the encryption status of the IaaS VM from Azure Resource Manager by doing the following:</span></span>

1. <span data-ttu-id="c7536-637">Zaloguj się do [klasycznego portalu Azure](https://portal.azure.com/), a następnie kliknij przycisk **maszyn wirtualnych** w okienku po lewej stronie, aby wyświetlić widok podsumowania maszyn wirtualnych w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c7536-637">Sign in to the [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in the left pane to see a summary view of the virtual machines in your subscription.</span></span> <span data-ttu-id="c7536-638">Można filtrować widok maszyn wirtualnych, wybierając Nazwa subskrypcji w **subskrypcji** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="c7536-638">You can filter the virtual machines view by selecting the subscription name in the **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="c7536-639">W górnej części **maszyn wirtualnych** kliknij przycisk **kolumn**.</span><span class="sxs-lookup"><span data-stu-id="c7536-639">At the top of the **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="c7536-640">Na **kolumny wybierz** bloku, wybierz opcję **szyfrowanie dysków**, a następnie kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="c7536-640">On the **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="c7536-641">Powinny pojawić się kolumna szyfrowanie dysków przedstawiający stan szyfrowania _włączone_ lub _nie włączono_ dla każdej maszyny Wirtualnej, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="c7536-641">You should see the disk-encryption column showing the encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in the following figure:</span></span>

 ![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-the-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-the-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="c7536-643">Pobieranie stanu szyfrowania zaszyfrowanej maszyn wirtualnych IaaS (system Windows/Linux) za pomocą polecenia cmdlet programu PowerShell szyfrowania dysków</span><span class="sxs-lookup"><span data-stu-id="c7536-643">Get the encryption status of an encrypted (Windows/Linux) IaaS VM by using the disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="c7536-644">Polecenia cmdlet programu PowerShell szyfrowanie dysków można uzyskać stanu szyfrowania maszyn wirtualnych IaaS `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="c7536-644">You can get the encryption status of the IaaS VM from the disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="c7536-645">Aby uzyskać ustawienia szyfrowania dla maszyny Wirtualnej, wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="c7536-645">To get the encryption settings for your VM, enter the following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="c7536-646">Możesz sprawdzić dane wyjściowe _Get-AzureRmVMDiskEncryptionStatus_ do szyfrowania klucza adresów URL.</span><span class="sxs-lookup"><span data-stu-id="c7536-646">You can inspect the output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="c7536-647">Wartości ustawienia OSVolumeEncrypted i DataVolumesEncrypted są ustawiane na _zaszyfrowane_, który wskazuje, że oba woluminy są szyfrowane za pomocą szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-647">The OSVolumeEncrypted and DataVolumesEncrypted settings values are set to _Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="c7536-648">Aby uzyskać informacje na temat włączania szyfrowania z szyfrowania dysków Azure za pomocą poleceń cmdlet programu PowerShell, zobacz wpisy blogu [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) i [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7536-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-649">Na maszynach wirtualnych systemu Linux, zajmuje trzech do czterech minut `Get-AzureRmVMDiskEncryptionStatus` polecenia cmdlet do raportowania stanu szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-649">On Linux VMs, it takes three to four minutes for the `Get-AzureRmVMDiskEncryptionStatus` cmdlet to report the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-the-iaas-vm-from-the-disk-encryption-cli-command"></a><span data-ttu-id="c7536-650">Pobieranie stanu szyfrowania maszyn wirtualnych IaaS szyfrowanie dysków polecenia interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c7536-650">Get the encryption status of the IaaS VM from the disk-encryption CLI command</span></span>
<span data-ttu-id="c7536-651">Przy użyciu polecenia interfejsu wiersza polecenia szyfrowanie dysków można uzyskać stanu szyfrowania maszyn wirtualnych IaaS `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="c7536-651">You can get the encryption status of the IaaS VM by using the disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="c7536-652">Aby uzyskać ustawienia szyfrowania dla maszyny Wirtualnej, wprowadź sesję wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="c7536-652">To get the encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="c7536-653">Wyłącz szyfrowanie uruchamiania maszyny Wirtualnej systemu Windows IaaS</span><span class="sxs-lookup"><span data-stu-id="c7536-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="c7536-654">Można wyłączyć szyfrowania na uruchomionej maszyny Wirtualnej systemu Linux IaaS lub systemu Windows za pomocą szablonu Menedżera zasobów szyfrowania dysków Azure lub poleceń cmdlet programu PowerShell i określić konfigurację odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="c7536-654">You can disable encryption on a running Windows or Linux IaaS VM via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify the decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="c7536-655">Maszyna wirtualna z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="c7536-655">Windows VM</span></span>
<span data-ttu-id="c7536-656">Wyłącz szyfrowanie krok wyłącza funkcję szyfrowania systemu operacyjnego i/lub ilość danych na Maszynie wirtualnej uruchomionej IaaS systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c7536-656">The disable-encryption step disables encryption of the OS, the data volume, or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="c7536-657">Nie można wyłączyć woluminu systemu operacyjnego i pozostawić ilość danych zaszyfrowanych.</span><span class="sxs-lookup"><span data-stu-id="c7536-657">You cannot disable the OS volume and leave the data volume encrypted.</span></span> <span data-ttu-id="c7536-658">Po wykonaniu kroku Wyłącz szyfrowanie Azure klasycznym modelu wdrażania aktualizacji modelu usług maszyny Wirtualnej i maszyn wirtualnych IaaS systemu Windows jest oznaczony jako odszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="c7536-658">When the disable-encryption step is performed, the Azure classic deployment model updates the VM service model, and the Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="c7536-659">Zawartość maszyny Wirtualnej nie są szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="c7536-659">The contents of the VM are no longer encrypted at rest.</span></span> <span data-ttu-id="c7536-660">Odszyfrowywanie nie powoduje usunięcia magazynu kluczy i materiału klucza szyfrowania (klucze szyfrowania funkcji BitLocker dla systemów Windows i hasło dla systemu Linux).</span><span class="sxs-lookup"><span data-stu-id="c7536-660">The decryption does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="c7536-661">Maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="c7536-661">Linux VM</span></span>
<span data-ttu-id="c7536-662">Wyłącz szyfrowanie krok wyłącza szyfrowanie danych woluminu na Maszynie wirtualnej uruchomionej IaaS systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c7536-662">The disable-encryption step disables encryption of the data volume on the running Linux IaaS VM.</span></span> <span data-ttu-id="c7536-663">Ten krok działa tylko, jeśli nie jest zaszyfrowany dysk systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7536-663">This step only works if the OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-664">Wyłączenie szyfrowania na dysku systemu operacyjnego nie jest dozwolona na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c7536-664">Disabling encryption on the OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="c7536-665">Wyłącz szyfrowanie na maszynie Wirtualnej IaaS istniejących lub nie działają</span><span class="sxs-lookup"><span data-stu-id="c7536-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="c7536-666">Można wyłączyć szyfrowania dysków na uruchomionych maszyn wirtualnych IaaS systemu Windows za pomocą [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="c7536-666">You can disable disk encryption on running Windows IaaS VMs by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="c7536-667">W szablonie szybki start Azure, kliknij polecenie **wdrażanie na platformie Azure**, wprowadź konfiguracji odszyfrowywania **parametry** bloku, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7536-667">On the Azure quick-start template, click **Deploy to Azure**, enter the decryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c7536-668">Wybierz subskrypcję, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** Aby włączyć szyfrowanie na nowej maszyny Wirtualnej IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7536-668">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="c7536-669">Dla maszyn wirtualnych systemu Linux, można wyłączyć szyfrowania za pomocą [wyłączyć szyfrowania na uruchomionej maszyny Wirtualnej systemu Linux](https://aka.ms/decrypt-linuxvm) szablonu.</span><span class="sxs-lookup"><span data-stu-id="c7536-669">For Linux VMs, you can disable encryption by using the [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="c7536-670">Poniższa tabela zawiera listę parametrów szablonu usługi Resource Manager wyłączenie szyfrowania na uruchomionej maszynie Wirtualnej IaaS:</span><span class="sxs-lookup"><span data-stu-id="c7536-670">The following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="c7536-671">Parametr</span><span class="sxs-lookup"><span data-stu-id="c7536-671">Parameter</span></span> | <span data-ttu-id="c7536-672">Opis</span><span class="sxs-lookup"><span data-stu-id="c7536-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7536-673">vmName</span><span class="sxs-lookup"><span data-stu-id="c7536-673">vmName</span></span> | <span data-ttu-id="c7536-674">Nazwa maszyny Wirtualnej, można wykonać w operacji szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-674">Name of the VM that the encryption operation is to be performed on.</span></span>
| <span data-ttu-id="c7536-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="c7536-675">volumeType</span></span> | <span data-ttu-id="c7536-676">Typ operacji odszyfrowywania odbywa się na wolumin.</span><span class="sxs-lookup"><span data-stu-id="c7536-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="c7536-677">Prawidłowe wartości to _OS_, _danych_, i _wszystkich_.</span><span class="sxs-lookup"><span data-stu-id="c7536-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="c7536-678">Nie można wyłączyć szyfrowania na uruchomienie woluminu systemu operacyjnego maszyny Wirtualnej systemu Windows IaaS/rozruchowego bez wyłączenie szyfrowania na _danych_ woluminu.</span><span class="sxs-lookup"><span data-stu-id="c7536-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on the _Data_ volume.</span></span> <span data-ttu-id="c7536-679">Należy również zauważyć, że wyłączenie szyfrowania na dysku systemu operacyjnego nie jest dozwolona na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c7536-679">Also note that disabling encryption on the OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="c7536-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="c7536-680">sequenceVersion</span></span> | <span data-ttu-id="c7536-681">Wersja sekwencji operacji funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7536-681">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="c7536-682">Zwiększ numer wersji, za każdym razem, gdy operacja odszyfrowywania dysku jest wykonywana na tej samej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-682">Increment this version number every time a disk decryption operation is performed on the same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="c7536-683">Wyłącz szyfrowanie na maszynie Wirtualnej IaaS istniejących lub nie działają</span><span class="sxs-lookup"><span data-stu-id="c7536-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="c7536-684">Aby wyłączyć szyfrowania na maszynie Wirtualnej IaaS istniejących lub jest uruchomiony przy użyciu polecenia cmdlet programu PowerShell, zobacz [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="c7536-684">To disable encryption on an existing or running IaaS VM by using the PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="c7536-685">To polecenie cmdlet obsługuje zarówno systemu Windows, jak i maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c7536-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="c7536-686">Aby wyłączyć szyfrowanie, instaluje rozszerzenia na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-686">To disable encryption, it installs an extension on the virtual machine.</span></span> <span data-ttu-id="c7536-687">Jeśli _nazwa_ parametr nie zostanie określony, rozszerzenie o nazwie domyślnej _AzureDiskEncryption za dla maszyn wirtualnych systemu Windows_ jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="c7536-687">If the _Name_ parameter is not specified, an extension with the default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="c7536-688">Na maszynach wirtualnych systemu Linux rozszerzenie AzureDiskEncryptionForLinux jest używane.</span><span class="sxs-lookup"><span data-stu-id="c7536-688">On Linux VMs, the AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="c7536-689">To polecenie cmdlet ponowny rozruch maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-689">This cmdlet reboots the virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="c7536-690">Włącz szyfrowanie dla zaszyfrowane wstępnie IaaS maszynę Wirtualną za pomocą dysku zarządzanego Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="c7536-691">Szablon Azure ARM zarządzane dysku służy do tworzenia zaszyfrowanego maszyny Wirtualnej z dysku VHD zaszyfrowane wstępnie przy użyciu szablonu ARM znajduje się w</span><span class="sxs-lookup"><span data-stu-id="c7536-691">Use the Azure Managed Disk ARM template to create a encrypted VM from a pre-encrypted VHD using the ARM template located at</span></span>   
<span data-ttu-id="c7536-692">[Utwórz nowe zaszyfrowanych dysków zarządzanych z zaszyfrowane wstępnie obiektu blob dysku VHD/magazynu] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="c7536-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="c7536-693">Włącz szyfrowanie dla nowej Linux IaaS maszyny Wirtualnej z dyskiem zarządzane Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="c7536-694">Szablon Azure ARM zarządzane dysku służy do tworzenia nowych zaszyfrowanych IaaS Maszynę wirtualną systemu Linux przy użyciu szablonu ARM znajduje się w</span><span class="sxs-lookup"><span data-stu-id="c7536-694">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
<span data-ttu-id="c7536-695">[Wdrażanie RHEL 7.2 z pełne szyfrowanie dysków] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="c7536-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="c7536-696">Włącz szyfrowanie dla nowej maszyny Wirtualnej IaaS systemu Windows z dysku zarządzanego Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="c7536-697">Szablon Azure ARM zarządzane dysku służy do tworzenia nowych zaszyfrowanych IaaS Maszynę wirtualną systemu Linux przy użyciu szablonu ARM znajduje się w</span><span class="sxs-lookup"><span data-stu-id="c7536-697">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
 <span data-ttu-id="c7536-698">[Tworzenie nowych zaszyfrowanych systemu Windows IaaS zarządzane dysku maszyny Wirtualnej z obrazu galerii] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="c7536-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="c7536-699">Jest to konieczne do migawki i/lub na dysku zarządzanego kopia zapasowa, wystąpienie maszyny Wirtualnej poza i przed włączeniem szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-699">It is mandatory to snapshot and/or backup a managed disk based VM instance outside of and prior to enabling Azure Disk Encryption.</span></span>  <span data-ttu-id="c7536-700">Migawki dysków zarządzanych może zostać pobrany z portalu, lub kopia zapasowa Azure można używać.</span><span class="sxs-lookup"><span data-stu-id="c7536-700">A snapshot of the managed disk can be taken from the portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="c7536-701">Kopie zapasowe upewnij się, że opcja odzyskiwania jest możliwe w przypadku dowolnego nieoczekiwany błąd podczas szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-701">Backups ensure that a recovery option is possible in the case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="c7536-702">Po utworzeniu kopii zapasowej polecenia cmdlet Set-AzureRmVMDiskEncryptionExtension może być używany do szyfrowania dysków zarządzanych, określając parametr - skipVmBackup.</span><span class="sxs-lookup"><span data-stu-id="c7536-702">Once a backup is made, the Set-AzureRmVMDiskEncryptionExtension cmdlet can be used to encrypt managed disks by specifying the -skipVmBackup parameter.</span></span>  <span data-ttu-id="c7536-703">To polecenie zakończy się niepowodzeniem przed dysków zarządzanych, na podstawie maszyny Wirtualnej, dopóki nie wykonano kopii zapasowej i podano tego parametru.</span><span class="sxs-lookup"><span data-stu-id="c7536-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="c7536-704">Aktualizowanie ustawień szyfrowania z istniejącej maszyny Wirtualnej z systemem innym niż premium zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="c7536-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="c7536-705">Użyj istniejących interfejsów szyfrowania obsługiwane dysku platformy Azure do uruchamiania maszyny Wirtualnej [PS poleceń cmdlet, interfejsu wiersza polecenia lub ARM szablonów] można zaktualizować ustawień szyfrowania AAD klient identyfikator/klucz tajny, klucz szyfrowania klucza [KEK], klucz szyfrowania funkcją BitLocker dla maszyny Wirtualnej systemu Windows lub hasło dla maszyny Wirtualnej systemu Linux itp. Ustawienie szyfrowania aktualizacji jest obsługiwana tylko dla maszyn wirtualnych przez inne niż premium magazynu.</span><span class="sxs-lookup"><span data-stu-id="c7536-705">Use the existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] to update the encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. The update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="c7536-706">Jest obsługiwana dla maszyn wirtualnych przez Magazyn w warstwie premium NNOT.</span><span class="sxs-lookup"><span data-stu-id="c7536-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="c7536-707">Dodatek</span><span class="sxs-lookup"><span data-stu-id="c7536-707">Appendix</span></span>
### <a name="connect-to-your-subscription"></a><span data-ttu-id="c7536-708">Nawiązywanie połączenia z subskrypcją</span><span class="sxs-lookup"><span data-stu-id="c7536-708">Connect to your subscription</span></span>
<span data-ttu-id="c7536-709">Przed kontynuowaniem należy przejrzeć *wymagania wstępne* w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="c7536-709">Before you proceed, review the *Prerequisites* section in this article.</span></span> <span data-ttu-id="c7536-710">Po upewnieniu się, że zostały spełnione wszystkie wymagania wstępne, podłącz do subskrypcji, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c7536-710">After you ensure that all prerequisites have been met, connect to your subscription by doing the following:</span></span>

1. <span data-ttu-id="c7536-711">Uruchom sesję programu PowerShell Azure i zaloguj się do konta platformy Azure przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="c7536-711">Start an Azure PowerShell session, and sign in to your Azure account with the following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="c7536-712">Jeśli masz wiele subskrypcji i chcesz określić, należy użyć, wpisz następujące polecenie, aby zobaczyć subskrypcje dla swojego konta:</span><span class="sxs-lookup"><span data-stu-id="c7536-712">If you have multiple subscriptions and want to specify one to use, type the following to see the subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="c7536-713">Aby określić subskrypcję, której chcesz użyć, wpisz:</span><span class="sxs-lookup"><span data-stu-id="c7536-713">To specify the subscription you want to use, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="c7536-714">Aby sprawdzić, czy skonfigurowane subskrypcja jest prawidłowa, wpisz:</span><span class="sxs-lookup"><span data-stu-id="c7536-714">To verify that the subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="c7536-715">Aby upewnić się, że są zainstalowane polecenia cmdlet szyfrowania dysków Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="c7536-715">To confirm the Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="c7536-716">Następujące dane wyjściowe stanowią potwierdzenie instalacji programu PowerShell szyfrowania dysków Azure:</span><span class="sxs-lookup"><span data-stu-id="c7536-716">The following output confirms the Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="c7536-717">Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c7536-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="c7536-718">W kolejnych sekcjach są niezbędne do przygotowania wstępnie zaszyfrowanego dysku VHD systemu Windows do wdrożenia jako zaszyfrowanego dysku VHD w programie Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7536-718">The sections that follow are necessary to prepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="c7536-719">Skorzystaj z informacji do przygotowania i rozruch świeże systemu Windows maszyny Wirtualnej (VHD) dla usługi Azure Site Recovery lub Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-719">Use the information to prepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-to-allow-non-tpm-for-os-protection"></a><span data-ttu-id="c7536-720">Aktualizacja zasad grupy, aby umożliwić bez modułu TPM do ochrony systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="c7536-720">Update group policy to allow non-TPM for OS protection</span></span>
<span data-ttu-id="c7536-721">Skonfiguruj ustawienia zasad grupy funkcji BitLocker **szyfrowania dysków funkcją BitLocker**, które znajdują się w obszarze **lokalnych zasad komputera** > **Konfiguracja komputera**  >  **Szablony administracyjne** > **składniki systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="c7536-721">Configure the BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="c7536-722">To ustawienie, aby zmienić **dyski z systemem operacyjnym** > **wymaga dodatkowego uwierzytelniania przy uruchamianiu** > **Zezwalaj na funkcję BitLocker bez zgodny moduł TPM**, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="c7536-722">Change this setting to **Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in the following figure:</span></span>

![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="c7536-724">Zainstaluj składniki funkcji BitLocker</span><span class="sxs-lookup"><span data-stu-id="c7536-724">Install BitLocker feature components</span></span>
<span data-ttu-id="c7536-725">W systemie Windows Server 2012 i nowszych Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="c7536-725">For Windows Server 2012 and later, use the following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="c7536-726">Dla systemu Windows Server 2008 R2 należy użyć następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="c7536-726">For Windows Server 2008 R2, use the following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-the-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="c7536-727">Przygotowanie woluminu systemu operacyjnego dla funkcji BitLocker przy użyciu`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="c7536-727">Prepare the OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="c7536-728">Aby skompresować partycji systemu operacyjnego i przygotowuje komputer do używania funkcji BitLocker, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c7536-728">To compress the OS partition and prepare the machine for BitLocker, execute the following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-the-os-volume-by-using-bitlocker"></a><span data-ttu-id="c7536-729">Ochrona woluminu systemu operacyjnego za pomocą funkcji BitLocker</span><span class="sxs-lookup"><span data-stu-id="c7536-729">Protect the OS volume by using BitLocker</span></span>
<span data-ttu-id="c7536-730">Użyj [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) polecenie, aby włączyć szyfrowanie na wolumin rozruchowy przy użyciu zewnętrznego funkcji ochrony klucza.</span><span class="sxs-lookup"><span data-stu-id="c7536-730">Use the [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command to enable encryption on the boot volume using an external key protector.</span></span> <span data-ttu-id="c7536-731">Również umieścić klucz zewnętrzny (plik .bek), na zewnętrznym dysku lub woluminie.</span><span class="sxs-lookup"><span data-stu-id="c7536-731">Also place the external key (.bek file) on the external drive or volume.</span></span> <span data-ttu-id="c7536-732">Szyfrowanie jest włączone na wolumin systemowy/rozruchowy po kolejnym rozruchu.</span><span class="sxs-lookup"><span data-stu-id="c7536-732">Encryption is enabled on the system/boot volume after the next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="c7536-733">Przygotowanie maszyny Wirtualnej z oddzielnych danych/zasobów wirtualnego dysku twardego do pobierania klucza zewnętrznego za pomocą funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7536-733">Prepare the VM with a separate data/resource VHD for getting the external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="c7536-734">Szyfrowanie dysku systemu operacyjnego na uruchomionej maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="c7536-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="c7536-735">Szyfrowanie dysku systemu operacyjnego na uruchomionej maszyny Wirtualnej systemu Linux jest obsługiwane w następujących dystrybucji:</span><span class="sxs-lookup"><span data-stu-id="c7536-735">Encryption of an OS drive on a running Linux VM is supported on the following distributions:</span></span>

* <span data-ttu-id="c7536-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="c7536-736">RHEL 7.2</span></span>
* <span data-ttu-id="c7536-737">7.2 centOS</span><span class="sxs-lookup"><span data-stu-id="c7536-737">CentOS 7.2</span></span>
* <span data-ttu-id="c7536-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c7536-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="c7536-739">Wymagania wstępne dotyczące szyfrowania dysku systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="c7536-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="c7536-740">Maszyna wirtualna musi zostać utworzony z obrazu witryny Marketplace usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7536-740">The VM must be created from the Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="c7536-741">Maszyna wirtualna platformy Azure z co najmniej 4 GB pamięci RAM (zalecany rozmiar to 7 GB).</span><span class="sxs-lookup"><span data-stu-id="c7536-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="c7536-742">(W przypadku RHEL i CentOS) Wyłącz SELinux.</span><span class="sxs-lookup"><span data-stu-id="c7536-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="c7536-743">Aby wyłączyć SELinux, zobacz "4.4.2.</span><span class="sxs-lookup"><span data-stu-id="c7536-743">To disable SELinux, see "4.4.2.</span></span> <span data-ttu-id="c7536-744">Wyłączanie SELinux"w [Przewodnik administratora i użytkownika SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-744">Disabling SELinux" in the [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on the VM.</span></span>
* <span data-ttu-id="c7536-745">Po wyłączeniu SELinux co najmniej raz ponowny rozruch maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-745">After you disable SELinux, reboot the VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="c7536-746">Kroki</span><span class="sxs-lookup"><span data-stu-id="c7536-746">Steps</span></span>
1. <span data-ttu-id="c7536-747">Utwórz maszynę Wirtualną za pomocą jednego z dystrybucji określony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c7536-747">Create a VM by using one of the distributions specified previously.</span></span>

 <span data-ttu-id="c7536-748">7.2 CentOS szyfrowania dysku systemu operacyjnego jest obsługiwane za pomocą specjalnego obrazu.</span><span class="sxs-lookup"><span data-stu-id="c7536-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="c7536-749">Aby użyć tego obrazu, należy określić "7.2n" jako jednostka SKU, podczas tworzenia maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="c7536-749">To use this image, specify "7.2n" as the SKU when you create the VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="c7536-750">Konfigurowanie maszyny Wirtualnej zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="c7536-750">Configure the VM according to your needs.</span></span> <span data-ttu-id="c7536-751">Jeśli zamierzasz do szyfrowania wszystkich (systemu operacyjnego i danych), dyski muszą być /etc/fstab określonego i instalację z dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="c7536-751">If you are going to encrypt all the (OS + data) drives, the data drives need to be specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="c7536-752">Użyj identyfikatora UUID =... Aby określić dyski danych w fstab/etc/zamiast określania nazwy urządzenia bloku (na przykład sdb1/dev /).</span><span class="sxs-lookup"><span data-stu-id="c7536-752">Use UUID=... to specify data drives in /etc/fstab instead of specifying the block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="c7536-753">Podczas szyfrowania kolejność dysków zmienia się na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-753">During encryption, the order of drives changes on the VM.</span></span> <span data-ttu-id="c7536-754">Jeśli maszyna wirtualna opiera się na określonej kolejności bloku urządzeń, nie będzie można zainstalować je po szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-754">If your VM relies on a specific order of block devices, it will fail to mount them after encryption.</span></span>

3. <span data-ttu-id="c7536-755">Wyloguj sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="c7536-755">Sign out of the SSH sessions.</span></span>

4. <span data-ttu-id="c7536-756">Aby zaszyfrować systemu operacyjnego, należy określić volumeType jako **wszystkie** lub **systemu operacyjnego** podczas możesz [włączyć szyfrowanie](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="c7536-756">To encrypt the OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="c7536-757">Wszystkie procesy przestrzeń użytkownika, które nie są uruchomione jako `systemd` usługi powinny skasowane z `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="c7536-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="c7536-758">Ponowny rozruch maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-758">Reboot the VM.</span></span> <span data-ttu-id="c7536-759">Po włączeniu szyfrowania dysku systemu operacyjnego na uruchomionej maszynie Wirtualnej, należy zaplanować przestój maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="c7536-760">Okresowo monitorować postęp szyfrowania zgodnie z instrukcjami podanymi w [następnej sekcji](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="c7536-760">Periodically monitor the progress of encryption by using the instructions in the [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="c7536-761">Po Get AzureRmVmDiskEncryptionStatus zawiera "VMRestartPending", należy ponownie uruchomić maszyny Wirtualnej, logując się do niego lub za pomocą portalu, programu PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c7536-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in to it or by using the portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot the VM
    ```
<span data-ttu-id="c7536-762">Przed ponownym, zaleca się zapisanie [diagnostyki rozruchu](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of the VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="c7536-763">Monitorowanie postępu szyfrowania systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="c7536-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="c7536-764">Możesz monitorować postęp szyfrowania systemu operacyjnego na trzy sposoby:</span><span class="sxs-lookup"><span data-stu-id="c7536-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="c7536-765">Użyj `Get-AzureRmVmDiskEncryptionStatus` polecenia cmdlet i przejrzyj pole postępu:</span><span class="sxs-lookup"><span data-stu-id="c7536-765">Use the `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect the ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="c7536-766">Po maszyny Wirtualnej osiągnie "Rozpoczęto szyfrowania dysku systemu operacyjnego", trwa około 40 do 50 minut na magazyn Premium kopii maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-766">After the VM reaches "OS disk encryption started," it takes about 40 to 50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="c7536-767">Z powodu [wystawiać #388](https://github.com/Azure/WALinuxAgent/issues/388) w WALinuxAgent, `OsVolumeEncrypted` i `DataVolumesEncrypted` wyświetlane jako `Unknown` w niektórych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="c7536-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="c7536-768">Z WALinuxAgent wersji 2.1.5 i później, ten problem zostanie rozwiązany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="c7536-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="c7536-769">Jeśli widzisz `Unknown` w danych wyjściowych, można sprawdzić stan szyfrowanie dysków za pomocą Eksploratora zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-769">If you see `Unknown` in the output, you can verify disk-encryption status by using the Azure Resource Explorer.</span></span>

 <span data-ttu-id="c7536-770">Przejdź do [Eksploratora zasobów Azure](https://resources.azure.com/), a następnie rozwiń węzeł tej hierarchii w panelu wyboru po lewej stronie:</span><span class="sxs-lookup"><span data-stu-id="c7536-770">Go to [Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in the selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="c7536-771">W InstanceView przewiń w dół aby zobaczyć stan szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="c7536-771">In the InstanceView, scroll down to see the encryption status of your drives.</span></span>

 ![Widok wystąpienia maszyny Wirtualnej](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="c7536-773">Przyjrzyj się [diagnostyki rozruchu](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="c7536-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="c7536-774">Komunikaty z rozszerzeniem ADE powinien być poprzedzony `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="c7536-774">Messages from the ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="c7536-775">Zaloguj się do maszyny Wirtualnej za pośrednictwem SSH i Pobierz dziennik rozszerzenia z:</span><span class="sxs-lookup"><span data-stu-id="c7536-775">Sign in to the VM via SSH, and get the extension log from:</span></span>

    <span data-ttu-id="c7536-776">/var/log/Azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="c7536-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="c7536-777">Zaleca się, że nie logowania się do maszyny Wirtualnej w trakcie szyfrowania systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7536-777">We recommend that you do not sign in to the VM while OS encryption is in progress.</span></span> <span data-ttu-id="c7536-778">Skopiuj dzienniki tylko wtedy, gdy te dwie metody nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="c7536-778">Copy the logs only when the other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="c7536-779">Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Linux</span><span class="sxs-lookup"><span data-stu-id="c7536-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="c7536-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="c7536-780">Ubuntu 16</span></span>
<span data-ttu-id="c7536-781">Skonfigurować szyfrowanie podczas instalacji dystrybucji, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-781">Configure encryption during the distribution installation by doing the following:</span></span>

1. <span data-ttu-id="c7536-782">Wybierz **skonfigurować zaszyfrowanych woluminach** po partycji dysków.</span><span class="sxs-lookup"><span data-stu-id="c7536-782">Select **Configure encrypted volumes** when you partition the disks.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="c7536-784">Utwórz dysk rozruchowy oddzielne, nie muszą być szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="c7536-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="c7536-785">Szyfrowanie dysku głównym.</span><span class="sxs-lookup"><span data-stu-id="c7536-785">Encrypt your root drive.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="c7536-787">Należy podać hasło.</span><span class="sxs-lookup"><span data-stu-id="c7536-787">Provide a passphrase.</span></span> <span data-ttu-id="c7536-788">Jest to hasło, które można przekazać do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-788">This is the passphrase that you upload to the key vault.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="c7536-790">Zakończ partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-790">Finish partitioning.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="c7536-792">Po rozruchu maszyny Wirtualnej i są wyświetlane pytanie o hasło, należy używać hasło podane w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="c7536-792">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="c7536-794">Przygotowywanie maszyny Wirtualnej do przekazywania do platformy Azure przy użyciu [tych instrukcji](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="c7536-794">Prepare the VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="c7536-795">Nie należy uruchamiać w ostatnim kroku (anulowania obsługi maszyny Wirtualnej) jeszcze.</span><span class="sxs-lookup"><span data-stu-id="c7536-795">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="c7536-796">Konfigurowanie szyfrowania do pracy z platformy Azure, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-796">Configure encryption to work with Azure by doing the following:</span></span>

1. <span data-ttu-id="c7536-797">Utwórz plik w obszarze /usr/local/sbin/azure_crypt_key.sh, z zawartością w poniższym skrypcie.</span><span class="sxs-lookup"><span data-stu-id="c7536-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with the content in the following script.</span></span> <span data-ttu-id="c7536-798">Należy zwrócić uwagę KeyFileName, ponieważ jest to nazwa pliku hasło używane przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-798">Pay attention to the KeyFileName, because it is the passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED to find suitable passphrase file ..." >&2
        echo -n "Try to enter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="c7536-799">Zmienianie konfiguracji kryptograficznego w */etc/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="c7536-799">Change the crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="c7536-800">Powinny wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="c7536-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="c7536-801">Jeśli edytujesz *azure_crypt_key.sh* w systemie Windows i zostanie skopiowana do systemu Linux, uruchom `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="c7536-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it to Linux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="c7536-802">Dodaj uprawnienia pliku wykonywalnego do skryptu:</span><span class="sxs-lookup"><span data-stu-id="c7536-802">Add executable permissions to the script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="c7536-803">Edytuj */etc/initramfs-tools/modules* przez dołączenie wiersze:</span><span class="sxs-lookup"><span data-stu-id="c7536-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="c7536-804">Uruchom `update-initramfs -u -k all` initramfs, aby zaktualizować `keyscript` zostały zastosowane.</span><span class="sxs-lookup"><span data-stu-id="c7536-804">Run `update-initramfs -u -k all` to update the initramfs to make the `keyscript` take effect.</span></span>

7. <span data-ttu-id="c7536-805">Teraz można anulowanie zastrzeżenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7536-805">Now you can deprovision the VM.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="c7536-807">Przejdź do następnego kroku i [przekazać dysk VHD](#upload-encrypted-vhd-to-an-azure-storage-account) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-807">Continue to the next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="c7536-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="c7536-808">openSUSE 13.2</span></span>
<span data-ttu-id="c7536-809">Aby skonfigurować szyfrowanie podczas instalacji dystrybucji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-809">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="c7536-810">Gdy partycji dysków, wybierz **szyfrowania woluminu grupy**, a następnie wprowadź hasło.</span><span class="sxs-lookup"><span data-stu-id="c7536-810">When you partition the disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="c7536-811">Jest to hasło, który trzeba będzie przekazać do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-811">This is the password that you will upload to your key vault.</span></span>

 ![openSUSE 13.2 Instalatora](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="c7536-813">Uruchom maszynę Wirtualną przy użyciu hasła.</span><span class="sxs-lookup"><span data-stu-id="c7536-813">Boot the VM using your password.</span></span>

 ![openSUSE 13.2 Instalatora](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="c7536-815">Przygotowywanie maszyny Wirtualnej do przekazywania do platformy Azure zgodnie z instrukcjami w [przygotowanie SLES lub openSUSE maszyny wirtualnej na platformie Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="c7536-815">Prepare the VM for uploading to Azure by following the instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="c7536-816">Nie należy uruchamiać w ostatnim kroku (anulowania obsługi maszyny Wirtualnej) jeszcze.</span><span class="sxs-lookup"><span data-stu-id="c7536-816">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="c7536-817">Aby skonfigurować szyfrowanie do pracy z platformą Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-817">To configure encryption to work with Azure, do the following:</span></span>
1. <span data-ttu-id="c7536-818">Edytuj /etc/dracut.conf i Dodaj następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="c7536-818">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="c7536-819">Komentarz te wiersze do końca /usr/lib/dracut/modules.d/90crypt/module-setup.sh pliku:</span><span class="sxs-lookup"><span data-stu-id="c7536-819">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="c7536-820">Dołącz następujący wiersz na początku /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh pliku:</span><span class="sxs-lookup"><span data-stu-id="c7536-820">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="c7536-821">I zmień wszystkich wystąpień:</span><span class="sxs-lookup"><span data-stu-id="c7536-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="c7536-822">na:</span><span class="sxs-lookup"><span data-stu-id="c7536-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="c7536-823">Edytuj /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh i dołącza je do "# Otwórz LUKS urządzenie":</span><span class="sxs-lookup"><span data-stu-id="c7536-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it to “# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="c7536-824">Uruchom `/usr/sbin/dracut -f -v` initrd aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7536-824">Run `/usr/sbin/dracut -f -v` to update the initrd.</span></span>

6. <span data-ttu-id="c7536-825">Teraz można anulowanie zastrzeżenia maszyny Wirtualnej i [przekazać dysk VHD](#upload-encrypted-vhd-to-an-azure-storage-account) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-825">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="c7536-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c7536-826">CentOS 7</span></span>
<span data-ttu-id="c7536-827">Aby skonfigurować szyfrowanie podczas instalacji dystrybucji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-827">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="c7536-828">Wybierz **szyfrowania danych** po partycji dysków.</span><span class="sxs-lookup"><span data-stu-id="c7536-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="c7536-830">Upewnij się, że **Szyfruj** jest zaznaczone dla partycji katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="c7536-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="c7536-832">Należy podać hasło.</span><span class="sxs-lookup"><span data-stu-id="c7536-832">Provide a passphrase.</span></span> <span data-ttu-id="c7536-833">Jest to hasło, które możesz przekazać do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-833">This is the passphrase that you will upload to your key vault.</span></span>

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="c7536-835">Po rozruchu maszyny Wirtualnej i są wyświetlane pytanie o hasło, należy używać hasło podane w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="c7536-835">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="c7536-837">Przygotowywanie maszyny Wirtualnej do przekazywania na platformie Azure przy użyciu instrukcji "CentOS 7.0 +" w [przygotowanie maszyny wirtualnej CentOS, oparty na platformie Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="c7536-837">Prepare the VM for uploading into Azure by using the "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="c7536-838">Nie należy uruchamiać w ostatnim kroku (anulowania obsługi maszyny Wirtualnej) jeszcze.</span><span class="sxs-lookup"><span data-stu-id="c7536-838">Do not run the last step (deprovisioning the VM) yet.</span></span>

6. <span data-ttu-id="c7536-839">Teraz można anulowanie zastrzeżenia maszyny Wirtualnej i [przekazać dysk VHD](#upload-encrypted-vhd-to-an-azure-storage-account) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c7536-839">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="c7536-840">Aby skonfigurować szyfrowanie do pracy z platformą Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7536-840">To configure encryption to work with Azure, do the following:</span></span>

1. <span data-ttu-id="c7536-841">Edytuj /etc/dracut.conf i Dodaj następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="c7536-841">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="c7536-842">Komentarz te wiersze do końca /usr/lib/dracut/modules.d/90crypt/module-setup.sh pliku:</span><span class="sxs-lookup"><span data-stu-id="c7536-842">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="c7536-843">Dołącz następujący wiersz na początku /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh pliku:</span><span class="sxs-lookup"><span data-stu-id="c7536-843">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="c7536-844">I zmień wszystkich wystąpień:</span><span class="sxs-lookup"><span data-stu-id="c7536-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="c7536-845">na</span><span class="sxs-lookup"><span data-stu-id="c7536-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="c7536-846">Edytuj /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh i Dołącz po "# Otwórz LUKS urządzenie":</span><span class="sxs-lookup"><span data-stu-id="c7536-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after the “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="c7536-847">Uruchom "/ usr/sbin/dracut - f - v" initrd aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7536-847">Run the “/usr/sbin/dracut -f -v” to update the initrd.</span></span>

![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-to-an-azure-storage-account"></a><span data-ttu-id="c7536-849">Przekazanie zaszyfrowanego dysku VHD do konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c7536-849">Upload encrypted VHD to an Azure storage account</span></span>
<span data-ttu-id="c7536-850">Po włączeniu szyfrowania funkcją BitLocker lub szyfrowania DM-Crypt lokalnego zaszyfrowanego dysku VHD musi można przekazać do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c7536-850">After BitLocker encryption or DM-Crypt encryption is enabled, the local encrypted VHD needs to be uploaded to your storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-the-disk-encryption-secret-for-the-pre-encrypted-vm-to-your-key-vault"></a><span data-ttu-id="c7536-851">Przekaż hasło szyfrowania dysków dla maszyny Wirtualnej zaszyfrowane wstępnie do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="c7536-851">Upload the disk-encryption secret for the pre-encrypted VM to your key vault</span></span>
<span data-ttu-id="c7536-852">Klucz tajny szyfrowanie dysków, które zostały uzyskane musi wcześniej przekazany jako klucza tajnego w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-852">The disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="c7536-853">Magazyn kluczy musi mieć uprawnienia, włączona dla klienta usługi Azure AD i szyfrowanie dysków.</span><span class="sxs-lookup"><span data-stu-id="c7536-853">The key vault needs to have disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="c7536-854">Hasło szyfrowania dysku nie jest zaszyfrowany przy KEK</span><span class="sxs-lookup"><span data-stu-id="c7536-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="c7536-855">Aby skonfigurować klucza tajnego w magazynie kluczy, należy użyć [AzureKeyVaultSecret zestawu](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="c7536-855">To set up the secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="c7536-856">Jeśli masz maszyny wirtualnej systemu Windows, plik bek jest zakodowany jako ciąg base64 i następnie przekazywane do przy użyciu magazynu kluczy `Set-AzureKeyVaultSecret` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7536-856">If you have a Windows virtual machine, the bek file is encoded as a base64 string and then uploaded to your key vault using the `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="c7536-857">Dla systemu Linux hasło jest zakodowany jako ciąg base64, a następnie przekazać do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-857">For Linux, the passphrase is encoded as a base64 string and then uploaded to the key vault.</span></span> <span data-ttu-id="c7536-858">Ponadto upewnij się, że następujące znaczniki są ustawione podczas tworzenia klucza tajnego w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="c7536-858">In addition, make sure that the following tags are set when you create the secret in the key vault.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="c7536-859">Użyj `$secretUrl` w następnym kroku dla [dołączanie dysku systemu operacyjnego bez użycia KEK](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="c7536-859">Use the `$secretUrl` in the next step for [attaching the OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="c7536-860">Hasło szyfrowania dysku zaszyfrowane za pomocą KEK</span><span class="sxs-lookup"><span data-stu-id="c7536-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="c7536-861">Przed przekazaniem klucza tajnego do magazynu kluczy, można opcjonalnie zaszyfrować przy użyciu klucza szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-861">Before you upload the secret to the key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="c7536-862">Użyj zawijania [interfejsu API](https://msdn.microsoft.com/library/azure/dn878066.aspx) najpierw szyfrowania klucza tajnego za pomocą klucza szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c7536-862">Use the wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) to first encrypt the secret using the key encryption key.</span></span> <span data-ttu-id="c7536-863">Wynik tej operacji zawijania jest base64 ciągu zakodowane w adresie URL, który można następnie przekazać jako klucz tajny przy użyciu [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7536-863">The output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using the [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="c7536-864">Użyj `$KeyEncryptionKey` i `$secretUrl` w następnym kroku dla [dołączanie dysku systemu operacyjnego przy użyciu KEK](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="c7536-864">Use `$KeyEncryptionKey` and `$secretUrl` in the next step for [attaching the OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="c7536-865">Określ adres URL tajne, po podłączeniu dysku systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="c7536-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="c7536-866">Bez użycia KEK</span><span class="sxs-lookup"><span data-stu-id="c7536-866">Without using a KEK</span></span>
<span data-ttu-id="c7536-867">Podczas dołączania dysk systemu operacyjnego, musisz przekazać `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="c7536-867">While you are attaching the OS disk, you need to pass `$secretUrl`.</span></span> <span data-ttu-id="c7536-868">Adres URL został wygenerowany w sekcji "nie jest zaszyfrowany przy KEK tajny szyfrowanie dysków".</span><span class="sxs-lookup"><span data-stu-id="c7536-868">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="c7536-869">Przy użyciu KEK</span><span class="sxs-lookup"><span data-stu-id="c7536-869">Using a KEK</span></span>
<span data-ttu-id="c7536-870">Po podłączeniu dysku systemu operacyjnego, należy przekazać `$KeyEncryptionKey` i `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="c7536-870">When you attach the OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="c7536-871">Adres URL został wygenerowany w sekcji "nie jest zaszyfrowany przy KEK tajny szyfrowanie dysków".</span><span class="sxs-lookup"><span data-stu-id="c7536-871">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="c7536-872">Pobierz w tym przewodniku</span><span class="sxs-lookup"><span data-stu-id="c7536-872">Download this guide</span></span>
<span data-ttu-id="c7536-873">Możesz pobrać ten przewodnik z [galerii TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="c7536-873">You can download this guide from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="c7536-874">Aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="c7536-874">For more information</span></span>
[<span data-ttu-id="c7536-875">Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 1</span><span class="sxs-lookup"><span data-stu-id="c7536-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="c7536-876">Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 2</span><span class="sxs-lookup"><span data-stu-id="c7536-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
