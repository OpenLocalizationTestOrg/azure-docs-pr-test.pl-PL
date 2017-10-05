---
title: "Dostosowywanie reguły zapory aplikacji sieci web w brama usługi aplikacji Azure — portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje na temat sposobu dostosowywania sieci web reguły zapory aplikacji w polu Brama aplikacji w portalu Azure."
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
ms.openlocfilehash: cdcbadbc3765dfc583c26e1b1453863d421c9a72
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="33d80-103">Dostosowywanie reguły zapory aplikacji sieci web za pośrednictwem portalu Azure</span><span class="sxs-lookup"><span data-stu-id="33d80-103">Customize web application firewall rules through the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="33d80-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="33d80-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="33d80-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="33d80-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="33d80-106">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="33d80-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="33d80-107">Brama aplikacji w usłudze Azure zapory aplikacji sieci web (WAF) zapewnia ochronę dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="33d80-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="33d80-108">Te zabezpieczenia są dostarczane przez Otwórz sieci Web aplikacji zabezpieczeń projektu (OWASP) podstawowe reguły Ustaw (CRS).</span><span class="sxs-lookup"><span data-stu-id="33d80-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="33d80-109">Niektóre zasady mogą spowodować fałszywych alarmów i zablokowanie ruchu prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="33d80-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="33d80-110">Z tego powodu bramy aplikacji oferuje możliwość dostosowywania grup reguł i zasad.</span><span class="sxs-lookup"><span data-stu-id="33d80-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="33d80-111">Aby uzyskać więcej informacji na określonej reguły grup i reguł, zobacz [listy grup reguł CRS zapory aplikacji sieci web i reguł](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="33d80-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="33d80-112">Jeśli bramy aplikacji nie używa warstwy zapory aplikacji sieci Web, opcja uaktualnienia brama aplikacji w warstwie zapory aplikacji sieci Web zostanie wyświetlony w okienku po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="33d80-112">If your application gateway is not using the WAF tier, the option to upgrade the application gateway to the WAF tier appears in the right pane.</span></span> 

![Włączanie zapory aplikacji sieci Web][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="33d80-114">Widok grup reguł i zasad</span><span class="sxs-lookup"><span data-stu-id="33d80-114">View rule groups and rules</span></span>

<span data-ttu-id="33d80-115">**Aby wyświetlić grupy reguł i zasad**</span><span class="sxs-lookup"><span data-stu-id="33d80-115">**To view rule groups and rules**</span></span>
   1. <span data-ttu-id="33d80-116">Przejdź na bramie aplikacji, a następnie wybierz **zapory aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="33d80-116">Browse to the application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="33d80-117">Wybierz **reguły zaawansowanej konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="33d80-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="33d80-118">Ten widok przedstawia tabeli na stronie grupy reguł podaną w zestawie reguł wybrany.</span><span class="sxs-lookup"><span data-stu-id="33d80-118">This view shows a table on the page of all the rule groups provided with the chosen rule set.</span></span> <span data-ttu-id="33d80-119">Zaznaczono wszystkie pola wyboru reguły.</span><span class="sxs-lookup"><span data-stu-id="33d80-119">All of the rule's check boxes are selected.</span></span>

![Konfigurowanie reguł wyłączone][1]

## <a name="search-for-rules-to-disable"></a><span data-ttu-id="33d80-121">Wyszukaj regułę do wyłączenia</span><span class="sxs-lookup"><span data-stu-id="33d80-121">Search for rules to disable</span></span>

<span data-ttu-id="33d80-122">**Aplikacja, ustawienia zapory w sieci Web** bloku umożliwia filtrowanie reguł za pomocą funkcji wyszukiwania tekstu.</span><span class="sxs-lookup"><span data-stu-id="33d80-122">The **Web application firewall settings** blade provides the capability to filter the rules through a text search.</span></span> <span data-ttu-id="33d80-123">Wynik wyświetla tylko grupy reguł i reguł, które zawierają tekst, który wyszukiwany.</span><span class="sxs-lookup"><span data-stu-id="33d80-123">The result displays only the rule groups and rules that contain the text you searched for.</span></span>

![Wyszukaj zasady][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="33d80-125">Wyłącz zasady grupy i zasady</span><span class="sxs-lookup"><span data-stu-id="33d80-125">Disable rule groups and rules</span></span>

<span data-ttu-id="33d80-126">Gdy sieci są wyłączenie reguł, można wyłączyć reguły całej grupy lub określone zasady w co najmniej jedną grupę reguł.</span><span class="sxs-lookup"><span data-stu-id="33d80-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="33d80-127">**Aby wyłączyć grupy reguł lub określone zasady**</span><span class="sxs-lookup"><span data-stu-id="33d80-127">**To disable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="33d80-128">Wyszukiwanie reguły lub grupy reguł, które mają zostać wyłączone.</span><span class="sxs-lookup"><span data-stu-id="33d80-128">Search for the rules or rule groups that you want to disable.</span></span>
   2. <span data-ttu-id="33d80-129">Usuń zaznaczenie pola wyboru dla reguł, które mają zostać wyłączone.</span><span class="sxs-lookup"><span data-stu-id="33d80-129">Clear the check boxes for the rules that you want to disable.</span></span> 
   2. <span data-ttu-id="33d80-130">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="33d80-130">Select **Save**.</span></span> 

![Zapisz zmiany][3]

## <a name="next-steps"></a><span data-ttu-id="33d80-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33d80-132">Next steps</span></span>

<span data-ttu-id="33d80-133">Po skonfigurowaniu reguł wyłączonych można poznać sposoby wyświetlania dzienników zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="33d80-133">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="33d80-134">Aby uzyskać więcej informacji, zobacz [diagnostyki bramy aplikacji](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="33d80-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
