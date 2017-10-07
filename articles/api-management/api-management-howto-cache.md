---
title: "buforowanie tooimprove wydajności w usłudze Azure API Management aaaAdd | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak załadować tooimprove hello opóźnień, przepustowości i usługi sieci web dla wywołania usługi Zarządzanie interfejsami API."
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
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a>Dodaj buforowania wydajności tooimprove w usłudze Azure API Management
Operacje w usłudze API Management można skonfigurować do buforowania odpowiedzi. Buforowanie odpowiedzi może znacznie zmniejszyć opóźnienie interfejsu API, zużycie przepustowości i obciążenie usługi sieci Web w przypadku danych, które nie zmieniają się często.

W tym przewodniku przedstawiono odpowiedzi tooadd buforowanie do interfejsu API i skonfigurować zasady dla operacji interfejsu API Echo przykład hello. Następnie można wywołać operacji hello w pamięci podręcznej tooverify portalu deweloperów hello w akcji.

> [!NOTE]
> Aby poznać informacje na temat buforowania elementów według kluczy przy użyciu wyrażeń zasad, zobacz artykuł [Custom caching in Azure API Management](api-management-sample-cache-by-key.md) (Niestandardowe buforowanie w usłudze Azure API Management).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Przed hello następujące kroki w tym przewodniku, należy dysponować wystąpienia usługi Zarządzanie interfejsami API z interfejsu API i skonfigurować produkt. Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.

## <a name="configure-caching"> </a>Konfigurowanie operacji do buforowania
W tym kroku należy przejrzeć ustawienia hello buforowania hello **UZYSKAĆ zasobów (buforowanej)** operacji próbki hello Echo interfejsu API.

> [!NOTE]
> Każde wystąpienie usługi Zarządzanie interfejsami API ma wstępnie skonfigurowane z interfejsem API Echo, które można tooexperiment używanych z i więcej informacji na temat interfejsu API zarządzania. Aby uzyskać więcej informacji, zobacz [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].
> 
> 

tooget pracę, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API. Trwa toohello zarządzanie interfejsami API wydawcy portalu.

![Portal wydawcy][api-management-management-console]

Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **Echo API**.

![Interfejs Echo API][api-management-echo-api]

Kliknij hello **operacji** , a następnie kliknij pozycję hello **UZYSKAĆ zasobów (buforowanej)** operacji hello **operacji** listy.

![Operacje interfejsu Echo API][api-management-echo-api-operations]

Kliknij przycisk hello **buforowanie** hello tooview kartę Ustawienia dla tej operacji pamięci podręcznej.

![Karta Buforowanie][api-management-caching-tab]

tooenable buforowanie dla operacji select hello **włączyć** pole wyboru. W tym przykładzie buforowanie jest włączone.

Wyznaczaną każdej operacji odpowiedzi, na podstawie wartości hello w hello **różne parametry ciągu zapytania** i **Vary przez nagłówki** pola. Jeśli chcesz toocache wiele odpowiedzi na podstawie parametrów ciągu zapytania lub nagłówków, można je skonfigurować w tych dwóch pól.

**Czas trwania** Określa interwał wygaśnięcia powitania hello buforowane odpowiedzi. W tym przykładzie jest interwał powitania **3600** sekund, co jest równoważne tooone godzinę.

Przy użyciu hello konfiguracji w tym przykładzie buforowania, hello pierwszego żądania toohello **UZYSKAĆ zasobów (buforowanej)** operacji zwraca odpowiedź z usługi zaplecza hello. Tej odpowiedzi będą buforowane, wyznaczaną przez hello określone parametry nagłówki i zapytania. Kolejne wywołania operacji toohello z pasujących parametrów, będzie mieć hello buforować odpowiedź zwrócona, dopóki interwał czasu trwania pamięci podręcznej hello utracił ważność.

## <a name="caching-policies"></a>Hello przeglądu buforowanie zasad
W tym kroku, przejrzyj hello buforowanie ustawienia hello **UZYSKAĆ zasobów (buforowanej)** operacji próbki hello Echo interfejsu API.

Jeśli skonfigurowano ustawienia buforowania dla operacji na powitania **buforowanie** karcie buforowanie zasad są dodawane do operacji hello. Te zasady można wyświetlać i edytować w edytorze zasad hello.

Kliknij przycisk **zasady** z hello **zarządzanie interfejsami API** menu na powitania po lewej stronie, a następnie wybierz **Echo API / GET zasobów (buforowanej)** z hello **operacji**listy rozwijanej.

![Operacja zakresu zasad][api-management-operation-dropdown]

W edytorze zasad hello zostaną wyświetlone powitalne zasad dla tej operacji.

![Edytor zasad usługi API Management][api-management-policy-editor]

Witaj definicji zasad dla tej operacji zawiera zasady hello definiujące hello buforowanie konfiguracji, które zostały sprawdzone za pomocą hello **buforowanie** kartę hello poprzedniego kroku.

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
> Buforowanie zasad w edytorze zasad hello toohello zmiany zostaną odzwierciedlone na powitania **buforowanie** kartę operację, i na odwrót.
> 
> 

## <a name="test-operation"></a>Wywołania operacji i przetestować hello buforowanie
Witaj toosee buforowania w akcji, możemy wywołać operację hello z hello portalu dla deweloperów. Kliknij przycisk **portalu dla deweloperów** w menu u góry prawo hello.

![Portal dla deweloperów][api-management-developer-portal-menu]

Kliknij przycisk **interfejsów API** w hello menu u góry, a następnie wybierz **Echo API**.

![Interfejs Echo API][api-management-apis-echo-api]

> Jeśli masz tylko jeden interfejs API skonfigurowane lub tooyour widoczne konta, klikając interfejsów API przejście bezpośrednio toohello operacji dla tego interfejsu API.
> 
> 

Wybierz hello **UZYSKAĆ zasobów (buforowanej)** operacji, a następnie kliknij przycisk **Otwórz konsolę**.

![Otwarta konsola][api-management-open-console]

Konsola Hello umożliwia operacji tooinvoke bezpośrednio z portalu dla deweloperów hello.

![Konsola][api-management-console]

Zachowaj wartości domyślne hello **param1** i **param2**.

Wybierz hello inny klawisz z hello **klucza subskrypcji** listy rozwijanej. Jeśli Twoje konto ma tylko jedną subskrypcję, zostanie ona od razu wybrana.

Wprowadź **sampleheader:value1** w hello **nagłówki żądań** pola tekstowego.

Kliknij przycisk **HTTP Get** i zanotuj hello nagłówków odpowiedzi.

Wprowadź **sampleheader:value2** w hello **nagłówki żądań** polu tekstowym, a następnie kliknij przycisk **HTTP Get**.

Należy zwrócić uwagę tej wartości hello **sampleheader** jest nadal **wartość1** hello odpowiedzi. Spróbuj niektórych różne wartości i należy pamiętać, że hello buforowanej odpowiedzi z pierwszym wywołaniu hello są zwracane.

Wprowadź **25** do hello **param2** pola, a następnie kliknij przycisk **HTTP Get**.

Należy zwrócić uwagę tej wartości hello **sampleheader** w hello odpowiedź jest teraz **wartość2**. Ponieważ wyniki operacji hello są wyznaczaną przez ciąg zapytania, nie został zwrócony hello poprzedniej odpowiedzi pamięci podręcznej.

## <a name="next-steps"> </a>Następne kroki
* Aby uzyskać więcej informacji na temat zasad buforowania, zobacz [buforowanie zasad] [ Caching policies] w hello [informacje o zasadach usługi API Management][API Management policy reference].
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


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
