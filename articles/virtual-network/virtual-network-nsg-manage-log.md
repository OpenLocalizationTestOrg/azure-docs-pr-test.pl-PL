---
title: "Monitorowanie działań, zdarzenia i liczniki dla grup NSG | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak włączyć operacyjne rejestrowanie dla grup NSG, zdarzenia i liczniki"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: 552f37dd704de25159bc0f0ad34fdae9ed8b73f5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="c17f8-103">Usługa Log Analytics dla sieciowych grup zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c17f8-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="c17f8-104">Grupy NSG można włączyć następujące kategorie dzienników diagnostycznych:</span><span class="sxs-lookup"><span data-stu-id="c17f8-104">You can enable the following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="c17f8-105">**Zdarzenie:** zawiera wpisy, dla których NSG reguły są stosowane do maszyn wirtualnych i wystąpień ról na podstawie adresu MAC.</span><span class="sxs-lookup"><span data-stu-id="c17f8-105">**Event:** Contains entries for which NSG rules are applied to VMs and instance roles based on MAC address.</span></span> <span data-ttu-id="c17f8-106">Stan zasady te są gromadzone co 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="c17f8-106">The status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="c17f8-107">**Licznik reguł:** reguł zawiera wpisy dla ile razy każda grupa NSG jest stosowana do odmowy lub zezwolić na ruch.</span><span class="sxs-lookup"><span data-stu-id="c17f8-107">**Rule counter:** Contains entries for how many times each NSG rule is applied to deny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="c17f8-108">Dzienniki diagnostyczne są dostępne tylko dla grup NSG wdrożone za pośrednictwem modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c17f8-108">Diagnostic logs are only available for NSGs deployed through the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="c17f8-109">Nie można włączyć rejestrowania diagnostycznego w celu grup NSG wdrożone za pośrednictwem klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c17f8-109">You cannot enable diagnostic logging for NSGs deployed through the classic deployment model.</span></span> <span data-ttu-id="c17f8-110">W celu lepszego zrozumienia dwóch modeli, odwołanie [modele wdrażania Azure opis](../resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c17f8-110">For a better understanding of the two models, reference the [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="c17f8-111">Rejestrowanie aktywności (wcześniej znane jako inspekcji lub operacyjne dzienniki) jest domyślnie włączone dla grup NSG, został utworzony za pomocą obu modelu wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="c17f8-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="c17f8-112">Aby ustalić, jakie operacje zostały zakończone na grup NSG w dzienniku aktywności, Wyszukaj wpisy zawierające następujących zasobów:</span><span class="sxs-lookup"><span data-stu-id="c17f8-112">To determine which operations were completed on NSGs in the activity log, look for entries that contain the following resource types:</span></span> 

- <span data-ttu-id="c17f8-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="c17f8-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="c17f8-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="c17f8-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="c17f8-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="c17f8-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="c17f8-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="c17f8-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="c17f8-117">Odczyt [Omówienie dziennika aktywności platformy Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) artykuł, aby dowiedzieć się więcej o Dzienniki aktywności.</span><span class="sxs-lookup"><span data-stu-id="c17f8-117">Read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article to learn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="c17f8-118">Włączanie rejestrowania diagnostycznego</span><span class="sxs-lookup"><span data-stu-id="c17f8-118">Enable diagnostic logging</span></span>

<span data-ttu-id="c17f8-119">Należy włączyć rejestrowanie diagnostyczne *każdego* NSG, które mają być zbierane dane.</span><span class="sxs-lookup"><span data-stu-id="c17f8-119">Diagnostic logging must be enabled for *each* NSG you want to collect data for.</span></span> <span data-ttu-id="c17f8-120">[Omówienie programu Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) wyjaśniono wysyłania dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="c17f8-120">The [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="c17f8-121">Jeśli nie masz istniejącej grupy NSG, wykonaj kroki [Utwórz grupę zabezpieczeń sieci](virtual-networks-create-nsg-arm-pportal.md) artykuł, aby go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="c17f8-121">If you don't have an existing NSG, complete the steps in the [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article to create one.</span></span> <span data-ttu-id="c17f8-122">Można włączyć NSG diagnostycznych rejestrowanie przy użyciu dowolnej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="c17f8-122">You can enable NSG diagnostic logging using any of the following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="c17f8-123">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c17f8-123">Azure portal</span></span>

<span data-ttu-id="c17f8-124">Aby włączyć rejestrowanie, zaloguj się za pomocą portalu [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c17f8-124">To use the portal to enable logging, login to the [portal](https://portal.azure.com).</span></span> <span data-ttu-id="c17f8-125">Kliknij przycisk **więcej usług**, wpisz *sieciowej grupy zabezpieczeń*.</span><span class="sxs-lookup"><span data-stu-id="c17f8-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="c17f8-126">Wybierz grupy NSG, aby włączyć rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="c17f8-126">Select the NSG you want to enable logging for.</span></span> <span data-ttu-id="c17f8-127">Postępuj zgodnie z instrukcjami dla zasobów obliczeniowych z systemem innym niż w [Włączanie dzienników diagnostycznych w portalu](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c17f8-127">Follow the instructions for non-compute resources in the [Enable diagnostic logs in the portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="c17f8-128">Wybierz **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, lub oba rodzaje dzienników.</span><span class="sxs-lookup"><span data-stu-id="c17f8-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="c17f8-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c17f8-129">PowerShell</span></span>

<span data-ttu-id="c17f8-130">Aby włączyć rejestrowanie za pomocą programu PowerShell, postępuj zgodnie z instrukcjami [Włączanie dzienników diagnostycznych za pomocą programu PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c17f8-130">To use PowerShell to enable logging, follow the instructions in the [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="c17f8-131">Oceny przed wprowadzeniem polecenia z tego artykułu następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="c17f8-131">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="c17f8-132">Można określić wartość dla `-ResourceId` parametru zastępując następujące [tekst], odpowiednio, następnie wpisując polecenie `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="c17f8-132">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="c17f8-133">Identyfikator dane wyjściowe polecenia wygląda podobnie do */subscriptions/ [Nazwa subskrypcji Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="c17f8-133">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="c17f8-134">Jeśli chcesz zbierać dane z kategorii dziennika Dodaj `-Categories [category]` na końcu polecenia w artykule, w którym kategorii jest *NetworkSecurityGroupEvent* lub *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="c17f8-134">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="c17f8-135">Jeśli nie używasz `-Categories` parametru, zbierania danych jest włączona dla dziennika kategorii.</span><span class="sxs-lookup"><span data-stu-id="c17f8-135">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="c17f8-136">Azure interfejsu wiersza polecenia (CLI)</span><span class="sxs-lookup"><span data-stu-id="c17f8-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="c17f8-137">Aby korzystać z interfejsu wiersza polecenia, aby włączyć rejestrowanie, postępuj zgodnie z instrukcjami [Włączanie dzienników diagnostycznych za pomocą interfejsu wiersza polecenia](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c17f8-137">To use the CLI to enable logging, follow the instructions in the [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="c17f8-138">Oceny przed wprowadzeniem polecenia z tego artykułu następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="c17f8-138">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="c17f8-139">Można określić wartość dla `-ResourceId` parametru zastępując następujące [tekst], odpowiednio, następnie wpisując polecenie `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="c17f8-139">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="c17f8-140">Identyfikator dane wyjściowe polecenia wygląda podobnie do */subscriptions/ [Nazwa subskrypcji Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="c17f8-140">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="c17f8-141">Jeśli chcesz zbierać dane z kategorii dziennika Dodaj `-Categories [category]` na końcu polecenia w artykule, w którym kategorii jest *NetworkSecurityGroupEvent* lub *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="c17f8-141">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="c17f8-142">Jeśli nie używasz `-Categories` parametru, zbierania danych jest włączona dla dziennika kategorii.</span><span class="sxs-lookup"><span data-stu-id="c17f8-142">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="c17f8-143">Zarejestrowane dane</span><span class="sxs-lookup"><span data-stu-id="c17f8-143">Logged data</span></span>

<span data-ttu-id="c17f8-144">Dane w formacie JSON jest przeznaczony dla obu dzienników.</span><span class="sxs-lookup"><span data-stu-id="c17f8-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="c17f8-145">Określone dane, które są przeznaczone dla każdego typu dziennika znajduje się w następujących sekcjach:</span><span class="sxs-lookup"><span data-stu-id="c17f8-145">The specific data written for each log type is listed in the following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="c17f8-146">Dziennik zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c17f8-146">Event log</span></span>
<span data-ttu-id="c17f8-147">Ten dziennik zawiera informacje o NSG, które zasady są stosowane do maszyn wirtualnych i wystąpień roli usługi, na podstawie adresu MAC w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c17f8-147">This log contains information about which NSG rules are applied to VMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="c17f8-148">Rejestrowane są następujące dane przykładowe dla każdego zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="c17f8-148">The following example data is logged for each event:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a><span data-ttu-id="c17f8-149">Zasada dziennika liczników</span><span class="sxs-lookup"><span data-stu-id="c17f8-149">Rule counter log</span></span>

<span data-ttu-id="c17f8-150">Ten dziennik zawiera informacje o poszczególnych regułach stosowane do zasobów.</span><span class="sxs-lookup"><span data-stu-id="c17f8-150">This log contains information about each rule applied to resources.</span></span> <span data-ttu-id="c17f8-151">Następujące przykładowe dane jest rejestrowane za każdym razem, których dotyczy reguła:</span><span class="sxs-lookup"><span data-stu-id="c17f8-151">The following example data is logged each time a rule is applied:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a><span data-ttu-id="c17f8-152">Wyświetlanie i analizowanie dzienników</span><span class="sxs-lookup"><span data-stu-id="c17f8-152">View and analyze logs</span></span>

<span data-ttu-id="c17f8-153">Aby dowiedzieć się, jak wyświetlać dane dziennika aktywności, przeczytaj [Omówienie dziennika aktywności platformy Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c17f8-153">To learn how to view activity log data, read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="c17f8-154">Aby dowiedzieć się jak wyświetlać dane dziennika diagnostycznego, przeczytaj [Omówienie programu Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c17f8-154">To learn how to view diagnostic log data, read the [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="c17f8-155">Po wysłaniu danych diagnostycznych do analizy dzienników można użyć [analytics sieciowej grupy zabezpieczeń usługi Azure](../log-analytics/log-analytics-azure-networking-analytics.md) rozszerzone szczegółowe informacje o rozwiązania do zarządzania (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="c17f8-155">If you send diagnostics data to Log Analytics, you can use the [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
