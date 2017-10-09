---
title: "aaaClient i serwer przechowywanie wersji zestawu SDK w usługach Mobile i aplikacje mobilne | Dokumentacja firmy Microsoft"
description: "Lista zestawów SDK klienta i zgodności serwera wersje zestawu SDK usług Mobile Services i usługi Azure Mobile Apps"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a>Przechowywanie wersji klienta i serwera w usługach Mobile i aplikacje mobilne
najnowszą wersję usług Azure Mobile Services Hello jest hello **Mobile Apps** funkcji Azure App Service.

Witaj klienta aplikacji mobilnych i zestawów SDK serwera są początkowo na podstawie usług Mobile Services, ale są one *nie* zgodne ze sobą.
Oznacza to, należy użyć *Mobile Apps* zestawu SDK klienta z *Mobile Apps* serwera zestawu SDK i podobnie dla *usług Mobile Services*. Niniejsza Umowa jest wymuszane za pośrednictwem wartość nagłówka specjalnych używanych przez powitania klienta i serwera zestawów SDK, `ZUMO-API-VERSION`.

Uwaga: po każdej zmianie tego dokumentu dotyczy tooa *usług Mobile Services* wewnętrznej bazy danych, nie zawsze musi toobe hostowanych w usłudze Mobile Services. Teraz jest możliwe toomigrate toorun usługi mobilnej w usłudze aplikacji bez wprowadzania żadnych zmian kodu, ale usługa hello będą nadal stosowane *usług Mobile Services* wersji zestawu SDK.

więcej informacji o toolearn migracji tooApp usługi bez wprowadzania żadnych zmian kodu zawiera artykuł hello [migracji tooAzure usługi Mobile App Service].

## <a name="header-specification"></a>Specyfikacja nagłówka
klucz Hello `ZUMO-API-VERSION` można określić nagłówka hello HTTP lub hello ciągu zapytania. wartość Hello jest ciąg wersji w postaci hello **x.y.z**.

Na przykład:

Pobierz https://service.azurewebsites.net/tables/TodoItem

NAGŁÓWKI: ZUMO-API-VERSION: 2.0.0

POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0

## <a name="opting-out-of-version-checking"></a>Rezygnacja z kontroli wersji
Można zrezygnować z wersji sprawdzanie przez ustawienie wartości **true** dla ustawienia aplikacji hello **MS_SkipVersionCheck**. Określ, w pliku web.config albo w hello sekcji Ustawienia aplikacji hello portalu Azure.

> [!NOTE]
> Istnieje wiele zmian zachowania między usług Mobile Services i aplikacji mobilnych, zwłaszcza w obszarach hello synchronizacji w trybie offline, uwierzytelniania i powiadomień wypychanych. Należy tylko opcja rezygnacji z wersji sprawdzania po pełną tooensure testowych, czy te zmiany zachowania nie dzielone funkcjonalności aplikacji.
>
>

## <a name="summary-of-compatibility-for-all-versions"></a>Podsumowanie zgodności dla wszystkich wersji
Wykres Hello poniżej przedstawia zgodność hello wszystkie typy klienta i serwera. Wewnętrznej bazie danych zostanie sklasyfikowany jako albo Mobile **usług** lub Mobile **aplikacji** oparte na powitania serwera zestawu SDK, który go używa.

|  | **Usługi mobilne** Node.js lub .NET | **Aplikacje mobilne** Node.js lub .NET |
| --- | --- | --- |
| [Klienci usług Mobile Services] |Ok |Błąd\* |
| [Aplikacje mobilne klientów] |Błąd\* |Ok |

\*Może to być kontrolowane przez określenie **MS_SkipVersionCheck**.

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a>Usługi mobilne klienta i serwera
powitania klienta zestawów SDK w poniższej tabeli hello są zgodne z **usług Mobile Services**.

Uwaga: hello zestawów SDK klienta usługi Mobile Services *nie* wysyłania wartości nagłówka `ZUMO-API-VERSION`. Jeśli usługa hello odbiera ten nagłówek lub ciąg zapytania zostanie zwrócony błąd, chyba że jawnie użytkownik zgodził się zgodnie z powyższym opisem.

### <a name="MobileServicesClients"></a>Mobile *usług* zestawów SDK klienta
| Platforma klienta | Wersja | Wartość nagłówka wersji |
| --- | --- | --- |
| Klient zarządzany (z systemem Windows, Xamarin) |[1.3.2](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |Nie dotyczy |
| iOS |[2.2.2](http://aka.ms/gc6fex) |Nie dotyczy |
| Android |[2.0.3](https://go.microsoft.com/fwLink/?LinkID=280126) |Nie dotyczy |
| HTML |[1.2.7](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |Nie dotyczy |

### <a name="mobile-services-server-sdks"></a>Mobile *usług* server SDK
| Platforma serwera | Wersja | Zaakceptowana wersja nagłówka |
| --- | --- | --- |
| .NET |[Wersja WindowsAzure.MobileServices.Backend.* 1.0.x](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |** Bez nagłówka wersji ** |
| Node.js |(wkrótce) |**Brak nagłówka wersji** |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a>Zachowanie zapleczy usług mobilnych
| ZUMO-API-VERSION | Wartość MS_SkipVersionCheck | Odpowiedź |
| --- | --- | --- |
| Nie określono |Dowolne |200 - OK |
| Dowolna wartość |True |200 - OK |
| Dowolna wartość |Określona wartość false nie |400 - Niewłaściwe żądanie |

## <a name="2.0.0"></a>Azure Mobile Apps klienta i serwera
### <a name="MobileAppsClients"></a>Mobile *aplikacji* zestawów SDK klienta
Sprawdzanie wersji wprowadzono począwszy hello następujące wersje klienta hello zestawu SDK dla **Azure Mobile Apps**:

| Platforma klienta | Wersja | Wartość nagłówka wersji |
| --- | --- | --- |
| Klient zarządzany (z systemem Windows, Xamarin) |[2.0.0](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |2.0.0 |
| iOS |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=529823) |2.0.0 |
| Android |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |3.0.0 |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a>Mobile *aplikacji* server SDK
Sprawdzanie wersji znajduje się w następujących wersjach zestawu SDK serwera:

| Platforma serwera | SDK | Zaakceptowana wersja nagłówka |
| --- | --- | --- |
| .NET |[Microsoft.Azure.Mobile.Server](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |2.0.0 |
| Node.js |[aplikacje Azure-mobile)](https://www.npmjs.com/package/azure-mobile-apps) |2.0.0 |

### <a name="behavior-of-mobile-apps-backends"></a>Zachowanie zapleczy aplikacji mobilnych
| ZUMO-API-VERSION | Wartość MS_SkipVersionCheck | Odpowiedź |
| --- | --- | --- |
| x.y.z ani mieć wartości Null |True |200 - OK |
| Wartość null |Określona wartość false nie |400 - Niewłaściwe żądanie |
| 1.x.y |Określona wartość false nie |400 - Niewłaściwe żądanie |
| 2.0.0-2.x.y |Określona wartość false nie |200 - OK |
| 3.0.0-3.x.y |Określona wartość false nie |400 - Niewłaściwe żądanie |

## <a name="next-steps"></a>Następne kroki
* [migracji tooAzure usługi Mobile App Service]

[Klienci usług Mobile Services]: #MobileServicesClients
[Aplikacje mobilne klientów]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[migracji tooAzure usługi Mobile App Service]: app-service-mobile-migrating-from-mobile-services.md
