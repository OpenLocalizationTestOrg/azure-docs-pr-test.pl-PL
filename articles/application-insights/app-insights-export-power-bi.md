---
title: "aaaExport tooPower BI z usługi Application Insights | Dokumentacja firmy Microsoft"
description: "Zapytania analityczne mogą być wyświetlane w usłudze Power BI."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a>Źródła danych usługi Power BI z usługi Application Insights
[Power BI](http://www.powerbi.com/) jest pakiet narzędzia do analizy biznesowe, które ułatwiają analizowanie danych i udostępniać informacji. Pulpity nawigacyjne sformatowanego są dostępne na każdym urządzeniu. Można połączyć dane z wielu źródeł, takich jak analiza zapytania z [Azure Application Insights](app-insights-overview.md).

Istnieją trzy metody zalecane eksportowania tooPower dane usługi Application Insights BI. Można ich używać oddzielnie lub razem.

* [**Power BI karty** ](#power-pi-adapter) — skonfiguruj Tworzenie pulpitu nawigacyjnego dane telemetryczne z aplikacji. wstępnie zdefiniowane Hello zbiór wykresy, ale można dodać własne zapytania z innych źródeł.
* [**Eksportuj zapytania analityczne** ](#export-analytics-queries) -pisać zapytania przy użyciu analizy, a następnie wyeksportować go tooPower BI. To zapytanie można umieścić na pulpicie nawigacyjnym, wraz z innymi danymi.
* [**Eksport ciągły i analiza strumienia** ](app-insights-export-stream-analytics.md) -się proces ten obejmuje więcej tooset pracy. Jest on przydatny, gdy chcesz tookeep dane przez dłuższy czas. W przeciwnym razie hello inne metody są zalecane.

## <a name="power-bi-adapter"></a>Power BI karty
Ta metoda tworzy pełne pulpitu nawigacyjnego dane telemetryczne dla Ciebie. wstępnie zdefiniowane Hello początkowego zestawu danych, ale można dodać więcej tooit danych.

### <a name="get-hello-adapter"></a>Pobierz hello karty
1. Zaloguj się za[usługi Power BI](https://app.powerbi.com/).
2. Otwórz **Pobierz dane**, **usług**, **usługi Application Insights**
   
    ![Pobierz ze źródła danych usługi Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. Podaj szczegóły hello zasobu usługi Application Insights.
   
    ![Pobierz ze źródła danych usługi Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. Zaczekaj minutę lub dwie na toobe danych hello zaimportowane.
   
    ![Power BI karty](./media/app-insights-export-power-bi/010.png)

Można edytować hello pulpitu nawigacyjnego, łączenie hello usługi Application Insights wykresów z systemami innych źródeł oraz z zapytaniami Analytics. Brak galerii wizualizacji, gdzie uzyskasz więcej wykresów, a każdy wykres ma parametry, które można ustawić.

Po początkowej importu hello, hello pulpitu nawigacyjnego i raportów hello nadal tooupdate codziennie. Można kontrolować harmonogram odświeżania hello na powitania zestawu danych.

## <a name="export-analytics-queries"></a>Zapytania analityczne eksportu
Trasa ta umożliwia toowrite żadnych Analytics chcesz zbadać, a następnie wyeksportować tego pulpitu nawigacyjnego usługi Power BI tooa. (Dodaj pulpit nawigacyjny toohello utworzone przez kartę hello).

### <a name="one-time-install-power-bi-desktop"></a>Jeden raz: Zainstaluj Power BI Desktop
tooimport kwerenda usługi Application Insights, użyj hello pulpitu wersja aplikacji Power BI. Ale następnie można opublikować toohello sieci web lub tooyour roboczym chmury usługi Power BI. 

Zainstaluj [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).

### <a name="export-an-analytics-query"></a>Eksportuj zapytania analityka
1. [Otwórz Analytics i zapisać zapytanie](app-insights-analytics-tour.md).
2. Testowanie i kwerendzie hello dopóki zakończeniu modyfikowania hello wyników.

   **Upewnij się, kwerendy hello działa prawidłowo w module analiz przed go wyeksportować.**
3. Na powitania **wyeksportować** menu, wybierz **Power BI (M)**. Zapisz plik tekstowy hello.
   
    ![Eksportuj zapytania usługi Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. Wybierz Power BI Desktop w **pobieranie danych, pustą zapytania** , a następnie w hello zapytania edytora, w obszarze **widoku** wybierz **zaawansowany Edytor zapytań**.

    Wklej hello wyeksportowane M język skryptu do hello zaawansowany Edytor zapytań.

    ![Edytor zaawansowanych zapytań](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. Konieczne może być tooprovide poświadczenia tooallow usługi Power BI tooaccess Azure. Użyj toosign "konta organizacyjnego" przy użyciu swojego konta Microsoft.
   
    ![Podaj poświadczenia Azure tooenable usługi Power BI toorun kwerenda usługi Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    (Tooverify hello poświadczeń, należy użyć hello ustawienia źródła danych menu polecenia hello edytora zapytań. Zwróć uwagę na to toospecify hello poświadczeń, których można użyć dla platformy Azure, która może być inny niż poświadczenia dla usługi Power BI.)
2. Wybierz wizualizacji zapytania i wybierz pola hello osi x, y i podzielenie wymiaru.
   
    ![Wybierz wizualizację](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. Opublikuj obszar roboczy chmury raportu tooyour usługi Power BI. Z tego miejsca można osadzić zsynchronizowanej wersji do innych stron sieci web.
   
    ![Wybierz wizualizację](./media/app-insights-export-power-bi/publish-power-bi.png)
4. Ręcznie odświeżyć raport hello w odstępach czasu, lub skonfigurowania zaplanowanego odświeżania na stronie Opcje hello.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="401-or-403-unauthorized"></a>401 lub 403 bez autoryzacji 
Może to nastąpić, jeśli refesh token nie został zaktualizowany. Spróbuj tooensure te kroki, nadal mieć dostęp. Jeśli masz dostęp, a poświadczenia hello refershing nie działa, otwórz bilet pomocy technicznej.

1. Zaloguj się do portalu Azure hello i upewnij się, że można uzyskać dostępu do zasobów hello
2. Spróbuj toorefresh poświadczenia hello hello pulpitu nawigacyjnego

### <a name="502-bad-gateway"></a>502 Niewłaściwa brama
Jest to zazwyczaj spowodowane Analytics kwerendę, która zwraca za dużo danych. Spróbuj użyć przy użyciu mniejszego zakresu czasu lub za pomocą hello [temu](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) lub [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) działa tylko [projektu](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello potrzebne pola.

Jeśli zmniejszenie hello zestawu danych pochodzących z hello Analytics query nie spełnia wymagań należy rozważyć użycie hello [interfejsu API](https://dev.applicationinsights.io/documentation/overview) toopull większy zestaw danych. Poniżej przedstawiono instrukcje eksportowania hello tooconvert M zapytania hello toouse interfejsu API.

1. Utwórz [klucz interfejsu API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)
2. Adres URL ARM z interfejsem API AI hello hello aktualizacji skryptu Power BI M, wyeksportowany z usługi Analytics zastępując (zobacz poniższy przykład)
   * Zastąp **https://management.azure.com/subscriptions/...**
   * **https://api.applicationinsights.io/beta/apps/...**
3. Na koniec Zaktualizuj poświadczenia toobasic i korzystania z klucza interfejsu API
  

**Istniejący skrypt**
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
**Zaktualizowany skrypt**
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a>O pobierania próbek
Jeśli aplikacja wyśle dużą ilość danych, funkcja adaptacyjną próbkowania hello może działać i wysłać określonego odsetka telemetrii. Witaj, które same ma wartość true, jeśli ręcznie ustawiono próbkowania hello zestawu SDK lub na wprowadzanie. [Dowiedz się więcej na temat próbkowania.](app-insights-sampling.md)


## <a name="next-steps"></a>Następne kroki
* [Power BI — informacje](http://www.powerbi.com/learning/)
* [Samouczek analityka](app-insights-analytics-tour.md)

