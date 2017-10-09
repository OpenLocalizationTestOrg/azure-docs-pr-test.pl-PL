---
title: "aaaAzure siatki zdarzeń zabezpieczeń i uwierzytelniania"
description: "Opisuje Azure zdarzeń siatki i jego pojęcia."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a>Zdarzenie siatki zabezpieczeń i uwierzytelniania 

Azure siatki zdarzeń ma trzy typy uwierzytelniania:

* Subskrypcja zdarzeń
* Publikowanie zdarzenia
* Dostarczania zdarzeń elementu WebHook

## <a name="webhook-event-delivery"></a>Dostarczania zdarzeń elementu WebHook

Element Webhook ma jeden wiele sposobów tooreceive zdarzeń w czasie rzeczywistym z siatki zdarzeń platformy Azure.

Zawsze jest nowe zdarzenie toobe gotowy dostarczane, siatki zdarzeń wysyła żądanie HTTP z tooyour elementu WebHook ze zdarzeniem hello w treści hello.

Po zarejestrowaniu własny punkt końcowy elementu WebHook siatki zdarzeń wysyła możesz żądania POST z kodem poprawności w kolejności tooprove punktu końcowego własności. Twoja aplikacja powinna toorespond przez wyświetlania kodu walidacji hello Wstecz. Zdarzenie siatki nie wyśle zdarzenia tooWebHook punktów końcowych, które nie przeszły hello weryfikacji.
 
### <a name="validation-details"></a>Szczegóły dotyczące sprawdzania poprawności:

* W czasie hello aktualizacja tworzenia subskrypcji zdarzeń siatki zdarzeń wpisów punktu końcowego "SubscriptionValidationEvent" zdarzeń toohello docelowej.
* Zdarzenie Hello zawiera wartość nagłówka "Typ zdarzenia: Walidacja".
* treści zdarzenia Hello ma hello tym samym schematem co inne zdarzenia, zdarzenia siatki.
* Dane zdarzenia Hello zawiera właściwość "ValidationCode" z ciągiem losowo generowany np. "ValidationCode: acb13...".

W kolejności tooprove punktu końcowego własność, echo np. Kod weryfikacji wstecz hello "ValidationResponse: acb13...".

Na koniec jest toonote ważne, czy siatka zdarzeń Azure obsługuje tylko punktów końcowych HTTPS elementu webhook.
## <a name="event-subscription"></a>Subskrypcja zdarzeń

zdarzenia tooan toosubscribe, musi mieć hello **Microsoft.EventGrid/EventSubscriptions/Write** wymagane uprawnienie na powitania zasobów. To uprawnienie jest konieczne, ponieważ pisania nową subskrypcję w zakresie hello hello zasobu. Witaj wymaganego zasobu różni się pod względem są subskrypcję tematu system tooa lub niestandardowego tematu. Oba typy są opisane w tej sekcji.

### <a name="system-topics-azure-service-publishers"></a>Tematy systemu (usługa Azure wydawców)

Tematy systemu należy toowrite uprawnienia nowej subskrypcji zdarzeń w zakresie hello publikowania zdarzeń hello hello zasobów. format Hello hello zasobu to:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

Na przykład toosubscribe tooan zdarzeń na konto magazynu o nazwie **myacct**, wymagane jest uprawnienie Microsoft.EventGrid/EventSubscriptions/Write hello na:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>Niestandardowe — tematy

Tematy niestandardowe należy toowrite uprawnienia nowej subskrypcji zdarzeń w zakresie hello hello siatki zdarzenia tematu. format Hello hello zasobu to:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

Na przykład toosubscribe tooa niestandardowego tematu o nazwie **mytopic**, wymagane jest uprawnienie Microsoft.EventGrid/EventSubscriptions/Write hello na:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>Publikowanie w temacie

Tematy za pomocą dostępu sygnatury dostępu Współdzielonego lub uwierzytelniania opartego na kluczu. Firma Microsoft zaleca SAS, ale uwierzytelniania opartego na kluczu udostępnia prosty programowania i jest zgodny z wielu istniejących wydawców elementu webhook. 

Wartość uwierzytelniania hello objąć hello nagłówka HTTP. Sygnatury dostępu Współdzielonego, można użyć **Æg sas token** hello wartości nagłówka. Dla uwierzytelniania opartego na kluczu, użyj **Æg sas klucza** hello wartości nagłówka.

### <a name="key-authentication"></a>Uwierzytelnianie za pomocą klucza

Uwierzytelnianie za pomocą klucza jest hello najprostszej formy uwierzytelniania. Użyj formatu hello:`aeg-sas-key: <your key>`

Na przykład można przekazać klucza z: 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>Tokeny sygnatur dostępu współdzielonego

Tokeny sygnatury dostępu Współdzielonego dla zdarzeń siatki obejmują hello zasobu czas wygaśnięcia i podpis. Witaj format tokenu sygnatury dostępu Współdzielonego hello jest: `r={resource}&e={expiration}&s={signature}`.

Hello zasób jest hello ścieżki dla toowhich tematu hello wysyłania zdarzeń. Na przykład ścieżka prawidłowego zasobu to:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

Podpis hello jest generowanie z klucza.

Na przykład prawidłowy **Æg sas token** wartość to:

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

Hello poniższy przykład tworzy token sygnatury dostępu Współdzielonego do użytku z siatki zdarzeń:

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a>Kontrola dostępu administracyjnego

Azure siatki zdarzeń umożliwia możesz toocontrol hello poziom dostępu podany toodifferent użytkowników toodo różne operacje zarządzania, takie jak listy subskrypcji zdarzeń, tworzenie nowych i generowania kluczy. Siatki zdarzenia dla tego korzysta z platformy Azure na podstawie ról dostępu Sprawdź (RBAC).

### <a name="operation-types"></a>Typy operacji

Siatka zdarzeń platformy Azure obsługuje hello następujące akcje:

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

Witaj ostatnie trzy operacje zwracany potencjalnie poufne informacje, które pobiera przefiltrowane z normalnych operacji odczytu. Jest najlepszym rozwiązaniem dla Ciebie toorestrict dostępu toothese operacji. Role niestandardowe można tworzyć przy użyciu [programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure interfejsu wiersza polecenia (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)i hello [interfejsu API REST](../active-directory/role-based-access-control-manage-access-rest.md).

### <a name="enforcing-role-based-access-check-rbac"></a>Wymuszanie roli na podstawie sprawdzanie dostępu (RBAC)

Użyj hello następujące kroki tooenforce RBAC dla różnych użytkowników:

#### <a name="create-a-custom-role-definition-file-json"></a>Utwórz plik definicji niestandardowej roli zabezpieczeń (JSON)

Witaj poniżej przedstawiono przykładowe definicje ról siatki zdarzeń, których użytkownicy tooperform różnych zestawów działań.

**EventGridReadOnlyRole.json**: Zezwalaj tylko na tylko operacji odczytu.
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

**EventGridNoDeleteListKeysRole.json**: Zezwalaj na akcje po ograniczone, ale nie zezwalaj akcje usuwania.
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
**EventGridContributorRole.json**: umożliwia wszystkie akcje siatki zdarzeń.  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a>Instalowanie i logowania tooAzure interfejsu wiersza polecenia

* Azure CLI w wersji 0.8.8 lub nowszej. tooinstall hello najnowszej wersji i powiąż go z subskrypcją platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md).
* Usługa Azure Resource Manager w interfejsu wiersza polecenia platformy Azure. Przejdź za[hello Using Azure CLI z hello Resource Manager](../xplat-cli-azure-resource-manager.md) więcej szczegółów.

#### <a name="create-a-custom-role"></a>Tworzenie niestandardowej roli zabezpieczeń

toocreate niestandardowej roli zabezpieczeń, należy użyć:

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a>Przypisz hello roli tooa użytkownika


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>Następne kroki

* Aby tooEvent wprowadzenie siatki, zobacz [o siatki zdarzeń](overview.md)
