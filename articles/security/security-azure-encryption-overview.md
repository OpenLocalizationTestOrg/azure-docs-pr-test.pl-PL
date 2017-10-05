---
title: "Omówienie usługi Azure szyfrowania | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 752568747ab96bc0a9c7fc5f24ff28c3bce4e09f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-encryption-overview"></a>Omówienie usługi Azure szyfrowania

Ten artykuł zawiera omówienie sposobu używania szyfrowania w Microsoft Azure. Obejmuje ona głównych obszarów szyfrowania, w tym szyfrowanie magazynowanych, szyfrowanie w locie i zarządzania kluczami z magazynu kluczy. Każda sekcja zawiera łącza do bardziej szczegółowych informacji.

## <a name="encryption-of-data-at-rest"></a>Szyfrowanie nieużywanych danych

Magazynowane dane zawierają informacje znajdują się w magazynu trwałego na nośniku fizycznym, w dowolnym formacie cyfrowym. Dotyczy to plików na nośnikach magnetycznych albo optycznych, danych archiwalnych i kopie zapasowe danych. Microsoft Azure oferuje wiele rozwiązań magazynu danych do różnych celów, w tym plików, dysków, obiektów blob i Magazyn tabel. Firma Microsoft udostępnia również szyfrowanie w celu ochrony [bazy danych SQL Azure](../sql-database/sql-database-technical-overview.md), [CosmosDB](../cosmos-db/introduction.md)i usługi Azure Data Lake.

Szyfrowanie danych magazynowanych jest dostępna dla usług na Azure oprogramowania — jako — usługa (SaaS), platformy jako — usługa (PaaS), a infrastruktura jako — usługa (IaaS) w chmurze modeli. Ten dokument zawiera podsumowanie i udostępnia zasoby, które ułatwiają korzystanie z platformy Azure opcje szyfrowania.

Aby uzyskać bardziej szczegółowe omówienie sposobu magazynowane dane są szyfrowane na platformie Azure, zobacz dokument zatytułowany [danych Azure szyfrowania na Rest](azure-security-encryption-atrest.md)

## <a name="azure-encryption-models"></a>Azure modeli szyfrowania

Azure obsługuje różne modele szyfrowania, w tym szyfrowania po stronie serwera za pomocą kluczy zarządzane przez usługę, przy użyciu kluczy zarządzany przez klienta w usłudze Azure Key Vault lub klucze zarządzany przez klienta na sprzęcie kontrolowane przez klienta. Szyfrowanie po stronie klienta umożliwia zarządzanie i przechowywanie kluczy lokalnie lub w innym Zabezpiecz lokalizację.

### <a name="client-side-encryption"></a>Szyfrowania po stronie klienta

Szyfrowanie po stronie klienta jest wykonywane poza platformą Azure. Szyfrowanie po stronie klienta obejmuje:

- Danych zaszyfrowanych przez aplikację, która jest uruchomiona w centrum danych klienta lub przez aplikację usługi
- Dane, które już są szyfrowane po odebraniu przez platformę Azure.

Szyfrowanie po stronie klienta dostawcy usług w chmurze nie ma dostępu do kluczy szyfrowania i nie może odszyfrować te dane. Zachować pełną kontrolę nad kluczy.

### <a name="server-side-encryption"></a>Szyfrowanie po stronie serwera

Trzy modele szyfrowania po stronie serwera oferują różne zarządzania kluczami właściwości, które można wybrać zgodnie z wymaganiami.

- **Zarządzane przez usługę kluczy** Podaj kombinację kontroli i wygody z małym obciążeniem

- **Zarządzany przez klienta klucze** zapewnia kontrolę nad kluczami, łącznie z możliwością dostosowania własnych kluczy (BYOK) lub wygenerować nowe.

- **Zarządzane przez usługę kluczy w ccustomer controlledhardware** umożliwia zarządzanie kluczami w repozytorium zastrzeżonych, która jest poza kontrolą firmy Microsoft. Jest to Host swój własny klucz (HYOK). Jednak konfiguracja jest złożona i najbardziej Azure services nie obsługują tego modelu.

### <a name="azure-disk-encryption"></a>Usługa Azure Disk Encryption

Maszyny wirtualne systemu Windows i Linux mogą być chronione przy użyciu [szyfrowania dysków Azure](azure-security-disk-encryption.md), który korzysta z [funkcji Windows BitLocker](https://technet.microsoft.com/library/cc766295(v=ws.10).aspx) technologii i Linux [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) ochrony zarówno dysków systemu operacyjnego i dysków z danymi z szyfrowanie całego woluminu.

Szyfrowanie kluczy i kluczy tajnych są chronione w sieci [usługi Azure Key Vault](../key-vault/key-vault-whatis.md) subskrypcji. Można utworzyć kopię zapasową i przywracania zaszyfrowanych maszyn wirtualnych, które są szyfrowane przy użyciu konfiguracji KEK przy użyciu usługi Kopia zapasowa Azure.

### <a name="azure-storage-service-encryption"></a>Szyfrowanie usługi Magazyn Azure

Dane przechowywane w magazynie Azure (obiektów Blob i pliku) mogą być szyfrowane w scenariuszach zarówno po stronie serwera i po stronie klienta.

[Szyfrowanie usługi Magazyn Azure](../storage/storage-service-encryption.md) (SSE) może automatycznie szyfrowania danych przed są przechowywane i automatycznie odszyfrowuje je, gdy można pobrać, co użytkownicy całkowicie niewidoczne procesu. Szyfrowanie usługi magazynu używa 256-bitowego [szyfrowania AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), które jest jednym z bloku najwyższy szyfry dostępne i obsługuje szyfrowania, odszyfrowywania i zarządzania kluczami w sposób przezroczysty.

### <a name="client-side-encryption-of-azure-blobs"></a>Szyfrowanie po stronie klienta obiekty BLOB platformy Azure

Szyfrowanie po stronie klienta obiekty BLOB platformy Azure można wykonać na różne sposoby.

Biblioteka klienta magazynu Azure dla pakietu NuGet programu .NET umożliwia szyfrowanie danych w aplikacjach klienckich przed przesłaniem go do magazynu Azure.

Aby dowiedzieć się więcej o i pobrać biblioteki klienta magazynu Azure dla pakietu NuGet programu .NET, można znaleźć w dokumencie zatytułowany [systemu Windows Azure Storage 8.3.0](https://www.nuget.org/packages/WindowsAzure.Storage)

Należy używać szyfrowania po stronie klienta z usługi Azure Key Vault, dane są szyfrowane przy użyciu jednorazowego symetrycznego zawartości szyfrowania klucza (CEK) generowany przez zestaw SDK klienta usługi Azure Storage. CEK są szyfrowane przy użyciu klucza szyfrowania klucza (KEK), który może być klucza symetrycznego lub para kluczy asymetrycznych. Można nim zarządzać lokalnie lub zapisz go w usłudze Azure Key Vault. Zaszyfrowane dane są następnie przekazywane do usługi Azure Storage.

Aby dowiedzieć się więcej na temat szyfrowania po stronie klienta z usługi Azure Key Vault i wprowadzenie do praktycznych instrukcji, można znaleźć w dokumencie zatytułowany [samouczek: szyfrowanie i odszyfrowywanie obiektów blob w magazynie platformy Microsoft Azure przy użyciu usługi Azure Key Vault](../storage/storage-encrypt-decrypt-blobs-key-vault.md)

Ponadto umożliwia także biblioteki klienta usługi Azure Storage dla języka Java przeprowadzić szyfrowania po stronie klienta przed przekazywanie danych do magazynu Azure oraz do odszyfrowania danych podczas pobierania go do klienta. Ta biblioteka obsługuje również integrację z [usługi Azure Key Vault](https://azure.microsoft.com/services/key-vault/) zarządzania kluczami konta magazynu.

### <a name="encryption-of-data-at-rest-with-azure-sql-database"></a>Szyfrowanie danych przechowywanych w bazie danych Azure SQL

[Baza danych SQL Azure](../sql-database/sql-database-technical-overview.md) jest ogólnego przeznaczenia relacyjnej bazy danych usługi Microsoft Azure obsługującym struktury, takich jak relacyjnej bazie danych, formatu JSON, przestrzennych i XML. Azure SQL obsługuje szyfrowanie po stronie serwera za pomocą funkcji funkcji przezroczystego szyfrowania danych (TDE) i szyfrowania po stronie klienta za pomocą funkcji zawsze szyfrowane.

#### <a name="transparent-data-encryption"></a>Transparent Data Encryption

[Funkcji TDE przezroczystego szyfrowania danych](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) jest używany do szyfrowania [programu SQL Server](https://www.microsoft.com/sql-server/sql-server-2016), [bazy danych SQL Azure](../sql-database/sql-database-technical-overview.md), i [magazyn danych SQL Azure](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) pliki danych w czasie rzeczywistym, przy użyciu klucza szyfrowania bazy danych (jeśli Istnieje), który jest przechowywany w bazie danych rozruchu rekordu dostępności podczas odzyskiwania.

Funkcji TDE chroni dane i plików dziennika, przy użyciu algorytmów szyfrowania AES i algorytmu 3DES. Szyfrowanie pliku bazy danych jest wykonywane na poziomie strony. strony w zaszyfrowanej bazy danych są szyfrowane, zanim są one zapisywane na dysku i są odszyfrowywane, jeśli są one odczytu do pamięci. Funkcji TDE jest teraz włączone domyślnie na nowo utworzone bazy danych Azure SQL.

#### <a name="always-encrypted"></a>Zawsze szyfrowane

[Zawsze zaszyfrowane](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) funkcji SQL Azure umożliwia szyfrowanie danych w aplikacjach klienckich przed przechowywania w bazie danych SQL Azure i umożliwia włączanie delegowania administrowania bazy danych lokalnych do udzielania podmiotom trzecim i obsługa oddzielenie tych, którzy należą i mogą wyświetlać dane i osób, które możesz nim zarządzać, ale nie powinny mieć dostępu do niego.

#### <a name="cellcolumn-level-encryption"></a>Szyfrowanie na poziomie kolumny/komórki

Baza danych SQL Azure umożliwia zastosowanie szyfrowania symetrycznego z kolumną zawierającą dane przy użyciu języka Transact-SQL. Ta metoda jest wywoływana [komórki szyfrowania na poziomie lub szyfrowania na poziomie kolumny](https://docs.microsoft.com/sql/relational-databases/security/encryption/encrypt-a-column-of-data) (OWA), ponieważ służy do szyfrowania określone kolumny lub komórki nawet określonych danych z różnymi kluczami szyfrowania. Zapewnia to bardziej szczegółowego możliwość szyfrowania niż funkcji TDE, który szyfruje dane na stronach.

CLE ma wbudowane funkcje, które służy do szyfrowania danych przy użyciu kluczy konfiguracji symetrycznej lub asymetrycznej, z kluczem publicznym certyfikatu lub za pomocą hasła przy użyciu algorytmu 3DES.

### <a name="cosmos-db-database-encryption"></a>Szyfrowanie bazy danych DB rozwiązania cosmos

[Azure DB rozwiązania Cosmos](../cosmos-db/database-encryption-at-rest.md) jest bazą danych globalnie rozproszone i wiele modeli firmy Microsoft. Dane użytkownika przechowywane w bazie danych rozwiązania Cosmos w pamięci trwałej (dysków SSD) są szyfrowane domyślnie; nie istnieją żadne formanty, aby ją włączyć lub wyłączyć. Szyfrowanie magazynowane jest implementowane za pomocą wielu technologii zabezpieczeń, takich jak systemy bezpiecznego magazynu kluczy, zaszyfrowanych sieci i interfejsów API usług kryptograficznych. Klucze szyfrowania są zarządzane przez firmę Microsoft i są obracane na wewnętrzne wytyczne firmy Microsoft.

### <a name="at-rest-encryption-in-azure-data-lake"></a>Szyfrowanie na rest w usłudze Azure Data Lake

[Usługa Azure Data Lake](../data-lake-store/data-lake-store-encryption.md) repozytorium dla przedsiębiorstw każdego typu danych zebranych w jednym miejscu przed żadnych formalnych definicji schematu lub wymagania. Azure Data Lake Store obsługuje "na domyślnie" przezroczystego szyfrowania danych magazynowanych, który jest definiowany podczas tworzenia konta. Domyślnie usługi Data Lake Store zarządza kluczy, ale istnieje możliwość zarządzania nimi samodzielnie.

Trzy rodzaje klucze są używane w szyfrowania i odszyfrowywania danych: klucz szyfrowania głównego (MEK), dane klucza szyfrowania i bloku klucza szyfrowania (BEK). MEK jest używany do szyfrowania klucza szyfrowania danych, który jest przechowywany na nośniku trwałe, a BEK jest określana na podstawie klucza szyfrowania danych i blok danych. Jeśli zarządzasz własnych kluczy można obracać MEK.

## <a name="encryption-of-data-in-transit"></a>Szyfrowanie danych podczas przesyłania

System Azure oferuje wiele mechanizmów zachować poufność dane przesyłane z jednej lokalizacji do innej.

### <a name="tlsssl-encryption-in-azure"></a>Protokoły TLS/SSL szyfrowania na platformie Azure

Firma Microsoft używa [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) protokołów (TLS) do ochrony danych, gdy są przesyłane między usługami w chmurze i klientów. Centrach danych firmy Microsoft negocjowania połączenia TLS w systemach klienckich łączących się z usługami Azure. TLS zapewnia silne uwierzytelnianie, poufność komunikatów i integralność (włączenie wykrywania naruszeniu wiadomości, przechwycenie i sfałszowaniem), współdziałanie, elastyczność algorytmów, łatwość wdrażania i używania.

[Udoskonalenia utajnienia](https://en.wikipedia.org/wiki/Forward_secrecy) (przekazywania PFS) jest chroni połączeń między systemy klienckie klientów i usługi w chmurze firmy Microsoft w klucze unikatowe. Połączenia używają również na podstawie RSA 2048 bitowego szyfrowania długości kluczy. Ta kombinacja utrudnia osobom niepowołanym do przechwycenia i dostępu do danych podczas przesyłania danych.

### <a name="azure-storage-transactions"></a>Transakcje magazynu Azure

Gdy interakcję z usługą Azure Storage za pomocą portalu Azure wszystkich transakcji została wykonana za pośrednictwem protokołu HTTPS. Umożliwia także interfejsu API REST magazynu za pośrednictwem protokołu HTTPS do interakcji z usługą Azure Storage. Podczas wywoływania interfejsów API REST do dostępu do obiektów na kontach magazynu przez włączenie zapewnienia bezpiecznego transferu wymagane dla konta magazynu, można wymusić użycie protokołu HTTPS.

Sygnatury dostępu współdzielonego ([SAS](../storage/storage-dotnet-shared-access-signature-part-1.md)), które mogą służyć do delegować dostęp do obiektów usługi Azure Storage, obejmują opcję, aby określić, że mogą być używane tylko z protokołu HTTPS przy użyciu sygnatury dostępu współdzielonego. Dzięki temu, że każdy wysyłanie linków z tokenami SAS używa odpowiedni protokół.

[Protokół SMB 3.0](https://technet.microsoft.com/library/dn551363(v=ws.11).aspx#BKMK_SMBEncryption) umożliwia dostęp do udziałów plików Azure obsługuje szyfrowania i jego dostępne w systemu Windows Server 2012 R2, Windows 8, Windows 8.1 i Windows 10, zezwalania na dostęp między region, a nawet dostęp na pulpicie.

Szyfrowanie po stronie klienta dane są szyfrowane przed wysłaniem do magazynu Azure, dzięki czemu jest on zaszyfrowany podczas przekazywania przez sieć.

### <a name="smb-encryption-over-azure-virtual-networks"></a>Szyfrowanie protokołu SMB za pośrednictwem sieci wirtualnych platformy Azure 

[Protokół SMB 3.0](https://support.microsoft.com/help/2709568/new-smb-3-0-features-in-the-windows-server-2012-file-server) w maszynach wirtualnych platformy Azure z systemem Windows Server 2012 i nowszych daje możliwość zapewnienia bezpiecznego transferu przez szyfrowanie danych przesyłanych za pośrednictwem sieci wirtualnych Azure, aby chronić przed naruszeniem i podsłuchiwaniu ataków danych. Administratorzy mogą włączyć szyfrowanie protokołu SMB dla całego serwera lub tylko określone udziały.

Domyślnie po włączeniu szyfrowania protokołu SMB dla udziału lub serwera, tylko klienci SMB 3 mogą uzyskać dostęp do zaszyfrowanych udziałów.

## <a name="in-transit-encryption-in-azure-virtual-machines"></a>Szyfrowanie podczas przesyłania danych na maszynach wirtualnych Azure

Dane przesyłane do z i między maszynami wirtualnymi Azure systemem Windows są szyfrowane na kilka sposobów, w zależności od rodzaju połączenia.

### <a name="rdp-sessions"></a>Sesje protokołu RDP

Możesz łączyć i zaloguj się do maszyny Wirtualnej platformy Azure przy użyciu [protokołu Remote Desktop Protocol](https://msdn.microsoft.com/library/aa383015(v=vs.85).aspx) (RDP) z komputerem klienckim z systemem Windows lub Mac z zainstalowanym klientem RDP. Dane przesyłane przez sieć w sesji protokołu RDP, może być chroniony przez protokół TLS.

Pulpit zdalny umożliwia również połączenie z maszyną wirtualną systemu Linux na platformie Azure.

### <a name="secure-access-to-linux-vms-with-ssh"></a>Bezpieczny dostęp do maszyn wirtualnych systemu Linux przy użyciu protokołu SSH

Można użyć [Secure Shell](../virtual-machines/linux/ssh-from-windows.md) (SSH), aby nawiązać połączenie maszyn wirtualnych systemu Linux działających na platformie Azure do zdalnego zarządzania. SSH jest protokołem zaszyfrowanego połączenia, który umożliwia bezpiecznego logowania za pośrednictwem niezabezpieczonego połączenia. Jest domyślnym protokołem połączenia dla maszyn wirtualnych systemu Linux hostowanych w systemie Azure. Używanie kluczy SSH do uwierzytelniania, pozwala uniknąć haseł do logowania. Protokół SSH używa pary kluczy publiczny/prywatny (szyfrowanie asymetryczne) do uwierzytelniania.

## <a name="azure-vpn-encryption"></a>Szyfrowanie sieci VPN platformy Azure

Azure można nawiązać za pośrednictwem wirtualnej sieci prywatnej, która tworzy bezpieczny tunel, aby chronić prywatność danych są wysyłane przez sieć.

### <a name="azure-vpn-gateway"></a>Azure VPN Gateway

[Brama sieci VPN](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md) może służyć do wysyłania zaszyfrowanych ruch między sieci wirtualnej i Twojej lokalizacji lokalnej w publicznego połączenia lub na wysyłanie ruchu między sieciami wirtualnymi.

Sieci VPN typu lokacja lokacja używa [IPsec](https://en.wikipedia.org/wiki/IPsec) szyfrowania transportu. Bramy sieci VPN platformy Azure, użyj zestaw propozycji domyślne. Można skonfigurować bramy sieci VPN platformy Azure do niestandardowych zasad IPsec i IKE za pomocą określonych algorytmów kryptograficznych i kluczy sile, a nie ustawia zasad domyślnych Azure.

### <a name="point-to-site-vpn"></a>Sieć VPN punkt lokacja

Sieci VPN typu punkt-lokacja Zezwalaj klienta komputerom dostęp do sieci wirtualnej platformy Azure. [Secure Socket Tunneling Protocol](https://technet.microsoft.com/library/2007.06.cableguy.aspx) (SSTP) służy do tworzenia tunelu VPN i można przechodzić między nimi zapory (tunelu jest wyświetlana jako połączenia HTTPS). Połączenie punkt lokacja z, można użyć własnego wewnętrznego głównego infrastruktury kluczy publicznych urzędu certyfikacji.

Można skonfigurować połączenia sieci VPN punkt lokacja, aby sieć wirtualną przy użyciu portalu Azure z certyfikatu uwierzytelniania lub środowiska PowerShell.

Aby dowiedzieć się więcej na temat połączeń sieci VPN typu punkt lokacja sieci wirtualnych platformy Azure, zobacz: [skonfigurowano połączenia punkt-lokacja z sieci wirtualnej przy użyciu uwierzytelniania certyfikacji: Azure portal](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md) i

[Skonfiguruj połączenie punkt-lokacja sieci wirtualnej przy użyciu uwierzytelniania certyfikatów: środowiska PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="site-to-site-vpn"></a>Sieci VPN typu lokacja lokacja 

Połączenie bramy sieci VPN typu lokacja-lokacja umożliwia łączenie sieci lokalnej z siecią wirtualną platformy Azure za pośrednictwem tunelu sieci VPN IPsec/IKE (IKEv1 lub IKEv2). Ten typ połączenia wymaga lokalnego urządzenia sieci VPN z przypisanym publicznym adresem IP dostępnym z zewnątrz.

Można skonfigurować połączenia sieci VPN lokacja lokacja, aby sieć wirtualną przy użyciu portalu Azure, programu PowerShell lub interfejsu wiersza polecenia platformy Azure (CLI).

Przeczytaj więcej informacji:

[Utwórz połączenie lokacja-lokacja w portalu Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

[Utwórz połączenie lokacja-lokacja](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

[Tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja lokacja za pomocą interfejsu wiersza polecenia](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="in-transit-encryption-in-azure-data-lake"></a>Szyfrowanie podczas przesyłania danych w usłudze Azure Data Lake

Dane przesyłane (inaczej dane w ruchu) również są zawsze szyfrowane w usłudze Data Lake Store. Oprócz tego, że dane są szyfrowane przed zapisaniem na nośniku trwałym, są również zawsze zabezpieczane podczas przesyłania przy użyciu protokołu HTTPS. Protokół HTTPS jest jedynym protokołem obsługiwanym przez interfejsy REST usługi Data Lake Store.

Aby dowiedzieć się więcej na temat szyfrowanie danych przesyłanych w usłudze Azure Data Lake, zobacz dokument zatytułowany [szyfrowanie danych w usłudze Azure Data Lake Store.](../data-lake-store/data-lake-store-encryption.md)

## <a name="key-management-with-azure-key-vault"></a>Zarządzanie kluczami z usługi Azure Key Vault

Bez prawidłowego ochrony i zarządzanie kluczami szyfrowania staje się bezużyteczny. Usługa Azure Key Vault jest zalecane rozwiązania firmy Microsoft do zarządzania i kontrolowanie dostępu do kluczy szyfrowania używanych przez usługi w chmurze. Można przypisać uprawnienia do klucze dostępu do usług lub użytkowników za pomocą konta usługi Azure Active Directory.

Usługa Azure Key Vault zwalnia organizacji trzeba skonfigurować, zastosować poprawki i obsługa sprzętowych modułów zabezpieczeń (HSM) i zarządzania kluczami oprogramowania. Z usługi Azure Key Vault Microsoft nigdy nie widzi klucze i aplikacje nie ma bezpośredniego dostępu do nich. Możesz zachować kontrolę. Można również zaimportować lub wygenerować klucze w sprzętowych modułów zabezpieczeń.

## <a name="next-steps"></a>Następne kroki

- [Przegląd zabezpieczeń platformy Azure](security-get-started-overview.md)
- [Przegląd zabezpieczeń sieci platformy Azure](security-network-overview.md)
- [Przegląd zabezpieczeń bazy danych platformy Azure](azure-database-security-overview.md)
- [Omówienie zabezpieczeń w maszynach wirtualnych platformy Azure](security-virtual-machines-overview.md)
- [Szyfrowanie danych w spoczynku](azure-security-encryption-atrest.md)
- [Najlepsze rozwiązania z zakresu zabezpieczeń i szyfrowania danych](azure-security-data-encryption-best-practices.md)
