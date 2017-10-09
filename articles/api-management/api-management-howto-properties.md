---
title: "właściwości toouse aaaHow w ramach zasad usługi Azure API Management"
description: "Dowiedz się, jak właściwości toouse w ramach zasad usługi Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a>Jak właściwości toouse w ramach zasad usługi Azure API Management
Zarządzanie interfejsami API zasady są zaawansowanych możliwości hello system, który umożliwia zachowanie hello toochange hello interfejsu API za pomocą konfiguracji hello wydawcy. Zasady są zbiór instrukcji, które są wykonywane sekwencyjnie na powitania żądania lub odpowiedzi interfejsu API. Deklaracji zasad może być skonstruowany przy użyciu wartości tekstowe literału, wyrażenie zasad i właściwości. 

Każde wystąpienie usługi Zarządzanie interfejsami API ma kolekcję właściwości par klucz/wartość, które są globalne toohello wystąpienie usługi. Te właściwości mogą być używane toomanage stałych wartości ciągów we wszystkich Konfiguracja interfejsu API i zasady. Każda właściwość ma hello następujące atrybuty.

| Atrybut | Typ | Opis |
| --- | --- | --- |
| Nazwa |Ciąg |Nazwa Hello hello właściwości. Może zawierać tylko litery, cyfry, okres, łączniki i znaki podkreślenia. |
| Wartość |Ciąg |wartość Hello hello właściwości. Nie może być pusta ani zawierać tylko odstępu. |
| Wpis tajny |Wartość logiczna |Określa, czy wartość hello jest klucz tajny i powinny być szyfrowane, czy nie. |
| Tagi |Tablica ciągów |Opcjonalnie tagi, które udostępniane mogą być używane toofilter hello właściwości listy. |

Właściwości są skonfigurowane w portalu wydawcy hello na powitania **właściwości** kartę. W hello poniższy przykład trzech właściwości są skonfigurowane.

![Właściwości][api-management-properties]

Wartości właściwości mogą zawierać ciągi literału i [wyrażenie zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx). Witaj poniższej tabeli przedstawiono hello poprzednie trzy przykładowe właściwości i ich atrybutów. Witaj wartość `ExpressionProperty` jest hello wyrażenie zasad, która zwraca ciąg zawierający bieżącą datę i godzinę. Witaj właściwości `ContosoHeaderValue` jest oznaczona jako klucz tajny, więc jego wartość nie jest wyświetlana.

| Nazwa | Wartość | Wpis tajny | Tagi |
| --- | --- | --- | --- |
| ContosoHeader |trackingId |False |Contoso |
| ContosoHeaderValue |•••••••••••••••••••••• |True |Contoso |
| ExpressionProperty |@(DateTime.Now.ToString()) |False | |

## <a name="toouse-a-property"></a>toouse właściwości
toouse właściwości w zasadach, nazwa właściwości hello miejscu wewnątrz podwójne pary nawiasów klamrowych, takich jak `{{ContosoHeader}}`, jak pokazano w hello poniższy przykład.

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

W tym przykładzie `ContosoHeader` jest używana jako nazwa hello nagłówka w `set-header` zasad, a `ContosoHeaderValue` jest używany jako wartość hello nagłówka. Gdy ta zasada jest oceniane podczas żądania lub odpowiedzi toohello interfejsu API zarządzania bramą, `{{ContosoHeader}}` i `{{ContosoHeaderValue}}` są zamieniane na ich wartości odpowiednich właściwości.

Właściwości mogą być używane jako atrybut pełną lub wartości elementów, jak pokazano w poprzednim przykładzie hello, ale również mogą zostać wstawione do albo połączone z część wyrażenia literału tekstu, jak pokazano w hello poniższy przykład:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`

Właściwości może również zawierać wyrażenie zasad. W hello poniższy przykład, hello `ExpressionProperty` jest używany.

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

W przypadku oceny tych zasad `{{ExpressionProperty}}` zastępuje z wartością: `@(DateTime.Now.ToString())`. Ponieważ wartość hello jest wyrażenie zasad, hello wyrażenie jest obliczane i zasad hello kontynuuje jego wykonywania.

Można to sprawdzić się w portalu dla deweloperów hello wywołując operację, która ma zasady z właściwości w zakresie. W hello poniższy przykład, operacja nosi nazwę Witaj dwie poprzedniego przykładu `set-header` zasad przy użyciu właściwości. Należy pamiętać, że odpowiedź hello zawiera dwa Nagłówki niestandardowe, które zostały skonfigurowane przy użyciu zasad z właściwościami.

![Portal dla deweloperów][api-management-send-results]

Jeśli przyjrzymy się hello [inspektora interfejsu API śledzenia](api-management-howto-api-inspector.md) dla wywołania obejmującej hello dwa poprzednie przykładowe zasady z właściwościami, można wyświetlić hello dwa `set-header` zasady z wartościami właściwości hello dodaje oraz hello wyrażenie zasad Obliczanie dla właściwości hello, który zawiera wyrażenie zasad hello.

![Interfejs API inspektora śledzenia][api-management-api-inspector-trace]

Należy pamiętać, że podczas wartości właściwości mogą zawierać wyrażenia zasad, wartości właściwości nie może zawierać inne właściwości. Jeśli tekst zawierający odwołania do właściwości jest używana do wartości właściwości, takie jak `Property value text {{MyProperty}}`, że odwołania do właściwości nie zostanie zastąpiony i zostanie dołączony hello wartości właściwości.

## <a name="toocreate-a-property"></a>toocreate właściwości
Kliknij toocreate właściwość **Dodaj właściwość** na powitania **właściwości** kartę.

![Dodaj właściwość][api-management-properties-add-property-menu]

**Nazwa** i **wartość** są wymaganymi wartościami. Jeśli wartość tej właściwości jest klucz tajny, sprawdź hello **jest klucz tajny** wyboru. Wprowadź co najmniej jeden toohelp opcjonalnych tagów z organizowania właściwości, a następnie kliknij przycisk **zapisać**.

![Dodaj właściwość][api-management-properties-add-property]

Po zapisaniu nowej właściwości hello **wyszukiwania właściwości** pole tekstowe jest wypełniane przy użyciu nazwy hello hello nową właściwość i nową właściwość hello jest wyświetlany. Wyczyść wszystkie właściwości toodisplay hello **wyszukiwania właściwości** pole tekstowe i naciśnij klawisz enter.

![Właściwości][api-management-properties-property-saved]

Informacje dotyczące tworzenia właściwości przy użyciu hello interfejsu API REST, zobacz [utworzyć właściwość przy użyciu interfejsu API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).

## <a name="tooedit-a-property"></a>tooedit właściwości
tooedit właściwości, kliknij przycisk **Edytuj** obok hello tooedit właściwości.

![Edytowanie właściwości][api-management-properties-edit]

Wprowadź żądane zmiany, a następnie kliknij przycisk **zapisać**. Jeśli zmienisz nazwę właściwości hello wszystkie zasady, które odwołują się do tej właściwości są automatycznie aktualizowane toouse hello nową nazwę.

![Edytowanie właściwości][api-management-properties-edit-property]

Informacje do edycji właściwości przy użyciu hello interfejsu API REST, zobacz [Edytuj właściwości przy użyciu interfejsu API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).

## <a name="toodelete-a-property"></a>toodelete właściwości
toodelete właściwości, kliknij przycisk **usunąć** obok hello toodelete właściwości.

![Usuń właściwość][api-management-properties-delete]

Kliknij przycisk **tak, usuń go** tooconfirm.

![Potwierdzenie usunięcia][api-management-delete-confirm]

> [!IMPORTANT]
> Jeśli właściwość hello odwołuje się do niego wszystkie zasady, nie będzie toosuccessfully go usunąć przed usunięciem hello właściwości z wszystkich zasad, które go używają.
> 
> 

Informacje dotyczące usuwania właściwości przy użyciu hello interfejsu API REST, zobacz [usunąć właściwości przy użyciu interfejsu API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).

## <a name="toosearch-and-filter-properties"></a>właściwości toosearch i filtru
Witaj **właściwości** karta zawiera wyszukiwania i filtrowania toohelp możliwości zarządzania właściwości. Lista właściwości hello toofilter według nazwy właściwości, wprowadź wyszukiwany termin w hello **wyszukiwania właściwości** pola tekstowego. Wyczyść wszystkie właściwości toodisplay hello **wyszukiwania właściwości** pole tekstowe i naciśnij klawisz enter.

![Wyszukiwanie][api-management-properties-search]

Lista właściwości hello toofilter przez wartości tagów wprowadzić jeden lub więcej tagów w hello **Filtruj według znaczników** pola tekstowego. Wyczyść wszystkie właściwości toodisplay hello **Filtruj według znaczników** pole tekstowe i naciśnij klawisz enter.

![Filtr][api-management-properties-filter]

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o pracy z zasadami
  * [Zasady w usłudze API Management](api-management-howto-policies.md)
  * [Dokumentacja zasad](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [Wyrażenia zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a>Obejrzyj film wideo
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

