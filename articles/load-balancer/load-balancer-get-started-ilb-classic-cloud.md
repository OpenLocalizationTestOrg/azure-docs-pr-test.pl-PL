---
title: "Wewnętrzny moduł równoważenia obciążenia dla usług w chmurze Azure aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa równoważenia w hello klasycznego modelu wdrażania przy użyciu programu PowerShell obciążenia toocreate jako wewnętrzne"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>Wprowadzenie do tworzenia wewnętrznego modułu równoważenia obciążenia (klasycznego) dla usług w chmurze

> [!div class="op_single_selector"]
> * [Program PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Usługi w chmurze](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](load-balancer-get-started-ilb-arm-ps.md).

## <a name="configure-internal-load-balancer-for-cloud-services"></a>Konfigurowanie wewnętrznego modułu równoważenia obciążenia dla usług w chmurze

Wewnętrzny moduł równoważenia obciążenia może być zastosowany zarówno do maszyn wirtualnych, jak i usług w chmurze. Punkt końcowy usługi równoważenia obciążenia wewnętrznego utworzone w usłudze w chmurze, który znajduje się poza regionalną sieć wirtualną będzie dostępna tylko w obrębie hello usługi w chmurze.

Konfiguracja usługi równoważenia obciążenia wewnętrznego Hello ma toobe ustawić podczas tworzenia hello hello pierwszym wdrożeniu hello w usłudze w chmurze, jak pokazano w poniższym przykładzie hello.

> [!IMPORTANT]
> Poniższe kroki hello toorun wymagań wstępnych jest toohave sieci wirtualnej już utworzone dla hello wdrożenie chmury. Konieczne będzie hello sieci wirtualnej nazwy i podsieci nazwę toocreate hello wewnętrzne Równoważenie obciążenia sieciowego.

### <a name="step-1"></a>Krok 1

Otwórz plik konfiguracji usługi hello (cscfg) dla danego wdrożenia chmury w programie Visual Studio i Dodaj powitania po ostatniej hello toocreate sekcji wewnętrzne Równoważenie obciążenia sieciowego w obszarze hello "`</Role>`" elementu hello konfiguracji sieci.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Dodajmy hello wartości hello sieci konfiguracji pliku tooshow wyglądu. Przykład Witaj przyjęto założenie, że utworzono sieci wirtualnej o nazwie "test_vnet" z 10.0.0.0/24 podsieci o nazwie test_subnet i statycznego adresu IP 10.0.0.4. Moduł równoważenia obciążenia Hello będzie miała nazwę testLB.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Aby uzyskać więcej informacji o schemacie modułu równoważenia obciążenia hello, zobacz [modułu równoważenia obciążenia Dodaj](https://msdn.microsoft.com/library/azure/dn722411.aspx).

### <a name="step-2"></a>Krok 2

Zmień hello usługi definicji (csdef) pliku tooadd punkty końcowe toohello wewnętrzne Równoważenie obciążenia sieciowego. obecnie Hello utworzeniu wystąpienia roli, pliku definicji usługi hello doda toohello wystąpień roli hello wewnętrzne Równoważenie obciążenia sieciowego.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

Następujące hello takie same wartości w powyższym przykładzie hello możemy dodać pliku definicji usługi hello wartości toohello.

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

ruch sieciowy Hello będzie równoważone za pomocą usługi równoważenia obciążenia testLB hello przy użyciu portu 80 dla żądań przychodzących, wysyłanie tooworker wystąpień roli również na porcie 80.

## <a name="next-steps"></a>Następne kroki

[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia przy użyciu koligacji źródłowych adresów IP)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)

