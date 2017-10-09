---
title: "aaaExtended zdarzeń w bazie danych SQL | Dokumentacja firmy Microsoft"
description: "Opisuje zdarzeń rozszerzonych (systemów Xevent) w bazie danych SQL Azure oraz jak sesji zdarzeń różnić się nieznacznie od sesji zdarzeń w programie Microsoft SQL Server."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 8c966a84412aa561c92b16e5c6902102483eb1bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="d7aa1-103">Rozszerzone zdarzenia w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="d7aa1-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="d7aa1-104">W tym temacie wyjaśniono, jak implementacja hello zdarzeń rozszerzonych w bazie danych SQL Azure jest nieco inne w porównaniu tooextended zdarzenia w programie Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-104">This topic explains how hello implementation of extended events in Azure SQL Database is slightly different compared tooextended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="d7aa1-105">Bazy danych SQL V12 uzyskane funkcja zdarzeń rozszerzonych hello hello drugi połowy kalendarza 2015.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-105">SQL Database V12 gained hello extended events feature in hello second half of calendar 2015.</span></span>
- <span data-ttu-id="d7aa1-106">SQL Server miał zdarzeń rozszerzonych od 2008.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="d7aa1-107">zestaw funkcji Hello rozszerzonej zdarzeń w bazie danych SQL jest podzbiór niezawodne funkcje hello na serwerze SQL.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-107">hello feature set of extended events on SQL Database is a robust subset of hello features on SQL Server.</span></span>

<span data-ttu-id="d7aa1-108">*Systemu XEvents* jest nieformalne pseudonimu, czasami używanego dla "zdarzeń rozszerzonych" blogów i innych nieformalne lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="d7aa1-109">Dodatkowe informacje o rozszerzonych zdarzeń dla usługi Azure SQL Database i programu Microsoft SQL Server są dostępne pod adresem:</span><span class="sxs-lookup"><span data-stu-id="d7aa1-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="d7aa1-110">Szybki Start: Rozszerzone zdarzenia w programie SQL Server</span><span class="sxs-lookup"><span data-stu-id="d7aa1-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="d7aa1-111">Rozszerzone zdarzenia</span><span class="sxs-lookup"><span data-stu-id="d7aa1-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="d7aa1-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d7aa1-112">Prerequisites</span></span>

<span data-ttu-id="d7aa1-113">W tym temacie przyjęto założenie, że masz już pewne informacje dotyczące:</span><span class="sxs-lookup"><span data-stu-id="d7aa1-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="d7aa1-114">[Usługa Azure SQL Database](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="d7aa1-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="d7aa1-115">[Rozszerzone zdarzenia](http://msdn.microsoft.com/library/bb630282.aspx) w programie Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="d7aa1-116">zbiorcze Hello dokumentacji dotyczących zdarzeń rozszerzonych stosuje tooboth programu SQL Server i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-116">hello bulk of our documentation about extended events applies tooboth SQL Server and SQL Database.</span></span>

<span data-ttu-id="d7aa1-117">Toohello przed ujawnieniem poniższych elementach jest przydatne, gdy wybieranie hello plik zdarzeń jako hello [docelowej](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="d7aa1-117">Prior exposure toohello following items is helpful when choosing hello Event File as hello [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="d7aa1-118">Usługi magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="d7aa1-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="d7aa1-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7aa1-119">PowerShell</span></span>
    - <span data-ttu-id="d7aa1-120">[Przy użyciu programu Azure PowerShell z usługą Azure Storage](../storage/common/storage-powershell-guide-full.md) — zawiera szczegółowe informacje na temat środowiska PowerShell i hello usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="d7aa1-121">Przykłady kodu</span><span class="sxs-lookup"><span data-stu-id="d7aa1-121">Code samples</span></span>

<span data-ttu-id="d7aa1-122">Powiązanych tematach przedstawiono dwa przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="d7aa1-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="d7aa1-123">Pierścienia kodu docelowego buforu dla zdarzeń rozszerzonych w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="d7aa1-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="d7aa1-124">Krótki prostego skryptu języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="d7aa1-125">Możemy wyróżnić w temacie przykładowy kod hello, że po zakończeniu z elementem docelowym pierścień buforu, należy zwolnić zasoby jego wykonując upuść alter `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-125">We emphasize in hello code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="d7aa1-126">Później można dodać inne wystąpienie buforu pierścień przez `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="d7aa1-127">Kod docelowego pliku zdarzenia rozszerzonego zdarzeń w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="d7aa1-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="d7aa1-128">Faza 1 jest toocreate PowerShell kontenera magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-128">Phase 1 is PowerShell toocreate an Azure Storage container.</span></span>
    - <span data-ttu-id="d7aa1-129">Faza 2 jest języka Transact-SQL używający hello kontenera magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-129">Phase 2 is Transact-SQL that uses hello Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="d7aa1-130">Różnice w języku Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="d7aa1-130">Transact-SQL differences</span></span>


- <span data-ttu-id="d7aa1-131">Podczas wykonywania hello [tworzenie zdarzeń sesji](http://msdn.microsoft.com/library/bb677289.aspx) polecenia na serwerze SQL, użyj hello **ON SERVER** klauzuli.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-131">When you execute hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use hello **ON SERVER** clause.</span></span> <span data-ttu-id="d7aa1-132">Ale w bazie danych SQL korzystasz hello **bazy danych na** klauzuli zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-132">But on SQL Database you use hello **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="d7aa1-133">Witaj **bazy danych na** klauzuli ma również zastosowanie toohello [ALTER zdarzenia sesji](http://msdn.microsoft.com/library/bb630368.aspx) i [PORZUCIĆ zdarzenia sesji](http://msdn.microsoft.com/library/bb630257.aspx) poleceń języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-133">hello **ON DATABASE** clause also applies toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="d7aa1-134">Najlepszym rozwiązaniem jest opcja sesji zdarzeń hello tooinclude z **STARTUP_STATE = ON** w Twojej **tworzenie zdarzeń sesji** lub **ALTER zdarzenia sesji** instrukcje.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-134">A best practice is tooinclude hello event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="d7aa1-135">Witaj **= ON** wartość obsługuje automatyczne ponowne uruchomienie po hello logicznej bazy danych z powodu pracy awaryjnej tooa zmiana konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-135">hello **= ON** value supports an automatic restart after a reconfiguration of hello logical database due tooa failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="d7aa1-136">Nowych widoków katalogów</span><span class="sxs-lookup"><span data-stu-id="d7aa1-136">New catalog views</span></span>

<span data-ttu-id="d7aa1-137">Witaj funkcji zdarzeń rozszerzonych jest obsługiwany przez kilka [widoków wykazu](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7aa1-137">hello extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="d7aa1-138">Widoków wykazu informujące o *metadanych lub definicji* sesji zdarzeń utworzonych przez użytkownika w bieżącej bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in hello current database.</span></span> <span data-ttu-id="d7aa1-139">Widoki Hello nie zwracają informacje na temat wystąpień zdarzeń aktywnych sesji.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-139">hello views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="d7aa1-140">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d7aa1-140">Name of</span></span><br/><span data-ttu-id="d7aa1-141">Przeglądanie katalogu</span><span class="sxs-lookup"><span data-stu-id="d7aa1-141">catalog view</span></span> | <span data-ttu-id="d7aa1-142">Opis</span><span class="sxs-lookup"><span data-stu-id="d7aa1-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7aa1-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="d7aa1-144">Zwraca wiersz dla każdej akcji każdego zdarzenia sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="d7aa1-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="d7aa1-146">Zwraca wiersz dla każdego zdarzenia w sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="d7aa1-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="d7aa1-148">Zwraca wiersz dla każdego dostosować w kolumnie jawnie ustawiona na zdarzenia i obiektów docelowych.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="d7aa1-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="d7aa1-150">Zwraca wiersz dla każdego obiektu docelowego zdarzeń dla sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="d7aa1-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="d7aa1-152">Zwraca wiersz dla każdej sesji zdarzeń w hello bazy danych SQL w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-152">Returns a row for each event session in hello SQL Database database.</span></span> |

<span data-ttu-id="d7aa1-153">Program Microsoft SQL Server, podobne widoków wykazu mają nazwy, które obejmują *.server\_*  zamiast *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="d7aa1-154">wzorzec nazwy Hello przypomina **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-154">hello name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="d7aa1-155">Nowe dynamicznych widoków zarządzania [(widoków DMV)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="d7aa1-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="d7aa1-156">Baza danych SQL Azure ma [dynamicznych widoków zarządzania (widoków DMV)](http://msdn.microsoft.com/library/bb677293.aspx) obsługujących zdarzeń rozszerzonych.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="d7aa1-157">Widoków DMV informujące o *active* sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="d7aa1-158">Nazwa DMV</span><span class="sxs-lookup"><span data-stu-id="d7aa1-158">Name of DMV</span></span> | <span data-ttu-id="d7aa1-159">Opis</span><span class="sxs-lookup"><span data-stu-id="d7aa1-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7aa1-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="d7aa1-161">Zwraca informacje o akcjach sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="d7aa1-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="d7aa1-163">Zwraca informacje dotyczące sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-163">Returns information about session events.</span></span> |
| <span data-ttu-id="d7aa1-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="d7aa1-165">Pokazuje hello wartości konfiguracji dla obiektów, które są powiązane tooa sesji.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-165">Shows hello configuration values for objects that are bound tooa session.</span></span> |
| <span data-ttu-id="d7aa1-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="d7aa1-167">Zwraca informacje na temat celów sesji.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="d7aa1-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="d7aa1-169">Zwraca wiersz dla każdej sesji zdarzeń, która jest zakresem toohello bieżącej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-169">Returns a row for each event session that is scoped toohello current database.</span></span> |

<span data-ttu-id="d7aa1-170">Program Microsoft SQL Server, podobne widoków wykazu są nazywane bez hello  *\_bazy danych* część hello name, takich jak:</span><span class="sxs-lookup"><span data-stu-id="d7aa1-170">In Microsoft SQL Server, similar catalog views are named without hello *\_database* portion of hello name, such as:</span></span>

- <span data-ttu-id="d7aa1-171">**sys.dm_xe_sessions**, a nie nazwy</span><span class="sxs-lookup"><span data-stu-id="d7aa1-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="d7aa1-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-tooboth"></a><span data-ttu-id="d7aa1-173">Typowe tooboth widoków DMV</span><span class="sxs-lookup"><span data-stu-id="d7aa1-173">DMVs common tooboth</span></span>
<span data-ttu-id="d7aa1-174">Dla zdarzeń rozszerzonych istnieją dodatkowe widoków DMV, które są typowe tooboth bazy danych SQL Azure i Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="d7aa1-174">For extended events there are additional DMVs that are common tooboth Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="d7aa1-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="d7aa1-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="d7aa1-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="d7aa1-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="d7aa1-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a><span data-ttu-id="d7aa1-179">Znajdowanie dostępnych zdarzeń rozszerzonych hello, działania i cele</span><span class="sxs-lookup"><span data-stu-id="d7aa1-179">Find hello available extended events, actions, and targets</span></span>

<span data-ttu-id="d7aa1-180">Możesz uruchomić proste SQL **wybierz** tooobtain listę dostępnych zdarzeń hello, akcje i obiekt docelowy.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-180">You can run a simple SQL **SELECT** tooobtain a list of hello available events, actions, and target.</span></span>

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<span data-ttu-id="d7aa1-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="d7aa1-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="d7aa1-182">Elementów docelowych dla sesji zdarzeń z bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="d7aa1-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="d7aa1-183">Poniżej przedstawiono obiektów docelowych, które można przechwycić wyniki z sesji zdarzeń w bazie danych SQL:</span><span class="sxs-lookup"><span data-stu-id="d7aa1-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="d7aa1-184">[Pierścień bufor docelowy](http://msdn.microsoft.com/library/ff878182.aspx) -krótko przechowuje dane zdarzenia w pamięci.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="d7aa1-185">[Docelowy licznik zdarzeń](http://msdn.microsoft.com/library/ff878025.aspx) -liczby wszystkich zdarzeń występujących podczas sesji zdarzeń rozszerzonych.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="d7aa1-186">[Docelowy plik zdarzeń](http://msdn.microsoft.com/library/ff878115.aspx) -kontenera magazynu Azure tooan pełną buforów zapisów.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers tooan Azure Storage container.</span></span>

<span data-ttu-id="d7aa1-187">Witaj [funkcji Śledzenie zdarzeń systemu Windows ()](http://msdn.microsoft.com/library/ms751538.aspx) interfejsu API nie jest dostępna dla zdarzeń rozszerzonych w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-187">hello [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="d7aa1-188">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="d7aa1-188">Restrictions</span></span>

<span data-ttu-id="d7aa1-189">Istnieje kilka różnic związanych z zabezpieczeniami befitting środowiska chmury hello bazy danych SQL:</span><span class="sxs-lookup"><span data-stu-id="d7aa1-189">There are a couple of security-related differences befitting hello cloud environment of SQL Database:</span></span>

- <span data-ttu-id="d7aa1-190">Zdarzeń rozszerzonych są oparte na powitania izolacji dzierżawców pojedynczego modelu.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-190">Extended events are founded on hello single-tenant isolation model.</span></span> <span data-ttu-id="d7aa1-191">Sesja zdarzeń w jednej bazie danych nie można uzyskać dostępu zdarzenia lub dane z innej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="d7aa1-192">Nie mogą wystawiać **tworzenie zdarzeń sesji** instrukcji w kontekście hello hello **wzorca** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-192">You cannot issue a **CREATE EVENT SESSION** statement in hello context of hello **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="d7aa1-193">Model uprawnień</span><span class="sxs-lookup"><span data-stu-id="d7aa1-193">Permission model</span></span>

<span data-ttu-id="d7aa1-194">Musi mieć **kontroli** uprawnień na powitania tooissue bazy danych **tworzenie zdarzeń sesji** instrukcji.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-194">You must have **Control** permission on hello database tooissue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="d7aa1-195">Witaj właściciel bazy danych (dbo) ma **kontroli** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-195">hello database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="d7aa1-196">Autoryzacje kontenera magazynu</span><span class="sxs-lookup"><span data-stu-id="d7aa1-196">Storage container authorizations</span></span>

<span data-ttu-id="d7aa1-197">Generowanie należy określić kontener z usługi Azure Storage tokenu sygnatury dostępu Współdzielonego Hello **rwl** hello uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-197">hello SAS token you generate for your Azure Storage container must specify **rwl** for hello permissions.</span></span> <span data-ttu-id="d7aa1-198">Witaj **rwl** wartość zawiera hello następujących uprawnień:</span><span class="sxs-lookup"><span data-stu-id="d7aa1-198">hello **rwl** value provides hello following permissions:</span></span>

- <span data-ttu-id="d7aa1-199">Odczyt</span><span class="sxs-lookup"><span data-stu-id="d7aa1-199">Read</span></span>
- <span data-ttu-id="d7aa1-200">Zapisywanie</span><span class="sxs-lookup"><span data-stu-id="d7aa1-200">Write</span></span>
- <span data-ttu-id="d7aa1-201">List</span><span class="sxs-lookup"><span data-stu-id="d7aa1-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="d7aa1-202">Zagadnienia dotyczące wydajności</span><span class="sxs-lookup"><span data-stu-id="d7aa1-202">Performance considerations</span></span>

<span data-ttu-id="d7aa1-203">Istnieją scenariusze, w którym intensywne użycie zdarzeń rozszerzonych może spowodować zgromadzenie aktywnych pamięci niż jest w dobrej kondycji dla hello całego systemu.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for hello overall system.</span></span> <span data-ttu-id="d7aa1-204">W związku z tym hello system bazy danych SQL Azure dynamicznie ustawia i dostosowuje limity hello ilość pamięci active można zgromadzonych przez usługę sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-204">Therefore hello Azure SQL Database system dynamically sets and adjusts limits on hello amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="d7aa1-205">Wiele czynników, przejdź do obliczania dynamicznej hello.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-205">Many factors go into hello dynamic calculation.</span></span>

<span data-ttu-id="d7aa1-206">Jeśli zostanie wyświetlony komunikat o błędzie z informacją, że maksymalna pamięci była wymuszana, są niektóre działania naprawcze, które można wykonać:</span><span class="sxs-lookup"><span data-stu-id="d7aa1-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="d7aa1-207">Uruchom mniejszą liczbę sesji jednoczesnych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="d7aa1-208">Za pomocą programu **Utwórz** i **ALTER** instrukcje dla sesji zdarzeń, Zmniejsz hello ilość pamięci na powitania **MAX\_pamięci** klauzuli.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce hello amount of memory you specify on hello **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="d7aa1-209">Opóźnienie sieci</span><span class="sxs-lookup"><span data-stu-id="d7aa1-209">Network latency</span></span>

<span data-ttu-id="d7aa1-210">Witaj **plik zdarzeń** docelowy może wystąpić opóźnienie sieci lub błędy podczas utrwalanie tooAzure danych z magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-210">hello **Event File** target might experience network latency or failures while persisting data tooAzure Storage blobs.</span></span> <span data-ttu-id="d7aa1-211">Inne zdarzenia w bazie danych SQL może zostać opóźnione przez toocomplete komunikacji sieciowej hello.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-211">Other events in SQL Database might be delayed while they wait for hello network communication toocomplete.</span></span> <span data-ttu-id="d7aa1-212">To opóźnienie może zmniejszyć obciążenie.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="d7aa1-213">toomitigate wydajności tego ryzyka, unikaj ustawiania hello **EVENT_RETENTION_MODE** opcję zbyt**NO_EVENT_LOSS** w definicji sesji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-213">toomitigate this performance risk, avoid setting hello **EVENT_RETENTION_MODE** option too**NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="d7aa1-214">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="d7aa1-214">Related links</span></span>

- <span data-ttu-id="d7aa1-215">[Używanie programu Azure PowerShell z usługą Azure Storage](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="d7aa1-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="d7aa1-216">Polecenia cmdlet usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d7aa1-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="d7aa1-217">[Przy użyciu programu Azure PowerShell z usługą Azure Storage](../storage/common/storage-powershell-guide-full.md) — zawiera szczegółowe informacje na temat środowiska PowerShell i hello usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>
- [<span data-ttu-id="d7aa1-218">Jak toouse magazynu obiektów Blob w .NET</span><span class="sxs-lookup"><span data-stu-id="d7aa1-218">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="d7aa1-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="d7aa1-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="d7aa1-220">Tworzenie sesji zdarzeń (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="d7aa1-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="d7aa1-221">Wpisy blogu Kehayias Jonathanowi o rozszerzonych zdarzenia w programie Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="d7aa1-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="d7aa1-222">Hello Azure *aktualizacje usługi* strony sieci Web, zawężony przez parametr tooAzure bazy danych SQL:</span><span class="sxs-lookup"><span data-stu-id="d7aa1-222">hello Azure *Service Updates* webpage, narrowed by parameter tooAzure SQL Database:</span></span>
    - [<span data-ttu-id="d7aa1-223">https://Azure.microsoft.com/Updates/?Service=SQL-Database</span><span class="sxs-lookup"><span data-stu-id="d7aa1-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="d7aa1-224">Inne tematy przykładowy kod dla zdarzeń rozszerzonych są dostępne pod adresem hello następującego łącza.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-224">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="d7aa1-225">Regularnie musi jednak sprawdzić wszelkie toosee próbki, czy hello przykładowy jest przeznaczony dla programu Microsoft SQL Server i bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-225">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="d7aa1-226">Następnie można zdecydować, czy drobne zmiany są potrzebne toorun hello próbki.</span><span class="sxs-lookup"><span data-stu-id="d7aa1-226">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
