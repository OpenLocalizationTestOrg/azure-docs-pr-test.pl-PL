---
title: "aaaConfigure hello NewTek TriCaster koder toosend strumień na żywo o pojedynczej szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooconfigure hello Tricaster live toosend kodera kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a>Użyj hello NewTek TriCaster koder toosend strumień na żywo o pojedynczej szybkości transmisji bitów
> [!div class="op_single_selector"]
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Elemental na żywo](media-services-configure-elemental-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

W tym temacie przedstawiono sposób tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo toosend kodera na żywo. Aby uzyskać więcej informacji, zobacz [Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Ten samouczek pokazuje, jak toomanage usługi Azure Media Services (AMS) za pomocą narzędzia Azure Media Services Explorer (AMSE). To narzędzie jest uruchamiane tylko na komputerze z systemem Windows. Mac lub Linux, za pomocą hello Azure portalu toocreate [kanałów](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) i [programy](media-services-portal-creating-live-encoder-enabled-channel.md).

> [!NOTE]
> Podczas wysyłania w udziale za pomocą Tricaster źródła kanałami tooAMS, obsługującymi kodowanie na żywo, może istnieć błędami występującymi audio/wideo w zdarzenia na żywo w przypadku określonych funkcji Tricaster, takie jak szybka Wycinanie między źródła danych lub przełączanie z typu . Witaj AMS zespołu działa w rozwiązaniu tych problemów, do tego czasu jest zaleca toouse te funkcje.
>
>

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

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. Określ nazwę kanału hello pole opisu jest opcjonalne. W ustawieniach kanału, wybierz **standardowe** dla hello opcji kodowanie na żywo z hello wprowadzania ustawiony protokół zbyt**RTMP**. Możesz pozostawić wszystkie inne ustawienia, ponieważ jest.

    Upewnij się, że hello **Start hello nowy kanał teraz** jest zaznaczone.

3. Kliknij przycisk **utworzyć kanał**.

   ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> kanał Hello może zająć toostart 20 minut.
>
>

Podczas uruchamiania kanału hello można [skonfigurować koder hello](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).

> [!IMPORTANT]
> Należy pamiętać, że rozliczanie zaczyna się jak kanału przechodzi do stanu gotowości. Aby uzyskać więcej informacji, zobacz [stanów kanału](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_tricaster_rtmp></a>Skonfiguruj hello NewTek TriCaster kodera
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
1. Utwórz nową **NewTek TriCaster** projektu w zależności od tego, jakie wideo źródło danych wejściowych jest używany.
2. Raz w ramach tego projektu, Znajdź hello **strumienia** przycisk, a następnie kliknij przycisk hello koło zębate ikonę dalej tooit tooaccess hello strumienia menu konfiguracji.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. Po otwarciu hello menu, kliknij przycisk **nowy** hello połączenia pozycji. Po wyświetleniu monitu dla typu połączenia hello, wybierz **Adobe Flash**.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. Kliknij przycisk **OK**.
5. Teraz można zaimportować profil FMLE klikając hello strzałkę listy rozwijanej w obszarze **przesyłania strumieniowego profilu** i przechodząc zbyt**Przeglądaj**.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. Przejdź toowhere hello skonfigurowane FMLE profil został zapisany.
7. Wybierz go, a następnie naciśnij klawisz **OK**.

    Po przekazaniu plików profilu hello kontynuować toohello następnego kroku.
8. Pobierz hello kanał wejściowy adres URL w kolejności tooassign on toohello Tricaster **punktu końcowego protokołu RTMP**.

    Przejdź wstecz toohello narzędzie AMSE i sprawdzić stan ukończenia hello kanału. Po hello stan został zmieniony z **uruchamianie** za**systemem**, możesz uzyskać hello wejściowy adres URL.

    Gdy kanał hello jest uruchomiona, kliknij prawym przyciskiem myszy nazwę kanału hello, przechodzenia toohover za pośrednictwem **tooclipboard kopia danych wejściowych URL** , a następnie wybierz **podstawowego adresu URL danych wejściowych**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. Wklej te informacje w hello **lokalizacji** pole w obszarze **Flash Server** w ramach hello Tricaster projektu. Również przypisać nazwę strumienia w hello **Identyfikator strumienia** pola.

    Jeśli dodano informacje o strumienia toohello FMLE profilu, można również importować go toothis sekcji klikając **importowanie ustawień**, nawigacja profilu FMLE toohello zapisane i klikając pozycję **OK**. Hello odpowiednie pola Flash serwera należy wypełnić hello informacje z FMLE.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. Gdy skończysz, kliknij przycisk **OK** u dołu hello hello ekranu. Po zakończeniu dane wejściowe audio i wideo w hello Tricaster rozpocząć przesyłanie strumieniowe tooAMS klikając hello **strumienia** przycisku.

     ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> Przed kliknięciem przycisku **strumienia**, możesz **musi** upewnij się, że kanał hello jest gotowy.
> Sprawdź także, czy nie tooleave hello kanału w stanie Gotowe bez wprowadzania wkład źródła danych przez czas dłuższy niż > 15 minut.
>
>

## <a name="test-playback"></a>Podczas odtwarzania testu
Przejdź narzędzie AMSE toohello, a następnie kliknij prawym przyciskiem myszy toobe kanału hello przetestowane. Z hello menu, umieść kursor nad **hello odtwarzania podglądu** i wybierz **z usługi Azure Media Player**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

Czy strumienia hello znajduje się w hello player, koder hello został tooAMS tooconnect poprawnie skonfigurowana.

Jeśli błąd kanału hello należy toobe resetowania i koder zmienić ustawienia. Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.  

## <a name="create-a-program"></a>Utwórz program
1. Po potwierdzeniu kanału odtwarzania, tworzenia programu. W obszarze hello **Live** narzędzia AMSE hello, kliknij prawym przyciskiem myszy w obszarze program hello i wybierz **utworzyć nowy Program**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
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

## <a name="next-step"></a>Następny krok
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
