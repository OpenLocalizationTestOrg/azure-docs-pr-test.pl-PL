---
title: AAA "warstw cenowych w bazie danych systemu Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: Warstw cenowych w bazie danych systemu Azure dla programu MySQL
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 2a05f00aff4f7166f04e035eb2a47e7662888ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>Azure bazy danych MySQL opcje i wydajność: Poznaj, co jest dostępne w każdej warstwy cenowej
Podczas tworzenia bazy danych Azure dla serwera MySQL zdecydujesz na trzy główne opcje tooconfigure hello zasoby przydzielone do tego serwera. Te opcje wpływ hello wydajności i skalowania powitania serwera.
- Warstwa cenowa
- Jednostki obliczeniowe
- Magazyn (GB)

Każda warstwa cenowa ma zakres toochoose (jednostki obliczeniowe) poziomów wydajności, w zależności od wymagań obciążenia. Wyższe poziomy wydajności zapewnienia jej dodatkowych zasobów przepustowości wyższej zaprojektowanego toodeliver serwera. Można zmienić warstwy cenowej praktycznie bez przestojów aplikacji poziomu wydajności powitania serwera.

> [!IMPORTANT]
> Gdy usługa hello znajduje się w publicznej wersji zapoznawczej, nie istnieje gwarantowane Umowa dotycząca poziomu usług (SLA).

Na serwerze usługi Azure Database for MySQL może znajdować się jedna lub wiele baz danych. Opt toocreate pojedynczej bazy danych na serwerze tooutilize wszystkie zasoby hello lub utworzyć wiele baz danych tooshare hello zasobów. 

## <a name="choose-a-pricing-tier"></a>Wybierz poziom cenowy
W wersji zapoznawczej, baza danych Azure dla programu MySQL zapewnia dwie warstwy cenowej: Basic i Standard. Warstwy Premium nie są jeszcze dostępne, ale będzie dostępna wkrótce. 

Witaj Poniższa tabela zawiera przykłady hello ceny warstw najlepiej dopasowane do różnych obciążeń aplikacji.

| Warstwa cenowa | Docelowe obciążenia |
| :----------- | :----------------|
| Podstawowa | Najodpowiedniejsza dla małych obciążeń, które wymagają skalowalnych zasobów obliczeniowych i magazynowania, bez zagwarantowania IOPS. Przykłady obejmują serwery używane do tworzenia i testowania lub niewielkie, rzadko używane aplikacje. |
| Standardowa | Witaj Przejdź toooption chmury aplikacje wymagające IOPS gwarancja wysokiej przepływności. Przykładami sieci web lub aplikacji analitycznych. |
| Premium | Najodpowiedniejsza dla obciążeń wymagających małe opóźnienia transakcji i we/wy. Zapewnia obsługę najlepsze powitania dla wielu użytkowników równocześnie. Zastosowanie toodatabases obsługuje misji kluczowych aplikacji.<br />Warstwa cenowa Premium Hello nie jest dostępne w wersji zapoznawczej. |

toodecide o cenach warstwy pierwszego uruchomienia przez określenie, czy obciążenie musi gwarancji IOPS. Jeśli tak, użyj warstwa cenowa standardowa.

| **Funkcje warstwy cenowej** | **Podstawowa** | **Standardowa** |
| :------------------------ | :-------- | :----------- |
| Maksymalna obliczeń jednostki | 100 | 800 | 
| Maksymalna całkowita ilość miejsca | 1 TB | 1 TB | 
| Gwarancji IOPS magazynu | Nie dotyczy | Tak | 
| Maksymalna przestrzeń magazynowa IOPS | Nie dotyczy | 3,000 | 
| Okres przechowywania kopii zapasowych bazy danych | 7 dni | 35 dni | 

Podgląd okresie hello nie można zmienić warstwy cenowej po utworzeniu powitania serwera. W przyszłości hello będzie można możliwy tooupgrade lub starszą wersję serwera z warstwy tooanother warstwy cenowej.

## <a name="understand-hello-price"></a>Zrozumienie hello cen
Podczas tworzenia nowej bazy danych Azure dla programu MySQL wewnątrz hello [Azure Portal](https://portal.azure.com/#create/Microsoft.MySQLServer), kliknij przycisk hello **warstwa cenowa** bloku i hello miesięczny koszt będą wyświetlane na podstawie na wybrane opcje hello. Jeśli nie masz subskrypcji platformy Azure, użyj hello Azure tooget Kalkulator cen szacowanej ceny. Odwiedź hello [Azure Kalkulator cen](https://azure.microsoft.com/pricing/calculator/) witryny sieci Web, następnie kliknij przycisk **Dodaj elementy**, rozwiń hello **baz danych** kategorii i wybierz polecenie **bazy danych Azure dla programu MySQL**  toocustomize hello opcje.

## <a name="choose-a-performance-level-compute-units"></a>Wybierz poziom wydajności (obliczeniowe jednostki)
Po określeniu hello warstwy cenowej bazy danych Azure, aby serwer MySQL jesteś poziom wydajności hello toodetermine gotowy, wybierając numer hello jednostek obliczeniowe potrzebne. Dobry punkt wyjścia jest 200 lub 400 jednostek obliczeniowe dla aplikacji, które wymaga wyższej współbieżności użytkownika do ich sieci web lub obciążeń analitycznych i Dostosuj przyrostowo zgodnie z potrzebami. 

Obliczeniowe jednostki to miara przepływności przetwarzania procesora CPU, który jest gwarantowana tooa dostępne toobe pojedynczy MySQL serwera bazy danych Azure. Do obliczenia jest mieszanych pomiarach procesora CPU i zasobów pamięci.  Aby uzyskać więcej informacji, zobacz [wyjaśniający jednostki obliczeniowe](concepts-compute-unit-and-storage.md)

### <a name="basic-pricing-tier-performance-levels"></a>Podstawowe ceny warstwy poziomy wydajności:

| **Poziom wydajności** | **50** | **100** |
| :-------------------- | :----- | :------ |
| Obliczeniowe maksymalna liczba jednostek | 50 | 100 |
| Rozmiar magazynu dołączone | 50 GB | 50 GB |
| Maksymalny rozmiar magazynu serwera\* | 1 TB | 1 TB |

### <a name="standard-pricing-tier-performance-levels"></a>Standardowa cenową warstwy poziomy wydajności:

| **Poziom wydajności** | **100** | **200** | **400** | **800** |
| :-------------------- | :------ | :------ | :------ | :------ |
| Obliczeniowe maksymalna liczba jednostek | 100 | 200 | 400 | 800 |
| Rozmiar magazynu dołączone i elastycznie IOPS | 125 GB<br/> 375 IOPS | 125 GB<br/> 375 IOPS | 125 GB<br/> 375 IOPS | 125 GB<br/> 375 IOPS |
| Maksymalny rozmiar magazynu serwera\* | 1 TB | 1 TB | 1 TB | 1 TB |
| Udostępniony serwerowi maksymalna liczba IOPS | IOPS 3000 | IOPS 3000 | IOPS 3000 | IOPS 3000 |
| Udostępniony serwerowi maksymalna liczba IOPS na GB | Stałe IOPS 3 na GB | Stałe IOPS 3 na GB | Stałe IOPS 3 na GB | Stałe IOPS 3 na GB |

\*Maksymalny rozmiar magazynu serwera odwołuje się rozmiar maksymalny zainicjowanego magazynu toohello serwera.

## <a name="storage"></a>Magazyn 
Konfiguracja magazynu Hello określa hello magazynu pojemność dostępna tooan Azure bazy danych MySQL serwera. Magazyn Hello używany przez usługę hello obejmuje hello pliki bazy danych, dzienników transakcji i dzienniki serwera hello MySQL. Należy wziąć pod uwagę rozmiar hello toohost przestrzeń dyskową wymaganą baz danych i hello wymagania dotyczące wydajności (IOPS), wybierając hello konfiguracji magazynu.

Niektóre pojemność magazynu to na co najmniej o każdej warstwy cenowej wymienionych w powyższej tabeli jako "Rozmiar magazynu dołączone." hello Po utworzeniu powitania serwera w przyrostach 125 GB się toohello dozwolonych pamięci masowej można dodać dodatkowej pojemności. pojemność magazynu dodatkowe Hello można skonfigurować niezależnie od hello obliczeniowe jednostki konfiguracji. zmiany ceny Hello oparte na powitania ilość pamięci masowej wybrane.

Konfiguracja IOPS Hello w każdym poziomie wydajności odnosi się toohello warstwa cenowa i rozmiar magazynu hello wybrany. Warstwa podstawowa nie ma gwarancji IOPS. W ramach warstwy cenowej standardowa hello hello IOPS Skaluj proporcjonalnie rozmiar magazynu toomaximum w stałej stosunek 3:1. magazynu Hello uwzględnione gwarancji 125 GB dla 375 zainicjowana IOPS, każde z nich rozmiaru we/wy się too256 KB. Możesz wybrać dodatkowe miejsce do magazynowania się too1 TB maksymalna, tooguarantee 3000 elastycznie IOPS.

Monitor hello metryki wykres w hello Azure portalu lub zapisu wiersza polecenia platformy Azure polecenia toomeasure hello zużycie pamięci masowej i IOPS. Toomonitor odpowiednich metryk są limit magazynu, procent użycia magazynu, Magazyn używany i procent we/wy.

>[!IMPORTANT]
> Znajduje się w wersji zapoznawczej, wybierz hello ilości miejsca w czasie hello utworzenia powitania serwera. Zmiana rozmiaru magazynu hello na istniejącym serwerze nie jest jeszcze obsługiwany. 

## <a name="scaling-a-server-up-or-down"></a>Skalować serwer w górę lub w dół
Możesz wybrać początkowo hello cennik warstwę i poziom wydajności podczas tworzenia bazy danych Azure dla programu MySQL. Później można skalować hello obliczeniowe jednostki górę lub w dół dynamicznie, w zakresie hello hello same warstwy cenowej. W hello portalu Azure, przesuń hello obliczeniowe jednostki w bloku warstwa cenowa powitania serwera lub skryptu go, postępując w tym przykładzie: [monitora i skalowania bazy danych Azure programu MySQL serwera przy użyciu wiersza polecenia platformy Azure](scripts/sample-scale-server.md)

Skalowanie jednostki obliczeniowe hello odbywa się niezależnie od hello maksymalny rozmiar magazynu wybrana.

Tle hello zmiana hello poziomu wydajności bazy danych tworzy replikę hello oryginalnej bazy danych na powitania nowy poziom wydajności, a następnie przełącza połączeń toohello repliki. W trakcie tego procesu nie zostały utracone nie dane. Podczas hello krótki chwilę po przełączyć możemy toohello repliki bazy danych toohello połączeń są wyłączone, niektóre transakcje w locie może zostać przywrócona. Czas przełączania jest zróżnicowany, ale średnio wynosi mniej niż 4 sekundy, a w ponad 99% przypadków wynosi mniej niż 30 sekund. W przypadku dużej liczby transakcji w locie na powitania obecnie połączeń są wyłączone, tego okna może trwać dłużej.

czas trwania Hello hello skali całego procesu zależy od tego, zarówno rozmiar hello, jak i warstwy cenowej powitania serwera przed i po zmianie hello. Na przykład serwer, który jest zmiana obliczeniowe jednostek w ramach warstwy cenowej standardowa hello, powinno zakończyć w ciągu kilku minut. nowe właściwości Hello powitania serwera nie są stosowane dopiero po zakończeniu zmiany hello.

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać więcej informacji o jednostkach obliczeniowe zobacz [wyjaśniający jednostki obliczeniowe](concepts-compute-unit-and-storage.md)
- Dowiedz się, jak za[monitora i skalowania bazy danych Azure programu MySQL serwera przy użyciu wiersza polecenia platformy Azure](scripts/sample-scale-server.md)
