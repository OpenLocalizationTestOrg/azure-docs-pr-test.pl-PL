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
# <a name="leverage-other-services-with-sql-data-warehouse"></a>Korzystać z innych usług z usługą Magazyn danych SQL
Ponadto tooits podstawowe funkcje, SQL Data Warehouse umożliwia użytkownikom tooleverage hello wiele innych usług Azure obok.  W szczególności obecnie przekierowaliśmy toodeeply zintegrować z hello następujące kroki:

* Power BI
* Azure Data Factory
* Azure Machine Learning
* Usługa Azure Stream Analytics

Pracujemy nad tooconnect z większej liczby usług między hello ekosystemu platformy Azure.

## <a name="power-bi"></a>Power BI
Power BI integracji umożliwia moc obliczeniową hello tooleverage usługi SQL Data Warehouse z raportowaniem dynamiczne hello i wizualizacja usługi Power BI. Power BI integracji obecnie obejmuje:

* **Bezpośrednie połączenia**: bardziej zaawansowane połączenia z logiczną przekazywanie do magazynu danych SQL.  Zapewnia szybszy analizy na większą skalę.
* **Otwórz w usłudze Power BI**: przycisk "Otwórz w usłudze Power BI" hello przekazuje wystąpienie tooPower informacji analizy Biznesowej, co zapewnia bardziej optymalne połączenie.

Zobacz [integracji z usługą Power BI](sql-data-warehouse-integrate-power-bi.md) lub hello [dokumentacji usługi Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) Aby uzyskać więcej informacji.

## <a name="azure-data-factory"></a>Azure Data Factory
Fabryka danych Azure umożliwia użytkownikom toocreate zarządzanych platformy, które potoków złożonych obciążenia wyodrębniania.  Integracja SQL Data Warehouse z fabryką danych Azure obejmuje następujące hello:

* **Procedury składowane**: organizowania hello wykonywania procedur składowanych na magazyn danych SQL.
* **Kopiuj**: Użyj ADF toomove danych do usługi SQL Data Warehouse.  Tej operacji można używać mechanizmu przepływu danych standardowych ADF lub PolyBase w obszarze hello obejmuje. 

Zobacz [integracji z fabryką danych Azure](sql-data-warehouse-integrate-azure-data-factory.md) lub hello [dokumentacji fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/) Aby uzyskać więcej informacji.

## <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning to usługi analytics w pełni zarządzana, dzięki czemu użytkownicy toocreate modeli skomplikowanych wykorzystaniu dużego zestawu narzędzi predykcyjnej.  Magazyn danych SQL jest obsługiwany jako źródło i miejsce docelowe dla tych modeli hello następujące funkcje:

* **Odczyt danych:** dysków modeli na dużą skalę przed SQL Data Warehouse przy użyciu T-SQL.
* **Zapis danych:** zatwierdzania zmian z każdego modelu z powrotem tooSQL hurtowni danych.

Zobacz [integracji z usługą Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) lub hello [dokumentacji usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) Aby uzyskać więcej informacji.

## <a name="azure-stream-analytics"></a>Usługa Azure Stream Analytics
Usługa Azure Stream Analytics jest złożone, w pełni zarządzana infrastruktura przetwarzania i wykorzystywanie danych zdarzeń generowanych przez Centrum zdarzeń usługi Azure.  Integracja z usługą SQL Data Warehouse umożliwia przesyłanie strumieniowe danych toobe skutecznie przetwarzane i przechowywane obok danych relacyjnych włączenie głębiej, bardziej zaawansowane analizy.  

* **Dane wyjściowe zadania:** Wyślij dane wyjściowe Stream Analytics bezpośrednio zadania tooSQL hurtowni danych.

Zobacz [integracji z usługą Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) lub hello [dokumentacji usługi Azure Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/) Aby uzyskać więcej informacji.

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
