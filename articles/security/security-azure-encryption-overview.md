---
title: "Omówienie szyfrowania aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o różnych opcji szyfrowania na platformie Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/18/2017
ms.author: barclayn
ms.openlocfilehash: ef9ab46de32b857e99e8fe628a61386b95cf197f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-overview"></a>Omówienie usługi Azure szyfrowania

Ten artykuł zawiera omówienie sposobu używania szyfrowania w Microsoft Azure. Obejmuje ona hello głównych obszarów szyfrowania, w tym szyfrowanie magazynowanych, szyfrowanie w locie i zarządzania kluczami z magazynu kluczy. Każda sekcja zawiera łącza do bardziej szczegółowych informacji.

## <a name="encryption-of-data-at-rest"></a>Szyfrowanie nieużywanych danych

Magazynowane dane zawierają informacje znajdują się w magazynu trwałego na nośniku fizycznym, w dowolnym formacie cyfrowym. Dotyczy to plików na nośnikach magnetycznych albo optycznych, danych archiwalnych i kopie zapasowe danych. Microsoft Azure oferuje różne toomeet rozwiązań magazynowania danych różnych potrzeb, w tym plików, dysków, obiektów blob i Magazyn tabel. Firma Microsoft udostępnia również szyfrowania tooprotect [bazy danych SQL Azure](../sql-database/sql-database-technical-overview.md), [CosmosDB](../cosmos-db/introduction.md)i usługi Azure Data Lake.

Szyfrowanie danych magazynowanych jest dostępna dla usług na hello Azure oprogramowania — jako — usługa (SaaS), platformy jako — usługa (PaaS) oraz modele chmury infrastruktury jako — usługa (IaaS). Ten dokument zawiera podsumowanie i udostępnia zasoby toohelp użyj opcji szyfrowania platformy Azure.

Aby uzyskać bardziej szczegółowe omówienie sposobu magazynowane dane są szyfrowane na platformie Azure, znajdziesz w dokumencie hello zatytułowany [danych Azure szyfrowania na Rest](azure-security-encryption-atrest.md)

## <a name="azure-encryption-models"></a>Azure modeli szyfrowania

Azure obsługuje różne modele szyfrowania, w tym szyfrowania po stronie serwera za pomocą kluczy zarządzane przez usługę, przy użyciu kluczy zarządzany przez klienta w usłudze Azure Key Vault lub klucze zarządzany przez klienta na sprzęcie kontrolowane przez klienta. Szyfrowanie po stronie klienta pozwala klucze toomanage i magazynu lokalnego w innym Zabezpiecz lokalizację.

### <a name="client-side-encryption"></a>Szyfrowania po stronie klienta

Szyfrowanie po stronie klienta jest wykonywane poza platformą Azure. Szyfrowanie po stronie klienta obejmuje:

- Danych zaszyfrowanych przez aplikację, która jest uruchomiona w centrum danych powitania klienta lub przez aplikację usługi
- Dane, które już są szyfrowane po odebraniu przez platformę Azure.

Szyfrowanie po stronie klienta dostawcy usług w chmurze hello nie ma kluczy szyfrowania toohello dostępu i nie może odszyfrować te dane. Zachować pełną kontrolę nad hello kluczy.

### <a name="server-side-encryption"></a>Szyfrowanie po stronie serwera

trzy modele szyfrowania po stronie serwera Hello oferują właściwości różnych zarządzania kluczami, które można wybrać zgodnie z wymaganiami.

- **Zarządzane przez usługę kluczy** Podaj kombinację kontroli i wygody z małym obciążeniem

- **Zarządzany przez klienta klucze** podać kontrolować hello kluczy, w tym toobring możliwości hello własnych kluczy (BYOK) lub toogenerate nowe.

- **Zarządzane przez usługę kluczy w ccustomer controlledhardware** pozwala toomanage kluczy w repozytorium zastrzeżonych, która jest poza kontrolą firmy Microsoft. Jest to Host swój własny klucz (HYOK). Jednak konfiguracja jest złożona i najbardziej Azure services nie obsługują tego modelu.

### <a name="azure-disk-encryption"></a>Usługa Azure Disk Encryption

Maszyny wirtualne systemu Windows i Linux mogą być chronione przy użyciu [szyfrowania dysków Azure](azure-security-disk-encryption.md), który używa hello [funkcji Windows BitLocker](https://technet.microsoft.com/library/cc766295(v=ws.10).aspx) technologii i Linux [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) tooprotect dysków systemu operacyjnego i dysków z danymi z szyfrowanie całego woluminu.

Szyfrowanie kluczy i kluczy tajnych są chronione w sieci [usługi Azure Key Vault](../key-vault/key-vault-whatis.md) subskrypcji. Można utworzyć kopię zapasową i przywracać zaszyfrowane maszyn wirtualnych, które są szyfrowane przy użyciu usługi Kopia zapasowa Azure hello konfiguracji KEK hello.

### <a name="azure-storage-service-encryption"></a>Szyfrowanie usługi Magazyn Azure

Dane przechowywane w magazynie Azure (obiektów Blob i pliku) mogą być szyfrowane w scenariuszach zarówno po stronie serwera i po stronie klienta.

[Szyfrowanie usługi Magazyn Azure](../storage/storage-service-encryption.md) (SSE) może automatycznie szyfrowania danych przed są przechowywane i automatycznie odszyfrowuje je, podczas pobierania, co hello przetworzyć całkowicie niewidoczne użytkowników. Szyfrowanie usługi magazynu używa 256-bitowego [szyfrowania AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), który jest jednym z hello najwyższy dostępny szyfrów bloku i obsługuje szyfrowania, odszyfrowywania i zarządzania kluczami w sposób przezroczysty.

### <a name="client-side-encryption-of-azure-blobs"></a>Szyfrowanie po stronie klienta obiekty BLOB platformy Azure

Szyfrowanie po stronie klienta obiekty BLOB platformy Azure można wykonać na różne sposoby.

Można użyć hello biblioteki klienta magazynu Azure dla danych tooencrypt pakietu NuGet programu .NET w ciągu poprzednich klienta toouploading w aplikacji go tooAzure magazynu.

więcej informacji na temat toolearn i pobierania hello biblioteki klienta magazynu Azure dla pakietu NuGet programu .NET, znajdziesz w dokumencie hello zatytułowany [systemu Windows Azure Storage 8.3.0](https://www.nuget.org/packages/WindowsAzure.Storage)

Należy używać szyfrowania po stronie klienta z usługi Azure Key Vault, dane są szyfrowane przy użyciu jednorazowego symetrycznego zawartości szyfrowania klucza (CEK) generowany przez klienta usługi Azure Storage hello zestawu SDK. Witaj CEK są szyfrowane przy użyciu klucza szyfrowania klucza (KEK), który może być klucza symetrycznego lub para kluczy asymetrycznych. Można nim zarządzać lokalnie lub zapisz go w usłudze Azure Key Vault. Witaj zaszyfrowane dane są następnie przekazywane tooAzure usługi magazynu.

więcej informacji na temat szyfrowania po stronie klienta z usługi Azure Key Vault toolearn i rozpoczynanie pracy z jak tooinstructions, zobacz dokument hello zatytułowany [samouczek: szyfrowanie i odszyfrowywanie obiektów blob w magazynie platformy Microsoft Azure przy użyciu usługi Azure Key Vault](../storage/storage-encrypt-decrypt-blobs-key-vault.md)

Ponadto umożliwia także hello biblioteki klienta magazynu Azure do szyfrowania po stronie klienta tooperform Java przed przekazaniem tooAzure magazynu i toodecrypt hello danych podczas pobierania go toohello klienta. Ta biblioteka obsługuje również integrację z [usługi Azure Key Vault](https://azure.microsoft.com/services/key-vault/) zarządzania kluczami konta magazynu.

### <a name="encryption-of-data-at-rest-with-azure-sql-database"></a>Szyfrowanie danych przechowywanych w bazie danych Azure SQL

[Baza danych SQL Azure](../sql-database/sql-database-technical-overview.md) jest ogólnego przeznaczenia relacyjnej bazy danych usługi Microsoft Azure obsługującym struktury, takich jak relacyjnej bazie danych, formatu JSON, przestrzennych i XML. Azure SQL obsługuje szyfrowanie po stronie serwera za pomocą funkcji funkcji przezroczystego szyfrowania danych (TDE) hello i szyfrowania po stronie klienta za pomocą funkcji zawsze zaszyfrowane hello.

#### <a name="transparent-data-encryption"></a>Transparent Data Encryption

[Funkcji TDE przezroczystego szyfrowania danych](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) jest używane tooencrypt [programu SQL Server](https://www.microsoft.com/sql-server/sql-server-2016), [bazy danych SQL Azure](../sql-database/sql-database-technical-overview.md), i [magazyn danych SQL Azure](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) pliki danych w czasie rzeczywistym przy użyciu klucza szyfrowania bazy danych (jeśli Istnieje), który jest przechowywany w hello rekordu rozruchowego bazy danych dostępności podczas odzyskiwania.

Funkcji TDE chroni dane i plików dziennika, przy użyciu algorytmów szyfrowania AES i algorytmu 3DES. Szyfrowanie pliku bazy danych hello jest wykonywane na poziomie strony hello; strony Hello w zaszyfrowanej bazy danych są szyfrowane, zanim zostały napisane toodisk i są odszyfrowywane, jeśli są one odczytu do pamięci. Funkcji TDE jest teraz włączone domyślnie na nowo utworzone bazy danych Azure SQL.

#### <a name="always-encrypted"></a>Zawsze szyfrowane

Witaj [zawsze zaszyfrowane](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) funkcja Azure SQL pozwala tooencrypt danych w aplikacji klienta wcześniejszych toostoring w bazie danych SQL Azure i umożliwia delegowanie tooenable toothird administracyjnej bazy danych lokalnie strony i obsługa oddzielenie tych, którzy należą i mogą wyświetlać dane hello i osób, które możesz nim zarządzać, ale nie powinny mieć dostępu tooit.

#### <a name="cellcolumn-level-encryption"></a>Szyfrowanie na poziomie kolumny/komórki

Baza danych SQL Azure umożliwia tooapply szyfrowania symetrycznego tooa kolumny danych przy użyciu języka Transact-SQL. Ta metoda jest wywoływana [komórki szyfrowania na poziomie lub szyfrowania na poziomie kolumny](https://docs.microsoft.com/sql/relational-databases/security/encryption/encrypt-a-column-of-data) (OWA), ponieważ umożliwia tooencrypt określone kolumny lub komórki nawet określonych danych z różnymi kluczami szyfrowania. Zapewnia to bardziej szczegółowego możliwość szyfrowania niż funkcji TDE, który szyfruje dane na stronach.

CLE ma wbudowane funkcje służy tooencrypt danych przy użyciu kluczy konfiguracji symetrycznej lub asymetrycznej, z hello klucz publiczny certyfikatu, lub za pomocą hasła przy użyciu algorytmu 3DES.

### <a name="cosmos-db-database-encryption"></a>Szyfrowanie bazy danych DB rozwiązania cosmos

[Azure DB rozwiązania Cosmos](../cosmos-db/database-encryption-at-rest.md) jest bazą danych globalnie rozproszone i wiele modeli firmy Microsoft. Dane użytkownika przechowywane w bazie danych rozwiązania Cosmos w pamięci trwałej (dysków SSD) są szyfrowane domyślnie; nie ma żadnych tooturn formantów tej funkcji. Szyfrowanie magazynowane jest implementowane za pomocą wielu technologii zabezpieczeń, takich jak systemy bezpiecznego magazynu kluczy, zaszyfrowanych sieci i interfejsów API usług kryptograficznych. Klucze szyfrowania są zarządzane przez firmę Microsoft i są obracane na wewnętrzne wytyczne firmy Microsoft.

### <a name="at-rest-encryption-in-azure-data-lake"></a>Szyfrowanie na rest w usłudze Azure Data Lake

[Usługa Azure Data Lake](../data-lake-store/data-lake-store-encryption.md) jest repozytorium dla przedsiębiorstw każdego typu danych zebranych w jednym miejscu wcześniejsze tooany formalną definicję schematu lub wymagania. Azure Data Lake Store obsługuje "na domyślnie" przezroczystego szyfrowania danych magazynowanych, skonfigurowanego podczas tworzenia hello Twojego konta. Domyślnie usługi Data Lake Store zarządza hello kluczy dla Ciebie, ale masz toomanage opcji hello je samodzielnie.

Trzy rodzaje klucze są używane w szyfrowania i odszyfrowywania danych: hello głównego klucza szyfrowania (MEK), dane klucza szyfrowania i klucz szyfrowania bloku (BEK). Hello MEK jest używany tooencrypt hello klucza szyfrowania danych, który jest przechowywany na nośniku trwałe, i hello BEK jest pochodną hello klucza szyfrowania danych i hello bloku danych. Jeśli zarządzasz własnych kluczy można obracać hello MEK.

## <a name="encryption-of-data-in-transit"></a>Szyfrowanie danych podczas przesyłania

System Azure oferuje wiele mechanizmów zachować poufność dane przesyłane z jednej lokalizacji tooanother.

### <a name="tlsssl-encryption-in-azure"></a>Protokoły TLS/SSL szyfrowania na platformie Azure

Firma Microsoft używa hello [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) protokołu tooprotect danych, gdy są przesyłane między hello usługi w chmurze i klientów. Centrach danych firmy Microsoft negocjowania połączenia TLS z systemami klienta, które połączenia tooAzure usług. TLS zapewnia silne uwierzytelnianie, poufność komunikatów i integralność (włączenie wykrywania naruszeniu wiadomości, przechwycenie i sfałszowaniem), współdziałanie, elastyczność algorytmów, łatwość wdrażania i używania.

[Udoskonalenia utajnienia](https://en.wikipedia.org/wiki/Forward_secrecy) (przekazywania PFS) jest chroni połączeń między systemy klienckie klientów i usługi w chmurze firmy Microsoft w klucze unikatowe. Połączenia używają również na podstawie RSA 2048 bitowego szyfrowania długości kluczy. Ta kombinacja utrudnia osobom niepowołanym toointercept i dostępu do danych podczas przesyłania danych.

### <a name="azure-storage-transactions"></a>Transakcje magazynu Azure

Gdy interakcję z usługą Azure Storage za pomocą portalu Azure hello wszystkich transakcji została wykonana za pośrednictwem protokołu HTTPS. Umożliwia także hello interfejsu API REST magazynu za pośrednictwem protokołu HTTPS toointeract z usługą Azure Storage. Podczas wywoływania metody hello interfejsów API REST tooaccess obiektów na kontach magazynu przez włączenie zapewnienia bezpiecznego transferu wymagane dla konta magazynu hello można wymusić hello korzystanie z protokołu HTTPS.

Sygnatury dostępu współdzielonego ([SAS](../storage/storage-dotnet-shared-access-signature-part-1.md)), które mogą być używane toodelegate dostępu do obiektów magazynu tooAzure, obejmują toospecify opcji tego hello tylko protokołu HTTPS, można użyć w przypadku przy użyciu sygnatury dostępu współdzielonego. Dzięki temu, że każdy wysyłanie linków z tokenami SAS używa hello odpowiedni protokół.

[Protokół SMB 3.0](https://technet.microsoft.com/library/dn551363(v=ws.11).aspx#BKMK_SMBEncryption) tooaccess używane udziały plików platformy Azure obsługuje szyfrowanie i jest dostępny w Windows Server 2012 R2, Windows 8, Windows 8.1 i Windows 10, umożliwiający dostęp między region i nawet uzyskać dostęp na pulpicie hello.

Szyfrowanie po stronie klienta szyfruje dane hello przed został wysłany tooAzure magazynu, dzięki czemu jest on zaszyfrowany podczas przekazywania przez sieć hello.

### <a name="smb-encryption-over-azure-virtual-networks"></a>Szyfrowanie protokołu SMB za pośrednictwem sieci wirtualnych platformy Azure 

[Protokół SMB 3.0](https://support.microsoft.com/help/2709568/new-smb-3-0-features-in-the-windows-server-2012-file-server) w maszynach wirtualnych platformy Azure, systemem operacyjnym Windows Server 2012 lub nowszym zapewnia hello danych toomake możliwości bezpiecznego transferu przez szyfrowanie danych przesyłanych za pośrednictwem sieci wirtualnych Azure, tooprotect przed naruszeniem i podsłuchiwaniu ataków. Administratorzy mogą włączyć szyfrowanie protokołu SMB dla całego serwera hello lub tylko określone udziały.

Domyślnie po włączeniu szyfrowania protokołu SMB dla udziału lub serwera, tylko klienci SMB 3 mogą tooaccess hello szyfrowane udziałów.

## <a name="in-transit-encryption-in-azure-virtual-machines"></a>Szyfrowanie podczas przesyłania danych na maszynach wirtualnych Azure

Dane przesyłane do z i między maszynami wirtualnymi Azure systemem Windows są szyfrowane na kilka sposobów, w zależności od charakteru hello hello połączenia.

### <a name="rdp-sessions"></a>Sesje protokołu RDP

Możesz łączyć i zaloguj się na tooan maszyna wirtualna platformy Azure przy użyciu hello [protokołu Remote Desktop Protocol](https://msdn.microsoft.com/library/aa383015(v=vs.85).aspx) (RDP) z komputerem klienckim z systemem Windows lub Mac z zainstalowanym klientem RDP. Dane przesyłane przez sieć hello w sesji protokołu RDP, może być chroniony przez protokół TLS.

Umożliwia także tooa tooconnect pulpitu zdalnego maszyny Wirtualnej systemu Linux na platformie Azure.

### <a name="secure-access-toolinux-vms-with-ssh"></a>Bezpieczny dostęp do maszyn wirtualnych tooLinux przy użyciu protokołu SSH

Można użyć [Secure Shell](../virtual-machines/linux/ssh-from-windows.md) tooLinux tooconnect (SSH) maszyn wirtualnych działających na platformie Azure do zdalnego zarządzania. SSH jest protokołem zaszyfrowanego połączenia, który umożliwia bezpiecznego logowania za pośrednictwem niezabezpieczonego połączenia. Jest hello domyślnego połączenia protokołu dla maszyn wirtualnych systemu Linux hostowanych w systemie Azure. Używanie kluczy SSH do uwierzytelniania, pozwala wyeliminować potrzebę hello toolog haseł w. Protokół SSH używa pary kluczy publiczny/prywatny (szyfrowanie asymetryczne) do uwierzytelniania.

## <a name="azure-vpn-encryption"></a>Szyfrowanie sieci VPN platformy Azure

Możesz połączyć tooAzure za pośrednictwem wirtualnej sieci prywatnej, która tworzy bezpieczny tunel tooprotect hello zasad ochrony prywatności danych hello są wysyłane przez sieć hello.

### <a name="azure-vpn-gateway"></a>Azure VPN Gateway

[Brama sieci VPN](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md) mogą być używane toosend zaszyfrowany ruch między sieci wirtualnej i lokalizacji lokalnej przez połączenie publiczny lub toosend ruchu między sieciami wirtualnymi.

Sieci VPN typu lokacja lokacja używa [IPsec](https://en.wikipedia.org/wiki/IPsec) szyfrowania transportu. Bramy sieci VPN platformy Azure, użyj zestaw propozycji domyślne. Można skonfigurować niestandardowe zasady IPsec i IKE toouse bram sieci VPN platformy Azure z określonych algorytmów kryptograficznych i kluczy sile, zamiast hello Azure domyślne zasady zestawy.

### <a name="point-to-site-vpn"></a>Sieć VPN punkt lokacja

Sieci VPN typu punkt-lokacja umożliwić komputerom klienckim poszczególnych dostępu tooan sieci wirtualnej platformy Azure. [Witaj Secure Socket Tunneling Protocol](https://technet.microsoft.com/library/2007.06.cableguy.aspx) (SSTP) jest tunel VPN hello toocreate używane i można przechodzić między nimi zapory (tunelu hello jest wyświetlana jako połączenia HTTPS). Połączenie punkt lokacja z, można użyć własnego wewnętrznego głównego infrastruktury kluczy publicznych urzędu certyfikacji.

Można skonfigurować punkt lokacja sieci VPN połączenia tooa sieć wirtualną przy użyciu hello portalu Azure z certyfikatu uwierzytelniania lub środowiska PowerShell.

toolearn więcej informacji na temat tooAzure połączenia VPN punkt lokacja sieci wirtualnych, zobacz: [skonfigurować tooa połączenie punkt-lokacja sieci wirtualnej przy użyciu uwierzytelniania certyfikacji: Azure portal](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md) i

[Skonfiguruj tooa połączenie punkt-lokacja sieci wirtualnej przy użyciu uwierzytelniania certyfikatów: środowiska PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="site-to-site-vpn"></a>Sieci VPN typu lokacja lokacja 

Połączenie bramy sieci VPN typu lokacja-lokacja jest używane tooconnect lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem tunelu VPN IPsec/IKE (IKEv1 lub IKEv2). Ten typ połączenia wymaga sieci VPN urządzeń znajdujących się lokalnie posiadających zewnętrznie połączonej publicznego tooit przypisany adres IP.

Można skonfigurować site-to-site VPN połączenia tooa sieć wirtualną przy użyciu hello portalu Azure, programu PowerShell lub hello Azure interfejsu wiersza polecenia (CLI).

Przeczytaj więcej informacji:

[Utwórz połączenie lokacja-lokacja w hello portalu Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

[Utwórz połączenie lokacja-lokacja](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

[Tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja lokacja za pomocą interfejsu wiersza polecenia](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="in-transit-encryption-in-azure-data-lake"></a>Szyfrowanie podczas przesyłania danych w usłudze Azure Data Lake

Dane przesyłane (inaczej dane w ruchu) również są zawsze szyfrowane w usłudze Data Lake Store. Ponadto tooencrypting danych przed toostoring toopersistent nośnika hello zawsze ochrona danych podczas przesyłania przy użyciu protokołu HTTPS. HTTPS jest hello tylko protokół, który jest obsługiwany w przypadku powitalne interfejsy Data Lake magazynu REST.

toolearn więcej informacji na temat szyfrowanie danych przesyłanych w usłudze Azure Data Lake, zobacz dokument hello zatytułowany [szyfrowanie danych w usłudze Azure Data Lake Store.](../data-lake-store/data-lake-store-encryption.md)

## <a name="key-management-with-azure-key-vault"></a>Zarządzanie kluczami z usługi Azure Key Vault

Bez prawidłowego ochrony i zarządzanie kluczami hello szyfrowania staje się bezużyteczny. Usługa Azure Key Vault jest zalecane rozwiązania firmy Microsoft do zarządzania i kontrolowanie dostępu tooencryption kluczy używanych przez usługi w chmurze. Można przypisać uprawnienia tooaccess kluczy tooservices lub toousers za pomocą konta usługi Azure Active Directory.

Usługa Azure Key Vault zwalnia organizacji tooconfigure potrzeby hello, zastosować poprawki i obsługa sprzętowych modułów zabezpieczeń (HSM) i zarządzania kluczami oprogramowania. Z usługi Azure Key Vault Microsoft nigdy nie widzi klucze i aplikacje nie ma bezpośredniego dostępu toothem; Możesz zachować kontrolę. Można również zaimportować lub wygenerować klucze w sprzętowych modułów zabezpieczeń.

## <a name="next-steps"></a>Następne kroki

- [Przegląd zabezpieczeń platformy Azure](security-get-started-overview.md)
- [Przegląd zabezpieczeń sieci platformy Azure](security-network-overview.md)
- [Przegląd zabezpieczeń bazy danych platformy Azure](azure-database-security-overview.md)
- [Omówienie zabezpieczeń w maszynach wirtualnych platformy Azure](security-virtual-machines-overview.md)
- [Szyfrowanie danych w spoczynku](azure-security-encryption-atrest.md)
- [Najlepsze rozwiązania z zakresu zabezpieczeń i szyfrowania danych](azure-security-data-encryption-best-practices.md)
