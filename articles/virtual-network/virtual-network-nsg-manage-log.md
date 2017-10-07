---
title: aaaMonitor operacje, zdarzenia i liczniki dla grup NSG | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooenable liczników, zdarzeń i operacyjne rejestrowania dla grupy NSG"
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
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="a9296-103">Usługa Log Analytics dla sieciowych grup zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="a9296-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="a9296-104">Możesz włączyć następujące kategorie dzienników diagnostycznych dla grup NSG hello:</span><span class="sxs-lookup"><span data-stu-id="a9296-104">You can enable hello following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="a9296-105">**Zdarzenie:** zawiera wpisy, dla których NSG reguły są stosowane tooVMs i wystąpienia ról na podstawie adresu MAC.</span><span class="sxs-lookup"><span data-stu-id="a9296-105">**Event:** Contains entries for which NSG rules are applied tooVMs and instance roles based on MAC address.</span></span> <span data-ttu-id="a9296-106">Stan Hello te reguły są gromadzone co 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="a9296-106">hello status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="a9296-107">**Licznik reguł:** zawiera wpisy dla ile razy każda grupa NSG do reguły jest stosowane toodeny lub zezwolić na ruch.</span><span class="sxs-lookup"><span data-stu-id="a9296-107">**Rule counter:** Contains entries for how many times each NSG rule is applied toodeny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="a9296-108">Dzienniki diagnostyczne są dostępne tylko dla grup NSG wdrożone za pośrednictwem modelu wdrażania usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="a9296-108">Diagnostic logs are only available for NSGs deployed through hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="a9296-109">Nie można włączyć rejestrowania diagnostycznego w celu grup NSG wdrożone za pośrednictwem hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="a9296-109">You cannot enable diagnostic logging for NSGs deployed through hello classic deployment model.</span></span> <span data-ttu-id="a9296-110">W celu lepszego zrozumienia hello dwóch modeli, odwołanie hello [modele wdrażania Azure opis](../resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a9296-110">For a better understanding of hello two models, reference hello [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="a9296-111">Rejestrowanie aktywności (wcześniej znane jako inspekcji lub operacyjne dzienniki) jest domyślnie włączone dla grup NSG, został utworzony za pomocą obu modelu wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="a9296-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="a9296-112">toodetermine, jakie operacje zostały zakończone na grup NSG w hello dziennik aktywności, Wyszukaj wpisy zawierające hello następujące typy zasobów:</span><span class="sxs-lookup"><span data-stu-id="a9296-112">toodetermine which operations were completed on NSGs in hello activity log, look for entries that contain hello following resource types:</span></span> 

- <span data-ttu-id="a9296-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="a9296-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="a9296-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="a9296-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="a9296-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="a9296-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="a9296-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="a9296-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="a9296-117">Witaj odczytu [omówienie hello dziennika aktywności platformy Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) toolearn artykułu więcej o Dzienniki aktywności.</span><span class="sxs-lookup"><span data-stu-id="a9296-117">Read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article toolearn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="a9296-118">Włączanie rejestrowania diagnostycznego</span><span class="sxs-lookup"><span data-stu-id="a9296-118">Enable diagnostic logging</span></span>

<span data-ttu-id="a9296-119">Należy włączyć rejestrowanie diagnostyczne *każdego* NSG ma toocollect danych.</span><span class="sxs-lookup"><span data-stu-id="a9296-119">Diagnostic logging must be enabled for *each* NSG you want toocollect data for.</span></span> <span data-ttu-id="a9296-120">Witaj [Omówienie programu Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) wyjaśniono wysyłania dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="a9296-120">hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="a9296-121">Jeśli nie masz istniejącej grupy NSG, pełną hello etapami hello [Utwórz grupę zabezpieczeń sieci](virtual-networks-create-nsg-arm-pportal.md) toocreate artykułu, jeden.</span><span class="sxs-lookup"><span data-stu-id="a9296-121">If you don't have an existing NSG, complete hello steps in hello [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article toocreate one.</span></span> <span data-ttu-id="a9296-122">Można włączyć NSG przy użyciu dowolnej z następujących metod hello diagnostyczne:</span><span class="sxs-lookup"><span data-stu-id="a9296-122">You can enable NSG diagnostic logging using any of hello following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="a9296-123">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a9296-123">Azure portal</span></span>

<span data-ttu-id="a9296-124">toouse hello portalu tooenable rejestrowania, logowanie toohello [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9296-124">toouse hello portal tooenable logging, login toohello [portal](https://portal.azure.com).</span></span> <span data-ttu-id="a9296-125">Kliknij przycisk **więcej usług**, wpisz *sieciowej grupy zabezpieczeń*.</span><span class="sxs-lookup"><span data-stu-id="a9296-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="a9296-126">Wybierz hello NSG ma tooenable rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="a9296-126">Select hello NSG you want tooenable logging for.</span></span> <span data-ttu-id="a9296-127">Wykonaj instrukcje hello zasobów z systemem innym niż obliczeń w hello [Włączanie dzienników diagnostycznych w portalu hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a9296-127">Follow hello instructions for non-compute resources in hello [Enable diagnostic logs in hello portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="a9296-128">Wybierz **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, lub oba rodzaje dzienników.</span><span class="sxs-lookup"><span data-stu-id="a9296-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="a9296-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9296-129">PowerShell</span></span>

<span data-ttu-id="a9296-130">toouse tooenable PowerShell rejestrowanie, wykonaj te instrukcje hello hello [Włączanie dzienników diagnostycznych za pomocą programu PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a9296-130">toouse PowerShell tooenable logging, follow hello instructions in hello [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="a9296-131">Sprawdź następujące informacje przed wprowadzeniem polecenie z artykułu hello hello:</span><span class="sxs-lookup"><span data-stu-id="a9296-131">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="a9296-132">Można określić hello toouse wartość dla hello `-ResourceId` parametru zastępując powitania po [tekst], zgodnie z potrzebami, następnie wpisując polecenie hello `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="a9296-132">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="a9296-133">Hello identyfikator dane wyjściowe polecenia hello wygląda podobnie zbyt*/subscriptions/ [Nazwa subskrypcji Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="a9296-133">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="a9296-134">Tylko dane toocollect z kategorii dziennika należy dodać `-Categories [category]` toohello koniec polecenia hello w artykule hello, gdzie kategorii jest *NetworkSecurityGroupEvent* lub *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="a9296-134">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="a9296-135">Jeśli nie używasz hello `-Categories` parametru, zbierania danych jest włączona dla dziennika kategorii.</span><span class="sxs-lookup"><span data-stu-id="a9296-135">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="a9296-136">Azure interfejsu wiersza polecenia (CLI)</span><span class="sxs-lookup"><span data-stu-id="a9296-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="a9296-137">toouse hello rejestrowania tooenable interfejsu wiersza polecenia, wykonaj te instrukcje hello hello [Włączanie dzienników diagnostycznych za pomocą interfejsu wiersza polecenia](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a9296-137">toouse hello CLI tooenable logging, follow hello instructions in hello [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="a9296-138">Sprawdź następujące informacje przed wprowadzeniem polecenie z artykułu hello hello:</span><span class="sxs-lookup"><span data-stu-id="a9296-138">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="a9296-139">Można określić hello toouse wartość dla hello `-ResourceId` parametru zastępując powitania po [tekst], zgodnie z potrzebami, następnie wpisując polecenie hello `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="a9296-139">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="a9296-140">Hello identyfikator dane wyjściowe polecenia hello wygląda podobnie zbyt*/subscriptions/ [Nazwa subskrypcji Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="a9296-140">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="a9296-141">Tylko dane toocollect z kategorii dziennika należy dodać `-Categories [category]` toohello koniec polecenia hello w artykule hello, gdzie kategorii jest *NetworkSecurityGroupEvent* lub *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="a9296-141">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="a9296-142">Jeśli nie używasz hello `-Categories` parametru, zbierania danych jest włączona dla dziennika kategorii.</span><span class="sxs-lookup"><span data-stu-id="a9296-142">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="a9296-143">Zarejestrowane dane</span><span class="sxs-lookup"><span data-stu-id="a9296-143">Logged data</span></span>

<span data-ttu-id="a9296-144">Dane w formacie JSON jest przeznaczony dla obu dzienników.</span><span class="sxs-lookup"><span data-stu-id="a9296-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="a9296-145">określone dane Hello zapisywane dla każdego typu dziennika ma na liście hello następujące sekcje:</span><span class="sxs-lookup"><span data-stu-id="a9296-145">hello specific data written for each log type is listed in hello following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="a9296-146">Dziennik zdarzeń</span><span class="sxs-lookup"><span data-stu-id="a9296-146">Event log</span></span>
<span data-ttu-id="a9296-147">Ten dziennik zawiera informacje o NSG, które zasady są stosowane tooVMs i wystąpień roli usługi, na podstawie adresu MAC w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a9296-147">This log contains information about which NSG rules are applied tooVMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="a9296-148">następujące przykładowe dane Hello jest rejestrowane dla każdego zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="a9296-148">hello following example data is logged for each event:</span></span>

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

### <a name="rule-counter-log"></a><span data-ttu-id="a9296-149">Zasada dziennika liczników</span><span class="sxs-lookup"><span data-stu-id="a9296-149">Rule counter log</span></span>

<span data-ttu-id="a9296-150">Ten dziennik zawiera informacje o każdym tooresources reguły.</span><span class="sxs-lookup"><span data-stu-id="a9296-150">This log contains information about each rule applied tooresources.</span></span> <span data-ttu-id="a9296-151">Witaj przykład rejestrowane są następujące dane każdym razem, gdy reguła jest stosowana:</span><span class="sxs-lookup"><span data-stu-id="a9296-151">hello following example data is logged each time a rule is applied:</span></span>

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

## <a name="view-and-analyze-logs"></a><span data-ttu-id="a9296-152">Wyświetlanie i analizowanie dzienników</span><span class="sxs-lookup"><span data-stu-id="a9296-152">View and analyze logs</span></span>

<span data-ttu-id="a9296-153">toolearn, w jaki sposób dane, rejestrować działania tooview odczytu hello [omówienie hello dziennika aktywności platformy Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a9296-153">toolearn how tooview activity log data, read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="a9296-154">toolearn, jak dane, rejestrować Diagnostyka tooview odczytu hello [Omówienie programu Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a9296-154">toolearn how tooview diagnostic log data, read hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="a9296-155">Po wysłaniu diagnostyki danych tooLog Analytics można użyć hello [analytics sieciowej grupy zabezpieczeń usługi Azure](../log-analytics/log-analytics-azure-networking-analytics.md) rozszerzone szczegółowe informacje o rozwiązania do zarządzania (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="a9296-155">If you send diagnostics data tooLog Analytics, you can use hello [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
