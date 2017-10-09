---
title: "Samouczek REST magistrali aaaService przy użyciu przekaźnika usługi Azure | Dokumentacja firmy Microsoft"
description: "Utworzyć prostą aplikację do hosta przekaźnika usługi Azure Service Bus, która uwidacznia interfejs REST."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="a59b2-103">Samouczek usługi Azure REST przekaźnika usługi WCF</span><span class="sxs-lookup"><span data-stu-id="a59b2-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="a59b2-104">W tym samouczku opisano, jak toobuild proste przekazywania Azure obsługiwania aplikacji, która uwidacznia interfejs REST.</span><span class="sxs-lookup"><span data-stu-id="a59b2-104">This tutorial describes how toobuild a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="a59b2-105">Interfejs REST umożliwia klientowi sieci web, takich jak przeglądarki sieci web, powitalne tooaccess interfejsów API usługi Service Bus za pośrednictwem protokołu HTTP żądania.</span><span class="sxs-lookup"><span data-stu-id="a59b2-105">REST enables a web client, such as a web browser, tooaccess hello Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="a59b2-106">Witaj samouczku tooconstruct modelu programowania hello REST Windows Communication Foundation (WCF) usługi REST usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a59b2-106">hello tutorial uses hello Windows Communication Foundation (WCF) REST programming model tooconstruct a REST service on Service Bus.</span></span> <span data-ttu-id="a59b2-107">Aby uzyskać więcej informacji, zobacz [Model programowania interfejsu REST usługi WCF](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) i [projektowanie i Implementowanie usług](/dotnet/framework/wcf/designing-and-implementing-services) w hello dokumentacji usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="a59b2-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in hello WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="a59b2-108">Krok 1. Tworzenie przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="a59b2-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="a59b2-109">przy użyciu toobegin hello funkcji przekazywania na platformie Azure, musisz najpierw utworzyć przestrzeń nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="a59b2-109">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="a59b2-110">Przestrzeń nazw zapewnia kontener określania zakresu na potrzeby adresowania zasobów platformy Azure w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a59b2-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="a59b2-111">Wykonaj hello [instrukcje w tym miejscu](relay-create-namespace-portal.md) toocreate przekazywania przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="a59b2-111">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a><span data-ttu-id="a59b2-112">Krok 2: Definiowanie toouse kontraktu usługi WCF opartego na interfejsie REST, z przekaźnika usługi Azure</span><span class="sxs-lookup"><span data-stu-id="a59b2-112">Step 2: Define a REST-based WCF service contract toouse with Azure Relay</span></span>

<span data-ttu-id="a59b2-113">Podczas tworzenia usługi WCF na interfejsie REST należy zdefiniować kontrakt hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-113">When you create a WCF REST-style service, you must define hello contract.</span></span> <span data-ttu-id="a59b2-114">kontrakt Hello Określa, jakie operacje hello obsługuje hosta.</span><span class="sxs-lookup"><span data-stu-id="a59b2-114">hello contract specifies what operations hello host supports.</span></span> <span data-ttu-id="a59b2-115">Operacja usługi może być rozumiana jako metoda usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a59b2-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="a59b2-116">Kontrakty są tworzone przez definiowanie interfejsu C++, C# lub Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="a59b2-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="a59b2-117">Każda metoda w interfejsie hello odpowiada tooa określonej operacji usługi.</span><span class="sxs-lookup"><span data-stu-id="a59b2-117">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="a59b2-118">Witaj [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atrybutu musi być zastosowany tooeach interfejsu i hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) atrybut musi być zastosowany tooeach operacji.</span><span class="sxs-lookup"><span data-stu-id="a59b2-118">hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied tooeach interface, and hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied tooeach operation.</span></span> <span data-ttu-id="a59b2-119">Jeśli metoda w interfejsie z atrybutem hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) nie ma hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), metoda nie jest uwidaczniana.</span><span class="sxs-lookup"><span data-stu-id="a59b2-119">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="a59b2-120">Kod Hello używany do wykonywania tych zadań pokazano przykład Witaj hello procedury.</span><span class="sxs-lookup"><span data-stu-id="a59b2-120">hello code used for these tasks is shown in hello example following hello procedure.</span></span>

<span data-ttu-id="a59b2-121">Witaj podstawowa różnica między kontraktu usługi WCF i kontrakt typu REST jest dodanie hello toohello właściwości [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="a59b2-121">hello primary difference between a WCF contract and a REST-style contract is hello addition of a property toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="a59b2-122">Ta właściwość umożliwia toomap metody w metodę interfejsu tooa na powitania po drugiej stronie powitania interfejsu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-122">This property enables you toomap a method in your interface tooa method on hello other side of hello interface.</span></span> <span data-ttu-id="a59b2-123">W tym przypadku użyjemy [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink tooHTTP metody GET.</span><span class="sxs-lookup"><span data-stu-id="a59b2-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink a method tooHTTP GET.</span></span> <span data-ttu-id="a59b2-124">Dzięki temu usługa Service Bus tooaccurately pobierać i interpretować polecenia wysyłane toohello interfejsu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-124">This allows Service Bus tooaccurately retrieve and interpret commands sent toohello interface.</span></span>

### <a name="toocreate-a-contract-with-an-interface"></a><span data-ttu-id="a59b2-125">toocreate kontrakt interfejsu</span><span class="sxs-lookup"><span data-stu-id="a59b2-125">toocreate a contract with an interface</span></span>

1. <span data-ttu-id="a59b2-126">Otwórz program Visual Studio jako administrator: kliknij prawym przyciskiem myszy program hello hello **Start** menu, a następnie kliknij przycisk **Uruchom jako administrator**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-126">Open Visual Studio as an administrator: right-click hello program in hello **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="a59b2-127">Utwórz nowy projekt aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="a59b2-127">Create a new console application project.</span></span> <span data-ttu-id="a59b2-128">Kliknij przycisk hello **pliku** menu i wybierz **nowy**, a następnie wybierz pozycję **projektu**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-128">Click hello **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="a59b2-129">W hello **nowy projekt** okno dialogowe, kliknij przycisk **Visual C#**, wybierz pozycję hello **aplikacji konsoli** szablonu i nadaj mu nazwę **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-129">In hello **New Project** dialog box, click **Visual C#**, select hello **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="a59b2-130">Użyj domyślnej hello **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-130">Use hello default **Location**.</span></span> <span data-ttu-id="a59b2-131">Kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-131">Click **OK** toocreate hello project.</span></span>
3. <span data-ttu-id="a59b2-132">W przypadku projektu C# program Visual Studio utworzy plik `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="a59b2-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="a59b2-133">Ta klasa zawiera pustą `Main()` metody wymagane dla toobuild projekt aplikacji konsoli poprawnie.</span><span class="sxs-lookup"><span data-stu-id="a59b2-133">This class contains an empty `Main()` method, required for a console application project toobuild correctly.</span></span>
4. <span data-ttu-id="a59b2-134">Dodawanie odwołań tooService magistrali i **System.ServiceModel.dll** toohello projekcie, instalując pakiet NuGet usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-134">Add references tooService Bus and **System.ServiceModel.dll** toohello project by installing hello Service Bus NuGet package.</span></span> <span data-ttu-id="a59b2-135">Ten pakiet automatycznie dodaje bibliotek usługi Service Bus toohello odwołania, a także hello WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-135">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="a59b2-136">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ImageListener** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-136">In Solution Explorer, right-click hello **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="a59b2-137">Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="a59b2-137">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="a59b2-138">Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-138">Click **Install**, and accept hello terms of use.</span></span>
5. <span data-ttu-id="a59b2-139">Należy jawnie dodać odwołanie za**System.ServiceModel.Web.dll** toohello projektu:</span><span class="sxs-lookup"><span data-stu-id="a59b2-139">You must explicitly add a reference too**System.ServiceModel.Web.dll** toohello project:</span></span>
   
    <span data-ttu-id="a59b2-140">a.</span><span class="sxs-lookup"><span data-stu-id="a59b2-140">a.</span></span> <span data-ttu-id="a59b2-141">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **odwołania** folder hello folderu projektu, a następnie kliknij przycisk **Dodaj odwołanie**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-141">In Solution Explorer, right-click hello **References** folder under hello project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="a59b2-142">b.</span><span class="sxs-lookup"><span data-stu-id="a59b2-142">b.</span></span> <span data-ttu-id="a59b2-143">W hello **Dodaj odwołanie** okna dialogowego kliknij hello **Framework** kartę na powitania po lewej stronie i w hello **wyszukiwania** wpisz **System.ServiceModel.Web** .</span><span class="sxs-lookup"><span data-stu-id="a59b2-143">In hello **Add Reference** dialog box, click hello **Framework** tab on hello left-hand side and in hello **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="a59b2-144">Wybierz hello **System.ServiceModel.Web** pole wyboru, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-144">Select hello **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="a59b2-145">Dodaj następujące hello `using` instrukcje na początku pliku Program.cs hello hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-145">Add hello following `using` statements at hello top of hello Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="a59b2-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) jest hello przestrzeni nazw, która zapewnia dostęp programistyczny toobasic funkcji usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="a59b2-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables programmatic access toobasic features of WCF.</span></span> <span data-ttu-id="a59b2-147">Przekaźnik WCF używa wielu hello obiektów i atrybutów kontraktów usług WCF toodefine.</span><span class="sxs-lookup"><span data-stu-id="a59b2-147">WCF Relay uses many of hello objects and attributes of WCF toodefine service contracts.</span></span> <span data-ttu-id="a59b2-148">W większości aplikacji przekaźnika użyjesz tej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="a59b2-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="a59b2-149">Podobnie [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) pomaga zdefiniować kanał hello jest obiektem hello służącym do komunikacji z przeglądarką sieci web Azure przekazywania i powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="a59b2-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define hello channel, which is hello object through which you communicate with Azure Relay and hello client web browser.</span></span> <span data-ttu-id="a59b2-150">Na koniec [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) zawiera typy hello, umożliwiające toocreate aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a59b2-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains hello types that enable you toocreate web-based applications.</span></span>
7. <span data-ttu-id="a59b2-151">Zmień nazwę hello `ImageListener` przestrzeni nazw zbyt**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-151">Rename hello `ImageListener` namespace too**Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="a59b2-152">Bezpośrednio po hello otwierania nawiasie klamrowym deklaracji przestrzeni nazw hello, zdefiniuj nowy interfejs o nazwie **IImageContract** i zastosować hello **ServiceContractAttribute** interfejs toohello atrybutu wartość `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="a59b2-152">Directly after hello opening curly brace of hello namespace declaration, define a new interface named **IImageContract** and apply hello **ServiceContractAttribute** attribute toohello interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="a59b2-153">Wartość przestrzeni nazw Hello różni się od przestrzeni nazw hello, używanej w całym zakresie hello kodu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-153">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="a59b2-154">Wartość przestrzeni nazw Hello jest używany jako unikatowy identyfikator dla tego kontraktu i powinna zawierać informacje o wersji.</span><span class="sxs-lookup"><span data-stu-id="a59b2-154">hello namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="a59b2-155">Aby uzyskać więcej informacji, zobacz [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498) (Obsługa wersji usług).</span><span class="sxs-lookup"><span data-stu-id="a59b2-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="a59b2-156">Jawne określenie hello przestrzeni nazw zapobiega dodawaniu Nazwa kontraktu toohello hello domyślnej wartości przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="a59b2-156">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="a59b2-157">W ramach hello `IImageContract` interfejsu, Zadeklaruj metodę dla hello jednej operacji hello `IImageContract` ujawnia kontraktu w hello na interfejsie i Zastosuj hello `OperationContractAttribute` atrybutu metody toohello mają tooexpose w ramach publicznej hello magistrali kontrakt.</span><span class="sxs-lookup"><span data-stu-id="a59b2-157">Within hello `IImageContract` interface, declare a method for hello single operation hello `IImageContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="a59b2-158">W hello **OperationContract** atrybutu, Dodaj hello **WebGet** wartości.</span><span class="sxs-lookup"><span data-stu-id="a59b2-158">In hello **OperationContract** attribute, add hello **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="a59b2-159">Grozi to umożliwia hello tooroute usługi przekazywania żądania HTTP GET zbyt`GetImage`i zwracać wartości hello tootranslate `GetImage` do odpowiedzi metody GETRESPONSE protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="a59b2-159">Doing so enables hello relay service tooroute HTTP GET requests too`GetImage`, and tootranslate hello return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="a59b2-160">Później w samouczku hello użyjesz tooaccess przeglądarki sieci web — metoda i toodisplay obraz powitania w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-160">Later in hello tutorial, you will use a web browser tooaccess this method, and toodisplay hello image in hello browser.</span></span>
11. <span data-ttu-id="a59b2-161">Bezpośrednio po hello `IImageContract` definicji, Zadeklaruj kanał dziedziczący zarówno hello `IImageContract` i `IClientChannel` interfejsów.</span><span class="sxs-lookup"><span data-stu-id="a59b2-161">Directly after hello `IImageContract` definition, declare a channel that inherits from both hello `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="a59b2-162">Kanał jest obiektem usługi WCF hello za pośrednictwem której hello usługa i klient przekazują informacje tooeach innych.</span><span class="sxs-lookup"><span data-stu-id="a59b2-162">A channel is hello WCF object through which hello service and client pass information tooeach other.</span></span> <span data-ttu-id="a59b2-163">Później utworzysz kanał hello w aplikacji hosta.</span><span class="sxs-lookup"><span data-stu-id="a59b2-163">Later, you will create hello channel in your host application.</span></span> <span data-ttu-id="a59b2-164">Azure przekazywania następnie używa tego kanału toopass hello żądania HTTP GET hello przeglądarki tooyour **GetImage** implementacji.</span><span class="sxs-lookup"><span data-stu-id="a59b2-164">Azure Relay then uses this channel toopass hello HTTP GET requests from hello browser tooyour **GetImage** implementation.</span></span> <span data-ttu-id="a59b2-165">Przekaźnik Hello używa również hello kanału tootake hello **GetImage** zwracać wartości i umożliwiło metody GETRESPONSE protokołu HTTP dla przeglądarki klienta hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-165">hello relay also uses hello channel tootake hello **GetImage** return value and translate it into an HTTP GETRESPONSE for hello client browser.</span></span>
12. <span data-ttu-id="a59b2-166">Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** tooconfirm hello dokładność pracy wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="a59b2-166">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="a59b2-167">Przykład</span><span class="sxs-lookup"><span data-stu-id="a59b2-167">Example</span></span>
<span data-ttu-id="a59b2-168">powitania po kod przedstawia podstawowy interfejs definiujący kontrakt usługi WCF przekazywania.</span><span class="sxs-lookup"><span data-stu-id="a59b2-168">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a><span data-ttu-id="a59b2-169">Krok 3: Implementowanie toouse kontraktu usługi WCF opartego na interfejsie REST usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="a59b2-169">Step 3: Implement a REST-based WCF service contract toouse Service Bus</span></span>
<span data-ttu-id="a59b2-170">Tworzenie usługi typu REST usługi WCF przekazywania wymaga najpierw utworzyć kontrakt hello, który został zdefiniowany przy użyciu interfejsu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-170">Creating a REST-style WCF Relay service requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="a59b2-171">Witaj następnym krokiem jest tooimplement hello interfejsu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-171">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="a59b2-172">Obejmuje to tworzenie klasy o nazwie **ImageService** hello zdefiniowane przez użytkownika, który zawiera **IImageContract** interfejsu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-172">This involves creating a class named **ImageService** that implements hello user-defined **IImageContract** interface.</span></span> <span data-ttu-id="a59b2-173">Po zaimplementowaniu kontraktu hello, następnie należy skonfigurować interfejs hello przy użyciu pliku App.config.</span><span class="sxs-lookup"><span data-stu-id="a59b2-173">After you implement hello contract, you then configure hello interface using an App.config file.</span></span> <span data-ttu-id="a59b2-174">Witaj plik konfiguracji zawiera niezbędne informacje dotyczące aplikacji hello, takie jak nazwa hello hello usługi, nazwa hello hello kontraktu i typ hello protokołu, który jest używany toocommunicate z usługą przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-174">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="a59b2-175">Kod Hello używany do wykonywania tych zadań podano w przykład Witaj hello procedury.</span><span class="sxs-lookup"><span data-stu-id="a59b2-175">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

<span data-ttu-id="a59b2-176">Podobnie jak w poprzednich kroków hello, jest bardzo mało różnica między implementacją kontraktu typu REST i kontraktu usługi WCF przekazywania.</span><span class="sxs-lookup"><span data-stu-id="a59b2-176">As with hello previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="tooimplement-a-rest-style-service-bus-contract"></a><span data-ttu-id="a59b2-177">kontrakt usługi Service Bus tooimplement typu REST</span><span class="sxs-lookup"><span data-stu-id="a59b2-177">tooimplement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="a59b2-178">Utwórz nową klasę o nazwie **ImageService** bezpośrednio po definicji hello hello **IImageContract** interfejsu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-178">Create a new class named **ImageService** directly after hello definition of hello **IImageContract** interface.</span></span> <span data-ttu-id="a59b2-179">Witaj **ImageService** klasa implementuje hello **IImageContract** interfejsu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-179">hello **ImageService** class implements hello **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="a59b2-180">Podobne implementacje interfejsu tooother, można zaimplementować definicję hello w innym pliku.</span><span class="sxs-lookup"><span data-stu-id="a59b2-180">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="a59b2-181">Jednak w tym samouczku implementacji hello jest wyświetlana w hello tego samego pliku jako hello definicja interfejsu i `Main()` metody.</span><span class="sxs-lookup"><span data-stu-id="a59b2-181">However, for this tutorial, hello implementation appears in hello same file as hello interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="a59b2-182">Zastosuj hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atrybutu toohello **IImageService** tooindicate klasy, która hello klasa jest implementacją kontraktu usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="a59b2-182">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello **IImageService** class tooindicate that hello class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="a59b2-183">Jak wspomniano wcześniej, ta przestrzeń nazw nie jest tradycyjną przestrzenią nazw.</span><span class="sxs-lookup"><span data-stu-id="a59b2-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="a59b2-184">Zamiast tego jest częścią architektury usługi WCF, która identyfikuje kontrakt hello hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-184">Instead, it is part of hello WCF architecture that identifies hello contract.</span></span> <span data-ttu-id="a59b2-185">Aby uzyskać więcej informacji, zobacz hello [nazwy kontraktów danych](https://msdn.microsoft.com/library/ms731045.aspx) tematu w hello dokumentacji usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="a59b2-185">For more information, see hello [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in hello WCF documentation.</span></span>
3. <span data-ttu-id="a59b2-186">Dodaj projekt tooyour obrazów JPG.</span><span class="sxs-lookup"><span data-stu-id="a59b2-186">Add a .jpg image tooyour project.</span></span>  
   
    <span data-ttu-id="a59b2-187">Jest to obraz powitania usługa wyświetla w hello odbieranie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="a59b2-187">This is a picture that hello service displays in hello receiving browser.</span></span> <span data-ttu-id="a59b2-188">Kliknij prawym przyciskiem myszy projekt i kliknij polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="a59b2-189">Następnie kliknij pozycję **Istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-189">Then click **Existing Item**.</span></span> <span data-ttu-id="a59b2-190">Użyj hello **Dodaj istniejący element** tooan toobrowse — okno dialogowe odpowiednie jpg, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-190">Use hello **Add Existing Item** dialog box toobrowse tooan appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="a59b2-191">Podczas dodawania pliku hello, upewnij się, że **wszystkie pliki** w toohello dalej hello listy rozwijanej zostanie wybrany **nazwa pliku:** pola.</span><span class="sxs-lookup"><span data-stu-id="a59b2-191">When adding hello file, make sure that **All Files** is selected in hello drop-down list next toohello **File name:** field.</span></span> <span data-ttu-id="a59b2-192">Witaj pozostałej części tego samouczka przyjęto założenie, że hello nazwa obrazu hello to "image.jpg".</span><span class="sxs-lookup"><span data-stu-id="a59b2-192">hello rest of this tutorial assumes that hello name of hello image is "image.jpg".</span></span> <span data-ttu-id="a59b2-193">Inny plik będzie mieć toorename hello obraz, lub zmień toocompensate Twojego kodu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-193">If you have a different file, you will have toorename hello image, or change your code toocompensate.</span></span>
4. <span data-ttu-id="a59b2-194">toomake się upewnić, że hello usługą można znaleźć plik obrazu hello, w **Eksploratora rozwiązań** kliknij prawym przyciskiem myszy plik obrazu hello, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-194">toomake sure that hello running service can find hello image file, in **Solution Explorer** right-click hello image file, then click **Properties**.</span></span> <span data-ttu-id="a59b2-195">W hello **właściwości** ustawić okienku **skopiuj tooOutput katalogu** za**Kopiuj, jeśli nowszy**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-195">In hello **Properties** pane, set **Copy tooOutput Directory** too**Copy if newer**.</span></span>
5. <span data-ttu-id="a59b2-196">Dodaj toohello odwołanie **System.Drawing.dll** toohello zestawu projektu, a także dodać następujące hello skojarzone `using` instrukcje.</span><span class="sxs-lookup"><span data-stu-id="a59b2-196">Add a reference toohello **System.Drawing.dll** assembly toohello project, and also add hello following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="a59b2-197">W hello **ImageService** klasy, Dodaj hello następujących konstruktora, że obciążenie hello mapę bitową i przygotowuje toosend on toohello przeglądarki klienta.</span><span class="sxs-lookup"><span data-stu-id="a59b2-197">In hello **ImageService** class, add hello following constructor that loads hello bitmap and prepares toosend it toohello client browser.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. <span data-ttu-id="a59b2-198">Bezpośrednio po poprzednim kodzie hello Dodaj następujące hello **GetImage** metoda hello **ImageService** klasy tooreturn HTTP komunikat, który zawiera obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="a59b2-198">Directly after hello previous code, add hello following **GetImage** method in hello **ImageService** class tooreturn an HTTP message that contains hello image.</span></span>
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    <span data-ttu-id="a59b2-199">Ta implementacja używa **MemoryStream** tooretrieve hello obrazu i przygotowywania ich do przesyłania strumieniowego toohello przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="a59b2-199">This implementation uses **MemoryStream** tooretrieve hello image and prepare it for streaming toohello browser.</span></span> <span data-ttu-id="a59b2-200">Go uruchamia hello strumieniowe w pozycji zero, deklaruje zawartość strumienia hello jako obraz jpeg i strumieni hello informacji.</span><span class="sxs-lookup"><span data-stu-id="a59b2-200">It starts hello stream position at zero, declares hello stream content as a jpeg, and streams hello information.</span></span>
8. <span data-ttu-id="a59b2-201">Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-201">From hello **Build** menu, click **Build Solution**.</span></span>

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a><span data-ttu-id="a59b2-202">toodefine hello konfigurację uruchamiania usługi sieci web hello usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="a59b2-202">toodefine hello configuration for running hello web service on Service Bus</span></span>
1. <span data-ttu-id="a59b2-203">W **Eksploratora rozwiązań**, kliknij dwukrotnie **App.config** tooopen go w edytorze programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-203">In **Solution Explorer**, double-click **App.config** tooopen it in hello Visual Studio editor.</span></span>
   
    <span data-ttu-id="a59b2-204">Witaj **App.config** plik zawiera hello nazwy usługi, punkt końcowy (to znaczy hello lokalizację przekazywania Azure udostępnia dla klientów i hosty toocommunicate ze sobą) i powiązanie (typ hello protokół, który jest używany toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="a59b2-204">hello **App.config** file includes hello service name, endpoint (that is, hello location Azure Relay exposes for clients and hosts toocommunicate with each other), and binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="a59b2-205">Witaj główną różnicą jest ten punkt końcowy usługi hello skonfigurowane odwołuje się tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) powiązania.</span><span class="sxs-lookup"><span data-stu-id="a59b2-205">hello main difference here is that hello configured service endpoint refers tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="a59b2-206">Witaj `<system.serviceModel>` — element XML jest elementem usługi WCF, który definiuje co najmniej jedna usługa.</span><span class="sxs-lookup"><span data-stu-id="a59b2-206">hello `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="a59b2-207">W tym miejscu jest nazwa usługi hello toodefine używane i punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="a59b2-207">Here, it is used toodefine hello service name and endpoint.</span></span> <span data-ttu-id="a59b2-208">U dołu hello hello `<system.serviceModel>` elementu (ale nadal w ramach `<system.serviceModel>`), Dodaj `<bindings>` element, który ma powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="a59b2-208">At hello bottom of hello `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has hello following content.</span></span> <span data-ttu-id="a59b2-209">Definiuje hello powiązania używane w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-209">This defines hello bindings used in hello application.</span></span> <span data-ttu-id="a59b2-210">Można zdefiniować wiele powiązań, ale w tym samouczku definiowane jest tylko jedno.</span><span class="sxs-lookup"><span data-stu-id="a59b2-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    <span data-ttu-id="a59b2-211">Witaj poprzedni kod definiuje przekazywania WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) powiązanie o **relayClientAuthenticationType** ustawić także**Brak**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-211">hello previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set too**None**.</span></span> <span data-ttu-id="a59b2-212">To ustawienie wskazuje, że punkt końcowy korzystający z tego powiązania nie wymaga poświadczeń klienta.</span><span class="sxs-lookup"><span data-stu-id="a59b2-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="a59b2-213">Po hello `<bindings>` elementu, Dodaj `<services>` elementu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-213">After hello `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="a59b2-214">Podobnymi powiązaniami toohello, można zdefiniować wiele usług w pojedynczym pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a59b2-214">Similar toohello bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="a59b2-215">Jednak w tym samouczku definiowana jest tylko jedna.</span><span class="sxs-lookup"><span data-stu-id="a59b2-215">However, for this tutorial, you define only one.</span></span>
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    <span data-ttu-id="a59b2-216">Ten krok obejmuje skonfigurowanie usługi, która będzie używana domyślna hello wcześniej zdefiniowany **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="a59b2-216">This step configures a service that uses hello previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="a59b2-217">Używa również domyślny hello **sbTokenProvider**, która jest zdefiniowana w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="a59b2-217">It also uses hello default **sbTokenProvider**, which is defined in hello next step.</span></span>
4. <span data-ttu-id="a59b2-218">Po hello `<services>` elementu, Utwórz `<behaviors>` element z powitania po zawartości, zastępując "element SAS_KEY" hello *sygnatura dostępu współdzielonego* klucza (SAS) uzyskanym wcześniej z hello [portalu Azure ][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="a59b2-218">After hello `<services>` element, create a `<behaviors>` element with hello following content, replacing "SAS_KEY" with hello *Shared Access Signature* (SAS) key you previously obtained from hello [Azure portal][Azure portal].</span></span>
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. <span data-ttu-id="a59b2-219">Nadal w pliku App.config w hello `<appSettings>` elementu, Zastąp hello całego połączenia ciąg wartości z ciągu połączenia hello uzyskanym wcześniej z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-219">Still in App.config, in hello `<appSettings>` element, replace hello entire connection string value with hello connection string you previously obtained from hello portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="a59b2-220">Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** toobuild hello całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="a59b2-220">From hello **Build** menu, click **Build Solution** toobuild hello entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="a59b2-221">Przykład</span><span class="sxs-lookup"><span data-stu-id="a59b2-221">Example</span></span>
<span data-ttu-id="a59b2-222">Witaj poniższy kod przedstawia implementację kontraktu i usługi dla usługi opartego na interfejsie REST uruchomionej na magistrali usług przy użyciu hello hello **WebHttpRelayBinding** powiązania.</span><span class="sxs-lookup"><span data-stu-id="a59b2-222">hello following code shows hello contract and service implementation for a REST-based service that is running on  Service Bus using hello **WebHttpRelayBinding** binding.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="a59b2-223">Witaj poniższy przykład przedstawia plik App.config hello skojarzonych z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-223">hello following example shows hello App.config file associated with hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a><span data-ttu-id="a59b2-224">Krok 4: Hostowanie toouse usługi WCF opartego na interfejsie REST hello Azure przekazywania</span><span class="sxs-lookup"><span data-stu-id="a59b2-224">Step 4: Host hello REST-based WCF service toouse Azure Relay</span></span>
<span data-ttu-id="a59b2-225">W tym kroku opisano, jak toorun sieci web usługi, przy użyciu aplikacji konsoli z przekaźnika usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="a59b2-225">This step describes how toorun a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="a59b2-226">Pełna lista hello kod napisany w tym kroku podano w przykład Witaj hello procedury.</span><span class="sxs-lookup"><span data-stu-id="a59b2-226">A complete listing of hello code written in this step is provided in hello example following hello procedure.</span></span>

### <a name="toocreate-a-base-address-for-hello-service"></a><span data-ttu-id="a59b2-227">adres podstawowy usługi hello toocreate</span><span class="sxs-lookup"><span data-stu-id="a59b2-227">toocreate a base address for hello service</span></span>
1. <span data-ttu-id="a59b2-228">W hello `Main()` deklaracji funkcji, tworzenie przestrzeni nazw hello zmiennej toostore projektu.</span><span class="sxs-lookup"><span data-stu-id="a59b2-228">In hello `Main()` function declaration, create a variable toostore hello namespace of your project.</span></span> <span data-ttu-id="a59b2-229">Upewnij się, że tooreplace `yourNamespace` o nazwie hello hello nazw przekaźnika utworzonego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="a59b2-229">Make sure tooreplace `yourNamespace` with hello name of hello Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="a59b2-230">Usługa Service Bus używa hello nazwą Twojej przestrzeni nazw toocreate Unikatowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="a59b2-230">Service Bus uses hello name of your namespace toocreate a unique URI.</span></span>
2. <span data-ttu-id="a59b2-231">Utwórz `Uri` wystąpienia dla adresu podstawowego hello hello usługi, która jest oparta na powitania przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="a59b2-231">Create a `Uri` instance for hello base address of hello service that is based on hello namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a><span data-ttu-id="a59b2-232">toocreate i skonfigurować hosta usługi sieci web hello</span><span class="sxs-lookup"><span data-stu-id="a59b2-232">toocreate and configure hello web service host</span></span>
* <span data-ttu-id="a59b2-233">Utwórz hosta usługi sieci web hello przy użyciu hello adresu URI utworzonego wcześniej w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a59b2-233">Create hello web service host, using hello URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="a59b2-234">host usługi Hello jest hello WCF obiekt, który tworzy hello aplikacji hosta.</span><span class="sxs-lookup"><span data-stu-id="a59b2-234">hello service host is hello WCF object that instantiates hello host application.</span></span> <span data-ttu-id="a59b2-235">W tym przykładzie przekazuje hello typ hosta ma toocreate ( **ImageService**), a także hello adres, w którym chcesz tooexpose hello hosta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a59b2-235">This example passes it hello type of host you want toocreate (an **ImageService**), and also hello address at which you want tooexpose hello host application.</span></span>

### <a name="toorun-hello-web-service-host"></a><span data-ttu-id="a59b2-236">host usługi sieci web hello toorun</span><span class="sxs-lookup"><span data-stu-id="a59b2-236">toorun hello web service host</span></span>
1. <span data-ttu-id="a59b2-237">Otwórz usługę hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-237">Open hello service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="a59b2-238">Usługa Hello jest teraz uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="a59b2-238">hello service is now running.</span></span>
2. <span data-ttu-id="a59b2-239">Wyświetla komunikat informujący, że usługa hello jest uruchomiona, i jak toostop hello usługi.</span><span class="sxs-lookup"><span data-stu-id="a59b2-239">Display a message indicating that hello service is running, and how toostop hello service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="a59b2-240">Po zakończeniu zamknij hosta usługi hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-240">When finished, close hello service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="a59b2-241">Przykład</span><span class="sxs-lookup"><span data-stu-id="a59b2-241">Example</span></span>
<span data-ttu-id="a59b2-242">Hello poniższy przykład zawiera hello kontrakt usługi i implementację z poprzednich kroków w usłudze hello samouczek i hosty hello w aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="a59b2-242">hello following example includes hello service contract and implementation from previous steps in hello tutorial and hosts hello service in a console application.</span></span> <span data-ttu-id="a59b2-243">Kompiluj powitania po kod do pliku wykonywalnego o nazwie ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="a59b2-243">Compile hello following code into an executable named ImageListener.exe.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a><span data-ttu-id="a59b2-244">Kompilowanie kodu hello</span><span class="sxs-lookup"><span data-stu-id="a59b2-244">Compiling hello code</span></span>
<span data-ttu-id="a59b2-245">Po utworzeniu rozwiązania hello, hello następujących aplikacji hello toorun:</span><span class="sxs-lookup"><span data-stu-id="a59b2-245">After building hello solution, do hello following toorun hello application:</span></span>

1. <span data-ttu-id="a59b2-246">Naciśnij klawisz **F5**, lub Wyszukaj toohello lokalizacji pliku wykonywalnego (ImageListener\bin\Debug\ImageListener.exe), toorun hello usługi.</span><span class="sxs-lookup"><span data-stu-id="a59b2-246">Press **F5**, or browse toohello executable file location (ImageListener\bin\Debug\ImageListener.exe), toorun hello service.</span></span> <span data-ttu-id="a59b2-247">Zachowaj hello aplikacja działa, ponieważ są wymagane tooperform hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="a59b2-247">Keep hello app running, as it's required tooperform hello next step.</span></span>
2. <span data-ttu-id="a59b2-248">Skopiuj i wklej adres hello z wiersza polecenia hello obraz powitania toosee przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="a59b2-248">Copy and paste hello address from hello command prompt into a browser toosee hello image.</span></span>
3. <span data-ttu-id="a59b2-249">Po zakończeniu naciśnij klawisz **Enter** w aplikacja hello tooclose w oknie wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="a59b2-249">When you are finished, press **Enter** in hello command prompt window tooclose hello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a59b2-250">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a59b2-250">Next steps</span></span>
<span data-ttu-id="a59b2-251">Teraz gdy masz utworzoną aplikację, która używa przekaźnika usługi Service Bus hello, zobacz hello następujące artykuły toolearn więcej temat przekaźnika usługi Azure:</span><span class="sxs-lookup"><span data-stu-id="a59b2-251">Now that you've built an application that uses hello Service Bus relay service, see hello following articles toolearn more about Azure Relay:</span></span>

* [<span data-ttu-id="a59b2-252">Omówienie architektury usługi Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="a59b2-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="a59b2-253">Omówienie usługi Azure Relay</span><span class="sxs-lookup"><span data-stu-id="a59b2-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="a59b2-254">Jak usługa z platformą .NET przekazywania toouse hello WCF</span><span class="sxs-lookup"><span data-stu-id="a59b2-254">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
