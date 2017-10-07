---
title: "aaaConfigure odbiornik zewnętrzny dla zawsze włączonych grup dostępności | Dokumentacja firmy Microsoft"
description: "Ten samouczek przeszukiwań hello użytkownika przez kroki tworzenia zawsze na odbiornik grupy dostępności na platformie Azure, który jest dostępny zewnętrznie przy użyciu publicznego adresu IP wirtualnej hello usługi skojarzonej chmury."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a>Skonfiguruj odbiornik zewnętrzny dla zawsze włączonych grup dostępności w systemie Azure
> [!div class="op_single_selector"]
> * [Odbiornik wewnętrzny](../classic/ps-sql-int-listener.md)
> * [Odbiornik zewnętrzny](../classic/ps-sql-ext-listener.md)
> 
> 

W tym temacie opisano sposób tooconfigure odbiornika dla zawsze włączonej grupy dostępności, która jest dostępna zewnętrznie w hello internet. Jest to możliwe, kojarząc usługi chmury hello **publiczny wirtualnego adresu IP (VIP)** adres hello odbiornika.

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

Grupy dostępności mogą zawierać replik, które są lokalne, Azure, lub obejmować zarówno lokalnych, jak i Azure dla konfiguracji hybrydowego. Azure replik może znajdować się w obrębie hello sam region lub w wielu regionach, przy użyciu wielu sieci wirtualnych (sieci wirtualne). Poniższe kroki Hello założono, że masz już [skonfigurowane grupy dostępności](../classic/portal-sql-alwayson-availability-groups.md) , ale nie skonfigurowano odbiornik.

## <a name="guidelines-and-limitations-for-external-listeners"></a>Zasady i ograniczenia dotyczące odbiorników zewnętrznych
Należy zwrócić uwagę następujące wskazówki dotyczące hello odbiornika grupy dostępności na platformie Azure, w przypadku wdrażania za pomocą hello chmury usługi siła adresu VIP hello:

* odbiornik grupy dostępności Hello jest obsługiwana w systemie Windows Server 2008 R2, Windows Server 2012 i Windows Server 2012 R2.
* Aplikacja kliencka Hello musi znajdować się na innej usługi chmury niż hello zawierających grupy dostępności maszyn wirtualnych. Usługi w chmurze Azure nie obsługuje bezpośredniego zwrotu serwera z klienta i serwera w hello takie same.
* Domyślnie hello opisanych w tym artykule pokazują, jak tooconfigure jednego odbiornika toouse hello chmury adres wirtualnego adresu IP (VIP) usługi. Jednak jest możliwe tooreserve i utworzenia wielu adresów VIP dla usługi w chmurze. Dzięki temu toouse hello etapami toocreate tego artykułu, wiele odbiorników, z których każda skojarzone z różnych adresów VIP. Aby uzyskać informacje dotyczące toocreate wielu adresów VIP, zobacz temat [wieloma wirtualnymi adresami IP dla danej usługi chmury](../../../load-balancer/load-balancer-multivip.md).
* W przypadku tworzenia odbiornika dla środowiska hybrydowego, w sieci lokalnej hello musi mieć toohello łączności publicznej sieci Internet w toohello dodanie sieć VPN lokacja lokacja z hello sieci wirtualnej platformy Azure. W przypadku hello podsieci platformy Azure, odbiornika grupy dostępności hello jest dostępny tylko za pomocą publicznego adresu IP hello hello odpowiedniej chmury usługi.
* Nie jest obsługiwana toocreate odbiornik zewnętrzny w hello takie same w chmurze, gdzie masz również odbiornik wewnętrznej przy użyciu usługi hello wewnętrznego modułu równoważenia obciążenia (ILB).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Ustalić dostępność hello hello odbiornika
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Ten artykuł skupia się na utworzenie odbiornika, który używa **równoważenia obciążenia zewnętrznych**. Jeśli odbiornik, który jest wirtualnej sieci prywatnej tooyour, zobacz hello wersję tego artykułu, który zawiera kroki tworzenia [odbiornik o ILB](../classic/ps-sql-int-listener.md)

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Tworzyć równoważeniem obciążenia punkty końcowe maszyny Wirtualnej z serwerem bezpośredniego zwrotu
Równoważenie obciążenia zewnętrznych używa hello hello wirtualnej publiczny wirtualny adres IP usługi w chmurze hello hostujący maszyny wirtualne. Nie należy toocreate ani w takim przypadku skonfigurowania funkcji równoważenia obciążenia hello.

Punkt końcowy z równoważeniem obciążenia należy utworzyć dla każdej maszyny Wirtualnej obsługuje replikę Azure. Jeśli masz repliki w wielu regionach, każdej repliki dla tego regionu musi być w hello takie same usługi w chmurze hello tej samej sieci wirtualnej. Repliki tworzenia grupy dostępności, obejmujące wiele regionów platformy Azure wymaga konfigurowania wielu sieci wirtualnych. Aby uzyskać więcej informacji na temat konfigurowania krzyżowego łączność sieci wirtualnej, zobacz [tooVNet Konfigurowanie sieci wirtualnej łączności](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. W hello portalu Azure Przejdź tooeach maszyny Wirtualnej repliki i widoku szczegółów hello hosting.
2. Kliknij przycisk hello **punkty końcowe** kartę hello maszyn wirtualnych.
3. Sprawdź, że hello **nazwa** i **Port publiczny** punktu końcowego odbiornika hello ma toouse nie jest już używany. W poniższym przykładzie hello nazwa hello "MyEndpoint" i hello port jest "1433".
4. Na kliencie lokalnym, Pobierz i zainstaluj [hello najnowsze modułu PowerShell](https://azure.microsoft.com/downloads/).
5. Uruchom **programu Azure PowerShell**. Nowe środowisko PowerShell otwarciu sesji z hello Azure administracyjne moduły załadowane.
6. Uruchom **Get-AzurePublishSettingsFile**. To polecenie cmdlet kieruje tooa przeglądarki toodownload publikowania ustawienia pliku tooa katalogiem lokalnym. Może pojawić się prośba o podanie poświadczeń logowania dla subskrypcji platformy Azure.
7. Uruchom hello **AzurePublishSettingsFile importu** pobranego pliku ustawień publikowania polecenie z hello ścieżka hello:
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    Gdy publikowanie hello jest importowany plik ustawień, można zarządzać subskrypcją platformy Azure w sesji programu PowerShell hello.
    
1. Skopiuj poniższy skrypt programu PowerShell hello w edytorze tekstu i ustaw hello toosuit wartości zmiennych środowiska (wartości domyślne zostały dołączone dla niektórych parametrów). Należy pamiętać, że grupy dostępności obejmuje regiony platformy Azure, należy uruchomić skrypt hello raz w każdym centrum danych dla usługi w chmurze hello i węzły, które znajdują się w tym centrum danych.
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. Po ustawieniu zmienne hello hello kopii skryptu w edytorze tekstu hello do programu Azure PowerShell toorun sesji go. Jeśli nadal wyświetlany jest monit hello >>, wpisz ponownie wprowadź, czy skrypt hello toomake zacznie działać.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Sprawdź, czy KB2854082 jest zainstalowana w razie potrzeby
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Otworzyć porty zapory hello w węzłach grupy dostępności
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Tworzenie odbiornika grupy dostępności hello

Tworzenie odbiornika grupy dostępności hello w dwóch krokach. Najpierw należy utworzyć zasobu klastra punktu dostępu klienta hello i skonfigurować zależności. Po drugie Skonfiguruj zasoby klastra hello przy użyciu programu PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Tworzenie punktu dostępu klienta hello i konfigurowanie hello zależności klastra
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Konfigurowanie zasobów klastra hello w programie PowerShell
1. W programie Równoważenie obciążenia zewnętrznej, należy uzyskać hello publiczny wirtualnego adresu IP usługi w chmurze hello zawierający repliki. Zaloguj się do hello portalu Azure. Przejdź toohello usługi w chmurze zawiera grupy dostępności maszyny Wirtualnej. Otwórz hello **pulpitu nawigacyjnego** widoku.
2. Należy zwrócić uwagę hello adres wyświetlany w obszarze **adres publiczny wirtualnego adresu IP (VIP)**. Jeśli rozwiązanie obejmuje sieci wirtualne, powtórz ten krok dla każdej usługi w chmurze zawiera maszyny Wirtualnej, który hostuje replikę.
3. Na jednym z hello maszyn wirtualnych Skopiuj poniższy skrypt programu PowerShell hello w edytorze tekstu i ustaw zmienne hello toohello wartości, które wcześniej zapisany.
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. Po ustawiono hello zmienne, Otwórz okno programu Windows PowerShell z podwyższonym poziomem uprawnień, a następnie skopiuj skrypt hello w edytorze tekstu hello oraz wkleić do programu Azure PowerShell toorun sesji. Jeśli nadal wyświetlany jest monit hello >>, wpisz ponownie wprowadź, czy skrypt hello toomake zacznie działać.
5. Powtórz te czynności na każdej maszynie Wirtualnej. Ten skrypt konfiguruje hello adresu IP zasobu z adresem IP hello hello usługi w chmurze i ustawia innych parametrów, takich jak port sondy hello. Gdy hello zasobu adres IP jest przełączany w tryb online, mogą następnie odpowiedzieć toohello sondowania na port sondy hello z hello równoważeniem obciążenia punktu końcowego utworzonej wcześniej w tym samouczku.

## <a name="bring-hello-listener-online"></a>Przełącz odbiornika hello w trybie online
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Elementy monitowania
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a>Odbiornik grupy dostępności hello testu (poziomu hello sam sieci wirtualnej)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a>Odbiornik grupy dostępności hello testu (za pośrednictwem hello internet)
Kolejność tooaccess hello odbiornika z hello poza siecią wirtualną, należy korzystać z równoważenia obciążenia zewnętrznego/public, (opisanej w tym temacie) zamiast ILB, która jest tylko do niej dostępu w ramach hello tej samej sieci wirtualnej. W parametrach połączenia hello możesz określić hello nazwa usługi w chmurze. Na przykład, jeśli masz usługi w chmurze o nazwie hello *mycloudservice*, instrukcja sqlcmd hello będzie następujące:

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

Inaczej niż w poprzednim przykładzie hello uwierzytelnianie SQL musi można użyć, ponieważ wywołujący hello nie można używać uwierzytelniania systemu windows za pośrednictwem hello internet. Aby uzyskać więcej informacji, zobacz [zawsze włączonej grupy dostępności w maszynie Wirtualnej platformy Azure: scenariusze łączności klienta](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx). Podczas korzystania z uwierzytelniania SQL, upewnij się, że utworzyć hello tej samej nazwy logowania w obu replikach. Aby uzyskać więcej informacji dotyczących rozwiązywania problemów z logowania z użyciem grup dostępności, zobacz [jak toomap logowania lub użyj zawarte SQL użytkownika tooconnect tooother replik bazy danych i bazy danych tooavailability map](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx).

Jeśli hello zawsze na repliki są w różnych podsieciach, klienci muszą określić **MultisubnetFailover = True** w parametrach połączenia hello. Powoduje to tooreplicas prób połączenia równoległego w różnych podsieciach hello. Należy pamiętać, że taki scenariusz obejmuje między region wdrożenia zawsze włączonej grupy dostępności.

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

