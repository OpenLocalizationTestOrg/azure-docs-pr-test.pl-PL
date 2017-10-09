---
title: zapytania analityczne ad hoc aaaRun przez wiele baz danych Azure SQL | Dokumentacja firmy Microsoft
description: "Uruchamianie zapytań ad hoc analytics przez wiele baz danych w hello Wingtip SaaS wielodostępnych aplikacji."
keywords: "samouczek usługi sql database"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: billgib; sstein
ms.openlocfilehash: 140cd51fdd03b5a548147282b51ceb0ad80c944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a>Uruchamianie zapytań analytics ad hoc we wszystkich dzierżaw Wingtip SaaS

W tym samouczku można spotkać zapytań rozproszonych hello cały zestaw baz danych dzierżawy tooenable ad hoc analytics. Elastyczne zapytanie jest używane tooenable rozproszonych zapytań, co wymaga dalszej analizy bazy danych jest wdrażany (serwer wykazu toohello). Te zapytania można wyodrębnić wgląd w codziennych danych operacyjnych hello aplikacji Wingtip SaaS hello stosie.


Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * O hello widoki globalne w każdej bazie danych, które umożliwiają wydajne wykonywanie zapytań w dzierżawców
> * Jak toodeploy bazy danych analizy ad hoc
> * Toorun rozkład zapytania dla wszystkich baz danych dzierżawy



toocomplete ukończenia tego samouczka, Utwórz hello się, że następujące wymagania wstępne:

* Aplikacja Wingtip SaaS Hello jest wdrażana. Zobacz toodeploy w mniej niż pięć minut [wdrażania i aplikacji Wingtip SaaS hello](sql-database-saas-tutorial.md)
* Zainstalowany jest program Azure PowerShell. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z programem Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* SQL Server Management Studio (SSMS) jest zainstalowany. toodownload i zainstaluj narzędzia SSMS, zobacz [pobierania programu SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


## <a name="ad-hoc-analytics-pattern"></a>Wzorzec analytics ad hoc

Jedną z możliwości dużą hello z aplikacjami SaaS jest toouse hello ogromnych ilości danych dzierżawy przechowywane w chmurze hello. Użyj tego danych toogain wgląd w informacje hello operacji i użycie aplikacji dzierżawcom, ich użytkowników, preferencje, zachowania, itp. Te szczegółowe informacje można przeprowadzają opracowanie funkcji, ulepszenia użyteczność i innych inwestycji w aplikacji i usług.

Uzyskiwanie dostępu do tych danych w jednej wielodostępnej bazie danych jest łatwe, ale nie jest tak proste, gdy są one znacznie rozproszone, potencjalnie nawet na tysiące baz danych. Jednym z podejść jest toouse [elastycznej zapytania](sql-database-elastic-query-overview.md), które umożliwia wykonywanie zapytań w rozproszonej zestaw baz danych z wspólny schemat. Elastyczne zapytanie używa pojedynczego *head* bazy danych, w którym zdefiniowano tabel zewnętrznych czy dublowany tabele lub widoki hello rozproszonych bazy danych (dzierżawcy). Zapytania przesłane toothis head bazy danych są skompilowane tooproduce planu zapytania rozproszonego z części zapytania hello przesuwana toohello dzierżawcy z bazy danych, zgodnie z potrzebami. Elastyczne zapytanie używa mapy niezależnego fragmentu hello w lokalizacji bazy danych katalogu hello hello tooprovide hello dzierżawy z baz danych. Instalator i zapytania są oczywiste, przy użyciu standardu [języka Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference)i obsługuje zapytań ad hoc z narzędzi, takich jak usługi Power BI i Excel.

Przekazując zapytania hello dzierżawcy z bazy danych, elastyczne zapytania zapewnia natychmiastowego wgląd w danych produkcyjnych na żywo. Jednak jak elastycznej zapytanie pobiera dane z potencjalnie wiele baz danych, zapytań, czas oczekiwania czasami może być większa niż równoważne zapytań przesłać tooa pojedynczej bazy danych wielu dzierżawców. Należy zachować ostrożność podczas projektowania zapytań toominimize hello danych zwracanych. Elastyczne zapytania jest często najlepiej dopasowane do badania niewielkich ilości danych w czasie rzeczywistym, min. toobuilding często używane lub analytics złożonych zapytań i raportów. Jeśli kwerendy nie również wykonać, obejrzyj hello [plan wykonania](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) toosee części zapytania hello ma zostać przesuwana toohello zdalnej bazy danych i ilość danych, które zostały zwrócone. Zapytania, które wymagają złożonych przetwarzania analitycznego mogą być lepiej obsłużone w niektórych przypadkach wyodrębniając danych dzierżawy na dedykowany bazy danych lub magazyn danych, zoptymalizowana pod kątem zapytania analityczne. Ten wzorzec jest szczegółowo hello [samouczek analizy dzierżawy](sql-database-saas-tutorial-tenant-analytics.md). 

## <a name="get-hello-wingtip-application-scripts"></a>Pobierz skrypty aplikacji hello Wingtip

Witaj Wingtip SaaS skrypty i kod źródłowy aplikacji są dostępne w hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repozytorium github. [Kroki skrypty Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-ticket-sales-data"></a>Tworzenie danych sprzedaży biletów

toorun zapytania względem bardziej interesującego zestawu danych, Utwórz danych sprzedaży biletów, uruchamiając hello generatora biletu.

1. W hello *PowerShell ISE*, otwórz hello... \\Modułów uczenia\\operacyjne Analytics\\Analytics ad hoc\\*AdhocAnalytics.ps1 pokaz* skryptów i ustaw następujące wartości hello:
   * **$DemoScenario** = 1, **zakupu biletów zdarzeń na wszystkich miejsc**.
2. Naciśnij klawisz **F5** do uruchamiania skryptu hello i generowanie sprzedaży biletów. Po uruchomieniu skryptu hello nadal hello kroków w tym samouczku. dane biletu Hello jest poddawany kwerendzie w hello *uruchamianie zapytań ad hoc distributed* sekcji, więc Zaczekaj hello biletu generator toocomplete, jeśli wciąż działa po przejściu toothat wykonywania.

## <a name="explore-hello-global-views"></a>Eksploruj hello widoki globalne

Hello aplikacji Wingtip SaaS jest utworzony przy użyciu modelu dzierżawy na bazę danych, więc schematu bazy danych dzierżawy hello jest zdefiniowana z punktu widzenia pojedynczej dzierżawy. Informacje dotyczące dzierżawy istnieje w jednej tabeli, *miejscową*, który zawsze pojedynczy wiersz i jest zaimplementowany jako sterty, bez klucza podstawowego. Inne tabele w schemacie hello nie ma potrzeby związane z toobe toohello *miejscową* tabeli, ponieważ podczas normalnego użytkowania, nigdy nie jest wątpliwości dane hello dzierżawy, które należy do.

Jednak podczas wykonywania zapytania dla wszystkich baz danych, ważne jest elastyczny zapytania można traktować hello danych tak, jakby była częścią jednej logicznej bazy danych podzielonej przez dzierżawcę. tooachieve to zestaw widoków "global" są dodane toohello bazy danych dzierżawy, która projektu identyfikator dzierżawcy do każdej z tabel hello, które będą pytani globalnie. Na przykład Witaj *VenueEvents* widoku dodaje obliczanej *VenueId* toohello kolumn zaprojektowana z hello *zdarzenia* tabeli. Poprzez definiowanie tabeli zewnętrznej hello hello head bazy danych za pośrednictwem *VenueEvents* (zamiast bazowy hello *zdarzenia* tabeli), elastyczne zapytanie jest możliwe toopush dół sprzężenia na podstawie *VenueId* , mogą być wykonywane równolegle na każdym zdalnej bazy danych (a nie na powitania head bazy danych). Zmniejsza to znacznie hello ilość danych, które ma zostać zwrócona, co powoduje znaczne zwiększenie wydajności dla wielu zapytań. Widoki globalne te zostały utworzone wcześniej w wszystkich baz danych dzierżawy (i w *basetenantdb*).

1. Otwórz w programie SSMS i [połączyć toohello tenants1 -&lt;użytkownika&gt; serwera](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms).
2. Rozwiń węzeł **baz danych**, kliknij prawym przyciskiem myszy **contosoconcerthall**i wybierz **nowe zapytanie**.
3. Uruchom następujące kwerendy tooexplore hello różnica między hello pojedynczej dzierżawy tabele i widoki globalne hello hello:

   ```T-SQL
   -- hello base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice hello plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- hello base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects hello VenueId retrieved from hello Venues table.
   SELECT * FROM VenueEvents
   ```

W tych widokach hello *VenueId* jest obliczany jako skrót hello miejscową nazwy, ale jakiejkolwiek metody mogą być używane toointroduce unikatową wartość. Ta metoda jest podobny sposób toohello hello klucz dzierżawy jest obliczana do użycia w katalogu hello.

Definicja hello tooexamine hello *miejsc* widoku:

1. W **Eksplorator obiektów**, rozwiń węzeł **contosoconcethall** > **widoków**:

   ![Widoki](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. Kliknij prawym przyciskiem myszy **dbo. Miejsc**.
3. Wybierz **skryptu widoku w postaci** > **utworzyć** > **nowe okno edytora zapytań**

Wszelkie inne hello skryptu *miejscową* widoków toosee sposób dodawania hello *VenueId*.

## <a name="deploy-hello-database-used-for-ad-hoc-distributed-queries"></a>Wdrażanie hello bazy danych używane do zapytań ad hoc rozproszonych

Tego ćwiczenia wdraża hello *adhocanalytics* bazy danych. Jest to hello head bazy danych, który będzie zawierać schemat hello używane do wykonywania zapytań dla wszystkich baz danych dzierżawy. Baza danych Hello jest wdrożony toohello istniejącego serwera katalogu, który jest serwerem hello używane dla wszystkich związanych z zarządzaniem baz danych w hello przykładowej aplikacji.

1. Otwórz... \\Modułów uczenia\\operacyjne Analytics\\Analytics ad hoc\\*AdhocAnalytics.ps1 pokaz* w hello *PowerShell ISE* i hello zestawu następujące wartości:
   * **$DemoScenario** = 2, **Deploy Ad-hoc analytics database**.

2. Naciśnij klawisz **F5** toorun hello skryptu i utworzenia hello *adhocanalytics* bazy danych.

W następnej sekcji hello możesz dodać bazy danych toohello schematu, może być używane toorun rozproszonych zapytań.

## <a name="configure-hello-database-for-running-distributed-queries"></a>Skonfiguruj bazę danych hello do uruchamiania zapytań rozproszonych

Tego ćwiczenia dodaje schematu (hello zewnętrznego źródła danych i definicji tabeli zewnętrznej) toohello ad hoc analytics bazy danych, która umożliwia wykonywanie zapytania dla wszystkich baz danych dzierżawy.

1. Otwórz program SQL Server Management Studio i połącz toohello bazy danych analizy ad hoc, utworzony w poprzednim kroku hello. Nazwa Hello hello bazy danych będzie adhocanalytics.
2. Otwórz ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *AdhocAnalyticsDB.sql zainicjować* w programie SSMS.
3. Przejrzyj skrypt SQL hello i zanotuj następujące hello:

   Elastyczne zapytanie używa poświadczeń o zakresie bazy danych tooaccess każdego hello dzierżawy z baz danych. To poświadczenie musi toobe dostępne w wszystkich hello baz danych i zwykle należy udzielić minimalnych uprawnień hello wymagane tooenable tych zapytań ad hoc.

    ![Tworzenie poświadczeń](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   Witaj zewnętrznego źródła danych, która jest zdefiniowane toouse hello dzierżawy niezależnego fragmentu mapy hello katalogu bazy danych. Korzystając z niniejszego jako hello zewnętrznego źródła danych, zapytania są rozproszone tooall bazy danych zarejestrowany w wykazie powitania po uruchomieniu kwerendy hello. Ponieważ nazwy serwerów są różne dla każdego wdrożenia, ten skrypt inicjacji pobiera hello lokalizacji bazy danych katalogu hello pobierając hello bieżącego serwera (@@servername) gdzie hello skrypt zostanie wykonany.

    ![Tworzenie zewnętrznego źródła danych](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   Witaj tabel zewnętrznych odwołujące się do widoki globalne hello opisanego w poprzedniej sekcji hello oraz zdefiniowana z **dystrybucji = SHARDED(VenueId)**. Ponieważ każdy *VenueId* mapy tooa pojedynczej bazy danych, poprawia to wydajność w wielu scenariuszach, jak pokazano w następnej sekcji hello.

    ![Tworzenie tabel zewnętrznych](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   Tabela lokalne powitania *VenueTypes* które jest tworzone i wypełniane. Tej tabeli danych odwołania jest typowe w przypadku wszystkich dzierżawy baz danych, więc może być reprezentowany jako lokalnej tabeli i wypełnione z hello wspólnych danych. Dla niektórych kwerend może to zmniejszyć hello ilości danych są przenoszone między hello dzierżawcy z bazy danych oraz hello *adhocanalytics* bazy danych.

    ![Tworzenie tabeli](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   Jeśli dołączysz tabele odwołań w ten sposób można się, że schemat tabeli hello tooupdate i dane po zaktualizowaniu hello dzierżawcy z bazy danych.

4. Naciśnij klawisz **F5** toorun hello skryptu i zainicjuj hello *adhocanalytics* bazy danych. 

Teraz można uruchomić zapytania rozproszone i zbieranie szczegółowych informacji we wszystkich dzierżawców!

## <a name="run-ad-hoc-distributed-queries"></a>Uruchamianie zapytań ad hoc rozproszonych

Teraz tego hello *adhocanalytics* baza danych jest skonfigurowany, przejdź dalej i uruchamiania niektórych zapytań rozproszonych. Zawiera hello wykonanie planu w celu lepszego zrozumienia, z którym dzieje hello przetwarzania zapytania. 

Podczas sprawdzania plan wykonania hello, umieść kursor nad hello planu ikony, aby uzyskać szczegółowe informacje. 

To ustawienie jest ważne toonote **dystrybucji = SHARDED(VenueId)** podczas zdefiniowanego hello zewnętrznego źródła danych, zwiększa wydajność w różnych scenariuszach. Ponieważ każdy *VenueId* mapy tooa pojedynczej bazy danych, filtrowania jest łatwo gotowe zdalnie, zwracająca hello tylko danych należy.

1. Otwórz plik ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql* w narzędziu SSMS.
2. Upewnij się, są połączone toohello **adhocanalytics** bazy danych.
3. Wybierz hello **zapytania** menu i kliknij przycisk **obejmują rzeczywisty Plan wykonania**
4. Wyróżnij hello *miejsc, które są obecnie zarejestrowane?* zapytania, a następnie naciśnij klawisz **F5**.

   Hello zapytanie zwraca listę całe miejsce hello, pokazujący, jak szybko i łatwo jest tooquery we wszystkich dzierżaw i zwracanych danych z każdej dzierżawy.

   Zbadaj hello planu i kosztów całej hello jest zapytania zdalnego hello ponieważ jesteśmy po prostu będzie tooeach dzierżawcy w bazie danych i wybierając hello miejscową informacji.

   ![Wybierz * z dbo. Miejsc](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. Wybierz hello dalej zapytania, a następnie naciśnij klawisz **F5**.

   To zapytanie sprzężenia danych z baz danych dzierżawy hello i lokalne powitania *VenueTypes* tabeli (lokalny, w jakiej jest tabelą w hello *adhocanalytics* bazy danych).

   Zbadaj hello planu i zobacz tego hello większość koszt jest hello zapytania zdalnego, ponieważ będziemy kwerendy informacji o miejscu każdego dzierżawcy (dbo. Miejsc), a następnie wykonaj szybkie sprzężenie lokalne powitania lokalnych *VenueTypes* tabeli toodisplay hello przyjazną nazwę.

   ![Dołącz do danych zdalnych i lokalnych](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. Teraz wybierz hello *na dzień zostały hello sprzedanych biletów większości?* zapytania, a następnie naciśnij klawisz **F5**.

   To zapytanie jest bardziej złożonych przyłączanie i agregacji. Co to jest ważne toonote jest najbardziej przetwarzania hello jest wykonywane zdalnie, czy ponownie, możemy przywrócić tylko wiersze hello potrzebne, zwracanie tylko jednego wiersza dla każdego miejscową agregacji biletu sprzedaży liczba na dzień.

   ![query](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a>Następne kroki

W tym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * Uruchamiania rozproszonych zapytań dla wszystkich baz danych dzierżawy
> * Wdrażanie bazy danych analizy ad hoc i dodawanie zapytań rozproszonych toorun tooit schematu.


Teraz spróbuj hello [samouczek analizy dzierżawy](sql-database-saas-tutorial-tenant-analytics.md) tooexplore wyodrębniania danych bazy danych analytics oddzielne tooa bardziej złożonych przetwarzania analizy...

## <a name="additional-resources"></a>Dodatkowe zasoby

* Dodatkowe [samouczki, które zależą od hello aplikacji Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Elastyczne zapytanie](sql-database-elastic-query-overview.md)
