---
title: "metadane aaaOpenAPI w usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Omówienie obsługi OpenAPI w funkcji platformy Azure"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a>Obsługa metadanych OpenAPI 2.0 w funkcjach Azure (wersja zapoznawcza)
OpenAPI 2.0 (dawniej Swagger) Obsługa metadanych w usługi Azure Functions to funkcja podglądu służy definicji toowrite 2.0 OpenAPI wewnątrz aplikacji funkcji. Następnie można obsługiwać tego pliku przy użyciu hello funkcji aplikacji.

[Metadane OpenAPI](http://swagger.io/) umożliwia funkcji, który jest hostem toobe interfejsu API REST wykorzystanych w ramach szerokiej gamy innego oprogramowania. Oprogramowanie zawiera oferty firmy Microsoft, takich jak PowerApps i hello [funkcji aplikacji interfejsu API usługi Azure App Service](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), narzędzia dla deweloperów innych firm, takich jak [Postman](https://www.getpostman.com/docs/importing_swagger), i [wiele pakietów więcej](http://swagger.io/tools/).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
>Firma Microsoft zaleca, począwszy od hello [Wprowadzenie — samouczek](./functions-api-definition-getting-started.md) i toolearn dokumentu toothis następnie zwracanie, więcej informacji na temat określonych funkcji.

## <a name="enable"></a>Włącz obsługę definicji OpenAPI
Można skonfigurować wszystkie ustawienia OpenAPI na powitania **definicji interfejsu API** strony aplikacji funkcji **funkcji platformy**.

Ustaw tooenable hello Generowanie hostowanej definicji OpenAPI i definicję szybkiego startu **źródła definicji interfejsu API** za**— funkcja (wersja zapoznawcza)**. **Zewnętrzny adres URL** umożliwia toouse Twojego funkcja definicji OpenAPI, która ma hostowaną w innym miejscu.

## <a name="generate-definition"></a>Generowanie szkielet Swagger z metadanych funkcji składowanej
Szablon może pomóc rozpocząć pisanie pierwszego definicję OpenAPI. Hello definicja szablonu funkcji tworzy rozrzedzonych definicji OpenAPI przy użyciu wszystkich metadanych hello w pliku function.json powitania dla każdej funkcji wyzwalacza HTTP. Należy toofill w więcej informacji na temat interfejsu API z hello [specyfikacji OpenAPI](http://swagger.io/specification/), takie jak szablony żądań i odpowiedzi.

Aby uzyskać instrukcje krok po kroku, zobacz hello [Wprowadzenie — samouczek](./functions-api-definition-getting-started.md).

### <a name="templates"></a>Dostępne szablony

|Nazwa| Opis |
|:-----|:-----|
|Wygenerowany definicji|Definicja OpenAPI z hello maksymalną ilość informacji, które można wywnioskować na podstawie metadanych istniejących hello funkcji.|

### <a name="quickstart-details"></a>Metadane uwzględnione w hello wygenerowane definicji

powitania po tabeli reprezentuje hello ustawienia portalu Azure i odpowiadające im dane w function.json ponieważ jest on szkielet Swagger zamapowanych toohello wygenerowany.

|Swagger.JSON|Portal interfejsu użytkownika|Function.JSON|
|:----|:-----|:-----|
|[Host](http://swagger.io/specification/#fixed-fields-15)|**Ustawienia aplikacji funkcji** > **ustawienia aplikacji usługi** > **omówienie** > **adresu URL**|*Nie istnieje*
|[Ścieżki](http://swagger.io/specification/#paths-object-29)|**Integracja** > **metod HTTP wybrane**|Powiązania: trasy
|[Ścieżka elementu](http://swagger.io/specification/#path-item-object-32)|**Integracja** > **szablon trasy**|Powiązania: metody
|[Bezpieczeństwo](http://swagger.io/specification/#security-scheme-object-112)|**Klucze**|*Nie istnieje*|
|operationID *|**Trasy + dozwolone zlecenia**|Trasy + dozwolonych poleceń|

\*Identyfikator operacji Hello jest wymagana tylko w przypadku integracji z PowerApps i przepływów.
> [!NOTE]
> rozszerzenie x-ms podsumowanie Hello zawiera nazwę wyświetlaną w aplikacji logiki, PowerApps i przepływów.
>
> toolearn więcej, zobacz [Dostosowywanie definicji struktury Swagger Twoje rozwiązanie PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).

## <a name="CICD"></a>Użyj elementu konfiguracji/CD definicji tooset interfejsu API

 Należy włączyć interfejsu API definicji hosting w portalu hello przed włączeniem toomodify kontroli źródła z definicji interfejsu API z kontroli źródła. Wykonaj te instrukcje:

1. Przeglądaj zbyt**definicji interfejsu API (wersja zapoznawcza)** w ustawieniach funkcji aplikacji.
  1. Ustaw **źródła definicji interfejsu API** za**funkcja**.
  1. Kliknij przycisk **API generowania definicji szablonu** , a następnie **zapisać** toocreate definicji szablonu modyfikowania później.
  1. Należy pamiętać, Twój adres URL definicji interfejsu API i klucz.
1. [Konfigurowanie ciągłej integracji/ciągłego wdrażania (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).
2. Modyfikowanie swagger.json w kontroli źródła na \site\wwwroot\.azurefunctions\swagger\swagger.json.

Teraz zmiany tooswagger.json w repozytorium, są obsługiwane przez aplikację funkcja pod adresem URL definicji interfejsu API hello i klucz zanotowaną w kroku 1.c.

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie — samouczek](functions-api-definition-getting-started.md). Spróbuj toosee nasze wskazówki OpenAPI definicji działania.
* [Azure repozytorium GitHub funkcji](https://github.com/Azure/Azure-Functions/). Zapoznaj się z toogive repozytorium funkcje hello nam opinii na temat Podglądu pomocy technicznej definicji hello interfejsu API. Tworzenie problem GitHub dla dowolną toosee aktualizacji.
* [Dokumentacja dla deweloperów usługi Azure funkcji](functions-reference.md). Więcej informacji na temat kodowania funkcji oraz definiowania wyzwalaczy i powiązań.
