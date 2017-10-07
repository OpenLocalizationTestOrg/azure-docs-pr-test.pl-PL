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
# <a name="load-data-into-storage-environments-for-analytics"></a>Ładowanie danych w środowiskach magazynowania do celów analizy
Hello zespołu w procesie nauki danych wymaga, aby dane można pozyskanych lub ładowane do szerokiej gamy magazynu różnych środowiskach toobe przetworzenia lub przeanalizowane w najlepszy sposób hello na każdym etapie procesu hello. Miejsca docelowe danych często używanych na potrzeby przetwarzania obejmują usługi Azure Blob Storage, baz danych SQL Azure, programu SQL Server na maszynie Wirtualnej platformy Azure, HDInsight (Hadoop) i usługi Azure Machine Learning. 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

To **menu** łączy tootopics, które opisują sposób tooingest danych w tych docelowe środowiska, w którym hello dane są przechowywane i przetwarzane.

Format techniczne i potrzeby biznesowe, a także hello początkową lokalizację oraz rozmiar danych określić środowiska docelowego hello konieczne do których hello toobe pozyskanych tooachieve hello celów analizy danych. Nie jest nietypowe dla scenariusza toobe danych toorequire przenosić między kilka środowisk tooachieve hello różnych zadań wymaganych tooconstruct model predykcyjny. Ta sekwencja zadań może zawierać na przykład Eksploracja danych, przetwarzanie wstępne czyszczenia, próbkowania w dół i uczenia modelu.

