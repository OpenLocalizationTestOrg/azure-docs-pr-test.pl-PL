---
title: "kody błędów aaaSQL — błąd połączenia z bazą danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o kodach błędów SQL dla bazy danych SQL klienta aplikacji, takich jak typowych błędów połączenia bazy danych, problemy kopii bazy danych i ogólne błędy. "
keywords: "Kod błędu SQL, sql dostępu, błędów połączenia bazy danych, kody błędów sql"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 2a23e4ca-ea93-4990-855a-1f9f05548202
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 683a7d72c935742f3f9f9a0c683e5d8161167d6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-error-codes-for-sql-database-client-applications-database-connection-error-and-other-issues"></a>Kody błędów SQL dla aplikacji klienckich, SQL Database: błąd połączenia i inne problemy z bazy danych
<!--
Old Title on MSDN:  Error Messages (Azure SQL Database)
ShortId on MSDN:  ff394106.aspx
Dx 4cff491e-9359-4454-bd7c-fb72c4c452ca
-->


Ten artykuł zawiera listę kodów błędów programu SQL dla aplikacji klienckich bazy danych SQL, w tym błędów połączenia bazy danych, błędów przejściowych (nazywanych również błędów przejściowych) błędy ładu zasobów, problemy kopii bazy danych, puli elastycznej i inne błędy. Większość kategorie są tooAzure określonej bazy danych SQL i nie są stosowane tooMicrosoft programu SQL Server.

## <a name="database-connection-errors-transient-errors-and-other-temporary-errors"></a>Błędów połączenia bazy danych, błędów przejściowych i innych tymczasowe błędy
Witaj poniższej tabeli opisano kody błędów SQL hello błędów utraty połączenia i innych błędów przejściowych, które mogą wystąpić, gdy aplikacja próbuje tooaccess bazy danych SQL. Dla Rozpoczynanie pracy — samouczki dotyczące tooAzure tooconnect bazy danych SQL, zobacz [łączenie tooAzure bazy danych SQL](sql-database-libraries.md).

### <a name="most-common-database-connection-errors-and-transient-fault-errors"></a>Najbardziej typowych błędów połączenia bazy danych i wystąpienia błędu przejściowego błędów
Witaj infrastruktury platformy Azure ma toodynamically możliwości hello ponownie skonfigurować serwery w przypadku złożonych zadań wystąpienia w hello usługi baza danych SQL.  Dynamicznego działania może spowodować, że klient programu toolose jego tooSQL połączenia bazy danych. Tego rodzaju błędu jest nazywany *błędu przejściowego*.

Zdecydowanie zaleca się, czy program kliencki ma Logika ponawiania, dzięki czemu można przywrócić połączenia po nadaniu hello błędu przejściowego czasu toocorrect się.  Firma Microsoft zaleca opóźnienie 5 sekund przed ponowną próbą wykonania Twojego pierwszego. Ponawia próbę po krótszy niż 5 sekund opóźnienia ryzyko związane z usługą hello utrudnione w chmurze. Każda kolejne próby opóźnienie hello powinien być zwiększany wykładniczo, zapasowej tooa maksymalnie 60 sekund.

Błąd przejściowy błędy manifestu zwykle wśród hello następujące komunikaty o błędach z programów klienckich:

* Baza danych &lt;db_name&gt; na serwerze &lt;Azure_instance&gt; nie jest obecnie dostępna. Ponów próbę połączenia hello później. Jeśli hello problem będzie się powtarzać, skontaktuj się z pomocą techniczną i podaj identyfikator śledzenia sesji hello &lt;session_id&gt;
* Baza danych &lt;db_name&gt; na serwerze &lt;Azure_instance&gt; nie jest obecnie dostępna. Ponów próbę połączenia hello później. Jeśli hello problem będzie się powtarzać, skontaktuj się z pomocą techniczną i podaj identyfikator śledzenia sesji hello &lt;session_id&gt;. (Program Microsoft SQL Server, błąd: 40613)
* Istniejące połączenie zostało zamknięte przez hosta zdalnego hello.
* System.Data.Entity.Core.EntityCommandExecutionException: Wystąpił błąd podczas wykonywania definicji polecenia hello. Zobacz hello wyjątek wewnętrzny, aby uzyskać szczegółowe informacje. ---> System.Data.SqlClient.SqlException: Wystąpił błąd poziomu transportu podczas odbierania wyników z powitania serwera. (Dostawca: Dostawca sesji, błąd: 19 — połączenie fizyczne nie jest używany)
* Połączenie próba tooa dodatkowej bazy danych nie powiodło się, ponieważ hello bazy danych jest w procesie hello reconfguration i jest zajęty, zastosowanie nowych stron podczas w środku hello transakcja active na powitania podstawowej bazy danych. 

Przykłady kodu logika ponowień zobacz:

* [Biblioteki połączeń dla bazy danych SQL i programu SQL Server](sql-database-libraries.md) 
* [Błędy połączenia toofix akcje i błędom przejściowym w bazie danych SQL](sql-database-connectivity-issues.md)

Omówienie hello *okresu blokowania* dla klientów używających ADO.NET jest dostępna w [programu SQL Server połączenia buforowanie (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

### <a name="transient-fault-error-codes"></a>Kody błędów błędu przejściowego
Witaj następujące błędy są przejściowe i należy wykonać ponownie w aplikacji logiki 

| Kod błędu: | Ważność | Opis |
| ---:| ---:|:--- |
| 4060 |16 |Nie można otworzyć bazy danych "%. & #x2a; ls" zażądał hello logowania. Witaj logowanie nie powiodło się. |
| 40197 |17 |Witaj, Usługa napotkała błąd podczas przetwarzania żądania. Spróbuj ponownie. Kod błędu: %d.<br/><br/>Otrzymasz ten błąd, gdy usługa hello nie działa toosoftware lub modernizacji sprzętu, awarii sprzętu lub inne problemy trybu failover. Kod błędu Hello (%d) osadzone w wiadomości powitania błędu 40197 udostępnia dodatkowe informacje o rodzaju hello awarii lub trybu failover, który wystąpił. Przykładowe kody są osadzone w wiadomości powitania błędu 40197 błąd hello są 40020, 40143 40166 i 40540.<br/><br/>Ponownie nawiązującego połączenie serwera bazy danych SQL tooyour automatycznie połączysz tooa dobrej kopii bazy danych. Aplikacja musi catch błąd 40197, dziennika hello osadzonych kod błędu: (%d) w ramach wiadomość hello do rozwiązywania problemów i ponowić próbę połączenia tooSQL bazy danych, aż hello zasoby są dostępne, a połączenie zostanie nawiązane ponownie. |
| 40501 |20 |Usługa Hello jest obecnie zajęta. Ponów żądanie powitania po 10 sekundach. Identyfikator zdarzenia: %ls. Kod: %d.<br/><br/>*Uwaga:* uzyskać więcej informacji, zobacz:<br/>• [Limity zasobów bazy danych SQL azure](sql-database-resource-limits.md). |
| 40613 |17 |Baza danych "%. & #x2a; ls" na serwerze "%. & #x2a; ls" nie jest obecnie dostępna. Ponów próbę połączenia hello później. Jeśli hello problem będzie się powtarzać, skontaktuj się z pomocą techniczną i podaj identyfikator śledzenia sesji hello "%. & #x2a; ls". |
| 49918 |16 |Nie można przetworzyć żądania. Żądanie tooprocess nie ma wystarczającej ilości zasobów.<br/><br/>Usługa Hello jest obecnie zajęta. Spróbuj ponownie później hello żądania. |
| 49919 |16 |Nie można procesu Utwórz lub zaktualizuj zapytanie. Zbyt wiele operacji tworzenia lub aktualizacji w toku dla subskrypcji "% ld".<br/><br/>Usługa Hello jest zajęta przetwarzania wielu utworzyć lub zaktualizować żądań dla subskrypcji lub serwera. Żądania są aktualnie zablokowane do optymalizacji zasobów. Zapytanie [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) dla oczekujących operacji. Zaczekaj do czasu tworzenia lub aktualizacji zakończeniu żądania lub usuń jedno z oczekujących żądań i ponów żądanie później. |
| 49920 |16 |Nie można przetworzyć żądania. Za dużo operacji w toku dla subskrypcji "% ld".<br/><br/>Usługa Hello jest zajęty przetwarzaniem wiele żądań dla tej subskrypcji. Żądania są aktualnie zablokowane do optymalizacji zasobów. Zapytanie [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) stanu operacji. Poczekaj, aż oczekujących żądań zakończeniu lub usuń jedno z oczekujących żądań i ponów żądanie później. |
| 4221 |16 |Średniego tooread logowania nie powiodła z powodu oczekiwania toolong na "HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING". Hello replika nie jest dostępna dla nazwy logowania, ponieważ brakuje dla transakcji, które zostały aktywny, gdy replika hello został ponownie przetworzony wersje wiersza. Witaj problem można rozwiązać przez wycofanie lub zatwierdzania hello aktywnych transakcji na powitania repliki podstawowej. Wystąpienia tego warunku można zminimalizować przez unikanie transakcji zapisu długa na powitania podstawowego. |

## <a name="database-copy-errors"></a>Błędy kopiowania bazy danych
Hello następujące błędy mogą wystąpić podczas kopiowania bazy danych w bazie danych SQL Azure. Więcej informacji znajdziesz w artykule [Kopiowanie bazy danych usługi Azure SQL Database](sql-database-copy.md).

| Kod błędu: | Ważność | Opis |
| ---:| ---:|:--- |
| 40635 |16 |Klient o adresie IP "%. & #x2a; ls" jest tymczasowo wyłączona. |
| 40637 |16 |Utwórz kopię bazy danych jest obecnie wyłączona. |
| 40561 |16 |Kopiowanie bazy danych nie powiodło się. Albo hello źródłowa lub docelowa baza danych nie istnieje. |
| 40562 |16 |Kopiowanie bazy danych nie powiodło się. Witaj źródłowa baza danych została porzucona. |
| 40563 |16 |Kopiowanie bazy danych nie powiodło się. Witaj docelowa baza danych została porzucona. |
| 40564 |16 |Kopiowanie bazy danych nie powiodło się ze względu na błąd wewnętrzny tooan. Porzuć docelową bazę danych i spróbuj ponownie. |
| 40565 |16 |Kopiowanie bazy danych nie powiodło się. Nie więcej niż 1 równoczesnych kopiowania bazy danych z hello tego samego źródła jest dozwolone. Porzuć docelową bazę danych i spróbuj ponownie później. |
| 40566 |16 |Kopiowanie bazy danych nie powiodło się ze względu na błąd wewnętrzny tooan. Porzuć docelową bazę danych i spróbuj ponownie. |
| 40567 |16 |Kopiowanie bazy danych nie powiodło się ze względu na błąd wewnętrzny tooan. Porzuć docelową bazę danych i spróbuj ponownie. |
| 40568 |16 |Kopiowanie bazy danych nie powiodło się. Źródłowa baza danych stała się niedostępna. Porzuć docelową bazę danych i spróbuj ponownie. |
| 40569 |16 |Kopiowanie bazy danych nie powiodło się. Docelowa baza danych stała się niedostępna. Porzuć docelową bazę danych i spróbuj ponownie. |
| 40570 |16 |Kopiowanie bazy danych nie powiodło się ze względu na błąd wewnętrzny tooan. Porzuć docelową bazę danych i spróbuj ponownie później. |
| 40571 |16 |Kopiowanie bazy danych nie powiodło się ze względu na błąd wewnętrzny tooan. Porzuć docelową bazę danych i spróbuj ponownie później. |

## <a name="resource-governance-errors"></a>Błędy ładu zasobów
następujące błędy Hello są spowodowane nadmiernego wykorzystania zasobów podczas pracy z bazą danych SQL Azure. Na przykład:

* Transakcja została Otwórz zbyt długo.
* Transakcja jest zbyt wiele blokują.
* Aplikacja zużywa zbyt dużej ilości pamięci.
* Aplikacja zużywa zbyt dużo `TempDb` miejsca.

Tematy pokrewne:

* Bardziej szczegółowe informacje znajdują się w tym miejscu: [limity zasobów bazy danych SQL Azure](sql-database-resource-limits.md)

| Kod błędu: | Ważność | Opis |
| ---:| ---:|:--- |
| 10928 |20 |Identyfikator zasobu: %d. limit %s Hello hello bazy danych wynosi %d i został osiągnięty. Aby uzyskać więcej informacji, zobacz [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637).<br/><br/>Witaj identyfikator zasobu wskazuje hello zasób, który został osiągnięty hello limit. Dla wątków roboczych hello identyfikator zasobu = 1. Sesje, hello identyfikator zasobu = 2.<br/><br/>*Uwaga:* Aby uzyskać więcej informacji o tym błędzie i w jaki sposób tooresolve, zobacz:<br/>• [Limity zasobów bazy danych SQL azure](sql-database-resource-limits.md). |
| 10929 |20 |Identyfikator zasobu: %d. Minimalna gwarancji %s Hello jest %d, maksymalny limit %d i hello bieżące użycie dla bazy danych hello wynosi %d. Jednak serwer hello jest obecnie zbyt zajęty toosupport żądań przekracza %d dla tej bazy danych. Aby uzyskać więcej informacji, zobacz [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637). W przeciwnym razie spróbuj ponownie później.<br/><br/>Witaj identyfikator zasobu wskazuje hello zasób, który został osiągnięty hello limit. Dla wątków roboczych hello identyfikator zasobu = 1. Sesje, hello identyfikator zasobu = 2.<br/><br/>*Uwaga:* Aby uzyskać więcej informacji o tym błędzie i w jaki sposób tooresolve, zobacz:<br/>• [Limity zasobów bazy danych SQL azure](sql-database-resource-limits.md). |
| 40544 |20 |Witaj baza danych osiągnęła swój limit przydziału. Partycji lub Usuń dane, Porzuć indeksy lub można znaleźć w dokumentacji hello możliwych rozwiązań. |
| 40549 |16 |Sesja jest przerwana z powodu długotrwałej transakcji. Spróbuj skrócić transakcję. |
| 40550 |16 |Witaj sesja została przerwana, ponieważ uzyskała zbyt wiele blokad. Spróbuj odczytu lub modyfikować mniej wierszy w ramach jednej transakcji. |
| 40551 |16 |Witaj sesja została przerwana z powodu nadmiernego `TEMPDB` użycia. Spróbuj zmodyfikować użycie miejsca na zapytanie tooreduce hello tabeli tymczasowej.<br/><br/>*Porada:* Jeśli używasz obiekty tymczasowe, co pozwala zaoszczędzić miejsce w hello `TEMPDB` bazy danych, przeciągając obiekty tymczasowe po nie są już potrzebne hello sesji. |
| 40552 |16 |Witaj sesja została przerwana z powodu nadmiernego transakcji użycie miejsca na dziennik. Spróbuj modyfikować mniej wierszy w ramach jednej transakcji.<br/><br/>*Porada:* po wykonaniu operacji wstawiania zbiorczego przy użyciu hello `bcp.exe` narzędzia lub hello `System.Data.SqlClient.SqlBulkCopy` klasy, spróbuj użyć hello `-b batchsize` lub `BatchSize` opcje toolimit hello liczbę wierszy skopiowany toohello server w każdej transakcji. Odbudowywania indeksu o hello `ALTER INDEX` instrukcji, spróbuj użyć hello `REBUILD WITH ONLINE = ON` opcji. |
| 40553 |16 |Witaj sesja została przerwana z powodu nadmiernego wykorzystania pamięci. Spróbuj zmodyfikować tooprocess Twojego zapytania mniej wierszy.<br/><br/>*Porada:* zmniejszeniu liczby hello `ORDER BY` i `GROUP BY` operacje w kodzie języka Transact-SQL zmniejsza wymagania dotyczące pamięci hello kwerendy. |

## <a name="elastic-pool-errors"></a>Błędy puli elastycznej
Hello następujące błędy są powiązane toocreating i używane są pule Elastics.

| Numer_błędu | ErrorSeverity | ErrorFormat | ErrorInserts | ErrorCause | ErrorCorrectiveAction |
|:--- |:--- |:--- |:--- |:--- |:--- |
| 1132 |EX_RESOURCE |Pula elastyczna Hello osiągnęła limit magazynu. Witaj użycia magazynu dla puli elastycznej hello nie może przekraczać MB (%d). |Limit miejsca na pulę elastyczną w MB. |Po osiągnięciu hello limit magazynu elastycznej puli hello, próba toowrite danych tooa w bazie danych. |Należy wziąć pod uwagę zwiększa Dtu hello hello puli elastycznej, jeśli to możliwe w kolejności tooincrease limit magazynu, zmniejszyć hello Magazyn używany przez pojedyncze bazy danych w puli elastycznej hello lub usunąć z puli elastycznej hello bazy danych. |
| 10929 |EX_USER |Minimalna gwarancji %s Hello jest %d, maksymalny limit %d i hello bieżące użycie dla bazy danych hello wynosi %d. Jednak serwer hello jest obecnie zbyt zajęty toosupport żądań przekracza %d dla tej bazy danych. Zobacz [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637) Aby uzyskać pomoc. W przeciwnym razie spróbuj ponownie później. |Minimalna wartość DTU na bazę danych; Maksymalnej wartości DTU na bazę danych |Witaj łączna liczba równoczesnych procesów roboczych (liczba żądań) dla wszystkich baz danych w limit hello próba tooexceed hello elastycznej puli w puli. |Należy rozważyć zwiększenie limitu procesu roboczego hello Dtu hello puli elastycznej, jeśli to możliwe w kolejności tooincrease lub usunąć z puli elastycznej hello bazy danych. |
| 40844 |EX_USER |Baza danych '%ls' na serwerze '%ls' jest '%ls' wersji bazy danych w puli elastycznej i nie może mieć relacji ciągła kopia. |Nazwa bazy danych, wersji bazy danych, nazwę serwera |Polecenie StartDatabaseCopy wydawane na inne niż premium bazę danych w puli elastycznej. |Wkrótce |
| 40857 |EX_USER |Nie znaleziono serwera puli elastycznej: '%ls', nazwa puli elastycznej: '%ls'. |Nazwa serwera. Nazwa puli elastycznej |Określona pula elastyczna nie istnieje w hello określonego serwera. |Podaj nazwę puli elastycznej prawidłowe. |
| 40858 |EX_USER |Na serwerze istnieje już pula elastyczna '%ls': '%ls' |Nazwa puli elastycznej, nazwa serwera |Określona pula elastyczna już istnieje w hello określonego serwera logicznego. |Podaj nową nazwę puli elastycznej. |
| 40859 |EX_USER |Pula elastyczna nie obsługuje warstwy usługi '%ls'. |Warstwa usług puli elastycznej |Warstwa określonej usługi nie jest obsługiwana dla puli elastycznej inicjowania obsługi administracyjnej. |Podaj poprawne edition hello lub nie podawaj warstwy usług domyślne hello toouse puste warstwy usługi. |
| 40860 |EX_USER |Kombinacja puli elastycznej usług i '%ls' cel '%ls' jest nieprawidłowa. |Nazwa puli elastycznej; Nazwa celu poziomu usługi |Elastyczne cel puli i usługi mogą być określone razem tylko wtedy, gdy cel usługi jest określony jako "ElasticPool". |Określ poprawny kombinacja puli elastycznej i cel usługi. |
| 40861 |EX_USER |Witaj wersji bazy danych "%. *ls nie może być inna niż warstwa usług puli elastycznej hello jest "%.* ls. |Wersja bazy danych, warstwa usług puli elastycznej |Wersja bazy danych Hello jest inna niż warstwa usług puli elastycznej hello. |Nie określaj wersji bazy danych, która jest inna niż warstwa usług puli elastycznej hello.  Należy pamiętać, że w tej wersji bazy danych hello toobe określony nie jest konieczne. |
| 40862 |EX_USER |Nazwa puli elastycznej musi być określona, jeśli określono cel usług puli elastycznej hello. |Brak |Cel usług puli elastycznej nie identyfikuje jednoznacznie puli elastycznej. |Określ nazwę puli elastycznej hello, jeśli przy użyciu cel usług puli elastycznej hello. |
| 40864 |EX_USER |Witaj Dtu dla puli elastycznej hello musi wynosić co najmniej (%d) Dtu dla warstwy usług "%. * ls. |Liczba jednostek Dtu dla puli elastycznej; Warstwa usług puli elastycznej. |Próba tooset hello Dtu dla puli elastycznej hello poniżej hello minimalnego limitu. |Spróbuj ponownie, ustawienie hello Dtu dla tooat puli elastycznej hello co najmniej hello minimalnego limitu. |
| 40865 |EX_USER |Witaj Dtu dla puli elastycznej hello nie może przekroczyć (%d) Dtu dla warstwy usług "%. * ls. |Liczba jednostek Dtu dla puli elastycznej; Warstwa usług puli elastycznej. |Próba tooset hello Dtu dla puli elastycznej hello powyżej hello maksymalny limit. |Spróbuj ponownie, ustawienie przekracza maksymalny limit hello hello Dtu dla hello toono puli elastycznej. |
| 40867 |EX_USER |Witaj maksymalna wartość DTU na bazę danych musi wynosić co najmniej (%d) dla warstwy usług "%. * ls. |Maksymalnej wartości DTU na bazę danych; Warstwa usług puli elastycznej |Próba hello tooset maksymalna wartość DTU na bazę danych poniżej hello obsługiwany limit. |Rozważ użycie warstwa usług puli elastycznej hello obsługującego hello pożądane ustawienie. |
| 40868 |EX_USER |Witaj maksymalna wartość DTU na bazę danych nie może przekroczyć (%d) dla warstwy usług "%. * ls. |Maksymalnej wartości DTU na bazę danych; Warstwa usług puli elastycznej. |Próba hello tooset maksymalna wartość DTU na bazę danych poza hello obsługiwany limit. |Rozważ użycie warstwa usług puli elastycznej hello obsługującego hello pożądane ustawienie. |
| 40870 |EX_USER |Witaj minimalna wartość DTU na bazę danych nie może przekroczyć (%d) dla warstwy usług "%. * ls. |Minimalna wartość DTU na bazę danych; Warstwa usług puli elastycznej. |Próba tooset hello minimalna wartość DTU na bazę danych poza hello obsługiwany limit. |Rozważ użycie warstwa usług puli elastycznej hello obsługującego hello pożądane ustawienie. |
| 40873 |EX_USER |Liczba Hello bazy danych (%d) i minimalna wartość DTU na bazę danych (%d) nie może przekraczać hello Dtu puli elastycznej hello (%d). |Liczba baz danych w puli elastycznej; Minimalna wartość DTU na bazę danych; Liczba jednostek Dtu puli elastycznej. |Próba toospecify minimalna wartość DTU dla baz danych w puli elastycznej hello przekraczającą hello Dtu puli elastycznej hello. |Należy rozważyć zwiększenie hello Dtu puli elastycznej hello, lub Zmniejsz hello minimalna wartość DTU na bazę danych lub Zmniejsz hello liczba baz danych w puli elastycznej hello. |
| 40877 |EX_USER |Nie można usunąć puli elastycznej, chyba że nie zawiera żadnych baz danych. |Brak |Pula elastyczna Hello zawiera jeden lub więcej baz danych i nie można usunąć. |Należy usunąć baz danych z puli elastycznej hello w kolejności toodelete go. |
| 40881 |EX_USER |Witaj puli elastycznej "%. * ls osiągnęła swój limit liczby bazy danych.  limit liczby bazy danych Hello hello puli elastycznej nie może przekroczyć (%d) dla puli elastycznej (% d) Dtu. |Nazwa puli elastycznej; limit liczby bazy danych w puli elastycznej; e Dtu dla puli zasobów. |Próba toocreate lub Dodaj pulę tooelastic bazy danych, po osiągnięciu limitu liczby bazy danych hello hello puli elastycznej. |Należy rozważyć zwiększenie hello Dtu hello puli elastycznej, jeśli to możliwe w kolejności tooincrease limit bazy danych lub usunąć z puli elastycznej hello bazy danych. |
| 40889 |EX_USER |Witaj Dtu lub limitu magazynowania dla puli elastycznej hello "%. * ls nie można zmniejszyć, ponieważ nie zapewniłoby z wystarczającą ilością wolnego miejsca dla bazy danych. |Nazwa puli elastycznej. |Próba limit magazynu hello toodecrease hello puli elastycznej poniżej jego użycia magazynu. |Rozważ ograniczenie użycia magazynu hello pojedynczych baz danych w puli elastycznej hello lub usuń jego Dtu lub magazynu bazy danych z puli hello w kolejności tooreduce limit. |
| 40891 |EX_USER |Witaj minimalna wartość DTU na bazę danych (%d) nie może przekraczać hello maksymalnej wartości DTU na bazę danych (%d). |Minimalna wartość DTU na bazę danych; Maksymalna wartość DTU na bazę danych. |Próba tooset hello minimalna wartość DTU na bazę danych jest większa niż maksymalna wartość DTU na bazę danych hello. |Upewnij się, że minimalna wartość DTU hello na baz danych nie przekracza hello maksymalna wartość DTU na bazę danych. |
| TBD |EX_USER |rozmiar magazynu Hello poszczególne bazy danych w puli elastycznej nie może przekraczać hello maksymalny rozmiar dozwolony przez "%. * puli elastycznej warstwy usługi ls. |Warstwa usług puli elastycznej |Maksymalny rozmiar Hello hello bazy danych przekracza hello maksymalny rozmiar dozwolony przez warstwa usług puli elastycznej hello. |Ustaw maksymalny rozmiar hello hello bazy danych, w ramach limitów hello hello maksymalny rozmiar dozwolony przez warstwa usług puli elastycznej hello. |

Tematy pokrewne:

* [Tworzenie puli elastycznej (C#)](sql-database-elastic-pool-manage-csharp.md) 
* [Zarządzanie puli elastycznej (C#)](sql-database-elastic-pool-manage-csharp.md). 
* [Tworzenie puli elastycznej (PowerShell)](sql-database-elastic-pool-manage-powershell.md) 
* [Monitorowanie i zarządzanie nimi puli elastycznej (PowerShell)](sql-database-elastic-pool-manage-powershell.md).

## <a name="general-errors"></a>Ogólne błędy
Witaj następujące błędy nie należą do żadnych poprzednich kategorii.

| Kod błędu: | Ważność | Opis |
| ---:| ---:|:--- |
| 15006 |16 |<AdministratorLogin>nie jest prawidłową nazwą, ponieważ zawiera ona nieprawidłowe znaki. |
| 18452 |14 |Logowanie nie powiodło się. Witaj nazwa logowania pochodzi z niezaufanej domeny i nie można używać z systemu Windows authentication.%. & #x2a; ls (nazwy logowania systemu Windows nie są obsługiwane w tej wersji programu SQL Server). |
| 18456 |14 |Logowanie nie powiodło się dla użytkownika "%. & #x2a;ls'.%. & #x2a % ls. & #x2a; ls (hello logowanie nie powiodło się dla użytkownika"%. & #x2a; ls". Nie można zmienić hasła Hello. Zmiany hasła podczas logowania nie jest obsługiwana w tej wersji programu SQL Server.) |
| 18470 |14 |Logowanie nie powiodło się dla użytkownika "%. & #x2a; ls". Przyczyna: konto hello jest disabled.%. & #x2a; ls |
| 40014 |16 |Nie można użyć wielu baz danych w hello tej samej transakcji. |
| 40054 |16 |Tabele bez indeksu klastrowanego są nieobsługiwane w tej wersji programu SQL Server. Utwórz indeks klastrowany i spróbuj ponownie. |
| 40133 |15 |Ta operacja jest nieobsługiwana w tej wersji programu SQL Server. |
| 40506 |16 |Określony identyfikator SID jest nieprawidłowy dla tej wersji programu SQL Server. |
| 40507 |16 |"%. & #x2a; ls nie można wywołać z parametrami w tej wersji programu SQL Server. |
| 40508 |16 |Użycie instrukcji nie jest obsługiwane tooswitch między bazami danych. Użyj nowego połączenia tooconnect tooa innej bazy danych. |
| 40510 |16 |Instrukcja "%. & #x2a; ls" nie jest obsługiwana w tej wersji programu SQL Server |
| 40511 |16 |Wbudowana funkcja "%. & #x2a; ls" nie jest obsługiwana w tej wersji programu SQL Server. |
| 40512 |16 |Przestarzałe funkcja '%ls' nie jest obsługiwana w tej wersji programu SQL Server. |
| 40513 |16 |Serwer zmiennej "%. & #x2a; ls" nie jest obsługiwana w tej wersji programu SQL Server. |
| 40514 |16 |'%ls' nie jest obsługiwana w tej wersji programu SQL Server. |
| 40515 |16 |Nazwa odwołania toodatabase i/lub serwera w "%. & #x2a; ls" nie jest obsługiwana w tej wersji programu SQL Server. |
| 40516 |16 |Globalne obiekty tymczasowe są nieobsługiwane w tej wersji programu SQL Server. |
| 40517 |16 |Słowo kluczowe lub opcja instrukcji "%. & #x2a; ls" nie jest obsługiwana w tej wersji programu SQL Server. |
| 40518 |16 |Polecenie DBCC "%. & #x2a; ls" nie jest obsługiwana w tej wersji programu SQL Server. |
| 40520 |16 |Zabezpieczana klasa "% S_MSG" jest nieobsługiwane w tej wersji programu SQL Server. |
| 40521 |16 |Zabezpieczana klasa "% S_MSG" jest nieobsługiwane w zakresie serwera hello w tej wersji programu SQL Server. |
| 40522 |16 |Typ podmiotu zabezpieczeń "%. & #x2a; ls" w bazie danych nie jest obsługiwane w tej wersji programu SQL Server. |
| 40523 |16 |Tworzenie "%. & #x2a; ls" niejawnego użytkownika nie jest obsługiwane w tej wersji programu SQL Server. Jawnie Utwórz użytkownika hello przed jego użyciem. |
| 40524 |16 |Typ danych "%. & #x2a; ls" nie jest obsługiwana w tej wersji programu SQL Server. |
| 40525 |16 |Z "%.ls" nie jest obsługiwane w tej wersji programu SQL Server. |
| 40526 |16 |"%. & #x2a; dostawcy zestawu wierszy ls nie jest obsługiwany w tej wersji programu SQL Server. |
| 40527 |16 |Połączonych serwerów nie są obsługiwane w tej wersji programu SQL Server. |
| 40528 |16 |Użytkownicy nie może być zmapowane toocertificates, klucze asymetryczne lub nazwy logowania systemu Windows w tej wersji programu SQL Server. |
| 40529 |16 |Wbudowana funkcja "%. & #x2a; ls" w personifikacji kontekst nie jest obsługiwany w tej wersji programu SQL Server. |
| 40532 |11 |Nie można otworzyć serwera "%. & #x2a; ls" zażądał hello logowania. Witaj logowanie nie powiodło się. |
| 40553 |16 |Witaj sesja została przerwana z powodu nadmiernego wykorzystania pamięci. Spróbuj zmodyfikować tooprocess Twojego zapytania mniej wierszy.<br/><br/>*Uwaga:* zmniejszeniu liczby hello `ORDER BY` i `GROUP BY` operacje w kodzie języka Transact-SQL pozwala zmniejszyć wymagania dotyczące pamięci hello kwerendy. |
| 40604 |16 |Można nie CREATE/ALTER DATABASE, ponieważ może to spowodować przekroczenie przydziału hello powitania serwera. |
| 40606 |16 |Dołączanie bazy danych nie jest obsługiwane w tej wersji programu SQL Server. |
| 40607 |16 |Nazwy logowania systemu Windows nie są obsługiwane w tej wersji programu SQL Server. |
| 40611 |16 |Serwery mogą mieć co najwyżej 128 reguł zapory. |
| 40614 |16 |Początkowy adres IP reguły zapory nie może przekraczać końcowy adres IP. |
| 40615 |16 |Nie można otworzyć serwera "{0}' zażądał hello logowania. Klient o adresie IP "{1}" tooaccess powitania serwera nie jest dozwolone.  tooenable dostępu, użyj hello portalu bazy danych SQL lub uruchom procedurę składowaną sp_set_firewall_rule na powitania bazy danych master toocreate reguły zapory dla tego adresu IP lub zakresu adresów.  Może potrwać toofive minut efektu tootake zmiany. |
| 40617 |16 |Nazwa reguły zapory Hello, która rozpoczyna się od <rule name> jest zbyt długa. Maksymalna długość to 128. |
| 40618 |16 |Nazwa reguły zapory Hello nie może być pusta. |
| 40620 |16 |Witaj logowanie nie powiodło się dla użytkownika "%. & #x2a; ls". Nie można zmienić hasła Hello. Zmiana hasła podczas logowania nie jest obsługiwana w tej wersji programu SQL Server. |
| 40627 |20 |Operacja na serwerze "{0}" i bazy danych "{1}" jest w toku. Poczekaj kilka minut przed podjęciem ponownej próby. |
| 40630 |16 |Sprawdzenie poprawności hasła nie powiodło się. Witaj hasło nie spełnia wymagań zasad, ponieważ jest zbyt krótki. |
| 40631 |16 |hasło określone Hello jest zbyt długa. hasło Hello powinna mieć nie więcej niż 128 znaków. |
| 40632 |16 |Sprawdzenie poprawności hasła nie powiodło się. Witaj hasło nie spełnia wymagań zasad, ponieważ nie jest wystarczająco złożone. |
| 40636 |16 |Nie można użyć zastrzeżonej nazwy bazy danych "%. & #x2a; ls" w tej operacji. |
| 40638 |16 |Nieprawidłowy identyfikator subskrypcji < identyfikator subskrypcji >. Subskrypcja nie istnieje. |
| 40639 |16 |Żądanie jest niezgodne z tooschema: <schema error>. |
| 40640 |20 |Witaj serwer napotkał nieoczekiwany wyjątek. |
| 40641 |16 |Witaj określona lokalizacja jest nieprawidłowa. |
| 40642 |17 |Serwer Hello jest obecnie zbyt zajęty. Spróbuj ponownie później. |
| 40643 |16 |Witaj określona wartość nagłówka x-ms-version jest nieprawidłowa. |
| 40644 |14 |Toohello dostępu nie powiodło się tooauthorize określonej subskrypcji. |
| 40645 |16 |ServerName <servername> nie może być pusta ani mieć wartości null. Go może zawierać tylko małe litery ''-'z', hello cyfry 0-9 i hello łącznik. Łącznik Hello nie mogą spowodować lub końcu hello nazwy. |
| 40646 |16 |Identyfikator subskrypcji nie może być pusta. |
| 40647 |16 |Subskrypcja < identyfikator subskrypcji nie ma servername serwera. |
| 40648 |17 |Wykonano zbyt wiele żądań. Spróbuj ponownie później. |
| 40649 |16 |Określono nieprawidłowy typ zawartości. Obsługiwane jest tylko aplikacja/xml. |
| 40650 |16 |Subskrypcja < identyfikator subskrypcji > nie istnieje lub nie jest gotowy do użycia hello. |
| 40651 |16 |Nie można toocreate serwera, ponieważ subskrypcja hello < identyfikator subskrypcji > jest wyłączona. |
| 40652 |16 |Nie można przenieść ani utworzyć serwera. Subskrypcja < identyfikator subskrypcji > przekroczy limit przydziału serwera. |
| 40671 |17 |Błąd komunikacji między bramą hello i hello usługi zarządzania. Spróbuj ponownie później. |
| 40852 |16 |Nie można otworzyć bazy danych "%. *ls na serwerze "%.* żądanie logowania hello ls. Toohello dostępu do bazy danych jest dozwolone tylko przy użyciu parametrów połączenia z włączoną obsługą zabezpieczeń. tooaccess to bazy danych, zmodyfikuj Twojej toocontain ciągów połączenia bezpieczne, na serwerze hello FQDN -.database.windows "Nazwa serwera".net powinna być nazwą too'server zmodyfikowane ".database. `secure`. windows.net. |
| 45168 |16 |Witaj systemu SQL Azure jest obciążony i umieszcza górny limit współbieżnych operacji CRUD bazy danych dla pojedynczego serwera (np. Tworzenie bazy danych). określony w komunikacie o błędzie hello serwer Hello przekroczyła maksymalną liczbę równoczesnych połączeń hello. Spróbuj ponownie później. |
| 45169 |16 |Witaj systemu SQL azure jest obciążony i umieszcza górny limit liczby powitania serwera równoczesnych operacji CRUD dla jednej subskrypcji (np. Utwórz serwera). Hello subskrypcji w błąd hello określony komunikat przekroczyła maksymalną liczbę równoczesnych połączeń hello i hello żądanie zostało odrzucone. Spróbuj ponownie później. |

## <a name="related-links"></a>Powiązane linki
* [Funkcje bazy danych Azure SQL](sql-database-features.md)
* [Limitom zasobów bazy danych SQL Azure](sql-database-resource-limits.md)

