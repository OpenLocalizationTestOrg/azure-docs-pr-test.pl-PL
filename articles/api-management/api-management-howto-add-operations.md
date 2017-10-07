---
title: "aaaHow tooadd tooan operacje interfejsu API w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd tooan operacje interfejsu API w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a>Jak tooadd tooan operacje interfejsu API w usłudze Azure API Management
Przed użyciem interfejsu API w usłudze API Management operacji musi zostać dodany. Ten przewodnik przedstawia jak tooadd i konfigurowania różnych typów tooan operacje interfejsu API w usłudze API Management.

## <a name="add-operation"></a>Dodać operację
Operacje są dodawane i tooan interfejsu API w portalu wydawcy hello. tooaccess hello wydawcy portalu, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.

![Portal wydawcy][api-management-management-console]

> Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.
> 
> 

Wybierz hello żądana interfejsu API w portalu wydawcy hello i wybierz opcję hello **operacji** kartę. 

![Operacje][api-management-operations]

Kliknij przycisk **operacji dodawania** tooadd nowej operacji. Witaj **nowej operacji** będą wyświetlane i hello **podpisu** będzie domyślnie wybierany kartę.

![Operacja dodania][api-management-add-operation]

Określ hello **zlecenie HTTP** wybierając z listy rozwijanej hello.

![Metoda HTTP][api-management-http-method]

<a name="url-template"></a>

Zdefiniuj szablon adresu URL hello wpisując fragmentu adresu URL składające się z jednego lub więcej segmentów ścieżki adresu URL i zero lub więcej parametrów ciągu zapytania. Szablon adresu URL Hello, dołączany toohello podstawowy adres URL hello interfejsu API, identyfikuje jednej operacji HTTP. Może zawierać jeden lub więcej o nazwie części zmiennych, które są identyfikowane za pomocą nawiasów klamrowych. Części te zmienne są nazywane parametrów szablonu i są dynamicznie przypisywane wartości wyodrębniony z adresu URL żądania hello, gdy trwa przetwarzanie żądania hello przez platformę interfejsu API zarządzania hello.

> Szablon adresu URL Hello mogą obejmować wzorców symboli wieloznacznych. Na przykład określenie `/*` przekazuj wszystkie żądania dotyczące toohello metody powrót tego HTTP zakończy się usługi.

![Szablon adresu URL][api-management-url-template]

<a name="rewrite-url-template"></a>

W razie potrzeby można określić hello **szablonu ponowne zapisywanie adresów URL**. Dzięki temu można toouse hello standardowy szablon adresu URL do przetwarzania przychodzących żądań na powitania frontonu, podczas wywoływania hello zaplecza za pośrednictwem adresu URL przekonwertowanego zgodnie z toohello ponownego zapisywania szablonu. Parametry szablonu z szablonu adresu URL hello powinien być używany w szablonie ponownego zapisywania hello. Witaj poniższy przykład przedstawia sposób zawartości typu zakodowane jako segment ścieżki w hello usługi sieci web z poprzedniego przykładu hello można podać jako parametr zapytania w hello interfejsu API opublikowane za pośrednictwem hello platformy zarządzania interfejsu API przy użyciu szablonów URL hello.

![Ponowne zapisywanie adresów URL szablonu][api-management-url-template-rewrite]

Operacja toohello wywołań zostanie użyty hello format `/customers?customerid=ALFKI` i będzie to zbyt mapować`/Customers('ALFKI')` po wywołaniu hello usługi zaplecza.

**Wyświetl** nazwy i **opis** Podaj opis operacji hello i są używane tooprovide dokumentacji deweloperzy toohello przy użyciu tego interfejsu API w portalu dla deweloperów hello.

![Opis][api-management-description]

Opis operacji Hello można określić jako zwykły tekst lub HTML w hello **opis** pola tekstowego.

## <a name="operation-caching"></a>Buforowanie operacji
Buforowanie odpowiedzi zmniejsza opóźnienia postrzegane przez konsumentów hello interfejsu API, obniża zużycie przepustowości i hello zmniejsza obciążenie wdrażanie usługi sieci web HTTP hello hello interfejsu API. 

tooeasily i szybko włączyć buforowanie dla operacji hello, wybierz hello **buforowanie** i sprawdź hello **włączyć** wyboru.

![Buforowanie][api-management-caching-tab]

**Czas trwania** określa okres czasu, podczas których hello odpowiedź operacji pozostaje w pamięci podręcznej hello hello. Hello wartość domyślna wynosi 3600 sekund lub 1 godzina.

Buforowanie kluczy są używane toodifferentiate między odpowiedzi, aby odpowiedź hello odpowiadającego klucz pamięci podręcznej różnych tooeach otrzyma własną oddzielne wartość w pamięci podręcznej. Opcjonalnie wprowadź parametrów ciągu zapytania określonego i/lub toobe nagłówki HTTP używany w obliczeniu wartości klucza pamięci podręcznej na powitania **różne parametry ciągu zapytania** i **Vary przez nagłówki** odpowiednio pola tekstowe. Gdy żaden nie jest adres URL określony, pełną żądania i hello następujące wartości nagłówka HTTP są używane podczas generowania klucza pamięci podręcznej: **Akceptuj** i **Accept-Charset**.

> Aby uzyskać więcej informacji o pamięci podręcznej i buforowania zasady, zobacz [jak wynikiem Azure API Management operacji toocache][How toocache operation results in Azure API Management].
> 
> 

## <a name="request-parameters"></a>Parametry żądania
Parametry operacji są zarządzane na powitania karta Parametry. Parametry określone w hello **szablon adresu URL** na powitania **podpisu** kartę są automatycznie dodawane i można zmienić, edytując hello szablon adresu URL. Dodatkowe parametry, można wprowadzić ręcznie.

tooadd nowy parametr zapytania, kliknij przycisk **dodać parametru zapytania** , a następnie wprowadź hello następujących informacji:

* **Nazwa** — Nazwa parametru.
* **Opis elementu** -krótki opis parametru hello (opcjonalnie).
* **Typ** — wybrany hello rozwijanej Typ parametru.
* **Wartości** -wartości, które można przypisać parametru toothis. Jedna z wartości hello może być oznaczony jako domyślny (opcjonalnie).
* **Wymagane** -był parametru hello zaznaczając pole wyboru hello jest wymagany. 

![Parametry żądania][api-management-request-parameters]

## <a name="request-body"></a>Treść żądania
Jeśli zezwala na operację hello (np. PUT, POST) i wymaga treści może podać przykład go we wszystkich hello obsługiwane formaty reprezentacja (np. json, XML). 

> Treść żądania Hello jest używany tylko w celach dokumentacji i nie jest weryfikowany.
> 
> 

tooenter treści żądania, Przełącz toohello **treści** kartę.

Kliknij przycisk **dodać reprezentacja**, wpisz nazwę odpowiedniego typu zawartości (np. application/json), wybierz je w listy rozwijanej hello i Wklej hello potrzeby przykład treści żądania w wybranym formacie hello w polu tekstowym hello. 

![Treść żądania][api-management-request-body]

W dodatkowych toorepresentations, można także określić opcjonalny opis w hello **opis** pola tekstowego.

## <a name="responses"></a>Odpowiedzi
Należy dobrze przykłady tooprovide odpowiedzi dla wszystkich kodów stanu, które może powodować hello operacji. Każdy kod stanu może mieć więcej niż jeden przykład treści odpowiedzi, po jednej dla każdego z hello obsługiwane typy zawartości. 

tooadd odpowiedzi, kliknij przycisk **Dodaj** i zacznij pisać kod stanu hello potrzebne. Taki stan hello przykładowy kod jest **200 OK**. Gdy kod hello jest wyświetlany w listy rozwijanej hello, zaznacz go i hello kod odpowiedzi jest utworzony i dodany tooyour operacji.

![Kod odpowiedzi][api-management-response-code]

Kliknij przycisk **dodać reprezentacja**zacznij wpisywać ciąg hello nazwa żądanego typu zawartości (np. application/json), a następnie wybierz pozycję w hello listy rozwijanej.

![Typ zawartości treści][api-management-response-body-content-type]

Wklej przykład treści odpowiedzi Witaj w wybranym formacie hello w polu tekstowym hello. 

![Treść odpowiedzi][api-management-response-body]

W razie potrzeby dodaj opcjonalny opis w hello **opis** pola tekstowego.

Po skonfigurowaniu operacji powitania kliknij **zapisać**.

## <a name="next-steps"> </a>Następne kroki
Po dodaniu interfejsu API tooan operacji hello, hello następnym krokiem jest tooassociate hello interfejsu API z produktem i opublikować go, dzięki czemu deweloperzy mogą wywoływać operacjach.

* [Jak toocreate i opublikuj produktu][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
