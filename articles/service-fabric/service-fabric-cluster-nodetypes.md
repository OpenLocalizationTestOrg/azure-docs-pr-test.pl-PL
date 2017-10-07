---
title: "aaaService sieci szkieletowej typy węzła i zestawy skalowania maszyny Wirtualnej | Dokumentacja firmy Microsoft"
description: "Opisuje powiązań zestawów skali tooVM typy węzłów sieci szkieletowej usług oraz sposób tooremote łączenia tooa wystąpienia zestawu skali maszyny Wirtualnej lub węzła klastra."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="0c398-103">Hello relacji między typami węzła sieci szkieletowej usług i zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0c398-103">hello relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="0c398-104">Zestawy skalowania maszyny wirtualnej są zasobami rozwiązań usługi obliczenia Azure można użyć toodeploy i zarządzanie kolekcją jako zestaw maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0c398-104">Virtual Machine Scale Sets are an Azure Compute resource you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="0c398-105">Każdy typ węzła który jest zdefiniowany w klastrze usługi sieć szkieletowa jest skonfigurowany jako osobne zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c398-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="0c398-106">Każdy typ węzła następnie można skalować w lub w dół niezależnie, mają różne zestawy otwartych portów i może mieć metryki pojemności różnych.</span><span class="sxs-lookup"><span data-stu-id="0c398-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="0c398-107">powitania po zrzut ekranu przedstawia klastra, która ma dwa typy węzłów: frontonu i wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0c398-107">hello following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="0c398-108">Każdy typ węzła ma pięć węzłów.</span><span class="sxs-lookup"><span data-stu-id="0c398-108">Each node type has five nodes each.</span></span>

![Zrzut ekranu przedstawiający klastra, która ma dwa typy węzłów][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a><span data-ttu-id="0c398-110">Mapowanie toonodes wystąpienia zestawu skali maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0c398-110">Mapping VM Scale Set instances toonodes</span></span>
<span data-ttu-id="0c398-111">Jak widać powyżej, wystąpienia zestawu skali maszyny Wirtualnej hello Uruchom z wystąpienia 0, a następnie rośnie.</span><span class="sxs-lookup"><span data-stu-id="0c398-111">As you can see above, hello VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="0c398-112">numerowanie Hello znajduje odzwierciedlenie w nazwach hello.</span><span class="sxs-lookup"><span data-stu-id="0c398-112">hello numbering is reflected in hello names.</span></span> <span data-ttu-id="0c398-113">Na przykład BackEnd_0 jest wystąpienie 0 hello zestawu skali maszyny Wirtualnej w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="0c398-113">For example, BackEnd_0 is instance 0 of hello BackEnd VM Scale Set.</span></span> <span data-ttu-id="0c398-114">Tego konkretnego zestawu skali maszyny Wirtualnej ma pięć wystąpień, o nazwie BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 i BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="0c398-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="0c398-115">Skalowanie w górę zestawu skali maszyny Wirtualnej jest tworzone nowe wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="0c398-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="0c398-116">Hello nowego zestawu skali maszyny Wirtualnej nazwy wystąpienia będzie zazwyczaj nazwa zestawu skali maszyny Wirtualnej hello + hello dalej liczby wystąpień.</span><span class="sxs-lookup"><span data-stu-id="0c398-116">hello new VM Scale Set instance name will typically be hello VM Scale Set name + hello next instance number.</span></span> <span data-ttu-id="0c398-117">W naszym przykładzie jest BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="0c398-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a><span data-ttu-id="0c398-118">Mapowanie maszyny Wirtualnej zestawu skalowania obciążenia równoważenia tooeach węzła typu/maszyny Wirtualnej zestawu skali</span><span class="sxs-lookup"><span data-stu-id="0c398-118">Mapping VM scale set load balancers tooeach node type/VM Scale Set</span></span>
<span data-ttu-id="0c398-119">Jeśli wdrożono klaster z portalu hello lub użyto szablonu usługi Resource Manager próbki hello, który mamy pod warunkiem, gdy zostanie wyświetlona lista wszystkich zasobów w grupie zasobów zostanie wyświetlona hello usługi równoważenia obciążenia dla każdego typu zestawu skali maszyny Wirtualnej lub węzeł.</span><span class="sxs-lookup"><span data-stu-id="0c398-119">If you have deployed your cluster from hello portal or have used hello sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see hello load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="0c398-120">Witaj nazwy będzie wyglądać mniej więcej tak: **LB -&lt;nazwa NodeType&gt;**.</span><span class="sxs-lookup"><span data-stu-id="0c398-120">hello name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="0c398-121">Na przykład LB-sfcluster4doc-0, jak pokazano w tym zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="0c398-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Zasoby][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="0c398-123">Połączenie zdalne tooa wystąpienia zestawu skali maszyny Wirtualnej lub węzła klastra</span><span class="sxs-lookup"><span data-stu-id="0c398-123">Remote connect tooa VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="0c398-124">Każdy typ węzła, który jest zdefiniowany w klastrze jest skonfigurowany jako osobne zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c398-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="0c398-125">Czy oznacza hello typy węzłów może być skalowana w dół niezależnie i można się z różnych jednostek SKU maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c398-125">That means hello node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="0c398-126">W przeciwieństwie do pojedynczego wystąpienia na maszynach wirtualnych hello wystąpienia zestawu skali maszyny Wirtualnej nie są wirtualnego adresu IP w swoich własnych.</span><span class="sxs-lookup"><span data-stu-id="0c398-126">Unlike single instance VMs, hello VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="0c398-127">Dlatego może być nieco wyzwanie podczas wyszukiwania adresu IP adres i port służy tooremote połączyć tooa określonego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="0c398-127">So it can be a bit challenging when you are looking for an IP address and port that you can use tooremote connect tooa specific instance.</span></span>

<span data-ttu-id="0c398-128">Poniżej przedstawiono kroki hello możesz wykonać toodiscover je.</span><span class="sxs-lookup"><span data-stu-id="0c398-128">Here are hello steps you can follow toodiscover them.</span></span>

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="0c398-129">Krok 1: Sprawdzić hello wirtualnego adresu IP dla typu węzła hello, a następnie reguły NAT ruchu przychodzącego protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="0c398-129">Step 1: Find out hello virtual IP address for hello node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="0c398-130">W kolejności tooget, że należy tooget hello translacji NAT ruchu przychodzącego zasady wartości, które zostały zdefiniowane jako część hello definicji zasobu dla **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="0c398-130">In order tooget that, you need tooget hello inbound NAT rules values that were defined as a part of hello resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="0c398-131">W portalu hello Przejdź bloku modułu równoważenia obciążenia toohello, a następnie **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="0c398-131">In hello portal, navigate toohello Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="0c398-133">W **ustawienia**, kliknij **reguł ruchu przychodzącego translatora adresów Sieciowych**.</span><span class="sxs-lookup"><span data-stu-id="0c398-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="0c398-134">To teraz zapewnia hello adresu IP i portu, których można używać tooremote połączyć toohello pierwszego wystąpienia zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c398-134">This now gives you hello IP address and port that you can use tooremote connect toohello first VM Scale Set instance.</span></span> <span data-ttu-id="0c398-135">W poniższym zrzucie ekranu hello, jest **104.42.106.156** i **3389**</span><span class="sxs-lookup"><span data-stu-id="0c398-135">In hello screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a><span data-ttu-id="0c398-137">Krok 2: Sprawdź hello port służy tooremote połączyć toohello określonego zestawu skali maszyny Wirtualnej/węzła wystąpienia</span><span class="sxs-lookup"><span data-stu-id="0c398-137">Step 2: Find out hello port that you can use tooremote connect toohello specific VM Scale Set instance/node</span></span>
<span data-ttu-id="0c398-138">Wcześniej w tym dokumencie I omówiono sposób wystąpienia zestawu skali maszyny Wirtualnej hello mapowania toohello węzłów.</span><span class="sxs-lookup"><span data-stu-id="0c398-138">Earlier in this document, I talked about how hello VM Scale Set instances map toohello nodes.</span></span> <span data-ttu-id="0c398-139">Użyjemy tego toofigure hello dokładne portu.</span><span class="sxs-lookup"><span data-stu-id="0c398-139">We will use that toofigure out hello exact port.</span></span>

<span data-ttu-id="0c398-140">porty Hello są przydzielane w kolejności rosnącej hello wystąpienia zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c398-140">hello ports are allocated in ascending order of hello VM Scale Set instance.</span></span> <span data-ttu-id="0c398-141">Dlatego w naszym przykładzie hello typ węzła frontonu hello portów dla poszczególnych wystąpień pięć hello są hello następujące.</span><span class="sxs-lookup"><span data-stu-id="0c398-141">so in my example for hello FrontEnd node type, hello ports for each of hello five instances are hello following.</span></span> <span data-ttu-id="0c398-142">Możesz teraz konieczne toodo hello mapowania tego samego wystąpienia zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c398-142">you now need toodo hello same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="0c398-143">**Wystąpienia zestawu skalowania maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="0c398-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="0c398-144">**Port**</span><span class="sxs-lookup"><span data-stu-id="0c398-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="0c398-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="0c398-145">FrontEnd_0</span></span> |<span data-ttu-id="0c398-146">3389</span><span class="sxs-lookup"><span data-stu-id="0c398-146">3389</span></span> |
| <span data-ttu-id="0c398-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="0c398-147">FrontEnd_1</span></span> |<span data-ttu-id="0c398-148">3390</span><span class="sxs-lookup"><span data-stu-id="0c398-148">3390</span></span> |
| <span data-ttu-id="0c398-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="0c398-149">FrontEnd_2</span></span> |<span data-ttu-id="0c398-150">3391</span><span class="sxs-lookup"><span data-stu-id="0c398-150">3391</span></span> |
| <span data-ttu-id="0c398-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="0c398-151">FrontEnd_3</span></span> |<span data-ttu-id="0c398-152">3392</span><span class="sxs-lookup"><span data-stu-id="0c398-152">3392</span></span> |
| <span data-ttu-id="0c398-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="0c398-153">FrontEnd_4</span></span> |<span data-ttu-id="0c398-154">3393</span><span class="sxs-lookup"><span data-stu-id="0c398-154">3393</span></span> |
| <span data-ttu-id="0c398-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="0c398-155">FrontEnd_5</span></span> |<span data-ttu-id="0c398-156">3394</span><span class="sxs-lookup"><span data-stu-id="0c398-156">3394</span></span> |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a><span data-ttu-id="0c398-157">Krok 3: Połączenie zdalne toohello określonego wystąpienia zestawu skali maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0c398-157">Step 3: Remote connect toohello specific VM Scale Set instance</span></span>
<span data-ttu-id="0c398-158">W poniższym zrzucie ekranu hello używać Podłączanie pulpitu zdalnego tooconnect toohello FrontEnd_1:</span><span class="sxs-lookup"><span data-stu-id="0c398-158">In hello screenshot below I use Remote Desktop Connection tooconnect toohello FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a><span data-ttu-id="0c398-160">Jak toochange hello portem RDP zakres wartości</span><span class="sxs-lookup"><span data-stu-id="0c398-160">How toochange hello RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="0c398-161">Przed wdrożeniem klastra</span><span class="sxs-lookup"><span data-stu-id="0c398-161">Before cluster deployment</span></span>
<span data-ttu-id="0c398-162">Podczas konfigurowania klastra hello przy użyciu szablonu usługi Resource Manager, możesz określić zakres hello w hello **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="0c398-162">When you are setting up hello cluster using an Resource Manager template, you can specify hello range in hello **inboundNatPools**.</span></span>

<span data-ttu-id="0c398-163">Przejdź definicji zasobu toohello **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="0c398-163">Go toohello resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="0c398-164">Zgodnie z tym znajdziesz opis hello **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="0c398-164">Under that you find hello description for **inboundNatPools**.</span></span>  <span data-ttu-id="0c398-165">Zastąp hello *wartość frontendPortRangeStart* i *wartość frontendPortRangeEnd* wartości.</span><span class="sxs-lookup"><span data-stu-id="0c398-165">Replace hello *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![InboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="0c398-167">Po wdrożeniu klastra</span><span class="sxs-lookup"><span data-stu-id="0c398-167">After cluster deployment</span></span>
<span data-ttu-id="0c398-168">To jest nieco bardziej skomplikowane i może spowodować maszyn wirtualnych hello ponownego przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="0c398-168">This is a bit more involved and may result in hello VMs getting recycled.</span></span> <span data-ttu-id="0c398-169">Konieczne będzie teraz nowe wartości tooset przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0c398-169">You will now have tooset new values using Azure PowerShell.</span></span> <span data-ttu-id="0c398-170">Upewnij się, że na tym komputerze jest zainstalowany program Azure PowerShell 1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0c398-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="0c398-171">Czy nie zostało zrobione to przed, można zdecydowanie wskazują należy wykonać hello czynności opisane w temacie [jak tooinstall i konfigurowanie programu Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="0c398-171">If you have not done this before, I strongly suggest that you follow hello steps outlined in [How tooinstall and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="0c398-172">Zaloguj się tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0c398-172">Sign in tooyour Azure account.</span></span> <span data-ttu-id="0c398-173">Jeśli tego polecenia programu PowerShell jakiegoś powodu nie powiedzie się, należy sprawdzić, czy został poprawnie zainstalowany program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0c398-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="0c398-174">Uruchom hello poniższe informacje tooget na moduł równoważenia obciążenia, aby zobaczyć wartości hello opis hello **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="0c398-174">Run hello following tooget details on your load balancer and you see hello values for hello description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="0c398-175">Teraz ustawić *wartość frontendPortRangeEnd* i *wartość frontendPortRangeStart* toohello wartości, które mają.</span><span class="sxs-lookup"><span data-stu-id="0c398-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* toohello values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="0c398-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0c398-176">Next steps</span></span>
* [<span data-ttu-id="0c398-177">Omówienie funkcji "Dowolne miejsce wdrożenie" hello i porównanie z klastrami zarządzane Azure</span><span class="sxs-lookup"><span data-stu-id="0c398-177">Overview of hello "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="0c398-178">Zabezpieczenia klastra</span><span class="sxs-lookup"><span data-stu-id="0c398-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="0c398-179">Zestaw SDK usług sieci szkieletowej i wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="0c398-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
