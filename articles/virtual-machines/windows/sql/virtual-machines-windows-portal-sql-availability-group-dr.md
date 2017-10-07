---
title: "aaaSQL odzyskiwania po awarii grup dostępności serwera — maszyny wirtualne Azure - | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak grupa tooconfigure dostępności programu SQL Server na maszynach wirtualnych platformy Azure z repliką w innym regionie."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a>Konfigurowanie zawsze włączonej grupy dostępności na maszynach wirtualnych Azure w różnych regionach

W tym artykule opisano, jak tooconfigure dostępności programu SQL Server zawsze włączone grupy replik na maszynach wirtualnych Azure w lokalizacji zdalnej platformy Azure. Użyj tego odzyskiwania po awarii toosupport konfiguracji.

Ten artykuł dotyczy tooAzure maszyn wirtualnych w trybie Menedżera zasobów.

Witaj poniższej ilustracji przedstawiono typowe wdrożenie grupy dostępności na maszynach wirtualnych Azure:

   ![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

W tym wdrożeniu wszystkie maszyny wirtualne znajdują się w jednym regionie Azure. repliki grupy dostępności Hello może mieć zatwierdzanie synchroniczne z automatycznej pracy awaryjnej na SQL-1 i 2 dla programu SQL. toobuild tej architektury, zobacz [szablonu grupy dostępności lub samouczek](virtual-machines-windows-portal-sql-availability-group-overview.md).

Tej architektury jest narażone toodowntime, gdy hello regionu Azure stanie się niedostępna. tooovercome tę lukę w zabezpieczeniach, Dodaj replikę w innym regionie Azure. Witaj poniższym diagramie przedstawiono wygląd architektura hello:

   ![DR grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

Witaj poprzedni diagram przedstawia nowej maszyny wirtualnej o nazwie SQL 3. SQL 3 jest w innym regionie Azure. SQL 3 jest dodawana toohello klastra pracy awaryjnej systemu Windows Server. SQL 3 może obsługiwać repliki grupy dostępności. Warto zauważyć, że hello region platformy Azure dla programu SQL 3 ma nowego modułu równoważenia obciążenia Azure.

>[!NOTE]
> Zestaw dostępności Azure jest wymagany, gdy hello więcej niż jeden maszyny wirtualnej znajduje się w tym samym regionie. Jeśli tylko jednej maszyny wirtualnej znajduje się w regionie hello, hello zestaw dostępności nie jest wymagane. Maszyny wirtualne można umieścić tylko w zestawie w czasie tworzenia dostępności. Jeśli hello maszyna wirtualna już znajduje się w zestawie dostępności, możesz dodać maszyny wirtualnej do dodatkowej repliki później.

W ramach tej architektury hello repliki w regionie zdalnego hello zwykle skonfigurowano tryb dostępności zatwierdzania asynchronicznego i ręczny tryb pracy awaryjnej.

W przypadku replik grupy dostępności na maszynach wirtualnych Azure w różnych regionach platformy Azure, wymaga każdego regionu:

* Brama sieci wirtualnej
* Połączenie bramy sieci wirtualnej

Witaj poniższym diagramie przedstawiono sposób sieci hello komunikacji między centrami danych.

   ![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
>Taka architektura wiąże się z opłatami za przesyłanie danych wychodzących dla danych replikowanych między regiony platformy Azure. Zobacz [przepustowości ceny](http://azure.microsoft.com/pricing/details/bandwidth/).  

## <a name="create-remote-replica"></a>Utwórz zdalnej repliki

toocreate repliki w centrum danych zdalnych hello następujące kroki:

1. [Tworzenie sieci wirtualnej w obszarze nowe hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

1. [Konfigurowanie połączenia do wirtualnymi przy użyciu portalu Azure hello](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).

   >[!NOTE]
   >W niektórych przypadkach może być toouse PowerShell toocreate hello wirtualnymi do połączenia. Na przykład korzystanie z różnych kont platformy Azure nie można skonfigurować połączenia hello w portalu hello. W takim przypadku wyświetlony [Konfiguruj do wirtualnymi połączenia za pomocą hello portalu Azure](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

1. [Tworzenie kontrolera domeny w obszarze nowe hello](../../../active-directory/active-directory-new-forest-virtual-machine.md).

   Ten kontroler domeny zapewnia uwierzytelnianie, jeśli hello kontrolera domeny w lokacji głównej hello jest niedostępny.

1. [Tworzenie maszyny wirtualnej programu SQL Server w obszarze nowe hello](virtual-machines-windows-portal-sql-server-provision.md).

1. [Utwórz moduł równoważenia obciążenia Azure w sieci hello na powitania nowy region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

   Ten moduł równoważenia obciążenia musi:

   - Można w hello tej samej sieci i podsieci, jak hello nowej maszyny wirtualnej.
   - Ma statyczny adres IP dla odbiornika grupy dostępności hello.
   - Obejmują puli zaplecza, składające się z tylko hello maszyn wirtualnych w tym samym regionie Witaj, jak hello modułu równoważenia obciążenia.
   - Użyj adresu IP określonego toohello sondowania portu TCP.
   - Ma toohello określonej reguły programu SQL Server w hello równoważenia obciążenia tego samego regionu.  

1. [Dodaj klaster pracy awaryjnej toohello funkcji nowy serwer SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

1. [Dołącz hello nowej domeny toohello programu SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

1. [Ustaw toouse konta usługi programu SQL Server hello nowe konto domeny](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).

1. [Dodaj hello nowego programu SQL Server toohello klastra pracy awaryjnej systemu Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).

1. Utwórz zasób adresu IP na powitania klastra.

   Można utworzyć zasobu adresu IP hello w Menedżerze klastra trybu Failover. Kliknij prawym przyciskiem myszy rolę grupy dostępności hello, kliknij przycisk **dodawania zasobów**, **więcej zasobów**i kliknij przycisk **adres IP**.

   ![Utwórz adres IP](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   Ten adres IP należy skonfigurować w następujący sposób:

   - Użyj hello sieci z centrum danych zdalnych hello.
   - Przypisz adres IP hello z hello nowe Azure modułu równoważenia obciążenia. 

1. Na hello nowego programu SQL Server w programie SQL Server Configuration Manager [Włącz zawsze włączone grupy dostępności](http://msdn.microsoft.com/library/ff878259.aspx).

1. [Porty zapory otwarte na hello nowy serwer SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

   numery portów Hello należy tooopen zależą od środowiska. Otwórz porty hello dublowania punktu końcowego i Azure załadować sondy kondycji modułu równoważenia.

1. [Dodaj grupę dostępności toohello repliki na powitania nowy serwer SQL](http://msdn.microsoft.com/library/hh213239.aspx).

   Dla replik w zdalnym regionie Azure należy ustawić dla asynchronicznego replikacji z ręcznego przełączania trybu failover.  

1. Dodaj zasób adresu IP hello jako zależność klastra (Nazwa sieciowa) punktu dostępu klienta odbiornika hello.

   Witaj Poniższy zrzut ekranu przedstawia poprawnego skonfigurowania zasobu klastra adresu IP:

   ![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   >Grupa zasobów klastra Hello zawiera oba adresy IP. Oba adresy IP są zależności dla punktu dostępu klienta odbiornika hello. Użyj hello **lub** operatora w konfiguracji zależności klastra hello.

1. [Ustaw parametry klastra hello w programie PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).

Uruchom skrypt programu PowerShell hello Nazwa sieciowa klastra hello, adres IP i port sondy, skonfigurowanego w module równoważenia obciążenia hello w regionie nowe hello.

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a>Ustaw połączenie dla wielu podsieci

Replika Hello w centrum danych zdalnych hello jest częścią grupy dostępności hello, ale jest w innej podsieci. Jeśli ta replika staje się repliką podstawową hello, limity czasu połączenia aplikacji mogą wystąpić. To zachowanie jest hello identyczny z lokalnej grupy dostępności w ramach wdrożenia wielu podsieci. tooallow połączeń za pośrednictwem aplikacji klienckich, zaktualizuj powitania klienta połączenie lub skonfigurować buforowanie na zasobu nazwy sieciowej klastra hello rozpoznawania nazw.

Najlepiej, zaktualizuj powitania klienta połączenia ciągów tooset `MultiSubnetFailover=Yes`. Zobacz [nawiązywania połączenia z MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).

Jeśli nie można zmodyfikować parametry połączenia hello, można skonfigurować buforowanie rozpoznawania nazw. Zobacz [przekroczeń limitu czasu połączenia w grupie dostępności wielu podsieci](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).

## <a name="fail-over-tooremote-region"></a>Tryb failover tooremote regionu

tootest odbiornika łączności toohello zdalnego regionu, można przełączyć hello repliki toohello zdalnego regionu. Replika hello jest asynchroniczne, pracy awaryjnej jest narażony toopotential utraty danych. toofail za pośrednictwem bez utraty danych, zmień toosynchronous tryb dostępności hello i ustawić tooautomatic tryb pracy awaryjnej hello. Użyj hello następujące kroki:

1. W **Eksplorator obiektów**, Połącz toohello wystąpienie programu SQL Server, który obsługuje replikę podstawową hello.
1. W obszarze **zawsze włączonych grup dostępności**, **grup dostępności**, kliknij prawym przyciskiem myszy tej grupy dostępności i kliknij przycisk **właściwości**.
1. Na powitania **ogólne** w obszarze **replik dostępności**, zestaw hello repliki pomocniczej w hello odzyskiwania po awarii lokacji toouse **zatwierdzania synchronicznego** tryb dostępności i **Automatyczne** tryb pracy awaryjnej.
1. Jeśli masz repliki pomocniczej w tej samej lokacji co repliki podstawowej wysokiej dostępności, ustaw tę replikę za**zatwierdzania asynchronicznego** i **ręcznego**.
1. Kliknij przycisk OK.
1. W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy hello grupy dostępności i kliknij przycisk **Pokaż pulpit nawigacyjny**.
1. Na pulpicie nawigacyjnym hello, sprawdź, że hello synchronizacji repliki w lokacji hello odzyskiwania po awarii.
1. W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy hello grupy dostępności i kliknij przycisk **pracy awaryjnej...** . SQL Server Management Studio otworzy toofail kreatora za pośrednictwem programu SQL Server.  
1. Kliknij przycisk **dalej**i wybierz hello wystąpienia programu SQL Server w lokacji hello odzyskiwania po awarii. Kliknij przycisk **dalej** ponownie.
1. Połącz toohello wystąpienia programu SQL Server w lokacji hello odzyskiwania po awarii i kliknij przycisk **dalej**.
1. Na powitania **Podsumowanie** , sprawdź ustawienia hello i kliknij przycisk **Zakończ**.

Po zakończeniu testowania łączności, przenoszenie danych podstawowych wstecz tooyour repliki podstawowej hello Centrum i ustawienia tootheir wstecz tryb dostępności hello normalnego działania. Hello poniższej tabeli przedstawiono hello normalne ustawienia robocze dotyczące architektury hello opisanych w tym dokumencie:

| Lokalizacja | Wystąpienie serwera | Rola | Tryb dostępności | Tryb pracy awaryjnej
| ----- | ----- | ----- | ----- | -----
| Centrum danych podstawowych | SQL 1 | Podstawowy | Synchroniczne | Automatyczne
| Centrum danych podstawowych | SQL 2 | Pomocniczy | Synchroniczne | Automatyczne
| Centrum danych w dodatkowej lub zdalnego | SQL 3 | Pomocniczy | Asynchroniczne | Ręcznie


### <a name="more-information-about-planned-and-forced-manual-failover"></a>Więcej informacji na temat planowanymi, jak i wymuszonego ręcznego przełączania trybu failover

Aby uzyskać więcej informacji zobacz następujące tematy hello:

- [Wykonaj planowane ręcznego przełączania trybu Failover grupy dostępności (SQL Server)](http://msdn.microsoft.com/library/hh231018.aspx)
- [Wykonaj wymuszonego ręcznego przełączania trybu Failover grupy dostępności (SQL Server)](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a>Linki do dodatkowych

* [Zawsze włączone grupy dostępności](http://msdn.microsoft.com/library/hh510230.aspx)
* [Maszyny wirtualne platformy Azure](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [Moduły równoważenia obciążenia Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [Zestawy dostępności Azure](../manage-availability.md)
