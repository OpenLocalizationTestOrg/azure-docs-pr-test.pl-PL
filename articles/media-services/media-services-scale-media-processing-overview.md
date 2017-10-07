---
title: "Omówienie przetwarzania multimediów aaaScaling | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie skalowania przetwarzania nośnika za pomocą usługi Azure Media Services."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: d17531f79d4c1e0d0fa544c4fb5c083684e706fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-media-processing-overview"></a>Skalowanie przetwarzania multimediów — omówienie
Ta strona umożliwia identyfikowanie, jak i dlaczego tooscale przetwarzania multimediów. 

## <a name="overview"></a>Omówienie
Konto usługi Media Services jest skojarzony z zarezerwowanych typu jednostki, który określa szybkość hello przetwarzania zadania przetwarzania multimediów. Można wybrać między hello następujące typy jednostek zarezerwowanych: **S1**, **S2**, lub **S3**. Na przykład hello tego samego zadania kodowania działa szybciej, gdy używasz hello **S2** jednostka zarezerwowanego typ porównania toohello **S1** typu. Aby uzyskać więcej informacji, zobacz hello [typy jednostek zarezerwowanych](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).

Ponadto toospecifying hello zastrzeżone typ jednostki, można określić tooprovision konta z zastrzeżone jednostki. Liczba Hello elastycznie jednostki zarezerwowanego określa hello liczbę zadań nośnika, które mogą być jednocześnie przetwarzane w ramach danego konta. Na przykład jeśli konto ma pięć jednostki zarezerwowanego, następnie nośnika pięć zadań będą uruchomione jednocześnie tak długo, jak istnieją toobe zadania przetwarzania. Witaj pozostałych zadań będzie czekać w kolejce hello i zostanie pobrana uzyskać przetwarzania sekwencyjnie, po zakończeniu uruchomione zadanie. Jeśli konto nie ma żadnych jednostek zarezerwowanego zainicjowano obsługę administracyjną, następnie zadania będą pobierane po kolei. W takim przypadku hello czas oczekiwania między jeden Kończenie zadań i hello uruchomienie kolejnej będzie zależeć od hello dostępność zasobów w systemie hello.

## <a name="choosing-between-different-reserved-unit-types"></a>Wybór między różnych zastrzeżonych typów jednostek
Witaj w poniższej tabeli ułatwia podjęcie decyzji, wybierając między różnych szybkościach kodowania. Również zapewnia kilka przypadków testu porównawczego i udostępnia adresy URL SAS, używaną filmy toodownload, na których można wykonać własne testy:

| Scenariusze | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| Zamierzonym użyciem case |Kodowanie pojedynczej szybkości transmisji bitów. <br/>Pliki SD lub poniżej rozwiązania, czas nie poufne, niskich kosztów. |Pojedynczej szybkości transmisji bitów i kodowanie wielu szybkości transmisji bitów.<br/>Normalnego użycia zarówno SD, jak i HD kodowania. |Pojedynczej szybkości transmisji bitów i kodowanie wielu szybkości transmisji bitów.<br/>Pełna HD oraz 4K rozpoznawania wideo. Czas przetwarzania poufnych, szybszych kodowania. |
| Testu porównawczego |[Plik wejściowy: 640x360p na 29,97 5 minut długich ramek/sekundę](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>Kodowanie pliku pojedynczej szybkości transmisji bitów MP4 tooa na powitania tego samego rozwiązania trwa około 11 minut. |[Plik wejściowy: 1280x720p na 29,97 5 minut długich ramek/sekundę](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)<br/><br/>Kodowanie z "H264 pojedynczej szybkości transmisji bitów 720p" wstępnie trwa około 5 minut.<br/><br/>Z kodowaniem "H264 szybkość transmisji bitów 720p" ustawienie wstępne trwa około 11,5 minut. |[Plik wejściowy: 1920x1080p na 29,97 5 minut długich ramek/sekundę](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D). <br/><br/>Kodowanie z "H264 pojedynczej szybkości transmisji bitów 1080p" wstępnie trwa około 2.7 minut.<br/><br/>Z kodowaniem "H264 szybkość transmisji bitów 1080p" ustawienie wstępne trwa około wersji 5.7 minut. |

## <a name="considerations"></a>Zagadnienia do rozważenia
> [!IMPORTANT]
> Zapoznaj się z uwagami opisane w tej sekcji.  
> 
> 

* Zastrzeżone jednostki działa w przypadku parallelizing przetwarzania nośnika, w tym Indeksowanie zadań za pomocą usługi Azure Media indeksatora.  Jednak w przeciwieństwie do kodowania zadania indeksowania nie są przetwarzane szybciej przy użyciu szybszych jednostek zarezerwowanych.
* Jeśli przy użyciu udostępnionych hello puli, oznacza to, bez żadnej jednostki zarezerwowane, a następnie zadań Koduj ma hello wydajności, podobnie jak w przypadku S1 RUs. Niestety nie są czas toohello górna granica nie poświęcić zadań w kolejce stanu i w dowolnym momencie, będą uruchomione co najwyżej tylko jedno zadanie.
* powitania po centrów danych nie oferują hello **S2** zastrzeżone typ jednostki: Brazylia Południowe i Indie Zachodnie.
* Witaj następujące centrum danych nie oferuje hello **S3** zastrzeżone typ jednostki: Indie Zachodnie.

## <a name="billing"></a>Rozliczenia

Opłaty są naliczane na podstawie rzeczywistej liczby minut użycia jednostek zarezerwowanych multimediów. Aby uzyskać szczegółowy opis, zobacz sekcję hello — często zadawane pytania hello [cenach usługi Media Services](https://azure.microsoft.com/pricing/details/media-services/) strony.   

## <a name="quotas-and-limitations"></a>Limity przydziału i ograniczenia
Aby uzyskać informacje o przydziały i ograniczenia i tooopen biletu pomocy technicznej, zobacz temat [przydziały i ograniczenia](media-services-quotas-and-limitations.md).

## <a name="next-step"></a>Następny krok
Osiągnięcia hello skalowanie przetwarzania zadania z jednej z tych technologii nośnika: 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

