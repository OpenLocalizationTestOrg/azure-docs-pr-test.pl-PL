---
title: "aaaBuild zintegrowanych rozwiązań z usługą Magazyn danych SQL | Dokumentacja firmy Microsoft"
description: "Narzędzia i partnerom rozwiązania, które integrują się z usługą Magazyn danych SQL. "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="370c5-103">Korzystać z innych usług z usługą Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="370c5-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="370c5-104">Ponadto tooits podstawowe funkcje, SQL Data Warehouse umożliwia użytkownikom tooleverage hello wiele innych usług Azure obok.</span><span class="sxs-lookup"><span data-stu-id="370c5-104">In addition tooits core functionality, SQL Data Warehouse enables users tooleverage many of hello other services in Azure alongside it.</span></span>  <span data-ttu-id="370c5-105">W szczególności obecnie przekierowaliśmy toodeeply zintegrować z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="370c5-105">Specifically, we have currently taken steps toodeeply integrate with hello following:</span></span>

* <span data-ttu-id="370c5-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="370c5-106">Power BI</span></span>
* <span data-ttu-id="370c5-107">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="370c5-107">Azure Data Factory</span></span>
* <span data-ttu-id="370c5-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="370c5-108">Azure Machine Learning</span></span>
* <span data-ttu-id="370c5-109">Usługa Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="370c5-109">Azure Stream Analytics</span></span>

<span data-ttu-id="370c5-110">Pracujemy nad tooconnect z większej liczby usług między hello ekosystemu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="370c5-110">We are working tooconnect with more services across hello Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="370c5-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="370c5-111">Power BI</span></span>
<span data-ttu-id="370c5-112">Power BI integracji umożliwia moc obliczeniową hello tooleverage usługi SQL Data Warehouse z raportowaniem dynamiczne hello i wizualizacja usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="370c5-112">Power BI integration allows you tooleverage hello compute power of SQL Data Warehouse with hello dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="370c5-113">Power BI integracji obecnie obejmuje:</span><span class="sxs-lookup"><span data-stu-id="370c5-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="370c5-114">**Bezpośrednie połączenia**: bardziej zaawansowane połączenia z logiczną przekazywanie do magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="370c5-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="370c5-115">Zapewnia szybszy analizy na większą skalę.</span><span class="sxs-lookup"><span data-stu-id="370c5-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="370c5-116">**Otwórz w usłudze Power BI**: przycisk "Otwórz w usłudze Power BI" hello przekazuje wystąpienie tooPower informacji analizy Biznesowej, co zapewnia bardziej optymalne połączenie.</span><span class="sxs-lookup"><span data-stu-id="370c5-116">**Open in Power BI**: hello 'Open in Power BI' button passes instance information tooPower BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="370c5-117">Zobacz [integracji z usługą Power BI](sql-data-warehouse-integrate-power-bi.md) lub hello [dokumentacji usługi Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="370c5-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or hello [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="370c5-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="370c5-118">Azure Data Factory</span></span>
<span data-ttu-id="370c5-119">Fabryka danych Azure umożliwia użytkownikom toocreate zarządzanych platformy, które potoków złożonych obciążenia wyodrębniania.</span><span class="sxs-lookup"><span data-stu-id="370c5-119">Azure Data Factory gives users a managed platform toocreate complex Extract-Load pipelines.</span></span>  <span data-ttu-id="370c5-120">Integracja SQL Data Warehouse z fabryką danych Azure obejmuje następujące hello:</span><span class="sxs-lookup"><span data-stu-id="370c5-120">SQL Data Warehouse's integration with Azure Data Factory includes hello following:</span></span>

* <span data-ttu-id="370c5-121">**Procedury składowane**: organizowania hello wykonywania procedur składowanych na magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="370c5-121">**Stored Procedures**: Orchestrate hello execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="370c5-122">**Kopiuj**: Użyj ADF toomove danych do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="370c5-122">**Copy**: Use ADF toomove data into SQL Data Warehouse.</span></span>  <span data-ttu-id="370c5-123">Tej operacji można używać mechanizmu przepływu danych standardowych ADF lub PolyBase w obszarze hello obejmuje.</span><span class="sxs-lookup"><span data-stu-id="370c5-123">This operation can use ADF's standard data movement mechanism or PolyBase under hello covers.</span></span> 

<span data-ttu-id="370c5-124">Zobacz [integracji z fabryką danych Azure](sql-data-warehouse-integrate-azure-data-factory.md) lub hello [dokumentacji fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="370c5-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="370c5-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="370c5-125">Azure Machine Learning</span></span>
<span data-ttu-id="370c5-126">Azure Machine Learning to usługi analytics w pełni zarządzana, dzięki czemu użytkownicy toocreate modeli skomplikowanych wykorzystaniu dużego zestawu narzędzi predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="370c5-126">Azure Machine Learning is a fully managed analytics service which allows users toocreate intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="370c5-127">Magazyn danych SQL jest obsługiwany jako źródło i miejsce docelowe dla tych modeli hello następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="370c5-127">SQL Data Warehouse is supported as both a source and destination for these models with hello following functionality:</span></span>

* <span data-ttu-id="370c5-128">**Odczyt danych:** dysków modeli na dużą skalę przed SQL Data Warehouse przy użyciu T-SQL.</span><span class="sxs-lookup"><span data-stu-id="370c5-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="370c5-129">**Zapis danych:** zatwierdzania zmian z każdego modelu z powrotem tooSQL hurtowni danych.</span><span class="sxs-lookup"><span data-stu-id="370c5-129">**Write Data:** Commit changes from any model back tooSQL Data Warehouse.</span></span>

<span data-ttu-id="370c5-130">Zobacz [integracji z usługą Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) lub hello [dokumentacji usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="370c5-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or hello [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="370c5-131">Usługa Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="370c5-131">Azure Stream Analytics</span></span>
<span data-ttu-id="370c5-132">Usługa Azure Stream Analytics jest złożone, w pełni zarządzana infrastruktura przetwarzania i wykorzystywanie danych zdarzeń generowanych przez Centrum zdarzeń usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="370c5-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="370c5-133">Integracja z usługą SQL Data Warehouse umożliwia przesyłanie strumieniowe danych toobe skutecznie przetwarzane i przechowywane obok danych relacyjnych włączenie głębiej, bardziej zaawansowane analizy.</span><span class="sxs-lookup"><span data-stu-id="370c5-133">Integration with SQL Data Warehouse allows for streaming data toobe effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="370c5-134">**Dane wyjściowe zadania:** Wyślij dane wyjściowe Stream Analytics bezpośrednio zadania tooSQL hurtowni danych.</span><span class="sxs-lookup"><span data-stu-id="370c5-134">**Job Output:** Send output from Stream Analytics jobs directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="370c5-135">Zobacz [integracji z usługą Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) lub hello [dokumentacji usługi Azure Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="370c5-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or hello [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
