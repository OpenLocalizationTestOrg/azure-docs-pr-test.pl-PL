---
title: "aaaCreate internetowy modułu równoważenia obciążenia dla usług w chmurze Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa równoważenia w klasycznym modelu wdrażania usług w chmurze obciążenia toocreate umożliwiających dostęp z Internetu"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a>Wprowadzenie do tworzenia dostępnego z Internetu modułu równoważenia obciążenia do usług w chmurze

> [!div class="op_single_selector"]
> * [Klasyczna witryna Azure Portal](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Przed rozpoczęciem pracy z zasobów platformy Azure, jest ważne toounderstand, że Azure ma obecnie dwa modele wdrażania: usługi Azure Resource Manager i model klasyczny. Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-classic-rm.md). Hello dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty hello u góry hello tego artykułu. W tym artykule omówiono hello klasycznego modelu wdrażania. Możesz również [Dowiedz się, jak usługa równoważenia przy użyciu usługi Azure Resource Manager obciążenia toocreate Internetem](load-balancer-get-started-internet-arm-ps.md).

Usługi w chmurze są automatycznie konfigurowane z modułem równoważenia obciążenia i można dostosować za pomocą modelu usługi hello.

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a>Tworzenie przy użyciu pliku definicji usługi hello modułu równoważenia obciążenia

Można wykorzystać hello Azure SDK dla platformy .NET 2.5 tooupdate usługi w chmurze. Ustawienia punktu końcowego usługi w chmurze zostały wprowadzone w hello [definicji usługi](https://msdn.microsoft.com/library/azure/gg557553.aspx) plik csdef.

Witaj poniższy przykład przedstawia sposób skonfigurowania plik servicedefinition.csdef do wdrażania chmury:

Sprawdzanie hello fragment pliku csdef hello wygenerowanych przez wdrożenia chmury, widać hello zewnętrznego punktu końcowego skonfigurowane toouse portów HTTP na porcie 10000, 10001 i 10002.

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a>Sprawdzanie kondycji modułu równoważenia obciążenia do usług w chmurze

Witaj, poniżej przedstawiono przykładowy sondy kondycji:

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

Witaj modułu równoważenia obciążenia łączy informacje hello hello punktu końcowego i hello toocreate sondowania hello adres URL w formie hello `http://{DIP of VM}:80/Probe.aspx` które może być używane tooquery hello kondycji hello usługi.

Witaj wykrywany przez usługę okresowe sond z hello tego samego adresu IP. Jest to żądanie sondy kondycji hello pochodzące z hosta hello hello węzła, którym jest uruchomiona maszyna wirtualna hello. Usługa Hello ma toorespond z kodem stanu 200 protokołu HTTP dla tooassume usługi równoważenia obciążenia hello hello usługi jest w dobrej kondycji. Inny stan HTTP kodu (na przykład 503) bezpośrednio przyjmuje hello maszynę wirtualną z obrotu.

Definicja sondowania Hello kontroluje również hello częstotliwość sondowania hello. W naszym przykładzie powyżej hello modułu równoważenia obciążenia jest sondowanie hello punktu końcowego co 5 sekund. Jeśli dodatnią odpowiedzi nie zostanie odebrana na 10 sekund (dwa interwały sondowania), sondy hello zakłada, że w dół, a hello maszyny wirtualnej jest wykluczony z cyklu. Podobnie jeśli usługa hello jest poza obrotu i odebrania odpowiedzi dodatnią, usługa hello jest przywracane toorotation od razu. Jeśli usługa hello jest zmienne między dobrej kondycji i złej kondycji, hello modułu równoważenia obciążenia można określić toodelay hello ponowne wprowadzenie toorotation wstecz hello usługi, dopóki zostanie dobrej kondycji liczbę sond.

Sprawdź hello usługi definicji schematu dla hello [sondy kondycji](https://msdn.microsoft.com/library/azure/jj151530.aspx) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki

[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)

[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)

