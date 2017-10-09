---
title: "Omówienie punktu końcowego przesyłania strumieniowego usługi multimediów aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie usługi Azure Media Services punkty końcowe przesyłania strumieniowego."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 097ab5e5-24e1-4e8e-b112-be74172c2701
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: f27f590175dcc945d1d3299fc0cae5a68cfbf4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-endpoints-overview"></a>Omówienie punktów końcowych przesyłania strumieniowego 

##<a name="overview"></a>Omówienie

W programie Microsoft Azure Media Services (AMS), **punktu końcowego przesyłania strumieniowego** reprezentuje usługę przesyłania strumieniowego, który może dostarczyć zawartości bezpośrednio tooa aplikacja odtwarzacza klienta lub tooa Content Delivery Network (CDN) w celu dalszej dystrybucji. Usługa Media Services udostępnia również bezproblemową integrację usługi Azure CDN. Hello strumienia wychodzącego z usługi StreamingEndpoint może być strumień na żywo, wideo na żądanie lub pobierania progresywnego zawartości na koncie usługi Media Services. Każde konto usługi Azure Media Services zawiera domyślne StreamingEndpoint. Dodatkowe punkty końcowe mogą być tworzone w ramach konta hello. Istnieją dwie wersje punkty końcowe, 1.0 i 2.0. Począwszy od stycznia 2017 10, wszystkie nowo utworzonego konta usługi AMS zostaną uwzględnione w wersji 2.0 **domyślne** StreamingEndpoint. Dodanie konta toothis punkty końcowe przesyłania strumieniowego dodatkowe będzie także w wersji 2.0. Ta zmiana nie ma wpływu na istniejące konta hello; istniejące punkty końcowe będą w wersji 1.0 i może być uaktualniony tooversion 2.0. Ta zmiana będzie zmiany zachowania, rozliczeń i funkcji (Aby uzyskać więcej informacji, zobacz hello **przesyłania strumieniowego, typy i wersje** sekcji opisane poniżej).

Ponadto, począwszy od wersji hello 2.15 (wydane w stycznia 2017 r), usługi Azure Media Services dodane hello następujące właściwości toohello punktu końcowego przesyłania strumieniowego jednostki: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Aby uzyskać szczegółowe informacje o tych właściwości, zobacz [to](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

Podczas tworzenia konta usługi Azure Media Services domyślnie standardowego punktu końcowego przesyłania strumieniowego jest tworzony w hello **zatrzymane** stanu. Nie można usunąć domyślnego hello punktu końcowego przesyłania strumieniowego. W zależności od hello Azure CDN dostępności w regionie hello docelowe, domyślnie nowo utworzony domyślny punktu końcowego przesyłania strumieniowego obejmuje również "StandardVerizon" CDN integracji dostawcy. 

>[!NOTE]
>Integracja z usługą Azure CDN, można wyłączyć przed rozpoczęciem powitalne punktu końcowego przesyłania strumieniowego.

Ten temat zawiera omówienie funkcji main hello udostępnianych przez punkty końcowe przesyłania strumieniowego.

## <a name="streaming-types-and-versions"></a>Typy i wersje przesyłania strumieniowego

### <a name="standardpremium-types-version-20"></a>Typy standardowe/Premium (wersja 2.0)

Począwszy od wersji stycznia 2017 hello Media Services, istnieją dwa typy przesyłania strumieniowego: **standardowe** i **Premium**. Te typy są częścią wersji punktu końcowego przesyłania strumieniowego hello "2.0".

Typ|Opis
---|---
**Standardowa**|Jest to hello opcję domyślną będzie działać dla hello większość scenariuszy hello.<br/>Po wybraniu tej opcji Pobierz/limited SLA, pierwszych 15 dni, po uruchomieniu hello punktu końcowego przesyłania strumieniowego wolnego.<br/>W przypadku utworzenia więcej niż jeden punkty końcowe przesyłania strumieniowego, tylko hello najpierw jednym jest bezpłatna dla hello pierwszych 15 dni, powitalne inne są rozliczane natychmiast po ich uruchomieniu. <br/>Należy pamiętać, że bezpłatnej wersji próbnej stosuje tylko toonewly utworzone konta usługi media i domyślnego punktu końcowego przesyłania strumieniowego. Istniejące punkty końcowe przesyłania strumieniowego, a ponadto utworzony punktów końcowych przesyłania strumieniowego nie obejmuje bezpłatna wersja próbna okres nawet są uaktualnione tooversion 2.0 lub zostały utworzone w wersji 2.0.
**Premium**|Ta opcja jest odpowiednia dla specjalistów scenariusze, które wymagają większej skali lub kontrolki.<br/>Zmiennej umowy SLA, oparty na premium przesyłania strumieniowego pojemność jednostki (SU) zakupionych dedykowanych punktów końcowych przesyłania strumieniowego na żywo w izolowanym środowisku i nie powodowały konfliktu dla zasobów.

Aby uzyskać szczegółowe informacje, zobacz hello **porównania przesyłania strumieniowego typy** następujących sekcji.

### <a name="classic-type-version-10"></a>Typ klasyczny (w wersji 1.0)

Dla użytkowników, którzy utworzone konta usługi AMS toohello wcześniejszych wersji 10 stycznia 2017 r, masz **klasycznego** typ punktu końcowego przesyłania strumieniowego. Ten typ jest częścią hello przesyłania strumieniowego punktu końcowego w wersji "1.0".

Jeśli Twoje **wersji "1.0"** punktu końcowego przesyłania strumieniowego ma > = 1 — wersja premium ("SU"), jednostki przesyłania strumieniowego będzie premium punktu końcowego przesyłania strumieniowego i zapewnia wszystkie funkcje AMS (podobnie jak hello **Standard/Premium** typu) bez żadnych dodatkowych czynności konfiguracyjnych.

>[!NOTE]
>**Klasycznym** punkty końcowe przesyłania strumieniowego (w wersji "1.0" i 0 SU), udostępnia funkcje ograniczona i nie zawiera umowy dotyczącej poziomu usług. Zaleca się toomigrate zbyt**standardowe** wpisz tooget lepsze środowisko i toouse funkcji, takich jak dynamicznego tworzenia pakietów lub szyfrowania i inne funkcje, które pochodzą z hello **standardowe** typu. toomigrate toohello **standardowe** wpisz, przejdź toohello [portalu Azure](https://portal.azure.com/) i wybierz **opcjonalnych tooStandard**. Aby uzyskać więcej informacji na temat migracji, zobacz hello [migracji](#migration-between-types) sekcji.
>
>Należy pamiętać, że ta operacja nie może zostać wycofana i ma wpływ cenową.
>
 
## <a name="comparing-streaming-types"></a>Porównanie typów przesyłania strumieniowego

### <a name="versions"></a>Wersje

|Typ|StreamingEndpointVersion|ScaleUnits|CDN|Rozliczenia|Umowa SLA| 
|--------------|----------|-----------------|-----------------|-----------------|-----------------|    
|Wdrożenie klasyczne|1.0|0|Nie dotyczy|Bezpłatna|Nie dotyczy|
|Standardowy punkt końcowy przesyłania strumieniowego|2.0|0|Tak|Płatne|Tak|
|Jednostki przesyłania strumieniowego Premium|1.0|>0|Tak|Płatne|Tak|
|Jednostki przesyłania strumieniowego Premium|2.0|>0|Tak|Płatne|Tak|

### <a name="features"></a>Funkcje

Funkcja|Standardowa|Premium
---|---|---
Pierwszy 15 dni wolne| Tak |Nie
Przepływność |Zapasowej too600 MB/s, gdy nie jest używana usługa Azure CDN. Można skalować usługi CDN.|200 MB/s na jednostka (SU). Można skalować usługi CDN.
Umowa SLA | 99.9|99,9 (200 MB/s na SU).
CDN|Usługi Azure CDN, innej sieci CDN lub nie CDN.|Usługi Azure CDN, innej sieci CDN lub nie CDN.
Karta jest proporcjonalna| Codziennie|Codziennie
Szyfrowania dynamicznego|Tak|Tak
Dynamiczne tworzenie pakietów|Tak|Tak
Skalowanie|Automatyczne skalowanie się przepływności toohello docelowe.|Dodatkowe jednostki przesyłania strumieniowego
IP filtrowania/G20/niestandardowy host|Tak|Tak
Pobierania progresywnego|Tak|Tak
Zalecane użycie |Zalecane hello większość przesyłania strumieniowego scenariuszy.|Użycie Professional.<br/>Jeśli uważasz, że masz potrzeb poza Standard. Skontaktuj się z nami (amsstreaming adresem), Jeśli przypuszczasz, rozmiar równoczesnych odbiorców większych niż 50 000 przeglądarki.


## <a name="migration-between-types"></a>Migracja między typami

Z | zbyt| Akcja
---|---|---
Wdrożenie klasyczne|Standardowa|Potrzeby tooopt w
Wdrożenie klasyczne|Premium| Skala (dodatkowe jednostki przesyłania strumieniowego)
Standard/Premium|Wdrożenie klasyczne|Niedostępne (jeśli punktu końcowego przesyłania strumieniowego w wersji 1.0. Może on tooclassic toochange z ustawień scaleunits zbyt "0")
Standard (lub bez CDN)|Premium z hello takie same konfiguracje|Dozwolone w hello **uruchomiona** stanu. (za pośrednictwem portalu Azure)
Premium (lub bez CDN)|Standardowa z hello takie same konfiguracje|Dozwolone w hello **uruchomiona** stanu (za pośrednictwem portalu Azure)
Standard (lub bez CDN)|Premium z różnych konfiguracji|Dozwolone w hello **zatrzymana** stanu (za pośrednictwem portalu Azure). Nie są dozwolone w hello stanu działania.
Premium (lub bez CDN)|Standard z różnych konfiguracji|Dozwolone w hello **zatrzymana** stanu (za pośrednictwem portalu Azure). Nie są dozwolone w hello stanu działania.
W wersji 1.0 z SU > = 1 z sieci CDN|Standard/Premium z nie CDN|Dozwolone w hello **zatrzymana** stanu. Nie są dozwolone w hello **uruchomiona** stanu.
W wersji 1.0 z SU > = 1 z sieci CDN|Standard lub bez CDN|Dozwolone w hello **zatrzymana** stanu. Nie są dozwolone w hello **uruchomiona** stanu. W wersji 1.0 CDN będzie jednej usunięta, a nowe utworzone i uruchomione.
W wersji 1.0 z SU > = 1 z sieci CDN|Premium lub bez CDN|Dozwolone w hello **zatrzymana** stanu. Nie są dozwolone w hello **uruchomiona** stanu. Klasyczne sieci CDN będzie jednej usunięta, a nowe utworzone i uruchomione.

## <a name="next-steps"></a>Następne kroki
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

