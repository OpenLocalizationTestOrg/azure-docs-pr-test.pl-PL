---
title: "aaaFix błędem połączenia SQL błąd przejściowy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot, diagnozowanie i zapobieganie błąd połączenia SQL lub Błąd przejściowy w bazie danych SQL Azure. "
keywords: "Połączenie SQL, ciąg połączenia, problemy z łącznością, błąd przejściowy, błąd połączenia"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a>Rozwiązywanie problemów, diagnozowanie i unikanie błędów połączenia SQL oraz błędów przejściowych w usłudze SQL Database
W tym artykule opisano, jak tooprevent, rozwiązywanie problemów, diagnozowanie i ograniczyć błędów połączenia i błędom przejściowym, których aplikacja kliencka napotka przy interakcji z bazy danych SQL Azure. Dowiedz się, jak tooconfigure Logika ponawiania próby utworzenia parametrów połączenia hello i inne ustawienia połączenia.

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a>Przejściowe błędy (błędów przejściowych)
Błąd przejściowy — Ponadto błędu przejściowego - ma podstawową przyczyną, który wkrótce zostanie rozwiązany automatycznie. Okazjonalne przyczyną błędów przejściowych jest podczas hello systemu Azure szybko przewiduje sprzętu zasobów toobetter równoważenia obciążenia różnych obciążeń. Większość tych zdarzeń ponowne konfigurowanie często Ukończono w mniej niż 60 sekund. Podczas tego zakresu czasu ponownej konfiguracji może mieć łączności wystawia tooAzure bazy danych SQL. Aplikacje łączenie tooAzure bazy danych SQL powinny być utworzone tooexpect tych błędów przejściowych dojścia ich zaimplementowanie ponów logikę w ich kodu zamiast udostępniając je toousers jako błędy aplikacji.

Jeśli program kliencki używa ADO.NET, program jest powiadamiany o błąd przejściowy hello przez throw hello z **SqlException**. Witaj **numer** właściwości można porównać z hello listę błędów przejściowych u góry hello tematu hello: [kody błędów SQL dla aplikacji klienckich, baza danych SQL](sql-database-develop-error-messages.md).

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Połączenie i polecenia
Będzie ponowić próbę nawiązania połączenia SQL hello lub ustanawiania go ponownie, w zależności od następujących hello:

* **Błąd przejściowy występuje podczas próby połączenia**: hello połączenie powinno być ponowione po opóźnienia przez kilka sekund.
* **Błąd przejściowy występuje w ciągu polecenia zapytania SQL**: hello polecenia należy nie natychmiast wykonać ponownie. Zamiast tego z opóźnieniem hello powinien świeżo ustanowić połączenia. Następnie można ponowić hello polecenia.

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a>Logika ponawiania próby dla błędów przejściowych
Programy klienckie, które od czasu do czasu wystąpienia błędu przejściowego są bardziej niezawodne, jeśli zawierają one logiki ponawiania próby.

Gdy program komunikuje się z bazą danych SQL Azure za pośrednictwem 3 oprogramowanie pośredniczące strony, zapytanie z dostawcą hello, czy oprogramowanie pośredniczące hello zawiera logiki ponawiania próby w przypadku błędów przejściowych.

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a>Zasady ponawiania
* Jeśli błąd hello jest przejściowe, należy wykonać ponownie tooopen próba połączenia.
* Instrukcję SQL SELECT, który zakończy się niepowodzeniem z powodu błędu przejściowego nie należy bezpośrednio wykonać ponownie.
  
  * Zamiast tego należy ustanowić nowego połączenia, a następnie ponów hello wybierz.
* Po instrukcji SQL UPDATE zakończy się niepowodzeniem z powodu błędu przejściowego, należy ustanowić połączenia świeże przed powitalne próba aktualizacji zostanie ponowiona.
  
  * Logika ponawiania Hello musi zapewnić, że ukończyć transakcji całą bazę danych hello lub tym hello cała transakcja zostanie wycofana.

#### <a name="other-considerations-for-retry"></a>Inne uwagi dotyczące ponownych prób
* Pliku wsadowego zostanie automatycznie uruchomiony po godzinach pracy, a które zostanie zakończony przed rano, akceptowalny toovery pacjenta długo interwałów czasu między jego ponownych prób.
* Program interfejsu użytkownika należy uwzględnić hello człowieka tendencję toogive się po zbyt długim czasie oczekiwania.
  
  * Jednak hello rozwiązania nie może być tooretry co kilka sekund, ponieważ te zasady mogą wypełniania hello system z żądaniami.

#### <a name="interval-increase-between-retries"></a>Zwiększ interwał między ponownymi próbami
Firma Microsoft zaleca opóźnienie 5 sekund przed ponowną próbą wykonania Twojego pierwszego. Ponawia próbę po krótszy niż 5 sekund opóźnienia ryzyko związane z usługą hello utrudnione w chmurze. Każda kolejne próby opóźnienie hello powinien być zwiększany wykładniczo, zapasowej tooa maksymalnie 60 sekund.

Omówienie hello *okresu blokowania* dla klientów używających ADO.NET jest dostępna w [programu SQL Server połączenia buforowanie (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

Można także tooset maksymalnej liczby ponownych prób zanim hello program własnym zakończy.

#### <a name="code-samples-with-retry-logic"></a>Przykłady kodu z logiki ponawiania próby
Przykłady kodu z logiki ponawiania próby w różnych językach programowania, są dostępne pod adresem:

* [Biblioteki połączeń dla bazy danych SQL i programu SQL Server](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a>Logika ponawiania testu
tootest Logika ponawiania należy symulować lub spowodować błąd, nie można usunąć, gdy program jest nadal uruchomiona.

##### <a name="test-by-disconnecting-from-hello-network"></a>Testowanie przez odłączenie od sieci hello
Jednym ze sposobów można przetestować Logika ponawiania jest toodisconnect sieciowej komputera klienckiego z hello hello program jest uruchomiona. Błąd Hello będą:

* **SqlException.Number** = 11001
* Komunikat o błędzie: "nie Nieznany host"

Jako część hello najpierw ponów próbę, program może poprawić błąd pisowni hello, a następnie spróbuj tooconnect.

toomake tym praktycznych, odłączeniu komputera od sieci hello przed rozpoczęciem pracy z programem. Następnie program rozpoznaje parametr czas, który powoduje, że hello program:

1. Dodaj tymczasowo 11001 tooits listę błędów tooconsider jako przejściowy.
2. Próba jego pierwszego połączenia w zwykły sposób.
3. Po hello jest zgłoszony błąd, Usuń z listy hello 11001.
4. Wyświetlony komunikat informujący hello użytkownika tooplug hello komputera do sieci hello.
   * Zatrzymać dalsze wykonywanie przy użyciu albo hello **Console.ReadLine** metody lub okna dialogowego z przycisku OK. Witaj naciśnięciu klawisza Enter hello po hello komputer jest podłączony do sieci hello.
5. Spróbuj ponownie wykonać tooconnect, oczekiwano Powodzenie.

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a>Testowanie według nazwy bazy danych hello błąd podczas nawiązywania połączenia
Program można celowo błędnie hello nazwy użytkownika przed hello pierwszą próbę połączenia. Błąd Hello będą:

* **SqlException.Number** = 18456
* Komunikat o błędzie: "Logowanie użytkownika"WRONG_MyUserName"nie powiodło się."

Jako część hello najpierw ponów próbę, program może poprawić błąd pisowni hello, a następnie spróbuj tooconnect.

toomake tym praktycznych, program może rozpoznać parametru czas, który powoduje, że hello program:

1. Dodaj tymczasowo 18456 tooits listę błędów tooconsider jako przejściowy.
2. Celowo Dodaj nazwę użytkownika toohello "WRONG_".
3. Po hello jest zgłoszony błąd, Usuń z listy hello 18456.
4. Usuń "WRONG_" z hello nazwy użytkownika.
5. Spróbuj ponownie wykonać tooconnect, oczekiwano Powodzenie.

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a>Parametry .NET SqlConnection ponownych prób połączenia
Jeśli program kliencki łączy tootooAzure bazy danych SQL przy użyciu klasy .NET Framework hello **System.Data.SqlClient.SqlConnection**, należy użyć .NET 4.6.1 lub nowszej (lub .NET Core), można wykorzystać jej funkcji ponów próbę połączenia. Szczegóły funkcji hello są [tutaj](http://go.microsoft.com/fwlink/?linkid=393996).

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


Podczas budowania hello [ciąg połączenia](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) dla Twojego **SqlConnection** obiektu, powinny koordynować wartości hello wśród hello następujące parametry:

* ConnectRetryCount &nbsp; &nbsp; *(wartość domyślna to 1. Zakres to od 0 do 255).*
* ConnectRetryInterval &nbsp; &nbsp; *(wartość domyślna to 1 sekundę. Zakres to od 1 do 60).*
* Limit czasu połączenia &nbsp; &nbsp; *(wartość domyślna to 15 sekund. Zakres to od 0 do 2147483647)*

W szczególności wybranej wartości upewnić powitania po true równości:

* Limit czasu połączenia = ConnectRetryCount * ConnectionRetryInterval

Na przykład, jeśli hello count = 3, interwał = 10 sekund, limit czasu równy tylko 29 sekund może nie dość przekazywać systemu hello wystarczająco dużo czasu, przez jego ponów 3 i końcowych na łączenie: 29 < 3 * 10.

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Połączenie i polecenia
Hello **ConnectRetryCount** i **ConnectRetryInterval** let parametrów z **SqlConnection** operację łączenia obiektu ponawiania hello bez informuje lub bothering Twojego Program, takich jak zwracanie program tooyour sterowania. ponowne próby Hello może wystąpić w hello następujące sytuacje:

* Wywołanie metody mySqlConnection.Open
* Wywołanie metody mySqlConnection.Execute

Brak subtlety. Jeśli wystąpi błąd przejściowy podczas Twojej *zapytania* jest wykonywana, Twoje **SqlConnection** obiekt łączy z nie hello ponów próbę wykonania operacji, a następnie go na pewno nie ponów próbę wykonania kwerendy. Jednak **SqlConnection** bardzo szybko kontroli hello połączenie przed wysłaniem kwerendy do wykonania. Jeśli szybkie sprawdzenie hello wykryje problem z połączeniem **SqlConnection** operację łączenia hello ponownych prób. Jeśli ponawiania hello zakończy się powodzeniem, możesz zapytanie jest wysyłane do wykonania.

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a>Czy ConnectRetryCount powinny być połączone z aplikacji logiki ponawiania próby?
Załóżmy, że aplikacja ma Logika ponawiania niestandardowych niezawodny. Może być ponów hello operację łączenia 4 godziny. Jeśli dodasz **ConnectRetryInterval** i **ConnectRetryCount** = 3 tooyour parametrów połączenia, zwiększy too4 liczby ponownych prób hello * 3 = 12 ponownych prób. Może nie ma takich dużą liczbę ponownych prób.

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a>TooAzure połączenia bazy danych SQL
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a>Połączenia: Parametry
Parametry połączenia Hello niezbędną do połączenia tooAzure bazy danych SQL są nieco inne niż ciąg hello podłączania tooMicrosoft programu SQL Server. Możesz skopiować hello parametry połączenia bazy danych z hello [portalu Azure](https://portal.azure.com/).

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a>Połączenia: Adres IP
Należy skonfigurować hello bazy danych SQL tooaccept komunikacji z serwerem z adresu IP hello hello komputera, który hostuje program kliencki. Można to zrobić, edytując ustawienia zapory hello za pośrednictwem hello [portalu Azure](https://portal.azure.com/).

Jeśli zapomnisz adres IP hello tooconfigure programu zakończy się niepowodzeniem, przydatną komunikat o błędzie stwierdzający hello niezbędne adresu IP.

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

Aby uzyskać więcej informacji, zobacz: [porady: Konfigurowanie ustawień zapory w bazie danych SQL](sql-database-configure-firewall-settings.md)

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a>Połączenia: porty
Zazwyczaj konieczne tooensure, czy port 1433 jest otwarty dla komunikacji wychodzącej, na komputerze hello, hostującym program kliencki.

Na przykład gdy program kliencki znajduje się na komputerze z systemem Windows, hello zapory systemu Windows na hoście hello pozwala tooopen portu 1433:

1. Otwórz Panel sterowania hello
2. &gt;Wszystkie elementy Panelu sterowania
3. &gt;Zapora systemu Windows
4. &gt;Ustawienia zaawansowane
5. &gt;Reguły ruchu wychodzącego
6. &gt;Akcje
7. &gt;Nowa reguła

Jeśli program kliencki znajduje się na maszynie wirtualnej platformy Azure (VM), należy przeczytać:<br/>[Porty inne niż 1433 ADO.NET 4.5 i bazy danych SQL](sql-database-develop-direct-route-ports-adonet-v12.md).

Aby uzyskać informacje dotyczące cofiguration portów i adresów IP, zobacz: [zapory bazy danych SQL Azure](sql-database-firewall-configure.md)

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a>Połączenie: ADO.NET 4.6.1
Jeśli program korzysta z klas ADO.NET, takich jak **System.Data.SqlClient.SqlConnection** tooAzure tooconnect bazy danych SQL, firma Microsoft zaleca użycie .NET Framework w wersji 4.6.1 lub nowszej.

ADO.NET 4.6.1:

* Bazy danych SQL Azure jest większą niezawodność po otwarciu połączenia przy użyciu hello **SqlConnection.Open** metody. Witaj **Otwórz** metoda zawiera teraz najlepsze nakładu ponawiania mechanizmy błędy tootransient odpowiedzi, niektóre błędy w określonym przedziale czasu połączenia hello.
* Obsługuje tworzenie puli połączeń. Obejmuje to efektywne weryfikacji, który hello połączenia obiektu udostępnia program działa.

Podczas korzystania z obiektu połączenia z puli połączeń, zaleca się, czy program tymczasowo zamknąć połączenie hello podczas nie bezpośrednio za pomocą. Ponowne otwarcie połączenia nie jest kosztowna hello sposób tworzenia nowego połączenia.

Jeśli używasz ADO.NET 4.0 lub wcześniejszym, zaleca się uaktualnienie toohello najnowsze ADO.NET.

* Począwszy od listopada 2015 r, możesz [Pobierz ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a>Diagnostyka
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a>Diagnostyka: Test sprawdzający, czy można połączyć z narzędzia
Jeśli program nie działa prawidłowo tooAzure tooconnect bazy danych SQL, jedną opcję diagnostyczne jest tooconnect tootry za pomocą narzędzia programu. W idealnym przypadku narzędzie hello będzie łączyć się przy użyciu hello samej bibliotece, używany przez program.

Na dowolnym komputerze z systemem Windows możesz spróbować tych narzędzi:

* SQL Server Management Studio (ssms.exe), który jest połączony za pomocą ADO.NET.
* sqlcmd.exe, który jest połączony za pomocą [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).

Po nawiązaniu połączenia, należy sprawdzić, czy działa krótkich zapytanie SQL SELECT.

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a>Diagnostyka: Sprawdź hello otwartych portów
Załóżmy, że podejrzewasz, że kończy się niepowodzeniem prób nawiązania połączenia z powodu tooport problemy. Na komputerze można uruchomić narzędzie, które raportów dotyczących konfiguracji portów hello.

Na powitania Linux mogą być przydatne następujące narzędzia:

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * (Zmienić hello przykładzie wartość toobe adresu IP).

W systemie Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) narzędzia mogą być pomocne. Oto wykonywania przykładzie, który proszeni hello sytuacji portu na serwerze bazy danych SQL Azure i której zostało uruchomione na komputerze przenośnym:

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a>Diagnostycznego: Błędy dziennika
Problem tymczasowy jest czasami najlepiej zdiagnozowany przez wykrywanie ogólne wzorca przez dni lub tygodnie.

Klient może pomóc w diagnozy przez funkcję rejestrowania wszystkich błędów napotkaniu. Może być możliwe toocorrelate wpisy dziennika hello z danymi błąd, który loguje się wewnętrznie bazy danych SQL Azure.

6 biblioteki przedsiębiorstwa (EntLib60) oferuje tooassist klas zarządzanych .NET z rejestrowaniem:

* [5 — jako łatwe jako objęte poza dziennika: przy użyciu hello bloku rejestrowania aplikacji](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a>Diagnostyka: Sprawdź dzienniki systemu pod kątem błędów
Poniżej przedstawiono niektóre instrukcji języka Transact-SQL SELECT tego zapytania dzienników błędów oraz innych informacji.

| Zapytanie dziennika | Opis |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |Witaj [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) widok zawiera informacje na temat poszczególnych zdarzeniami, w tym te, które mogą powodować przejściowe błędy lub awarie połączenia.<br/><br/>W idealnym przypadku można skorelować hello **godzina_rozpoczęcia** lub **end_time** wartości informująca, gdy program kliencki wystąpienia problemów.<br/><br/>**Porada:** należy połączyć toohello **wzorca** toorun bazy danych to. |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |Witaj [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) widoku oferuje zagregowanej liczby typów zdarzeń dla dodatkowych diagnostyczne.<br/><br/>**Porada:** należy połączyć toohello **wzorca** toorun bazy danych to. |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a>Diagnostyka: Wyszukaj problem zdarzeń w dzienniku bazy danych SQL hello
Możesz wyszukać wpisy dotyczące problemu zdarzenia w dzienniku hello bazy danych SQL Azure. Spróbuj hello następującej instrukcji języka Transact-SQL SELECT w hello **wzorca** bazy danych:

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a>Kilka wierszy zwrócony z sys.fn_xe_telemetry_blob_target_read_file
Następnie jest jak może wyglądać zwróconego wiersza. wartości zerowe Hello pokazano często nie mają wartości null w innych wierszy.

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a>Biblioteka Enterprise 6
6 biblioteki przedsiębiorstwa (EntLib60) to platforma klas .NET ułatwiająca implementację niezawodne klientów usługi w chmurze, z których jeden jest usługą bazy danych SQL Azure hello. Możesz znaleźć, obszar dedykowanych tooeach tematy, w którym EntLib60 może pomóc odwiedzając pierwszy:

* [Biblioteka Enterprise 6 kwietnia 2013 r.](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

Logika ponawiania do obsługi błędów przejściowych jest jeden obszar, w którym można pomóc EntLib60:

* [4 - perseverance, klucz tajny wszystkie sukcesy: przy użyciu hello bloku aplikacji obsługi błędów przejściowych](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> Witaj EntLib60 kod źródłowy jest dostępny dla publicznego [Pobierz](http://go.microsoft.com/fwlink/p/?LinkID=290898). Firma Microsoft nie ma funkcji dalsze toomake planów aktualizacji lub konserwacji tooEntLib aktualizacji.
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a>Klasy EntLib60 dla błędów przejściowych i spróbuj ponownie
następujące klasy EntLib60 Hello są szczególnie użyteczne w przypadku logiki ponawiania próby. Wszystkie te znajdują się w lub wchodzi w, hello przestrzeni nazw **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:

*W obszarze nazw hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*

* **RetryPolicy** — klasa
  
  * **ExecuteAction** — metoda
* **ExponentialBackoff** — klasa
* **SqlDatabaseTransientErrorDetectionStrategy** — klasa
* **ReliableSqlConnection** — klasa
  
  * **Parametr ExecuteCommand** — metoda

W obszarze nazw hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:

* **AlwaysTransientErrorDetectionStrategy** — klasa
* **NeverTransientErrorDetectionStrategy** — klasa

Oto łącza tooinformation o EntLib60:

* Bezpłatne [Pobierz książkę: tooMicrosoft przewodnik dewelopera biblioteki Enterprise wydanie 2](http://www.microsoft.com/download/details.aspx?id=41145)
* Najlepsze rozwiązania: [ponów ogólne wskazówki](../best-practices-retry-general.md) ma znakomity szczegółowym omówieniem logiki ponawiania próby.
* Pobieranie NuGet [Biblioteka Enterprise — Obsługa błędów przejściowych bloku aplikacji w wersji 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a>EntLib60: blok rejestrowania hello
* Blok rejestrowania Hello jest bardzo elastyczne i można skonfigurować rozwiązanie umożliwiający:
  
  * Utwórz i wiadomości dziennika są przechowywane w różnych lokalizacjach.
  * Przeprowadzania kategoryzacji i filtrowania wiadomości.
  * Zbierz informacje kontekstowe, które jest rejestrowanie przydatne do debugowania i śledzenia, a także do przeprowadzania inspekcji i ogólnych wymagań.
* Witaj rejestrowania bloku streszczenia Witaj logowania funkcji z hello miejsce docelowe dziennika, aby kod aplikacji hello jest spójne, niezależnie od hello lokalizację i typ magazynu rejestrowania docelowego hello.

Aby uzyskać więcej informacji, zobacz: [5 - jako łatwe jako objęte poza dziennika: przy użyciu rejestrowania bloku aplikacji hello](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a>Kod źródłowy EntLib60 IsTransient — metoda
Dalej z hello **SqlDatabaseTransientErrorDetectionStrategy** klasa, jest kod źródłowy hello C# hello **IsTransient** metody. Kod źródłowy Hello wyjaśnia, błędów, które zostały uznane za przejściowy toobe i ponów próbę, począwszy od kwietnia 2013 warta.

Wiele **//comment** wiersze zostały usunięte z tej kopii tooemphasize czytelności.

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a>Następne kroki
* Do rozwiązywania problemów inne typowe problemy z połączeniami bazy danych SQL Azure, odwiedź stronę [połączenia Rozwiązywanie problemów tooAzure bazy danych SQL](sql-database-troubleshoot-common-connection-issues.md).
* [Połączenie z serwerem SQL buforowanie (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [*Ponawianie próby* jest Apache 2.0 licencjonowane ogólnego przeznaczenia, ponawianie próby biblioteki napisany w **Python**, toosimplify hello zadania dodawania ponawiania toojust zachowanie dotyczące wszystkich elementów.](https://pypi.python.org/pypi/retrying)

