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
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="679ad-103">Wprowadzenie do tworzenia dostępnego z Internetu modułu równoważenia obciążenia do usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="679ad-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="679ad-104">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="679ad-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="679ad-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="679ad-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="679ad-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="679ad-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="679ad-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="679ad-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="679ad-108">Przed rozpoczęciem pracy z zasobów platformy Azure, jest ważne toounderstand, że Azure ma obecnie dwa modele wdrażania: usługi Azure Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="679ad-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="679ad-109">Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="679ad-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="679ad-110">Hello dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty hello u góry hello tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="679ad-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="679ad-111">W tym artykule omówiono hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="679ad-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="679ad-112">Możesz również [Dowiedz się, jak usługa równoważenia przy użyciu usługi Azure Resource Manager obciążenia toocreate Internetem](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="679ad-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="679ad-113">Usługi w chmurze są automatycznie konfigurowane z modułem równoważenia obciążenia i można dostosować za pomocą modelu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="679ad-113">Cloud services are automatically configured with a load balancer and can be customized via hello service model.</span></span>

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a><span data-ttu-id="679ad-114">Tworzenie przy użyciu pliku definicji usługi hello modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="679ad-114">Create a load balancer using hello service definition file</span></span>

<span data-ttu-id="679ad-115">Można wykorzystać hello Azure SDK dla platformy .NET 2.5 tooupdate usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="679ad-115">You can leverage hello Azure SDK for .NET 2.5 tooupdate your cloud service.</span></span> <span data-ttu-id="679ad-116">Ustawienia punktu końcowego usługi w chmurze zostały wprowadzone w hello [definicji usługi](https://msdn.microsoft.com/library/azure/gg557553.aspx) plik csdef.</span><span class="sxs-lookup"><span data-stu-id="679ad-116">Endpoint settings for cloud services are made in hello [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="679ad-117">Witaj poniższy przykład przedstawia sposób skonfigurowania plik servicedefinition.csdef do wdrażania chmury:</span><span class="sxs-lookup"><span data-stu-id="679ad-117">hello following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="679ad-118">Sprawdzanie hello fragment pliku csdef hello wygenerowanych przez wdrożenia chmury, widać hello zewnętrznego punktu końcowego skonfigurowane toouse portów HTTP na porcie 10000, 10001 i 10002.</span><span class="sxs-lookup"><span data-stu-id="679ad-118">Checking hello snippet for hello .csdef file generated by a cloud deployment, you can see hello external endpoint configured toouse ports HTTP on port 10000, 10001, and 10002.</span></span>

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

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="679ad-119">Sprawdzanie kondycji modułu równoważenia obciążenia do usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="679ad-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="679ad-120">Witaj, poniżej przedstawiono przykładowy sondy kondycji:</span><span class="sxs-lookup"><span data-stu-id="679ad-120">hello following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="679ad-121">Witaj modułu równoważenia obciążenia łączy informacje hello hello punktu końcowego i hello toocreate sondowania hello adres URL w formie hello `http://{DIP of VM}:80/Probe.aspx` które może być używane tooquery hello kondycji hello usługi.</span><span class="sxs-lookup"><span data-stu-id="679ad-121">hello load balancer combines hello information of hello endpoint and hello information of hello probe toocreate a URL in hello form of `http://{DIP of VM}:80/Probe.aspx` that can be used tooquery hello health of hello service.</span></span>

<span data-ttu-id="679ad-122">Witaj wykrywany przez usługę okresowe sond z hello tego samego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="679ad-122">hello service detects periodic probes from hello same IP address.</span></span> <span data-ttu-id="679ad-123">Jest to żądanie sondy kondycji hello pochodzące z hosta hello hello węzła, którym jest uruchomiona maszyna wirtualna hello.</span><span class="sxs-lookup"><span data-stu-id="679ad-123">This is hello health probe request coming from hello host of hello node where hello virtual machine is running.</span></span> <span data-ttu-id="679ad-124">Usługa Hello ma toorespond z kodem stanu 200 protokołu HTTP dla tooassume usługi równoważenia obciążenia hello hello usługi jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="679ad-124">hello service has toorespond with a HTTP 200 status code for hello load balancer tooassume that hello service is healthy.</span></span> <span data-ttu-id="679ad-125">Inny stan HTTP kodu (na przykład 503) bezpośrednio przyjmuje hello maszynę wirtualną z obrotu.</span><span class="sxs-lookup"><span data-stu-id="679ad-125">Any other HTTP status code (for example 503) directly takes hello virtual machine out of rotation.</span></span>

<span data-ttu-id="679ad-126">Definicja sondowania Hello kontroluje również hello częstotliwość sondowania hello.</span><span class="sxs-lookup"><span data-stu-id="679ad-126">hello probe definition also controls hello frequency of hello probe.</span></span> <span data-ttu-id="679ad-127">W naszym przykładzie powyżej hello modułu równoważenia obciążenia jest sondowanie hello punktu końcowego co 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="679ad-127">In our case above, hello load balancer is probing hello endpoint every 5 secs.</span></span> <span data-ttu-id="679ad-128">Jeśli dodatnią odpowiedzi nie zostanie odebrana na 10 sekund (dwa interwały sondowania), sondy hello zakłada, że w dół, a hello maszyny wirtualnej jest wykluczony z cyklu.</span><span class="sxs-lookup"><span data-stu-id="679ad-128">If no positive answer is received for 10 secs (two probe intervals), hello probe is assumed down, and hello virtual machine is taken out of rotation.</span></span> <span data-ttu-id="679ad-129">Podobnie jeśli usługa hello jest poza obrotu i odebrania odpowiedzi dodatnią, usługa hello jest przywracane toorotation od razu.</span><span class="sxs-lookup"><span data-stu-id="679ad-129">Similarly, if hello service is out of rotation and a positive answer is received, hello service is put back toorotation right away.</span></span> <span data-ttu-id="679ad-130">Jeśli usługa hello jest zmienne między dobrej kondycji i złej kondycji, hello modułu równoważenia obciążenia można określić toodelay hello ponowne wprowadzenie toorotation wstecz hello usługi, dopóki zostanie dobrej kondycji liczbę sond.</span><span class="sxs-lookup"><span data-stu-id="679ad-130">If hello service is fluctuating between healthy and unhealthy, hello load balancer can decide toodelay hello re-introduction of hello service back toorotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="679ad-131">Sprawdź hello usługi definicji schematu dla hello [sondy kondycji](https://msdn.microsoft.com/library/azure/jj151530.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="679ad-131">Check hello service definition schema for hello [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="679ad-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="679ad-132">Next steps</span></span>

<span data-ttu-id="679ad-133">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="679ad-133">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md)</span></span>

<span data-ttu-id="679ad-134">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="679ad-134">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="679ad-135">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="679ad-135">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>

