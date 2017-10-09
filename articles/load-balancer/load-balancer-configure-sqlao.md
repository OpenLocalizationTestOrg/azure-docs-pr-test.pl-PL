---
title: "dla bazy danych SQL zawsze włączone, usługi równoważenia obciążenia aaaConfigure | Dokumentacja firmy Microsoft"
description: "Skonfiguruj toowork usługi równoważenia obciążenia z na zawsze SQL i jak Implementacja SQL hello usługę równoważenia obciążenia tooleverage toocreate programu powershell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a>Konfigurowanie usługi równoważenia obciążenia dla bazy danych SQL zawsze na

Obecnie można uruchomić z ILB grup dostępności AlwaysOn programu SQL Server. Grupa dostępności jest rozwiązania najważniejszych programu SQL Server, aby uzyskać wysoką dostępność i odzyskiwanie po awarii. Witaj odbiornika grupy dostępności zezwala aplikacjom klienckim tooseamlessly połączyć toohello repliki podstawowej, niezależnie od hello liczby replik hello w konfiguracji hello.

Hello nazwa odbiornika (DNS) jest adresem IP zamapowanych tooa równoważeniem obciążenia i modułowi równoważenia obciążenia Azure kieruje hello przychodzącego ruchu tooonly hello podstawowy serwer hello zestawu replik.

Obsługa ILB można użyć dla punktów końcowych AlwaysOn programu SQL Server (odbiornika). Teraz kontrolują dostępność hello odbiornika hello i można wybrać adres IP z równoważeniem obciążenia hello określonej podsieci w sieci wirtualnej (VNet).

Przy użyciu ILB na powitania odbiornika, hello punkt końcowy serwera SQL (np. serwera = tcp:ListenerName, 1433; baza danych = DatabaseName) jest dostępny tylko dla:

* Usług i maszyn wirtualnych w tej samej sieci wirtualnej hello
* Usług i maszyn wirtualnych z sieci połączonych lokalnie
* Usług i maszyn wirtualnych z połączonych sieci wirtualnych

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

Rysunek 1 — skonfigurowana z modułem równoważenia obciążenia internetowy funkcji SQL AlwaysOn

## <a name="add-internal-load-balancer-toohello-service"></a>Dodawanie usługi toohello wewnętrzny moduł równoważenia obciążenia

1. Poniższy przykład hello możemy konfigurowania w sieci wirtualnej, która zawiera podsieć o nazwie "Podsieć 1":

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. Dodawanie punktów końcowych ze zrównoważonym obciążeniem dla ILB na każdej maszynie Wirtualnej

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    W powyższym przykładzie hello, masz 2 maszyny Wirtualnej o nazwie "sqlsvc1" i "sqlsvc2" działa w chmurze hello usługi "Sqlsvc". Po utworzeniu hello ILB z `DirectServerReturn` przełącznika, możesz dodać punktów końcowych ze zrównoważonym toohello ILB tooallow SQL tooconfigure hello odbiorników dla grup dostępności hello obciążenia.

Aby uzyskać więcej informacji o funkcji SQL AlwaysOn, zobacz [skonfigurować wewnętrzny moduł równoważenia obciążenia dla grupy dostępności AlwaysOn w usłudze Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

## <a name="see-also"></a>Zobacz też
[Przed rozpoczęciem konfigurowania internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md)

[Przed rozpoczęciem konfigurowania wewnętrznego modułu równoważenia obciążenia](load-balancer-get-started-ilb-arm-ps.md)

[Configure a Load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
