---
title: "Użycie zasobów dostawcy interfejsu API | Dokumentacja firmy Microsoft"
description: "Odwołania do interfejsu API, użycie zasobów, który pobiera informacje o użyciu stosu Azure"
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b6055923-b6a6-45f0-8979-225b713150ae
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: alfredop
ms.openlocfilehash: 0c45ce3bc93945ed8700464beebabcda07e8d77c
ms.sourcegitcommit: dfd49613fce4ce917e844d205c85359ff093bb9c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2017
---
# <a name="provider-resource-usage-api"></a>Interfejs API użycia zasobów dostawcy
Termin *dostawcy* stosuje się do administratora usługi i wszystkich dostawców delegowanego. Azure operatorów stosu i dostawców delegowanego służy użycia dostawcy interfejsu API do wyświetlania użycia bezpośredniego dzierżawcom. Na przykład pokazany na rysunku P0 można wywołać dostawcy interfejsu API, aby uzyskać użycia informacji o jego P1 i P2 przez bezpośredniego użycia i P1 można wywołać użycie informacji na temat P3 i P4.

![Model koncepcyjny hierarchii dostawcy](media/azure-stack-provider-resource-api/image1.png)

## <a name="api-call-reference"></a>Odwołanie do wywołania interfejsu API
### <a name="request"></a>Żądanie
Żądanie pobiera szczegóły zużycia dla żądanego subskrypcje i żądanej przedziale czasu. Nie ma żadnych treści żądania.

Ten interfejs API użycia jest dostawcy interfejsu API, aby obiekt wywołujący musi mieć przypisaną rolę właściciela, współautora lub czytelnika subskrypcji dostawcy.

| **— Metoda** | **Identyfikator URI żądania** |
| --- | --- |
| POBIERZ |https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}& subscriberId = {sub1.1} & api-version = 2015-06-01-preview & continuationToken = {wartości tokenu} |

### <a name="arguments"></a>Argumenty
| **Argument** | **Opis** |
| --- | --- |
| *armendpoint* |Menedżer zasobów punktu końcowego platformy Azure środowiska Azure stosu. Konwencja stosu Azure jest, że nazwa punktu końcowego usługi Azure Resource Manager jest w formacie `https://adminmanagement.{domain-name}`. Na przykład dla zestawu SDK, jeśli nazwa domeny jest *local.azurestack.external*, to jest punkt końcowy Menedżera zasobów `https://adminmanagement.local.azurestack.external`. |
| *subId* |Identyfikator subskrypcji użytkownika, który wykonuje wywołanie. |
| *reportedStartTime* |Uruchomienie zapytania. Wartość *DateTime* powinny być uniwersalny czas koordynowany (UTC) i na początku godziny, na przykład 13:00. Codzienne agregacji ta wartość północy czasu UTC. Format jest *wpisywany* ISO 8601. Na przykład *2015-06-16T18% 3a53% 3a11% 2b00% 3a00Z*, gdzie dwukropkiem została zmieniona na *% 3a* i plus została zmieniona na *% 2b* tak, aby przyjazną identyfikatora URI. |
| *reportedEndTime* |Godzina zakończenia zapytania. Ograniczenia, które dotyczą *reportedStartTime* mają też zastosowanie do tego argumentu. Wartość *reportedEndTime* nie może być w przyszłości lub bieżącą datę. Jeśli tak jest, wynik jest ustawiony na "przetwarzania nie ukończenia." |
| *aggregationGranularity* |Opcjonalny parametr, który ma dwa odrębne wartości potencjalnych: dni i godzin. Jako wartości sugerują, jeden zwraca w dzienne dane, a drugi to rozpoznawanie co godzinę. Opcja codzienne jest ustawieniem domyślnym. |
| *subscriberId* |Identyfikator subskrypcji. Aby uzyskać odfiltrowane dane, wymagany jest identyfikator subskrypcji bezpośredniego dzierżawcy dostawcy. Jeśli określono parametr ID nie subskrypcji, wywołanie zwraca dane użycia dla wszystkich dostawcy bezpośredniego dzierżawców. |
| *wersja interfejsu API* |Wersja protokołu, który służy do zgłoszenia tego żądania. Ta wartość jest równa *2015-06-01-preview*. |
| *continuationToken* |Token jest pobierana z ostatnim wywołaniem dostawcy użycia interfejsu API. Token ten jest potrzebna, gdy odpowiedź jest większa niż 1000 wierszy i działa jako zakładka postęp. Jeśli token nie jest obecny, dane są pobierane z początku dnia lub przekazano godzinę, w oparciu o stopień szczegółowości. |

### <a name="response"></a>Odpowiedź
Pobierz /subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00 & reportedEndTime = 2015-06-01T00% 3a00% 3a00% 2b00% 3a00 & aggregationGranularity = codziennie & subscriberId = sub1.1 & api-version = 1.0

```json
{
"value": [
{

"id":
"/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-

meterID1",
"name": "sub1.1-meterID1",
"type": "Microsoft.Commerce/UsageAggregate",

"properties": {
"subscriptionId":"sub1.1",
"usageStartTime": "2015-03-03T00:00:00+00:00",
"usageEndTime": "2015-03-04T00:00:00+00:00",
"instanceData":"{\"Microsoft.Resources\":{\"resourceUri\":\"resourceUri1\",\"location\":\"Alaska\",\"tags\":null,\"additionalInfo\":null}}",
"quantity":2.4000000000,
"meterId":"meterID1"

}
},

…
```

### <a name="response-details"></a>Szczegóły odpowiedzi
| **Argument** | **Opis** |
| --- | --- |
| *Identyfikator* |Unikatowy identyfikator użycia agregacji. |
| *Nazwa* |Nazwa wartości zagregowanej użycia. |
| *Typ* |Definicja zasobu. |
| *Identyfikator subskrypcji* |Identyfikator subskrypcji użytkownika stosu Azure. |
| *usageStartTime* |Czas UTC uruchomienie zasobnika użycia, do którego należy ta wartość zagregowana użycia.|
| *usageEndTime* |Godzina zakończenia UTC zasobnika użycia, do którego należy ta wartość zagregowana użycia. |
| *instanceData* |Pary klucz wartość Szczegóły wystąpienia (w formacie nowych):<br> *resourceUri*: identyfikator zasobu, który obejmuje grup zasobów i nazwę wystąpienia w pełni kwalifikowana. <br> *Lokalizacja*: regionu, w którym uruchomiono tę usługę. <br> *tagi*: tagi zasobów, które są określone przez użytkownika. <br> *części informacje dodatkowe aby*: więcej szczegółowych informacji o zasobu, który został wykorzystany, na przykład typ wersji lub obrazu systemu operacyjnego. |
| *ilość* |Ilość zużycia zasobów, które wystąpiły w tym przedziale czasu. |
| *meterId* |Unikatowy identyfikator zasobu, który został wykorzystany (nazywane również *ResourceID*). |

## <a name="next-steps"></a>Następne kroki
[Dokumentacja interfejsu API użycia zasobów przez dzierżawcę](azure-stack-tenant-resource-usage-api.md)

[Często zadawane pytania dotyczące wykorzystania](azure-stack-usage-related-faq.md)
