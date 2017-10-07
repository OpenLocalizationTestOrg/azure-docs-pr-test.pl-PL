---
title: "aaaSecure dostęp do aplikacji logiki tooAzure | Dokumentacja firmy Microsoft"
description: "Dodawanie zabezpieczeń do ochrony tootriggers dostępu, danych wejściowych i wyjściowych parametry akcji i usług używanych wraz z przepływów pracy w programie Azure Logic Apps."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a>Bezpieczny dostęp do aplikacji logiki tooyour

Istnieje wiele toohelp dostępne narzędzia, które należy zabezpieczyć aplikację logiki.

* Zabezpieczanie dostępu tootrigger aplikacja logiki (wyzwalacza żądania HTTP)
* Zabezpieczanie dostępu toomanage, edytować lub odczytać aplikacji logiki
* Zabezpieczanie dostępu toocontents z wejściami i wyjściami dla przebiegu
* Zabezpieczanie parametrów lub danych wejściowych w ramach działań w przepływie pracy
* Zabezpieczanie tooservices dostępu, który odbierania żądań z przepływu pracy

## <a name="secure-access-tootrigger"></a>Bezpieczny dostęp tootrigger

Podczas pracy z aplikacji logiki, które są generowane na żądania HTTP ([żądania](../connectors/connectors-native-reqres.md) lub [Webhook](../connectors/connectors-native-webhook.md)), można ograniczyć dostęp tak, aby tylko autoryzowani klienci mogą wyzwalać hello aplikacji logiki. Wszystkie żądania do aplikacji logiki są szyfrowane i chronione za pomocą protokołu SSL.

### <a name="shared-access-signature"></a>Sygnatury dostępu współdzielonego

Każdy punkt końcowy żądania dla aplikacji logiki obejmuje [dostępu sygnatury dostępu Współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) jako część hello adresu URL. Każdy adres URL zawiera `sp`, `sv`, i `sig` parametr zapytania. Uprawnienia są określane przez `sp`, i odpowiada metod tooHTTP dozwolonych, `sv` jest toogenerate wersja użyta hello, i `sig` jest używane tooauthenticate tootrigger dostępu. Podpis Hello jest generowany przy użyciu algorytmu hello SHA256 z kluczem tajnym na wszystkie właściwości i ścieżki adresu URL hello. klucz tajny Hello nigdy nie jest widoczne i opublikowana i są przechowywane w zaszyfrowanej i przechowywane hello aplikacji logiki. Aplikację logiki autoryzuje tylko wyzwalaczy, które zawiera prawidłowy podpis utworzone za pomocą hello klucz tajny.

#### <a name="regenerate-access-keys"></a>Ponowne generowanie kluczy dostępu

Można ponownie wygenerować nowy klucz bezpiecznego w dowolnym momencie za pośrednictwem portalu hello interfejsu API REST lub Azure. Wszystkie bieżącego adresów URL, które zostały wygenerowane wcześniej przy użyciu starego klucza hello są aplikacji logiki hello toofire nieważne i nie będzie autoryzowany.

1. Hello portalu Azure Otwórz aplikację logiki hello ma tooregenerate klucza
1. Kliknij przycisk hello **klucze dostępu** elementu menu pod **ustawienia**
1. Wybierz hello tooregenerate klucza i pełny hello procesu

Adresy URL, który można pobrać po ponowne generowanie są podpisane za pomocą hello nowy klucz dostępu.

#### <a name="creating-callback-urls-with-an-expiration-date"></a>Tworzenie adresów URL wywołania zwrotnego z datą wygaśnięcia

Adres URL hello w przypadku udostępniania innym osobom, można wygenerować adresy URL określone klucze i daty ważności, zgodnie z potrzebami. Można następnie bezproblemowo przywracania kluczy lub zapewnienia toofire dostępu do aplikacji jest ograniczony tooa niektórych timespan. Można określić datę wygaśnięcia dla danego adresu URL za pośrednictwem hello [logiki aplikacji interfejsu API REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

W treści hello zawiera właściwości hello `NotAfter` jako ciąg daty JSON, który zwraca adres URL wywołania zwrotnego, który jest prawidłowy tylko do hello `NotAfter` daty i godziny.

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>Tworzenie adresów URL z podstawowym lub pomocniczym klucz tajny

Podczas generowania lub umieszczanie na liście adresów URL wywołania zwrotnego na podstawie żądań wyzwalaczy, można także określić adres URL, hello który klucza toouse toosign.  Możesz wygenerować adresu URL podpisane przez określonego klucza za pomocą hello [logiki aplikacji interfejsu API REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers) w następujący sposób:

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

W treści hello zawiera właściwości hello `KeyType` jako `Primary` lub `Secondary`.  Zwróci ono podpisane przez klucz zabezpieczeń hello określony adres URL.

### <a name="restrict-incoming-ip-addresses"></a>Ogranicz przychodzących adresów IP

Ponadto toohello Shared Access Signature, warto zapoznać się z toorestrict wywoływanie aplikacji logiki tylko z określonym klientem.  Na przykład, jeśli zarządzasz punktu końcowego za pośrednictwem usługi Azure API Management, można ograniczyć hello logiki aplikacji tooonly Zaakceptuj Żądanie hello, gdy hello żądanie pochodzi z adresu IP wystąpienia interfejsu API zarządzania hello.

To ustawienie można skonfigurować w ramach ustawień aplikacji logiki hello:

1. Hello portalu Azure Otwórz aplikację logiki hello ma ograniczenia adresu IP tooadd
1. Kliknij przycisk hello **konfiguracji kontroli dostępu** elementu menu pod **ustawienia**
1. Określ listę hello toobe zakresów adresów IP zaakceptowane przez wyzwalacz hello

Prawidłowy zakres IP ma hello format `192.168.1.1/255`. Witaj logiki aplikacji tooonly fire jako aplikację logiki zagnieżdżonych, zaznacz hello **tylko innych aplikacji logiki** opcji. Ta opcja powoduje zapisanie zasobów toohello pusta tablica, co oznacza, że tylko wywołania z hello samą usługą fire (aplikacje logiki nadrzędnego) pomyślnie.

> [!NOTE]
> Nadal można uruchomić aplikacji logiki z wyzwalaczem żądanie za pośrednictwem interfejsu API REST hello / zarządzania `/triggers/{triggerName}/run` niezależnie od adresu IP. Ten scenariusz wymaga uwierzytelniania przed hello interfejsu API REST Azure, a wszystkie zdarzenia pojawiały się hello dziennik inspekcji Azure. Ustaw dostęp do kontrolowania zasad odpowiednio.

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Ustawianie zakresów adresów IP w definicji zasobu hello

Jeśli używasz [Szablon wdrożenia](logic-apps-create-deploy-template.md) tooautomate wdrożeń, ustawienia zakres IP hello można skonfigurować na powitania zasobu szablon.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>Dodawanie usługi Azure Active Directory, OAuth lub innych zabezpieczeń

protokoły więcej autoryzacji na podstawie aplikacji logiki, tooadd [Azure API Management](https://azure.microsoft.com/services/api-management/) oferuje rozbudowane monitorowanie, zabezpieczeń, zasad i dokumentacji dla dowolnego punktu końcowego z tooexpose możliwości hello aplikacji logiki jako interfejs API. Zarządzanie interfejsami API Azure mogą uwidaczniać publicznych lub prywatnych punktu końcowego dla aplikacji logiki hello, który może używać usługi Azure Active Directory, certyfikat, OAuth lub innych standardów zabezpieczeń. Po odebraniu żądania usługi Azure API Management przekazuje hello żądania toohello aplikacja logiki (wykonanie żadnych ograniczeń locie lub przekształcenia wymagane). Można użyć hello przychodzące zakres IP ustawień na powitania logiki aplikacji tooonly umożliwiającej toobe aplikacji logiki hello wywołany z interfejsu API zarządzania.

## <a name="secure-access-toomanage-or-edit-logic-apps"></a>Bezpieczny dostęp do aplikacji logiki toomanage lub edycji

Tak, aby tylko określonym użytkownikom lub grupom są możliwe tooperform operacji dla zasobu hello, można ograniczyć dostęp toomanagement operacji w aplikacji logiki. Aplikacje logiki używać hello Azure [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md) funkcji i można dostosować za pomocą hello tych samych narzędzi.  Istnieje kilka wbudowanych ról, które można przypisać również członkowie tooas Twojej subskrypcji:

* **Współautor aplikacji logiki** — zapewnia dostęp tooview, edycji i aktualizacji aplikacji logiki.  Nie można usunąć zasobu hello ani wykonywać operacje administracyjne.
* **Operator aplikacji logiki** — można wyświetlić aplikacji logiki hello i Historia uruchomień i włączanie/wyłączanie.  Nie można edytować ani aktualizacji definicji hello.

Można również użyć [Blokada zasobu Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent, zmienianie lub usuwanie aplikacji logiki. Ta funkcja jest przydatna tooprevent produkcji zasobów z zmiany i usunięcia.

## <a name="secure-access-toocontents-of-hello-run-history"></a>Toocontents bezpieczny dostęp z hello Historia uruchomień

Z poprzednich zakresów adresów IP toospecific działa, można ograniczyć toocontents dostępu do danych wejściowych lub wyjściowych.  

Wszystkie dane w ramach wykonywania przepływu pracy są szyfrowane przesyłanych i przechowywanych. Gdy historii toorun połączeń, usługa hello uwierzytelnia Żądanie hello i udostępnia łącza toohello żądania i odpowiedzi wejściami i wyjściami. To łącze może być chronione żądań tak tylko zawartość hello powrócić tooview zawartości z wyznaczonych zakresu adresów IP. Ta funkcja służy do kontroli dostępu dodatkowe. Można nawet określić adres IP, takich jak `0.0.0.0` , nikt nie mógł uzyskać dostępu do danych wejściowych/wyjściowych. Tylko osoby z uprawnieniami administratora może usunąć to ograniczenie, zapewniając możliwość powitania dla zawartości tooworkflow dostępu "just-in-time".

To ustawienie można skonfigurować w ramach ustawienia zasobów hello hello portalu Azure:

1. Hello portalu Azure Otwórz aplikację logiki hello ma ograniczenia adresu IP tooadd
1. Kliknij przycisk hello **konfiguracji kontroli dostępu** elementu menu pod **ustawienia**
1. Określ listę hello zakresy adresów IP dla toocontent dostępu

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Ustawianie zakresów adresów IP w definicji zasobu hello

Jeśli używasz [Szablon wdrożenia](logic-apps-create-deploy-template.md) tooautomate wdrożeń, ustawienia zakres IP hello można skonfigurować na powitania zasobu szablon.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>Zabezpieczanie parametry i dane wejściowe w przepływie pracy

Możesz tooparameterize niektórych aspektów definicję przepływu pracy dla wdrażania w środowiskach. Ponadto niektóre parametry mogą być bezpiecznego parametrów, które nie mają tooappear podczas edytowania przepływu pracy, takich jak identyfikator klienta i klucz tajny klienta dla [uwierzytelniania usługi Azure Active Directory](../connectors/connectors-native-http.md#authentication) akcji HTTP.

### <a name="using-parameters-and-secure-parameters"></a>Przy użyciu parametrów i bezpieczne

tooaccess hello wartości parametru zasobów w czasie wykonywania, hello [język definicji przepływu pracy](http://aka.ms/logicappsdocs) zapewnia `@parameters()` operacji. Można również [Określ parametry szablonu wdrażania zasobów hello](../azure-resource-manager/resource-group-authoring-templates.md#parameters). Ale jeśli określony typ parametru hello jako `securestring`, parametr hello nie będą zwracane z hello reszty hello definicji zasobu i nie będzie dostępny, wyświetlając zasobów powitania po wdrożeniu.

> [!NOTE]
> Jeśli parametr jest używany w nagłówkach hello lub treści żądania, parametr hello mogą być widoczne uzyskując dostęp do historii hello Uruchom i wychodzących żądania HTTP. Należy zasad dostępu do zawartości tooset się odpowiednio.
> Nagłówki autoryzacji nie są widoczne za pośrednictwem wejściowych i wyjściowych. Dlatego jeśli klucz tajny hello jest używany istnieje, klucz tajny hello nie jest pobieranie.

#### <a name="resource-deployment-template-with-secrets"></a>Szablon wdrożenia zasobów z kluczy tajnych

Witaj poniższy przykład przedstawia wdrożenia, który odwołuje się do parametru secure `secret` w czasie wykonywania. W pliku parametrów oddzielne można określić wartość środowiska hello hello `secret`, lub użyj [KeyVault Menedżera zasobów Azure](../azure-resource-manager/resource-manager-keyvault-parameter.md) kluczy tajnych tooretrieve na wdrażanie czasu.

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a>Bezpieczny dostęp do odbierania żądań tooservices z przepływu pracy

Istnieje wiele sposobów toohelp są bezpieczne, dowolną aplikację logiki hello punktu końcowego wymaga tooaccess.

### <a name="using-authentication-on-outbound-requests"></a>Przy użyciu uwierzytelniania w odpowiedzi na żądania wychodzącego

Podczas pracy z HTTP, HTTP + Swagger (otwarty interfejs API) lub elementu Webhook akcji, możesz dodać wysyłane żądania toohello uwierzytelniania. Mogą obejmować uwierzytelnianie podstawowe, uwierzytelnianie certyfikatu lub uwierzytelniania usługi Azure Active Directory. Szczegóły dotyczące sposobu tooconfigure tego uwierzytelniania można znaleźć [w tym artykule](../connectors/connectors-native-http.md#authentication).

### <a name="restricting-access-toologic-app-ip-addresses"></a>Ograniczenia adresów IP aplikacji toologic dostępu

Wywołania z aplikacji logiki pochodzą z określonego zestawu adresów IP dla regionu. Możesz dodać dodatkowe filtrowania tooonly akceptowania żądań od wyznaczonych adresów IP. Aby uzyskać listę adresów IP, zobacz [limity aplikacji logiki i konfiguracji](logic-apps-limits-and-config.md#configuration).

### <a name="on-premises-connectivity"></a>Łączność lokalna

Aplikacje logiki mają integracji z kilku usług tooprovide bezpieczny i niezawodny lokalnej komunikacji.

#### <a name="on-premises-data-gateway"></a>Brama danych lokalnych

Wiele łączników zarządzanych dla usługi logic apps Podaj bezpieczna łączność systemów lokalnych tooon, w tym systemie plików, SQL, SharePoint i bazy danych DB2. Brama Hello przekazuje dane z lokalnych źródeł w kanałach zaszyfrowane za pomocą hello Azure Service Bus. Cały ruch pochodzi jako bezpieczny ruch wychodzący z hello bramy agenta. Dowiedz się więcej o [działanie bramy danych hello](logic-apps-gateway-install.md#gateway-cloud-service).

#### <a name="azure-api-management"></a>Usługa Azure API Management

[Zarządzanie interfejsami API Azure](https://azure.microsoft.com/services/api-management/) ma opcji łączności lokalnie, w tym site-to-site VPN i ExpressRoute integracji zabezpieczonych systemów lokalnych tooon serwera proxy i komunikacji. W hello projektanta aplikacji logiki możesz szybko zaznaczyć interfejs API widoczne z usługi Azure API Management w przepływie pracy, zapewniając systemów lokalnych tooon szybki dostęp.

#### <a name="hybrid-connections-from-azure-app-service"></a>Połączenia hybrydowe z usługi aplikacji Azure

Funkcja hello lokalnymi hybrydowego połączenia dla interfejsu API Azure i Web apps toocommunicate lokalnego.  Więcej informacji dotyczących połączeń hybrydowych i jak można znaleźć tooconfigure [w tym artykule](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="next-steps"></a>Następne kroki
[Tworzenie szablonu wdrożenia](logic-apps-create-deploy-template.md)  
[Obsługa wyjątków](logic-apps-exception-handling.md)  
[Monitorowanie aplikacji logiki](logic-apps-monitor-your-logic-apps.md)  
[Diagnozowanie błędów aplikacji logiki i problemy](logic-apps-diagnosing-failures.md)  
