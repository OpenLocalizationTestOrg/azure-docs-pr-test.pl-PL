---
title: "tooPower danych analizy dzienników aaaExport BI | Dokumentacja firmy Microsoft"
description: "Usługa Power BI jest oparte na chmurze usługi analizy biznesowej firmy Microsoft, który udostępnia zaawansowane wizualizacje i raporty do analizy różne zestawy danych.  Analiza dzienników stale wyeksportować dane z repozytorium OMS hello do usługi Power BI, można wykorzystać jej wizualizacje i narzędzia do analizy.  W tym artykule opisano, jak tooconfigure zapytania w programie analizy dzienników, która automatycznie wyeksportować tooPower BI w regularnych odstępach czasu."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a>Eksportuj tooPower danych analizy dzienników analizy Biznesowej

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie tego procesu eksportowania analizy dzienników danych tooPower BI przestanie działać.  Istniejących harmonogramów, które zostały utworzone przed rozpoczęciem uaktualniania zostanie wyłączony. 
>
> Po uaktualnieniu, używa usługi Azure Log Analytics hello tej samej platformy jako usługi Application Insights i używać tego samego procesu tooexport analizy dzienników zapytań tooPower BI jako hello [hello tooexport procesu usługi Application Insights odpytuje tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).  Można wyeksportować albo hello zapytania przy użyciu konsoli analizy hello, zgodnie z opisem w tym artykule, lub wybrać hello **usługi Power BI** przycisk u góry hello hello ekranu w hello dziennik wyszukiwania portalu.



[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) jest oparte na chmurze usługi analizy biznesowej firmy Microsoft, który udostępnia zaawansowane wizualizacje i raporty do analizy różne zestawy danych.  Analiza dzienników można automatycznie eksportować dane z repozytorium OMS hello do usługi Power BI, można wykorzystać jej wizualizacje i narzędzia do analizy.

Po skonfigurowaniu usługi Power BI z analizy dzienników, możesz utworzyć dziennika zapytań, które wyeksportować zestawów danych ich wyniki toocorresponding w usłudze Power BI.  Witaj zapytania i eksportowanie nadal tooautomatically uruchamiane zgodnie z harmonogramem, który definiuje zestaw danych hello tookeep się toodate z hello najnowsze dane zebrane przez analizy dzienników.

![TooPower analizy dziennika analizy Biznesowej](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a>Power BI harmonogramów
A *Power BI harmonogram* obejmuje wyszukiwania dziennika, które eksportuje z hello OMS repozytorium tooa odpowiedniego zestawu danych w usłudze Power BI i harmonogram, który określa, jak często to wyszukiwanie jest uruchamiany tookeep hello zestawu danych bieżącego zestawu danych.

pola Hello w zestawie danych hello będzie odpowiadała właściwości hello hello rekordów zwróconych hello dziennik wyszukiwania.  Jeśli wyszukiwanie hello rekordy różnych typów, a następnie hello zestawu danych będzie zawierać wszystkie hello właściwości każdej z hello uwzględnione typy rekordów.  

> [!NOTE]
> Jest najlepszym toouse praktyki dziennik wyszukiwania zapytanie zwracające dane pierwotne jako min. tooperforming konsolidacji przy użyciu poleceń, takich jak [miary](log-analytics-search-reference.md#measure).  Można wykonywać żadnych agregacji i obliczeń w usłudze Power BI z hello nieprzetworzone dane.
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a>Łączenie tooPower obszar roboczy OMS analizy Biznesowej
Zanim można eksportować z analizy dzienników tooPower analizy Biznesowej, należy połączyć konta usługi Power BI tooyour obszar roboczy OMS za pomocą hello procedury.  

1. W konsoli OMS powitania kliknij hello **ustawienia** kafelka.
2. Wybierz **kont**.
3. W hello **informacje o obszarze roboczym** kliknij sekcję **połączyć tooPower konta usługi BI**.
4. Wprowadź poświadczenia hello na koncie usługi Power BI.

## <a name="create-a-power-bi-schedule"></a>Utwórz harmonogram Power BI
Utwórz harmonogram Power BI dla każdego zestawu danych za pomocą hello procedury.

1. W konsoli OMS powitania kliknij hello **wyszukiwania dziennika** kafelka.
2. Wpisz kwerendę lub wybierz zapisane wyszukiwanie, że zwraca hello dane mają tooexport zbyt**usługi Power BI**.  
3. Kliknij przycisk hello **usługi Power BI** u góry hello hello strony tooopen hello **usługi Power BI** okna dialogowego.
4. Podaj informacje hello w hello poniżej tabeli i kliknij przycisk **zapisać**.

| Właściwość | Opis |
|:--- |:--- |
| Nazwa |Nazwa tooidentify hello harmonogram podczas wyświetlania listy hello harmonogramy usługi Power BI. |
| Zapisane wyszukiwanie |Witaj toorun wyszukiwania dziennika.  Możesz wybrać hello bieżącego zapytania lub wybierz istniejące zapisane wyszukiwanie z listy rozwijanej hello. |
| Harmonogram |Jak często hello toorun zapisane wyszukiwanie i eksportowanie toohello zestawu danych z usługi Power BI.  wartość Hello musi wynosić od 15 minut do 24 godzin. |
| Nazwa zestawu danych |Nazwa Hello hello dataset w usłudze Power BI.  Zostanie ono utworzone, jeśli nie istnieje i zaktualizowany, jeśli istnieje. |

## <a name="viewing-and-removing-power-bi-schedules"></a>Wyświetlanie i usuwanie Power BI harmonogramów
Wyświetlanie listy hello istniejących Power BI harmonogramów z hello procedury.

1. W konsoli OMS powitania kliknij hello **ustawienia** kafelka.
2. Wybierz **Power BI**.

Ponadto zaplanować szczegóły toohello hello, hello liczbę hello harmonogram zostało uruchomione w hello w zeszłym tygodniu i hello hello ostatniej synchronizacji są wyświetlane.  Synchronizacji hello napotkała błędy, po kliknięciu hello łącze toorun dziennika wyszukiwanie rekordów z szczegóły błędu hello.

Harmonogram można usunąć, klikając hello **X** w hello **kolumna usunąć**.  Harmonogram można wyłączyć, wybierając **poza**.  toomodify harmonogramu należy ją usunąć i utwórz ją ponownie z nowymi ustawieniami hello.

![Power BI harmonogramów](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a>Przykładowe wskazówki
Witaj poniższej sekcji przedstawiono przykład tworzenia harmonogramu Power BI i przy użyciu jego toocreate zestawu danych prosty raport.  W tym przykładzie wszystkie dane dotyczące wydajności dla zestawu komputerów jest wyeksportowany tooPower BI i wykres liniowy tworzona jest toodisplay użycie procesora.

### <a name="create-log-search"></a>Tworzenie dziennika wyszukiwania
Firma Microsoft Rozpocznij od utworzenia dziennika wyszukiwanie danych hello czy chcemy toosend toohello dataset.  W tym przykładzie użyjemy zapytanie zwracające wszystkie dane dotyczące wydajności na komputerach z nazwą rozpoczyna się od *srv*.  

![Power BI harmonogramów](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a>Tworzenie Power BI wyszukiwania
Firma Microsoft kliknij hello **usługi Power BI** tooopen hello usługi Power BI w oknie dialogowym przycisk i zawierają hello wymagane informacje.  Firma Microsoft ma toorun tego Wyszukaj raz na godzinę i utworzyć zestawu danych o nazwie *wydajności Contoso*.  Ponieważ firma Microsoft już otwarte wyszukiwania hello tworzy dane hello chcemy, możemy Zachowaj domyślne hello *Użyj bieżącego zapytania wyszukiwania* dla **zapisanych wyszukiwań**.

![Power BI wyszukiwania](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a>Sprawdź Power BI wyszukiwania
tooverify, że poprawnie utworzyliśmy hello harmonogramu, możemy wyświetlić hello listę Power BI wyszukiwania w obszarze hello **ustawienia** kafelka na pulpicie nawigacyjnym OMS hello.  Firma Microsoft Poczekaj kilka minut i Odśwież tego widoku, dopóki nie zgłasza, że przeprowadzono synchronizacji hello.

![Power BI wyszukiwania](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a>Sprawdź hello dataset w usłudze Power BI
Firma Microsoft Zaloguj się do naszej konta w [powerbi.microsoft.com](http://powerbi.microsoft.com/) i przewiń zbyt**zestawów danych** u dołu hello hello w lewym okienku.  Zobaczysz, że hello *wydajności Contoso* zestaw danych znajduje się wskazujący naszych eksportu zostało uruchomione pomyślnie.

![Power BI w zestawie danych](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a>Tworzenie raportu na podstawie w zestawie danych
Firma Microsoft wybierz hello **wydajności Contoso** zestawu danych, a następnie kliknij polecenie **wyniki** w hello **pola** okienku na powitania prawo tooview hello pola, które są częścią tego zestawu danych.  toocreate czy wiersza wykres przedstawiający poziom wykorzystania procesora dla każdego komputera, wykonujemy hello następujące akcje.

1. Wybierz wizualizacji wykresu hello wiersza.
2. Przeciągnij **ObjectName** za**filtru poziomu raportu** i sprawdź **procesora**.
3. Przeciągnij **CounterName** za**filtru poziomu raportu** i sprawdź **% czasu procesora**.
4. Przeciągnij **równowartości** za**wartości**.
5. Przeciągnij **komputera** za**legendy**.
6. Przeciągnij **TimeGenerated** za**osi**.

Firma Microsoft można zauważyć, że ten wykres liniowy wynikowy hello jest wyświetlany hello danymi z naszym zestawie danych.

![Wykres liniowy Power BI](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a>Zapisz raport hello
Firma Microsoft, Zapisz raport hello, klikając hello Zapisz przycisk u góry hello hello ekranu i Zweryfikuj, że będzie teraz wyświetlany w sekcji raportów hello w okienku po lewej stronie powitania.

![Power BI raportów](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) toobuild zapytania, które mogą być eksportowane tooPower BI.
* Dowiedz się więcej o [usługi Power BI](http://powerbi.microsoft.com) wizualizacje toobuild oparte na eksportuje analizy dzienników.
