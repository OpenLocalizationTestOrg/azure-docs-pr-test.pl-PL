---
title: Ochrona danych osobowych magazynowane z szyfrowaniem aaaAzure | Dokumentacja firmy Microsoft
description: "W tym artykule jest częścią serii, pomaga użyć danych osobowych Azure tooprotect"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="53284-103">Technologii szyfrowania Azure: ochrony danych osobowych w stanie spoczynku z szyfrowaniem</span><span class="sxs-lookup"><span data-stu-id="53284-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="53284-104">Ten artykuł pomaga w zrozumieniu i użytkowaniu danych toosecure technologii szyfrowania Azure w stanie spoczynku.</span><span class="sxs-lookup"><span data-stu-id="53284-104">This article helps you understand and use Azure encryption technologies toosecure data at rest.</span></span>

<span data-ttu-id="53284-105">Szyfrowanie danych magazynowanych jest jako najlepsze rozwiązanie tooprotect poufnych i osobistych danych i toomeet zgodności i wymaganiami dotyczącymi ochrony prywatności danych.</span><span class="sxs-lookup"><span data-stu-id="53284-105">Encryption of data at rest is essential as a best practice tooprotect sensitive or personal data and toomeet compliance and data privacy requirements.</span></span>
<span data-ttu-id="53284-106">Szyfrowanie rest jest zaprojektowana tooprevent atakująca hello uzyskanie dostępu do danych hello bez szyfrowania, zapewniając hello, którego dane są szyfrowane, gdy na dysku.</span><span class="sxs-lookup"><span data-stu-id="53284-106">Encryption at rest is designed tooprevent hello attacker from accessing hello unencrypted data by ensuring hello data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="53284-107">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="53284-107">Scenario</span></span> 

<span data-ttu-id="53284-108">Firma rejs dużych, siedzibą hello Stanów Zjednoczonych, rozwija trasy toooffer jego operacji w hello Śródziemnego i Bałtyckiego mórz oraz hello brytyjskich.</span><span class="sxs-lookup"><span data-stu-id="53284-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="53284-109">toosupport tych działań uzyskała mniejszych rejs wiersze na podstawie we Włoszech, Niemczech, Dania i hello Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="53284-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="53284-110">Witaj firma korzysta z danych firmowych toostore Microsoft Azure w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="53284-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="53284-111">Może to obejmować pracowników i/lub klienta informacje takie jak:</span><span class="sxs-lookup"><span data-stu-id="53284-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="53284-112">adresy</span><span class="sxs-lookup"><span data-stu-id="53284-112">addresses</span></span>
- <span data-ttu-id="53284-113">Numery telefonów</span><span class="sxs-lookup"><span data-stu-id="53284-113">phone numbers</span></span>
- <span data-ttu-id="53284-114">Numery identyfikacyjne podatku</span><span class="sxs-lookup"><span data-stu-id="53284-114">tax identification numbers</span></span>
- <span data-ttu-id="53284-115">Inne informacje</span><span class="sxs-lookup"><span data-stu-id="53284-115">medical information</span></span>
- <span data-ttu-id="53284-116">informacje o karcie kredytowej</span><span class="sxs-lookup"><span data-stu-id="53284-116">credit card information</span></span>

<span data-ttu-id="53284-117">Hello firmy muszą chronić prywatność hello pracowników i klientów danych podczas przesyłania danych dostępny toothose działów, które go potrzebują.</span><span class="sxs-lookup"><span data-stu-id="53284-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="53284-118">(na przykład lista płac i zastrzeżenia działów)</span><span class="sxs-lookup"><span data-stu-id="53284-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="53284-119">wiersz rejs Hello zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność zawierający dane osobowe tootrack relacje z bieżących i starszych klientów.</span><span class="sxs-lookup"><span data-stu-id="53284-119">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="53284-120">Opis problemu</span><span class="sxs-lookup"><span data-stu-id="53284-120">Problem statement</span></span>

<span data-ttu-id="53284-121">Hello firmy muszą chronić prywatność hello pracowników i klientów danych osobowych podczas wprowadzania danych dostępny toothose działów, które go potrzebują (na przykład lista płac i zastrzeżenia działów).</span><span class="sxs-lookup"><span data-stu-id="53284-121">hello company must protect hello privacy of employees’ and customers’ personal data while making data accessible toothose departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="53284-122">Tej zapewnionej jest przechowywany poza centrum danych firmowych kontrolowane hello i nie są pod kontrolą fizycznych hello firmy.</span><span class="sxs-lookup"><span data-stu-id="53284-122">This personal data is stored outside of hello corporate-controlled data center and is not under hello company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="53284-123">Celem firmy</span><span class="sxs-lookup"><span data-stu-id="53284-123">Company goal</span></span>

<span data-ttu-id="53284-124">W ramach strategii zabezpieczeń obrony zabezpieczeń wielowarstwowy jest tooensure celem firmy, czy wszystkie źródła danych, które zawierają dane osobowe użytkownika są szyfrowane, łącznie z tymi znajdującymi się w magazynie w chmurze.</span><span class="sxs-lookup"><span data-stu-id="53284-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal tooensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="53284-125">Jeśli nieautoryzowany danych osobowych toohello dostępu korzyści osób, musi należeć do formularza, który będzie renderowany go nie można go odczytać.</span><span class="sxs-lookup"><span data-stu-id="53284-125">If unauthorized persons gain access toohello personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="53284-126">Zastosowanie szyfrowania powinna być łatwa lub przezroczyste — dla użytkowników i administratorów.</span><span class="sxs-lookup"><span data-stu-id="53284-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="53284-127">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="53284-127">Solutions</span></span>

<span data-ttu-id="53284-128">Usługi platformy Azure zapewniają wiele toohelp narzędzia i technologie ochrony danych osobowych w stanie spoczynku szyfrując go.</span><span class="sxs-lookup"><span data-stu-id="53284-128">Azure services provide multiple tools and technologies toohelp you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="53284-129">W usłudze Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="53284-129">Azure Key Vault</span></span>

<span data-ttu-id="53284-130">[Usługa Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) zapewnia bezpieczny magazyn kluczy hello używać tooencrypt danych przechowywanych w usługach Azure i hello zaleca klucza rozwiązanie pamięci masowej i zarządzania.</span><span class="sxs-lookup"><span data-stu-id="53284-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for hello keys used tooencrypt data at rest in Azure services and is hello recommended key storage and management solution.</span></span> <span data-ttu-id="53284-131">Zarządzanie kluczami szyfrowania jest istotne toosecuring przechowywanych danych.</span><span class="sxs-lookup"><span data-stu-id="53284-131">Encryption key management is essential toosecuring stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a><span data-ttu-id="53284-132">Jak używać usługi Azure Key Vault tooprotect klucze szyfrowania danych osobowych?</span><span class="sxs-lookup"><span data-stu-id="53284-132">How do I use Azure Key Vault tooprotect keys that encrypt personal data?</span></span>

<span data-ttu-id="53284-133">toouse usługi Azure Key Vault, należy tooan subskrypcji konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="53284-133">toouse Azure Key Vault, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="53284-134">Należy również zainstalować programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53284-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="53284-135">Kroki obejmują przy użyciu następujących hello toodo poleceń cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="53284-135">Steps include using PowerShell cmdlets toodo hello following:</span></span>

1. <span data-ttu-id="53284-136">Połącz tooyour subskrypcji</span><span class="sxs-lookup"><span data-stu-id="53284-136">Connect tooyour subscriptions</span></span>

2. <span data-ttu-id="53284-137">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="53284-137">Create a key vault</span></span>

3. <span data-ttu-id="53284-138">Dodawanie klucza lub magazynu kluczy tajnych toohello</span><span class="sxs-lookup"><span data-stu-id="53284-138">Add a key or secret toohello key vault</span></span>

4. <span data-ttu-id="53284-139">Rejestrowanie aplikacji używających magazynu kluczy hello usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53284-139">Register applications that will use hello key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="53284-140">Autoryzowanie hello aplikacji toouse hello klucza lub klucza tajnego</span><span class="sxs-lookup"><span data-stu-id="53284-140">Authorize hello applications toouse hello key or secret</span></span>

<span data-ttu-id="53284-141">toocreate magazyn kluczy, użyj polecenia cmdlet programu PowerShell New-AzureRmKeyVault hello.</span><span class="sxs-lookup"><span data-stu-id="53284-141">toocreate a key vault, use hello New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="53284-142">Przypisze nazwę magazynu, nazwa grupy zasobów i lokalizacji geograficznej.</span><span class="sxs-lookup"><span data-stu-id="53284-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="53284-143">Nazwa magazynu hello będą używane podczas zarządzania kluczami za pośrednictwem innych poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="53284-143">You’ll use hello vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="53284-144">Aplikacje używające magazynu hello za pomocą interfejsu API REST hello użyje magazynu hello identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="53284-144">Applications that use hello vault through hello REST API will use hello vault URI.</span></span>

<span data-ttu-id="53284-145">Usługa Azure Key Vault zapewniają klucza chronionego przez oprogramowanie dla Ciebie lub zaimportować istniejący klucz w. Plik PFX.</span><span class="sxs-lookup"><span data-stu-id="53284-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="53284-146">W magazynie hello można przechowywać klucze tajne (hasła).</span><span class="sxs-lookup"><span data-stu-id="53284-146">You can also store secrets (passwords) in hello vault.</span></span>

<span data-ttu-id="53284-147">Można również wygenerowanie klucza w lokalnym module HSM i przenieść tooHSMs w hello usługi Key Vault bez opuszczania hello granic modułu HSM klucz hello.</span><span class="sxs-lookup"><span data-stu-id="53284-147">You can also generate a key in your local HSM and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary.</span></span>

<span data-ttu-id="53284-148">Aby uzyskać szczegółowe instrukcje na temat używania usługi Azure Key Vault, wykonaj hello kroki opisane w temacie [wprowadzenie do usługi Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="53284-148">For detailed instructions on using Azure Key Vault, follow hello steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="53284-149">Aby uzyskać listę poleceń cmdlet programu PowerShell używane z usługą Azure Key Vault, zobacz [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="53284-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="53284-150">Szyfrowanie dysków Azure dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="53284-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="53284-151">[Azure szyfrowania dysku dla systemu Windows i maszyn wirtualnych systemu Linux IaaS](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) chroni dane osobowe magazynowane na maszynach wirtualnych Azure i integruje się z usługą Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="53284-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="53284-152">Używa szyfrowania dysków Azure [funkcji BitLocker](https://technet.microsoft.com/library/cc732774.aspx) w systemie Windows i [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) w systemie Linux tooencrypt hello zarówno systemu operacyjnego i hello dysków danych.</span><span class="sxs-lookup"><span data-stu-id="53284-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt both hello OS and hello data disks.</span></span> <span data-ttu-id="53284-153">Szyfrowanie dysków Azure jest obsługiwana na Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 i na klientach z systemem Windows 8 i Windows 10.</span><span class="sxs-lookup"><span data-stu-id="53284-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a><span data-ttu-id="53284-154">Jak używać danych osobowych tooprotect szyfrowania dysków Azure?</span><span class="sxs-lookup"><span data-stu-id="53284-154">How do I use Azure Disk Encryption tooprotect personal data?</span></span>

<span data-ttu-id="53284-155">toouse szyfrowania dysków Azure należy tooan subskrypcji konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="53284-155">toouse Azure Disk Encryption, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="53284-156">tooenable Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="53284-156">tooenable Azure Disk Encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="53284-157">Użyj hello Azure dysku szyfrowania szablonu usługi Resource Manager, programu PowerShell lub szyfrowanie dysków tooenable interfejsu wiersza polecenia (CLI) hello i określ konfiguracji szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="53284-157">Use hello Azure Disk Encryption Resource Manager template, PowerShell, or hello command line interface (CLI) tooenable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="53284-158">Udziel dostępu toohello platformy Azure tooread hello szyfrowania materiału z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="53284-158">Grant access toohello Azure platform tooread hello encryption material from your key vault.</span></span>

3. <span data-ttu-id="53284-159">Podaj Azure Active Directory (AAD) aplikacji tożsamości toowrite hello szyfrowania tooyour materiału klucza magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="53284-159">Provide an Azure Active Directory (AAD) application identity toowrite hello encryption key material tooyour key vault.</span></span>

<span data-ttu-id="53284-160">Azure hello maszyny Wirtualnej i konfiguracji magazynu kluczy hello aktualizacji i skonfiguruj zaszyfrowanych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53284-160">Azure will update hello VM and hello key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="53284-161">Po skonfigurowaniu toosupport Twojego magazynu kluczy szyfrowania dysków Azure można dodać klucza szyfrowania klucza (KEK), bezpieczeństwa i toosupport kopii zapasowej zaszyfrowanego maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="53284-161">When you set up your key vault toosupport Azure Disk Encryption, you can add a key encryption key (KEK) for added security and toosupport backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="53284-162">Szczegółowe instrukcje dotyczące scenariuszy wdrażania i możliwości użytkowników znajdują się w [Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span><span class="sxs-lookup"><span data-stu-id="53284-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="53284-163">Szyfrowanie usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="53284-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="53284-164">[Azure magazynu usługi szyfrowania (SSE) dla danych magazynowanych](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) pomaga chronić i chronić Twoje toomeet danych Twojej organizacji zobowiązań zabezpieczeń i zgodności.</span><span class="sxs-lookup"><span data-stu-id="53284-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="53284-165">Magazyn Azure automatycznie szyfruje dane przy użyciu toostorage toopersisting wcześniejsze szyfrowania AES 256-bitowego i odszyfrowuje je, tooretrieval wcześniejsze.</span><span class="sxs-lookup"><span data-stu-id="53284-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior toopersisting toostorage, and decrypts it prior tooretrieval.</span></span> <span data-ttu-id="53284-166">Ta usługa jest dostępna dla obiektów blob Azure i plików.</span><span class="sxs-lookup"><span data-stu-id="53284-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a><span data-ttu-id="53284-167">Jak używać danych osobowych tooprotect szyfrowanie usługi Magazyn?</span><span class="sxs-lookup"><span data-stu-id="53284-167">How do I use Storage Service Encryption tooprotect personal data?</span></span>

<span data-ttu-id="53284-168">tooenable szyfrowanie usługi Magazyn, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="53284-168">tooenable Storage Service Encryption, do hello following:</span></span>

1. <span data-ttu-id="53284-169">Zaloguj się do hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="53284-169">Log into hello Azure portal.</span></span>

2. <span data-ttu-id="53284-170">Wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="53284-170">Select a storage account.</span></span>

3. <span data-ttu-id="53284-171">W obszarze Ustawienia w sekcji usługa Blob hello, wybierz szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="53284-171">In Settings, under hello Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="53284-172">W obszarze hello sekcji usługi plików wybierz szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="53284-172">Under hello File Service section, select Encryption.</span></span>

<span data-ttu-id="53284-173">Po kliknięciu ustawienie szyfrowania hello, można włączyć lub wyłączyć szyfrowanie usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="53284-173">After you click hello Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="53284-174">Nowe dane będą szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="53284-174">New data will be encrypted.</span></span> <span data-ttu-id="53284-175">Dane w istniejących plików z tego konta magazynu pozostaną niezaszyfrowane.</span><span class="sxs-lookup"><span data-stu-id="53284-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="53284-176">Po włączeniu szyfrowania, skopiuj konto magazynu toohello danych przy użyciu jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="53284-176">After enabling encryption, copy data toohello storage account using one of hello following methods:</span></span>

1. <span data-ttu-id="53284-177">Kopiowanie obiektów blob lub pliki z hello [narzędzia wiersza polecenia AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span><span class="sxs-lookup"><span data-stu-id="53284-177">Copy blobs or files with hello [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="53284-178">[Instalowanie udziału plików, za pomocą protokołu SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) , można użyć narzędzia, takich jak pliki toocopy Robocopy.</span><span class="sxs-lookup"><span data-stu-id="53284-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy toocopy files.</span></span>

3. <span data-ttu-id="53284-179">Kopiowanie pliku lub obiektu blob danych tooand z magazynu obiektów blob lub między magazynu kont przy użyciu narzędzia [biblioteki klienta magazynu, takich jak .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="53284-179">Copy blob or file data tooand from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="53284-180">Użyj [Eksploratora usługi Storage](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooyour konta magazynu obiektów blob tooupload z włączone szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="53284-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload blobs tooyour storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="53284-181">Przezroczyste szyfrowanie danych</span><span class="sxs-lookup"><span data-stu-id="53284-181">Transparent Data Encryption</span></span>

<span data-ttu-id="53284-182">Funkcji przezroczystego szyfrowania danych (TDE) jest funkcją w usługach SQL Azure za pomocą którego można zaszyfrować dane na poziomie zarówno hello bazy danych i serwera.</span><span class="sxs-lookup"><span data-stu-id="53284-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both hello database and server levels.</span></span> <span data-ttu-id="53284-183">Funkcji TDE jest teraz włączone domyślnie na wszystkie nowo utworzone bazy danych.</span><span class="sxs-lookup"><span data-stu-id="53284-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="53284-184">Funkcji TDE wykonuje w czasie rzeczywistym we/wy szyfrowanie i odszyfrowywanie hello plików danych i dziennika.</span><span class="sxs-lookup"><span data-stu-id="53284-184">TDE performs real-time I/O encryption and decryption of hello data and log files.</span></span>

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a><span data-ttu-id="53284-185">Jak używać funkcji TDE tooprotect osobistych danych?</span><span class="sxs-lookup"><span data-stu-id="53284-185">How do I use TDE tooprotect personal data?</span></span>

<span data-ttu-id="53284-186">Za pomocą hello interfejsu API REST lub przy użyciu programu PowerShell, można skonfigurować funkcji TDE za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="53284-186">You can configure TDE through hello Azure portal, by using hello REST API, or by using PowerShell.</span></span> <span data-ttu-id="53284-187">tooenable funkcji TDE na istniejącej bazy danych przy użyciu hello Azure Portal hello następujące:</span><span class="sxs-lookup"><span data-stu-id="53284-187">tooenable TDE on an existing database using hello Azure Portal, do hello following:</span></span>

1. <span data-ttu-id="53284-188">Odwiedź hello Azure w portalu <https://portal.azure.com> i zaloguj się przy użyciu konta administratora platformy Azure lub współautora.</span><span class="sxs-lookup"><span data-stu-id="53284-188">Visit hello Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="53284-189">Na transparencie po lewej stronie powitania kliknij tooBROWSE, a następnie kliknij bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="53284-189">On hello left banner, click tooBROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="53284-190">W okienku po lewej stronie powitania bazy danych SQL kliknij bazy danych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="53284-190">With SQL databases selected in hello left pane, click your user database.</span></span>

4. <span data-ttu-id="53284-191">W bloku bazy danych hello kliknij pozycję wszystkie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="53284-191">In hello database blade, click All settings.</span></span>

5. <span data-ttu-id="53284-192">W bloku ustawienia powitania kliknij danych przezroczystego szyfrowania części tooopen hello danych przezroczystego szyfrowania blok.</span><span class="sxs-lookup"><span data-stu-id="53284-192">In hello Settings blade, click Transparent data encryption part tooopen hello Transparent data encryption blade.</span></span>

6. <span data-ttu-id="53284-193">W bloku szyfrowania danych hello, Przenieś tooOn przycisk szyfrowania danych hello, a następnie kliknij Zapisz (u góry hello strony hello) tooapply hello ustawienie.</span><span class="sxs-lookup"><span data-stu-id="53284-193">In hello Data encryption blade, move hello Data encryption button tooOn, and then click Save (at hello top of hello page) tooapply hello setting.</span></span> <span data-ttu-id="53284-194">Witaj stanu szyfrowania będzie przybliżona hello postęp hello przezroczystego szyfrowania danych.</span><span class="sxs-lookup"><span data-stu-id="53284-194">hello Encryption status will approximate hello progress of hello transparent data encryption.</span></span>

![Włączanie szyfrowania danych](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="53284-196">Instrukcje dotyczące sposobu tooenable funkcji TDE i informacji na temat odszyfrowywania chronionych funkcji TDE baz danych i inne można znaleźć w artykule hello [przezroczystego szyfrowania danych z bazy danych SQL Azure.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span><span class="sxs-lookup"><span data-stu-id="53284-196">Instructions on how tooenable TDE and information on decrypting TDE-protected databases and more can be found in hello article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="53284-197">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="53284-197">Summary</span></span>

<span data-ttu-id="53284-198">Witaj firmy można wykonywać jego celem szyfrowania danych osobowych przechowywanych w hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="53284-198">hello company can accomplish its goal of encrypting personal data stored in hello Azure cloud.</span></span> <span data-ttu-id="53284-199">Można to zrobić za pomocą szyfrowania dysków Azure zbyt chronić całą woluminów.</span><span class="sxs-lookup"><span data-stu-id="53284-199">They can do this by using Azure Disk Encryption too protect entire volumes.</span></span> <span data-ttu-id="53284-200">Może to obejmować zarówno hello pliki systemu operacyjnego, jak i plików danych, które zawierają dane osobowe i innych poufnych danych.</span><span class="sxs-lookup"><span data-stu-id="53284-200">This may include both hello operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="53284-201">Szyfrowanie usługi Magazyn Azure mogą być używane tooprotect danych osobowych, które są przechowywane w plikach i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="53284-201">Azure Storage Service encryption can be used tooprotect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="53284-202">W przypadku danych przechowywanych w bazach danych Azure SQL przezroczystego szyfrowania danych zapewnia ochronę przed nieautoryzowanym ujawnienia informacji osobistych.</span><span class="sxs-lookup"><span data-stu-id="53284-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="53284-203">tooprotect hello kluczy, które są używane tooencrypt danych na platformie Azure, hello firmy można używać usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="53284-203">tooprotect hello keys that are used tooencrypt data in Azure, hello company can use Azure Key Vault.</span></span> <span data-ttu-id="53284-204">Usprawnia to proces zarządzania kluczami hello i umożliwia hello firmy toomaintain kontrolę nad kluczami, które dostępu i szyfrowanie danych osobowych.</span><span class="sxs-lookup"><span data-stu-id="53284-204">This streamlines hello key management process and enables hello company toomaintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53284-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="53284-205">Next steps</span></span>

- [<span data-ttu-id="53284-206">Przewodnik rozwiązywania problemów szyfrowania dysków Azure</span><span class="sxs-lookup"><span data-stu-id="53284-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="53284-207">Szyfrowanie maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="53284-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="53284-208">Szyfrowanie danych w usłudze Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="53284-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="53284-209">Azure DB rozwiązania Cosmos szyfrowania bazy danych w stanie spoczynku</span><span class="sxs-lookup"><span data-stu-id="53284-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
