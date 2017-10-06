---
title: "Eksportowanie tooSQL z usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Stale wyeksportować za pomocą usługi Stream Analytics tooSQL dane usługi Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a>Wskazówki: Eksportowanie tooSQL z usługi Application Insights przy użyciu usługi analiza strumienia
W tym artykule przedstawiono sposób toomove dane telemetryczne z [Azure Application Insights] [ start] do bazy danych Azure SQL za pomocą [eksportu ciągłego] [ export] i [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). 

Eksport ciągły przenosi dane telemetryczne do usługi Azure Storage w formacie JSON. Firma Microsoft będzie analizować hello obiektów JSON przy użyciu usługi Azure Stream Analytics i utworzyć wiersze w tabeli bazy danych.

(Eksportu ciągłego jest ogólnie rzecz biorąc, toodo sposób hello analizy hello dane telemetryczne aplikacji wysyłania tooApplication szczegółowych informacji. Można dostosować ten kod przykładowy toodo innymi z hello wyeksportowane dane telemetryczne, takich jak agregacji danych.)

Zaczniemy założeń hello już aplikacji hello ma toomonitor.

W tym przykładzie użyjemy hello strony widoku danych, ale hello tego samego wzorca można z łatwością rozszerzyć tooother typów danych, takich jak niestandardowe zdarzenia i wyjątki. 

## <a name="add-application-insights-tooyour-application"></a>Dodawanie usługi Application Insights tooyour aplikacji
Rozpoczęto tooget:

1. [Skonfiguruj usługę Application Insights dla stron sieci web](app-insights-javascript.md). 
   
    (W tym przykładzie firma Microsoft będzie skupić się na przetwarzanie danych widoku strony z powitania klienta przeglądarki, ale można również skonfigurować usługi Application Insights po stronie serwera na powitania z Twojej [Java](app-insights-java-get-started.md) lub [ASP.NET](app-insights-asp-net.md) żądania aplikacji i procesów zależności i inne dane telemetryczne serwera.)
2. Publikowanie aplikacji i obserwować dane telemetryczne w zasobu usługi Application Insights.

## <a name="create-storage-in-azure"></a>Tworzenie magazynu na platformie Azure
Eksport ciągły zawsze generuje konto magazynu Azure tooan danych, więc najpierw należy toocreate hello magazynu.

1. Utwórz konto magazynu w ramach subskrypcji w hello [portalu Azure][portal].
   
    ![W portalu Azure wybierz nowy, danych, magazynu. Zaznacz klasycznym, wybierz polecenie Utwórz. Podaj nazwę magazynu.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. Tworzenie kontenera
   
    ![W hello nowego magazynu wybierz kontenery, kliknij Kafelek kontenery hello, a następnie dodaj](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. Skopiuj klucz dostępu do magazynu hello
   
    Będzie on potrzebny wkrótce tooset się usługa analiza strumienia wejściowego toohello hello.
   
    ![W magazynie hello Otwórz ustawienia kluczy i kopiować hello podstawowy klucz dostępu](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a>Uruchom magazynu tooAzure eksportu ciągłego
1. W hello portalu Azure Przejdź zasobu usługi Application Insights toohello utworzone dla aplikacji.
   
    ![Kliknij przycisk Przeglądaj, usługi Application Insights aplikacji](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. Utwórz eksport ciągły.
   
    ![Wybierz ustawienia, Eksport ciągły](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    Wybierz utworzone wcześniej konto magazynu hello:

    ![Ustaw miejsce docelowe hello eksportu](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    Ustaw hello typy zdarzeń, które mają toosee:

    ![Wybierz typy zdarzeń](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. Let niektóre dane gromadzone. Zaczekaj i innym użytkownikom za pomocą aplikacji przez pewien czas. Dane telemetryczne wejdzie i zobaczysz statystyczne wykresów w [Eksploratora metryk](app-insights-metrics-explorer.md) i zdarzeń z [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md). 
   
    I ponadto hello danych będzie eksportować tooyour magazynu. 
2. Sprawdź hello wyeksportowane dane, albo w portalu hello — wybierz **Przeglądaj**, wybierz konto magazynu, a następnie **kontenery** — lub w programie Visual Studio. W programie Visual Studio, wybierz **wyświetlić / w chmurze Explorer**i otwórz Azure / magazynu. (Jeśli nie mają tej opcji menu, należy tooinstall hello Azure SDK: Otwórz okno dialogowe Nowy projekt hello a Visual C# / w chmurze / Get Microsoft Azure SDK dla platformy .NET.)
   
    ![W programie Visual Studio Otwórz przeglądarkę serwera, Azure, Magazyn](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    Zanotuj hello wspólnej część nazwy ścieżki hello, która jest pochodną klucz nazwy i instrumentacji aplikacji hello. 

Witaj zdarzenia są zapisywane pliki tooblob w formacie JSON. Każdy plik może zawierać co najmniej jednego zdarzenia. Dlatego chcemy dane zdarzeń hello tooread i Filtruj limit pól hello, którą chcemy udostępnić. Wszystkie rodzaje czynności, które firma Microsoft może wykonywać hello danych, ale naszego planu obecnie jest toouse Stream Analytics toomove hello danych tooa bazy danych SQL. Który ułatwi partii łatwe toorun interesujące zapytań.

## <a name="create-an-azure-sql-database"></a>Utwórz bazę danych Azure SQL
Ponownie od subskrypcji w [portalu Azure][portal], Utwórz bazę danych hello (i nowy serwer, chyba że masz już jeden) toowhich przedstawiono tworzenie hello danych.

![Nowe dane, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

Upewnij się, że tego serwera bazy danych hello zezwala na dostęp tooAzure usług:

![Przeglądaj, serwery, serwera, ustawień, zapory, tooAzure Zezwalaj na dostęp](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a>Utwórz tabelę w bazie danych SQL Azure
Połączenia bazy danych toohello utworzony w poprzedniej sekcji hello z narzędzia do zarządzania preferowany. W ramach tego przewodnika użyjemy [narzędzia do zarządzania serwerem SQL](https://msdn.microsoft.com/ms174173.aspx) (SSMS).

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

Utwórz nowe zapytanie i wykonaj powitania po T-SQL:

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

W tym przykładzie użyto dane wyświetleń strony. toosee hello innych dostępnych danych, sprawdź dane wyjściowe JSON i zobaczyć hello [wyeksportować modelu danych](app-insights-export-data-model.md).

## <a name="create-an-azure-stream-analytics-instance"></a>Utwórz wystąpienie usługi Azure Stream Analytics
Z hello [klasycznego portalu Azure](https://manage.windowsazure.com/), wybierz usługę Azure Stream Analytics hello i utworzyć nowe zadanie usługi Stream Analytics:

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

Podczas tworzenia nowego zadania hello rozwiń jego szczegóły:

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a>Ustawianie lokalizacji obiektu blob
Ustaw wprowadzania tootake z obiektu blob z eksportu ciągłego:

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

Teraz musisz hello podstawowy klucz dostępu z konta magazynu, który wcześniej zapisany. Ustaw jako hello klucz konta magazynu.

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a>Wzorzec prefiksu ścieżki zestawu
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

Jest zbyt hello tooset się, że Format daty**RRRR-MM-DD** (z **łączniki**).

Witaj wzorzec prefiksu ścieżki Określa sposób odnajdowania usługi Stream Analytics plików wejściowych hello w magazynie hello. Należy tooset on toohow toocorrespond eksportu ciągłego przechowuje dane hello. Ustaw go następująco:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

W tym przykładzie:

* `webapplication27`to nazwa hello hello zasobu usługi Application Insights **w przypadku małych**. 
* `1234...`jest klucz Instrumentacji hello hello zasobu usługi Application Insights **z kreskami usunięte**. 
* `PageViews`Typ hello danych chcemy tooanalyze. dostępne typy Hello są zależne od filtru hello, ustawionych w eksportu ciągłego. Sprawdź hello wyeksportowane dane toosee hello innych dostępnych typów i zobacz hello [wyeksportować modelu danych](app-insights-export-data-model.md).
* `/{date}/{time}`wzorzec są zapisywane jako literału.

Nazwa hello tooget iKey zasobu usługi Application Insights, otwórz Essentials na stronie Przegląd i Otwórz ustawienia.

#### <a name="finish-initial-setup"></a>Zakończ początkowej konfiguracji
Upewnij się, format serializacji hello:

![Potwierdź i zamknąć kreatora](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

Zamknij kreatora hello i poczekaj, aż hello toocomplete Instalatora.

> [!TIP]
> Użyj toocheck funkcja próbki hello poprawnie ustawiona ścieżka wejściowa hello. Jeśli działanie nie powiodło się: Sprawdź, czy dane w magazynie hello zakresu czasu próbki hello została wybrana opcja. Dokonaj edycji definicji wejściowych hello i sprawdź Ustaw hello konta magazynu, ścieżkę prefiks i Data formacie poprawnie.
> 
> 

## <a name="set-query"></a>Zapytanie zestawu
Otwórz sekcję zapytania hello:

![Analiza strumienia wybierz zapytanie](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

Zastąp hello domyślne zapytanie z:

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

Należy zauważyć, że najpierw hello kilka właściwości są toopage określonych danych widoku. Eksporty inne typy telemetrii ma inne właściwości. Zobacz hello [szczegółowe odwołania do modelu danych dla hello typy właściwości i wartości.](app-insights-export-data-model.md)

## <a name="set-up-output-toodatabase"></a>Konfigurowanie toodatabase danych wyjściowych
Wybierz SQL jako dane wyjściowe hello.

![Analiza strumienia wybierz dane wyjściowe](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

Określ bazę danych SQL hello.

![Uzupełnij informacje dotyczące hello bazy danych](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

Zamknij kreatora hello i poczekaj, aż powiadomienie, które skonfigurowano hello danych wyjściowych.

## <a name="start-processing"></a>Rozpocznij przetwarzanie
Uruchom zadanie hello z hello pasku akcji:

![W module analiz strumienia kliknij przycisk Start](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

Można wybrać, czy przetwarzanie toostart hello danych od teraz lub toostart z wcześniejszych danych. ostatnie Hello jest przydatne, jeśli masz już uruchomione na chwilę eksportu ciągłego.

![W module analiz strumienia kliknij przycisk Start](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

Po kilku minutach Przejdź wstecz tooSQL narzędzia do zarządzania serwerem i obejrzyj hello przepływu danych, w. Na przykład użyć zapytania następująco:

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a>Pokrewne artykuły:
* [Eksportuj tooPowerBI przy użyciu usługi analiza strumienia](app-insights-export-power-bi.md)
* [Szczegółowe dane modelu odwołania dla hello typy właściwości i wartości.](app-insights-export-data-model.md)
* [Eksport ciągły w usłudze Application Insights](app-insights-export-telemetry.md)
* [Usługa Application Insights](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

