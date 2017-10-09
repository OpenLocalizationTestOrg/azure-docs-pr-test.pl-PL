---
title: "aaaUse fabryki danych Azure z usługą Magazyn danych SQL | Dokumentacja firmy Microsoft"
description: "Porady dotyczące przy użyciu fabryki danych Azure (ADF) w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="c3ea9-103">Użyj fabryki danych Azure z usługą Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="c3ea9-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="c3ea9-104">Fabryka danych Azure zapewnia pełni zarządzanego metodę organizowanie hello transferu danych i wykonywania procedur składowanych na magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="c3ea9-104">Azure Data Factory provides a fully managed method for orchestrating hello transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="c3ea9-105">Pozwoli to toomore łatwo Konfiguracja i harmonogram złożony wyodrębniania, przekształcania i ładowania (ETL) procedur z usługą Magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="c3ea9-105">This will allow you toomore easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="c3ea9-106">Aby uzyskać bardziej szczegółowy przegląd fabryki danych Azure, zobacz hello [dokumentacji fabryki danych Azure][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="c3ea9-106">For a more complete overview of Azure Data Factory, see hello [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="c3ea9-107">Przenoszenie danych</span><span class="sxs-lookup"><span data-stu-id="c3ea9-107">Data Movement</span></span>
<span data-ttu-id="c3ea9-108">Fabryka danych Azure umożliwia przenoszenie danych między zarówno lokalnych źródeł i różnych usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c3ea9-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="c3ea9-109">Ogólne, bieżący integracji z fabryką danych Azure obsługuje tooand przeniesienia danych z hello następujących lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="c3ea9-109">Overall, current integration with Azure Data Factory supports data movement tooand from hello following locations:</span></span>

* <span data-ttu-id="c3ea9-110">Magazyn obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c3ea9-110">Azure blob storage</span></span>
* <span data-ttu-id="c3ea9-111">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c3ea9-111">Azure SQL Database</span></span>
* <span data-ttu-id="c3ea9-112">Lokalny serwer SQL</span><span class="sxs-lookup"><span data-stu-id="c3ea9-112">On-premises SQL Server</span></span>
* <span data-ttu-id="c3ea9-113">Program SQL Server na IaaS</span><span class="sxs-lookup"><span data-stu-id="c3ea9-113">SQL Server on IaaS</span></span>

<span data-ttu-id="c3ea9-114">Informacje dotyczące jak aktywność kopiowania tooset zapasowych sekcji [skopiować dane z fabryką danych Azure][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="c3ea9-114">For information on how tooset up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="c3ea9-115">Procedury składowane</span><span class="sxs-lookup"><span data-stu-id="c3ea9-115">Stored Procedures</span></span>
 <span data-ttu-id="c3ea9-116">W hello sam sposób można też używać tooschedule transferu danych, fabryki danych Azure mogą być używane tooorchestrate hello wykonywania procedur składowanych.</span><span class="sxs-lookup"><span data-stu-id="c3ea9-116">In hello same way it can be used tooschedule data transfer, Azure Data Factory can also be used tooorchestrate hello execution of stored procedures.</span></span>  <span data-ttu-id="c3ea9-117">Umożliwia bardziej złożonych toobe potoki utworzone i rozszerza fabryki danych Azure możliwości tooleverage hello moc obliczeniową usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ea9-117">This allows more complex pipelines toobe created and extends Azure Data Factory's ability tooleverage hello computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3ea9-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3ea9-118">Next steps</span></span>
<span data-ttu-id="c3ea9-119">Omówienie integracji, zobacz [Omówienie integracji usługi SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="c3ea9-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="c3ea9-120">Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="c3ea9-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

