---
title: Schemat Encoder Standard aaaMedia | Dokumentacja firmy Microsoft
description: "Witaj temat zawiera omówienie hello Media Encoder Standard schematu."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 4c060062-8ef2-41d9-834e-e81e8eafcf2e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 82bad27b9546f75557ac691ff148b46990647632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-schema"></a>Schemat Media Encoder Standard
W tym temacie opisano niektóre elementy hello i typy hello schematu XML, na którym [ustawienia standardu Media Encoder Standard](media-services-mes-presets-overview.md) opierają się. Witaj temat zawiera opis elementów i ich prawidłowe wartości. pełny schemat Hello zostaną opublikowane w późniejszym terminie.  

## <a name="Preset"></a>Ustawienia domyślne (element główny)
Definiuje ustawienie kodowania.  

### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Kodowanie** |[Kodowanie](media-services-mes-schema.md#Encoding) |Element główny wskazuje, że źródeł dla wejścia hello toobe zakodowany. |
| **Dane wyjściowe** |[Dane wyjściowe](media-services-mes-schema.md#Output) |Kolekcja plików żądanego wyniku. |

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Wersja**<br/><br/> Wymagane |**xs:decimal** |Witaj wstępnie wersji. Witaj, obowiązują następujące ograniczenia: wartość xs:fractionDigits = wartość "1" i xs:minInclusive = "1" na przykład **wersja = "1.0"**. |

## <a name="Encoding"></a>Kodowanie
Zawiera sekwencję hello następujące elementy.  

### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **H264Video** |[H264Video](media-services-mes-schema.md#H264Video) |Ustawienia dla kodowanie wideo H.264. |
| **AACAudio** |[AACAudio](media-services-mes-schema.md#AACAudio) |Ustawienia kodowania audio AAC. |
| **BmpImage** |[BmpImage](media-services-mes-schema.md#BmpImage) |Ustawienia dla obrazu w formacie Bmp. |
| **PngImage** |[PngImage](media-services-mes-schema.md#PngImage) |Ustawienia dla obrazów Png. |
| **JpgImage** |[JpgImage](media-services-mes-schema.md#JpgImage) |Ustawienia dla obrazów Jpg. |

## <a name="H264Video"></a>H264Video
### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **TwoPass**<br/><br/> minOccurs = "0" |**xs:Boolean** |Aktualnie obsługiwana jest tylko jeden przebieg kodowania. |
| **KeyFrameInterval**<br/><br/> minOccurs = "0"<br/><br/> **domyślne = "00: 00:02"** |**xs: Time** |Określa hello stały odstęp między ramki IDR w jednostkach czasu w sekundach. Nazywana także tooas hello GOP duration. Zobacz **SceneChangeDetection** (patrz poniżej) do kontrolowania, czy hello kodera można różni się od tej wartości. |
| **SceneChangeDetection**<br/><br/> minOccurs = "0"<br/><br/> domyślne = "false" |**xs:Boolean** |Jeśli zestaw tootrue, prób kodera sceny toodetect Zmień hello wideo i wstawia IDR ramkę. |
| **Złożoność**<br/><br/> minOccurs = "0"<br/><br/> domyślne = "Zrównoważony" |**xs:String** |Formanty hello kompromis między kodowania jakości szybkość i wideo. Może być jednym z hello następujące wartości: **szybkości**, **zrównoważony**, lub **jakości**<br/><br/> Wartość domyślna: **zrównoważonym** |
| **SyncMode**<br/><br/> minOccurs = "0" | |Funkcja mają być widoczne w przyszłych wersjach. |
| **H264Layers**<br/><br/> minOccurs = "0" |[H264Layers](media-services-mes-schema.md#H264Layers) |Kolekcja warstw wideo danych wyjściowych. |

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Warunek** |**xs:String** | Podczas wprowadzania hello nie ma karty wideo, może być tooforce hello koder tooinsert monochromatyczny Ścieżka wideo. toodo, który użyć warunku = "InsertBlackIfNoVideoBottomLayerOnly" (tooinsert wideo na wyłącznie hello najniższa szybkość transmisji bitów) lub warunek = "InsertBlackIfNoVideo" (tooinsert wideo na wszystkie dane wyjściowe szybkości transmisji bitów). Aby uzyskać więcej informacji, zobacz [ten](media-services-advanced-encoding-with-mes.md#no_video) temat.|

## <a name="H264Layers"></a>H264Layers

Domyślnie w przypadku wysłania koder toohello wejściowego, który zawiera tylko audio i wideo nie zawartości wyjściowej hello będzie zawierać pliki z tylko danych audio. Niektóre odtwarzacze może nie być możliwe toohandle takich danych wyjściowych strumieni. Można użyć hello H264Video **InsertBlackIfNoVideo** atrybutu ustawienie tooforce hello koder tooadd wyjściowego toohello Ścieżka wideo w tym scenariuszu. Aby uzyskać więcej informacji, zobacz [ten](media-services-advanced-encoding-with-mes.md#no_video) temat.
              
### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **H264Layer**<br/><br/> minOccurs = maxOccurs "0" = "unbounded" |[H264Layer](media-services-mes-schema.md#H264Layer) |Kolekcja H264 warstwy. |

## <a name="H264Layer"></a>H264Layer
> [!NOTE]
> Limity wideo są oparte na wartości hello opisanych w hello [poziomy H264](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Levels) tabeli.  
> 
> 

### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Profil**<br/><br/> minOccurs = "0"<br/><br/> domyślne = "Auto" |**xs:String** |Może być jedną z następujących hello **xs:string** wartości: **automatycznie**, **linii bazowej**, **Main**, **wysokiej**. |
| **Poziom**<br/><br/> minOccurs = "0"<br/><br/> domyślne = "Auto" |**xs:String** | |
| **Szybkość transmisji bitów**<br/><br/> minOccurs = "0" |**xs:int** |używany dla tej warstwy wideo określonej w KB/s Hello szybkości transmisji bitów. |
| **MaxBitrate**<br/><br/> minOccurs = "0" |**xs:int** |Witaj maksymalną szybkość transmisji bitów używany dla tej warstwy wideo określonej w KB/s. |
| **BufferWindow**<br/><br/> minOccurs = "0"<br/><br/> domyślne = "00: 00:05" |**xs: Time** |Długość buforu wideo hello. |
| **Szerokość**<br/><br/> minOccurs = "0" |**xs:int** |Szerokość hello wyjście wideo ramki, w pikselach.<br/><br/> Należy pamiętać, że obecnie, należy określić zarówno szerokość i wysokość. Witaj szerokość i wysokość muszą toobe liczby parzyste. |
| **Wysokość**<br/><br/> minOccurs = "0" |**xs:int** |Wysokość hello wyjście wideo ramki, w pikselach.<br/><br/> Należy pamiętać, że obecnie, należy określić zarówno szerokość i wysokość. Witaj szerokość i wysokość muszą toobe liczby parzyste.|
| **BFrames**<br/><br/> minOccurs = "0" |**xs:int** |Liczba ramek B między ramki odwołania. |
| **ReferenceFrames**<br/><br/> minOccurs = "0"<br/><br/> domyślne = "3" |**xs:int** |Liczba ramek odwołania w GOP. |
| **EntropyMode**<br/><br/> minOccurs = "0"<br/><br/> domyślne = "Cabac" |**xs:String** |Może być jednym z hello następujące wartości: **Cabac** i **Cavlc**. |
| **Szybkość klatek**<br/><br/> minOccurs = "0" |Liczba wymierna |Określa szybkość klatek hello danych wyjściowych hello wideo. Użyj domyślnej "0/1" toolet hello kodera Użyj hello samej ramce szybkości jako danych wejściowych hello wideo. Dozwolone wartości są oczekiwanego toobe wspólnej szybkości odtwarzania wideo, jak pokazano poniżej. Jednak wszystkie prawidłowe wymierna jest dozwolone. Na przykład 1/1 byłoby 1 kl. / s i jest prawidłowy.<br/><br/> -12/1 (12 kl. / s)<br/><br/> -15/1 (15 kl. / s)<br/><br/> -24/1 (24 kl. / s)<br/><br/> 24000/1001 (23.976 kl. / s)<br/><br/> -25/1 (25 kl. / s)<br/><br/>  -30/1 (30 kl. / s)<br/><br/> 30000/1001 (29,97 kl. / s) <br/> <br/>**Uwaga** w przypadku tworzenia niestandardowego ustawienie wstępne kodowania wielu szybkości transmisji bitów, następnie wszystkie warstwy hello ustawienia wstępnego **musi** Użyj hello takie same wartości szybkość klatek.|
| **AdaptiveBFrame**<br/><br/> minOccurs = "0" |**xs:Boolean** |Kopiowanie z kodera multimediów Azure |
| **Wycinków**<br/><br/> minOccurs = "0"<br/><br/> domyślne = "0" |**xs:int** |Określa liczbę wycinków ramki jest podzielony na. Zaleca się używanie domyślnego. |

## <a name="AACAudio"></a>AACAudio
 Zawiera sekwencję hello następujące elementy i grupy.  

 Aby uzyskać więcej informacji na temat AAC, zobacz [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding).  

### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Profil**<br/><br/> minOccurs = "0"<br/><br/> domyślne = "AACLC" |**xs:String** |Może być jednym z hello następujące wartości: **AACLC**, **HEAACV1**, lub **HEAACV2**. |

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Warunek** |**xs:String** |tooforce hello koder tooproduce element zawartości zawierający dyskretnej ścieżki audio, gdy dane wejściowe nie zawierają żadnych audio, określ wartość "InsertSilenceIfNoAudio" hello.<br/><br/> Domyślnie w przypadku wysłania koder toohello wejściowego, który zawiera tylko wideo i audio nie następnie zawartości wyjściowej hello będzie zawierać pliki, które zawierają dane tylko wideo. Niektóre odtwarzacze może nie być możliwe toohandle takich danych wyjściowych strumieni. W tym scenariuszu, można użyć tego ustawienia tooforce hello koder tooadd wyjściowego toohello dyskretnej ścieżki audio. |

### <a name="groups"></a>Grupy
| Dokumentacja | Opis |
| --- | --- |
| [AudioGroup](media-services-mes-schema.md#AudioGroup)<br/><br/> minOccurs = "0" |Zobacz opis [AudioGroup](media-services-mes-schema.md#AudioGroup) tooknow hello odpowiednią liczbę kanałów, częstotliwość próbkowania i szybkość transmisji bitów, które można ustawić dla każdego profilu. |

## <a name="AudioGroup"></a>AudioGroup
Aby uzyskać szczegóły, jakie wartości są prawidłowe dla każdego profilu zobacz poniższą tabelą "Szczegóły kodera-dekodera Audio" hello.  

### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Kanały**<br/><br/> minOccurs = "0" |**xs:int** |Witaj liczba kanałów audio zakodowane. Witaj poniżej przedstawiono prawidłowe opcje: 1, 2, 5, 6, 8.<br/><br/> Domyślne: 2. |
| **SamplingRate**<br/><br/> minOccurs = "0" |**xs:int** |częstotliwość próbkowania audio Hello, określona w Hz. |
| **Szybkość transmisji bitów**<br/><br/> minOccurs = "0" |**xs:int** |używane podczas kodowania hello audio określonej w KB/s Hello szybkości transmisji bitów. |

### <a name="audio-codec-details"></a>Szczegóły kodera-dekodera audio
Kodera-dekodera audio|Szczegóły  
-----------------|---  
**AACLC**|1:<br/><br/> -11025: 8 &lt;= szybkości transmisji bitów &lt; 16<br/><br/> -12000: 8 &lt;= szybkości transmisji bitów &lt; 16<br/><br/> -16000: 8 &lt;= szybkości transmisji bitów &lt;32<br/><br/>-22050: 24 &lt;= szybkości transmisji bitów &lt; 32<br/><br/> -24000: 24 &lt;= szybkości transmisji bitów &lt; 32<br/><br/> -32000: 32 &lt;= szybkości transmisji bitów &lt;= 192<br/><br/> -44100: 56 &lt;= szybkości transmisji bitów &lt;= 288<br/><br/> -48000: 56 &lt;= szybkości transmisji bitów &lt;= 288<br/><br/> -88200: 128 &lt;= szybkości transmisji bitów &lt;= 288<br/><br/> -96000: 128 &lt;= szybkości transmisji bitów &lt;= 288<br/><br/> 2:<br/><br/> -11025: 16 &lt;= szybkości transmisji bitów &lt; 24<br/><br/> -12000: 16 &lt;= szybkości transmisji bitów &lt; 24<br/><br/> -16000: 16 &lt;= szybkości transmisji bitów &lt; 40<br/><br/> -22050: 32 &lt;= szybkości transmisji bitów &lt; 40<br/><br/> -24000: 32 &lt;= szybkości transmisji bitów &lt; 40<br/><br/> -32000: 40 &lt;= szybkości transmisji bitów &lt;= 384<br/><br/> -44100: 96 &lt;= szybkości transmisji bitów &lt;= 576<br/><br/> -48000: 96 &lt;= szybkości transmisji bitów &lt;= 576<br/><br/> -88200: 256 &lt;= szybkości transmisji bitów &lt;= 576<br/><br/> -96000: 256 &lt;= szybkości transmisji bitów &lt;= 576<br/><br/> 5/6:<br/><br/> -32000: 160 &lt;= szybkości transmisji bitów &lt;= 896<br/><br/> -44100: 240 &lt;= szybkości transmisji bitów &lt;= 1024<br/><br/> -48000: 240 &lt;= szybkości transmisji bitów &lt;= 1024<br/><br/> -88200: 640 &lt;= szybkości transmisji bitów &lt;= 1024<br/><br/> -96000: 640 &lt;= szybkości transmisji bitów &lt;= 1024<br/><br/> 8:<br/><br/> -32000: 224 &lt;= szybkości transmisji bitów &lt;= 1024<br/><br/> -44100: 384 &lt;= szybkości transmisji bitów &lt;= 1024<br/><br/> -48000: 384 &lt;= szybkości transmisji bitów &lt;= 1024<br/><br/> -88200: 896 &lt;= szybkości transmisji bitów &lt;= 1024<br/><br/> -96000: 896 &lt;= szybkości transmisji bitów &lt;= 1024  
**HEAACV1**|1:<br/><br/> -22050 b: szybkości transmisji bitów = 8<br/><br/> -24000: 8 &lt;= szybkości transmisji bitów &lt;= 10<br/><br/> -32000: 12 &lt;= szybkości transmisji bitów &lt;= 64<br/><br/> -44100: 20 &lt;= szybkości transmisji bitów &lt;= 64<br/><br/> -48000: 20 &lt;= szybkości transmisji bitów &lt;= 64<br/><br/> -88200 b: szybkości transmisji bitów = 64<br/><br/> 2:<br/><br/> -32000: 16 &lt;= szybkości transmisji bitów &lt;= 128<br/><br/> -44100: 16 &lt;= szybkości transmisji bitów &lt;= 128<br/><br/> -48000: 16 &lt;= szybkości transmisji bitów &lt;= 128<br/><br/> -88200: 96 &lt;= szybkości transmisji bitów &lt;= 128<br/><br/> -96000: 96 &lt;= szybkości transmisji bitów &lt;= 128<br/><br/> 5/6:<br/><br/> -32000: 64 &lt;= szybkości transmisji bitów &lt;= 320<br/><br/> -44100: 64 &lt;= szybkości transmisji bitów &lt;= 320<br/><br/> -48000: 64 &lt;= szybkości transmisji bitów &lt;= 320<br/><br/> -88200: 256 &lt;= szybkości transmisji bitów &lt;= 320<br/><br/> -96000: 256 &lt;= szybkości transmisji bitów &lt;= 320<br/><br/> 8:<br/><br/> -32000: 96 &lt;= szybkości transmisji bitów &lt;= 448<br/><br/> -44100: 96 &lt;= szybkości transmisji bitów &lt;= 448<br/><br/> -48000: 96 &lt;= szybkości transmisji bitów &lt;= 448<br/><br/> -88200: 384 &lt;= szybkości transmisji bitów &lt;= 448<br/><br/> -96000: 384 &lt;= szybkości transmisji bitów &lt;= 448  
**HEAACV2**|2:<br/><br/> -22050: 8 &lt;= szybkości transmisji bitów &lt;= 10<br/><br/> -24000: 8 &lt;= szybkości transmisji bitów &lt;= 10<br/><br/> -32000: 12 &lt;= szybkości transmisji bitów &lt;= 64<br/><br/> -44100: 20 &lt;= szybkości transmisji bitów &lt;= 64<br/><br/> -48000: 20 &lt;= szybkości transmisji bitów &lt;= 64<br/><br/> -88200: 64 &lt;= szybkości transmisji bitów &lt;= 64  
  

## <a name="Clip"></a>Clip
### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Czas rozpoczęcia** |**DURATION** |Określa czas rozpoczęcia hello prezentacji. wartość StartTime Hello musi toomatch hello bezwzględną znacznikami czasu hello wejściowy plik wideo. Na przykład, jeśli hello pierwszej ramki hello wejściowy plik wideo ma sygnaturę 12:00:10.000, a następnie wartość StartTime powinna być co najmniej 12:00:10.000 lub nowszej. |
| **Czas trwania** |**DURATION** |Określa czas trwania hello prezentacji (na przykład wygląd nakładka wideo hello). |

## <a name="Output"></a>Dane wyjściowe
### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Nazwa pliku** |**xs:String** |Nazwa Hello hello pliku wyjściowego.<br/><br/> Można użyć makra opisanego w hello następujące nazwy plików wyjściowych hello toobuild tabeli. Na przykład:<br/><br/> **"Wyjście": [{"FileName": "{nazwę bazową}*{rozpoznawania}*plik MP4 {szybkości transmisji bitów}", "Format": {"Type": "MP4Format"}}] ** |

### <a name="macros"></a>Makra
| Makra | Opis |
| --- | --- |
| **{Nazwę bazową}** |Jeśli przeprowadzasz kodowanie VoD hello {nazwę bazową} jest hello najpierw 32 znaków hello AssetFile.Name właściwości pliku podstawowego hello w hello zasobów wejściowych.<br/><br/> Jeśli zasobów wejściowych hello jest archiwum na żywo, następnie hello {nazwę bazową} jest pochodną hello trackName atrybutów w manifeście serwera hello. Jeśli przesyłasz subclip zadania przy użyciu hello TopBitrate, podobnie jak w: "< VideoStream\>TopBitrate < / VideoStream\>", plik wyjściowy hello zawiera wideo, a następnie hello {nazwę bazową} jest hello pierwsze 32 znaki trackName hello z hello warstwę wideo z hello najwyższej szybkości transmisji bitów.<br/><br/> Jeśli zamiast tego są przesyłania zadania subclip przy użyciu wszystkich szybkości wprowadzania transmisji hello bitów, takich jak "< VideoStream\>* < / VideoStream\>", plik wyjściowy hello zawiera wideo, a następnie {nazwę bazową} hello jest najpierw 32 znaków hello trackName programu Witaj odpowiednia warstwa wideo. |
| **{Koder-dekoder}** |Mapuje zbyt "H264" wideo i "AAC" dla audio. |
| **{Szybkości transmisji bitów}** |Witaj docelowego wideo szybkości transmisji bitów zawiera hello pliku wyjściowego audio i wideo lub audio transmisji bitów docelowej, jeśli plik wyjściowy hello zawiera tylko audio. wartość Hello używana jest hello szybkości transmisji bitów w KB/s. |
| **{Kanału}** |Liczba kanałów audio, jeśli plik hello zawiera audio. |
| **{Szerokość}** |Szerokość hello wideo, w pikselach, w pliku wyjściowym hello, jeśli plik hello zawiera wideo. |
| **{Wysokość}** |Wysokość hello wideo, w pikselach, w pliku wyjściowym hello, jeśli plik hello zawiera wideo. |
| **{Rozszerzenia}** |Dziedziczy hello właściwości "Type" dla pliku wyjściowego hello. Nazwa pliku wyjściowego Hello będzie mieć rozszerzenie, które jest jednym z: "mp4", "ts", "jpg", "png" lub "bmp". |
| **{Index}** |Obowiązkowe dla miniatur. Powinien mieć tylko występuje jeden raz. |

## <a name="Video"></a>Wideo (typ złożony dziedziczy koder-dekoder)
### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Rozpocznij** |**xs:String** | |
| **Krok** |**xs:String** | |
| **Zakres** |**xs:String** | |
| **PreserveResolutionAfterRotation** |**xs:Boolean** |Aby szczegółowe informacje, zobacz hello następujących sekcji: [PreserveResolutionAfterRotation](media-services-mes-schema.md#PreserveResolutionAfterRotation) |

### <a name="PreserveResolutionAfterRotation"></a>PreserveResolutionAfterRotation
Zalecane jest toouse hello PreserveResolutionAfterRotation flagi w połączeniu z wartościami rozpoznawania wyrażony w procentach (Width = "100%", wysokość = "100%").  

Domyślnie program hello kodowania ustawień rozpoznawania (szerokość, wysokość) w hello predefiniowane Media Encoder Standard (rynkowej) są przeznaczone dla plików wideo za pomocą 0 stopni. Na przykład, jeśli wejściowy plik wideo jest 1280 x 720 z zero stopni, następnie hello domyślne ustawienia sprawdź, czy dane wyjściowe hello ma hello tego samego rozwiązania. Obraz poniżej jest widoczny.  

![MESRoation1](./media/media-services-shemas/media-services-mes-roation1.png) 

Jednakże oznacza to, że jeśli wejściowy plik wideo hello została przechwycona z obrotu różna od zera (np.) na smartfonie lub tablecie przechowywanych w pionie), następnie rynkowej domyślnie zastosuje hello kodowania rozpoznawania toohello ustawienia (szerokość, wysokość) danych wejściowych wideo, a następnie kompensacji hello obrotu. Na przykład zobacz hello obraz poniżej. Hello ustawienie wstępne używa Width = "100%", wysokość = "100%", który rynkowej interpretowane jako wymagające hello dane wyjściowe toobe 1280 pikseli szerokości i wysokości 720 pikseli. Po obracanie hello wideo, ją następnie zmniejsza toofit obraz powitania w danym przedziale wiodące obszarów toopillar pole na powitania lewy i prawy.  

![MESRoation2](./media/media-services-shemas/media-services-mes-roation2.png) 

Jeśli hello powyżej nie jest konieczne hello zachowanie, a następnie umożliwia użycie hello flagi PreserveResolutionAfterRotation i ustaw dla niej zbyt "prawda" (wartość domyślna to "false"). Dlatego jeśli Twoje wstępnie zdefiniowane ma szerokość = "100%", wysokość = "100%" i ustaw zbyt "prawda", wejściowy plik wideo, czyli 1280 pikseli szerokości i wysokości o 90 stopni 720 pikseli zostanie utworzenie danych wyjściowych z zero stopni, ale 720 pikseli szerokości i 1280 PreserveResolutionAfterRotation wysokości pikseli. Obraz powitania poniżej jest widoczny.  

![MESRoation3](./media/media-services-shemas/media-services-mes-roation3.png) 

## <a name="FormatGroup"></a>FormatGroup (grupa)
### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **BmpFormat** |**BmpFormat** | |
| **PngFormat** |**PngFormat** | |
| **JpgFormat** |**JpgFormat** | |

## <a name="BmpLayer"></a>BmpLayer
### <a name="element"></a>Element
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Szerokość**<br/><br/> minOccurs = "0" |**xs:int** | |
| **Wysokość**<br/><br/> minOccurs = "0" |**xs:int** | |

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Warunek** |**xs:String** | |

## <a name="PngLayer"></a>PngLayer
### <a name="element"></a>Element
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Szerokość**<br/><br/> minOccurs = "0" |**xs:int** | |
| **Wysokość**<br/><br/> minOccurs = "0" |**xs:int** | |

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Warunek** |**xs:String** | |

## <a name="JpgLayer"></a>JpgLayer
### <a name="element"></a>Element
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Szerokość**<br/><br/> minOccurs = "0" |**xs:int** | |
| **Wysokość**<br/><br/> minOccurs = "0" |**xs:int** | |
| **Jakość**<br/><br/> minOccurs = "0" |**xs:int** |Prawidłowe wartości: 1(worst)-100(best) |

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Warunek** |**xs:String** | |

## <a name="PngLayers"></a>PngLayers
### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **PngLayer**<br/><br/> minOccurs = maxOccurs "0" = "unbounded" |[PngLayer](media-services-mes-schema.md#PngLayer) | |

## <a name="BmpLayers"></a>BmpLayers
### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **BmpLayer**<br/><br/> minOccurs = maxOccurs "0" = "unbounded" |[BmpLayer](media-services-mes-schema.md#BmpLayer) | |

## <a name="JpgLayers"></a>JpgLayers
### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **JpgLayer**<br/><br/> minOccurs = maxOccurs "0" = "unbounded" |[JpgLayer](media-services-mes-schema.md#JpgLayer) | |

## <a name="BmpImage"></a>BmpImage (typ złożony dziedziczy wideo)
### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs = "0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Warstwy PNG |

## <a name="JpgImage"></a>JpgImage (typ złożony dziedziczy wideo)
### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs = "0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Warstwy PNG |

## <a name="PngImage"></a>PngImage (typ złożony dziedziczy wideo)
### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs = "0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Warstwy PNG |

## <a name="examples"></a>Przykłady
Zobacz przykłady XML ustawień, które są tworzone na podstawie tego schematu, zobacz [ustawienia zadania rynkowej (Media Encoder Standard)](media-services-mes-presets-overview.md).

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

