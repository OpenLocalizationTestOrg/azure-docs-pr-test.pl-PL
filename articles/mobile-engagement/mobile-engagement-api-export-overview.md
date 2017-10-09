---
title: "Przegląd interfejsu API wyeksportować zaangażowania aaaMobile"
description: "Dowiedz się hello podstawowe informacje o eksportowaniu danych pierwotnych wygenerowanych przez użytkownika urządzenia tooleverage go w własnych narzędzi"
services: mobile-engagement
documentationcenter: mobile
author: kpiteira
manager: erikre
editor: 
ms.assetid: 9380d47b-d7fa-4d4c-888f-97e6482196bb
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 04/26/2016
ms.author: kapiteir
ms.openlocfilehash: f55be29a29878e74f6a33419f08a5574a07a7478
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mobile-engagement-export-api-overview"></a>Przegląd interfejsu API usługi Mobile Engagement eksportu
## <a name="introduction"></a>Wprowadzenie
W tym dokumencie dowiesz się hello podstawowe informacje o eksportowaniu danych pierwotnych wygenerowanych przez użytkownika urządzenia tooleverage go w własnych narzędzi.

## <a name="pre-requisites"></a>Wymagania wstępne
Eksportowanie hello nieprzetworzone dane z usługi Mobile Engagement wymaga:

* Interfejs API uwierzytelniania Instalator toobe toouse stanie hello interfejsów API (zobacz [instalacji ręcznej uwierzytelniania](mobile-engagement-api-authentication-manual.md)),
* Użyj hello interfejsów API REST lub hello [.net SDK](mobile-engagement-dotnet-sdk-service-api.md),
* Konto magazynu Azure.

> [!NOTE]
> Zaleca się również hello znakomity [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/), co najmniej w fazie programowanie hello, ponieważ zapewnia łatwe toouse interfejsu użytkownika do interakcji z usługą Azure Storage.
> 
> 

## <a name="what-can-be-exported"></a>Co można eksportować?
Usługa Mobile Engagement umożliwia jego toocollect użytkowników wiele typów danych i w związku z tym ma kilka typów eksportu odpowiednie toothese różnych typów danych.
Istnieją 2 podstawowych typów eksportu:

* Migawki: zwykle używane tooexport danych, który reprezentuje stan i dla którego usługa Mobile Engagement ma historię. W tym na przykład tag (app-info), tokeny lub wypychanej kampanii opinie. W rezultacie tych typów eksportu nie są związane z datą tooa.
* historyczne: ten typ eksportu jest używany dla danych, które akumuluje wraz z upływem czasu, takich jak działania lub zdarzenia, na przykład.

Witaj w poniższej tabeli opisano wyczerpujący wszystkich hello możliwe eksportu:

| Typ eksportu | Typ danych | Opis |
| --- | --- | --- |
| Snapshot |Wypychanie |Generuje eksportu kampanie wypychania opinie na podstawie na deviceid/nazwa użytkownika |
| Snapshot |Tag |Generuje eksportu hello tag (app-info) skojarzone tooeach urządzeń |
| Snapshot |Urządzenie |Generuje eksportu większość hello danych dotyczących urządzeń, takich jak technicals hello (modelu, ustawienia regionalne, strefa czasowa,...), tagi hello, po raz pierwszy dostępny... |
| Snapshot |Token |Generuje eksportu wszystkie hello prawidłowych tokenów. |
| Historyczne |Działanie |Generuje eksportu wszystkie operacje powitania dla każdego urządzenia w danym okresie czasu |
| Historyczne |Wydarzenie |Generuje eksportu wszystkie operacje powitania dla każdego urządzenia w danym okresie czasu |
| Historyczne |Zadanie |Generuje eksportu wszystkie zadania powitania dla każdego urządzenia w danym okresie czasu |
| Historyczne |Błąd |Generuje eksportu wszystkich błędów powitania dla każdego urządzenia w danym okresie czasu |

## <a name="how-does-it-work"></a>Jak to działa?
Eksportowanie jest długa uruchomionych zadań, które mogą być bardzo duże pliki danych. Z tego powodu nie można tooreturn wywoływanej natychmiast toodownload pliku.
W kolejności tooexport dane z usługi Mobile Engagement, będą miały toocreate **zadania eksportu** za pomocą interfejsu API, które zazwyczaj określić:

* Typ Hello eksportu (migawki lub historycznych)
* Typ danych Hello,
* Witaj **kontenera magazynu Azure** (w tym prawidłowe sygnatury dostępu Współdzielonego z uprawnieniami do zapisu) którym zostanie zapisany wynik hello hello eksportu.
* np. parametr adresu URL kontenera przykład byłoby https://[StorageAccountName].blob.core.windows.net/[ContainerName]? [SASWritePermissionsToken]  

Oto przykład rzeczywistych. https://testazmeexport.blob.Core.Windows.NET/test1234azme?SV=2015-12-11&ss=b&SRT=SCO&SP=rwdlac&SE=2016-12-17T04:59:26Z & st = 2016-12-16T20:59:26Z & spr = https & sig = KRF3aVWjp2NEJDzjlmoplmu0M9HHlLdkBWRPAFmw90Q % 3D

Należy pamiętać, że może potrwać kilka minut, aż Twoje toobe zadanie uruchomione, a następnie może uruchomić od kilku sekund godzin tooseveral niewielki rozmiar aplikacji dla aplikacji z wielu użytkowników lub działania.

Po utworzeniu zadania hello jest możliwe toocheck toosee jej stan, jeśli jest nadal uruchomiona lub jeśli została ukończona.

Gdy zadanie hello jest zakończyło się pomyślnie, hello wynikowy plik danych jest dostępna na powitania podano kontenera magazynu.

