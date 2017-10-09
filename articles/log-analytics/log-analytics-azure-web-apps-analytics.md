---
title: aaaView dane analityczne Azure Web Apps | Dokumentacja firmy Microsoft
description: "Zbierać metryki różnych różnych zasobów aplikacji sieci Web platformy Azure, można użyć hello Azure Web Apps Analytics rozwiązania toogain insights dotyczących aplikacji sieci Web platformy Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 20ff337f-b1a3-4696-9b5a-d39727a94220
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: banders
ms.openlocfilehash: 7e9725f95c9faf01da89184975ad5444dd19ff95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-analytic-data-for-metrics-across-all-your-azure-web-app-resources"></a>Wyświetl dane analityczne metryki różnych zasobów aplikacji sieci Web Azure

![Symbol aplikacji sieci Web](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)  
Hello rozwiązania analizy aplikacji sieci Web platformy Azure (wersja zapoznawcza) zapewnia wgląd w Twoje [Azure Web Apps](../app-service-web/app-service-web-overview.md) przez zbieranie metryk różnych różnych zasobów aplikacji sieci Web platformy Azure. Z rozwiązaniem hello można analizować i wyszukiwać dane metryki zasobów aplikacji sieci web.

Za pomocą rozwiązania hello, można wyświetlić:

- Górny aplikacje sieci Web z hello najwyższy czas odpowiedzi
- Liczba żądań w aplikacji sieci Web, włącznie z żądaniami udane i nieudane
- Górny aplikacje sieci Web z najwyższym ruchu przychodzącego i wychodzącego
- Plany usługi TOP z wysokie użycie procesora CPU i pamięci
- Operacje dziennika aktywności aplikacji sieci Web platformy Azure

## <a name="connected-sources"></a>Połączone źródła

W przeciwieństwie do większości innych rozwiązań analizy dzienników danych nie jest zbieranych dla aplikacji sieci Web Azure przez agentów. Wszystkie dane używane przez rozwiązanie hello pochodzi bezpośrednio z platformy Azure.

| Połączone źródło | Obsługiwane | Opis |
| --- | --- | --- |
| [Agenci dla systemu Windows](log-analytics-windows-agents.md) | Nie | rozwiązanie Hello nie zbiera informacje z agentów systemu Windows. |
| [Agenci dla systemu Linux](log-analytics-linux-agents.md) | Nie | rozwiązanie Hello nie zbiera informacje z agentów systemu Linux. |
| [Grupa zarządzania programu SCOM](log-analytics-om-agents.md) | Nie | rozwiązanie Hello nie zbiera informacje z agentów w podłączonej grupy zarządzania SCOM. |
| [Konto usługi Azure Storage](log-analytics-azure-storage.md) | Nie | rozwiązanie Hello nie nie zbierają informacje z usługi Azure storage. |

## <a name="prerequisites"></a>Wymagania wstępne

- tooaccess informacje dotyczące pomiaru zasobów w aplikacji sieci Web platformy Azure, musi mieć subskrypcję platformy Azure.

## <a name="configuration"></a>Konfiguracja

Wykonaj następujące kroki tooconfigure hello Azure Web Apps analizy rozwiązania dla obszarów roboczych hello.

1. Włącz hello Azure Web Apps Analytics rozwiązania z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).
2. [Włącz tooOMS rejestrowania metryki zasobów platformy Azure przy użyciu programu PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

Witaj rozwiązania analizy aplikacji sieci Web Azure zbiera dwóch zestawów metryki z platformy Azure:

- Metryki aplikacji sieci Web platformy Azure
  - Pamięć średni zestaw roboczy
  - Średni czas odpowiedzi
  - Odebrano wysłane bajty
  - Czas procesora CPU
  - Żądania
  - Zestaw roboczy pamięci
  - Httpxxx
- Metryki planu usługi aplikacji
  - Odebrano wysłane bajty
  - Procent użycia procesora CPU
  - Długość kolejki dysku
  - Długość kolejki http
  - Procent pamięci

Metryki planu usługi aplikacji są zbierane tylko, jeśli używasz planu dedykowanych usługi. To nie ma zastosowania toofree lub udostępnionego planów usługi aplikacji.

Jeśli dodasz hello rozwiązania przy użyciu portalu OMS hello, zostanie wyświetlone następujące hello kafelka. Należy zbyt[włączyć tooOMS rejestrowania metryki zasobów platformy Azure przy użyciu programu PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

![Zostanie wykonana oceny powiadomień](./media/log-analytics-azure-web-apps-analytics/performing-assessment.png)

Po skonfigurowaniu rozwiązania hello danych powinien rozpocząć przepływu roboczego tooyour w ciągu 15 minut.

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello

Po dodaniu hello Azure Web Apps Analytics rozwiązania tooyour roboczym hello **Analytics aplikacji sieci Web Azure** kafelka dodaniu tooyour pulpitu nawigacyjnego przeglądu. Ten Kafelek jest wyświetlana liczba Liczba hello Azure Web Apps, że rozwiązanie hello ma tooin dostępu do Twojej subskrypcji platformy Azure.

![Kafelek Analytics aplikacji sieci Web platformy Azure](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-tile.png)

### <a name="view-azure-web-apps-analytics-information"></a>Wyświetlanie informacji o Analytics aplikacji sieci Web Azure

Kliknij hello **Analytics aplikacji sieci Web Azure** hello tooopen kafelka **Analytics aplikacji sieci Web Azure** pulpitu nawigacyjnego. pulpit nawigacyjny Hello zawiera bloki hello hello w poniższej tabeli. Każdy blok wyświetla się tooten elementów pasujących do kryteriów w bloku hello określenia zakresu zakresu i czasu. Można uruchomić wyszukiwania dziennika, który zwraca wszystkie rekordy, klikając **zobaczyć wszystkie** u dołu hello bloku hello lub przez kliknięcie nagłówka bloku hello.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| Kolumna | Opis |
| --- | --- |
| Używanie usługi Azure |   |
| Trendy żądania aplikacji sieci Web | Przedstawia wykres hello trend żądania aplikacji sieci Web dla zakresu dat hello wybranego wiersza i pokazuje listę hello Najczęstsze żądania dziesięć sieci web. Kliknij przycisk wyszukiwania dziennika hello wiersza wykresu toorun<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code> <br>Kliknij przycisk wyszukiwania dziennika hello sieci web żądania metryki trend żądanie toorun elementu żądania sieci web. |
| Czas odpowiedzi aplikacji sieci Web | Przedstawia wykres liniowy hello czas odpowiedzi aplikacji sieci Web dla hello zakres dat, które zostały wybrane. Również pokazuje listę listę hello top Web dziesięć odpowiedzi aplikacji czasu. Kliknij przycisk wyszukiwania dziennika hello toorun wykresu<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code><br> Polecenie toorun aplikacji sieci Web wyszukiwania dziennika, zwracając czas odpowiedzi dla hello aplikacji sieci Web. |
| Ruch w aplikacji sieci Web | Przedstawia wykres liniowy dla ruchu aplikacje sieci Web w MB i list top hello ruchu aplikacji sieci Web. Kliknij przycisk wyszukiwania dziennika hello toorun wykresu<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code><br> Wszystkie aplikacje sieci Web z ruchem będzie wyświetlana dla hello ostatniej minuty. Kliknij przycisk toorun aplikacji sieci Web, dziennik wyszukiwania przedstawiający bajtów odebranych i wysłanych do hello aplikacji sieci Web. |
| Plany usługi aplikacji Azure |   |
| Planów usługi App Service z procesora &gt; 80% | Pokazuje hello łączna liczba plany usługi App Service, który ma użycie procesora CPU przekracza 80% i listy hello planów usługi aplikacji 10 pierwszych według użycia Procesora. Kliknij przycisk toorun całkowity obszar hello dziennik wyszukiwania<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code><br> Będzie wyświetlana lista planów usługi aplikacji i ich średnie wykorzystanie procesora CPU. Kliknij przycisk wyszukiwania dziennika przedstawiający jego średnie wykorzystanie procesora CPU toorun planu usługi App Service. |
| Planów usługi App Service z wykorzystanie pamięci &gt; 80% | Pokazuje hello łączna liczba plany usługi App Service, który ma użycie pamięci jest większa niż 80% i listy hello planów usługi aplikacji 10 pierwszych przez użycie pamięci. Kliknij przycisk toorun całkowity obszar hello dziennik wyszukiwania<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code><br> Będzie wyświetlana lista planów usługi aplikacji i ich średnie wykorzystanie pamięci. Kliknij przycisk wyszukiwania dziennika przedstawiający jego średnie wykorzystanie pamięci toorun planu usługi App Service. |
| Dzienniki aktywności aplikacji sieci Web platformy Azure |   |
| Inspekcji działania aplikacji sieci Web platformy Azure | Pokazuje hello całkowita liczba aplikacji sieci Web za pomocą [Dzienniki aktywności](log-analytics-activity.md) i list hello 10 pierwszych działania dziennika operacji. Kliknij przycisk toorun całkowity obszar hello dziennik wyszukiwania<code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code><br> Go to lista hello operacje tworzenia dzienników działania. Kliknij działanie dziennika operacji toorun wyszukiwania dziennika, która wyświetla rekordy hello hello operacji. |



### <a name="azure-web-apps"></a>Azure Web Apps

Na pulpicie nawigacyjnym hello użytkownik może przejść do szczegółów tooget uzyskać lepszy wgląd w Twoje metryki aplikacji sieci Web. Ten pierwszy zestaw bloków Pokaż trend hello hello żądań aplikacji sieci Web, liczbę błędów (na przykład HTTP404), ruchu i Średni czas odpowiedzi w czasie. Przedstawiono również podział te metryki dla różnych aplikacji sieci Web.

![Azure używanie bloków](./media/log-analytics-azure-web-apps-analytics/web-apps-dash01.png)

Główną przyczyną pokazujący, że dane są tak, aby można zidentyfikować aplikacji sieci Web z czasem odpowiedzi wysokiej i Znajdź toofind hello główną przyczynę. Próg limitu jest również zastosowane toohelp użytkownik, który więcej łatwo zidentyfikować hello takich, które mają problemy.

- Aplikacje sieci Web zaznaczone na czerwono mają wyższe niż 1 sekunda czas odpowiedzi.
- Wyświetlane w kolorze pomarańczowym aplikacji sieci Web mają wyższe niż 0,7 sekundę i mniejsza niż 1 sekunda czas odpowiedzi.
- Aplikacje sieci Web wyświetlany na zielono mieć drugi poniżej 0,7 czas odpowiedzi.

Hello po dziennik wyszukiwania przykład obrazu, zawiera ten hello *anugup3* aplikacji sieci web ma czas reakcji znacznie wyższa niż hello innych aplikacji sieci web.

![Przykład wyszukiwania dziennika](./media/log-analytics-azure-web-apps-analytics/web-app-search-example.png)

### <a name="app-service-plans"></a>Plany usługi App Service

Jeśli korzystasz z dedykowanym plany usługi, może również zbierać metryki dla planów usługi aplikacji. W tym widoku, zostanie wyświetlony, Twoje plany usługi App Service z wysokie użycie procesora CPU lub pamięci (&gt; 80%). Przedstawia on także hello top aplikacji usługi z wysokie użycie pamięci lub zasobów Procesora. Podobnie próg limitu jest zastosowane toohelp użytkownik, który więcej łatwo zidentyfikować hello takich, które mają problemy.

- Plany usługi App Service zaznaczone na czerwono mają wyższe niż 80% wykorzystania Procesora/pamięci.
- Wyświetlane w kolorze pomarańczowym planów usługi App Service ma wykorzystanie Procesora/pamięci, wyższy niż 60%, a mniejszy niż 80%.
- Plany usługi App Service wyświetlany na zielono ma mniej niż 60% wykorzystania Procesora/pamięci.

![Bloki planów usługi aplikacji Azure](./media/log-analytics-azure-web-apps-analytics/web-apps-dash02.png)

## <a name="azure-web-apps-log-searches"></a>Azure wyszukiwania dzienników aplikacji sieci Web

Witaj **listy z popularnych Azure Web Apps zapytania wyszukiwania** pokazuje hello wszystkie powiązane Dzienniki aktywności dla aplikacji sieci Web, która zapewnia wgląd w działania hello, wykonywane na zasobów aplikacji sieci Web. Wyświetla również wszystkie hello dotyczące operacji i hello liczba ich wystąpienia.

Przy użyciu dowolnego zapytania wyszukiwania dziennika hello jako punkt początkowy, możesz łatwo utworzyć alertu. Na przykład może być toocreate alert, gdy metryki Średni czas odpowiedzi jest większy niż co 1 s.

## <a name="next-steps"></a>Następne kroki

- Utwórz [alert](log-analytics-alerts-creating.md) dla określonej metryki.
- Użyj [wyszukiwania dziennika](log-analytics-log-searches.md) tooview szczegółowych informacji z dzienników działania.
