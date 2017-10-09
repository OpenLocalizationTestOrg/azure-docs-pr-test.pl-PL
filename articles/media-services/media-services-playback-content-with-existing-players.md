---
title: "aaaUse istniejących tooplayback odtwarzacze zawartości - Azure | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera listę istniejących odtwarzaczy, możesz za pomocą tooplayback zawartości."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 54817345a19a9d3b18f1e7b352c3342043a569b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="playing-your-content-with-existing-players"></a>Odtwarzanie zawartości z istniejących graczy
Usługa Azure Media Services obsługuje wiele popularnych formatach przesyłania strumieniowego, takie jak Smooth Streaming, HTTP transmisji strumieniowej na żywo i MPEG-Dash. Ten temat kieruje użytkownika tooexisting odtwarzaczy, których można używać tootest strumienie.

### <a name="hello-azure-portal-media-services-content-player"></a>Odtwarzacz zawartości Hello portalu Azure Media Services
Witaj **Azure** portal udostępnia odtwarzacz zawartości możesz za pomocą tootest wideo.

Witaj, kliknij polecenie potrzeby wideo (Upewnij się, że został on [opublikowane](media-services-portal-publish.md)) i kliknij przycisk hello **odtwarzania** u dołu hello hello portalu.

Zagadnienia do rozważenia:

* Witaj **ODTWARZACZ zawartości MEDIA SERVICES** odtwarza z domyślnego hello punktu końcowego przesyłania strumieniowego. Jeśli chcesz tooplay z punktu końcowego przesyłania strumieniowego innych niż domyślne, należy użyć innego odtwarzacza Na przykład [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Azure Media Player
Użyj [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback zawartości (Wyczyść lub protected) w jednym z następujących formatów hello:

* Smooth Streaming
* MPEG DASH
* HLS
* MP4 progresywnego

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>Szyfrowania AES z tokenem
[http://aestoken.azurewebsites.NET](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Odtwarzaczy programu Silverlight
#### <a name="monitoring"></a>Monitorowanie
[http://SMF.cloudapp.NET/healthmonitor](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a>PlayReady z tokenem
[http://sltoken.azurewebsites.NET](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a>Odtwarzacze kreska
[http://dashplayer.azurewebsites.NET](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a>Inne
tootest HLS adresów URL można również użyć:

* **Safari** na urządzeniu z systemem iOS lub
* **Odtwarzacz HLS 3ivx** w systemie Windows.

## <a name="developing-video-players"></a>Tworzenie odtwarzaczy wideo
Aby uzyskać informacje o toodevelop własne odtwarzaczy, zobacz temat [opracowywanie odtwarzaczy wideo](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
