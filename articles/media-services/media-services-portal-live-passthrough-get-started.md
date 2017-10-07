---
title: "strumień aaaLive za pomocą koderów lokalnych przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki tworzenia kanału, który jest skonfigurowany do dostarczania w formie przekazywania hello."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a>Jak tooperform transmisja strumieniowa na żywo z lokalnymi koderów przy użyciu hello portalu Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Ten samouczek przedstawia kroki hello przy użyciu hello Azure portalu toocreate **kanału** skonfigurowanego do dostarczania w formie przekazywania. 

## <a name="prerequisites"></a>Wymagania wstępne
Samouczek hello toocomplete wymagane są następujące Hello:

* Konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Konto usługi Media Services. Zobacz toocreate konto usługi Media Services [jak tooCreate konta usługi Media Services](media-services-portal-create-account.md).
* Kamera internetowa. Na przykład [koder Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).

Zdecydowanie zaleca się hello tooreview następujące artykuły:

* [Obsługa protokołu RTMP i kodery na żywo w usłudze Azure Media Services](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [Omówienie transmisji strumieniowej na żywo przy użyciu usługi Azure Media Services](media-services-manage-channels-overview.md)
* [Transmisja strumieniowa na żywo za pomocą koderów lokalnych tworzących strumienie o różnej szybkości transmisji bitów](media-services-live-streaming-with-onprem-encoders.md)

## <a id="scenario"></a>Typowy scenariusz transmisji strumieniowej na żywo
Witaj poniższych krokach opisano zadania związane z tworzeniem typowych aplikacji transmisji strumieniowej na żywo używających kanałów skonfigurowanych do dostarczania przekazywania. Ten samouczek pokazuje, jak toocreate kanał w formie przekazywania i wydarzeń na żywo oraz zarządzania nimi.

>[!NOTE]
>Upewnij się, że jest hello, z którego mają zostać toostream zawartości punktu końcowego przesyłania strumieniowego w hello **systemem** stanu. 
    
1. Połącz komputer tooa kamerę wideo. Uruchom i skonfiguruj lokalny koder na żywo, który wyprowadza strumień protokołu RTMP o różnej szybkości transmisji bitów lub pofragmentowany strumień MP4. Aby uzyskać więcej informacji, zobacz temat [Obsługa protokołu RTMP i kodery na żywo w usłudze Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Ten krok można również wykonać po utworzeniu kanału.
2. Utwórz i uruchom kanał w formie przekazywania.
3. Adres URL pozyskiwania, Pobierz hello kanału. 
   
    adres URL pozyskiwania Hello jest używany przez hello kodera na żywo toosend hello strumienia toohello kanału.
4. Pobiera adres URL podglądu kanału hello. 
   
    Użyj tego adresu URL tooverify, czy kanał prawidłowo odbiera strumień na żywo hello.
5. Utwórz program lub wydarzenie na żywo. 
   
    Przy użyciu hello portalu Azure, również utworzenie wydarzenia na żywo tworzy zasób. 

6. Uruchom wydarzenie/program hello, gdy są toostart gotowe, przesyłania strumieniowego i archiwizacji.
7. Opcjonalnie hello kodera na żywo może być sygnałowego toostart anonsu. Witaj reklama jest wstawiana hello strumienia wyjściowego.
8. Zatrzymaj wydarzenie/program hello zawsze, gdy chcesz toostop przesyłanie strumieniowe i archiwizowanie wydarzenia hello.
9. Usuń wydarzenie/program hello (i opcjonalnie można również usunąć hello zasobów).     

> [!IMPORTANT]
> Zapoznaj się z tematem [transmisję strumieniową na żywo za pomocą koderów lokalnych, które tworzą strumienie o różnych szybkościach transmisji bitów](media-services-live-streaming-with-onprem-encoders.md) toolearn założenia i zagadnienia związane z toolive przesyłania strumieniowego z koderów lokalnych i kanałów w formie przekazywania.
> 
> 

## <a name="tooview-notifications-and-errors"></a>tooview powiadomień i błędów
Jeśli chcesz tooview powiadomienia i błędy generowane przez hello portalu Azure, kliknij ikonę powiadomienia hello.

![Powiadomienia](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a>Tworzenie i uruchamianie kanałów i wydarzeń w formie przekazywania
Kanał jest skojarzony z wydarzeniami/programami, umożliwiających toocontrol hello publikowania i przechowywania segmentów strumienia na żywo. Kanały zarządzają wydarzeniami. 

Można określić hello liczbę godzin zawartości hello rejestrowane tooretain hello programu przez ustawienie hello **okno archiwum** długości. Tę wartość można ustawić z co najmniej 5 minut tooa maksymalnie 25 godzin. Długość okna archiwum określa również dostępny hello maksymalną ilość czasu, klienci mogą zwrócić wstecz od bieżącego położenia na żywo hello. Zdarzenia mogą być uruchamiane hello określoną ilość czasu, ale zawartość, która wykracza poza długość okna hello jest stale odrzucana. Ta wartość tej właściwości określa również, jak długo klient hello mogą być manifesty.

Każde wydarzenie jest skojarzone z elementem zawartości. toopublish hello zdarzenia, należy utworzyć Lokalizator OnDemand dla hello skojarzonych zasobów. Lokalizator umożliwia toobuild adresu URL przesyłania strumieniowego, która może zapewnić tooyour klientów.

Kanał obsługuje toothree współbieżnie uruchomionych zdarzeń, dzięki czemu można tworzyć wiele archiwów hello samego strumienia przychodzącego. Dzięki temu toopublish i archiwum różnych części wydarzenia zgodnie z potrzebami. Na przykład konkretnym wymaganiom biznesowym jest tooarchive sześciu godzin programu, ale toobroadcast ostatnich 10 minut. tooaccomplish, należy toocreate dwa jednocześnie uruchomione programy. Jeden program ustawiono tooarchive sześciu godzin zdarzenia hello, ale hello program nie został opublikowany. Hello inny program jest zestaw tooarchive przez 10 minut i ten program zostanie opublikowany.

Istniejących wydarzeń na żywo nie należy używać ponownie. Zamiast tego należy utworzyć i uruchomić nowe wydarzenie dla każdego wydarzenia.

Uruchomić zdarzenie hello, gdy są toostart gotowe, przesyłania strumieniowego i archiwizacji. Zatrzymaj hello program zawsze, gdy chcesz toostop przesyłanie strumieniowe i archiwizowanie wydarzenia hello. 

toodelete zarchiwizowane zawartość, Zatrzymaj i Usuń hello zdarzeń, a następnie usuń hello skojarzonego elementu zawartości. Nie można usunąć elementu zawartości, jeśli jest on używany przez zdarzenie; Najpierw należy usunąć Hello zdarzeń. 

Nawet po zatrzymaniu i usunięciu hello zdarzeń, hello użytkownicy będą mogli toostream zarchiwizowaną zawartość wideo na żądanie, dla tak długo, jak hello zasobów nie zostaną usunięte.

Jeśli chcesz zarchiwizować hello tooretain zawartości, ale nie jest dostępny do przesyłania strumieniowego, Usuń hello przesyłania strumieniowego lokalizatora.

### <a name="toouse-hello-portal-toocreate-a-channel"></a>toouse hello portalu toocreate kanału
W tej sekcji przedstawiono sposób toouse hello **szybkie tworzenie** toocreate opcja kanał w formie przekazywania.

Więcej szczegółowych informacji dotyczących kanałów przekazujących można znaleźć w temacie [Transmisja strumieniowa na żywo za pomocą koderów lokalnych tworzących strumienie o różnej szybkości transmisji bitów](media-services-live-streaming-with-onprem-encoders.md).

1. W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.
2. W hello **ustawienia** okna, kliknij przycisk **transmisja strumieniowa na żywo**. 
   
    ![Wprowadzenie](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    Witaj **transmisja strumieniowa na żywo** zostanie wyświetlone okno.
3. Kliknij przycisk **szybkie tworzenie** protokołu pozyskiwania toocreate kanał w formie przekazywania z hello RTMP.
   
    Witaj **Utwórz nowy kanał** zostanie wyświetlone okno.
4. Nadaj nazwę hello nowy kanał, a następnie kliknij przycisk **Utwórz**. 
   
    Kanał w formie przekazywania to tworzy z hello protokołu pozyskiwania RTMP.

## <a name="create-events"></a>Tworzenie wydarzeń
1. Wybierz toowhich kanału, ma tooadd zdarzenia.
2. Naciśnij przycisk **Wydarzenie na żywo**.

![Wydarzenie](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a>Pobieranie adresów URL pozyskiwania
Po utworzeniu kanału hello można uzyskać pozyskiwania adresów URL, które zapewnią toohello kodera na żywo. Witaj koder używa tych adresów URL tooinput strumień na żywo.

![Utworzone](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a>Obejrzyj hello zdarzeń
toowatch hello zdarzenia, kliknij przycisk **czujki** w hello Azure hello portalu lub kopiowania URL przesyłania strumieniowego i Użyj wybranego odtwarzacza. 

![Utworzone](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

Wydarzenia na żywo automatycznie Pobierz zawartość przekonwertowanego żądanie tooon po zatrzymaniu.

## <a name="clean-up"></a>Czyszczenie
Więcej szczegółowych informacji dotyczących kanałów przekazujących można znaleźć w temacie [Transmisja strumieniowa na żywo za pomocą koderów lokalnych tworzących strumienie o różnej szybkości transmisji bitów](media-services-live-streaming-with-onprem-encoders.md).

* Kanał można zatrzymać tylko wtedy, gdy wszystkie wydarzenia/programy na kanale hello zostały zatrzymane.  Po zatrzymaniu kanału hello nie nie poniesiesz żadnych dodatkowych opłat. Jeśli wymagane jest toostart go ponownie, będzie mieć hello sam adres URL pozyskiwania, więc nie trzeba tooreconfigure kodera.
* Kanał można usunąć tylko wtedy, gdy wszystkie wydarzenia na żywo w kanale hello zostały usunięte.

## <a name="view-archived-content"></a>Wyświetlanie zarchiwizowanej zawartości
Nawet po zatrzymaniu i usunięciu hello zdarzeń, hello użytkownicy będą mogli toostream zarchiwizowaną zawartość wideo na żądanie, dla tak długo, jak hello zasobów nie zostaną usunięte. Nie można usunąć elementu zawartości, jeśli jest on używany przez zdarzenie; Najpierw należy usunąć Hello zdarzeń. 

Wybierz zasobów, toomanage **ustawienie** i kliknij przycisk **zasoby**.

![Elementy zawartości](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a>Następny krok
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

