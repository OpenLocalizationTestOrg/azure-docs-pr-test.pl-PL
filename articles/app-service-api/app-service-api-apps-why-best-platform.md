---
title: wprowadzenie aplikacji aaaAPI | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak usługa Azure App Service pomaga tworzyć i obsługiwać interfejsy API RESTful oraz z nich korzystać."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 60049a16-8159-47aa-a34b-110be0d8dab6
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: alkarche
ms.openlocfilehash: f066e96db667d4685480001bc43c2b1bff4ea352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-apps-overview"></a>Omówienie API Apps
Aplikacje interfejsu API w usłudze Azure App Service funkcji oferty, dzięki któremu można łatwiej toodevelop hosta i korzystanie z interfejsów API w chmurze hello i lokalnych. Aplikacje interfejsu API zapewniają zabezpieczenia klasy korporacyjnej, prostą kontrolę dostępu, połączenia hybrydowe, automatyczne generowanie zestawów SDK oraz bezproblemową integrację z usługą [Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).

[Usługa Azure App Service](../app-service/app-service-value-prop-what-is.md) to w pełni zarządzana platforma obsługująca scenariusze dotyczące integracji, sieci Web oraz urządzeń przenośnych. Funkcja API Apps należy do zestawu obejmującego cztery typy aplikacji udostępniane przez [usługę Azure App Service](../app-service/app-service-value-prop-what-is.md).

![Typy aplikacji w usłudze Azure App Service](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## <a name="why-use-api-apps"></a>Dlaczego warto używać aplikacji API Apps?
Oto główne funkcje aplikacji API Apps:

* **Przełącz istniejący interfejs API jako — jest** — nie masz toochange żadnego hello kod w istniejących interfejsów API tootake korzyści aplikacji interfejsu API — wystarczy go wdrożyć w aplikacji interfejsu API tooan kodu. Interfejs API może korzystać z dowolnego języka lub platformy obsługiwanej przez usługę App Service, na przykład ASP.NET, C#, Java, PHP, Node.js lub Python.
* **Łatwość użycia** — dzięki zintegrowanej obsłudze [metadanych interfejsu API programu Swagger](http://swagger.io/) interfejsy API są łatwo dostępne dla różnych klientów.  Za pomocą różnych języków, takich jak C#, Java i Javascript, można automatycznie generować kod klienta dla interfejsów API. [Mechanizm CORS](app-service-api-cors-consume-javascript.md) można łatwo konfigurować bez zmieniania kodu. Aby uzyskać więcej informacji, zobacz artykuły [App Service API Apps metadata for API discovery and code generation](app-service-api-metadata.md) (Metadane funkcji App Service API Apps służące do odnajdywania interfejsów API i generowania kodu) oraz [Korzystanie z aplikacji interfejsu API z poziomu języka JavaScript przy użyciu mechanizmu CORS](app-service-api-cors-consume-javascript.md). 
* **Prosta kontrola dostępu** — ochrona aplikacji interfejsu API przed nieuwierzytelnionym dostępem bez zmiany kodu tooyour. Wbudowane usługi uwierzytelniania umożliwiają zabezpieczenie interfejsów API przed dostępem innych usług lub klientów reprezentujących użytkowników. Obsługiwani dostawcy tożsamości obejmują usługę Azure Active Directory, konta Google i Microsoft oraz serwisy Facebook i Twitter. Klienci mogą używać biblioteki uwierzytelniania usługi Active Directory (ADAL) lub hello zestaw SDK usługi Mobile Apps. Aby uzyskać więcej informacji, zobacz [Authentication and authorization for API Apps in Azure App Service](app-service-api-authentication.md) (Uwierzytelnianie i autoryzacja aplikacji interfejsu API w usłudze Azure App Service).
* **Integracja z programem Visual Studio** — dedykowane narzędzia w programie Visual Studio usprawnić pracę hello tworzenie, wdrażanie, wykorzystywanie, debugowanie i zarządzanie aplikacje interfejsu API. Aby uzyskać więcej informacji, zobacz [Announcing hello Azure SDK 2.8.1 dla platformy .NET](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).
* **Integracja z funkcją Logic Apps** — tworzone aplikacje interfejsu API mogą być używane przez funkcję [App Service Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).  Aby uzyskać więcej informacji, zobacz artykuły [Using your custom API hosted on App Service with Logic apps](../logic-apps/logic-apps-custom-hosted-api.md) (Używanie niestandardowego interfejsu API hostowanego przez usługę App Service razem z aplikacjami Logic Apps) oraz [New schema version 2015-08-01-preview](../logic-apps/logic-apps-schema-2015-08-01.md) (Nowa wersja schematu 2015-08-01-preview).

Ponadto aplikacja interfejsu API może korzystać z funkcji udostępnianych przez usługi [Web Apps](../app-service-web/app-service-web-overview.md) i [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md). Witaj odwrotnej również ma wartość true: użycie aplikacji sieci web lub aplikacji mobilnej toohost interfejsu API może korzystać z funkcji API Apps, takich jak metadane programu Swagger dla klienta generowanie kodu i mechanizmu CORS przeglądarce międzydomenowy dostęp. Hello jedyna różnica między hello trzy typy aplikacji (API, sieci web i mobilnych) jest hello nazw oraz ikon dla nich w hello portalu Azure.

## <a name="whats-hello-difference-between-api-apps-and-azure-api-management"></a>Jaka jest różnica hello Azure API Management i aplikacji API Apps?
API Apps i [Azure API Management](../api-management/api-management-key-concepts.md) to usługi, które się uzupełniają:

* Usługa API Management służy do zarządzania interfejsami API. Możesz zawiesić frontonu usługi API Management toomonitor interfejsu API i ograniczania użycia, manipulować danymi wejściowymi i dane wyjściowe, integrować kilka interfejsów API w jednym punkcie końcowym i tak dalej. Hello zarządzane interfejsy API mogą być hostowane w dowolnym miejscu.
* Usługa API Apps umożliwia hostowanie interfejsów API. Usługa Hello obejmuje funkcje ułatwiające tworzenie i spójniejsze interfejsów API, ale nie hello rodzaje monitorowania, ograniczania przepustowości, manipulowanie lub konsolidacji, że jest zarządzanie interfejsami API. Jeśli funkcje usługi API Management nie są potrzebne, można hostować interfejsy API w usłudze API Apps.

Na poniższym schemacie przedstawiono użycie usługi API Management w celu korzystania z interfejsów API hostowanych w usłudze API Apps i innych miejscach.

![Usługi Azure API Management i API Apps](./media/app-service-api-apps-why-best-platform/apia-apim.png)

Niektóre funkcje usług API Management i API Apps działają podobnie,  na przykład umożliwiają automatyzację obsługi mechanizmu CORS. Jeśli korzystasz ze sobą Witaj dwie usługi, należy użyć interfejsu API zarządzania do obsługi mechanizmu CORS ponieważ działa ona jako fronton tooyour interfejsu API aplikacji hello. 

## <a name="getting-started"></a>Wprowadzenie
tooget wprowadzenie do API Apps przez wdrożenie przykładowy kod tooone, zobacz samouczek powitania dla różnych platform, które chcesz:

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.js](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

tooask pytania dotyczące aplikacji interfejsu API, Utwórz wątek hello [forum usługi API Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps). 

