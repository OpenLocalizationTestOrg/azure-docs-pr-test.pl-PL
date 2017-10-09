---
title: "ruch aaaVerify Azure sieci obserwatora IP przepływ weryfikacji - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocheck Jeśli tooor ruch z maszyny wirtualnej jest dozwolony lub odrzucany, przy użyciu wiersza polecenia platformy Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="a8a80-103">Sprawdź, czy ruch jest dozwolony lub z maszyny Wirtualnej z przepływem Sprawdź IP zabronione tooor a składnik Azure obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="a8a80-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a8a80-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a8a80-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="a8a80-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8a80-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="a8a80-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="a8a80-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="a8a80-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="a8a80-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="a8a80-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="a8a80-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="a8a80-109">Przepływ IP Sprawdź jest funkcją obserwatora sieciowego, który umożliwia tooverify Jeśli ruch jest dozwolony tooor z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8a80-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="a8a80-110">Ten scenariusz jest przydatne tooget bieżący stan czy maszynę wirtualną można rozmawiać tooan zasobu zewnętrznego i wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a8a80-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="a8a80-111">Sprawdź przepływ IP można tooverify używane w regułach grupy zabezpieczeń sieci (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="a8a80-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="a8a80-112">Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź tooensure ruchu, które mają zablokowany jest prawidłowo blokowane przez hello NSG.</span><span class="sxs-lookup"><span data-stu-id="a8a80-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="a8a80-113">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="a8a80-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a8a80-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="a8a80-114">Before you begin</span></span>

<span data-ttu-id="a8a80-115">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego lub istniejącego wystąpienia obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="a8a80-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="a8a80-116">Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.</span><span class="sxs-lookup"><span data-stu-id="a8a80-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a8a80-117">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="a8a80-117">Scenario</span></span>

<span data-ttu-id="a8a80-118">W tym scenariuszu Sprawdź przepływ IP tooverify Jeśli maszynę wirtualną można, komunikować tooa będzie znany adres IP usługi Bing.</span><span class="sxs-lookup"><span data-stu-id="a8a80-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="a8a80-119">Ruch hello jest niedozwolone, zwraca hello reguły zabezpieczeń, która odrzuciła ten ruch.</span><span class="sxs-lookup"><span data-stu-id="a8a80-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="a8a80-120">toolearn więcej informacji na temat przepływu Sprawdź IP, odwiedź stronę [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a8a80-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="a8a80-121">Uzyskiwanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a8a80-121">Get a VM</span></span>

<span data-ttu-id="a8a80-122">Przepływ IP Sprawdź testy tooor ruch z adresu IP na tooor maszyny wirtualnej, z zdalnego miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="a8a80-122">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="a8a80-123">Identyfikator maszyny wirtualnej jest wymagany dla polecenia cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="a8a80-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="a8a80-124">Jeśli znasz już identyfikator hello hello toouse maszyny wirtualnej, można pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="a8a80-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a><span data-ttu-id="a8a80-125">Pobierz hello kart Sieciowych</span><span class="sxs-lookup"><span data-stu-id="a8a80-125">Get hello NICS</span></span>

<span data-ttu-id="a8a80-126">adres IP karty Sieciowej na maszynie wirtualnej hello Hello jest potrzebne w tym przykładzie Pobieramy hello karty interfejsu sieciowego na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8a80-126">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="a8a80-127">Jeśli znasz już IP hello adresu, który ma tootest na maszynie wirtualnej hello, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="a8a80-127">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="a8a80-128">Sprawdź uruchomienia przepływu IP</span><span class="sxs-lookup"><span data-stu-id="a8a80-128">Run IP flow verify</span></span>

<span data-ttu-id="a8a80-129">Teraz, gdy mamy informacji hello potrzebne toorun hello polecenia cmdlet, przeprowadzana hello `network watcher ip-flow-verify` ruchu hello tootest polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a8a80-129">Now that we have hello information needed toorun hello cmdlet, we run hello `network watcher ip-flow-verify` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="a8a80-130">W tym przykładzie używamy hello pierwszego adresu IP na powitania pierwszej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="a8a80-130">In this example, we are using hello first IP address on hello first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> <span data-ttu-id="a8a80-131">Przepływ IP Sprawdź wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona toorun.</span><span class="sxs-lookup"><span data-stu-id="a8a80-131">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="a8a80-132">Przejrzyj wyniki</span><span class="sxs-lookup"><span data-stu-id="a8a80-132">Review Results</span></span>

<span data-ttu-id="a8a80-133">Po uruchomieniu `network watcher ip-flow-verify` hello wyniki są zwracane, hello poniższym przykładzie jest hello wyniki zwrócone z hello poprzedzających krok.</span><span class="sxs-lookup"><span data-stu-id="a8a80-133">After running `network watcher ip-flow-verify` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="a8a80-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a8a80-134">Next steps</span></span>

<span data-ttu-id="a8a80-135">Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które są zdefiniowane w dół.</span><span class="sxs-lookup"><span data-stu-id="a8a80-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="a8a80-136">Dowiedz się tooaudit ustawienia grupy NSG, odwiedzając [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a8a80-136">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
