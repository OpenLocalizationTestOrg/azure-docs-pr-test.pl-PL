---
title: "Migracja rozwiązania do usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące migracji za rozwiązania do platformy Azure SQL Data Warehouse."
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
ms.openlocfilehash: 771b9456e66b8a1e41f72340b695b19e2adaf793
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-solution-to-azure-sql-data-warehouse"></a><span data-ttu-id="06f0e-103">Migracja rozwiązania do usługi Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="06f0e-103">Migrate your solution to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="06f0e-104">Zobacz, na czym polega migracji istniejącego rozwiązania bazy danych do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="06f0e-104">See what's involved in migrating an existing database solution to Azure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="06f0e-105">Profilu obciążenia</span><span class="sxs-lookup"><span data-stu-id="06f0e-105">Profile your workload</span></span>
<span data-ttu-id="06f0e-106">Przed przeprowadzeniem migracji, należy się, że niektóre usługi SQL Data Warehouse to odpowiednie rozwiązanie dla obciążenia.</span><span class="sxs-lookup"><span data-stu-id="06f0e-106">Before migrating, you want to be certain SQL Data Warehouse is the right solution for your workload.</span></span> <span data-ttu-id="06f0e-107">Magazyn danych SQL to Rozproszony system przeznaczone do wykonywania analizy w dużej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="06f0e-107">SQL Data Warehouse is a distributed system designed to perform analytics on large data.</span></span>  <span data-ttu-id="06f0e-108">Migracja do usługi SQL Data Warehouse wymaga pewnych zmian projektowych, które nie są zbyt niezbędne, aby dowiedzieć się, ale może potrwać pewien czas do wykonania.</span><span class="sxs-lookup"><span data-stu-id="06f0e-108">Migrating to SQL Data Warehouse requires some design changes that are not too hard to understand but might take some time to implement.</span></span> <span data-ttu-id="06f0e-109">Firmy wymaga hurtowni danych klasy korporacyjnej, korzyści są warto działania.</span><span class="sxs-lookup"><span data-stu-id="06f0e-109">If your business requires an enterprise-class data warehouse, the benefits are worth the effort.</span></span> <span data-ttu-id="06f0e-110">Jednak jeśli nie potrzebujesz możliwości usługi SQL Data Warehouse jest bardziej ekonomiczne rozwiązanie, aby użyć serwera SQL lub bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="06f0e-110">However, if you don't need the power of SQL Data Warehouse, it is more cost-effective to use SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="06f0e-111">Należy rozważyć użycie usługi SQL Data Warehouse przy możesz:</span><span class="sxs-lookup"><span data-stu-id="06f0e-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="06f0e-112">Ma co najmniej jeden terabajtów danych</span><span class="sxs-lookup"><span data-stu-id="06f0e-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="06f0e-113">Zaplanuj uruchamianie analityka w dużych ilości danych</span><span class="sxs-lookup"><span data-stu-id="06f0e-113">Plan to run analytics on large amounts of data</span></span>
- <span data-ttu-id="06f0e-114">Będą potrzebowali możliwości skalowania zasobów obliczeniowych i magazynu</span><span class="sxs-lookup"><span data-stu-id="06f0e-114">Need the ability to scale compute and storage</span></span> 
- <span data-ttu-id="06f0e-115">Czy chcesz zmniejszyć koszty wstrzymywanie zasoby obliczeniowe, gdy nie są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="06f0e-115">Want to save costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="06f0e-116">Magazyn danych SQL nie jest używany do operacyjnej obciążenia (OLTP), które mają:</span><span class="sxs-lookup"><span data-stu-id="06f0e-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="06f0e-117">Wysoka częstotliwość odczyty i zapisy</span><span class="sxs-lookup"><span data-stu-id="06f0e-117">High frequency reads and writes</span></span>
- <span data-ttu-id="06f0e-118">Wybiera dużą liczbę pojedynczych</span><span class="sxs-lookup"><span data-stu-id="06f0e-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="06f0e-119">Dużej ilości wstawia pojedynczy wiersz</span><span class="sxs-lookup"><span data-stu-id="06f0e-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="06f0e-120">Wiersz po wierszu przetwarzania potrzeb</span><span class="sxs-lookup"><span data-stu-id="06f0e-120">Row by row processing needs</span></span>
- <span data-ttu-id="06f0e-121">Niezgodnych formatach (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="06f0e-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-the-migration"></a><span data-ttu-id="06f0e-122">Planowanie migracji</span><span class="sxs-lookup"><span data-stu-id="06f0e-122">Plan the migration</span></span>

<span data-ttu-id="06f0e-123">Po określeniu migrację istniejącego rozwiązania do usługi SQL Data Warehouse, koniecznie planowania migracji, przed rozpoczęciem pracy.</span><span class="sxs-lookup"><span data-stu-id="06f0e-123">Once you have decided to migrate an existing solution to SQL Data Warehouse, it is important to plan the migration before getting started.</span></span> 

<span data-ttu-id="06f0e-124">Jeden celem planowania jest zapewnienie, że dane, z tabeli schematów i kodu są zgodne z usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="06f0e-124">One goal of planning is to ensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="06f0e-125">Istnieją pewne różnice zgodności w celu obejścia między bieżącego systemu i SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="06f0e-125">There are some compatibility differences to work around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="06f0e-126">Ponadto migracji dużych ilości danych do platformy Azure wymaga czasu.</span><span class="sxs-lookup"><span data-stu-id="06f0e-126">Plus, migrating large amounts of data to Azure takes time.</span></span> <span data-ttu-id="06f0e-127">Należy dokładnie zaplanować przyspiesza pobieranie danych do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="06f0e-127">Careful planning expedites getting your data to Azure.</span></span> 

<span data-ttu-id="06f0e-128">Innym celem planowania jest zmiany projektu upewnij się, że rozwiązanie korzysta z wysoką wydajność zapytań przez usługi SQL Data Warehouse pozwala uzyskać.</span><span class="sxs-lookup"><span data-stu-id="06f0e-128">Another goal of planning is to make design adjustments to ensure your solution takes advantage of the high query performance SQL Data Warehouse is designed to provide.</span></span> <span data-ttu-id="06f0e-129">Projektowanie hurtowni danych do skalowania wprowadza różnych projektowy wzorców i dlatego tradycyjnych metod nie zawsze są najlepiej.</span><span class="sxs-lookup"><span data-stu-id="06f0e-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always the best.</span></span> <span data-ttu-id="06f0e-130">Mimo że pewnych zmian projektu mogą być wykonywane po migracji, wcześniej wprowadzania zmian w procesie zapisze późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="06f0e-130">Although you can make some design adjustments after migration, making changes sooner in the process will save time later.</span></span>

<span data-ttu-id="06f0e-131">Do przeprowadzenia prawidłowej migracji, należy przeprowadzić migrację z tabeli schematów, kodu i danych.</span><span class="sxs-lookup"><span data-stu-id="06f0e-131">To perform a successful migration, you need to migrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="06f0e-132">Aby uzyskać wskazówki dotyczące tych tematów migracji zobacz:</span><span class="sxs-lookup"><span data-stu-id="06f0e-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="06f0e-133">Migracja z schematów</span><span class="sxs-lookup"><span data-stu-id="06f0e-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="06f0e-134">Migrowanie kodu</span><span class="sxs-lookup"><span data-stu-id="06f0e-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="06f0e-135">[Migrowanie danych](sql-data-warehouse-migrate-data.md).</span><span class="sxs-lookup"><span data-stu-id="06f0e-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform the migration


## Deploy the solution


## Validate the migration

-->

## <a name="next-steps"></a><span data-ttu-id="06f0e-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="06f0e-136">Next steps</span></span>
<span data-ttu-id="06f0e-137">CAT (zespół doradczy klientów) ma także niektóre dużą wskazówek magazyn danych SQL, które publikują one za pośrednictwem blogów.</span><span class="sxs-lookup"><span data-stu-id="06f0e-137">The CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="06f0e-138">Spójrz na ich artykułu [migrowanie danych do usługi Azure SQL Data Warehouse w praktyce] [ Migrating data to Azure SQL Data Warehouse in practice] dodatkowe wskazówki dotyczące migracji.</span><span class="sxs-lookup"><span data-stu-id="06f0e-138">Take a look at their article, [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data to Azure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
