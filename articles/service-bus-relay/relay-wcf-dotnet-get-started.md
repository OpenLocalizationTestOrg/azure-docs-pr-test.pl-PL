---
title: "aaaGet pracę z przekaźników Azure przekazywania WCF w programie .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse WCF przekazywania Azure przekazuje tooconnect dwóch aplikacji udostępnianych w różnych lokalizacjach."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a>Jak toouse WCF przekazywania Azure przekazuje z platformą .NET
W tym artykule opisano, jak toouse hello Azure przekaźnika usługi. Hello przykłady są napisane w języku C# i używają interfejsu API Windows Communication Foundation (WCF) hello z rozszerzeniami zawartymi w hello zestawu usługi Service Bus. Aby uzyskać więcej informacji na temat przekaźnika usługi Azure, zobacz hello [Omówienie przekaźnika usługi Azure](relay-what-is-it.md).

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a>Co to jest przekazywania WCF?

Hello Azure [ *przekazywania WCF* ](relay-what-is-it.md) usługa umożliwia toobuild hybrydowych aplikacji działających w centrum danych Azure i w lokalnym środowisku korporacyjnym. Usługa przekaźnika Hello ułatwia to umożliwiając toosecurely udostępnianie usług Windows Communication Foundation (WCF), które znajdują się w korporacyjnym środowisku sieci toohello chmury publicznej, bez konieczności tooopen połączenia zapory lub wymaganie Infrastruktura sieci firmowej tooa niepożądanych zmian.

![Pojęcia dotyczące przekaźnika WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

Przekaźnik Azure umożliwia toohost usług WCF w istniejącym środowisku korporacyjnym. Następnie można oddelegować nasłuchiwanie przychodzących sesji i żądań toothese usług toohello przekaźnika usługi WCF działającej na platformie Azure. Dzięki temu można tooexpose te kodu tooapplication usługi uruchomione na platformie Azure, lub pracowników toomobile lub środowiskom partnerów w ekstranecie. Przekazywanie umożliwia toosecurely kontroli, kto ma dostęp do tych usług na poziomie szczegółowych. Udostępnia funkcjonalność aplikacji tooexpose wydajny i bezpieczny sposób i dane z istniejących rozwiązań korporacyjnych i korzystanie z zalet go z hello chmury.

W tym artykule opisano, jak toocreate przekazywania Azure toouse usługi sieci web WCF ujawnianej za pomocą powiązania kanału TCP, która implementuje bezpieczną konwersację między dwiema stronami.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a>Pobierz pakiet NuGet usługi Service Bus hello
Witaj [pakietu NuGet usługi Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus) jest hello Najprostszym sposobem tooget hello interfejsu API usługi Service Bus i tooconfigure aplikacji ze wszystkimi zależnościami usługi Service Bus hello. Pakiet NuGet hello tooinstall w projekcie, hello następujące:

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy pozycję **Odwołania**, a następnie kliknij pozycję **Zarządzaj pakietami NuGet**.
2. Wyszukaj "Service Bus" i wybierz hello **Microsoft Azure Service Bus** elementu. Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij hello następujące okno dialogowe:
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a>Udostępnianie i korzystanie z usługi sieci web SOAP w przypadku protokołu TCP
tooexpose istniejącej usługi sieci web WCF SOAP wykorzystania zewnętrznego należy zmiany toohello usługi powiązań i adresów. Może to wymagać pliku konfiguracji tooyour zmiany lub może wymagać zmiany kodu, w zależności od tego, jak możesz mieć i konfigurowana usług WCF. Należy zauważyć, że WCF pozwala toohave wielu punktów końcowych sieci za pośrednictwem hello tę samą usługę, dzięki czemu można zachować istniejące hello wewnętrznych punktów końcowych podczas dodawania punktów końcowych przekazywania dla użytku zewnętrznego dostęp na powitania sam czas.

To zadanie służy do kompilacji prostą usługę WCF i dodawać tooit odbiornika przekazywania. Tym ćwiczeniu przyjęto założenie, masz pewną znajomość programu Visual Studio i w związku z tym nie omówiono wszystkich szczegółów hello tworzenia projektu. Zamiast tego należy go koncentruje się na powitania kodu.

Przed rozpoczęciem tych kroków, wykonaj następujące procedury tooset Twojego środowiska hello:

1. W programie Visual Studio Utwórz aplikację konsoli, która zawiera dwa projekty — "Client" i "Usługa", w ramach rozwiązania hello.
2. Dodawanie projektów tooboth pakietu NuGet usługi Service Bus hello. Ten pakiet dodaje wszystkie projekty tooyour hello zestawu niezbędne odwołania.

### <a name="how-toocreate-hello-service"></a>Jak toocreate hello usługi
Najpierw należy utworzyć samą usługę hello. Każda usługa WCF składa się z co najmniej trzech oddzielnych części:

* Definicja kontraktu, który opisuje jakie komunikaty są wymieniane i jakie operacje są wywoływane toobe.
* Implementacja tej Umowy.
* Host, który obsługuje usługę WCF hello i udostępnia kilka punktów końcowych.

Witaj przykłady kodu w tej sekcji dotyczą każdego z tych składników.

Witaj kontrakt definiuje jedną operację `AddNumbers`, która dodaje dwie liczby i zwraca wynik hello. Witaj `IProblemSolverChannel` interfejs umożliwia powitania klienta toomore łatwe zarządzanie czasem życia powitania serwera proxy. Utworzenie takiego interfejsu jest traktowane jako najlepsze rozwiązanie. Jest tooput dobrze tego kontraktu definicji w osobnym pliku, dzięki czemu możesz odwoływać ten plik z projektów obu "Client" i "Usługa", ale można również skopiować kod hello do obu tych projektów.

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

Z kontraktem hello w miejscu implementacja hello jest następujący:

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a>Programowe konfigurowanie hosta usługi
Hello kontrakt i implementacja są na miejscu można hostować hello usługi. Hosting następuje wewnątrz [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) obiektu, który zajmuje się zarządzaniem wystąpieniami usługi hello i hosty hello punkty końcowe nasłuchujące komunikatów. Hello poniższy kod umożliwia skonfigurowanie usługi hello zarówno standardowym lokalnym punktem końcowym i przekazywania punktu końcowego tooillustrate hello wyglądu, obok siebie, wewnętrznych i zewnętrznych punktów końcowych. Zastąp ciąg hello *przestrzeni nazw* z przestrzeni nazw i *yourKey* za hello klucza sygnatury dostępu Współdzielonego uzyskanym w poprzednim kroku konfiguracji hello.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

W przykładzie hello utworzysz dwa punkty końcowe, które znajdują się na powitania sam kontraktu implementacji. Jeden jest lokalny, a drugi jest rzutowany za pośrednictwem przekaźnika usługi Azure. Witaj podstawowe różnice między nimi są powiązania hello; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) dla hello lokalna i [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) dla punktu końcowego przekazywania hello i hello adresów. Witaj lokalny punkt końcowy ma adres sieci lokalnej z unikatowym portem. Witaj przekazywania punkt końcowy ma adres złożony z ciągu hello `sb`, przestrzeni nazw, a hello ścieżki "solver". Powoduje to hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identyfikowanie punktu końcowego usługi hello jako punktu końcowego TCP usługi Service Bus (przekaźnik) z w pełni kwalifikowana nazwa zewnętrzna DNS. Jeśli umieścisz kod hello, zastępując symbole zastępcze hello na powitania `Main` funkcja hello **usługi** aplikacji, konieczne będzie funkcjonalności usługi. Jeśli chcesz, aby Twoje toolisten usługi wyłącznie na powitania przekazywania, Usuń deklarację lokalnego punktu końcowego hello.

### <a name="configure-a-service-host-in-hello-appconfig-file"></a>Konfigurowanie hosta usługi w pliku App.config hello
Można również skonfigurować hosta hello przy użyciu pliku App.config hello. Kod hostowania w tym przypadku usługi Hello pojawia się w następnym przykładzie hello.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

definicje punktu końcowego Hello Przenieś do pliku App.config hello. Hello pakiet NuGet już dodał szereg definicji toohello pliku App.config, które są hello wymagane rozszerzenia konfiguracji dla przekaźnika usługi Azure. Witaj następujący przykład, który jest dokładny hello odpowiednikiem poprzedniego kodu hello, powinien pojawić się bezpośrednio pod hello **system.serviceModel** elementu. Ten przykład kodu zakłada, że przestrzeń nazw języka C# w Twoim projekcie ma nazwę **Service**.
Zastąp symbole zastępcze hello z przekaźnika przestrzeni nazw i klucza sygnatury dostępu Współdzielonego.

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

Po wprowadzeniu tych zmian usługa hello jest uruchamiana tak jak poprzednio, ale z dwoma aktywnymi punktami końcowymi: jednym lokalnym i jednym nasłuchującym w chmurze hello.

### <a name="create-hello-client"></a>Utwórz powitania klienta
#### <a name="configure-a-client-programmatically"></a>Programowe konfigurowanie klienta
tooconsume hello usługi, można utworzyć klienta WCF, za pomocą [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) obiektu. Usługa Service Bus używa opartego na tokenie modelu zabezpieczeń, który jest implementowany z użyciem sygnatury dostępu współdzielonego. Witaj [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) klasa reprezentuje dostawcę tokenu zabezpieczającego z wbudowanymi metodami factory zwracających niektórych dobrze znanych dostawców tokenu. Witaj poniższym przykładzie użyto hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) metody toohandle hello nabycie hello odpowiedniego tokenu sygnatury dostępu Współdzielonego. Witaj, nazwa i klucz są uzyskiwane z portalu hello zgodnie z opisem w poprzedniej sekcji hello.

Pierwszy, odniesienia lub kopia hello `IProblemSolver` kontraktu kodu z hello usługi do projektu client.

Następnie należy zastąpić kod hello w hello `Main` metody powitania klienta, ponownie zastępując tekst zastępczy hello przestrzeni nazw przekazywania i klucza sygnatury dostępu Współdzielonego.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

Teraz można tworzyć powitania klienta i hello usługę, uruchomić je (najpierw uruchomić usługę hello), powitania klienta i wywołuje usługę hello drukuje **9**. Można uruchomić powitania klienta i serwera na różnych maszynach, nawet za pośrednictwem sieci, a komunikacja hello będą nadal działać. Kod klienta Hello można również uruchomić w chmurze hello lub lokalnie.

#### <a name="configure-a-client-in-hello-appconfig-file"></a>Konfigurowanie klienta w pliku App.config hello
Witaj następującego kodu pokazuje, jak tooconfigure powitania klienta przy użyciu hello pliku App.config.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

definicje punktu końcowego Hello Przenieś do pliku App.config hello. Witaj poniższy przykład, który jest hello taki sam jak hello kod przedstawiony poprzednio, powinien pojawić się bezpośrednio pod hello `<system.serviceModel>` elementu. W tym miejscu jak poprzednio, należy zastąpić symbole zastępcze hello przekazywania przestrzeni nazw i klucza sygnatury dostępu Współdzielonego.

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello Azure przekazywania, wykonaj te więcej toolearn łącza.

* [Co to jest usługa Azure Relay?](relay-what-is-it.md)
* [Omówienie architektury usługi Azure Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* Pobierz przykłady usługi Service Bus z [przykładów dla platformy Azure] [ Azure samples] lub zobacz hello [Przegląd przykładów usługi Service Bus][overview of Service Bus samples].

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
