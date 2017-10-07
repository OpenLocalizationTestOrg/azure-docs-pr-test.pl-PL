---
title: "aaaMicrosoft usługi Azure Media Services scenariuszy i dostępność funkcji centrów | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie scenariuszy usługi Microsoft Azure Media Services oraz dostępności funkcji i usług w centrach danych."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a>Scenariusze i dostępność funkcji usługi Media Services w centrach danych

Microsoft Azure Media Services (AMS) umożliwia przekazywanie toosecurely, przechowywanie, kodowanie i pakietów zawartości wideo lub audio zarówno na żądanie i na żywo przesyłania strumieniowego dostarczania toovarious klientów (na przykład TV, PC i urządzeń przenośnych).

AMS działa w wielu centrach danych wokół hello world. Tych centrach danych są pogrupowane w toogeographic regionach, zapewniając elastyczność podczas wybierania, gdzie toobuild aplikacji. Możesz przejrzeć hello [lista regionów i ich lokalizacje](https://azure.microsoft.com/regions/). 

W tym temacie przedstawiono typowe scenariusze dostarczania zawartości [na żywo](#live_scenarios) lub [na żądanie](#vod_scenarios). temat Hello zawiera także szczegółowe informacje o dostępności nośnika funkcji i usług między centrami danych.

## <a name="overview"></a>Omówienie

### <a name="prerequisites"></a>Wymagania wstępne

toostart przy użyciu usługi Azure Media Services, powinien mieć następujące hello:

* Konto platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com).
* Konto usługi Azure Media Services. Aby uzyskać więcej informacji, zobacz temat [Tworzenie konta](media-services-portal-create-account.md).
* Witaj, z którego mają zostać toostream zawartości punktu końcowego przesyłania strumieniowego ma toobe w hello **systemem** stanu.

    Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. toostart przesyłania strumieniowego zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania, hello punktu końcowego przesyłania strumieniowego ma toobe w hello **systemem** stanu.

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a>Często używane obiekty podczas opracowywania przed hello modelu AMS OData

Witaj poniższej ilustracji przedstawiono niektóre obiekty hello najczęściej używane podczas tworzenia modelu Media Services OData hello.

Kliknij przycisk tooview obraz powitania pełny jego rozmiar.  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

Możesz wyświetlić hello całego modelu [tutaj](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a>Ochrona zawartości w magazynie i wyczyść dostarczyć multimediów strumieniowych w hello (z systemem innym niż szyfrowane)

![Wideo na żądanie — przepływ pracy](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. Przekaż plik multimedialny wysokiej jakości do elementu zawartości.

    Zalecane jest tooapply zasobów tooyour opcji szyfrowania magazynu w kolejności tooprotect zawartość podczas przekazywania i podczas przechowywania w magazynie.
2. Kodowanie tooa zestawu plików MP4 z adaptacyjną szybkością transmisji bitów.

    Zaleca się, że toohello opcji szyfrowania magazynu tooapply output zasobów w kolejności tooprotect przechowywaną zawartość.
3. Skonfiguruj zasady dostarczania elementu zawartości (stosowane podczas dynamicznego tworzenia pakietów).

    Jeśli element zawartości jest szyfrowany w magazynie, **musisz** skonfigurować zasady dostarczania elementu zawartości.
4. Opublikuj hello zawartości, tworząc Lokalizator OnDemand.
5. Prześlij strumieniowo opublikowaną zawartość.

Aby uzyskać informacje na temat dostępności w centrach danych, zobacz hello [dostępności](#availability) sekcji.

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a>Ochrona zawartości w magazynie i dostarczanie dynamicznie szyfrowanych multimediów strumieniowych

![Ochrona za pomocą PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. Przekaż plik multimedialny wysokiej jakości do elementu zawartości. Zastosuj zasobów toohello opcji szyfrowania magazynu.
2. Kodowanie tooa zestawu plików MP4 z adaptacyjną szybkością transmisji bitów. Zastosuj zawartości wyjściowej toohello opcji szyfrowania magazynu.
3. Utwórz klucz szyfrowania zawartości dla zasobów hello ma toobe dynamicznie zaszyfrowany podczas odtwarzania.
4. Skonfiguruj zasady autoryzacji klucza zawartości.
5. Skonfiguruj zasady dostarczania elementu zawartości (używane podczas dynamicznego tworzenia pakietów i dynamicznego szyfrowania).
6. Opublikuj hello zawartości, tworząc Lokalizator OnDemand.
7. Prześlij strumieniowo opublikowaną zawartość.

Aby uzyskać informacje na temat dostępności w centrach danych, zobacz hello [dostępności](#availability) sekcji.

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a>Użyj analizy multimediów tooderive przydatnych wyników analiz z filmy wideo

Analiza multimediów to kolekcja składników mowy i obrazu, które ułatwiają przydatnych wyników analiz tooderive organizacjom i przedsiębiorstwom podstawie posiadanych plików wideo. Aby uzyskać więcej informacji, zobacz temat [Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md).

1. Przekaż plik multimedialny wysokiej jakości do elementu zawartości.
2. Przetwarzać pliki wideo z jednej z usług analizy multimediów hello opisanych w hello [omówienie analizy multimediów](media-services-analytics-overview.md) sekcji.
3. Procesory multimediów usługi Analiza multimediów tworzą pliki MP4 lub JSON. Plik MP4 utworzony przez procesor multimediów można pobrać progresywnie hello pliku. Plik JSON utworzony przez procesor multimediów można pobrać pliku hello z hello magazynu obiektów blob platformy Azure.

Aby uzyskać informacje na temat dostępności w centrach danych, zobacz hello [dostępności](#availability) sekcji.

## <a name="deliver-progressive-download"></a>Dostarczanie pobierania progresywnego

1. Przekaż plik multimedialny wysokiej jakości do elementu zawartości.
2. Kodowanie tooa pojedynczego pliku MP4.
3. Opublikuj hello zawartości, tworząc Lokalizator OnDemand lub SAS.

    W przypadku użycia lokalizatora SAS zawartość hello jest pobierana z hello magazynu obiektów blob platformy Azure. W takim przypadku nie trzeba toohave punkty końcowe w stanie uruchomionym przesyłania strumieniowego.
4. Pobierz progresywnie zawartość.

## <a id="live_scenarios"></a>Dostarczanie zdarzeń transmisji strumieniowej na żywo 

1. Pozyskaj zawartość na żywo przy użyciu różnych protokołów transmisji strumieniowej na żywo (np. RTMP lub Smooth Streaming).
2. (Opcjonalnie) Zakoduj strumień w formie strumienia o adaptacyjnej szybkości transmisji bitów.
3. Wyświetl podgląd transmisji strumieniowej na żywo.
4. Dostarczanie zawartości hello za pośrednictwem wspólnych protokołów przesyłania strumieniowego (na przykład MPEG DASH, Smooth, HLS) bezpośrednio tooyour klientów lub tooa Content Delivery Network (CDN) w celu dalszej dystrybucji.

    — lub —

    Rekord i magazynu zawartości hello pozyskanych w kolejności toobe strumieniowego nowszej (wideo na żądanie).

W trakcie transmisji strumieniowych na żywo, możesz wybrać jedną z następujących hello tras:

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Praca z kanałami odbierającymi strumień na żywo o różnych szybkościach transmisji bitów z koderów lokalnych (przekazujących)

Witaj Poniższy diagram przedstawia hello główne elementy platformy hello AMS, które są związane z hello **przekazywanego** przepływu pracy.

![Przepływ pracy na żywo](./media/scenarios-and-availability/media-services-live-streaming-current.png)

Aby uzyskać więcej informacji, zobacz temat [Praca z kanałami odbierającymi strumień na żywo o różnych szybkościach transmisji bitów z koderów lokalnych](media-services-live-streaming-with-onprem-encoders.md).

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Praca z kanałami, które są włączone tooperform live encoding w usłudze Azure Media Services

Witaj Poniższy diagram przedstawia hello główne elementy platformy AMS hello związanych z transmisji strumieniowej na żywo przepływu pracy gdzie kanał jest włączony tooperform live encoding w usłudze Media Services.

![Przepływ pracy na żywo](./media/scenarios-and-availability/media-services-live-streaming-new.png)

Aby uzyskać więcej informacji, zobacz [Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Aby uzyskać informacje na temat dostępności w centrach danych, zobacz hello [dostępności](#availability) sekcji.

## <a name="consuming-content"></a>Korzystanie z zawartości

Usługa Azure Media Services udostępnia hello narzędzi można muszą sformatowanego toocreate aplikacji dynamicznej klienckich odtwarzacza dla większości platform, w tym: iOS urządzeń, urządzenia z systemem Android, Windows, Windows Phone, Xbox i dekodera pola. powitania po tematu zawiera linki tooSDKs oraz struktur odtwarzaczy, których można używać toodevelop własnych aplikacji klienckich, które multimediów strumieniowych dostarczanych z usługi Media Services. Aby uzyskać więcej informacji, zobacz temat [Projektowanie aplikacji płatnika wideo](media-services-develop-video-players.md)

## <a name="enabling-azure-cdn"></a>Włączanie usługi Azure CDN

Usługa Media Services obsługuje integrację z usługą Azure CDN. Aby uzyskać informacje na temat tooenable Azure CDN, zobacz [jak punkty końcowe przesyłania strumieniowego tooManage w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md).

## <a id="scaling"></a>Skalowanie konta usługi Media Services

Klienci usługi AMS mogą skalować punkty końcowe przesyłania strumieniowego, przetwarzanie multimediów i przechowywanie na swoich kontach usługi AMS.

* Klienci usługi Media Services mogą wybrać **Standardowy** punkt końcowy przesyłania strumieniowego lub punkt końcowy przesyłania strumieniowego **Premium**. **Standardowy** punkt końcowy przesyłania strumieniowego jest odpowiedni w przypadku większości obciążeń przesyłania strumieniowego. Obejmuje on hello takie same funkcje jak **Premium** przesyłania strumieniowego przepustowości wychodzącej punktów końcowych i umożliwiają Skalowanie automatyczne. 

    Punkty końcowe przesyłania strumieniowego **Premium** są odpowiednie w przypadku zaawansowanych obciążeń, ponieważ zapewniają dedykowaną i skalowalną pojemność przepustowości. Klienci, którzy mają punkt końcowy przesyłania strumieniowego **Premium**, domyślnie uzyskują jedną jednostkę przesyłania strumieniowego (SU, streaming unit). Witaj punktu końcowego przesyłania strumieniowego można skalować, dodając SUs. Każdy SU udostępnia dodatkowe ograniczenie użycia przepustowości pojemności toohello aplikacji. Aby uzyskać więcej informacji na temat skalowania **Premium** punkty końcowe przesyłania strumieniowego, zobacz hello [skalowanie punktów końcowych przesyłania strumieniowego](media-services-portal-scale-streaming-endpoints.md) tematu.

* Konto usługi Media Services jest skojarzony z zarezerwowanych typu jednostki, który określa szybkość hello przetwarzania zadania przetwarzania multimediów. Można wybrać między hello następujące typy jednostek zarezerwowanych: **S1**, **S2**, lub **S3**. Na przykład hello tego samego zadania kodowania działa szybciej, gdy używasz hello **S2** jednostka zarezerwowanego typ porównania toohello **S1** typu.

    Ponadto toospecifying hello zastrzeżone typ jednostki, można określić tooprovision Twojego konta z **jednostki zarezerwowanego** (RUs). Liczba Hello elastycznie RUs określa hello liczbę zadań nośnika, które mogą być jednocześnie przetwarzane w ramach danego konta.

    >[!NOTE]
    >Jednostki zarezerwowane przekształcają wszystkie operacje przetwarzania multimediów do postaci równoległej, uwzględniając zadania Indeksowania za pomocą usługi Azure Media Indexer. Jednak w przeciwieństwie do kodowania zadania indeksowania nie są przetwarzane szybciej przy użyciu szybszych jednostek zarezerwowanych.

    Aby uzyskać więcej informacji, zobacz temat [Skalowanie przetwarzania multimediów](media-services-portal-scale-media-processing.md).
* Możliwe jest także skalowanie konta usługi Media Services przez dodanie tooit kont magazynu. Każde konto magazynu jest ograniczona too500 TB. tooexpand pojemność magazynu poza ograniczenia domyślne hello, można wybrać tooattach wiele magazynów kont tooa jednego konta usługi Media Services. Aby uzyskać więcej informacji, zobacz temat [Zarządzanie kontami magazynu](meda-services-managing-multiple-storage-accounts.md).

##<a id="availability"></a>Dostępność funkcji usługi Media Services w centrach danych

Ta sekcja zawiera szczegółowe informacje o dostępności funkcji usługi Media Services w centrach danych.

### <a name="ams-accounts"></a>Konta usługi AMS

#### <a name="availability"></a>Dostępność

Można tworzyć konta usługi Media Services w następujących regionach hello: Europa Północna, Europa Zachodnia, zachodnie stany USA, wschodnie stany USA, Azja południowo-wschodnia, Azja Wschodnia, Japonia Zachodnia, Japonia Wschodnia, Brazylia Południowa, Indie Zachodnie, Indie Południowe i Indie środkowe. 

### <a name="streaming-endpoints"></a>Punkty końcowe przesyłania strumieniowego 

Klienci usługi Media Services mogą wybrać **Standardowy** punkt końcowy przesyłania strumieniowego lub punkt końcowy przesyłania strumieniowego **Premium**. Aby uzyskać więcej informacji, zobacz hello [skalowanie](#scaling) sekcji.

#### <a name="availability"></a>Dostępność

|Nazwa|Stan|Centra danych
|---|---|---|
|Standardowa|Ogólna dostępność|Wszystkie|
|Premium|Ogólna dostępność|Wszystkie|

### <a name="live-encoding"></a>Kodowanie na żywo

#### <a name="availability"></a>Dostępność

Dostępne we wszystkich centrach danych z wyjątkiem następujących regionów: Niemcy, Brazylia Południowa, Indie Zachodnie, Indie Południowe i Indie Środkowe. 

### <a name="encoding-media-processors"></a>Kodowanie procesorów multimediów

Usługa AMS oferuje dwa kodery na żądanie: **Media Encoder Standard** i **Media Encoder Premium Workflow**. Aby uzyskać więcej informacji, zobacz temat [Przegląd i porównanie koderów multimediów na żądanie na platformie Azure ](media-services-encode-asset.md). 

#### <a name="availability"></a>Dostępność

|Nazwa procesora multimediów|Stan|Centra danych
|---|---|---|
|Usługa Media Encoder Standard|Ogólna dostępność|Wszystkie|
|Przepływ pracy usługi Media Encoder w warstwie Premium|Ogólna dostępność|Wszystkie z wyjątkiem Chin|

### <a name="analytics-media-processors"></a>Procesory multimediów usługi analizy

Analiza multimediów to kolekcja składników mowy i obrazu, która ułatwia przydatnych wyników analiz tooderive organizacjom i przedsiębiorstwom podstawie posiadanych plików wideo. Aby uzyskać więcej informacji, zobacz temat [Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md).

#### <a name="availability"></a>Dostępność

|Nazwa procesora multimediów|Stan|Centra danych
|---|---|---|
|Azure Media Face Detector|Wersja zapoznawcza|Wszystkie|
|Azure Media Hyperlapse|Wersja zapoznawcza|Wszystkie|
|Azure Media Indexer|Ogólna dostępność|Wszystkie|
|Azure Media Motion Detector|Wersja zapoznawcza|Wszystkie|
|Azure Media OCR|Wersja zapoznawcza|Wszystkie|
|Azure Media Redactor|Wersja zapoznawcza|Wszystkie|
|Azure Media Stabilizer|Wersja zapoznawcza|Wszystkie|
|Azure Media Video Thumbnails|Wersja zapoznawcza|Wszystkie|
|Azure Media Indexer 2|Wersja zapoznawcza|Wszystkie z wyjątkiem Chin i obszaru administracji federalnej USA|

### <a name="protection"></a>Ochrona

Microsoft Azure Media Services umożliwia toosecure możesz z hello razem, gdy opuszczą komputera za pośrednictwem przechowywania, przetwarzania i dostarczania multimediów. Aby uzyskać więcej informacji, zobacz temat [Ochrona zawartości usługi AMS](media-services-content-protection-overview.md).

#### <a name="availability"></a>Dostępność

|Szyfrowanie|Stan|Centra danych|
|---|---|---| 
|Magazyn|Ogólna dostępność|Wszystkie|
|Klucze AES-128|Ogólna dostępność|Wszystkie|
|FairPlay|Ogólna dostępność|Wszystkie|
|PlayReady|Ogólna dostępność|Wszystkie|
|Widevine|Ogólna dostępność|Wszystkie regiony z wyjątkiem Niemiec, Rządu Federalnego i Chin.

### <a name="reserved-units-rus"></a>Jednostki zarezerwowane (RU)

Liczba Hello elastycznie jednostki zarezerwowanego określa hello liczbę zadań nośnika, które mogą być jednocześnie przetwarzane w ramach danego konta. 

Aby uzyskać więcej informacji, zobacz hello [skalowanie](#scaling) sekcji.

#### <a name="availability"></a>Dostępność

Dostępne we wszystkich centrach danych.

### <a name="reserved-unit-ru-type"></a>Typ jednostki zarezerwowanej (RU)

Konto usługi Media Services jest skojarzony z typem jednostka zarezerwowanego, który określa szybkość hello przetwarzania zadania przetwarzania multimediów. Można wybrać między hello następujące typy jednostek zarezerwowanych: S1, S2 lub S3.

Aby uzyskać więcej informacji, zobacz hello [skalowanie](#scaling) sekcji.

#### <a name="availability"></a>Dostępność

|Nazwa typu jednostki zarezerwowanej|Stan|Centra danych
|---|---|---|
|S1|Ogólna dostępność|Wszystkie|
|S2|Ogólna dostępność|Wszystkie regiony z wyjątkiem Brazylii Południowej i Indii Zachodnich|
|S3|Ogólna dostępność|Wszystkie regiony z wyjątkiem Indii Zachodnich|

## <a name="next-steps"></a>Następne kroki

Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

