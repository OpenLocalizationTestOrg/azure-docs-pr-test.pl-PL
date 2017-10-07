---
title: przetwarzanie przez dodanie jednostek kodowania - Azure media aaaScale |  Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toohow tooadd kodowania jednostki z platformą .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a>Jak tooscale kodowanie przy użyciu zestawu .NET SDK
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Omówienie
> [!IMPORTANT]
> Upewnij się, że hello tooreview [omówienie](media-services-scale-media-processing-overview.md) tooget tematu więcej informacji na temat skalowania przetwarzania tematu nośnika.
> 
> 

toochange hello zastrzeżone jednostki typu i hello liczbę zastrzeżone jednostki przy użyciu zestawu .NET SDK kodowania hello następujące:

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>Otwarcie biletu pomocy technicznej
Domyślnie co konto usługi Media Services można skalować tooup too25 kodowania i 5 na żądanie jednostek zarezerwowanego przesyłania strumieniowego. Wyższy limit mogą żądać przez otwarcie biletu pomocy technicznej.

### <a name="open-a-support-ticket"></a>Otwórz bilet pomocy technicznej
tooopen biletu pomocy technicznej hello następujące:

1. Kliknij przycisk [uzyskać pomoc techniczną](https://manage.windowsazure.com/?getsupport=true). Jeśli użytkownik nie jest zalogowany, będzie można tooenter zostanie wyświetlony monit o poświadczenia.
2. Wybierz subskrypcję.
3. Wybierz pozycję "Technical" w obszarze typu pomocy technicznej.
4. Kliknij pozycję "Utwórz bilet".
5. Wybierz "Azure Media Services" w liście produktów hello wyświetlone na następnej stronie powitania.
6. Wybierz opcję "Typ problemu" odpowiednią dla tego problemu.
7. Kliknij przycisk Kontynuuj.
8. Postępuj zgodnie z instrukcjami wyświetlanymi na następnej stronie, a następnie wprowadź szczegóły problemu.
9. Kliknij przycisk Zatwierdź tooopen hello biletu.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

