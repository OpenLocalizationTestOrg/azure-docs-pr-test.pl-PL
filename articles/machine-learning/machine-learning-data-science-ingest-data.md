---
title: "aaaLoad danych do środowiska usługi Azure storage analytics | Dokumentacja firmy Microsoft"
description: "Przenieś tooand danych z magazynu obiektów Blob platformy Azure"
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
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="9c92b-103">Ładowanie danych w środowiskach magazynowania do celów analizy</span><span class="sxs-lookup"><span data-stu-id="9c92b-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="9c92b-104">Hello zespołu w procesie nauki danych wymaga, aby dane można pozyskanych lub ładowane do szerokiej gamy magazynu różnych środowiskach toobe przetworzenia lub przeanalizowane w najlepszy sposób hello na każdym etapie procesu hello.</span><span class="sxs-lookup"><span data-stu-id="9c92b-104">hello Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments toobe processed or analyzed in hello most appropriate way in each stage of hello process.</span></span> <span data-ttu-id="9c92b-105">Miejsca docelowe danych często używanych na potrzeby przetwarzania obejmują usługi Azure Blob Storage, baz danych SQL Azure, programu SQL Server na maszynie Wirtualnej platformy Azure, HDInsight (Hadoop) i usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9c92b-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="9c92b-106">To **menu** łączy tootopics, które opisują sposób tooingest danych w tych docelowe środowiska, w którym hello dane są przechowywane i przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="9c92b-106">This **menu** links tootopics that describe how tooingest data into these target environments where hello data is stored and processed.</span></span>

<span data-ttu-id="9c92b-107">Format techniczne i potrzeby biznesowe, a także hello początkową lokalizację oraz rozmiar danych określić środowiska docelowego hello konieczne do których hello toobe pozyskanych tooachieve hello celów analizy danych.</span><span class="sxs-lookup"><span data-stu-id="9c92b-107">Technical and business needs, as well as hello initial location, format and size of your data will determine hello target environments into which hello data needs toobe ingested tooachieve hello goals of your analysis.</span></span> <span data-ttu-id="9c92b-108">Nie jest nietypowe dla scenariusza toobe danych toorequire przenosić między kilka środowisk tooachieve hello różnych zadań wymaganych tooconstruct model predykcyjny.</span><span class="sxs-lookup"><span data-stu-id="9c92b-108">It is not uncommon for a scenario toorequire data toobe moved between several environments tooachieve hello variety of tasks required tooconstruct a predictive model.</span></span> <span data-ttu-id="9c92b-109">Ta sekwencja zadań może zawierać na przykład Eksploracja danych, przetwarzanie wstępne czyszczenia, próbkowania w dół i uczenia modelu.</span><span class="sxs-lookup"><span data-stu-id="9c92b-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

