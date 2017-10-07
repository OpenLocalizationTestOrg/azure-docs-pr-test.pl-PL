---
title: "Eksport aaaContinuous dane telemetryczne z usługi Application Insights | Dokumentacja firmy Microsoft"
description: "Eksportuj toostorage danych diagnostycznych i użycia w systemie Microsoft Azure i pobierz go z tego miejsca."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a>Eksportuj dane telemetryczne z usługi Application Insights
Chcesz tookeep telemetrii przez czas dłuższy niż okres przechowywania standardowe hello? Lub przetwarzać dane w jakiś sposób specjalne? Eksport ciągły jest idealna to. Hello zdarzenia, które są widoczne w portalu usługi Application Insights hello może być eksportowany toostorage platformie Microsoft Azure w formacie JSON. Z tego miejsca można pobrać danych i zapisu, niezależnie od kod należy tooprocess go.  

Przy użyciu eksportu ciągłego może pociągnąć za sobą dodatkowe opłaty. Sprawdź Twojej [model cenowy](http://azure.microsoft.com/pricing/details/application-insights/).

Przed skonfigurowaniem Eksport ciągły istnieje kilka rozwiązań alternatywnych można tooconsider:

* przycisk Eksportuj Hello u góry bloku metryki lub wyszukiwania hello umożliwia transfer arkusz kalkulacyjny programu Excel tooan tabel i wykresów.

* [Analiza](app-insights-analytics.md) zapewnia język kwerendy zaawansowanych telemetrii. Można także wyeksportować wyniki.
* Jeśli szukasz zbyt[eksplorować dane w usłudze Power BI](app-insights-export-power-bi.md), możesz to zrobić bez użycia eksportu ciągłego.
* Witaj [dostępu do danych interfejsu API REST](https://dev.applicationinsights.io/) pozwala uzyskiwać dostęp do telemetrii programowo.

Po eksportu ciągłego kopiuje Twojej toostorage danych (jeżeli pozostawał dla tak długo, jak chcesz), jest on nadal dostępny w usłudze Application Insights dla hello zwykle [okres przechowywania](app-insights-data-retention-privacy.md).

## <a name="setup"></a>Utwórz eksport ciągły
1. Hello zasobu usługi Application Insights dla aplikacji, otwórz eksportu ciągłego i wybierz polecenie **Dodaj**:

    ![Przewiń w dół i kliknij przycisk eksportu ciągłego](./media/app-insights-export-telemetry/01-export.png)

2. Wybierz typy danych telemetrycznych hello ma tooexport.

3. Utwórz lub wybierz [konto magazynu Azure](../storage/common/storage-introduction.md) miejscu toostore hello danych.

    > [!Warning]
    > Domyślnie program hello lokalizacji magazynu zostanie ustawiona toohello tego samego regionu geograficznego co zasób usługi Application Insights. Jeśli jest przechowywany w innym regionie, może spowodować naliczenie opłat transferu.

    ![Kliknij przycisk Dodaj, wyeksportować miejsce docelowe konto magazynu, a następnie utwórz nowy magazyn lub wybierz istniejący magazyn](./media/app-insights-export-telemetry/02-add.png)

4. Utwórz lub Wybierz kontener magazynu hello:

    ![Kliknij przycisk Wybierz typy zdarzeń](./media/app-insights-export-telemetry/create-container.png)

Po utworzeniu eksportu uruchamia przejście. Tylko Pobierz dane przychodzący po utworzeniu hello eksportu.

Może to być opóźnienie około godziny przed wyświetleniem danych w magazynie hello.

### <a name="tooedit-continuous-export"></a>Eksport ciągły tooedit

Jeśli chcesz typów zdarzeń toochange hello później, po prostu edytować Eksport hello:

![Kliknij przycisk Wybierz typy zdarzeń](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a>Eksport ciągły toostop

Wyłącz toostop hello eksportu, kliknij przycisk. Po kliknięciu włączyć ponownie, hello eksportu zostanie uruchomiony ponownie z nowymi danymi. Użytkownik nie będzie otrzymywał hello dane, które dotarły w portalu hello podczas eksportowania została wyłączona.

Eksport hello toostop stałe, usuń go. Dzięki temu nie powoduje usunięcia danych z magazynu.

### <a name="cant-add-or-change-an-export"></a>Nie można dodać lub zmienić eksportu?
* eksporty tooadd lub zmiany, należy właściciela, współautora lub Application Insights współautora praw dostępu. [Dowiedz się więcej o rolach][roles].

## <a name="analyze"></a>Jakie zdarzenia uzyskać?
Witaj wyeksportowanych danych jest hello nieprzetworzone dane telemetryczne, otrzymywanych z aplikacji, ale dodamy danych lokalizacji, które firma Microsoft obliczenia z adresu IP powitania klienta.

Dane, które zostały odrzucone przez [próbkowania](app-insights-sampling.md) nie jest uwzględniony w hello wyeksportowane dane.

Inne metryki obliczanej nie są uwzględniane. Na przykład firma Microsoft nie Eksportuj średnie wykorzystanie procesora CPU, ale eksportowania telemetrii raw hello, z którego jest obliczana średnia hello.

Witaj danych obejmuje również hello wyniki dowolnego [testów sieci web dostępności](app-insights-monitor-web-app-availability.md) , które zostały skonfigurowane.

> [!NOTE]
> **Próbkowania.** Jeśli aplikacja wyśle dużą ilość danych, funkcja próbkowania hello może działać i tylko część telemetrii hello wygenerowane wysyłać. [Dowiedz się więcej na temat próbkowania.](app-insights-sampling.md)
>
>

## <a name="get"></a>Sprawdź hello danych
Możesz sprawdzić magazynu hello bezpośrednio w portalu hello. Kliknij przycisk **Przeglądaj**, wybierz konto magazynu, a następnie otwórz **kontenery**.

Otwórz tooinspect magazynu Azure w programie Visual Studio, **widoku**, **Eksplorator chmury**. (Jeśli nie masz tego polecenia menu, należy tooinstall hello Azure SDK: Otwórz hello **nowy projekt** okna dialogowego, rozwiń Visual C# / w chmurze i wybierz polecenie **pobrać zestaw Microsoft Azure SDK dla platformy .NET**.)

Po otwarciu magazynie obiektów blob, zobaczysz kontener z zestawu plików obiektów blob. Witaj identyfikatora URI poszczególnych plików pochodząca z nazwę zasobu usługi Application Insights, jego klucza instrumentacji, telemetrii — typ, datę i godzinę. (nazwa zasobu hello jest tylko małe litery, a klucza Instrumentacji hello pomija łączniki).

![Sprawdź hello magazynu obiektów blob za pomocą odpowiedniego narzędzia](./media/app-insights-export-telemetry/04-data.png)

Witaj Data i godzina są UTC i gdy telemetrii hello został złożony w magazynie hello — nie hello czasu został wygenerowany. Dlatego podczas pisania kodu toodownload hello danych, jej przechodzić liniowo hello danych.

Poniżej przedstawiono formularz hello hello ścieżki:

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

gdzie

* `blobCreationTimeUtc`Godzina blob utworzenia w hello wewnętrznego jest przemieszczania magazynu
* `blobDeliveryTimeUtc`gdy obiekt blob jest Magazyn docelowy eksportu skopiowanych toohello po raz hello

## <a name="format"></a>Format danych
* Każdy obiekt blob jest to plik tekstowy, który zawiera wiele "\n'-separated wierszy. Zawiera ona dane telemetryczne hello przetwarzane w czasie około pół minuty.
* Każdy wiersz reprezentuje punktu danych telemetrii, takich jak żądania lub strony widoku.
* Każdy wiersz jest niesformatowany dokumentu JSON. Toosit i stare go, otwórz go w programie Visual Studio i wybierz pozycję Edytuj, zaawansowane, Format pliku:

![Dane telemetryczne hello widoku z narzędziem do odpowiedniego](./media/app-insights-export-telemetry/06-json.png)

Okresach czasu są w taktach, gdzie znaczniki 10 000 = 1 MS. Na przykład te wartości wyświetlane przez czas 1 MS toosend żądania z przeglądarki hello, 3ms tooreceive i 1.8s tooprocess hello strony w przeglądarce hello:

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[Szczegółowe dane modelu odwołania dla hello typy właściwości i wartości.](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a>Przetwarzanie danych hello
Na małą skalę można zapisać niektórych toopull kodu od siebie danych, przeczytaj je do arkusza kalkulacyjnego i tak dalej. Na przykład:

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

Dla większych przykładowy kod, zobacz [przy użyciu roli procesu roboczego][exportasa].

## <a name="delete"></a>Usuń stare dane
Należy pamiętać, że jest odpowiedzialny za zarządzanie pojemności pamięci masowej i usuwania starych danych hello, jeśli to konieczne.

## <a name="if-you-regenerate-your-storage-key"></a>Jeśli musisz ponownie wygenerować klucz magazynu...
Jeśli zmienisz magazynu kluczy tooyour hello Eksport ciągły przestaną działać. Zostanie wyświetlone powiadomienie na koncie Azure.

Otwarcie bloku eksportu ciągłego hello i edytowanie eksportu. Edytuj hello docelowego eksportu, ale pozostaw hello wybrane tego samego magazynu. Kliknij przycisk OK tooconfirm.

![Edytuj hello ciągłego wyeksportować, Otwórz i zamknąć ją docelowego eksportu.](./media/app-insights-export-telemetry/07-resetstore.png)

Witaj Eksport ciągły zostanie uruchomiony ponownie.

## <a name="export-samples"></a>Przykłady eksportu

* [Eksportuj tooSQL przy użyciu usługi analiza strumienia][exportasa]
* [Stream Analytics próbki 2](app-insights-export-stream-analytics.md)

Na większą skalę, należy wziąć pod uwagę [HDInsight](https://azure.microsoft.com/services/hdinsight/) -klastrów Hadoop w chmurze hello. Usługa HDInsight zapewnia różne technologie zarządzania i analizy danych big data i może używać tooprocess danych, który został wyeksportowany z usługi Application Insights.

## <a name="q--a"></a>Pytania i odpowiedzi
* *Ale wszystkie wybrane jednorazowe pobierania wykresu.*  

    Tak, możesz to zrobić. U góry hello hello bloku, kliknij przycisk **eksportowanie danych**.
* *Skonfigurować eksportu, ale nie ma żadnych danych w magazynie my.*

    Application Insights dotarła wszystkie dane telemetryczne z aplikacji ponieważ konfigurowanie hello eksportu? Otrzymasz nowych danych.
* *Nastąpiła tooset się eksportu, ale nastąpiła odmowa dostępu*

    Jeśli konto hello jest własnością organizacji, należy toobe hello właściciele i współautorzy grup.
* *Można wyeksportować proste toomy własnych z lokalnym magazynem?*

    Nie, Niestety. Nasze mechanizm eksportu jest obecnie obsługiwane tylko z usługą Azure storage w tej chwili.  
* *Czy istnieje limit żadnych toohello ilość danych, które należy umieścić w sklep?*

    Nie. Firma Microsoft będzie przechowywać przekazywanie danych do momentu usunięcia hello eksportu. Jeśli mamy trafień hello zewnętrzne limity dla magazynu obiektów blob, ale jest to bardzo dużych zostanie zatrzymana. Należy się tooyou toocontrol ile miejsca do magazynowania można użyć.  
* *Jak wiele obiektów blob zobacz w magazynie hello*

  * Dla typu danych co wybrany tooexport, nowy obiekt blob jest tworzony co minutę (jeśli są dostępne dane).
  * Ponadto w przypadku aplikacji o dużym ruchu, jednostki dodatkowe partycji są przydzielone. W takim przypadku każdej jednostki tworzy obiektu blob, co minutę.
* *I ponownie wygenerować hello toomy klucza magazynu lub zmienić nazwę hello hello kontenera i hello eksportu nie działają.*

    Edytuj Eksport hello i otwarcie bloku docelowego eksportu hello. Pozostaw hello tego samego magazynu co poprzednio zaznaczone, a następnie kliknij przycisk OK tooconfirm. Eksport zostanie uruchomiony ponownie. Zmiana hello była w hello ostatnie kilka dni, nie spowodować utratę danych.
* *Czy można wstrzymać hello eksportu?*

    Tak. Kliknij przycisk Wyłącz.

## <a name="code-samples"></a>Przykłady kodu

* [Przykładowe analiza strumienia](app-insights-export-stream-analytics.md)
* [Eksportuj tooSQL przy użyciu usługi analiza strumienia][exportasa]
* [Szczegółowe dane modelu odwołania dla hello typy właściwości i wartości.](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
