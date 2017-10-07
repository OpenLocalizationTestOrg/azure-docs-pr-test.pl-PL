---
title: "Magazyn w pamięci XTP aaaMonitor | Dokumentacja firmy Microsoft"
description: "Szacowana i monitorowanie magazynu w pamięci XTP korzystać, pojemności; Napraw błąd pojemności 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="3a3a5-103">Monitorowanie magazynu OLTP w pamięci</span><span class="sxs-lookup"><span data-stu-id="3a3a5-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="3a3a5-104">Korzystając z [OLTP w pamięci](sql-database-in-memory.md), dane w tabelach zoptymalizowanych pod kątem pamięci i zmiennych tabel znajdują się w magazynie OLTP w pamięci.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="3a3a5-105">Każda warstwa usług Premium ma maksymalny rozmiar magazynu OLTP w pamięci, które opisano w hello [artykułu warstwach usług bazy danych SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="3a3a5-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="3a3a5-106">Po przekroczeniu tego limitu insert i zaktualizować operacji mogą kończyć się niepowodzeniem (z powodu błędu 41823).</span><span class="sxs-lookup"><span data-stu-id="3a3a5-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="3a3a5-107">W tym momencie zostanie potrzebują tooeither usuwania danych tooreclaim pamięci lub Uaktualnij warstwę wydajności hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-107">At that point you will need tooeither delete data tooreclaim memory, or upgrade hello performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a><span data-ttu-id="3a3a5-108">Określić, czy dane będą pasować hello zakończenia przechowywania w pamięci</span><span class="sxs-lookup"><span data-stu-id="3a3a5-108">Determine whether data will fit within hello in-memory storage cap</span></span>
<span data-ttu-id="3a3a5-109">Określić limit magazynu hello: Zapoznaj się hello [artykułu warstwach usług bazy danych SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) dla caps magazynu hello hello różnych poziomów usług Premium.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-109">Determine hello storage cap: consult hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for hello storage caps of hello different Premium service tiers.</span></span>

<span data-ttu-id="3a3a5-110">Szacowanie pamięci wymagania dla tabeli zoptymalizowanej pod kątem pamięci działa hello sam sposób dla programu SQL Server, ponieważ jest w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-110">Estimating memory requirements for a memory-optimized table works hello same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="3a3a5-111">Potrwać kilka minut tooreview tematu [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a3a5-111">Take a few minutes tooreview that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="3a3a5-112">Należy pamiętać, że tabela hello i zmiennej wiersze tabeli, a także indeksów, są wliczane do rozmiaru danych przez użytkownika maksymalną hello.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-112">Note that hello table and table variable rows, as well as indexes, count toward hello max user data size.</span></span> <span data-ttu-id="3a3a5-113">Ponadto instrukcji ALTER TABLE musi mieć wystarczającej ilości miejsca toocreate nowej wersji hello całą tabelę i jego indeksy.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-113">In addition, ALTER TABLE needs enough room toocreate a new version of hello entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="3a3a5-114">Monitorowanie i zgłaszanie alertów</span><span class="sxs-lookup"><span data-stu-id="3a3a5-114">Monitoring and alerting</span></span>
<span data-ttu-id="3a3a5-115">Można monitorować użycie magazynu w pamięci w procentach hello [cap magazynu dla warstwę wydajności](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) w hello Azure [portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="3a3a5-115">You can monitor in-memory storage use as a percentage of hello [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="3a3a5-116">W bloku bazy danych hello Znajdź okno wykorzystania zasobów hello, a następnie kliknij przycisk Edytuj.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-116">On hello Database blade, locate hello Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="3a3a5-117">Następnie wybierz metrykę hello `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-117">Then select hello metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="3a3a5-118">tooadd alert, kliknij na powitania wykorzystania zasobów pole tooopen hello metryki bloku, a następnie kliknij pozycję Dodaj alert.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-118">tooadd an alert, click on hello Resource Utilization box tooopen hello Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="3a3a5-119">Lub użyj hello następujące zapytanie hello tooshow wartość użycia magazynu w pamięci:</span><span class="sxs-lookup"><span data-stu-id="3a3a5-119">Or use hello following query tooshow hello in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="3a3a5-120">Popraw sytuacji braku pamięci — błąd 41823</span><span class="sxs-lookup"><span data-stu-id="3a3a5-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="3a3a5-121">W operacji INSERT, UPDATE i Utwórz się niepowodzeniem z komunikatem o błędzie 41823 uruchomione wyniki braku pamięci.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="3a3a5-122">Komunikat o błędzie 41823 wskazuje, że hello tabel zoptymalizowanych pod kątem pamięci i zmiennych tabel Przekroczono maksymalny rozmiar hello.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-122">Error message 41823 indicates that hello memory-optimized tables and table variables have exceeded hello maximum size.</span></span>

<span data-ttu-id="3a3a5-123">tooresolve ten błąd, albo:</span><span class="sxs-lookup"><span data-stu-id="3a3a5-123">tooresolve this error, either:</span></span>

* <span data-ttu-id="3a3a5-124">Usuwanie danych z tabel zoptymalizowanych pod kątem pamięci hello, potencjalnie Odciążanie tootraditional danych hello, tabel opartej na dysku. lub,</span><span class="sxs-lookup"><span data-stu-id="3a3a5-124">Delete data from hello memory-optimized tables, potentially offloading hello data tootraditional, disk-based tables; or,</span></span>
* <span data-ttu-id="3a3a5-125">Uaktualnij tooone warstwy usługi hello za mało przechowywania w pamięci dla danych hello należy tookeep w tabelach zoptymalizowanych pod kątem pamięci.</span><span class="sxs-lookup"><span data-stu-id="3a3a5-125">Upgrade hello service tier tooone with enough in-memory storage for hello data you need tookeep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a3a5-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3a3a5-126">Next steps</span></span>
<span data-ttu-id="3a3a5-127">Do monitorowania wskazówki, zobacz [monitorowania bazy danych SQL Azure przy użyciu dynamicznych widoków zarządzania](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="3a3a5-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
