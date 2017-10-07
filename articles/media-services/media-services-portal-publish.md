---
title: "AAA\"publikowania zawartości za pomocą hello portalu Azure | Dokumentacja firmy Microsoft\""
description: "Ten samouczek przedstawia kroki hello publikowania zawartości przy użyciu hello portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a>Publikowanie zawartości z hello portalu Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>Omówienie
> [!NOTE]
> toocomplete tego samouczka jest potrzebne konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

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

Aby uzyskać więcej informacji, zobacz [dostarczanie zawartości omówienie](media-services-deliver-content-overview.md).

> [!NOTE]
> Jeśli używasz hello portalu toocreate lokalizatorów przed marcem 2015 r., zostały utworzone lokalizatory z dwuletnim okresem ważności.  
> 
> 

tooupdate Data wygaśnięcia na lokalizatorze użyj [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) lub [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) interfejsów API. Należy pamiętać, że po zaktualizowaniu hello daty wygaśnięcia lokalizatora SAS następuje zmiana adresu URL hello.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello portalu toopublish zasobów
toouse hello portalu toopublish zasobów hello następujące:

1. W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.
2. Wybierz kolejno pozycje **Ustawienia** > **Elementy zawartości**.
3. Wybierz hello zasobów, które mają toopublish.
4. Kliknij przycisk hello **publikowania** przycisku.
5. Wybierz typ lokalizatora hello.
6. Kliknij przycisk **Dodaj**.
   
    ![Publikowanie](./media/media-services-portal-vod-get-started/media-services-publish1.png)

adres URL Hello zostanie dodany toohello listę **publikowane adresy URL**.

## <a name="play-content-from-hello-portal"></a>Odtwarzanie zawartości z portalu hello
Witaj Azure portal udostępnia odtwarzacz zawartości możesz za pomocą tootest wideo.

Kliknij żądany hello wideo, a następnie kliknij przycisk hello **odtwarzanie** przycisku.

![Publikowanie](./media/media-services-portal-vod-get-started/media-services-play.png)

Zagadnienia do rozważenia:

* Upewnij się, że hello wideo został opublikowany.
* To **Media player** odtwarza z domyślnego hello punktu końcowego przesyłania strumieniowego. Jeśli chcesz, aby tooplay z innych niż domyślne przesyłania strumieniowego punktu końcowego, kliknij adres URL hello toocopy i użyć innego odtwarzacza. (np. [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)).
* Witaj, z którego są przesyłania strumieniowego punktu końcowego przesyłania strumieniowego musi być uruchomiona.  

## <a name="next-steps"></a>Następne kroki
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

