---
title: "Samouczek usługi Azure Service Bus WCF przekazywania | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5347bf85cad32b59677369d51a1f36529aef6662
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="c6a3d-103">Samouczek usługi Azure przekaźnika usługi WCF</span><span class="sxs-lookup"><span data-stu-id="c6a3d-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="c6a3d-104">Ten przewodnik opisuje sposób tworzenia prostego klienta WCF przekazywania aplikacji i usług przy użyciu przekaźnika usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-104">This tutorial describes how to build a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="c6a3d-105">Aby podobnego samouczka dotyczącego używa [usługi magistrali komunikatów](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), zobacz [Rozpoczynanie pracy z kolejek usługi Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="c6a3d-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="c6a3d-106">Ten samouczek umożliwia poznanie kroków, które są wymagane do utworzenia aplikacji klienta i usługi WCF przekazywania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-106">Working through this tutorial gives you an understanding of the steps that are required to create a WCF Relay client and service application.</span></span> <span data-ttu-id="c6a3d-107">Podobnie jak ich odpowiedniki WCF oryginalnej usługa jest strukturą ujawniającą jeden lub więcej punktów końcowych, z których każdy ujawnia co najmniej jedną operację usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="c6a3d-108">Punkt końcowy usługi określa adres usługi, powiązanie zawierające informacje umożliwiające klientowi komunikowanie się z usługą i kontrakt definiujący funkcje zapewniane klientom przez usługę.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-108">The endpoint of a service specifies an address where the service can be found, a binding that contains the information that a client must communicate with the service, and a contract that defines the functionality provided by the service to its clients.</span></span> <span data-ttu-id="c6a3d-109">Podstawowa różnica między WCF i przekazywania WCF jest, że punkt końcowy jest widoczna w chmurze zamiast lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-109">The main difference between WCF and WCF Relay is that the endpoint is exposed in the cloud instead of locally on your computer.</span></span>

<span data-ttu-id="c6a3d-110">Po zapoznaniu się z sekwencją tematów w tym samouczku będziesz mieć uruchomioną usługę i klienta, który może wywoływać operacje usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-110">After you work through the sequence of topics in this tutorial, you will have a running service, and a client that can invoke the operations of the service.</span></span> <span data-ttu-id="c6a3d-111">W pierwszym temacie opisano sposób konfigurowania konta.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-111">The first topic describes how to set up an account.</span></span> <span data-ttu-id="c6a3d-112">Następne kroki opisują sposób definiowania usługi używającej kontraktu, wdrażania usługi i konfigurowania usługi w kodzie.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-112">The next steps describe how to define a service that uses a contract, how to implement the service, and how to configure the service in code.</span></span> <span data-ttu-id="c6a3d-113">Opisano również sposób hostowania i uruchamiania usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-113">They also describe how to host and run the service.</span></span> <span data-ttu-id="c6a3d-114">Tworzona jest samodzielnie hostowana usługa, a klient i usługa są uruchomione na tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-114">The service that is created is self-hosted and the client and service run on the same computer.</span></span> <span data-ttu-id="c6a3d-115">Usługę można skonfigurować przy użyciu kodu lub pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-115">You can configure the service by using either code or a configuration file.</span></span>

<span data-ttu-id="c6a3d-116">Ostatnie trzy kroki opisują sposób tworzenia aplikacji klienckiej, konfigurowania aplikacji klienckiej oraz tworzenia i użycia klienta, który może uzyskać dostęp do funkcji hosta.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-116">The final three steps describe how to create a client application, configure the client application, and create and use a client that can access the functionality of the host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6a3d-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c6a3d-117">Prerequisites</span></span>

<span data-ttu-id="c6a3d-118">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c6a3d-118">To complete this tutorial, you'll need the following:</span></span>

* <span data-ttu-id="c6a3d-119">[Program Microsoft Visual Studio w wersji 2015 lub nowszej](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="c6a3d-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="c6a3d-120">W tym samouczku korzysta z programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="c6a3d-121">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-121">An active Azure account.</span></span> <span data-ttu-id="c6a3d-122">Jeśli go nie masz, możesz utworzyć bezpłatne konto w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="c6a3d-123">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c6a3d-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="c6a3d-124">Tworzenie przestrzeni nazw usługi</span><span class="sxs-lookup"><span data-stu-id="c6a3d-124">Create a service namespace</span></span>

<span data-ttu-id="c6a3d-125">Pierwszym krokiem jest utworzenie przestrzeni nazw i uzyskanie [dostępu sygnatury dostępu Współdzielonego](../service-bus-messaging/service-bus-sas.md) klucza.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-125">The first step is to create a namespace, and to obtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="c6a3d-126">Przestrzeń nazw wyznacza granice aplikacji dla każdej aplikacji widocznej za pośrednictwem usługi przekazywania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-126">A namespace provides an application boundary for each application exposed through the relay service.</span></span> <span data-ttu-id="c6a3d-127">Klucz sygnatury dostępu współdzielonego jest automatycznie generowany przez system po utworzeniu przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-127">A SAS key is automatically generated by the system when a service namespace is created.</span></span> <span data-ttu-id="c6a3d-128">Kombinacja przestrzeni nazw usługi i klucza sygnatury dostępu Współdzielonego dostarcza poświadczenia dla platformy Azure w celu uwierzytelniania dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-128">The combination of service namespace and SAS key provides the credentials for Azure to authenticate access to an application.</span></span> <span data-ttu-id="c6a3d-129">Postępuj zgodnie z [instrukcjami podanymi w tym miejscu](relay-create-namespace-portal.md), aby utworzyć przestrzeń nazw przekazywania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-129">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="c6a3d-130">Definiowanie kontraktu usługi WCF</span><span class="sxs-lookup"><span data-stu-id="c6a3d-130">Define a WCF service contract</span></span>

<span data-ttu-id="c6a3d-131">Kontrakt usługi określa, jakie operacje (terminologia usługi sieci web dla metod lub funkcji) usługa obsługuje.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-131">The service contract specifies what operations (the web service terminology for methods or functions) the service supports.</span></span> <span data-ttu-id="c6a3d-132">Kontrakty są tworzone przez definiowanie interfejsu C++, C# lub Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="c6a3d-133">Każda metoda w interfejsie odpowiada określonej operacji usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-133">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="c6a3d-134">W odniesieniu do każdego interfejsu należy zastosować atrybut [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx), a w odniesieniu do każdej operacji należy zastosować atrybut [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="c6a3d-134">Each interface must have the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied to it, and each operation must have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied to it.</span></span> <span data-ttu-id="c6a3d-135">Jeśli metoda w interfejsie z atrybutem [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) nie ma atrybutu [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), nie jest ujawniana.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-135">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="c6a3d-136">Kod dla tych zadań podano w przykładzie zamieszczonym na końcu procedury.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-136">The code for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="c6a3d-137">Kontrakty i usługi bardziej szczegółowo omówiono w artykule [Projektowanie i implementowanie usług](https://msdn.microsoft.com/library/ms729746.aspx) w dokumentacji platformy WCF.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="c6a3d-138">Tworzenie kontraktu przekazywania przy użyciu interfejsu</span><span class="sxs-lookup"><span data-stu-id="c6a3d-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="c6a3d-139">Otwórz program Visual Studio jako administrator, klikając prawym przyciskiem myszy ikonę programu w menu **Start**, a następnie wybierając polecenie **Uruchom jako administrator**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-139">Open Visual Studio as an administrator by right-clicking the program in the **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="c6a3d-140">Utwórz nowy projekt aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-140">Create a new console application project.</span></span> <span data-ttu-id="c6a3d-141">Kliknij menu **Plik** i wybierz pozycję **Nowy**, a następnie kliknij pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-141">Click the **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="c6a3d-142">W oknie dialogowym **Nowy projekt** kliknij pozycję **Visual C#** (jeśli pozycja **Visual C#** nie jest wyświetlana, sprawdź w obszarze **Inne języki**).</span><span class="sxs-lookup"><span data-stu-id="c6a3d-142">In the **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="c6a3d-143">Kliknij przycisk **aplikacji konsoli (.NET Framework)** szablonu i nadaj mu nazwę **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-143">Click the **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="c6a3d-144">Kliknij przycisk **OK**, aby utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-144">Click **OK** to create the project.</span></span>

    ![][2]

3. <span data-ttu-id="c6a3d-145">Zainstaluj pakiet NuGet magistrali usług.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-145">Install the Service Bus NuGet package.</span></span> <span data-ttu-id="c6a3d-146">Ten pakiet automatycznie dodaje odwołania do bibliotek usługi Service Bus, jak również przestrzeń nazw **System.ServiceModel** usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-146">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="c6a3d-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) jest przestrzenią nazw umożliwiającą programowy dostęp do podstawowych funkcji platformy WCF.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables you to programmatically access the basic features of WCF.</span></span> <span data-ttu-id="c6a3d-148">Usługa Service Bus używa wielu obiektów i atrybutów usługi WCF do definiowania kontraktów usług.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-148">Service Bus uses many of the objects and attributes of WCF to define service contracts.</span></span>

    <span data-ttu-id="c6a3d-149">W Eksploratorze rozwiązań kliknij projekt prawym przyciskiem myszy, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="c6a3d-149">In Solution Explorer, right-click the project, and then click **Manage NuGet Packages...**.</span></span> <span data-ttu-id="c6a3d-150">Kliknij kartę **Przeglądanie**, a następnie wyszukaj ciąg `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-150">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="c6a3d-151">Upewnij się, że nazwa projektu jest zaznaczona w polu **Wersje**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-151">Ensure that the project name is selected in the **Version(s)** box.</span></span> <span data-ttu-id="c6a3d-152">Kliknij pozycję **Zainstaluj** i zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-152">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="c6a3d-153">W Eksploratorze rozwiązań kliknij dwukrotnie plik Program.cs, aby otworzyć go w edytorze, jeśli nie został jeszcze otwarty.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-153">In Solution Explorer, double-click the Program.cs file to open it in the editor, if it is not already open.</span></span>
5. <span data-ttu-id="c6a3d-154">Dodaj następujące instrukcje using na początku pliku:</span><span class="sxs-lookup"><span data-stu-id="c6a3d-154">Add the following using statements at the top of the file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="c6a3d-155">Zmień nazwę przestrzeni nazw z domyślnej nazwy **EchoService** na **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-155">Change the namespace name from its default name of **EchoService** to **Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c6a3d-156">W tym samouczku używana przestrzeń nazw C# **Microsoft.ServiceBus.Samples**, który jest przestrzeń nazw kontraktu podstawie zarządzane typu, który jest używany w pliku konfiguracji w [Konfigurowanie klienta platformy WCF](#configure-the-wcf-client) krok.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-156">This tutorial uses the C# namespace **Microsoft.ServiceBus.Samples**, which is the namespace of the contract-based managed type that is used in the configuration file in the [Configure the WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="c6a3d-157">Możesz określić dowolną przestrzeń nazw podczas kompilowania tego przykładu, jednak samouczek nie będzie działać, jeśli nie zmodyfikujesz następnie odpowiednio przestrzeni nazw kontraktu i usługi w pliku konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-157">You can specify any namespace you want when you build this sample; however, the tutorial will not work unless you then modify the namespaces of the contract and service accordingly, in the application configuration file.</span></span> <span data-ttu-id="c6a3d-158">Przestrzeń nazw określona w pliku App.config musi być taka sama jak przestrzeń nazw określona w plikach C#.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-158">The namespace specified in the App.config file must be the same as the namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="c6a3d-159">Bezpośrednio po `Microsoft.ServiceBus.Samples` deklaracji przestrzeni nazw, ale w przestrzeni nazw Zdefiniuj nowy interfejs o nazwie `IEchoContract` i zastosować `ServiceContractAttribute` do interfejsu z wartością przestrzeni nazw `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-159">Directly after the `Microsoft.ServiceBus.Samples` namespace declaration, but within the namespace, define a new interface named `IEchoContract` and apply the `ServiceContractAttribute` attribute to the interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="c6a3d-160">Wartość przestrzeni nazw różni się od przestrzeni nazw używanej w kodzie.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-160">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="c6a3d-161">Zamiast tego wartość przestrzeni nazw jest używana jako unikatowy identyfikator dla tego kontraktu.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-161">Instead, the namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="c6a3d-162">Jawne określenie przestrzeni nazw zapobiega dodawaniu domyślnej wartości przestrzeni nazw do nazwy kontraktu.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-162">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span> <span data-ttu-id="c6a3d-163">Wklej następujący kod po deklaracji przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="c6a3d-163">Paste the following code after the namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="c6a3d-164">Zazwyczaj przestrzeń nazw kontraktu usługi zawiera schemat nazewnictwa uwzględniający informacje o wersji.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-164">Typically, the service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="c6a3d-165">Uwzględnienie informacji o wersji w przestrzeni nazw kontraktu usługi umożliwia usługom izolowanie istotnych zmian przez zdefiniowanie nowego kontraktu usługi z nową przestrzenią nazw i ujawnienie go w nowym punkcie końcowym.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-165">Including version information in the service contract namespace enables services to isolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="c6a3d-166">W ten sposób klienci mogą nadal używać starego kontraktu usługi bez konieczności aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-166">In this manner, clients can continue to use the old service contract without having to be updated.</span></span> <span data-ttu-id="c6a3d-167">Informacje o wersji mogą zawierać datę lub numer kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-167">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="c6a3d-168">Aby uzyskać więcej informacji, zobacz [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498) (Obsługa wersji usług).</span><span class="sxs-lookup"><span data-stu-id="c6a3d-168">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="c6a3d-169">Schemat nazewnictwa przestrzeni nazw kontraktu usługi, używany w tym przykładzie, nie zawiera informacji o wersji.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-169">For the purposes of this tutorial, the naming scheme of the service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="c6a3d-170">W ramach `IEchoContract` interfejsu, Zadeklaruj metodę dla pojedynczej operacji `IEchoContract` kontraktu udostępnia w interfejsie i Zastosuj `OperationContractAttribute` atrybut do metody, którą chcesz uwidocznić jako część publicznego kontraktu usługi WCF przekazywania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c6a3d-170">Within the `IEchoContract` interface, declare a method for the single operation the `IEchoContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="c6a3d-171">Bezpośrednio po definicji interfejsu `IEchoContract` zadeklaruj kanał dziedziczący zarówno po `IEchoContract`, jak i interfejsie `IClientChannel`, w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="c6a3d-171">Directly after the `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also to the `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="c6a3d-172">Kanał jest obiektem platformy WCF, za pomocą którego host i klient przekazują do siebie informacje.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-172">A channel is the WCF object through which the host and client pass information to each other.</span></span> <span data-ttu-id="c6a3d-173">Później napiszesz kod dla kanału obsługujący echo informacji przesyłanych między dwiema aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-173">Later, you will write code against the channel to echo information between the two applications.</span></span>
10. <span data-ttu-id="c6a3d-174">W menu **Kompilacja** kliknij pozycję **Kompiluj rozwiązanie** lub naciśnij klawisze **Ctrl+Shift+B**, aby potwierdzić dokładność pracy wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-174">From the **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="c6a3d-175">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6a3d-175">Example</span></span>

<span data-ttu-id="c6a3d-176">Poniższy kod przedstawia podstawowy interfejs definiujący kontrakt usługi WCF przekazywania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-176">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

<span data-ttu-id="c6a3d-177">Teraz, gdy interfejs został utworzony, możesz go zaimplementować.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-177">Now that the interface is created, you can implement the interface.</span></span>

## <a name="implement-the-wcf-contract"></a><span data-ttu-id="c6a3d-178">Implementowanie kontraktu usługi WCF</span><span class="sxs-lookup"><span data-stu-id="c6a3d-178">Implement the WCF contract</span></span>

<span data-ttu-id="c6a3d-179">Tworzenie przekaźnika usługi Azure wymaga, aby najpierw utworzyć kontrakt definiowany przy użyciu interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-179">Creating an Azure relay requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="c6a3d-180">Więcej informacji na temat tworzenia interfejsu podano w opisie poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-180">For more information about creating the interface, see the previous step.</span></span> <span data-ttu-id="c6a3d-181">Następnym krokiem jest zaimplementowanie interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-181">The next step is to implement the interface.</span></span> <span data-ttu-id="c6a3d-182">Jest to związane z utworzeniem klasy o nazwie `EchoService` implementującej interfejs `IEchoContract` zdefiniowany przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-182">This involves creating a class named `EchoService` that implements the user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="c6a3d-183">Po zaimplementowaniu interfejsu należy go skonfigurować przy użyciu pliku konfiguracji App.config.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-183">After you implement the interface, you then configure the interface using an App.config configuration file.</span></span> <span data-ttu-id="c6a3d-184">Plik konfiguracji zawiera niezbędne informacje dla aplikacji, takie jak nazwa usługi, Nazwa kontraktu i typ protokołu używanego do komunikacji z usługą przekazywania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-184">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="c6a3d-185">Kod używany do wykonywania tych zadań podano w przykładzie zamieszczonym po procedurze.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-185">The code used for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="c6a3d-186">Bardziej ogólne omówienie sposobu implementowania kontraktu usługi można znaleźć w temacie [Implementowanie kontraktów usług](https://msdn.microsoft.com/library/ms733764.aspx) w dokumentacji platformy WCF.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-186">For a more general discussion about how to implement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in the WCF documentation.</span></span>

1. <span data-ttu-id="c6a3d-187">Utwórz nową klasę o nazwie `EchoService` bezpośrednio po definicji interfejsu `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-187">Create a new class named `EchoService` directly after the definition of the `IEchoContract` interface.</span></span> <span data-ttu-id="c6a3d-188">Klasa `EchoService` implementuje interfejs `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-188">The `EchoService` class implements the `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="c6a3d-189">Podobnie jak w przypadku innych implementacji interfejsów, można zaimplementować definicję w innym pliku.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-189">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="c6a3d-190">Jednak w przypadku tego samouczka implementację umieszczono w tym samym pliku, w którym znajduje się definicja interfejsu i metoda `Main`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-190">However, for this tutorial, the implementation is located in the same file as the interface definition and the `Main` method.</span></span>
2. <span data-ttu-id="c6a3d-191">Zastosuj atrybut [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) do interfejsu `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-191">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the `IEchoContract` interface.</span></span> <span data-ttu-id="c6a3d-192">Ten atrybut określa nazwę usługi i przestrzeń nazw.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-192">The attribute specifies the service name and namespace.</span></span> <span data-ttu-id="c6a3d-193">Po wykonaniu tych czynności klasa `EchoService` wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="c6a3d-193">After doing so, the `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="c6a3d-194">Zaimplementuj metodę `Echo` zdefiniowaną w interfejsie `IEchoContract` w klasie `EchoService`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-194">Implement the `Echo` method defined in the `IEchoContract` interface in the `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="c6a3d-195">Kliknij pozycję **Kompilacja**, a następnie kliknij pozycję **Kompiluj rozwiązanie**, aby potwierdzić dokładność wykonanej pracy.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-195">Click **Build**, then click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="define-the-configuration-for-the-service-host"></a><span data-ttu-id="c6a3d-196">Definiowanie konfiguracji hosta usługi</span><span class="sxs-lookup"><span data-stu-id="c6a3d-196">Define the configuration for the service host</span></span>

1. <span data-ttu-id="c6a3d-197">Plik konfiguracji jest bardzo podobny do pliku konfiguracji platformy WCF.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-197">The configuration file is very similar to a WCF configuration file.</span></span> <span data-ttu-id="c6a3d-198">Zawiera nazwę usługi, punkt końcowy (czyli lokalizacji przekazywania Azure udostępnia klientom i hostom komunikować się ze sobą) i powiązanie (typ protokołu używanego do komunikacji).</span><span class="sxs-lookup"><span data-stu-id="c6a3d-198">It includes the service name, endpoint (that is, the location that Azure Relay exposes for clients and hosts to communicate with each other), and the binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="c6a3d-199">Główną różnicą jest odwoływanie się tego skonfigurowanego punktu końcowego usługi do powiązania [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding), które nie jest częścią programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-199">The main difference is that this configured service endpoint refers to a [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of the .NET Framework.</span></span> <span data-ttu-id="c6a3d-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) jest jednym z powiązań zdefiniowanych przez usługę.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of the bindings defined by the service.</span></span>
2. <span data-ttu-id="c6a3d-201">W **Eksploratorze rozwiązań** kliknij dwukrotnie plik App.config, aby otworzyć go w edytorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-201">In **Solution Explorer**, double-click the App.config file to open it in the Visual Studio editor.</span></span>
3. <span data-ttu-id="c6a3d-202">W elemencie `<appSettings>` zastąp symbole zastępcze nazwą przestrzeni nazw usługi i kluczem sygnatury dostępu współdzielonego skopiowanym we wcześniejszym kroku.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-202">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="c6a3d-203">W tagach `<system.serviceModel>` dodaj element `<services>`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-203">Within the `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="c6a3d-204">Wiele aplikacji przekazywania można zdefiniować w pojedynczym pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-204">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="c6a3d-205">W tym samouczku zdefiniowano jednak tylko jedną.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-205">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="c6a3d-206">W elemencie `<services>` dodaj element `<service>`, aby zdefiniować nazwę usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-206">Within the `<services>` element, add a `<service>` element to define the name of the service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="c6a3d-207">W elemencie `<service>` zdefiniuj lokalizację kontraktu punktu końcowego i wpisz powiązanie dla punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-207">Within the `<service>` element, define the location of the endpoint contract, and also the type of binding for the endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="c6a3d-208">Punkt końcowy określa, gdzie klient będzie szukać aplikacji hosta.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-208">The endpoint defines where the client will look for the host application.</span></span> <span data-ttu-id="c6a3d-209">Później w samouczku ten krok można utworzyć identyfikatora URI, który w pełni ujawnia hosta za pośrednictwem przekaźnika usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-209">Later, the tutorial uses this step to create a URI that fully exposes the host through Azure Relay.</span></span> <span data-ttu-id="c6a3d-210">Powiązanie deklaruje, że TCP jest używany protokół do komunikowania się z usługą przekazywania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-210">The binding declares that we are using TCP as the protocol to communicate with the relay service.</span></span>
7. <span data-ttu-id="c6a3d-211">W menu **Kompilacja** kliknij pozycję **Kompiluj rozwiązanie**, aby potwierdzić dokładność wykonanej pracy.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-211">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="c6a3d-212">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6a3d-212">Example</span></span>

<span data-ttu-id="c6a3d-213">Poniższy kod przedstawia implementację kontraktu usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-213">The following code shows the implementation of the service contract.</span></span>

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

<span data-ttu-id="c6a3d-214">Poniższy kod przedstawia podstawowy format pliku App.config skojarzonego z hostem usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-214">The following code shows the basic format of the App.config file associated with the service host.</span></span>

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

## <a name="host-and-run-a-basic-web-service-to-register-with-the-relay-service"></a><span data-ttu-id="c6a3d-215">Hostowanie i uruchamianie usługi sieci web podstawowe zarejestrować za pomocą usługi przekazywania</span><span class="sxs-lookup"><span data-stu-id="c6a3d-215">Host and run a basic web service to register with the relay service</span></span>

<span data-ttu-id="c6a3d-216">W tym kroku opisano sposób uruchamiania usługi przekaźnika usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-216">This step describes how to run an Azure Relay service.</span></span>

### <a name="create-the-relay-credentials"></a><span data-ttu-id="c6a3d-217">Utwórz poświadczenia przekazywania</span><span class="sxs-lookup"><span data-stu-id="c6a3d-217">Create the relay credentials</span></span>

1. <span data-ttu-id="c6a3d-218">W procedurze `Main()` utwórz dwie zmienne do przechowywania przestrzeni nazw i klucza sygnatury dostępu współdzielonego odczytanego z okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-218">In `Main()`, create two variables in which to store the namespace and the SAS key that are read from the console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="c6a3d-219">Klucz sygnatury dostępu Współdzielonego zostanie później służyć do dostęp do projektu.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-219">The SAS key will be used later to access your project.</span></span> <span data-ttu-id="c6a3d-220">Przestrzeń nazw jest przekazywana jako parametr do procedury `CreateServiceUri` w celu utworzenia identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-220">The namespace is passed as a parameter to `CreateServiceUri` to create a service URI.</span></span>
2. <span data-ttu-id="c6a3d-221">Korzystając z obiektu [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior), zadeklaruj zamiar użycia klucza sygnatury dostępu współdzielonego jako typu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-221">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as the credential type.</span></span> <span data-ttu-id="c6a3d-222">Dodaj poniższy kod bezpośrednio po kodzie dodanym w ostatnim kroku.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-222">Add the following code directly after the code added in the last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-the-service"></a><span data-ttu-id="c6a3d-223">Utwórz adres podstawowy usługi</span><span class="sxs-lookup"><span data-stu-id="c6a3d-223">Create a base address for the service</span></span>

<span data-ttu-id="c6a3d-224">Po kodzie dodanym w ostatnim kroku utwórz `Uri` wystąpienie dla podstawowego adresu usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-224">After the code you added in the last step, create a `Uri` instance for the base address of the service.</span></span> <span data-ttu-id="c6a3d-225">Ten identyfikator URI określa schemat magistrali usług, przestrzeń nazw i ścieżkę interfejsu usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-225">This URI specifies the Service Bus scheme, the namespace, and the path of the service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="c6a3d-226">Skrót „sb” (schemat magistrali usług) oznacza, że używany jest protokół TCP.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-226">"sb" is an abbreviation for the Service Bus scheme, and indicates that we are using TCP as the protocol.</span></span> <span data-ttu-id="c6a3d-227">Tę deklarację umieszczono również uprzednio w pliku konfiguracji, gdy określono powiązanie [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx).</span><span class="sxs-lookup"><span data-stu-id="c6a3d-227">This was also previously indicated in the configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as the binding.</span></span>

<span data-ttu-id="c6a3d-228">W tym samouczku użyto identyfikatora URI `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-228">For this tutorial, the URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-the-service-host"></a><span data-ttu-id="c6a3d-229">Tworzenie i Konfigurowanie hosta usługi</span><span class="sxs-lookup"><span data-stu-id="c6a3d-229">Create and configure the service host</span></span>

1. <span data-ttu-id="c6a3d-230">Ustaw tryb łączności `AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-230">Set the connectivity mode to `AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="c6a3d-231">Tryb łączności opisuje protokół używany przez usługę do komunikowania się z usługą przekazywania; protokołu HTTP lub TCP.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-231">The connectivity mode describes the protocol the service uses to communicate with the relay service; either HTTP or TCP.</span></span> <span data-ttu-id="c6a3d-232">Przy użyciu domyślnego ustawienia `AutoDetect`, usługa próbuje nawiązać przekazywania Azure za pośrednictwem protokołu TCP, jeśli jest dostępna i HTTP Jeśli TCP jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-232">Using the default setting `AutoDetect`, the service attempts to connect to Azure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="c6a3d-233">To ustawienie nie dotyczy protokołu określonego przez usługę dla komunikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-233">Note that this differs from the protocol the service specifies for client communication.</span></span> <span data-ttu-id="c6a3d-234">Ten protokół jest ustalany na podstawie używanego powiązania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-234">That protocol is determined by the binding used.</span></span> <span data-ttu-id="c6a3d-235">Na przykład usługa może używać [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) powiązania, który określa, że jej punkt końcowy komunikuje się z klientami za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-235">For example, a service can use the [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="c6a3d-236">Czy sama usługa może określać **ConnectivityMode.AutoDetect** tak, aby usługa komunikuje się z przekaźnika usługi Azure za pośrednictwem protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-236">That same service could specify **ConnectivityMode.AutoDetect** so that the service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="c6a3d-237">Utwórz hosta usługi przy użyciu identyfikatora URI utworzonego wcześniej w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-237">Create the service host, using the URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="c6a3d-238">Host usługi jest obiektem platformy WCF tworzącym wystąpienie usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-238">The service host is the WCF object that instantiates the service.</span></span> <span data-ttu-id="c6a3d-239">W tym miejscu możesz przekazać typ usługi, który chcesz utworzyć (typ `EchoService`), a także adres, pod którym usługa powinna być ujawniona.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-239">Here, you pass it the type of service you want to create (an `EchoService` type), and also to the address at which you want to expose the service.</span></span>
3. <span data-ttu-id="c6a3d-240">Na początku pliku Program.cs dodaj odwołania do opisów [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) i [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="c6a3d-240">At the top of the Program.cs file, add references to [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="c6a3d-241">Ponownie w procedurze `Main()` skonfiguruj punkt końcowy do obsługi dostępu publicznego.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-241">Back in `Main()`, configure the endpoint to enable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="c6a3d-242">Ten krok informuje usługi przekazywania, który aplikacji można znaleźć, sprawdzając źródła danych projektu ATOM publicznie.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-242">This step informs the relay service that your application can be found publicly by examining the ATOM feed for your project.</span></span> <span data-ttu-id="c6a3d-243">Jeśli ustawisz opcję **DiscoveryType** z ustawieniem **private**, klient nadal mógłby uzyskać dostęp do usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-243">If you set **DiscoveryType** to **private**, a client would still be able to access the service.</span></span> <span data-ttu-id="c6a3d-244">Jednak usługa nie pojawią się podczas wyszukiwania nazw przekazywania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-244">However, the service would not appear when it searches the Relay namespace.</span></span> <span data-ttu-id="c6a3d-245">Zamiast tego klient musiałby wcześniej znać ścieżkę punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-245">Instead, the client would have to know the endpoint path beforehand.</span></span>
5. <span data-ttu-id="c6a3d-246">Zapisz poświadczenia usługi w punktach końcowych zdefiniowanych w pliku App.config:</span><span class="sxs-lookup"><span data-stu-id="c6a3d-246">Apply the service credentials to the service endpoints defined in the App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="c6a3d-247">Jak zauważono w poprzednim kroku, w pliku konfiguracji możesz zadeklarować kilka usług i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-247">As stated in the previous step, you could have declared multiple services and endpoints in the configuration file.</span></span> <span data-ttu-id="c6a3d-248">W takim przypadku ten kod pomijałby plik konfiguracji i wyszukiwałby każdy punkt końcowy, do którego powinien zastosować Twoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-248">If you had, this code would traverse the configuration file and search for every endpoint to which it should apply your credentials.</span></span> <span data-ttu-id="c6a3d-249">W tym samouczku plik konfiguracyjny zawiera jednak tylko jeden punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-249">However, for this tutorial, the configuration file has only one endpoint.</span></span>

### <a name="open-the-service-host"></a><span data-ttu-id="c6a3d-250">Otworzyć hosta usługi</span><span class="sxs-lookup"><span data-stu-id="c6a3d-250">Open the service host</span></span>

1. <span data-ttu-id="c6a3d-251">Otwórz usługę.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-251">Open the service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="c6a3d-252">Poinformuj użytkownika, że usługa jest uruchomiona, i wyjaśnij, jak zamknąć usługę.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-252">Inform the user that the service is running, and explain how to shut down the service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="c6a3d-253">Po zakończeniu zamknij hosta usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-253">When finished, close the service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="c6a3d-254">Naciśnij klawisze **Ctrl+Shift+B**, aby skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-254">Press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="example"></a><span data-ttu-id="c6a3d-255">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6a3d-255">Example</span></span>

<span data-ttu-id="c6a3d-256">Kodu usługi zakończone powinna wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-256">Your completed service code should appear as follows.</span></span> <span data-ttu-id="c6a3d-257">Ten kod zawiera kontrakt usługi i implementację z poprzednich kroków samouczka i hostuje usługę w aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-257">The code includes the service contract and implementation from previous steps in the tutorial, and hosts the service in a console application.</span></span>

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

## <a name="create-a-wcf-client-for-the-service-contract"></a><span data-ttu-id="c6a3d-258">Tworzenie klienta platformy WCF dla kontraktu usługi</span><span class="sxs-lookup"><span data-stu-id="c6a3d-258">Create a WCF client for the service contract</span></span>

<span data-ttu-id="c6a3d-259">Następnym krokiem jest utworzenie aplikacji klienckiej i zdefiniowanie kontraktu usługi, który będzie implementowany w następnych krokach.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-259">The next step is to create a client application and define the service contract you will implement in later steps.</span></span> <span data-ttu-id="c6a3d-260">Należy pamiętać, że wiele z tych kroków przypomina kroki używany do tworzenia usługi: definiowanie kontraktu, edytowanie pliku App.config pliku, aby połączyć się z usługą przekazywania przy użyciu poświadczeń i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-260">Note that many of these steps resemble the steps used to create a service: defining a contract, editing an App.config file, using credentials to connect to the relay service, and so on.</span></span> <span data-ttu-id="c6a3d-261">Kod używany do wykonywania tych zadań podano w przykładzie zamieszczonym po procedurze.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-261">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="c6a3d-262">Utwórz nowy projekt w bieżącym rozwiązaniu programu Visual Studio dla klienta, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c6a3d-262">Create a new project in the current Visual Studio solution for the client by doing the following:</span></span>

   1. <span data-ttu-id="c6a3d-263">W Eksploratorze rozwiązań w tym samym rozwiązaniu, które zawiera tę usługę, kliknij prawym przyciskiem myszy bieżące rozwiązanie (nie projekt) i kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-263">In Solution Explorer, in the same solution that contains the service, right-click the current solution (not the project), and click **Add**.</span></span> <span data-ttu-id="c6a3d-264">Następnie kliknij pozycję **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-264">Then click **New Project**.</span></span>
   2. <span data-ttu-id="c6a3d-265">W **Dodawanie nowego projektu** okno dialogowe, kliknij przycisk **Visual C#** (Jeśli **Visual C#** nie jest wyświetlana, sprawdź w obszarze **inne języki**) wybierz pozycję **Aplikacji konsoli (.NET Framework)** szablonu i nadaj mu nazwę **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-265">In the **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select the **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="c6a3d-266">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-266">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="c6a3d-267">W Eksploratorze rozwiązań kliknij dwukrotnie plik Program.cs w projekcie **EchoClient**, aby otworzyć go w edytorze, jeśli nie został jeszcze otwarty.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-267">In Solution Explorer, double-click the Program.cs file in the **EchoClient** project to open it in the editor, if it is not already open.</span></span>
3. <span data-ttu-id="c6a3d-268">Zmień nazwę przestrzeni nazw z domyślnej nazwy `EchoClient` na `Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-268">Change the namespace name from its default name of `EchoClient` to `Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="c6a3d-269">Zainstaluj [pakietu NuGet usługi Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus): w Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **EchoClient** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-269">Install the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click the **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="c6a3d-270">Kliknij kartę **Przeglądanie**, a następnie wyszukaj ciąg `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-270">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="c6a3d-271">Kliknij pozycję **Zainstaluj** i zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-271">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="c6a3d-272">Dodaj instrukcję `using` dla przestrzeni nazw [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) w pliku Program.cs.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-272">Add a `using` statement for the [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in the Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="c6a3d-273">Dodaj definicję kontraktu usługi do przestrzeni nazw jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-273">Add the service contract definition to the namespace, as shown in the following example.</span></span> <span data-ttu-id="c6a3d-274">Ta definicja jest identyczna z definicją używaną w projekcie **Usługa**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-274">Note that this definition is identical to the definition used in the **Service** project.</span></span> <span data-ttu-id="c6a3d-275">Ten kod należy dodać na początku przestrzeni nazw `Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-275">You should add this code at the top of the `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="c6a3d-276">Naciśnij klawisze **Ctrl+Shift+B**, aby skompilować klienta.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-276">Press **Ctrl+Shift+B** to build the client.</span></span>

### <a name="example"></a><span data-ttu-id="c6a3d-277">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6a3d-277">Example</span></span>

<span data-ttu-id="c6a3d-278">Poniższy kod przedstawia bieżący stan pliku Program.cs w **EchoClient** projektu.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-278">The following code shows the current status of the Program.cs file in the **EchoClient** project.</span></span>

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

## <a name="configure-the-wcf-client"></a><span data-ttu-id="c6a3d-279">Konfigurowanie klienta platformy WCF</span><span class="sxs-lookup"><span data-stu-id="c6a3d-279">Configure the WCF client</span></span>

<span data-ttu-id="c6a3d-280">W tym kroku zostanie utworzony plik App.config dla podstawowej aplikacji klienckiej uzyskującej dostęp do usługi utworzonej wcześniej w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-280">In this step, you create an App.config file for a basic client application that accesses the service created previously in this tutorial.</span></span> <span data-ttu-id="c6a3d-281">Ten plik App.config definiuje kontrakt, powiązanie i nazwę punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-281">This App.config file defines the contract, binding, and name of the endpoint.</span></span> <span data-ttu-id="c6a3d-282">Kod używany do wykonywania tych zadań podano w przykładzie zamieszczonym po procedurze.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-282">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="c6a3d-283">W Eksploratorze rozwiązań kliknij projekt **EchoClient** i kliknij dwukrotnie plik **App.config**, aby otworzyć go w edytorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-283">In Solution Explorer, in the **EchoClient** project, double-click **App.config** to open the file in the Visual Studio editor.</span></span>
2. <span data-ttu-id="c6a3d-284">W elemencie `<appSettings>` zastąp symbole zastępcze nazwą przestrzeni nazw usługi i kluczem sygnatury dostępu współdzielonego skopiowanym we wcześniejszym kroku.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-284">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="c6a3d-285">W elemencie system.serviceModel dodaj element `<client>`.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-285">Within the system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="c6a3d-286">Ten krok umożliwia zadeklarowanie, że definiowana jest aplikacja kliencka w stylu platformy WCF.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-286">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="c6a3d-287">W elemencie `client` zdefiniuj nazwę, kontrakt i typ powiązania punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-287">Within the `client` element, define the name, contract, and binding type for the endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="c6a3d-288">Ten krok określa nazwę punktu końcowego i kontrakt zdefiniowany w usłudze i fakt, że aplikacja kliencka używa protokołu TCP do komunikowania się z przekaźnika usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-288">This step defines the name of the endpoint, the contract defined in the service, and the fact that the client application uses TCP to communicate with Azure Relay.</span></span> <span data-ttu-id="c6a3d-289">Nazwa punktu końcowego jest używana w następnym kroku do powiązania tej konfiguracji pliku końcowego z identyfikatorem URI usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-289">The endpoint name is used in the next step to link this endpoint configuration with the service URI.</span></span>
5. <span data-ttu-id="c6a3d-290">Kliknij przycisk **pliku**, następnie kliknij przycisk **Zapisz wszystko**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-290">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="c6a3d-291">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6a3d-291">Example</span></span>

<span data-ttu-id="c6a3d-292">Poniższy kod przedstawia plik App.config dla klienta Echo.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-292">The following code shows the App.config file for the Echo client.</span></span>

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

## <a name="implement-the-wcf-client"></a><span data-ttu-id="c6a3d-293">Implementowanie klienta platformy WCF</span><span class="sxs-lookup"><span data-stu-id="c6a3d-293">Implement the WCF client</span></span>
<span data-ttu-id="c6a3d-294">W tym kroku zostanie zaimplementowana podstawowa aplikacja kliencka uzyskująca dostęp do usługi utworzonej wcześniej w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-294">In this step, you implement a basic client application that accesses the service you created previously in this tutorial.</span></span> <span data-ttu-id="c6a3d-295">Podobnie jak usługa, klient wykonuje wiele operacji przekazywania Azure dostępu do:</span><span class="sxs-lookup"><span data-stu-id="c6a3d-295">Similar to the service, the client performs many of the same operations to access Azure Relay:</span></span>

1. <span data-ttu-id="c6a3d-296">Ustawienie trybu łączności.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-296">Sets the connectivity mode.</span></span>
2. <span data-ttu-id="c6a3d-297">Utworzenie identyfikatora URI, który lokalizuje usługę hosta.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-297">Creates the URI that locates the host service.</span></span>
3. <span data-ttu-id="c6a3d-298">Uzyskanie poświadczeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-298">Defines the security credentials.</span></span>
4. <span data-ttu-id="c6a3d-299">Zastosowanie poświadczeń do połączenia.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-299">Applies the credentials to the connection.</span></span>
5. <span data-ttu-id="c6a3d-300">Otwarcie połączenia.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-300">Opens the connection.</span></span>
6. <span data-ttu-id="c6a3d-301">Wykonanie zadań specyficznych dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-301">Performs the application-specific tasks.</span></span>
7. <span data-ttu-id="c6a3d-302">Zamknięcie połączenia.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-302">Closes the connection.</span></span>

<span data-ttu-id="c6a3d-303">Jedną z głównych różnic jest jednak czy aplikacja kliencka używa kanał połączyć się z usługą przekazywania, podczas gdy usługa korzysta z **ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-303">However, one of the main differences is that the client application uses a channel to connect to the relay service, whereas the service uses a call to **ServiceHost**.</span></span> <span data-ttu-id="c6a3d-304">Kod używany do wykonywania tych zadań podano w przykładzie zamieszczonym po procedurze.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-304">The code used for these tasks is provided in the example following the procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="c6a3d-305">Wdrażanie aplikacji klienta</span><span class="sxs-lookup"><span data-stu-id="c6a3d-305">Implement a client application</span></span>
1. <span data-ttu-id="c6a3d-306">Ustaw tryb łączności **AutoDetect**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-306">Set the connectivity mode to **AutoDetect**.</span></span> <span data-ttu-id="c6a3d-307">Dodaj następujący kod w metodzie `Main()` aplikacji **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-307">Add the following code inside the `Main()` method of the **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="c6a3d-308">Zdefiniuj zmienne do przechowywania wartości przestrzeni nazw i klucza sygnatury dostępu współdzielonego odczytanego z okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-308">Define variables to hold the values for the service namespace, and SAS key that are read from the console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="c6a3d-309">Utwórz identyfikator URI, który określa lokalizację hosta w projekcie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-309">Create the URI that defines the location of the host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="c6a3d-310">Utwórz obiekt poświadczeń dla punktu końcowego przestrzeni nazw Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-310">Create the credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="c6a3d-311">Utwórz fabrykę kanałów ładującą konfigurację opisaną w pliku App.config.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-311">Create the channel factory that loads the configuration described in the App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="c6a3d-312">Fabryka kanałów jest obiektem platformy WCF tworzącym kanał komunikacyjny dla usługi i aplikacji klienckich.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-312">A channel factory is a WCF object that creates a channel through which the service and client applications communicate.</span></span>
6. <span data-ttu-id="c6a3d-313">Zastosuj poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-313">Apply the credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="c6a3d-314">Utwórz i otwórz kanał dla usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-314">Create and open the channel to the service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="c6a3d-315">Zapisz podstawowy interfejs użytkownika i funkcje dla echa.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-315">Write the basic user interface and functionality for the echo.</span></span>

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

    <span data-ttu-id="c6a3d-316">W kodzie użyto wystąpienia obiektu kanału jako serwera proxy dla usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-316">Note that the code uses the instance of the channel object as a proxy for the service.</span></span>
9. <span data-ttu-id="c6a3d-317">Zamknij kanał i fabrykę.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-317">Close the channel, and close the factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="c6a3d-318">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6a3d-318">Example</span></span>

<span data-ttu-id="c6a3d-319">Wypełniony kod powinien wyglądać następująco, jak utworzyć aplikację klienta, jak wywoływanie operacji usługi oraz sposób zamykania klienta po wywołaniu operacji zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-319">Your completed code should appear as follows, showing how to create a client application, how to call the operations of the service, and how to close the client after the operation call is finished.</span></span>

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

## <a name="run-the-applications"></a><span data-ttu-id="c6a3d-320">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="c6a3d-320">Run the applications</span></span>

1. <span data-ttu-id="c6a3d-321">Naciśnij klawisze **Ctrl+Shift+B** w celu skompilowania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-321">Press **Ctrl+Shift+B** to build the solution.</span></span> <span data-ttu-id="c6a3d-322">Powoduje to skompilowanie zarówno projektu klienta, jak i projektu usługi utworzonych w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-322">This builds both the client project and the service project that you created in the previous steps.</span></span>
2. <span data-ttu-id="c6a3d-323">Przed uruchomieniem aplikacji klienckiej musisz upewnić się, że aplikacja usługi jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-323">Before running the client application, you must make sure that the service application is running.</span></span> <span data-ttu-id="c6a3d-324">W Eksploratorze rozwiązań w programie Visual Studio kliknij prawym przyciskiem myszy rozwiązanie **EchoService**, a następnie kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-324">In Solution Explorer in Visual Studio, right-click the **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="c6a3d-325">W oknie dialogowym właściwości rozwiązania kliknij pozycję **Projekt startowy**, a następnie kliknij przycisk **Wiele projektów startowych**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-325">In the solution properties dialog box, click **Startup Project**, then click the **Multiple startup projects** button.</span></span> <span data-ttu-id="c6a3d-326">Upewnij się, że pozycja **EchoService** jest wyświetlana na początku listy.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-326">Make sure **EchoService** appears first in the list.</span></span>
4. <span data-ttu-id="c6a3d-327">Ustaw w polu **Akcja** zarówno dla projektu **EchoService**, jak i projektu **EchoClient** ustawienie **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-327">Set the **Action** box for both the **EchoService** and **EchoClient** projects to **Start**.</span></span>

    ![][5]
5. <span data-ttu-id="c6a3d-328">Kliknij pozycję **Zależności projektu**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-328">Click **Project Dependencies**.</span></span> <span data-ttu-id="c6a3d-329">W polu **Projekty** wybierz pozycję **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-329">In the **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="c6a3d-330">Upewnij się, że w polu **Zależny od** jest zaznaczona opcja **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-330">In the **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="c6a3d-331">Kliknij przycisk **OK**, aby zamknąć okno dialogowe **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-331">Click **OK** to dismiss the **Properties** dialog.</span></span>
7. <span data-ttu-id="c6a3d-332">Naciśnij klawisz **F5**, aby uruchomić oba projekty.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-332">Press **F5** to run both projects.</span></span>
8. <span data-ttu-id="c6a3d-333">Oba okna konsoli zostaną otwarte z monitami o podanie nazwy przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-333">Both console windows open and prompt you for the namespace name.</span></span> <span data-ttu-id="c6a3d-334">Najpierw należy uruchomić usługę, dlatego w oknie konsoli **EchoService** wprowadź przestrzeń nazw, a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-334">The service must run first, so in the **EchoService** console window, enter the namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="c6a3d-335">Następnie zostanie wyświetlony monit o podanie klucza sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-335">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="c6a3d-336">Wprowadź klucz sygnatury dostępu współdzielonego i naciśnij klawisz ENTER.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-336">Enter the SAS key and press ENTER.</span></span>

    <span data-ttu-id="c6a3d-337">Oto przykładowe dane wyjściowe z okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-337">Here is example output from the console window.</span></span> <span data-ttu-id="c6a3d-338">Poniższe wartości podano tutaj wyłącznie jako przykład.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-338">Note that the values provided here are for example purposes only.</span></span>

    <span data-ttu-id="c6a3d-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="c6a3d-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="c6a3d-340">Aplikacja usługi wyświetla w oknie konsoli adres, na którym nasłuchuje, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-340">The service application prints to the console window the address on which it's listening, as seen in the following example.</span></span>

    <span data-ttu-id="c6a3d-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span><span class="sxs-lookup"><span data-stu-id="c6a3d-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span></span>
10. <span data-ttu-id="c6a3d-342">W oknie konsoli **EchoClient** wprowadź te same informacje, które zostały wprowadzone uprzednio dla aplikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-342">In the **EchoClient** console window, enter the same information that you entered previously for the service application.</span></span> <span data-ttu-id="c6a3d-343">Wykonaj poprzednie kroki, aby wprowadzić tę samą przestrzeń nazw i klucz sygnatury dostępu współdzielonego dla aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-343">Follow the previous steps to enter the same service namespace and SAS key values for the client application.</span></span>
11. <span data-ttu-id="c6a3d-344">Po wprowadzeniu tych wartości klient otworzy kanał do usługi i będzie monitować o wprowadzenie tekstu, jak w poniższym przykładzie danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-344">After entering these values, the client opens a channel to the service and prompts you to enter some text as seen in the following console output example.</span></span>

    `Enter text to echo (or [Enter] to exit):`

    <span data-ttu-id="c6a3d-345">Wprowadź tekst, który zostanie wysłany do aplikacji usługi, i naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-345">Enter some text to send to the service application and press Enter.</span></span> <span data-ttu-id="c6a3d-346">Ten tekst jest wysyłany do usługi za pośrednictwem operacji usługi Echo i pojawia się w oknie konsoli usługi, jak w poniższym przykładzie danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-346">This text is sent to the service through the Echo service operation and appears in the service console window as in the following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="c6a3d-347">Aplikacja kliencka odbiera wartość zwracaną przez operację `Echo`, która jest oryginalnym tekstem, i wyświetla go w oknie swojej konsoli.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-347">The client application receives the return value of the `Echo` operation, which is the original text, and prints it to its console window.</span></span> <span data-ttu-id="c6a3d-348">Poniżej przestawiono przykład danych wyjściowych z okna konsoli klienta.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-348">The following is example output from the client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="c6a3d-349">Możesz kontynuować wysyłanie wiadomości tekstowych z klienta do usługi w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-349">You can continue sending text messages from the client to the service in this manner.</span></span> <span data-ttu-id="c6a3d-350">Po zakończeniu naciśnij klawisz Enter w oknach konsoli klienta i usługi, aby zamknąć obie aplikacje.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-350">When you are finished, press Enter in the client and service console windows to end both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6a3d-351">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6a3d-351">Next steps</span></span>

<span data-ttu-id="c6a3d-352">W tym samouczku przedstawiono sposób tworzenia klienta przekaźnika usługi Azure, aplikacji i usług przy użyciu funkcji WCF przekaźnika usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-352">This tutorial showed how to build an Azure Relay client application and service using the WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="c6a3d-353">Aby podobnego samouczka dotyczącego używa [usługi magistrali komunikatów](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), zobacz [Rozpoczynanie pracy z kolejek usługi Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="c6a3d-353">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="c6a3d-354">Aby dowiedzieć się więcej na temat przekaźnika usługi Azure, zobacz następujące tematy.</span><span class="sxs-lookup"><span data-stu-id="c6a3d-354">To learn more about Azure Relay, see the following topics.</span></span>

* [<span data-ttu-id="c6a3d-355">Omówienie architektury usługi Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="c6a3d-355">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="c6a3d-356">Omówienie usługi Azure Relay</span><span class="sxs-lookup"><span data-stu-id="c6a3d-356">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="c6a3d-357">Jak używać przekaźnika usługi WCF z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="c6a3d-357">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
