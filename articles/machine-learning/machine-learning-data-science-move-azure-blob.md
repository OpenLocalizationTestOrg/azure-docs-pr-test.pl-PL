---
title: "aaaMove tooand danych z magazynu obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Przenieś tooand danych z magazynu obiektów Blob platformy Azure"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a>Przenieś tooand danych z magazynu obiektów Blob platformy Azure
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Która metoda jest najlepsze dla Ciebie zależy od danego scenariusza. Witaj [scenariusze zaawansowana analityka w usłudze Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) artykuł pomaga ustalić hello zasoby potrzebne dla różnych przepływów pracy nauki danych używany w hello zaawansowane analizy procesu.

> [!NOTE]
> Magazyn obiektów blob tooAzure pełne wprowadzenie można znaleźć za[podstawy obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) i zbyt[usługi obiektów Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

Alternatywnie, można użyć [fabryki danych Azure](https://azure.microsoft.com/services/data-factory/) do: 

* Tworzenie i planowanie potok, który pobiera dane z magazynu obiektów blob platformy Azure 
* przekazywanie ich tooa opublikowane usługi sieci web Azure Machine Learning, 
* otrzymywać wyniki analizy predykcyjnej hello, i 
* Przekaż hello toostorage wyników. 

Aby uzyskać więcej informacji, zobacz [tworzenie potoków predykcyjnej przy użyciu fabryki danych Azure i usługi Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).

## <a name="prerequisites"></a>Wymagania wstępne
Tym dokumencie przyjęto założenie, że masz subskrypcję platformy Azure, konta magazynu i hello odpowiedniego klucza magazynu dla tego konta. Przed przekazaniem/pobieranie danych, musisz znać Azure klucz konta magazynu nazwy i konta.

* tooset zapasową subskrypcji platformy Azure, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).
* Aby uzyskać instrukcje dotyczące tworzenia konta magazynu oraz uzyskiwanie konta i informacje o kluczu, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).

