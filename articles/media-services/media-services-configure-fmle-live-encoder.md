---
title: "aaaConfigure hello toosend koder FMLE strumień na żywo o pojedynczej szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooconfigure hello interfejsu Flash Media na żywo kodera (FMLE) koder toosend kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a>Użyj hello FMLE koder toosend strumień na żywo o pojedynczej szybkości transmisji bitów
> [!div class="op_single_selector"]
> * [FMLE](media-services-configure-fmle-live-encoder.md)
> * [Elemental na żywo](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
>
>

W tym temacie przedstawiono sposób tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) toosend kodera (FMLE) tooAMS kanałów, które są włączone kodowanie na żywo strumienia pojedynczej szybkości transmisji bitów. Aby uzyskać więcej informacji, zobacz [Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Ten samouczek pokazuje, jak toomanage usługi Azure Media Services (AMS) za pomocą narzędzia Azure Media Services Explorer (AMSE). To narzędzie jest uruchamiane tylko na komputerze z systemem Windows. Mac lub Linux, za pomocą hello Azure portalu toocreate [kanałów](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) i [programy](media-services-portal-creating-live-encoder-enabled-channel.md).

Należy pamiętać, że w tym samouczku opisano przy użyciu AAC. FMLE nie obsługuje jednak AAC domyślnie. Będzie potrzebny toopurchase wtyczki do kodowania AAC przykład MainConcept: [AAC wtyczki](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)

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

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. Określ nazwę kanału hello pole opisu jest opcjonalne. W ustawieniach kanału, wybierz **standardowe** dla hello opcji kodowanie na żywo z hello wprowadzania ustawiony protokół zbyt**RTMP**. Możesz pozostawić wszystkie inne ustawienia, ponieważ jest.

    Upewnij się, że hello **Start hello nowy kanał teraz** jest zaznaczone.

3. Kliknij przycisk **utworzyć kanał**.

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> kanał Hello może zająć toostart 20 minut.
>
>

Podczas uruchamiania kanału hello można [skonfigurować koder hello](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).

> [!IMPORTANT]
> Należy pamiętać, że rozliczanie zaczyna się jak kanału przechodzi do stanu gotowości. Aby uzyskać więcej informacji, zobacz [stanów kanału](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_fmle_rtmp></a>Skonfiguruj hello FMLE kodera
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
1. Przejdź toohello, który interfejs Flash Media na żywo kodera (FMLE) na maszynie hello jest używany.

    Interfejs Hello jest jednej strony głównej ustawień. Poświęć należy wziąć pod uwagę następujące hello zalecane ustawienia tooget wprowadzenie do przesyłania strumieniowego przy użyciu FMLE.

   * Format: Szybkość klatek H.264: 30,00
   * Rozmiar wejściowe: 1280 x 720
   * Szybkość transmisji bitów: 5000 KB/s (może być określany na podstawie ograniczenia sieci)  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     Przy użyciu naprzemiennych źródeł, skontaktuj się z hello znacznikiem wyboru opcji "Opcji Usuń przeplot"
2. Klucz hello wybierz ikonę tooFormat dalej, te dodatkowe ustawienia powinny być:

   * Profil: Main
   * Poziom: 4.0
   * Częstotliwość klatki kluczowej: 2 sekundy.

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. Ustaw następujące istotne ustawienia audio hello:

   * Format: AAC
   * Częstotliwość próbkowania: Hz 44100 b
   * Szybkość transmisji bitów: 192 kb/s

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. Pobierz hello kanał wejściowy adres URL w kolejności tooassign on toohello FMLE **punktu końcowego protokołu RTMP**.

    Przejdź wstecz toohello narzędzie AMSE i sprawdzić stan ukończenia hello kanału. Po hello stan został zmieniony z **uruchamianie** za**systemem**, możesz uzyskać hello wejściowy adres URL.

    Gdy kanał hello jest uruchomiona, kliknij prawym przyciskiem myszy nazwę kanału hello, przechodzenia toohover za pośrednictwem **tooclipboard kopia danych wejściowych URL** , a następnie wybierz **podstawowego adresu URL danych wejściowych**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. Wklej te informacje w hello **FMS URL** pole hello dane wyjściowe sekcji, a następnie przypisz nazwę strumienia.

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    Dodatkowe nadmiarowości Powtórz te czynności z hello dodatkowej wprowadzania adresu URL.
6. Wybierz przycisk **Połącz**.

> [!IMPORTANT]
> Przed kliknięciem przycisku **Connect**, możesz **musi** upewnij się, że kanał hello jest gotowy.
> Sprawdź także, czy nie tooleave hello kanału w stanie Gotowe bez wprowadzania wkład źródła danych przez czas dłuższy niż > 15 minut.
>
>

## <a name="test-playback"></a>Podczas odtwarzania testu

Przejdź narzędzie AMSE toohello, a następnie kliknij prawym przyciskiem myszy toobe kanału hello przetestowane. Z hello menu, umieść kursor nad **hello odtwarzania podglądu** i wybierz **z usługi Azure Media Player**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

Czy strumienia hello znajduje się w hello player, koder hello został tooAMS tooconnect poprawnie skonfigurowana.

Jeśli błąd kanału hello należy toobe resetowania i koder zmienić ustawienia. Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.  

## <a name="create-a-program"></a>Utwórz program
1. Po potwierdzeniu kanału odtwarzania, tworzenia programu. W obszarze hello **Live** narzędzia AMSE hello, kliknij prawym przyciskiem myszy w obszarze program hello i wybierz **utworzyć nowy Program**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
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
