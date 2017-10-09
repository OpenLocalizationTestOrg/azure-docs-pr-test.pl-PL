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
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="248d8-103">Dostosowywanie reguły zapory aplikacji sieci web za pośrednictwem hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="248d8-103">Customize web application firewall rules through hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="248d8-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="248d8-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="248d8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="248d8-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="248d8-106">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="248d8-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="248d8-107">Zapora aplikacji sieci web Hello Azure Application Gateway (WAF) zapewnia ochronę dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="248d8-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="248d8-108">Te zabezpieczenia są dostarczane przez hello Otwórz sieci Web aplikacji zabezpieczeń projektu (OWASP) podstawowe reguły Ustaw (CRS).</span><span class="sxs-lookup"><span data-stu-id="248d8-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="248d8-109">Niektóre zasady mogą spowodować fałszywych alarmów i zablokowanie ruchu prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="248d8-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="248d8-110">Z tego powodu Application Gateway udostępnia hello możliwości toocustomize zasady grupy i zasady.</span><span class="sxs-lookup"><span data-stu-id="248d8-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="248d8-111">Aby uzyskać więcej informacji na powitania określonej reguły grup i reguł, zobacz [listy grup reguł CRS zapory aplikacji sieci web i reguł](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="248d8-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="248d8-112">Bramy aplikacji nie używa hello warstwy zapory aplikacji sieci Web, w okienku po prawej stronie powitania pojawia się hello opcja tooupgrade hello aplikacji bramy toohello zapory aplikacji sieci Web warstwy.</span><span class="sxs-lookup"><span data-stu-id="248d8-112">If your application gateway is not using hello WAF tier, hello option tooupgrade hello application gateway toohello WAF tier appears in hello right pane.</span></span> 

![Włączanie zapory aplikacji sieci Web][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="248d8-114">Widok grup reguł i zasad</span><span class="sxs-lookup"><span data-stu-id="248d8-114">View rule groups and rules</span></span>

<span data-ttu-id="248d8-115">**grupy reguł tooview i reguł**</span><span class="sxs-lookup"><span data-stu-id="248d8-115">**tooview rule groups and rules**</span></span>
   1. <span data-ttu-id="248d8-116">Przeglądaj toohello aplikacji bramy, a następnie wybierz **zapory aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="248d8-116">Browse toohello application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="248d8-117">Wybierz **reguły zaawansowanej konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="248d8-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="248d8-118">Ten widok przedstawia tabeli na stronie powitania wszystkich grup reguł hello wyposażone hello wybrany zestaw reguł.</span><span class="sxs-lookup"><span data-stu-id="248d8-118">This view shows a table on hello page of all hello rule groups provided with hello chosen rule set.</span></span> <span data-ttu-id="248d8-119">Zaznaczono wszystkie pola wyboru hello reguły.</span><span class="sxs-lookup"><span data-stu-id="248d8-119">All of hello rule's check boxes are selected.</span></span>

![Konfigurowanie reguł wyłączone][1]

## <a name="search-for-rules-toodisable"></a><span data-ttu-id="248d8-121">Wyszukaj zasady toodisable</span><span class="sxs-lookup"><span data-stu-id="248d8-121">Search for rules toodisable</span></span>

<span data-ttu-id="248d8-122">Witaj **aplikacja, ustawienia zapory w sieci Web** bloku zapewnia możliwość hello toofilter hello reguł za pomocą funkcji wyszukiwania tekstu.</span><span class="sxs-lookup"><span data-stu-id="248d8-122">hello **Web application firewall settings** blade provides hello capability toofilter hello rules through a text search.</span></span> <span data-ttu-id="248d8-123">wynik Hello wyświetla tylko grupy reguł hello i reguł, które zawierają hello wyszukiwany tekst.</span><span class="sxs-lookup"><span data-stu-id="248d8-123">hello result displays only hello rule groups and rules that contain hello text you searched for.</span></span>

![Wyszukaj zasady][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="248d8-125">Wyłącz zasady grupy i zasady</span><span class="sxs-lookup"><span data-stu-id="248d8-125">Disable rule groups and rules</span></span>

<span data-ttu-id="248d8-126">Gdy sieci są wyłączenie reguł, można wyłączyć reguły całej grupy lub określone zasady w co najmniej jedną grupę reguł.</span><span class="sxs-lookup"><span data-stu-id="248d8-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="248d8-127">**grupy reguł toodisable lub określone zasady**</span><span class="sxs-lookup"><span data-stu-id="248d8-127">**toodisable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="248d8-128">Wyszukiwanie hello reguły lub grupy reguł, które mają toodisable.</span><span class="sxs-lookup"><span data-stu-id="248d8-128">Search for hello rules or rule groups that you want toodisable.</span></span>
   2. <span data-ttu-id="248d8-129">Usuń zaznaczenie pól wyboru hello hello zasady, które mają toodisable.</span><span class="sxs-lookup"><span data-stu-id="248d8-129">Clear hello check boxes for hello rules that you want toodisable.</span></span> 
   2. <span data-ttu-id="248d8-130">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="248d8-130">Select **Save**.</span></span> 

![Zapisz zmiany][3]

## <a name="next-steps"></a><span data-ttu-id="248d8-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="248d8-132">Next steps</span></span>

<span data-ttu-id="248d8-133">Po skonfigurowaniu reguł wyłączone, możesz dowiedzieć się jak tooview dzienniki zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="248d8-133">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="248d8-134">Aby uzyskać więcej informacji, zobacz [diagnostyki bramy aplikacji](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="248d8-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
