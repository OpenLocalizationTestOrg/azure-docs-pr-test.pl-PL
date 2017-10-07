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
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a>Hello relacji między typami węzła sieci szkieletowej usług i zestawy skalowania maszyny wirtualnej
Zestawy skalowania maszyny wirtualnej są zasobami rozwiązań usługi obliczenia Azure można użyć toodeploy i zarządzanie kolekcją jako zestaw maszyn wirtualnych. Każdy typ węzła który jest zdefiniowany w klastrze usługi sieć szkieletowa jest skonfigurowany jako osobne zestawu skali maszyny Wirtualnej. Każdy typ węzła następnie można skalować w lub w dół niezależnie, mają różne zestawy otwartych portów i może mieć metryki pojemności różnych.

powitania po zrzut ekranu przedstawia klastra, która ma dwa typy węzłów: frontonu i wewnętrznej bazy danych.  Każdy typ węzła ma pięć węzłów.

![Zrzut ekranu przedstawiający klastra, która ma dwa typy węzłów][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a>Mapowanie toonodes wystąpienia zestawu skali maszyny Wirtualnej
Jak widać powyżej, wystąpienia zestawu skali maszyny Wirtualnej hello Uruchom z wystąpienia 0, a następnie rośnie. numerowanie Hello znajduje odzwierciedlenie w nazwach hello. Na przykład BackEnd_0 jest wystąpienie 0 hello zestawu skali maszyny Wirtualnej w wewnętrznej bazie danych. Tego konkretnego zestawu skali maszyny Wirtualnej ma pięć wystąpień, o nazwie BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 i BackEnd_4.

Skalowanie w górę zestawu skali maszyny Wirtualnej jest tworzone nowe wystąpienie. Hello nowego zestawu skali maszyny Wirtualnej nazwy wystąpienia będzie zazwyczaj nazwa zestawu skali maszyny Wirtualnej hello + hello dalej liczby wystąpień. W naszym przykładzie jest BackEnd_5.

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a>Mapowanie maszyny Wirtualnej zestawu skalowania obciążenia równoważenia tooeach węzła typu/maszyny Wirtualnej zestawu skali
Jeśli wdrożono klaster z portalu hello lub użyto szablonu usługi Resource Manager próbki hello, który mamy pod warunkiem, gdy zostanie wyświetlona lista wszystkich zasobów w grupie zasobów zostanie wyświetlona hello usługi równoważenia obciążenia dla każdego typu zestawu skali maszyny Wirtualnej lub węzeł.

Witaj nazwy będzie wyglądać mniej więcej tak: **LB -&lt;nazwa NodeType&gt;**. Na przykład LB-sfcluster4doc-0, jak pokazano w tym zrzut ekranu:

![Zasoby][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a>Połączenie zdalne tooa wystąpienia zestawu skali maszyny Wirtualnej lub węzła klastra
Każdy typ węzła, który jest zdefiniowany w klastrze jest skonfigurowany jako osobne zestawu skali maszyny Wirtualnej.  Czy oznacza hello typy węzłów może być skalowana w dół niezależnie i można się z różnych jednostek SKU maszyny Wirtualnej. W przeciwieństwie do pojedynczego wystąpienia na maszynach wirtualnych hello wystąpienia zestawu skali maszyny Wirtualnej nie są wirtualnego adresu IP w swoich własnych. Dlatego może być nieco wyzwanie podczas wyszukiwania adresu IP adres i port służy tooremote połączyć tooa określonego wystąpienia.

Poniżej przedstawiono kroki hello możesz wykonać toodiscover je.

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a>Krok 1: Sprawdzić hello wirtualnego adresu IP dla typu węzła hello, a następnie reguły NAT ruchu przychodzącego protokołu RDP
W kolejności tooget, że należy tooget hello translacji NAT ruchu przychodzącego zasady wartości, które zostały zdefiniowane jako część hello definicji zasobu dla **Microsoft.Network/loadBalancers**.

W portalu hello Przejdź bloku modułu równoważenia obciążenia toohello, a następnie **ustawienia**.

![LBBlade][LBBlade]

W **ustawienia**, kliknij **reguł ruchu przychodzącego translatora adresów Sieciowych**. To teraz zapewnia hello adresu IP i portu, których można używać tooremote połączyć toohello pierwszego wystąpienia zestawu skali maszyny Wirtualnej. W poniższym zrzucie ekranu hello, jest **104.42.106.156** i **3389**

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a>Krok 2: Sprawdź hello port służy tooremote połączyć toohello określonego zestawu skali maszyny Wirtualnej/węzła wystąpienia
Wcześniej w tym dokumencie I omówiono sposób wystąpienia zestawu skali maszyny Wirtualnej hello mapowania toohello węzłów. Użyjemy tego toofigure hello dokładne portu.

porty Hello są przydzielane w kolejności rosnącej hello wystąpienia zestawu skali maszyny Wirtualnej. Dlatego w naszym przykładzie hello typ węzła frontonu hello portów dla poszczególnych wystąpień pięć hello są hello następujące. Możesz teraz konieczne toodo hello mapowania tego samego wystąpienia zestawu skali maszyny Wirtualnej.

| **Wystąpienia zestawu skalowania maszyny Wirtualnej** | **Port** |
| --- | --- |
| FrontEnd_0 |3389 |
| FrontEnd_1 |3390 |
| FrontEnd_2 |3391 |
| FrontEnd_3 |3392 |
| FrontEnd_4 |3393 |
| FrontEnd_5 |3394 |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a>Krok 3: Połączenie zdalne toohello określonego wystąpienia zestawu skali maszyny Wirtualnej
W poniższym zrzucie ekranu hello używać Podłączanie pulpitu zdalnego tooconnect toohello FrontEnd_1:

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a>Jak toochange hello portem RDP zakres wartości
### <a name="before-cluster-deployment"></a>Przed wdrożeniem klastra
Podczas konfigurowania klastra hello przy użyciu szablonu usługi Resource Manager, możesz określić zakres hello w hello **inboundNatPools**.

Przejdź definicji zasobu toohello **Microsoft.Network/loadBalancers**. Zgodnie z tym znajdziesz opis hello **inboundNatPools**.  Zastąp hello *wartość frontendPortRangeStart* i *wartość frontendPortRangeEnd* wartości.

![InboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a>Po wdrożeniu klastra
To jest nieco bardziej skomplikowane i może spowodować maszyn wirtualnych hello ponownego przetworzenia. Konieczne będzie teraz nowe wartości tooset przy użyciu programu Azure PowerShell. Upewnij się, że na tym komputerze jest zainstalowany program Azure PowerShell 1.0 lub nowszej. Czy nie zostało zrobione to przed, można zdecydowanie wskazują należy wykonać hello czynności opisane w temacie [jak tooinstall i konfigurowanie programu Azure PowerShell.](/powershell/azure/overview)

Zaloguj się tooyour konto platformy Azure. Jeśli tego polecenia programu PowerShell jakiegoś powodu nie powiedzie się, należy sprawdzić, czy został poprawnie zainstalowany program Azure PowerShell.

```
Login-AzureRmAccount
```

Uruchom hello poniższe informacje tooget na moduł równoważenia obciążenia, aby zobaczyć wartości hello opis hello **inboundNatPools**:

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

Teraz ustawić *wartość frontendPortRangeEnd* i *wartość frontendPortRangeStart* toohello wartości, które mają.

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a>Następne kroki
* [Omówienie funkcji "Dowolne miejsce wdrożenie" hello i porównanie z klastrami zarządzane Azure](service-fabric-deploy-anywhere.md)
* [Zabezpieczenia klastra](service-fabric-cluster-security.md)
* [Zestaw SDK usług sieci szkieletowej i wprowadzenie](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
