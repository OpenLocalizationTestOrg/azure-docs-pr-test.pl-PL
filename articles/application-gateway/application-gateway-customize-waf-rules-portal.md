---
title: "reguły zapory aplikacji sieci web aaaCustomize bramę aplikacji Azure — portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje dotyczące sposobu reguły zapory aplikacji sieci web toocustomize w bramy aplikacji z hello portalu Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a>Dostosowywanie reguły zapory aplikacji sieci web za pośrednictwem hello portalu Azure

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-customize-waf-rules-cli.md)

Zapora aplikacji sieci web Hello Azure Application Gateway (WAF) zapewnia ochronę dla aplikacji sieci web. Te zabezpieczenia są dostarczane przez hello Otwórz sieci Web aplikacji zabezpieczeń projektu (OWASP) podstawowe reguły Ustaw (CRS). Niektóre zasady mogą spowodować fałszywych alarmów i zablokowanie ruchu prawdziwe. Z tego powodu Application Gateway udostępnia hello możliwości toocustomize zasady grupy i zasady. Aby uzyskać więcej informacji na powitania określonej reguły grup i reguł, zobacz [listy grup reguł CRS zapory aplikacji sieci web i reguł](application-gateway-crs-rulegroups-rules.md).

>[!NOTE]
> Bramy aplikacji nie używa hello warstwy zapory aplikacji sieci Web, w okienku po prawej stronie powitania pojawia się hello opcja tooupgrade hello aplikacji bramy toohello zapory aplikacji sieci Web warstwy. 

![Włączanie zapory aplikacji sieci Web][fig1]

## <a name="view-rule-groups-and-rules"></a>Widok grup reguł i zasad

**grupy reguł tooview i reguł**
   1. Przeglądaj toohello aplikacji bramy, a następnie wybierz **zapory aplikacji sieci Web**.  
   2. Wybierz **reguły zaawansowanej konfiguracji**.  
   Ten widok przedstawia tabeli na stronie powitania wszystkich grup reguł hello wyposażone hello wybrany zestaw reguł. Zaznaczono wszystkie pola wyboru hello reguły.

![Konfigurowanie reguł wyłączone][1]

## <a name="search-for-rules-toodisable"></a>Wyszukaj zasady toodisable

Witaj **aplikacja, ustawienia zapory w sieci Web** bloku zapewnia możliwość hello toofilter hello reguł za pomocą funkcji wyszukiwania tekstu. wynik Hello wyświetla tylko grupy reguł hello i reguł, które zawierają hello wyszukiwany tekst.

![Wyszukaj zasady][2]

## <a name="disable-rule-groups-and-rules"></a>Wyłącz zasady grupy i zasady

Gdy sieci są wyłączenie reguł, można wyłączyć reguły całej grupy lub określone zasady w co najmniej jedną grupę reguł. 

**grupy reguł toodisable lub określone zasady**

   1. Wyszukiwanie hello reguły lub grupy reguł, które mają toodisable.
   2. Usuń zaznaczenie pól wyboru hello hello zasady, które mają toodisable. 
   2. Wybierz pozycję **Zapisz**. 

![Zapisz zmiany][3]

## <a name="next-steps"></a>Następne kroki

Po skonfigurowaniu reguł wyłączone, możesz dowiedzieć się jak tooview dzienniki zapory aplikacji sieci Web. Aby uzyskać więcej informacji, zobacz [diagnostyki bramy aplikacji](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
