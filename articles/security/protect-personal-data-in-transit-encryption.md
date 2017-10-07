---
title: "dane osobowe aaaProtect podczas przesyłania przy użyciu szyfrowania na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przy użyciu szyfrowania w danych osobowych Azure tooprotect"
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
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="c75e4-103">Technologii szyfrowania Azure: ochrony danych osobowych podczas przesyłania przy użyciu szyfrowania</span><span class="sxs-lookup"><span data-stu-id="c75e4-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="c75e4-104">Ten artykuł pomoże zrozumieć i użyć szyfrowania Azure technologii toosecure danych podczas przesyłania.</span><span class="sxs-lookup"><span data-stu-id="c75e4-104">This article will help you understand and use Azure encryption technologies toosecure data in transit.</span></span> 

<span data-ttu-id="c75e4-105">Ochrona prywatności hello danych osobowych przesyłane przez sieć hello jest integralną część strategii zabezpieczeń obrony zabezpieczeń wielowarstwowy.</span><span class="sxs-lookup"><span data-stu-id="c75e4-105">Protecting hello privacy of personal data as it travels across hello network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="c75e4-106">Szyfrowanie podczas przesyłania jest zaprojektowana tooprevent osoba atakująca przechwytuje transmisji jest możliwe tooview lub użyj hello danych.</span><span class="sxs-lookup"><span data-stu-id="c75e4-106">Encryption in transit is designed tooprevent an attacker who intercepts transmissions from being able tooview or use hello data.</span></span>

## <a name="scenario"></a><span data-ttu-id="c75e4-107">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="c75e4-107">Scenario</span></span>

<span data-ttu-id="c75e4-108">Firma rejs dużych, siedzibą w Stanach Zjednoczonych hello, rozwija trasy toooffer jego operacji w Śródziemnego hello, Adriatyku i Bałtyckiego mórz, jak również hello brytyjskich.</span><span class="sxs-lookup"><span data-stu-id="c75e4-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="c75e4-109">toosupport tych działań uzyskała mniejszych rejs wiersze na podstawie we Włoszech Niemczech, Dania i hello Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="c75e4-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="c75e4-110">Witaj firma korzysta z danych firmowych toostore Microsoft Azure w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="c75e4-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="c75e4-111">Dotyczy to również dane osobowe, takich jak nazwy, adresy, numery telefonów i informacje o karcie kredytowej z jej klientów globalnych.</span><span class="sxs-lookup"><span data-stu-id="c75e4-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="c75e4-112">Zawiera także tradycyjnych zasobów ludzkich informacje takie jak adresy, numery telefonów, numery identyfikacyjne podatku i medyczne informacje dotyczące pracowników firmy we wszystkich lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="c75e4-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="c75e4-113">wiersz rejs Hello zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność zawierający dane osobowe tootrack relacje z bieżących i starszych klientów.</span><span class="sxs-lookup"><span data-stu-id="c75e4-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="c75e4-114">Dane osobowe klientów została wprowadzona w hello bazy danych z oddziałach firmy hello i podróży agentów znajduje się wokół hello world.</span><span class="sxs-lookup"><span data-stu-id="c75e4-114">Personal data of customers is entered in hello database from hello company’s remote offices and from travel agents located around hello world.</span></span> <span data-ttu-id="c75e4-115">Dokumenty zawierające informacje o kliencie są transferowane za pośrednictwem hello sieci tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="c75e4-115">Documents containing customer information are transferred across hello network tooAzure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="c75e4-116">Opis problemu</span><span class="sxs-lookup"><span data-stu-id="c75e4-116">Problem statement</span></span>

<span data-ttu-id="c75e4-117">Hello firmy muszą chronić prywatność hello klientów i danych osobistych pracowników w czasie, gdy jest w tooand przesyłanych z usług Azure.</span><span class="sxs-lookup"><span data-stu-id="c75e4-117">hello company must protect hello privacy of customers’ and employees’ personal data while it is in transit tooand from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="c75e4-118">Celem firmy</span><span class="sxs-lookup"><span data-stu-id="c75e4-118">Company goal</span></span>

<span data-ttu-id="c75e4-119">Witaj tooensure celem firmy szyfrowanie danych osobistych, gdy poza dysku.</span><span class="sxs-lookup"><span data-stu-id="c75e4-119">hello company goal tooensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="c75e4-120">Jeśli osoby nieupoważnione przechwycenia danych osobowych hello wyłączyć dysk, musi należeć do formularza, który będzie renderowany go nie można go odczytać.</span><span class="sxs-lookup"><span data-stu-id="c75e4-120">If unauthorized persons intercept hello off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="c75e4-121">Zastosowanie szyfrowania powinna być łatwa lub całkowicie niewidoczne dla użytkowników i administratorów.</span><span class="sxs-lookup"><span data-stu-id="c75e4-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="c75e4-122">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="c75e4-122">Solutions</span></span>

<span data-ttu-id="c75e4-123">Usługi platformy Azure zapewniają wiele toohelp narzędzia i technologie ochrony przesyłanych danych osobistych.</span><span class="sxs-lookup"><span data-stu-id="c75e4-123">Azure services provide multiple tools and technologies toohelp you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="c75e4-124">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c75e4-124">Azure Storage</span></span>

<span data-ttu-id="c75e4-125">Dane przechowywane w chmurze hello musi przejść z powitania klienta, które mogą być fizycznie umieszczony w dowolnym miejscu w Witaj świecie toohello centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="c75e4-125">Data that is stored in hello cloud must travel from hello client, which can be physically located anywhere in hello world, toohello Azure data center.</span></span> <span data-ttu-id="c75e4-126">Po pobraniu danych przez użytkowników, przechodzi w hello przeciwne kierunku.</span><span class="sxs-lookup"><span data-stu-id="c75e4-126">When that data is retrieved by users, it travels again, in hello opposite direction.</span></span> <span data-ttu-id="c75e4-127">Dane są przesyłane za pośrednictwem hello publicznego Internetu jest zawsze na ryzyko przechwycenia przez osoby atakujące.</span><span class="sxs-lookup"><span data-stu-id="c75e4-127">Data that is in transit over hello public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="c75e4-128">Jest ważne tooprotect hello prywatności danych osobowych za pomocą szyfrowania na poziomie transportu toosecure, ponieważ przesyłane między lokacjami.</span><span class="sxs-lookup"><span data-stu-id="c75e4-128">It is important tooprotect hello privacy of personal data by using transport-level encryption toosecure it as it moves between locations.</span></span>

<span data-ttu-id="c75e4-129">Witaj protokołu HTTPS zapewnia kanał komunikacyjny bezpieczne, szyfrowane przez hello Internet.</span><span class="sxs-lookup"><span data-stu-id="c75e4-129">hello HTTPS protocol provides a secure, encrypted communications channel over hello Internet.</span></span> <span data-ttu-id="c75e4-130">HTTPS powinny być używane tooaccess obiektów w usłudze Azure Storage i podczas wywoływania interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="c75e4-130">HTTPS should be used tooaccess objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="c75e4-131">Wymuszanie użycia protokołu HTTPS hello przy użyciu [sygnatury dostępu współdzielonego](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) obiektów magazynu tooAzure dostępu toodelegate (SAS).</span><span class="sxs-lookup"><span data-stu-id="c75e4-131">You enforce use of hello HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure Storage objects.</span></span> <span data-ttu-id="c75e4-132">Istnieją dwa typy sygnatury dostępu Współdzielonego: sygnatury dostępu Współdzielonego usługi i konto sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="c75e4-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="c75e4-133">Jak utworzyć sygnatury dostępu Współdzielonego usługi?</span><span class="sxs-lookup"><span data-stu-id="c75e4-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="c75e4-134">Sygnatury dostępu Współdzielonego usługi delegatów dostępu tooa zasobu tylko w jednej z usług magazynu hello (usługa blob, kolejki, tabeli lub pliku).</span><span class="sxs-lookup"><span data-stu-id="c75e4-134">A Service SAS delegates access tooa resource in just one of hello storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="c75e4-135">tooconstruct usługi sygnatury dostępu Współdzielonego hello następujące:</span><span class="sxs-lookup"><span data-stu-id="c75e4-135">tooconstruct a Service SAS, do hello following:</span></span>

1. <span data-ttu-id="c75e4-136">Określ hello pole wersji podpisane</span><span class="sxs-lookup"><span data-stu-id="c75e4-136">Specify hello Signed Version Field</span></span>

2. <span data-ttu-id="c75e4-137">Określ hello zasobów podpisane (obiektów Blob i tylko usługa plików)</span><span class="sxs-lookup"><span data-stu-id="c75e4-137">Specify hello Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="c75e4-138">Określ parametry zapytania tooOverride nagłówki odpowiedzi (usługa Blob i tylko usługa plików)</span><span class="sxs-lookup"><span data-stu-id="c75e4-138">Specify Query Parameters tooOverride Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="c75e4-139">Określ hello nazwy tabeli (Table usługi tylko)</span><span class="sxs-lookup"><span data-stu-id="c75e4-139">Specify hello Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="c75e4-140">Określ hello zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="c75e4-140">Specify hello Access Policy</span></span>

6. <span data-ttu-id="c75e4-141">Określ hello okres ważności sygnatury</span><span class="sxs-lookup"><span data-stu-id="c75e4-141">Specify hello Signature Validity Interval</span></span>

8. <span data-ttu-id="c75e4-142">Określ uprawnienia</span><span class="sxs-lookup"><span data-stu-id="c75e4-142">Specify Permissions</span></span>

9. <span data-ttu-id="c75e4-143">Określ adres IP lub zakres adresów IP</span><span class="sxs-lookup"><span data-stu-id="c75e4-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="c75e4-144">Określ hello protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="c75e4-144">Specify hello HTTP Protocol</span></span>

11. <span data-ttu-id="c75e4-145">Określ zakres dostępu do tabeli</span><span class="sxs-lookup"><span data-stu-id="c75e4-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="c75e4-146">Określ hello identyfikator podpisane</span><span class="sxs-lookup"><span data-stu-id="c75e4-146">Specify hello Signed Identifier</span></span>

13. <span data-ttu-id="c75e4-147">Określ hello podpisu</span><span class="sxs-lookup"><span data-stu-id="c75e4-147">Specify hello Signature</span></span>

<span data-ttu-id="c75e4-148">Aby uzyskać szczegółowe instrukcje, zobacz [konstruowania sygnatury dostępu Współdzielonego usługi](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="c75e4-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="c75e4-149">Jak utworzyć sygnatury dostępu Współdzielonego konta?</span><span class="sxs-lookup"><span data-stu-id="c75e4-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="c75e4-150">Sygnatury dostępu Współdzielonego konta deleguje dostęp tooresources w co najmniej jednej usługi magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="c75e4-150">An Account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="c75e4-151">Możesz również delegować dostęp tooread, zapisu i operacji usuwania kontenerów obiektów blob, tabel, kolejek i udziałów plików, które nie są dozwolone z sygnatury dostępu Współdzielonego usługi.</span><span class="sxs-lookup"><span data-stu-id="c75e4-151">You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="c75e4-152">Konstrukcja SAS konta jest podobne toothat SAS usługi.</span><span class="sxs-lookup"><span data-stu-id="c75e4-152">Construction of an Account SAS is similar toothat of a Service SAS.</span></span> <span data-ttu-id="c75e4-153">Aby uzyskać szczegółowe instrukcje, zobacz [konstruowania SAS konta.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="c75e4-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="c75e4-154">Jak wymusić HTTPS podczas wywoływania interfejsów API REST?</span><span class="sxs-lookup"><span data-stu-id="c75e4-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="c75e4-155">tooenforce hello użycie protokołu HTTPS podczas wywoływania interfejsów API REST tooaccess obiektów na kontach magazynu, można włączyć bezpieczny Transfer wymagane dla konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="c75e4-155">tooenforce hello use of HTTPS when calling REST APIs tooaccess objects in storage accounts, you can enable Secure Transfer Required for hello storage account.</span></span> 

1. <span data-ttu-id="c75e4-156">Hello portalu Azure, wybierz **Utwórz konto magazynu**, lub wybierz istniejące konto magazynu, **ustawienia** , a następnie **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="c75e4-156">In hello Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="c75e4-157">W obszarze **bezpieczny Transfer wymagane**, wybierz pozycję **włączone**.</span><span class="sxs-lookup"><span data-stu-id="c75e4-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Tworzenie konta magazynu](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="c75e4-159">Aby uzyskać szczegółowe instrukcje, w tym jak tooenable bezpieczny Transfer wymagane programowo, zobacz [wymaga bezpiecznego transferu](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="c75e4-159">For more detailed instructions, including how tooenable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="c75e4-160">Jak zaszyfrować danych w usłudze magazyn plików Azure?</span><span class="sxs-lookup"><span data-stu-id="c75e4-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="c75e4-161">tooencrypt danych przesyłanych z [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), można użyć protokołu SMB 3.x z systemu Windows 8, 8.1 i 10 i Windows Server 2012 R2 i Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c75e4-161">tooencrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="c75e4-162">Korzystając z usługi pliki Azure hello, każde połączenie bez szyfrowania nie powiedzie się, gdy "Bezpieczny transfer wymagane" jest włączona.</span><span class="sxs-lookup"><span data-stu-id="c75e4-162">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="c75e4-163">W tym scenariuszy przy użyciu protokołu SMB 2.1, SMB 3.0 bez szyfrowania i niektórych odmian powitania klienta SMB w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="c75e4-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="c75e4-164">Azure szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="c75e4-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="c75e4-165">Inną opcją w przypadku ochrony danych osobowych, gdy są przesyłane między aplikacji klienckiej i usługi Azure Storage jest [szyfrowania po stronie klienta](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="c75e4-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="c75e4-166">Witaj, dane są szyfrowane przed przesyłane do usługi Azure Storage i podczas pobierania danych hello z usługi Azure Storage, hello dane zostaną odszyfrowane, po odebraniu na powitania po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="c75e4-166">hello data is encrypted before being transferred into Azure Storage and when you retrieve hello data from Azure Storage, hello data is decrypted after it is received on hello client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="c75e4-167">Azure VPN lokacja lokacja</span><span class="sxs-lookup"><span data-stu-id="c75e4-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="c75e4-168">Dane osobowe tooprotect efektywny sposób przesyłane między siecią firmową lub użytkownika i hello sieci wirtualnej platformy Azure jest toouse [lokacja lokacja](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) lub [punkt lokacja](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) wirtualnej sieci prywatnej (VPN).</span><span class="sxs-lookup"><span data-stu-id="c75e4-168">An effective way tooprotect personal data in transit between a corporate network or user and hello Azure virtual network is toouse a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="c75e4-169">Połączenie VPN tworzy bezpieczny tunel zaszyfrowanych przez hello Internet.</span><span class="sxs-lookup"><span data-stu-id="c75e4-169">A VPN connection creates a secure encrypted tunnel across hello Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="c75e4-170">Jak utworzyć połączenie VPN lokacja lokacja?</span><span class="sxs-lookup"><span data-stu-id="c75e4-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="c75e4-171">Sieć VPN lokacja lokacja łączy wielu użytkowników na powitania tooAzure sieci firmowej.</span><span class="sxs-lookup"><span data-stu-id="c75e4-171">A site-to-site VPN connects multiple users on hello corporate network tooAzure.</span></span> <span data-ttu-id="c75e4-172">toocreate połączenie lokacja lokacja w hello portalu Azure, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="c75e4-172">toocreate a site-to-site connection in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="c75e4-173">Tworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c75e4-173">Create a virtual network.</span></span>

2. <span data-ttu-id="c75e4-174">Określ serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="c75e4-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="c75e4-175">Utwórz podsieć bramy hello.</span><span class="sxs-lookup"><span data-stu-id="c75e4-175">Create hello gateway subnet.</span></span>

4. <span data-ttu-id="c75e4-176">Utwórz hello bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c75e4-176">Create hello VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="c75e4-177">Utwórz bramę sieci lokalnej hello.</span><span class="sxs-lookup"><span data-stu-id="c75e4-177">Create hello local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="c75e4-178">Skonfiguruj urządzenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c75e4-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="c75e4-179">Utwórz połączenie sieci VPN hello.</span><span class="sxs-lookup"><span data-stu-id="c75e4-179">Create hello VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="c75e4-180">Sprawdź hello połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c75e4-180">Verify hello VPN connection.</span></span>

<span data-ttu-id="c75e4-181">Aby uzyskać szczegółowe instrukcje na sposób połączenia toocreate lokacja do lokacji w hello Azure portalu, zobacz [Utwórz lokacja do lokacji połączenie hello portalu Azure.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="c75e4-181">For more detailed instructions on how toocreate a site-to-site connection in hello Azure portal, see [Create a Site-to-Site  connection in hello Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="c75e4-182">Jak utworzyć połączenie VPN punkt lokacja?</span><span class="sxs-lookup"><span data-stu-id="c75e4-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="c75e4-183">Sieć VPN punkt-lokacja tworzy bezpieczne połączenie z tooa komputera klienta dla sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c75e4-183">A Point-to-Site VPN creates a secure connection from an individual client computer tooa virtual network.</span></span> <span data-ttu-id="c75e4-184">Jest to przydatne, jeśli chcesz tooAzure tooconnect z lokalizacji zdalnej, takich jak z domu lub konferencji w hotelach Centrum.</span><span class="sxs-lookup"><span data-stu-id="c75e4-184">This is useful when you  want tooconnect tooAzure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="c75e4-185">toocreate połączenie punkt lokacja w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c75e4-185">toocreate a point-to-site  connection in hello Azure portal,</span></span>

1. <span data-ttu-id="c75e4-186">Tworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c75e4-186">Create a virtual network.</span></span>

2. <span data-ttu-id="c75e4-187">Dodaj podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="c75e4-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="c75e4-188">Określ serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="c75e4-188">Specify a DNS server.</span></span> <span data-ttu-id="c75e4-189">(opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="c75e4-189">(optional)</span></span>

4. <span data-ttu-id="c75e4-190">Utwórz bramę sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c75e4-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="c75e4-191">Generowanie certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="c75e4-191">Generate certificates.</span></span>

6. <span data-ttu-id="c75e4-192">Dodaj pulę adresów powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="c75e4-192">Add hello client address pool.</span></span>

7. <span data-ttu-id="c75e4-193">Przekazywanie danych certyfikatu publicznego certyfikatu głównego hello.</span><span class="sxs-lookup"><span data-stu-id="c75e4-193">Upload hello root certificate public certificate data.</span></span>

8. <span data-ttu-id="c75e4-194">Generowanie i zainstaluj pakiet konfiguracji klienta VPN hello.</span><span class="sxs-lookup"><span data-stu-id="c75e4-194">Generate and install hello VPN client configuration package.</span></span>

9. <span data-ttu-id="c75e4-195">Zainstaluj certyfikat wyeksportowany klienta.</span><span class="sxs-lookup"><span data-stu-id="c75e4-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="c75e4-196">Połącz tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c75e4-196">Connect tooAzure.</span></span>

11. <span data-ttu-id="c75e4-197">Weryfikowanie połączenia.</span><span class="sxs-lookup"><span data-stu-id="c75e4-197">Verify your connection.</span></span>

<span data-ttu-id="c75e4-198">Aby uzyskać szczegółowe instrukcje, zobacz [skonfigurować tooa połączenie punkt-lokacja sieci wirtualnej przy użyciu uwierzytelniania certyfikatów: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="c75e4-198">For more detailed instructions, see [Configure a Point-to-Site connection tooa VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="c75e4-199">PROTOKÓŁ SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="c75e4-199">SSL/TLS</span></span>

<span data-ttu-id="c75e4-200">Firma Microsoft zaleca, aby zawsze używała danych tooexchange protokołów SSL/TLS w różnych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="c75e4-200">Microsoft recommends that you always use SSL/TLS protocols tooexchange data across different locations.</span></span> <span data-ttu-id="c75e4-201">Organizacje, które wybrać toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove dużych zestawów danych za pośrednictwem dedykowanej o dużej szybkości łącza sieci WAN może także szyfrowanie danych hello hello przy użyciu protokołu SSL/TLS lub innymi protokołami zapewnia dodatkową ochronę na poziomie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c75e4-201">Organizations that choose toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove large data sets over a dedicated high-speed WAN link can also encrypt hello data at hello application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="c75e4-202">Szyfrowanie domyślnie</span><span class="sxs-lookup"><span data-stu-id="c75e4-202">Encryption by default</span></span>

<span data-ttu-id="c75e4-203">Firma Microsoft używa szyfrowania tooprotect danych przesyłanych między klientami i usług w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="c75e4-203">Microsoft uses encryption tooprotect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="c75e4-204">Jeśli użytkownik korzysta z usługi Azure Storage za pomocą portalu Azure hello, wszystkich transakcji jest realizowana za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c75e4-204">If you are interacting with Azure Storage through hello Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="c75e4-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) to protokół hello czy centrach danych firmy Microsoft podejmie toonegotiate systemach klientów łączących tooMicrosoft usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c75e4-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is hello protocol that Microsoft data centers will attempt toonegotiate with client systems that connect tooMicrosoft cloud services.</span></span> <span data-ttu-id="c75e4-206">TLS zapewnia silne uwierzytelnianie, poufność komunikatów i integralność (umożliwia wykrywanie naruszeniu wiadomości, zatrzymania oraz sfałszowaniem), współdziałanie, elastyczność algorytmów, łatwość wdrażania i używania.</span><span class="sxs-lookup"><span data-stu-id="c75e4-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="c75e4-207">[Udoskonalenia utajnienia](https://en.wikipedia.org/wiki/Forward_secrecy) (przekazywania PFS) jest również zastosować, dzięki czemu każdego połączenia między systemy klienckie klientów i usługi w chmurze firmy Microsoft w klucze unikatowe.</span><span class="sxs-lookup"><span data-stu-id="c75e4-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="c75e4-208">Usługi w chmurze tooMicrosoft połączeń także korzystać na podstawie RSA 2048 bitowego szyfrowania długości kluczy.</span><span class="sxs-lookup"><span data-stu-id="c75e4-208">Connections tooMicrosoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="c75e4-209">Witaj Kombinacja protokołu TLS, długości kluczy RSA 2048-bitowych, i PFS utrudnia bardziej ktoś toointercept i dostępu do danych, które są przesyłane między usługami w chmurze firmy Microsoft i klientów.</span><span class="sxs-lookup"><span data-stu-id="c75e4-209">hello combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone toointercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="c75e4-210">Przesyłane dane są zawsze szyfrowane w [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span><span class="sxs-lookup"><span data-stu-id="c75e4-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="c75e4-211">Ponadto tooencrypting danych przed toostoring toopersistent nośnika hello zawsze ochrona danych podczas przesyłania przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c75e4-211">In addition tooencrypting data prior toostoring toopersistent media, hello data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="c75e4-212">HTTPS jest hello tylko protokół, który jest obsługiwany w przypadku powitalne interfejsy Data Lake magazynu REST.</span><span class="sxs-lookup"><span data-stu-id="c75e4-212">HTTPS is hello only protocol that is supported for hello Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="c75e4-213">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c75e4-213">Summary</span></span>

<span data-ttu-id="c75e4-214">Witaj firmy można wykonywać jego celem ochrony prywatności danych i hello takich danych, wymuszając tooAzure połączenia HTTPS magazynów, przy użyciu sygnatury dostępu współdzielonego i umożliwiające bezpieczny Transfer wymagane na kontach magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="c75e4-214">hello company can accomplish its goal of protecting personal data and hello privacy of such data by enforcing HTTPS connections tooAzure Storage, using Shared Access Signatures and enabling Secure Transfer Required on hello storage accounts.</span></span> <span data-ttu-id="c75e4-215">Mogą one również chronić dane osobiste przy użyciu połączenia protokołu SMB 3.0 i implementowanie szyfrowania po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="c75e4-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="c75e4-216">Połączenia sieci VPN lokacja lokacja z hello toohello sieci firmowej sieci wirtualnej platformy Azure i połączeń sieci VPN punkt lokacja z poszczególnych użytkowników będzie tworzenia bezpiecznego tunelu za pośrednictwem której można bezpiecznie przesyłane dane osobowe.</span><span class="sxs-lookup"><span data-stu-id="c75e4-216">Site-to-site VPN connections from hello corporate network toohello Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="c75e4-217">Rozwiązania szyfrowania domyślna firmy Microsoft będzie dalej chronić prywatność hello danych osobowych.</span><span class="sxs-lookup"><span data-stu-id="c75e4-217">Microsoft’s default encryption practices will further protect hello privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c75e4-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c75e4-218">Next steps</span></span>

- [<span data-ttu-id="c75e4-219">Dobre praktyki dotyczące zabezpieczeń danych platformy Azure i szyfrowania</span><span class="sxs-lookup"><span data-stu-id="c75e4-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="c75e4-220">Planowanie i projektowanie dla usługi VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="c75e4-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="c75e4-221">VPN Gateway — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="c75e4-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="c75e4-222">Kupowanie i konfigurowanie certyfikatu SSL usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="c75e4-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
