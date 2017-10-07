---
title: "toocreate aaaHow interfejsów API w usłudze Azure API Management"
description: "Dowiedz się, jak toocreate i skonfigurować interfejsów API w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a>Jak toocreate interfejsów API w usłudze Azure API Management
Interfejs API w usłudze API Management reprezentuje zestaw operacji, które może być wywoływany przez aplikacje klienckie. Nowe interfejsy API są tworzone w portalu wydawcy hello, a następnie hello potrzebne, że operacje są dodawane. Po dodaniu hello operacje, hello interfejsu API jest dodawany tooa produktu i mogą być publikowane. Po opublikowaniu interfejsu API można subskrybowanego tooand używane przez programistów.

Ten przewodnik przedstawia hello pierwszym krokiem w procesie hello: jak toocreate i skonfiguruj nowy interfejs API w usłudze API Management. Aby uzyskać więcej informacji na operacje dodawania i publikowania produktu, zobacz [jak tooadd tooan operacje interfejsu API] [ How tooadd operations tooan API] i [jak toocreate i opublikuj produktu] [ How toocreate and publish a product].

## <a name="create-new-api"></a>Utwórz nowy interfejs API
Interfejsy API są tworzone i skonfigurować w portalu wydawcy hello. tooaccess hello wydawcy portalu, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.

![Portal wydawcy][api-management-management-console]

> Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.
> 
> 

Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **dodać interfejsu API**.

![Tworzenie interfejsu API][api-management-create-api]

Użyj hello **dodać nowy interfejs API** tooconfigure okna hello nowy interfejs API.

![Dodawanie nowego interfejsu API][api-management-add-new-api]

Hello następujące pola są używane tooconfigure hello nowy interfejs API.

* **Nazwa interfejsu API sieci Web** to unikatowa i opisowa nazwa hello interfejsu API. Jest on wyświetlany w portalach hello deweloperów i wydawcy.
* **Adres URL usługi sieci Web** odwołania hello implementacja interfejsu API hello usługi HTTP. Zarządzanie interfejsami API przekazuje żądania toothis adres.
* **Sufiks adresu URL interfejsu API sieci Web** jest dołączany toohello podstawowego adresu URL dla usługi zarządzania hello interfejsu API. podstawowy adres URL Hello jest typowe dla wszystkich interfejsów API hostowanych przez wystąpienie usługi Zarządzanie interfejsami API. Zarządzanie interfejsami API odróżnia interfejsy API według ich sufiks i w związku z tym sufiks hello muszą być unikatowe dla każdego interfejsu API dla danego wydawcy.
* **Schemat adresu URL interfejsu API sieci Web** określa protokoły mogą być używane tooaccess hello API. HTTPs jest określony, domyślnie.
* toooptionally dodać produkt tooa interfejsu API, kliknij polecenie hello **produktów (opcjonalnie)** listy rozwijanej i wybierz produkt. Ten krok może być powtarzane wiele razy tooadd hello interfejsu API toomultiple produktów.

Po hello potrzebne wartości są skonfigurowane, kliknij przycisk **zapisać**. Po utworzeniu nowego interfejsu API hello hello strony podsumowania dla interfejsu API hello jest wyświetlana w hello wydawcy portalu.

![Podsumowanie interfejsu API][api-management-api-summary]

## <a name="configure-api-settings"></a>Ustawień skonfiguruj interfejsu API
Można użyć hello **ustawienia** karcie tooverify i edytować hello konfigurację interfejsu API. **Nazwa interfejsu API sieci Web**, **adres URL usługi sieci Web**, i **sufiks adresu URL interfejsu API sieci Web** początkowo są ustawiane podczas hello interfejsu API jest tworzony i mogą być modyfikowane w tym miejscu. **Opis** zapewnia opcjonalny opis, a **schemat adresu URL interfejsu API sieci Web** określa protokoły mogą być używane tooaccess hello API.

![Ustawienia interfejsu API][api-management-api-settings]

Uwierzytelnianie bramy tooconfigure hello wewnętrznej bazy danych usługi implementującej hello interfejsu API, wybierz hello **zabezpieczeń** hello kartę **przy użyciu poświadczeń** listy rozwijanej mogą być używane tooconfigure **HTTP podstawowe** lub **certyfikaty klienta** uwierzytelniania. Uwierzytelnianie podstawowe toouse HTTP, wystarczy wprowadzić poświadczenia hello potrzebne. Uzyskać przy użyciu uwierzytelniania certyfikatu klienta, zobacz [jak za pomocą klienta usług zaplecza toosecure certyfikatów uwierzytelniania w usłudze Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].

Witaj **zabezpieczeń** karty mogą być również używane tooconfigure **autoryzacji użytkownika** przy użyciu protokołu OAuth 2.0. Aby uzyskać więcej informacji, zobacz [jak kont przy użyciu narzędzia Projektant tooauthorize OAuth 2.0 w usłudze Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].

![Ustawień uwierzytelniania podstawowego][api-management-api-settings-credentials]

Kliknij przycisk **zapisać** toosave wszystkie wprowadzone zmiany toohello ustawień interfejsu API.

## <a name="next-steps"> </a>Następne kroki
Po utworzeniu interfejsu API i skonfigurowane ustawienia hello, hello następne kroki są tooadd hello operacji toohello interfejsu API, Dodaj hello interfejsu API tooa produktu, a następnie opublikować go, aby była ona dostępna dla deweloperów. Aby uzyskać więcej informacji zobacz następujące artykuły hello.

* [Jak tooadd tooan operacje interfejsu API][How tooadd operations tooan API]
* [Jak toocreate i opublikuj produktu][How toocreate and publish a product]

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
