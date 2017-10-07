---
title: "aaaFind następnego przeskoku z Azure sieci obserwatora następnego przeskoku - REST | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak i można znaleźć jakie hello następnego przeskoku typu jest adres ip przy użyciu następnego przeskoku hello interfejsu API REST Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="215be-103">Dowiedz się hello Typ następnego przeskoku jest przy użyciu możliwości następnego przeskoku hello w obserwatora sieciowego Azure przy użyciu interfejsu API REST Azure</span><span class="sxs-lookup"><span data-stu-id="215be-103">Find out what hello next hop type is using hello Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="215be-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="215be-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="215be-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="215be-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="215be-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="215be-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="215be-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="215be-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="215be-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="215be-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="215be-109">Następny przeskok jest funkcją obserwatora sieciowego, która umożliwia określenie hello uzyskać typ następnego przeskoku hello i adresu IP na podstawie określonej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="215be-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="215be-110">Ta funkcja jest przydatna przy określaniu, jeśli ruchu wychodzącego maszyny wirtualnej są przesyłane za pośrednictwem bramy, Internetu lub sieci wirtualne tooget tooits docelowego.</span><span class="sxs-lookup"><span data-stu-id="215be-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="215be-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="215be-111">Before you begin</span></span>

<span data-ttu-id="215be-112">ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="215be-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="215be-113">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="215be-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="215be-114">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="215be-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="215be-115">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="215be-115">Scenario</span></span>

<span data-ttu-id="215be-116">Scenariusz Hello omówione w tym artykule używa następnego przeskoku, funkcja obserwatora sieciowego, który znajduje się typ następnego przeskoku hello i adres IP dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="215be-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="215be-117">odwiedź stronę toolearn więcej informacji na temat następnego przeskoku [następnego przeskoku omówienie](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="215be-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="215be-118">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="215be-118">In this scenario, you will:</span></span>

* <span data-ttu-id="215be-119">Pobrać hello następnego skoku dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="215be-119">Retrieve hello next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="215be-120">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="215be-120">Log in with ARMClient</span></span>

<span data-ttu-id="215be-121">Zaloguj się za tooarmclient przy użyciu poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="215be-121">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="215be-122">Pobieranie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="215be-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="215be-123">Uruchom maszynę wirtualną powitania po tooreturn skryptu.</span><span class="sxs-lookup"><span data-stu-id="215be-123">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="215be-124">Te informacje są potrzebne do uruchomienia następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="215be-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="215be-125">Hello następującego kodu wymaga wartości dla hello następujące zmienne:</span><span class="sxs-lookup"><span data-stu-id="215be-125">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="215be-126">**Identyfikator subskrypcji** — Witaj toouse identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="215be-126">**subscriptionId** - hello subscription Id toouse.</span></span>
- <span data-ttu-id="215be-127">**resourceGroupName** — Witaj Nazwa grupy zasobów, która zawiera maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="215be-127">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="215be-128">Z danych wyjściowych poniżej hello, identyfikator hello maszyny wirtualnej hello jest używany w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="215be-128">From hello following output, hello id of hello virtual machine is used in hello following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a><span data-ttu-id="215be-129">Pobierz następnego skoku</span><span class="sxs-lookup"><span data-stu-id="215be-129">Get Next Hop</span></span>

<span data-ttu-id="215be-130">Po utworzeniu nagłówek autoryzacji hello hello następnego przeskoku z maszyny wirtualnej może zostać pobrany.</span><span class="sxs-lookup"><span data-stu-id="215be-130">Once hello authorization header is created, hello next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="215be-131">Witaj następujące wartości należy zastąpić dla toowork przykładowy kod hello.</span><span class="sxs-lookup"><span data-stu-id="215be-131">hello following values must be replaced for hello code example toowork.</span></span>

> [!Important]
> <span data-ttu-id="215be-132">Dla interfejsu API REST obserwatora sieciowego wywołania hello Nazwa grupy zasobów w żądaniu hello się, że identyfikator URI jest hello grupę zasobów, która zawiera hello obserwatora sieciowego nie zasoby hello czynności diagnostyczne hello są wykonywane na.</span><span class="sxs-lookup"><span data-stu-id="215be-132">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> <span data-ttu-id="215be-133">Następnego przeskoku wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona toorun.</span><span class="sxs-lookup"><span data-stu-id="215be-133">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="results"></a><span data-ttu-id="215be-134">Wyniki</span><span class="sxs-lookup"><span data-stu-id="215be-134">Results</span></span>

<span data-ttu-id="215be-135">Witaj poniższy fragment kodu jest przykład danych wyjściowych hello odebrane.</span><span class="sxs-lookup"><span data-stu-id="215be-135">hello following snippet is an example of hello output received.</span></span> <span data-ttu-id="215be-136">Witaj wyniki zawierają hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="215be-136">hello results contain hello following values:</span></span>

* <span data-ttu-id="215be-137">**Typ następnego przeskoku** — ta wartość jest jednym z hello następujące wartości: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway lub None.</span><span class="sxs-lookup"><span data-stu-id="215be-137">**nextHopType** - This value is one of hello following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="215be-138">**adres IP następnego przeskoku** — Witaj adres IP następnego przeskoku hello.</span><span class="sxs-lookup"><span data-stu-id="215be-138">**nextHopIpAddress** - hello IP address of hello next hop.</span></span>
* <span data-ttu-id="215be-139">**routeTableId** — wartość hello jest albo identyfikatorem uri dla tabeli tras hello skojarzone z trasą hello, lub zdefiniowanej przez użytkownika nie trasy jest wartość zdefiniowanych hello *trasa systemowa* jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="215be-139">**routeTableId** - hello value is either a uri for hello route table associated with hello route, or if no user-defined route is defined hello value of *System Route* is returned.</span></span>

<span data-ttu-id="215be-140">Oto Hello hello wyniki w formacie json.</span><span class="sxs-lookup"><span data-stu-id="215be-140">hello following are hello results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="215be-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="215be-141">Next steps</span></span>

<span data-ttu-id="215be-142">Po toofind stanie się hello następnego skoku dla maszyny wirtualnej można wyświetlić hello bezpieczeństwa zasobów sieciowych, odwiedzając [widok zabezpieczeń — omówienie](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="215be-142">Once you have been able toofind out hello next hop for a virtual machine, you can view hello security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














