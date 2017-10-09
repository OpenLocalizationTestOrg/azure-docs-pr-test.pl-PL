---
title: "aaaResource Menedżera interfejsów API REST | Dokumentacja firmy Microsoft"
description: "Omówienie hello uwierzytelniania interfejsów API REST usługi Resource Manager i przykłady użycia"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a>Interfejsy API REST Menedżera zasobów
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Interfejs wiersza polecenia platformy Azure](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [Interfejs API REST](resource-manager-rest-api.md)
> 
> 

Za co wywołanie tooAzure Resource Manager za każdy wdrożonej szablon za co konto magazynu skonfigurowanych istnieją co najmniej jednego wywołania toohello usługi Azure Resource Manager przez interfejs API RESTful. Ten temat jest przeznaczony toothose interfejsów API i sposób ich wywołania bez przy użyciu dowolnego zestawu SDK w ogóle. Takie rozwiązanie jest przydatne, jeśli mają pełną kontrolę nad tooAzure żądania lub hello zestawu SDK dla preferowany język jest niedostępny lub nie obsługuje operacji hello, które są potrzebne.

W tym artykule nie przechodzi przez każdy interfejs API, który jest narażony na platformie Azure, ale raczej używa niektóre operacje jako przykłady sposobu połączenia toothem. Po zidentyfikowaniu podstawy hello może odczytywać hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind szczegółowe informacje dotyczące sposobu toouse hello reszty hello interfejsów API.

## <a name="authentication"></a>Authentication
Uwierzytelnianie dla Menedżera zasobów jest obsługiwane przez usługi Azure Active Directory (AD). tooany tooconnect interfejsu API, musisz najpierw tooauthenticate z usługi Azure AD tooreceive tokenu uwierzytelniania, które można przekazać na żądanie tooevery. Jak możemy są opisujące wywołanie czystej bezpośrednio toohello interfejsów API REST przyjęto założenie, że nie chcesz tooauthenticate przy wyświetlaniu monitu o nazwę użytkownika i hasło. Możemy również założenie, że nie używasz dwa mechanizmy uwierzytelniania Multi-Factor. W związku z tym utworzymy tak zwany aplikacji usługi Azure AD i są używane toolog w nazwy głównej usługi. Należy jednak pamiętać, że usługi Azure AD obsługuje kilka procedur uwierzytelniania i wszystkich z nich może być używane tooretrieve ten token uwierzytelniania, czego potrzebujemy dla kolejnych żądań interfejsu API.
Postępuj zgodnie z [Azure tworzenie aplikacji usługi AD i nazwę główną usługi](resource-group-create-service-principal-portal.md) instrukcje krok po kroku.

### <a name="generating-an-access-token"></a>Generuje Token dostępu
Uwierzytelnianie w usłudze Azure AD odbywa się przez wywołanie metody limit tooAzure AD, znajdujący się w login.microsoftonline.com. tooauthenticate, należy hello toohave następujących informacji:

* Identyfikator dzierżawy usługi Azure AD (hello nazwa tej usługi Azure AD, czy używasz toolog w, często hello taki sam jak firmy, ale nie jest konieczna)
* Identyfikator aplikacji (podjętych podczas kroku tworzenia aplikacji hello Azure AD)
* Hasło (wybranej podczas tworzenia hello aplikacji usługi Azure AD)

Hello następujące żądania HTTP upewnij się, że tooreplace "Azure AD dzierżawy ID", "Identyfikator aplikacji" i "Password" hello poprawne wartości.

**Rodzajowe żądanie HTTP:**

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

... zostanie (Jeśli uwierzytelnianie zakończy się powodzeniem) powoduje odpowiedzi toohello podobne, po odpowiedzi:

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
(' access_token ' hello w hello poprzedzających odpowiedzi zostały skrócone tooincrease czytelności)

**Generowanie tokenu dostępu, używając Bash:**

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

**Generowanie tokenu dostępu przy użyciu programu PowerShell:**

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

odpowiedź Hello zawiera token dostępu, informacje o tym, jak długo token jest prawidłowy i informacje o jakie zasobów można użyć tokenu dla.
token dostępu Hello otrzymane w hello poprzedniego wywołania HTTP muszą być przekazywane w dla wszystkich toohello żądania interfejsu API Menedżera zasobów. Przekaż go jako wartość nagłówka o nazwie "Autoryzacja" o wartości hello "Bearer YOUR_ACCESS_TOKEN". Zwróć uwagę, hello odstęp między "Bearer" i tokenu dostępu.

Jak widać z hello powyżej wynik HTTP hello token jest prawidłowy dla określonego okresu czasu, w którym powinien pamięci podręcznej i ponowne użycie tego samego tokenu. Nawet jeśli jest możliwe tooauthenticate w usłudze Azure AD dla każdego wywołania interfejsu API, może być bardzo mało wydajne.

## <a name="calling-resource-manager-rest-apis"></a>Menedżer zasobów wywołania interfejsów API REST
W tym temacie używa tylko kilka interfejsów API tooexplain hello podstawowe sposoby użycia operacji REST hello. Informacje o wszystkich operacji hello, zobacz [interfejsów API REST usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).

### <a name="list-all-subscriptions"></a>Wyświetl listę wszystkich subskrypcji
Jednej z operacji najprostszym hello, które może wykonywać jest toolist hello dostępnych subskrypcji są dostępne. Hello następujące żądania jest widoczny jak token dostępu hello jest przekazywany jako nagłówka:

(Zamiast YOUR_ACCESS_TOKEN Twojego rzeczywiste Token dostępu).

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

... i w związku z tym można uzyskać listę subskrypcji tej nazwy głównej usługi jest możliwość tooaccess

(Identyfikatory subskrypcji zostały skrócone dla czytelności)

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a>Wyświetl listę wszystkich grup zasobów w określonej subskrypcji
Wszystkie zasoby dostępne z hello interfejsów API Menedżera zasobów są zagnieżdżone w grupie zasobów. Menedżer zasobów dla istniejącej grupy zasobów można badać w ramach subskrypcji przy użyciu hello następujące żądania HTTP GET. Zwróć uwagę, jak identyfikator subskrypcji hello jest przekazywany jako część adresu URL hello teraz.

(Zamiast YOUR_ACCESS_TOKEN i IDENTYFIKATOR_SUBSKRYPCJI dostępu rzeczywisty identyfikator token i subskrypcji)

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

Witaj odpowiedzi, możesz uzyskać zależy od tego, czy zdefiniowano żadnych grup zasobów, a jeśli tak, jak wiele.

(Identyfikatory subskrypcji zostały skrócone dla czytelności)

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
Do tej pory firma Microsoft już tylko zostały zapytań hello interfejsów API Menedżera zasobów informacji. Nadszedł czas, możemy utworzyć niektórych zasobów i Zacznijmy od hello Najprostszym z nich wszystkie grupy zasobów. Hello następujące żądania HTTP tworzy grupę zasobów w regionu/lokalizacji i dodaje tooit tagu.

(Zastąp YOUR_ACCESS_TOKEN, IDENTYFIKATOR_SUBSKRYPCJI, RESOURCE_GROUP_NAME z rzeczywistego tokenu dostępu, identyfikator subskrypcji i nazwę grupy zasobów ma toocreate hello)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

W przypadku powodzenia można uzyskać odpowiedzi, która jest podobne toohello po odpowiedzi:

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

Pomyślnie utworzona grupa zasobów na platformie Azure. Gratulacje!

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a>Wdrażanie grupy zasobów tooa zasobów przy użyciu szablonu usługi Resource Manager
Usługa Resource Manager można wdrożyć zasobów za pomocą szablonów. Szablon definiuje kilka zasobów oraz ich zależności. Dla tej sekcji przyjęto założenie, znasz szablony Menedżera zasobów i firma Microsoft tylko wyświetlić sposób toomake hello API wywołać toostart wdrożenia. Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).

Wdrożenie szablonu nie różnią się znacznie toohow wywołania innych interfejsów API. Jeden istotnym elementem jest, że wdrażania szablonu może zająć sporo czasu. Wywołanie interfejsu API Hello właśnie zwraca i jest tooyou jako tooquery developer stanu toofind wdrożenia hello wychodzących po zakończeniu wdrażania hello. Aby uzyskać więcej informacji, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).

W tym przykładzie używamy publicznie ujawnionych szablon dostępny na [GitHub](https://github.com/Azure/azure-quickstart-templates). Szablon Hello używamy wdraża regionu zachodnie stany USA toohello maszyny Wirtualnej systemu Linux. Mimo że w tym przykładzie używa szablonu dostępne w publicznych repozytorium, takich jak GitHub, zamiast tego można przekazać hello pełny szablon jako część żądania hello. Należy pamiętać, że firma Microsoft udostępnia wartości parametrów w żądaniu hello, które są używane wewnątrz hello wdrożyć szablon.

(Zastąp IDENTYFIKATOR_SUBSKRYPCJI, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD i DNS_NAME_FOR_PUBLIC_IP toovalues odpowiednie dla żądania)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

Hello długi JSON odpowiedzi na to żądanie został pominięty tooimprove czytelność niniejszej dokumentacji. odpowiedź Hello zawiera informacje o hello opartego na szablonie wdrożenia, który został utworzony.

## <a name="next-steps"></a>Następne kroki

- toolearn dotyczące obsługi operacji asynchronicznych REST, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).
