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
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a>Technologii szyfrowania Azure: ochrony danych osobowych podczas przesyłania przy użyciu szyfrowania

Ten artykuł pomoże zrozumieć i użyć szyfrowania Azure technologii toosecure danych podczas przesyłania. 

Ochrona prywatności hello danych osobowych przesyłane przez sieć hello jest integralną część strategii zabezpieczeń obrony zabezpieczeń wielowarstwowy. Szyfrowanie podczas przesyłania jest zaprojektowana tooprevent osoba atakująca przechwytuje transmisji jest możliwe tooview lub użyj hello danych.

## <a name="scenario"></a>Scenariusz

Firma rejs dużych, siedzibą w Stanach Zjednoczonych hello, rozwija trasy toooffer jego operacji w Śródziemnego hello, Adriatyku i Bałtyckiego mórz, jak również hello brytyjskich. toosupport tych działań uzyskała mniejszych rejs wiersze na podstawie we Włoszech Niemczech, Dania i hello Zjednoczone Królestwo 

Witaj firma korzysta z danych firmowych toostore Microsoft Azure w chmurze hello. Dotyczy to również dane osobowe, takich jak nazwy, adresy, numery telefonów i informacje o karcie kredytowej z jej klientów globalnych. Zawiera także tradycyjnych zasobów ludzkich informacje takie jak adresy, numery telefonów, numery identyfikacyjne podatku i medyczne informacje dotyczące pracowników firmy we wszystkich lokalizacjach. wiersz rejs Hello zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność zawierający dane osobowe tootrack relacje z bieżących i starszych klientów.

Dane osobowe klientów została wprowadzona w hello bazy danych z oddziałach firmy hello i podróży agentów znajduje się wokół hello world. Dokumenty zawierające informacje o kliencie są transferowane za pośrednictwem hello sieci tooAzure magazynu.

## <a name="problem-statement"></a>Opis problemu

Hello firmy muszą chronić prywatność hello klientów i danych osobistych pracowników w czasie, gdy jest w tooand przesyłanych z usług Azure.

## <a name="company-goal"></a>Celem firmy

Witaj tooensure celem firmy szyfrowanie danych osobistych, gdy poza dysku. Jeśli osoby nieupoważnione przechwycenia danych osobowych hello wyłączyć dysk, musi należeć do formularza, który będzie renderowany go nie można go odczytać. Zastosowanie szyfrowania powinna być łatwa lub całkowicie niewidoczne dla użytkowników i administratorów.

## <a name="solutions"></a>Rozwiązania

Usługi platformy Azure zapewniają wiele toohelp narzędzia i technologie ochrony przesyłanych danych osobistych.

### <a name="azure-storage"></a>Azure Storage

Dane przechowywane w chmurze hello musi przejść z powitania klienta, które mogą być fizycznie umieszczony w dowolnym miejscu w Witaj świecie toohello centrum danych Azure. Po pobraniu danych przez użytkowników, przechodzi w hello przeciwne kierunku. Dane są przesyłane za pośrednictwem hello publicznego Internetu jest zawsze na ryzyko przechwycenia przez osoby atakujące. Jest ważne tooprotect hello prywatności danych osobowych za pomocą szyfrowania na poziomie transportu toosecure, ponieważ przesyłane między lokacjami.

Witaj protokołu HTTPS zapewnia kanał komunikacyjny bezpieczne, szyfrowane przez hello Internet. HTTPS powinny być używane tooaccess obiektów w usłudze Azure Storage i podczas wywoływania interfejsów API REST. Wymuszanie użycia protokołu HTTPS hello przy użyciu [sygnatury dostępu współdzielonego](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) obiektów magazynu tooAzure dostępu toodelegate (SAS). Istnieją dwa typy sygnatury dostępu Współdzielonego: sygnatury dostępu Współdzielonego usługi i konto sygnatury dostępu Współdzielonego.

#### <a name="how-do-i-construct-a-service-sas"></a>Jak utworzyć sygnatury dostępu Współdzielonego usługi?

Sygnatury dostępu Współdzielonego usługi delegatów dostępu tooa zasobu tylko w jednej z usług magazynu hello (usługa blob, kolejki, tabeli lub pliku). tooconstruct usługi sygnatury dostępu Współdzielonego hello następujące:

1. Określ hello pole wersji podpisane

2. Określ hello zasobów podpisane (obiektów Blob i tylko usługa plików)

3. Określ parametry zapytania tooOverride nagłówki odpowiedzi (usługa Blob i tylko usługa plików)

4. Określ hello nazwy tabeli (Table usługi tylko)

5. Określ hello zasad dostępu

6. Określ hello okres ważności sygnatury

8. Określ uprawnienia

9. Określ adres IP lub zakres adresów IP

10. Określ hello protokołu HTTP

11. Określ zakres dostępu do tabeli

12. Określ hello identyfikator podpisane

13. Określ hello podpisu

Aby uzyskać szczegółowe instrukcje, zobacz [konstruowania sygnatury dostępu Współdzielonego usługi](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).

#### <a name="how-do-i-construct-an-account-sas"></a>Jak utworzyć sygnatury dostępu Współdzielonego konta?

Sygnatury dostępu Współdzielonego konta deleguje dostęp tooresources w co najmniej jednej usługi magazynu hello. Możesz również delegować dostęp tooread, zapisu i operacji usuwania kontenerów obiektów blob, tabel, kolejek i udziałów plików, które nie są dozwolone z sygnatury dostępu Współdzielonego usługi. Konstrukcja SAS konta jest podobne toothat SAS usługi. Aby uzyskać szczegółowe instrukcje, zobacz [konstruowania SAS konta.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a>Jak wymusić HTTPS podczas wywoływania interfejsów API REST?

tooenforce hello użycie protokołu HTTPS podczas wywoływania interfejsów API REST tooaccess obiektów na kontach magazynu, można włączyć bezpieczny Transfer wymagane dla konta magazynu hello. 

1. Hello portalu Azure, wybierz **Utwórz konto magazynu**, lub wybierz istniejące konto magazynu, **ustawienia** , a następnie **konfiguracji**.

2. W obszarze **bezpieczny Transfer wymagane**, wybierz pozycję **włączone**.

![Tworzenie konta magazynu](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

Aby uzyskać szczegółowe instrukcje, w tym jak tooenable bezpieczny Transfer wymagane programowo, zobacz [wymaga bezpiecznego transferu](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a>Jak zaszyfrować danych w usłudze magazyn plików Azure?

tooencrypt danych przesyłanych z [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), można użyć protokołu SMB 3.x z systemu Windows 8, 8.1 i 10 i Windows Server 2012 R2 i Windows Server 2016. Korzystając z usługi pliki Azure hello, każde połączenie bez szyfrowania nie powiedzie się, gdy "Bezpieczny transfer wymagane" jest włączona. W tym scenariuszy przy użyciu protokołu SMB 2.1, SMB 3.0 bez szyfrowania i niektórych odmian powitania klienta SMB w systemie Linux.

#### <a name="azure-client-side-encryption"></a>Azure szyfrowania po stronie klienta

Inną opcją w przypadku ochrony danych osobowych, gdy są przesyłane między aplikacji klienckiej i usługi Azure Storage jest [szyfrowania po stronie klienta](https://docs.microsoft.com/azure/storage/storage-client-side-encryption). Witaj, dane są szyfrowane przed przesyłane do usługi Azure Storage i podczas pobierania danych hello z usługi Azure Storage, hello dane zostaną odszyfrowane, po odebraniu na powitania po stronie klienta.

### <a name="azure-site-to-site-vpn"></a>Azure VPN lokacja lokacja

Dane osobowe tooprotect efektywny sposób przesyłane między siecią firmową lub użytkownika i hello sieci wirtualnej platformy Azure jest toouse [lokacja lokacja](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) lub [punkt lokacja](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) wirtualnej sieci prywatnej (VPN). Połączenie VPN tworzy bezpieczny tunel zaszyfrowanych przez hello Internet.

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a>Jak utworzyć połączenie VPN lokacja lokacja?

Sieć VPN lokacja lokacja łączy wielu użytkowników na powitania tooAzure sieci firmowej. toocreate połączenie lokacja lokacja w hello portalu Azure, hello następujące:

1. Tworzenie sieci wirtualnej.

2. Określ serwer DNS.

3. Utwórz podsieć bramy hello.

4. Utwórz hello bramy sieci VPN. 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. Utwórz bramę sieci lokalnej hello.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. Skonfiguruj urządzenie sieci VPN.

7. Utwórz połączenie sieci VPN hello.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. Sprawdź hello połączenia sieci VPN.

Aby uzyskać szczegółowe instrukcje na sposób połączenia toocreate lokacja do lokacji w hello Azure portalu, zobacz [Utwórz lokacja do lokacji połączenie hello portalu Azure.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a>Jak utworzyć połączenie VPN punkt lokacja?

Sieć VPN punkt-lokacja tworzy bezpieczne połączenie z tooa komputera klienta dla sieci wirtualnej. Jest to przydatne, jeśli chcesz tooAzure tooconnect z lokalizacji zdalnej, takich jak z domu lub konferencji w hotelach Centrum. toocreate połączenie punkt lokacja w hello portalu Azure

1. Tworzenie sieci wirtualnej.

2. Dodaj podsieć bramy.

3. Określ serwer DNS. (opcjonalnie)

4. Utwórz bramę sieci wirtualnej.

5. Generowanie certyfikatów.

6. Dodaj pulę adresów powitania klienta.

7. Przekazywanie danych certyfikatu publicznego certyfikatu głównego hello.

8. Generowanie i zainstaluj pakiet konfiguracji klienta VPN hello.

9. Zainstaluj certyfikat wyeksportowany klienta.

10. Połącz tooAzure.

11. Weryfikowanie połączenia.

Aby uzyskać szczegółowe instrukcje, zobacz [skonfigurować tooa połączenie punkt-lokacja sieci wirtualnej przy użyciu uwierzytelniania certyfikatów: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)

### <a name="ssltls"></a>PROTOKÓŁ SSL/TLS

Firma Microsoft zaleca, aby zawsze używała danych tooexchange protokołów SSL/TLS w różnych lokalizacjach. Organizacje, które wybrać toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove dużych zestawów danych za pośrednictwem dedykowanej o dużej szybkości łącza sieci WAN może także szyfrowanie danych hello hello przy użyciu protokołu SSL/TLS lub innymi protokołami zapewnia dodatkową ochronę na poziomie aplikacji.

### <a name="encryption-by-default"></a>Szyfrowanie domyślnie

Firma Microsoft używa szyfrowania tooprotect danych przesyłanych między klientami i usług w chmurze Azure. Jeśli użytkownik korzysta z usługi Azure Storage za pomocą portalu Azure hello, wszystkich transakcji jest realizowana za pośrednictwem protokołu HTTPS.

[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) to protokół hello czy centrach danych firmy Microsoft podejmie toonegotiate systemach klientów łączących tooMicrosoft usługi w chmurze. TLS zapewnia silne uwierzytelnianie, poufność komunikatów i integralność (umożliwia wykrywanie naruszeniu wiadomości, zatrzymania oraz sfałszowaniem), współdziałanie, elastyczność algorytmów, łatwość wdrażania i używania.

[Udoskonalenia utajnienia](https://en.wikipedia.org/wiki/Forward_secrecy) (przekazywania PFS) jest również zastosować, dzięki czemu każdego połączenia między systemy klienckie klientów i usługi w chmurze firmy Microsoft w klucze unikatowe. Usługi w chmurze tooMicrosoft połączeń także korzystać na podstawie RSA 2048 bitowego szyfrowania długości kluczy. Witaj Kombinacja protokołu TLS, długości kluczy RSA 2048-bitowych, i PFS utrudnia bardziej ktoś toointercept i dostępu do danych, które są przesyłane między usługami w chmurze firmy Microsoft i klientów.

Przesyłane dane są zawsze szyfrowane w [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview). Ponadto tooencrypting danych przed toostoring toopersistent nośnika hello zawsze ochrona danych podczas przesyłania przy użyciu protokołu HTTPS. HTTPS jest hello tylko protokół, który jest obsługiwany w przypadku powitalne interfejsy Data Lake magazynu REST.

## <a name="summary"></a>Podsumowanie

Witaj firmy można wykonywać jego celem ochrony prywatności danych i hello takich danych, wymuszając tooAzure połączenia HTTPS magazynów, przy użyciu sygnatury dostępu współdzielonego i umożliwiające bezpieczny Transfer wymagane na kontach magazynu hello. Mogą one również chronić dane osobiste przy użyciu połączenia protokołu SMB 3.0 i implementowanie szyfrowania po stronie klienta. Połączenia sieci VPN lokacja lokacja z hello toohello sieci firmowej sieci wirtualnej platformy Azure i połączeń sieci VPN punkt lokacja z poszczególnych użytkowników będzie tworzenia bezpiecznego tunelu za pośrednictwem której można bezpiecznie przesyłane dane osobowe. Rozwiązania szyfrowania domyślna firmy Microsoft będzie dalej chronić prywatność hello danych osobowych.

## <a name="next-steps"></a>Następne kroki

- [Dobre praktyki dotyczące zabezpieczeń danych platformy Azure i szyfrowania](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [Planowanie i projektowanie dla usługi VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [VPN Gateway — często zadawane pytania](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [Kupowanie i konfigurowanie certyfikatu SSL usługi aplikacji Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
