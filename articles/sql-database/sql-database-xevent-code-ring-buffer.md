---
title: "aaaXEvent bufor pierścień kod dla bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Zawiera przykładowy kod języka Transact-SQL, która zostaje łatwo i szybko przy użyciu hello bufor pierścień obiektu docelowego w bazie danych SQL Azure."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 2510fb3f-c8f2-437a-8f49-9d5f6c96e75b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 21df748d9999d6837d2b5bbe4a3f47fb351b4633
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a>Pierścienia kodu docelowego buforu dla zdarzeń rozszerzonych w bazie danych SQL

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Chcesz próbkę kompletny kod dla hello najprostszym szybko toocapture i przekazuje informacje dla zdarzeń rozszerzonych podczas testu. Najprostszym docelowy Hello danych zdarzeń rozszerzonych jest hello [docelowego buforu pierścień](http://msdn.microsoft.com/library/ff878182.aspx).

W tym temacie przedstawiono przykładowy kod języka Transact-SQL, który:

1. Tworzy tabelę z toodemonstrate danych z.
2. Tworzy sesję dla istniejących zdarzeń rozszerzonych mianowicie **sqlserver.sql_statement_starting**.
   
   * Witaj zdarzenie jest ograniczona tooSQL zawierających określony ciąg aktualizacji instrukcji: **instrukcji, takich jak '% aktualizacji tabEmployee %'**.
   * Wybiera dane wyjściowe hello toosend cel tooa zdarzenia hello typu pierścień buforu, a mianowicie **package0.ring_buffer**.
3. Uruchamia hello sesji zdarzeń.
4. Problemy z kilku prostych instrukcji SQL UPDATE.
5. Problemy z SQL SELECT instrukcji tooretrieve zdarzeń dane wyjściowe hello bufor pierścień.
   
   * **sys.dm_xe_database_session_targets** i innych dynamicznych widoków zarządzania (widoków DMV) są połączone.
6. Zatrzymuje hello sesji zdarzeń.
7. Porzucania hello pierścień buforu docelowego, toorelease jego zasoby.
8. Odrzuca hello sesji zdarzeń i hello pokaz tabeli.

## <a name="prerequisites"></a>Wymagania wstępne

* Konto i subskrypcja platformy Azure. Po zarejestrowaniu się możesz skorzystać z [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* Wszystkie bazy danych, które można utworzyć tabeli.
  
  * Opcjonalnie można [utworzyć **AdventureWorksLT** demonstracyjna baza danych](sql-database-get-started.md) w minutach.
* SQL Server Management Studio (ssms.exe), najlepiej najnowszej miesięcznej wersji aktualizacji. 
  Możesz pobrać najnowszą ssms.exe hello z:
  
  * Temat zatytułowany [pobierania programu SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Pobieranie toohello bezpośredniego łącza.](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a>Przykład kodu

Drobne modyfikacji hello Poniższy przykładowy kod bufor pierścień może działać w bazy danych SQL Azure lub programu Microsoft SQL Server. Witaj różnica polega na obecność hello hello węzła 'bazy _danych"w nazwie hello niektórych dynamicznych widoków zarządzania (widoków DMV), używany w klauzuli FROM hello w kroku 5. Na przykład:

* sys.dm_xe**bazy _danych**_session_targets
* sys.dm_xe_session_targets

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a>Zawartość buforów pierścień

My używamy przykładowy kod hello toorun ssms.exe.

wyniki hello tooview, możemy kliknięciu komórki hello w obszarze nagłówka kolumny hello **target_data_XML**.

Następnie w okienku wyników hello możemy kliknięciu komórki hello w obszarze nagłówka kolumny hello **target_data_XML**. Kliknij ten przycisk utworzyć inną kartę pliku w ssms.exe w których hello zawartość komórki wynik hello został wyświetlony, w formacie XML.

dane wyjściowe Hello jest wyświetlany w powitania po bloku. Wygląda na to długie, ale jest tylko dwa  **<event>**  elementów.

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a>Zwolnij zasoby zajmowane przez użytkownika bufor pierścień

Po zakończeniu Twojej buforem pierścienia, można ją usunąć i zwolnić jego zasoby wystawiania **ALTER** następujące hello, takich jak:

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


Definicja Hello sesji zdarzeń jest zaktualizowana, ale nie został porzucony. Później można dodać inne wystąpienie sesji zdarzeń tooyour bufor pierścień hello:

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a>Więcej informacji

temat głównej Hello rozszerzonej zdarzeń w bazie danych SQL Azure jest:

* [Rozszerzony zagadnienia dotyczące zdarzeń w bazie danych SQL](sql-database-xevent-db-diff-from-svr.md), która różni się znacząco niektórych aspektów rozszerzone zdarzenia, które różnią się od bazy danych SQL Azure i programu Microsoft SQL Server.

Inne tematy przykładowy kod dla zdarzeń rozszerzonych są dostępne pod adresem hello następującego łącza. Regularnie musi jednak sprawdzić wszelkie toosee próbki, czy hello przykładowy jest przeznaczony dla programu Microsoft SQL Server i bazy danych SQL Azure. Następnie można zdecydować, czy drobne zmiany są potrzebne toorun hello próbki.

* Przykładowy kod bazy danych SQL Azure: [kod docelowy plik zdarzeń rozszerzonych zdarzeń w bazie danych SQL](sql-database-xevent-code-event-file.md)

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
