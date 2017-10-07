---
title: "aaaDiagnose i rozwiązywania problemów | Dokumentacja firmy Microsoft"
description: "W tym samouczku przedstawiono sposób toodiagnose i rozwiązywania problemów w środowisku Insights serii czasu"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a>Diagnozowanie i rozwiązywanie problemów w środowisku Insights serii czasu

## <a name="i-dont-see-my-data"></a>Moje dane nie są widoczne
Poniżej przedstawiono przyczyny, dlaczego może nie być wyświetlana danych w środowisku w hello [portal Azure czas serii Insights](https://insights.timeseries.azure.com).

### <a name="your-event-source-doesnt-have-data-in-json-format"></a>Źródła zdarzeń nie zawiera danych w formacie JSON
Azure czas serii Insights obsługuje obecnie tylko dane JSON. Przykłady JSON dla [kształtów JSON obsługiwany](time-series-insights-send-events.md#supported-json-shapes).

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a>Po zarejestrowaniu źródła zdarzeń nie dostarczył hello klucz, który ma uprawnienia wymagane hello
* Centrum IoT należy tooprovide hello klucz, który ma **usługa połączyć** uprawnienia.

   ![Uprawnienia do połączenia z usługi Centrum IoT](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   Jak pokazano w hello poprzedzających obrazu, albo hello zasad **iothubowner** i **usługi** będzie działać, ponieważ mają **usługa połączyć** uprawnienia.
* W przypadku Centrum zdarzeń należy tooprovide hello klucz, który ma **nasłuchiwania** uprawnienia.

   ![Uprawnienie nasłuchiwania Centrum zdarzeń](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   Jak pokazano w hello poprzedzających obrazu, albo zasad hello **odczytu** i **zarządzanie** będzie działać, ponieważ mają **nasłuchiwania** uprawnienia.

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a>Hello pod warunkiem, że grupy odbiorców jest wyłączne tooTime serii Insights
Centrum IoT i Centrum zdarzeń, aby uzyskać podczas rejestrowania wymagamy grupy odbiorców hello toospecify, które mają być używane do odczytywania danych. Ta grupa użytkowników nie muszą zostać udostępnione. Jeśli jest on udostępniony hello podstawowej Centrum zdarzeń automatycznie rozłącza jeden czytników hello losowo.

## <a name="i-see-my-data-but-theres-a-lag"></a>Dane są widoczne, ale istnieje opóźnienie
Poniżej przedstawiono przyczyny, dlaczego napotkać częściowe dane w środowisku w hello [portalu czasu serii Insights](https://insights.timeseries.azure.com).

### <a name="your-environment-is-getting-throttled"></a>Środowisko jest wprowadzenie ograniczany.
limit ograniczania Hello są wymuszane na podstawie typu jednostki SKU i pojemności hello środowiska. Wszystkie źródła zdarzeń w środowisku hello udostępnianie tej pojemności. Jeśli hello źródła zdarzenia z Centrum IoT i Centrum zdarzeń jest wypychanie danych po przekroczeniu limitów hello wymuszone, zobacz ograniczania przepustowości i opóźnienia.

powitania po diagram przedstawia środowisko czasu serii Insights, które ma SKU S1 i pojemności 3. Może on ruch przychodzący 3 miliony zdarzeń na dzień.

![Obecna pojemność jednostki SKU środowiska](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

Załóżmy, że to środowisko jest wprowadzania komunikaty z Centrum zdarzeń z prędkości wejściowej hello pokazano powitania po diagramu:

![Transfer danych przychodzących przykład szybkość Centrum zdarzeń](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

Jak pokazano na diagramie hello, stawki dziennej wejściowych hello jest ~ 67,000 wiadomości. Ta stawka tłumaczy około too46 wiadomości co minutę. Jeśli każdy komunikat Centrum zdarzeń jest spłaszczoną tooa pojedyncze zdarzenie Insights serii czasu, to środowisko widzi nie ograniczania. Jeśli każdy komunikat Centrum zdarzeń jest spłaszczoną too100 Insights serii czas zdarzenia, następnie 4,600 zdarzenia powinny być pozyskanych co minutę. Środowisku S1 SKU o pojemności 3 można tylko 2100 zdarzeń wejściowych co minutę (1 miliona zdarzeń na dzień = 700 zdarzenia na minutę na poziomie jednostki 3 = 2100 zdarzenia na minutę). W związku z tym Zobacz lag toothrottling ukończenia. 

Ogólny zrozumieć sposób działania spłaszczania logiki, zobacz [kształtów JSON obsługiwany](time-series-insights-send-events.md#supported-json-shapes).

#### <a name="recommended-steps"></a>Zalecane czynności
toofix hello opóźnienie hello zwiększyć pojemność jednostki SKU środowiska. Aby uzyskać więcej informacji, zobacz [jak tooscale środowiska czasu serii Insights](time-series-insights-how-to-scale-your-environment.md).

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a>Wypychanie danych historycznych i powodujące powolne wejściowych
Jeśli łączysz istniejące źródło zdarzenia jest prawdopodobne, że z Centrum IoT i Centrum zdarzeń zawiera już dane w nim. Dlatego środowiska hello uruchamia ściąganie danych z hello początek okresu przechowywania wiadomość hello zdarzeń źródła. 

To zachowanie jest hello domyślne zachowanie i nie może zostać zastąpiona. Można Uwzględnij, ograniczania i może upłynąć trochę czasu, toocatch się na odbieranie danych historycznych.

#### <a name="recommended-steps"></a>Zalecane czynności
toofix hello opóźnienie hello wykonaj następujące kroki:
1. Zwiększ hello SKU pojemności toohello maksymalną dozwoloną wartość (10, w tym przypadku). Po zwiększeniu pojemności hello rozpocznie się proces wejściowych hello, przechwytywanie się znacznie szybciej. Można zwizualizować, jak szybko jest przechwytywanie za pośrednictwem hello dostępności wykresu w hello [portalu czasu serii Insights](https://insights.timeseries.azure.com). Naliczane są opłaty za hello zwiększenie pojemności.
2. Po zawiera opóźnienie hello zmniejszania hello jednostki SKU pojemności wstecz tooyour normalne wejściowych.

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a>Źródła zdarzeń *nazwa właściwości sygnatury czasowej* ustawienie nie działa
Zapewnienia, że hello nazwy i wartości odpowiadają toohello następujące reguły:
* Nazwa właściwości sygnatury czasowej Hello jest _z uwzględnieniem wielkości liter_.
* wartość właściwości sygnatury czasowej Hello, które pochodzą ze źródła zdarzenia w postaci ciągu JSON, powinien mieć hello format _RRRR-MM-Ddtgg. FFFFFFFK_. Na przykład taki ciąg "2008-04-12T12:53Z".
