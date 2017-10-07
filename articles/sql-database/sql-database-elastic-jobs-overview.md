---
title: bazy danych chmury skalowalnych w poziomie aaaManaging | Dokumentacja firmy Microsoft
description: "Przedstawia usługa zadań hello elastycznej bazy danych"
metakeywords: azure sql database elastic databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 6fa47cf2-1162-4534-a206-6e2d95b78580
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: b6d330cd712421b8cba781e835830772e6e5b77e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-scaled-out-cloud-databases"></a>Zarządzanie bazami danych w chmurze skalowalnych w poziomie
Witaj toomanage skalowalnych w poziomie podzielonej baz danych, **zadania elastycznej bazy danych** funkcji (wersja zapoznawcza) umożliwia tooreliably można wykonać skryptu języka Transact-SQL (T-SQL) między grupą baz danych, w tym:

* niestandardowy zbiór baz danych (co omówiono poniżej)
* wszystkie bazy danych w [puli elastycznej](sql-database-elastic-pool.md)
* zestaw niezależnego fragmentu (utworzone za pomocą [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md)). 

## <a name="documentation"></a>Dokumentacja
* [Zainstaluj składniki zadania elastycznej bazy danych hello](sql-database-elastic-jobs-service-installation.md). 
* [Rozpoczynanie pracy z zadaniami elastycznej bazy danych](sql-database-elastic-jobs-getting-started.md).
* [Utwórz zadania i zarządzać nimi za pomocą programu PowerShell](sql-database-elastic-jobs-powershell.md).
* [Tworzenie i zarządzanie nimi skalowanej baz danych SQL Azure](sql-database-elastic-jobs-getting-started.md)

**Zadania elastyczne bazy danych** jest obecnie obsługiwana w środowisku klienta Azure usługi chmury, która umożliwia wykonanie hello ad hoc i zaplanowanych zadań administracyjnych, które są nazywane **zadania**. Z zadaniami można łatwo i niezawodnie Zarządzanie grupami dużych baz danych SQL Azure za pomocą operacji administracyjnych tooperform skrypty języka Transact-SQL. 

![Usługa zadań elastycznej bazy danych][1]

## <a name="why-use-jobs"></a>Dlaczego warto używać zadania?
**Zarządzanie**

Łatwe zmiany schematu, Zarządzanie poświadczeniami, aktualizacje danych odwołania, zbierania danych wydajności lub gromadzenia danych telemetrii dzierżawy (klienta).

**Raporty**

Agregowanie danych z kolekcji baz danych SQL Azure do tabeli pojedynczego miejsca docelowego.

**Zmniejszenie nakładów pracy**

Normalnie należy połączyć z bazą danych tooeach niezależnie w instrukcji języka Transact-SQL toorun kolejności lub wykonywanie innych zadań administracyjnych. Zadanie obsługuje zadania hello rejestrowania w bazie danych tooeach hello docelowej grupy. Możesz również zdefiniować, obsługa i utrwalić toobe skrypty języka Transact-SQL wykonywane przez grupę baz danych SQL Azure.

**Ewidencjonowanie aktywności**

Zadania są uruchamiane hello skrypt i dziennika hello stan wykonywania dla każdej bazy danych. Umożliwia również wyświetlenie automatyczny, gdy występują błędy.

**Elastyczność**

Zdefiniuj niestandardowe grupy baz danych SQL Azure oraz określić harmonogramy uruchamiania zadania.

> [!NOTE]
> W hello portalu Azure tylko ograniczonego zestawu funkcji tooSQL Azure elastyczne pule są dostępne. Użyj hello interfejsów API środowiska PowerShell tooaccess hello pełny zestaw bieżącą funkcjonalność.
> 
> 

## <a name="applications"></a>Aplikacje
* Wykonywanie zadań administracyjnych, takich jak wdrażanie nowego schematu.
* Zaktualizuj informacje produktu danych wspólnych dla wszystkich baz danych. Lub aktualizacji automatycznych harmonogramy każdy dzień tygodnia po godzinach.
* Odbuduj indeksy tooimprove kwerendy wydajności. Odbudowanie Hello może być skonfigurowany tooexecute w kolekcji baz danych cyklicznie, takich jak poza godzinami szczytu.
* Zbieranie wyników zapytania z zestawu baz danych do centralnej tabeli na podstawie bieżącego. Wydajność zapytania mogą być wykonywane stale i skonfigurować tootrigger toobe dodatkowe zadania wykonywane.
* Wykonanie dłużej uruchomione zapytania przetwarzania danych w dużych zestawach baz danych, na przykład Witaj zbierania danych telemetrycznych klienta. Wyniki są zbierane w tabeli docelowej jednego do dalszej analizy.

## <a name="elastic-database-jobs-end-to-end"></a>Zadania elastyczne bazy danych: end-to-end
1. Zainstaluj hello **zadania elastycznej bazy danych** składników. Aby uzyskać więcej informacji, zobacz [zadania instalowania elastycznej bazy danych](sql-database-elastic-jobs-service-installation.md). Jeśli hello instalacja nie powiedzie się, zobacz [jak toouninstall](sql-database-elastic-jobs-uninstall.md).
2. Użyj hello tooaccess interfejsów API środowiska PowerShell więcej funkcji, na przykład tworzenie kolekcji niestandardowy bazy danych, dodawanie harmonogramów i/lub zbierania zestawów wyników. Użyj portalu hello prostą instalację i tworzenia/monitorowania zadań ograniczone tooexecution przed **puli elastycznej**. 
3. Utwórz zaszyfrowane poświadczenia do wykonywania zadań i [dodać hello użytkownika (lub roli) tooeach bazy danych w grupie hello](sql-database-security-overview.md).
4. Tworzenie skryptu T-SQL, który można uruchomić dla każdej bazy danych w grupie hello idempotentności. 
5. Wykonaj te kroki zadania toocreate przy użyciu portalu Azure hello: [Tworzenie zadania i zarządzać nimi elastycznej bazy danych](sql-database-elastic-jobs-create-and-manage.md). 
6. Lub użyć skryptów środowiska PowerShell: [Utwórz zadania elastycznej bazy danych SQL Database, przy użyciu programu PowerShell (wersja zapoznawcza) i zarządzać nimi](sql-database-elastic-jobs-powershell.md).

## <a name="idempotent-scripts"></a>Skrypty idempotentności
skrypty Hello musi być [idempotentności](https://en.wikipedia.org/wiki/Idempotence). Proste warunków "idempotentności" oznacza, że jeśli hello skryptu zakończy się pomyślnie i jest uruchamiany ponownie, hello takiego samego wyniku występuje. Skrypt może zakończyć się niepowodzeniem ze względu na problemy z siecią tootransient. W takim przypadku zadania hello automatycznie ponowi uruchamianie skryptu hello wstępnie zdefiniowane kilka razy przed desisting. Skrypt idempotentności ma hello spowodować takie same nawet wtedy, gdy pomyślnym uruchomieniu dwa razy. 

Proste działanie jest tootest hello istnienia obiektu przed jej tworzenia.  

    IF NOT EXIST (some_object)
    -- Create hello object 
    -- If it exists, drop hello object before recreating it.

Podobnie skryptu musi być możliwe tooexecute pomyślnie testując logicznie dla i przeciwdziałanie wszystkie problemy znalezione.

## <a name="failures-and-logs"></a>Awarie i dzienniki
Jeśli skrypt zakończy się niepowodzeniem po wielu próbach, zadania hello rejestruje hello błąd i kontynuuje. Po zakończeniu zadania (to znaczy do uruchomienia wszystkich baz danych w grupie hello), można sprawdzić jego lista nieudanych prób. Dzienniki Hello szczegółowo toodebug uszkodzenie skryptów. 

## <a name="group-types-and-creation"></a>Typy grupy i utworzenia
Istnieją dwa rodzaje grup: 

1. Ustawia niezależnego fragmentu
2. Grupy niestandardowe

Identyfikator niezależnego fragmentu zestaw grup są tworzone przy użyciu hello [narzędzi elastycznej bazy danych](sql-database-elastic-scale-introduction.md). Podczas tworzenia grupy zestaw niezależnych baz danych są dodawane lub usuwane z grupy hello automatycznie. Na przykład nowy identyfikator niezależnego fragmentu zostanie automatycznie w grupie hello podczas dodawania toohello niezależnego fragmentu mapy. Zadania mogą być następnie uruchamiane na powitania grupy.

Grupy niestandardowe na hello drugiej strony, sztywno są zdefiniowane. Należy jawnie dodać lub usunąć baz danych z niestandardowych grup. Po przerwaniu bazy danych w grupie hello, zadanie hello podejmie skryptu hello toorun hello bazy danych, co spowoduje niepowodzenie ostatecznego. Grup utworzonych za pomocą portalu Azure hello obecnie są grup niestandardowych. 

## <a name="components-and-pricing"></a>Składniki i cen
Witaj następujące składniki współpracują ze sobą toocreate usługi w chmurze Azure, który umożliwia wykonanie ad hoc zadań administracyjnych. Hello składniki są zainstalowane i skonfigurowane automatycznie podczas instalacji, w ramach subskrypcji. Można zidentyfikować hello usług, jak wszystkie mają takie same generowanych automatycznie hello nazwy. Nazwa Hello jest unikatowa i składa się z hello prefiksu "edj" następują znaki losowo generowany 21.

* **Usługa w chmurze Azure**: zadania elastycznej bazy danych (wersja zapoznawcza) jest dostarczany jako chmury Azure hostowanej klienta usługi tooperform wykonywanie hello żądane zadania. Z portalu hello hello usługa jest wdrożony, a w ramach subskrypcji Microsoft Azure. Hello domyślne wdrożona usługa działa z hello co najmniej dwóch procesu roboczego ról wysokiej dostępności. Witaj domyślny rozmiar każdej roli proces roboczy (ElasticDatabaseJobWorker) działa na wystąpienie A0. O cenach, zobacz [cennik usługi w chmurze](https://azure.microsoft.com/pricing/details/cloud-services/). 
* **Baza danych SQL Azure**: hello usługa używa bazy danych SQL Azure, znany jako hello **bazy danych kontroli** toostore wszystkie hello zadania metadanych. warstwy usług Hello domyślne to S0. O cenach, zobacz [cennik usługi SQL Database](https://azure.microsoft.com/pricing/details/sql-database/).
* **Usługa Azure Service Bus**: Azure Service Bus jest koordynacji hello pracy w ramach hello usługi w chmurze Azure. Zobacz [usługi magistrali cennik](https://azure.microsoft.com/pricing/details/service-bus/).
* **Magazyn Azure**: używane jest konto magazynu Azure toostore diagnostycznych danych wyjściowych rejestrowania w zdarzeniu hello, który problem wymaga dalszych debugowania (zobacz [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](../cloud-services/cloud-services-dotnet-diagnostics.md)). O cenach, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-elastic-database-jobs-work"></a>Jak działają zadania elastycznej bazy danych
1. Baza danych SQL Azure jest wyznaczony **bazy danych kontroli** który przechowuje wszystkie dane meta dane i stan.
2. dostęp do bazy danych kontroli Hello uzyskują hello **zadania usługi** toolaunch i Śledź tooexecute zadania.
3. Dwa różne role komunikują się z bazą danych sterowania hello: 
   * Kontroler: Określa zadania, które wymagają hello tooperform zadania żądanej zadań i zadań zakończonych niepowodzeniem prób przez utworzenie nowego zadania.
   * Wykonywanie zadań dla zadania: Wykonuje hello zadania.

### <a name="job-task-types"></a>Typy zadań zadania
Istnieje wiele typów zadania, wykonujących wykonywanie zadań:

* ShardMapRefresh: Zapytania hello toodetermine mapy niezależnego fragmentu wszystkie hello bazy danych używane jako niezależne
* ScriptSplit: Zostaje skryptu hello między "Przejdź" instrukcji w partii
* ExpandJob: Tworzy podrzędnych zadania dla każdej bazy danych z zadania przeznaczonego dla grupy baz danych
* ScriptExecution: Skrypt dla określonej bazy danych przy użyciu określonych poświadczeń wykonuje
* Dacpac: DACPAC tooa określonej bazy danych przy użyciu poświadczeń w szczególności dotyczy

## <a name="end-to-end-job-execution-work-flow"></a>Zadanie end-to-end wykonywania z przepływu pracy
1. Za pomocą portalu hello albo hello interfejs API środowiska PowerShell, zadania są wstawiane do hello **bazy danych kontroli**. zadanie Hello żąda wykonania skryptu języka Transact-SQL w odniesieniu do grupy baz danych przy użyciu określonych poświadczeń.
2. Kontroler Hello identyfikuje hello nowe zadanie. Zadania są tworzone i wykonać skryptu hello toosplit i toorefresh hello grupy baz danych. Ponadto nowe zadanie zostanie utworzona i wykonywane zadanie hello tooexpand i Utwórz nowy element podrzędny zadania, gdzie każde zadanie podrzędne jest hello tooexecute określonego skryptu języka Transact-SQL w bazie danych poszczególnych w grupie hello.
3. Kontroler Hello identyfikuje hello utworzone zadań podrzędnych. Dla każdego zadania kontrolera hello tworzy i uruchamia skrypt hello tooexecute zadań zadania w bazie danych. 
4. Po zakończeniu wszystkich zadań zadania, kontrolera hello aktualizuje stan tooa ukończyć zadania hello. 
   W dowolnym momencie podczas wykonywania zadania hello interfejs API środowiska PowerShell może być używane tooview hello bieżący stan wykonywania zadania. Wszystkie godziny są zwracane przez hello interfejsów API programu PowerShell są reprezentowane w formacie UTC. W razie potrzeby żądanie anulowania może być inicjowane toostop zadania. 

## <a name="next-steps"></a>Następne kroki
[Zainstaluj składniki hello](sql-database-elastic-jobs-service-installation.md), następnie [tworzenie i dodawanie dziennika w bazie danych tooeach w grupie hello baz danych](sql-database-manage-logins.md). toofurther zrozumieć Tworzenie zadania i zarządzanie nimi, zobacz [tworzenie i zarządzanie nimi zadania elastycznej bazy danych](sql-database-elastic-jobs-create-and-manage.md). Zobacz też [wprowadzenie zadania elastycznej bazy danych](sql-database-elastic-jobs-getting-started.md).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->


