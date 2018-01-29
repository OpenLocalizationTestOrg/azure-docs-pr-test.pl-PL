---
title: "Samouczek usługi Azure Service Bus WCF przekazywania | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji klienta i usługi przy użyciu przekaźnika usługi WCF."
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
ms.date: 11/02/2017
ms.author: sethm
ms.openlocfilehash: a0b06c32cf5f154cf5eb01842d9b917dcb35f7b3
ms.sourcegitcommit: 3df3fcec9ac9e56a3f5282f6c65e5a9bc1b5ba22
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/04/2017
---
# <a name="azure-wcf-relay-tutorial"></a>Samouczek usługi Azure przekaźnika usługi WCF

Ten przewodnik opisuje sposób tworzenia prostego klienta WCF przekazywania aplikacji i usług przy użyciu przekaźnika usługi Azure. Aby podobnego samouczka dotyczącego używa [komunikatów usługi Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), zobacz [Rozpoczynanie pracy z kolejek usługi Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

Ten samouczek umożliwia poznanie kroków, które są wymagane do utworzenia aplikacji klienta i usługi WCF przekazywania. Podobnie jak ich odpowiedniki WCF oryginalnej usługa jest strukturą ujawniającą jeden lub więcej punktów końcowych, z których każdy ujawnia co najmniej jedną operację usługi. Punkt końcowy usługi określa adres usługi, powiązanie zawierające informacje umożliwiające klientowi komunikowanie się z usługą i kontrakt definiujący funkcje zapewniane klientom przez usługę. Podstawowa różnica między WCF i przekazywania WCF jest, że punkt końcowy jest widoczna w chmurze zamiast lokalnie na komputerze.

Po zapoznaniu się z sekwencją tematów w tym samouczku będziesz mieć uruchomioną usługę i klienta, który może wywoływać operacje usługi. W pierwszym temacie opisano sposób konfigurowania konta. Następne kroki opisują sposób definiowania usługi używającej kontraktu, wdrażania usługi i konfigurowania usługi w kodzie. Opisano również sposób hostowania i uruchamiania usługi. Tworzona jest samodzielnie hostowana usługa, a klient i usługa są uruchomione na tym samym komputerze. Usługę można skonfigurować przy użyciu kodu lub pliku konfiguracji.

Ostatnie trzy kroki opisują sposób tworzenia aplikacji klienckiej, konfigurowania aplikacji klienckiej oraz tworzenia i użycia klienta, który może uzyskać dostęp do funkcji hosta.

## <a name="prerequisites"></a>Wymagania wstępne

Do wykonania kroków tego samouczka niezbędne są następujące elementy:

* [Program Microsoft Visual Studio w wersji 2015 lub nowszej](http://visualstudio.com). W tym samouczku korzysta z programu Visual Studio 2017 r.
* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/free/).

## <a name="create-a-service-namespace"></a>Tworzenie przestrzeni nazw usługi

Pierwszym krokiem jest utworzenie przestrzeni nazw i uzyskanie [dostępu sygnatury dostępu Współdzielonego](../service-bus-messaging/service-bus-sas.md) klucza. Przestrzeń nazw wyznacza granice aplikacji dla każdej aplikacji widocznej za pośrednictwem usługi przekazywania. Klucz sygnatury dostępu współdzielonego jest automatycznie generowany przez system po utworzeniu przestrzeni nazw usługi. Kombinacja przestrzeni nazw usługi i klucza sygnatury dostępu Współdzielonego dostarcza poświadczenia dla platformy Azure w celu uwierzytelniania dostępu do aplikacji. Postępuj zgodnie z [instrukcjami podanymi w tym miejscu](relay-create-namespace-portal.md), aby utworzyć przestrzeń nazw przekazywania.

## <a name="define-a-wcf-service-contract"></a>Definiowanie kontraktu usługi WCF

Kontrakt usługi określa, jakie operacje (terminologia usługi sieci web dla metod lub funkcji) usługa obsługuje. Kontrakty są tworzone przez definiowanie interfejsu C++, C# lub Visual Basic. Każda metoda w interfejsie odpowiada określonej operacji usługi. W odniesieniu do każdego interfejsu należy zastosować atrybut [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx), a w odniesieniu do każdej operacji należy zastosować atrybut [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx). Jeśli metoda w interfejsie z atrybutem [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) nie ma atrybutu [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), nie jest ujawniana. Kod dla tych zadań podano w przykładzie zamieszczonym na końcu procedury. Kontrakty i usługi bardziej szczegółowo omówiono w artykule [Projektowanie i implementowanie usług](https://msdn.microsoft.com/library/ms729746.aspx) w dokumentacji platformy WCF.

### <a name="create-a-relay-contract-with-an-interface"></a>Tworzenie kontraktu przekazywania przy użyciu interfejsu

1. Otwórz program Visual Studio jako administrator, klikając prawym przyciskiem myszy ikonę programu w menu **Start**, a następnie wybierając polecenie **Uruchom jako administrator**.
2. Utwórz nowy projekt aplikacji konsoli. Kliknij menu **Plik** i wybierz pozycję **Nowy**, a następnie kliknij pozycję **Projekt**. W oknie dialogowym **Nowy projekt** kliknij pozycję **Visual C#** (jeśli pozycja **Visual C#** nie jest wyświetlana, sprawdź w obszarze **Inne języki**). Kliknij przycisk **aplikacji konsoli (.NET Framework)** szablonu i nadaj mu nazwę **EchoService**. Kliknij przycisk **OK**, aby utworzyć projekt.

    ![][2]

3. Zainstaluj pakiet NuGet magistrali usług. Ten pakiet automatycznie dodaje odwołania do bibliotek usługi Service Bus, jak również przestrzeń nazw **System.ServiceModel** usługi WCF. [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) jest przestrzenią nazw umożliwiającą programowy dostęp do podstawowych funkcji platformy WCF. Usługa Service Bus używa wielu obiektów i atrybutów usługi WCF do definiowania kontraktów usług.

    W Eksploratorze rozwiązań kliknij projekt prawym przyciskiem myszy, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** . Kliknij kartę **Przeglądanie**, a następnie wyszukaj ciąg **WindowsAzure.ServiceBus**. Upewnij się, że nazwa projektu jest zaznaczona w polu **Wersje**. Kliknij pozycję **Zainstaluj** i zaakceptuj warunki użytkowania.

    ![][3]
4. W Eksploratorze rozwiązań kliknij dwukrotnie plik Program.cs, aby otworzyć go w edytorze, jeśli nie został jeszcze otwarty.
5. Dodaj następujące instrukcje using na początku pliku:

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. Zmień nazwę przestrzeni nazw z domyślnej nazwy **EchoService** na **Microsoft.ServiceBus.Samples**.

   > [!IMPORTANT]
   > W tym samouczku używana przestrzeń nazw C# **Microsoft.ServiceBus.Samples**, który jest przestrzeń nazw kontraktu podstawie zarządzane typu, który jest używany w pliku konfiguracji w [Konfigurowanie klienta platformy WCF](#configure-the-wcf-client) krok. Możesz określić dowolną przestrzeń nazw podczas kompilowania tego przykładu, jednak samouczek nie będzie działać, jeśli nie zmodyfikujesz następnie odpowiednio przestrzeni nazw kontraktu i usługi w pliku konfiguracji aplikacji. Przestrzeń nazw określona w pliku App.config musi być taka sama jak przestrzeń nazw określona w plikach C#.
   >
   >
7. Bezpośrednio po `Microsoft.ServiceBus.Samples` deklaracji przestrzeni nazw, ale w przestrzeni nazw Zdefiniuj nowy interfejs o nazwie `IEchoContract` i zastosować `ServiceContractAttribute` do interfejsu z wartością przestrzeni nazw `http://samples.microsoft.com/ServiceModel/Relay/`. Wartość przestrzeni nazw różni się od przestrzeni nazw używanej w kodzie. Zamiast tego wartość przestrzeni nazw jest używana jako unikatowy identyfikator dla tego kontraktu. Jawne określenie przestrzeni nazw zapobiega dodawaniu domyślnej wartości przestrzeni nazw do nazwy kontraktu. Wklej następujący kod po deklaracji przestrzeni nazw:

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > Zazwyczaj przestrzeń nazw kontraktu usługi zawiera schemat nazewnictwa uwzględniający informacje o wersji. Uwzględnienie informacji o wersji w przestrzeni nazw kontraktu usługi umożliwia usługom izolowanie istotnych zmian przez zdefiniowanie nowego kontraktu usługi z nową przestrzenią nazw i ujawnienie go w nowym punkcie końcowym. W ten sposób klienci mogą nadal używać starego kontraktu usługi bez konieczności aktualizacji. Informacje o wersji mogą zawierać datę lub numer kompilacji. Aby uzyskać więcej informacji, zobacz [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498) (Obsługa wersji usług). Schemat nazewnictwa przestrzeni nazw kontraktu usługi, używany w tym przykładzie, nie zawiera informacji o wersji.
   >
   >
8. W ramach `IEchoContract` interfejsu, Zadeklaruj metodę dla pojedynczej operacji `IEchoContract` kontraktu udostępnia w interfejsie i Zastosuj `OperationContractAttribute` atrybut do metody, którą chcesz uwidocznić jako część publicznego kontraktu usługi WCF przekazywania w następujący sposób:

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. Bezpośrednio po definicji interfejsu `IEchoContract` zadeklaruj kanał dziedziczący zarówno po `IEchoContract`, jak i interfejsie `IClientChannel`, w sposób pokazany poniżej:

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    Kanał jest obiektem platformy WCF, za pomocą którego host i klient przekazują do siebie informacje. Później napiszesz kod dla kanału obsługujący echo informacji przesyłanych między dwiema aplikacjami.
10. W menu **Kompilacja** kliknij pozycję **Kompiluj rozwiązanie** lub naciśnij klawisze **Ctrl+Shift+B**, aby potwierdzić dokładność pracy wykonanej do tej pory.

### <a name="example"></a>Przykład

Poniższy kod przedstawia podstawowy interfejs definiujący kontrakt usługi WCF przekazywania.

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

Teraz, gdy interfejs został utworzony, możesz go zaimplementować.

## <a name="implement-the-wcf-contract"></a>Implementowanie kontraktu usługi WCF

Tworzenie przekaźnika usługi Azure wymaga, aby najpierw utworzyć kontrakt definiowany przy użyciu interfejsu. Więcej informacji na temat tworzenia interfejsu podano w opisie poprzedniego kroku. Następnym krokiem jest zaimplementowanie interfejsu. Jest to związane z utworzeniem klasy o nazwie `EchoService` implementującej interfejs `IEchoContract` zdefiniowany przez użytkownika. Po zaimplementowaniu interfejsu należy go skonfigurować przy użyciu pliku konfiguracji App.config. Plik konfiguracji zawiera niezbędne informacje dla aplikacji, takie jak nazwa usługi, Nazwa kontraktu i typ protokołu używanego do komunikacji z usługą przekazywania. Kod używany do wykonywania tych zadań podano w przykładzie zamieszczonym po procedurze. Bardziej ogólne omówienie sposobu implementowania kontraktu usługi można znaleźć w temacie [Implementowanie kontraktów usług](https://msdn.microsoft.com/library/ms733764.aspx) w dokumentacji platformy WCF.

1. Utwórz nową klasę o nazwie `EchoService` bezpośrednio po definicji interfejsu `IEchoContract`. Klasa `EchoService` implementuje interfejs `IEchoContract`.

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    Podobnie jak w przypadku innych implementacji interfejsów, można zaimplementować definicję w innym pliku. Jednak w przypadku tego samouczka implementację umieszczono w tym samym pliku, w którym znajduje się definicja interfejsu i metoda `Main`.
2. Zastosuj atrybut [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) do interfejsu `IEchoContract`. Ten atrybut określa nazwę usługi i przestrzeń nazw. Po wykonaniu tych czynności klasa `EchoService` wygląda następująco:

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. Zaimplementuj metodę `Echo` zdefiniowaną w interfejsie `IEchoContract` w klasie `EchoService`.

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. Kliknij pozycję **Kompilacja**, a następnie kliknij pozycję **Kompiluj rozwiązanie**, aby potwierdzić dokładność wykonanej pracy.

### <a name="define-the-configuration-for-the-service-host"></a>Definiowanie konfiguracji hosta usługi

1. Plik konfiguracji jest bardzo podobny do pliku konfiguracji platformy WCF. Zawiera nazwę usługi, punkt końcowy (czyli lokalizacji przekazywania Azure udostępnia klientom i hostom komunikować się ze sobą) i powiązanie (typ protokołu używanego do komunikacji). Główną różnicą jest odwoływanie się tego skonfigurowanego punktu końcowego usługi do powiązania [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding), które nie jest częścią programu .NET Framework. [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) jest jednym z powiązań zdefiniowanych przez usługę.
2. W **Eksploratorze rozwiązań** kliknij dwukrotnie plik App.config, aby otworzyć go w edytorze programu Visual Studio.
3. W elemencie `<appSettings>` zastąp symbole zastępcze nazwą przestrzeni nazw usługi i kluczem sygnatury dostępu współdzielonego skopiowanym we wcześniejszym kroku.
4. W tagach `<system.serviceModel>` dodaj element `<services>`. Wiele aplikacji przekazywania można zdefiniować w pojedynczym pliku konfiguracji. W tym samouczku zdefiniowano jednak tylko jedną.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. W elemencie `<services>` dodaj element `<service>`, aby zdefiniować nazwę usługi.

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. W elemencie `<service>` zdefiniuj lokalizację kontraktu punktu końcowego i wpisz powiązanie dla punktu końcowego.

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    Punkt końcowy określa, gdzie klient będzie szukać aplikacji hosta. Później w samouczku ten krok można utworzyć identyfikatora URI, który w pełni ujawnia hosta za pośrednictwem przekaźnika usługi Azure. Powiązanie deklaruje, że TCP jest używany protokół do komunikowania się z usługą przekazywania.
7. W menu **Kompilacja** kliknij pozycję **Kompiluj rozwiązanie**, aby potwierdzić dokładność wykonanej pracy.

### <a name="example"></a>Przykład

Poniższy kod przedstawia implementację kontraktu usługi.

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

Poniższy kod przedstawia podstawowy format pliku App.config skojarzonego z hostem usługi.

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

## <a name="host-and-run-a-basic-web-service-to-register-with-the-relay-service"></a>Hostowanie i uruchamianie usługi sieci web podstawowe zarejestrować za pomocą usługi przekazywania

W tym kroku opisano sposób uruchamiania usługi przekaźnika usługi Azure.

### <a name="create-the-relay-credentials"></a>Utwórz poświadczenia przekazywania

1. W procedurze `Main()` utwórz dwie zmienne do przechowywania przestrzeni nazw i klucza sygnatury dostępu współdzielonego odczytanego z okna konsoli.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    Klucz sygnatury dostępu Współdzielonego zostanie później służyć do dostęp do projektu. Przestrzeń nazw jest przekazywana jako parametr do procedury `CreateServiceUri` w celu utworzenia identyfikatora URI.
2. Korzystając z obiektu [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior), zadeklaruj zamiar użycia klucza sygnatury dostępu współdzielonego jako typu poświadczeń. Dodaj poniższy kod bezpośrednio po kodzie dodanym w ostatnim kroku.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-the-service"></a>Utwórz adres podstawowy usługi

Po kodzie dodanym w ostatnim kroku utwórz `Uri` wystąpienie dla podstawowego adresu usługi. Ten identyfikator URI określa schemat magistrali usług, przestrzeń nazw i ścieżkę interfejsu usługi.

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

Skrót „sb” (schemat magistrali usług) oznacza, że używany jest protokół TCP. Tę deklarację umieszczono również uprzednio w pliku konfiguracji, gdy określono powiązanie [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx).

W tym samouczku użyto identyfikatora URI `sb://putServiceNamespaceHere.windows.net/EchoService`.

### <a name="create-and-configure-the-service-host"></a>Tworzenie i Konfigurowanie hosta usługi

1. Ustaw tryb łączności `AutoDetect`.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    Tryb łączności opisuje protokół używany przez usługę do komunikowania się z usługą przekazywania; protokołu HTTP lub TCP. Przy użyciu domyślnego ustawienia `AutoDetect`, usługa próbuje nawiązać przekazywania Azure za pośrednictwem protokołu TCP, jeśli jest dostępna i HTTP Jeśli TCP jest niedostępny. To ustawienie nie dotyczy protokołu określonego przez usługę dla komunikacji klienckiej. Ten protokół jest ustalany na podstawie używanego powiązania. Na przykład usługa może używać [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) powiązania, który określa, że jej punkt końcowy komunikuje się z klientami za pośrednictwem protokołu HTTP. Czy sama usługa może określać **ConnectivityMode.AutoDetect** tak, aby usługa komunikuje się z przekaźnika usługi Azure za pośrednictwem protokołu TCP.
2. Utwórz hosta usługi przy użyciu identyfikatora URI utworzonego wcześniej w tej sekcji.

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    Host usługi jest obiektem platformy WCF tworzącym wystąpienie usługi. W tym miejscu możesz przekazać typ usługi, który chcesz utworzyć (typ `EchoService`), a także adres, pod którym usługa powinna być ujawniona.
3. Na początku pliku Program.cs dodaj odwołania do opisów [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) i [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. Ponownie w procedurze `Main()` skonfiguruj punkt końcowy do obsługi dostępu publicznego.

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    Ten krok informuje usługi przekazywania, który aplikacji można znaleźć, sprawdzając źródła danych projektu ATOM publicznie. Jeśli ustawisz opcję **DiscoveryType** z ustawieniem **private**, klient nadal mógłby uzyskać dostęp do usługi. Jednak usługa nie pojawią się podczas wyszukiwania nazw przekazywania. Zamiast tego klient musiałby wcześniej znać ścieżkę punktu końcowego.
5. Zapisz poświadczenia usługi w punktach końcowych zdefiniowanych w pliku App.config:

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    Jak zauważono w poprzednim kroku, w pliku konfiguracji możesz zadeklarować kilka usług i punktów końcowych. W takim przypadku ten kod pomijałby plik konfiguracji i wyszukiwałby każdy punkt końcowy, do którego powinien zastosować Twoje poświadczenia. W tym samouczku plik konfiguracyjny zawiera jednak tylko jeden punkt końcowy.

### <a name="open-the-service-host"></a>Otworzyć hosta usługi

1. Otwórz usługę.

    ```csharp
    host.Open();
    ```
2. Poinformuj użytkownika, że usługa jest uruchomiona, i wyjaśnij, jak zamknąć usługę.

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. Po zakończeniu zamknij hosta usługi.

    ```csharp
    host.Close();
    ```
4. Naciśnij klawisze **Ctrl+Shift+B**, aby skompilować projekt.

### <a name="example"></a>Przykład

Kodu usługi zakończone powinna wyglądać następująco. Ten kod zawiera kontrakt usługi i implementację z poprzednich kroków samouczka i hostuje usługę w aplikacji konsoli.

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

           // Create the credentials object for the endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create the service URI based on the service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create the service host reading the configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create the ServiceRegistrySettings behavior for the endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add the Relay credentials to all endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open the service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            // Close the service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-the-service-contract"></a>Tworzenie klienta platformy WCF dla kontraktu usługi

Następnym krokiem jest utworzenie aplikacji klienckiej i zdefiniowanie kontraktu usługi, który będzie implementowany w następnych krokach. Należy pamiętać, że wiele z tych kroków przypomina kroki używany do tworzenia usługi: definiowanie kontraktu, edytowanie pliku App.config pliku, aby połączyć się z usługą przekazywania przy użyciu poświadczeń i tak dalej. Kod używany do wykonywania tych zadań podano w przykładzie zamieszczonym po procedurze.

1. Utwórz nowy projekt w bieżącym rozwiązaniu programu Visual Studio dla klienta, wykonując następujące czynności:

   1. W Eksploratorze rozwiązań w tym samym rozwiązaniu, które zawiera tę usługę, kliknij prawym przyciskiem myszy bieżące rozwiązanie (nie projekt) i kliknij pozycję **Dodaj**. Następnie kliknij pozycję **Nowy projekt**.
   2. W **Dodawanie nowego projektu** okno dialogowe, kliknij przycisk **Visual C#** (Jeśli **Visual C#** nie jest wyświetlana, sprawdź w obszarze **inne języki**) wybierz pozycję **Aplikacji konsoli (.NET Framework)** szablonu i nadaj mu nazwę **EchoClient**.
   3. Kliknij przycisk **OK**.
      <br />
2. W Eksploratorze rozwiązań kliknij dwukrotnie plik Program.cs w projekcie **EchoClient**, aby otworzyć go w edytorze, jeśli nie został jeszcze otwarty.
3. Zmień nazwę przestrzeni nazw z domyślnej nazwy `EchoClient` na `Microsoft.ServiceBus.Samples`.
4. Zainstaluj [pakietu NuGet usługi Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus): w Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **EchoClient** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**. Kliknij kartę **Przeglądanie**, a następnie wyszukaj ciąg `Microsoft Azure Service Bus`. Kliknij pozycję **Zainstaluj** i zaakceptuj warunki użytkowania.

    ![][3]
5. Dodaj instrukcję `using` dla przestrzeni nazw [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) w pliku Program.cs.

    ```csharp
    using System.ServiceModel;
    ```
6. Dodaj definicję kontraktu usługi do przestrzeni nazw jak pokazano w poniższym przykładzie. Ta definicja jest identyczna z definicją używaną w projekcie **Usługa**. Ten kod należy dodać na początku przestrzeni nazw `Microsoft.ServiceBus.Samples`.

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. Naciśnij klawisze **Ctrl+Shift+B**, aby skompilować klienta.

### <a name="example"></a>Przykład

Poniższy kod przedstawia bieżący stan pliku Program.cs w **EchoClient** projektu.

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

## <a name="configure-the-wcf-client"></a>Konfigurowanie klienta platformy WCF

W tym kroku zostanie utworzony plik App.config dla podstawowej aplikacji klienckiej uzyskującej dostęp do usługi utworzonej wcześniej w tym samouczku. Ten plik App.config definiuje kontrakt, powiązanie i nazwę punktu końcowego. Kod używany do wykonywania tych zadań podano w przykładzie zamieszczonym po procedurze.

1. W Eksploratorze rozwiązań kliknij projekt **EchoClient** i kliknij dwukrotnie plik **App.config**, aby otworzyć go w edytorze programu Visual Studio.
2. W elemencie `<appSettings>` zastąp symbole zastępcze nazwą przestrzeni nazw usługi i kluczem sygnatury dostępu współdzielonego skopiowanym we wcześniejszym kroku.
3. W elemencie system.serviceModel dodaj element `<client>`.

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
4. W elemencie `client` zdefiniuj nazwę, kontrakt i typ powiązania punktu końcowego.

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    Ten krok określa nazwę punktu końcowego i kontrakt zdefiniowany w usłudze i fakt, że aplikacja kliencka używa protokołu TCP do komunikowania się z przekaźnika usługi Azure. Nazwa punktu końcowego jest używana w następnym kroku do powiązania tej konfiguracji pliku końcowego z identyfikatorem URI usługi.
5. Kliknij przycisk **pliku**, następnie kliknij przycisk **Zapisz wszystko**.

## <a name="example"></a>Przykład

Poniższy kod przedstawia plik App.config dla klienta Echo.

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

## <a name="implement-the-wcf-client"></a>Implementowanie klienta platformy WCF
W tym kroku zostanie zaimplementowana podstawowa aplikacja kliencka uzyskująca dostęp do usługi utworzonej wcześniej w tym samouczku. Podobnie jak usługa, klient wykonuje wiele operacji przekazywania Azure dostępu do:

1. Ustawienie trybu łączności.
2. Utworzenie identyfikatora URI, który lokalizuje usługę hosta.
3. Uzyskanie poświadczeń zabezpieczeń.
4. Zastosowanie poświadczeń do połączenia.
5. Otwarcie połączenia.
6. Wykonanie zadań specyficznych dla aplikacji.
7. Zamknięcie połączenia.

Jedną z głównych różnic jest jednak czy aplikacja kliencka używa kanał połączyć się z usługą przekazywania, podczas gdy usługa korzysta z **ServiceHost**. Kod używany do wykonywania tych zadań podano w przykładzie zamieszczonym po procedurze.

### <a name="implement-a-client-application"></a>Wdrażanie aplikacji klienta
1. Ustaw tryb łączności **AutoDetect**. Dodaj następujący kod w metodzie `Main()` aplikacji **EchoClient**.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. Zdefiniuj zmienne do przechowywania wartości przestrzeni nazw i klucza sygnatury dostępu współdzielonego odczytanego z okna konsoli.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. Utwórz identyfikator URI, który określa lokalizację hosta w projekcie przekazywania.

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. Utwórz obiekt poświadczeń dla punktu końcowego przestrzeni nazw Twojej usługi.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. Utwórz fabrykę kanałów ładującą konfigurację opisaną w pliku App.config.

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    Fabryka kanałów jest obiektem platformy WCF tworzącym kanał komunikacyjny dla usługi i aplikacji klienckich.
6. Zastosuj poświadczenia.

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. Utwórz i otwórz kanał dla usługi.

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. Zapisz podstawowy interfejs użytkownika i funkcje dla echa.

    ```csharp
    Console.WriteLine("Enter text to echo (or [Enter] to exit):");
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

    W kodzie użyto wystąpienia obiektu kanału jako serwera proxy dla usługi.
9. Zamknij kanał i fabrykę.

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a>Przykład

Wypełniony kod powinien wyglądać następująco, jak utworzyć aplikację klienta, jak wywoływanie operacji usługi oraz sposób zamykania klienta po wywołaniu operacji zostało zakończone.

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

            Console.WriteLine("Enter text to echo (or [Enter] to exit):");
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

## <a name="run-the-applications"></a>Uruchamianie aplikacji

1. Naciśnij klawisze **Ctrl+Shift+B** w celu skompilowania rozwiązania. Powoduje to skompilowanie zarówno projektu klienta, jak i projektu usługi utworzonych w poprzednich krokach.
2. Przed uruchomieniem aplikacji klienckiej musisz upewnić się, że aplikacja usługi jest uruchomiona. W Eksploratorze rozwiązań w programie Visual Studio kliknij prawym przyciskiem myszy rozwiązanie **EchoService**, a następnie kliknij pozycję **Właściwości**.
3. W oknie dialogowym właściwości rozwiązania kliknij pozycję **Projekt startowy**, a następnie kliknij przycisk **Wiele projektów startowych**. Upewnij się, że pozycja **EchoService** jest wyświetlana na początku listy.
4. Ustaw w polu **Akcja** zarówno dla projektu **EchoService**, jak i projektu **EchoClient** ustawienie **Uruchom**.

    ![][5]
5. Kliknij pozycję **Zależności projektu**. W polu **Projekty** wybierz pozycję **EchoClient**. Upewnij się, że w polu **Zależny od** jest zaznaczona opcja **EchoService**.

    ![][6]
6. Kliknij przycisk **OK**, aby zamknąć okno dialogowe **Właściwości**.
7. Naciśnij klawisz **F5**, aby uruchomić oba projekty.
8. Oba okna konsoli zostaną otwarte z monitami o podanie nazwy przestrzeni nazw. Najpierw należy uruchomić usługę, dlatego w oknie konsoli **EchoService** wprowadź przestrzeń nazw, a następnie naciśnij klawisz **Enter**.
9. Następnie zostanie wyświetlony monit o podanie klucza sygnatury dostępu współdzielonego. Wprowadź klucz sygnatury dostępu współdzielonego i naciśnij klawisz ENTER.

    Oto przykładowe dane wyjściowe z okna konsoli. Poniższe wartości podano tutaj wyłącznie jako przykład.

    `Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`

    Aplikacja usługi wyświetla w oknie konsoli adres, na którym nasłuchuje, jak w poniższym przykładzie.

    `Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`
10. W oknie konsoli **EchoClient** wprowadź te same informacje, które zostały wprowadzone uprzednio dla aplikacji usługi. Wykonaj poprzednie kroki, aby wprowadzić tę samą przestrzeń nazw i klucz sygnatury dostępu współdzielonego dla aplikacji klienckiej.
11. Po wprowadzeniu tych wartości klient otworzy kanał do usługi i będzie monitować o wprowadzenie tekstu, jak w poniższym przykładzie danych wyjściowych konsoli.

    `Enter text to echo (or [Enter] to exit):`

    Wprowadź tekst, który zostanie wysłany do aplikacji usługi, i naciśnij klawisz Enter. Ten tekst jest wysyłany do usługi za pośrednictwem operacji usługi Echo i pojawia się w oknie konsoli usługi, jak w poniższym przykładzie danych wyjściowych.

    `Echoing: My sample text`

    Aplikacja kliencka odbiera wartość zwracaną przez operację `Echo`, która jest oryginalnym tekstem, i wyświetla go w oknie swojej konsoli. Poniżej przestawiono przykład danych wyjściowych z okna konsoli klienta.

    `Server echoed: My sample text`
12. Możesz kontynuować wysyłanie wiadomości tekstowych z klienta do usługi w ten sposób. Po zakończeniu naciśnij klawisz Enter w oknach konsoli klienta i usługi, aby zamknąć obie aplikacje.

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono sposób tworzenia klienta przekaźnika usługi Azure, aplikacji i usług przy użyciu funkcji WCF przekaźnika usługi Service Bus. Aby podobnego samouczka dotyczącego używa [usługi magistrali komunikatów](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), zobacz [Rozpoczynanie pracy z kolejek usługi Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

Aby dowiedzieć się więcej na temat przekaźnika usługi Azure, zobacz następujące tematy.

* [Omówienie architektury usługi Azure Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [Omówienie usługi Azure Relay](relay-what-is-it.md)
* [Jak używać przekaźnika usługi WCF z platformą .NET](relay-wcf-dotnet-get-started.md)

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
