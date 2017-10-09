---
title: "aaaImport interfejs API do usługi Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooimport interfejsu API i jego operacji do usługi Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a>Jak tooimport hello definicji interfejsu API z operacjami w usłudze Azure API Management
W usłudze API Management można tworzyć nowych interfejsów API i operacji hello ręcznie dodawać lub hello interfejsu API można zaimportować wraz z operacji hello w jednym kroku.

Interfejsy API i ich operacje mogą być importowane przy użyciu następujących formatów hello.

* WADL
* Swagger

W tym przewodniku pokazano, jak tworzyć nowy interfejs API i zaimportować jego operacji w jednym kroku. Informacje dotyczące ręcznego tworzenia interfejsu API i dodawanie działań, zobacz [jak toocreate interfejsów API] [ How toocreate APIs] i [jak tooadd tooan operacje interfejsu API] [ How tooadd operations tooan API].

## <a name="import-api"> </a>Importowanie interfejsu API
Interfejsy API są tworzone i skonfigurować w portalu wydawcy hello. tooaccess hello wydawcy portalu, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API. Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.

![Portal wydawcy][api-management-management-console]

Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **zaimportować interfejsu API**.

![Interfejs API importu][api-management-import-apis]

Witaj **Import API** okno ma trzy karty odpowiadające toohello trzy sposoby tooprovide hello interfejsu API specyfikacji.

* **Ze Schowka** umożliwia toopaste specyfikacji hello interfejsu API w polu tekstowym wyznaczonych hello.
* **Z pliku** pozwala toobrowse tooand hello wybierz plik, który zawiera specyfikację hello interfejsu API.
* **Z adresu URL** pozwala toosupply hello adresu URL toohello specyfikacji hello interfejsu API.

![Format importu interfejsu API][api-management-import-api-clipboard]

Po podaniu specyfikacji hello interfejsu API, użyj przycisków radiowych hello na powitania prawo tooindicate hello specyfikacji formatu. Witaj następujące formaty są obsługiwane.

* WADL
* Swagger

Następnie wprowadź **sufiks adresu URL interfejsu API sieci Web**. To jest dołączany toohello podstawowego adresu URL dla interfejsu API usługi zarządzania. podstawowy adres URL Hello jest typowe dla wszystkich interfejsów API hostowanych na każde wystąpienie usługi Zarządzanie interfejsami API. Zarządzanie interfejsami API odróżnia interfejsy API według ich sufiks i w związku z tym sufiks hello muszą być unikatowe dla każdego interfejsu API w określonym wystąpieniu usługi interfejsu API zarządzania.

Po wprowadzeniu wszystkich wartości kliknij **zapisać** toocreate hello API i hello skojarzone operacji. 

> [!NOTE]
> Samouczek importowania podstawowe Kalkulator interfejsu API w formacie struktury Swagger, zobacz [Zarządzanie pierwszy interfejs API usługi Azure API Management](api-management-get-started.md).
> 
> 

## <a name="export-api"></a> Wyeksportować interfejsu API
W tooimporting dodanie nowych interfejsów API, można wyeksportować definicje hello swoje interfejsy API z hello wydawcy portalu. toodo tak, kliknij przycisk **wyeksportować interfejsu API** z hello **karta Podsumowanie** z Twojej **interfejsu API**.

![Eksportuj interfejsu API][api-management-export-api]

Interfejsy API można wyeksportować za pomocą WADL lub struktury Swagger. Zaznacz pożądany format hello, kliknij przycisk **zapisać**, a następnie wybierz lokalizację hello w plik, który hello toosave.

![Format eksportu interfejsu API][api-management-export-api-format]

## <a name="next-steps"> </a>Następne kroki
Po utworzeniu interfejsu API i operacje hello zaimportowane, można zobaczyć i skonfigurować dodatkowe ustawienia, Dodaj hello interfejsu API tooa produktu, a następnie opublikować go, aby była ona dostępna dla deweloperów. Aby uzyskać więcej informacji zobacz następujące przewodniki hello.

* [Jak ustawienia tooconfigure interfejsu API][How tooconfigure API settings]
* [Jak toocreate i opublikuj produktu][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
