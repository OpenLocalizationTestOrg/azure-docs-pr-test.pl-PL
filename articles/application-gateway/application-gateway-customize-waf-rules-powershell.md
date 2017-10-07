---
title: "reguły zapory aplikacji sieci web aaaCustomize bramę aplikacji Azure — PowerShell | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje dotyczące sposobu reguły zapory aplikacji sieci web toocustomize w bramy aplikacji przy użyciu programu PowerShell."
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
ms.openlocfilehash: f320e687b0f621515255469dac8e375cdd900dda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a>Dostosowywanie reguły zapory aplikacji sieci web za pomocą programu PowerShell

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-customize-waf-rules-cli.md)

Zapora aplikacji sieci web Hello Azure Application Gateway (WAF) zapewnia ochronę dla aplikacji sieci web. Te zabezpieczenia są dostarczane przez hello Otwórz sieci Web aplikacji zabezpieczeń projektu (OWASP) podstawowe reguły Ustaw (CRS). Niektóre zasady mogą spowodować fałszywych alarmów i zablokowanie ruchu prawdziwe. Z tego powodu Application Gateway udostępnia hello możliwości toocustomize zasady grupy i zasady. Aby uzyskać więcej informacji na powitania określonej reguły grup i reguł, zobacz [listy grup CRS reguły zapory aplikacji sieci web i reguł](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Widok grup reguł i zasad

Hello następujące przykłady kodu przedstawiono sposób tooview zasady, a zasada grupy, które są konfigurowane na bramie aplikacji z obsługą zapory aplikacji sieci Web.

### <a name="view-rule-groups"></a>Grupy reguł widoku

powitania po przykładzie pokazano, jak tooview grup reguł:

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

następujące dane wyjściowe Hello jest skróconą odpowiedzi z hello poprzedzających przykład:

```
OWASP (Ver. 3.0):

    REQUEST-910-IP-REPUTATION:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            910011     Rule 910011
            910012     Rule 910012
            ...        ...

    REQUEST-911-METHOD-ENFORCEMENT:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            911011     Rule 911011
            ...        ...

OWASP (Ver. 2.2.9):

    crs_20_protocol_violations:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            960911     Invalid HTTP Request Line
            981227     Apache Error: Invalid URI in Request.
            960000     Attempted multipart/form-data bypass
            ...        ...
```

## <a name="disable-rules"></a>Wyłącz reguły

Witaj poniższy przykład powoduje wyłączenie reguł `910018` i `910017` na bramę aplikacji:

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Następne kroki

Po skonfigurowaniu reguł wyłączone, możesz dowiedzieć się jak tooview dzienniki zapory aplikacji sieci Web. Aby uzyskać więcej informacji, zobacz [diagnostyki bramy aplikacji](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
