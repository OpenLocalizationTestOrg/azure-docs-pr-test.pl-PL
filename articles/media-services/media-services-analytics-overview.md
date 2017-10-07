---
title: aaaMedia Analytics na platformie Media Services hello | Dokumentacja firmy Microsoft
description: "Omówienie publicznej wersji zapoznawczej z analizy multimediów, Kolekcja usług wizji mowy i komputera w skali przedsiębiorstwa, zgodności i zabezpieczeń oraz globalne"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a>Analiza multimediów na powitania platformy Media Services
## <a name="overview"></a>Omówienie
Organizacje więcej używany jest wideo jako hello preferowanych tootrain średnia pracownikom, zaangażowania klientów i znaczenie biznesowe dokumentu. Chmury obliczeniowej zapewnia toostore sposób strumienia i dostęp do tych duże pliki multimedialne. Jednak wraz z rozwojem firmy biblioteki zawartości wideo, musi on równie skuteczne środki wyodrębniania szczegółowych informacji z hello zawartości. 

tooaddress tę potrzebę rosnącym usługi Azure Media Services udostępnia analizy multimediów Azure. Analiza multimediów to kolekcja składników mowy i obrazu, która ułatwia przydatnych wyników analiz tooderive organizacjom i przedsiębiorstwom podstawie posiadanych plików wideo. Utworzony przy użyciu składników platformy Media Services core hello, analiza multimediów może obsługiwać nośnika przetwarzania na dużą skalę na jeden dzień.

Z analizy multimediów deweloperzy mogą szybko Przełącz zaawansowane funkcje wideo do aplikacji. Zapewnia on środowiskach przedsiębiorstw hello skali, zgodności zabezpieczeń i globalne wymagane przez dużych organizacjach.

Witaj Poniższy diagram przedstawia analizy multimediów i inne główne elementy platformy Media Services hello. 

![Wideo na żądanie — przepływ pracy](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

Procesory multimediów usługi Analiza multimediów tworzą pliki MP4 lub JSON. Procesor multimediów tworzy plik MP4, można pobrać progresywnie hello pliku. Jeśli procesor multimediów powoduje utworzenie pliku JSON, możesz pobrać hello plik z magazynu obiektów Blob platformy Azure. 

## <a name="media-analytics-services"></a>Usług analizy multimediów

### <a name="indexer"></a>Indeksator
Z usługi Azure Media indeksatora możesz wprowadzić zawartości można wyszukiwać i generować-kodowane ścieżki. Porównaniu toohello poprzedniej wersji Preview 2 indeksatora multimediów Azure ma szybciej indeksowania i szerszych języka obsługuje. Obsługiwane języki angielski, hiszpański, francuski, niemiecki, włoski, chiński, portugalski i arabski. Aby uzyskać szczegółowe informacje i przykłady, zobacz [przetwarzanie plików wideo z usługi Azure Media Indexer 2](media-services-process-content-with-indexer2.md).
### <a name="hyperlapse"></a>Hyperlapse
Microsoft Hyperlapse łączy stabilizacji wideo i możliwości ujęć poklatkowych toocreate szybki i eksploatacyjny filmy wideo z zawartości długiej. Oprócz tworzenia ujęć poklatkowych wideo, możesz użyć przyspieszonych ujęć poklatkowych toocreate stabilna filmy wideo z obraz wideo przechwycone przez telefony komórkowe i kamery. Aby uzyskać szczegółowe informacje i przykłady, zobacz [przyspieszonych ujęć poklatkowych plików multimedialnych na pliki z usługi Azure Media Hyperlapse](media-services-hyperlapse-content.md).
### <a name="motion-detector"></a>Wykrywanie ruchu
Czujnik ruchu toodetect ruchu można użyć w pliku wideo z nieruchomy tła. Dzięki temu możliwe toocheck dla fałszywych alarmów zdarzeń ruchu wykrywane przez kamer nadzoru. Aby uzyskać szczegółowe informacje i przykłady, zobacz [wykrywanie na potrzeby analizy multimediów Azure ruchu](media-services-motion-detection.md).
### <a name="face-detector"></a>Wykrywanie twarzy
Przy użyciu detektora krój, można wykryć powierzchni użytkowników i ich emocji, w tym szczęście, sadness i niespodziewanego. To ma kilka przydatne branży aplikacji, w dalszej części, tym agregowanie i analizowanie danych reakcji uczestników zdarzenia. Aby uzyskać szczegółowe informacje i przykłady, zobacz [wykrywania twarzy na obrazie i emocji dla analizy multimediów Azure](media-services-face-and-emotion-detection.md).
### <a name="video-summarization"></a>Podsumowanie wideo
Podsumowanie wideo mogą pomóc tworzyć podsumowania długich filmów wideo, wybierając automatycznie interesujące wstawki z hello źródła wideo. Ta możliwość jest przydatne, gdy chcesz tooprovide szybki przegląd tooexpect które długie wideo. Aby uzyskać szczegółowe informacje i przykłady, zobacz [podsumowanie wideo toocreate miniatur wideo multimediów Azure użyj](media-services-video-summarization.md).
### <a name="optical-character-recognition"></a>Optyczne rozpoznawanie znaków
Z usługi Azure Media Rozpoznawania (OCR) zawartość tekstu w plikach wideo można przekonwertować na tekst cyfrowy można edytować, wyszukiwanie. Następnie można zautomatyzować wyodrębniania hello łatwy do rozpoznania metadanych z hello sygnału wideo multimediów.
### <a name="scalable-face-redaction"></a>Skalowalna krój redakcyjne
Azure Media Redactor jest procesora nośnika analizy multimediów, które oferuje skalowalne krój redakcyjne w chmurze hello. Za pomocą redakcyjne krój, można zmodyfikować Twoje kroje wideo tooblur wybrane osoby. Możesz toouse hello krój redakcyjne usługi na nośniku wiadomości lub uczestniczy bezpieczeństwa publicznego. Kilka minut najmniejszym zawiera wiele kroje może zająć godziny tooredact ręcznie, ale z tą usługą redakcyjne krój trwa tylko kilka prostych kroków. Aby uzyskać więcej informacji, zobacz hello [redagowanie krojów z analizy multimediów Azure](media-services-face-redaction.md) artykułu.

## <a name="common-scenarios"></a>Typowe scenariusze
Analiza multimediów może ułatwić organizacjom i przedsiębiorstwom zgromadzonych nowych danych z wideo i więcej efektywnie zarządzać dużych ilości zawartości wideo. Poniżej przedstawiono kilka scenariuszy:

* **Wywołaj centrów**. Nawet w przypadku pojawienie się hello mediów społecznościowych odbiorcy biura obsługi ułatwienia nadal znaczną część transakcji obsługi klienta. Zakodowane w tych danych audio jest duża ilość informacji klienta, które mogą być przeanalizowane tooachieve wyższy stopień zadowolenia klientów. Przy użyciu nośnika indeksatora, organizacje można wyodrębnić tekst i twórz indeksów wyszukiwania i pulpity nawigacyjne. Następnie mogli wyodrębnić informacji dotyczących typowych utrudnień, źródeł utrudnień i inne odpowiednie dane.
* **Łagodzenie zawartość wygenerowaną przez użytkowników**. Z nośnika wiadomości działów toopolice gniazda w wielu organizacjach istnieją portale publicznych, które akceptują wygenerowaną przez użytkowników nośniki, takie jak pliki wideo i obrazów. Hello ilością zawartości można zwiększyć powodu toounexpected zdarzenia. W tych scenariuszach jest trudne tooconduct skuteczne recenzje ręczne zawartości dla właściwości. Klienci mogą polegać na hello toofocus usługi łagodzenia zawartości dla zawartości, która jest odpowiednia.
* **Nadzoru**. Z hello wzrost użycia kamer IP pochodzą rosnącym spisu wideo nadzoru. Ręcznie recenzowania nadzoru wideo jest błąd toohuman intensywnego i podatnych na błędy. Analiza multimediów udostępnia usługi, takie jak przyspieszonych ujęć poklatkowych toomake hello procesu przeglądu, zarządzania i tworzenie pochodnych łatwiejsze, wykrywania twarzy na obrazie i wykrywania ruchu.

## <a name="media-analytics-media-processors"></a>Procesory multimediów usługi analiza multimediów
To sekcja procesory multimediów analizy multimediów hello list pokazuje sposób toouse .NET lub REST tooget obiektu procesora (MP) nośnika.

### <a name="mp-names"></a>Nazwy pakietu administracyjnego
* Podgląd indeksatora 2 multimediów Azure
* Azure Media Indexer
* Azure Media Hyperlapse
* Azure Media Face Detector
* Azure Media Motion Detector
* Azure Media Video Thumbnails
* Azure Media OCR

### <a name="net"></a>.NET
powitania po funkcja przyjmuje jeden z hello określony pakiet administracyjny nazwy i zwraca obiekt pakietu administracyjnego.

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a>REST
Żądanie:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

Odpowiedź:

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a>Pokazy
Zobacz [pokazy analizy multimediów Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).

## <a name="next-steps"></a>Następne kroki
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Pokrewne artykuły:
Zobacz [anonsu analiza usługi multimediów](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
