---
title: "aaaUse skalowania automatycznego akcje toosend poczty e-mail i elementu webhook powiadomień o alertach. | Microsoft Docs"
description: "Zobacz, jak toocall akcji skalowania automatycznego toouse adresy URL w sieci web lub wysyłania powiadomień e-mail w monitorze Azure. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a>Użyj automatycznego skalowania akcje toosend poczty e-mail i elementu webhook powiadomień o alertach w monitorze Azure
W tym artykule opisano, jak skonfigurowaniu wyzwalaczy tak, aby można było wywołać adresu URL sieci web określonego lub wysyłania wiadomości e-mail w oparciu akcji skalowania automatycznego na platformie Azure.  

## <a name="webhooks"></a>elementów webhook
Elementów Webhook pozwalają tooroute hello Azure powiadomień o alertach tooother systemów przetwarzania końcowego lub niestandardowych powiadomień. Na przykład routingu tooservices alertu hello, które może obsłużyć przychodzący sieci web żądania toosend programu SMS, usterki dziennika powiadamiać zespołu za pomocą rozmowy lub usługami wiadomości, webhook hello itp. identyfikator URI musi być prawidłowy punkt końcowy HTTP lub HTTPS.

## <a name="email"></a>Adres e-mail
Może być wysyłana wiadomość e-mail tooany prawidłowy adres e-mail. Administratorzy i współadministratorzy hello subskrypcji, którym jest uruchomiona reguła hello również otrzymasz powiadomienie.

## <a name="cloud-services-and-web-apps"></a>Usługi w chmurze i aplikacje sieci Web
Użytkownik może zgody na z portalu Azure hello farm serwerów (aplikacje sieci Web) i usług w chmurze.

* Wybierz hello **skalowanie przez** metryki.

![Skalowanie przez](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a>Zestawy skalowania maszyny wirtualnej
W przypadku nowszych maszyn wirtualnych utworzonych za pomocą Menedżera zasobów (zestawy skalowania maszyny wirtualnej) można skonfigurować to przy użyciu interfejsu API REST, szablony usługi Resource Manager, programu PowerShell i interfejsu wiersza polecenia. Interfejs portalu nie jest jeszcze dostępna.
Korzystając z interfejsu API REST hello lub szablonu usługi Resource Manager, element include w hello powiadomienia o hello następujące opcje.

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| Pole | Obowiązkowe? | Opis |
| --- | --- | --- |
| Operacja |Tak |Wartość musi być "Skala" |
| sendToSubscriptionAdministrator |Tak |Wartość musi być "prawda" lub "false" |
| sendToSubscriptionCoAdministrators |Tak |Wartość musi być "prawda" lub "false" |
| customEmails |Tak |wartość może być null [] lub tablicy ciągów wiadomości e-mail |
| elementów webhook |Tak |wartość może być zerowy lub nieprawidłowy identyfikator Uri |
| serviceUri |Tak |Nieprawidłowy identyfikator Uri protokołu https |
| properties |Tak |Wartość musi być pusty {} lub może zawierać pary klucz wartość |

## <a name="authentication-in-webhooks"></a>Uwierzytelnianie w elementów webhook
Element webhook Hello uwierzytelniania z użyciem uwierzytelniania opartego na tokenie, gdzie zapisać elementu webhook hello identyfikatora URI identyfikatorem token jako parametr zapytania. Na przykład https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue

## <a name="autoscale-notification-webhook-payload-schema"></a>Funkcja automatycznego skalowania powiadomień elementu webhook ładunku schematu
Podczas generowania powiadomień skalowania automatycznego hello hello następujące metadane znajduje się w ładunku webhook hello:

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| Pole | Obowiązkowe? | Opis |
| --- | --- | --- |
| status |Tak |Stan Hello, który wskazuje, że wygenerowano akcji skalowania automatycznego |
| Operacja |Tak |Zwiększanie wystąpień będzie "Skaluj w poziomie" i w przypadku spadku wystąpień będzie "W skali" |
| Kontekst |Tak |kontekst akcji skalowania automatycznego Hello |
| sygnatura czasowa |Tak |Sygnatura czasowa wyzwolenia hello akcji skalowania automatycznego |
| id |Tak |Identyfikator Menedżera zasobów hello ustawieniu skalowania automatycznego |
| name |Tak |Nazwa Hello hello ustawieniu skalowania automatycznego |
| Szczegóły |Tak |Wyjaśnienie działań hello hello automatycznego skalowania usługi trwało i hello zmiana liczby wystąpień hello |
| subscriptionId |Tak |Identyfikator subskrypcji hello zasobu docelowego, który wykonywane jest skalowanie |
| Grupy zasobów o nazwie |Tak |Nazwa grupy zasobów zasobu docelowego hello wykonywane jest skalowanie |
| resourceName |Tak |Nazwa zasobu docelowego hello, że wykonywane jest skalowanie |
| Typ zasobu |Tak |Witaj trzy obsługiwane wartości: "microsoft.classiccompute/domainnames/slots/roles" - role usługi w chmurze, "microsoft.compute/virtualmachinescalesets" - zestawy skalowania maszyny wirtualnej i "Microsoft.Web/serverfarms" - aplikacji sieci Web |
| resourceId |Tak |Identyfikator zasobu docelowego hello, że wykonywane jest skalowanie Menedżera zasobów |
| portalLink |Tak |Strona podsumowania toohello linku portalu Azure hello zasobu docelowego |
| oldCapacity |Tak |Witaj bieżącą (stare) liczbę wystąpień podczas skalowania automatycznego trwało akcji skalowania |
| newCapacity |Tak |Hello skalowania automatycznego zbyt skalowania zasobu hello nowe liczba wystąpień|
| Właściwości |Nie |Opcjonalny. Zbiór < klucz, wartość > pary (na przykład słownika < String, String >). pole właściwości Hello jest opcjonalne. W niestandardowego interfejsu użytkownika lub przepływu pracy na podstawie aplikacji logiki można wprowadzić klucze i wartości, które mogą zostać przekazane za pomocą hello ładunku. Alternatywny sposób wywołania elementu webhook wychodzącego toohello kopii toopass właściwości niestandardowych jest toouse hello webhook identyfikatora URI się (jako parametry kwerendy) |
