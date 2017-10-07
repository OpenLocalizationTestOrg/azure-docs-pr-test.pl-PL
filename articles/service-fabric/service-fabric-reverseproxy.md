---
title: "aaaAzure sieci szkieletowej usług odwrotny serwer proxy | Dokumentacja firmy Microsoft"
description: "Użyj usługi sieć szkieletowa zwrotnego serwera proxy dla toomicroservices komunikacji z wewnętrznych i zewnętrznych klastra hello."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a>Zwrotny serwer proxy w sieci szkieletowej usług Azure
Witaj zwrotnego serwera proxy, wbudowanego w sieci szkieletowej usług Azure adresów mikrousług w klastrze usługi sieć szkieletowa hello, który udostępnia punktów końcowych HTTP.

## <a name="microservices-communication-model"></a>Model komunikacji Mikrousług
Mikrousług w sieci szkieletowej usług zwykle Uruchom w podzestawie maszyny wirtualne w klastrze hello i można przenosić od jednego tooanother maszyny wirtualnej z różnych przyczyn. Tak hello punktów końcowych mikrousług można zmienić dynamicznie. Witaj typowy wzorzec toocommunicate toohello mikrousługi znajduje się poniżej hello rozwiązać pętli:

1. Rozwiązania lokalizacji usługi hello początkowo za pośrednictwem usługi nazewnictwa hello.
2. Usługa toohello Connect.
3. Określić hello przyczyny błędów połączenia i rozpoznać lokalizacji usługi hello ponownie, gdy jest to konieczne.

Ten proces obejmuje zwykle zawijania biblioteki klienta komunikacji w pętli ponawiania implementujący hello usługi zasady rozwiązania i spróbuj ponownie.
Aby uzyskać więcej informacji, zobacz [Connect i łączyć się z usługami](service-fabric-connect-and-communicate-with-services.md).

### <a name="communicating-by-using-hello-reverse-proxy"></a>Komunikacja za pomocą hello zwrotnego serwera proxy
we wszystkich węzłach klastra hello hello jest uruchamiany Hello zwrotnego serwera proxy w sieci szkieletowej usług. Wykonuje proces rozpoznawania całej usługi hello w imieniu klienta, a następnie przesyła dalej żądanie klienta hello. Tak uruchomić w klastrze hello klienci mogą używać dowolnego klienta HTTP komunikacji bibliotek tootalk toohello usługi docelowej, przy użyciu zwrotnego serwera proxy hello czy działa lokalnie na hello na tym samym węźle.

![Wewnętrznej komunikacji][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a>Osiągnięcia mikrousług z zewnątrz hello klastra
Hello domyślny model komunikacji zewnętrznej mikrousług to model opcjonalnych, gdzie każdego nie można uzyskać dostępu do usługi bezpośrednio z klientami zewnętrznymi. [Moduł równoważenia obciążenia Azure](../load-balancer/load-balancer-overview.md), który jest granicę sieci między mikrousług i klientami zewnętrznymi, wykonuje translatora adresów sieciowych i zewnętrzne przekazuje żądania punkty końcowe IP:port toointernal. toomake mikrousługi punktu końcowego tooexternal dostępny bezpośrednio klientów, należy najpierw skonfigurować port tooforward tooeach ruchu, który hello usługi używa modułu równoważenia obciążenia w klastrze hello. Ponadto większość mikrousług, szczególnie stanowe mikrousług, nie na żywo na wszystkich węzłach klastra hello. Witaj mikrousług można przenosić między węzłami w tryb failover. W takich przypadkach usługi równoważenia obciążenia skutecznie nie można określić lokalizacji hello węzła docelowego hello toowhich replik hello przekazywała ruchu.

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a>Osiągnięcia mikrousług za pośrednictwem hello zwrotny serwer proxy z poza hello klastra
Zamiast konfigurować hello port poszczególnych usług w usłudze równoważenia obciążenia, można skonfigurować tylko hello portu hello zwrotnego serwera proxy w usłudze równoważenia obciążenia. Taka konfiguracja pozwala klientom poza klastrem hello reach usługi wewnątrz klastra hello przy użyciu zwrotnego serwera proxy hello bez dodatkowej konfiguracji.

![Komunikacji zewnętrznej][0]

> [!WARNING]
> Po skonfigurowaniu port proxy odwrotnej hello w usłudze równoważenia obciążenia wszystkie mikrousług hello klastra, które udostępniają punkt końcowy HTTP adresowane z poza hello klastra.
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a>Format identyfikatora URI do adresowania usług przy użyciu zwrotnego serwera proxy hello
Witaj zwrotnego serwera proxy jest używana powinny zostać przekazane określonych uniform resource identifier (URI) format tooidentify hello partycji toowhich hello przychodzącego żądania obsługi:

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* **http (s):** hello zwrotny serwer proxy może być skonfigurowany tooaccept HTTP lub ruchu HTTPS. Przekazywanie protokołu HTTPS, można znaleźć zbyt[uzyskuj Usługa bezpiecznego tooa hello zwrotnego serwera proxy](service-fabric-reverseproxy-configure-secure-communication.md) po toolisten Instalatora zwrotnego serwera proxy w protokole HTTPS.
* **Klaster pełną nazwę domeny (FQDN) | wewnętrznym adresem IP:** dla klientów zewnętrznych, można skonfigurować hello zwrotnego serwera proxy, aby był dostępny za pośrednictwem hello klastra domeny, na przykład mycluster.eastus.cloudapp.azure.com. Domyślnie program hello zwrotnego serwera proxy jest uruchamiany na każdym węźle. Dla wewnętrznej ruchu hello zwrotny serwer proxy można połączyć się z hosta lokalnego lub na dowolny węzeł wewnętrzny adres IP, np. 10.0.0.1.
* **Port:** jest to, że jest to port hello, na przykład 19081, który został określony dla zwrotnego serwera proxy hello.
* **ServiceInstanceName:** jest hello Pełna nazwa wystąpienia usługi hello wdrożone próbujesz tooreach bez hello "fabric: /" schematu. Na przykład tooreach hello *fabric: / myapp/Moja_usługa/* usługi, należy użyć *myapp/Moja_usługa*.

    Nazwa wystąpienia usługi Hello jest rozróżniana wielkość liter. Przy użyciu innej wielkości znaków dla nazwy wystąpienia usługi hello w adresie URL hello powoduje toofail żądań hello z 404 (nie znaleziono).
* **Sufiks ścieżki:** to hello rzeczywiste ścieżki adresu URL, takie jak *myapi/wartości/Dodaj/3*, dla hello interesujące tooconnect do usługi.
* **PartitionKey:** usługi podzielonym na partycje, jest to klucz obliczanej partycji hello hello partycji, które mają tooreach. Należy pamiętać, że jest to *nie* hello identyfikator GUID partycji. Ten parametr nie jest wymagana w przypadku usług korzystających z schemat partycji singleton hello.
* **PartitionKind:** to schemat partycji usługi hello. Może to być "Int64Range" lub "O nazwie". Ten parametr nie jest wymagana w przypadku usług korzystających z schemat partycji singleton hello.
* **ListenerName** punkty końcowe hello z usługi hello są formularza hello {"Punkty końcowe": {"Listener1": "Punk końcowy 1", "Listener2": "Punk końcowy 2"...}}. Gdy usługa hello udostępnia wiele punktów końcowych, identyfikuje punkt końcowy hello tego żądania klienta hello powinny zostać przekazane. Ten można pominąć w przypadku usługi hello tylko jeden odbiornik.
* **TargetReplicaSelector** Określa jak powinna być zaznaczona hello docelowej repliki lub wystąpienia.
  * W przypadku stanowego usługi docelowej hello hello TargetReplicaSelector może być jedną z następujących hello: "PrimaryReplica", "RandomSecondaryReplica" lub "RandomReplica". Jeśli ten parametr nie jest określony, hello domyślną jest "PrimaryReplica".
  * Gdy Usługa docelowa hello jest bezstanowych, zwrotny serwer proxy wybiera losowe wystąpienie hello partycji tooforward hello żądanie usługi.
* **Limit czasu:** określa hello przekroczenia limitu czasu dla żądania hello HTTP utworzonych przez usługę toohello zwrotny serwer proxy hello imieniu hello żądania klienta. Witaj, wartość domyślna to 60 sekund. Jest to parametr opcjonalny.

### <a name="example-usage"></a>Przykład użycia
Na przykład Przyjrzyjmy hello *fabric: / MyApp/Moja_usługa* usługi, która otwiera odbiornik HTTP na powitania następującego adresu URL:

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

Poniżej przedstawiono zasoby hello hello usługi:

* `/index.html`
* `/api/users/<userId>`

Jeśli usługa hello używa singleton hello schemat partycjonowania, hello *PartitionKey* i *PartitionKind* parametrów ciągu zapytania nie są wymagane, a usługa hello jest osiągalna przy użyciu bramy hello jako:

* Zewnętrznie:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`
* Wewnętrznie:`http://localhost:19081/MyApp/MyService`

Jeśli usługa hello używa hello Int64 jednolity schemat partycjonowania, hello *PartitionKey* i *PartitionKind* parametrów ciągu zapytania musi być używane tooreach partycji usługi hello:

* Zewnętrznie:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`
* Wewnętrznie:`http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`

tooreach hello zasobów, które udostępnia usługi hello, po prostu umieść ścieżka zasobu powitania po nazwie usługi hello w adresie URL hello:

* Zewnętrznie:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`
* Wewnętrznie:`http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`

Hello bramy następnie przekazuje te żądania usługi toohello adresu URL:

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a>Specjalnej obsługi podczas udostępniania portów usług
Bramy aplikacji Azure prób tooresolve usługą adresów ponownie i ponów żądanie hello, gdy nie można nawiązać połączenia usługi. Jest główną zaletą bramy aplikacji, ponieważ kod klienta nie jest potrzebne tooimplement własnej rozdzielczości usługi rozwiązać pętli.

Ogólnie rzecz biorąc gdy nie można połączyć się z usługą, wystąpienie usługi hello lub repliki został przeniesiony tooa innego węzła w ramach jego normalnej cyklu życia. W takim przypadku bramy aplikacji może pojawić się sieci połączenia błąd wskazujący, że punkt końcowy, bez otwartego dłużej na powitania pierwotnie rozpoznać adres.

Jednak repliki lub wystąpień usługi można udostępniać procesu hosta i może również udostępniać port obsługiwanych przez serwer sieci web opartych na pliku http.sys w tym:

* [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [WebListener platformy ASP.NET Core](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [Katana](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

W takim przypadku prawdopodobnie tego serwera sieci web hello jest dostępne w hello procesu hosta i odpowiada toorequests, ale hello rozpoznać wystąpienia usługi lub replika nie jest już dostępny na hoście hello. W takim przypadku hello bramy z serwera sieci web hello otrzyma odpowiedzi HTTP 404. W związku z tym HTTP 404 ma dwa różne znaczenie:

- Wielkość liter #1: adres usługi hello jest poprawna, ale nie istnieje zasób hello hello żądanego użytkownika.
- Przypadek #2: adres usługi hello jest nieprawidłowa, i zasobu hello hello żądanego użytkownika może istnieć na inny węzeł.

pierwszym przypadku Hello jest normalne 404 protokołu HTTP, która jest uznawana za błąd użytkownika. Jednak w drugim przypadku hello hello użytkownik zażądał z zasobem, który istnieje. Brama aplikacji został toolocate, który ponieważ hello samą usługą została przeniesiona. Aplikacji potrzeb tooresolve hello adres bramy ponownie i ponowić żądanie hello.

Brama aplikacji w związku z tym musi toodistinguish sposób, między tymi dwoma przypadkami. toomake, że różnica, wskazówkę z serwera hello jest wymagana.

* Domyślnie bramy aplikacji zakłada przypadku #2 i próbuje ponownie Żądanie hello tooresolve i problem.
* tooApplication przypadku #1 tooindicate bramy, usługa hello powinna zwracać powitania po nagłówka odpowiedzi HTTP:

  `X-ServiceFabric : ResourceNotFound`

Tego nagłówka odpowiedzi HTTP wskazuje normalnej sytuacji HTTP 404, w których hello żądany zasób nie istnieje, a bramy aplikacji nie będzie próbował adres usługi hello tooresolve ponownie.

## <a name="setup-and-configuration"></a>Instalacja i Konfiguracja

### <a name="enable-reverse-proxy-via-azure-portal"></a>Włącz zwrotnego serwera proxy za pośrednictwem portalu Azure

Azure portal udostępnia opcję tooenable zwrotnego serwera proxy podczas tworzenia nowego klastra sieci szkieletowej usług.
W obszarze **klastra tworzenia sieci szkieletowej usług**, krok 2: konfigurację klastra, konfiguracja typu węzła, zaznacz pole wyboru hello zbyt "Włącz zwrotnego serwera proxy".
Do konfigurowania bezpiecznej zwrotnego serwera proxy, można określić certyfikat SSL w kroku 3: zbyt zabezpieczeń, konfigurowanie ustawień zabezpieczeń klastra, hello zaznacz pole wyboru "Obejmują certyfikat protokołu SSL dla zwrotnego serwera proxy" i wprowadź szczegóły certyfikatu hello.

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a>Włącz zwrotny serwer proxy przy użyciu szablonów usługi Azure Resource Manager

Można użyć hello [szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable hello zwrotnego serwera proxy w sieci szkieletowej usług dla klastra hello.

Odwołuje się zbyt[skonfigurować HTTPS zwrotnego serwera Proxy w klastrze bezpiecznego](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) dla usługi Azure Resource Manager szablonu przykłady tooconfigure bezpiecznego zwrotny serwer proxy z certyfikatu i obsługa Przerzucanie certyfikatów.

Po pierwsze możesz uzyskać szablon hello hello klastra, które mają toodeploy. Można użyć hello przykładowych szablonów lub utworzyć niestandardowy szablon usługi Resource Manager. Następnie można włączyć hello zwrotny serwer proxy przy użyciu hello następujące kroki:

1. Zdefiniuj port dla zwrotnego serwera proxy hello w hello [sekcji parametrów](../azure-resource-manager/resource-group-authoring-templates.md) hello szablonu.

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. Określ port powitania dla każdego z obiektów nodetype hello w hello **klastra** [sekcji Typ zasobu](../azure-resource-manager/resource-group-authoring-templates.md).

    Hello port jest identyfikowane przez nazwę parametru hello, reverseProxyEndpointPort.

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. tooaddress hello zwrotny serwer proxy z poza hello Azure klastra, skonfigurować zasady modułu równoważenia obciążenia Azure hello hello port, który określono w kroku 1.

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. tooconfigure certyfikatów SSL na porcie powitania dla zwrotnego serwera proxy hello, Dodaj hello certyfikatu toohello ***reverseProxyCertificate*** właściwości w hello **klastra** [sekcji Typ zasobu](../resource-group-authoring-templates.md).

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a>Obsługa certyfikatu zwrotny serwer proxy, który różni się od hello klastra certyfikatu
 Jeśli certyfikat zwrotny serwer proxy hello różni się od hello certyfikatu, który zabezpiecza hello klastra, to hello wcześniej określić certyfikat powinien być zainstalowany na maszynie wirtualnej hello i dodany listy kontroli dostępu toohello (ACL), dzięki czemu można sieci szkieletowej usług do niego dostęp. Można to zrobić w hello **virtualMachineScaleSets** [sekcji Typ zasobu](../resource-group-authoring-templates.md). W przypadku instalacji należy dodać osProfile toohello tego certyfikatu. sekcja rozszerzenia Hello hello szablonu można aktualizować hello certyfikatu w hello listy ACL.

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> Korzystając z certyfikatów, które różnią się od hello klastra certyfikatu tooenable hello zwrotny serwer proxy istniejącego klastra, zainstaluj certyfikat zwrotny serwer proxy hello i zaktualizuj hello listy ACL w klastrze hello, przed włączeniem hello zwrotnego serwera proxy. Zakończenie hello [szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) wdrożenia przy użyciu ustawień hello wymienione wcześniej przed rozpoczęciem wdrażania tooenable hello zwrotny serwer proxy w kroki 1 – 4.

## <a name="next-steps"></a>Następne kroki
* Zobacz przykład protokołu HTTP do komunikacji między usługami w [przykładowy projekt w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Usługa HTTP toosecure przekazywania z hello zwrotnego serwera proxy](service-fabric-reverseproxy-configure-secure-communication.md)
* [Zdalne wywołania procedur z usług zdalnych niezawodne usługi](service-fabric-reliable-services-communication-remoting.md)
* [Interfejs API, który używa OWIN w niezawodnej usługi sieci Web](service-fabric-reliable-services-communication-webapi.md)
* [Komunikacyjny WCF za pomocą niezawodnych usług](service-fabric-reliable-services-communication-wcf.md)
* Opcje konfiguracji dodatkowych zwrotnego serwera proxy, można znaleźć w części bramy aplikacji/Http [ustawienia klastra dostosować sieci szkieletowej usług](service-fabric-cluster-fabric-settings.md).

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
