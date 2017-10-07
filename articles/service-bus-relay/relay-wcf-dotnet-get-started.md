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
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="e100d-103">Jak toouse WCF przekazywania Azure przekazuje z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="e100d-103">How toouse Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="e100d-104">W tym artykule opisano, jak toouse hello Azure przekaźnika usługi.</span><span class="sxs-lookup"><span data-stu-id="e100d-104">This article describes how toouse hello Azure Relay service.</span></span> <span data-ttu-id="e100d-105">Hello przykłady są napisane w języku C# i używają interfejsu API Windows Communication Foundation (WCF) hello z rozszerzeniami zawartymi w hello zestawu usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e100d-105">hello samples are written in C# and use hello Windows Communication Foundation (WCF) API with extensions contained in hello Service Bus assembly.</span></span> <span data-ttu-id="e100d-106">Aby uzyskać więcej informacji na temat przekaźnika usługi Azure, zobacz hello [Omówienie przekaźnika usługi Azure](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="e100d-106">For more information about Azure relay, see hello [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="e100d-107">Co to jest przekazywania WCF?</span><span class="sxs-lookup"><span data-stu-id="e100d-107">What is WCF Relay?</span></span>

<span data-ttu-id="e100d-108">Hello Azure [ *przekazywania WCF* ](relay-what-is-it.md) usługa umożliwia toobuild hybrydowych aplikacji działających w centrum danych Azure i w lokalnym środowisku korporacyjnym.</span><span class="sxs-lookup"><span data-stu-id="e100d-108">hello Azure [*WCF Relay*](relay-what-is-it.md) service enables you toobuild hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="e100d-109">Usługa przekaźnika Hello ułatwia to umożliwiając toosecurely udostępnianie usług Windows Communication Foundation (WCF), które znajdują się w korporacyjnym środowisku sieci toohello chmury publicznej, bez konieczności tooopen połączenia zapory lub wymaganie Infrastruktura sieci firmowej tooa niepożądanych zmian.</span><span class="sxs-lookup"><span data-stu-id="e100d-109">hello relay service facilitates this by enabling you toosecurely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or requiring intrusive changes tooa corporate network infrastructure.</span></span>

![Pojęcia dotyczące przekaźnika WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="e100d-111">Przekaźnik Azure umożliwia toohost usług WCF w istniejącym środowisku korporacyjnym.</span><span class="sxs-lookup"><span data-stu-id="e100d-111">Azure Relay enables you toohost WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="e100d-112">Następnie można oddelegować nasłuchiwanie przychodzących sesji i żądań toothese usług toohello przekaźnika usługi WCF działającej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e100d-112">You can then delegate listening for incoming sessions and requests toothese WCF services toohello relay service running within Azure.</span></span> <span data-ttu-id="e100d-113">Dzięki temu można tooexpose te kodu tooapplication usługi uruchomione na platformie Azure, lub pracowników toomobile lub środowiskom partnerów w ekstranecie.</span><span class="sxs-lookup"><span data-stu-id="e100d-113">This enables you tooexpose these services tooapplication code running in Azure, or toomobile workers or extranet partner environments.</span></span> <span data-ttu-id="e100d-114">Przekazywanie umożliwia toosecurely kontroli, kto ma dostęp do tych usług na poziomie szczegółowych.</span><span class="sxs-lookup"><span data-stu-id="e100d-114">Relay enables you toosecurely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="e100d-115">Udostępnia funkcjonalność aplikacji tooexpose wydajny i bezpieczny sposób i dane z istniejących rozwiązań korporacyjnych i korzystanie z zalet go z hello chmury.</span><span class="sxs-lookup"><span data-stu-id="e100d-115">It provides a powerful and secure way tooexpose application functionality and data from your existing enterprise solutions and take advantage of it from hello cloud.</span></span>

<span data-ttu-id="e100d-116">W tym artykule opisano, jak toocreate przekazywania Azure toouse usługi sieci web WCF ujawnianej za pomocą powiązania kanału TCP, która implementuje bezpieczną konwersację między dwiema stronami.</span><span class="sxs-lookup"><span data-stu-id="e100d-116">This article discusses how toouse Azure Relay toocreate a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a><span data-ttu-id="e100d-117">Pobierz pakiet NuGet usługi Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="e100d-117">Get hello Service Bus NuGet package</span></span>
<span data-ttu-id="e100d-118">Witaj [pakietu NuGet usługi Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus) jest hello Najprostszym sposobem tooget hello interfejsu API usługi Service Bus i tooconfigure aplikacji ze wszystkimi zależnościami usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-118">hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is hello easiest way tooget hello Service Bus API and tooconfigure your application with all of hello Service Bus dependencies.</span></span> <span data-ttu-id="e100d-119">Pakiet NuGet hello tooinstall w projekcie, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="e100d-119">tooinstall hello NuGet package in your project, do hello following:</span></span>

1. <span data-ttu-id="e100d-120">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy pozycję **Odwołania**, a następnie kliknij pozycję **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e100d-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="e100d-121">Wyszukaj "Service Bus" i wybierz hello **Microsoft Azure Service Bus** elementu.</span><span class="sxs-lookup"><span data-stu-id="e100d-121">Search for "Service Bus" and select hello **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="e100d-122">Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij hello następujące okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="e100d-122">Click **Install** toocomplete hello installation, then close hello following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="e100d-123">Udostępnianie i korzystanie z usługi sieci web SOAP w przypadku protokołu TCP</span><span class="sxs-lookup"><span data-stu-id="e100d-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="e100d-124">tooexpose istniejącej usługi sieci web WCF SOAP wykorzystania zewnętrznego należy zmiany toohello usługi powiązań i adresów.</span><span class="sxs-lookup"><span data-stu-id="e100d-124">tooexpose an existing WCF SOAP web service for external consumption, you must make changes toohello service bindings and addresses.</span></span> <span data-ttu-id="e100d-125">Może to wymagać pliku konfiguracji tooyour zmiany lub może wymagać zmiany kodu, w zależności od tego, jak możesz mieć i konfigurowana usług WCF.</span><span class="sxs-lookup"><span data-stu-id="e100d-125">This may require changes tooyour configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="e100d-126">Należy zauważyć, że WCF pozwala toohave wielu punktów końcowych sieci za pośrednictwem hello tę samą usługę, dzięki czemu można zachować istniejące hello wewnętrznych punktów końcowych podczas dodawania punktów końcowych przekazywania dla użytku zewnętrznego dostęp na powitania sam czas.</span><span class="sxs-lookup"><span data-stu-id="e100d-126">Note that WCF allows you toohave multiple network endpoints over hello same service, so you can retain hello existing internal endpoints while adding relay endpoints for external access at hello same time.</span></span>

<span data-ttu-id="e100d-127">To zadanie służy do kompilacji prostą usługę WCF i dodawać tooit odbiornika przekazywania.</span><span class="sxs-lookup"><span data-stu-id="e100d-127">In this task, you build a simple WCF service and add a relay listener tooit.</span></span> <span data-ttu-id="e100d-128">Tym ćwiczeniu przyjęto założenie, masz pewną znajomość programu Visual Studio i w związku z tym nie omówiono wszystkich szczegółów hello tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="e100d-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all hello details of creating a project.</span></span> <span data-ttu-id="e100d-129">Zamiast tego należy go koncentruje się na powitania kodu.</span><span class="sxs-lookup"><span data-stu-id="e100d-129">Instead, it focuses on hello code.</span></span>

<span data-ttu-id="e100d-130">Przed rozpoczęciem tych kroków, wykonaj następujące procedury tooset Twojego środowiska hello:</span><span class="sxs-lookup"><span data-stu-id="e100d-130">Before starting these steps, complete hello following procedure tooset up your environment:</span></span>

1. <span data-ttu-id="e100d-131">W programie Visual Studio Utwórz aplikację konsoli, która zawiera dwa projekty — "Client" i "Usługa", w ramach rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within hello solution.</span></span>
2. <span data-ttu-id="e100d-132">Dodawanie projektów tooboth pakietu NuGet usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-132">Add hello Service Bus NuGet package tooboth projects.</span></span> <span data-ttu-id="e100d-133">Ten pakiet dodaje wszystkie projekty tooyour hello zestawu niezbędne odwołania.</span><span class="sxs-lookup"><span data-stu-id="e100d-133">This package adds all hello necessary assembly references tooyour projects.</span></span>

### <a name="how-toocreate-hello-service"></a><span data-ttu-id="e100d-134">Jak toocreate hello usługi</span><span class="sxs-lookup"><span data-stu-id="e100d-134">How toocreate hello service</span></span>
<span data-ttu-id="e100d-135">Najpierw należy utworzyć samą usługę hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-135">First, create hello service itself.</span></span> <span data-ttu-id="e100d-136">Każda usługa WCF składa się z co najmniej trzech oddzielnych części:</span><span class="sxs-lookup"><span data-stu-id="e100d-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="e100d-137">Definicja kontraktu, który opisuje jakie komunikaty są wymieniane i jakie operacje są wywoływane toobe.</span><span class="sxs-lookup"><span data-stu-id="e100d-137">Definition of a contract that describes what messages are exchanged and what operations are toobe invoked.</span></span>
* <span data-ttu-id="e100d-138">Implementacja tej Umowy.</span><span class="sxs-lookup"><span data-stu-id="e100d-138">Implementation of that contract.</span></span>
* <span data-ttu-id="e100d-139">Host, który obsługuje usługę WCF hello i udostępnia kilka punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="e100d-139">Host that hosts hello WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="e100d-140">Witaj przykłady kodu w tej sekcji dotyczą każdego z tych składników.</span><span class="sxs-lookup"><span data-stu-id="e100d-140">hello code examples in this section address each of these components.</span></span>

<span data-ttu-id="e100d-141">Witaj kontrakt definiuje jedną operację `AddNumbers`, która dodaje dwie liczby i zwraca wynik hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-141">hello contract defines a single operation, `AddNumbers`, that adds two numbers and returns hello result.</span></span> <span data-ttu-id="e100d-142">Witaj `IProblemSolverChannel` interfejs umożliwia powitania klienta toomore łatwe zarządzanie czasem życia powitania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="e100d-142">hello `IProblemSolverChannel` interface enables hello client toomore easily manage hello proxy lifetime.</span></span> <span data-ttu-id="e100d-143">Utworzenie takiego interfejsu jest traktowane jako najlepsze rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="e100d-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="e100d-144">Jest tooput dobrze tego kontraktu definicji w osobnym pliku, dzięki czemu możesz odwoływać ten plik z projektów obu "Client" i "Usługa", ale można również skopiować kod hello do obu tych projektów.</span><span class="sxs-lookup"><span data-stu-id="e100d-144">It's a good idea tooput this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy hello code into both projects.</span></span>

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

<span data-ttu-id="e100d-145">Z kontraktem hello w miejscu implementacja hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="e100d-145">With hello contract in place, hello implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="e100d-146">Programowe konfigurowanie hosta usługi</span><span class="sxs-lookup"><span data-stu-id="e100d-146">Configure a service host programmatically</span></span>
<span data-ttu-id="e100d-147">Hello kontrakt i implementacja są na miejscu można hostować hello usługi.</span><span class="sxs-lookup"><span data-stu-id="e100d-147">With hello contract and implementation in place, you can now host hello service.</span></span> <span data-ttu-id="e100d-148">Hosting następuje wewnątrz [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) obiektu, który zajmuje się zarządzaniem wystąpieniami usługi hello i hosty hello punkty końcowe nasłuchujące komunikatów.</span><span class="sxs-lookup"><span data-stu-id="e100d-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of hello service and hosts hello endpoints that listen for messages.</span></span> <span data-ttu-id="e100d-149">Hello poniższy kod umożliwia skonfigurowanie usługi hello zarówno standardowym lokalnym punktem końcowym i przekazywania punktu końcowego tooillustrate hello wyglądu, obok siebie, wewnętrznych i zewnętrznych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="e100d-149">hello following code configures hello service with both a regular local endpoint and a relay endpoint tooillustrate hello appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="e100d-150">Zastąp ciąg hello *przestrzeni nazw* z przestrzeni nazw i *yourKey* za hello klucza sygnatury dostępu Współdzielonego uzyskanym w poprzednim kroku konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-150">Replace hello string *namespace* with your namespace name and *yourKey* with hello SAS key that you obtained in hello previous setup step.</span></span>

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

<span data-ttu-id="e100d-151">W przykładzie hello utworzysz dwa punkty końcowe, które znajdują się na powitania sam kontraktu implementacji.</span><span class="sxs-lookup"><span data-stu-id="e100d-151">In hello example, you create two endpoints that are on hello same contract implementation.</span></span> <span data-ttu-id="e100d-152">Jeden jest lokalny, a drugi jest rzutowany za pośrednictwem przekaźnika usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="e100d-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="e100d-153">Witaj podstawowe różnice między nimi są powiązania hello; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) dla hello lokalna i [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) dla punktu końcowego przekazywania hello i hello adresów.</span><span class="sxs-lookup"><span data-stu-id="e100d-153">hello key differences between them are hello bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for hello local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for hello relay endpoint and hello addresses.</span></span> <span data-ttu-id="e100d-154">Witaj lokalny punkt końcowy ma adres sieci lokalnej z unikatowym portem.</span><span class="sxs-lookup"><span data-stu-id="e100d-154">hello local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="e100d-155">Witaj przekazywania punkt końcowy ma adres złożony z ciągu hello `sb`, przestrzeni nazw, a hello ścieżki "solver".</span><span class="sxs-lookup"><span data-stu-id="e100d-155">hello relay endpoint has an endpoint address composed of hello string `sb`, your namespace name, and hello path "solver."</span></span> <span data-ttu-id="e100d-156">Powoduje to hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identyfikowanie punktu końcowego usługi hello jako punktu końcowego TCP usługi Service Bus (przekaźnik) z w pełni kwalifikowana nazwa zewnętrzna DNS.</span><span class="sxs-lookup"><span data-stu-id="e100d-156">This results in hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying hello service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="e100d-157">Jeśli umieścisz kod hello, zastępując symbole zastępcze hello na powitania `Main` funkcja hello **usługi** aplikacji, konieczne będzie funkcjonalności usługi.</span><span class="sxs-lookup"><span data-stu-id="e100d-157">If you place hello code replacing hello placeholders into hello `Main` function of hello **Service** application, you will have a functional service.</span></span> <span data-ttu-id="e100d-158">Jeśli chcesz, aby Twoje toolisten usługi wyłącznie na powitania przekazywania, Usuń deklarację lokalnego punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-158">If you want your service toolisten exclusively on hello relay, remove hello local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-hello-appconfig-file"></a><span data-ttu-id="e100d-159">Konfigurowanie hosta usługi w pliku App.config hello</span><span class="sxs-lookup"><span data-stu-id="e100d-159">Configure a service host in hello App.config file</span></span>
<span data-ttu-id="e100d-160">Można również skonfigurować hosta hello przy użyciu pliku App.config hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-160">You can also configure hello host using hello App.config file.</span></span> <span data-ttu-id="e100d-161">Kod hostowania w tym przypadku usługi Hello pojawia się w następnym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-161">hello service hosting code in this case appears in hello next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="e100d-162">definicje punktu końcowego Hello Przenieś do pliku App.config hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-162">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="e100d-163">Hello pakiet NuGet już dodał szereg definicji toohello pliku App.config, które są hello wymagane rozszerzenia konfiguracji dla przekaźnika usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="e100d-163">hello NuGet package has already added a range of definitions toohello App.config file, which are hello required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="e100d-164">Witaj następujący przykład, który jest dokładny hello odpowiednikiem poprzedniego kodu hello, powinien pojawić się bezpośrednio pod hello **system.serviceModel** elementu.</span><span class="sxs-lookup"><span data-stu-id="e100d-164">hello following example, which is hello exact equivalent of hello previous code, should appear directly beneath hello **system.serviceModel** element.</span></span> <span data-ttu-id="e100d-165">Ten przykład kodu zakłada, że przestrzeń nazw języka C# w Twoim projekcie ma nazwę **Service**.</span><span class="sxs-lookup"><span data-stu-id="e100d-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="e100d-166">Zastąp symbole zastępcze hello z przekaźnika przestrzeni nazw i klucza sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="e100d-166">Replace hello placeholders with your relay namespace name and SAS key.</span></span>

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

<span data-ttu-id="e100d-167">Po wprowadzeniu tych zmian usługa hello jest uruchamiana tak jak poprzednio, ale z dwoma aktywnymi punktami końcowymi: jednym lokalnym i jednym nasłuchującym w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-167">After you make these changes, hello service starts as it did before, but with two live endpoints: one local and one listening in hello cloud.</span></span>

### <a name="create-hello-client"></a><span data-ttu-id="e100d-168">Utwórz powitania klienta</span><span class="sxs-lookup"><span data-stu-id="e100d-168">Create hello client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="e100d-169">Programowe konfigurowanie klienta</span><span class="sxs-lookup"><span data-stu-id="e100d-169">Configure a client programmatically</span></span>
<span data-ttu-id="e100d-170">tooconsume hello usługi, można utworzyć klienta WCF, za pomocą [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) obiektu.</span><span class="sxs-lookup"><span data-stu-id="e100d-170">tooconsume hello service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="e100d-171">Usługa Service Bus używa opartego na tokenie modelu zabezpieczeń, który jest implementowany z użyciem sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="e100d-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="e100d-172">Witaj [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) klasa reprezentuje dostawcę tokenu zabezpieczającego z wbudowanymi metodami factory zwracających niektórych dobrze znanych dostawców tokenu.</span><span class="sxs-lookup"><span data-stu-id="e100d-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="e100d-173">Witaj poniższym przykładzie użyto hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) metody toohandle hello nabycie hello odpowiedniego tokenu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="e100d-173">hello following example uses hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method toohandle hello acquisition of hello appropriate SAS token.</span></span> <span data-ttu-id="e100d-174">Witaj, nazwa i klucz są uzyskiwane z portalu hello zgodnie z opisem w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-174">hello name and key are those obtained from hello portal as described in hello previous section.</span></span>

<span data-ttu-id="e100d-175">Pierwszy, odniesienia lub kopia hello `IProblemSolver` kontraktu kodu z hello usługi do projektu client.</span><span class="sxs-lookup"><span data-stu-id="e100d-175">First, reference or copy hello `IProblemSolver` contract code from hello service into your client project.</span></span>

<span data-ttu-id="e100d-176">Następnie należy zastąpić kod hello w hello `Main` metody powitania klienta, ponownie zastępując tekst zastępczy hello przestrzeni nazw przekazywania i klucza sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="e100d-176">Then, replace hello code in hello `Main` method of hello client, again replacing hello placeholder text with your relay namespace and SAS key.</span></span>

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

<span data-ttu-id="e100d-177">Teraz można tworzyć powitania klienta i hello usługę, uruchomić je (najpierw uruchomić usługę hello), powitania klienta i wywołuje usługę hello drukuje **9**.</span><span class="sxs-lookup"><span data-stu-id="e100d-177">You can now build hello client and hello service, run them (run hello service first), and hello client calls hello service and prints **9**.</span></span> <span data-ttu-id="e100d-178">Można uruchomić powitania klienta i serwera na różnych maszynach, nawet za pośrednictwem sieci, a komunikacja hello będą nadal działać.</span><span class="sxs-lookup"><span data-stu-id="e100d-178">You can run hello client and server on different machines, even across networks, and hello communication will still work.</span></span> <span data-ttu-id="e100d-179">Kod klienta Hello można również uruchomić w chmurze hello lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="e100d-179">hello client code can also run in hello cloud or locally.</span></span>

#### <a name="configure-a-client-in-hello-appconfig-file"></a><span data-ttu-id="e100d-180">Konfigurowanie klienta w pliku App.config hello</span><span class="sxs-lookup"><span data-stu-id="e100d-180">Configure a client in hello App.config file</span></span>
<span data-ttu-id="e100d-181">Witaj następującego kodu pokazuje, jak tooconfigure powitania klienta przy użyciu hello pliku App.config.</span><span class="sxs-lookup"><span data-stu-id="e100d-181">hello following code shows how tooconfigure hello client using hello App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="e100d-182">definicje punktu końcowego Hello Przenieś do pliku App.config hello.</span><span class="sxs-lookup"><span data-stu-id="e100d-182">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="e100d-183">Witaj poniższy przykład, który jest hello taki sam jak hello kod przedstawiony poprzednio, powinien pojawić się bezpośrednio pod hello `<system.serviceModel>` elementu.</span><span class="sxs-lookup"><span data-stu-id="e100d-183">hello following example, which is hello same as hello code listed previously, should appear directly beneath hello `<system.serviceModel>` element.</span></span> <span data-ttu-id="e100d-184">W tym miejscu jak poprzednio, należy zastąpić symbole zastępcze hello przekazywania przestrzeni nazw i klucza sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="e100d-184">Here, as before, you must replace hello placeholders with your relay namespace and SAS key.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e100d-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e100d-185">Next steps</span></span>
<span data-ttu-id="e100d-186">Teraz, kiedy znasz już podstawy hello Azure przekazywania, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="e100d-186">Now that you've learned hello basics of Azure Relay, follow these links toolearn more.</span></span>

* [<span data-ttu-id="e100d-187">Co to jest usługa Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="e100d-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="e100d-188">Omówienie architektury usługi Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="e100d-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="e100d-189">Pobierz przykłady usługi Service Bus z [przykładów dla platformy Azure] [ Azure samples] lub zobacz hello [Przegląd przykładów usługi Service Bus][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="e100d-189">Download Service Bus samples from [Azure samples][Azure samples] or see hello [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
