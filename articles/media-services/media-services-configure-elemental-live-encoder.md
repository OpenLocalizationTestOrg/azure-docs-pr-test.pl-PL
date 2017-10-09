---
title: "aaaConfigure hello toosend kodera na żywo stanie wolnym strumień na żywo o pojedynczej szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooconfigure hello toosend kodera na żywo stanie wolnym kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a>Użyj toosend kodera na żywo stanie wolnym hello strumień na żywo o pojedynczej szybkości transmisji bitów
> [!div class="op_single_selector"]
> * [Elemental na żywo](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

W tym temacie przedstawiono sposób tooconfigure hello [stanie wolnym Live](http://www.elementaltechnologies.com/products/elemental-live) toosend kodera kanałami tooAMS, obsługującymi kodowanie na żywo strumienia pojedynczej szybkości transmisji bitów.  Aby uzyskać więcej informacji, zobacz [Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Ten samouczek pokazuje, jak toomanage usługi Azure Media Services (AMS) za pomocą narzędzia Azure Media Services Explorer (AMSE). To narzędzie jest uruchamiane tylko na komputerze z systemem Windows. Mac lub Linux, za pomocą hello Azure portalu toocreate [kanałów](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) i [programy](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Wymagania wstępne
* Musi mieć praktyczną wiedzę o użyciu stanie wolnym Live sieci web interfejsu toocreate wydarzeń na żywo.
* [Tworzenie konta usługi Azure Media Services](media-services-portal-create-account.md)
* Upewnij się, brak punktu końcowego przesyłania strumieniowego uruchomiona. Aby uzyskać więcej informacji, zobacz [zarządzanie punktami końcowymi przesyłania strumieniowego w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md).
* Zainstaluj najnowszą wersję hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) narzędzia.
* Uruchom narzędzie hello i Połącz konto tooyour AMS.

## <a name="tips"></a>Porady
* Jeśli to możliwe, użyj połączenia internetowego hardwired.
* Regułą podczas określania wymaganiach odnośnie do przepustowości jest hello toodouble przesyłania strumieniowego szybkości transmisji bitów. Chociaż nie jest to wymagane, może pomóc zmniejszyć wpływ hello sieci przeciążona.
* Gdy za pomocą oprogramowania na podstawie koderów, zamknij wszystkie zbędne programy.

## <a name="elemental-live-with-rtp-ingest"></a>Pozyskiwania stanie wolnym Live przy włączonej ochronie czasu rzeczywistego
W tej sekcji przedstawiono, jak tooconfigure hello stanie wolnym Live kodera, który wysyła pojedynczej szybkości transmisji bitów strumień na żywo przy użyciu protokołu RTP.  Aby uzyskać więcej informacji, zobacz [strumieni MPEG-TS przy użyciu protokołu RTP](media-services-manage-live-encoder-enabled-channels.md#channel).

### <a name="create-a-channel"></a>Tworzenie kanału

1. Narzędzie AMSE hello Przejdź toohello **Live** karcie, a następnie kliknij prawym przyciskiem myszy w obszarze kanału hello. Wybierz **Utwórz kanał...** z hello menu.

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. Określ nazwę kanału hello pole opisu jest opcjonalne. W ustawieniach kanału, wybierz **standardowe** dla hello opcji kodowanie na żywo z hello wprowadzania ustawiony protokół zbyt**RTP (MPEG-TS)**. Możesz pozostawić wszystkie inne ustawienia, ponieważ jest.

    Upewnij się, że hello **Start hello nowy kanał teraz** jest zaznaczone.

3. Kliknij przycisk **utworzyć kanał**.

   ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> kanał Hello może zająć toostart 20 minut.
>
>

Podczas uruchamiania kanału hello można [skonfigurować koder hello](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).

> [!IMPORTANT]
> Należy pamiętać, że rozliczanie zaczyna się jak kanału przechodzi do stanu gotowości. Aby uzyskać więcej informacji, zobacz [stanów kanału](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

### <a id=configure_elemental_rtp></a>Konfigurowanie kodera na żywo stanie wolnym hello
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

#### <a name="configuration-steps"></a>Kroki konfiguracji
1. Przejdź toohello **stanie wolnym Live** sieci web interfejsu i skonfigurować hello kodera dla **UDP/TS** przesyłania strumieniowego.
2. Po utworzeniu nowego zdarzenia, przewiń w dół toohello grupy danych wyjściowych i dodać hello **UDP/TS** grupy wyjściowej.
3. Utwórz nowe dane wyjściowe, zaznaczając **nowego strumienia** , a następnie klikając polecenie **dodać danych wyjściowych**.  

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > Zaleca się zdarzenie stanie wolnym hello ma kod czasowy hello ustawić także kodera hello toohelp "Zegara systemowego" Połącz ponownie w przypadku hello awarii strumienia.
   >
   >
4. Teraz, gdy hello danych wyjściowych został utworzony, kliknij przycisk **dodać strumienia**. Teraz można skonfigurować ustawienia wyjściowej Hello.
5. Przewiń w dół toohello "Strumień 1", która właśnie została utworzona, kliknij przycisk hello **wideo** karcie po lewej stronie powitania i rozwiń hello **zaawansowane** w sekcji Ustawienia.

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    Podczas aktywnego stanie wolnym ma szeroki zakres dostosowywania dostępne, hello następujące ustawienia są zalecane w przypadku wprowadzenie do przesyłania strumieniowego tooAMS.

   * Rozdzielczość: 1280 x 720
   * Szybkość klatek: 30
   * Rozmiar GOP: 60 klatek
   * Tryb przeplotu: progresywnego
   * Szybkość transmisji bitów: 5000000 bit/s (to może być określany na podstawie ograniczenia sieci)

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. Pobierz hello kanał wejściowy adres URL.

    Przejdź wstecz toohello narzędzie AMSE i sprawdzić stan ukończenia hello kanału. Po hello stan został zmieniony z **uruchamianie** za**systemem**, możesz uzyskać hello wejściowy adres URL.

    Gdy kanał hello jest uruchomiona, kliknij prawym przyciskiem myszy nazwę kanału hello, przechodzenia toohover za pośrednictwem **tooclipboard kopia danych wejściowych URL** , a następnie wybierz **podstawowego adresu URL danych wejściowych**.  

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. Wklej te informacje w hello **miejsce docelowe głównej** pole hello Elemental. Wszystkie inne ustawienia mogą pozostać hello domyślne.

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    Nadmiarowości dodatkowe Powtórz te kroki hello dodatkowej wprowadzania adresu URL, tworząc osobne karty "Wyjściowej" do przesyłania strumieniowego UDP/usług terminalowych.
3. Kliknij przycisk **Utwórz** (Jeśli utworzono nowe zdarzenie) lub **aktualizacji** (jeśli edycji istniejące zdarzenie) i przejdź dalej toostart hello kodera.

> [!IMPORTANT]
> Przed kliknięciem przycisku **Start** na powitania stanie wolnym Live interfejs sieci web, możesz **musi** upewnij się, że kanał hello jest gotowy.
> Sprawdź także, czy nie tooleave hello kanału w stanie Gotowe bez zdarzenia przez czas dłuższy niż > 15 minut.
>
>

Po działaniu strumienia hello 30 sekund, przejdź wstecz toohello AMSE narzędzia i testowania odtwarzania.  

### <a name="test-playback"></a>Podczas odtwarzania testu

Przejdź narzędzie AMSE toohello, a następnie kliknij prawym przyciskiem myszy toobe kanału hello przetestowane. Z hello menu, umieść kursor nad **hello odtwarzania podglądu** i wybierz **z usługi Azure Media Player**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

Czy strumienia hello znajduje się w hello player, koder hello został tooAMS tooconnect poprawnie skonfigurowana.

Jeśli błąd kanału hello należy toobe resetowania i koder zmienić ustawienia. Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.   

### <a name="create-a-program"></a>Utwórz program
1. Po potwierdzeniu kanału odtwarzania, tworzenia programu. W obszarze hello **Live** narzędzia AMSE hello, kliknij prawym przyciskiem myszy w obszarze program hello i wybierz **utworzyć nowy Program**.  

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. Nazwy hello program i w razie potrzeby dostosuj hello **długość okna archiwum** (domyślne ustawienia too4 godzin, w których). Można także określić miejsce przechowywania lub pozostaw domyślne hello.  
3. Sprawdź hello **Start hello Program teraz** pole.
4. Kliknij przycisk **utworzyć Program**.  

    >[!NOTE]
    > Tworzenie programu zajmuje mniej czasu niż tworzenie kanału.   
      
5. Po uruchomieniu hello program potwierdzić odtwarzania przez kliknięcie prawym przyciskiem myszy hello program i przechodząc zbyt**programach hello odtwarzania** , a następnie wybierając **z usługi Azure Media Player**.  
6. Po potwierdzeniu, kliknij prawym przyciskiem myszy hello program ponownie i wybierz **skopiuj hello adresu URL danych wyjściowych tooClipboard** (lub pobrać te informacje z hello **programu informacji i ustawień** opcji z hello menu).

strumień Hello jest teraz gotowy toobe osadzony w odtwarzacza lub odbiorcami tooan rozproszone na żywo wyświetlanie.  

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
