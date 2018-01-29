---
title: Azure Service Bus metryki w monitorze Azure (wersja zapoznawcza) | Dokumentacja firmy Microsoft
description: "Użyj monitorowania Azure, aby monitorować jednostek usługi Service Bus"
services: service-bus-messaging
documentationcenter: .NET
author: christianwolf42
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/19/2017
ms.author: sethm
ms.openlocfilehash: fcc7e1cbacc7889c9525207b238162e6caa6b00b
ms.sourcegitcommit: 4ed3fe11c138eeed19aef0315a4f470f447eac0c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/23/2017
---
# <a name="azure-service-bus-metrics-in-azure-monitor-preview"></a>Azure Service Bus metryki w monitorze Azure (wersja zapoznawcza)

Metryki usługi Service Bus zapewnia stanu zasobów w Twojej subskrypcji platformy Azure. Ze bogatym zestawem danych metryki można ocenić ogólną kondycję zasobów usługi Service Bus, nie tylko na poziomie przestrzeni nazw, ale na poziomie jednostki. Te statystyki może być istotne, ponieważ ich ułatwiają monitorowanie stanu usługi Service Bus. Metryki może również pomóc rozwiązać głównej przyczyny problemów bez konieczności skontaktuj się z pomocą techniczną platformy Azure.

Azure Monitor udostępnia interfejsy użytkownika ujednoliconego do monitorowania na różne usługi platformy Azure. Aby uzyskać więcej informacji, zobacz [monitorowania na platformie Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview.md) i [metryki pobrać Monitor Azure z platformą .NET](https://github.com/Azure-Samples/monitor-dotnet-metrics-api) w witrynie GitHub.

## <a name="access-metrics"></a>Metryki dostępu

Azure Monitor oferuje wiele sposobów metryki dostępu. Można albo metryki dostęp za pośrednictwem [portalu Azure](https://portal.azure.com), lub użyj interfejsów API usługi Azure monitora (REST i .NET) i rozwiązań analitycznych, takie jak operacji Management Suite i usługi Event Hubs. Aby uzyskać więcej informacji, zobacz [metryki Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-metrics.md#access-metrics-via-the-rest-api).

Metryki są domyślnie włączone i są dostępne najnowsze w ciągu 30 dni od danych. Jeśli chcesz zachować dane przez dłuższy okres czasu, można archiwizować dane metryk do konta usługi Azure Storage. Te ustawienia zostaną skonfigurowane w [ustawień diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) w monitorze Azure.

## <a name="access-metrics-in-the-portal"></a>Metryki dostępu w portalu

Można monitorować metryk w czasie, [portalu Azure](https://portal.azure.com). Poniższy przykład przedstawia sposób wyświetlania pomyślnych żądań i żądań przychodzących na poziomie konta:

![][1]

Dostępne metryki bezpośrednio za pomocą przestrzeni nazw. Aby to zrobić, wybierz obszar nazw, a następnie kliknij przycisk **metryki (Peview)**. Aby wyświetlić metryki filtrowane do zakresu jednostki, wybierz obiekt, a następnie kliknij przycisk **metryki (wersja zapoznawcza)**.

![][2]

Dla metryki pomocnicze, wymiary możesz filtrować z żądaną wartością.

## <a name="billing"></a>Rozliczenia

Przy użyciu metryk w monitorze Azure jest obecnie bezpłatna podczas w wersji zapoznawczej. Jednak użycie dodatkowe rozwiązania, które pozyskiwania danych metryki, użytkownik może zostać użyta przez te rozwiązania. Na przykład możesz są rozliczane przez usługi Azure Storage archiwizacji danych metryk do konta usługi Azure Storage. Również są rozliczane przez operację Management Suite (OMS), jeśli strumienia danych metryki z usługą OMS dla zaawansowanej analizy.

Następujące metryki zawiera przegląd kondycji usługi. 

> [!NOTE]
> Firma Microsoft są wycofano kilka miar, ponieważ są one przenoszone pod inną nazwą. To może wymagać aktualizacji z odwołania. Metryki oznaczonej jako "przestarzałe" — słowo kluczowe nie będą obsługiwane idąc dalej.

Wszystkie wartości metryki są wysyłane do monitora Azure co minutę. Odstęp czasu określa przedział czasu, dla której przedstawiono wartości metryk. Obsługiwany interwał wszystkie metryki usługi Service Bus to 1 minuta.

## <a name="request-metrics"></a>Metryki żądania

Zlicza żądania operacji danych i zarządzania.

| Nazwa metryki | Opis |
| ------------------- | ----------------- |
| Przychodzące żądania (wersja zapoznawcza) | Liczba żądań wysyłanych do usługi Service Bus w określonym czasie. <br/><br/> Jednostka: liczba <br/> Typ agregacji: Całkowita liczba <br/> Wymiar: Nazwa jednostki|
|Liczba pomyślnych żądań (wersja zapoznawcza)|Liczba pomyślnych żądań wprowadzone w usłudze Service Bus w określonym czasie.<br/><br/> Jednostka: liczba <br/> Typ agregacji: Całkowita liczba <br/> Wymiar: Nazwa jednostki|
|Błędy serwera (wersja zapoznawcza)|Liczba żądań przetworzonych nie z powodu błędu usługi Service Bus w określonym czasie.<br/><br/> Jednostka: liczba <br/> Typ agregacji: Całkowita liczba <br/> Wymiar: Nazwa jednostki|
|Błędy użytkownika (wersja zapoznawcza)|Liczba żądań przetworzonych nie ze względu na błędy użytkowników w określonym czasie.<br/><br/> Jednostka: liczba <br/> Typ agregacji: Całkowita liczba <br/> Wymiar: Nazwa jednostki|
|Ograniczeniem przepustowości żądań (wersja zapoznawcza)|Liczba żądań, które zostały ograniczenie, ponieważ przekroczono użycia.<br/><br/> Jednostka: liczba <br/> Typ agregacji: Całkowita liczba <br/> Wymiar: Nazwa jednostki|

## <a name="message-metrics"></a>Metryki wiadomości

| Nazwa metryki | Opis |
| ------------------- | ----------------- |
|Komunikaty przychodzące (wersja zapoznawcza)|Liczba zdarzeń lub wiadomości wysyłanych do usługi Service Bus w określonym czasie.<br/><br/> Jednostka: liczba <br/> Typ agregacji: Całkowita liczba <br/> Wymiar: Nazwa jednostki|
|Wysyła komunikaty wychodzące (wersja zapoznawcza)|Liczba zdarzeń lub komunikatów odebranych z usługi Service Bus w określonym czasie.<br/><br/> Jednostka: liczba <br/> Typ agregacji: Całkowita liczba <br/> Wymiar: Nazwa jednostki|

## <a name="connection-metrics"></a>Metryki połączenia

| Nazwa metryki | Opis |
| ------------------- | ----------------- |
|ActiveConnections (wersja zapoznawcza)|Liczba aktywnych połączeń przestrzeni nazw, a także jednostki.<br/><br/> Jednostka: liczba <br/> Typ agregacji: Całkowita liczba <br/> Wymiar: Nazwa jednostki|
|Otwartego połączenia (wersja zapoznawcza)|Liczba otwartych połączeń.<br/><br/> Jednostka: liczba <br/> Typ agregacji: Całkowita liczba <br/> Wymiar: Nazwa jednostki|
|Zamknięte połączenia (wersja zapoznawcza)|Liczba połączeń zamknięte.<br/><br/> Jednostka: liczba <br/> Typ agregacji: Całkowita liczba <br/> Wymiar: Nazwa jednostki |

## <a name="resource-usage-metrics"></a>Metryki użycia zasobów

| Nazwa metryki | Opis |
| ------------------- | ----------------- |
|Użycie procesora CPU na przestrzeń nazw (wersja zapoznawcza)|Procent użycia procesora CPU przestrzeni nazw.<br/><br/> Jednostka: procent <br/> Typ agregacji: maksymalna <br/> Wymiar: Nazwa jednostki|
|Użycie rozmiar pamięci na przestrzeń nazw (wersja zapoznawcza)|Procent wykorzystania pamięci przestrzeni nazw.<br/><br/> Jednostka: procent <br/> Typ agregacji: maksymalna <br/> Wymiar: Nazwa jednostki|

## <a name="metrics-dimensions"></a>Wymiary metryk

Usługa Azure Service Bus obsługuje następujące wymiary metryki w monitorze Azure. Dodawanie wymiarów do Twojej metryki jest opcjonalna. Jeśli nie zostaną dodane wymiarów, metryki są określone na poziomie przestrzeni nazw. 

|Nazwa wymiaru|Opis|
| ------------------- | ----------------- |
|Nazwa jednostki| Usługa Service Bus obsługuje jednostek obsługi komunikatów w przestrzeni nazw.|

## <a name="next-steps"></a>Następne kroki

Zobacz [Azure monitorowanie — Przegląd](../monitoring-and-diagnostics/monitoring-overview.md).

[1]: ./media/service-bus-metrics-azure-monitor/service-bus-monitor1.png
[2]: ./media/service-bus-metrics-azure-monitor/service-bus-monitor2.png


