---
title: "reguły zapory aplikacji sieci web aaaCustomize bramę aplikacji Azure — 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje dotyczące sposobu reguły zapory aplikacji sieci web toocustomize w bramy aplikacji z hello Azure CLI 2.0."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b83ffb9f6a7e0d0c8c970885d2bcb3b63d32581c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a>Dostosowywanie reguły zapory aplikacji sieci web za pośrednictwem hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-customize-waf-rules-cli.md)

Zapora aplikacji sieci web Hello Azure Application Gateway (WAF) zapewnia ochronę dla aplikacji sieci web. Te zabezpieczenia są dostarczane przez hello Otwórz sieci Web aplikacji zabezpieczeń projektu (OWASP) podstawowe reguły Ustaw (CRS). Niektóre zasady mogą spowodować fałszywych alarmów i zablokowanie ruchu prawdziwe. Z tego powodu Application Gateway udostępnia hello możliwości toocustomize zasady grupy i zasady. Aby uzyskać więcej informacji na powitania określonej reguły grup i reguł, zobacz [listy grup reguł CRS zapory aplikacji sieci web i reguł](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Widok grup reguł i zasad

Hello następujące przykłady kodu pokazują, jak tooview reguł i grup, które można skonfigurować reguły.

### <a name="view-rule-groups"></a>Grupy reguł widoku

Witaj poniższy przykład pokazuje, jak tooview hello grup reguł:

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

następujące dane wyjściowe Hello jest skróconą odpowiedzi z hello poprzedzających przykład:

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  },
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_2.2.9",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
   "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "crs_20_protocol_violations",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "2.2.9",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

### <a name="view-rules-in-a-rule-group"></a>Wyświetl reguły grupy reguły

Witaj poniższy przykład pokazuje, jak tooview zasady grupy określonej reguły:

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

następujące dane wyjściowe Hello jest skróconą odpowiedzi z hello poprzedzających przykład:

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": [
          {
            "description": "Rule 910011",
            "ruleId": 910011
          },
          ...
        ]
      }
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

## <a name="disable-rules"></a>Wyłącz reguły

Witaj poniższy przykład powoduje wyłączenie reguł `910018` i `910017` na bramę aplikacji:

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Następne kroki

Po skonfigurowaniu reguł wyłączone, możesz dowiedzieć się jak tooview dzienniki zapory aplikacji sieci Web. Aby uzyskać więcej informacji, zobacz [diagnostyki bramy aplikacji](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
