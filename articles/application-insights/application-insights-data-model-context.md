---
title: aaaAzure aplikacji modelu danych Telemetrii Insights - kontekstu Telemetrii | Dokumentacja firmy Microsoft
description: Model danych kontekstu aplikacji Insights telemetrii
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a>Kontekst danych telemetrii: model danych usługi Application Insights

Każdy element danych telemetrycznych może mieć pól jednoznacznie kontekstu. Każde pole umożliwia scenariusza monitorowania. Użyj hello niestandardowe właściwości z kolekcji toostore niestandardowych lub specyficznych dla aplikacji informacje kontekstowe.


##<a name="application-version"></a>Wersja aplikacji

Informacje w polach kontekstu aplikacji hello jest zawsze o aplikacji hello, który wysyła dane telemetryczne hello. Wersja aplikacji jest używany tooanalyze trend zmiany w zachowanie aplikacji hello i jej wdrożenia toohello korelacji.

Maksymalna długość: 1024


##<a name="client-ip-address"></a>Adres IP klienta

adres IP Hello powitania klienta urządzenia. IPv4 i IPv6 są obsługiwane. Po wysłaniu danych telemetrycznych z usługi kontekstu lokalizacji hello jest o hello użytkownika, który zainicjował operację hello hello usługi. Usługi Application Insights wyodrębnienia informacji o lokalizacji geograficznej hello z hello IP klienta, a następnie instrukcja truncate. Dlatego IP klienta samodzielnie nie można użyć jako informacje umożliwiające identyfikację użytkownika końcowego. 

Maksymalna długość: 46


##<a name="device-type"></a>Typ urządzenia

Pierwotnie został użyty w tym polu tooindicate hello typ użytkownika końcowego hello urządzenia hello aplikacji hello. Dzisiaj hello urządzenia typu "Przeglądarki" z telemetrii po stronie serwera z typem urządzenia hello 'Komputera' użyć głównie toodistinguish JavaScript telemetrii.

Maksymalna długość: 64


##<a name="operation-id"></a>Identyfikator operacji

Unikatowy identyfikator hello działania głównego. Ten identyfikator umożliwia telemetrii toogroup przez kilka składników. Zobacz [korelacji telemetrii](application-insights-correlation.md) szczegółowe informacje. Identyfikator operacji Hello jest tworzony przez żądanie lub widok strony. Wszystkie inne dane telemetryczne ustawia tego pola wartość toohello hello zawierające żądania lub widoku strony. 

Maksymalna długość: 128


##<a name="parent-operation-id"></a>Identyfikator działania nadrzędnego

Witaj Unikatowy identyfikator hello telemetrii bezpośrednim elementem nadrzędnym składnika. Zobacz [korelacji telemetrii](application-insights-correlation.md) szczegółowe informacje.

Maksymalna długość: 128


##<a name="operation-name"></a>Nazwa operacji

Nazwa Hello (grupa) hello operacji. Nazwa operacji Hello jest tworzony przez żądanie lub widok strony. Wszystkie pozostałe elementy danych telemetrycznych ta wartość pola toohello dla hello zawierające żądania lub strony widoku. Nazwa operacji służy do znajdowania wszystkie elementy telemetrii hello grupy operacji (na przykład "GET głównej/Index"). Ta właściwość kontekst jest używany tooanswer, które pytania, takich jak "co to są hello wyjątków typowe zgłaszanych na tej stronie."

Maksymalna długość: 1024


##<a name="synthetic-source-of-hello-operation"></a>Syntetyczne źródło hello operacji

Nazwa źródła syntetycznych. Niektóre dane telemetryczne z aplikacji hello może reprezentować ruchu syntetycznego. Może być witryny sieci web hello indeksowania przez przeszukiwarkę sieci web, testy dostępności lokacji lub śladów z diagnostycznych bibliotek, takich jak Insights zestaw SDK usługi Application sam.

Maksymalna długość: 1024


##<a name="session-id"></a>Identyfikator sesji

Identyfikator sesji - hello wystąpienia użytkownika hello interakcji z aplikacją hello. Informacje w polach kontekstu sesji hello jest zawsze o hello użytkownika końcowego. Po wysłaniu danych telemetrycznych z usługi kontekstu sesji hello jest o hello użytkownika, który zainicjował operację hello hello usługi.

Maksymalna długość: 64


##<a name="anonymous-user-id"></a>Identyfikator użytkownika anonimowego

Identyfikator użytkownika anonimowego. Reprezentuje użytkownika końcowego hello aplikacji hello. Po wysłaniu danych telemetrycznych z usługi kontekstu użytkownika hello jest o hello użytkownika, który zainicjował operację hello hello usługi.

[Próbkowanie](app-insights-sampling.md) jest jednym z hello techniki toominimize hello ilość zbieranych danych telemetrycznych. Próbkowanie tooeither prób algorytm próbki przychodzący lub wychodzący wszystkich hello skorelowane telemetrii. Identyfikator użytkownika anonimowego jest używana do próbkowania generowania oceny. Dlatego użytkownik anonimowy identyfikator powinien być wystarczająco losowych wartości. 

Przy użyciu nazwy użytkownika toostore identyfikatora użytkownika anonimowego jest nieprawidłowe użycie pola hello. Za pomocą identyfikatora użytkownika uwierzytelnione.

Maksymalna długość: 128


##<a name="authenticated-user-id"></a>Identyfikator użytkownika uwierzytelnionego

Identyfikator uwierzytelnionego użytkownika. Witaj przeciwne identyfikatora użytkownika anonimowego, to pole reprezentuje użytkownika hello o przyjaznej nazwie. Od momentu jego osobowe go nie są zbierane domyślnie przez większość zestaw SDK.

Maksymalna długość: 1024


##<a name="account-id"></a>Identyfikator konta

W aplikacjach wielodostępnej jest identyfikator konta hello lub nazwę użytkownika, który hello działa z. Przykładami mogą być identyfikator subskrypcji platformy Azure portalu lub blogu nazwa obsługi blogów.

Maksymalna długość: 1024


##<a name="cloud-role"></a>Rola w chmurze

Nazwa aplikacji hello roli hello jest częścią. Mapuje bezpośrednio toohello nazwy roli na platformie azure. Może być również używane toodistinguish micro usług, które są częścią pojedynczej aplikacji.

Maksymalna długość: 256


##<a name="cloud-role-instance"></a>Wystąpienie roli w chmurze

Nazwa wystąpienia hello, w którym jest uruchomiona aplikacja hello. Nazwa komputera lokalnego, aby uzyskać nazwę wystąpienia dla platformy Azure.

Maksymalna długość: 256


##<a name="internal-sdk-version"></a>Wewnętrzne: Wersja zestawu SDK

Wersja zestawu SDK. Zobacz https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification informacji.

Maksymalna długość: 64


##<a name="internal-node-name"></a>Wewnętrzne: Nazwa węzła

To pole reprezentuje nazwę węzła hello używana do celów rozliczeń. Użyj toooverride hello standardowe wykrywanie węzłów.

Maksymalna długość: 256


## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak za[rozszerzanie i filtrować dane telemetryczne](app-insights-api-filtering-sampling.md).
- Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.
- Zapoznaj się z kolekcji właściwości kontekstu standardowe [konfiguracji](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).
