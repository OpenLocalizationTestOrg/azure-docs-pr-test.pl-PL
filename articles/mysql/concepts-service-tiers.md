---
title: Warstw cenowych w bazie danych systemu Azure dla programu MySQL | Dokumentacja firmy Microsoft
description: Warstw cenowych w bazie danych systemu Azure dla programu MySQL
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 11/03/2017
ms.openlocfilehash: ae7e57e9b40f5194c15525a48843060bbccaa956
ms.sourcegitcommit: 38c9176c0c967dd641d3a87d1f9ae53636cf8260
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/06/2017
---
# <a name="azure-database-for-mysql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>Azure bazy danych MySQL opcje i wydajność: Poznaj, co jest dostępne w każdej warstwy cenowej
Podczas tworzenia bazy danych Azure dla serwera MySQL zdecydujesz się na trzy główne opcje do konfigurowania zasobów przydzielonych dla tego serwera. Te opcje wpływ na wydajność i skalę serwera.
- Warstwa cenowa
- Jednostki obliczeniowe
- Magazyn (GB)

Każda warstwa cenowa ma zakres poziomy wydajności (jednostki obliczeniowe) do wyboru, w zależności od wymagań obciążenia. Wyższe poziomy wydajności serwera na celu zapewnienie wyższej przepustowości zapewnienia jej dodatkowych zasobów. Można zmienić warstwy cenowej praktycznie bez przestojów aplikacji poziomu wydajności serwera.

> [!IMPORTANT]
> Gdy usługa znajduje się w publicznej wersji zapoznawczej, nie istnieje gwarantowane Umowa dotycząca poziomu usług (SLA).

Na serwerze usługi Azure Database for MySQL może znajdować się jedna lub wiele baz danych. Można wybrać opcję utworzenia jednej bazy danych na serwer w celu wykorzystania wszystkich zasobów. Można też utworzyć wiele baz danych, współdzielących zasoby. 

## <a name="choose-a-pricing-tier"></a>Wybierz poziom cenowy
W wersji zapoznawczej, baza danych Azure dla programu MySQL zapewnia dwie warstwy cenowej: Basic i Standard. Warstwy Premium nie są jeszcze dostępne, ale będzie dostępna wkrótce. 

Poniższa tabela zawiera przykłady warstw cenowych najlepiej nadaje się do różnych obciążeń aplikacji.

| Warstwa cenowa | Docelowe obciążenia |
| :----------- | :----------------|
| Podstawowa | Najodpowiedniejsza dla małych obciążeń, które wymagają skalowalnych zasobów obliczeniowych i magazynowania, bez zagwarantowania IOPS. Przykłady obejmują serwery używane do tworzenia i testowania lub niewielkie, rzadko używane aplikacje. |
| Standardowa | Opcja Przejdź do chmury aplikacje wymagające IOPS gwarancja wysokiej przepływności. Przykładami sieci web lub aplikacji analitycznych. |
| Premium | Najodpowiedniejsza dla obciążeń wymagających małe opóźnienia transakcji i we/wy. Obsługuje najlepsze dla wielu użytkowników równocześnie. Zastosowanie do bazy danych, które obsługują misji kluczowych aplikacji.<br />Warstwa cenowa Premium nie jest dostępne w wersji zapoznawczej. |

Aby zdecydować się na warstwę cenową, najpierw uruchomić przez określenie, czy obciążenie musi gwarancji IOPS. Jeśli tak, użyj warstwa cenowa standardowa.

| **Funkcje warstwy cenowej** | **Podstawowa** | **Standardowa** |
| :------------------------ | :-------- | :----------- |
| Maksymalna obliczeń jednostki | 100 | 800 | 
| Maksymalna całkowita ilość miejsca | 1 TB | 1 TB | 
| Gwarancji IOPS magazynu | Nie dotyczy | Tak | 
| Maksymalna przestrzeń magazynowa IOPS | Nie dotyczy | 3,000 | 
| Okres przechowywania kopii zapasowych bazy danych | 7 dni | 35 dni | 

W okresie preview nie można zmienić warstwy cenowej po utworzeniu serwera. W przyszłości będzie można rejestrować uaktualnić lub starszą wersję serwera z jedną warstwę cenową do innej warstwy.

## <a name="understand-the-price"></a>Zrozumienie ceny
Podczas tworzenia nowej bazy danych Azure dla programu MySQL wewnątrz [portalu Azure](https://portal.azure.com/#create/Microsoft.MySQLServer), wybierz pozycję **warstwa cenowa** strony i miesięczny koszt jest wyświetlana na podstawie wybranych opcji. Jeśli nie masz subskrypcji platformy Azure, użyj Azure Kalkulator cen, aby pobrać szacowanej ceny. Odwiedź [Kalkulator cen platformy Azure](https://azure.microsoft.com/pricing/calculator/) witryny sieci Web, następnie kliknij przycisk **Dodaj elementy**, rozwiń węzeł **baz danych** kategorii i wybierz polecenie **bazy danych Azure dla programu MySQL** Aby dostosować opcje.

## <a name="choose-a-performance-level-compute-units"></a>Wybierz poziom wydajności (obliczeniowe jednostki)
Po określeniu warstwy cenowej bazy danych Azure, aby serwer MySQL, można przystąpić do określenia poziomu wydajności do poziomu, wybierając liczbę jednostek obliczeniowe potrzebne. Dobry punkt wyjścia jest 200 lub 400 jednostek obliczeniowe dla aplikacji, które wymaga wyższej współbieżności użytkownika do ich sieci web lub obciążeń analitycznych i Dostosuj przyrostowo zgodnie z potrzebami. 

Obliczenia bazy danych jednostki to miara przepływności przetwarzania procesora CPU, który może być dostępne dla pojedynczej bazy danych Azure dla serwera MySQL. Do obliczenia jest mieszanych pomiarach procesora CPU i zasobów pamięci.  Aby uzyskać więcej informacji, zobacz [wyjaśniający jednostki obliczeniowe](concepts-compute-unit-and-storage.md)

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

\*Maksymalny rozmiar magazynu serwera odnosi się do rozmiaru pamięci masowej elastycznie serwera.

## <a name="storage"></a>Magazyn 
Konfiguracja magazynu definiuje ilość dostępnej pojemności do bazy danych MySQL serwera Azure. Magazyn używany przez usługę zawiera pliki bazy danych, dzienników transakcji i MySQL dzienniki serwera. Należy wziąć pod uwagę rozmiar pamięci masowej niezbędne do obsługi baz danych i wymagania dotyczące wydajności (IOPS), wybierając konfiguracji magazynu.

Niektóre pojemność magazynu to na co najmniej o każdej warstwy cenowej wymienione w powyższej tabeli jako "Rozmiar magazynu dołączone." Podczas tworzenia serwera w przyrostach 125 GB do dozwolonych masowej można dodać dodatkowej pojemności. Niezależnie od konfiguracji jednostki obliczeniowe można skonfigurować dodatkowe miejsce. Zmiany ceny zależą od ilości przestrzeni dyskowej wybrane.

Konfiguracja IOPS w każdym poziomie wydajności odnosi się do warstwy cenowej i wybrany rozmiar magazynu. Warstwa podstawowa nie ma gwarancji IOPS. W ramach warstwa cenowa standardowa IOPS skalować proporcjonalnie maksymalny rozmiar magazynu w stałej stosunek 3:1. Magazyn dołączony gwarancji 125 GB dla 375 zainicjowana IOPS, każdy z we/wy o długości maksymalnie 256 KB. Istnieje możliwość dodatkowego magazynu maksymalnie 1 TB, aby zagwarantować 3000 elastycznie IOPS.

Monitorowanie wykres metryki w portalu Azure lub tworzenia poleceń wiersza polecenia platformy Azure do pomiaru użycia magazynu i IOPS. Odpowiednich metryk do monitorowania są limit magazynu, procent użycia magazynu, Magazyn używany i procent we/wy.

>[!IMPORTANT]
> W wersji zapoznawczej, wybierz ilość miejsca w magazynie w momencie utworzenia serwera. Zmiana rozmiaru magazynu na istniejącym serwerze nie jest jeszcze obsługiwany. 

## <a name="scaling-a-server-up-or-down"></a>Skalować serwer w górę lub w dół
Podczas tworzenia bazy danych Azure dla programu MySQL początkowo wybierz cenową warstwę i poziom wydajności. Później, jednostki obliczeniowe można skalować w górę lub w dół dynamicznie, w zakresie tej samej warstwie cenowej. W portalu Azure, przesuń jednostki obliczeniowe na stronie warstwa cenowa serwera lub skrypt go, postępując w tym przykładzie: [monitora i skalowania bazy danych Azure programu MySQL serwera przy użyciu wiersza polecenia platformy Azure](scripts/sample-scale-server.md)

Skalowanie jednostki obliczeniowe odbywa się niezależnie od maksymalny rozmiar magazynu wybrana.

W tle zmiana poziomu wydajności serwera na nowy poziom wydajności zostanie utworzona kopia oryginalnego serwera, a następnie przełącza połączenia z serwerem skopiowane. W trakcie tego procesu nie zostały utracone nie dane. Podczas krótki moment, gdy system przełącza się do nowej kopii serwera połączeń z bazą danych są wyłączone, więc niektóre transakcje w locie może zostać przywrócona. Czas przełączania jest zróżnicowany, ale średnio wynosi mniej niż 4 sekundy, a w ponad 99% przypadków wynosi mniej niż 30 sekund. Jeśli w momencie wyłączenia połączeń liczba bieżących transakcji będzie bardzo duża, czas przełączania może się wydłużyć.

Czas trwania procesu całej skali zależy od zarówno rozmiar i warstwę cenową serwera przed i po zmianie. Na przykład serwer, który jest zmiana obliczeniowe jednostek w warstwie cenowej standardowa powinno zakończyć w ciągu kilku minut. Nowe właściwości dla serwera nie są stosowane dopiero po zakończeniu zmiany.

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać więcej informacji o jednostkach obliczeniowe zobacz [wyjaśniający jednostki obliczeniowe](concepts-compute-unit-and-storage.md)
- Dowiedz się, jak [monitora i skalowania bazy danych Azure programu MySQL serwera przy użyciu wiersza polecenia platformy Azure](scripts/sample-scale-server.md)
