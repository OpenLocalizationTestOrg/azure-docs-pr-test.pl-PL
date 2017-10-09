---
title: "aaaWhat są pule elastyczne? Zarządzanie wielu baz danych SQL — Azure | Dokumentacja firmy Microsoft"
description: "Zarządzanie i skalowanie wielu baz danych SQL — setki i tysięcy - wykorzystujących pule elastyczne. Jedna cena dla zasobów, którą można dystrybuować, w razie potrzeby."
keywords: "wiele baz danych, bazy danych zasobów, wydajność bazy danych"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: b46e7fdc-2238-4b3b-a944-8ab36c5bdb8e
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 07/31/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 2098d7817ebe1277b5c131421f23c00803ec78f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-pools-help-you-manage-and-scale-multiple-sql-databases"></a>Elastyczne pule pozwalają na zarządzanie i skalowania wielu baz danych SQL

Pule elastyczne bazy danych SQL są proste i ekonomiczne rozwiązanie do zarządzania i skalowanie wielu baz danych, które mają wymagania użycia różnych i nieprzewidywalnych. Hello elastycznej puli baz danych na jednym serwerze bazy danych SQL Azure i udostępnianie jest określona liczba zasobów ([elastycznych jednostkach transakcji bazy danych](sql-database-what-is-a-dtu.md) (Edtu)) w cenie zestawu. Pule elastyczne w bazie danych SQL Azure zapewniają SaaS deweloperzy toooptimize hello cen wydajność grupę baz danych w ramach wyznaczonych budżetu dostarczając elastyczność wydajności dla każdej bazy danych.   

> [!NOTE]
> Pule elastyczne są ogólnodostępne we wszystkich regionach platformy Azure oprócz Indii Zachodnich, gdzie są obecnie dostępne w wersji zapoznawczej.  Pule elastyczne zostaną udostępnione ogólnie w tych regionach tak szybko, jak to możliwe.
>

## <a name="what-are-sql-elastic-pools"></a>Co to są pule elastyczne SQL? 

Deweloperzy SaaS tworzą aplikacje w oparciu o warstwy danych w dużej skali składające się z wielu baz danych. Wspólnego wzorca aplikacji jest tooprovision pojedynczej bazy danych dla każdego klienta. Ale różnych klientów często mają różne i nieprzewidywalnych wzorców użycia i jest trudne toopredict wymagań dotyczących zasobów hello każdego użytkownika poszczególne bazy danych. Tradycyjnie masz dwie opcje: 

- Nadmiernego udostępniania zasobów opartych na szczytowe użycie i za pośrednictwem płatności, lub
- Koszt na powitania koszt wydajności i odbiorcy zadowolenia podczas pików toosave niepełnego udostępniania. 

Pule elastyczne rozwiązać ten problem, zapewniając, który baz danych pobrać hello wydajności zasobów, które są im potrzebne, gdy są one wymagane. Udostępniają one prosty mechanizm alokacji zasobów w ramach przewidywalnego budżetu. toolearn więcej informacji na temat wzorców projektowych dla aplikacji SaaS wykorzystujących pule elastyczne, zobacz [wzorce projektowe dla wielodostępnych aplikacji SaaS przy użyciu usługi Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Elastic-databases-helps-SaaS-developers-tame-explosive-growth/player]
>

Pule elastyczne Włączanie hello developer toopurchase [elastycznych jednostkach transakcji bazy danych](sql-database-what-is-a-dtu.md) (Edtu) dla puli współużytkowane przez wiele nieprzewidywalne okresów tooaccommodate baz danych użycia przez pojedyncze bazy danych. Hello wymaganie eDTU dla puli jest określany przez użycie agregacji hello z jej baz danych. Witaj liczbę jednostek Edtu puli toohello dostępne jest kontrolowana przez hello developer budżetu. Deweloper Hello po prostu dodaje puli toohello baz danych, ustawia hello minimalna i maksymalna liczba jednostek Edtu hello baz danych, a następnie ustawia hello eDTU puli hello oparte na ich budżetu. Deweloper może użyć pul tooseamlessly wzrostu ich usługi z firmy dojrzałe tooa uruchamiania gotowa na coraz większej skali.

W ramach puli hello pojedynczych baz danych są podane hello elastyczność tooauto skali w ramach zestawu parametrów. Duże obciążenie bazy danych mogą zużywać więcej jednostek Edtu toomeet żądanie. Bazy danych pod niskim obciążeniem wykorzystują mniej jednostek eDTU, a bazy danych bez obciążenia nie zużywają jednostek eDTU. Inicjowanie obsługi administracyjnej zasobów dla całej puli hello, a nie dla pojedynczych baz danych upraszcza zadania związane z zarządzaniem. Dodatkowo mają przewidywalna budżetu hello puli. Dodatkowe Edtu można dodać istniejącej puli tooan bez przestojów bazy danych, z tą różnicą, że hello baz danych może być konieczne toobe przenieść hello tooprovide dodatkowe obliczeniowe zasobów dla hello nowe zastrzeżenie eDTU. Podobnie, jeśli dodatkowe jednostki eDTU nie są już potrzebne, można je usunąć z istniejącej puli w dowolnej chwili. I nie można dodać ani odjąć puli toohello baz danych. Jeśli baza danych przewidywalnie niewystarczająco wykorzystuje zasoby, należy ją przenieść.

Możesz utworzyć i zarządzać puli elastycznej za pomocą hello [portalu Azure](sql-database-elastic-pool-manage-portal.md), [PowerShell](sql-database-elastic-pool-manage-powershell.md), [języka Transact-SQL](sql-database-elastic-pool-manage-tsql.md), [C#](sql-database-elastic-pool-manage-csharp.md), i hello interfejsu API REST. 

## <a name="when-should-you-consider-a-sql-database-elastic-pool"></a>Kiedy należy rozważyć puli elastycznej bazy danych SQL

Pule są odpowiednie dla wielu baz danych o określonych wzorcach użycia. Dla danej bazy danych ten wzorzec charakteryzuje się niskim średnim wykorzystaniem oraz stosunkowo rzadkimi okresami zwiększonego użycia.

Witaj więcej baz danych można dodać tooa puli hello jest większa, stają się z oszczędności. W zależności od application wzorzec wykorzystania jest możliwe toosee oszczędności mających co najmniej dwóch S3 baz danych.  

Witaj poniższych sekcjach przedstawiono ułatwiające zrozumienie, jakie jak tooassess, jeśli w określonej kolekcji baz danych, które mogą korzystać z w puli. cześć przykłady pule standardowych, ale hello te same zasady mają zastosowanie również tooBasic i pule Premium.

### <a name="assessing-database-utilization-patterns"></a>Ocena wzorców użycia bazy danych

Witaj poniższej ilustracji przedstawiono przykład bazy danych, która zużywa dużo czasu bezczynności, ale również okresowo wzrósł z działaniem. Jest to wzorzec użycia, który jest odpowiedni dla puli:

   ![pojedyncza baza danych odpowiednia dla puli](./media/sql-database-elastic-pool/one-database.png)

Dla hello okres 5 minutową przedstawionym, pików DB1 się Dtu too90, ale jego średni całkowity użycia jest mniejsza niż 5 Dtu. S3 poziom wydajności jest wymagane toorun to obciążenie w pojedynczej bazy danych, ale spowoduje to pozostawienie większość zasobów hello nieużywane w okresach niskiej aktywności.

Pula umożliwia te nieużywane toobe Dtu współużytkowane przez wiele baz danych i tak zmniejsza koszt Dtu hello potrzebne i ogólnej.

Opierając się na powitania poprzedni przykład, załóżmy, że istnieją dodatkowe baz danych, podobne wzorce użycia jako DB1. W hello następne dwa poniższe rysunki, hello wykorzystania cztery bazy danych i 20 baz danych są warstwowego na powitania sam wykres tooillustrate hello nienakładający charakter ich użycia wraz z upływem czasu:

   ![cztery bazy danych z wzorcem użycia odpowiednim dla puli](./media/sql-database-elastic-pool/four-databases.png)

  ![dwadzieścia baz danych z wzorcem użycia odpowiednim dla puli](./media/sql-database-elastic-pool/twenty-databases.png)

za pomocą hello czarny wiersza w powyższej ilustracji hello przedstawiono Hello agregacji użycie jednostek DTU dla wszystkich baz danych 20. Oznacza to łączny użycie jednostek dtu w warstwie hello nigdy nie przekracza 100 Dtu czy wskazuje hello 20 baz danych można udostępniać 100 jednostek Edtu w tym przedziale czasu. Powoduje to zmniejszenie 20 x jednostek Dtu i 13 x cen redukcji porównaniu tooplacing poszczególnych baz danych hello S3 poziomów wydajności dla pojedynczej bazy danych.

W tym przykładzie jest idealnym rozwiązaniem hello z następujących powodów:

* Istnieją duże różnice między użyciem szczytowym a średnim użyciem na bazę danych.  
* Witaj szczytowego wykorzystania dla każdej bazy danych występuje w różnych punktach w czasie.
* Jednostki eDTU są współdzielone przez wiele baz danych.

Cena Hello puli jest funkcją hello jednostek Edtu puli. 1,5 x większa niż hello cenie jednostkowej jednostek DTU dla pojedynczej bazy danych jest hello cenie jednostkowej eDTU dla puli **jednostek Edtu puli może być współużytkowane przez wiele baz danych i potrzebne są mniej łączna liczba jednostek Edtu**. Te różnice w cennik i udostępnianie jednostek eDTU są podstawy hello hello cen oszczędności ryzyko zapewniają pule.  

Witaj przyjąć następujące reguły związane z toodatabase bazy danych i liczba wykorzystania pomocy tooensure polegającego na dostarczaniu puli zmniejszyć koszt w porównaniu toousing poziomy wydajności pojedynczej bazy danych.

### <a name="minimum-number-of-databases"></a>Minimalna liczba baz danych

Jeśli suma hello hello Dtu poziomów wydajności dla pojedynczej bazy danych jest więcej niż 1,5 x Edtu hello potrzebne do puli hello, puli elastycznej jest tańsze. Aby sprawdzić dostępne rozmiary, zobacz [limity liczby jednostek eDTU i magazynu dla pul elastycznych i elastycznych baz danych](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

***Przykład***<br>
Co najmniej dwa S3 baz danych lub co najmniej 15 S0 baz danych są potrzebne do 100 jednostek eDTU puli toobe bardziej ekonomiczne rozwiązanie niż używanie poziomów wydajności dla pojedynczej bazy danych.

### <a name="maximum-number-of-concurrently-peaking-databases"></a>Maksymalna liczba baz danych z równoczesnymi szczytami użycia

Za pomocą udostępniania jednostek Edtu, nie wszystkie bazy danych w puli można jednocześnie używać jednostek Edtu w górę toohello Ogranicz dostępne podczas używania poziomów wydajności dla pojedynczej bazy danych. Witaj mniejszą liczbę baz danych, które jednocześnie szczytowa, hello niższe eDTU puli hello może być zestaw i powitalne więcej puli ekonomicznego hello staje się. Ogólnie rzecz biorąc nie więcej niż 2/3 (lub 67%) baz danych hello w puli hello powinien jednocześnie szczytowa tootheir eDTU ograniczyć.

***Przykład***<br>
koszty tooreduce trzy S3 bazy danych w puli eDTU 200, co najwyżej dwa z tych baz danych można jednocześnie, jego szczytowa znacznie ich użycia. W przeciwnym razie jeśli więcej niż dwa z tych czterech baz danych S3 jednocześnie szczytowa, puli hello musi toomore toobe o rozmiarze niż 200 Edtu. Jeśli pula hello jest po zmianie rozmiaru toomore niż 200 jednostek Edtu, więcej S3 baz danych potrzebny toobe dodane toohello puli tookeep koszty niższy niż poziom wydajności dla pojedynczej bazy danych.

Należy pamiętać, że w tym przykładzie nie należy wziąć pod uwagę użycie innych baz danych w puli hello. Jeśli wszystkie bazy danych ma niektórych wykorzystania na dowolnym etapie w czasie, następnie mniej niż 2/3 (lub 67%) hello baz danych można szczytowa jednocześnie.

### <a name="dtu-utilization-per-database"></a>Użycie jednostek DTU na bazę danych
Duża różnica pomiędzy hello maksymalne i średnie wykorzystanie bazy danych wskazuje dłuższe okresy niskiego poziomu wykorzystania i krótkich okresach wysokie użycie. Ten wzorzec użycia jest idealny dla współużytkowania zasobów między bazami danych. Bazę danych należy rozważyć do umieszczenia w puli, jeśli jej szczytowe użycie jest ponad 1,5 raza większe niż jej średnie użycie.

***Przykład***<br>
Bazy danych programu S3 pików too100 Dtu i średnio używa 67 Dtu lub mniej, są odpowiednimi kandydatami do udostępniania jednostek Edtu w puli. Alternatywnie S1 bazą danych pików too20 Dtu i wykorzystuje średnio 13 Dtu lub mniej, są odpowiednimi kandydatami do puli.

## <a name="how-do-i-choose-hello-correct-pool-size"></a>Jak wybrać rozmiar puli poprawne hello?

Hello najlepszy rozmiar puli zależy od hello łączna liczba jednostek Edtu i zasobów magazynowania potrzebnych dla wszystkich baz danych w puli hello. Obejmuje to określania hello większych hello następującego:

* Maksymalna liczba jednostek Dtu wykorzystywane przez wszystkie bazy danych w puli hello.
* Wykorzystywany przez wszystkie bazy danych w puli hello bajtów pamięci masowej.

Aby sprawdzić dostępne rozmiary, zobacz [limity liczby jednostek eDTU i magazynu dla pul elastycznych i elastycznych baz danych](#what-are-the-resource-limits-for-elastic-pools).

Baza danych SQL automatycznie ocenia użycie zasobów historycznych hello baz danych na istniejącym serwerze bazy danych SQL i zaleca konfiguracji odpowiedniej puli hello w hello portalu Azure. W dodatku toohello zalecenia wbudowane środowisko szacuje hello użycie w jednostkach eDTU dla niestandardową grupę baz danych na powitania serwera. Dzięki temu możesz toodo analizy "warunkowej" interaktywnie Dodawanie puli toohello baz danych i usuwając je analizy użycia zasobów tooget i zmiany rozmiaru porady przed zatwierdzeniem zmiany. Aby uzyskać instrukcje, zobacz [Monitorowanie puli elastycznej, zmienianie jej rozmiaru i zarządzanie nią](sql-database-elastic-pool-manage-portal.md).

W przypadkach, gdy nie można użyć narzędzia hello następujący krok po kroku można oszacować, czy pula jest bardziej ekonomiczne rozwiązanie niż pojedyncze bazy danych:

1. Szacowanie Edtu hello potrzebne dla puli hello w następujący sposób:

   MAX(<*łączna liczba baz danych* X *średnie użycie jednostek DTU na bazę danych*>,<br>
   <*liczba baz danych jednocześnie osiągających szczyt użycia* X *użycie szczytowe jednostek DTU na bazę danych*)
2. Szacowanie hello potrzebne dla puli hello przez dodanie hello liczbę bajtów potrzebnych dla wszystkich hello baz danych w puli hello miejsca do magazynowania. Następnie określ rozmiar puli eDTU hello, który zawiera ten ilość miejsca w magazynie. Aby uzyskać informacje o limitach magazynu puli na podstawie rozmiaru puli w jednostkach eDTU, zobacz [limity liczby jednostek eDTU i magazynu dla pul elastycznych i elastycznych baz danych](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).
3. Zająć hello hello szacunków eDTU większych z kroku 1 i 2.
4. Zobacz hello [bazy danych SQL cennikiem](https://azure.microsoft.com/pricing/details/sql-database/) i Znajdź rozmiaru hello najmniejszą liczbę jednostek eDTU puli, która jest większa niż szacowania hello w kroku 3.
5. Porównanie cen puli hello z kroku 5 toohello cena za pomocą hello poziomy wydajności odpowiednie dla pojedynczych baz danych.

### <a name="changing-elastic-pool-resources"></a>Zmiana elastycznej puli zasobów

Można zwiększyć lub zmniejszyć hello zasoby dostępne tooan elastycznej puli na podstawie potrzeb dotyczących zasobów.

* Zmiana hello minimalna liczba jednostek Edtu na bazę danych lub maksymalna liczba jednostek Edtu na bazę danych zazwyczaj kończy się w ciągu 5 minut lub mniej.
* Zmiana hello Edtu na pulę, zależy od hello łączną ilość miejsca używanego przez wszystkie bazy danych w puli hello. Wprowadzanie zmian trwa średnio 90 minut na każde 100 GB. Na przykład jeśli całkowita ilość miejsca hello jest używany przez wszystkie bazy danych w puli hello jest 200 GB, a następnie hello oczekuje się, że czas oczekiwania na zmianę hello puli eDTU na pulę wynosi 3 godziny lub mniej.

## <a name="what-are-hello-resource-limits-for-elastic-pools"></a>Jakie są ograniczenia zasobów powitania dla pul elastycznych?

następujące tabele Hello opisano hello zasobów limity pul elastycznych.  Należy zauważyć, że limity zasobów hello pojedynczych baz danych w puli elastycznej zazwyczaj hello takie same jak w przypadku pojedynczych baz danych poza puli na podstawie Dtu i hello warstwy usług.  Na przykład hello max równoczesnych procesów roboczych S2 bazy danych to 120 pracowników.  Tak hello max równoczesnych procesów roboczych dla bazy danych w puli standardowej jest również 120 pracowników Jeśli hello max DTU na bazę danych w puli hello to 50 jednostek Dtu (co jest równoważne tooS2).

[!INCLUDE [SQL DB service tiers table for elastic pools](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Jeśli używane są wszystkie Dtu puli elastycznej, każda baza danych w puli hello odbiera równa ilości zasobów tooprocess zapytania.  Witaj usługi baza danych SQL zawiera sprawiedliwe przydzielanie zasobów między bazami danych, zapewniając równe wycinków czasu obliczeniowego udostępnianie zasobów. Udostępnianie sprawiedliwe przydzielanie zasobów dla elastycznej puli zasobów jest dodatkowo tooany ilości zasobów, w przeciwnym razie gwarantowane tooeach bazy danych, gdy hello minimalna wartość DTU na bazę danych jest ustawiona wartość niezerową tooa.

### <a name="database-properties-for-pooled-databases"></a>Właściwości bazy danych dla puli baz danych

Witaj w poniższej tabeli opisano właściwości hello puli baz danych.

| Właściwość | Opis |
|:--- |:--- |
| Maksymalna liczba jednostek eDTU na bazę danych |Witaj maksymalną liczbę jednostek Edtu, że wszystkie bazy danych w puli hello mogą użyć, jeśli dostępne na podstawie wykorzystania przez innych baz danych w puli hello.  Maksymalna liczba jednostek eDTU na bazę danych nie jest gwarancją zasobów dla bazy danych.  To ustawienie jest ustawienie globalne stosuje tooall hello puli baz danych. Wartość maksymalna liczba jednostek Edtu na bazę danych pików toohandle wystarczająco duża użycia bazy danych. Pewien stopień nadmiarowego zatwierdzania oczekuje się, ponieważ puli hello przyjęto założenie wzorców użycia gorącego i zimnych dla baz danych gdzie wszystkie bazy danych są nie jednocześnie peaking. Na przykład, załóżmy, że hello szczytowego wykorzystania dla jednej bazy danych jest 20 jednostek Edtu i tylko 20% baz danych hello 100 w puli hello szczytu na powitania tym samym czasie.  Jeśli eDTU hello max dla jednej bazy danych ma wartość Edtu too20, jest uzasadnione tooovercommit hello puli 5 razy, a zestaw hello Edtu na pulę too400. |
| Minimalna liczba jednostek eDTU na bazę danych |Witaj minimalną liczbę jednostek Edtu, że wszystkie bazy danych w puli hello jest gwarantowana.  To ustawienie jest ustawienie globalne stosuje tooall hello puli baz danych. Hello minimalną liczbę jednostek eDTU na bazę danych można ustawić too0 i jest również hello wartości domyślnej. Ta właściwość jest ustawiona tooanywhere między 0 a hello wykorzystania średnią liczbę jednostek eDTU na bazę danych. iloczyn Hello hello liczba baz danych w puli hello i hello minimalna liczba jednostek Edtu na bazę danych nie może przekraczać hello Edtu na pulę.  Na przykład jeśli pula zawiera 20 bazy danych i hello minimalna eDTU na bazę danych, ustaw too10 jednostek Edtu, następnie hello Edtu na pulę musi być przynajmniej tak duże jak Edtu 200. |
| Maksymalny rozmiar magazynu danych na bazę danych |Witaj pamięci masowej dla bazy danych w puli. Puli baz danych udostępnić puli magazynu, więc magazynu bazy danych jest ograniczona toohello mniejszych pozostałych puli magazynu i maksymalnej pamięci masowej na bazę danych. Maksymalna liczba magazyn na bazę danych odwołuje się toohello maksymalny rozmiar plików danych hello i nie zawiera hello miejsca używanego przez pliki dziennika. |
|||

## <a name="using-other-sql-database-features-with-elastic-pools"></a>Używanie innych funkcji bazy danych SQL z pul elastycznych

### <a name="elastic-jobs-and-elastic-pools"></a>Zadania elastyczne i pul elastycznych

W przypadku puli zadania zarządzania są uproszczone dzięki uruchamianiu skryptów w **[zadaniach elastycznych](sql-database-elastic-jobs-overview.md)**. Zadanie elastyczne eliminuje większość monotonnych czynności związanych z dużą liczbą baz danych. toobegin, zobacz [wprowadzenie zadania elastyczne](sql-database-elastic-jobs-getting-started.md).

Aby uzyskać więcej informacji na temat innych narzędzi do pracy z wieloma bazami danych, zobacz artykuł dotyczący [skalowania w poziomie za pomocą usługi Azure SQL Database](sql-database-elastic-scale-introduction.md).

### <a name="business-continuity-options-for-databases-in-an-elastic-pool"></a>Opcje ciągłości działania dla baz danych w puli elastycznej
Baz danych w puli zazwyczaj Obsługa hello sam [funkcjach ciągłości biznesowej](sql-database-business-continuity.md) , które są dostępne toosingle baz danych.

- **Punktu w czasie przywracania**: punktu w czasie przywracania używa automatycznego bazy danych toorecover kopii zapasowych bazy danych w puli tooa określonego punktu w czasie. Zobacz [Przywracanie do punktu w czasie](sql-database-recovery-using-backups.md#point-in-time-restore).

- **Geograficzne**: geograficzne zapewnia hello domyślna opcja odzyskiwania, gdy baza danych jest niedostępna z powodu zdarzenia w regionie hello, gdzie jest hostowana hello bazy danych. Zobacz [przywracania bazy danych SQL Azure lub pracy awaryjnej tooa dodatkowej](sql-database-disaster-recovery.md)

- **Aktywna replikacja geograficzna**: w przypadku aplikacji, które są bardziej agresywną wymagania odzyskiwania niż geograficzne mogą oferować, skonfigurować [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md).

## <a name="manage-sql-database-elastic-pools-using-hello-azure-portal"></a>Zarządzaj pulami elastycznej bazy danych SQL przy użyciu hello portalu Azure

### <a name="creating-a-new-sql-database-elastic-pool-using-hello-azure-portal"></a>Tworzenie nowej puli elastycznej bazy danych SQL przy użyciu hello portalu Azure

Istnieją dwa sposoby w hello portalu Azure można utworzyć puli elastycznej. Możesz zrobić to od początku, jeśli znasz ustawienia puli hello, lub uruchomić zgodnie z zaleceniami hello usługi. SQL Database ma wbudowane narzędzie analizy zalecane ustawienia puli elastycznej, jeśli jest to bardziej ekonomiczne na podstawie hello poza danych telemetrii użycia baz danych. 

Tworzenie z istniejącej puli elastycznej **serwera** bloku w portalu hello jest hello Najprostszym sposobem toomove istniejących baz danych w puli elastycznej. Można również utworzyć puli elastycznej, wyszukując **puli elastycznej SQL** w hello **Marketplace** lub klikając **+ Dodaj** w hello **pule elastyczne SQL**Przeglądaj bloku. Jesteś toospecify stanie nowego lub istniejącego serwera do obsługi przepływu pracy w tej puli.

> [!NOTE]
> Można utworzyć wiele pul na serwerze, ale nie można dodać bazy danych z różnych serwerów do hello tej samej puli.
>  

Witaj warstwa cenowa puli określa hello funkcji elastics toohello dostępne w puli hello i hello maksymalną liczbę jednostek Edtu (maks. wartość eDTU) i bazy danych dostępności tooeach magazynu (GB). Aby uzyskać więcej informacji, zobacz [warstwy usług](#edtu-and-storage-limits-for-elastic-pools).

Kliknij toochange hello warstwę cenową dla puli hello **warstwa cenowa**, kliknij hello cenowym, a następnie kliknij przycisk **wybierz**.

> [!IMPORTANT]
> Po wybraniu hello warstwy cenowej i zatwierdź zmiany, klikając **OK** w ostatnim kroku hello, nie będzie hello stanie toochange cenowym hello puli. toochange hello warstwę cenową istniejącej puli elastycznej, tworzenie elastycznej puli w hello żądanej warstwy cenowej i Migrowanie hello baz danych toothis nową pulę.
>

Jeśli hello baz danych, z którymi pracujesz ma za mało danych telemetrii historycznych danych użycia, hello **szacowane eDTU i GB użycia** wykresu i hello **rzeczywiste użycie jednostek eDTU** toohelp aktualizacji wykresu słupkowego wprowadzeniu konfiguracji decyzji. Ponadto hello usługi może spowodować toohelp komunikat zalecenie hello możesz odpowiedniego rozmiaru puli.

Hello usługi SQL Database ocenia historyczne dane użycia i zaleca jednej lub kilku pul, gdy jest bardziej ekonomiczne rozwiązanie niż używanie pojedynczych baz danych. Każde zalecenie jest konfigurowane z unikatowym podzbiorem powitania serwera baz danych, które najlepiej odpowiadają hello puli.

![zalecana pula](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

Witaj zalecenie puli obejmuje:

- Warstwę cenową dla puli hello (Basic, Standard, Premium lub Premium RS)
- Odpowiednie **Jednostki eDTU PULI** (określane również jako Maks. wartość eDTU na pulę)
- Witaj **maks. wartość eDTU** i **min. wartość eDTU** na bazę danych
- Witaj listę zalecanych baz danych dla puli hello

> [!IMPORTANT]
> Usługa Hello uwzględnia hello ostatnich 30 dni telemetrii podczas rekomendowania pul. Dla toobe bazy danych, traktowane jako kandydatem do puli elastycznej musi istnieć co najmniej 7 dni. Bazy, które znajdują się już w puli elastycznej, nie są brane pod uwagę podczas tworzenia zaleceń dla puli elastycznej.
>

Hello usługa oblicza zapotrzebowanie na zasoby oraz opłacalność przenoszenia hello jednej bazy danych w poszczególnych warstwach usług w pulach hello sam warstwy. Na przykład wszystkie bazy danych w warstwie Standardowej na serwerze są oceniane pod względem dopasowania do Standardowej puli elastycznej. Oznacza to, że usługa hello nie tworzy zalecenia dotyczące warstwy między takich jak przeniesienie standardowe bazy danych do puli Premium.

Po dodaniu puli toohello baz danych, zalecenia są generowane dynamicznie na podstawie hello historycznych danych użycia hello baz danych, wybrana przez Ciebie. Te zalecenia są wyświetlane w hello jednostek eDTU i GB wykres użycia i transparent zalecenie u góry hello hello **Konfigurowanie puli** bloku. Te zalecenia są zamierzone tooassist można utworzyć puli elastycznej zoptymalizowane pod kątem konkretnych baz danych.

![zalecenia dynamiczne](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

### <a name="manage-and-monitor-an-elastic-pool"></a>Zarządzanie i monitorowanie puli elastycznej

W portalu Azure hello można monitorować użycie hello puli elastycznej i baz danych hello w tej puli. Można również utworzyć zestaw zmian tooyour puli elastycznej i Prześlij wszystkie zmiany na powitania sam czas. Te zmiany obejmują dodawanie lub usuwanie baz danych, zmiana ustawień puli elastycznej lub zmiany ustawień bazy danych.

powitania po grafika przedstawia przykład puli elastycznej. Widok Hello zawiera:

*  Wykresy do monitorowania użycia zasobów, zarówno hello puli elastycznej i hello zawartych baz danych w puli hello.
*  Witaj **Konfiguruj** puli toomake przycisku zmienia toohello puli elastycznej.
*  Witaj **Utwórz bazę danych** przycisku, który tworzy bazę danych i dodaje go toohello bieżącej puli elastycznej.
*  Zadania elastyczne, które ułatwiają zarządzanie dużej liczby baz danych, uruchamiając skrypty Transact SQL wszystkich baz danych na liście.

![Widok puli](./media/sql-database-elastic-pool-manage-portal/basic.png)

Możesz toosee określonej puli tooa jego wykorzystania zasobów. Domyślnie pula hello jest użycie magazynu i eDTU tooshow skonfigurowanych hello ostatniej godziny. Wykres Hello może być skonfigurowany tooshow różnych metryk za pośrednictwem różnych czas systemu windows. Kliknij przycisk hello **wykorzystania zasobów** wykresu w obszarze **monitorowania puli elastycznej** tooshow szczegółowy widok hello określonej metryki za pośrednictwem hello określone okno czasu.

![Monitorowanie puli elastycznej](./media/sql-database-elastic-pool-manage-portal/basic-2.png)

![Blok metryki](./media/sql-database-elastic-pool-manage-portal/metric.png)

### <a name="toocustomize-hello-chart-display"></a>Wyświetl wykres hello toocustomize

Można edytować hello wykres i toodisplay bloku metryki hello innych metryk, takich jak procent, procent we/wy danych i dziennika we/wy procent wykorzystania procesora CPU.

![Kliknij przycisk Edytuj](./media/sql-database-elastic-pool-manage-portal/edit-metric.png)

Na powitania **Edytuj wykres** formularza, wybierz zakres czasu (Ostatnia godzina dzisiaj, lub ostatni tydzień), lub kliknij przycisk **niestandardowych** tooselect data zakresu w hello ostatnich dwóch tygodni. Można wybrać pasek lub wykres liniowy, a następnie wybierz hello toomonitor zasobów.

> [!Note]
> Tylko metryki z tej samej jednostki miary można wyświetlić w hello hello pod adresem hello sam czas. Na przykład w przypadku wybrania "procent liczby jednostek eDTU" następnie możesz wybrać tylko innych metryk odsetku hello jednostką miary.
>

[Kliknij przycisk Edytuj](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

### <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Zarządzanie i monitorowanie baz danych w puli elastycznej

Można również monitorować pojedyncze bazy danych dla potencjalne problemy. W obszarze **elastycznej bazy danych monitorowania**, jest wykres przedstawia metryki pięć baz danych. Domyślnie program hello wykres Wyświetla hello top 5 baz danych w puli hello przez użycie średnią liczbę jednostek eDTU w hello ostatniej godziny. 

![Monitorowanie puli elastycznej](./media/sql-database-elastic-pool-manage-portal/basic-3.png)

Kliknij przycisk hello **użycie w jednostkach eDTU dla bazy danych dla hello ostatniej godziny** w obszarze **elastycznej bazy danych monitorowania**. Spowoduje to otwarcie **wykorzystania zasobów bazy danych** i udostępnia szczegółowy widok hello użycia bazy danych w puli hello. Przy użyciu siatki hello w dolnej części bloku hello hello, można wybrać żadnych baz danych w toodisplay puli hello jej użycie w hello wykresu (w górę too5 baz danych). Można również dostosować hello metryki i przedziału czasowego wyświetlane na wykresie hello klikając **Edytuj wykres**.

![Blok wykorzystanie zasobów bazy danych](./media/sql-database-elastic-pool-manage-portal/db-utilization.png)

### <a name="toocustomize-hello-view"></a>Widok hello toocustomize

Edytuj hello wykresu tooselect zakres czasu (Ostatnia godzina lub po 24 godzinach), lub kliknij przycisk **niestandardowych** tooselect różnych dziennie w hello poza toodisplay 2 tygodnie.

![Kliknij pozycję Edytuj wykres](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

![Kliknij przycisk niestandardowe](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

Możesz również kliknąć hello **porównania baz danych przez** tooselect listy rozwijanej różne metryki toouse podczas porównywania baz danych.

![Edytuj wykres hello](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect toomonitor baz danych

Na liście bazy danych hello w hello **wykorzystania zasobów bazy danych** bloku można znaleźć określonej bazy danych przez wyszukiwanie stronach hello liście hello lub wpisując hello nazwę bazy danych. Użyj hello wyboru tooselect hello bazy danych.

![Wyszukaj toomonitor baz danych](./media/sql-database-elastic-pool-manage-portal/select-dbs.png)


### <a name="add-an-alert-tooan-elastic-pool-resource"></a>Dodaj zasób puli elastycznej tooan alertu

Można dodać reguły tooan elastycznej puli, która Wyślij wiadomość e-mail punkty końcowe tooURL ciągów toopeople lub alert, kiedy puli elastycznej hello trafienia ustawiony próg użycia.

**tooadd zasobów tooany alertu:**

1. Kliknij hello **wykorzystania zasobów** hello tooopen wykresu **Metryka** bloku, kliknij przycisk **Dodaj alert**, a następnie wprowadź informacje hello w hello **Dodawanie alertu Reguła** bloku (**zasobów** są automatycznie konfigurowane pracy z puli hello toobe).
2. Wpisz **nazwa** i **opis** , które identyfikują hello tooyou alertów oraz odbiorców hello.
3. Wybierz **Metryka** , które mają tooalert z listy hello.

    Wykres Hello dynamicznie pokazuje wykorzystania zasobów dla tego toohelp metryki, wybierz próg.

4. Wybierz **warunku** (większe niż poniżej, itd.) i **próg**.
5. Wybierz **okres** hello metryki czasu reguły muszą zostać spełnione przed hello wyzwalaczy alertu.
6. Kliknij przycisk **OK**.

Aby uzyskać więcej informacji, zobacz [tworzyć alerty bazy danych SQL w portalu Azure](sql-database-insights-alerts-portal.md).

### <a name="move-a-database-into-an-elastic-pool"></a>Przenoszenie bazy danych w puli elastycznej

Można dodać lub usunąć bazy danych z istniejącej puli. Witaj baz danych może być w innych pulach. Jednak można dodawać tylko baz danych, które są na hello sam serwer logiczny.

 ![Kliknij przycisk Konfiguruj pulę](./media/sql-database-elastic-pool-manage-portal/configure-pool.png)

![Kliknij przycisk Dodaj toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)

![Wybierz tooadd baz danych](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

![Dodawanie puli oczekujące](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

![Klikanie pozycji Zapisz.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="move-a-database-out-of-an-elastic-pool"></a>Przenoszenie bazy danych z puli elastycznej

![Wyświetlanie listy baz danych](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

![Wyświetlanie listy baz danych](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

![Podgląd bazy danych Dodawanie i usuwanie](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

![Klikanie pozycji Zapisz.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="change-performance-settings-of-an-elastic-pool"></a>Zmień ustawienia wydajności puli elastycznej

Podczas monitorowania wykorzystania zasobów hello elastycznej puli może stwierdzić, że pewnych zmian są potrzebne. Może być pula hello wymaga zmiany hello limity wydajność lub pamięć masową. Prawdopodobnie ma toochange hello ustawienia do bazy danych w puli hello. Można zmienić ustawienia hello puli hello w dowolnym czasie tooget hello równowagę wydajności i kosztów. Zobacz [kiedy należy puli elastycznej użyć?](sql-database-elastic-pool.md) Aby uzyskać więcej informacji.

toochange hello jednostek Edtu i Magazyn limity dla każdej puli i jednostek Edtu na bazę danych:

![Użycie zasobów w puli elastycznej](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

![Aktualizacja puli elastycznej i nowych miesięczny koszt](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="manage-sql-database-elastic-pools-using-powershell"></a>Zarządzaj pulami elastycznej bazy danych SQL przy użyciu programu PowerShell

toocreate i zarządzać pule elastyczne bazy danych SQL przy użyciu programu Azure PowerShell, użyj następującego polecenia cmdlet programu PowerShell hello. Jeśli konieczne tooinstall lub uaktualnić programu PowerShell, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps). toocreate i zarządzania nimi można znaleźć bazy danych, serwerów i reguły zapory, [Utwórz i Zarządzaj serwerami bazy danych SQL Azure i baz danych przy użyciu programu PowerShell](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-powershell). 

> [!TIP]
> Dla programu PowerShell przykładowe skrypty, zobacz [tworzenie elastycznych pul i przenoszenia baz danych między pulami i z puli przy użyciu programu PowerShell](scripts/sql-database-move-database-between-pools-powershell.md) i [toomonitor Użyj programu PowerShell i skali Pula elastyczna SQL w bazie danych SQL Azure](scripts/sql-database-monitor-and-scale-pool-powershell.md).
>

| Polecenie cmdlet | Opis |
| --- | --- |
|[Nowe AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool)|Tworzy elastycznej puli baz danych na serwerze logicznym SQL.|
|[Get-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/get-azurermsqlelasticpool)|Pobiera pule elastyczne i ich wartości właściwości na serwerze logicznym SQL.|
|[Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)|Modyfikuje właściwości elastycznej puli baz danych na serwerze logicznym SQL.|
|[Remove-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/remove-azurermsqlelasticpool)|Usuwa elastycznej puli baz danych na serwerze logicznym SQL.|
|[Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity)|Pobiera stan hello działań w puli elastycznej na serwerze logicznym SQL.|
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Tworzy nową bazę danych w istniejącej puli lub jako pojedynczej bazy danych. |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Pobiera jeden lub więcej baz danych.|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Ustawia właściwości dla bazy danych lub istniejącą bazę danych są przenoszone do z i między pule elastyczne.|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Usuwa z bazy danych.|

> [!TIP]
> Tworzenie wielu baz danych w puli elastycznej może trwać, jeśli odbywa się za pomocą portalu hello lub poleceń cmdlet programu PowerShell, który tworzenie tylko jednej bazy danych w czasie. Tworzenie tooautomate w puli elastycznej, zobacz [CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).
>

## <a name="manage-sql-database-elastic-pools-using-hello-azure-cli"></a>Zarządzaj pulami elastycznej bazy danych SQL przy użyciu hello wiersza polecenia platformy Azure

toocreate i zarządzanie nimi pule elastyczne bazy danych SQL z hello [interfejsu wiersza polecenia Azure](/cli/azure/overview), poniższych hello [bazy danych SQL interfejsu wiersza polecenia Azure](/cli/azure/sql/db) poleceń. Użyj hello [powłoki chmury](/azure/cloud-shell/overview) toorun hello interfejsu wiersza polecenia w przeglądarce lub [zainstalować](/cli/azure/install-azure-cli) go na system macOS, Linux lub Windows. 

> [!TIP]
> Dla interfejsu wiersza polecenia Azure przykładowe skrypty, zobacz [toomove CLI Użyj bazy danych Azure SQL w puli elastycznej SQL](scripts/sql-database-move-database-between-pools-cli.md) i [tooscale Użyj wiersza polecenia platformy Azure puli elastycznej SQL w bazie danych SQL Azure](scripts/sql-database-scale-pool-cli.md).
>

| Polecenie cmdlet | Opis |
| --- | --- |
|[Tworzenie puli elastyczna az sql](/cli/azure/sql/elastic-pool#create)|Tworzy puli elastycznej.|
|[Lista elastyczna pula sql az](/cli/azure/sql/elastic-pool#list)|Zwraca listę pul elastycznych na serwerze.|
|[AZ pula elastyczna listy-baz danych sql](/cli/azure/sql/elastic-pool#list-dbs)|Zwraca listę baz danych w puli elastycznej.|
|[Elastyczna pula sql az listy — wersje](/cli/azure/sql/elastic-pool#list-editions)|Również obejmuje ustawienia jednostek dtu w warstwie dostępnej puli, limity magazynu, a dla ustawienia bazy danych. W kolejności tooreduce szczegółowości, limity dodatkowego miejsca do magazynowania i na bazę danych ustawienia są domyślnie ukryte.|
|[Aktualizacja elastyczna pula sql az](/cli/azure/sql/elastic-pool#update)|Aktualizuje puli elastycznej.|
|[Usuń elastyczna pula sql az](/cli/azure/sql/elastic-pool#delete)|Usuwa hello puli elastycznej.|

## <a name="manage-sql-database-elastic-pools-using-transact-sql"></a>Zarządzaj pulami elastycznej bazy danych SQL przy użyciu języka Transact-SQL

toocreate i przenoszenia baz danych w istniejącej puli elastycznej lub tooreturn informacje o puli elastycznej bazy danych SQL z Transact-SQL, użyj następującego polecenia T-SQL hello. Możesz wykonywać te polecenia przy użyciu hello portalu Azure, [programu SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), lub inny program, który można połączyć z serwerem bazy danych SQL Azure tooan i przekazać języka Transact-SQL polecenia. toocreate i zarządzania nimi można znaleźć bazy danych, serwerów i reguły zapory, [Utwórz i Zarządzaj serwerami bazy danych SQL Azure i baz danych przy użyciu języka Transact-SQL](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-transact-sql).

> [!IMPORTANT]
> Nie można tworzyć, aktualizować lub usuwać puli elastycznej bazy danych SQL Azure przy użyciu języka Transact-SQL. Można dodać lub usunąć z puli elastycznej bazy danych i używasz widoków DMV tooreturn informacje o istniejących pul elastycznych.
>

| Polecenie | Opis |
| --- | --- |
|[Utwórz bazę danych (baza danych Azure SQL)](/sql/t-sql/statements/create-database-azure-sql-database)|Tworzy nową bazę danych w istniejącej puli lub jako pojedynczej bazy danych. Musi być połączony toohello bazy danych master toocreate nową bazę danych.|
| [ALTER DATABASE (baza danych Azure SQL)](/sql/t-sql/statements/alter-database-azure-sql-database) |Przenoszenie bazy danych do z lub między elastyczne pule.|
|[Usuwanie bazy danych (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Usuwa z bazy danych.|
|[sys.elastic_pool_resource_stats (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-elastic-pool-resource-stats-azure-sql-database)|Zwraca statystyki użycia zasobów dla wszystkich hello elastyczne pule baz danych serwera logicznego. Dla każdej puli elastycznej bazy danych jest jeden wiersz dla każdej sekundzie 15 raportowania okna (cztery wiersze na minutę). W tym procesora CPU, we/wy, dziennika, użycia magazynu i użycie równoczesnych żądań/sesji przez wszystkie bazy danych w puli hello.|
|[sys.database_service_objectives (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Zwraca hello edition (warstwy usług), celem usługi (warstwa cenowa) i nazwę puli elastycznej dla bazy danych Azure SQL lub usługi Azure SQL Data Warehouse. Jeśli zalogowany toohello głównej bazy danych na serwerze bazy danych SQL Azure, zwraca informacje o wszystkich baz danych. Dla usługi Azure SQL Data Warehouse musi być połączony toohello bazy danych master.|

## <a name="manage-sql-database-elastic-pools-using-hello-rest-api"></a>Zarządzaj pulami elastycznej bazy danych SQL przy użyciu hello interfejsu API REST

toocreate i Zarządzaj pulami elastycznej bazy danych SQL przy użyciu hello interfejsu API REST, zobacz [interfejsu API REST bazy danych SQL Azure](/rest/api/sql/).

## <a name="next-steps"></a>Następne kroki

* Aby obejrzeć wideo, zobacz [Microsoft Virtual Academy kursu wideo na możliwości elastycznej bazy danych SQL Azure](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554)
* toolearn więcej informacji na temat wzorców projektowych dla aplikacji SaaS wykorzystujących pule elastyczne, zobacz [wzorce projektowe dla wielodostępnych aplikacji SaaS przy użyciu usługi Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).
* Samouczek SaaS wykorzystujących pule elastyczne, zobacz [toohello wprowadzenie aplikacji Wingtip SaaS](sql-database-wtp-overview.md).
