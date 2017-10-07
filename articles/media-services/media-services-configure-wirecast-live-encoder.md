---
title: "aaaConfigure hello toosend koder Telestream Wirecast strumień na żywo o pojedynczej szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooconfigure hello Wirecast live toosend kodera kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a>Użyj hello Wirecast koder toosend strumień na żywo o pojedynczej szybkości transmisji bitów
> [!div class="op_single_selector"]
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [Elemental na żywo](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

W tym temacie przedstawiono sposób tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo toosend kodera na żywo.  Aby uzyskać więcej informacji, zobacz [Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Ten samouczek pokazuje, jak toomanage usługi Azure Media Services (AMS) za pomocą narzędzia Azure Media Services Explorer (AMSE). To narzędzie jest uruchamiane tylko na komputerze z systemem Windows. Mac lub Linux, za pomocą hello Azure portalu toocreate [kanałów](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) i [programy](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Wymagania wstępne
* [Tworzenie konta usługi Azure Media Services](media-services-portal-create-account.md)
* Upewnij się, brak punktu końcowego przesyłania strumieniowego uruchomiona. Aby uzyskać więcej informacji, zobacz [zarządzanie punktami końcowymi przesyłania strumieniowego w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md)
* Zainstaluj najnowszą wersję hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) narzędzia.
* Uruchom narzędzie hello i Połącz konto tooyour AMS.

## <a name="tips"></a>Porady
* Jeśli to możliwe, użyj połączenia internetowego hardwired.
* Regułą podczas określania wymaganiach odnośnie do przepustowości jest hello toodouble przesyłania strumieniowego szybkości transmisji bitów. Chociaż nie jest to wymagane, może pomóc zmniejszyć wpływ hello sieci przeciążona.
* Gdy za pomocą oprogramowania na podstawie koderów, zamknij wszystkie zbędne programy.

## <a name="create-a-channel"></a>Tworzenie kanału
1. Narzędzie AMSE hello Przejdź toohello **Live** karcie, a następnie kliknij prawym przyciskiem myszy w obszarze kanału hello. Wybierz **Utwórz kanał...** z hello menu.

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. Określ nazwę kanału hello pole opisu jest opcjonalne. W ustawieniach kanału, wybierz **standardowe** dla hello opcji kodowanie na żywo z hello wprowadzania ustawiony protokół zbyt**RTMP**. Możesz pozostawić wszystkie inne ustawienia, ponieważ jest.

    Upewnij się, że hello **Start hello nowy kanał teraz** jest zaznaczone.

3. Kliknij przycisk **utworzyć kanał**.

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> kanał Hello może zająć toostart 20 minut.
>
>

Podczas uruchamiania kanału hello można [skonfigurować koder hello](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).

> [!IMPORTANT]
> Należy pamiętać, że rozliczanie zaczyna się jak kanału przechodzi do stanu gotowości. Aby uzyskać więcej informacji, zobacz [stanów kanału](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_wirecast_rtmp></a>Skonfiguruj hello koder Telestream Wirecast
W tym samouczek hello są używane następujące ustawienia danych wyjściowych. Hello pozostałej części tej sekcji opisano kroki konfiguracji szczegółowo.

**Wideo**:

* Koder-dekoder: H.264
* Profil: Wysoki (poziom 4.0)
* Szybkość transmisji bitów: 5000 KB/s
* Klatki kluczowej: 2 sekundy (60 sekund)
* Szybkość klatek: 30

**Audio**:

* Koder-dekoder: AAC (LC —)
* Szybkość transmisji bitów: 192 kb/s
* Częstotliwość próbkowania: 44,1 kHz

### <a name="configuration-steps"></a>Kroki konfiguracji
1. Otwórz aplikację Telestream Wirecast hello na powitania maszyna nie jest używane i skonfigurować do przesyłania strumieniowego RTMP.
2. Konfigurowanie danych wyjściowych hello przechodząc toohello **dane wyjściowe** kartę i wybierając **ustawienia wyjściowej...** .

    Upewnij się, że hello **miejsce docelowe danych wyjściowych** ustawiono zbyt**serwera RTMP**.
3. Kliknij przycisk **OK**.
4. Na stronie ustawień hello ustawić hello **docelowego** toobe pola **usługi Azure Media Services**.

    Witaj profilu kodowanie jest wstępnie zaznaczona zbyt**H.264 Azure 720 p 16:9 (1280 x 720)**. toocustomize te ustawienia, wybierz opcję hello koło zębate ikonę toohello rogu hello listy rozwijanej, a następnie wybierz **nowe ustawienie wstępne**.

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. Skonfiguruj ustawienia kodera.

    Hello nazwy ustawienia wstępnego i sprawdź, czy hello następujących zalecanych ustawień:

    **Wideo**

   * Koder: MainConcept H.264
   * Klatek na sekundę: 30
   * Średnia szybkość transmisji bitów: 5000 kbitów na sekundę (może być określany na podstawie ograniczenia sieci)
   * Profil: Main
   * Klatki co: 60 klatek

    **Audio**

   * Docelowa szybkość transmisji bitów: 192 kbitów/s
   * Częstotliwość próbkowania: 44 100 kHz

     ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. Naciśnij klawisz **zapisać**.

    pola Encoding Hello ma teraz hello nowo utworzony profil dostępne do wyboru.

    Upewnij się, że wybrano hello nowy profil.
7. Pobierz hello kanał wejściowy adres URL w kolejności tooassign on toohello Wirecast **punktu końcowego protokołu RTMP**.

    Przejdź wstecz toohello narzędzie AMSE i sprawdzić stan ukończenia hello kanału. Po hello stan został zmieniony z **uruchamianie** za**systemem**, możesz uzyskać hello wejściowy adres URL.

    Gdy kanał hello jest uruchomiona, kliknij prawym przyciskiem myszy nazwę kanału hello, przechodzenia toohover za pośrednictwem **tooclipboard kopia danych wejściowych URL** , a następnie wybierz **podstawowego adresu URL danych wejściowych**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. W hello Wirecast **ustawienia wyjściowej** okna, Wklej te informacje w hello **adres** pole hello dane wyjściowe sekcji, a następnie przypisz nazwę strumienia.

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. Kliknij przycisk **OK**.
2. Na powitania głównego **Wirecast** Sprawdź źródeł danych wejściowych dla audio i wideo są gotowe, a następnie naciśnij **strumienia** w hello lewego górnego rogu.

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> Przed kliknięciem przycisku **strumienia**, możesz **musi** upewnij się, że kanał hello jest gotowy.
> Sprawdź także, czy nie tooleave hello kanału w stanie Gotowe bez wprowadzania wkład źródła danych przez czas dłuższy niż > 15 minut.
>
>

## <a name="test-playback"></a>Podczas odtwarzania testu

Przejdź narzędzie AMSE toohello, a następnie kliknij prawym przyciskiem myszy toobe kanału hello przetestowane. Z hello menu, umieść kursor nad **hello odtwarzania podglądu** i wybierz **z usługi Azure Media Player**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

Czy strumienia hello znajduje się w hello player, koder hello został tooAMS tooconnect poprawnie skonfigurowana.

Jeśli błąd kanału hello należy toobe resetowania i koder zmienić ustawienia. Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.  

## <a name="create-a-program"></a>Utwórz program
1. Po potwierdzeniu kanału odtwarzania, tworzenia programu. W obszarze hello **Live** narzędzia AMSE hello, kliknij prawym przyciskiem myszy w obszarze program hello i wybierz **utworzyć nowy Program**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. Nazwy hello program i w razie potrzeby dostosuj hello **długość okna archiwum** (domyślne ustawienia too4 godzin, w których). Można także określić miejsce przechowywania lub pozostaw domyślne hello.  
3. Sprawdź hello **Start hello Program teraz** pole.
4. Kliknij przycisk **utworzyć Program**.  

   >[!NOTE]
   >Tworzenie programu zajmuje mniej czasu niż tworzenie kanału.
       
5. Po uruchomieniu hello program potwierdzić odtwarzania przez kliknięcie prawym przyciskiem myszy hello program i przechodząc zbyt**programach hello odtwarzania** , a następnie wybierając **z usługi Azure Media Player**.  
6. Po potwierdzeniu, kliknij prawym przyciskiem myszy hello program ponownie i wybierz **skopiuj hello adresu URL danych wyjściowych tooClipboard** (lub pobrać te informacje z hello **programu informacji i ustawień** opcji z hello menu).

strumień Hello jest teraz gotowy toobe osadzony w odtwarzacza lub odbiorcami tooan rozproszone na żywo wyświetlanie.  

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
