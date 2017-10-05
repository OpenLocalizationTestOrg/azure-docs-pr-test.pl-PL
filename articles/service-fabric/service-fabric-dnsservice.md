---
title: "Usługa Azure Service Fabric DNS | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi dns platformy Service Fabric wykrywania mikrousług z wewnątrz klastra."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/27/2017
ms.author: msfussell
ms.openlocfilehash: 9871bc5aa4e74ab0faef401d67c4e9558eb5e14b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="37491-103">Usługa DNS w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="37491-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="37491-104">Usługa DNS jest opcjonalny systemu usługi można włączyć w klastrze do odnajdywania innych usług za pomocą protokołu DNS.</span><span class="sxs-lookup"><span data-stu-id="37491-104">The DNS Service is an optional system service that you can enable in your cluster to discover other services using the DNS protocol.</span></span>

<span data-ttu-id="37491-105">Wiele usług, zwłaszcza konteneryzowanych usług, może mieć nazwę istniejącego adresu URL, a możliwość rozwiązać je przy użyciu standardowego protokołu DNS (a nie protokołu Naming Service) jest pożądane, szczególnie w scenariuszach "przyrostu i przesunięcia".</span><span class="sxs-lookup"><span data-stu-id="37491-105">Many services, especially containerized services, can have an existing URL name, and being able to resolve them using the standard DNS protocol (rather than the Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="37491-106">Usługa DNS umożliwia mapowanie nazwy DNS na nazwę usługi i dlatego rozpoznać adresów IP punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="37491-106">The DNS service enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="37491-107">Usługa DNS mapuje nazwy DNS nazwy usługi, które z kolei są rozpoznawane przez usługę nazewnictwa do zwracania punktu końcowego usługi.</span><span class="sxs-lookup"><span data-stu-id="37491-107">The DNS service maps DNS names to service names, which in turn are resolved by the Naming Service to return the service endpoint.</span></span> <span data-ttu-id="37491-108">Nazwy DNS dla usługi znajduje się w momencie tworzenia obiektu.</span><span class="sxs-lookup"><span data-stu-id="37491-108">The DNS name for the service is provided at the time of creation.</span></span> 

![Punkty końcowe usługi][0]

## <a name="enabling-the-dns-service"></a><span data-ttu-id="37491-110">Włączanie usługi DNS</span><span class="sxs-lookup"><span data-stu-id="37491-110">Enabling the DNS service</span></span>
<span data-ttu-id="37491-111">Najpierw należy włączyć usługę DNS w klastrze.</span><span class="sxs-lookup"><span data-stu-id="37491-111">First you need to enable the DNS service in your cluster.</span></span> <span data-ttu-id="37491-112">Pobierz szablon dla klastra, który chcesz wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="37491-112">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="37491-113">Można użyć [przykładowy szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) lub Utwórz szablon usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="37491-113">You can either use the [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="37491-114">Można włączyć usługę DNS z następujących kroków:</span><span class="sxs-lookup"><span data-stu-id="37491-114">You can enable the DNS service with the following steps:</span></span>

1. <span data-ttu-id="37491-115">Sprawdź, czy `apiversion` ustawiono `2017-07-01-preview` dla `Microsoft.ServiceFabric/clusters` zasobów i jeśli nie, zaktualizować go jak pokazano w poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="37491-115">Check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in the following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="37491-116">Teraz włączyć usługę DNS przez dodanie poniższego `addonFeatures` sekcji po `fabricSettings` sekcji, jak pokazano w poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="37491-116">Now enable the DNS service by adding the following `addonFeatures` section after the `fabricSettings` section as shown in the following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="37491-117">Po aktualizacji szablonu klastra z poprzednim zmiany ich zastosowania i umożliwić Uaktualnianie ukończone.</span><span class="sxs-lookup"><span data-stu-id="37491-117">Once you have updated your cluster template with the preceding changes, apply them and let the upgrade complete.</span></span> <span data-ttu-id="37491-118">Po wykonaniu tych czynności, usługa systemu DNS uruchamiania w klastrze, który jest nazywany `fabric:/System/DnsService` sekcji usługi systemu w programie Service Fabric explorer.</span><span class="sxs-lookup"><span data-stu-id="37491-118">Once complete, the DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in the Service Fabric explorer.</span></span> 

<span data-ttu-id="37491-119">Alternatywnie można włączyć usługę DNS za pośrednictwem portalu w czasie tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="37491-119">Alternatively, you can enable the DNS service through the portal at the time of cluster creation.</span></span> <span data-ttu-id="37491-120">Usługa DNS można ją włączyć przez zaznaczenie pola wyboru dla `Include DNS service` w `Cluster configuration` menu, jak pokazano na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="37491-120">The DNS service can be enabled by checking the box for `Include DNS service` in the `Cluster configuration` menu as shown in the following screenshot:</span></span>

![Włączanie usługi DNS za pośrednictwem portalu][2]


## <a name="setting-the-dns-name-for-your-service"></a><span data-ttu-id="37491-122">Ustawienie nazwy DNS dla usługi</span><span class="sxs-lookup"><span data-stu-id="37491-122">Setting the DNS name for your service</span></span>
<span data-ttu-id="37491-123">Gdy usługa DNS działa w klastrze, można ustawić nazwy DNS dla usługi deklaratywnie dla usług domyślnych w `ApplicationManifest.xml` lub za pomocą poleceń programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="37491-123">Once the DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in the `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-the-dns-name-for-a-default-service-in-the-applicationmanifestxml"></a><span data-ttu-id="37491-124">Ustawienie nazwy DNS dla usługi domyślne w pliku ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="37491-124">Setting the DNS name for a default service in the ApplicationManifest.xml</span></span>
<span data-ttu-id="37491-125">Otwórz projekt w Visual Studio lub ulubionego edytora, a `ApplicationManifest.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="37491-125">Open your project in Visual Studio, or your favorite editor, and open the `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="37491-126">Przejdź do sekcji domyślnej usługi i dla każdej usługi, dodać `ServiceDnsName` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="37491-126">Go to the default services section, and for each service add the `ServiceDnsName` attribute.</span></span> <span data-ttu-id="37491-127">Poniższy przykład pokazuje, jak ustawić nazwę DNS usługi`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="37491-127">The following example shows how to set the DNS name of the service to `service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="37491-128">Gdy aplikacja jest wdrażana, wystąpienie usługi w programie Service Fabric explorer zawiera nazwę DNS dla tego wystąpienia, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="37491-128">Once the application is deployed, the service instance in the Service Fabric explorer shows the DNS name for this instance, as shown in the following figure:</span></span> 

![Punkty końcowe usługi][1]

### <a name="setting-the-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="37491-130">Ustawienie nazwy DNS dla usługi przy użyciu programu Powershell</span><span class="sxs-lookup"><span data-stu-id="37491-130">Setting the DNS name for a service using Powershell</span></span>
<span data-ttu-id="37491-131">Można ustawić nazwy DNS dla usługi, tworząc go za pomocą `New-ServiceFabricService` środowiska Powershell.</span><span class="sxs-lookup"><span data-stu-id="37491-131">You can set the DNS name for a service when creating it using the `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="37491-132">Poniższy przykład tworzy nową usługę bezstanowych z nazwą DNS`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="37491-132">The following example creates a new stateless service with the DNS name `service1.application1`</span></span>

```powershell
    New-ServiceFabricService `
    -Stateless `
    -PartitionSchemeSingleton `
    -ApplicationName `fabric:/application1 `
    -ServiceName fabric:/application1/service1 `
    -ServiceTypeName Service1Type `
    -InstanceCount 1 `
    -ServiceDnsName service1.application1
```

## <a name="using-dns-in-your-services"></a><span data-ttu-id="37491-133">Przy użyciu systemu DNS w usługach</span><span class="sxs-lookup"><span data-stu-id="37491-133">Using DNS in your services</span></span>
<span data-ttu-id="37491-134">Jeśli wdrożono więcej niż jedna usługa, można znaleźć punktów końcowych z innymi usługami w celu komunikowania się z przy użyciu nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="37491-134">If you deploy more than one service, you can find the endpoints of other services to communicate with  by using a DNS name.</span></span> <span data-ttu-id="37491-135">Usługa DNS ma zastosowanie tylko do usług bezstanowych, ponieważ protokół DNS nie może komunikować się z usługami stanowych.</span><span class="sxs-lookup"><span data-stu-id="37491-135">The DNS service is only applicable to stateless services, since the DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="37491-136">Dla stanowych usług można użyć wbudowanych zwrotny serwer proxy dla połączenia http do wywołania partycji określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="37491-136">For stateful services, you can use the built-in reverse proxy for http calls to call a particular service partition.</span></span>

<span data-ttu-id="37491-137">Poniższy kod przedstawia sposób wywołania innej usługi, która to po prostu wywołanie regularne http, w którym podać port i dowolną ścieżkę opcjonalne jako część adresu URL.</span><span class="sxs-lookup"><span data-stu-id="37491-137">The following code shows how to call another service, which is simply a regular http call where you provide the port and any optional path as part of the URL.</span></span>

```csharp
public class ValuesController : Controller
{
    // GET api
    [HttpGet]
    public async Task<string> Get()
    {
        string result = "";
        try
        {
            Uri uri = new Uri("http://service1.application1:8080/api/values");
            HttpClient client = new HttpClient();
            var response = await client.GetAsync(uri);
            result = await response.Content.ReadAsStringAsync();
            
        }
        catch (Exception e)
        {
            Console.Write(e.Message);
        }

        return result;
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="37491-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="37491-138">Next steps</span></span>
<span data-ttu-id="37491-139">Dowiedz się więcej na temat usługi komunikacji w klastrze z [połączenia i łączyć się z usługami](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="37491-139">Learn more about service communication within the cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
