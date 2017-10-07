---
title: "aaaAzure usługi Service Fabric DNS | Dokumentacja firmy Microsoft"
description: "Korzystanie z usługi dns platformy Service Fabric wykrywania mikrousług z wewnątrz hello klastra."
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
ms.openlocfilehash: fa536f0e41f52c4942702d0a1bdcd3ed7d418d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="68dd2-103">Usługa DNS w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="68dd2-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="68dd2-104">Hello usługi DNS jest opcjonalny systemu usługi można włączyć w Twojej toodiscover klastra innych usług przy użyciu protokołu DNS hello.</span><span class="sxs-lookup"><span data-stu-id="68dd2-104">hello DNS Service is an optional system service that you can enable in your cluster toodiscover other services using hello DNS protocol.</span></span>

<span data-ttu-id="68dd2-105">Wiele usług, zwłaszcza konteneryzowanych usług, może mieć nazwę istniejącego adresu URL i jest w stanie tooresolve je przy użyciu standardowego protokołu DNS hello (zamiast protokołu Naming Service hello) jest pożądane, szczególnie w scenariuszach "przyrostu i przesunięcia".</span><span class="sxs-lookup"><span data-stu-id="68dd2-105">Many services, especially containerized services, can have an existing URL name, and being able tooresolve them using hello standard DNS protocol (rather than hello Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="68dd2-106">Hello usługi DNS umożliwia możesz toomap nazwy tooa usługi nazwy DNS i dlatego rozpoznać adresów IP punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="68dd2-106">hello DNS service enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="68dd2-107">Witaj usługi DNS mapuje nazwy tooservice nazwy DNS, które z kolei są rozpoznawane przez punkt końcowy usługi hello hello Naming Service tooreturn.</span><span class="sxs-lookup"><span data-stu-id="68dd2-107">hello DNS service maps DNS names tooservice names, which in turn are resolved by hello Naming Service tooreturn hello service endpoint.</span></span> <span data-ttu-id="68dd2-108">nazwy DNS Hello hello usługi znajduje się na powitania godzina utworzenia.</span><span class="sxs-lookup"><span data-stu-id="68dd2-108">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![Punkty końcowe usługi][0]

## <a name="enabling-hello-dns-service"></a><span data-ttu-id="68dd2-110">Włączanie usługi DNS hello</span><span class="sxs-lookup"><span data-stu-id="68dd2-110">Enabling hello DNS service</span></span>
<span data-ttu-id="68dd2-111">Najpierw należy usługa DNS hello tooenable w klastrze.</span><span class="sxs-lookup"><span data-stu-id="68dd2-111">First you need tooenable hello DNS service in your cluster.</span></span> <span data-ttu-id="68dd2-112">Pobierz szablon hello hello klastra, które mają toodeploy.</span><span class="sxs-lookup"><span data-stu-id="68dd2-112">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="68dd2-113">Można albo użyj hello [przykładowy szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) lub Utwórz szablon usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="68dd2-113">You can either use hello [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="68dd2-114">Można włączyć usługę DNS hello z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="68dd2-114">You can enable hello DNS service with hello following steps:</span></span>

1. <span data-ttu-id="68dd2-115">Sprawdź, że hello `apiversion` ustawiono zbyt`2017-07-01-preview` dla hello `Microsoft.ServiceFabric/clusters` zasobów i jeśli nie, zaktualizować go pokazane na powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="68dd2-115">Check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in hello following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="68dd2-116">Teraz włączyć hello usługi DNS, dodając następujące hello `addonFeatures` sekcji po hello `fabricSettings` sekcji pokazane na powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="68dd2-116">Now enable hello DNS service by adding hello following `addonFeatures` section after hello `fabricSettings` section as shown in hello following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="68dd2-117">Po aktualizacji szablonu klastra z hello poprzedzających zmiany ich zastosowania i umożliwić hello Ukończono uaktualnianie.</span><span class="sxs-lookup"><span data-stu-id="68dd2-117">Once you have updated your cluster template with hello preceding changes, apply them and let hello upgrade complete.</span></span> <span data-ttu-id="68dd2-118">Po wykonaniu tych czynności hello usługi systemu DNS uruchamiania w klastrze, który jest nazywany `fabric:/System/DnsService` sekcji usługi systemu w hello Service Fabric explorer.</span><span class="sxs-lookup"><span data-stu-id="68dd2-118">Once complete, hello DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in hello Service Fabric explorer.</span></span> 

<span data-ttu-id="68dd2-119">Alternatywnie można włączyć hello usługi DNS za pośrednictwem portalu hello w czasie hello tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="68dd2-119">Alternatively, you can enable hello DNS service through hello portal at hello time of cluster creation.</span></span> <span data-ttu-id="68dd2-120">Hello usługi DNS, można ją włączyć przez zaznaczenie pola wyboru powitania dla `Include DNS service` w hello `Cluster configuration` menu, jak pokazano w powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="68dd2-120">hello DNS service can be enabled by checking hello box for `Include DNS service` in hello `Cluster configuration` menu as shown in hello following screenshot:</span></span>

![Włączanie usługi DNS za pośrednictwem portalu hello][2]


## <a name="setting-hello-dns-name-for-your-service"></a><span data-ttu-id="68dd2-122">Ustawianie hello nazwy DNS dla usługi</span><span class="sxs-lookup"><span data-stu-id="68dd2-122">Setting hello DNS name for your service</span></span>
<span data-ttu-id="68dd2-123">Po hello usługa DNS działa w klastrze, można ustawić nazwy DNS dla usługi deklaratywnie dla usług domyślnych w hello `ApplicationManifest.xml` lub za pomocą poleceń programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="68dd2-123">Once hello DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in hello `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a><span data-ttu-id="68dd2-124">Nazwa DNS hello usługi domyślne ustawienia w pliku ApplicationManifest.xml hello</span><span class="sxs-lookup"><span data-stu-id="68dd2-124">Setting hello DNS name for a default service in hello ApplicationManifest.xml</span></span>
<span data-ttu-id="68dd2-125">Otwórz projekt w programie Visual Studio lub ulubionego edytora, a hello `ApplicationManifest.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="68dd2-125">Open your project in Visual Studio, or your favorite editor, and open hello `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="68dd2-126">Przejdź do sekcji usługi domyślne toohello i dla każdej usługi Dodaj hello `ServiceDnsName` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="68dd2-126">Go toohello default services section, and for each service add hello `ServiceDnsName` attribute.</span></span> <span data-ttu-id="68dd2-127">Witaj poniższy przykład pokazuje, jak tooset hello nazwę DNS usługi hello zbyt`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="68dd2-127">hello following example shows how tooset hello DNS name of hello service too`service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="68dd2-128">Po wdrożeniu aplikacji hello wystąpienie usługi hello w hello Eksploratora usługi sieć szkieletowa przedstawia hello nazwy DNS dla tego wystąpienia, pokazane na następującej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="68dd2-128">Once hello application is deployed, hello service instance in hello Service Fabric explorer shows hello DNS name for this instance, as shown in hello following figure:</span></span> 

![Punkty końcowe usługi][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="68dd2-130">Ustawianie hello nazwy DNS dla usługi przy użyciu programu Powershell</span><span class="sxs-lookup"><span data-stu-id="68dd2-130">Setting hello DNS name for a service using Powershell</span></span>
<span data-ttu-id="68dd2-131">Można ustawić hello nazwy DNS dla usługi, tworząc go za pomocą hello `New-ServiceFabricService` środowiska Powershell.</span><span class="sxs-lookup"><span data-stu-id="68dd2-131">You can set hello DNS name for a service when creating it using hello `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="68dd2-132">Witaj poniższy przykład tworzy nową usługę bezstanowych o nazwie DNS hello`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="68dd2-132">hello following example creates a new stateless service with hello DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="68dd2-133">Przy użyciu systemu DNS w usługach</span><span class="sxs-lookup"><span data-stu-id="68dd2-133">Using DNS in your services</span></span>
<span data-ttu-id="68dd2-134">Jeśli wdrożono więcej niż jedna usługa można znaleźć hello punktów końcowych toocommunicate innych usług z przy użyciu nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="68dd2-134">If you deploy more than one service, you can find hello endpoints of other services toocommunicate with  by using a DNS name.</span></span> <span data-ttu-id="68dd2-135">Hello usługi DNS jest tylko usług toostateless dotyczy, ponieważ hello protokołu DNS nie może komunikować się z usługami stanowych.</span><span class="sxs-lookup"><span data-stu-id="68dd2-135">hello DNS service is only applicable toostateless services, since hello DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="68dd2-136">Dla stanowych usług można hello wbudowanych zwrotny serwer proxy http wywołania toocall partycji określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="68dd2-136">For stateful services, you can use hello built-in reverse proxy for http calls toocall a particular service partition.</span></span>

<span data-ttu-id="68dd2-137">Witaj poniższy kod przedstawia sposób toocall innej usługi, która jest po prostu regularne protokołu http wywołać którym podać hello port i dowolną ścieżkę opcjonalne jako część adresu URL hello.</span><span class="sxs-lookup"><span data-stu-id="68dd2-137">hello following code shows how toocall another service, which is simply a regular http call where you provide hello port and any optional path as part of hello URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="68dd2-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68dd2-138">Next steps</span></span>
<span data-ttu-id="68dd2-139">Dowiedz się więcej na temat usługi komunikacji w ramach klastra hello z [połączenia i łączyć się z usługami](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="68dd2-139">Learn more about service communication within hello cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
