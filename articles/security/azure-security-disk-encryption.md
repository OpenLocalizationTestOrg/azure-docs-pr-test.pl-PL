---
title: "Szyfrowanie dysków systemu Windows i maszyn wirtualnych systemu Linux IaaS aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="3417e-103">Szyfrowanie dysków Azure dla systemu Windows i maszyn wirtualnych systemu Linux IaaS</span><span class="sxs-lookup"><span data-stu-id="3417e-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="3417e-104">Microsoft Azure jest silnie zatwierdzone tooensuring prywatności danych suwerenności danych i umożliwia toocontrol platformy Azure hostowanej danych za pomocą wielu zaawansowanych technologii tooencrypt, sterowania i zarządzania kluczami szyfrowania, inspekcji i kontroli dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="3417e-104">Microsoft Azure is strongly committed tooensuring your data privacy, data sovereignty and enables you toocontrol your Azure hosted data through a range of advanced technologies tooencrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="3417e-105">Zapewnia to użytkownikom Azure hello elastyczność toochoose hello rozwiązania, która najlepiej spełnia ich potrzeb biznesowych.</span><span class="sxs-lookup"><span data-stu-id="3417e-105">This provides Azure customers hello flexibility toochoose hello solution that best meets their business needs.</span></span> <span data-ttu-id="3417e-106">W tym dokumencie, możemy przedstawiono nowe rozwiązanie technologii tooa "Szyfrowania dysków Azure dla systemu Windows i Linux IaaS VM" toohelp ochrony i chronić Twoje toomeet danych Twojej organizacji zobowiązań zabezpieczeń i zgodności.</span><span class="sxs-lookup"><span data-stu-id="3417e-106">In this paper, we will introduce you tooa new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” toohelp protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="3417e-107">dokument Hello znajdują się szczegółowe wskazówki dotyczące jak toouse hello Azure dysku szyfrowania funkcje takie jak hello obsługiwane scenariusze i hello środowiska użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3417e-107">hello paper provides detailed guidance on how toouse hello Azure disk encryption features including hello supported scenarios and hello user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-108">Zastosowanie niektórych zaleceń zamieszczonych może zwiększyć danych, sieci i użycia zasobów obliczeniowych, co powoduje dodatkowych kosztów licencji lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3417e-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="3417e-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3417e-109">Overview</span></span>
<span data-ttu-id="3417e-110">Szyfrowanie dysków Azure jest nową możliwość, która pomaga szyfrowania dysków maszyny wirtualnej systemu Windows i Linux IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="3417e-111">Szyfrowanie dysków Azure korzysta z branżowymi hello [funkcji BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funkcji systemu Windows i hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) funkcji szyfrowania woluminów tooprovide Linux hello systemu operacyjnego i dysków z danymi hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-111">Azure Disk Encryption leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="3417e-112">rozwiązanie Hello jest zintegrowany z [usługi Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp sterowania i zarządzania hello szyfrowanie dysków kluczy i kluczy tajnych w magazynie kluczy subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3417e-112">hello solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="3417e-113">rozwiązanie Hello gwarantuje również, że wszystkie dane na powitania dysków maszyny wirtualnej są szyfrowane, gdy w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-113">hello solution also ensures that all data on hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="3417e-114">Szyfrowanie dysków Azure dla systemu Windows i maszyn wirtualnych systemu Linux IaaS, jest teraz w **ogólnej dostępności** we wszystkich regionach publicznej platformy Azure i regiony AzureGov standardowe maszyn wirtualnych i maszyn wirtualnych z magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="3417e-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="3417e-115">Scenariusze szyfrowania</span><span class="sxs-lookup"><span data-stu-id="3417e-115">Encryption scenarios</span></span>
<span data-ttu-id="3417e-116">Witaj rozwiązania szyfrowania dysków Azure obsługuje hello następujących scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="3417e-116">hello Azure Disk Encryption solution supports hello following customer scenarios:</span></span>

* <span data-ttu-id="3417e-117">Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS utworzone na podstawie wstępnie zaszyfrowany dysk VHD i kluczy szyfrowania</span><span class="sxs-lookup"><span data-stu-id="3417e-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="3417e-118">Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS utworzone na podstawie hello obsługiwane galerii Azure obrazów</span><span class="sxs-lookup"><span data-stu-id="3417e-118">Enable encryption on new IaaS VMs created from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="3417e-119">Włącz szyfrowanie dla istniejących maszyn wirtualnych IaaS działające na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3417e-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="3417e-120">Wyłącz szyfrowanie na maszynach wirtualnych IaaS systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3417e-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="3417e-121">Wyłącz szyfrowanie dysków danych dla maszyn wirtualnych systemu Linux IaaS</span><span class="sxs-lookup"><span data-stu-id="3417e-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="3417e-122">Włącz szyfrowanie dysków zarządzanych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="3417e-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="3417e-123">Aktualizowanie ustawień szyfrowania istniejących zaszyfrowanych inne niż premium magazynu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3417e-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="3417e-124">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych, zaszyfrowane za pomocą klucza szyfrowania</span><span class="sxs-lookup"><span data-stu-id="3417e-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="3417e-125">rozwiązanie Hello obsługuje następujące scenariusze dla maszyn wirtualnych IaaS, jeśli są włączone w systemie Microsoft Azure hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-125">hello solution supports hello following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="3417e-126">Integracja z usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="3417e-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="3417e-127">Maszyny wirtualne warstwy standardowa: [A, D DS, G, GS, F i itp szeregów maszyn wirtualnych IaaS](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="3417e-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="3417e-128">Włącz szyfrowania w systemach Windows i Linux maszyny wirtualne IaaS i dysków zarządzanych maszyn wirtualnych z hello obsługiwane galerii Azure obrazów</span><span class="sxs-lookup"><span data-stu-id="3417e-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="3417e-129">Wyłącz szyfrowanie dysków systemu operacyjnego i danych dla maszyn wirtualnych IaaS systemu Windows i dysków zarządzanych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="3417e-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="3417e-130">Wyłącz szyfrowanie dysków danych dla maszyn wirtualnych systemu Linux IaaS i dysków zarządzanych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="3417e-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="3417e-131">Włącz szyfrowanie dla maszyn wirtualnych IaaS systemem kliencki system operacyjny Windows</span><span class="sxs-lookup"><span data-stu-id="3417e-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="3417e-132">Włącz szyfrowanie dla woluminów przy użyciu ścieżki instalacji</span><span class="sxs-lookup"><span data-stu-id="3417e-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="3417e-133">Włącz szyfrowanie dla maszyn wirtualnych systemu Linux skonfigurowany z dysku przy użyciu mdadm zastosowanie rozkładania (RAID)</span><span class="sxs-lookup"><span data-stu-id="3417e-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="3417e-134">Włącz szyfrowanie dla maszyn wirtualnych systemu Linux przy użyciu LVM dla dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="3417e-135">Włącz szyfrowanie dla maszyn wirtualnych systemu Windows skonfigurowane z funkcją miejsca do magazynowania</span><span class="sxs-lookup"><span data-stu-id="3417e-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="3417e-136">Aktualizowanie ustawień szyfrowania istniejących zaszyfrowanych inne niż premium magazynu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3417e-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="3417e-137">Wszystkie publiczne Azure i AzureGov regiony są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3417e-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="3417e-138">rozwiązanie Hello nie obsługuje następujące scenariusze, funkcje i technologie hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-138">hello solution does not support hello following scenarios, features, and technology:</span></span>

* <span data-ttu-id="3417e-139">Maszyny wirtualne IaaS warstwa podstawowa</span><span class="sxs-lookup"><span data-stu-id="3417e-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="3417e-140">Wyłączenie szyfrowania na dysku systemu operacyjnego dla maszyn wirtualnych systemu Linux IaaS</span><span class="sxs-lookup"><span data-stu-id="3417e-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="3417e-141">Wyłączenie szyfrowania na dysku danych, jeśli hello dysku systemu operacyjnego jest szyfrowany dla maszyn wirtualnych systemu Linux Iaas</span><span class="sxs-lookup"><span data-stu-id="3417e-141">Disabling encryption on a data drive if hello OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="3417e-142">Maszyny wirtualne IaaS, utworzony przy użyciu hello klasycznego metodę tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3417e-142">IaaS VMs that are created by using hello classic VM creation method</span></span>
* <span data-ttu-id="3417e-143">Włącz szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS niestandardowych obrazów klienta nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="3417e-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="3417e-144">Włącz enccryption w systemie operacyjnym Linux LVM dysk nie jest obsługiwany obecnie.</span><span class="sxs-lookup"><span data-stu-id="3417e-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="3417e-145">Ta obsługa rozpocznie się wkrótce.</span><span class="sxs-lookup"><span data-stu-id="3417e-145">This support will come soon.</span></span>
* <span data-ttu-id="3417e-146">Integracja z lokalnej usługi zarządzania kluczami</span><span class="sxs-lookup"><span data-stu-id="3417e-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="3417e-147">Usługa pliki Azure (udostępnionego systemu plików), sieciowego systemu plików (NFS), dynamiczne woluminy i maszyn wirtualnych systemu Windows, które są skonfigurowane przy użyciu systemów opartych na oprogramowaniu RAID</span><span class="sxs-lookup"><span data-stu-id="3417e-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="3417e-148">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych, szyfrowane bez klucza szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="3417e-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="3417e-149">Zaktualizuj ustawienia szyfrowania istniejącego magazynu premium zaszyfrowanych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-150">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych jest obsługiwana tylko dla maszyn wirtualnych, które są szyfrowane przy hello KEK konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3417e-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="3417e-151">Nie jest obsługiwana na maszynach wirtualnych, które są szyfrowane bez KEK.</span><span class="sxs-lookup"><span data-stu-id="3417e-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="3417e-152">KEK jest opcjonalnym parametrem, który włącza szyfrowanie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="3417e-153">Ta obsługa zostanie wkrótce uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="3417e-153">This support is coming soon.</span></span>
> <span data-ttu-id="3417e-154">Aktualizuj ustawienia szyfrowania istniejący magazyn w warstwie premium zaszyfrowanych maszyny Wirtualnej nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3417e-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="3417e-155">Ta obsługa zostanie wkrótce uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="3417e-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="3417e-156">Funkcji szyfrowania</span><span class="sxs-lookup"><span data-stu-id="3417e-156">Encryption features</span></span>
<span data-ttu-id="3417e-157">Po włączeniu i wdrożeniu szyfrowania dysków Azure dla maszyn wirtualnych IaaS platformy Azure, hello następujące funkcje są włączone, w zależności od konfiguracji hello podane:</span><span class="sxs-lookup"><span data-stu-id="3417e-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, hello following capabilities are enabled, depending on hello configuration provided:</span></span>

* <span data-ttu-id="3417e-158">Szyfrowanie woluminu rozruchowego hello systemu operacyjnego woluminu tooprotect hello magazynowane w magazynie</span><span class="sxs-lookup"><span data-stu-id="3417e-158">Encryption of hello OS volume tooprotect hello boot volume at rest in your storage</span></span>
* <span data-ttu-id="3417e-159">Szyfrowanie danych woluminów tooprotect hello ilości danych przechowywanych w magazynie</span><span class="sxs-lookup"><span data-stu-id="3417e-159">Encryption of data volumes tooprotect hello data volumes at rest in your storage</span></span>
* <span data-ttu-id="3417e-160">Wyłączenie szyfrowania na powitania systemu operacyjnego i danych dyski dla maszyn wirtualnych IaaS systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3417e-160">Disabling encryption on hello OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="3417e-161">Wyłączenie szyfrowania danych hello dyski dla maszyn wirtualnych systemu Linux IaaS (tylko wtedy, gdy nie jest zaszyfrowany to dysk systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="3417e-161">Disabling encryption on hello data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="3417e-162">Ochrona hello szyfrowania kluczy i kluczy tajnych w magazynie kluczy subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3417e-162">Safeguarding hello encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="3417e-163">Raportowanie stanu szyfrowania hello hello szyfrowane maszyn wirtualnych IaaS</span><span class="sxs-lookup"><span data-stu-id="3417e-163">Reporting hello encryption status of hello encrypted IaaS VM</span></span>
* <span data-ttu-id="3417e-164">Usuwanie ustawień konfiguracji szyfrowania dysków z maszyn wirtualnych IaaS hello</span><span class="sxs-lookup"><span data-stu-id="3417e-164">Removal of disk-encryption configuration settings from hello IaaS virtual machine</span></span>
* <span data-ttu-id="3417e-165">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych za pomocą usługi Kopia zapasowa Azure hello</span><span class="sxs-lookup"><span data-stu-id="3417e-165">Backup and restore of encrypted VMs by using hello Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-166">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych jest obsługiwana tylko dla maszyn wirtualnych, które są szyfrowane przy hello KEK konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3417e-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="3417e-167">Nie jest obsługiwana na maszynach wirtualnych, które są szyfrowane bez KEK.</span><span class="sxs-lookup"><span data-stu-id="3417e-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="3417e-168">KEK jest opcjonalnym parametrem, który włącza szyfrowanie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="3417e-169">Szyfrowanie dysków Azure maszyny Wirtualne IaaS dla systemu Windows i Linux rozwiązanie obejmuje:</span><span class="sxs-lookup"><span data-stu-id="3417e-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="3417e-170">Witaj rozszerzenie szyfrowanie dysków dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3417e-170">hello disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="3417e-171">Witaj rozszerzenie szyfrowanie dysków dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="3417e-171">hello disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="3417e-172">Witaj szyfrowanie dysków poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3417e-172">hello disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="3417e-173">Witaj szyfrowania dysku poleceń cmdlet Azure interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="3417e-173">hello disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="3417e-174">Witaj szablonów usługi Azure Resource Manager szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="3417e-174">hello disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="3417e-175">Witaj rozwiązania szyfrowania dysków Azure jest obsługiwana na maszynach wirtualnych IaaS, które korzystają z systemu Windows lub systemu operacyjnego Linux.</span><span class="sxs-lookup"><span data-stu-id="3417e-175">hello Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="3417e-176">Aby uzyskać więcej informacji na temat hello obsługiwanych systemów operacyjnych, zobacz hello "wymagania wstępne" sekcji.</span><span class="sxs-lookup"><span data-stu-id="3417e-176">For more information about hello supported operating systems, see hello "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-177">Brak bez dodatkowych opłat szyfrowanie dysków maszyny Wirtualnej przy użyciu szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="3417e-178">Opis korzyści</span><span class="sxs-lookup"><span data-stu-id="3417e-178">Value proposition</span></span>
<span data-ttu-id="3417e-179">Po zastosowaniu rozwiązania hello zarządzania szyfrowania dysków Azure mogą spełniać powitania po potrzeb biznesowych:</span><span class="sxs-lookup"><span data-stu-id="3417e-179">When you apply hello Azure Disk Encryption-management solution, you can satisfy hello following business needs:</span></span>

* <span data-ttu-id="3417e-180">Maszyny wirtualne IaaS są już zabezpieczone w stanie spoczynku, ponieważ mogą używać szyfrowania standardowych technologii tooaddress zabezpieczeń i zgodności wymagań organizacyjnych.</span><span class="sxs-lookup"><span data-stu-id="3417e-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology tooaddress organizational security and compliance requirements.</span></span>
* <span data-ttu-id="3417e-181">Maszyny wirtualne IaaS rozruchu w obszarze klucze kontrolowane przez klienta i zasad, a można inspekcji ich użycia w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="3417e-182">Szyfrowanie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="3417e-182">Encryption workflow</span></span>
<span data-ttu-id="3417e-183">Szyfrowanie dysków tooenable systemu Windows i maszyn wirtualnych systemu Linux, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3417e-183">tooenable disk encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="3417e-184">Wybierz scenariusz szyfrowania spośród hello poprzedzających scenariuszy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="3417e-184">Choose an encryption scenario from among hello preceding encryption scenarios.</span></span>
2. <span data-ttu-id="3417e-185">Włączyć tooenabling szyfrowanie dysków za pomocą szablonu Menedżera zasobów szyfrowania dysków Azure hello, poleceń cmdlet programu PowerShell lub polecenia interfejsu wiersza polecenia, a następnie określ hello konfiguracji szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="3417e-185">Opt in tooenabling disk encryption via hello Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify hello encryption configuration.</span></span>

   * <span data-ttu-id="3417e-186">W przypadku hello szyfrowane klienta scenariusz wirtualnego dysku twardego przekazać konto magazynu tooyour wirtualnego dysku twardego hello szyfrowane i hello magazynu kluczy tooyour materiału klucza szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="3417e-186">For hello customer-encrypted VHD scenario, upload hello encrypted VHD tooyour storage account and hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="3417e-187">Następnie podaj tooenable konfiguracji szyfrowania hello na nowej maszyny Wirtualnej IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-187">Then, provide hello encryption configuration tooenable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="3417e-188">Nowe maszyny wirtualne, które są tworzone na podstawie hello Marketplace i istniejących maszyn wirtualnych, które zostały już uruchomione na platformie Azure Podaj tooenable konfiguracji szyfrowania hello na powitania maszyn wirtualnych IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-188">For new VMs that are created from hello Marketplace and existing VMs that are already running in Azure, provide hello encryption configuration tooenable encryption on hello IaaS VM.</span></span>

3. <span data-ttu-id="3417e-189">Udziel dostępu toohello platformy Azure tooread hello klucza szyfrowania materiału (klucze szyfrowania funkcji BitLocker dla systemów Windows) i hasło dla systemu Linux z magazynu kluczy szyfrowania tooenable na powitania maszyn wirtualnych IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-189">Grant access toohello Azure platform tooread hello encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault tooenable encryption on hello IaaS VM.</span></span>

4. <span data-ttu-id="3417e-190">Podaj hello Azure Active Directory (Azure AD) aplikacji tożsamości toowrite hello szyfrowania tooyour materiału klucza magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-190">Provide hello Azure Active Directory (Azure AD) application identity toowrite hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="3417e-191">Dzięki temu włącza szyfrowanie na powitania maszyn wirtualnych IaaS dla scenariuszy hello wspomnianego w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="3417e-191">Doing so enables encryption on hello IaaS VM for hello scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="3417e-192">Azure aktualizuje modelu usługi hello maszyny Wirtualnej przy użyciu szyfrowania i hello konfiguracji magazynu kluczy i konfiguruje zaszyfrowanych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-192">Azure updates hello VM service model with encryption and hello key vault configuration, and sets up your encrypted VM.</span></span>

 ![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="3417e-194">Odszyfrowywanie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="3417e-194">Decryption workflow</span></span>
<span data-ttu-id="3417e-195">Szyfrowanie dysków toodisable dla maszyn wirtualnych IaaS, pełną hello następujące ogólne kroki:</span><span class="sxs-lookup"><span data-stu-id="3417e-195">toodisable disk encryption for IaaS VMs, complete hello following high-level steps:</span></span>

1. <span data-ttu-id="3417e-196">Wybierz toodisable szyfrowania (odszyfrowywania) na uruchomionych maszyn wirtualnych IaaS na platformie Azure za pośrednictwem hello szablon Menedżera zasobów szyfrowania dysków Azure lub poleceń cmdlet programu PowerShell i określ hello odszyfrowywania konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3417e-196">Choose toodisable encryption (decryption) on a running IaaS VM in Azure via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify hello decryption configuration.</span></span>

 <span data-ttu-id="3417e-197">Ten krok powoduje wyłączenie szyfrowania woluminu danych systemu operacyjnego lub hello hello lub obu tych programów na powitania uruchamiania maszyny Wirtualnej systemu Windows IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-197">This step disables encryption of hello OS or hello data volume or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="3417e-198">Jednakże jak wspomniano w poprzedniej sekcji hello, wyłączenie szyfrowania dysku systemu operacyjnego Linux nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3417e-198">However, as mentioned in hello previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="3417e-199">krok odszyfrowywania Hello jest dozwolone tylko w przypadku dysków z danymi na maszynach wirtualnych systemu Linux tak długo, jak hello dysk systemu operacyjnego nie jest zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="3417e-199">hello decryption step is allowed only for data drives on Linux VMs as long as hello OS disk is not encrypted.</span></span>
2. <span data-ttu-id="3417e-200">Aktualizacje Azure hello modelu usług maszyny Wirtualnej, a hello IaaS maszyny Wirtualnej jest oznaczony jako odszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="3417e-200">Azure updates hello VM service model, and hello IaaS VM is marked decrypted.</span></span> <span data-ttu-id="3417e-201">zawartość Hello hello maszyny Wirtualnej nie są szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="3417e-201">hello contents of hello VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-202">Operacja disable szyfrowania Hello nie powoduje usunięcia z magazynu i hello szyfrowania klucza materiału klucza (klucze szyfrowania funkcji BitLocker dla systemów Windows) lub hasło dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="3417e-202">hello disable-encryption operation does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="3417e-203">Wyłączenie szyfrowania dysku systemu operacyjnego Linux nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3417e-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="3417e-204">krok odszyfrowywania Hello jest dozwolone tylko w przypadku dysków z danymi na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="3417e-204">hello decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="3417e-205">Wyłączenie szyfrowania dysku danych dla systemu Linux nie jest obsługiwane, jeśli hello dysku systemu operacyjnego jest szyfrowany.</span><span class="sxs-lookup"><span data-stu-id="3417e-205">Disabling data disk encryption for Linux is not supported if hello OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3417e-206">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3417e-206">Prerequisites</span></span>
<span data-ttu-id="3417e-207">Przed włączeniem szyfrowania dysków Azure na maszynach wirtualnych Azure IaaS dla hello obsługiwane scenariusze, które zostały omówione w sekcji "Przegląd" hello, zobacz hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="3417e-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for hello supported scenarios that were discussed in hello "Overview" section, see hello following prerequisites:</span></span>

* <span data-ttu-id="3417e-208">Zasoby toocreate prawidłowy aktywną subskrypcją platformy Azure musi mieć na platformie Azure w regionach hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3417e-208">You must have a valid active Azure subscription toocreate resources in Azure in hello supported regions.</span></span>
* <span data-ttu-id="3417e-209">Szyfrowanie dysków Azure jest obsługiwana na powitania następujące wersje systemu Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 i Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="3417e-209">Azure Disk Encryption is supported on hello following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="3417e-210">Szyfrowanie dysków Azure jest obsługiwana w następujących wersjach klientów systemu Windows hello: Windows 10 i Windows 8 klienta.</span><span class="sxs-lookup"><span data-stu-id="3417e-210">Azure Disk Encryption is supported on hello following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-211">Dla systemu Windows Server 2008 R2 musisz mieć zainstalowany przed włączeniem szyfrowania na platformie Azure programu .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="3417e-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="3417e-212">Można zainstalować z witryny Windows Update, instalując hello opcjonalną aktualizację programu Microsoft .NET Framework 4.5.2 dla systemów opartych na x64 systemu Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="3417e-212">You can install it from Windows Update by installing hello optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="3417e-213">Szyfrowanie dysków Azure jest obsługiwana na powitania po galerii Azure na podstawie dystrybucje systemu Linux serwera oraz wersje:</span><span class="sxs-lookup"><span data-stu-id="3417e-213">Azure Disk Encryption is supported on hello following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="3417e-214">Dystrybucja systemu Linux</span><span class="sxs-lookup"><span data-stu-id="3417e-214">Linux Distribution</span></span> | <span data-ttu-id="3417e-215">Wersja</span><span class="sxs-lookup"><span data-stu-id="3417e-215">Version</span></span> | <span data-ttu-id="3417e-216">Typ woluminu obsługiwany w przypadku szyfrowania</span><span class="sxs-lookup"><span data-stu-id="3417e-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="3417e-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3417e-217">Ubuntu</span></span> | <span data-ttu-id="3417e-218">16.04 — CODZIENNIE LTS</span><span class="sxs-lookup"><span data-stu-id="3417e-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="3417e-219">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="3417e-219">OS and Data disk</span></span> |
| <span data-ttu-id="3417e-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3417e-220">Ubuntu</span></span> | <span data-ttu-id="3417e-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="3417e-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="3417e-222">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="3417e-222">OS and Data disk</span></span> |
| <span data-ttu-id="3417e-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3417e-223">Ubuntu</span></span> | <span data-ttu-id="3417e-224">12.10</span><span class="sxs-lookup"><span data-stu-id="3417e-224">12.10</span></span> | <span data-ttu-id="3417e-225">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-225">Data disk</span></span> |
| <span data-ttu-id="3417e-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3417e-226">Ubuntu</span></span> | <span data-ttu-id="3417e-227">12.04</span><span class="sxs-lookup"><span data-stu-id="3417e-227">12.04</span></span> | <span data-ttu-id="3417e-228">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-228">Data disk</span></span> |
| <span data-ttu-id="3417e-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="3417e-229">RHEL</span></span> | <span data-ttu-id="3417e-230">7.3</span><span class="sxs-lookup"><span data-stu-id="3417e-230">7.3</span></span> | <span data-ttu-id="3417e-231">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="3417e-231">OS and Data disk</span></span> |
| <span data-ttu-id="3417e-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="3417e-232">RHEL</span></span> | <span data-ttu-id="3417e-233">7.2</span><span class="sxs-lookup"><span data-stu-id="3417e-233">7.2</span></span> | <span data-ttu-id="3417e-234">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="3417e-234">OS and Data disk</span></span> |
| <span data-ttu-id="3417e-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="3417e-235">RHEL</span></span> | <span data-ttu-id="3417e-236">6.8</span><span class="sxs-lookup"><span data-stu-id="3417e-236">6.8</span></span> | <span data-ttu-id="3417e-237">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="3417e-237">OS and Data disk</span></span> |
| <span data-ttu-id="3417e-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="3417e-238">RHEL</span></span> | <span data-ttu-id="3417e-239">6.7</span><span class="sxs-lookup"><span data-stu-id="3417e-239">6.7</span></span> | <span data-ttu-id="3417e-240">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-240">Data disk</span></span> |
| <span data-ttu-id="3417e-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="3417e-241">CentOS</span></span> | <span data-ttu-id="3417e-242">7.3</span><span class="sxs-lookup"><span data-stu-id="3417e-242">7.3</span></span> | <span data-ttu-id="3417e-243">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="3417e-243">OS and Data disk</span></span> |
| <span data-ttu-id="3417e-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="3417e-244">CentOS</span></span> | <span data-ttu-id="3417e-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="3417e-245">7.2n</span></span> | <span data-ttu-id="3417e-246">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="3417e-246">OS and Data disk</span></span> |
| <span data-ttu-id="3417e-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="3417e-247">CentOS</span></span> | <span data-ttu-id="3417e-248">6.8</span><span class="sxs-lookup"><span data-stu-id="3417e-248">6.8</span></span> | <span data-ttu-id="3417e-249">Dysk systemu operacyjnego i danych</span><span class="sxs-lookup"><span data-stu-id="3417e-249">OS and Data disk</span></span> |
| <span data-ttu-id="3417e-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="3417e-250">CentOS</span></span> | <span data-ttu-id="3417e-251">7.1</span><span class="sxs-lookup"><span data-stu-id="3417e-251">7.1</span></span> | <span data-ttu-id="3417e-252">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-252">Data disk</span></span> |
| <span data-ttu-id="3417e-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="3417e-253">CentOS</span></span> | <span data-ttu-id="3417e-254">7.0</span><span class="sxs-lookup"><span data-stu-id="3417e-254">7.0</span></span> | <span data-ttu-id="3417e-255">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-255">Data disk</span></span> |
| <span data-ttu-id="3417e-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="3417e-256">CentOS</span></span> | <span data-ttu-id="3417e-257">6.7</span><span class="sxs-lookup"><span data-stu-id="3417e-257">6.7</span></span> | <span data-ttu-id="3417e-258">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-258">Data disk</span></span> |
| <span data-ttu-id="3417e-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="3417e-259">CentOS</span></span> | <span data-ttu-id="3417e-260">6.6</span><span class="sxs-lookup"><span data-stu-id="3417e-260">6.6</span></span> | <span data-ttu-id="3417e-261">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-261">Data disk</span></span> |
| <span data-ttu-id="3417e-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="3417e-262">CentOS</span></span> | <span data-ttu-id="3417e-263">6.5</span><span class="sxs-lookup"><span data-stu-id="3417e-263">6.5</span></span> | <span data-ttu-id="3417e-264">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-264">Data disk</span></span> |
| <span data-ttu-id="3417e-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="3417e-265">openSUSE</span></span> | <span data-ttu-id="3417e-266">13.2</span><span class="sxs-lookup"><span data-stu-id="3417e-266">13.2</span></span> | <span data-ttu-id="3417e-267">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-267">Data disk</span></span> |
| <span data-ttu-id="3417e-268">SLES</span><span class="sxs-lookup"><span data-stu-id="3417e-268">SLES</span></span> | <span data-ttu-id="3417e-269">12 Z DODATKIEM SP1</span><span class="sxs-lookup"><span data-stu-id="3417e-269">12 SP1</span></span> | <span data-ttu-id="3417e-270">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-270">Data disk</span></span> |
| <span data-ttu-id="3417e-271">SLES</span><span class="sxs-lookup"><span data-stu-id="3417e-271">SLES</span></span> | <span data-ttu-id="3417e-272">12 dodatku SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="3417e-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="3417e-273">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-273">Data disk</span></span> |
| <span data-ttu-id="3417e-274">SLES</span><span class="sxs-lookup"><span data-stu-id="3417e-274">SLES</span></span> | <span data-ttu-id="3417e-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="3417e-275">HPC 12</span></span> | <span data-ttu-id="3417e-276">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-276">Data disk</span></span> |
| <span data-ttu-id="3417e-277">SLES</span><span class="sxs-lookup"><span data-stu-id="3417e-277">SLES</span></span> | <span data-ttu-id="3417e-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="3417e-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="3417e-279">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-279">Data disk</span></span> |
| <span data-ttu-id="3417e-280">SLES</span><span class="sxs-lookup"><span data-stu-id="3417e-280">SLES</span></span> | <span data-ttu-id="3417e-281">11 Z DODATKIEM SP4</span><span class="sxs-lookup"><span data-stu-id="3417e-281">11 SP4</span></span> | <span data-ttu-id="3417e-282">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="3417e-282">Data disk</span></span> |

* <span data-ttu-id="3417e-283">Szyfrowanie dysków Azure wymaga, że magazyn kluczy i maszyny wirtualne znajdują się w hello sam region platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3417e-283">Azure Disk Encryption requires that your key vault and VMs reside in hello same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-284">Konfigurowanie zasobów hello w oddzielnych regionach powoduje to niepowodzenie w włączenie funkcji szyfrowania dysków Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-284">Configuring hello resources in separate regions causes a failure in enabling hello Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="3417e-285">tooset w górę i Konfigurowanie magazynu kluczy do szyfrowania dysków Azure, zobacz sekcję **ustawiony w górę i konfigurowania magazynu kluczy szyfrowania dysków Azure** w hello *wymagania wstępne* sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="3417e-285">tooset up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="3417e-286">tooset w górę i konfigurowania aplikacji usługi Azure AD w usłudze Azure Active directory szyfrowanie dysków Azure, zobacz sekcję **skonfigurowanie aplikacji hello Azure AD w usłudze Azure Active Directory** w hello *wymagania wstępne* w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="3417e-286">tooset up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up hello Azure AD application in Azure Active Directory** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="3417e-287">tooset w górę i skonfigurować zasady dostępu magazynu kluczy hello aplikacji hello Azure AD, zobacz sekcję **skonfigurować zasady dostępu magazynu kluczy hello aplikacji hello Azure AD** w hello *wymagania wstępne* sekcji w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="3417e-287">tooset up and configure hello key vault access policy for hello Azure AD application, see section **Set up hello key vault access policy for hello Azure AD application** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="3417e-288">tooprepare wstępnie zaszyfrowanego dysku VHD systemu Windows, zobacz sekcję **przygotować wstępnie zaszyfrowanego dysku VHD systemu Windows** w hello *dodatku*.</span><span class="sxs-lookup"><span data-stu-id="3417e-288">tooprepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="3417e-289">tooprepare wstępnie zaszyfrowanego dysku VHD systemu Linux, zobacz sekcję **przygotować wstępnie zaszyfrowanego dysku VHD systemu Linux** w hello *dodatku*.</span><span class="sxs-lookup"><span data-stu-id="3417e-289">tooprepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="3417e-290">Hello platformy Azure wymaga dostępu toohello szyfrowania kluczy lub kluczy tajnych w toomake Twojego magazynu kluczy ich toohello dostępne maszyny wirtualnej, podczas rozruchu i odszyfrowuje hello wolumin maszyny wirtualnej systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3417e-290">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello virtual machine when it boots and decrypts hello virtual machine OS volume.</span></span> <span data-ttu-id="3417e-291">toogrant uprawnienia tooAzure platformy, zestaw hello **EnabledForDiskEncryption** właściwość w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-291">toogrant permissions tooAzure platform, set hello **EnabledForDiskEncryption** property in hello key vault.</span></span> <span data-ttu-id="3417e-292">Aby uzyskać więcej informacji, zobacz **ustawiony w górę i konfigurowania magazynu kluczy szyfrowania dysków Azure** w hello dodatku.</span><span class="sxs-lookup"><span data-stu-id="3417e-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in hello Appendix.</span></span>
* <span data-ttu-id="3417e-293">Klucz tajny magazynu kluczy, a adresy URL KEK musi być numerów wersji.</span><span class="sxs-lookup"><span data-stu-id="3417e-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="3417e-294">Azure wymusza to ograniczenie wersji.</span><span class="sxs-lookup"><span data-stu-id="3417e-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="3417e-295">Nieprawidłowy klucz tajny i KEK adresów URL zobacz następujące przykłady hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-295">For valid secret and KEK URLs, see hello following examples:</span></span>

  * <span data-ttu-id="3417e-296">Przykład prawidłowego adresu URL tajny: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="3417e-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="3417e-297">Przykład prawidłowy adres URL KEK: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="3417e-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="3417e-298">Szyfrowanie dysków Azure nie obsługuje określania numery portów, jako część adresy URL KEK i kluczy tajnych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="3417e-299">Przykłady adresów URL magazynu kluczy obsługiwanych i nieobsługiwanych można znaleźć w następujących hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-299">For examples of non-supported and supported key vault URLs, see hello following:</span></span>

  * <span data-ttu-id="3417e-300">Adres URL magazynu kluczy można zaakceptować *https://contosovault.vault.azure.net:443/klucze tajne/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="3417e-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="3417e-301">Adres URL magazynu kluczy dopuszczalne: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="3417e-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="3417e-302">tooenable funkcja szyfrowania dysków Azure hello, hello maszyn wirtualnych IaaS musi spełniać następujące wymagania dotyczące konfiguracji punktu końcowego sieci hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-302">tooenable hello Azure Disk Encryption feature, hello IaaS VMs must meet hello following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="3417e-303">tooget token tooconnect tooyour magazyn kluczy, hello maszyn wirtualnych IaaS musi być możliwe tooconnect punktu końcowego usługi Azure Active Directory tooan, \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="3417e-303">tooget a token tooconnect tooyour key vault, hello IaaS VM must be able tooconnect tooan Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="3417e-304">toowrite hello szyfrowania kluczy tooyour magazynu kluczy, hello IaaS maszyny Wirtualnej musi być punktu końcowego magazynu kluczy toohello tooconnect stanie.</span><span class="sxs-lookup"><span data-stu-id="3417e-304">toowrite hello encryption keys tooyour key vault, hello IaaS VM must be able tooconnect toohello key vault endpoint.</span></span>
  * <span data-ttu-id="3417e-305">Hello IaaS maszyny Wirtualnej musi być możliwe tooconnect tooan magazynu Azure punktu końcowego czy hosty hello repozytorium rozszerzenie Azure i konto magazynu Azure, że hosty hello pliki VHD.</span><span class="sxs-lookup"><span data-stu-id="3417e-305">hello IaaS VM must be able tooconnect tooan Azure storage endpoint that hosts hello Azure extension repository and an Azure storage account that hosts hello VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3417e-306">Jeśli zasady zabezpieczeń ogranicza dostęp z maszynami wirtualnymi Azure toohello Internet, można rozwiązać hello poprzedzających identyfikatora URI i skonfigurować określonej reguły toohello łączność wychodząca tooallow adresów IP.</span><span class="sxs-lookup"><span data-stu-id="3417e-306">If your security policy limits access from Azure VMs toohello Internet, you can resolve hello preceding URI and configure a specific rule tooallow outbound connectivity toohello IPs.</span></span>
  >
  ><span data-ttu-id="3417e-307">tooconfigure i dostępu do usługi Azure Key Vault za zaporą (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="3417e-307">tooconfigure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="3417e-308">Użyj hello najnowszą wersję zestawu SDK usługi Azure PowerShell w wersji tooconfigure szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-308">Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="3417e-309">Pobieranie hello najnowszej wersji [wersji programu Azure PowerShell](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="3417e-309">Download hello latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="3417e-310">Szyfrowanie dysków Azure nie jest obsługiwana w [zestawu SDK usługi Azure PowerShell w wersji 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="3417e-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="3417e-311">Jeśli wyświetlany błąd powiązane toousing programu Azure PowerShell 1.1.0, zobacz [tooAzure powiązane błąd szyfrowania dysków Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="3417e-311">If you are receiving an error related toousing Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="3417e-312">toorun dowolnego polecenia wiersza polecenia platformy Azure i powiązać ją z subskrypcją platformy Azure, należy najpierw zainstalować wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="3417e-312">toorun any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="3417e-313">tooinstall wiersza polecenia platformy Azure i powiązać ją z subskrypcją platformy Azure, zobacz [jak tooinstall i Konfigurowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3417e-313">tooinstall Azure CLI and associate it with your Azure subscription, see [How tooinstall and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="3417e-314">Zobacz toouse Azure CLI for Mac, Linux i Windows Azure Resource Manager [polecenia wiersza polecenia platformy Azure w trybie Menedżera zasobów](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="3417e-314">toouse Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="3417e-315">Podczas szyfrowania dysków zarządzanych, jest obowiązkowy tootake wymagań wstępnych migawkę hello zarządzane dysku lub z kopii zapasowej dysku hello poza szyfrowania przed tooenabling szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-315">When encrypting a managed disk, it is mandatory prerequisite tootake a snapshot of hello managed disk or a backup of hello disk outside of Azure Disk Encryption prior tooenabling encryption.</span></span>  <span data-ttu-id="3417e-316">Bez kopii zapasowej w miejscu wszelkie nieoczekiwany błąd podczas szyfrowania może spowodować hello dysku i wirtualna niedostępna bez opcji odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="3417e-316">Without a backup in place, any unexpected failure during encryption may render hello disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="3417e-317">Zestaw AzureRmVMDiskEncryptionExtension nie jest obecnie kopii dysków zarządzanych i będzie błąd, jeśli użyty przed dysków zarządzanych, chyba że został określony parametr - skipVmBackup hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless hello -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="3417e-318">Ten parametr jest niebezpieczne toouse, chyba że już wykonano kopię zapasową poza szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-318">This parameter is unsafe toouse unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="3417e-319">Jeśli określono parametr - skipVmBackup hello, hello polecenia cmdlet nie dokona kopii zapasowej tooencryption wcześniejsze dysku hello zarządzane.</span><span class="sxs-lookup"><span data-stu-id="3417e-319">When hello -skipVmBackup parameter is specified, hello cmdlet will not make a backup of hello managed disk prior tooencryption.</span></span>  <span data-ttu-id="3417e-320">Z tego powodu uważa się obowiązkowe toomake wymagań wstępnych się, że należy wykonywać kopii zapasowej dysku zarządzanego hello, maszyna wirtualna znajduje się w miejscu wcześniejsze tooenabling szyfrowania dysków Azure w przypadku odzyskiwania jest nowsza.</span><span class="sxs-lookup"><span data-stu-id="3417e-320">For this reason, it is considered a mandatory prerequisite toomake sure a backup of hello managed disk VM is in place prior tooenabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="3417e-321">Parametr - skipVmBackup Hello nigdy nie powinien być używany, chyba że migawka lub kopia zapasowa została już dokonana poza szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-321">hello -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="3417e-322">Hello rozwiązania szyfrowania dysków Azure używa zewnętrznego ochrony klucza funkcji BitLocker hello maszyn wirtualnych IaaS systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3417e-322">hello Azure Disk Encryption solution uses hello BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="3417e-323">Dla domeny dołączonego do maszyn wirtualnych, nie należy wypchnąć żadnych zasad grupy, które wymuszania funkcji ochrony Moduł TPM.</span><span class="sxs-lookup"><span data-stu-id="3417e-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="3417e-324">Aby uzyskać informacje o zasadach grupy hello "Zezwalaj na funkcję BitLocker bez zgodny moduł TPM", zobacz [dokumentacja zasad grupy funkcji BitLocker](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="3417e-324">For information about hello group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="3417e-325">Zasady funkcji BitLocker na maszynach wirtualnych przyłączony do domeny z zasad grupy niestandardowe musi zawierać hello następujące ustawienia: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` szyfrowania dysków Azure zakończy się niepowodzeniem, jeśli ustawienia zasad niestandardowych grup do używania funkcji Bitlocker są niezgodne.</span><span class="sxs-lookup"><span data-stu-id="3417e-325">Bitlocker policy on domain joined virtual machines with custom group policy must include hello following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="3417e-326">Na komputerach, które nie miał hello poprawne ustawienia zasad stosowania nowych zasad hello, wymuszanie hello nowych zasad tooupdate (gpupdate.exe/Force) i ponowne uruchomienie może być wymagane.</span><span class="sxs-lookup"><span data-stu-id="3417e-326">On machines that did not have hello correct policy setting, applying hello new policy, forcing hello new policy tooupdate (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="3417e-327">toocreate aplikację usługi Azure AD tworzenia magazynu kluczy, lub skonfigurować istniejący magazyn kluczy i włączenia szyfrowania, zobacz hello [skrypt programu PowerShell wymagań wstępnych szyfrowania dysków Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="3417e-327">toocreate an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see hello [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="3417e-328">wymagań wstępnych szyfrowania dysków tooconfigure przy użyciu hello wiersza polecenia platformy Azure, zobacz [ten skrypt Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="3417e-328">tooconfigure disk-encryption prerequisites using hello Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="3417e-329">toouse hello kopia zapasowa Azure usługa tooback zapasowej i przywracania szyfrowane maszyn wirtualnych, po włączeniu szyfrowania z szyfrowania dysków Azure, szyfrowania maszyn wirtualnych przy użyciu konfiguracji klucza szyfrowania dysków Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-329">toouse hello Azure Backup service tooback up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using hello Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="3417e-330">Hello usługi Backup obsługuje maszyny wirtualne, które są szyfrowane za pomocą tylko KEK konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3417e-330">hello Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="3417e-331">Zobacz [jak tooback zapasowej i przywracania szyfrowane maszyn wirtualnych przy użyciu szyfrowania usługi Kopia zapasowa Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="3417e-331">See [How tooback up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="3417e-332">Podczas szyfrowania woluminu systemu operacyjnego Linux, należy pamiętać, że ponowne uruchomienie maszyny Wirtualnej jest obecnie wymagane na końcu hello hello procesu.</span><span class="sxs-lookup"><span data-stu-id="3417e-332">When encrypting a Linux OS volume, note that a VM restart is currently required at hello end of hello process.</span></span> <span data-ttu-id="3417e-333">Można to zrobić za pomocą portalu hello, programu powershell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3417e-333">This can be done via hello portal, powershell, or CLI.</span></span>   <span data-ttu-id="3417e-334">postęp hello tootrack szyfrowania, okresowo sondować hello stanu komunikat zwrócony przez https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus Get AzureRmVMDiskEncryptionStatus.</span><span class="sxs-lookup"><span data-stu-id="3417e-334">tootrack hello progress of encryption, periodically poll hello status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="3417e-335">Po zakończeniu szyfrowania komunikatu o stanie hello hello zwróconych przez to polecenie będzie tę informację.</span><span class="sxs-lookup"><span data-stu-id="3417e-335">Once encryption is complete, hello hello status message returned by this command will indicate this.</span></span>  <span data-ttu-id="3417e-336">Na przykład "postępu: dysk systemu operacyjnego zostały pomyślnie zaszyfrowane, wykonaj ponowny rozruch hello maszyny Wirtualnej" w tym hello punktu maszyny Wirtualnej może być uruchomiona ponownie oraz używane.</span><span class="sxs-lookup"><span data-stu-id="3417e-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot hello VM"  At this point hello VM can be restarted and used.</span></span>  

* <span data-ttu-id="3417e-337">Azure szyfrowanie dysku dla systemu Linux wymaga toohave dysków danych zainstalowanego w systemie Linux tooencryption uprzedniego</span><span class="sxs-lookup"><span data-stu-id="3417e-337">Azure Disk Encryption for Linux requires data disks toohave a mounted file system in Linux prior tooencryption</span></span>

* <span data-ttu-id="3417e-338">Rekursywnie dysków zainstalowanych danych nie są obsługiwane przez hello szyfrowania dysków Azure dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="3417e-338">Recursively mounted data disks are not supported by hello Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="3417e-339">Na przykład jeśli hello system docelowy ma zainstalowany dysk na /foo/bar i następnie w /foo/bar/baz, szyfrowanie hello /foo/bar/baz powiedzie się, ale szyfrowania paska/foo/zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="3417e-339">For example, if hello target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, hello encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="3417e-340">Szyfrowanie dysków Azure jest obsługiwana tylko na obrazach obsługiwane galerii Azure, które spełniają wymagania wstępne wymienione wyżej hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet hello aforementioned prerequisites.</span></span> <span data-ttu-id="3417e-341">Niestandardowe obrazy klienta nie są obsługiwane schemat partycji toocustom i zachowania procesu, które mogą występować w tych obrazów.</span><span class="sxs-lookup"><span data-stu-id="3417e-341">Customer custom images are not supported due toocustom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="3417e-342">Co więcej, nawet galerii opartej na obrazie maszyny Wirtualnej, która początkowo spełnione wymagania wstępne zostały zmienione po utworzeniu mogą być niezgodne.</span><span class="sxs-lookup"><span data-stu-id="3417e-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="3417e-343">Dla czy powodu hello sugerowane procedury do szyfrowania maszyny Wirtualnej systemu Linux jest toostart z czystą galerii, szyfrowania hello maszyny Wirtualnej, a następnie dodaj niestandardowe oprogramowania lub toohello danych maszyny Wirtualnej, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="3417e-343">For that reason, hello suggested procedure for encrypting a Linux VM is toostart from a clean gallery image, encrypt hello VM, and then add custom software or data toohello VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="3417e-344">Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych jest obsługiwana tylko dla maszyn wirtualnych, które są szyfrowane przy hello KEK konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3417e-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="3417e-345">Nie jest obsługiwana na maszynach wirtualnych, które są szyfrowane bez KEK.</span><span class="sxs-lookup"><span data-stu-id="3417e-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="3417e-346">KEK jest opcjonalnym parametrem, który umożliwia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="3417e-347">Konfigurowanie hello aplikacji usługi Azure AD w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3417e-347">Set up hello Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="3417e-348">Jeśli potrzebujesz toobe szyfrowania włączone w przypadku uruchomionej maszyny Wirtualnej na platformie Azure szyfrowania dysków Azure generuje i zapisuje magazynu kluczy tooyour hello szyfrowania kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-348">When you need encryption toobe enabled on a running VM in Azure, Azure Disk Encryption generates and writes hello encryption keys tooyour key vault.</span></span> <span data-ttu-id="3417e-349">Zarządzanie kluczy szyfrowania w magazynie kluczy, wymaga uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3417e-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="3417e-350">W tym celu należy utworzyć aplikację usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3417e-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="3417e-351">Szczegółowy opis kroków można znaleźć rejestrowania aplikacji hello "Get tożsamości dla aplikacji hello" część hello wpis w blogu [usługi Azure Key Vault - krok po kroku](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="3417e-351">You can find detailed steps for registering an application in hello “Get an Identity for hello Application” section of hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="3417e-352">Ten wpis zawiera również liczbę przykłady przydatne do instalowania i konfigurowania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="3417e-353">Na potrzeby uwierzytelniania można użyć uwierzytelniania opartego na klucz tajny klienta i uwierzytelnianie klienta oparte na certyfikatach usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3417e-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="3417e-354">Uwierzytelnianie oparte na protokole klucz tajny klienta dla usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3417e-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="3417e-355">kolejnych sekcjach Hello pomoże Ci skonfigurować uwierzytelnianie oparte na klucz tajny klienta dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3417e-355">hello sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="3417e-356">Tworzenie aplikacji usługi Azure AD przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3417e-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="3417e-357">Użyj następującego toocreate polecenia cmdlet programu PowerShell usługi Azure AD aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-357">Use hello following PowerShell cmdlet toocreate an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="3417e-358">$azureAdApplication.ApplicationId jest hello Azure AD ClientID i $aadClientSecret jest klucz tajny klienta hello korzystała nowsze tooenable szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-358">$azureAdApplication.ApplicationId is hello Azure AD ClientID and $aadClientSecret is hello client secret that you should use later tooenable Azure Disk Encryption.</span></span> <span data-ttu-id="3417e-359">Chroń klucz tajny klienta usługi Azure AD hello odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="3417e-359">Safeguard hello Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a><span data-ttu-id="3417e-360">Konfigurowanie hello Azure AD identyfikator klienta i klucz tajny z hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3417e-360">Setting up hello Azure AD client ID and secret from hello Azure classic portal</span></span>
<span data-ttu-id="3417e-361">Można również ustawić zapasowej identyfikator klienta usługi Azure AD i klucz tajny przy użyciu hello [klasycznego portalu Azure]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3417e-361">You can also set up your Azure AD client ID and secret by using hello [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="3417e-362">tooperform to zadanie, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3417e-362">tooperform this task, do hello following:</span></span>

1. <span data-ttu-id="3417e-363">Kliknij przycisk hello **usługi Active Directory** kartę.</span><span class="sxs-lookup"><span data-stu-id="3417e-363">Click hello **Active Directory** tab.</span></span>

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="3417e-365">Kliknij przycisk **Dodawanie aplikacji**, a następnie wpisz nazwę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-365">Click **Add Application**, and then type hello application name.</span></span>

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="3417e-367">Kliknij przycisk strzałki hello, a następnie skonfigurować właściwości aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-367">Click hello arrow button, and then configure hello application properties.</span></span>

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="3417e-369">Kliknij znacznik wyboru hello w dolnym toofinish lewym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-369">Click hello check mark in hello lower left corner toofinish.</span></span> <span data-ttu-id="3417e-370">zostanie wyświetlona strona konfiguracji aplikacji Hello, a identyfikator klienta usługi Azure AD hello są wyświetlane u dołu hello strony hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-370">hello application configuration page appears, and hello Azure AD client ID is displayed at hello bottom of hello page.</span></span>

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="3417e-372">Zapisz klucz tajny klienta hello Azure AD, klikając hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3417e-372">Save hello Azure AD client secret by clicking hello **Save** button.</span></span> <span data-ttu-id="3417e-373">Należy pamiętać, klucz tajny klienta hello Azure AD w polu tekstowym hello kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-373">Note hello Azure AD client secret in hello keys text box.</span></span> <span data-ttu-id="3417e-374">Chroń odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="3417e-374">Safeguard it appropriately.</span></span>

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="3417e-376">Witaj poprzedzających przepływu nie jest obsługiwana na powitania klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-376">hello preceding flow is not supported on hello Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="3417e-377">Użyj istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="3417e-377">Use an existing application</span></span>
<span data-ttu-id="3417e-378">tooexecute hello następujące polecenia, uzyskiwał i wykorzystywał hello [modułu Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="3417e-378">tooexecute hello following commands, obtain and use hello [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-379">Witaj następujące polecenia musi zostać wykonana z nowe okno programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3417e-379">hello following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="3417e-380">Nie należy używać programu Azure PowerShell lub hello Azure Resource Manager okna tooexecute hello poleceń.</span><span class="sxs-lookup"><span data-stu-id="3417e-380">Do not use Azure PowerShell or hello Azure Resource Manager window tooexecute hello commands.</span></span> <span data-ttu-id="3417e-381">Zalecamy takie podejście, ponieważ te polecenia cmdlet w hello MSOnline module lub Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3417e-381">We recommend this approach because these cmdlets are in hello MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="3417e-382">Uwierzytelnianie oparte na certyfikatach dla usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3417e-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="3417e-383">Uwierzytelnianie oparte na certyfikatach AD Azure aktualnie nie jest obsługiwane na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="3417e-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="3417e-384">Witaj następnych sekcjach Pokaż jak tooconfigure uwierzytelniania opartego na certyfikatach dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3417e-384">hello sections that follow show how tooconfigure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="3417e-385">Tworzenie aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3417e-385">Create an Azure AD application</span></span>
<span data-ttu-id="3417e-386">toocreate aplikacji usługi Azure AD, wykonaj hello następującego polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3417e-386">toocreate an Azure AD application, execute hello following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-387">Zastąp następujące hello `yourpassword` ciąg bezpieczne hasło, a hasło hello zabezpieczenia.</span><span class="sxs-lookup"><span data-stu-id="3417e-387">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="3417e-388">Po zakończeniu tego kroku przekazać magazyn kluczy tooyour pliku PFX i włączyć hello dostępu zasad wymaganych toodeploy tooa tego certyfikatu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-388">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy needed toodeploy that certificate tooa VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="3417e-389">Użyj istniejącej aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3417e-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="3417e-390">W przypadku konfigurowania uwierzytelniania opartego na certyfikatach dla istniejącej aplikacji, użyj poleceń cmdlet programu PowerShell hello pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="3417e-390">If you are configuring certificate-based authentication for an existing application, use hello PowerShell cmdlets shown here.</span></span> <span data-ttu-id="3417e-391">Tooexecute się, że można je z nowe okno programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3417e-391">Be sure tooexecute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="3417e-392">Po zakończeniu tego kroku przekazać magazyn kluczy tooyour pliku PFX, aby włączyć zasady dostępu hello potrzebne toodeploy hello certyfikatu tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-392">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy that's needed toodeploy hello certificate tooa VM.</span></span>

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a><span data-ttu-id="3417e-393">Przekaż magazyn kluczy tooyour pliku PFX</span><span class="sxs-lookup"><span data-stu-id="3417e-393">Upload a PFX file tooyour key vault</span></span>
<span data-ttu-id="3417e-394">Aby uzyskać szczegółowy opis tego procesu, zobacz [hello oficjalny Blog zespołu usługi Azure Key Vault](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="3417e-394">For a detailed explanation of this process, see [hello Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="3417e-395">Jednak hello następującego polecenia cmdlet programu PowerShell są potrzebne dla hello zadania.</span><span class="sxs-lookup"><span data-stu-id="3417e-395">However, hello following PowerShell cmdlets are all you need for hello task.</span></span> <span data-ttu-id="3417e-396">Tooexecute się, że można je z konsoli programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3417e-396">Be sure tooexecute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-397">Zastąp następujące hello `yourpassword` ciąg bezpieczne hasło, a hasło hello zabezpieczenia.</span><span class="sxs-lookup"><span data-stu-id="3417e-397">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

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

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a><span data-ttu-id="3417e-398">Wdróż certyfikat w tooan Twojego magazynu kluczy, istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3417e-398">Deploy a certificate in your key vault tooan existing VM</span></span>
<span data-ttu-id="3417e-399">Po zakończeniu przekazywania hello PFX, Wdróż certyfikat w istniejącej maszyny Wirtualnej z następujących hello tooan magazynu kluczy hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-399">After you finish uploading hello PFX, deploy a certificate in hello key vault tooan existing VM with hello following:</span></span>
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

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a><span data-ttu-id="3417e-400">Skonfigurować zasady dostępu magazynu kluczy hello aplikacji hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3417e-400">Set up hello key vault access policy for hello Azure AD application</span></span>
<span data-ttu-id="3417e-401">Aplikacja Azure AD wymaga praw tooaccess hello kluczy ani kluczy tajnych w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-401">Your Azure AD application needs rights tooaccess hello keys or secrets in hello vault.</span></span> <span data-ttu-id="3417e-402">Użyj hello [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) polecenia cmdlet toogrant uprawnienia toohello aplikacji przy użyciu Identyfikatora klienta hello (który został wygenerowany, gdy aplikacja hello została zarejestrowana) jako hello _— ServicePrincipalName_ wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="3417e-402">Use hello [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissions toohello application, using hello client ID (which was generated when hello application was registered) as hello _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="3417e-403">toolearn więcej, zobacz hello blogu [usługi Azure Key Vault - krok po kroku](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="3417e-403">toolearn more, see hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="3417e-404">Poniżej przedstawiono przykład sposobu tooperform to zadanie za pomocą programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3417e-404">Here is an example of how tooperform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="3417e-405">Szyfrowanie dysków Azure wymaga hello tooconfigure po aplikacji klienckiej tooyour usługi Azure AD zasad dostępu: _WrapKey_ i _ustawić_ uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="3417e-405">Azure Disk Encryption requires you tooconfigure hello following access policies tooyour Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="3417e-406">Terminologia</span><span class="sxs-lookup"><span data-stu-id="3417e-406">Terminology</span></span>
<span data-ttu-id="3417e-407">niektóre typowe terminy hello jest używany przez tę technologię, użyj hello w poniższej tabeli terminologii toounderstand:</span><span class="sxs-lookup"><span data-stu-id="3417e-407">toounderstand some of hello common terms used by this technology, use hello following terminology table:</span></span>

| <span data-ttu-id="3417e-408">Terminologia</span><span class="sxs-lookup"><span data-stu-id="3417e-408">Terminology</span></span> | <span data-ttu-id="3417e-409">Definicja</span><span class="sxs-lookup"><span data-stu-id="3417e-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="3417e-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="3417e-410">Azure AD</span></span> | <span data-ttu-id="3417e-411">Usługa Azure AD [usługi Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="3417e-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="3417e-412">Konto usługi Azure AD jest wymagane do uwierzytelniania, przechowywania i pobierania kluczy tajnych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="3417e-413">W usłudze Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="3417e-413">Azure Key Vault</span></span> | <span data-ttu-id="3417e-414">Key Vault jest usługą zarządzania kryptograficznych, klucza opartego na zweryfikowane FIPS Federal Information Processing standardów sprzętowych modułów zabezpieczeń, które pomagają w ochronie z kluczy kryptograficznych i kluczy tajnych poufnych.</span><span class="sxs-lookup"><span data-stu-id="3417e-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="3417e-415">Aby uzyskać więcej informacji, zobacz [Key Vault](https://azure.microsoft.com/services/key-vault/) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="3417e-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="3417e-416">ARM</span><span class="sxs-lookup"><span data-stu-id="3417e-416">ARM</span></span> | <span data-ttu-id="3417e-417">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3417e-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="3417e-418">Funkcja BitLocker</span><span class="sxs-lookup"><span data-stu-id="3417e-418">BitLocker</span></span> |<span data-ttu-id="3417e-419">[Funkcja BitLocker](https://technet.microsoft.com/library/hh831713.aspx) jest branży Windows woluminu szyfrowania technologia, która została użyta tooenable szyfrowania dysków na maszynach wirtualnych IaaS systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3417e-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used tooenable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="3417e-420">KSB</span><span class="sxs-lookup"><span data-stu-id="3417e-420">BEK</span></span> | <span data-ttu-id="3417e-421">Klucze szyfrowania funkcji BitLocker są woluminu rozruchowego używanego tooencrypt hello systemu operacyjnego i woluminów danych.</span><span class="sxs-lookup"><span data-stu-id="3417e-421">BitLocker encryption keys are used tooencrypt hello OS boot volume and data volumes.</span></span> <span data-ttu-id="3417e-422">klucze funkcji BitLocker Hello są chronione w magazynie kluczy jako kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="3417e-422">hello BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="3417e-423">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="3417e-423">CLI</span></span> | <span data-ttu-id="3417e-424">Zobacz [interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3417e-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="3417e-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="3417e-425">DM-Crypt</span></span> |<span data-ttu-id="3417e-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) hello podsystem opartych na systemie Linux lub przezroczystego szyfrowania dysku, który został użyty tooenable szyfrowania dysków na maszyn wirtualnych systemu Linux IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is hello Linux-based, transparent disk-encryption subsystem that's used tooenable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="3417e-427">KEK</span><span class="sxs-lookup"><span data-stu-id="3417e-427">KEK</span></span> | <span data-ttu-id="3417e-428">Klucz szyfrowania jest hello klucza asymetrycznego (RSA 2048) można używać tooprotect lub zawijać hello klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="3417e-428">Key encryption key is hello asymmetric key (RSA 2048) that you can use tooprotect or wrap hello secret.</span></span> <span data-ttu-id="3417e-429">Możesz podać zabezpieczeń sprzętowych modułów (HSM)-chronione klucza lub klucza chronionego przez oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="3417e-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="3417e-430">Aby uzyskać więcej informacji, zobacz [usługi Azure Key Vault](https://azure.microsoft.com/services/key-vault/) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="3417e-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="3417e-431">PS polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3417e-431">PS cmdlets</span></span> | <span data-ttu-id="3417e-432">Zobacz [poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3417e-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="3417e-433">Instalowanie i Konfigurowanie magazynu kluczy do szyfrowania dysków Azure</span><span class="sxs-lookup"><span data-stu-id="3417e-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="3417e-434">Szyfrowanie dysków Azure ułatwia zabezpieczenie hello szyfrowanie dysków kluczy i kluczy tajnych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-434">Azure Disk Encryption helps safeguard hello disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="3417e-435">tooset się magazynu kluczy do szyfrowania dysków Azure, pełną hello kroki w każdym hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="3417e-435">tooset up your key vault for Azure Disk Encryption, complete hello steps in each of hello following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="3417e-436">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="3417e-436">Create a key vault</span></span>
<span data-ttu-id="3417e-437">toocreate magazyn kluczy, użyj jednej z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="3417e-437">toocreate a key vault, use one of hello following options:</span></span>

* [<span data-ttu-id="3417e-438">"101-klucza-magazynu-Create" Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3417e-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="3417e-439">Polecenia cmdlet magazynu kluczy Azure programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3417e-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="3417e-440">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3417e-440">Azure Resource Manager</span></span>
* <span data-ttu-id="3417e-441">Jak zbyt[bezpiecznego magazynu kluczy](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="3417e-441">How too[Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-442">Jeśli magazyn kluczy zostały już skonfigurowane dla Twojej subskrypcji, Pomiń toohello następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="3417e-442">If you have already set up a key vault for your subscription, skip toohello next section.</span></span>

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="3417e-444">Konfigurowanie klucza szyfrowania (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="3417e-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="3417e-445">Toouse KEK dla dodatkową warstwę zabezpieczeń dla kluczy szyfrowania hello funkcji BitLocker, należy dodać magazyn kluczy KEK tooyour.</span><span class="sxs-lookup"><span data-stu-id="3417e-445">If you want toouse a KEK for an additional layer of security for hello BitLocker encryption keys, add a KEK tooyour key vault.</span></span> <span data-ttu-id="3417e-446">Użyj hello [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate polecenia cmdlet klucz szyfrowania kluczy w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-446">Use hello [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate a key encryption key in hello key vault.</span></span> <span data-ttu-id="3417e-447">Można także zaimportować KEK z lokalnymi Zarządzanie klucza HSM.</span><span class="sxs-lookup"><span data-stu-id="3417e-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="3417e-448">Aby uzyskać więcej informacji, zobacz [klucza magazynu dokumentacji](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="3417e-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="3417e-449">Możesz dodać hello KEK przechodząc tooAzure Resource Manager lub przy użyciu interfejsu magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-449">You can add hello KEK by going tooAzure Resource Manager or by using your key vault interface.</span></span>

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="3417e-451">Ustaw uprawnienia magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="3417e-451">Set key vault permissions</span></span>
<span data-ttu-id="3417e-452">Hello platformy Azure wymaga dostępu toohello szyfrowania kluczy lub kluczy tajnych w toomake Twojego magazynu kluczy ich toohello dostępne maszyny Wirtualnej do rozruchu i odszyfrowywania hello woluminów.</span><span class="sxs-lookup"><span data-stu-id="3417e-452">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello VM for booting and decrypting hello volumes.</span></span> <span data-ttu-id="3417e-453">toogrant uprawnienia toohello platformy Azure, zestawu hello **EnabledForDiskEncryption** właściwości w kluczu hello magazynu za pomocą polecenia cmdlet programu PowerShell magazynu kluczy hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-453">toogrant permissions toohello Azure platform, set hello **EnabledForDiskEncryption** property in hello key vault by using hello key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="3417e-454">Można również ustawić hello **EnabledForDiskEncryption** właściwości, przechodząc na stronę hello [Eksploratora zasobów Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3417e-454">You can also set hello **EnabledForDiskEncryption** property by visiting hello [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="3417e-455">Jak wspomniano wcześniej, musisz ustawić hello **EnabledForDiskEncryption** właściwości magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-455">As mentioned earlier, you must set hello **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="3417e-456">W przeciwnym razie hello wdrożenie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="3417e-456">Otherwise, hello deployment will fail.</span></span>

<span data-ttu-id="3417e-457">Jak pokazano poniżej, można skonfigurować zasady dostępu dla aplikacji usługi Azure AD z hello magazynu kluczy interfejsu:</span><span class="sxs-lookup"><span data-stu-id="3417e-457">You can set up access policies for your Azure AD application from hello key vault interface, as shown here:</span></span>

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="3417e-460">Na powitania **zasady dostępu zaawansowane** i upewnij się, że magazynu kluczy jest włączona obsługa szyfrowania dysków Azure:</span><span class="sxs-lookup"><span data-stu-id="3417e-460">On hello **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Usługi Azure key vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="3417e-462">Scenariusze wdrażania szyfrowanie dysków oraz możliwości użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3417e-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="3417e-463">Aby umożliwić wiele scenariuszy szyfrowania dysków i hello kroki mogą się różnić zgodnie z toohello scenariusza.</span><span class="sxs-lookup"><span data-stu-id="3417e-463">You can enable many disk-encryption scenarios, and hello steps may vary according toohello scenario.</span></span> <span data-ttu-id="3417e-464">Witaj poniższych częściach omówiono scenariusze hello większej liczby szczegółów.</span><span class="sxs-lookup"><span data-stu-id="3417e-464">hello following sections cover hello scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a><span data-ttu-id="3417e-465">Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS, które są tworzone na podstawie hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="3417e-465">Enable encryption on new IaaS VMs that are created from hello Marketplace</span></span>
<span data-ttu-id="3417e-466">Można włączyć szyfrowanie dysków na nowej maszyny Wirtualnej systemu Windows IaaS z hello Marketplace na platformie Azure przy użyciu hello [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="3417e-466">You can enable disk encryption on new IaaS Windows VM from hello Marketplace in Azure by using hello  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="3417e-467">W szablonie hello Azure szybki start kliknij **wdrażanie tooAzure**, wprowadź konfiguracji szyfrowania hello na powitania **parametry** bloku, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3417e-467">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="3417e-468">Wybierz hello subskrypcji, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** tooenable szyfrowania na nowej maszyny Wirtualnej IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-468">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-469">Ten szablon umożliwia tworzenie nowych zaszyfrowanych Windows maszynę Wirtualną, która używa obrazu galerii hello systemu Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="3417e-469">This template creates a new encrypted Windows VM that uses hello Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="3417e-470">Można włączyć szyfrowanie dysków na nowe IaaS RedHat Linux 7.2 maszynę Wirtualną za pomocą macierzy RAID-0 200 GB, za pomocą tego [szablonu usługi Resource Manager](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="3417e-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="3417e-471">Po wdrożeniu szablonu hello sprawdzić stanu szyfrowania hello maszyny Wirtualnej za pomocą hello `Get-AzureRmVmDiskEncryptionStatus` polecenia cmdlet, zgodnie z opisem w [OS szyfrowania dysków na uruchomionej maszyny Wirtualnej systemu Linux](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="3417e-471">After you deploy hello template, verify hello VM encryption status by using hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="3417e-472">Gdy maszyna hello zwraca stan _VMRestartPending_, uruchom ponownie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-472">When hello machine returns a status of _VMRestartPending_, restart hello VM.</span></span>

<span data-ttu-id="3417e-473">Witaj Poniższa tabela zawiera listę parametrów szablonu usługi Resource Manager hello nowych maszyn wirtualnych z scenariusz Marketplace hello przy użyciu Identyfikatora klienta usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="3417e-473">hello following table lists hello Resource Manager template parameters for new VMs from hello Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="3417e-474">Parametr</span><span class="sxs-lookup"><span data-stu-id="3417e-474">Parameter</span></span> | <span data-ttu-id="3417e-475">Opis</span><span class="sxs-lookup"><span data-stu-id="3417e-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3417e-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="3417e-476">adminUserName</span></span> | <span data-ttu-id="3417e-477">Nazwa użytkownika administratora hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-477">Admin user name for hello virtual machine.</span></span> |
| <span data-ttu-id="3417e-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="3417e-478">adminPassword</span></span> | <span data-ttu-id="3417e-479">Hasło użytkownika administratora hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-479">Admin user password for hello virtual machine.</span></span> |
| <span data-ttu-id="3417e-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="3417e-480">newStorageAccountName</span></span> | <span data-ttu-id="3417e-481">Nazwa toostore konta magazynu hello systemu operacyjnego i danych wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="3417e-481">Name of hello storage account toostore OS and data VHDs.</span></span> |
| <span data-ttu-id="3417e-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="3417e-482">vmSize</span></span> | <span data-ttu-id="3417e-483">Rozmiar hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-483">Size of hello VM.</span></span> <span data-ttu-id="3417e-484">Obecnie obsługiwane są tylko standardowe A, D i G serii.</span><span class="sxs-lookup"><span data-stu-id="3417e-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="3417e-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="3417e-485">virtualNetworkName</span></span> | <span data-ttu-id="3417e-486">Nazwa hello sieć wirtualna tego hello wirtualna karta sieciowa powinna należeć do.</span><span class="sxs-lookup"><span data-stu-id="3417e-486">Name of hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="3417e-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="3417e-487">subnetName</span></span> | <span data-ttu-id="3417e-488">Nazwa podsieci hello hello sieć wirtualna tego hello wirtualna karta sieciowa powinna należeć do.</span><span class="sxs-lookup"><span data-stu-id="3417e-488">Name of hello subnet in hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="3417e-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="3417e-489">AADClientID</span></span> | <span data-ttu-id="3417e-490">Identyfikator klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych tooyour klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="3417e-490">Client ID of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="3417e-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="3417e-491">AADClientSecret</span></span> | <span data-ttu-id="3417e-492">Klucz tajny klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych tooyour klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="3417e-492">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="3417e-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="3417e-493">keyVaultURL</span></span> | <span data-ttu-id="3417e-494">Adres URL hello klucza magazynu tego hello klucz należy przekazać do funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="3417e-494">URL of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="3417e-495">Możesz pobrać go za pomocą polecenia cmdlet hello `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="3417e-495">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="3417e-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="3417e-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="3417e-497">Adres URL hello klucza szyfrowania klucza, który jest używany tooencrypt hello generowane klucza funkcji BitLocker (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="3417e-497">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="3417e-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3417e-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="3417e-499">Grupa zasobów hello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-499">Resource group of hello key vault.</span></span> |
| <span data-ttu-id="3417e-500">vmName</span><span class="sxs-lookup"><span data-stu-id="3417e-500">vmName</span></span> | <span data-ttu-id="3417e-501">Nazwa hello maszynę Wirtualną, która hello operacji szyfrowania jest wykonywane na toobe.</span><span class="sxs-lookup"><span data-stu-id="3417e-501">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="3417e-502">_KeyEncryptionKeyURL_ jest parametrem opcjonalnym.</span><span class="sxs-lookup"><span data-stu-id="3417e-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="3417e-503">Możesz objąć własne KEK toofurther zabezpieczenie hello klucza szyfrowania danych (klucz tajny hasło) w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-503">You can bring your own KEK toofurther safeguard hello data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="3417e-504">Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS, które są tworzone na podstawie klienta systemu szyfrowania plików VHD i kluczy szyfrowania</span><span class="sxs-lookup"><span data-stu-id="3417e-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="3417e-505">W tym scenariuszu można włączyć szyfrowanie przy użyciu szablonu usługi Resource Manager hello, poleceń cmdlet programu PowerShell lub polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3417e-505">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="3417e-506">Witaj poniższe sekcje zawierają opis większa szablonu usługi Resource Manager hello szczegóły i polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3417e-506">hello following sections explain in greater detail hello Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="3417e-507">Wykonaj instrukcje hello z jednego z tych sekcji przygotowania zaszyfrowane wstępnie obrazy, których można użyć w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-507">Follow hello instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="3417e-508">Po utworzeniu obrazu hello hello kroki służą w hello następnej sekcji toocreate zaszyfrowanych maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-508">After hello image is created, you can use hello steps in hello next section toocreate an encrypted Azure VM.</span></span>

* [<span data-ttu-id="3417e-509">Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3417e-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="3417e-510">Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Linux</span><span class="sxs-lookup"><span data-stu-id="3417e-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="3417e-511">Przy użyciu szablonu usługi Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="3417e-511">Using hello Resource Manager template</span></span>
<span data-ttu-id="3417e-512">Można włączyć szyfrowanie dysków na zaszyfrowany dysk VHD za pomocą hello [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="3417e-512">You can enable disk encryption on your encrypted VHD by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="3417e-513">W szablonie hello Azure szybki start kliknij **wdrażanie tooAzure**, wprowadź konfiguracji szyfrowania hello na powitania **parametry** bloku, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3417e-513">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="3417e-514">Wybierz hello subskrypcji, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** tooenable szyfrowania na hello nowej maszyny Wirtualnej IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-514">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello new IaaS VM.</span></span>

<span data-ttu-id="3417e-515">Witaj Poniższa tabela zawiera listę parametrów szablonu usługi Resource Manager hello zaszyfrowany dysk VHD:</span><span class="sxs-lookup"><span data-stu-id="3417e-515">hello following table lists hello Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="3417e-516">Parametr</span><span class="sxs-lookup"><span data-stu-id="3417e-516">Parameter</span></span> | <span data-ttu-id="3417e-517">Opis</span><span class="sxs-lookup"><span data-stu-id="3417e-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3417e-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="3417e-518">newStorageAccountName</span></span> | <span data-ttu-id="3417e-519">Nazwa hello toostore konta magazynu hello szyfrowane wirtualnego dysku twardego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3417e-519">Name of hello storage account toostore hello encrypted OS VHD.</span></span> <span data-ttu-id="3417e-520">To konto magazynu należy już zostały utworzone w hello same grupy zasobów i tej samej lokalizacji co hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-520">This storage account should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="3417e-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="3417e-521">osVhdUri</span></span> | <span data-ttu-id="3417e-522">Identyfikator URI hello wirtualnego dysku twardego systemu operacyjnego z hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3417e-522">URI of hello OS VHD from hello storage account.</span></span> |
| <span data-ttu-id="3417e-523">osType</span><span class="sxs-lookup"><span data-stu-id="3417e-523">osType</span></span> | <span data-ttu-id="3417e-524">Typ produktu systemu operacyjnego (Windows/Linux).</span><span class="sxs-lookup"><span data-stu-id="3417e-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="3417e-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="3417e-525">virtualNetworkName</span></span> | <span data-ttu-id="3417e-526">Nazwa hello sieć wirtualna tego hello wirtualna karta sieciowa powinna należeć do.</span><span class="sxs-lookup"><span data-stu-id="3417e-526">Name of hello VNet that hello VM NIC should belong to.</span></span> <span data-ttu-id="3417e-527">Witaj nazwa powinna już zostały utworzone w hello takie same grupy zasobów i tej samej lokalizacji co hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-527">hello name should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="3417e-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="3417e-528">subnetName</span></span> | <span data-ttu-id="3417e-529">Nazwa podsieci hello na powitania sieć wirtualna tego hello wirtualna karta sieciowa powinna należeć do.</span><span class="sxs-lookup"><span data-stu-id="3417e-529">Name of hello subnet on hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="3417e-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="3417e-530">vmSize</span></span> | <span data-ttu-id="3417e-531">Rozmiar hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-531">Size of hello VM.</span></span> <span data-ttu-id="3417e-532">Obecnie obsługiwane są tylko standardowe A, D i G serii.</span><span class="sxs-lookup"><span data-stu-id="3417e-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="3417e-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="3417e-533">keyVaultResourceID</span></span> | <span data-ttu-id="3417e-534">Witaj ResourceID, który identyfikuje hello zasobu magazynu kluczy Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3417e-534">hello ResourceID that identifies hello key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="3417e-535">Możesz pobrać go za pomocą polecenia cmdlet programu PowerShell hello `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="3417e-535">You can get it by using hello PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="3417e-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="3417e-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="3417e-537">Adres URL klucza szyfrowania dysków hello, który został skonfigurowany w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-537">URL of hello disk-encryption key that's set up in hello key vault.</span></span> |
| <span data-ttu-id="3417e-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="3417e-538">keyVaultKekUrl</span></span> | <span data-ttu-id="3417e-539">Adres URL hello klucza szyfrowania klucza szyfrowania hello wygenerowany klucz szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="3417e-539">URL of hello key encryption key for encrypting hello generated disk-encryption key.</span></span> |
| <span data-ttu-id="3417e-540">vmName</span><span class="sxs-lookup"><span data-stu-id="3417e-540">vmName</span></span> | <span data-ttu-id="3417e-541">Nazwa hello maszyn wirtualnych IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-541">Name of hello IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="3417e-542">Za pomocą poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3417e-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="3417e-543">Można włączyć szyfrowanie dysków na zaszyfrowany dysk VHD za pomocą polecenia cmdlet programu PowerShell hello [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="3417e-543">You can enable disk encryption on your encrypted VHD by using hello PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="3417e-544">Za pomocą polecenia interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="3417e-544">Using CLI commands</span></span>
<span data-ttu-id="3417e-545">Szyfrowanie dysków tooenable dla tego scenariusza za pomocą polecenia interfejsu wiersza polecenia hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3417e-545">tooenable disk encryption for this scenario by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="3417e-546">Ustawianie zasad dostępu w magazynie kluczy:</span><span class="sxs-lookup"><span data-stu-id="3417e-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="3417e-547">Zestaw hello **EnabledForDiskEncryption** flagi:</span><span class="sxs-lookup"><span data-stu-id="3417e-547">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="3417e-548">Ustaw uprawnienia tooAzure AD aplikacji toowrite kluczy tajnych tooyour magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="3417e-548">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="3417e-549">tooenable szyfrowania w przypadku istniejących lub uruchomionej maszyny Wirtualnej, typ:</span><span class="sxs-lookup"><span data-stu-id="3417e-549">tooenable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="3417e-550">Pobierz stan szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="3417e-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="3417e-551">szyfrowanie tooenable na nowej maszyny Wirtualnej z zaszyfrowany dysk VHD, użyj hello następujące parametry hello `azure vm create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="3417e-551">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="3417e-552">Włącz szyfrowanie dla istniejących lub uruchomione maszyny Wirtualnej systemu Windows IaaS na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3417e-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="3417e-553">W tym scenariuszu można włączyć szyfrowanie przy użyciu szablonu usługi Resource Manager hello, poleceń cmdlet programu PowerShell lub polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3417e-553">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="3417e-554">Witaj poniższych sekcjach opisano szczegółowo sposób tooenable hello go przy użyciu szablonu usługi Resource Manager i polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3417e-554">hello following sections explain in greater detail how tooenable it by using hello Resource Manager template and CLI commands.</span></span>

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="3417e-555">Przy użyciu szablonu usługi Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="3417e-555">Using hello Resource Manager template</span></span>
<span data-ttu-id="3417e-556">Można włączyć szyfrowanie dysku na istniejących lub uruchomione maszyny wirtualne IaaS systemu Windows na platformie Azure przy użyciu hello [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="3417e-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="3417e-557">W szablonie hello Azure szybki start kliknij **wdrażanie tooAzure**, wprowadź konfiguracji szyfrowania hello na powitania **parametry** bloku, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3417e-557">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="3417e-558">Wybierz hello subskrypcji, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** tooenable szyfrowania na powitania istniejące lub uruchamiania maszyn wirtualnych IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-558">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="3417e-559">Witaj Poniższa tabela zawiera listę parametrów szablonu usługi Resource Manager hello istniejących lub działających maszyn wirtualnych, które mają identyfikator klienta usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="3417e-559">hello following table lists hello Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="3417e-560">Parametr</span><span class="sxs-lookup"><span data-stu-id="3417e-560">Parameter</span></span> | <span data-ttu-id="3417e-561">Opis</span><span class="sxs-lookup"><span data-stu-id="3417e-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3417e-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="3417e-562">AADClientID</span></span> | <span data-ttu-id="3417e-563">Identyfikator klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych toohello klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="3417e-563">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="3417e-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="3417e-564">AADClientSecret</span></span> | <span data-ttu-id="3417e-565">Klucz tajny klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych toohello klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="3417e-565">Client secret of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="3417e-566">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3417e-566">keyVaultName</span></span> | <span data-ttu-id="3417e-567">Nazwa klucza hello magazynu tego hello klucz należy przekazać do funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="3417e-567">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="3417e-568">Możesz pobrać go za pomocą polecenia cmdlet hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="3417e-568">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="3417e-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="3417e-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="3417e-570">Adres URL hello klucza szyfrowania klucza, który jest używany tooencrypt hello generowane klucza funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="3417e-570">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="3417e-571">Ten parametr jest opcjonalny w przypadku wybrania **nokek** na liście rozwijanej UseExistingKek hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-571">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="3417e-572">W przypadku wybrania **kek** na liście rozwijanej UseExistingKek hello, musisz wprowadzić hello _keyEncryptionKeyURL_ wartości.</span><span class="sxs-lookup"><span data-stu-id="3417e-572">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="3417e-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="3417e-573">volumeType</span></span> | <span data-ttu-id="3417e-574">Typ operacji szyfrowania hello jest wykonywana na wolumin.</span><span class="sxs-lookup"><span data-stu-id="3417e-574">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="3417e-575">Prawidłowe wartości to _OS_, _danych_, i _wszystkich_.</span><span class="sxs-lookup"><span data-stu-id="3417e-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="3417e-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="3417e-576">sequenceVersion</span></span> | <span data-ttu-id="3417e-577">Wersja sekwencji hello działania funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="3417e-577">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="3417e-578">Zwiększ numer wersji, za każdym razem, gdy operacji szyfrowania dysków odbywa się na powitania tej samej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-578">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="3417e-579">vmName</span><span class="sxs-lookup"><span data-stu-id="3417e-579">vmName</span></span> | <span data-ttu-id="3417e-580">Nazwa hello maszynę Wirtualną, która hello operacji szyfrowania jest wykonywane na toobe.</span><span class="sxs-lookup"><span data-stu-id="3417e-580">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="3417e-581">_KeyEncryptionKeyURL_ jest parametrem opcjonalnym.</span><span class="sxs-lookup"><span data-stu-id="3417e-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="3417e-582">W magazynie kluczy hello przełączeniem własne KEK toofurther zabezpieczenie hello klucza szyfrowania danych (funkcji BitLocker Szyfrowanie klucz tajny).</span><span class="sxs-lookup"><span data-stu-id="3417e-582">You can bring your own KEK toofurther safeguard hello data encryption key (BitLocker encryption secret) in hello key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="3417e-583">Za pomocą poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3417e-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="3417e-584">Aby uzyskać informacje na temat włączania szyfrowania z szyfrowania dysków Azure za pomocą poleceń cmdlet programu PowerShell, zobacz hello blogach [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) i [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="3417e-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="3417e-585">Za pomocą polecenia interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="3417e-585">Using CLI commands</span></span>
<span data-ttu-id="3417e-586">szyfrowanie tooenable na istniejących lub uruchomione maszyny Wirtualnej systemu Windows IaaS na platformie Azure przy użyciu polecenia interfejsu wiersza polecenia hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3417e-586">tooenable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="3417e-587">zasady dostępu tooset w magazynie kluczy hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-587">tooset access policies in hello key vault:</span></span>
   * <span data-ttu-id="3417e-588">Zestaw hello **EnabledForDiskEncryption** flagi:</span><span class="sxs-lookup"><span data-stu-id="3417e-588">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="3417e-589">Ustaw uprawnienia tooAzure AD aplikacji toowrite kluczy tajnych tooyour magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="3417e-589">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="3417e-590">tooenable szyfrowania w przypadku istniejących lub uruchomionej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="3417e-590">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="3417e-591">Stan szyfrowania tooget:</span><span class="sxs-lookup"><span data-stu-id="3417e-591">tooget encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="3417e-592">szyfrowanie tooenable na nowej maszyny Wirtualnej z zaszyfrowany dysk VHD, użyj hello następujące parametry hello `azure vm create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="3417e-592">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="3417e-593">Włącz szyfrowanie dla istniejących lub nie działają IaaS maszyny Wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3417e-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="3417e-594">Można włączyć szyfrowanie dysków na istniejące lub nie działają IaaS maszyny Wirtualnej systemu Linux na platformie Azure przy użyciu hello [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="3417e-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="3417e-595">Kliknij przycisk **wdrażanie tooAzure** na szablon hello Azure szybki start, wprowadź konfiguracji szyfrowania hello na powitania **parametry** bloku, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3417e-595">Click **Deploy tooAzure** on hello Azure quick-start template, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="3417e-596">Wybierz hello subskrypcji, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** tooenable szyfrowania na powitania istniejące lub uruchamiania maszyn wirtualnych IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-596">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="3417e-597">Witaj w poniższej tabeli przedstawiono parametry szablonu usługi Resource Manager dla istniejących lub działających maszyn wirtualnych, które mają identyfikator klienta usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="3417e-597">hello following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="3417e-598">Parametr</span><span class="sxs-lookup"><span data-stu-id="3417e-598">Parameter</span></span> | <span data-ttu-id="3417e-599">Opis</span><span class="sxs-lookup"><span data-stu-id="3417e-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3417e-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="3417e-600">AADClientID</span></span> | <span data-ttu-id="3417e-601">Identyfikator klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych toohello klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="3417e-601">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="3417e-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="3417e-602">AADClientSecret</span></span> | <span data-ttu-id="3417e-603">Klucz tajny klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych tooyour klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="3417e-603">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="3417e-604">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3417e-604">keyVaultName</span></span> | <span data-ttu-id="3417e-605">Nazwa klucza hello magazynu tego hello klucz należy przekazać do funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="3417e-605">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="3417e-606">Możesz pobrać go za pomocą polecenia cmdlet hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="3417e-606">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="3417e-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="3417e-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="3417e-608">Adres URL hello klucza szyfrowania klucza, który jest używany tooencrypt hello generowane klucza funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="3417e-608">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="3417e-609">Ten parametr jest opcjonalny w przypadku wybrania **nokek** na liście rozwijanej UseExistingKek hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-609">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="3417e-610">W przypadku wybrania **kek** na liście rozwijanej UseExistingKek hello, musisz wprowadzić hello _keyEncryptionKeyURL_ wartości.</span><span class="sxs-lookup"><span data-stu-id="3417e-610">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="3417e-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="3417e-611">volumeType</span></span> | <span data-ttu-id="3417e-612">Typ operacji szyfrowania hello jest wykonywana na wolumin.</span><span class="sxs-lookup"><span data-stu-id="3417e-612">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="3417e-613">Nieprawidłowy obsługiwane wartości to _OS_ lub _wszystkie_ (dla RHEL 7.2, CentOS 7.2 i Ubuntu 16.04), i _danych_ (dla wszystkich innych dystrybucji).</span><span class="sxs-lookup"><span data-stu-id="3417e-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="3417e-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="3417e-614">sequenceVersion</span></span> | <span data-ttu-id="3417e-615">Wersja sekwencji hello działania funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="3417e-615">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="3417e-616">Zwiększ numer wersji, za każdym razem, gdy operacji szyfrowania dysków odbywa się na powitania tej samej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-616">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="3417e-617">vmName</span><span class="sxs-lookup"><span data-stu-id="3417e-617">vmName</span></span> | <span data-ttu-id="3417e-618">Nazwa hello maszynę Wirtualną, która hello operacji szyfrowania jest wykonywane na toobe.</span><span class="sxs-lookup"><span data-stu-id="3417e-618">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |
| <span data-ttu-id="3417e-619">Hasło</span><span class="sxs-lookup"><span data-stu-id="3417e-619">passPhrase</span></span> | <span data-ttu-id="3417e-620">Klucz szyfrowania danych hello wpisz silne hasło.</span><span class="sxs-lookup"><span data-stu-id="3417e-620">Type a strong passphrase as hello data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="3417e-621">_KeyEncryptionKeyURL_ jest parametrem opcjonalnym.</span><span class="sxs-lookup"><span data-stu-id="3417e-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="3417e-622">Możesz objąć własne KEK toofurther zabezpieczenie hello klucza szyfrowania danych (klucz tajny hasło) w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-622">You can bring your own KEK toofurther safeguard hello data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="3417e-623">Polecenia interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="3417e-623">CLI commands</span></span>
<span data-ttu-id="3417e-624">Można włączyć szyfrowanie dysków na zaszyfrowany dysk VHD przez zainstalowanie i używanie hello [polecenia interfejsu wiersza polecenia](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3417e-624">You can enable disk encryption on your encrypted VHD by installing and using hello [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="3417e-625">szyfrowanie tooenable na istniejących lub działających maszyn wirtualnych systemu Linux IaaS na platformie Azure przy użyciu polecenia interfejsu wiersza polecenia hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3417e-625">tooenable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="3417e-626">Ustawianie zasad dostępu w magazynie kluczy hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-626">Set access policies in hello key vault:</span></span>

 * <span data-ttu-id="3417e-627">Zestaw hello **EnabledForDiskEncryption** flagi:</span><span class="sxs-lookup"><span data-stu-id="3417e-627">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="3417e-628">Ustaw uprawnienia tooAzure AD aplikacji toowrite kluczy tajnych tooyour magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="3417e-628">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="3417e-629">tooenable szyfrowania w przypadku istniejących lub uruchomionej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="3417e-629">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="3417e-630">Pobierz stan szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="3417e-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="3417e-631">szyfrowanie tooenable na nowej maszyny Wirtualnej z zaszyfrowany dysk VHD, użyj hello następujące parametry hello `azure vm create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="3417e-631">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="3417e-632">Pobierz stan szyfrowania hello zaszyfrowanych maszyny wirtualnej IaaS</span><span class="sxs-lookup"><span data-stu-id="3417e-632">Get hello encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="3417e-633">Przy użyciu usługi Azure Resource Manager można uzyskać stanu szyfrowania hello [poleceń cmdlet programu PowerShell](/powershell/azure/overview), lub polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3417e-633">You can get hello encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="3417e-634">Hello w następujących sekcjach wyjaśniono, jak hello toouse klasycznego portalu Azure i tooget polecenia interfejsu wiersza polecenia hello stanu szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="3417e-634">hello following sections explain how toouse hello Azure classic portal and CLI commands tooget hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="3417e-635">Uzyskiwanie hello stanu szyfrowania zaszyfrowanej maszyny Wirtualnej systemu Windows przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3417e-635">Get hello encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="3417e-636">Z usługi Azure Resource Manager można uzyskać stanu szyfrowania hello hello maszyn wirtualnych IaaS hello następujący:</span><span class="sxs-lookup"><span data-stu-id="3417e-636">You can get hello encryption status of hello IaaS VM from Azure Resource Manager by doing hello following:</span></span>

1. <span data-ttu-id="3417e-637">Zaloguj się toohello [klasycznego portalu Azure](https://portal.azure.com/), a następnie kliknij przycisk **maszyn wirtualnych** w toosee w okienku po lewej stronie powitania widok podsumowania hello maszyn wirtualnych w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3417e-637">Sign in toohello [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in hello left pane toosee a summary view of hello virtual machines in your subscription.</span></span> <span data-ttu-id="3417e-638">Można filtrować widok maszyn wirtualnych hello wybierając Nazwa subskrypcji hello hello **subskrypcji** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="3417e-638">You can filter hello virtual machines view by selecting hello subscription name in hello **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="3417e-639">U góry hello hello **maszyn wirtualnych** kliknij przycisk **kolumn**.</span><span class="sxs-lookup"><span data-stu-id="3417e-639">At hello top of hello **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="3417e-640">Na powitania **kolumny wybierz** bloku, wybierz opcję **szyfrowanie dysków**, a następnie kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="3417e-640">On hello **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="3417e-641">Powinien zostać wyświetlony stan szyfrowania hello przedstawiający hello szyfrowanie dysków kolumny _włączone_ lub _nie włączono_ dla każdej maszyny Wirtualnej, jak pokazano w następującej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-641">You should see hello disk-encryption column showing hello encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in hello following figure:</span></span>

 ![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="3417e-643">Pobierz stan szyfrowania hello zaszyfrowanych maszyny wirtualnej IaaS (system Windows/Linux) za pomocą polecenia cmdlet programu PowerShell szyfrowanie dysków hello</span><span class="sxs-lookup"><span data-stu-id="3417e-643">Get hello encryption status of an encrypted (Windows/Linux) IaaS VM by using hello disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="3417e-644">Można pobrać stanu szyfrowania hello hello maszyn wirtualnych IaaS z polecenia cmdlet programu PowerShell szyfrowanie dysków hello `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="3417e-644">You can get hello encryption status of hello IaaS VM from hello disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="3417e-645">ustawienia szyfrowania hello tooget dla maszyny Wirtualnej, wprowadź następujące hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-645">tooget hello encryption settings for your VM, enter hello following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="3417e-646">Możesz sprawdzić dane wyjściowe hello _Get-AzureRmVMDiskEncryptionStatus_ do szyfrowania klucza adresów URL.</span><span class="sxs-lookup"><span data-stu-id="3417e-646">You can inspect hello output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

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

<span data-ttu-id="3417e-647">Witaj OSVolumeEncrypted i DataVolumesEncrypted ustawienia wartości są ustawiane too_Encrypted_, który pokazuje, że oba woluminy są szyfrowane za pomocą szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-647">hello OSVolumeEncrypted and DataVolumesEncrypted settings values are set too_Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="3417e-648">Aby uzyskać informacje na temat włączania szyfrowania z szyfrowania dysków Azure za pomocą poleceń cmdlet programu PowerShell, zobacz hello blogach [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) i [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="3417e-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-649">Na maszynach wirtualnych systemu Linux, trwa trzy minut toofour hello `Get-AzureRmVMDiskEncryptionStatus` stanu szyfrowania hello tooreport polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3417e-649">On Linux VMs, it takes three toofour minutes for hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a><span data-ttu-id="3417e-650">Pobrać stanu szyfrowania hello hello maszyn wirtualnych IaaS z polecenia interfejsu wiersza polecenia szyfrowanie dysków hello</span><span class="sxs-lookup"><span data-stu-id="3417e-650">Get hello encryption status of hello IaaS VM from hello disk-encryption CLI command</span></span>
<span data-ttu-id="3417e-651">Stan szyfrowania hello hello maszyn wirtualnych IaaS można uzyskać za pomocą polecenia interfejsu wiersza polecenia szyfrowanie dysków hello `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="3417e-651">You can get hello encryption status of hello IaaS VM by using hello disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="3417e-652">ustawienia szyfrowania hello tooget dla maszyny Wirtualnej, wprowadź sesję wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="3417e-652">tooget hello encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="3417e-653">Wyłącz szyfrowanie uruchamiania maszyny Wirtualnej systemu Windows IaaS</span><span class="sxs-lookup"><span data-stu-id="3417e-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="3417e-654">Można wyłączyć szyfrowania na uruchomionej maszyny Wirtualnej systemu Linux IaaS lub systemu Windows za pośrednictwem hello szablon Menedżera zasobów szyfrowania dysków Azure lub poleceń cmdlet programu PowerShell i określić hello odszyfrowywania konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3417e-654">You can disable encryption on a running Windows or Linux IaaS VM via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify hello decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="3417e-655">Maszyna wirtualna z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="3417e-655">Windows VM</span></span>
<span data-ttu-id="3417e-656">krok Wyłącz szyfrowanie Hello wyłącza funkcję szyfrowania hello systemu operacyjnego i/lub ilość danych hello na powitania uruchamiania maszyny Wirtualnej systemu Windows IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-656">hello disable-encryption step disables encryption of hello OS, hello data volume, or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="3417e-657">Nie można wyłączyć hello woluminu systemu operacyjnego i pozostawić hello ilość danych zaszyfrowanych.</span><span class="sxs-lookup"><span data-stu-id="3417e-657">You cannot disable hello OS volume and leave hello data volume encrypted.</span></span> <span data-ttu-id="3417e-658">Po wykonaniu kroku Wyłącz szyfrowanie hello hello Azure klasycznego modelu wdrażania aktualizacji modelu usługi hello maszyny Wirtualnej, a hello maszyny Wirtualnej systemu Windows IaaS jest oznaczony jako odszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="3417e-658">When hello disable-encryption step is performed, hello Azure classic deployment model updates hello VM service model, and hello Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="3417e-659">zawartość Hello hello maszyny Wirtualnej nie są szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="3417e-659">hello contents of hello VM are no longer encrypted at rest.</span></span> <span data-ttu-id="3417e-660">odszyfrowywanie Hello nie powoduje usunięcia z magazynu i hello szyfrowania klucza materiału klucza (klucze szyfrowania funkcji BitLocker dla systemów Windows i hasło dla systemu Linux).</span><span class="sxs-lookup"><span data-stu-id="3417e-660">hello decryption does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="3417e-661">Maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="3417e-661">Linux VM</span></span>
<span data-ttu-id="3417e-662">krok Wyłącz szyfrowanie Hello wyłącza funkcję szyfrowania woluminu danych hello na powitania uruchamiania maszyny Wirtualnej systemu Linux IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-662">hello disable-encryption step disables encryption of hello data volume on hello running Linux IaaS VM.</span></span> <span data-ttu-id="3417e-663">Ten krok działa tylko, jeśli hello dysk systemu operacyjnego nie jest zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="3417e-663">This step only works if hello OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-664">Wyłączenie szyfrowania na powitania dysk systemu operacyjnego nie jest dozwolona na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="3417e-664">Disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="3417e-665">Wyłącz szyfrowanie na maszynie Wirtualnej IaaS istniejących lub nie działają</span><span class="sxs-lookup"><span data-stu-id="3417e-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="3417e-666">Można wyłączyć szyfrowania dysków na uruchomionych maszyn wirtualnych IaaS systemu Windows za pomocą hello [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="3417e-666">You can disable disk encryption on running Windows IaaS VMs by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="3417e-667">W szablonie hello Azure szybki start kliknij **wdrażanie tooAzure**, wprowadź konfiguracji odszyfrowywania hello na powitania **parametry** bloku, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3417e-667">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello decryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="3417e-668">Wybierz hello subskrypcji, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** tooenable szyfrowania na nowej maszyny Wirtualnej IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-668">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="3417e-669">Dla maszyn wirtualnych systemu Linux, można wyłączyć szyfrowania za pomocą hello [wyłączyć szyfrowania na uruchomionej maszyny Wirtualnej systemu Linux](https://aka.ms/decrypt-linuxvm) szablonu.</span><span class="sxs-lookup"><span data-stu-id="3417e-669">For Linux VMs, you can disable encryption by using hello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="3417e-670">Witaj Poniższa tabela zawiera listę parametrów szablonu usługi Resource Manager wyłączenie szyfrowania na uruchomionej maszynie Wirtualnej IaaS:</span><span class="sxs-lookup"><span data-stu-id="3417e-670">hello following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="3417e-671">Parametr</span><span class="sxs-lookup"><span data-stu-id="3417e-671">Parameter</span></span> | <span data-ttu-id="3417e-672">Opis</span><span class="sxs-lookup"><span data-stu-id="3417e-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3417e-673">vmName</span><span class="sxs-lookup"><span data-stu-id="3417e-673">vmName</span></span> | <span data-ttu-id="3417e-674">Nazwa hello maszynę Wirtualną, która hello operacji szyfrowania jest wykonywane na toobe.</span><span class="sxs-lookup"><span data-stu-id="3417e-674">Name of hello VM that hello encryption operation is toobe performed on.</span></span>
| <span data-ttu-id="3417e-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="3417e-675">volumeType</span></span> | <span data-ttu-id="3417e-676">Typ operacji odszyfrowywania odbywa się na wolumin.</span><span class="sxs-lookup"><span data-stu-id="3417e-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="3417e-677">Prawidłowe wartości to _OS_, _danych_, i _wszystkich_.</span><span class="sxs-lookup"><span data-stu-id="3417e-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="3417e-678">Nie można wyłączyć szyfrowania na uruchomienie woluminu systemu operacyjnego maszyny Wirtualnej systemu Windows IaaS/rozruchowego bez wyłączenie szyfrowania na powitania _danych_ woluminu.</span><span class="sxs-lookup"><span data-stu-id="3417e-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on hello _Data_ volume.</span></span> <span data-ttu-id="3417e-679">Należy również zauważyć, że wyłączenie szyfrowania na powitania dysk systemu operacyjnego nie jest dozwolona na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="3417e-679">Also note that disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="3417e-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="3417e-680">sequenceVersion</span></span> | <span data-ttu-id="3417e-681">Wersja sekwencji hello działania funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="3417e-681">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="3417e-682">Zwiększ numer wersji, za każdym razem, gdy operacji odszyfrowywania dysku jest wykonywana na powitania tej samej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-682">Increment this version number every time a disk decryption operation is performed on hello same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="3417e-683">Wyłącz szyfrowanie na maszynie Wirtualnej IaaS istniejących lub nie działają</span><span class="sxs-lookup"><span data-stu-id="3417e-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="3417e-684">Zobacz toodisable szyfrowania w przypadku istniejących lub nie działają IaaS maszyny Wirtualnej za pomocą polecenia cmdlet programu PowerShell hello, [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="3417e-684">toodisable encryption on an existing or running IaaS VM by using hello PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="3417e-685">To polecenie cmdlet obsługuje zarówno systemu Windows, jak i maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="3417e-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="3417e-686">szyfrowania toodisable instaluje rozszerzenia w maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-686">toodisable encryption, it installs an extension on hello virtual machine.</span></span> <span data-ttu-id="3417e-687">Jeśli hello _nazwa_ parametr nie zostanie określony, rozszerzenie nazwy domyślnej hello _AzureDiskEncryption za dla maszyn wirtualnych systemu Windows_ jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="3417e-687">If hello _Name_ parameter is not specified, an extension with hello default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="3417e-688">Na maszynach wirtualnych systemu Linux rozszerzenia AzureDiskEncryptionForLinux hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="3417e-688">On Linux VMs, hello AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="3417e-689">To polecenie cmdlet ponowny rozruch hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-689">This cmdlet reboots hello virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="3417e-690">Włącz szyfrowanie dla zaszyfrowane wstępnie IaaS maszynę Wirtualną za pomocą dysku zarządzanego Azure</span><span class="sxs-lookup"><span data-stu-id="3417e-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="3417e-691">Użyj toocreate szablonu Azure ARM zarządzane dysku hello, którego zaszyfrowanych maszyny Wirtualnej z dysku VHD zaszyfrowane wstępnie przy użyciu szablonu ARM hello znajdujący się w</span><span class="sxs-lookup"><span data-stu-id="3417e-691">Use hello Azure Managed Disk ARM template toocreate a encrypted VM from a pre-encrypted VHD using hello ARM template located at</span></span>   
<span data-ttu-id="3417e-692">[Utwórz nowe zaszyfrowanych dysków zarządzanych z zaszyfrowane wstępnie obiektu blob dysku VHD/magazynu] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="3417e-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="3417e-693">Włącz szyfrowanie dla nowej Linux IaaS maszyny Wirtualnej z dyskiem zarządzane Azure</span><span class="sxs-lookup"><span data-stu-id="3417e-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="3417e-694">Użyj toocreate szablonu Azure ARM zarządzane dysku hello szyfrowane nowej maszyny Wirtualnej IaaS systemu Linux przy użyciu szablonu ARM hello znajdujący się w</span><span class="sxs-lookup"><span data-stu-id="3417e-694">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
<span data-ttu-id="3417e-695">[Wdrażanie RHEL 7.2 z pełne szyfrowanie dysków] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="3417e-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="3417e-696">Włącz szyfrowanie dla nowej maszyny Wirtualnej IaaS systemu Windows z dysku zarządzanego Azure</span><span class="sxs-lookup"><span data-stu-id="3417e-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="3417e-697">Użyj toocreate szablonu Azure ARM zarządzane dysku hello szyfrowane nowej maszyny Wirtualnej IaaS systemu Linux przy użyciu szablonu ARM hello znajdujący się w</span><span class="sxs-lookup"><span data-stu-id="3417e-697">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
 <span data-ttu-id="3417e-698">[Tworzenie nowych zaszyfrowanych systemu Windows IaaS zarządzane dysku maszyny Wirtualnej z obrazu galerii] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="3417e-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="3417e-699">Obowiązkowe toosnapshot i/lub tworzenia kopii zapasowych dysków zarządzanych i opartych na wystąpienie maszyny Wirtualnej poza wcześniejsze tooenabling szyfrowania dysków Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-699">It is mandatory toosnapshot and/or backup a managed disk based VM instance outside of and prior tooenabling Azure Disk Encryption.</span></span>  <span data-ttu-id="3417e-700">Migawki dysków zarządzanych w hello może zostać pobrany z portalu hello, lub kopia zapasowa Azure można używać.</span><span class="sxs-lookup"><span data-stu-id="3417e-700">A snapshot of hello managed disk can be taken from hello portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="3417e-701">Kopie zapasowe upewnij się, że opcji odzyskiwania jest możliwe w przypadku hello żadnych nieoczekiwany błąd podczas szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="3417e-701">Backups ensure that a recovery option is possible in hello case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="3417e-702">Po utworzeniu kopii zapasowej polecenia cmdlet hello AzureRmVMDiskEncryptionExtension zestaw może być dysków używanych tooencrypt zarządzane, określając parametr - skipVmBackup hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-702">Once a backup is made, hello Set-AzureRmVMDiskEncryptionExtension cmdlet can be used tooencrypt managed disks by specifying hello -skipVmBackup parameter.</span></span>  <span data-ttu-id="3417e-703">To polecenie zakończy się niepowodzeniem przed dysków zarządzanych, na podstawie maszyny Wirtualnej, dopóki nie wykonano kopii zapasowej i podano tego parametru.</span><span class="sxs-lookup"><span data-stu-id="3417e-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="3417e-704">Aktualizowanie ustawień szyfrowania z istniejącej maszyny Wirtualnej z systemem innym niż premium zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="3417e-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="3417e-705">Używanie hello istniejącego dysku platformy Azure szyfrowania obsługiwane interfejsów do uruchamiania maszyny Wirtualnej [PS poleceń cmdlet, interfejsu wiersza polecenia lub ARM szablonów] tooupdate hello ustawienia szyfrowania, takich jak usługi AAD klienta identyfikator/klucz tajny, klucz szyfrowania klucza [KEK], klucz szyfrowania funkcją BitLocker dla maszyny Wirtualnej systemu Windows lub hasło dla Ustawienie szyfrowania aktualizacji hello itp. maszyny Wirtualnej systemu Linux jest obsługiwana tylko dla maszyn wirtualnych przez inne niż premium magazynu.</span><span class="sxs-lookup"><span data-stu-id="3417e-705">Use hello existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] tooupdate hello encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. hello update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="3417e-706">Jest obsługiwana dla maszyn wirtualnych przez Magazyn w warstwie premium NNOT.</span><span class="sxs-lookup"><span data-stu-id="3417e-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="3417e-707">Dodatek</span><span class="sxs-lookup"><span data-stu-id="3417e-707">Appendix</span></span>
### <a name="connect-tooyour-subscription"></a><span data-ttu-id="3417e-708">Połącz tooyour subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3417e-708">Connect tooyour subscription</span></span>
<span data-ttu-id="3417e-709">Przed kontynuowaniem należy przejrzeć hello *wymagania wstępne* w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="3417e-709">Before you proceed, review hello *Prerequisites* section in this article.</span></span> <span data-ttu-id="3417e-710">Po upewnieniu się, że zostały spełnione wszystkie wymagania wstępne, podłącz subskrypcji tooyour hello następujący:</span><span class="sxs-lookup"><span data-stu-id="3417e-710">After you ensure that all prerequisites have been met, connect tooyour subscription by doing hello following:</span></span>

1. <span data-ttu-id="3417e-711">Uruchom sesję programu PowerShell Azure i zaloguj się tooyour konto platformy Azure za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-711">Start an Azure PowerShell session, and sign in tooyour Azure account with hello following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="3417e-712">Jeśli masz wiele subskrypcji i chcesz toouse jeden toospecify, wpisz powitania po toosee hello subskrypcje dla swojego konta:</span><span class="sxs-lookup"><span data-stu-id="3417e-712">If you have multiple subscriptions and want toospecify one toouse, type hello following toosee hello subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="3417e-713">Subskrypcja hello toospecify ma toouse, wpisz:</span><span class="sxs-lookup"><span data-stu-id="3417e-713">toospecify hello subscription you want toouse, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="3417e-714">tooverify czy subskrypcję hello jest poprawna, wpisz:</span><span class="sxs-lookup"><span data-stu-id="3417e-714">tooverify that hello subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="3417e-715">Witaj tooconfirm szyfrowania dysków Azure są zainstalowane polecenia cmdlet, wpisz:</span><span class="sxs-lookup"><span data-stu-id="3417e-715">tooconfirm hello Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="3417e-716">następujące dane wyjściowe Hello potwierdza hello Azure PowerShell szyfrowania dysku instalacji:</span><span class="sxs-lookup"><span data-stu-id="3417e-716">hello following output confirms hello Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="3417e-717">Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3417e-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="3417e-718">kolejnych sekcjach Hello są niezbędne tooprepare zaszyfrowane wstępnie dysku VHD systemu Windows dla wdrożenia jako zaszyfrowanego dysku VHD w programie Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="3417e-718">hello sections that follow are necessary tooprepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="3417e-719">Użyj hello tooprepare informacji i rozruchu świeże systemu Windows maszyny Wirtualnej (VHD) dla usługi Azure Site Recovery lub Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-719">Use hello information tooprepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a><span data-ttu-id="3417e-720">Aktualizowanie grupy zasad tooallow bez modułu TPM do ochrony systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="3417e-720">Update group policy tooallow non-TPM for OS protection</span></span>
<span data-ttu-id="3417e-721">Ustawienia zasad grupy funkcji BitLocker hello **szyfrowania dysków funkcją BitLocker**, które znajdują się w obszarze **lokalnych zasad komputera** > **Konfiguracja komputera**  >  **Szablony administracyjne** > **składniki systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="3417e-721">Configure hello BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="3417e-722">Zmienić to ustawienie zbyt**dyski z systemem operacyjnym** > **wymaga dodatkowego uwierzytelniania przy uruchamianiu** > **Zezwalaj na funkcję BitLocker bez zgodny moduł TPM**, jak pokazano w hello następującej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="3417e-722">Change this setting too**Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in hello following figure:</span></span>

![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="3417e-724">Zainstaluj składniki funkcji BitLocker</span><span class="sxs-lookup"><span data-stu-id="3417e-724">Install BitLocker feature components</span></span>
<span data-ttu-id="3417e-725">W systemie Windows Server 2012 i nowszych Użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="3417e-725">For Windows Server 2012 and later, use hello following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="3417e-726">Dla systemu Windows Server 2008 R2 należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="3417e-726">For Windows Server 2008 R2, use hello following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="3417e-727">Przygotowanie hello woluminu systemu operacyjnego dla funkcji BitLocker przy użyciu`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="3417e-727">Prepare hello OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="3417e-728">toocompress hello partycji systemu operacyjnego i przygotowanie maszyny hello funkcji BitLocker, należy wykonać hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="3417e-728">toocompress hello OS partition and prepare hello machine for BitLocker, execute hello following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a><span data-ttu-id="3417e-729">Ochrona powitalnych woluminu systemu operacyjnego za pomocą funkcji BitLocker</span><span class="sxs-lookup"><span data-stu-id="3417e-729">Protect hello OS volume by using BitLocker</span></span>
<span data-ttu-id="3417e-730">Użyj hello [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) polecenia tooenable szyfrowania na powitania wolumin rozruchowy przy użyciu zewnętrznego funkcji ochrony klucza.</span><span class="sxs-lookup"><span data-stu-id="3417e-730">Use hello [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command tooenable encryption on hello boot volume using an external key protector.</span></span> <span data-ttu-id="3417e-731">Również umieścić klucz zewnętrzny hello (plik .bek) na powitania zewnętrzny dysk lub wolumin.</span><span class="sxs-lookup"><span data-stu-id="3417e-731">Also place hello external key (.bek file) on hello external drive or volume.</span></span> <span data-ttu-id="3417e-732">Szyfrowanie jest włączone na wolumin systemowy/rozruchowy powitania po następnym ponownym uruchomieniu hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-732">Encryption is enabled on hello system/boot volume after hello next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="3417e-733">Przygotowanie hello maszyny Wirtualnej z oddzielnych danych/zasobów wirtualnego dysku twardego do pobierania klucza zewnętrznego hello za pomocą funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="3417e-733">Prepare hello VM with a separate data/resource VHD for getting hello external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="3417e-734">Szyfrowanie dysku systemu operacyjnego na uruchomionej maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="3417e-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="3417e-735">Szyfrowanie dysku systemu operacyjnego na uruchomionej maszyny Wirtualnej systemu Linux jest obsługiwana na powitania po dystrybucji:</span><span class="sxs-lookup"><span data-stu-id="3417e-735">Encryption of an OS drive on a running Linux VM is supported on hello following distributions:</span></span>

* <span data-ttu-id="3417e-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="3417e-736">RHEL 7.2</span></span>
* <span data-ttu-id="3417e-737">7.2 centOS</span><span class="sxs-lookup"><span data-stu-id="3417e-737">CentOS 7.2</span></span>
* <span data-ttu-id="3417e-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="3417e-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="3417e-739">Wymagania wstępne dotyczące szyfrowania dysku systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="3417e-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="3417e-740">Witaj maszyny Wirtualnej musi zostać utworzona z obrazu witryny Marketplace hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3417e-740">hello VM must be created from hello Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="3417e-741">Maszyna wirtualna platformy Azure z co najmniej 4 GB pamięci RAM (zalecany rozmiar to 7 GB).</span><span class="sxs-lookup"><span data-stu-id="3417e-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="3417e-742">(W przypadku RHEL i CentOS) Wyłącz SELinux.</span><span class="sxs-lookup"><span data-stu-id="3417e-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="3417e-743">toodisable SELinux, zobacz "4.4.2.</span><span class="sxs-lookup"><span data-stu-id="3417e-743">toodisable SELinux, see "4.4.2.</span></span> <span data-ttu-id="3417e-744">Wyłączanie SELinux"w hello [Przewodnik administratora i użytkownika SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-744">Disabling SELinux" in hello [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on hello VM.</span></span>
* <span data-ttu-id="3417e-745">Po wyłączeniu SELinux co najmniej raz ponowny rozruch hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-745">After you disable SELinux, reboot hello VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="3417e-746">Kroki</span><span class="sxs-lookup"><span data-stu-id="3417e-746">Steps</span></span>
1. <span data-ttu-id="3417e-747">Utwórz maszynę Wirtualną za pomocą jednego z dystrybucji hello określony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="3417e-747">Create a VM by using one of hello distributions specified previously.</span></span>

 <span data-ttu-id="3417e-748">7.2 CentOS szyfrowania dysku systemu operacyjnego jest obsługiwane za pomocą specjalnego obrazu.</span><span class="sxs-lookup"><span data-stu-id="3417e-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="3417e-749">toouse to obrazów, określ "7.2n" hello SKU podczas tworzenia hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="3417e-749">toouse this image, specify "7.2n" as hello SKU when you create hello VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="3417e-750">Skonfiguruj zgodnie z potrzebami tooyour hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-750">Configure hello VM according tooyour needs.</span></span> <span data-ttu-id="3417e-751">Jeśli zamierzasz tooencrypt wszystkie dyski hello (systemu operacyjnego i danych), dyski danych hello muszą toobe określonego i instalację z /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="3417e-751">If you are going tooencrypt all hello (OS + data) drives, hello data drives need toobe specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="3417e-752">Użyj identyfikatora UUID =... toospecify dysków danych w fstab/etc/zamiast określania nazwy urządzenia bloku hello (na przykład /dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="3417e-752">Use UUID=... toospecify data drives in /etc/fstab instead of specifying hello block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="3417e-753">Podczas szyfrowania, kolejność hello zmiany dysków na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-753">During encryption, hello order of drives changes on hello VM.</span></span> <span data-ttu-id="3417e-754">Jeśli maszyna wirtualna opiera się na określonej kolejności urządzeń bloku, zakończy się niepowodzeniem toomount je po szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="3417e-754">If your VM relies on a specific order of block devices, it will fail toomount them after encryption.</span></span>

3. <span data-ttu-id="3417e-755">Wyloguj hello sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="3417e-755">Sign out of hello SSH sessions.</span></span>

4. <span data-ttu-id="3417e-756">tooencrypt hello systemu operacyjnego, określ volumeType jako **wszystkie** lub **OS** podczas możesz [włączyć szyfrowanie](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="3417e-756">tooencrypt hello OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="3417e-757">Wszystkie procesy przestrzeń użytkownika, które nie są uruchomione jako `systemd` usługi powinny skasowane z `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="3417e-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="3417e-758">Ponowny rozruch hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-758">Reboot hello VM.</span></span> <span data-ttu-id="3417e-759">Po włączeniu szyfrowania dysku systemu operacyjnego na uruchomionej maszynie Wirtualnej, należy zaplanować przestój maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="3417e-760">Okresowo monitorować postęp hello szyfrowania za pomocą instrukcji hello w hello [następnej sekcji](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="3417e-760">Periodically monitor hello progress of encryption by using hello instructions in hello [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="3417e-761">Po Get AzureRmVmDiskEncryptionStatus zawiera "VMRestartPending", należy ponownie uruchomić maszyny Wirtualnej, logując się tooit lub za pomocą portalu hello, programu PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3417e-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in tooit or by using hello portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
<span data-ttu-id="3417e-762">Przed ponownym, zaleca się zapisanie [diagnostyki rozruchu](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of hello VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="3417e-763">Monitorowanie postępu szyfrowania systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="3417e-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="3417e-764">Możesz monitorować postęp szyfrowania systemu operacyjnego na trzy sposoby:</span><span class="sxs-lookup"><span data-stu-id="3417e-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="3417e-765">Użyj hello `Get-AzureRmVmDiskEncryptionStatus` polecenia cmdlet i sprawdzić hello postępu pola:</span><span class="sxs-lookup"><span data-stu-id="3417e-765">Use hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect hello ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="3417e-766">Po hello wirtualna osiągnie "Rozpoczęto szyfrowania dysku systemu operacyjnego", trwa około 40 minutach too50 na magazyn Premium kopii maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-766">After hello VM reaches "OS disk encryption started," it takes about 40 too50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="3417e-767">Z powodu [wystawiać #388](https://github.com/Azure/WALinuxAgent/issues/388) w WALinuxAgent, `OsVolumeEncrypted` i `DataVolumesEncrypted` wyświetlane jako `Unknown` w niektórych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="3417e-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="3417e-768">Z WALinuxAgent wersji 2.1.5 i później, ten problem zostanie rozwiązany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="3417e-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="3417e-769">Jeśli widzisz `Unknown` w danych wyjściowych hello, można sprawdzić stan szyfrowanie dysków za pomocą hello Eksploratora zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-769">If you see `Unknown` in hello output, you can verify disk-encryption status by using hello Azure Resource Explorer.</span></span>

 <span data-ttu-id="3417e-770">Przejdź za[Eksploratora zasobów Azure](https://resources.azure.com/), a następnie rozwiń węzeł tej hierarchii w hello panelu wyboru po lewej stronie:</span><span class="sxs-lookup"><span data-stu-id="3417e-770">Go too[Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in hello selection panel on left:</span></span>

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

 <span data-ttu-id="3417e-771">W hello InstanceView przewiń w dół toosee hello stan szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="3417e-771">In hello InstanceView, scroll down toosee hello encryption status of your drives.</span></span>

 ![Widok wystąpienia maszyny Wirtualnej](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="3417e-773">Przyjrzyj się [diagnostyki rozruchu](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="3417e-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="3417e-774">Wiadomości powitania ADE rozszerzenia musi być poprzedzona ciągiem `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="3417e-774">Messages from hello ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="3417e-775">Zaloguj się toohello maszyny Wirtualnej za pośrednictwem SSH i Pobierz dziennik rozszerzenia powitania od:</span><span class="sxs-lookup"><span data-stu-id="3417e-775">Sign in toohello VM via SSH, and get hello extension log from:</span></span>

    <span data-ttu-id="3417e-776">/var/log/Azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="3417e-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="3417e-777">Zaleca się, że nie podpiszesz w toohello maszyny Wirtualnej w trakcie szyfrowania systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3417e-777">We recommend that you do not sign in toohello VM while OS encryption is in progress.</span></span> <span data-ttu-id="3417e-778">Skopiuj dzienniki hello tylko wtedy, gdy hello dwóch innych metod nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="3417e-778">Copy hello logs only when hello other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="3417e-779">Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Linux</span><span class="sxs-lookup"><span data-stu-id="3417e-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="3417e-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="3417e-780">Ubuntu 16</span></span>
<span data-ttu-id="3417e-781">Konfigurowanie szyfrowania podczas instalacji dystrybucji hello hello następujący:</span><span class="sxs-lookup"><span data-stu-id="3417e-781">Configure encryption during hello distribution installation by doing hello following:</span></span>

1. <span data-ttu-id="3417e-782">Wybierz **skonfigurować zaszyfrowanych woluminach** po partycji dysków hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-782">Select **Configure encrypted volumes** when you partition hello disks.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="3417e-784">Utwórz dysk rozruchowy oddzielne, nie muszą być szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="3417e-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="3417e-785">Szyfrowanie dysku głównym.</span><span class="sxs-lookup"><span data-stu-id="3417e-785">Encrypt your root drive.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="3417e-787">Należy podać hasło.</span><span class="sxs-lookup"><span data-stu-id="3417e-787">Provide a passphrase.</span></span> <span data-ttu-id="3417e-788">Jest to hasło hello przekazanie toohello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-788">This is hello passphrase that you upload toohello key vault.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="3417e-790">Zakończ partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="3417e-790">Finish partitioning.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="3417e-792">Po rozruchu hello maszyny Wirtualnej i są wyświetlane pytanie o hasło, należy używać hello hasło, podane w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="3417e-792">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="3417e-794">Przygotowanie hello maszyny Wirtualnej do przekazywania do platformy Azure przy użyciu [tych instrukcji](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="3417e-794">Prepare hello VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="3417e-795">Nie należy jeszcze uruchamiać hello ostatni krok (hello anulowania obsługi maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="3417e-795">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="3417e-796">Skonfiguruj toowork szyfrowania z platformy Azure, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-796">Configure encryption toowork with Azure by doing hello following:</span></span>

1. <span data-ttu-id="3417e-797">Utwórz plik w obszarze /usr/local/sbin/azure_crypt_key.sh, zawartością hello hello następującego skryptu.</span><span class="sxs-lookup"><span data-stu-id="3417e-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with hello content in hello following script.</span></span> <span data-ttu-id="3417e-798">Należy zwrócić uwagę toohello KeyFileName, ponieważ jest nazwa pliku hasło hello używana przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-798">Pay attention toohello KeyFileName, because it is hello passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="3417e-799">Zmienianie konfiguracji crypt hello w */etc/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="3417e-799">Change hello crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="3417e-800">Powinny wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="3417e-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="3417e-801">Jeśli edytujesz *azure_crypt_key.sh* w systemie Windows i skopiować go tooLinux, uruchom `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="3417e-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it tooLinux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="3417e-802">Dodaj uprawnienia pliku wykonywalnego toohello skryptu:</span><span class="sxs-lookup"><span data-stu-id="3417e-802">Add executable permissions toohello script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="3417e-803">Edytuj */etc/initramfs-tools/modules* przez dołączenie wiersze:</span><span class="sxs-lookup"><span data-stu-id="3417e-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="3417e-804">Uruchom `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` zostały zastosowane.</span><span class="sxs-lookup"><span data-stu-id="3417e-804">Run `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` take effect.</span></span>

7. <span data-ttu-id="3417e-805">Teraz można anulowanie zastrzeżenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3417e-805">Now you can deprovision hello VM.</span></span>

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="3417e-807">Kontynuować toohello następnego kroku i [przekazać dysk VHD](#upload-encrypted-vhd-to-an-azure-storage-account) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-807">Continue toohello next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="3417e-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="3417e-808">openSUSE 13.2</span></span>
<span data-ttu-id="3417e-809">szyfrowanie tooconfigure podczas instalacji dystrybucji hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3417e-809">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="3417e-810">Gdy partycji dysków hello, wybierz **szyfrowania woluminu grupy**, a następnie wprowadź hasło.</span><span class="sxs-lookup"><span data-stu-id="3417e-810">When you partition hello disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="3417e-811">Jest to hasło hello przekaże tooyour magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-811">This is hello password that you will upload tooyour key vault.</span></span>

 ![openSUSE 13.2 Instalatora](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="3417e-813">Witaj rozruchu maszyny Wirtualnej przy użyciu hasła.</span><span class="sxs-lookup"><span data-stu-id="3417e-813">Boot hello VM using your password.</span></span>

 ![openSUSE 13.2 Instalatora](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="3417e-815">Przygotowanie hello maszyny Wirtualnej dla przekazywania tooAzure, wykonując następujące instrukcje hello [przygotowanie SLES lub openSUSE maszyny wirtualnej na platformie Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="3417e-815">Prepare hello VM for uploading tooAzure by following hello instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="3417e-816">Nie należy jeszcze uruchamiać hello ostatni krok (hello anulowania obsługi maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="3417e-816">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="3417e-817">tooconfigure toowork szyfrowania z platformy Azure, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3417e-817">tooconfigure encryption toowork with Azure, do hello following:</span></span>
1. <span data-ttu-id="3417e-818">Edytuj hello /etc/dracut.conf, a następnie dodaj powitania po wierszu:</span><span class="sxs-lookup"><span data-stu-id="3417e-818">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="3417e-819">Komentarz te wiersze końca hello hello pliku /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="3417e-819">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="3417e-820">Dołącz hello następującego wiersza początku hello /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh pliku hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-820">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="3417e-821">I zmień wszystkich wystąpień:</span><span class="sxs-lookup"><span data-stu-id="3417e-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="3417e-822">na:</span><span class="sxs-lookup"><span data-stu-id="3417e-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="3417e-823">Edytuj /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh i dołącza je za "# Otwórz LUKS urządzenie":</span><span class="sxs-lookup"><span data-stu-id="3417e-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it too“# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
5. <span data-ttu-id="3417e-824">Uruchom `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="3417e-824">Run `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span></span>

6. <span data-ttu-id="3417e-825">Teraz można anulowanie zastrzeżenia hello maszyny Wirtualnej i [przekazać dysk VHD](#upload-encrypted-vhd-to-an-azure-storage-account) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-825">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="3417e-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="3417e-826">CentOS 7</span></span>
<span data-ttu-id="3417e-827">szyfrowanie tooconfigure podczas instalacji dystrybucji hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3417e-827">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="3417e-828">Wybierz **szyfrowania danych** po partycji dysków.</span><span class="sxs-lookup"><span data-stu-id="3417e-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="3417e-830">Upewnij się, że **Szyfruj** jest zaznaczone dla partycji katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="3417e-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="3417e-832">Należy podać hasło.</span><span class="sxs-lookup"><span data-stu-id="3417e-832">Provide a passphrase.</span></span> <span data-ttu-id="3417e-833">Jest to hasło hello przekaże tooyour magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-833">This is hello passphrase that you will upload tooyour key vault.</span></span>

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="3417e-835">Po rozruchu hello maszyny Wirtualnej i są wyświetlane pytanie o hasło, należy używać hello hasło, podane w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="3417e-835">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="3417e-837">Przygotowanie hello maszyny Wirtualnej do przekazywania na platformie Azure za pomocą instrukcji "CentOS 7.0 +" hello w [przygotowanie maszyny wirtualnej CentOS, oparty na platformie Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="3417e-837">Prepare hello VM for uploading into Azure by using hello "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="3417e-838">Nie należy jeszcze uruchamiać hello ostatni krok (hello anulowania obsługi maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="3417e-838">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

6. <span data-ttu-id="3417e-839">Teraz można anulowanie zastrzeżenia hello maszyny Wirtualnej i [przekazać dysk VHD](#upload-encrypted-vhd-to-an-azure-storage-account) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3417e-839">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="3417e-840">tooconfigure toowork szyfrowania z platformy Azure, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3417e-840">tooconfigure encryption toowork with Azure, do hello following:</span></span>

1. <span data-ttu-id="3417e-841">Edytuj hello /etc/dracut.conf, a następnie dodaj powitania po wierszu:</span><span class="sxs-lookup"><span data-stu-id="3417e-841">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="3417e-842">Komentarz te wiersze końca hello hello pliku /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="3417e-842">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="3417e-843">Dołącz hello następującego wiersza początku hello /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh pliku hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-843">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="3417e-844">I zmień wszystkich wystąpień:</span><span class="sxs-lookup"><span data-stu-id="3417e-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="3417e-845">na</span><span class="sxs-lookup"><span data-stu-id="3417e-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="3417e-846">Edytuj /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh i Dołącz po "# Otwórz LUKS urządzenie" hello:</span><span class="sxs-lookup"><span data-stu-id="3417e-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after hello “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
5. <span data-ttu-id="3417e-847">Uruchom hello "/ usr/sbin/dracut - f - v" tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="3417e-847">Run hello “/usr/sbin/dracut -f -v” tooupdate hello initrd.</span></span>

![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a><span data-ttu-id="3417e-849">Przekaż zaszyfrowanego dysku VHD tooan konta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="3417e-849">Upload encrypted VHD tooan Azure storage account</span></span>
<span data-ttu-id="3417e-850">Po włączeniu szyfrowania funkcją BitLocker lub szyfrowania DM-Crypt lokalne powitania szyfrowane konta magazynu wirtualnego dysku twardego musi przekazać toobe tooyour.</span><span class="sxs-lookup"><span data-stu-id="3417e-850">After BitLocker encryption or DM-Crypt encryption is enabled, hello local encrypted VHD needs toobe uploaded tooyour storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a><span data-ttu-id="3417e-851">Przekaż hello hasło szyfrowania dysków dla magazynu kluczy hello zaszyfrowane wstępnie wirtualna tooyour</span><span class="sxs-lookup"><span data-stu-id="3417e-851">Upload hello disk-encryption secret for hello pre-encrypted VM tooyour key vault</span></span>
<span data-ttu-id="3417e-852">klucz tajny szyfrowanie dysków hello uzyskany wcześniej, należy przekazać jako klucza tajnego w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="3417e-852">hello disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="3417e-853">magazyn kluczy Hello musi toohave szyfrowania dysku i uprawnienia włączona dla klienta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3417e-853">hello key vault needs toohave disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="3417e-854">Hasło szyfrowania dysku nie jest zaszyfrowany przy KEK</span><span class="sxs-lookup"><span data-stu-id="3417e-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="3417e-855">tooset się klucz tajny hello w magazynie kluczy, użyj [AzureKeyVaultSecret zestawu](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="3417e-855">tooset up hello secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="3417e-856">Jeśli masz maszyny wirtualnej systemu Windows, plik bek hello został zakodowany jako ciąg base64 i następnie przekazać magazyn kluczy tooyour przy użyciu hello `Set-AzureKeyVaultSecret` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3417e-856">If you have a Windows virtual machine, hello bek file is encoded as a base64 string and then uploaded tooyour key vault using hello `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="3417e-857">Dla systemu Linux hasło hello został zakodowany jako ciąg w formacie base64, a następnie przekazać magazyn kluczy toohello.</span><span class="sxs-lookup"><span data-stu-id="3417e-857">For Linux, hello passphrase is encoded as a base64 string and then uploaded toohello key vault.</span></span> <span data-ttu-id="3417e-858">Ponadto upewnij się, że ten powitania po tagi są ustawiane podczas tworzenia hello klucza tajnego w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-858">In addition, make sure that hello following tags are set when you create hello secret in hello key vault.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="3417e-859">Użyj hello `$secretUrl` w następnym kroku powitania dla [Trwa dołączanie dysku hello systemu operacyjnego bez użycia KEK](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="3417e-859">Use hello `$secretUrl` in hello next step for [attaching hello OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="3417e-860">Hasło szyfrowania dysku zaszyfrowane za pomocą KEK</span><span class="sxs-lookup"><span data-stu-id="3417e-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="3417e-861">Przed przekazaniem magazynu kluczy tajnych toohello hello, można opcjonalnie zaszyfrować przy użyciu klucza szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="3417e-861">Before you upload hello secret toohello key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="3417e-862">Użyj hello zawijania [interfejsu API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst zaszyfrować klucza tajnego hello przy użyciu klucza szyfrowania klucza hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-862">Use hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encrypt hello secret using hello key encryption key.</span></span> <span data-ttu-id="3417e-863">Witaj wynik tej operacji zawijania jest base64 ciągu zakodowane w adresie URL, który można następnie przekazać jako klucz tajny przy użyciu hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3417e-863">hello output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using hello [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
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

<span data-ttu-id="3417e-864">Użyj `$KeyEncryptionKey` i `$secretUrl` w następnym kroku powitania dla [Trwa dołączanie dysku hello systemu operacyjnego przy użyciu KEK](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="3417e-864">Use `$KeyEncryptionKey` and `$secretUrl` in hello next step for [attaching hello OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="3417e-865">Określ adres URL tajne, po podłączeniu dysku systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="3417e-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="3417e-866">Bez użycia KEK</span><span class="sxs-lookup"><span data-stu-id="3417e-866">Without using a KEK</span></span>
<span data-ttu-id="3417e-867">Podczas dołączania dysku hello systemu operacyjnego, należy toopass `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="3417e-867">While you are attaching hello OS disk, you need toopass `$secretUrl`.</span></span> <span data-ttu-id="3417e-868">adres URL Hello został wygenerowany w sekcji "nie jest zaszyfrowany przy KEK tajny szyfrowanie dysków" hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-868">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="3417e-869">Przy użyciu KEK</span><span class="sxs-lookup"><span data-stu-id="3417e-869">Using a KEK</span></span>
<span data-ttu-id="3417e-870">Po podłączeniu dysku systemu operacyjnego hello przekazać `$KeyEncryptionKey` i `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="3417e-870">When you attach hello OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="3417e-871">adres URL Hello został wygenerowany w sekcji "nie jest zaszyfrowany przy KEK tajny szyfrowanie dysków" hello.</span><span class="sxs-lookup"><span data-stu-id="3417e-871">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

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

## <a name="download-this-guide"></a><span data-ttu-id="3417e-872">Pobierz w tym przewodniku</span><span class="sxs-lookup"><span data-stu-id="3417e-872">Download this guide</span></span>
<span data-ttu-id="3417e-873">W tym przewodniku można pobrać z hello [galerii TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="3417e-873">You can download this guide from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="3417e-874">Aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="3417e-874">For more information</span></span>
[<span data-ttu-id="3417e-875">Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 1</span><span class="sxs-lookup"><span data-stu-id="3417e-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="3417e-876">Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 2</span><span class="sxs-lookup"><span data-stu-id="3417e-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
