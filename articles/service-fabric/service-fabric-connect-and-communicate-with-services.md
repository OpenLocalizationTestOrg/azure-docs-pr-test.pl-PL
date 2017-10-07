---
title: "aaaConnect i komunikować się z usługami w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak połączyć tooresolve i komunikować się z usługami w sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>Połącz i łączyć się z usługami w sieci szkieletowej usług
W sieci szkieletowej usług Usługa gdzieś działa w klastrze usługi sieć szkieletowa, zazwyczaj są rozproszone na wielu maszyn wirtualnych. Można ją przenosić z tooanother w jednym miejscu przez właściciela usługi hello lub automatycznie przez sieć szkieletowa usług. Usługi nie są statycznie wiązanej tooa określonego komputera lub adres.

Aplikacji usługi Service Fabric zazwyczaj składa się z wielu różnych usług, w którym każda usługa wykonuje zadanie specjalne. Tych usług może komunikować się z sobą tooform w pełną funkcji, takich jak renderowania różne części aplikacji sieci web. Dostępne są także klienta, które aplikacje łączące tooand łączyć się z usługami. W tym dokumencie omówiono sposób tooset się komunikacji z i od usługi w sieci szkieletowej usług.

Ten film Microsoft Virtual Academy omówiono także komunikacji usługi:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>Przełącz własnego protokołu
Sieć szkieletowa usług ułatwia zarządzanie cyklem życia hello usług, ale nie powoduje decyzje na temat działania usługi. W tym komunikacji. Po otwarciu usługi przez usługi Service Fabric, będący tooset możliwości usługi się punkt końcowy dla przychodzących żądań przy użyciu dowolnego stosu protokołu lub komunikacji ma. Usługa będzie nasłuchiwać zwykłym **IP:port** adresów przy użyciu dowolnego schematu adresowania, takich jak identyfikator URI. Wiele wystąpień usługi lub replik może udostępniać procesu hosta, w którym to przypadku one będzie konieczne toouse różnych portów albo użyj mechanizm współużytkowania portów, takie jak sterownik jądra hello http.sys w systemie Windows. W obu przypadkach musi być unikatowo adresowane każdego wystąpienia usługi lub repliki w ramach procesu hosta.

![Punkty końcowe usługi][1]

## <a name="service-discovery-and-resolution"></a>Odnajdowanie usługi i rozwiązania
W rozproszonym systemie usługi mogą być przenoszone ze tooanother na jednym komputerze wraz z upływem czasu. Może to nastąpić z różnych powodów, takich jak zasób równoważenia uaktualnień, pracy w trybie Failover lub skalowalnych w poziomie. Oznacza to, że adresy punktów końcowych usługi zmienić usługi hello przenosi toonodes z różnymi adresami IP, a może otwierać na różnych portów, jeśli usługa hello używa dynamicznie wybranego portu.

![Dystrybucja usług programu][7]

Sieć szkieletowa usług zapewnia możliwość odnajdywania i rozpoznawania usługi o nazwie hello Naming Service. Witaj Naming Service obsługuje wystąpień usługi o nazwie tabeli, która mapuje adresy punktów końcowych toohello, które one nasłuchiwać. Wszystkie wystąpienia usługi o nazwie w sieci szkieletowej usług mają unikatowe nazwy, reprezentowane jako identyfikatory URI, na przykład `"fabric:/MyApplication/MyService"`. nie zmienia nazwę Hello hello usługi okresu istnienia hello hello usługi, jest tylko adresy punktów końcowych hello, które można zmienić podczas przenoszenia usług. To jest analogiczne toowebsites, gdy mają stałe adresy URL, ale gdzie adresu IP hello mogą ulec zmianie. I podobne tooDNS hello sieci Web, która rozwiązuje adresy tooIP adresów URL witryny sieci Web, usługi Service Fabric ma Rejestrator mapująca adres punktu końcowego tootheir nazwy usługi.

![Punkty końcowe usługi][2]

Rozpoznawanie i łączenie tooservices obejmuje następujące kroki, uruchom w pętli hello:

* **Rozwiąż**: hello punktu końcowego Get, który opublikował usługę z hello Naming Service.
* **Połącz**: Podłączanie usługi toohello niezależnie od protokołu używa w tym punkcie końcowym.
* **Spróbuj ponownie**: próba połączenia może zakończyć się niepowodzeniem dla dowolnej liczby przyczyn, na przykład jeśli hello usługi została przeniesiona, ponieważ adres punktu końcowego hello ostatni czas hello został rozwiązany. W takim przypadku hello poprzedzających rozwiązanie i połączyć kroki należy toobe ponowione, a ten cykl powtarza się do chwili pomyślnego połączenia hello.

## <a name="connecting-tooother-services"></a>Połączenie usług tooother
Łączenie tooeach usług innych wewnątrz klastra zazwyczaj bezpośrednio uzyskać dostęp punkty końcowe hello innych usług ponieważ hello węzłów w klastrze na powitania tej samej sieci lokalnej. toomake jest łatwiejsze tooconnect między usługami, Service Fabric zawiera dodatkowe usługi, które używają hello Naming Service. Usługa DNS i usługa zwrotnego serwera proxy.


### <a name="dns-service"></a>Usługa DNS
Ponieważ wiele usług, zwłaszcza konteneryzowanych usług, może mieć nazwę istniejącego adresu URL, jest w stanie tooresolve je przy użyciu hello standardowy protokół DNS (a nie protokołu Naming Service hello) bardzo wygodny, szczególnie w aplikacji "przyrostu i" scenariusze. Jest to tak, jakie hello usługa DNS ma. Umożliwia możesz toomap nazwy tooa usługi nazwy DNS, a więc rozpoznać adresów IP punktu końcowego. 

Jako hello przedstawiono na poniższym diagramie, hello usługa DNS, jest uruchomiona w klastrze usługi sieć szkieletowa hello, mapuje nazwy tooservice nazwy DNS, które następnie są rozpoznawane przez hello Naming Service tooreturn hello punktu końcowego adresy tooconnect do. nazwy DNS Hello hello usługi znajduje się na powitania godzina utworzenia. 

![Punkty końcowe usługi][9]

Więcej informacji dotyczących sposobu hello toouse usługi DNS, zobacz [usługa DNS w sieci szkieletowej usług Azure](service-fabric-dnsservice.md) artykułu.

### <a name="reverse-proxy-service"></a>Zwrotny serwer proxy usługi
Hello zwrotnego serwera proxy dotyczy usługi w klastrze hello, który ujawnia punktów końcowych HTTP, HTTPS w tym. Hello zwrotnego serwera proxy jest znacznie ułatwione wywołaniem innych usług i formatu identyfikatora URI ich metod przez określony i połączenia uchwytów hello rozwiązać, ponów próbę wykonania kroków wymaganych do toocommunicate jedną usługę przy użyciu innego hello nazw usługi. Innymi słowy ukrywa on hello usługi nazw użytkownika podczas wywoływania metody innych usług, dokonując to prosty jak wywołanie adresu URL.

![Punkty końcowe usługi][10]

Więcej informacji na temat jak toouse hello wstecznego usługi serwera proxy można znaleźć [odwrotny serwer proxy w sieci szkieletowej usług Azure](service-fabric-reverseproxy.md) artykułu.

## <a name="connections-from-external-clients"></a>Połączenia z klientami zewnętrznymi
Łączenie tooeach usług innych wewnątrz klastra zazwyczaj bezpośrednio uzyskać dostęp punkty końcowe hello innych usług ponieważ hello węzłów w klastrze na powitania tej samej sieci lokalnej. W przypadku środowisk jednak klastra może być za modułem równoważenia obciążenia, który przekierowuje ruch przychodzący zewnętrznych za pomocą ograniczonego zestawu portów. W takich przypadkach usługi nadal może komunikować się ze sobą i rozwiązać przy użyciu adresów hello Naming Service, ale dodatkowych czynności musi być podjęte tooallow klientów zewnętrznych tooconnect tooservices.

## <a name="service-fabric-in-azure"></a>Sieć szkieletowa usług na platformie Azure
Klastra sieci szkieletowej usług w usłudze Azure znajduje się za usługą równoważenia obciążenia Azure. Wszystkie ruch zewnętrzny toohello klaster musi przejść przez hello modułu równoważenia obciążenia. Witaj modułu równoważenia obciążenia będzie automatycznie przesyłał dalej ruch ruchu przychodzącego na losowe tooa danego portu *węzła* mający hello otworzyć tego samego portu. Hello modułu równoważenia obciążenia Azure tylko zna porty otwarty na powitania *węzłów*, nie może określić dotyczących otwarte porty przez osobę *usług*.

![Azure topologii równoważenia obciążenia i sieci szkieletowej usług][3]

Na przykład w kolejności tooaccept zewnętrznych ruch na porcie **80**, musi być skonfigurowany hello następujące czynności:

1. Zapisu to usługa, która nasłuchuje na porcie 80. Skonfiguruj port 80 w pliku ServiceManifest.xml hello usługi i otwórz odbiornik usługi hello, na przykład serwer sieci web hostowania samoobsługowego.

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. Tworzenie klastra sieci szkieletowej usług na platformie Azure i określić port **80** jako port punktu końcowego niestandardowych hello typu węzła, który będzie hostem usługi hello. Jeśli masz więcej niż jeden typ węzła, można skonfigurować *ograniczenia umieszczania* na powitania usługi tooensure uruchomieniu na typ węzła hello otworzyć port punktu końcowego niestandardowych hello.

    ![Otwarcie portu dla typu węzła][4]
3. Po utworzeniu klastra hello, skonfiguruj hello Azure usługi równoważenia obciążenia w hello klastra grupy zasobów tooforward ruch na porcie 80. Podczas tworzenia klastra za pośrednictwem portalu Azure hello, to jest automatycznie utworzyć dla każdego portu niestandardowego punktu końcowego, który został skonfigurowany.

    ![Ruch do przodu w hello modułu równoważenia obciążenia Azure][5]
4. Witaj używa modułu równoważenia obciążenia Azure czy toodetermine sondowania lub nie toosend ruchu tooa określonego węzła. Hello sondowania okresowo sprawdza punkt końcowy każdego toodetermine węzła czy odpowiada hello węzła. W przypadku niepowodzenia tooreceive odpowiedzi po skonfigurowaną liczbę razy sondowania hello modułu równoważenia obciążenia hello zatrzymuje wysyłania ruchu toothat węzła. Podczas tworzenia klastra za pośrednictwem portalu Azure hello, badanie automatycznie jest konfigurowane dla poszczególnych portów niestandardowych punktu końcowego, który został skonfigurowany.

    ![Ruch do przodu w hello modułu równoważenia obciążenia Azure][8]

Jest ważne tooremember, który hello modułu równoważenia obciążenia Azure i badania hello tylko wiedzieć o hello *węzłów*, nie hello *usług* uruchomione w węzłach hello. Hello modułu równoważenia obciążenia Azure będą zawsze wysyłały toonodes ruchu, który odpowiada toohello sondowania, więc należy uważać tooensure usługi są dostępne w hello węzłów, które są stanie toorespond toohello sondowania.

## <a name="reliable-services-built-in-communication-api-options"></a>Niezawodnej usługi: Opcje komunikacji wbudowanej interfejsu API
framework niezawodne usługi Hello jest dostarczany z kilku opcji wbudowanych komunikacji. Hello decyzja o tym, które jedną będzie najlepsza zależy od hello wybór hello modelu, hello communication framework i hello programowania usług są napisane w języku programowania.

* **Nie określonego protokołu:** Jeśli nie ma określonego wybór framework komunikacji, ale ma tooget coś do pracy szybko, a następnie jest doskonałym rozwiązaniem hello automatycznie [service remoting](service-fabric-reliable-services-communication-remoting.md), dzięki czemu Wywołanie procedury zdalnej jednoznacznie dla Reliable Services i Reliable Actors. Jest to najprostszy hello i najszybszy sposób tooget wprowadzenie do komunikacji usługi. Service remoting obsługuje rozpoznawanie adresy usługi, połączenia, ponów próbę i obsługa błędów. To jest dostępna dla C# i aplikacji Java.
* **HTTP**: komunikat niezależny od języka HTTP zapewnia wybór standardowych z narzędziami i serwery HTTP dostępne w wielu językach obsługiwanych przez sieć szkieletowa usług. Usługi mogą używać żadnych HTTP stosu, w tym [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) dla aplikacji C#. Klienci napisane w języku C# można wykorzystać hello `ICommunicationClient` i `ServicePartitionClient` klas, natomiast dla języka Java, użyj hello `CommunicationClient` i `FabricServicePartitionClient` klas, [usługi rozdzielczości, połączeń HTTP i ponów próbę wykonania pętli](service-fabric-reliable-services-communication.md).
* **Usługi WCF**: Jeśli istniejący kod, który używa WCF jako platforma sieci komunikacji, a następnie użyć hello `WcfCommunicationListener` powitania po stronie serwera i `WcfCommunicationClient` i `ServicePartitionClient` klasy powitania klienta. To jednak jest dostępna tylko dla aplikacji C# w klastrach z systemem Windows. Aby uzyskać więcej informacji, zobacz ten artykuł [WCF na podstawie wykonania stosu komunikacji hello](service-fabric-reliable-services-communication-wcf.md).

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>Przy użyciu protokołów niestandardowych i innych platform komunikacji
Usługi można użyć protokołu lub framework do komunikacji, czy jest protokołem binarne niestandardowych za pośrednictwem gniazda TCP lub za pośrednictwem przesyłania strumieniowego zdarzenia [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) lub [Centrum IoT Azure](https://azure.microsoft.com/services/iot-hub/). Sieć szkieletowa usług zawiera komunikacji interfejsów API stosu komunikacji, można podłączyć wszystkie hello pracy toodiscover i połączyć jest pobieranej przez użytkownika. Znajduje się w artykule o hello [model komunikacji niezawodnej usługi](service-fabric-reliable-services-communication.md) więcej szczegółów.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello pojęcia i interfejsami API dostępnymi w hello [model komunikacji niezawodnej usługi](service-fabric-reliable-services-communication.md), następnie szybko rozpocząć pracę z [service remoting](service-fabric-reliable-services-communication-remoting.md) lub jak przejść szczegółowe toolearn toowrite odbiornik komunikacji przy użyciu [interfejsu API sieci Web z hosta samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md).

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
