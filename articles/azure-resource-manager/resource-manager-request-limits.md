---
title: "limity żądań aaaAzure Resource Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse ograniczania z usługi Azure Resource Manager zażąda po osiągnięciu limitu subskrypcji."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a>Ograniczanie żądań Resource Manager
Dla każdej subskrypcji i dzierżawy limity Resource Manager too15 żądania, 000 na godzinę i zapis too1 żądania, 200 na godzinę. Te limity mają zastosowanie wystąpienia usługi Azure Resource Manager tooeach; istnieje wiele wystąpień w każdym regionie Azure i usługi Azure Resource Manager jest wdrożony tooall Azure regionów.  Zatem w praktyce limity są wydajnie znacznie wyższa niż wymienione powyżej, jako użytkownik żądań są zazwyczaj obsługiwane przez wiele różnych wystąpień.

Jeśli aplikacji lub skryptu osiągnie tych ograniczeń, należy toothrottle Twojego żądania. W tym temacie pokazano, jak hello toodetermine pozostałych żądań przed osiągnięciem limitu hello i jak toorespond po osiągnięciu limitu hello.

Po osiągnięciu limitu hello, otrzymasz kod stanu hello HTTP **429 zbyt wiele żądań**.

Liczba żądań Hello jest tooeither zakresie subskrypcji lub dzierżawy. Jeśli masz wiele, aplikacjami wysyłania żądań w ramach subskrypcji, hello żądań z tymi aplikacjami zostaną dodane razem toodetermine hello liczba pozostałych żądań.

Subskrypcja zakres żądania są hello obejmują przekazywanie identyfikator subskrypcji, takie jak pobieranie hello grup zasobów w ramach subskrypcji. Żądania dzierżawy w zakresie nie ma identyfikator subskrypcji, takie jak pobieranie prawidłowych lokalizacji platformy Azure.

## <a name="remaining-requests"></a>Pozostałych żądań
Można określić hello liczbę pozostałych żądań, sprawdzając nagłówków odpowiedzi. Każde żądanie zawiera wartości hello liczbę żądań zapisu i odczytu pozostałych. Witaj poniższej tabeli opisano hello nagłówki odpowiedzi, który można sprawdzić dla tych wartości:

| Nagłówek odpowiedzi | Opis |
| --- | --- |
| x-MS-ratelimit-Remaining-Subscription-Reads |Odczytuje subskrypcji zakres pozostałych |
| x-MS-ratelimit-Remaining-Subscription-Writes |Zapisuje zakres subskrypcji pozostałych |
| x-MS-ratelimit-Remaining-tenant-Reads |Zakres dzierżawy odczytuje pozostałych |
| x-MS-ratelimit-Remaining-tenant-Writes |Zapisuje zakres dzierżawy pozostałych |
| x-MS-ratelimit-Remaining-Subscription-Resource-Requests |Subskrypcja zakresu pozostałych żądań typu zasobu.<br /><br />Wartość tego nagłówka jest zwracany tylko wtedy, jeśli usługa została zastąpiona hello domyślny limit. Menedżer zasobów dodaje tej wartości, zamiast hello subskrypcji odczytów i zapisów. |
| x-MS-ratelimit-Remaining-Subscription-Resource-ENTITIES-Read |Subskrypcja zakresu pozostałych żądania kolekcji dla typu zasobu.<br /><br />Wartość tego nagłówka jest zwracany tylko wtedy, jeśli usługa została zastąpiona hello domyślny limit. Ta wartość określa hello liczba pozostałych żądań kolekcji (listy zasobów). |
| x-MS-ratelimit-Remaining-tenant-Resource-Requests |Zakres dzierżawy pozostałych żądań typu zasobu.<br /><br />Ten nagłówek jest dodawać tylko dla żądań na poziomie dzierżawy, a tylko wtedy, gdy usługa została zastąpiona hello domyślny limit. Menedżer zasobów dodaje tej wartości, zamiast hello dzierżawy odczytów i zapisów. |
| x-MS-ratelimit-Remaining-tenant-Resource-ENTITIES-Read |Dzierżawy zakresu pozostałych żądania kolekcji dla typu zasobu.<br /><br />Ten nagłówek jest dodawać tylko dla żądań na poziomie dzierżawy, a tylko wtedy, gdy usługa została zastąpiona hello domyślny limit. |

## <a name="retrieving-hello-header-values"></a>Pobieranie wartości nagłówka hello
Nie różni się od pobierania wartości nagłówka się podczas pobierania tych wartości nagłówka w tym kod lub skrypt. 

Na przykład w **C#**, możesz pobrać wartość nagłówka hello **HttpWebResponse** obiektu o nazwie **odpowiedzi** z hello następującego kodu:

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

W **PowerShell**, pobrać wartość nagłówka hello z operacji Invoke WebRequest.

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

Lub, jeśli chcesz toosee hello pozostałych żądań do debugowania, możesz podać hello **-Debug** parametru na Twojej **środowiska PowerShell** polecenia cmdlet.

```powershell
Get-AzureRmResourceGroup -Debug
```

Która zwraca wiele wartości, w tym powitania po wartość odpowiedzi:

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

W **interfejsu wiersza polecenia Azure**, pobrać wartość nagłówka hello za pomocą hello na pełniejsze opcji.

```azurecli
azure group list -vv --json
```

Która zwraca wiele wartości, w tym hello następującego obiektu:

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a>Oczekiwania przed wysłaniem żądania dalej
Po osiągnięciu limitu żądań hello Resource Manager zwraca hello **429** kod stanu HTTP i **ponownych prób po** wartość w nagłówku hello. Witaj **ponownych prób po** wartość określa hello liczbę sekund oczekiwania w aplikacji (lub uśpienia) przed wysłaniem hello następnego żądania. Po wysłaniu żądania, przed upływem hello wartość ponownych prób, Twoje żądanie nie jest przetwarzane i nowa wartość ponownych prób jest zwracany.

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji na temat limitów i przydziały zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md).
* toolearn dotyczące obsługi żądań asynchronicznych REST, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).
