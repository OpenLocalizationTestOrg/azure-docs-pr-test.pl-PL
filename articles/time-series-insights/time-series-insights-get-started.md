---
title: "aaaCreate środowiska Azure czas serii Insights | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, jak toocreate środowisko serii czasu, podłącz go źródło zdarzenia tooan i gotowe tooanalyze danych zdarzeń w minutach."
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a>Tworzenie nowego środowiska czasu serii wgląd w hello portalu Azure

Środowisko usługi Time Series Insights jest zasobem platformy Azure, który umożliwia pozyskiwanie i magazynowanie danych. Klienci udostępnić środowiska za pośrednictwem portalu Azure hello hello wymagana pojemność.

## <a name="steps-toocreate-hello-environment"></a>Kroki toocreate hello środowiska

Wykonaj te kroki toocreate środowiska:

1.  Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2.  Kliknij znak ("+") plus hello hello górnym lewym rogu.
3.  Wyszukiwanie "Czas serii Insights" w polu wyszukiwania hello.

  ![Utwórz środowisko czasu serii Insights hello](media/get-started/getstarted-create-environment1.png)

4.  Wybierz pozycję „Time Series Insights” i kliknij przycisk „Utwórz”.

  ![Utwórz grupę zasobów hello Insights serii czasu](media/get-started/getstarted-create-environment2.png)

5.  Podaj nazwę środowiska. Ta nazwa będzie reprezentować środowiska hello [Eksploratorze serię czas](https://insights.timeseries.azure.com).
6.  Wybierz subskrypcję. Musi ona zawierać źródło zdarzeń. Czas serii Insights może automatycznie wykrywa Centrum IoT Azure i Centrum zdarzeń zasobów istniejących w hello tej samej subskrypcji.
7.  Wybierz lub utwórz grupę zasobów. Grupa zasobów jest kolekcją używanych razem zasobów platformy Azure.
8.  Wybierz lokalizację hostowania. w centrach tooavoid przenoszenie danych między danych, wybierz lokalizację, która zawiera źródło zdarzeń.
9.  Wybierz warstwę cenową.
10. Wybierz wydajność. Wydajność środowiska można zmienić po jego utworzeniu.
11. Utwórz środowisko. Możesz również przypiąć pulpitu nawigacyjnego toohello środowisko, by mieć łatwy dostęp przy każdym logowaniu.

  ![Utwórz hello Insights serii czasu numeru pin toodashboard](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>Następne kroki

* [Definiowanie zasad dostępu danych](time-series-insights-data-access.md) tooaccess środowiska w [portalu Insights serii czasu](https://insights.timeseries.azure.com)
* [Tworzenie źródła zdarzeń](time-series-insights-add-event-source.md)
* [Wysyłanie zdarzeń](time-series-insights-send-events.md) toohello źródło zdarzenia
