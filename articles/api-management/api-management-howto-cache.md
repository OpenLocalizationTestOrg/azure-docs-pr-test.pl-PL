---
title: "Dodawanie buforowania w celu poprawy wydajności usługi Azure API Management | Microsoft Docs"
description: "Dowiedz się, jak poprawić czas oczekiwania, zużycie przepustowości i obciążenie usługi sieci Web w przypadku wywołań usługi API Management."
services: api-management
documentationcenter: 
author: steved0x
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
ms.openlocfilehash: 59c595f0d5ce849f44c46fdb6cab0b44d35fffa0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="add-caching-to-improve-performance-in-azure-api-management"></a>Dodawanie buforowania w celu poprawy wydajności usługi Azure API Management
Operacje w usłudze API Management można skonfigurować do buforowania odpowiedzi. Buforowanie odpowiedzi może znacznie zmniejszyć opóźnienie interfejsu API, zużycie przepustowości i obciążenie usługi sieci Web w przypadku danych, które nie zmieniają się często.

Ten przewodnik pokazuje, jak dodać buforowanie odpowiedzi do interfejsu API oraz skonfigurować zasady dla przykładowych operacji interfejsu Echo API. Następnie możesz wywołać operację z portalu dla deweloperów, aby sprawdzić działanie buforowania.

> [!NOTE]
> Aby poznać informacje na temat buforowania elementów według kluczy przy użyciu wyrażeń zasad, zobacz artykuł [Custom caching in Azure API Management](api-management-sample-cache-by-key.md) (Niestandardowe buforowanie w usłudze Azure API Management).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Przed wykonaniem kroków w tym przewodniku potrzebne jest wystąpienie usługi API Management ze skonfigurowanymi interfejsem API i produktem. Jeśli jeszcze nie masz utworzonego wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].

## <a name="configure-caching"> </a>Konfigurowanie operacji do buforowania
W tym kroku należy przejrzeć ustawienia buforowania operacji **GET Resource (cached)** (Buforowane pobieranie zasobu) przykładowego interfejsu Echo API.

> [!NOTE]
> Każde wystąpienie usługi API Management ma wstępnie skonfigurowany interfejs Echo API, który może służyć do eksperymentów oraz poznawania usługi API Management. Aby uzyskać więcej informacji, zobacz [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].
> 
> 

Na początku kliknij opcję **Portal wydawcy** w klasycznej witrynie Azure Portal dla usługi API Management. Spowoduje to przejście do portalu wydawcy usługi API Management.

![Portal wydawcy][api-management-management-console]

Aby zaimportować, kliknij opcję **Interfejsy API** z menu **API Management** po lewej stronie, a następnie kliknij pozycję **Echo API**.

![Interfejs Echo API][api-management-echo-api]

Kliknij kartę **Operacje**, a następnie kliknij operację **GET Resource (cached)** z listy **Operacje**.

![Operacje interfejsu Echo API][api-management-echo-api-operations]

Kliknij kartę **Buforowanie**, aby wyświetlić ustawienia buforowania dla tej operacji.

![Karta Buforowanie][api-management-caching-tab]

Aby włączyć buforowanie operacji, zaznacz pole wyboru **Włącz**. W tym przykładzie buforowanie jest włączone.

Każda odpowiedź operacji zawiera klucz generowany na podstawie wartości w polach **Zróżnicuj według parametrów ciągu kwerendy** i **Zróżnicuj na podstawie nagłówków**. Jeśli chcesz buforować wiele odpowiedzi na podstawie parametrów ciągu zapytania lub nagłówków, możesz je skonfigurować w tych dwóch polach.

**Czas trwania** określa interwał wygasania buforowanych odpowiedzi. W tym przykładzie interwał wynosi **3600** sekund, czyli godzinę.

Jeśli użyjemy konfiguracji buforowania w tym przykładzie, pierwsze żądanie operacji **GET Resource (cached)** zwraca odpowiedź z usługi zaplecza. Ta odpowiedź zostanie zbuforowana z kluczem uwzględniającym określone nagłówki i parametry ciągu zapytania. Dla kolejnych wywołań operacji z pasującymi parametrami będą zwracana buforowaną odpowiedź do czasu wygaśnięcia interwału czasu trwania pamięci podręcznej.

## <a name="caching-policies"> </a>Przeglądanie zasad buforowania
W tym kroku przejrzysz ustawienia buforowania operacji **GET Resource (cached)** przykładowego interfejsu Echo API.

Jeśli ustawienia buforowania są skonfigurowane dla operacji na karcie **Buforowanie**, zasady buforowania są dodawane dla operacji. Te zasady te można wyświetlać i edytować w edytorze zasad.

Kliknij opcję **Zasady** z menu **API Management** po lewej stronie, a następnie wybierz pozycje **Echo API / GET Resource (cached)** z listy rozwijanej **Operacja**.

![Operacja zakresu zasad][api-management-operation-dropdown]

Powoduje to wyświetlenie zasad dla tej operacji w edytorze zasad.

![Edytor zasad usługi API Management][api-management-policy-editor]

Definicja zasad dla tej operacji obejmuje zasady definiujące konfigurację buforowania wyświetloną na karcie **Buforowanie** w poprzednim kroku.

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> Zmiany wprowadzone w zasadach buforowania w edytorze zasad zostaną odzwierciedlone na karcie **Buforowanie** i na odwrót.
> 
> 

## <a name="test-operation"> </a>Wywoływanie operacji i testowanie buforowania
Możemy wywołać operację z portalu dla deweloperów, aby sprawdzić działanie buforowania. Kliknij przycisk **Portal dla deweloperów** w prawym górnym menu.

![Portal dla deweloperów][api-management-developer-portal-menu]

Kliknij opcję **Interfejsy API** w górnym menu, a następnie wybierz pozycję **Echo API**.

![Interfejs Echo API][api-management-apis-echo-api]

> Jeśli istnieje tylko jeden interfejs API skonfigurowany lub widoczny dla Twojego konta, kliknięcie opcji Interfejsy API powoduje przejście bezpośrednio do operacji dla tego interfejsu API.
> 
> 

Wybierz operację **GET Resource (cached)**, a następnie kliknij przycisk **Otwórz konsolę**.

![Otwarta konsola][api-management-open-console]

Konsola umożliwia wywoływanie operacji bezpośrednio z portalu dla deweloperów.

![Konsola][api-management-console]

Zachowaj wartości domyślne parametrów **param1** i **param2**.

Wybierz żądany klucz subskrypcji z listy rozwijanej **subscription-key**. Jeśli Twoje konto ma tylko jedną subskrypcję, zostanie ona od razu wybrana.

Wprowadź wartość **sampleheader:value1** w polu tekstowym **Nagłówki żądań**.

Kliknij przycisk **HTTP Get** i zanotuj nagłówki odpowiedzi.

Wprowadź wartość **sampleheader:value2** w polu tekstowym **Nagłówki żądań**, a następnie kliknij przycisk **HTTP Get**.

Zauważ, że wartość **sampleheader** jest nadal równa **value1** w odpowiedzi. Wypróbuj kilka różnych wartości i zauważ, że zwracana jest buforowana odpowiedź z pierwszego wywołania.

Wprowadź wartość **25** w polu **param2**, a następnie kliknij przycisk **HTTP Get**.

Zauważ, że wartość **sampleheader** w odpowiedzi jest teraz równa **value2**. Ponieważ wyniki operacji są oznaczanie kluczami na podstawie ciągu zapytania, poprzednio zbuforowana odpowiedź nie została zwrócona.

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
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review the caching policies]: #caching-policies
[Call an operation and test the caching]: #test-operation
[Next steps]: #next-steps
