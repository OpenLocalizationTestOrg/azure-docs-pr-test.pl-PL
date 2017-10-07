---
title: "aaaConfigure odbiornik ILB dla zawsze włączonych grup dostępności na platformie Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek używa zasobów utworzone za pomocą hello klasycznego modelu wdrażania i tworzy zawsze na odbiornik grupy dostępności na platformie Azure, która używa wewnętrznego modułu równoważenia obciążenia."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a>Skonfiguruj odbiornik ILB dla zawsze włączonych grup dostępności w systemie Azure
> [!div class="op_single_selector"]
> * [Odbiornik wewnętrzny](../classic/ps-sql-int-listener.md)
> * [Odbiornik zewnętrzny](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a>Omówienie

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono używanie hello hello klasycznego modelu wdrażania. Zaleca się, że większości nowych wdrożeń Użyj modelu Resource Manager hello.

Zobacz tooconfigure odbiornika dla zawsze włączone grupy dostępności w modelu Resource Manager hello [skonfigurowania funkcji równoważenia obciążenia dla grupy dostępności AlwaysOn w Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

Grupy dostępności może zawierać replik z lokalnymi tylko lub tylko Azure lub który obejmować zarówno lokalnych, jak i Azure dla hybrydowych konfiguracje. Azure replik może znajdować się w obrębie hello sam region lub w wielu regionach, które używają wielu sieci wirtualnych. Witaj procedury przedstawione w tym artykule założono, że istnieje już [skonfigurowane grupy dostępności](../classic/portal-sql-alwayson-availability-groups.md) , ale nie ma jeszcze skonfigurowany odbiornik.

## <a name="guidelines-and-limitations-for-internal-listeners"></a>Zasady i ograniczenia dotyczące odbiorników wewnętrzny
Użycie Hello wewnętrznego modułu równoważenia obciążenia (ILB) z odbiornika grupy dostępności na platformie Azure jest toohello podmiotu następujące wytyczne:

* odbiornik grupy dostępności Hello jest obsługiwana w systemie Windows Server 2008 R2, Windows Server 2012 i Windows Server 2012 R2.
* Tylko jeden odbiornik grupy dostępności wewnętrzny jest obsługiwana dla każdej usługi w chmurze, ponieważ odbiornik hello jest skonfigurowany toohello ILB, a istnieje tylko jeden ILB dla każdej usługi w chmurze. Jest jednak możliwe toocreate wiele odbiorników zewnętrznych. Aby uzyskać więcej informacji, zobacz [skonfigurować odbiornik zewnętrzny dla zawsze włączonych grup dostępności na platformie Azure](../classic/ps-sql-ext-listener.md).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Ustalić dostępność hello hello odbiornika
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Ten artykuł skupia się na utworzenie odbiornika, który używa ILB. Odbiornik publiczny lub zewnętrzne, należy wyświetlić wersję hello tego artykułu, w którym omówiono ustawienia zapasowej [zewnętrznych odbiornika](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Tworzyć równoważeniem obciążenia punkty końcowe maszyny Wirtualnej z serwerem bezpośredniego zwrotu
Należy najpierw utworzyć ILB, uruchamiając skrypt hello później w tej sekcji.

Tworzenie punktu końcowego z równoważeniem obciążenia dla każdej maszyny Wirtualnej, który obsługuje replikę Azure. Jeśli masz repliki w wielu regionach, każdej repliki dla tego regionu musi być w hello takie same usługi w chmurze hello sama sieć wirtualna platformy Azure. Tworzenie dostępności replik grupy, obejmujące wiele regionów platformy Azure wymaga konfigurowania wielu sieci wirtualnych. Aby uzyskać więcej informacji na temat konfigurowania granic łączność sieci wirtualnej, zobacz [skonfigurować łączność sieciową toovirtual sieci wirtualnej](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. W hello portalu Azure Przejdź tooeach maszynę Wirtualną, która obsługuje szczegóły hello tooview repliki.

2. Kliknij przycisk hello **punkty końcowe** kartę dla każdej maszyny Wirtualnej.

3. Sprawdź, że hello **nazwa** i **Port publiczny** punktu końcowego odbiornika hello, który ma być toouse nie są już używane. Na przykład Witaj w tej sekcji, nazwa hello to *MyEndpoint*, a hello port jest *1433*.

4. Na kliencie lokalnym, należy pobrać i zainstalować najnowsze hello [modułu PowerShell](https://azure.microsoft.com/downloads/).

5. Uruchom program Azure PowerShell.  
    Otwiera nową sesję programu PowerShell, z hello Azure administracyjne załadowanych modułów.

6. Uruchom polecenie `Get-AzurePublishSettingsFile`. To polecenie cmdlet kieruje tooa przeglądarki toodownload publikowania ustawienia pliku tooa katalogiem lokalnym. Użytkownik może zostać poproszony o podanie poświadczeń logowania dla subskrypcji platformy Azure.

7. Uruchom następujące hello `Import-AzurePublishSettingsFile` pobranego pliku ustawień publikowania polecenie z hello ścieżka hello:

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    Po publikowania hello jest importowany plik ustawień, można zarządzać subskrypcją platformy Azure w sesji programu PowerShell hello.

8. Aby uzyskać *ILB*, Przypisz statyczny adres IP. Sprawdź hello bieżącą konfigurację sieci wirtualnej, uruchamiając następujące polecenie hello:

        (Get-AzureVNetConfig).XMLConfiguration
9. Uwaga hello *podsieci* nazwę podsieci hello, która zawiera hello maszyn wirtualnych, które hosta replik hello. Ta nazwa jest używana w parametrze hello $SubnetName w skrypcie hello.

10. Uwaga hello *VirtualNetworkSite* nazwy i hello uruchamianie *prefiks adresu* dla podsieci hello, który zawiera hello maszyn wirtualnych, które hosta replik hello. Wyszukaj dostępnego adresu IP przez przekazanie toohello obie wartości `Test-AzureStaticVNetIP` polecenia i sprawdzając hello *AvailableAddresses*. Na przykład, jeśli hello sieci wirtualnej nosi nazwę *MyVNet* i ma zakres adresów podsieci, która rozpoczyna się od *172.16.0.128*, hello następujące polecenie, pojawi się lista dostępnych adresów:

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. Wybierz jedną z dostępnych adresów hello i użyć go w parametrze hello $ILBStaticIP skryptu hello na powitania następnego kroku.

12. Skopiuj powitania po Edytor tekstu tooa skrypt programu PowerShell i ustaw hello toosuit wartości zmiennych środowiska. Wartości domyślne zostały dołączone niektórych parametrów.  

    Istniejące wdrożenia, które korzysta z grup koligacji nie można dodać ILB. Aby uzyskać więcej informacji na temat wymagań dotyczących ILB, zobacz [Omówienie usługi równoważenia obciążenia wewnętrznego](../../../load-balancer/load-balancer-internal-overview.md).

    Ponadto jeśli grupy dostępności obejmuje regiony platformy Azure, należy uruchomić skrypt hello raz w centrum danych z każdej usługi w chmurze hello i węzły, które znajdują się w tym centrum danych.

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. Po ustawieniu zmienne hello hello Kopiuj skrypt z hello tekstu Edytor tooyour PowerShell sesji toorun go. Jeśli nadal wyświetlany jest monit hello  **>>** , naciśnij klawisz Enter ponownie toomake się, że skrypt hello zacznie działać.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Sprawdź, czy KB2854082 jest zainstalowana w razie potrzeby
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Otworzyć porty zapory hello w węzłach grupy dostępności
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Tworzenie odbiornika grupy dostępności hello

Tworzenie odbiornika grupy dostępności hello w dwóch krokach. Najpierw należy utworzyć zasobu klastra punktu dostępu klienta hello i skonfigurować zależności. Po drugie skonfiguruj hello zasoby klastra w programie PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Tworzenie punktu dostępu klienta hello i konfigurowanie hello zależności klastra
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Konfigurowanie zasobów klastra hello w programie PowerShell
1. ILB należy użyć adresu IP hello hello ILB, który został utworzony wcześniej. tooobtain adresów IP to w programie PowerShell hello Użyj następującego skryptu:

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. Na jednym z hello maszyn wirtualnych Skopiuj skrypt programu PowerShell hello do edytora tekstu tooa systemu operacyjnego, a następnie ustaw zmienne hello toohello wartości, które wcześniej zapisany.

    Dla systemu Windows Server 2012 lub nowszym Użyj następującego skryptu hello:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    Dla systemu Windows Server 2008 R2 Użyj następującego skryptu hello:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. Po utworzeniu zestawu hello zmiennych, Otwórz okno programu Windows PowerShell z podwyższonym poziomem uprawnień, Wklej hello skrypt z edytora tekstów hello do toorun sesji programu PowerShell go. Jeśli nadal wyświetlany jest monit hello  **>>** , naciśnij klawisz Enter, ponownie toomake się upewnić, że skrypt hello zacznie działać.

4. Powtórz hello w poprzednich krokach dla każdej maszyny Wirtualnej.  
    Ten skrypt konfiguruje zasobu adresu IP hello o adresie IP hello hello usługi w chmurze i ustawia innych parametrów, takich jak port sondy hello. Gdy zasób adresu IP hello w tryb online, jego odpowiadają toohello sondowania na porcie sondowania powitania od hello równoważeniem obciążenia punktu końcowego, który został utworzony wcześniej.

## <a name="bring-hello-listener-online"></a>Przełącz odbiornika hello w trybie online
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Elementy monitowania
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a>Odbiornik grupy dostępności hello testu (poziomu hello sam sieci wirtualnej)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
