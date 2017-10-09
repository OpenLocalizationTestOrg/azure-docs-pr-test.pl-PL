---
title: "aaaCreate wewnętrznego Azure PowerShell klasycznego moduł równoważenia - obciążenia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa równoważenia w hello klasycznego modelu wdrażania przy użyciu programu PowerShell obciążenia toocreate jako wewnętrzne"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a>Wprowadzenie do tworzenia wewnętrznego modułu równoważenia obciążenia (klasycznego) przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> * [Program PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Usługi w chmurze](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](load-balancer-get-started-ilb-arm-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a>Tworzenie zestawu wewnętrznego modułu równoważenia obciążenia dla maszyn wirtualnych

toocreate wewnętrznego modułu równoważenia obciążenia ustaw i hello serwerów, które będzie wysyłać ich tooit ruchu sieciowego, masz następujące hello toodo:

1. Utwórz wystąpienie wewnętrzne Równoważenie obciążenia sieciowego, który będzie hello punkt końcowy przychodzącego ruchu toobe równoważone między serwerami hello zestawu z równoważeniem obciążenia.
2. Dodawanie punktów końcowych odpowiadającego toohello maszyn wirtualnych, które będzie otrzymywał hello ruchu przychodzącego.
3. Konfigurowanie serwerów hello, które będą wysyłane się, że hello ruchu toobe o zrównoważonym obciążeniu toosend ich ruchu toohello wirtualny adres IP (VIP) wystąpienia hello wewnętrzne Równoważenie obciążenia sieciowego.

### <a name="step-1-create-an-internal-load-balancing-instance"></a>Krok 1: utwórz wystąpienie wewnętrznego równoważenia obciążenia

Dla istniejącej usługi w chmurze lub wdrożyć w obszarze regionalnej sieci wirtualnej usługi w chmurze można utworzyć wystąpienia wewnętrzne Równoważenie obciążenia sieciowego z hello następujących poleceń programu Windows PowerShell:

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

Należy pamiętać, że to zastosowanie hello [AzureEndpoint Dodaj](https://msdn.microsoft.com/library/dn495300.aspx) zestaw parametrów DefaultProbe hello używa polecenia cmdlet programu Windows PowerShell. Aby uzyskać więcej informacji na temat dodatkowych zestawów parametrów, zobacz artykuł [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a>Krok 2: Dodawanie punktów końcowych toohello równoważenia obciążenia wewnętrznego wystąpienia

Oto przykład:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a>Krok 3: Konfigurowanie Twojego toosend serwerów ich ruchu toohello nowego wewnętrzne Równoważenie obciążenia sieciowego punktu końcowego

Ma zbyt skonfigurować serwery hello, których ruch jest będzie toobe ze zrównoważonym obciążeniem toouse hello nowy adres IP (hello VIP) hello wystąpienia wewnętrzne Równoważenie obciążenia sieciowego. Jest to adres hello, na które hello równoważenia obciążenia wewnętrznego nasłuchuje wystąpienie. W większości przypadków należy toojust dodawania lub modyfikowania rekordu DNS dla hello VIP wystąpienia hello wewnętrzne Równoważenie obciążenia sieciowego.

Jeśli określony adres IP hello podczas tworzenia hello wystąpienia hello wewnętrzne Równoważenie obciążenia sieciowego, masz już hello VIP. W przeciwnym razie można wyświetlić VIP hello z hello następującego polecenia:

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

toouse tych poleceń, wprowadź wartości hello i Usuń hello < i >. Oto przykład:

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

Z widoku hello hello polecenia Get-AzureInternalLoadBalancer Zanotuj adres IP hello i serwery tooyour niezbędne zmiany hello lub tooensure rekordy DNS, który toohello VIP pobiera skierować ruchu związanego z.

> [!NOTE]
> platformy Microsoft Azure Hello używa statycznych, publicznie routingu adresów IPv4 dla różnych scenariuszy administracyjnych. adres IP Hello jest 168.63.129.16. Ten adres IP nie powinien być blokowany przez zapory, ponieważ może to spowodować nieoczekiwane zachowanie.
> Z zakresie tooAzure wewnętrzne Równoważenie obciążenia sieciowego ten adres IP jest używana przez monitorowanie sond z stan kondycji hello toodetermine usługi równoważenia obciążenia powitania dla maszyn wirtualnych w zestawie o zrównoważonym obciążeniu. Jeśli grupa zabezpieczeń sieci jest toorestrict używanych maszyn wirtualnych tooAzure ruchu w zestawie wewnętrznie równoważeniem obciążenia lub zastosowane tooa podsieci sieci wirtualnej, upewnij się, że reguły zabezpieczeń sieci został dodany ruchu tooallow 168.63.129.16.

## <a name="example-of-internal-load-balancing"></a>Przykład wewnętrznego równoważenia obciążenia

toostep hello zakończenia tooend proces tworzenia zestawu z równoważeniem obciążenia dla dwóch przykładowe konfiguracje, zobaczysz hello w następujących sekcjach.

### <a name="an-internet-facing-multi-tier-application"></a>Aplikacja wielowarstwowa, dostępna z Internetu

Ma tooprovide usługi równoważenia obciążenia bazy danych dla zestawu serwerów sieci web skierowane do Internetu. Oba zestawy serwerów są hostowane na jednej usłudze w chmurze Azure. Port 1433 tooTCP ruchu serwera sieci Web muszą być dystrybuowane między dwiema maszynami wirtualnymi w hello warstwy bazy danych. Rysunek 1 pokazuje konfigurację hello.

![Wewnętrzny zestawu z równoważeniem obciążenia dla warstwy bazy danych hello](./media/load-balancer-internal-getstarted/IC736321.png)

Konfiguracja Hello obejmuje następujące hello:

* Witaj istniejącą usługę w chmurze hostowania maszyn wirtualnych hello nosi nazwę mytestcloud.
* dwa istniejących serwerów bazy danych Hello są nazywane DB1, bazy danych DB2.
* Serwery sieci Web w warstwie web hello połączenia toohello serwerów baz danych w warstwie bazy danych hello przy użyciu hello prywatnego adresu IP. Inną opcją jest toouse własnego systemu DNS dla sieci wirtualnej hello i ręcznie zarejestrować rekordu A dla zestawu modułu równoważenia obciążenia wewnętrznego hello.

Witaj następujące polecenia Skonfiguruj nowe wystąpienie wewnętrzny równoważenia obciążenia o nazwie **ILBset** i Dodaj maszyny wirtualne toohello punkty końcowe odpowiadającego toohello dwa serwery baz danych:

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a>Usuwanie konfiguracji wewnętrznego równoważenia obciążenia

tooremove maszynę wirtualną jako punkt końcowy z wystąpieniem usługi równoważenia obciążenia wewnętrznego hello Użyj następującego polecenia:

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

toouse tych poleceń, podaj wartości hello, usuwanie hello < i >.

Oto przykład:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

tooremove wystąpienia usługi równoważenia obciążenia wewnętrznego z usługą w chmurze, hello Użyj następującego polecenia:

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

toouse tych poleceń, wypełnij wartość hello i Usuń hello < i >.

Oto przykład:

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a>Dodatkowe informacje na temat poleceń cmdlet wewnętrznego modułu równoważenia obciążenia

tooobtain dodatkowe informacje dotyczące równoważenia obciążenia wewnętrznego poleceń cmdlet narzędzia, uruchom następujące polecenia w wierszu polecenia programu Windows PowerShell hello:

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a>Następne kroki

[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia przy użyciu koligacji źródłowych adresów IP)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)

