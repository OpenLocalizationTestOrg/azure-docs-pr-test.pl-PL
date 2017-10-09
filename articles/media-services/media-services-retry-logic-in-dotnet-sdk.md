---
title: "Logika aaaRetry w hello SDK usługi Media Services dla platformy .NET | Dokumentacja firmy Microsoft"
description: "Hello temat zawiera omówienie logiki ponawiania próby w hello SDK usługi Media Services dla platformy .NET."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 527b61a6-c862-4bd8-bcbc-b9aea1ffdee3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 18d0a9d68e55a48bc769fb6ae5711ddba78ed8e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retry-logic-in-hello-media-services-sdk-for-net"></a>Spróbuj ponownie logikę hello SDK usługi Media Services dla platformy .NET
Podczas pracy z usługami Microsoft Azure, może wystąpić błędów przejściowych. W przypadku wystąpienia błędu przejściowego, w większości przypadków po kilku próbach hello operacja zakończy się pomyślnie. Witaj SDK usługi Media Services dla platformy .NET implementuje hello ponawiania logiki toohandle błędów przejściowych skojarzone z wyjątków i błędów spowodowanych przez żądania sieci web, wykonywanie kwerend zapisywania zmian i operacje magazynu.  Domyślnie program hello SDK usługi Media Services dla platformy .NET wykonuje czterech ponownych prób przed ponownie zgłaszanie hello wyjątek tooyour aplikacji. kodu aplikacji Hello następnie musi poprawnie obsługiwać tego wyjątku.  

 Witaj poniżej znajduje się krótki wskazówek dotyczących żądania sieci Web, magazynu, zapytania i metody SaveChanges zasad:  

* Witaj zasad magazynu jest używana do operacje magazynu obiektów blob (przekazywanie i pobieranie plików zasobów).  
* Hello zasady żądania sieci Web jest używana dla żądania ogólnego sieci web (na przykład w przypadku uzyskiwanie tokenu uwierzytelniania i rozpoznawania użytkowników hello klastra punktu końcowego).  
* Hello zapytania zasad jest używane do wykonywania zapytań jednostek z REST (na przykład mediaContext.Assets.Where(...)).  
* Witaj SaveChanges zasad służy do czynności wykonywanych przez zmiany danych w ramach usługi hello (na przykład tworzenie jednostki aktualizowania jednostki, dla operacji podczas wywoływania funkcji usługi).  
  
  Ten temat zawiera listę typów wyjątków i Logika ponawiania próby kody błędów, które są obsługiwane przez hello SDK usługi Media Services dla platformy .NET.  

## <a name="exception-types"></a>Typy wyjątków
Witaj poniższej tabeli opisano wyjątki hello tego zestawu SDK usługi Media Services dla platformy .NET dojść lub nie obsługuje dla niektórych operacji, które mogą być przyczyną błędów przejściowych.  

| Wyjątek | Żądanie sieci Web | Magazyn | Zapytanie | Metody SaveChanges |
| --- | --- | --- | --- | --- |
| WebException<br/>Aby uzyskać więcej informacji, zobacz hello [kodów stanu WebException](media-services-retry-logic-in-dotnet-sdk.md#WebExceptionStatus) sekcji. |Tak |Tak |Tak |Tak |
| DataServiceClientException<br/> Aby uzyskać więcej informacji, zobacz [kody stanu błędu HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Nie |Tak |Tak |Tak |
| DataServiceQueryException<br/> Aby uzyskać więcej informacji, zobacz [kody stanu błędu HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Nie |Tak |Tak |Tak |
| DataServiceRequestException<br/> Aby uzyskać więcej informacji, zobacz [kody stanu błędu HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Nie |Tak |Tak |Tak |
| DataServiceTransportException |Nie |Nie |Tak |Tak |
| TimeoutException |Tak |Tak |Tak |Nie |
| Socketexception — |Tak |Tak |Tak |Tak |
| StorageException |Nie |Tak |Nie |Nie |
| IOException |Nie |Tak |Nie |Nie |

### <a name="WebExceptionStatus"></a>Kody stanu WebException
Witaj poniższej tabeli przedstawiono które błędu WebException Logika ponawiania hello kody jest zaimplementowana. Witaj [WebExceptionStatus](http://msdn.microsoft.com/library/system.net.webexceptionstatus.aspx) wyliczenie definiuje hello kodów stanu.  

| Stan | Żądanie sieci Web | Magazyn | Zapytanie | Metody SaveChanges |
| --- | --- | --- | --- | --- |
| ConnectFailure |Tak |Tak |Tak |Tak |
| NameResolutionFailure |Tak |Tak |Tak |Tak |
| ProxyNameResolutionFailure |Tak |Tak |Tak |Tak |
| SendFailure |Tak |Tak |Tak |Tak |
| PipelineFailure |Tak |Tak |Tak |Nie |
| ConnectionClosed |Tak |Tak |Tak |Nie |
| KeepAliveFailure |Tak |Tak |Tak |Nie |
| Nieznany |Tak |Tak |Tak |Nie |
| ReceiveFailure |Tak |Tak |Tak |Nie |
| RequestCanceled |Tak |Tak |Tak |Nie |
| Limit czasu |Tak |Tak |Tak |Nie |
| ProtocolError <br/>Ponów próbę Hello na ProtocolError jest kontrolowana przez Obsługa kod stanu HTTP hello. Aby uzyskać więcej informacji, zobacz [kody stanu błędu HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Tak |Tak |Tak |Tak |

### <a name="HTTPStatusCode"></a>Kody stanu błędu HTTP
Podczas operacji zapytania i metody SaveChanges throw DataServiceClientException, DataServiceQueryException lub DataServiceQueryException, hello kod stanu HTTP Błąd jest zwracany w hello StatusCode właściwości.  Witaj poniższej tabeli przedstawiono dla kody błędów Logika ponawiania hello jest zaimplementowana.  

| Stan | Żądanie sieci Web | Magazyn | Zapytanie | Metody SaveChanges |
| --- | --- | --- | --- | --- |
| 401 |Nie |Tak |Nie |Nie |
| 403 |Nie |Tak<br/>Obsługa ponownych prób z czeka dłużej. |Nie |Nie |
| 408 |Tak |Tak |Tak |Tak |
| 429 |Tak |Tak |Tak |Tak |
| 500 |Tak |Tak |Tak |Nie |
| 502 |Tak |Tak |Tak |Nie |
| 503 |Tak |Tak |Tak |Tak |
| 504 |Tak |Tak |Tak |Nie |

Tootake przyjrzeć się hello rzeczywistego wykonania hello SDK usługi Media Services dla platformy .NET Logika ponawiania, zobacz [azure sdk media services dla](https://github.com/Azure/azure-sdk-for-media-services/tree/dev/src/net/Client/TransientFaultHandling).

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

