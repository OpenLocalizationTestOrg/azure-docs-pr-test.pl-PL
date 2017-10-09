---
title: "kody błędów usługi Media Services aaaAzure | Dokumentacja firmy Microsoft"
description: "Witaj temat zawiera omówienie usługi Azure Media Services kody błędów."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: de1ffd6dee8901a3051eb5032536c3669482d6b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-error-codes"></a>Kody błędów w usłudze Azure Media Services
Korzystając z usługi Microsoft Azure Media Services, może zostać wyświetlony kody błędów HTTP z usługi hello w zależności od problemów, takich jak tokeny uwierzytelniania wygasa tooactions, które nie są obsługiwane w usłudze Media Services. Witaj poniżej znajduje się lista **kody błędów HTTP** mogą być zwrócone przez usługę Media Services oraz hello możliwe powoduje, że dla nich.  

## <a name="400-bad-request"></a>400 Niewłaściwe żądanie
Żądanie hello zawiera nieprawidłowe informacje i zostało odrzucone z powodu tooone hello z następujących powodów:

* Określono nieobsługiwaną wersję interfejsu API. Aktualna wersja powitania dla [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).
* nie określono wersji Hello interfejsu API usługi Media Services. Aby uzyskać informacji na temat sposobu toospecify hello wersja interfejsu API, zobacz [dokumentacja interfejsu API REST Media Services operacji](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).
  
  > [!NOTE]
  > Jeśli używasz tooMedia tooconnect hello .NET lub zestawów SDK Java usługi, hello wersja interfejsu API określono dla Ciebie za każdym razem spróbuj i wykonanie akcji dla usługi Media Services.
  > 
  > 
* Niezdefiniowane właściwości został określony. Nazwa właściwości Hello jest komunikat o błędzie hello. Można określić tylko właściwości, które są członkami danej jednostki. Zobacz [dokumentacja interfejsu API REST usługi Azure Media Services](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) listę obiektów i ich właściwości.
* Określono nieprawidłową wartość właściwości. Nazwa właściwości Hello jest komunikat o błędzie hello. Zobacz hello poprzedniej konsolidacji dla typów prawidłowej właściwości i ich wartości.
* Wartość właściwości nie istnieje i jest wymagany.
* Część określony adres URL hello zawiera nieprawidłowe wartości.
* Próba wprowadzone tooupdate właściwości WriteOnce.
* Próba wprowadzone zadanie, które ma wejściowych zasobu z AssetFile głównej, która nie została określona lub nie można ustalić toocreate.
* Próba wprowadzone tooupdate lokalizatora SAS. Lokalizatory sygnatury dostępu Współdzielonego tylko można utworzyć ani usunąć. Przesyłanie strumieniowe lokalizatorów można aktualizować. Aby uzyskać więcej informacji, zobacz [Lokalizatory](https://docs.microsoft.com/rest/api/media/operations/locator).
* Nieobsługiwana operacja lub zapytanie zostało przesłane.

## <a name="401-unauthorized"></a>401 nieautoryzowane
Nie można uwierzytelnić żądania Hello, (przed może być upoważnionych) z powodu tooone z hello z następujących powodów:

* Brak nagłówka uwierzytelniania.
* Wartość nagłówka uwierzytelnienia zła.
  * Witaj token utracił ważność. 
  * Hello token zawiera nieprawidłowy podpis.

## <a name="403-forbidden"></a>403 Zabroniony
Żądanie hello jest niedozwolona z powodu tooone hello z następujących powodów:

* Witaj konta usługi Media Services nie można odnaleźć lub została usunięta.
* Hello konta usługi Media Services jest wyłączona, a typ żądania hello nie HTTP GET. Operacje usługi zwróci również 403 odpowiedzi.
* Witaj token uwierzytelniania nie zawiera informacji o poświadczeniach użytkowników hello: Nazwa konta i/lub identyfikator subskrypcji. Te informacje można znaleźć w hello rozszerzenie interfejsu użytkownika usługi multimediów dla konta usługi Media Services w portalu zarządzania Azure hello.
* Nie można uzyskać dostępu do zasobu Hello.
  
  * Próba wprowadzone toouse MediaProcessor, który nie jest dostępny dla konta usługi Media Services.
  * Nastąpiła próba tooupdate obiekt JobTemplate zdefiniowany przez usługę Media Services.
  * Próba wprowadzone toooverwrite lokalizatora niektóre inne konta usługi Media Services firmy.
  * Próba wprowadzone toooverwrite ContentKey niektóre inne konta usługi Media Services firmy.
* Nie można utworzyć zasobu Hello powodu tooa usługi przydział został osiągnięty dla konta usługi Media Services hello. Aby uzyskać więcej informacji na powitania przydziały usługi, zobacz [przydziały i ograniczenia](media-services-quotas-and-limitations.md).

## <a name="404-not-found"></a>404 — Nie odnaleziono
Witaj żądania nie jest dozwolona w zasobie z powodu tooone z hello z następujących powodów:

* Próba wprowadzone tooupdate jednostki, która nie istnieje.
* Próba wprowadzone toodelete jednostki, która nie istnieje.
* Próba wprowadzone toocreate jednostki, która łączy tooan jednostki, która nie istnieje.
* Próba wprowadzone tooGET jednostki, która nie istnieje.
* Próba wprowadzone toospecify konta magazynu, który nie jest skojarzony z hello konta usługi Media Services.  

## <a name="409-conflict"></a>409 Konflikt
Żądanie hello jest niedozwolona z powodu tooone hello z następujących powodów:

* Więcej niż jeden AssetFile ma hello nazwy określonej w obrębie hello zasobów.
* Nastąpiła próba toocreate drugi głównej AssetFile w hello zasobów.
* Nastąpiła próba toocreate ContentKey z hello określony identyfikator jest już używany.
* Nastąpiła próba toocreate lokalizatora z hello określony identyfikator jest już używany.
* Więcej niż jeden IngestManifestFile ma hello nazwy określonej w obrębie hello IngestManifest.
* Próba wprowadzone toolink drugi toohello ContentKey szyfrowania magazynu szyfrowane magazynu trwałego.
* Nastąpiła próba toolink hello toohello ContentKey tego samego zasobu.
* Nastąpiła próba toocreate tooan lokalizatora zasobów, których kontenera magazynu nie istnieje lub nie jest już skojarzony z hello zasobów.
* Próba wprowadzone toocreate tooan lokalizatora zasobów, który ma już lokalizatorów 5 w użyciu. (Magazynu azure wymusza hello limit pięciu zasady dostępu współużytkowanego na jeden kontener magazynu).
* Łączenie zasobów tooan IngestManifestAsset konta magazynu nie jest hello takie samo jak konto magazynu hello jest używany przez nadrzędny hello IngestManifest.  

## <a name="500-internal-server-error"></a>500 Wewnętrzny błąd serwera
Podczas przetwarzania żądania hello hello, Media Services napotka błąd uniemożliwiający hello przetwarzania przed kontynuowaniem. Może to być spowodowane tooone hello z następujących powodów:

* Tworzenie zasobu lub zadanie nie powiedzie się, ponieważ informacje o limicie przydziału usługi konta usługi Media Services hello jest tymczasowo niedostępna.
* Tworzenie zasobów lub IngestManifest kontenera magazynu obiektów blob nie powiedzie się, ponieważ informacje o koncie magazynu hello konta jest tymczasowo niedostępna.
* Inne wystąpił nieoczekiwany błąd.

## <a name="503-service-unavailable"></a>503 Usługa jest niedostępna
Serwer Hello jest aktualnie w stanie tooreceive żądań. Ten błąd może być spowodowane przez usługę toohello nadmiernego żądania. Mechanizm ograniczania usługi Media Services ogranicza hello użycie zasobów dla aplikacji, które należy nadmiernego żądania toohello usługi.

> [!NOTE]
> Sprawdź hello błąd komunikat i błąd kodu ciąg tooget bardziej szczegółowe informacje o przyczynie hello, którą uzyskano hello błąd 503. Ten błąd nie zawsze oznacza ograniczania.
> 
> 

Opisy stanu możliwe są:

* "Serwer jest zajęty. Uruchamia poprzedniej tego typu żądania zajęło więcej niż {0} sek."
* "Serwer jest zajęty. Więcej niż {0} żądań na sekundę może być ograniczony."
* "Serwer jest zajęty. Więcej niż {0} żądania w ciągu sekund {1} może być ograniczony."

toohandle ten błąd, firma Microsoft zaleca używanie Logika ponawiania wykładniczego wycofywania. Oznacza to, za pomocą oczekiwania stopniowo dłużej między kolejnymi próbami kolejnych odpowiedzi.  Aby uzyskać więcej informacji, zobacz [bloku aplikacji obsługi błędów przejściowych](https://msdn.microsoft.com/library/hh680905.aspx).

> [!NOTE]
> Jeśli używasz [Azure Media Services SDK dla platformy .net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), hello logiki ponawiania próby dla błędu hello 503 zostało zaimplementowane przez hello zestawu SDK.  
> 
> 

## <a name="see-also"></a>Zobacz też
[Kody błędów zarządzania usługi multimediów](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

