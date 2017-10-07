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
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="1f3cd-103">Samouczek usługi Azure przekaźnika usługi WCF</span><span class="sxs-lookup"><span data-stu-id="1f3cd-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="1f3cd-104">W tym samouczku opisano, jak toobuild proste WCF przekazywania aplikacji klienckiej i usługi przy użyciu przekaźnika usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-104">This tutorial describes how toobuild a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="1f3cd-105">Aby podobnego samouczka dotyczącego używa [usługi magistrali komunikatów](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), zobacz [Rozpoczynanie pracy z kolejek usługi Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="1f3cd-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="1f3cd-106">Ten samouczek umożliwia poznanie kroków hello, które są wymagane toocreate aplikacji klienta i usługi przekaźnika usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-106">Working through this tutorial gives you an understanding of hello steps that are required toocreate a WCF Relay client and service application.</span></span> <span data-ttu-id="1f3cd-107">Podobnie jak ich odpowiedniki WCF oryginalnej usługa jest strukturą ujawniającą jeden lub więcej punktów końcowych, z których każdy ujawnia co najmniej jedną operację usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="1f3cd-108">Witaj punkt końcowy usługi Określa adres gdzie można znaleźć usługi hello, powiązanie zawierające informacje powitania klienta muszą komunikować się z usługą hello i kontrakt definiujący hello funkcje udostępniane przez klientów tooits usługi hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-108">hello endpoint of a service specifies an address where hello service can be found, a binding that contains hello information that a client must communicate with hello service, and a contract that defines hello functionality provided by hello service tooits clients.</span></span> <span data-ttu-id="1f3cd-109">Witaj podstawowa różnica między WCF i przekazywania WCF jest ten punkt końcowy hello jest widoczna w chmurze hello zamiast lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-109">hello main difference between WCF and WCF Relay is that hello endpoint is exposed in hello cloud instead of locally on your computer.</span></span>

<span data-ttu-id="1f3cd-110">Po zakończeniu pracy hello sekwencją tematów w tym samouczku, będzie mieć uruchomioną usługę i klienta, który można wywołać operacji hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-110">After you work through hello sequence of topics in this tutorial, you will have a running service, and a client that can invoke hello operations of hello service.</span></span> <span data-ttu-id="1f3cd-111">Witaj w pierwszym temacie opisano sposób tooset konta.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-111">hello first topic describes how tooset up an account.</span></span> <span data-ttu-id="1f3cd-112">Witaj następne kroki opisują sposób toodefine usługi używającej kontraktu, jak tooimplement hello usługi i jak tooconfigure hello usługi w kodzie.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-112">hello next steps describe how toodefine a service that uses a contract, how tooimplement hello service, and how tooconfigure hello service in code.</span></span> <span data-ttu-id="1f3cd-113">Opisano również sposób toohost i uruchom usługi hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-113">They also describe how toohost and run hello service.</span></span> <span data-ttu-id="1f3cd-114">Witaj usługi, która jest tworzona jest samodzielnie hostowana i powitania klienta i usługa są uruchomione na powitania tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-114">hello service that is created is self-hosted and hello client and service run on hello same computer.</span></span> <span data-ttu-id="1f3cd-115">Usługa hello można skonfigurować przy użyciu kodu lub pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-115">You can configure hello service by using either code or a configuration file.</span></span>

<span data-ttu-id="1f3cd-116">Witaj ostatnie trzy kroki opisują sposób toocreate aplikacji klienckiej, konfigurowania powitania klienta aplikacji, tworzenie i użycia klienta, który można uzyskać dostępu do funkcji hello hello hosta.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-116">hello final three steps describe how toocreate a client application, configure hello client application, and create and use a client that can access hello functionality of hello host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f3cd-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1f3cd-117">Prerequisites</span></span>

<span data-ttu-id="1f3cd-118">toocomplete tego samouczka będziesz potrzebować hello następujące:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-118">toocomplete this tutorial, you'll need hello following:</span></span>

* <span data-ttu-id="1f3cd-119">[Program Microsoft Visual Studio w wersji 2015 lub nowszej](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="1f3cd-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="1f3cd-120">W tym samouczku korzysta z programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="1f3cd-121">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-121">An active Azure account.</span></span> <span data-ttu-id="1f3cd-122">Jeśli go nie masz, możesz utworzyć bezpłatne konto w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="1f3cd-123">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1f3cd-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="1f3cd-124">Tworzenie przestrzeni nazw usługi</span><span class="sxs-lookup"><span data-stu-id="1f3cd-124">Create a service namespace</span></span>

<span data-ttu-id="1f3cd-125">pierwszym krokiem Hello jest toocreate przestrzeni nazw i tooobtain [dostępu sygnatury dostępu Współdzielonego](../service-bus-messaging/service-bus-sas.md) klucza.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-125">hello first step is toocreate a namespace, and tooobtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="1f3cd-126">Przestrzeń nazw wyznacza granice aplikacji dla każdej aplikacji widocznej za pośrednictwem usługi przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-126">A namespace provides an application boundary for each application exposed through hello relay service.</span></span> <span data-ttu-id="1f3cd-127">Klucz sygnatury dostępu Współdzielonego jest automatycznie generowane przez system powitania po utworzeniu przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-127">A SAS key is automatically generated by hello system when a service namespace is created.</span></span> <span data-ttu-id="1f3cd-128">Hello kombinacji przestrzeni nazw usługi i klucza sygnatury dostępu Współdzielonego zapewnia poświadczenia hello Azure tooauthenticate dostępu tooan aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-128">hello combination of service namespace and SAS key provides hello credentials for Azure tooauthenticate access tooan application.</span></span> <span data-ttu-id="1f3cd-129">Wykonaj hello [instrukcje w tym miejscu](relay-create-namespace-portal.md) toocreate przekazywania przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-129">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="1f3cd-130">Definiowanie kontraktu usługi WCF</span><span class="sxs-lookup"><span data-stu-id="1f3cd-130">Define a WCF service contract</span></span>

<span data-ttu-id="1f3cd-131">kontrakt usługi Hello Określa, jakie operacje (hello terminologia usługi sieci web dla metod lub funkcji) hello usługa obsługuje.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-131">hello service contract specifies what operations (hello web service terminology for methods or functions) hello service supports.</span></span> <span data-ttu-id="1f3cd-132">Kontrakty są tworzone przez definiowanie interfejsu C++, C# lub Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="1f3cd-133">Każda metoda w interfejsie hello odpowiada tooa określonej operacji usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-133">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="1f3cd-134">Każdego interfejsu należy zastosować hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) tooit zastosować atrybutu i każdej operacji musi być hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit atrybut zastosowany.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-134">Each interface must have hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied tooit, and each operation must have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied tooit.</span></span> <span data-ttu-id="1f3cd-135">Jeśli metoda w interfejsie z atrybutem hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atrybut nie ma hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) atrybutu — metoda nie jest uwidaczniana.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-135">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="1f3cd-136">Hello kod dla tych zadań podano w przykład Witaj hello procedury.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-136">hello code for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="1f3cd-137">Aby uzyskać bardziej szczegółowo omówiono kontrakty i usługi, zobacz [projektowanie i Implementowanie usług](https://msdn.microsoft.com/library/ms729746.aspx) w hello dokumentacji usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in hello WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="1f3cd-138">Tworzenie kontraktu przekazywania przy użyciu interfejsu</span><span class="sxs-lookup"><span data-stu-id="1f3cd-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="1f3cd-139">Otwórz program Visual Studio jako administrator, klikając prawym przyciskiem myszy program hello w hello **Start** menu i wybierając **Uruchom jako administrator**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-139">Open Visual Studio as an administrator by right-clicking hello program in hello **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="1f3cd-140">Utwórz nowy projekt aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-140">Create a new console application project.</span></span> <span data-ttu-id="1f3cd-141">Kliknij przycisk hello **pliku** menu i wybierz **nowy**, następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-141">Click hello **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="1f3cd-142">W hello **nowy projekt** okna dialogowego, kliknij przycisk **Visual C#** (Jeśli **Visual C#** nie jest wyświetlana, sprawdź w obszarze **inne języki**).</span><span class="sxs-lookup"><span data-stu-id="1f3cd-142">In hello **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="1f3cd-143">Kliknij przycisk hello **aplikacji konsoli (.NET Framework)** szablonu i nadaj mu nazwę **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-143">Click hello **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="1f3cd-144">Kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-144">Click **OK** toocreate hello project.</span></span>

    ![][2]

3. <span data-ttu-id="1f3cd-145">Zainstaluj pakiet NuGet usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-145">Install hello Service Bus NuGet package.</span></span> <span data-ttu-id="1f3cd-146">Ten pakiet automatycznie dodaje bibliotek usługi Service Bus toohello odwołania, a także hello WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-146">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="1f3cd-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) jest hello przestrzeni nazw, która pozwala tooprogrammatically dostępu hello podstawowych funkcji usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables you tooprogrammatically access hello basic features of WCF.</span></span> <span data-ttu-id="1f3cd-148">Usługa Service Bus używa wielu hello obiektów i atrybutów kontraktów usług WCF toodefine.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-148">Service Bus uses many of hello objects and attributes of WCF toodefine service contracts.</span></span>

    <span data-ttu-id="1f3cd-149">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** . Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-149">In Solution Explorer, right-click hello project, and then click **Manage NuGet Packages...**. Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="1f3cd-150">Upewnij się, że nazwa projektu hello jest zaznaczona w hello **wersje** pole.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-150">Ensure that hello project name is selected in hello **Version(s)** box.</span></span> <span data-ttu-id="1f3cd-151">Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-151">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="1f3cd-152">W Eksploratorze rozwiązań kliknij dwukrotnie tooopen pliku Program.cs hello on w edytorze hello, jeśli nie jest jeszcze otwarty.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-152">In Solution Explorer, double-click hello Program.cs file tooopen it in hello editor, if it is not already open.</span></span>
5. <span data-ttu-id="1f3cd-153">Dodaj hello następujące instrukcje using u góry pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-153">Add hello following using statements at hello top of hello file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="1f3cd-154">Nazwa przestrzeni nazw hello zmiany z domyślnej nazwy **EchoService** za**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-154">Change hello namespace name from its default name of **EchoService** too**Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1f3cd-155">W tym samouczku używana przestrzeń nazw hello C# **Microsoft.ServiceBus.Samples**, czyli hello nazw hello na podstawie umowy zarządzanego typu, który jest używany w pliku konfiguracyjnym hello w hello [klienta WCF hello Konfiguruj](#configure-the-wcf-client) kroku.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-155">This tutorial uses hello C# namespace **Microsoft.ServiceBus.Samples**, which is hello namespace of hello contract-based managed type that is used in hello configuration file in hello [Configure hello WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="1f3cd-156">Można określić dowolną przestrzeń nazw podczas kompilowania tego przykładu; jednak hello samouczek nie będzie działać, jeśli nie zmodyfikujesz następnie przestrzeni nazw hello hello kontraktu i usługi, w pliku konfiguracyjnym aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-156">You can specify any namespace you want when you build this sample; however, hello tutorial will not work unless you then modify hello namespaces of hello contract and service accordingly, in hello application configuration file.</span></span> <span data-ttu-id="1f3cd-157">Witaj przestrzeń nazw określona w hello App.config plik musi być hello sam hello przestrzeń nazw określona w plikach C#.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-157">hello namespace specified in hello App.config file must be hello same as hello namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="1f3cd-158">Bezpośrednio po hello `Microsoft.ServiceBus.Samples` deklaracji przestrzeni nazw, ale w ramach hello przestrzeni nazw, zdefiniuj nowy interfejs o nazwie `IEchoContract` i zastosować hello `ServiceContractAttribute` atrybutu toohello interfejsu z wartością przestrzeni nazw `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-158">Directly after hello `Microsoft.ServiceBus.Samples` namespace declaration, but within hello namespace, define a new interface named `IEchoContract` and apply hello `ServiceContractAttribute` attribute toohello interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="1f3cd-159">Wartość przestrzeni nazw Hello różni się od przestrzeni nazw hello, używanej w całym zakresie hello kodu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-159">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="1f3cd-160">Zamiast tego wartość przestrzeni nazw hello jest używany jako unikatowy identyfikator dla tego kontraktu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-160">Instead, hello namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="1f3cd-161">Jawne określenie hello przestrzeni nazw zapobiega dodawaniu Nazwa kontraktu toohello hello domyślnej wartości przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-161">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span> <span data-ttu-id="1f3cd-162">Wklej hello następującego kodu po deklaracji przestrzeni nazw hello:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-162">Paste hello following code after hello namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="1f3cd-163">Zwykle hello przestrzeń nazw kontraktu usługi zawiera schemat nazewnictwa uwzględniający informacje o wersji.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-163">Typically, hello service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="1f3cd-164">W tym informacje o wersji w przestrzeni nazw kontraktu usługi hello umożliwia usług tooisolate najważniejszych zmian przez zdefiniowanie nowego kontraktu usługi z nowej przestrzeni nazw i ujawnienie go na nowy punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-164">Including version information in hello service contract namespace enables services tooisolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="1f3cd-165">W ten sposób klienci mogą nadal toouse hello starego kontraktu usługi bez konieczności toobe aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-165">In this manner, clients can continue toouse hello old service contract without having toobe updated.</span></span> <span data-ttu-id="1f3cd-166">Informacje o wersji mogą zawierać datę lub numer kompilacji.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-166">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="1f3cd-167">Aby uzyskać więcej informacji, zobacz [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498) (Obsługa wersji usług).</span><span class="sxs-lookup"><span data-stu-id="1f3cd-167">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="1f3cd-168">Witaj celów tego samouczka hello nazewnictwa schematu przestrzeni nazw kontraktu usługi hello nie zawiera informacje o wersji.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-168">For hello purposes of this tutorial, hello naming scheme of hello service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="1f3cd-169">W ramach hello `IEchoContract` interfejsu, Zadeklaruj metodę dla hello jednej operacji hello `IEchoContract` ujawnia kontraktu w hello na interfejsie i Zastosuj hello `OperationContractAttribute` atrybutu toohello metodę, która ma tooexpose jako część hello publicznego przekaźnika usługi WCF kontraktu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-169">Within hello `IEchoContract` interface, declare a method for hello single operation hello `IEchoContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="1f3cd-170">Bezpośrednio po hello `IEchoContract` definicji interfejsu, Zadeklaruj kanał dziedziczący z `IEchoContract` , a także toohello `IClientChannel` interfejsu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-170">Directly after hello `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also toohello `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="1f3cd-171">Kanał jest obiektem usługi WCF hello za pomocą którego hello host i klient przekazują tooeach informacje o innych.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-171">A channel is hello WCF object through which hello host and client pass information tooeach other.</span></span> <span data-ttu-id="1f3cd-172">Później napiszesz kod względem hello kanału tooecho informacji między dwiema aplikacjami hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-172">Later, you will write code against hello channel tooecho information between hello two applications.</span></span>
10. <span data-ttu-id="1f3cd-173">Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** lub naciśnij klawisz **Ctrl + Shift + B** tooconfirm hello dokładność pracy wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-173">From hello **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="1f3cd-174">Przykład</span><span class="sxs-lookup"><span data-stu-id="1f3cd-174">Example</span></span>

<span data-ttu-id="1f3cd-175">powitania po kod przedstawia podstawowy interfejs definiujący kontrakt usługi WCF przekazywania.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-175">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

<span data-ttu-id="1f3cd-176">Teraz, gdy hello interfejs został utworzony, można zaimplementować interfejsu hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-176">Now that hello interface is created, you can implement hello interface.</span></span>

## <a name="implement-hello-wcf-contract"></a><span data-ttu-id="1f3cd-177">Implementowanie hello WCF kontraktu</span><span class="sxs-lookup"><span data-stu-id="1f3cd-177">Implement hello WCF contract</span></span>

<span data-ttu-id="1f3cd-178">Tworzenie przekazywania Azure wymaga, należy najpierw utworzyć kontrakt hello, który został zdefiniowany przy użyciu interfejsu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-178">Creating an Azure relay requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="1f3cd-179">Aby uzyskać więcej informacji na temat tworzenia interfejsu hello Zobacz hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-179">For more information about creating hello interface, see hello previous step.</span></span> <span data-ttu-id="1f3cd-180">Witaj następnym krokiem jest tooimplement hello interfejsu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-180">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="1f3cd-181">Obejmuje to tworzenie klasy o nazwie `EchoService` hello zdefiniowane przez użytkownika, który zawiera `IEchoContract` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-181">This involves creating a class named `EchoService` that implements hello user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="1f3cd-182">Po zaimplementowaniu interfejsu hello, następnie należy skonfigurować interfejs hello przy użyciu pliku konfiguracji App.config.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-182">After you implement hello interface, you then configure hello interface using an App.config configuration file.</span></span> <span data-ttu-id="1f3cd-183">Witaj plik konfiguracji zawiera niezbędne informacje dotyczące aplikacji hello, takie jak nazwa hello hello usługi, nazwa hello hello kontraktu i typ hello protokołu, który jest używany toocommunicate z usługą przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-183">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="1f3cd-184">Kod Hello używany do wykonywania tych zadań podano w przykład Witaj hello procedury.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-184">hello code used for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="1f3cd-185">Aby uzyskać bardziej ogólne omówienie sposobu kontraktu tooimplement usługi, zobacz [Implementowanie kontraktów usług](https://msdn.microsoft.com/library/ms733764.aspx) w hello dokumentacji usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-185">For a more general discussion about how tooimplement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in hello WCF documentation.</span></span>

1. <span data-ttu-id="1f3cd-186">Utwórz nową klasę o nazwie `EchoService` bezpośrednio po definicji hello hello `IEchoContract` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-186">Create a new class named `EchoService` directly after hello definition of hello `IEchoContract` interface.</span></span> <span data-ttu-id="1f3cd-187">Witaj `EchoService` klasa implementuje hello `IEchoContract` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-187">hello `EchoService` class implements hello `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="1f3cd-188">Podobne implementacje interfejsu tooother, można zaimplementować definicję hello w innym pliku.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-188">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="1f3cd-189">Jednak w tym samouczku implementacji hello znajduje się w hello tego samego pliku jako hello definicja interfejsu i hello `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-189">However, for this tutorial, hello implementation is located in hello same file as hello interface definition and hello `Main` method.</span></span>
2. <span data-ttu-id="1f3cd-190">Zastosuj hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atrybutu toohello `IEchoContract` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-190">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello `IEchoContract` interface.</span></span> <span data-ttu-id="1f3cd-191">Atrybut Hello określa hello nazwę usługi i przestrzeń nazw.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-191">hello attribute specifies hello service name and namespace.</span></span> <span data-ttu-id="1f3cd-192">Po wykonaniu tej czynności, hello `EchoService` klasy wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-192">After doing so, hello `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="1f3cd-193">Implementowanie hello `Echo` metody zdefiniowanej w hello `IEchoContract` interfejsu w hello `EchoService` klasy.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-193">Implement hello `Echo` method defined in hello `IEchoContract` interface in hello `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="1f3cd-194">Kliknij przycisk **kompilacji**, następnie kliknij przycisk **Kompiluj rozwiązanie** tooconfirm hello dokładność wykonanej pracy.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-194">Click **Build**, then click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="define-hello-configuration-for-hello-service-host"></a><span data-ttu-id="1f3cd-195">Definiowanie konfiguracji hello hello hosta usługi</span><span class="sxs-lookup"><span data-stu-id="1f3cd-195">Define hello configuration for hello service host</span></span>

1. <span data-ttu-id="1f3cd-196">plik konfiguracji Hello jest bardzo podobne pliku konfiguracji usługi WCF tooa.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-196">hello configuration file is very similar tooa WCF configuration file.</span></span> <span data-ttu-id="1f3cd-197">Zawiera nazwę usługi hello, punkt końcowy (to znaczy hello lokalizację ujawniający przekazywania Azure dla klientów i hosty toocommunicate ze sobą) i hello powiązanie (typ hello protokół, który jest używany toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="1f3cd-197">It includes hello service name, endpoint (that is, hello location that Azure Relay exposes for clients and hosts toocommunicate with each other), and hello binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="1f3cd-198">Witaj główną różnicą jest to skonfigurowanego punktu końcowego usługi tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) powiązania, który nie jest częścią hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-198">hello main difference is that this configured service endpoint refers tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of hello .NET Framework.</span></span> <span data-ttu-id="1f3cd-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) jest jednym z powiązań hello zdefiniowanych przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of hello bindings defined by hello service.</span></span>
2. <span data-ttu-id="1f3cd-200">W **Eksploratora rozwiązań**, kliknij dwukrotnie tooopen pliku App.config hello go w edytorze programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-200">In **Solution Explorer**, double-click hello App.config file tooopen it in hello Visual Studio editor.</span></span>
3. <span data-ttu-id="1f3cd-201">W hello `<appSettings>` elementu, zastąp symbole zastępcze hello hello nazwą przestrzeni nazw usługi i hello klucza sygnatury dostępu Współdzielonego, który został skopiowany w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-201">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="1f3cd-202">W ramach hello `<system.serviceModel>` Dodaj tagi, `<services>` elementu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-202">Within hello `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="1f3cd-203">Wiele aplikacji przekazywania można zdefiniować w pojedynczym pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-203">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="1f3cd-204">W tym samouczku zdefiniowano jednak tylko jedną.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-204">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="1f3cd-205">W ramach hello `<services>` elementu, Dodaj `<service>` nazwa hello toodefine elementu hello usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-205">Within hello `<services>` element, add a `<service>` element toodefine hello name of hello service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="1f3cd-206">W ramach hello `<service>` elementu, zdefiniuj lokalizację kontraktu punktu końcowego hello hello, a także hello wpisz powiązanie dla punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-206">Within hello `<service>` element, define hello location of hello endpoint contract, and also hello type of binding for hello endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="1f3cd-207">punkt końcowy Hello definiuje, gdzie powitania klienta będzie szukać aplikacji hosta hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-207">hello endpoint defines where hello client will look for hello host application.</span></span> <span data-ttu-id="1f3cd-208">Później hello samouczku ten krok toocreate identyfikator URI, który w pełni ujawnia hosta hello za pośrednictwem przekaźnika usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-208">Later, hello tutorial uses this step toocreate a URI that fully exposes hello host through Azure Relay.</span></span> <span data-ttu-id="1f3cd-209">Witaj powiązanie deklaruje, że TCP jest używany jako hello toocommunicate protokołu z usługą przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-209">hello binding declares that we are using TCP as hello protocol toocommunicate with hello relay service.</span></span>
7. <span data-ttu-id="1f3cd-210">Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** tooconfirm hello dokładność wykonanej pracy.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-210">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="1f3cd-211">Przykład</span><span class="sxs-lookup"><span data-stu-id="1f3cd-211">Example</span></span>

<span data-ttu-id="1f3cd-212">Witaj poniższy kod przedstawia implementację hello hello kontraktu usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-212">hello following code shows hello implementation of hello service contract.</span></span>

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

<span data-ttu-id="1f3cd-213">Witaj poniższy kod przedstawia podstawowy format pliku App.config hello skojarzona z hostem usługi hello hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-213">hello following code shows hello basic format of hello App.config file associated with hello service host.</span></span>

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

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a><span data-ttu-id="1f3cd-214">Hostowanie i uruchamianie tooregister usługi sieci web podstawowe z usługą przekazywania hello</span><span class="sxs-lookup"><span data-stu-id="1f3cd-214">Host and run a basic web service tooregister with hello relay service</span></span>

<span data-ttu-id="1f3cd-215">W tym kroku opisano, jak toorun Azure przekazywania usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-215">This step describes how toorun an Azure Relay service.</span></span>

### <a name="create-hello-relay-credentials"></a><span data-ttu-id="1f3cd-216">Utwórz hello przekazywania poświadczeń</span><span class="sxs-lookup"><span data-stu-id="1f3cd-216">Create hello relay credentials</span></span>

1. <span data-ttu-id="1f3cd-217">W `Main()`, Utwórz dwie zmienne, w których toostore hello nazw i klucza sygnatury dostępu Współdzielonego, które są odczytywane z okna konsoli hello hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-217">In `Main()`, create two variables in which toostore hello namespace and hello SAS key that are read from hello console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="1f3cd-218">klucz sygnatury dostępu Współdzielonego Hello będą używane nowsze tooaccess Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-218">hello SAS key will be used later tooaccess your project.</span></span> <span data-ttu-id="1f3cd-219">przestrzeń nazw Hello jest przekazywana jako parametr zbyt`CreateServiceUri` toocreate identyfikator URI usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-219">hello namespace is passed as a parameter too`CreateServiceUri` toocreate a service URI.</span></span>
2. <span data-ttu-id="1f3cd-220">Przy użyciu [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) , Zadeklaruj, że będziesz używać klucza sygnatury dostępu Współdzielonego jako typu poświadczeń hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-220">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as hello credential type.</span></span> <span data-ttu-id="1f3cd-221">Dodaj następujące kod bezpośrednio po hello kodzie dodanym w ostatnim kroku hello hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-221">Add hello following code directly after hello code added in hello last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a><span data-ttu-id="1f3cd-222">Utwórz adres podstawowy usługi hello</span><span class="sxs-lookup"><span data-stu-id="1f3cd-222">Create a base address for hello service</span></span>

<span data-ttu-id="1f3cd-223">Po kodzie hello dodanym w ostatnim kroku hello utworzyć `Uri` wystąpienie dla adresu podstawowego hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-223">After hello code you added in hello last step, create a `Uri` instance for hello base address of hello service.</span></span> <span data-ttu-id="1f3cd-224">Ten identyfikator URI Określa schemat magistrali usług hello, hello przestrzeni nazw i hello ścieżkę interfejsu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-224">This URI specifies hello Service Bus scheme, hello namespace, and hello path of hello service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="1f3cd-225">"sb" stanowi skrót od hello schemat magistrali usług i wskazuje, że TCP jest używany protokół hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-225">"sb" is an abbreviation for hello Service Bus scheme, and indicates that we are using TCP as hello protocol.</span></span> <span data-ttu-id="1f3cd-226">Wskazano to również uprzednio w pliku konfiguracyjnym hello, gdy [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) został określony w powiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-226">This was also previously indicated in hello configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as hello binding.</span></span>

<span data-ttu-id="1f3cd-227">W tym samouczku hello identyfikator URI jest `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-227">For this tutorial, hello URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-hello-service-host"></a><span data-ttu-id="1f3cd-228">Tworzenie i Konfigurowanie hosta usługi hello</span><span class="sxs-lookup"><span data-stu-id="1f3cd-228">Create and configure hello service host</span></span>

1. <span data-ttu-id="1f3cd-229">Ustaw tryb łączności hello zbyt`AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-229">Set hello connectivity mode too`AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="1f3cd-230">Witaj tryb łączności opisuje toocommunicate hello protokołu hello używa usługi z usługą przekazywania hello; protokołu HTTP lub TCP.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-230">hello connectivity mode describes hello protocol hello service uses toocommunicate with hello relay service; either HTTP or TCP.</span></span> <span data-ttu-id="1f3cd-231">Przy użyciu ustawienia domyślne hello `AutoDetect`, usługa hello podejmuje tooAzure tooconnect przekazywania za pośrednictwem protokołu TCP, jeśli jest dostępna i HTTP, jeśli protokół TCP nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-231">Using hello default setting `AutoDetect`, hello service attempts tooconnect tooAzure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="1f3cd-232">Określa Uwaga ta różni się od hello protokołu hello usługi do komunikacji z klientem.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-232">Note that this differs from hello protocol hello service specifies for client communication.</span></span> <span data-ttu-id="1f3cd-233">Ten protokół jest ustalany przez powiązanie hello używane.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-233">That protocol is determined by hello binding used.</span></span> <span data-ttu-id="1f3cd-234">Na przykład usługa może używać hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) powiązania, który określa, że jej punkt końcowy komunikuje się z klientami za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-234">For example, a service can use hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="1f3cd-235">Czy sama usługa może określać **ConnectivityMode.AutoDetect** tak, aby usługa hello komunikuje się z przekaźnika usługi Azure za pośrednictwem protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-235">That same service could specify **ConnectivityMode.AutoDetect** so that hello service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="1f3cd-236">Utwórz hosta usługi hello, za pomocą powitalne identyfikatora URI utworzonego wcześniej w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-236">Create hello service host, using hello URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="1f3cd-237">host usługi Hello jest hello WCF obiekt, który tworzy hello usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-237">hello service host is hello WCF object that instantiates hello service.</span></span> <span data-ttu-id="1f3cd-238">W tym miejscu możesz przekazać typ hello usługi ma toocreate ( `EchoService` typu) i również adres toohello ma tooexpose hello usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-238">Here, you pass it hello type of service you want toocreate (an `EchoService` type), and also toohello address at which you want tooexpose hello service.</span></span>
3. <span data-ttu-id="1f3cd-239">U góry pliku Program.cs hello hello, dodaj odwołania do zbyt[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) i [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="1f3cd-239">At hello top of hello Program.cs file, add references too[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="1f3cd-240">W `Main()`, skonfiguruj hello punktu końcowego tooenable publicznie.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-240">Back in `Main()`, configure hello endpoint tooenable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="1f3cd-241">Ten krok informuje usługi przekazywania hello czy aplikacji może być znajdowana przez zbadanie źródła danych ATOM hello projektu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-241">This step informs hello relay service that your application can be found publicly by examining hello ATOM feed for your project.</span></span> <span data-ttu-id="1f3cd-242">Jeśli ustawisz **DiscoveryType** za**prywatnej**, klient nadal będą mogli tooaccess hello usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-242">If you set **DiscoveryType** too**private**, a client would still be able tooaccess hello service.</span></span> <span data-ttu-id="1f3cd-243">Jednak usługa hello nie pojawią się podczas wyszukiwania hello przekazywania w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-243">However, hello service would not appear when it searches hello Relay namespace.</span></span> <span data-ttu-id="1f3cd-244">Zamiast tego powitania klienta musi ścieżkę punktu końcowego hello tooknow wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-244">Instead, hello client would have tooknow hello endpoint path beforehand.</span></span>
5. <span data-ttu-id="1f3cd-245">Zastosuj poświadczenia usługi hello toohello punktów końcowych usługi zdefiniowane w pliku App.config hello:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-245">Apply hello service credentials toohello service endpoints defined in hello App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="1f3cd-246">Jak już wspomniano w poprzednim kroku hello, możesz zadeklarować kilka usług i punktów końcowych w pliku konfiguracyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-246">As stated in hello previous step, you could have declared multiple services and endpoints in hello configuration file.</span></span> <span data-ttu-id="1f3cd-247">Jeśli użytkownik ma, ten kod pomijałby plik konfiguracji hello i wyszukiwania dla każdego punktu końcowego toowhich powinien zastosować Twoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-247">If you had, this code would traverse hello configuration file and search for every endpoint toowhich it should apply your credentials.</span></span> <span data-ttu-id="1f3cd-248">W tym samouczku plik konfiguracyjny hello ma tylko jeden punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-248">However, for this tutorial, hello configuration file has only one endpoint.</span></span>

### <a name="open-hello-service-host"></a><span data-ttu-id="1f3cd-249">Otwórz hello hosta usługi</span><span class="sxs-lookup"><span data-stu-id="1f3cd-249">Open hello service host</span></span>

1. <span data-ttu-id="1f3cd-250">Otwórz usługę hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-250">Open hello service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="1f3cd-251">Powiadamia użytkownika hello hello usługa jest uruchomiona i opisano sposób tooshut dół hello usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-251">Inform hello user that hello service is running, and explain how tooshut down hello service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="1f3cd-252">Po zakończeniu zamknij hosta usługi hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-252">When finished, close hello service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="1f3cd-253">Naciśnij klawisz **Ctrl + Shift + B** toobuild hello projektu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-253">Press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="example"></a><span data-ttu-id="1f3cd-254">Przykład</span><span class="sxs-lookup"><span data-stu-id="1f3cd-254">Example</span></span>

<span data-ttu-id="1f3cd-255">Kodu usługi zakończone powinna wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-255">Your completed service code should appear as follows.</span></span> <span data-ttu-id="1f3cd-256">Kod Hello zawiera hello kontrakt usługi i implementację z poprzednich kroków samouczka hello i hosty hello usługę w aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-256">hello code includes hello service contract and implementation from previous steps in hello tutorial, and hosts hello service in a console application.</span></span>

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

## <a name="create-a-wcf-client-for-hello-service-contract"></a><span data-ttu-id="1f3cd-257">Tworzenie klienta WCF dla kontraktu usługi hello</span><span class="sxs-lookup"><span data-stu-id="1f3cd-257">Create a WCF client for hello service contract</span></span>

<span data-ttu-id="1f3cd-258">Witaj, następnym krokiem jest toocreate aplikacji klienckiej i definiowanie kontraktu usługi hello, który będzie implementowany w następnych krokach.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-258">hello next step is toocreate a client application and define hello service contract you will implement in later steps.</span></span> <span data-ttu-id="1f3cd-259">Należy pamiętać, że wiele z tych kroków przypomina kroki hello używane toocreate usługi: definiowanie kontraktu, edytowanie pliku App.config plików przy użyciu poświadczeń usługi przekazywania toohello tooconnect i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-259">Note that many of these steps resemble hello steps used toocreate a service: defining a contract, editing an App.config file, using credentials tooconnect toohello relay service, and so on.</span></span> <span data-ttu-id="1f3cd-260">Kod Hello używany do wykonywania tych zadań podano w przykład Witaj hello procedury.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-260">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="1f3cd-261">Utwórz nowy projekt w bieżącym rozwiązaniu programu Visual Studio powitania klienta hello hello następujący:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-261">Create a new project in hello current Visual Studio solution for hello client by doing hello following:</span></span>

   1. <span data-ttu-id="1f3cd-262">W Eksploratorze rozwiązań w hello tego samego rozwiązania, które zawiera usługę hello, kliknij prawym przyciskiem myszy hello bieżące rozwiązanie (nie projekt hello) i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-262">In Solution Explorer, in hello same solution that contains hello service, right-click hello current solution (not hello project), and click **Add**.</span></span> <span data-ttu-id="1f3cd-263">Następnie kliknij pozycję **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-263">Then click **New Project**.</span></span>
   2. <span data-ttu-id="1f3cd-264">W hello **Dodawanie nowego projektu** okno dialogowe, kliknij przycisk **Visual C#** (Jeśli **Visual C#** nie jest wyświetlana, sprawdź w obszarze **inne języki**) wybierz pozycję hello **Aplikacji konsoli (.NET Framework)** szablonu i nadaj mu nazwę **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-264">In hello **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select hello **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="1f3cd-265">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-265">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="1f3cd-266">W Eksploratorze rozwiązań kliknij dwukrotnie plik Program.cs hello w hello **EchoClient** projektu tooopen on w edytorze hello, jeśli nie jest jeszcze otwarty.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-266">In Solution Explorer, double-click hello Program.cs file in hello **EchoClient** project tooopen it in hello editor, if it is not already open.</span></span>
3. <span data-ttu-id="1f3cd-267">Nazwa przestrzeni nazw hello zmiany z domyślnej nazwy `EchoClient` zbyt`Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-267">Change hello namespace name from its default name of `EchoClient` too`Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="1f3cd-268">Zainstaluj hello [pakietu NuGet usługi Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus): w Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **EchoClient** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-268">Install hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click hello **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="1f3cd-269">Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-269">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="1f3cd-270">Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-270">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="1f3cd-271">Dodaj `using` instrukcji dla hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) przestrzeni nazw w pliku Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-271">Add a `using` statement for hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in hello Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="1f3cd-272">Dodać hello definicji toohello przestrzeń nazw kontraktu usługi, jak pokazano hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-272">Add hello service contract definition toohello namespace, as shown in hello following example.</span></span> <span data-ttu-id="1f3cd-273">Należy pamiętać, że ta definicja identyczne toohello definicją używaną w hello **usługi** projektu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-273">Note that this definition is identical toohello definition used in hello **Service** project.</span></span> <span data-ttu-id="1f3cd-274">Ten kod należy dodać u góry hello hello `Microsoft.ServiceBus.Samples` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-274">You should add this code at hello top of hello `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="1f3cd-275">Naciśnij klawisz **Ctrl + Shift + B** toobuild powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-275">Press **Ctrl+Shift+B** toobuild hello client.</span></span>

### <a name="example"></a><span data-ttu-id="1f3cd-276">Przykład</span><span class="sxs-lookup"><span data-stu-id="1f3cd-276">Example</span></span>

<span data-ttu-id="1f3cd-277">Witaj poniższy kod przedstawia bieżący stan pliku Program.cs hello hello w hello **EchoClient** projektu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-277">hello following code shows hello current status of hello Program.cs file in hello **EchoClient** project.</span></span>

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

## <a name="configure-hello-wcf-client"></a><span data-ttu-id="1f3cd-278">Konfigurowanie powitania klienta WCF</span><span class="sxs-lookup"><span data-stu-id="1f3cd-278">Configure hello WCF client</span></span>

<span data-ttu-id="1f3cd-279">W tym kroku utworzysz plik App.config dla podstawowej aplikacji klienckiej, która uzyskuje dostęp do usługi hello utworzonej wcześniej w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-279">In this step, you create an App.config file for a basic client application that accesses hello service created previously in this tutorial.</span></span> <span data-ttu-id="1f3cd-280">Ten plik App.config definiuje kontrakt hello, powiązania i nazwa punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-280">This App.config file defines hello contract, binding, and name of hello endpoint.</span></span> <span data-ttu-id="1f3cd-281">Kod Hello używany do wykonywania tych zadań podano w przykład Witaj hello procedury.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-281">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="1f3cd-282">W Eksploratorze rozwiązań w hello **EchoClient** projektu, kliknij dwukrotnie **App.config** tooopen hello plik w edytorze programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-282">In Solution Explorer, in hello **EchoClient** project, double-click **App.config** tooopen hello file in hello Visual Studio editor.</span></span>
2. <span data-ttu-id="1f3cd-283">W hello `<appSettings>` elementu, zastąp symbole zastępcze hello hello nazwą przestrzeni nazw usługi i hello klucza sygnatury dostępu Współdzielonego, który został skopiowany w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-283">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="1f3cd-284">W elemencie system.serviceModel hello, Dodaj `<client>` elementu.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-284">Within hello system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="1f3cd-285">Ten krok umożliwia zadeklarowanie, że definiowana jest aplikacja kliencka w stylu platformy WCF.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-285">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="1f3cd-286">W ramach hello `client` elementu, zdefiniuj hello nazwę, kontrakt i typ powiązania punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-286">Within hello `client` element, define hello name, contract, and binding type for hello endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="1f3cd-287">Ten krok umożliwia określenie nazwy hello hello punktu końcowego, hello kontrakt zdefiniowany w hello usługi i hello fakt, że aplikacja kliencka hello używa TCP toocommunicate z przekaźnika usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-287">This step defines hello name of hello endpoint, hello contract defined in hello service, and hello fact that hello client application uses TCP toocommunicate with Azure Relay.</span></span> <span data-ttu-id="1f3cd-288">Witaj Nazwa punktu końcowego jest używana w hello następny krok toolink tej konfiguracji pliku końcowego z usługą hello identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-288">hello endpoint name is used in hello next step toolink this endpoint configuration with hello service URI.</span></span>
5. <span data-ttu-id="1f3cd-289">Kliknij przycisk **pliku**, następnie kliknij przycisk **Zapisz wszystko**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-289">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="1f3cd-290">Przykład</span><span class="sxs-lookup"><span data-stu-id="1f3cd-290">Example</span></span>

<span data-ttu-id="1f3cd-291">Witaj poniższy kod przedstawia plik App.config powitania klienta Echo hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-291">hello following code shows hello App.config file for hello Echo client.</span></span>

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

## <a name="implement-hello-wcf-client"></a><span data-ttu-id="1f3cd-292">Klient WCF hello wdrożenie</span><span class="sxs-lookup"><span data-stu-id="1f3cd-292">Implement hello WCF client</span></span>
<span data-ttu-id="1f3cd-293">W tym kroku należy zaimplementować podstawowej aplikacji klienckiej, która uzyskuje dostęp do usługi hello, utworzony wcześniej w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-293">In this step, you implement a basic client application that accesses hello service you created previously in this tutorial.</span></span> <span data-ttu-id="1f3cd-294">Podobne toohello, powitania klienta będzie przeprowadzać usługa wiele hello tej samej operacji tooaccess przekazywania Azure:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-294">Similar toohello service, hello client performs many of hello same operations tooaccess Azure Relay:</span></span>

1. <span data-ttu-id="1f3cd-295">Ustawia tryb łączności hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-295">Sets hello connectivity mode.</span></span>
2. <span data-ttu-id="1f3cd-296">Tworzy identyfikator URI, który lokalizuje usługę hosta hello hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-296">Creates hello URI that locates hello host service.</span></span>
3. <span data-ttu-id="1f3cd-297">Definiuje hello poświadczeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-297">Defines hello security credentials.</span></span>
4. <span data-ttu-id="1f3cd-298">Stosuje hello poświadczenia toohello połączenia.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-298">Applies hello credentials toohello connection.</span></span>
5. <span data-ttu-id="1f3cd-299">Otwiera hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-299">Opens hello connection.</span></span>
6. <span data-ttu-id="1f3cd-300">Wykonuje zadania specyficzne dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-300">Performs hello application-specific tasks.</span></span>
7. <span data-ttu-id="1f3cd-301">Zamyka połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-301">Closes hello connection.</span></span>

<span data-ttu-id="1f3cd-302">Jedną z głównych różnic hello jest jednak czy aplikacja kliencka hello używa usługi przekazywania toohello tooconnect kanału, natomiast usługa hello używa wywołania zbyt**ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-302">However, one of hello main differences is that hello client application uses a channel tooconnect toohello relay service, whereas hello service uses a call too**ServiceHost**.</span></span> <span data-ttu-id="1f3cd-303">Kod Hello używany do wykonywania tych zadań podano w przykład Witaj hello procedury.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-303">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="1f3cd-304">Wdrażanie aplikacji klienta</span><span class="sxs-lookup"><span data-stu-id="1f3cd-304">Implement a client application</span></span>
1. <span data-ttu-id="1f3cd-305">Ustaw tryb łączności hello zbyt**Autowykrywanie**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-305">Set hello connectivity mode too**AutoDetect**.</span></span> <span data-ttu-id="1f3cd-306">Dodaj następujące kodu wewnątrz hello hello `Main()` metody hello **EchoClient** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-306">Add hello following code inside hello `Main()` method of hello **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="1f3cd-307">Zdefiniuj zmienne toohold hello wartości hello przestrzeni nazw usługi i klucza sygnatury dostępu Współdzielonego odczytanego z hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-307">Define variables toohold hello values for hello service namespace, and SAS key that are read from hello console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="1f3cd-308">Utwórz hello identyfikator URI, który definiuje lokalizacji hello hello hosta w projekcie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-308">Create hello URI that defines hello location of hello host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="1f3cd-309">Utwórz obiekt poświadczeń powitania dla punktu końcowego przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-309">Create hello credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="1f3cd-310">Utwórz hello fabrykę kanałów ładującą konfigurację hello opisaną w pliku App.config hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-310">Create hello channel factory that loads hello configuration described in hello App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="1f3cd-311">Fabryka kanałów jest obiektem platformy WCF tworzącym kanał za pomocą którego komunikują się hello usługi i aplikacje klienckie.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-311">A channel factory is a WCF object that creates a channel through which hello service and client applications communicate.</span></span>
6. <span data-ttu-id="1f3cd-312">Zastosuj hello poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-312">Apply hello credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="1f3cd-313">Utwórz i otwórz hello kanału toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-313">Create and open hello channel toohello service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="1f3cd-314">Zapisywanie hello podstawowy interfejs użytkownika oraz funkcje dla echa hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-314">Write hello basic user interface and functionality for hello echo.</span></span>

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

    <span data-ttu-id="1f3cd-315">Uwaga hello kod używa hello wystąpienia obiektu kanału hello jako serwer proxy dla usługi hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-315">Note that hello code uses hello instance of hello channel object as a proxy for hello service.</span></span>
9. <span data-ttu-id="1f3cd-316">Zamknij kanał hello i zamknij hello fabryki.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-316">Close hello channel, and close hello factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="1f3cd-317">Przykład</span><span class="sxs-lookup"><span data-stu-id="1f3cd-317">Example</span></span>

<span data-ttu-id="1f3cd-318">Wypełniony kod powinien wyglądać następująco, przedstawiający sposób toocreate aplikacji klienckiej, jak toocall hello operacje usługi hello i jak tooclose hello klienta po wykonaniu operacji hello wywołanie zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-318">Your completed code should appear as follows, showing how toocreate a client application, how toocall hello operations of hello service, and how tooclose hello client after hello operation call is finished.</span></span>

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

## <a name="run-hello-applications"></a><span data-ttu-id="1f3cd-319">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="1f3cd-319">Run hello applications</span></span>

1. <span data-ttu-id="1f3cd-320">Naciśnij klawisz **Ctrl + Shift + B** toobuild hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-320">Press **Ctrl+Shift+B** toobuild hello solution.</span></span> <span data-ttu-id="1f3cd-321">Powoduje to skompilowanie zarówno projektu klienta hello, jak i projekt usługi hello utworzony w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-321">This builds both hello client project and hello service project that you created in hello previous steps.</span></span>
2. <span data-ttu-id="1f3cd-322">Przed działającej aplikacji hello klienta musi upewnij się, czy aplikacja usługi hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-322">Before running hello client application, you must make sure that hello service application is running.</span></span> <span data-ttu-id="1f3cd-323">W Eksploratorze rozwiązań w programie Visual Studio, kliknij prawym przyciskiem myszy hello **EchoService** rozwiązania, następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-323">In Solution Explorer in Visual Studio, right-click hello **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="1f3cd-324">Okno dialogowe właściwości rozwiązania hello, kliknij przycisk **projekt startowy**, kliknij przycisk hello **wiele projektów startowych** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-324">In hello solution properties dialog box, click **Startup Project**, then click hello **Multiple startup projects** button.</span></span> <span data-ttu-id="1f3cd-325">Upewnij się, że **EchoService** się na początku listy hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-325">Make sure **EchoService** appears first in hello list.</span></span>
4. <span data-ttu-id="1f3cd-326">Zestaw hello **akcji** pole dla obu hello **EchoService** i **EchoClient** projektów zbyt**Start**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-326">Set hello **Action** box for both hello **EchoService** and **EchoClient** projects too**Start**.</span></span>

    ![][5]
5. <span data-ttu-id="1f3cd-327">Kliknij pozycję **Zależności projektu**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-327">Click **Project Dependencies**.</span></span> <span data-ttu-id="1f3cd-328">W hello **projekty** wybierz opcję **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-328">In hello **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="1f3cd-329">W hello **zależy od** upewnij się, **EchoService** jest zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-329">In hello **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="1f3cd-330">Kliknij przycisk **OK** toodismiss hello **właściwości** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-330">Click **OK** toodismiss hello **Properties** dialog.</span></span>
7. <span data-ttu-id="1f3cd-331">Naciśnij klawisz **F5** toorun oba projekty.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-331">Press **F5** toorun both projects.</span></span>
8. <span data-ttu-id="1f3cd-332">Oba okna konsoli otwórz i wyświetlenie monitu o hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-332">Both console windows open and prompt you for hello namespace name.</span></span> <span data-ttu-id="1f3cd-333">Hello usługa musi być uruchomiona, dlatego w hello **EchoService** oknie konsoli, wprowadź hello przestrzeni nazw, a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-333">hello service must run first, so in hello **EchoService** console window, enter hello namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="1f3cd-334">Następnie zostanie wyświetlony monit o podanie klucza sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-334">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="1f3cd-335">Wprowadź klucz sygnatury dostępu Współdzielonego hello i naciśnij klawisz ENTER.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-335">Enter hello SAS key and press ENTER.</span></span>

    <span data-ttu-id="1f3cd-336">Oto przykładowe dane wyjściowe z okna konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-336">Here is example output from hello console window.</span></span> <span data-ttu-id="1f3cd-337">Należy pamiętać, że wartości hello pod warunkiem, że w tym miejscu są na przykład tylko do celów.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-337">Note that hello values provided here are for example purposes only.</span></span>

    <span data-ttu-id="1f3cd-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="1f3cd-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="1f3cd-339">Aplikacja usługi Hello drukuje toohello adres konsoli programu Windows hello na którym nasłuchuje, widziany hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-339">hello service application prints toohello console window hello address on which it's listening, as seen in hello following example.</span></span>

    <span data-ttu-id="1f3cd-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span><span class="sxs-lookup"><span data-stu-id="1f3cd-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span></span>
10. <span data-ttu-id="1f3cd-341">W hello **EchoClient** oknie konsoli, należy wprowadzić te same informacje, które zostały wprowadzone uprzednio dla aplikacji usługi hello hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-341">In hello **EchoClient** console window, enter hello same information that you entered previously for hello service application.</span></span> <span data-ttu-id="1f3cd-342">Wykonaj Witaj Witaj tooenter poprzednie kroki tej samej przestrzeni nazw usługi i skojarzenia zabezpieczeń wartości dla aplikacji klienckiej hello klucza.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-342">Follow hello previous steps tooenter hello same service namespace and SAS key values for hello client application.</span></span>
11. <span data-ttu-id="1f3cd-343">Po wprowadzeniu tych wartości, powitania klienta otwiera kanału usługi toohello monitów i możesz tooenter tekstu, jak hello poniższy przykład danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-343">After entering these values, hello client opens a channel toohello service and prompts you tooenter some text as seen in hello following console output example.</span></span>

    `Enter text tooecho (or [Enter] tooexit):`

    <span data-ttu-id="1f3cd-344">Wprowadź niektórych aplikacji usługi toohello toosend tekstu, a następnie naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-344">Enter some text toosend toohello service application and press Enter.</span></span> <span data-ttu-id="1f3cd-345">Ten tekst jest wysyłany toohello usługi za pośrednictwem hello operacji usługi Echo i pojawia się w oknie konsoli usługi hello jak hello następujące przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-345">This text is sent toohello service through hello Echo service operation and appears in hello service console window as in hello following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="1f3cd-346">Witaj aplikacja kliencka odbiera wartość zwracaną hello hello `Echo` operacja, która jest hello oryginalny tekst i wyświetla go tooits oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-346">hello client application receives hello return value of hello `Echo` operation, which is hello original text, and prints it tooits console window.</span></span> <span data-ttu-id="1f3cd-347">Witaj poniżej przedstawiono przykładowe dane wyjściowe z okna konsoli powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-347">hello following is example output from hello client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="1f3cd-348">Możesz kontynuować wysyłanie wiadomości SMS z powitania klienta toohello usługi w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-348">You can continue sending text messages from hello client toohello service in this manner.</span></span> <span data-ttu-id="1f3cd-349">Po zakończeniu naciśnij klawisz Enter w powitania klienta i usługi konsoli windows tooend obydwu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-349">When you are finished, press Enter in hello client and service console windows tooend both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f3cd-350">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1f3cd-350">Next steps</span></span>

<span data-ttu-id="1f3cd-351">W tym samouczku przedstawiono, jak toobuild Azure przekazywania aplikacji klienckiej i usługi za pomocą hello możliwości WCF przekaźnika usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-351">This tutorial showed how toobuild an Azure Relay client application and service using hello WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="1f3cd-352">Aby podobnego samouczka dotyczącego używa [usługi magistrali komunikatów](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), zobacz [Rozpoczynanie pracy z kolejek usługi Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="1f3cd-352">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="1f3cd-353">toolearn więcej informacji na temat przekaźnika usługi Azure, zobacz następujące tematy hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-353">toolearn more about Azure Relay, see hello following topics.</span></span>

* [<span data-ttu-id="1f3cd-354">Omówienie architektury usługi Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="1f3cd-354">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="1f3cd-355">Omówienie usługi Azure Relay</span><span class="sxs-lookup"><span data-stu-id="1f3cd-355">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="1f3cd-356">Jak usługa z platformą .NET przekazywania toouse hello WCF</span><span class="sxs-lookup"><span data-stu-id="1f3cd-356">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
