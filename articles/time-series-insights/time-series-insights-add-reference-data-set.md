---
title: "aaaAdd odwołanie do zestawu danych tooyour Azure czas serii Insights środowiska | Dokumentacja firmy Microsoft"
description: "W tym samouczku Dodaj odwołanie do zestawu danych tooyour Insights serii czasu środowiska"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Tworzenie zestawu danych odwołania dla danego środowiska Insights serii czasu za pomocą portalu Ibiza hello

Odwołanie do zestawu danych jest kolekcją elementów, które zostały rozszerzone przy użyciu hello zdarzenia ze źródła zdarzenia. Aparat transferu danych przychodzących usługi Time Series Insights łączy zdarzenie ze źródła zdarzenia z elementem w zestawie danych referencyjnych. To rozszerzone zdarzenie jest następnie dostępne dla zapytania. Tego sprzężenia jest oparta na powitania kluczy zdefiniowane w zestawie danych odwołania.

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a>Kroki tooadd środowisku tooyour odwołanie do zestawu danych

1. Zaloguj się toohello [portalu Ibiza](https://portal.azure.com).
2. Kliknij przycisk "Wszystkie zasoby" hello menu po lewej stronie portalu Ibiza hello hello.
3. Wybierz środowisko usługi Time Series Insights.

    ![Utworzenie zestawu danych odwołania Insights serii czasu hello](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. Wybierz opcję „Zestawy danych referencyjnych”, kliknij przycisk „+ Dodaj”.

    ![Utworzenie zestawu danych hello czasu serii Insights odwołanie - szczegóły](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. Określ nazwę zestawu danych odwołania hello hello.
6. Określ nazwę klucza hello i jego typu. Ta nazwa i typ jest używane toopick hello prawidłowe właściwości ze zdarzenia hello w źródle zdarzeń. Na przykład jeśli podasz nazwę klucza jako "DeviceId" i typu "String" hello czasu Insights serii wejściowych aparat wyszukuje właściwości o nazwie hello "DeviceId" typu "String" hello zdarzenia przychodzącego. Musisz podać więcej niż jednego klucza toojoin ze zdarzeniem hello. Właściwość Hello musi odpowiadać nazwie jest rozróżniana wielkość liter.

     ![Utworzenie zestawu danych hello czasu serii Insights odwołanie - szczegóły](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. Kliknij przycisk „Utwórz”.

## <a name="next-steps"></a>Następne kroki

* [Zarządzanie danymi referencyjnymi](time-series-insights-manage-reference-data-csharp.md) na drodze programowej.
* Aby hello pełną dokumentację interfejsu API, zobacz [odwołania API danych](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) dokumentu.
