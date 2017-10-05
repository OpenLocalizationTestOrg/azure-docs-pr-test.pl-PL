---
title: "Ładowanie danych do środowiska usługi Azure storage analytics | Dokumentacja firmy Microsoft"
description: "Przenoszenie danych do oraz z usługi Azure Blob Storage"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7fbf3bfedca8fa57a5e9428c9399558992b4acbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="15914-103">Ładowanie danych w środowiskach magazynowania do celów analizy</span><span class="sxs-lookup"><span data-stu-id="15914-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="15914-104">Proces nauki zespołu danych wymaga danych można pozyskanych lub ładowane do różnych środowiskach innego magazynu do przetworzenia lub przeanalizowane w najlepszy sposób na każdym etapie procesu.</span><span class="sxs-lookup"><span data-stu-id="15914-104">The Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments to be processed or analyzed in the most appropriate way in each stage of the process.</span></span> <span data-ttu-id="15914-105">Miejsca docelowe danych często używanych na potrzeby przetwarzania obejmują usługi Azure Blob Storage, baz danych SQL Azure, programu SQL Server na maszynie Wirtualnej platformy Azure, HDInsight (Hadoop) i usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="15914-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="15914-106">To **menu** linki do tematów opisujących sposób pozyskiwania danych w tych docelowe środowiska, w którym dane są przechowywane i przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="15914-106">This **menu** links to topics that describe how to ingest data into these target environments where the data is stored and processed.</span></span>

<span data-ttu-id="15914-107">Format techniczne i potrzeby biznesowe, a także początkową lokalizację oraz rozmiar danych określić środowiska docelowego, w których dane mają być pozyskanych w celach analizy.</span><span class="sxs-lookup"><span data-stu-id="15914-107">Technical and business needs, as well as the initial location, format and size of your data will determine the target environments into which the data needs to be ingested to achieve the goals of your analysis.</span></span> <span data-ttu-id="15914-108">Nie jest nietypowe dla scenariusza wymaganych danych do przeniesienia między środowiskami kilka do osiągnięcia różnych zadań wymaganych do utworzenia modelu predykcyjnego.</span><span class="sxs-lookup"><span data-stu-id="15914-108">It is not uncommon for a scenario to require data to be moved between several environments to achieve the variety of tasks required to construct a predictive model.</span></span> <span data-ttu-id="15914-109">Ta sekwencja zadań może zawierać na przykład Eksploracja danych, przetwarzanie wstępne czyszczenia, próbkowania w dół i uczenia modelu.</span><span class="sxs-lookup"><span data-stu-id="15914-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

