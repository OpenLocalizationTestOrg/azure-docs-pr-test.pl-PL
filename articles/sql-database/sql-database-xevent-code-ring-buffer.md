---
title: "Kod bufor pierścień systemu XEvent dla bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Zawiera przykładowy kod języka Transact-SQL, które zostało utworzone przy użyciu obiektu docelowego buforu pierścień w bazie danych SQL Azure łatwo i szybko."
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
ms.openlocfilehash: 6fbefe151901ac3b15d93712422878fc4d6206f1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="4d9f7-103">Pierścienia kodu docelowego buforu dla zdarzeń rozszerzonych w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="4d9f7-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="4d9f7-104">Chcesz próbkę kompletny kod dla szybkiego Najprostszym sposobem przechwytywania i przekazuje informacje dla zdarzeń rozszerzonych podczas testu.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-104">You want a complete code sample for the easiest quick way to capture and report information for an extended event during a test.</span></span> <span data-ttu-id="4d9f7-105">Najprostszym elementu docelowego dla danych zdarzeń rozszerzonych jest [docelowego buforu pierścień](http://msdn.microsoft.com/library/ff878182.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d9f7-105">The easiest target for extended event data is the [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="4d9f7-106">W tym temacie przedstawiono przykładowy kod języka Transact-SQL, który:</span><span class="sxs-lookup"><span data-stu-id="4d9f7-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="4d9f7-107">Tworzy tabelę z danymi, aby zademonstrować z.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-107">Creates a table with data to demonstrate with.</span></span>
2. <span data-ttu-id="4d9f7-108">Tworzy sesję dla istniejących zdarzeń rozszerzonych mianowicie **sqlserver.sql_statement_starting**.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="4d9f7-109">Zdarzenie jest ograniczona do instrukcji SQL, które zawierają określony ciąg aktualizacji: **instrukcji, takich jak '% aktualizacji tabEmployee %'**.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-109">The event is limited to SQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="4d9f7-110">Wybiera do wysłania dane wyjściowe zdarzenia do elementu docelowego typu pierścień buforu, a mianowicie **package0.ring_buffer**.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-110">Chooses to send the output of the event to a target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="4d9f7-111">Uruchamia sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-111">Starts the event session.</span></span>
4. <span data-ttu-id="4d9f7-112">Problemy z kilku prostych instrukcji SQL UPDATE.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="4d9f7-113">Problemy z instrukcję SQL SELECT, aby pobrać dane wyjściowe zdarzenia z buforu pierścień.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-113">Issues a SQL SELECT statement to retrieve event output from the Ring Buffer.</span></span>
   
   * <span data-ttu-id="4d9f7-114">**sys.dm_xe_database_session_targets** i innych dynamicznych widoków zarządzania (widoków DMV) są połączone.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="4d9f7-115">Zatrzymuje sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-115">Stops the event session.</span></span>
7. <span data-ttu-id="4d9f7-116">Odrzuca docelowej pierścień buforu, aby zwolnić zasoby jego.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-116">Drops the Ring Buffer target, to release its resources.</span></span>
8. <span data-ttu-id="4d9f7-117">Odrzuca sesji zdarzeń i pokaz tabeli.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-117">Drops the event session and the demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d9f7-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4d9f7-118">Prerequisites</span></span>

* <span data-ttu-id="4d9f7-119">Konto i subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-119">An Azure account and subscription.</span></span> <span data-ttu-id="4d9f7-120">Po zarejestrowaniu się możesz skorzystać z [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d9f7-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4d9f7-121">Wszystkie bazy danych, które można utworzyć tabeli.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="4d9f7-122">Opcjonalnie można [utworzyć **AdventureWorksLT** demonstracyjna baza danych](sql-database-get-started.md) w minutach.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="4d9f7-123">SQL Server Management Studio (ssms.exe), najlepiej najnowszej miesięcznej wersji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="4d9f7-124">Możesz pobrać najnowszą ssms.exe od:</span><span class="sxs-lookup"><span data-stu-id="4d9f7-124">You can download the latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="4d9f7-125">Temat zatytułowany [pobierania programu SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d9f7-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="4d9f7-126">Łącze do pobrania.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-126">A direct link to the download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="4d9f7-127">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="4d9f7-127">Code sample</span></span>

<span data-ttu-id="4d9f7-128">Drobne zmiany w poniższym przykładzie kodu bufor pierścień umożliwia uruchamianie bazy danych SQL Azure lub programu Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-128">With very minor modification, the following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="4d9f7-129">Różnica polega na obecność węzeł 'bazy _danych"nazwach niektórych dynamicznych widoków zarządzania (widoków DMV), używany w klauzuli FROM w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-129">The difference is the presence of the node '_database' in the name of some dynamic management views (DMVs), used in the FROM clause in Step 5.</span></span> <span data-ttu-id="4d9f7-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4d9f7-130">For example:</span></span>

* <span data-ttu-id="4d9f7-131">sys.dm_xe**bazy _danych**_session_targets</span><span class="sxs-lookup"><span data-stu-id="4d9f7-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="4d9f7-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="4d9f7-132">sys.dm_xe_session_targets</span></span>

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

## <a name="ring-buffer-contents"></a><span data-ttu-id="4d9f7-133">Zawartość buforów pierścień</span><span class="sxs-lookup"><span data-stu-id="4d9f7-133">Ring Buffer contents</span></span>

<span data-ttu-id="4d9f7-134">My używamy ssms.exe uruchomić przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-134">We used ssms.exe to run the code sample.</span></span>

<span data-ttu-id="4d9f7-135">Aby wyświetlić wyniki, możemy kliknięciu komórki w nagłówku kolumny **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-135">To view the results, we clicked the cell under the column header **target_data_XML**.</span></span>

<span data-ttu-id="4d9f7-136">Następnie w okienku wyników możemy kliknięciu komórki w nagłówku kolumny **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-136">Then in the results pane we clicked the cell under the column header **target_data_XML**.</span></span> <span data-ttu-id="4d9f7-137">Kliknij ten przycisk utworzyć inną kartę pliku w ssms.exe w którym zawartość komórki wynik został wyświetlony, w formacie XML.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-137">This click created another file tab in ssms.exe in which the content of the result cell was displayed, as XML.</span></span>

<span data-ttu-id="4d9f7-138">Dane wyjściowe przedstawiono w następującym fragmencie.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-138">The output is shown in the following block.</span></span> <span data-ttu-id="4d9f7-139">Wygląda na to długie, ale jest tylko dwa  **<event>**  elementów.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-139">It looks long, but it is just two **<event>** elements.</span></span>

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


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="4d9f7-140">Zwolnij zasoby zajmowane przez użytkownika bufor pierścień</span><span class="sxs-lookup"><span data-stu-id="4d9f7-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="4d9f7-141">Po zakończeniu Twojej buforem pierścienia, można ją usunąć i zwolnić jego zasoby wystawiania **ALTER** podobnie do następującego:</span><span class="sxs-lookup"><span data-stu-id="4d9f7-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like the following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="4d9f7-142">Definicja sesji zdarzeń jest zaktualizowana, ale nie został porzucony.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-142">The definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="4d9f7-143">Później można dodać inne wystąpienie buforu pierścień do sesji zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="4d9f7-143">Later you can add another instance of the Ring Buffer to your event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="4d9f7-144">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="4d9f7-144">More information</span></span>

<span data-ttu-id="4d9f7-145">Podstawowy temat rozszerzonej zdarzeń w bazie danych SQL Azure jest:</span><span class="sxs-lookup"><span data-stu-id="4d9f7-145">The primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="4d9f7-146">[Rozszerzony zagadnienia dotyczące zdarzeń w bazie danych SQL](sql-database-xevent-db-diff-from-svr.md), która różni się znacząco niektórych aspektów rozszerzone zdarzenia, które różnią się od bazy danych SQL Azure i programu Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="4d9f7-147">Inne tematy przykładowy kod dla zdarzeń rozszerzonych są dostępne w poniższych łączy.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-147">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="4d9f7-148">Regularnie należy jednak sprawdzić wszelkie przykład, aby zobaczyć, czy próbki jest przeznaczony dla programu Microsoft SQL Server i bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-148">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="4d9f7-149">Następnie można zdecydować, czy drobne zmiany są potrzebne do uruchomienia przykładu.</span><span class="sxs-lookup"><span data-stu-id="4d9f7-149">Then you can decide whether minor changes are needed to run the sample.</span></span>

* <span data-ttu-id="4d9f7-150">Przykładowy kod bazy danych SQL Azure: [kod docelowy plik zdarzeń rozszerzonych zdarzeń w bazie danych SQL](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="4d9f7-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
