---
title: "aaaMutiple adresy VIP dla usługi w chmurze"
description: "Omówienie z wieloma wirtualnymi adresami IP i w jaki sposób tooset wielu adresów VIP na usługi w chmurze"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a>Konfigurowanie wielu adresów VIP dla usługi w chmurze

Usługi w chmurze Azure dostępne za pośrednictwem hello podane publicznego Internetu przy użyciu adresu IP na platformie Azure. Ten publiczny adres IP jest określony tooas VIP (wirtualny adres IP), ponieważ jest on połączony toohello Azure Usługa równoważenia obciążenia, a nie hello wystąpień maszyn wirtualnych (VM) w ramach usługi w chmurze hello. Można uzyskać dostępu do dowolnego wystąpienia maszyny Wirtualnej w ramach usługi w chmurze przy użyciu pojedynczego wirtualnego adresu IP.

Istnieją jednak scenariuszy, w których może wymagać więcej niż jeden VIP jako toohello punktu wejścia sama usługa w chmurze. Na przykład usługi w chmurze może hostować wiele witryn sieci Web, które wymagają łączności SSL przy użyciu hello domyślnego portu 443, ponieważ każda lokacja jest hostowana dla różnych klientów lub dzierżawców. W tym scenariuszu należy toohave inny publiczny połączonej adres IP dla każdej witryny sieci Web. Witaj Poniższy diagram przedstawia typowy wielodostępne hostingu sieci web potrzebujących SSL wielu certyfikatów na powitania sam port publiczny.

![Scenariusz Multi VIP SSL](./media/load-balancer-multivip/Figure1.png)

W przykładzie hello powyżej, wszystkie wirtualne adresy IP Użyj hello ruchu i tym samym port publiczny (port 443) jest przekierowane tooone, lub więcej obciążenia zrównoważonym maszyn wirtualnych na unikatowy port prywatny hello wewnętrznego adresu IP usługi w chmurze hello hosting wszystkich hello witryn sieci Web.

> [!NOTE]
> Inny hello Użyj hello wymagające sytuacji wieloma wirtualnymi adresami IP obsługuje wiele odbiorniki grupy dostępności funkcji SQL AlwaysOn na powitania sam zestaw maszyn wirtualnych.

Wirtualne adresy IP są dynamiczne domyślnie, co oznacza, że hello rzeczywistego adresu IP przypisanego toohello usługi w chmurze mogą się zmieniać wraz z upływem czasu. tooprevent czy zapobiec, istnieje możliwość rezerwowania adresu VIP dla usługi. toolearn więcej informacji na temat zarezerwowane wirtualne adresy IP, zobacz [zastrzeżone publicznego adresu IP](../virtual-network/virtual-networks-reserved-public-ip.md).

> [!NOTE]
> Zobacz [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses/) Aby uzyskać informacje o cenach na adresy VIP i zarezerwowane adresy IP.

Można używać środowiska PowerShell tooverify hello wirtualne adresy IP używane przez usług w chmurze, oraz dodawania i Usuń VIP, skojarzyć punkt końcowy tooan VIP oraz konfigurowanie równoważenia na określonego adresu VIP obciążenia.

## <a name="limitations"></a>Ograniczenia

W tej chwili funkcja wielu adresów VIP jest ograniczony toohello następujące scenariusze:

* **Tylko IaaS**. Można włączyć tylko Multi VIP dla usług w chmurze, które zawierają maszyny wirtualne. Nie można użyć adresu VIP wielu wystąpień roli PaaS scenariuszy.
* **PowerShell tylko**. Wiele adresów VIP może zarządzać tylko przy użyciu programu PowerShell.

Ograniczenia te są tymczasowe i mogą ulec zmianie w dowolnym momencie. Upewnij się, że toorevisit tej strony tooverify przyszłe zmiany.

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a>Jak usługa w chmurze tooa tooadd adresu VIP
Usługa tooyour tooadd adresu VIP, uruchom następujące polecenia programu PowerShell hello:

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

To polecenie wyświetla wynik toohello podobne, następujące przykładowe:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a>Jak tooremove adresu VIP z usługi w chmurze
tooremove hello VIP dodawane tooyour usługi na przykład Witaj powyżej hello uruchom następujące polecenia programu PowerShell:

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> Można usunąć adresu VIP, jeśli ma ona nie tooit punkty końcowe skojarzone.


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a>Jak tooretrieve VIP informacji z usługi w chmurze
tooretrieve hello wirtualne adresy IP skojarzone z usługą w chmurze, uruchom hello następującego skryptu programu PowerShell:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

skrypt Hello wyświetla wynik toohello podobne, następujące przykładowe:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

W tym przykładzie usługa w chmurze hello ma 3 wirtualne adresy IP:

* **Adres Vip1** jest hello domyślny adres VIP, wiesz, że ponieważ hello IsDnsProgrammedName jest ustawiany tootrue.
* **Vip2** i **Vip3** nie są używane jako nie mają adresy IP. One tylko będzie używany, jeśli skojarzone toohello punktu końcowego adresu VIP.

> [!NOTE]
> Subskrypcją będzie obciążana dla dodatkowe wirtualne adresy IP, gdy są one powiązane z punktem końcowym. Aby uzyskać więcej informacji o cenach, zobacz [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a>Jak punktu końcowego tooan tooassociate adresu VIP

tooassociate adresu VIP w chmurze tooan punkt końcowy usługi, uruchom następujące polecenia programu PowerShell hello:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

Witaj polecenie tworzy punkt końcowy o nazwie adresów VIP połączonych toohello *Vip2* na porcie *80*i łączy go toohello maszyny Wirtualnej o nazwie *myVM1* w usłudze w chmurze o nazwie  *Moja_usługa* przy użyciu *TCP* na porcie *8080*.

tooverify hello konfiguracji, uruchom następujące polecenia programu PowerShell hello:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

Witaj dane wyjściowe wyglądają toohello podobnie poniższy przykład:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a>Jak tooenable Równoważenie obciążenia na określonych adresów VIP

Pojedynczego wirtualnego adresu IP można skojarzyć z wieloma maszynami wirtualnymi na potrzeby równoważenia obciążenia. Przykładowo, jeśli masz usługi w chmurze o nazwie *Moja_usługa*i dwie maszyny wirtualne o nazwie *myVM1* i *myVM2*. I usługi w chmurze ma wiele adresów VIP, jeden z nich o nazwie *Vip2*. Jeśli chcesz, aby cały ruch tooport tooensure *81* na *Vip2* jest rozmieszczana między *myVM1* i *myVM2* na porcie *8181* Uruchom hello następujący skrypt programu PowerShell:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

Można także zaktualizować Twojego toouse usługi równoważenia obciążenia różnych adresów VIP. Na przykład po uruchomieniu poniższego polecenia programu PowerShell hello ulegnie zmianie toouse zestaw o nazwie adresu Vip1 adresu VIP do równoważenia obciążenia hello:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a>Następne kroki

[Analiza dzienników Azure Równoważenie obciążenia](load-balancer-monitor-log.md)

[Omówienie usługi równoważenia obciążenia połączonej Internet](load-balancer-internet-overview.md)

[Przed rozpoczęciem pracy internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md)

[Omówienie sieci wirtualnej](../virtual-network/virtual-networks-overview.md)

[Interfejsy API REST zastrzeżonego adresu IP](https://msdn.microsoft.com/library/azure/dn722420.aspx)
