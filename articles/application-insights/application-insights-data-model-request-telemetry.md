---
title: "aaaAzure aplikacji modelu danych Telemetrii Insights — żądanie Telemetrii | Dokumentacja firmy Microsoft"
description: "Model danych usługi Insights aplikacji dla dane telemetryczne żądania"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 6042975a35f5e672e5adb5390feecc63d0b284b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="request-telemetry-application-insights-data-model"></a>Żądanie telemetrii: model danych usługi Application Insights

Element dane telemetryczne żądania (w [usługi Application Insights](app-insights-overview.md)) reprezentuje hello logicznej sekwencji wykonywania wyzwalane przez aplikację tooyour żądania zewnętrznego. Każdy wykonywania żądania jest identyfikowany przez unikatowy `ID` i `url` zawierający wszystkie parametry wykonywania hello. Żądania można grupować wg logicznej `name` i zdefiniuj hello `source` tego żądania. Wykonanie kodu może spowodować `success` lub `fail` i ma określony `duration`. Może być zgrupowane wykonaniami sukcesów i niepowodzeń przez `resultCode`. Godzina rozpoczęcia dla dane telemetryczne żądania hello zdefiniowane na poziomie schematu envelope hello.

Żądanie telemetrii obsługuje modelu rozszerzalności standardowe hello przy użyciu niestandardowych `properties` i `measurements`.

## <a name="name"></a>Nazwa

Nazwa żądania hello reprezentuje żądania hello tooprocess ścieżkę kodu. Niski Kardynalność tooallow wartość lepiej grupowanie żądań. Dla żądania HTTP reprezentuje hello metody HTTP i szablon ścieżki adresu URL, takie jak `GET /values/{id}` bez rzeczywistego hello `id` wartość.

Aplikacji zestawu SDK sieci web Insights wysyła Nazwa żądania "w jakim jest" z przypadkiem tooletter zakresie. Grupowanie w interfejsie użytkownika jest rozróżniana wielkość liter, `GET /Home/Index` jest liczony oddzielnie od `GET /home/INDEX` mimo że często prowadzi hello takie same wykonywanie akcji i kontrolerów. Witaj przyczyny, która jest adresy URL na ogół są [z uwzględnieniem wielkości liter](http://www.w3.org/TR/WD-html40-970708/htmlweb.html). Może być toosee, jeśli wszystkie `404` dla adresów URL hello wpisany wielkimi literami. Możesz przeczytać więcej na żądanie nazwy kolekcji przez zestaw SDK sieci Web ASP.Net w hello [wpis w blogu](http://apmtips.com/blog/2015/02/23/request-name-and-url/).

Maksymalna długość: 1024 znaki

## <a name="id"></a>ID

Identyfikator wystąpienia wywołania żądania. Używane na potrzeby korelacji między żądaniem i innych elementów telemetrii. Identyfikator powinien być globalnie unikatowe. Aby uzyskać więcej informacji, zobacz [korelacji](application-insights-correlation.md) strony.

Maksymalna długość: 128 znaków

## <a name="url"></a>Url

Adres URL żądania z wszystkich parametrów ciągu zapytania.

Maksymalna długość: 2048 znaków

## <a name="source"></a>Element źródłowy

Źródło żądania hello. Przykłady są klucza Instrumentacji hello wywołującego hello lub adres ip hello hello wywołującego. Aby uzyskać więcej informacji, zobacz [korelacji](application-insights-correlation.md) strony.

Maksymalna długość: 1024 znaki

## <a name="duration"></a>Czas trwania

Żądaj czasu trwania w formacie: `DD.HH:MM:SS.MMMMMM`. Musi być dodatnia i mniejsza niż `1000` dni. To pole jest wymagane, ponieważ dane telemetryczne żądania reprezentuje hello operację, podając hello rozpoczęcie i zakończenie hello.

## <a name="response-code"></a>Kod odpowiedzi

Wynik wykonania żądania. Kod stanu HTTP dla żądania HTTP. Być może jest ona `HRESULT` wartość lub wyjątek typu dla innych typów żądań.

Maksymalna długość: 1024 znaki

## <a name="success"></a>Powodzenie

Oznaczenia wywołanie powiodła się czy nie. To pole jest wymagane. Gdy nie ustawiony w sposób jawny zbyt`false` -żądania toobe uznawany za pomyślny. Ustaw tę wartość za`false` Jeśli operacja została przerwana przez wyjątek lub zwrócił błąd o kodzie wynik.

W przypadku aplikacji sieci web hello usługi Application Insights zdefiniować żądania jako zakończony niepowodzeniem, jeśli kod odpowiedzi hello jest mniej hello `400` może być mniejszy niż zbyt`401`. Jeśli to domyślne mapowanie nie są zgodne hello semantycznego aplikacji hello istnieją jednak przypadki. Kod odpowiedzi `404` może wskazywać "żadne rekordy", które mogą być częścią regularnego przepływu. Może także wskazywać przerwany link. Hello przerwane łącza można zaimplementować nawet bardziej zaawansowanych logiki. Przerwane łącza można oznaczyć jako błędy tylko wtedy, gdy łącza te znajdują się na powitania sam lokacji analizując adres url odwołania. Lub oznaczyć je jako błędy podczas uzyskiwania dostępu do z aplikacji mobilnej hello firmy. Podobnie `301` i `302` wskazuje błąd podczas uzyskiwania dostępu do z powitania klienta, który nie obsługuje przekierowania.

Częściowo zaakceptowane zawartości `206` może wskazywać na błąd ogólny żądania. Na przykład punkt końcowy usługi Application Insights otrzymuje partii elementów telemetrii jako pojedyncze żądanie. Zwraca `206` Jeśli niektóre elementy w partii hello nie zostały przetworzone pomyślnie. Współczynnik zwiększania `206` wskazuje problem, który należy zbadać toobe. Podobne zastosuje zbyt`207` wiele stanów, gdzie mogą być Powodzenie hello hello najgorszy kody oddzielne odpowiedzi.

Możesz przeczytać więcej w wyniku żądania kodu i kodu stanu w hello [wpis w blogu](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).

## <a name="custom-properties"></a>Właściwości niestandardowe

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Miar niestandardowych

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Następne kroki

- [Pisanie niestandardowych żądanie telemetrii](app-insights-api-custom-events-metrics.md#trackrequest)
- Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.
- Dowiedz się, jak za[Konfigurowanie platformy ASP.NET Core](app-insights-asp-net.md) aplikacji z usługą Application Insights.
- Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.
