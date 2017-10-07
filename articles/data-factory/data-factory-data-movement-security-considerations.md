---
title: "aaaSecurity zagadnienia dotyczące przenoszenia danych z fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zabezpieczania przenoszenia danych z fabryki danych Azure."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 4bfce8884df14ad5b94e28ad3dfcf7025e2130a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---security-considerations-for-data-movement"></a>Fabryka danych Azure — zagadnienia dotyczące zabezpieczeń dla przepływu danych
## <a name="introduction"></a>Wprowadzenie
W tym artykule opisano infrastrukturę podstawowych zabezpieczeń, że usługi przenoszenia danych z fabryki danych Azure używać toosecure danych. Zasoby dotyczące zarządzania fabryki danych Azure są tworzone w infrastrukturze zabezpieczeń platformy Azure i użyj wszystkich możliwych zabezpieczenia oferowanych na platformie Azure.

W ramach rozwiązania fabryki danych jest tworzony co najmniej jeden [potok](data-factory-create-pipelines.md) danych. Potoki to logiczne grupy działań, które wspólnie wykonują zadanie. Potoki te znajdują się w regionie hello, w której został utworzony hello fabryki danych. 

Mimo że fabryki danych jest dostępna tylko w **zachodnie stany USA**, **wschodnie stany USA**, i **Europa Północna** regionach, jest dostępna usługa przenoszenia danych hello [globalnie w kilka obszarów](data-factory-data-movement-activities.md#global). Fabryka danych, które usługa gwarantuje, że dane, nie pozostawi obszaru geograficznego / regionu, chyba że jawnie poinstruować hello toouse usługi alternatywny region Jeśli usługa przenoszenia danych hello nie jest jeszcze wdrożone toothat regionu. 

Fabryka danych Azure, sam nie przechowuje żadnych danych, z wyjątkiem poświadczeń połączonej usługi dla magazynów danych chmury, które są szyfrowane za pomocą certyfikatów. Umożliwia tworzenie przepływów pracy z danymi tooorchestrate przepływu danych między [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) i przetwarzania danych przy użyciu [obliczeniowe usług](data-factory-compute-linked-services.md) w innych regionów lub lokalnego środowisko. Umożliwia ona również zbyt[monitorować i zarządzać nimi przepływy pracy](data-factory-monitor-manage-pipelines.md) za pomocą obu programowych i mechanizmów interfejsu użytkownika.

Przenoszenie danych przy użyciu fabryki danych Azure została **certyfikowane** dla:
-   [HIPAA/HITECH](https://www.microsoft.com/en-us/trustcenter/Compliance/HIPAA)  
-   [ISO/IEC 27001](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27001)  
-   [ISO/IEC 27018](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27018) 
-   [CSA GWIAZDY](https://www.microsoft.com/en-us/trustcenter/Compliance/CSA-STAR-Certification)
     
Jeśli interesuje Cię zgodności platformy Azure i jak Azure zabezpiecza własnej infrastruktury, odwiedź hello [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx). 

W tym artykule firma Microsoft analizuje zagadnienia dotyczące zabezpieczeń w hello następujące dwa scenariusze przepływu danych: 

- **Scenariusz chmury**— w tym scenariuszu źródłowym i docelowym są publicznie dostępny za pośrednictwem Internetu. Obejmują one usługi magazynu w chmurze zarządzanych, takich jak usługi Azure Storage, Magazyn danych SQL Azure, baza danych SQL Azure, Azure Data Lake Store, Amazon S3, Amazon Redshift, usługi SaaS, takie jak Salesforce i protokoły sieci web, takich jak FTP i OData. Pełną listę obsługiwanych źródeł danych można znaleźć [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- **Scenariusza hybrydowego**— w tym scenariuszu źródłowe lub docelowe znajduje się za zaporą lub w firmowej sieci lub hello danych lokalnych magazyn jest w sieci prywatnej / wirtualnych sieci (w większości przypadków hello źródła) i nie jest dostępny publicznie element . W tym scenariuszu dzielą się również hostowanych na maszynach wirtualnych serwerów bazy danych.

## <a name="cloud-scenarios"></a>Scenariusze chmury
###<a name="securing-data-store-credentials"></a>Zabezpieczanie poświadczeń magazynu danych
Fabryka danych Azure chroni poświadczeń magazynu danych przez **szyfrowania** je za pomocą **certyfikaty zarządzany przez firmę Microsoft**. Te certyfikaty są obracane co **dwuletni** (w tym migracja poświadczeń i odnawiania certyfikatów). Te zaszyfrowane poświadczenia są bezpiecznie przechowywane w **magazyn Azure zarządzanych przez usługi zarządzania fabryki danych Azure**. Aby uzyskać więcej informacji na temat zabezpieczeń usługi Azure Storage można znaleźć [Omówienie zabezpieczeń magazynu Azure](../security/security-storage-overview.md).

### <a name="data-encryption-in-transit"></a>Szyfrowanie danych podczas przesyłania
Jeśli magazyn danych w chmurze hello obsługuje protokół HTTPS lub TLS, wszystkie dane transferu między usługi przenoszenia danych z fabryki danych i magazynu danych w chmurze są za pośrednictwem bezpiecznego kanału HTTPS lub TLS.

> [!NOTE]
> Wszystkie połączenia zbyt**bazy danych SQL Azure** i **magazyn danych SQL Azure** zawsze wymagają szyfrowania (SSL/TLS), podczas gdy dane są przesyłane tooand z hello bazy danych. Podczas tworzenia potoku za pomocą edytora JSON, Dodaj hello **szyfrowania** właściwości i ustaw dla niej zbyt**true** w hello **ciąg połączenia**. Jeśli używasz hello [kreatora kopiowania](data-factory-azure-copy-wizard.md), Kreator hello ustawia tę właściwość domyślnie. Dla **usługi Azure Storage**, można użyć **HTTPS** w parametrach połączenia hello.

### <a name="data-encryption-at-rest"></a>Szyfrowanie danych w spoczynku
Niektóre dane są przechowywane Obsługa szyfrowania danych magazynowanych. Zalecamy, aby włączyć mechanizm szyfrowania danych dla tych magazynów danych. 

#### <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse
Przezroczysty danych szyfrowania (funkcji TDE) w usłudze Azure SQL Data Warehouse pomaga w ochronie przed zagrożeniem hello złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania danych przechowywanych. To zachowanie jest przezroczysty toohello klienta. Aby uzyskać więcej informacji, zobacz [Zabezpieczanie bazy danych w usłudze SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md).

#### <a name="azure-sql-database"></a>Usługa Azure SQL Database
Baza danych SQL Azure obsługuje również przezroczystego szyfrowania danych (funkcji TDE), która pomaga w ochronie przed zagrożeniem hello złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania danych hello bez konieczności zmiany toohello aplikacji. To zachowanie jest przezroczysty toohello klienta. Aby uzyskać więcej informacji, zobacz [przezroczystego szyfrowania danych z bazy danych SQL Azure](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database). 

#### <a name="azure-data-lake-store"></a>Azure Data Lake Store
Usługa Azure Data Lake store zapewnia również szyfrowanie danych przechowywanych w hello konta. Po włączeniu usługi Data Lake store szyfruje dane przed wprowadzeniem trwałych i automatycznie odszyfrowuje przed pobierania, dzięki czemu dostęp do danych powitania klienta toohello przezroczysty. Aby uzyskać więcej informacji, zobacz [zabezpieczeń w usłudze Azure Data Lake Store](../data-lake-store/data-lake-store-security-overview.md). 

#### <a name="azure-blob-storage-and-azure-table-storage"></a>Magazyn obiektów Blob platformy Azure i magazynu tabel platformy Azure
Usługa Azure storage magazynu obiektów Blob i tabel Azure obsługuje magazynu usługi szyfrowania (SSE), który automatycznie szyfruje dane, zanim toostorage utrwalanie i odszyfrowywane przed pobierania. Aby uzyskać więcej informacji, zobacz [szyfrowanie usługi Magazyn Azure dla danych magazynowanych](../storage/common/storage-service-encryption.md).

#### <a name="amazon-s3"></a>Amazon S3
Amazon S3 obsługuje szyfrowanie danych przechowywanych klienta i serwera. Aby uzyskać więcej informacji, zobacz [ochrona danych przy użyciu szyfrowania](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html). Fabryki danych nie obsługuje obecnie, Amazon S3 wewnątrz wirtualnych chmury prywatnej (VPC).

#### <a name="amazon-redshift"></a>Amazon Redshift
Amazon Redshift obsługuje szyfrowanie klastra dla przechowywanych danych. Aby uzyskać więcej informacji, zobacz [szyfrowania bazy danych Redshift Amazon](http://docs.aws.amazon.com/redshift/latest/mgmt/working-with-db-encryption.html). Fabryki danych nie obsługuje obecnie, Amazon Redshift wewnątrz VPC. 

#### <a name="salesforce"></a>SalesForce
SalesForce obsługuje szyfrowanie platformy osłony, który umożliwia szyfrowanie wszystkich plików, załączników i pola niestandardowe. Aby uzyskać więcej informacji, zobacz [hello opis przepływ uwierzytelniania OAuth serwera sieci Web](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_web_server_oauth_flow.htm).  

## <a name="hybrid-scenarios-using-data-management-gateway"></a>Scenariuszy hybrydowych (przy użyciu bramy zarządzania danymi)
Scenariusze hybrydowe wymagają toobe brama zarządzania danymi zainstalowane w sieci lokalnej lub w sieci wirtualnej (Azure) lub prywatnej chmury wirtualne (Amazon). Brama Hello musi być możliwe tooaccess hello danych lokalnych magazynów. Aby uzyskać więcej informacji na temat bramy hello zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md). 

![Kanały zarządzania bramy danych](media/data-factory-data-movement-security-considerations/data-management-gateway-channels.png)

Witaj **kanał poleceń** umożliwia komunikację między usługi przenoszenia danych z fabryki danych i brama zarządzania danymi. Komunikacja Hello zawiera informacje dotyczące działania toohello. kanał danych Hello jest używany do przenoszenia danych między lokalnych magazynów danych i magazyny danych w chmurze.    

### <a name="on-premises-data-store-credentials"></a>Dane lokalne przechowywanie poświadczeń
Witaj poświadczenia dla sieci lokalnych magazynów danych są przechowywane lokalnie (nie w chmurze hello). Można ich ustawiać na trzy różne sposoby. 

- Przy użyciu **zwykłego tekstu** (mniej bezpieczna opcja) za pośrednictwem protokołu HTTPS z portalu Azure / Kreator kopiowania. poświadczenia Hello są przekazywane w brama lokalna toohello zwykłego tekstu.
- Przy użyciu **biblioteki JavaScript kryptografii z Kreatora kopiowania**.
- Przy użyciu **kliknij — gdy na podstawie aplikacji Menedżera poświadczeń**. Kliknij Hello — po wykonuje aplikacji na maszynie lokalnej hello bramy toohello dostępu i ustawia poświadczenia dla magazynu danych hello. Tej opcji i hello są kolejnej hello najbardziej bezpieczne opcje. aplikacja Menedżer poświadczeń Hello, domyślnie używa portu hello 8050 na komputerze hello bramy na potrzeby bezpiecznej komunikacji.  
- Użyj [AzureRmDataFactoryEncryptValue nowy](/powershell/module/azurerm.datafactories/New-AzureRmDataFactoryEncryptValue) poświadczenia tooencrypt polecenia cmdlet programu PowerShell. polecenie cmdlet Hello używa certyfikatów hello, że brama jest skonfigurowany toouse tooencrypt hello poświadczeń. Można użyć poświadczeń hello szyfrowane zwróconych przez to polecenie cmdlet i dodaj go za**EncryptedCredential** element hello **connectionString** w hello pliku JSON, który jest używany z hello [ Nowy AzureRmDataFactoryLinkedService](/powershell/module/azurerm.datafactories/new-azurermdatafactorylinkedservice) polecenia cmdlet lub we fragmencie kodu JSON hello w hello Edytor fabryki danych w portalu hello. Ta opcja i hello kliknij — po zatwierdzeniu aplikacji hello najbardziej bezpieczne opcje. 

#### <a name="javascript-cryptography-library-based-encryption"></a>Szyfrowanie oparte na bibliotece kryptografii JavaScript
Można szyfrować poświadczeń magazynu danych przy użyciu [biblioteki JavaScript kryptografii](https://www.microsoft.com/download/details.aspx?id=52439) z hello [kreatora kopiowania](data-factory-copy-wizard.md). Po wybraniu tej opcji hello kreatora kopiowania pobiera klucz publiczny hello bramy i używa go poświadczeń magazynu danych hello tooencrypt. poświadczenia Hello są odszyfrować hello maszyna bramy i chroniony przez system Windows [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx).

**Obsługiwane przeglądarki:** programu IE 8, IE9, IE10, IE11, Microsoft Edge i przeglądarki Firefox najnowszej, Chrome, Opera, przeglądarki Safari. 

#### <a name="click-once-credentials-manager-app"></a>Kliknij przycisk — raz aplikacji Menedżera poświadczeń
Możesz uruchomić powitania kliknij — gdy na podstawie aplikacji Menedżera poświadczeń z portalu Azure/kopii kreatora podczas tworzenia potoków. Ta aplikacja gwarantuje, czy poświadczenia nie są przekazywane w postaci zwykłego tekstu za pośrednictwem przewodowy hello. Domyślnie używa portu hello **8050** na komputerze hello bramy na potrzeby bezpiecznej komunikacji. W razie potrzeby można zmienić tego portu.  
  
![Port HTTPS dla bramy hello](media/data-factory-data-movement-security-considerations/https-port-for-gateway.png)

Obecnie brama zarządzania danymi używa pojedynczego **certyfikatu**. Ten certyfikat został utworzony podczas instalacji bramy hello (dotyczy tooData brama zarządzania utworzone po listopada 2016 i wersji 2.4.xxxx.x lub nowszej). Ten certyfikat może zastąpić certyfikat SSL/TLS. Ten certyfikat jest używany przez powitania kliknij — po toosecurely aplikacji Menedżera poświadczeń połączenia toohello bramy komputera w celu ustawienia poświadczeń magazynu danych. Przechowuje dane poświadczeń magazynu bezpiecznie lokalnymi przy użyciu systemu Windows hello [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx) na maszynie hello z bramą. 

> [!NOTE]
> Starsze bram, które zostały zainstalowane przed listopada 2016 lub 2.3.xxxx.x wersji nadal poświadczeń toouse szyfrowane i przechowywane w chmurze. Nawet w przypadku uaktualniania hello bramy toohello najnowszej wersji hello poświadczenia nie są migrowane tooan na lokalnej maszynie    
  
| Wersja bramy (podczas tworzenia) | Poświadczenia zapisane | Poświadczeń szyfrowania / zabezpieczeń | 
| --------------------------------- | ------------------ | --------- |  
| < = 2.3.xxxx.x | W chmurze | Zaszyfrowane za pomocą certyfikatu (inny niż hello używaną przez aplikację Menedżer poświadczeń) | 
| > = 2.4.xxxx.x | Lokalnie | Zabezpieczone za pomocą DPAPI | 
  

### <a name="encryption-in-transit"></a>Szyfrowanie podczas przesyłania
Są wszystkie operacje transferu danych za pośrednictwem bezpiecznego kanału **HTTPS** i **TLS za pośrednictwem protokołu TCP** ataków man-in--middle tooprevent podczas komunikowania się z usługami Azure.
 
Można również użyć [IPSec VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md) lub [Express Route](../expressroute/expressroute-introduction.md) kanał komunikacyjny bezpiecznego hello toofurther między siecią lokalną a Azure.

Sieć wirtualna jest logiczną reprezentacja sieci w chmurze hello. Możesz połączyć tooyour sieci lokalnej sieci wirtualnej platformy Azure (VNet), konfigurując IPSec sieci VPN (site-to-site) lub usługi Express Route (prywatnej komunikacji równorzędnej)       

Witaj Poniższa tabela zawiera podsumowanie hello sieciowe i bramy konfiguracji zalecenia na podstawie różnych kombinacji lokalizacje źródłowa i docelowa dla hybrydowych przenoszenia danych.

| Element źródłowy | Element docelowy | Konfiguracja sieci | Instalator bramy |
| ------ | ----------- | --------------------- | ------------- | 
| Lokalnie | Maszyny wirtualne i usługi w chmurze wdrożony w sieci wirtualnych | IPSec VPN (punkt lokacja lub lokacja lokacja) | Brama może być zainstalowana lokalnie lub na platformie Azure wirtualnej maszyny (VM) w sieci wirtualnej | 
| Lokalnie | Maszyny wirtualne i usługi w chmurze wdrożony w sieci wirtualnych | ExpressRoute (prywatnej komunikacji równorzędnej) | Brama może być zainstalowana lokalnie lub na maszynie Wirtualnej platformy Azure w sieci wirtualnej | 
| Lokalnie | Usług Azure, których publiczny punkt końcowy | ExpressRoute (publicznej komunikacji równorzędnej) | Brama musi być zainstalowany na lokalnym | 

Witaj poniższych ilustracjach przedstawiono użycie hello brama zarządzania danymi do przenoszenia danych między lokalną bazą danych i usług Azure przy użyciu expressroute i sieci VPN IPSec (z sieci wirtualnej):

**Usługi Express Route:**
 
![Użyj bramy Expressroute](media/data-factory-data-movement-security-considerations/express-route-for-gateway.png) 

**Protokół IPSec sieci VPN:**

![Sieć VPN IPSec z bramy](media/data-factory-data-movement-security-considerations/ipsec-vpn-for-gateway.png)

### <a name="firewall-configurations-and-whitelisting-ip-address-of-gateway"></a>Konfiguracje zapór i listę dozwolonych podobnej adres IP bramy

#### <a name="firewall-requirements-for-on-premisesprivate-network"></a>Wymagania dotyczące zapory dla sieci o lokalnym/prywatnym  
W przedsiębiorstwie **firmowej zapory** działa na routerze centralnej hello hello organizacji. A **zapory systemu Windows** działa jako demon na komputerze lokalnym hello, na które hello zainstalowano bramę. 

Witaj Poniższa tabela zawiera **port wyjściowy** i wymagania dotyczące domeny dla hello **firmowej zapory**.

| Nazwy domen | Porty wyjściowe | Opis |
| ------------ | -------------- | ----------- | 
| `*.servicebus.windows.net` | 443, 80 | Wymagane przez hello bramy tooconnect toodata przepływu usług w fabryce danych |
| `*.core.windows.net` | 443 | Używane przez hello bramy tooconnect tooAzure konta magazynu w przypadku użycia hello [przemieszczane kopiowania](data-factory-copy-activity-performance.md#staged-copy) funkcji. | 
| `*.frontend.clouddatahub.net` | 443 | Wymagane przez hello bramy tooconnect toohello usługi fabryka danych Azure. | 
| `*.database.windows.net` | 1433   | (OPCJONALNIE) wymagane, jeśli folderem docelowym jest baza danych Azure SQL / Azure SQL Data Warehouse. Użyj hello przemieszczane kopiowania funkcji toocopy danych tooAzure SQL bazy danych/usługi Azure SQL Data Warehouse bez konieczności otwierania hello portu 1433. | 
| `*.azuredatalakestore.net` | 443 | (OPCJONALNIE) potrzebna do folderu docelowego jest Azure Data Lake store | 

> [!NOTE] 
> Może mieć porty toomanage / listę dozwolonych podobnej domen na hello firmowa Zapora poziomu źródeł odpowiednich danych. Ta tabela używa tylko bazy danych SQL Azure, Magazyn danych SQL Azure, Azure Data Lake Store jako przykłady.   

Witaj Poniższa tabela zawiera **port wejściowy** wymagania dotyczące hello **zapory systemu windows**.

| Porty wejściowe | Opis | 
| ------------- | ----------- | 
| 8050 (TCP) | Wymagane przez hello poświadczenia Menedżera aplikacji toosecurely zestaw poświadczeń dla lokalnych magazynów danych na powitania bramy. | 

![Wymagania dotyczące portów bramy](media\data-factory-data-movement-security-considerations/gateway-port-requirements.png) 

#### <a name="ip-configurations-whitelisting-in-data-store"></a>Konfiguracje adresów IP / listę dozwolonych podobnej danych magazynu
Niektóre sklepy danych w chmurze hello również wymagać niedozwolonych adres IP komputera hello dostępu do nich. Upewnij się, że adres IP hello hello maszyna bramy jest białej / odpowiednio skonfigurowane w zaporze.

Witaj następujące magazyny danych chmury wymagają niedozwolonych adres IP komputera bramy hello. Niektóre z tych magazynów danych, domyślnie nie może wymagać niedozwolonych hello adresu IP. 

- [Azure SQL Database](../sql-database/sql-database-firewall-configure.md) 
- [Magazyn danych SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal)
- [Azure Data Lake Store](../data-lake-store/data-lake-store-secure-data.md#set-ip-address-range-for-data-access)
- [Azure Cosmos DB](../documentdb/documentdb-firewall-support.md)
- [Amazon Redshift](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 

## <a name="frequently-asked-questions"></a>Często zadawane pytania

**Pytanie:** można udostępniać hello bramy dla fabryki danych?
**Odpowiedź:** nie obsługujemy tej funkcji jeszcze. Aktywnie pracujemy nad go.

**Pytanie:** jakie są wymagania portu hello toowork bramy hello?
**Odpowiedź:** brama podejmuje tooopen oparte na protokole HTTP połączeń internetowych. Witaj **wychodzącego porty 443 i 80** muszą być otwarte dla bramy toomake tego połączenia. Otwórz **ruchu przychodzącego dla portu 8050** tylko na poziomie komputera hello (nie na poziomie firmowej zapory) dla aplikacji Menedżer poświadczeń. Jeśli baza danych SQL Azure lub usługi Azure SQL Data Warehouse jest używany jako źródło / docelowego, następnie należy tooopen **1433** również port. Aby uzyskać więcej informacji, zobacz [konfiguracji i adresy IP listę dozwolonych podobnej zapory](#firewall-configurations-and-whitelisting-ip-address-of gateway) sekcji. 

**Pytanie:** jakie są wymagania dotyczące certyfikatów dla bramy?
**Odpowiedź:** bieżącej bramy wymaga certyfikatu, który jest używany przez aplikacji Menedżera poświadczeń hello w bezpieczny sposób ustawiania poświadczeń magazynu danych. Ten certyfikat jest certyfikatu z podpisem własnym utworzone i skonfigurowane przez hello instalacji bramy. Można użyć własnych TLS / SSL zamiast tego certyfikatu. Aby uzyskać więcej informacji, zobacz [kliknij — raz poświadczeń aplikacji Menedżera](#click-once-credentials-manager-app) sekcji. 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać informacje o wydajności działania kopiowania, zobacz [skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md).

 
