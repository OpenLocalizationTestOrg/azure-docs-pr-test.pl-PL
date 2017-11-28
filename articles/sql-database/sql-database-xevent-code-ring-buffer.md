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
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="7e500-103">Pierścienia kodu docelowego buforu dla zdarzeń rozszerzonych w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="7e500-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="7e500-104">Chcesz próbkę kompletny kod dla hello najprostszym szybko toocapture i przekazuje informacje dla zdarzeń rozszerzonych podczas testu.</span><span class="sxs-lookup"><span data-stu-id="7e500-104">You want a complete code sample for hello easiest quick way toocapture and report information for an extended event during a test.</span></span> <span data-ttu-id="7e500-105">Najprostszym docelowy Hello danych zdarzeń rozszerzonych jest hello [docelowego buforu pierścień](http://msdn.microsoft.com/library/ff878182.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e500-105">hello easiest target for extended event data is hello [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="7e500-106">W tym temacie przedstawiono przykładowy kod języka Transact-SQL, który:</span><span class="sxs-lookup"><span data-stu-id="7e500-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="7e500-107">Tworzy tabelę z toodemonstrate danych z.</span><span class="sxs-lookup"><span data-stu-id="7e500-107">Creates a table with data toodemonstrate with.</span></span>
2. <span data-ttu-id="7e500-108">Tworzy sesję dla istniejących zdarzeń rozszerzonych mianowicie **sqlserver.sql_statement_starting**.</span><span class="sxs-lookup"><span data-stu-id="7e500-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="7e500-109">Witaj zdarzenie jest ograniczona tooSQL zawierających określony ciąg aktualizacji instrukcji: **instrukcji, takich jak '% aktualizacji tabEmployee %'**.</span><span class="sxs-lookup"><span data-stu-id="7e500-109">hello event is limited tooSQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="7e500-110">Wybiera dane wyjściowe hello toosend cel tooa zdarzenia hello typu pierścień buforu, a mianowicie **package0.ring_buffer**.</span><span class="sxs-lookup"><span data-stu-id="7e500-110">Chooses toosend hello output of hello event tooa target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="7e500-111">Uruchamia hello sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7e500-111">Starts hello event session.</span></span>
4. <span data-ttu-id="7e500-112">Problemy z kilku prostych instrukcji SQL UPDATE.</span><span class="sxs-lookup"><span data-stu-id="7e500-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="7e500-113">Problemy z SQL SELECT instrukcji tooretrieve zdarzeń dane wyjściowe hello bufor pierścień.</span><span class="sxs-lookup"><span data-stu-id="7e500-113">Issues a SQL SELECT statement tooretrieve event output from hello Ring Buffer.</span></span>
   
   * <span data-ttu-id="7e500-114">**sys.dm_xe_database_session_targets** i innych dynamicznych widoków zarządzania (widoków DMV) są połączone.</span><span class="sxs-lookup"><span data-stu-id="7e500-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="7e500-115">Zatrzymuje hello sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7e500-115">Stops hello event session.</span></span>
7. <span data-ttu-id="7e500-116">Porzucania hello pierścień buforu docelowego, toorelease jego zasoby.</span><span class="sxs-lookup"><span data-stu-id="7e500-116">Drops hello Ring Buffer target, toorelease its resources.</span></span>
8. <span data-ttu-id="7e500-117">Odrzuca hello sesji zdarzeń i hello pokaz tabeli.</span><span class="sxs-lookup"><span data-stu-id="7e500-117">Drops hello event session and hello demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e500-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7e500-118">Prerequisites</span></span>

* <span data-ttu-id="7e500-119">Konto i subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7e500-119">An Azure account and subscription.</span></span> <span data-ttu-id="7e500-120">Po zarejestrowaniu się możesz skorzystać z [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e500-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7e500-121">Wszystkie bazy danych, które można utworzyć tabeli.</span><span class="sxs-lookup"><span data-stu-id="7e500-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="7e500-122">Opcjonalnie można [utworzyć **AdventureWorksLT** demonstracyjna baza danych](sql-database-get-started.md) w minutach.</span><span class="sxs-lookup"><span data-stu-id="7e500-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="7e500-123">SQL Server Management Studio (ssms.exe), najlepiej najnowszej miesięcznej wersji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7e500-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="7e500-124">Możesz pobrać najnowszą ssms.exe hello z:</span><span class="sxs-lookup"><span data-stu-id="7e500-124">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="7e500-125">Temat zatytułowany [pobierania programu SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e500-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="7e500-126">Pobieranie toohello bezpośredniego łącza.</span><span class="sxs-lookup"><span data-stu-id="7e500-126">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="7e500-127">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="7e500-127">Code sample</span></span>

<span data-ttu-id="7e500-128">Drobne modyfikacji hello Poniższy przykładowy kod bufor pierścień może działać w bazy danych SQL Azure lub programu Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7e500-128">With very minor modification, hello following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="7e500-129">Witaj różnica polega na obecność hello hello węzła 'bazy _danych"w nazwie hello niektórych dynamicznych widoków zarządzania (widoków DMV), używany w klauzuli FROM hello w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="7e500-129">hello difference is hello presence of hello node '_database' in hello name of some dynamic management views (DMVs), used in hello FROM clause in Step 5.</span></span> <span data-ttu-id="7e500-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7e500-130">For example:</span></span>

* <span data-ttu-id="7e500-131">sys.dm_xe**bazy _danych**_session_targets</span><span class="sxs-lookup"><span data-stu-id="7e500-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="7e500-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="7e500-132">sys.dm_xe_session_targets</span></span>

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

## <a name="ring-buffer-contents"></a><span data-ttu-id="7e500-133">Zawartość buforów pierścień</span><span class="sxs-lookup"><span data-stu-id="7e500-133">Ring Buffer contents</span></span>

<span data-ttu-id="7e500-134">My używamy przykładowy kod hello toorun ssms.exe.</span><span class="sxs-lookup"><span data-stu-id="7e500-134">We used ssms.exe toorun hello code sample.</span></span>

<span data-ttu-id="7e500-135">wyniki hello tooview, możemy kliknięciu komórki hello w obszarze nagłówka kolumny hello **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="7e500-135">tooview hello results, we clicked hello cell under hello column header **target_data_XML**.</span></span>

<span data-ttu-id="7e500-136">Następnie w okienku wyników hello możemy kliknięciu komórki hello w obszarze nagłówka kolumny hello **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="7e500-136">Then in hello results pane we clicked hello cell under hello column header **target_data_XML**.</span></span> <span data-ttu-id="7e500-137">Kliknij ten przycisk utworzyć inną kartę pliku w ssms.exe w których hello zawartość komórki wynik hello został wyświetlony, w formacie XML.</span><span class="sxs-lookup"><span data-stu-id="7e500-137">This click created another file tab in ssms.exe in which hello content of hello result cell was displayed, as XML.</span></span>

<span data-ttu-id="7e500-138">dane wyjściowe Hello jest wyświetlany w powitania po bloku.</span><span class="sxs-lookup"><span data-stu-id="7e500-138">hello output is shown in hello following block.</span></span> <span data-ttu-id="7e500-139">Wygląda na to długie, ale jest tylko dwa  **<event>**  elementów.</span><span class="sxs-lookup"><span data-stu-id="7e500-139">It looks long, but it is just two **<event>** elements.</span></span>

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


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="7e500-140">Zwolnij zasoby zajmowane przez użytkownika bufor pierścień</span><span class="sxs-lookup"><span data-stu-id="7e500-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="7e500-141">Po zakończeniu Twojej buforem pierścienia, można ją usunąć i zwolnić jego zasoby wystawiania **ALTER** następujące hello, takich jak:</span><span class="sxs-lookup"><span data-stu-id="7e500-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like hello following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="7e500-142">Definicja Hello sesji zdarzeń jest zaktualizowana, ale nie został porzucony.</span><span class="sxs-lookup"><span data-stu-id="7e500-142">hello definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="7e500-143">Później można dodać inne wystąpienie sesji zdarzeń tooyour bufor pierścień hello:</span><span class="sxs-lookup"><span data-stu-id="7e500-143">Later you can add another instance of hello Ring Buffer tooyour event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="7e500-144">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="7e500-144">More information</span></span>

<span data-ttu-id="7e500-145">temat głównej Hello rozszerzonej zdarzeń w bazie danych SQL Azure jest:</span><span class="sxs-lookup"><span data-stu-id="7e500-145">hello primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="7e500-146">[Rozszerzony zagadnienia dotyczące zdarzeń w bazie danych SQL](sql-database-xevent-db-diff-from-svr.md), która różni się znacząco niektórych aspektów rozszerzone zdarzenia, które różnią się od bazy danych SQL Azure i programu Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7e500-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="7e500-147">Inne tematy przykładowy kod dla zdarzeń rozszerzonych są dostępne pod adresem hello następującego łącza.</span><span class="sxs-lookup"><span data-stu-id="7e500-147">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="7e500-148">Regularnie musi jednak sprawdzić wszelkie toosee próbki, czy hello przykładowy jest przeznaczony dla programu Microsoft SQL Server i bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7e500-148">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="7e500-149">Następnie można zdecydować, czy drobne zmiany są potrzebne toorun hello próbki.</span><span class="sxs-lookup"><span data-stu-id="7e500-149">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

* <span data-ttu-id="7e500-150">Przykładowy kod bazy danych SQL Azure: [kod docelowy plik zdarzeń rozszerzonych zdarzeń w bazie danych SQL](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="7e500-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
