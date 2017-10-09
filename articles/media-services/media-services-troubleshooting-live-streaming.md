---
title: "Transmisja strumieniowa na żywo w przewodniku aaaTroubleshooting | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera sugestie dotyczące sposobu tootroubleshoot live problemów przesyłania strumieniowego."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a>Przewodnik rozwiązywania problemów z transmisją strumieniową na żywo
Ten temat zawiera sugestie dotyczące tootroubleshoot niektóre na żywo, przesyłanie strumieniowe problemów.

## <a name="issues-related-tooon-premises-encoders"></a>Problemy związane z koderów lokalnych tooon
W tej sekcji przedstawiono sugestie dotyczące sposobu tootroubleshoot koderów pokrewne lokalnych tooon problemów, które są skonfigurowane toosend kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo.

### <a name="problem-would-like-toosee-logs"></a>Problem: Chcieliby toosee dzienniki
* **Potencjalny problem**: nie można Znajdź kodera dzienników, która może pomóc w debugowaniu problemów.
  
  * **Telestream Wirecast**: zwykle można znaleźć dzienniki w obszarze C:\Users\{username} \AppData\Roaming\Wirecast\ 
  * **Stanie wolnym Live**: można znaleźć ma toologs łącza na powitania portalu zarządzania. Polecenie **Statystyka**, następnie **dzienniki**. Na powitania **pliki dziennika** strony, zostanie wyświetlona lista dzienników dla wszystkich hello elementów LiveEvent; wybierz hello jedną dopasowania bieżącej sesji. 
  * **Flash Media Live Encoder**: można znaleźć hello **katalog dziennika...**  przechodząc toohello **kodowanie dziennika** kartę.

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>Problem: Nie jest dostępna opcja wyprowadzania progresywnego strumienia
* **Potencjalny problem**: koder hello używane automatycznie nie bez przeplotu.. 
  
    **Kroki rozwiązywania problemów**: Poszukaj usuwania przeplotu opcji w interfejsie kodera hello. Po włączeniu cofnąć przeplot Sprawdź ponownie ustawienia wyjściowej progresywnego. 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a>Problem: Nastąpiła kilka ustawień wyjściowej koder i tooconnect nadal nie.
* **Potencjalny problem**: Azure kodowania kanału nie zostało prawidłowo zresetowane. 
  
    **Kroki rozwiązywania problemów**: Upewnij się, że koder hello jest już wypychanie tooAMS, Zatrzymaj i zresetować hello kanału. Raz uruchomić ponownie, spróbuj się połączyć kodera hello nowe ustawienia. Jeśli to nadal nie rozwiąże problemu hello, spróbuj utworzyć nowy kanał całkowicie, czasami kanałów może zostać uszkodzony po kilku nieudanych próbach.  
* **Potencjalny problem**: rozmiar GOP hello lub klatki ustawienia nie są optymalne. 
  
    **Kroki rozwiązywania problemów**: interwał rozmiaru lub klatki kluczowej GOP zalecane jest 2 sekundy. Niektóre kodery obliczyć tego ustawienia w liczbę ramek, podczas gdy inne sekund. Na przykład: podczas wyprowadzania 30 klatek na sekundę, hello GOP rozmiar będzie 60 klatek, która jest równoważne too2 sekund.  
* **Potencjalny problem**: porty zamkniętego blokują hello strumienia. 
  
    **Kroki rozwiązywania problemów**: podczas przesyłania strumieniowego za pośrednictwem protokołu RTMP, sprawdź zaporę i/lub otwartych portów wychodzących 1935 i 1936 tooconfirm ustawienia serwera proxy. Korzystając z RTP przesyłania strumieniowego, upewnij się, że jest otwarty port wychodzący 2010. 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a>Problem: Podczas konfigurowania hello koder toostream z hello protokołu RTP, brak miejsca tooenter nazwę hosta.
* **Potencjalny problem**: wiele RTP kodery nie zezwalaj na dla nazwy hosta i adresu IP, należy uzyskać toobe.  
  
    **Kroki rozwiązywania problemów**: toofind hello adres IP, otwórz wiersz polecenia na każdym komputerze. toodo to w systemie Windows, otwórz hello uruchamiania wykonywania (WIN + R), a następnie wpisz tooopen "cmd".  
  
    Po otwarciu hello wiersza polecenia, wpisz "Ping [nazwa hosta AMS]". 
  
    Nazwa hosta Hello mogą pochodzić, pomijając hello numer portu z hello adresu URL pozyskiwania Azure, jako wyróżniane na powitania poniższy przykład: 
  
    RTP://Test2-amstest009.RTP.Channel.mediaservices.Windows.NET:2010 / 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> Jeśli po wykonaniu hello kroki rozwiązywania problemów, które nadal nie można pomyślnie przesyłania strumieniowego, należy przesłać biletu pomocy technicznej za pomocą hello portalu Azure.
> 
> 

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

