---
title: "aaaConfigure zawsze na dostępność odbiorniki grupy — Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Skonfiguruj odbiorniki grupy dostępności na powitania usługi Azure Resource Manager modelu przy użyciu wewnętrznego modułu równoważenia obciążenia z co najmniej jeden adres IP."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a>Skonfiguruj co najmniej jeden zawsze na dostępność odbiorniki grupy - Resource Manager
W tym temacie przedstawiono sposób:

* Utwórz wewnętrznego modułu równoważenia obciążenia dla grupy dostępności programu SQL Server przy użyciu poleceń cmdlet programu PowerShell.
* Dodaj dodatkowe IP adresów tooa modułu równoważenia obciążenia dla więcej niż jednej grupy dostępności. 

Odbiornik grupy dostępności jest nazwą sieci wirtualnej Klienci nawiązują połączenie toofor dostęp do bazy danych. Na maszynach wirtualnych Azure usługi równoważenia obciążenia przechowuje hello adresu IP dla odbiornika hello. trasy modułu równoważenia obciążenia Hello ruch toohello wystąpienia programu SQL Server nasłuchuje na porcie sondowania hello. Zazwyczaj grupa dostępności używa wewnętrznego modułu równoważenia obciążenia. Azure wewnętrznego modułu równoważenia obciążenia może obsługiwać jeden lub wiele adresów IP. Każdy adres IP używa portu określonych sondowania. Ten dokument zawiera jak toouse PowerShell toocreate modułu równoważenia obciążenia, lub Dodaj adresy IP tooan istniejący moduł równoważenia obciążenia dla grupy dostępności programu SQL Server. 

Witaj tooassign możliwości wielu IP adresów tooan wewnętrznego modułu równoważenia obciążenia jest nowy tooAzure i jest dostępna tylko w modelu usługi Resource Manager. toocomplete to zadanie należy toohave wdrożone grupy dostępności programu SQL Server na maszynach wirtualnych Azure w modelu usługi Resource Manager. Maszyny wirtualne zarówno programu SQL Server, trzeba należeć toohello tego samego zestawu dostępności. Można użyć hello [szablonów Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically utworzyć grupy dostępności hello Azure Resource Manager. Ten szablon tworzy automatycznie grupy dostępności hello, w tym hello wewnętrznego modułu równoważenia obciążenia. Jeśli wolisz, możesz [ręczne konfigurowanie zawsze włączonej grupy dostępności](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

W tym temacie wymaga już skonfigurowania grup dostępności.  

Tematy pokrewne obejmują:

* [Konfigurowanie grup dostępności AlwaysOn w maszynie Wirtualnej platformy Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Konfigurowanie połączenia do wirtualnymi przy użyciu usługi Azure Resource Manager i programu PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a>Konfigurowanie Zapory systemu Windows hello
Skonfiguruj dostęp programu SQL Server tooallow zapory systemu Windows hello. reguły zapory Hello dopuszczać porty toohello połączeń TCP za pomocą wystąpienia programu SQL Server hello i badania odbiornika hello. Aby uzyskać szczegółowe instrukcje, zobacz [Konfigurowanie Zapory systemu Windows dla dostępu aparatu bazy danych](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1). Utwórz regułę ruchu przychodzącego dla hello port programu SQL Server i port sondy hello.

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a>Przykładowy skrypt: Tworzenie wewnętrznego modułu równoważenia obciążenia przy użyciu programu PowerShell
> [!NOTE]
> Jeśli utworzono grupy dostępności z hello [szablonów Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello wewnętrznego modułu równoważenia obciążenia został już utworzony. 
> 
> 

Witaj następujący skrypt programu PowerShell tworzy wewnętrznego modułu równoważenia obciążenia, konfiguruje reguły równoważenia obciążenia hello i ustawia adres IP dla modułu równoważenia obciążenia hello. skrypt hello toorun, Otwórz program Windows PowerShell ISE, a następnie wklej hello skryptu w okienku skryptów hello. Użyj `Login-AzureRMAccount` toolog w tooPowerShell. Jeśli masz wiele subskrypcji Azure, użyj `Select-AzureRmSubscription ` tooset hello subskrypcji. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <a name="Add-IP"></a>Przykładowy skrypt: Dodaj IP address tooan istniejący moduł równoważenia obciążenia przy użyciu programu PowerShell
toouse ponad grupy dostępności, Dodaj dodatkowe równoważenia obciążenia toohello adresów IP. Każdy adres IP wymaga własne reguły równoważenia obciążenia, port sondy oraz portu frontonu.

Witaj frontonu jest hello port czy aplikacje używają wystąpienia programu SQL Server toohello tooconnect. Adresy IP dla różnych dostępności grupy można używać hello tego samego portu frontonu.

> [!NOTE]
> Dla grup dostępności programu SQL Server każdy adres IP wymaga sondowania określonego portu. Na przykład jeśli jeden adres IP modułu równoważenia obciążenia używa portu sondowania 59999, nie adresów IP w tej usługi równoważenia obciążenia można użyć portu sondowania 59999.

* Uzyskać informacji dotyczących ograniczeń usługi równoważenia obciążenia, zobacz **adresu IP frontonu prywatne dla usługi równoważenia obciążenia** w obszarze [sieci limity — usługi Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).
* Aby uzyskać informacji na temat limitów grupy dostępności, zobacz [ograniczenia (grupy dostępności)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).

Witaj poniższy skrypt dodaje nowe IP adres tooan istniejącej usługi równoważenia obciążenia. Witaj ILB korzysta z portu odbiornika hello dla portów frontonu równoważenia obciążenia hello. Port ten może być hello port, który serwer SQL nasłuchuje na. Dla domyślnego wystąpienia programu SQL Server hello portu to 1433. reguły dla grupy dostępności równoważenia obciążenia Hello wymaga pływającego adresu IP (bezpośredni zwrot serwera), port zaplecza hello jest hello takie same jak port frontonu hello. Zaktualizuj zmienne hello w danym środowisku. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a>Skonfiguruj odbiornik hello

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a>Port odbiornika hello zestawu w programie SQL Server Management Studio

1. Uruchom program SQL Server Management Studio i połącz toohello repliki podstawowej.

1. Przejdź za**wysokiej dostępności funkcji AlwaysOn** | **grup dostępności** | **odbiorniki grupy dostępności**. 

1. Powinna zostać wyświetlona nazwa odbiornika hello utworzonego w Menedżerze klastra trybu Failover. Kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij przycisk **właściwości**.

1. W hello **portu** Określ numer portu odbiornika grupy dostępności hello hello przy użyciu hello $EndpointPort użyto wcześniej (1433 była hello domyślna), następnie kliknij przycisk **OK**.

## <a name="test-hello-connection-toohello-listener"></a>Odbiornik toohello połączenia hello testu

tootest hello połączenia:

1. RDP tooa programu SQL Server, który znajduje się w hello sam wirtualnych sieci, ale nie nie własnych hello repliki. To może być hello innego serwera SQL w klastrze hello.

1. Użyj **sqlcmd** narzędzie tootest hello połączenia. Na przykład ustanawia hello następującego skryptu **sqlcmd** repliki podstawowej toohello połączenia za pośrednictwem hello odbiornika z uwierzytelnianiem systemu Windows:
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    Jeśli odbiornik hello używa portu innego niż hello domyślnego portu (1433), określ hello port w parametrach połączenia hello. Na przykład hello następującego polecenia sqlcmd łączy odbiornika tooa portu 1435: 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Witaj SQLCMD połączenia automatycznie łączy toowhichever wystąpienie programu SQL Server repliki podstawowej hello hostów. 

> [!NOTE]
> Upewnij się, że port hello określony jest otwarty na zaporze hello obu serwerów SQL. Oba serwery wymagają regułę ruchu przychodzącego dla portu TCP, którego używasz hello. Zobacz [Dodawanie lub edytowanie reguły zapory](http://technet.microsoft.com/library/cc753558.aspx) Aby uzyskać więcej informacji. 
> 
> 

## <a name="guidelines-and-limitations"></a>Wytyczne i ograniczenia
Należy uwzględnić następujące wytyczne dotyczące odbiornika grupy dostępności na platformie Azure przy użyciu wewnętrznego modułu równoważenia obciążenia hello:

* Wewnętrzny moduł równoważenia obciążenia, należy tylko na uzyskiwanie dostępu do odbiornika hello z WE hello tej samej sieci wirtualnej.


## <a name="for-more-information"></a>Aby uzyskać więcej informacji
Aby uzyskać więcej informacji, zobacz [dostępności Konfigurowanie zawsze włączonej grupy w maszynie Wirtualnej platformy Azure ręcznie](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

## <a name="powershell-cmdlets"></a>Polecenia cmdlet programu PowerShell
Użyj powitania po toocreate poleceń cmdlet programu PowerShell wewnętrznego modułu równoważenia obciążenia maszyn wirtualnych platformy Azure.

* [Nowy AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) tworzy moduł równoważenia obciążenia. 
* [Nowy AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) tworzy konfigurację IP frontonu modułu równoważenia obciążenia. 
* [Nowy AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) tworzona jest reguła Konfiguracja usługi równoważenia obciążenia. 
* [Nowy AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) tworzy Konfiguracja puli adresów zaplecza, usługi równoważenia obciążenia. 
* [Nowy AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) tworzy badania konfiguracji usługi równoważenia obciążenia.
* [Usuń AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) usuwa modułu równoważenia obciążenia z grupy zasobów platformy Azure.
