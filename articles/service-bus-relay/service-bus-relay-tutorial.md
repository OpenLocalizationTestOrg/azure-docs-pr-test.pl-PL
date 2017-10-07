---
title: "Samouczek usługi magistrali usługi WCF przekazywania aaaAzure | Dokumentacja firmy Microsoft"
description: "Tworzenie klienta usługi Service Bus, aplikacji i usług przy użyciu przekaźnika usługi WCF."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a>Samouczek usługi Azure przekaźnika usługi WCF

W tym samouczku opisano, jak toobuild proste WCF przekazywania aplikacji klienckiej i usługi przy użyciu przekaźnika usługi Azure. Aby podobnego samouczka dotyczącego używa [usługi magistrali komunikatów](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), zobacz [Rozpoczynanie pracy z kolejek usługi Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

Ten samouczek umożliwia poznanie kroków hello, które są wymagane toocreate aplikacji klienta i usługi przekaźnika usługi WCF. Podobnie jak ich odpowiedniki WCF oryginalnej usługa jest strukturą ujawniającą jeden lub więcej punktów końcowych, z których każdy ujawnia co najmniej jedną operację usługi. Witaj punkt końcowy usługi Określa adres gdzie można znaleźć usługi hello, powiązanie zawierające informacje powitania klienta muszą komunikować się z usługą hello i kontrakt definiujący hello funkcje udostępniane przez klientów tooits usługi hello. Witaj podstawowa różnica między WCF i przekazywania WCF jest ten punkt końcowy hello jest widoczna w chmurze hello zamiast lokalnie na komputerze.

Po zakończeniu pracy hello sekwencją tematów w tym samouczku, będzie mieć uruchomioną usługę i klienta, który można wywołać operacji hello hello usługi. Witaj w pierwszym temacie opisano sposób tooset konta. Witaj następne kroki opisują sposób toodefine usługi używającej kontraktu, jak tooimplement hello usługi i jak tooconfigure hello usługi w kodzie. Opisano również sposób toohost i uruchom usługi hello. Witaj usługi, która jest tworzona jest samodzielnie hostowana i powitania klienta i usługa są uruchomione na powitania tym samym komputerze. Usługa hello można skonfigurować przy użyciu kodu lub pliku konfiguracji.

Witaj ostatnie trzy kroki opisują sposób toocreate aplikacji klienckiej, konfigurowania powitania klienta aplikacji, tworzenie i użycia klienta, który można uzyskać dostępu do funkcji hello hello hosta.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka będziesz potrzebować hello następujące:

* [Program Microsoft Visual Studio w wersji 2015 lub nowszej](http://visualstudio.com). W tym samouczku korzysta z programu Visual Studio 2017 r.
* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/free/).

## <a name="create-a-service-namespace"></a>Tworzenie przestrzeni nazw usługi

pierwszym krokiem Hello jest toocreate przestrzeni nazw i tooobtain [dostępu sygnatury dostępu Współdzielonego](../service-bus-messaging/service-bus-sas.md) klucza. Przestrzeń nazw wyznacza granice aplikacji dla każdej aplikacji widocznej za pośrednictwem usługi przekazywania hello. Klucz sygnatury dostępu Współdzielonego jest automatycznie generowane przez system powitania po utworzeniu przestrzeni nazw usługi. Hello kombinacji przestrzeni nazw usługi i klucza sygnatury dostępu Współdzielonego zapewnia poświadczenia hello Azure tooauthenticate dostępu tooan aplikacji. Wykonaj hello [instrukcje w tym miejscu](relay-create-namespace-portal.md) toocreate przekazywania przestrzeni nazw.

## <a name="define-a-wcf-service-contract"></a>Definiowanie kontraktu usługi WCF

kontrakt usługi Hello Określa, jakie operacje (hello terminologia usługi sieci web dla metod lub funkcji) hello usługa obsługuje. Kontrakty są tworzone przez definiowanie interfejsu C++, C# lub Visual Basic. Każda metoda w interfejsie hello odpowiada tooa określonej operacji usługi. Każdego interfejsu należy zastosować hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) tooit zastosować atrybutu i każdej operacji musi być hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit atrybut zastosowany. Jeśli metoda w interfejsie z atrybutem hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atrybut nie ma hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) atrybutu — metoda nie jest uwidaczniana. Hello kod dla tych zadań podano w przykład Witaj hello procedury. Aby uzyskać bardziej szczegółowo omówiono kontrakty i usługi, zobacz [projektowanie i Implementowanie usług](https://msdn.microsoft.com/library/ms729746.aspx) w hello dokumentacji usługi WCF.

### <a name="create-a-relay-contract-with-an-interface"></a>Tworzenie kontraktu przekazywania przy użyciu interfejsu

1. Otwórz program Visual Studio jako administrator, klikając prawym przyciskiem myszy program hello w hello **Start** menu i wybierając **Uruchom jako administrator**.
2. Utwórz nowy projekt aplikacji konsoli. Kliknij przycisk hello **pliku** menu i wybierz **nowy**, następnie kliknij przycisk **projektu**. W hello **nowy projekt** okna dialogowego, kliknij przycisk **Visual C#** (Jeśli **Visual C#** nie jest wyświetlana, sprawdź w obszarze **inne języki**). Kliknij przycisk hello **aplikacji konsoli (.NET Framework)** szablonu i nadaj mu nazwę **EchoService**. Kliknij przycisk **OK** toocreate hello projektu.

    ![][2]

3. Zainstaluj pakiet NuGet usługi Service Bus hello. Ten pakiet automatycznie dodaje bibliotek usługi Service Bus toohello odwołania, a także hello WCF **System.ServiceModel**. [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) jest hello przestrzeni nazw, która pozwala tooprogrammatically dostępu hello podstawowych funkcji usługi WCF. Usługa Service Bus używa wielu hello obiektów i atrybutów kontraktów usług WCF toodefine.

    W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** . Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`. Upewnij się, że nazwa projektu hello jest zaznaczona w hello **wersje** pole. Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.

    ![][3]
4. W Eksploratorze rozwiązań kliknij dwukrotnie tooopen pliku Program.cs hello on w edytorze hello, jeśli nie jest jeszcze otwarty.
5. Dodaj hello następujące instrukcje using u góry pliku hello hello:

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. Nazwa przestrzeni nazw hello zmiany z domyślnej nazwy **EchoService** za**Microsoft.ServiceBus.Samples**.

   > [!IMPORTANT]
   > W tym samouczku używana przestrzeń nazw hello C# **Microsoft.ServiceBus.Samples**, czyli hello nazw hello na podstawie umowy zarządzanego typu, który jest używany w pliku konfiguracyjnym hello w hello [klienta WCF hello Konfiguruj](#configure-the-wcf-client) kroku. Można określić dowolną przestrzeń nazw podczas kompilowania tego przykładu; jednak hello samouczek nie będzie działać, jeśli nie zmodyfikujesz następnie przestrzeni nazw hello hello kontraktu i usługi, w pliku konfiguracyjnym aplikacji hello. Witaj przestrzeń nazw określona w hello App.config plik musi być hello sam hello przestrzeń nazw określona w plikach C#.
   >
   >
7. Bezpośrednio po hello `Microsoft.ServiceBus.Samples` deklaracji przestrzeni nazw, ale w ramach hello przestrzeni nazw, zdefiniuj nowy interfejs o nazwie `IEchoContract` i zastosować hello `ServiceContractAttribute` atrybutu toohello interfejsu z wartością przestrzeni nazw `http://samples.microsoft.com/ServiceModel/Relay/`. Wartość przestrzeni nazw Hello różni się od przestrzeni nazw hello, używanej w całym zakresie hello kodu. Zamiast tego wartość przestrzeni nazw hello jest używany jako unikatowy identyfikator dla tego kontraktu. Jawne określenie hello przestrzeni nazw zapobiega dodawaniu Nazwa kontraktu toohello hello domyślnej wartości przestrzeni nazw. Wklej hello następującego kodu po deklaracji przestrzeni nazw hello:

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > Zwykle hello przestrzeń nazw kontraktu usługi zawiera schemat nazewnictwa uwzględniający informacje o wersji. W tym informacje o wersji w przestrzeni nazw kontraktu usługi hello umożliwia usług tooisolate najważniejszych zmian przez zdefiniowanie nowego kontraktu usługi z nowej przestrzeni nazw i ujawnienie go na nowy punkt końcowy. W ten sposób klienci mogą nadal toouse hello starego kontraktu usługi bez konieczności toobe aktualizacji. Informacje o wersji mogą zawierać datę lub numer kompilacji. Aby uzyskać więcej informacji, zobacz [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498) (Obsługa wersji usług). Witaj celów tego samouczka hello nazewnictwa schematu przestrzeni nazw kontraktu usługi hello nie zawiera informacje o wersji.
   >
   >
8. W ramach hello `IEchoContract` interfejsu, Zadeklaruj metodę dla hello jednej operacji hello `IEchoContract` ujawnia kontraktu w hello na interfejsie i Zastosuj hello `OperationContractAttribute` atrybutu toohello metodę, która ma tooexpose jako część hello publicznego przekaźnika usługi WCF kontraktu, w następujący sposób:

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. Bezpośrednio po hello `IEchoContract` definicji interfejsu, Zadeklaruj kanał dziedziczący z `IEchoContract` , a także toohello `IClientChannel` interfejsu, jak pokazano poniżej:

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    Kanał jest obiektem usługi WCF hello za pomocą którego hello host i klient przekazują tooeach informacje o innych. Później napiszesz kod względem hello kanału tooecho informacji między dwiema aplikacjami hello.
10. Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** lub naciśnij klawisz **Ctrl + Shift + B** tooconfirm hello dokładność pracy wykonanej do tej pory.

### <a name="example"></a>Przykład

powitania po kod przedstawia podstawowy interfejs definiujący kontrakt usługi WCF przekazywania.

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Teraz, gdy hello interfejs został utworzony, można zaimplementować interfejsu hello.

## <a name="implement-hello-wcf-contract"></a>Implementowanie hello WCF kontraktu

Tworzenie przekazywania Azure wymaga, należy najpierw utworzyć kontrakt hello, który został zdefiniowany przy użyciu interfejsu. Aby uzyskać więcej informacji na temat tworzenia interfejsu hello Zobacz hello w poprzednim kroku. Witaj następnym krokiem jest tooimplement hello interfejsu. Obejmuje to tworzenie klasy o nazwie `EchoService` hello zdefiniowane przez użytkownika, który zawiera `IEchoContract` interfejsu. Po zaimplementowaniu interfejsu hello, następnie należy skonfigurować interfejs hello przy użyciu pliku konfiguracji App.config. Witaj plik konfiguracji zawiera niezbędne informacje dotyczące aplikacji hello, takie jak nazwa hello hello usługi, nazwa hello hello kontraktu i typ hello protokołu, który jest używany toocommunicate z usługą przekazywania hello. Kod Hello używany do wykonywania tych zadań podano w przykład Witaj hello procedury. Aby uzyskać bardziej ogólne omówienie sposobu kontraktu tooimplement usługi, zobacz [Implementowanie kontraktów usług](https://msdn.microsoft.com/library/ms733764.aspx) w hello dokumentacji usługi WCF.

1. Utwórz nową klasę o nazwie `EchoService` bezpośrednio po definicji hello hello `IEchoContract` interfejsu. Witaj `EchoService` klasa implementuje hello `IEchoContract` interfejsu.

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    Podobne implementacje interfejsu tooother, można zaimplementować definicję hello w innym pliku. Jednak w tym samouczku implementacji hello znajduje się w hello tego samego pliku jako hello definicja interfejsu i hello `Main` metody.
2. Zastosuj hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atrybutu toohello `IEchoContract` interfejsu. Atrybut Hello określa hello nazwę usługi i przestrzeń nazw. Po wykonaniu tej czynności, hello `EchoService` klasy wygląda następująco:

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. Implementowanie hello `Echo` metody zdefiniowanej w hello `IEchoContract` interfejsu w hello `EchoService` klasy.

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. Kliknij przycisk **kompilacji**, następnie kliknij przycisk **Kompiluj rozwiązanie** tooconfirm hello dokładność wykonanej pracy.

### <a name="define-hello-configuration-for-hello-service-host"></a>Definiowanie konfiguracji hello hello hosta usługi

1. plik konfiguracji Hello jest bardzo podobne pliku konfiguracji usługi WCF tooa. Zawiera nazwę usługi hello, punkt końcowy (to znaczy hello lokalizację ujawniający przekazywania Azure dla klientów i hosty toocommunicate ze sobą) i hello powiązanie (typ hello protokół, który jest używany toocommunicate). Witaj główną różnicą jest to skonfigurowanego punktu końcowego usługi tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) powiązania, który nie jest częścią hello .NET Framework. [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) jest jednym z powiązań hello zdefiniowanych przez usługę hello.
2. W **Eksploratora rozwiązań**, kliknij dwukrotnie tooopen pliku App.config hello go w edytorze programu Visual Studio hello.
3. W hello `<appSettings>` elementu, zastąp symbole zastępcze hello hello nazwą przestrzeni nazw usługi i hello klucza sygnatury dostępu Współdzielonego, który został skopiowany w poprzednim kroku.
4. W ramach hello `<system.serviceModel>` Dodaj tagi, `<services>` elementu. Wiele aplikacji przekazywania można zdefiniować w pojedynczym pliku konfiguracji. W tym samouczku zdefiniowano jednak tylko jedną.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. W ramach hello `<services>` elementu, Dodaj `<service>` nazwa hello toodefine elementu hello usługi.

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. W ramach hello `<service>` elementu, zdefiniuj lokalizację kontraktu punktu końcowego hello hello, a także hello wpisz powiązanie dla punktu końcowego hello.

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    punkt końcowy Hello definiuje, gdzie powitania klienta będzie szukać aplikacji hosta hello. Później hello samouczku ten krok toocreate identyfikator URI, który w pełni ujawnia hosta hello za pośrednictwem przekaźnika usługi Azure. Witaj powiązanie deklaruje, że TCP jest używany jako hello toocommunicate protokołu z usługą przekazywania hello.
7. Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** tooconfirm hello dokładność wykonanej pracy.

### <a name="example"></a>Przykład

Witaj poniższy kod przedstawia implementację hello hello kontraktu usługi.

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

Witaj poniższy kod przedstawia podstawowy format pliku App.config hello skojarzona z hostem usługi hello hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a>Hostowanie i uruchamianie tooregister usługi sieci web podstawowe z usługą przekazywania hello

W tym kroku opisano, jak toorun Azure przekazywania usługi.

### <a name="create-hello-relay-credentials"></a>Utwórz hello przekazywania poświadczeń

1. W `Main()`, Utwórz dwie zmienne, w których toostore hello nazw i klucza sygnatury dostępu Współdzielonego, które są odczytywane z okna konsoli hello hello.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    klucz sygnatury dostępu Współdzielonego Hello będą używane nowsze tooaccess Twojego projektu. przestrzeń nazw Hello jest przekazywana jako parametr zbyt`CreateServiceUri` toocreate identyfikator URI usługi.
2. Przy użyciu [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) , Zadeklaruj, że będziesz używać klucza sygnatury dostępu Współdzielonego jako typu poświadczeń hello. Dodaj następujące kod bezpośrednio po hello kodzie dodanym w ostatnim kroku hello hello.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a>Utwórz adres podstawowy usługi hello

Po kodzie hello dodanym w ostatnim kroku hello utworzyć `Uri` wystąpienie dla adresu podstawowego hello hello usługi. Ten identyfikator URI Określa schemat magistrali usług hello, hello przestrzeni nazw i hello ścieżkę interfejsu usługi hello.

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

"sb" stanowi skrót od hello schemat magistrali usług i wskazuje, że TCP jest używany protokół hello. Wskazano to również uprzednio w pliku konfiguracyjnym hello, gdy [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) został określony w powiązaniu hello.

W tym samouczku hello identyfikator URI jest `sb://putServiceNamespaceHere.windows.net/EchoService`.

### <a name="create-and-configure-hello-service-host"></a>Tworzenie i Konfigurowanie hosta usługi hello

1. Ustaw tryb łączności hello zbyt`AutoDetect`.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    Witaj tryb łączności opisuje toocommunicate hello protokołu hello używa usługi z usługą przekazywania hello; protokołu HTTP lub TCP. Przy użyciu ustawienia domyślne hello `AutoDetect`, usługa hello podejmuje tooAzure tooconnect przekazywania za pośrednictwem protokołu TCP, jeśli jest dostępna i HTTP, jeśli protokół TCP nie jest dostępna. Określa Uwaga ta różni się od hello protokołu hello usługi do komunikacji z klientem. Ten protokół jest ustalany przez powiązanie hello używane. Na przykład usługa może używać hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) powiązania, który określa, że jej punkt końcowy komunikuje się z klientami za pośrednictwem protokołu HTTP. Czy sama usługa może określać **ConnectivityMode.AutoDetect** tak, aby usługa hello komunikuje się z przekaźnika usługi Azure za pośrednictwem protokołu TCP.
2. Utwórz hosta usługi hello, za pomocą powitalne identyfikatora URI utworzonego wcześniej w tej sekcji.

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    host usługi Hello jest hello WCF obiekt, który tworzy hello usługi. W tym miejscu możesz przekazać typ hello usługi ma toocreate ( `EchoService` typu) i również adres toohello ma tooexpose hello usługi.
3. U góry pliku Program.cs hello hello, dodaj odwołania do zbyt[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) i [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. W `Main()`, skonfiguruj hello punktu końcowego tooenable publicznie.

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    Ten krok informuje usługi przekazywania hello czy aplikacji może być znajdowana przez zbadanie źródła danych ATOM hello projektu. Jeśli ustawisz **DiscoveryType** za**prywatnej**, klient nadal będą mogli tooaccess hello usługi. Jednak usługa hello nie pojawią się podczas wyszukiwania hello przekazywania w przestrzeni nazw. Zamiast tego powitania klienta musi ścieżkę punktu końcowego hello tooknow wcześniej.
5. Zastosuj poświadczenia usługi hello toohello punktów końcowych usługi zdefiniowane w pliku App.config hello:

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    Jak już wspomniano w poprzednim kroku hello, możesz zadeklarować kilka usług i punktów końcowych w pliku konfiguracyjnym hello. Jeśli użytkownik ma, ten kod pomijałby plik konfiguracji hello i wyszukiwania dla każdego punktu końcowego toowhich powinien zastosować Twoje poświadczenia. W tym samouczku plik konfiguracyjny hello ma tylko jeden punkt końcowy.

### <a name="open-hello-service-host"></a>Otwórz hello hosta usługi

1. Otwórz usługę hello.

    ```csharp
    host.Open();
    ```
2. Powiadamia użytkownika hello hello usługa jest uruchomiona i opisano sposób tooshut dół hello usługi.

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Po zakończeniu zamknij hosta usługi hello.

    ```csharp
    host.Close();
    ```
4. Naciśnij klawisz **Ctrl + Shift + B** toobuild hello projektu.

### <a name="example"></a>Przykład

Kodu usługi zakończone powinna wyglądać następująco. Kod Hello zawiera hello kontrakt usługi i implementację z poprzednich kroków samouczka hello i hosty hello usługę w aplikacji konsoli.

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a>Tworzenie klienta WCF dla kontraktu usługi hello

Witaj, następnym krokiem jest toocreate aplikacji klienckiej i definiowanie kontraktu usługi hello, który będzie implementowany w następnych krokach. Należy pamiętać, że wiele z tych kroków przypomina kroki hello używane toocreate usługi: definiowanie kontraktu, edytowanie pliku App.config plików przy użyciu poświadczeń usługi przekazywania toohello tooconnect i tak dalej. Kod Hello używany do wykonywania tych zadań podano w przykład Witaj hello procedury.

1. Utwórz nowy projekt w bieżącym rozwiązaniu programu Visual Studio powitania klienta hello hello następujący:

   1. W Eksploratorze rozwiązań w hello tego samego rozwiązania, które zawiera usługę hello, kliknij prawym przyciskiem myszy hello bieżące rozwiązanie (nie projekt hello) i kliknij przycisk **Dodaj**. Następnie kliknij pozycję **Nowy projekt**.
   2. W hello **Dodawanie nowego projektu** okno dialogowe, kliknij przycisk **Visual C#** (Jeśli **Visual C#** nie jest wyświetlana, sprawdź w obszarze **inne języki**) wybierz pozycję hello **Aplikacji konsoli (.NET Framework)** szablonu i nadaj mu nazwę **EchoClient**.
   3. Kliknij przycisk **OK**.
      <br />
2. W Eksploratorze rozwiązań kliknij dwukrotnie plik Program.cs hello w hello **EchoClient** projektu tooopen on w edytorze hello, jeśli nie jest jeszcze otwarty.
3. Nazwa przestrzeni nazw hello zmiany z domyślnej nazwy `EchoClient` zbyt`Microsoft.ServiceBus.Samples`.
4. Zainstaluj hello [pakietu NuGet usługi Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus): w Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **EchoClient** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**. Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`. Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.

    ![][3]
5. Dodaj `using` instrukcji dla hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) przestrzeni nazw w pliku Program.cs hello.

    ```csharp
    using System.ServiceModel;
    ```
6. Dodać hello definicji toohello przestrzeń nazw kontraktu usługi, jak pokazano hello poniższy przykład. Należy pamiętać, że ta definicja identyczne toohello definicją używaną w hello **usługi** projektu. Ten kod należy dodać u góry hello hello `Microsoft.ServiceBus.Samples` przestrzeni nazw.

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. Naciśnij klawisz **Ctrl + Shift + B** toobuild powitania klienta.

### <a name="example"></a>Przykład

Witaj poniższy kod przedstawia bieżący stan pliku Program.cs hello hello w hello **EchoClient** projektu.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a>Konfigurowanie powitania klienta WCF

W tym kroku utworzysz plik App.config dla podstawowej aplikacji klienckiej, która uzyskuje dostęp do usługi hello utworzonej wcześniej w tym samouczku. Ten plik App.config definiuje kontrakt hello, powiązania i nazwa punktu końcowego hello. Kod Hello używany do wykonywania tych zadań podano w przykład Witaj hello procedury.

1. W Eksploratorze rozwiązań w hello **EchoClient** projektu, kliknij dwukrotnie **App.config** tooopen hello plik w edytorze programu Visual Studio hello.
2. W hello `<appSettings>` elementu, zastąp symbole zastępcze hello hello nazwą przestrzeni nazw usługi i hello klucza sygnatury dostępu Współdzielonego, który został skopiowany w poprzednim kroku.
3. W elemencie system.serviceModel hello, Dodaj `<client>` elementu.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    Ten krok umożliwia zadeklarowanie, że definiowana jest aplikacja kliencka w stylu platformy WCF.
4. W ramach hello `client` elementu, zdefiniuj hello nazwę, kontrakt i typ powiązania punktu końcowego hello.

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    Ten krok umożliwia określenie nazwy hello hello punktu końcowego, hello kontrakt zdefiniowany w hello usługi i hello fakt, że aplikacja kliencka hello używa TCP toocommunicate z przekaźnika usługi Azure. Witaj Nazwa punktu końcowego jest używana w hello następny krok toolink tej konfiguracji pliku końcowego z usługą hello identyfikatora URI.
5. Kliknij przycisk **pliku**, następnie kliknij przycisk **Zapisz wszystko**.

## <a name="example"></a>Przykład

Witaj poniższy kod przedstawia plik App.config powitania klienta Echo hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a>Klient WCF hello wdrożenie
W tym kroku należy zaimplementować podstawowej aplikacji klienckiej, która uzyskuje dostęp do usługi hello, utworzony wcześniej w tym samouczku. Podobne toohello, powitania klienta będzie przeprowadzać usługa wiele hello tej samej operacji tooaccess przekazywania Azure:

1. Ustawia tryb łączności hello.
2. Tworzy identyfikator URI, który lokalizuje usługę hosta hello hello.
3. Definiuje hello poświadczeń zabezpieczeń.
4. Stosuje hello poświadczenia toohello połączenia.
5. Otwiera hello połączenia.
6. Wykonuje zadania specyficzne dla aplikacji hello.
7. Zamyka połączenie hello.

Jedną z głównych różnic hello jest jednak czy aplikacja kliencka hello używa usługi przekazywania toohello tooconnect kanału, natomiast usługa hello używa wywołania zbyt**ServiceHost**. Kod Hello używany do wykonywania tych zadań podano w przykład Witaj hello procedury.

### <a name="implement-a-client-application"></a>Wdrażanie aplikacji klienta
1. Ustaw tryb łączności hello zbyt**Autowykrywanie**. Dodaj następujące kodu wewnątrz hello hello `Main()` metody hello **EchoClient** aplikacji.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. Zdefiniuj zmienne toohold hello wartości hello przestrzeni nazw usługi i klucza sygnatury dostępu Współdzielonego odczytanego z hello konsoli.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. Utwórz hello identyfikator URI, który definiuje lokalizacji hello hello hosta w projekcie przekazywania.

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. Utwórz obiekt poświadczeń powitania dla punktu końcowego przestrzeni nazw usługi.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. Utwórz hello fabrykę kanałów ładującą konfigurację hello opisaną w pliku App.config hello.

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    Fabryka kanałów jest obiektem platformy WCF tworzącym kanał za pomocą którego komunikują się hello usługi i aplikacje klienckie.
6. Zastosuj hello poświadczeń.

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. Utwórz i otwórz hello kanału toohello usługi.

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. Zapisywanie hello podstawowy interfejs użytkownika oraz funkcje dla echa hello.

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    Uwaga hello kod używa hello wystąpienia obiektu kanału hello jako serwer proxy dla usługi hello.
9. Zamknij kanał hello i zamknij hello fabryki.

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a>Przykład

Wypełniony kod powinien wyglądać następująco, przedstawiający sposób toocreate aplikacji klienckiej, jak toocall hello operacje usługi hello i jak tooclose hello klienta po wykonaniu operacji hello wywołanie zostało zakończone.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a>Uruchamianie aplikacji hello

1. Naciśnij klawisz **Ctrl + Shift + B** toobuild hello rozwiązania. Powoduje to skompilowanie zarówno projektu klienta hello, jak i projekt usługi hello utworzony w poprzednich krokach hello.
2. Przed działającej aplikacji hello klienta musi upewnij się, czy aplikacja usługi hello jest uruchomiona. W Eksploratorze rozwiązań w programie Visual Studio, kliknij prawym przyciskiem myszy hello **EchoService** rozwiązania, następnie kliknij przycisk **właściwości**.
3. Okno dialogowe właściwości rozwiązania hello, kliknij przycisk **projekt startowy**, kliknij przycisk hello **wiele projektów startowych** przycisku. Upewnij się, że **EchoService** się na początku listy hello.
4. Zestaw hello **akcji** pole dla obu hello **EchoService** i **EchoClient** projektów zbyt**Start**.

    ![][5]
5. Kliknij pozycję **Zależności projektu**. W hello **projekty** wybierz opcję **EchoClient**. W hello **zależy od** upewnij się, **EchoService** jest zaznaczony.

    ![][6]
6. Kliknij przycisk **OK** toodismiss hello **właściwości** okna dialogowego.
7. Naciśnij klawisz **F5** toorun oba projekty.
8. Oba okna konsoli otwórz i wyświetlenie monitu o hello przestrzeni nazw. Hello usługa musi być uruchomiona, dlatego w hello **EchoService** oknie konsoli, wprowadź hello przestrzeni nazw, a następnie naciśnij klawisz **Enter**.
9. Następnie zostanie wyświetlony monit o podanie klucza sygnatury dostępu współdzielonego. Wprowadź klucz sygnatury dostępu Współdzielonego hello i naciśnij klawisz ENTER.

    Oto przykładowe dane wyjściowe z okna konsoli hello. Należy pamiętać, że wartości hello pod warunkiem, że w tym miejscu są na przykład tylko do celów.

    `Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`

    Aplikacja usługi Hello drukuje toohello adres konsoli programu Windows hello na którym nasłuchuje, widziany hello poniższy przykład.

    `Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`
10. W hello **EchoClient** oknie konsoli, należy wprowadzić te same informacje, które zostały wprowadzone uprzednio dla aplikacji usługi hello hello. Wykonaj Witaj Witaj tooenter poprzednie kroki tej samej przestrzeni nazw usługi i skojarzenia zabezpieczeń wartości dla aplikacji klienckiej hello klucza.
11. Po wprowadzeniu tych wartości, powitania klienta otwiera kanału usługi toohello monitów i możesz tooenter tekstu, jak hello poniższy przykład danych wyjściowych konsoli.

    `Enter text tooecho (or [Enter] tooexit):`

    Wprowadź niektórych aplikacji usługi toohello toosend tekstu, a następnie naciśnij klawisz Enter. Ten tekst jest wysyłany toohello usługi za pośrednictwem hello operacji usługi Echo i pojawia się w oknie konsoli usługi hello jak hello następujące przykładowe dane wyjściowe.

    `Echoing: My sample text`

    Witaj aplikacja kliencka odbiera wartość zwracaną hello hello `Echo` operacja, która jest hello oryginalny tekst i wyświetla go tooits oknie konsoli. Witaj poniżej przedstawiono przykładowe dane wyjściowe z okna konsoli powitania klienta.

    `Server echoed: My sample text`
12. Możesz kontynuować wysyłanie wiadomości SMS z powitania klienta toohello usługi w ten sposób. Po zakończeniu naciśnij klawisz Enter w powitania klienta i usługi konsoli windows tooend obydwu aplikacji.

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono, jak toobuild Azure przekazywania aplikacji klienckiej i usługi za pomocą hello możliwości WCF przekaźnika usługi Service Bus. Aby podobnego samouczka dotyczącego używa [usługi magistrali komunikatów](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), zobacz [Rozpoczynanie pracy z kolejek usługi Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

toolearn więcej informacji na temat przekaźnika usługi Azure, zobacz następujące tematy hello.

* [Omówienie architektury usługi Azure Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [Omówienie usługi Azure Relay](relay-what-is-it.md)
* [Jak usługa z platformą .NET przekazywania toouse hello WCF](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
