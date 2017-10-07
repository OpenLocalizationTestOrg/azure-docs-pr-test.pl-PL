---
title: "aaaMigrate tooSQL Twojego rozwiązania magazynu danych | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące migracji za platformy SQL Data Warehouse tooAzure rozwiązania."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a><span data-ttu-id="eedb5-103">Migrowanie tooAzure Twojego rozwiązania magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="eedb5-103">Migrate your solution tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="eedb5-104">Zobacz, na czym polega migracji istniejącej tooAzure rozwiązania bazy danych SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eedb5-104">See what's involved in migrating an existing database solution tooAzure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="eedb5-105">Profilu obciążenia</span><span class="sxs-lookup"><span data-stu-id="eedb5-105">Profile your workload</span></span>
<span data-ttu-id="eedb5-106">Przed migracją, która ma toobe pewność, że usługa SQL Data Warehouse jest hello odpowiednie rozwiązanie dla obciążenia.</span><span class="sxs-lookup"><span data-stu-id="eedb5-106">Before migrating, you want toobe certain SQL Data Warehouse is hello right solution for your workload.</span></span> <span data-ttu-id="eedb5-107">Magazyn danych SQL to Rozproszony system przeznaczony analytics tooperform na dużej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="eedb5-107">SQL Data Warehouse is a distributed system designed tooperform analytics on large data.</span></span>  <span data-ttu-id="eedb5-108">Migrowanie tooSQL magazyn danych wymaga pewnych zmian projektowych, które nie są zbyt twardych toounderstand, ale może potrwać kilka tooimplement czas.</span><span class="sxs-lookup"><span data-stu-id="eedb5-108">Migrating tooSQL Data Warehouse requires some design changes that are not too hard toounderstand but might take some time tooimplement.</span></span> <span data-ttu-id="eedb5-109">Firmy wymaga hurtowni danych klasy korporacyjnej, korzyści hello są warto hello wysiłku.</span><span class="sxs-lookup"><span data-stu-id="eedb5-109">If your business requires an enterprise-class data warehouse, hello benefits are worth hello effort.</span></span> <span data-ttu-id="eedb5-110">Jednak jeśli nie potrzebujesz zasilania hello usługi SQL Data Warehouse, to bardziej ekonomiczne toouse serwera SQL lub bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="eedb5-110">However, if you don't need hello power of SQL Data Warehouse, it is more cost-effective toouse SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="eedb5-111">Należy rozważyć użycie usługi SQL Data Warehouse przy możesz:</span><span class="sxs-lookup"><span data-stu-id="eedb5-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="eedb5-112">Ma co najmniej jeden terabajtów danych</span><span class="sxs-lookup"><span data-stu-id="eedb5-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="eedb5-113">Plan toorun analizy dużych ilości danych</span><span class="sxs-lookup"><span data-stu-id="eedb5-113">Plan toorun analytics on large amounts of data</span></span>
- <span data-ttu-id="eedb5-114">Należy hello możliwości tooscale obliczeniowej i pamięci masowej</span><span class="sxs-lookup"><span data-stu-id="eedb5-114">Need hello ability tooscale compute and storage</span></span> 
- <span data-ttu-id="eedb5-115">Chcę koszty toosave wstrzymując zasoby obliczeniowe, gdy nie są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="eedb5-115">Want toosave costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="eedb5-116">Magazyn danych SQL nie jest używany do operacyjnej obciążenia (OLTP), które mają:</span><span class="sxs-lookup"><span data-stu-id="eedb5-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="eedb5-117">Wysoka częstotliwość odczyty i zapisy</span><span class="sxs-lookup"><span data-stu-id="eedb5-117">High frequency reads and writes</span></span>
- <span data-ttu-id="eedb5-118">Wybiera dużą liczbę pojedynczych</span><span class="sxs-lookup"><span data-stu-id="eedb5-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="eedb5-119">Dużej ilości wstawia pojedynczy wiersz</span><span class="sxs-lookup"><span data-stu-id="eedb5-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="eedb5-120">Wiersz po wierszu przetwarzania potrzeb</span><span class="sxs-lookup"><span data-stu-id="eedb5-120">Row by row processing needs</span></span>
- <span data-ttu-id="eedb5-121">Niezgodnych formatach (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="eedb5-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-hello-migration"></a><span data-ttu-id="eedb5-122">Planowanie migracji hello</span><span class="sxs-lookup"><span data-stu-id="eedb5-122">Plan hello migration</span></span>

<span data-ttu-id="eedb5-123">Po określeniu toomigrate tooSQL istniejącego rozwiązania magazynu danych, jest ważne tooplan hello migracji przed rozpoczęciem pracy.</span><span class="sxs-lookup"><span data-stu-id="eedb5-123">Once you have decided toomigrate an existing solution tooSQL Data Warehouse, it is important tooplan hello migration before getting started.</span></span> 

<span data-ttu-id="eedb5-124">Jeden cel planowania jest tooensure dane z schematy tabeli i kodu są zgodne z usługą Magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="eedb5-124">One goal of planning is tooensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="eedb5-125">Brak niektórych zgodności różnice toowork wokół między bieżącego systemu i SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eedb5-125">There are some compatibility differences toowork around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="eedb5-126">Ponadto Migrowanie dużych ilości danych tooAzure wymaga czasu.</span><span class="sxs-lookup"><span data-stu-id="eedb5-126">Plus, migrating large amounts of data tooAzure takes time.</span></span> <span data-ttu-id="eedb5-127">Należy dokładnie zaplanować przyspiesza pobieranie tooAzure Twojego danych.</span><span class="sxs-lookup"><span data-stu-id="eedb5-127">Careful planning expedites getting your data tooAzure.</span></span> 

<span data-ttu-id="eedb5-128">Innym celem planowania jest projekt toomake tooensure dostosowań, które rozwiązanie korzysta z hello wysoką wydajność zapytań SQL Data Warehouse jest zaprojektowany tooprovide.</span><span class="sxs-lookup"><span data-stu-id="eedb5-128">Another goal of planning is toomake design adjustments tooensure your solution takes advantage of hello high query performance SQL Data Warehouse is designed tooprovide.</span></span> <span data-ttu-id="eedb5-129">Projektowania magazynów danych do skalowania wprowadza wzorce projektowania i dlatego tradycyjnych metod nie są zawsze hello najlepiej.</span><span class="sxs-lookup"><span data-stu-id="eedb5-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always hello best.</span></span> <span data-ttu-id="eedb5-130">Mimo że pewnych zmian projektu mogą być wykonywane po migracji, wcześniej wprowadzania zmian w procesie hello zapisze późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="eedb5-130">Although you can make some design adjustments after migration, making changes sooner in hello process will save time later.</span></span>

<span data-ttu-id="eedb5-131">tooperform udanej migracji, należy toomigrate Twojego schematy tabeli, kodu i danych.</span><span class="sxs-lookup"><span data-stu-id="eedb5-131">tooperform a successful migration, you need toomigrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="eedb5-132">Aby uzyskać wskazówki dotyczące tych tematów migracji zobacz:</span><span class="sxs-lookup"><span data-stu-id="eedb5-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="eedb5-133">Migracja z schematów</span><span class="sxs-lookup"><span data-stu-id="eedb5-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="eedb5-134">Migrowanie kodu</span><span class="sxs-lookup"><span data-stu-id="eedb5-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="eedb5-135">[Migrowanie danych](sql-data-warehouse-migrate-data.md).</span><span class="sxs-lookup"><span data-stu-id="eedb5-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a><span data-ttu-id="eedb5-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eedb5-136">Next steps</span></span>
<span data-ttu-id="eedb5-137">Hello CAT (zespół doradczy klientów) ma także niektóre dużą wskazówek magazyn danych SQL, które publikują one za pośrednictwem blogów.</span><span class="sxs-lookup"><span data-stu-id="eedb5-137">hello CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="eedb5-138">Spójrz na ich artykułu [migrowanie danych tooAzure SQL Data Warehouse w praktyce] [ Migrating data tooAzure SQL Data Warehouse in practice] dodatkowe wskazówki dotyczące migracji.</span><span class="sxs-lookup"><span data-stu-id="eedb5-138">Take a look at their article, [Migrating data tooAzure SQL Data Warehouse in practice][Migrating data tooAzure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
