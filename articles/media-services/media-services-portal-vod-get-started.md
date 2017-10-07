---
title: "wprowadzenie do dostarczania VoD przy użyciu portalu Azure hello aaaGet | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki wdrażania podstawowej usługi dostarczania zawartości wideo na żądanie (VoD) z aplikacją Azure Media Services (AMS) przy użyciu portalu Azure hello hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a>Wprowadzenie do dostarczania zawartości na żądanie przy użyciu hello portalu Azure
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Ten samouczek przedstawia kroki wdrażania podstawowej usługi dostarczania zawartości wideo na żądanie (VoD) z aplikacją Azure Media Services (AMS) przy użyciu portalu Azure hello hello.

## <a name="prerequisites"></a>Wymagania wstępne
Samouczek hello toocomplete wymagane są następujące Hello:

* Konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Konto usługi Media Services. Zobacz toocreate konto usługi Media Services [jak tooCreate konta usługi Media Services](media-services-portal-create-account.md).

W tym samouczku opisano hello następujące zadania:

1. Uruchamianie punktu końcowego przesyłania strumieniowego.
2. Ładowanie pliku wideo.
3. Kodowanie pliku źródłowego hello do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów.
4. Publikowanie zawartości hello i get przesyłania strumieniowego i pobierania progresywnego adresów URL.  
5. Odtwarzanie zawartości.

## <a name="start-streaming-endpoints"></a>Uruchamianie punktu końcowego przesyłania strumieniowego 

Podczas pracy w usłudze Azure Media Services jednym z hello najbardziej typowych scenariuszy jest dostarczanie plików wideo przy użyciu przesyłania strumieniowego adaptacyjną szybkością transmisji bitów. Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver adaptacyjnej szybkości bitowej MP4 zakodowane zawartości w formatach transmisji strumieniowej obsługiwanych przez usługi Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, bez konieczności toostore wstępnie umieszczone wersje każdego z tych formatach.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 

toostart hello punktu końcowego przesyłania strumieniowego, hello następujące:

1. Zaloguj się w hello [portalu Azure](https://portal.azure.com/).
2. W oknie Ustawienia powitania kliknij punkty końcowe przesyłania strumieniowego. 
3. Kliknij przycisk domyślny hello punktu końcowego przesyłania strumieniowego. 

    zostanie wyświetlone okno Szczegóły punktu KOŃCOWEGO przesyłania STRUMIENIOWEGO domyślne Hello.

4. Kliknij ikonę Start hello.
5. Kliknij przycisk toosave przycisk Zapisz hello zmiany.

## <a name="upload-files"></a>Przekazywanie plików
toostream wideo przy użyciu usługi Azure Media Services, potrzebne tooupload hello źródłowe pliki wideo, zakodować je do wielokrotnych szybkości transmisji bitów i opublikuj hello wynik. pierwszym krokiem Hello zostało opisane w tej sekcji. 

1. W hello **ustawienie** okna, kliknij przycisk **zasoby**.
   
    ![Przekazywanie plików](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. Kliknij przycisk hello **przekazać** przycisku.
   
    Witaj **przekazywanie zawartości wideo** zostanie wyświetlone okno.
   
   > [!NOTE]
   > Nie ma żadnego limitu rozmiaru pliku.
   > 
   > 
3. Przeglądaj toohello potrzeby wideo na komputerze, zaznacz go i kliknij przycisk OK.  
   
    rozpocznie się przekazywanie Hello, aby zobaczyć postęp hello pod nazwą pliku hello.  

Po ukończeniu przekazywania hello Zobacz hello nowy element zawartości na liście hello **zasoby** okna. 

## <a name="encode-assets"></a>Kodowanie elementów zawartości

Podczas pracy w usłudze Azure Media Services jednym z hello najbardziej typowych scenariuszy jest dostarczanie przesyłania strumieniowego klientów tooyour adaptacyjną szybkością transmisji bitów. Usługa Media Services obsługuje hello następujące technologie przesyłania strumieniowego adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare pliki wideo do przesyłania strumieniowego o adaptacyjnej szybkości bitowej, należy tooencode źródła wideo do plików o różnych szybkościach transmisji bitów. Należy używać hello **Media Encoder Standard** tooencode koder wideo.  

Media Services udostępnia również funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver Twojego MP4s wielokrotnej szybkości transmisji bitów w następujących formatów przesyłania strumieniowego hello: MPEG DASH, HLS, Smooth Streaming, bez konieczności toorepackage w tych formatach. Dzięki funkcji dynamicznego tworzenia pakietów, wystarczy toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services, tworzy i służy hello właściwą odpowiedź na podstawie żądań klienta.

tootake korzyści z dynamicznego tworzenia pakietów, należy tooencode pliku źródłowego do zestawu plików MP4 wielokrotnej szybkości transmisji bitów (kroki kodowania hello przedstawiono w dalszej części tej sekcji).

### <a name="toouse-hello-portal-tooencode"></a>tooencode portalu hello toouse
W tej sekcji opisano kroki hello może zająć tooencode zawartości przy użyciu standardu Media Encoder Standard.

1. W hello **ustawienia** wybierz **zasoby**.  
2. W hello **zasoby** okna, wybierz hello zasobów chcesz tooencode.
3. Naciśnij klawisz hello **Koduj** przycisku.
4. W hello **kodowanie elementu zawartości** okna, hello wybierz procesor "Media Encoder Standard" oraz ustawienie wstępne. Aby uzyskać informacje o ustawieniach wstępnych, zobacz [Automatyczne generowanie drabiny szybkości transmisji bitów](media-services-autogen-bitrate-ladder-with-mes.md) i [Ustawienia wstępne zadań usługi MES](media-services-mes-presets-overview.md). Jeśli planujesz toocontrol które kodowania ustawienia wstępnego pamiętać to: koniecznie tooselect hello ustawienia wstępnego najbardziej odpowiednie dla wejściowego pliku wideo. Na przykład, jeśli znasz wejściowy plik wideo ma rozdzielczość 1920 x 1080 pikseli, następnie można hello "H264 szybkość transmisji bitów 1080p" wstępnie zdefiniowane. Jeśli wideo jest w niskiej rozdzielczości (640 x 360), nie używaj ustawienia wstępnego „Wielokrotna szybkość transmisji bitów H264 1080p”.
   
   Aby ułatwić zarządzanie istnieje możliwość edytowania hello nazwę zawartości wyjściowej hello i nazwę hello hello zadania.
   
   ![Kodowanie elementów zawartości](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. Kliknij przycisk **Utwórz**.

### <a name="monitor-encoding-job-progress"></a>Monitorowanie postępu zadania kodowania
postęp hello toomonitor hello kodowanie zadania, kliknij przycisk **ustawienia** (u góry hello hello strony), a następnie wybierz **zadania**.

![Zadania](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a>Publikowanie zawartości
tooprovide użytkownika przy użyciu adresu URL, który może być używane toostream lub pobierania zawartości, należy najpierw należy zbyt "Publikuj" zawartości, tworząc Lokalizator. Lokalizatory zapewniają toofiles dostępu do zawartych w hello zasobów. Usługa Media Services obsługuje dwa typy lokalizatorów: 

* Przesyłanie strumieniowe lokalizatory (OnDemandOrigin) używane do adaptacyjnego przesyłania strumieniowego (na przykład toostream MPEG DASH, HLS lub Smooth Streaming). toocreate Lokalizator przesyłania strumieniowego zawartości musi zawierać plik .ism. 
* Progresywne lokalizatory (SAS) używane do dostarczania plików wideo przy użyciu pobierania progresywnego.

Adresu URL przesyłania strumieniowego ma hello zgodny z formatem i może być używany tooplay Smooth Streaming zasoby.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

Dołącz toobuild jako HLS URL, przesyłania strumieniowego (format = m3u8-aapl) toohello adresu URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

Dołącz toobuild jako MPEG DASH URL, przesyłania strumieniowego (format = mpd-time-csf) toohello adresu URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


Adres URL SAS ma hello zgodny z formatem.

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> Jeśli używasz hello portalu toocreate lokalizatorów przed marcem 2015 r., zostały utworzone lokalizatory z okresem wygaśnięcia dwa lata.  
> 
> 

tooupdate Data wygaśnięcia na lokalizatorze użyj [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) lub [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) interfejsów API. Po zaktualizowaniu daty wygaśnięcia lokalizatora SAS hello zmienia hello adresu URL.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello portalu toopublish zasobów
toouse hello portalu toopublish zasobów hello następujące:

1. Wybierz kolejno pozycje **Ustawienia** > **Elementy zawartości**.
2. Wybierz hello zasobów, które mają toopublish.
3. Kliknij przycisk hello **publikowania** przycisku.
4. Wybierz typ lokalizatora hello.
5. Kliknij przycisk **Dodaj**.
   
    ![Publikowanie](./media/media-services-portal-vod-get-started/media-services-publish1.png)

adres URL Hello jest dodawany listy toohello **publikowane adresy URL**.

## <a name="play-content-from-hello-portal"></a>Odtwarzanie zawartości z portalu hello
Witaj Azure portal udostępnia odtwarzacz zawartości możesz za pomocą tootest wideo.

Kliknij żądany hello wideo, a następnie kliknij przycisk hello **odtwarzanie** przycisku.

![Publikowanie](./media/media-services-portal-vod-get-started/media-services-play.png)

Zagadnienia do rozważenia:

* toobegin przesyłania strumieniowego, uruchom uruchomionych hello **domyślne** punktu końcowego przesyłania strumieniowego.
* Upewnij się, że hello wideo został opublikowany.
* To **Media player** odtwarza z domyślnego hello punktu końcowego przesyłania strumieniowego. Jeśli chcesz, aby tooplay z innych niż domyślne przesyłania strumieniowego punktu końcowego, kliknij adres URL hello toocopy i użyć innego odtwarzacza. (np. [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)).

## <a name="next-steps"></a>Następne kroki
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

