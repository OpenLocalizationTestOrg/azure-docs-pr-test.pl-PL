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
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a><span data-ttu-id="7f2b7-103">Dostosowywanie reguły zapory aplikacji sieci web za pośrednictwem hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7f2b7-103">Customize web application firewall rules through hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f2b7-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7f2b7-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="7f2b7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f2b7-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="7f2b7-106">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="7f2b7-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="7f2b7-107">Zapora aplikacji sieci web Hello Azure Application Gateway (WAF) zapewnia ochronę dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7f2b7-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="7f2b7-108">Te zabezpieczenia są dostarczane przez hello Otwórz sieci Web aplikacji zabezpieczeń projektu (OWASP) podstawowe reguły Ustaw (CRS).</span><span class="sxs-lookup"><span data-stu-id="7f2b7-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="7f2b7-109">Niektóre zasady mogą spowodować fałszywych alarmów i zablokowanie ruchu prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="7f2b7-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="7f2b7-110">Z tego powodu Application Gateway udostępnia hello możliwości toocustomize zasady grupy i zasady.</span><span class="sxs-lookup"><span data-stu-id="7f2b7-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="7f2b7-111">Aby uzyskać więcej informacji na powitania określonej reguły grup i reguł, zobacz [listy grup reguł CRS zapory aplikacji sieci web i reguł](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="7f2b7-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="7f2b7-112">Widok grup reguł i zasad</span><span class="sxs-lookup"><span data-stu-id="7f2b7-112">View rule groups and rules</span></span>

<span data-ttu-id="7f2b7-113">Hello następujące przykłady kodu pokazują, jak tooview reguł i grup, które można skonfigurować reguły.</span><span class="sxs-lookup"><span data-stu-id="7f2b7-113">hello following code examples show how tooview rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="7f2b7-114">Grupy reguł widoku</span><span class="sxs-lookup"><span data-stu-id="7f2b7-114">View rule groups</span></span>

<span data-ttu-id="7f2b7-115">Witaj poniższy przykład pokazuje, jak tooview hello grup reguł:</span><span class="sxs-lookup"><span data-stu-id="7f2b7-115">hello following example shows how tooview hello rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="7f2b7-116">następujące dane wyjściowe Hello jest skróconą odpowiedzi z hello poprzedzających przykład:</span><span class="sxs-lookup"><span data-stu-id="7f2b7-116">hello following output is a truncated response from hello preceding example:</span></span>

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

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="7f2b7-117">Wyświetl reguły grupy reguły</span><span class="sxs-lookup"><span data-stu-id="7f2b7-117">View rules in a rule group</span></span>

<span data-ttu-id="7f2b7-118">Witaj poniższy przykład pokazuje, jak tooview zasady grupy określonej reguły:</span><span class="sxs-lookup"><span data-stu-id="7f2b7-118">hello following example shows how tooview rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="7f2b7-119">następujące dane wyjściowe Hello jest skróconą odpowiedzi z hello poprzedzających przykład:</span><span class="sxs-lookup"><span data-stu-id="7f2b7-119">hello following output is a truncated response from hello preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="7f2b7-120">Wyłącz reguły</span><span class="sxs-lookup"><span data-stu-id="7f2b7-120">Disable rules</span></span>

<span data-ttu-id="7f2b7-121">Witaj poniższy przykład powoduje wyłączenie reguł `910018` i `910017` na bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="7f2b7-121">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="7f2b7-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f2b7-122">Next steps</span></span>

<span data-ttu-id="7f2b7-123">Po skonfigurowaniu reguł wyłączone, możesz dowiedzieć się jak tooview dzienniki zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7f2b7-123">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="7f2b7-124">Aby uzyskać więcej informacji, zobacz [diagnostyki bramy aplikacji](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="7f2b7-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
