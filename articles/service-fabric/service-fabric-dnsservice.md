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
# <a name="dns-service-in-azure-service-fabric"></a>Usługa DNS w sieci szkieletowej usług Azure
Hello usługi DNS jest opcjonalny systemu usługi można włączyć w Twojej toodiscover klastra innych usług przy użyciu protokołu DNS hello.

Wiele usług, zwłaszcza konteneryzowanych usług, może mieć nazwę istniejącego adresu URL i jest w stanie tooresolve je przy użyciu standardowego protokołu DNS hello (zamiast protokołu Naming Service hello) jest pożądane, szczególnie w scenariuszach "przyrostu i przesunięcia". Hello usługi DNS umożliwia możesz toomap nazwy tooa usługi nazwy DNS i dlatego rozpoznać adresów IP punktu końcowego. 

Witaj usługi DNS mapuje nazwy tooservice nazwy DNS, które z kolei są rozpoznawane przez punkt końcowy usługi hello hello Naming Service tooreturn. nazwy DNS Hello hello usługi znajduje się na powitania godzina utworzenia. 

![Punkty końcowe usługi][0]

## <a name="enabling-hello-dns-service"></a>Włączanie usługi DNS hello
Najpierw należy usługa DNS hello tooenable w klastrze. Pobierz szablon hello hello klastra, które mają toodeploy. Można albo użyj hello [przykładowy szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) lub Utwórz szablon usługi Resource Manager. Można włączyć usługę DNS hello z hello następujące kroki:

1. Sprawdź, że hello `apiversion` ustawiono zbyt`2017-07-01-preview` dla hello `Microsoft.ServiceFabric/clusters` zasobów i jeśli nie, zaktualizować go pokazane na powitania po fragment kodu:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Teraz włączyć hello usługi DNS, dodając następujące hello `addonFeatures` sekcji po hello `fabricSettings` sekcji pokazane na powitania po fragment kodu: 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. Po aktualizacji szablonu klastra z hello poprzedzających zmiany ich zastosowania i umożliwić hello Ukończono uaktualnianie. Po wykonaniu tych czynności hello usługi systemu DNS uruchamiania w klastrze, który jest nazywany `fabric:/System/DnsService` sekcji usługi systemu w hello Service Fabric explorer. 

Alternatywnie można włączyć hello usługi DNS za pośrednictwem portalu hello w czasie hello tworzenia klastra. Hello usługi DNS, można ją włączyć przez zaznaczenie pola wyboru powitania dla `Include DNS service` w hello `Cluster configuration` menu, jak pokazano w powitania po zrzut ekranu:

![Włączanie usługi DNS za pośrednictwem portalu hello][2]


## <a name="setting-hello-dns-name-for-your-service"></a>Ustawianie hello nazwy DNS dla usługi
Po hello usługa DNS działa w klastrze, można ustawić nazwy DNS dla usługi deklaratywnie dla usług domyślnych w hello `ApplicationManifest.xml` lub za pomocą poleceń programu Powershell.

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a>Nazwa DNS hello usługi domyślne ustawienia w pliku ApplicationManifest.xml hello
Otwórz projekt w programie Visual Studio lub ulubionego edytora, a hello `ApplicationManifest.xml` pliku. Przejdź do sekcji usługi domyślne toohello i dla każdej usługi Dodaj hello `ServiceDnsName` atrybutu. Witaj poniższy przykład pokazuje, jak tooset hello nazwę DNS usługi hello zbyt`service1.application1`

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
Po wdrożeniu aplikacji hello wystąpienie usługi hello w hello Eksploratora usługi sieć szkieletowa przedstawia hello nazwy DNS dla tego wystąpienia, pokazane na następującej ilustracji hello: 

![Punkty końcowe usługi][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a>Ustawianie hello nazwy DNS dla usługi przy użyciu programu Powershell
Można ustawić hello nazwy DNS dla usługi, tworząc go za pomocą hello `New-ServiceFabricService` środowiska Powershell. Witaj poniższy przykład tworzy nową usługę bezstanowych o nazwie DNS hello`service1.application1`

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

## <a name="using-dns-in-your-services"></a>Przy użyciu systemu DNS w usługach
Jeśli wdrożono więcej niż jedna usługa można znaleźć hello punktów końcowych toocommunicate innych usług z przy użyciu nazwy DNS. Hello usługi DNS jest tylko usług toostateless dotyczy, ponieważ hello protokołu DNS nie może komunikować się z usługami stanowych. Dla stanowych usług można hello wbudowanych zwrotny serwer proxy http wywołania toocall partycji określonej usługi.

Witaj poniższy kod przedstawia sposób toocall innej usługi, która jest po prostu regularne protokołu http wywołać którym podać hello port i dowolną ścieżkę opcjonalne jako część adresu URL hello.

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

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat usługi komunikacji w ramach klastra hello z [połączenia i łączyć się z usługami](service-fabric-connect-and-communicate-with-services.md)

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
