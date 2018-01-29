---
title: "Scenariusze usługi Microsoft Azure Media Services i dostępność funkcji w centrach danych | Microsoft Docs"
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
ms.openlocfilehash: d9994dd7bfb6b6bf949a7708c07651d667929ae4
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a>Scenariusze i dostępność funkcji usługi Media Services w centrach danych

Usługa Microsoft Azure Media Services (AMS) umożliwia bezpieczne przekazywanie, przechowywanie, kodowanie i tworzenie pakietów zawartości wideo lub audio na potrzeby transmisji strumieniowej na żądanie i na żywo do różnych klientów (np. odbiorników TV, komputerów i urządzeń przenośnych).

Usługa AMS działa w wielu centrach danych na całym świecie. Te centra danych są grupowane w regiony geograficzne, dzięki czemu można elastycznie wybierać miejsca kompilowania aplikacji. Możesz zapoznać się z [listą regionów i ich lokalizacji](https://azure.microsoft.com/regions/). 

W tym temacie przedstawiono typowe scenariusze dostarczania zawartości [na żywo](#live_scenarios) lub [na żądanie](#vod_scenarios). Temat zawiera także szczegółowe informacje o dostępności usług i funkcji multimedialnych w centrach danych.

## <a name="overview"></a>Omówienie

### <a name="prerequisites"></a>Wymagania wstępne

Do rozpoczęcia korzystania z usługi Azure Media Services potrzebne są:

* Konto platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com).
* Konto usługi Azure Media Services. Aby uzyskać więcej informacji, zobacz temat [Tworzenie konta](media-services-portal-create-account.md).
* Punkt końcowy przesyłania strumieniowego, z którego chcesz strumieniowo przesyłać zawartość, musi mieć stan **Uruchomiony**.

    Po utworzeniu konta usługi AMS zostanie do niego dodany **domyślny** punkt końcowy przesyłania strumieniowego mający stan **Zatrzymany**. Aby rozpocząć przesyłanie strumieniowe zawartości oraz korzystać z dynamicznego tworzenia pakietów i szyfrowania, punkt końcowy przesyłania strumieniowego musi mieć stan **Uruchomiony**.

### <a name="commonly-used-objects-when-developing-against-the-ams-odata-model"></a>Najczęściej używane obiekty podczas projektowania w modelu AMS OData

Na poniższym obrazie przedstawiono niektóre z najczęściej używanych obiektów podczas tworzenia w modelu Media Services OData.

Kliknij obraz, aby go wyświetlić w pełnym rozmiarze.  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

Cały model możesz obejrzeć [tutaj](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-the-clear-non-encrypted"></a>Ochrona zawartości w magazynie i dostarczanie multimediów strumieniowych w formie niezaszyfrowanej

![Wideo na żądanie — przepływ pracy](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. Przekaż plik multimedialny wysokiej jakości do elementu zawartości.

    Zaleca się stosowanie opcji szyfrowania magazynu w odniesieniu do elementu zawartości, aby chronić zawartość podczas przekazywania oraz przechowywania w magazynie.
2. Wykonaj kodowanie do zestawu plików MP4 o adaptacyjnej szybkości transmisji bitów.

    Zaleca się stosowanie opcji szyfrowania magazynu w odniesieniu do elementu zawartości wyjściowej, aby chronić przechowywaną zawartość.
3. Skonfiguruj zasady dostarczania elementu zawartości (stosowane podczas dynamicznego tworzenia pakietów).

    Jeśli element zawartości jest szyfrowany w magazynie, **musisz** skonfigurować zasady dostarczania elementu zawartości.
4. Opublikuj element zawartości, tworząc lokalizator OnDemand.
5. Prześlij strumieniowo opublikowaną zawartość.

Aby uzyskać informacje na temat dostępności w centrach danych, zobacz sekcję [Dostępność](#availability).

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a>Ochrona zawartości w magazynie i dostarczanie dynamicznie szyfrowanych multimediów strumieniowych

![Ochrona za pomocą PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. Przekaż plik multimedialny wysokiej jakości do elementu zawartości. Zastosuj opcję szyfrowania magazynu w odniesieniu do elementu zawartości.
2. Wykonaj kodowanie do zestawu plików MP4 o adaptacyjnej szybkości transmisji bitów. Zastosuj opcję szyfrowania magazynu w odniesieniu do elementu zawartości wyjściowej.
3. Utwórz klucz szyfrowania zawartości dla elementu zawartości, który ma zostać dynamicznie zaszyfrowany podczas odtwarzania.
4. Skonfiguruj zasady autoryzacji klucza zawartości.
5. Skonfiguruj zasady dostarczania elementu zawartości (używane podczas dynamicznego tworzenia pakietów i dynamicznego szyfrowania).
6. Opublikuj element zawartości, tworząc lokalizator OnDemand.
7. Prześlij strumieniowo opublikowaną zawartość.

Aby uzyskać informacje na temat dostępności w centrach danych, zobacz sekcję [Dostępność](#availability).

## <a name="use-media-analytics-to-derive-actionable-insights-from-your-videos"></a>Korzystanie z Analizy multimediów w celu uzyskania przydatnych wyników analiz na podstawie danych wideo

Analiza multimediów to kolekcja składników mowy i obrazu, które ułatwiają organizacjom i przedsiębiorstwom uzyskiwanie przydatnych wyników analiz na podstawie posiadanych plików wideo. Aby uzyskać więcej informacji, zobacz temat [Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md).

1. Przekaż plik multimedialny wysokiej jakości do elementu zawartości.
2. Przetwarzaj pliki wideo za pomocą jednej z usług analizy multimediów opisanych w sekcji [Przegląd usług analizy multimediów](media-services-analytics-overview.md).
3. Procesory multimediów usługi Analiza multimediów tworzą pliki MP4 lub JSON. Plik MP4 utworzony przez procesor multimediów można pobrać progresywnie. Plik JSON utworzony przez procesor multimediów można pobrać z magazynu Azure Blob Storage.

Aby uzyskać informacje na temat dostępności w centrach danych, zobacz sekcję [Dostępność](#availability).

## <a name="deliver-progressive-download"></a>Dostarczanie pobierania progresywnego

1. Przekaż plik multimedialny wysokiej jakości do elementu zawartości.
2. Wykonaj kodowanie do pojedynczego pliku MP4.
3. Opublikuj element zawartości, tworząc lokalizator OnDemand lub SAS.

    W przypadku użycia lokalizatora SAS zawartość zostanie pobrana z magazynu Azure Blob Storage. W takim przypadku nie są konieczne punkty końcowe przesyłania strumieniowego w stanie uruchomionym.
4. Pobierz progresywnie zawartość.

## <a id="live_scenarios"></a>Dostarczanie zdarzeń transmisji strumieniowej na żywo 

1. Pozyskaj zawartość na żywo przy użyciu różnych protokołów transmisji strumieniowej na żywo (np. RTMP lub Smooth Streaming).
2. (Opcjonalnie) Zakoduj strumień w formie strumienia o adaptacyjnej szybkości transmisji bitów.
3. Wyświetl podgląd transmisji strumieniowej na żywo.
4. Dostarczaj zawartość za pośrednictwem wspólnych protokołów przesyłania strumieniowego (np. MPEG DASH, Smooth, HLS) bezpośrednio do klientów lub do usługi Content Delivery Network (CDN) w celu dalszej dystrybucji

    — lub —

    zarejestruj i przechowaj pozyskaną zawartość do celów przesyłania strumieniowego w późniejszym czasie (wideo na żądanie).

W trakcie transmisji strumieniowej na żywo można wybrać jedną z następujących tras:

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Praca z kanałami odbierającymi strumień na żywo o różnych szybkościach transmisji bitów z koderów lokalnych (przekazujących)

Na poniższym diagramie przedstawiono główne elementy platformy AMS, które są zaangażowane w przepływ pracy **przekazywania**.

![Przepływ pracy na żywo](./media/scenarios-and-availability/media-services-live-streaming-current.png)

Aby uzyskać więcej informacji, zobacz temat [Praca z kanałami odbierającymi strumień na żywo o różnych szybkościach transmisji bitów z koderów lokalnych](media-services-live-streaming-with-onprem-encoders.md).

### <a name="working-with-channels-that-are-enabled-to-perform-live-encoding-with-azure-media-services"></a>Praca z kanałami obsługującymi kodowanie na żywo za pomocą usługi Azure Media Services

Na poniższym diagramie przedstawiono główne elementy platformy AMS biorące udział w przepływie pracy transmisji strumieniowej na żywo, gdy kanał obsługuje kodowanie na żywo za pomocą usługi Media Services.

![Przepływ pracy na żywo](./media/scenarios-and-availability/media-services-live-streaming-new.png)

Aby uzyskać więcej informacji, zobacz temat [Praca z kanałami obsługującymi funkcję Live Encoding w usłudze Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Aby uzyskać informacje na temat dostępności w centrach danych, zobacz sekcję [Dostępność](#availability).

## <a name="consuming-content"></a>Korzystanie z zawartości

Usługa Azure Media Services udostępnia narzędzia potrzebne do tworzenia zaawansowanych, dynamicznych aplikacji klienckich odtwarzacza dla większości platform, takich jak: urządzenia z systemem iOS, urządzenia z systemem Android, urządzenia z systemem Windows, telefony z systemem Windows Phone, konsole Xbox i dekodery. Poniższy temat zawiera linki do zestawów SDK oraz struktur odtwarzaczy, których można użyć do opracowywania własnych aplikacji klienckich korzystających z multimediów strumieniowych dostarczanych przez usługę Media Services. Aby uzyskać więcej informacji, zobacz temat [Projektowanie aplikacji płatnika wideo](media-services-develop-video-players.md)

## <a name="enabling-azure-cdn"></a>Włączanie usługi Azure CDN

Usługa Media Services obsługuje integrację z usługą Azure CDN. Aby uzyskać informacje o sposobie włączania usługi Azure CDN, zobacz temat [Zarządzanie punktami końcowymi przesyłania strumieniowego na koncie usługi Media Services](media-services-portal-manage-streaming-endpoints.md).

## <a id="scaling"></a>Skalowanie konta usługi Media Services

Klienci usługi AMS mogą skalować punkty końcowe przesyłania strumieniowego, przetwarzanie multimediów i przechowywanie na swoich kontach usługi AMS.

* Klienci usługi Media Services mogą wybrać **Standardowy** punkt końcowy przesyłania strumieniowego lub punkt końcowy przesyłania strumieniowego **Premium**. **Standardowy** punkt końcowy przesyłania strumieniowego jest odpowiedni w przypadku większości obciążeń przesyłania strumieniowego. Oferuje on te same funkcje, co punkty końcowe przesyłania strumieniowego **Premium**, oraz automatycznie skaluje przepustowość wychodzącą. 

    Punkty końcowe przesyłania strumieniowego **Premium** są odpowiednie w przypadku zaawansowanych obciążeń, ponieważ zapewniają dedykowaną i skalowalną pojemność przepustowości. Klienci, którzy mają punkt końcowy przesyłania strumieniowego **Premium**, domyślnie uzyskują jedną jednostkę przesyłania strumieniowego (SU, streaming unit). Punkt końcowy przesyłania strumieniowego można skalować poprzez dodawanie jednostek SU. Każdy jednostka SU zwiększa pojemność przepustowości aplikacji. Aby uzyskać więcej informacji na temat skalowania punktów końcowych przesyłania strumieniowego **Premium**, zobacz temat [Skalowanie punktów końcowych przesyłania strumieniowego](media-services-portal-scale-streaming-endpoints.md).

* Konto usługi Media Services jest skojarzone z typem jednostki zarezerwowanej określającym szybkość, z jaką są przetwarzane zadania przetwarzania multimediów. Można wybrać jeden z następujących typów jednostki zarezerwowanej: **S1**, **S2** lub **S3**. Na przykład to samo zadanie kodowania jest wykonywane szybciej przy użyciu typu jednostki zarezerwowanej **S2** niż w przypadku użycia typu **S1**.

    Oprócz określenia typu jednostki zarezerwowanej można określić aprowizację swojego konta przy użyciu **jednostek zarezerwowanych** (RU, Reserved Unit). Liczba zainicjowanych jednostek zarezerwowanych określa liczbę zadań multimedialnych, które mogą być przetwarzane jednocześnie w ramach danego konta.

    >[!NOTE]
    >Jednostki zarezerwowane przekształcają wszystkie operacje przetwarzania multimediów do postaci równoległej, uwzględniając zadania Indeksowania za pomocą usługi Azure Media Indexer. Jednak w przeciwieństwie do kodowania zadania indeksowania nie są przetwarzane szybciej przy użyciu szybszych jednostek zarezerwowanych.

    Aby uzyskać więcej informacji, zobacz temat [Skalowanie przetwarzania multimediów](media-services-portal-scale-media-processing.md).
* Możliwe jest także skalowanie konta usługi Media Services przez dodanie do niego kont magazynu. Pojemność każdego konta magazynu jest ograniczona do 500 TB. Aby rozszerzyć pojemność magazynu poza ograniczenia domyślne, można dołączyć wiele kont magazynu do jednego konta usługi Media Services. Aby uzyskać więcej informacji, zobacz temat [Zarządzanie kontami magazynu](meda-services-managing-multiple-storage-accounts.md).

##<a id="availability"></a>Dostępność funkcji usługi Media Services w centrach danych

Ta sekcja zawiera szczegółowe informacje o dostępności funkcji usługi Media Services w centrach danych.

### <a name="ams-accounts"></a>Konta usługi AMS

#### <a name="availability"></a>Dostępność

Konta usługi Media Services można tworzyć w następujących regionach: Europa Północna, Europa Zachodnia, Zachodnie stany USA, Wschodnie stany USA, Azja Południowo-Wschodnia, Azja Wschodnia, Japonia Zachodnia, Japonia Wschodnia, Brazylia Południowa, Indie Zachodnie, Indie Południowe i Indie Środkowe. 

### <a name="streaming-endpoints"></a>Punkty końcowe przesyłania strumieniowego 

Klienci usługi Media Services mogą wybrać **Standardowy** punkt końcowy przesyłania strumieniowego lub punkt końcowy przesyłania strumieniowego **Premium**. Aby uzyskać więcej informacji, zobacz sekcję opisującą [skalowanie](#scaling).

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

Analiza multimediów to kolekcja składników mowy i obrazu, które ułatwiają organizacjom i przedsiębiorstwom pozyskiwanie przydatnych informacji z posiadanych plików wideo. Aby uzyskać więcej informacji, zobacz temat [Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md).

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

Usługi Microsoft Azure Media Services umożliwiają zabezpieczenie multimediów od momentu wysłania danych z komputera w ramach procesów przechowywania, przetwarzania i dostarczania. Aby uzyskać więcej informacji, zobacz temat [Ochrona zawartości usługi AMS](media-services-content-protection-overview.md).

#### <a name="availability"></a>Dostępność

|Szyfrowanie|Stan|Centra danych|
|---|---|---| 
|Magazyn|Ogólna dostępność|Wszystkie|
|Klucze AES-128|Ogólna dostępność|Wszystkie|
|FairPlay|Ogólna dostępność|Wszystkie|
|PlayReady|Ogólna dostępność|Wszystkie|
|Widevine|Ogólna dostępność|Wszystkie regiony z wyjątkiem Niemiec, Rządu Federalnego i Chin.

### <a name="reserved-units-rus"></a>Jednostki zarezerwowane (RU)

Liczba zainicjowanych jednostek zarezerwowanych określa liczbę zadań multimedialnych, które mogą być przetwarzane jednocześnie w ramach danego konta. 

Aby uzyskać więcej informacji, zobacz sekcję opisującą [skalowanie](#scaling).

#### <a name="availability"></a>Dostępność

Dostępne we wszystkich centrach danych.

### <a name="reserved-unit-ru-type"></a>Typ jednostki zarezerwowanej (RU)

Konto usługi Media Services jest skojarzone z typem jednostki zarezerwowanej określającym szybkość, z jaką są przetwarzane zadania przetwarzania multimediów. Można wybrać jeden z następujących typów jednostki zarezerwowanej: S1, S2 lub S3.

Aby uzyskać więcej informacji, zobacz sekcję opisującą [skalowanie](#scaling).

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

