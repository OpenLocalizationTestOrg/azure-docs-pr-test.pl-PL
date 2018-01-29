---
title: "Dodawanie buforowania w celu poprawy wydajności usługi Azure API Management | Microsoft Docs"
description: "Dowiedz się, jak poprawić czas oczekiwania, zużycie przepustowości i obciążenie usługi sieci Web w przypadku wywołań usługi API Management."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7458ad6e0a864d742f74ce743ce3179594113c00
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2017
---
# <a name="add-caching-to-improve-performance-in-azure-api-management"></a>Dodawanie buforowania w celu poprawy wydajności usługi Azure API Management
Operacje w usłudze API Management można skonfigurować do buforowania odpowiedzi. Buforowanie odpowiedzi może znacznie zmniejszyć opóźnienie interfejsu API, zużycie przepustowości i obciążenie usługi sieci Web w przypadku danych, które nie zmieniają się często.
 
Aby uzyskać bardziej szczegółowe informacje na temat buforowania, zobacz [API Management caching policies](api-management-caching-policies.md) (Zasady buforowania w usłudze API Management) i [Custom caching in Azure API Management](api-management-sample-cache-by-key.md) (Buforowanie niestandardowe w usłudze Azure API Management).

![zasady buforowania](media/api-management-howto-cache/cache-policies.png)

Zawartość:

> [!div class="checklist"]
> * Dodawanie buforowania odpowiedzi do interfejsu API
> * Sprawdzanie działania buforowania

## <a name="prerequisites"></a>Wymagania wstępne

W celu ukończenia tego samouczka:

+ [Utwórz wystąpienie usługi Azure API Management](get-started-create-service-instance.md)
+ [Zaimportuj i opublikuj interfejs API](import-and-publish.md)

## <a name="caching-policies"> </a>Dodawanie zasad buforowania

W zasadach buforowania pokazanych w tym przykładzie pierwsze żądanie operacji **GetSpeakers** zwraca odpowiedź z usługi zaplecza. Ta odpowiedź jest zbuforowana z kluczem uwzględniającym określone nagłówki i parametry ciągu zapytania. Dla kolejnych wywołań operacji z pasującymi parametrami będą zwracana buforowaną odpowiedź do czasu wygaśnięcia interwału czasu trwania pamięci podręcznej.

1. Zaloguj się do witryny Azure Portal pod adresem [https://portal.azure.com](https://portal.azure.com).
2. Przejdź do swojego wystąpienia usługi APIM.
3. Wybierz kartę **API**.
4. Kliknij pozycję **Demo Conference API** (Pokazowy interfejs API konferencji) na liście interfejsów API.
5. Wybierz operację **GetSpeakers**.
6. W górnej części ekranu wybierz kartę **Projektowanie**.
7. W oknie **Przychodzące przetwarzanie** kliknij trójkąt (obok ołówka).

    ![edytor kodu](media/api-management-howto-cache/code-editor.png)
8. Wybierz pozycję **Edytor kodu**.
9. W elemencie **inbound** (przychodzące) dodaj następujące zasady:

        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
            <vary-by-header>Authorization</vary-by-header>
        </cache-lookup>

10. W elemencie **outbound** (wychodzące) dodaj następujące zasady:

        <cache-store caching-mode="cache-on" duration="20" />

    **Czas trwania** określa interwał wygasania buforowanych odpowiedzi. W tym przykładzie interwał to **20** sekund.

## <a name="test-operation"> </a>Wywoływanie operacji i testowanie buforowania
Wywołaj operację z portalu dla deweloperów, aby sprawdzić działanie buforowania.

1. W portalu Azure przejdź do swojego wystąpienia usługi APIM.
2. Wybierz kartę **Interfejsy API**.
3. Wybierz interfejs API, do którego dodano zasady buforowania.
4. Wybierz operację **GetSpeakers**.
5. Kliknij kartę **Test** w prawym górnym menu.
6. Kliknij pozycję **Wyślij**.

## <a name="next-steps"> </a>Następne kroki
* Aby uzyskać więcej informacji na temat zasad buforowania, zobacz [Caching policies][Caching policies] (Zasady buforowania) w artykule [API Management policy reference][API Management policy reference] (Dokumentacja zasad usługi API Management).
* Aby poznać informacje na temat buforowania elementów według kluczy przy użyciu wyrażeń zasad, zobacz artykuł [Custom caching in Azure API Management](api-management-sample-cache-by-key.md) (Niestandardowe buforowanie w usłudze Azure API Management).

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: get-started-create-service-instance.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: get-started-create-service-instance.md

[Configure an operation for caching]: #configure-caching
[Review the caching policies]: #caching-policies
[Call an operation and test the caching]: #test-operation
[Next steps]: #next-steps
