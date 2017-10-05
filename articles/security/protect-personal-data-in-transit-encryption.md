---
title: "Ochrona danych osobowych podczas przesyłania przy użyciu szyfrowania na platformie Azure | Dokumentacja firmy Microsoft"
description: "Ochrona danych osobowych, za pomocą szyfrowania na platformie Azure"
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
ms.openlocfilehash: 99e40b8a09a2f151e7f83fbb58bdfc00ae4b1268
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="a5425-103">Technologii szyfrowania Azure: ochrony danych osobowych podczas przesyłania przy użyciu szyfrowania</span><span class="sxs-lookup"><span data-stu-id="a5425-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="a5425-104">Ten artykuł pomoże zrozumieć i użyć technologii szyfrowania Azure do zabezpieczania danych podczas przesyłania.</span><span class="sxs-lookup"><span data-stu-id="a5425-104">This article will help you understand and use Azure encryption technologies to secure data in transit.</span></span> 

<span data-ttu-id="a5425-105">Ochrona prywatności danych osobowych podczas przekazywania przez sieć jest integralną część strategii zabezpieczeń obrony zabezpieczeń wielowarstwowy.</span><span class="sxs-lookup"><span data-stu-id="a5425-105">Protecting the privacy of personal data as it travels across the network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="a5425-106">Szyfrowanie podczas przesyłania zaprojektowano w celu zapobieżenia osoba atakująca przechwytuje transmisji mogli wyświetlić lub użyć danych.</span><span class="sxs-lookup"><span data-stu-id="a5425-106">Encryption in transit is designed to prevent an attacker who intercepts transmissions from being able to view or use the data.</span></span>

## <a name="scenario"></a><span data-ttu-id="a5425-107">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="a5425-107">Scenario</span></span>

<span data-ttu-id="a5425-108">Firma rejs dużych, siedzibą w Stanach Zjednoczonych rozwija operacjach oferowanie trasy w DS, Adriatyku i Bałtyckiego mórz, jak również brytyjskich.</span><span class="sxs-lookup"><span data-stu-id="a5425-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="a5425-109">Aby zapewnić obsługę tych działań, ustawił mniejszych rejs wiersze na podstawie we Włoszech, Niemczech, Dania i Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="a5425-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span> 

<span data-ttu-id="a5425-110">Przez firmę Microsoft Azure do przechowywania danych firmowych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a5425-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="a5425-111">Dotyczy to również dane osobowe, takich jak nazwy, adresy, numery telefonów i informacje o karcie kredytowej z jej klientów globalnych.</span><span class="sxs-lookup"><span data-stu-id="a5425-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="a5425-112">Zawiera także tradycyjnych zasobów ludzkich informacje takie jak adresy, numery telefonów, numery identyfikacyjne podatku i medyczne informacje dotyczące pracowników firmy we wszystkich lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="a5425-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="a5425-113">Wiersz rejs zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność zawierający informacje osobiste, aby śledzić relacje z bieżących i starszych klientów.</span><span class="sxs-lookup"><span data-stu-id="a5425-113">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="a5425-114">Dane osobowe klientów została wprowadzona w bazie danych w oddziałach firmy, jak i z agentów podróży na całym świecie.</span><span class="sxs-lookup"><span data-stu-id="a5425-114">Personal data of customers is entered in the database from the company’s remote offices and from travel agents located around the world.</span></span> <span data-ttu-id="a5425-115">Dokumenty zawierające informacje o kliencie są przesyłane przez sieć do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="a5425-115">Documents containing customer information are transferred across the network to Azure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="a5425-116">Opis problemu</span><span class="sxs-lookup"><span data-stu-id="a5425-116">Problem statement</span></span>

<span data-ttu-id="a5425-117">Firmy muszą chronić prywatność danych osobowych pracowników i klientów, jest przesyłane do i z usług Azure.</span><span class="sxs-lookup"><span data-stu-id="a5425-117">The company must protect the privacy of customers’ and employees’ personal data while it is in transit to and from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="a5425-118">Celem firmy</span><span class="sxs-lookup"><span data-stu-id="a5425-118">Company goal</span></span>

<span data-ttu-id="a5425-119">Celem firmy, aby upewnić się, że dane osobowe są szyfrowane, gdy poza dysku.</span><span class="sxs-lookup"><span data-stu-id="a5425-119">The company goal to ensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="a5425-120">Jeśli osoby nieupoważnione przechwycenia danych osobowych wyłączyć dysk, musi należeć do formularza, który będzie renderowany go nie można go odczytać.</span><span class="sxs-lookup"><span data-stu-id="a5425-120">If unauthorized persons intercept the off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="a5425-121">Zastosowanie szyfrowania powinna być łatwa lub całkowicie niewidoczne dla użytkowników i administratorów.</span><span class="sxs-lookup"><span data-stu-id="a5425-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="a5425-122">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="a5425-122">Solutions</span></span>

<span data-ttu-id="a5425-123">Usługi Azure zapewniają wiele narzędzia i technologie, aby pomóc w ochronie danych osobowych podczas przesyłania.</span><span class="sxs-lookup"><span data-stu-id="a5425-123">Azure services provide multiple tools and technologies to help you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="a5425-124">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a5425-124">Azure Storage</span></span>

<span data-ttu-id="a5425-125">Dane przechowywane w chmurze musi przesyłane z klientem, które mogą być fizycznie umieszczony w dowolnym miejscu na świecie, centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="a5425-125">Data that is stored in the cloud must travel from the client, which can be physically located anywhere in the world, to the Azure data center.</span></span> <span data-ttu-id="a5425-126">Po pobraniu przez użytkowników dane przesyłane ponownie, w przeciwnym kierunku.</span><span class="sxs-lookup"><span data-stu-id="a5425-126">When that data is retrieved by users, it travels again, in the opposite direction.</span></span> <span data-ttu-id="a5425-127">Dane są przesyłane za pośrednictwem publicznego Internetu jest zawsze na ryzyko przechwycenia przez osoby atakujące.</span><span class="sxs-lookup"><span data-stu-id="a5425-127">Data that is in transit over the public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="a5425-128">Należy chronić prywatność danych osobowych za pomocą szyfrowania na poziomie transportu zabezpieczyć przesyłane między lokacjami.</span><span class="sxs-lookup"><span data-stu-id="a5425-128">It is important to protect the privacy of personal data by using transport-level encryption to secure it as it moves between locations.</span></span>

<span data-ttu-id="a5425-129">Protokół HTTPS udostępnia kanał komunikacyjny bezpieczne, zaszyfrowane za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="a5425-129">The HTTPS protocol provides a secure, encrypted communications channel over the Internet.</span></span> <span data-ttu-id="a5425-130">Dostęp do obiektów w usłudze Azure Storage i podczas wywoływania interfejsów API REST używanego protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a5425-130">HTTPS should be used to access objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="a5425-131">Wymusić użycie protokołu HTTPS, korzystając z [sygnatury dostępu współdzielonego](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS), aby delegować dostęp do obiektów usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a5425-131">You enforce use of the HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) to delegate access to Azure Storage objects.</span></span> <span data-ttu-id="a5425-132">Istnieją dwa typy sygnatury dostępu Współdzielonego: sygnatury dostępu Współdzielonego usługi i konto sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="a5425-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="a5425-133">Jak utworzyć sygnatury dostępu Współdzielonego usługi?</span><span class="sxs-lookup"><span data-stu-id="a5425-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="a5425-134">Sygnatury dostępu Współdzielonego usługi deleguje dostęp do zasobów tylko w jednej z usług magazynu (usługa blob, kolejki, tabeli lub pliku).</span><span class="sxs-lookup"><span data-stu-id="a5425-134">A Service SAS delegates access to a resource in just one of the storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="a5425-135">Do utworzenia sygnatury dostępu Współdzielonego usługi, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5425-135">To construct a Service SAS, do the following:</span></span>

1. <span data-ttu-id="a5425-136">Określ pola wersji podpisem</span><span class="sxs-lookup"><span data-stu-id="a5425-136">Specify the Signed Version Field</span></span>

2. <span data-ttu-id="a5425-137">Określ zasób podpisem (obiektów Blob i tylko usługa plików)</span><span class="sxs-lookup"><span data-stu-id="a5425-137">Specify the Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="a5425-138">Określ parametry zapytania, aby zastąpić nagłówki odpowiedzi (tylko usługi obiektów Blob i plików)</span><span class="sxs-lookup"><span data-stu-id="a5425-138">Specify Query Parameters to Override Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="a5425-139">Określ nazwę tabeli (tylko usługa tabel)</span><span class="sxs-lookup"><span data-stu-id="a5425-139">Specify the Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="a5425-140">Określ zasady dostępu</span><span class="sxs-lookup"><span data-stu-id="a5425-140">Specify the Access Policy</span></span>

6. <span data-ttu-id="a5425-141">Określ okres ważności sygnatury</span><span class="sxs-lookup"><span data-stu-id="a5425-141">Specify the Signature Validity Interval</span></span>

8. <span data-ttu-id="a5425-142">Określ uprawnienia</span><span class="sxs-lookup"><span data-stu-id="a5425-142">Specify Permissions</span></span>

9. <span data-ttu-id="a5425-143">Określ adres IP lub zakres adresów IP</span><span class="sxs-lookup"><span data-stu-id="a5425-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="a5425-144">Określ protokół HTTP</span><span class="sxs-lookup"><span data-stu-id="a5425-144">Specify the HTTP Protocol</span></span>

11. <span data-ttu-id="a5425-145">Określ zakres dostępu do tabeli</span><span class="sxs-lookup"><span data-stu-id="a5425-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="a5425-146">Określ identyfikator podpisem</span><span class="sxs-lookup"><span data-stu-id="a5425-146">Specify the Signed Identifier</span></span>

13. <span data-ttu-id="a5425-147">Określ podpisu</span><span class="sxs-lookup"><span data-stu-id="a5425-147">Specify the Signature</span></span>

<span data-ttu-id="a5425-148">Aby uzyskać szczegółowe instrukcje, zobacz [konstruowania sygnatury dostępu Współdzielonego usługi](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="a5425-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="a5425-149">Jak utworzyć sygnatury dostępu Współdzielonego konta?</span><span class="sxs-lookup"><span data-stu-id="a5425-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="a5425-150">Sygnatury dostępu Współdzielonego konta deleguje dostęp do zasobów w co najmniej jednej usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="a5425-150">An Account SAS delegates access to resources in one or more of the storage services.</span></span> <span data-ttu-id="a5425-151">Możesz również delegować dostęp do operacji odczytu, zapisu i usuwania dla kontenerów obiektów blob, tabel, kolejek i udziałów plików, co jest niedozwolone w wypadku sygnatury dostępu współdzielonego usługi.</span><span class="sxs-lookup"><span data-stu-id="a5425-151">You can also delegate access to read, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="a5425-152">Konstrukcja SAS konta jest podobny do sygnatury dostępu Współdzielonego usługi.</span><span class="sxs-lookup"><span data-stu-id="a5425-152">Construction of an Account SAS is similar to that of a Service SAS.</span></span> <span data-ttu-id="a5425-153">Aby uzyskać szczegółowe instrukcje, zobacz [konstruowania SAS konta.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="a5425-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="a5425-154">Jak wymusić HTTPS podczas wywoływania interfejsów API REST?</span><span class="sxs-lookup"><span data-stu-id="a5425-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="a5425-155">Aby wymusić użycie protokołu HTTPS podczas wywoływania interfejsów API REST do dostępu do obiektów na kontach magazynu, należy włączyć bezpieczny Transfer wymagane dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="a5425-155">To enforce the use of HTTPS when calling REST APIs to access objects in storage accounts, you can enable Secure Transfer Required for the storage account.</span></span> 

1. <span data-ttu-id="a5425-156">W portalu Azure wybierz **Utwórz konto magazynu**, lub wybierz istniejące konto magazynu, **ustawienia** , a następnie **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="a5425-156">In the Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="a5425-157">W obszarze **bezpieczny Transfer wymagane**, wybierz pozycję **włączone**.</span><span class="sxs-lookup"><span data-stu-id="a5425-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Tworzenie konta magazynu](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="a5425-159">Aby uzyskać szczegółowe instrukcje, łącznie ze sposobem programowo włączyć bezpieczny Transfer wymaganego, zobacz [wymaga bezpiecznego transferu](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="a5425-159">For more detailed instructions, including how to enable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="a5425-160">Jak zaszyfrować danych w usłudze magazyn plików Azure?</span><span class="sxs-lookup"><span data-stu-id="a5425-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="a5425-161">Szyfrowanie danych przesyłanych z [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), można użyć protokołu SMB 3.x z systemu Windows 8, 8.1 i 10 i Windows Server 2012 R2 i Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a5425-161">To encrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="a5425-162">Usługa pliki Azure jest używana, każde połączenie bez szyfrowania nie powiedzie się po włączeniu "Bezpieczny transfer wymagane".</span><span class="sxs-lookup"><span data-stu-id="a5425-162">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="a5425-163">W tym scenariuszy przy użyciu protokołu SMB 2.1, SMB 3.0 bez szyfrowania i niektórych odmian klient protokołu SMB w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="a5425-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="a5425-164">Azure szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="a5425-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="a5425-165">Inną opcją w przypadku ochrony danych osobowych, gdy są przesyłane między aplikacji klienckiej i usługi Azure Storage jest [szyfrowania po stronie klienta](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="a5425-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="a5425-166">Dane są szyfrowane przed przesyłane do usługi Azure Storage, a podczas pobierania danych z usługi Azure Storage, dane zostaną odszyfrowane po odebraniu po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="a5425-166">The data is encrypted before being transferred into Azure Storage and when you retrieve the data from Azure Storage, the data is decrypted after it is received on the client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="a5425-167">Azure VPN lokacja lokacja</span><span class="sxs-lookup"><span data-stu-id="a5425-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="a5425-168">Efektywny sposób ochrony danych osobowych przesyłane między siecią firmową lub użytkownika i sieć wirtualna platformy Azure jest użycie [lokacja lokacja](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) lub [punkt lokacja](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) wirtualnej sieci prywatnej (VPN).</span><span class="sxs-lookup"><span data-stu-id="a5425-168">An effective way to protect personal data in transit between a corporate network or user and the Azure virtual network is to use a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="a5425-169">Połączenie VPN tworzy bezpieczny tunel zaszyfrowanych przez Internet.</span><span class="sxs-lookup"><span data-stu-id="a5425-169">A VPN connection creates a secure encrypted tunnel across the Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="a5425-170">Jak utworzyć połączenie VPN lokacja lokacja?</span><span class="sxs-lookup"><span data-stu-id="a5425-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="a5425-171">Sieć VPN lokacja lokacja łączy wielu użytkowników w sieci firmowej do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a5425-171">A site-to-site VPN connects multiple users on the corporate network to Azure.</span></span> <span data-ttu-id="a5425-172">Aby utworzyć połączenie lokacja lokacja, w portalu Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5425-172">To create a site-to-site connection in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="a5425-173">Tworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5425-173">Create a virtual network.</span></span>

2. <span data-ttu-id="a5425-174">Określ serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="a5425-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="a5425-175">Utwórz podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="a5425-175">Create the gateway subnet.</span></span>

4. <span data-ttu-id="a5425-176">Utwórz bramę sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="a5425-176">Create the VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="a5425-177">Utwórz bramę sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="a5425-177">Create the local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="a5425-178">Skonfiguruj urządzenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="a5425-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="a5425-179">Utwórz połączenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="a5425-179">Create the VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="a5425-180">Sprawdź połączenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="a5425-180">Verify the VPN connection.</span></span>

<span data-ttu-id="a5425-181">Aby uzyskać bardziej szczegółowe instrukcje dotyczące sposobu tworzenia połączenia lokacja lokacja w portalu Azure Zobacz [Utwórz połączenie lokacja-lokacja w portalu Azure.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="a5425-181">For more detailed instructions on how to create a site-to-site connection in the Azure portal, see [Create a Site-to-Site  connection in the Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="a5425-182">Jak utworzyć połączenie VPN punkt lokacja?</span><span class="sxs-lookup"><span data-stu-id="a5425-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="a5425-183">Sieć VPN punkt-lokacja tworzy bezpieczne połączenie z komputera klienckiego do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5425-183">A Point-to-Site VPN creates a secure connection from an individual client computer to a virtual network.</span></span> <span data-ttu-id="a5425-184">Jest to przydatne, jeśli chcesz połączyć się z platformy Azure z lokalizacji zdalnej, takich jak z domu lub konferencji w hotelach Centrum.</span><span class="sxs-lookup"><span data-stu-id="a5425-184">This is useful when you  want to connect to Azure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="a5425-185">Aby utworzyć połączenie punkt lokacja w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a5425-185">To create a point-to-site  connection in the Azure portal,</span></span>

1. <span data-ttu-id="a5425-186">Tworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5425-186">Create a virtual network.</span></span>

2. <span data-ttu-id="a5425-187">Dodaj podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="a5425-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="a5425-188">Określ serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="a5425-188">Specify a DNS server.</span></span> <span data-ttu-id="a5425-189">(opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="a5425-189">(optional)</span></span>

4. <span data-ttu-id="a5425-190">Utwórz bramę sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5425-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="a5425-191">Generowanie certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="a5425-191">Generate certificates.</span></span>

6. <span data-ttu-id="a5425-192">Dodaj pulę adresów klienta.</span><span class="sxs-lookup"><span data-stu-id="a5425-192">Add the client address pool.</span></span>

7. <span data-ttu-id="a5425-193">Przekazywanie danych certyfikatu publicznego certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="a5425-193">Upload the root certificate public certificate data.</span></span>

8. <span data-ttu-id="a5425-194">Generowanie i zainstaluj pakiet konfiguracji klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="a5425-194">Generate and install the VPN client configuration package.</span></span>

9. <span data-ttu-id="a5425-195">Zainstaluj certyfikat wyeksportowany klienta.</span><span class="sxs-lookup"><span data-stu-id="a5425-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="a5425-196">Połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="a5425-196">Connect to Azure.</span></span>

11. <span data-ttu-id="a5425-197">Weryfikowanie połączenia.</span><span class="sxs-lookup"><span data-stu-id="a5425-197">Verify your connection.</span></span>

<span data-ttu-id="a5425-198">Aby uzyskać szczegółowe instrukcje, zobacz [skonfigurować połączenie punkt-lokacja sieci wirtualnej przy użyciu uwierzytelniania certyfikatów: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="a5425-198">For more detailed instructions, see [Configure a Point-to-Site connection to a VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="a5425-199">PROTOKÓŁ SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="a5425-199">SSL/TLS</span></span>

<span data-ttu-id="a5425-200">Firma Microsoft zaleca używanie protokołów SSL/TLS do wymiany danych w różnych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="a5425-200">Microsoft recommends that you always use SSL/TLS protocols to exchange data across different locations.</span></span> <span data-ttu-id="a5425-201">Organizacje, które chce używać [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) przenoszenia dużych zestawów danych za pośrednictwem dedykowanej sieci WAN o dużej szybkości łącza można również zaszyfrować dane na poziomie aplikacji przy użyciu protokołu SSL/TLS lub innymi protokołami dla dodano ochronę.</span><span class="sxs-lookup"><span data-stu-id="a5425-201">Organizations that choose to use [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) to move large data sets over a dedicated high-speed WAN link can also encrypt the data at the application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="a5425-202">Szyfrowanie domyślnie</span><span class="sxs-lookup"><span data-stu-id="a5425-202">Encryption by default</span></span>

<span data-ttu-id="a5425-203">Firma Microsoft używa szyfrowania, aby chronić dane przesyłane między klientami i usług w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="a5425-203">Microsoft uses encryption to protect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="a5425-204">Jeśli użytkownik korzysta z usługi Azure Storage za pośrednictwem portalu Azure, wszystkich transakcji jest realizowana za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a5425-204">If you are interacting with Azure Storage through the Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="a5425-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) to protokół, który centrach danych firmy Microsoft podejmie próbę negocjowania systemach klientów łączących się z usługami w chmurze firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a5425-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is the protocol that Microsoft data centers will attempt to negotiate with client systems that connect to Microsoft cloud services.</span></span> <span data-ttu-id="a5425-206">TLS zapewnia silne uwierzytelnianie, poufność komunikatów i integralność (umożliwia wykrywanie naruszeniu wiadomości, zatrzymania oraz sfałszowaniem), współdziałanie, elastyczność algorytmów, łatwość wdrażania i używania.</span><span class="sxs-lookup"><span data-stu-id="a5425-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="a5425-207">[Udoskonalenia utajnienia](https://en.wikipedia.org/wiki/Forward_secrecy) (przekazywania PFS) jest również zastosować, dzięki czemu każdego połączenia między systemy klienckie klientów i usługi w chmurze firmy Microsoft w klucze unikatowe.</span><span class="sxs-lookup"><span data-stu-id="a5425-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="a5425-208">Połączenia usług chmurowych firmy Microsoft również korzystać na podstawie RSA 2048 bitowego szyfrowania długości kluczy.</span><span class="sxs-lookup"><span data-stu-id="a5425-208">Connections to Microsoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="a5425-209">Kombinacja protokołu TLS, długości kluczy RSA 2048-bitowych, i PFS utrudnia bardziej ktoś do przechwycenia i dostępu do danych, które są przesyłane między usługami w chmurze firmy Microsoft i klientów.</span><span class="sxs-lookup"><span data-stu-id="a5425-209">The combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone to intercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="a5425-210">Przesyłane dane są zawsze szyfrowane w [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span><span class="sxs-lookup"><span data-stu-id="a5425-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="a5425-211">Oprócz tego, że dane są szyfrowane przed zapisaniem na nośniku trwałym, są również zawsze zabezpieczane podczas przesyłania przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a5425-211">In addition to encrypting data prior to storing to persistent media, the data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="a5425-212">Protokół HTTPS jest jedynym protokołem obsługiwanym przez interfejsy REST usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a5425-212">HTTPS is the only protocol that is supported for the Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="a5425-213">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a5425-213">Summary</span></span>

<span data-ttu-id="a5425-214">Firmy mogą wykonywać jego celem ochrony danych osobowych i prywatności takich danych, wymuszając połączenia HTTPS z usługi Azure Storage, przy użyciu sygnatury dostępu współdzielonego i umożliwiające bezpieczny Transfer wymagane dla kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="a5425-214">The company can accomplish its goal of protecting personal data and the privacy of such data by enforcing HTTPS connections to Azure Storage, using Shared Access Signatures and enabling Secure Transfer Required on the storage accounts.</span></span> <span data-ttu-id="a5425-215">Mogą one również chronić dane osobiste przy użyciu połączenia protokołu SMB 3.0 i implementowanie szyfrowania po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="a5425-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="a5425-216">Połączenia sieci VPN lokacja lokacja z sieci firmowej do sieci wirtualnej platformy Azure i połączeń sieci VPN punkt lokacja z poszczególnych użytkowników będzie tworzenia bezpiecznego tunelu za pośrednictwem której można bezpiecznie przesyłane dane osobowe.</span><span class="sxs-lookup"><span data-stu-id="a5425-216">Site-to-site VPN connections from the corporate network to the Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="a5425-217">Rozwiązania szyfrowania domyślna firmy Microsoft będzie jeszcze lepiej chronić prywatność danych osobowych.</span><span class="sxs-lookup"><span data-stu-id="a5425-217">Microsoft’s default encryption practices will further protect the privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5425-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a5425-218">Next steps</span></span>

- [<span data-ttu-id="a5425-219">Dobre praktyki dotyczące zabezpieczeń danych platformy Azure i szyfrowania</span><span class="sxs-lookup"><span data-stu-id="a5425-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="a5425-220">Planowanie i projektowanie dla usługi VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="a5425-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="a5425-221">VPN Gateway — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="a5425-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="a5425-222">Kupowanie i konfigurowanie certyfikatu SSL usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="a5425-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
