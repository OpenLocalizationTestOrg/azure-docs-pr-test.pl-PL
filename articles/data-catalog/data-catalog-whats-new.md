---
title: "aaaWhat do nowego w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie nowych funkcji dodać tooAzure wykazu danych."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 1201f8d4-6f26-4182-af3f-91e758a12303
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/22/2017
ms.author: maroche
ms.openlocfilehash: f60130487ece39e110446b68544945089d2ab37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-azure-data-catalog"></a>What's new in Azure Data Catalog
Aktualizuje zbyt**Azure Data Catalog** są wydawane regularnie. Nie każdy wydanie obejmuje nowe funkcje dla użytkownika, ponieważ niektóre wersje są koncentruje się na możliwości usługi zaplecza. Ta strona przedstawia nowej usługi Azure Data Catalog dodano toohello możliwości dla użytkownika.

## <a name="whats-new-for-august-2017"></a>Co to jest nowe w sierpniu 2017 
Począwszy od sierpnia 2017 r. hello następujące funkcje zostały dodane tooAzure wykazu danych:

*   Nowe próbki dewelopera jest dostępny do tworzenia i zarządzania metadanych relacji przy użyciu hello interfejsu API REST wykazu danych. Witaj *zaimportować informacje dotyczące relacji do wykazu danych* przykład jest dostępny na powitania [strony przykłady kodu usługi Data Catalog](https://azure.microsoft.com/resources/samples/?service=data-catalog&sort=0). 
* Obsługa wyodrębniania przyłączyć metadanych relacji ze źródeł danych programu Teradata podczas rejestrowania przy użyciu narzędzia rejestracji źródła danych hello tabele powiązane.
* Obsługuje dla funkcji zwracającej tabelę serwera SQL (TVF) obiektów podczas rejestrowania źródła danych programu SQL Server przy użyciu narzędzia rejestracji źródła danych hello.
* Wiele aktualizacji i ulepszenia wydajności hello tooincrease i użyteczność hello portalu wykazu danych.

## <a name="whats-new-for-july-2017"></a>Nowości dotyczące 2017 lipca 
Począwszy od 2017 lipca hello następujące funkcje zostały dodane tooAzure wykazu danych:
*   Obsługa bardziej szczegółową kontrolę nad tym operacji na metadanych dozwolonym:
    - Administratorzy katalogu można ograniczyć tagi toocontribute możliwości użytkowników i pokrewne metadane toohello katalogu, włączenie wykazu toohello dostęp tylko do odczytu.
    - Administratorzy katalogu mogą ograniczyć użytkowników możliwości tooregister nowych źródeł danych w katalogu hello.
    - Administratorzy katalogu mogą ograniczyć własność tootake możliwości użytkowników metadanych zasobów danych w katalogu hello.
    - Można udzielać uprawnienia grupy zabezpieczeń usługi Active Directory tooAzure i użytkowników w celu ułatwienia zarządzania uprawnieniami.
* Obsługa relacje między zarejestrowanych zasobów danych i odnajdowania zasobów powiązanych danych w portalu wykazu danych hello, w tym:
    - Wyodrębnianie metadanych relacji z programu SQL Server (w tym usługi Azure SQL Database), Oracle i MySQL źródeł danych, korzystając z hello narzędzia rejestracji źródła danych wykazu danych.
    - Odnajdywanie zasobów powiązanych danych podczas wyświetlania w portalu wykazu danych hello metadanych zasobów.
    - Toodefine operacje odnajdywania i zarządzania relacjami między zasobów danych za pomocą hello interfejsu API REST wykazu danych.

Aby uzyskać dodatkowe informacje na temat zarządzania uprawnień w wykazie danych, zobacz [jak toosecure uzyskują dostęp do zasobów katalogu i danych toodata](data-catalog-how-to-secure-catalog.md).
Aby uzyskać dodatkowe informacje o relacje w wykazie danych, zobacz [jak tooview powiązane zasoby danych w usłudze Azure Data Catalog](data-catalog-how-to-view-related-data-assets.md).

## <a name="whats-new-for-june-2017"></a>Nowości dotyczące 2017 czerwca 
Począwszy od czerwca 2017 r. hello następujące funkcje zostały dodane tooAzure wykazu danych:
*   Obsługa źródeł danych programu Sybase, Apache Cassandra i bazy danych MongoDB. Użytkownicy mogą teraz zarejestrować i odnajdowania Cassandra i bazy danych MongoDB i tabele i baz danych programu Sybase, tabel i widoków.

> [!NOTE]
> Podczas rejestrowania bazy danych MongoDB i Cassandra tabel zawierających kolumny o złożonych typach danych przykład rekordów i tablic, te kolumny nie zostaną uwzględnione w metadanych hello dodać tooData katalogu.

## <a name="whats-new-for-may-2017"></a>Nowości dotyczące 2017 maja 
Począwszy od 2017 maja hello następujące funkcje zostały dodane tooAzure wykazu danych:
*   Nowe próbki dewelopera jest dostępna dla hello zbiorczym importowaniem firm słownik terminów. przykład importowania zbiorczego słownik Hello jest dostępny na powitania [strona Przykłady dewelopera usługi Data Catalog](https://docs.microsoft.com/azure/data-catalog/data-catalog-samples). 
*   Obsługa, edytując informacje dotyczące połączenia ODBC w portalu Azure Data Catalog hello. Właścicieli zasobów danych i administratorów usługi Data Catalog edytować hello informacje o połączeniu dla zarejestrowanego źródła danych bez konieczności źródeł danych hello toore rejestru.
*   Obsługa aktywne adresy URL w definicji słownik biznesowych wraz z opisami. Adresy URL została uwzględniona w właściwości Opis i definicji hello dla firm terminów, adresy URL hello będą wyświetlane jako hiperłącze w portalu wykazu danych hello.
*   Obsługa wyświetlania ekspert nazwy dodatkowo tooexpert adresy e-mail. Podczas przeglądania ekspertów w hello właściwości zasobu danych w portalu wykazu danych hello, pełna nazwa hello ekspertów z usługi Azure Active Directory będzie wyświetlany w hello etykietka narzędzia.

## <a name="whats-new-for-april-2017"></a>Nowości dotyczące kwietnia 2017 
Począwszy od kwietnia 2017 r. hello następujące funkcje zostały dodane tooAzure wykazu danych:
*   Obsługa ODBC — źródła danych. Użytkownicy mogą teraz zarejestrować i odnajdywanie baz danych ODBC, tabel i widoków przy użyciu narzędzia rejestracji źródła danych usługi Data Catalog hello.

## <a name="whats-new-for-march-2017"></a>Nowości dotyczące 2017 marca 
Począwszy od 2017 marca hello następujące funkcje zostały dodane tooAzure wykazu danych:
*   Obsługa przy użyciu grup zabezpieczeń usługi AAD dla administratorów usługi Data Catalog.
*   Wykaz danych Azure jest obecnie dostępna w nowych region platformy Azure. Klientów można udostępnić hello Azure Data Catalog w hello zachodnie centralnej nam regionie, dodanie tooEast USA, zachodnie stany USA, Europa Zachodnia i Australia Wschodnia, Europa Północna, Europa i Azja południowo-wschodnia. Aby uzyskać więcej informacji, zobacz [regiony platformy Azure](https://azure.microsoft.com/regions/).

## <a name="whats-new-for-february-2017"></a>Nowości dotyczące lutego 2017 
Począwszy od lutego 2017 r. hello następujące funkcje zostały dodane tooAzure wykazu danych:
*   Obsługa zaawansowanych ustawień w narzędzia rejestracji źródła danych usługi Data Catalog hello. Użytkownicy mogą określić wartości limitu czasu polecenia podczas rejestrowania źródła danych.
*   Obsługa FTP i PostgreSQL źródeł danych. Użytkownicy mogą teraz zarejestrować i odnajdywanie FTP pliki i katalogi i bazy danych PostgreSQL, tabele i widoki.

## <a name="whats-new-for-january-2017"></a>Nowości dotyczące stycznia 2017 r 
Począwszy od stycznia 2017 r. hello następujące funkcje zostały dodane tooAzure wykazu danych:
*   Wykaz danych Azure jest obecnie [GWIAZDKĘ CSA](https://www.microsoft.com/trustcenter/compliance/csa-star-certification) zgodne.
*   Integracja z [Get i Przekształć w programie Excel 2016 i dodatku Power Query dla programu Excel](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605). Użytkownicy programu Excel można udostępnić zapytań i odnajdywanie zapytań przy użyciu usługi Azure Data Catalog z wewnątrz programu Excel. Ta funkcja jest dostępna toousers z licencjami usługi Power BI Pro.

## <a name="whats-new-for-december-2016"></a>Nowości dotyczące grudnia 2016
Począwszy od grudnia 2016 r. hello następujące funkcje zostały dodane tooAzure wykazu danych:
*   Wykaz danych Azure jest obecnie [HIPAA](https://www.microsoft.com/trustcenter/Compliance/HIPAA) i [Klauzulami modelu UE](https://www.microsoft.com/TrustCenter/Compliance/EU-Model-Clauses) zgodne.
*   Obsługa do edycji informacji dotyczących połączenia źródła danych. Właścicieli zasobów danych i administratorów usługi Data Catalog edytować hello informacje dotyczące połączenia dla źródeł danych zarejestrowanych bez konieczności źródeł danych hello toore rejestru.
*   Obsługa źródeł danych witryny Salesforce.com. Użytkownicy mogą teraz zarejestrować i odnajdywanie obiektów Salesforce.


## <a name="whats-new-for-november-2016"></a>Nowości dotyczące listopada 2016
Począwszy od listopada 2016 r. hello następujące funkcje zostały dodane tooAzure wykazu danych:
*   Wykaz danych Azure jest obecnie [ISO/IEC 27001](https://www.microsoft.com/trustcenter/compliance/iso-iec-27001) i [ISO/IEC 27018](https://www.microsoft.com/TrustCenter/Compliance/iso-iec-27018) zgodne.
*   Obsługa rejestracji ręcznej hello źródeł danych ODBC, za pomocą portalu wykazu danych hello i interfejsu API REST.

## <a name="whats-new-for-september-2016"></a>Nowości dotyczące wrześniu 2016 r.
Począwszy od września 2016 r. hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Obsługa IBM DB2 źródeł danych. Użytkownicy mogą teraz zarejestrować i odnajdywanie bazy danych DB2, tabel i widoków.
* Obsługa źródeł danych bazy danych Azure rozwiązania Cosmos. Użytkownicy mogą teraz zarejestrować i odnajdywanie DB rozwiązania Cosmos baz danych i kolekcji.
* Obsługa dostosowywania hello nazwy wykazu w hello portalu wykazu danych. Administratorzy katalogu mogą teraz udostępnić tekst, który jest wyświetlany w tytule hello w portalu, takie jak nazwa organizacji hello.

## <a name="whats-new-for-august-2016"></a>Co to jest nowe w sierpniu 2016
Począwszy od sierpnia 2016 roku hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Rozszerzenia dla rejestracji źródła danych programu SQL Server Master Data Services (MDS). Użytkownicy teraz mogą obejmować profile podglądy i dane podczas rejestrowania przy użyciu narzędzia rejestracji źródła danych usługi Data Catalog hello jednostek MDS.
* Obsługa zdefiniowane przez administratora organizacji zapisane wyszukiwania. Podczas zapisywania wyszukiwania w portalu wykazu danych hello, Administratorzy usługi Data Catalog można wybrać toosave wyszukiwania do użytku osobistego i dla wszystkich użytkowników wykazu. Organizacyjnej zapisane wyszukiwania są udostępniane wszystkim użytkownikom w katalogu i zapewnia standardowych punktów początkowych dla odnajdywanie źródła danych.
* Aktualizuje toohello właściwości widoku w hello portalu wykazu danych. Wszystkie właściwości zasobów danych są teraz wyświetlane i zarządzania nimi tooprovide jednej, o zmiennym rozmiarze okienka obsługi bardziej spójny i łatwy.

## <a name="whats-new-for-july-2016"></a>Nowości dotyczące lipca 2016 r.
Począwszy od lipca 2016 hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Obsługa źródeł danych programu SQL Server Master Data Services (MDS). Użytkownicy mogą teraz zarejestrować i odnajdowania usług MDS modeli i jednostek.
* Obsługa procedur składowanych serwera SQL. Użytkownicy mogą teraz zarejestrować i odnajdywanie obiektów procedury składowanej w źródłach danych programu SQL Server.
* Obsługa dodatkowych języków w portalu Azure Data Catalog hello i hello narzędzia rejestracji źródła danych, łącznie z 18 obsługiwanych języków. Witaj środowisko użytkownika usługi Azure Data Catalog jest zlokalizowana na podstawie preferencji językowych hello ustawiony w systemie Windows lub w przeglądarce sieci web hello.
* Aktualizacje i uściślenia dla hello Data Catalog strony głównej portalu, tym lepsza wydajność i prostsze użytkowników.

## <a name="whats-new-for-june-2016"></a>Nowości dotyczące czerwca 2016 r.
Począwszy od czerwca 2016 hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Obsługa zmiana rozmiaru kolumn w widoku listy hello podczas odnajdywania zasobów danych w hello portalu wykazu danych. Teraz użytkownicy mogą zmieniać rozmiar poszczególnych kolumn toomore łatwo odczytać metadanych długich zasobów, takich jak znaczniki wraz z opisami.
* Dodatek Power Query dla programu Excel został dodany toohello menu "Otwórz w" hello portalu wykazu danych. Użytkownicy mogą teraz otworzyć obsługiwanych źródeł danych w programie Excel 2016 lub w programie Excel 2010 i Excel 2013 z hello [dodatku Power Query dla programu Excel](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605) zainstalować dodatek.
* Obsługa źródeł danych magazynu tabel platformy Azure. Użytkownicy mogą teraz zarejestrować i odnajdywanie obiektów tabeli w źródłach danych usługi Azure Storage.

## <a name="whats-new-for-may-2016"></a>Nowości dotyczące maj 2016
Począwszy od maj 2016 hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Słownik biznesowy, która pozwala administratorom wykazu toodefine firm warunków i hierarchie toocreate wspólnego słownika biznesowych. Użytkownicy można oznaczać zarejestrowanych zasobów danych z słownik terminów toomake go toodiscover łatwiejsze i zrozumieć ich zawartość hello hello katalogu. Aby uzyskać więcej informacji, zobacz [jak tooset się hello słownik biznesowy dla postanowieniom znakowanie](data-catalog-how-to-business-glossary.md)  
* Ulepszenia toohello słownik biznesowy wykazu danych, który umożliwia użytkownikom tooupdate wiele terminów w ramach jednej operacji. Użytkownicy mogą wybrać wiele warunków tooedit hello następujące pola:
  * Termin nadrzędny: hello użytkownik może wybrać nowy termin nadrzędnej, a wszystkie wybrane warunki są elementami podrzędnymi zaktualizowane toobe termin nadrzędny hello wybrane. Jeśli hello wybrane postanowienia, które mają hello tym samym elemencie nadrzędnym, a następnie elementem nadrzędnym jest wyświetlany w polu tekstowym hello, w przeciwnym razie pola Termin nadrzędnego hello jest tooblank zestawu.   
  * Znaczniki i uczestników: użytkownicy, można dodawać i usuwać tagów i uczestników dla wielu terminów przy użyciu hello występują takie same jak znakowanie wielu zasobów danych.

> [!NOTE]
> Słownik biznesowy Hello jest dostępna tylko w hello Standard Edition usługi Azure Data Catalog. Witaj bezpłatna wersja nie zapewnia możliwości, dla której działalność znakowanie lub słownik biznesowy.

## <a name="whats-new-for-march-2016"></a>Nowości dotyczące marca 2016
Wersji marca 2016 r hello następujące funkcje zostały dodane tooAzure danych katalogu: g:

* Skonsolidowane punkt końcowy interfejsu API REST programowy dostęp do możliwości wyszukiwania hello i możliwości zarządzania zasobów katalogu hello usługi Azure Data Catalog. Ten punkt końcowy wyszukiwania interfejsu API interfejsu API punktu końcowego i katalog został przestarzałe i zaprzestać 21 marca 2016 r. Nie wprowadzono żadnych zmian toohello semantykę hello interfejsu API. Tylko punkt końcowy hello zmienić identyfikatora URI. Aby uzyskać dodatkowe informacje, zobacz hello [dokumentacja interfejsu API REST usługi Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267595.aspx). Aby uzyskać przykłady interfejsu API, zobacz [Przykłady dewelopera usługi Azure Data Catalog](data-catalog-samples.md).

## <a name="whats-new-for-february-2016"></a>Nowości w lutym 2016 r.
Począwszy od lutego 2016 hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Wybór źródła danych nowo zmienioną środowisko w narzędzia rejestracji źródła danych usługi Azure Data Catalog hello. Witaj narzędzia rejestracji źródła danych został zaktualizowany toomake it łatwiejsze toolocate użytkownik, a następnie zaznacz hello źródeł danych obsługiwane przez usługi Azure Data Catalog.
* Obsługa 10 dodatkowych języków w portalu Azure Data Catalog hello i narzędzia rejestracji źródła danych hello. Ponadto tooEnglish, hello Azure Data Catalog obsługi jest teraz dostępna w niemiecki, hiszpański, francuski, włoski, japoński, koreański, portugalski — Brazylia, rosyjski, chiński uproszczony i języka chińskiego tradycyjnego. Hello Azure Data Catalog jest zlokalizowana środowisko użytkownika zgodnie z preferencjami języka hello ustawiony w systemie Windows lub w przeglądarce sieci web hello użytkownika.
* Obsługa — replikacja geograficzna usługi Azure Data Catalog danych biznesowych ciągłości i odzyskiwanie po awarii. Wszystkie zawartości wykazu danych Azure, w tym adnotacji metadanych i crowdsourced danych źródłowych, teraz są replikowane między dwóch regionach platformy Azure na toocustomers nie dodatkowych kosztów. Hello regiony platformy Azure są wstępnie skojarzone, co najmniej 500 mil od siebie i wykonaj mapowania hello zgodnie z opisem w [firm ciągłości i odzyskiwanie po awarii (BCDR): Azure łączyć regionów](../best-practices-availability-paired-regions.md).
* Obsługa zmiana hello subskrypcji platformy Azure, używany przez wykaz danych Azure. Azure Data Catalog Administratorzy mogą używać hello strony ustawień w portalu Azure Data Catalog hello — tooselect innej subskrypcji platformy Azure w celach rozliczeń.

## <a name="whats-new-for-january-2016"></a>Nowości dotyczące styczeń 2016
Począwszy od stycznia 2016 r. hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Obsługa ręcznie rejestrowanie dodatkowych źródeł danych. Możesz teraz użyć "Utwórz ręcznie wpis" w portalu Azure Data Catalog hello, lub hello tooregister interfejsu API REST usługi Azure Data Catalog hello następujące źródła danych:
  * OData - funkcja, zestaw jednostek oraz kontenera jednostek
  * HTTP - pliku, punkt końcowy, raportów i lokacji
  * System plików — plik
  * SharePoint — listy
  * FTP - plików i katalogów
  * Witryny SalesForce.com — obiekt
  * Bazy danych DB2 — tabeli, widoku i bazy danych
  * PostgreSQL — tabeli, widoku i bazy danych
* Obsługa "Otwórz w SQL Server Data Tools" dla źródła danych serwera SQL (łącznie z bazy danych SQL Azure i usługi Azure SQL Data Warehouse).  
* Możliwość rejestrowania i odnajdywanie, widoki SAP HANA i pakietów. Możesz zarejestrować SAP HANA źródła danych przy użyciu danych usługi Azure Data Catalog hello narzędzia rejestracji źródła i można dodawać adnotacje i odnajdywać zarejestrowanego źródła danych SAP HANA przy użyciu portalu Azure Data Catalog hello.
* Witaj toopin możliwości i odpiąć zasobów danych w portalu Azure Data Catalog hello. Możesz wybrać toomake zasoby danych toopin ich toorediscover i ponownego użycia.
* Nowo przeprojektowana strona główna w portalu Azure Data Catalog hello. Witaj Nowa strona główna zawiera wgląd w hello bieżącą aktywność użytkowników — w tym opublikowanych niedawno zasoby przypięty zasobów i zapisane wyszukiwania — i wgląd w działania hello w hello katalogu jako jedną całość.
* Obsługa trwałych ustawień w portalu Azure Data Catalog hello. Ustawienia czynności użytkownika — tym widoku siatki lub kafelka hello liczba wyników na stronie i kliknij lub wyłącz podświetlanie - są zachowywane między sesjami użytkownika.
* Wykaz danych Azure jest obecnie dostępna w dwóch nowych regionów platformy Azure. Klientów można udostępnić hello Azure Data Catalog w hello Północna Europie i Azji Południowo-Wschodnia regionach, dodanie tooEast USA, zachodnie stany USA, Europa Zachodnia i Australia Wschodnia. Aby uzyskać więcej informacji, zobacz [regiony platformy Azure](https://azure.microsoft.com/regions/).

> [!NOTE]
> "Otwórz w SQL Server Data Tools" wymaga programu Visual Studio 2013 Update 4 oraz narzędzia programu SQL Server toobe zainstalowane. tooinstall hello najnowszej wersji programu SQL Server Data Tools, odwiedź stronę [Pobierz programu SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).


## <a name="whats-new-for-december-2015"></a>Nowości dotyczące grudnia 2015 r.
Począwszy od grudnia 2015 hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Obsługa danych profilów dla źródeł danych magazynu danych SQL Azure. Podczas rejestrowania usługi Azure SQL Data Warehouse tabele i widoki, użytkownicy mogą wybrać tooinclude danych profilu metryki z metadanymi hello wyodrębnione ze źródła danych hello.
* Możliwość rejestrowania i odnajdywanie obiektów MySQL i baz danych. Użytkownicy mogą zarejestrować MySQL źródła danych przy użyciu danych usługi Azure Data Catalog hello narzędzia rejestracji źródła i może dodawać adnotacje i odnajdywać zarejestrowanego źródła danych MySQL, przy użyciu portalu Azure Data Catalog hello.
* Obsługa SPNEGO i uwierzytelnianie systemu Windows dla źródeł danych programu Teradata. Podczas rejestrowania programu Teradata tabele i widoki, użytkownicy mogą wybrać tooTeradata tooconnect przy użyciu uwierzytelniania SPNEGO i systemu Windows, a LDAP i TD2.
* Obsługa usługi Azure Data Lake Store źródeł danych. Użytkownicy mogą teraz zarejestrować i odnajdywania źródeł danych usługi Azure Data Lake Store za pomocą usługi Azure Data Catalog.
* Obsługa ręcznie określenie ustawień serwera proxy sieci w narzędzia rejestracji źródła danych usługi Azure Data Catalog hello. Użytkownicy mogą wybierać "Modyfikuj ustawienia serwera proxy" Strona powitalna narzędzia hello i można określić hello proxy adres i port toobe używane przez narzędzie hello.

## <a name="whats-new-for-november-2015"></a>Nowości dotyczące listopada 2015
Począwszy od listopada 2015 hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Witaj tooview możliwości i skopiuj parametry połączenia z portalu usługi Azure Data Catalog hello programu SQL Server (w tym usługi Azure SQL Database) i źródłami danych programu Oracle. Użytkownicy mogą kliknąć łącze "Wyświetl parametry połączenia" w hello informacje o połączeniu dla programu SQL Server lub Oracle tabeli, widoku lub bazy danych, toosee hello parametry połączenia używane źródło danych toohello tooconnect. Parametry połączenia ADO.NET, ODBC i OLEDB oraz JDBC są dostępne dla źródła danych serwera SQL. ODBC i OLEDB parametry połączenia są dostępne dla źródła danych Oracle.
* Obsługa podczas rejestrowania programu Teradata tabele i widoki, w tym danych profilów.
* Obsługę "Otwórz w Power BI Desktop" dla programu SQL Server (łącznie z bazy danych SQL Azure i usługi Azure SQL Data Warehouse), SQL Server Analysis Services, Azure Storage i system plików HDFS źródła.  
* Obsługa uwierzytelniania LDAP dla źródeł danych programu Teradata. Podczas rejestrowania programu Teradata tabele i widoki, użytkownicy mogą wybrać tooTeradata tooconnect przy użyciu protokołu LDAP, a TD2 uwierzytelniania.
* Obsługa "Otwórz w programie Excel" dla źródła danych programu Teradata.
* Obsługa ostatnie terminy wyszukiwania w hello portalu wykazu danych Azure. Podczas wyszukiwania w portalu hello, użytkownicy mogą wybrać z obsługi odnajdowania hello tooaccelerate warunki wyszukiwania ostatnio używane.
* Obsługa podglądu dla źródeł danych programu Teradata. Podczas rejestrowania programu Teradata tabele i widoki, użytkownicy mogą wybrać tooinclude migawki rekordy z metadanymi hello wyodrębnione ze źródła danych hello.
* Obsługa "Otwórz w programie Excel" dla źródła danych magazynu danych SQL Azure.
* Obsługa do definiowania i edytowania schematów na poziomie kolumny dla ręcznie zarejestrowanych zasobów danych. Po utworzeniu ręcznie przy użyciu portalu Azure Data Catalog hello zasobu danych, użytkownicy mogą dodawać definicje kolumn w właściwości zasobów danych hello.
* Obsługa zapytań "ma" podczas wyszukiwania Azure Data Catalog, tooenable hello odnajdywanie zarejestrowanych zasobów danych, które posiadają określonych metadanych. Składnia zapytania w usłudze Azure Data Catalog zawiera teraz:

| Składnia zapytania | Przeznaczenie |
| --- | --- |
| `has:previews` |Umożliwia znalezienie zasobów danych, które obejmują Podgląd |
| `has:documentation` |Umożliwia znalezienie zasobów danych, dla których dostarczono dokumentacji |
| `has:tableDataProfiles` |Umożliwia znalezienie zasobów danych z danych na poziomie tabeli informacje o profilu |
| `has:columnsDataProfiles` |Umożliwia znalezienie zasobów danych z danych na poziomie kolumny informacje o profilu |


> [!NOTE]
> "Otwórz w programie Power BI Desktop" wymaga bieżącej wersji toobe aplikacji Power BI Desktop hello zainstalowane. Jeśli wystąpią problemy lub błędy podczas korzystania z tej funkcji, upewnij się, że masz najnowszą wersję programu Power BI Desktop z hello [witryny PowerBI.com](https://powerbi.com).


## <a name="whats-new-for-october-2015"></a>Nowości dotyczące października 2015
Począwszy od października 2015 hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Obsługa szyfrowania przechowywanych danych podglądy i danych profilów dla zarejestrowanych źródeł danych. Wykaz danych Azure niewidocznie szyfruje wszystkie rekordy w wersji zapoznawczej i danych profili zarejestrowany w usludze hello, bez konieczności zarządzania kluczami przez administratorów wykazu źródeł danych.
* Obsługa źródeł danych programu Teradata. Użytkownicy mogą teraz zarejestrować i odnajdywanie Teradata tabel i widoków.
* Obsługa lokalnych źródeł danych Hive. Użytkownicy mogą teraz zarejestrować i wykrywa tabele programu Hive dla Apache Hive w Hadoop lokalnych źródeł danych.
* Obsługa zapisane wyszukiwania w portalu Azure Data Catalog hello. Użytkownicy mogą zapisywać terminy wyszukiwania i tooeasily opcje filtru Powtórz poprzednie wyszukiwania i definiować widoki przydatne hello katalogu zawartości. Użytkownika można również oznaczyć zapisane wyszukiwanie jako domyślny wyszukiwania. Gdy użytkownik kliknie ikonę wyszukiwania hello "Lupa" na stronie głównej portalu usługi Azure Data Catalog hello lub ze strony "wprowadzenie" hello, hello użytkownika są wykonywane bezpośrednio toohello zapisane wyszukiwanie oznaczonej jako domyślny.
* Obsługa tekstu sformatowanego dokumentacji zarejestrowanych zasobów danych i kontenery w portalu Azure Data Catalog hello. Użytkownicy mogą teraz podać dokumentacji dla zasobów danych, takich jak tabele, widoki i raporty i kontenerów, takie jak bazy danych i modele dla scenariuszy, w którym tagów i opisy nie są wystarczające.
* Obsługa ręcznie rejestrowanie znanych danych typów źródła. Użytkownicy, można ręcznie wprowadzić informacje o źródle danych przy użyciu portalu Azure Data Catalog powitania dla wszystkich typów źródła danych obsługiwane przez usługi Azure Data Catalog.
* Obsługa autoryzowanie grup zabezpieczeń usługi Azure Active Directory. Administratorzy katalogu mogą włączyć dostęp toosecurity grupy katalogu, kont użytkowników, dzięki czemu można łatwiej toomanage tooAzure dostępu do wykazu danych.
* Obsługa otwieranie gałęzi źródeł danych w programie Excel z hello portalu wykazu danych Azure.

> [!NOTE]
> Hello bieżącej wersji obsługiwane są tylko Teradata TD2 uwierzytelniania. Dodatkowe uwierzytelnianie mechanizmów są obsługiwane w przyszłych wersjach.

> [!NOTE]
> Funkcja "Otwórz w programie Excel" hello toouse dla źródeł danych Hive, użytkowników musi być zainstalowany sterownik ODBC hello gałęzi.

## <a name="whats-new-for-september-2015"></a>Nowości dotyczące wrzesień 2015
Począwszy od września 2015 r. hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Obsługa podczas rejestrowania źródła danych gałęzi w tym danych profilów.
* Obsługa programowo odnajdywania hello API katalogu, ułatwiając toointegrate aplikacji z usługą Azure Data Catalog.
* Nowe dane "wprowadzenie" źródła obsługi odnajdowania w portalu Azure Data Catalog hello. Podczas wprowadzania hello "wykryć" strony portalu wykazu danych Azure hello bez wprowadzania wyszukiwanego terminu, mają być przedstawiane przy jednoczesnym hello katalogu zawartość, łącznie hello najczęściej używane znaczniki, ekspertów typy źródeł danych i typów obiektów.
* Możliwość rejestrowania i odnajdywanie obiektów magazynu danych SQL Azure i baz danych. Aby uzyskać dodatkowe informacje na temat usługi Azure SQL Data Warehouse, zobacz [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
* Możliwość rejestrowania i odnajdywanie modele usług SQL Server Analysis Services i serwerów SQL Server Reporting Services jako kontenerów. Podczas rejestrowania obiektów SSAS i SSRS, usługa Azure Data Catalog tworzy wpis hello SSAS modelu i serwer SSRS oraz hello raportów i innych obiektów. kontenery Hello mogą być wykrywane i opatrzone adnotacjami przy użyciu portalu Azure Data Catalog hello. Użytkownicy mogą również wyszukiwanie i filtrowanie zawartości hello modelu lub serwer w toosearching dodaniu i filtrowania hello zawartość katalogu hello.
* Możliwość rejestrowania i odnajdywania obiektów SQL Server Analysis Services za pośrednictwem protokołu HTTP/HTTPS. Użytkownicy teraz można podłączyć serwery tooSSAS przy użyciu adresu URL (na przykład https://servername/olap/msmdpump.dll) zamiast nazwy serwera i uwierzytelnianie podstawowe i anonimowe połączenia można używać w dodanie tooWindows uwierzytelniania. Aby uzyskać dodatkowe informacje na temat tooSSAS połączeń HTTP i HTTPS, zobacz [usługi tooAnalysis skonfiguruj HTTP dostępu](https://msdn.microsoft.com/library/gg492140.aspx).
* Obsługa Hive źródeł danych w usłudze HDInsight. Użytkownicy mogą teraz zarejestrować i wykrywa tabele programu Hive dla Apache Hive w Hadoop w HDInsight źródeł danych. Aby uzyskać dodatkowe informacje na temat Hive w usłudze HDInsight, zobacz hello [Centrum dokumentacji usługi HDInsight](../hdinsight/hdinsight-use-hive.md).
* Możliwość rejestrowania i odnajdywanie bazami danych Oracle i klastrów systemu plików HDFS jako kontenerów. Podczas rejestrowania programu Oracle tabele i widoki lub system plików HDFS, usługa Azure Data Catalog tworzy wpis hello bazy danych, tabel i widoków. Witaj bazy danych mogą być wykrywane i opatrzone adnotacjami przy użyciu portalu Azure Data Catalog hello. Użytkownicy mogą również wyszukiwanie i filtrowanie hello zawartości bazy danych lub klastra dodatkowo toosearching i filtrowanie zawartości hello hello katalogu.
* Obsługa ręcznie rejestrowanie typy źródeł danych nieznany. Użytkowników ręcznie wprowadzić informacje o źródle danych przy użyciu portalu Azure Data Catalog hello, dzięki czemu źródeł danych nie jest jawnie obsługiwany przez hello narzędzia rejestracji źródła danych można dodawać adnotacje i odnajdywane.
* Możliwość rejestrowania i wykrywania baz danych programu SQL Server jako kontenerów. Podczas rejestrowania programu SQL Server tabele i widoki, usługa Azure Data Catalog tworzy wpis hello bazy danych, tabel i widoków. Witaj bazy danych mogą być wykrywane i opatrzone adnotacjami przy użyciu portalu Azure Data Catalog hello. Użytkownicy mogą również wyszukiwanie i filtrowanie zawartości hello w toosearching dodaniu i filtrowania hello zawartość katalogu hello bazy danych.

> [!NOTE]
> SSAS i SSRS obiektów, które zostały zarejestrowane toohello wcześniejszych wersji 18 września musi ponownie zarejestrowane przy użyciu narzędzia rejestracji źródła danych hello przed hello modelu lub serwer jest dodawany wpis katalogu toohello. Ponowne rejestrowanie źródła danych nie ma wpływu na dodanych przez użytkowników w portalu Azure Data Catalog hello adnotacji.

> [!NOTE]
> Oracle tabele i widoki plików HDFS i katalogi, które zostały zarejestrowane toohello wcześniejszych wersji 11 września, należy ponownie zarejestrować za pomocą narzędzia rejestracji źródła danych hello przed hello bazy danych lub w klastrze jest dodawany wpis katalogu toohello. Ponowne rejestrowanie źródła danych nie ma wpływu na dodanych przez użytkowników w portalu Azure Data Catalog hello adnotacji.

> [!NOTE]
> Tabel programu SQL Server i widoków, które zostały zarejestrowane toohello wcześniejszych wersji 4 września, należy ponownie zarejestrować za pomocą narzędzia rejestracji źródła danych hello przed dodaniem katalogu toohello hello wpis w bazie danych. Ponowne rejestrowanie źródła danych nie ma wpływu na dodanych przez użytkowników w portalu Azure Data Catalog hello adnotacji.

## <a name="whats-new-for-august-2015"></a>Nowości dotyczące sierpień 2015
Począwszy od sierpnia 2015 r. hello następujące funkcje zostały dodane tooAzure wykazu danych:

* Obsługa danych profilowania źródeł danych programu SQL Server i Oracle. Podczas rejestrowania programu SQL Server i Oracle tabele i widoki, użytkownicy mogą wybrać tooinclude danych profilu dla obiektów hello jest zarejestrowany. Profil danych Hello obejmuje statystyki na poziomie obiektu i na poziomie kolumny.
* Obsługa systemu plików HDFS Hadoop źródeł danych. Użytkownicy mogą teraz zarejestrować i odnajdywania systemu plików HDFS plików i katalogów.
* Obsługa zapewniające informacje dotyczące żądania dostępu do zarejestrowanych źródeł danych. Dla dowolnego zasobu zarejestrowanych danych użytkownicy mogą teraz zawierają instrukcje żądania dostępu, w tym adresy URL lub przesyłanie pocztą e-mail łączy, tooeasily zintegrować z istniejących narzędzi i procesów.
* Etykietki narzędzi dla tagów i ekspertów, toomake go łatwiejsze toodiscover co użytkownicy podano jakie metadane dla zarejestrowanych zasobów danych.
* Dodaliśmy nowe "Użytkownika" przycisk i menu tooour górnym pasku nawigacyjnym. To menu umożliwia użytkownikowi hello Zobacz hello toolog konto używane na tooAzure Data Catalog i toosign limit, w razie potrzeby. To menu zawiera również hello nazwy katalogu, która jest przydatna toodevelopers przy użyciu hello interfejsu API REST usługi Azure Data Catalog.
* Standard Edition tylko: Podczas dodawania zasobów toodata właścicieli, Azure Data Catalog obsługuje teraz zarówno kont użytkowników i grup zabezpieczeń jako właścicieli. tooadd grupę zabezpieczeń jako właściciela dla wybranych zasobów danych, można wprowadzić nazwę wyświetlaną grupy albo hello lub grupy hello UPN adresu e-mail, jeśli istnieje.
* Obsługa źródeł danych magazynu obiektów Blob Azure. Użytkownicy mogą teraz zarejestrować i odnajdywanie obiektów blob magazynu Azure i katalogów.

