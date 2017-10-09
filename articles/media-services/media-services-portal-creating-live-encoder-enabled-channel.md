---
title: "aaaHow tooperform transmisja strumieniowa na żywo przy użyciu usługi Azure Media Services toocreate wielokrotnej szybkości transmisji bitów strumieni z hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przeszukiwań możesz hello kroki tworzenia kanału, który odbiera strumień na żywo o pojedynczej szybkości transmisji bitów i koduje go toomulti szybkości transmisji bitów przy użyciu hello portalu Azure."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a>Jak tooperform transmisja strumieniowa na żywo przy użyciu usługi Azure Media Services toocreate różnych szybkościach transmisji bitów strumieni z hello portalu Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [Interfejs API REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Ten samouczek przedstawia kroki tworzenia hello **kanału** który odbiera strumień na żywo o pojedynczej szybkości transmisji bitów i koduje go toomulti szybkości transmisji bitów.

> [!NOTE]
> Aby uzyskać więcej informacji o pojęciach tooChannels powiązane, obsługującymi kodowanie na żywo, zobacz [transmisja strumieniowa na żywo przy użyciu usługi Azure Media Services toocreate wielokrotnej szybkości transmisji bitów strumienie](media-services-manage-live-encoder-enabled-channels.md).
> 
> 

## <a name="common-live-streaming-scenario"></a>Typowy scenariusz transmisji strumieniowej na żywo
Witaj poniżej przedstawiono ogólne etapy tworzenia typowych aplikacji transmisji strumieniowej na żywo.

> [!NOTE]
> Obecnie hello maksymalny zalecany czas trwania wydarzenia na żywo wynosi 8 godzin. Skontaktuj się pod adresem amslived@Microsoft.com, jeśli potrzebujesz toorun kanał na dłuższe okresy.
> 
> 

1. Połącz komputer tooa kamerę wideo. Uruchom i skonfiguruj lokalny koder na żywo, który wysyła strumień o pojedynczej szybkości transmisji w jednym z hello następujących protokołów: RTMP, Smooth Streaming lub RTP (MPEG-TS). Aby uzyskać więcej informacji, zobacz temat [Obsługa protokołu RTMP i kodery na żywo w usłudze Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Ten krok można również wykonać po utworzeniu kanału.
2. Utwórz i uruchom kanał. 
3. Adres URL pozyskiwania, Pobierz hello kanału. 
   
    adres URL pozyskiwania Hello jest używany przez hello kodera na żywo toosend hello strumienia toohello kanału.
4. Pobiera adres URL podglądu kanału hello. 
   
    Użyj tego adresu URL tooverify, czy kanał prawidłowo odbiera strumień na żywo hello.
5. Utwórz wydarzenie/program (to spowoduje również utworzenie elementu zawartości). 
6. Publikowanie zdarzenia hello, (który spowoduje utworzenie lokalizatora OnDemand dla skojarzonego elementu zawartości hello).    
7. Uruchomić zdarzenie hello, gdy są toostart gotowe, przesyłania strumieniowego i archiwizacji.
8. Opcjonalnie hello kodera na żywo może być sygnałowego toostart anonsu. Witaj reklama jest wstawiana hello strumienia wyjściowego.
9. Zatrzymaj hello zdarzenia przy każdym toostop przesyłanie strumieniowe i archiwizowanie wydarzenia hello.
10. Usuń wydarzenie hello (i opcjonalnie można również usunąć hello zasobów).   

## <a name="in-this-tutorial"></a>Informacje o tym samouczku
W tym samouczku hello Azure portal jest hello tooaccomplish używane następujące zadania: 

1. Utworzyć kanał będący włączone tooperform kodowanie na żywo.
2. Get hello adresu URL pozyskiwania w kolejności toosupply on toolive kodera. Hello koder na żywo użyje tego adresu URL tooingest hello strumienia do kanału hello.
3. Utworzenie wydarzenia/programu (i elementu zawartości).
4. Publikowanie hello zawartości i uzyskiwanie adresów URL przesyłania strumieniowego.  
5. Odtwarzanie zawartości.
6. Czyszczenie.

## <a name="prerequisites"></a>Wymagania wstępne
Samouczek hello toocomplete wymagane są następujące Hello.

* toocomplete tego samouczka jest potrzebne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. 
  Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* Konto usługi Media Services. Zobacz toocreate konto usługi Media Services [Utwórz konto](media-services-portal-create-account.md).
* Kamera internetowa i koder, który może wysyłać strumień na żywo o pojedynczej szybkości transmisji bitów.

## <a name="create-a-channel"></a>Tworzenie kanału
1. W hello [portalu Azure](https://portal.azure.com/), wybierz usługi Media Services, a następnie kliknij polecenie Nazwa konta usługi Media Services.
2. Wybierz pozycję **Transmisja strumieniowa na żywo**.
3. Wybierz pozycję **Tworzenie niestandardowe**. Ta opcja umożliwi utworzenie kanału, który jest skonfigurowany do przeprowadzania kodowania na żywo.
   
    ![Tworzenie kanału](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. Kliknij pozycję **Ustawienia**.
   
   1. Wybierz hello **Live Encoding** typ kanału. Ten typ Określa, że toocreate kanał obsługujący kodowanie na żywo. Czy oznacza hello przychodzące pojedynczej szybkości transmisji bitów wysyłanych toohello kanału i kodowany do strumienia wielokrotnej szybkości transmisji bitów przy użyciu ustawień kodera na żywo określonego strumienia. Aby uzyskać więcej informacji, zobacz [transmisja strumieniowa na żywo przy użyciu usługi Azure Media Services toocreate wielokrotnej szybkości transmisji bitów strumienie](media-services-manage-live-encoder-enabled-channels.md). Kliknij przycisk OK.
   2. Określ nazwę kanału.
   3. Kliknij przycisk OK u dołu hello hello ekranu.
5. Wybierz hello **pozyskiwania** kartę.
   
   1. Na tej stronie można wybrać protokół przesyłania strumieniowego. Dla hello **Live Encoding** są opcje protokołu prawidłowy typ kanału:
      
      * Pojedyncza szybkość transmisji bitów podzielonej zawartości w formacie MP4 (Smooth Streaming)
      * Pojedyncza szybkość transmisji bitów w formacie RTMP
      * RTP (MPEG TS): strumień transportu MPEG-2 przy użyciu protokołu RTP.
        
        Aby uzyskać szczegółowe informacje na temat każdego protokołu, zobacz [transmisja strumieniowa na żywo przy użyciu usługi Azure Media Services toocreate wielokrotnej szybkości transmisji bitów strumienie](media-services-manage-live-encoder-enabled-channels.md).
        
        Nie można zmienić opcji protokołu hello podczas hello kanał lub skojarzone z nim wydarzenia/programy są uruchomione. Jeśli potrzebujesz różnych protokołów, utwórz osobny kanał dla każdego protokołu przesyłania strumieniowego.  
   2. Ograniczenia adresów IP można stosować na powitania pozyskiwania. 
      
       Witaj IP można zdefiniować adresy, które są dozwolone tooingest kanału toothis wideo. Dozwolone adresy IP można określić jako pojedynczy adres IP (np. „10.0.0.1”), zakres adresów IP przy użyciu adresu IP i maski podsieci CIDR (np. „10.0.0.1/22”) lub zakres adresów IP przy użyciu adresu IP i maski podsieci w zapisie kropkowo-cyfrowym (np. „10.0.0.1(255.255.252.0)”).
      
       Jeśli adresy IP nie zostaną określone i brakuje definicji reguły, to żaden adres IP nie będzie dozwolony. tooallow dowolnego adresu IP, Utwórz regułę i ustaw wartość 0.0.0.0/0.
6. Na powitania **Podgląd** karcie, zastosować ograniczenia adresów IP na powitania podglądu.
7. Na powitania **kodowanie** karcie, określ ustawienie wstępne kodowania hello. 
   
    Obecnie hello tylko system można wybrać ustawienie wstępne jest **domyślna rozdzielczość 720p**. toospecify niestandardowego ustawień, otwórz bilet pomocy technicznej firmy Microsoft. Następnie wprowadź nazwę hello hello ustawienie wstępne utworzone automatycznie. 

> [!NOTE]
> Obecnie hello uruchomienie kanału może potrwać too30 minut. Resetowanie kanału może potrwać too5 minut.
> 
> 

Po utworzeniu kanału hello można kliknąć w kanale hello i wybierz **ustawienia** którym można zobaczyć konfiguracje kanałów. 

Aby uzyskać więcej informacji, zobacz [transmisja strumieniowa na żywo przy użyciu usługi Azure Media Services toocreate wielokrotnej szybkości transmisji bitów strumienie](media-services-manage-live-encoder-enabled-channels.md).

## <a name="get-ingest-urls"></a>Pobieranie adresów URL pozyskiwania
Po utworzeniu kanału hello można uzyskać pozyskiwania adresów URL, które zapewnią toohello kodera na żywo. Witaj koder używa tych adresów URL tooinput strumień na żywo.

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a>Tworzenie wydarzeń i zarządzanie nimi
### <a name="overview"></a>Omówienie
Kanał jest skojarzony z wydarzeniami/programami, umożliwiających toocontrol hello publikowania i przechowywania segmentów strumienia na żywo. Kanały zarządzają wydarzeniami/programami. Witaj relacja kanału i programu jest bardzo podobne nośnika tootraditional, gdzie kanał ma stały strumień zawartości, a program zdarzeń zakresie toosome upłynął, w tym kanale.

Można określić hello liczbę godzin tooretain zawartości hello rejestrowane zdarzenia hello przez ustawienie hello **okno archiwum** długości. Tę wartość można ustawić z co najmniej 5 minut tooa maksymalnie 25 godzin. Długość okna archiwum określa również dostępny hello maksymalną ilość czasu, klienci mogą zwrócić wstecz od bieżącego położenia na żywo hello. Zdarzenia mogą być uruchamiane hello określoną ilość czasu, ale zawartość, która wykracza poza długość okna hello jest stale odrzucana. Ta wartość tej właściwości określa również, jak długo klient hello mogą być manifesty.

Każde wydarzenie jest skojarzone z elementem zawartości. należy utworzyć Lokalizator OnDemand dla hello zdarzeń hello toopublish związane z nią zasobów. Lokalizator umożliwi toobuild adresu URL przesyłania strumieniowego, która może zapewnić tooyour klientów.

Kanał obsługuje toothree współbieżnie uruchomionych zdarzeń, dzięki czemu można tworzyć wiele archiwów hello samego strumienia przychodzącego. Dzięki temu toopublish i archiwum różnych części wydarzenia zgodnie z potrzebami. Na przykład konkretnym wymaganiom biznesowym jest tooarchive sześciu godzin zdarzenia, ale toobroadcast ostatnich 10 minut. tooaccomplish, potrzebne są dwie uruchomionych współbieżnie toocreate zdarzeń. Jedno zdarzenie ustawiono tooarchive sześciu godzin zdarzenia hello, ale hello program nie został opublikowany. Witaj innych zdarzeń jest zestaw tooarchive przez 10 minut i ten program zostanie opublikowany.

Nie należy używać ponownie istniejących programów dla nowych zdarzeń. Zamiast tego należy utworzyć i uruchomić nowy program dla każdego zdarzenia.

Uruchom wydarzenie/program, gdy są toostart gotowe, przesyłania strumieniowego i archiwizacji. Zatrzymaj hello zdarzenia przy każdym toostop przesyłanie strumieniowe i archiwizowanie wydarzenia hello. 

toodelete zarchiwizowane zawartość, Zatrzymaj i Usuń hello zdarzeń, a następnie usuń hello skojarzonego elementu zawartości. Nie można usunąć elementu zawartości, jeśli jest on używany przez zdarzenie hello; Najpierw należy usunąć Hello zdarzeń. 

Nawet po zatrzymaniu i usunięciu hello zdarzeń, hello użytkownicy będą mogli toostream zarchiwizowaną zawartość wideo na żądanie, dla tak długo, jak hello zasobów nie zostaną usunięte.

Jeśli chcesz zarchiwizować hello tooretain zawartości, ale nie jest dostępny do przesyłania strumieniowego, Usuń hello przesyłania strumieniowego lokalizatora.

### <a name="createstartstop-events"></a>Tworzenie, uruchamianie i zatrzymywanie wydarzeń
Po utworzeniu strumienia hello otrzymywanych hello kanału można rozpocząć hello strumienia zdarzeń przez utworzenie zasobów, programu i lokalizatora przesyłania strumieniowego. Spowoduje to archiwum hello strumienia i stał się dostępny tooviewers za pośrednictwem punktu końcowego przesyłania strumieniowego hello. 

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 

Istnieją dwa sposoby toostart zdarzeń: 

1. Z hello **kanału** kliknij przycisk **wydarzenie na żywo** tooadd nowe zdarzenie.
   
    Określ nazwę wydarzenia, nazwę elementu zawartości, okno archiwum i opcję szyfrowania.
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    Jeśli **publikowania teraz tego zdarzenia na żywo** zaznaczone, hello zdarzeń hello adresy URL publikowania zostaną utworzone.
   
    Możesz nacisnąć przycisk **Start**, gdy są gotowe toostream hello zdarzeń.
   
    Po uruchomieniu zdarzenia hello możesz nacisnąć przycisk **czujki** toostart odtwarzanie hello zawartości.
2. Alternatywnie można użyć skrótu i kliknąć przycisk **Go Live** przycisk na powitania **kanału** strony. Spowoduje to utworzenie domyślnych elementów treści, programu i lokalizatora przesyłania strumieniowego.
   
    Zdarzenie Hello jest nazywane **domyślne** i okno archiwum hello ustawiono too8 godzin.

Możesz obserwować hello zdarzeń opublikowanej z hello **wydarzenia na żywo** strony. 

Jeśli klikniesz pozycję **Zakończ transmisję na żywo**, wszystkie wydarzenia na żywo zostaną zatrzymane. 

## <a name="watch-hello-event"></a>Obejrzyj hello zdarzeń
toowatch hello zdarzenia, kliknij przycisk **czujki** w hello Azure hello portalu lub kopiowania URL przesyłania strumieniowego i Użyj wybranego odtwarzacza. 

![Utworzone](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

Zdarzenia na żywo automatycznie konwertuje zawartość tooon żądanie zdarzenia po zatrzymaniu.

## <a name="clean-up"></a>Czyszczenie
Jeśli zakończeniu strumieniowego przesyłania zdarzeń i chcesz tooclean zasobów hello udostępnione wcześniej, wykonaj procedury hello.

* Zatrzymaj wypychanie hello strumienia z kodera hello.
* Zatrzymaj kanał hello. Po zatrzymaniu kanału hello nie będą naliczane opłaty. Jeśli wymagane jest toostart go ponownie, będzie mieć hello sam adres URL pozyskiwania, więc nie trzeba tooreconfigure kodera.
* Można zatrzymać punkt końcowy przesyłania strumieniowego, chyba że chcesz toocontinue tooprovide hello archiwum zdarzenia na żywo jako strumień na żądanie. Jeśli kanał hello jest w stanie zatrzymania, nie będą naliczane opłaty.

## <a name="view-archived-content"></a>Wyświetlanie zarchiwizowanej zawartości
Nawet po zatrzymaniu i usunięciu hello zdarzeń, hello użytkownicy będą mogli toostream zarchiwizowaną zawartość wideo na żądanie, dla tak długo, jak hello zasobów nie zostaną usunięte. Nie można usunąć elementu zawartości, jeśli jest on używany przez zdarzenie; Najpierw należy usunąć Hello zdarzeń. 

Wybierz zasobów, toomanage **ustawienie** i kliknij przycisk **zasoby**.

![Elementy zawartości](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a>Zagadnienia do rozważenia
* Obecnie hello maksymalny zalecany czas trwania wydarzenia na żywo wynosi 8 godzin. Skontaktuj się pod adresem amslived@Microsoft.com, jeśli potrzebujesz toorun kanał na dłuższe okresy.
* Upewnij się, że hello punktu końcowego przesyłania strumieniowego z którego mają zostać toostream zawartości znajduje się w hello **systemem** stanu.

## <a name="next-step"></a>Następny krok
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

