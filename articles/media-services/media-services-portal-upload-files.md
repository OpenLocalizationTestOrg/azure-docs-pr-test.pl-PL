---
title: "AAA\"przekazywania plików do konta usługi Media Services przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft\""
description: "Ten samouczek przedstawia kroki hello przekazywania plików do konta usługi Media Services przy użyciu hello portalu Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a>Przekazywanie plików do konta usługi Media Services przy użyciu hello portalu Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> toocomplete tego samouczka jest potrzebne konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 


Za pomocą usługi Media Services można przekazać pliki cyfrowe do elementu zawartości. Witaj zasobów może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżek i napisów plików (i hello metadane dotyczące tych plików.) Po przekazaniu plików hello zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.


## <a name="upload-files"></a>Przekazywanie plików

>[!NOTE]
>Brak limitu toohello maksymalny obsługiwany rozmiar pliku do przetwarzania w usłudze Media Services. Zobacz [to](media-services-quotas-and-limitations.md) tematu, aby uzyskać szczegółowe informacje dotyczące limitu rozmiaru pliku hello.
>

1. W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.
2. Na powitania **ustawienia** bloku, kliknij przycisk **zasoby**.
   
    ![Przekazywanie plików](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. Kliknij przycisk hello **przekazać** przycisku.
   
    Witaj **przekazywanie zawartości wideo** zostanie wyświetlone okno.
   
   > [!NOTE]
   > Nie ma żadnego limitu rozmiaru pliku.
   > 
   > 
4. Przeglądaj toohello potrzeby wideo na komputerze, zaznacz go i kliknij przycisk OK.  
   
    rozpocznie się przekazywanie Hello, aby zobaczyć postęp hello pod nazwą pliku hello.  

Po ukończeniu przekazywania hello zobaczysz hello nowy element zawartości na liście hello **zasoby** okna. 

## <a name="next-steps"></a>Następne kroki
Teraz możesz zakodować przekazane elementy zawartości. Więcej informacji znajduje się na stronie [Kodowanie elementów zawartości](media-services-portal-encode.md).

Umożliwia także tootrigger usługi Azure Functions zadania kodowania, na podstawie pliku odbieranych w kontenerze hello skonfigurowane. Aby uzyskać więcej informacji, zobacz [ten przykład](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

