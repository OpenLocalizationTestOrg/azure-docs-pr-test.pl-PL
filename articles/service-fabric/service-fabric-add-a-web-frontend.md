---
title: "aaaCreate frontonu sieci web dla aplikacji sieci szkieletowej usług Azure przy użyciu platformy ASP.NET Core | Dokumentacja firmy Microsoft"
description: "Udostępnianie sieci web toohello aplikacji sieci szkieletowej usług za pomocą platformy ASP.NET Core projektu i komunikacja między usługami komunikacji za pośrednictwem komunikacji zdalnej usługi."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="dd1f5-103">Tworzenie frontonu sieci web usługi aplikacji przy użyciu platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="dd1f5-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="dd1f5-104">Domyślnie usługi sieć szkieletowa usług Azure nie udostępniają toohello publiczny interfejs sieci web.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-104">By default, Azure Service Fabric services do not provide a public interface toohello web.</span></span> <span data-ttu-id="dd1f5-105">tooexpose klientów tooHTTP funkcji aplikacji, masz toocreate sieci web projektu tooact jako punkt wejścia, a następnie komunikować się z tooyour występują poszczególnych usług.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-105">tooexpose your application's functionality tooHTTP clients, you have toocreate a web project tooact as an entry point and then communicate from there tooyour individual services.</span></span>

<span data-ttu-id="dd1f5-106">W tym samouczku będziemy uruchomienia instalacji gdzie możemy przerwał pracę w hello [tworzenie pierwszej aplikacji w programie Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) samouczka i Dodaj usługę sieci web platformy ASP.NET Core przed hello usługi stanowej licznika.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-106">In this tutorial, we pick up where we left off in hello [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of hello stateful counter service.</span></span> <span data-ttu-id="dd1f5-107">Jeśli jeszcze nie możesz wrócić do poprzedniej strony i najpierw kroków opisanych w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="dd1f5-108">Konfigurowanie środowiska dla platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="dd1f5-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="dd1f5-109">Należy toofollow programu Visual Studio 2017 wraz z tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-109">You need Visual Studio 2017 toofollow along with this tutorial.</span></span> <span data-ttu-id="dd1f5-110">Dowolna wersja będzie wykonywać.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="dd1f5-111">Zainstaluj program Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="dd1f5-112">toodevelop aplikacji platformy ASP.NET Core Service Fabric, powinny mieć powitania po obciążeń zainstalowane:</span><span class="sxs-lookup"><span data-stu-id="dd1f5-112">toodevelop ASP.NET Core Service Fabric applications, you should have hello following workloads installed:</span></span>
 - <span data-ttu-id="dd1f5-113">**Programowanie Azure** (w obszarze *sieci Web & chmurze*)</span><span class="sxs-lookup"><span data-stu-id="dd1f5-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="dd1f5-114">**ASP.NET i sieć web development** (w obszarze *sieci Web & chmurze*)</span><span class="sxs-lookup"><span data-stu-id="dd1f5-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="dd1f5-115">**Programowanie wieloplatformowych .NET core** (w obszarze *inne procesami*)</span><span class="sxs-lookup"><span data-stu-id="dd1f5-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="dd1f5-116">Witaj .NET Core tools dla programu Visual Studio 2015 są już aktualizowany, jednak są nadal przy użyciu programu Visual Studio 2015, konieczne będzie toohave [.NET Core VS 2015 narzędzi Preview 2](https://www.microsoft.com/net/download/core) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-116">hello .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-tooyour-application"></a><span data-ttu-id="dd1f5-117">Dodawanie aplikacji ASP.NET Core tooyour usługi</span><span class="sxs-lookup"><span data-stu-id="dd1f5-117">Add an ASP.NET Core service tooyour application</span></span>
<span data-ttu-id="dd1f5-118">Platformy ASP.NET Core to platforma programistyczna lekka międzyplatformowa sieci web można używać nowoczesnych toocreate interfejsu użytkownika sieci web i interfejsów API sieci web.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> 

<span data-ttu-id="dd1f5-119">Dodajmy istniejącej aplikacji tooour projektu interfejsu API sieci Web platformy ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-119">Let's add an ASP.NET Web API project tooour existing application.</span></span>

1. <span data-ttu-id="dd1f5-120">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **usług** poziomu projekt aplikacji hello i wybierz polecenie **Dodaj > Nowa usługa sieci szkieletowej usług**.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-120">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Dodawanie nowej usługi tooan istniejącej aplikacji][vs-add-new-service]
2. <span data-ttu-id="dd1f5-122">Na powitania **Tworzenie usługi** wybierz pozycję **platformy ASP.NET Core** i nadaj mu nazwę.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-122">On hello **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![Wybieranie usługi sieci web ASP.NET w oknie dialogowym hello nowej usługi][vs-new-service-dialog]

3. <span data-ttu-id="dd1f5-124">Witaj następnej strony zawiera zestaw platformy ASP.NET Core szablonów projektu.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-124">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="dd1f5-125">Należy pamiętać, że te są hello sama usługa ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello hello wyborów, że można zobaczyć został utworzony projekt platformy ASP.NET Core poza aplikacją sieci szkieletowej usług z małej ilości tooregister dodatkowy kod.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-125">Note that these are hello same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code tooregister hello service with hello Service Fabric runtime.</span></span> <span data-ttu-id="dd1f5-126">W tym samouczku, wybierz **interfejsu API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="dd1f5-127">Jednak możesz zastosować hello tego samego pojęcia toobuilding aplikacji sieci web pełna.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-127">However, you can apply hello same concepts toobuilding a full web application.</span></span>
   
    ![Wybieranie typu projektu programu ASP.NET][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="dd1f5-129">Po utworzeniu projektu interfejsu API sieci Web powinien mieć dwie usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="dd1f5-130">Kontynuując toobuild aplikacji, można dodać więcej usług w hello dokładnie tak samo.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-130">As you continue toobuild your application, you can add more services in exactly hello same way.</span></span> <span data-ttu-id="dd1f5-131">Każdy może być niezależnie określonej wersji, jak i uaktualnionych.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="dd1f5-132">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="dd1f5-132">Run hello application</span></span>
<span data-ttu-id="dd1f5-133">tooget zorientować się, co możemy wykonane, umożliwia wdrażanie nowej aplikacji hello i podejmij zapewnia przyjrzeć się hello domyślne zachowanie hello szablonu interfejsu API platformy ASP.NET Core sieci Web.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-133">tooget a sense of what we've done, let's deploy hello new application and take a look at hello default behavior that hello ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="dd1f5-134">Naciśnij klawisz F5 w programie Visual Studio toodebug hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-134">Press F5 in Visual Studio toodebug hello app.</span></span>
2. <span data-ttu-id="dd1f5-135">Po zakończeniu wdrożenia programu Visual Studio uruchamia głównego toohello przeglądarki z hello usługi interfejsu API sieci Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-135">When deployment is complete, Visual Studio launches a browser toohello root of hello ASP.NET Web API service.</span></span> <span data-ttu-id="dd1f5-136">Hello Web API platformy ASP.NET Core szablonu nie udostępniają domyślne zachowanie dla elementu głównego hello, więc powinna zostać wyświetlona w przeglądarce hello błąd 404.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-136">hello ASP.NET Core Web API template doesn't provide default behavior for hello root, so you should see a 404 error in hello browser.</span></span>
3. <span data-ttu-id="dd1f5-137">Dodaj `/api/values` toohello lokalizacji w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-137">Add `/api/values` toohello location in hello browser.</span></span> <span data-ttu-id="dd1f5-138">Wywołuje to hello `Get` metody na powitania ValuesController hello szablonu interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-138">This invokes hello `Get` method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="dd1f5-139">Zwraca odpowiedź domyślna hello dostarczone przez szablon hello — tablicy JSON, który zawiera dwa ciągi:</span><span class="sxs-lookup"><span data-stu-id="dd1f5-139">It returns hello default response that is provided by hello template--a JSON array that contains two strings:</span></span>
   
    ![Wartości domyślne zwrócony z interfejsu API platformy ASP.NET Core sieci Web szablonu][browser-aspnet-template-values]
   
    <span data-ttu-id="dd1f5-141">Hello koniec samouczka hello ta strona wyświetli hello najbardziej aktualną wartość licznika z naszej usługi stanowej zamiast hello domyślne parametry.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-141">By hello end of hello tutorial, this page will show hello most recent counter value from our stateful service instead of hello default strings.</span></span>

## <a name="connect-hello-services"></a><span data-ttu-id="dd1f5-142">Połączenie usług hello</span><span class="sxs-lookup"><span data-stu-id="dd1f5-142">Connect hello services</span></span>
<span data-ttu-id="dd1f5-143">Sieć szkieletowa usług oferuje pełną elastyczność w sposób komunikowania się z usługami reliable services.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="dd1f5-144">Wewnątrz aplikacji konieczne może być usług, które są dostępne za pośrednictwem protokołu TCP, innych usług, które są dostępne za pośrednictwem interfejsu API REST protokołu HTTP i nadal innych usług, które są dostępne za pośrednictwem gniazda sieci web.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="dd1f5-145">W tle na dostępne opcje hello oraz kompromisy hello zaangażowany, zobacz [komunikacji z usługami](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="dd1f5-145">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="dd1f5-146">W tym samouczku używamy [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), podany w hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in hello SDK.</span></span>

<span data-ttu-id="dd1f5-147">W hello podejście Service Remoting (zaprojektowany na zdalnych wywołań procedur lub RPC) można zdefiniować jako hello publicznego kontraktu usługi hello tooact interfejsu.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-147">In hello Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface tooact as hello public contract for hello service.</span></span> <span data-ttu-id="dd1f5-148">Następnie należy użyć tego toogenerate interfejsu klasy serwera proxy do interakcji z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-148">Then, you use that interface toogenerate a proxy class for interacting with hello service.</span></span>

### <a name="create-hello-remoting-interface"></a><span data-ttu-id="dd1f5-149">Tworzenie interfejsu usług zdalnych hello</span><span class="sxs-lookup"><span data-stu-id="dd1f5-149">Create hello remoting interface</span></span>
<span data-ttu-id="dd1f5-150">Zacznijmy od utworzenia tooact interfejsu hello jako kontraktu hello między usługi stanowej hello i innych usług, w tym wielkość hello projektu sieci web platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-150">Let's start by creating hello interface tooact as hello contract between hello stateful service and other services, in this case hello ASP.NET Core web project.</span></span> <span data-ttu-id="dd1f5-151">Ten interfejs musi być współużytkowane przez wszystkie usługi, które go używają toomake wywołania RPC, dlatego utworzymy własnego projektu biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-151">This interface must be shared by all services that use it toomake RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="dd1f5-152">W Eksploratorze rozwiązań kliknij rozwiązanie prawym przyciskiem myszy i wybierz polecenie **Dodaj** > **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="dd1f5-153">Wybierz hello **Visual C#** wpisu w hello lewego okienka nawigacji i wybierz opcję hello **biblioteki klas** szablonu.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-153">Choose hello **Visual C#** entry in hello left navigation pane and then select hello **Class Library** template.</span></span> <span data-ttu-id="dd1f5-154">Upewnij się, ta wersja .NET Framework hello ustawiono zbyt**4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-154">Ensure that hello .NET Framework version is set too**4.5.2**.</span></span>
   
    ![Tworzenie projektu interfejsu usługi stanowej][vs-add-class-library-project]

3. <span data-ttu-id="dd1f5-156">Zainstaluj hello **Microsoft.ServiceFabric.Services.Remoting** pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-156">Install hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="dd1f5-157">Wyszukaj **Microsoft.ServiceFabric.Services.Remoting** w hello NuGet pakietu manager, a następnie zainstaluj go dla wszystkich projektów w rozwiązaniu hello korzystających Service Remoting, w tym:</span><span class="sxs-lookup"><span data-stu-id="dd1f5-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager and install it for all projects in hello solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="dd1f5-158">Projekt biblioteki klas Hello, który zawiera hello interfejsu usługi</span><span class="sxs-lookup"><span data-stu-id="dd1f5-158">hello Class Library project that contains hello service interface</span></span>
   - <span data-ttu-id="dd1f5-159">projekt usługi Stateful Hello</span><span class="sxs-lookup"><span data-stu-id="dd1f5-159">hello Stateful Service project</span></span>
   - <span data-ttu-id="dd1f5-160">Witaj projekt usługi sieci web platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="dd1f5-160">hello ASP.NET Core web service project</span></span>
   
    ![Dodawanie pakietu NuGet usługi hello][vs-services-nuget-package]

4. <span data-ttu-id="dd1f5-162">W bibliotece klas hello, Tworzenie interfejsu z jedną metodę `GetCountAsync`, i rozszerzenie interfejsu hello `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-162">In hello class library, create an interface with a single method, `GetCountAsync`, and extend hello interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="dd1f5-163">interfejsu usług zdalnych Hello musi pochodzić od tooindicate tego interfejsu, jest interfejsem Service Remoting.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-163">hello remoting interface must derive from this interface tooindicate that it is a Service Remoting interface.</span></span>
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a><span data-ttu-id="dd1f5-164">Implementowanie interfejsu hello w usłudze stanowe</span><span class="sxs-lookup"><span data-stu-id="dd1f5-164">Implement hello interface in your stateful service</span></span>
<span data-ttu-id="dd1f5-165">Teraz, gdy zdefiniowaniu hello interfejsu, potrzebujemy tooimplement w usługi stanowej hello.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-165">Now that we have defined hello interface, we need tooimplement it in hello stateful service.</span></span>

1. <span data-ttu-id="dd1f5-166">W usłudze stanowe dodać projektu biblioteki klas toohello odwołania, zawierający hello interfejsu.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-166">In your stateful service, add a reference toohello class library project that contains hello interface.</span></span>
   
    ![Dodawanie odwołania projektu biblioteki klas toohello w hello usługi stanowej][vs-add-class-library-reference]
2. <span data-ttu-id="dd1f5-168">Zlokalizuj hello klasy, która dziedziczy `StatefulService`, takich jak `MyStatefulService`i rozszerzyć ją tooimplement hello `ICounter` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-168">Locate hello class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it tooimplement hello `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="dd1f5-169">Teraz wdrożyć hello pojedynczej metody, która jest zdefiniowana w hello `ICounter` interfejsu `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-169">Now implement hello single method that is defined in hello `ICounter` interface, `GetCountAsync`.</span></span>
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="dd1f5-170">Udostępnianie hello usługi stanowej przy użyciu odbiornika usługi zdalne usługi</span><span class="sxs-lookup"><span data-stu-id="dd1f5-170">Expose hello stateful service using a service remoting listener</span></span>
<span data-ttu-id="dd1f5-171">Z hello `ICounter` interfejsu zaimplementowanego, ostatnim krokiem hello jest kanał komunikacyjny Service Remoting hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-171">With hello `ICounter` interface implemented, hello final step is tooopen hello Service Remoting communication channel.</span></span> <span data-ttu-id="dd1f5-172">Usługi stanowej, Usługa Service Fabric realizuje z możliwością przesłonięcia metody o nazwie `CreateServiceReplicaListeners`.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="dd1f5-173">Przy użyciu tej metody można określić odbiorników komunikacji, na podstawie typu hello komunikacji mają tooenable dla usługi.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-173">With this method, you can specify one or more communication listeners, based on hello type of communication that you want tooenable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="dd1f5-174">wywoływana jest metoda równoważne Hello otwierania usług toostateless kanał komunikacji `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-174">hello equivalent method for opening a communication channel toostateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="dd1f5-175">W takim przypadku możemy zastąpić istniejący hello `CreateServiceReplicaListeners` — metoda i zapewnić wystąpienie `ServiceRemotingListener`, co powoduje z punktem końcowym które jest wywoływane z klientów za pośrednictwem `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-175">In this case, we replace hello existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="dd1f5-176">Witaj `CreateServiceRemotingListener` — metoda rozszerzenia na powitania `IService` interfejs umożliwiający tooeasily utworzyć `ServiceRemotingListener` przy użyciu wszystkich ustawień domyślnych.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-176">hello `CreateServiceRemotingListener` extension method on hello `IService` interface allows you tooeasily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="dd1f5-177">toouse tej metody rozszerzenia, upewnij się, masz hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` zaimportowane przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-177">toouse this extension method, ensure you have hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a><span data-ttu-id="dd1f5-178">Witaj ServiceProxy klasy toointeract za pomocą usługi hello</span><span class="sxs-lookup"><span data-stu-id="dd1f5-178">Use hello ServiceProxy class toointeract with hello service</span></span>
<span data-ttu-id="dd1f5-179">Nasza usługa stanowa jest teraz gotowy tooreceive ruchu z innych usług za pośrednictwem wywołania RPC.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-179">Our stateful service is now ready tooreceive traffic from other services over RPC.</span></span> <span data-ttu-id="dd1f5-180">Związku z czym jej pozostaje polega na dodaniu hello toocommunicate kodu z nim z hello usługi sieci web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-180">So all that remains is adding hello code toocommunicate with it from hello ASP.NET web service.</span></span>

1. <span data-ttu-id="dd1f5-181">W projekcie platformy ASP.NET, należy dodać odwołanie do biblioteki klas toohello zawierający hello `ICounter` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-181">In your ASP.NET project, add a reference toohello class library that contains hello `ICounter` interface.</span></span>

2. <span data-ttu-id="dd1f5-182">Wcześniej dodane hello **Microsoft.ServiceFabric.Services.Remoting** projektu ASP.NET toohello pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-182">Earlier you added hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello ASP.NET project.</span></span> <span data-ttu-id="dd1f5-183">Ten pakiet zawiera hello `ServiceProxy` klasy, które zostaną użyte usługi stanowej toohello wywołuje toomake RPC.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-183">This package provides hello `ServiceProxy` class which you use toomake RPC calls toohello stateful service.</span></span> <span data-ttu-id="dd1f5-184">Upewnij się, że ten pakiet NuGet jest zainstalowane na powitania projekt usługi sieci web platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-184">Ensure this NuGet package is installed in hello ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="dd1f5-185">W hello **kontrolerów** folder, otwórz hello `ValuesController` klasy.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-185">In hello **Controllers** folder, open hello `ValuesController` class.</span></span> <span data-ttu-id="dd1f5-186">Należy pamiętać, że hello `Get` metoda obecnie tylko zwraca tablicę ustalony ciąg "wartość1" i "wartość2"--odpowiadającego widzieliśmy wcześniej w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-186">Note that hello `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in hello browser.</span></span> <span data-ttu-id="dd1f5-187">Zastąp tę implementację hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="dd1f5-187">Replace this implementation with hello following code:</span></span>
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    <span data-ttu-id="dd1f5-188">pierwszy wiersz kodu Hello jest hello klucz.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-188">hello first line of code is hello key one.</span></span> <span data-ttu-id="dd1f5-189">toocreate hello ICounter proxy toohello usługi stanowej, należy tooprovide dwa rodzaje informacji: Nazwa partycji identyfikator i hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-189">toocreate hello ICounter proxy toohello stateful service, you need tooprovide two pieces of information: a partition ID and hello name of hello service.</span></span>
   
    <span data-ttu-id="dd1f5-190">Można użyć partycjonowania usługi stanowej tooscale przez podzielenie ich stan w różnych zasobników, oparte na kluczu zdefiniowana, takich jak identyfikator klienta lub kod pocztowy.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-190">You can use partitioning tooscale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="dd1f5-191">W naszym prostej aplikacji hello usługi stanowej ma tylko jedną partycję, tak hello klucza nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-191">In our trivial application, hello stateful service only has one partition, so hello key doesn't matter.</span></span> <span data-ttu-id="dd1f5-192">Dowolny klawisz, który podasz doprowadzi toohello tej samej partycji.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-192">Any key that you provide will lead toohello same partition.</span></span> <span data-ttu-id="dd1f5-193">toolearn więcej informacji na temat partycjonowania usług, zobacz [jak toopartition niezawodne usługi sieć szkieletowa usług](service-fabric-concepts-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="dd1f5-193">toolearn more about partitioning services, see [How toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="dd1f5-194">Nazwa usługi Hello jest identyfikatorem URI hello formularza w sieci szkieletowej: /&lt;nazwa_aplikacji&gt;/&lt;service_name&gt;.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-194">hello service name is a URI of hello form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="dd1f5-195">Z tych dwóch rodzajów informacji usługi sieć szkieletowa może jednoznacznie zidentyfikować maszyny hello, które powinny być wysyłane żądania.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-195">With these two pieces of information, Service Fabric can uniquely identify hello machine that requests should be sent to.</span></span> <span data-ttu-id="dd1f5-196">Witaj `ServiceProxy` klasa również bezproblemowo obsługuje hello na wtedy, gdy wystąpi awaria maszyny hello, który jest hostem partycji usługi stanowej hello i inną maszynę musi być awansowana tootake jego miejscu.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-196">hello `ServiceProxy` class also seamlessly handles hello case where hello machine that hosts hello stateful service partition fails and another machine must be promoted tootake its place.</span></span> <span data-ttu-id="dd1f5-197">Ta warstwa abstrakcji udostępnia pisania hello toodeal kod klienta z innymi usługami znacznie prostsze.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-197">This abstraction makes writing hello client code toodeal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="dd1f5-198">Po mamy powitania serwera proxy, po prostu Wywołaj firma Microsoft hello `GetCountAsync` metodę i zwraca jego wynik.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-198">Once we have hello proxy, we simply invoke hello `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="dd1f5-199">Naciśnij klawisz F5, ponownie toorun hello zmodyfikował aplikację.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-199">Press F5 again toorun hello modified application.</span></span> <span data-ttu-id="dd1f5-200">Jako przed, Visual Studio automatycznie uruchamia hello przeglądarki toohello katalog główny projektu sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-200">As before, Visual Studio automatically launches hello browser toohello root of hello web project.</span></span> <span data-ttu-id="dd1f5-201">Dodaj ścieżkę "interfejsu api/values" hello, a powinien zostać wyświetlony hello zwrócił bieżącą wartość licznika.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-201">Add hello "api/values" path, and you should see hello current counter value returned.</span></span>
   
    ![wartość licznika stanowe Hello wyświetlany w przeglądarce hello][browser-aspnet-counter-value]
   
    <span data-ttu-id="dd1f5-203">Odśwież przeglądarkę hello okresowo toosee hello licznika wartość aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-203">Refresh hello browser periodically toosee hello counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="dd1f5-204">Kestrel i WebListener</span><span class="sxs-lookup"><span data-stu-id="dd1f5-204">Kestrel and WebListener</span></span>

<span data-ttu-id="dd1f5-205">Witaj domyślnego serwera sieci web platformy ASP.NET Core, znany jako Kestrel, jest [nie są obecnie obsługiwane za obsługę ruchu internetowego bezpośredniego](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="dd1f5-205">hello default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="dd1f5-206">W związku z tym hello szablonu usługi bezstanowej platformy ASP.NET Core dla sieci szkieletowej usług używa [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) domyślnie.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-206">As a result, hello ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="dd1f5-207">toolearn więcej informacji na temat Kestrel i WebListener w usługach sieci szkieletowej usług można znaleźć zbyt[platformy ASP.NET Core w usługach niezawodnej usługi sieć szkieletowa](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="dd1f5-207">toolearn more about Kestrel and WebListener in Service Fabric services, please refer too[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-tooa-reliable-actor-service"></a><span data-ttu-id="dd1f5-208">Łączenie usługi niezawodnego aktora tooa</span><span class="sxs-lookup"><span data-stu-id="dd1f5-208">Connecting tooa Reliable Actor service</span></span>
<span data-ttu-id="dd1f5-209">Ten samouczek koncentruje się na dodanie frontonu sieci web, które komunikowały się z usługi stanowej.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="dd1f5-210">Można jednak wykonać bardzo podobne tooactors tootalk modelu.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-210">However, you can follow a very similar model tootalk tooactors.</span></span> <span data-ttu-id="dd1f5-211">Podczas tworzenia projektu niezawodnego aktora Visual Studio automatycznie generuje projektu interfejsu.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="dd1f5-212">Można tego interfejsu toogenerate proxy aktora w toocommunicate projektu sieci web hello z aktorem hello.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-212">You can use that interface toogenerate an actor proxy in hello web project toocommunicate with hello actor.</span></span> <span data-ttu-id="dd1f5-213">kanał komunikacyjny Hello jest dostarczany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-213">hello communication channel is provided automatically.</span></span> <span data-ttu-id="dd1f5-214">Więc nie trzeba toodo wszystko to odpowiednik tooestablishing `ServiceRemotingListener` jak dla usługi stanowej hello w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-214">So you do not need toodo anything that is equivalent tooestablishing a `ServiceRemotingListener` like you did for hello stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="dd1f5-215">Jak działają usługi sieci web w klastrze lokalnym</span><span class="sxs-lookup"><span data-stu-id="dd1f5-215">How web services work on your local cluster</span></span>
<span data-ttu-id="dd1f5-216">Ogólnie rzecz biorąc można wdrożyć dokładnie hello tej samej sieci szkieletowej usług aplikacji tooa wielu maszyny klastra, że można wdrożyć w klastrze lokalnym i można zdecydowanie pewność, że działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-216">In general, you can deploy exactly hello same Service Fabric application tooa multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="dd1f5-217">Jest to spowodowane klaster lokalny jest po prostu konfigurację pięcioma węzłami, w której jest zwinięty tooa jednego komputera.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-217">This is because your local cluster is simply a five-node configuration that is collapsed tooa single machine.</span></span>

<span data-ttu-id="dd1f5-218">Po przejściu do usługi tooweb, istnieje jednak jeden nuance klucza.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-218">When it comes tooweb services, however, there is one key nuance.</span></span> <span data-ttu-id="dd1f5-219">Gdy klaster znajduje się za usługą równoważenia obciążenia, jak ma na platformie Azure, musi zapewnić, że usługi sieci web są wdrażane na każdym komputerze od modułu równoważenia obciążenia powitania po prostu okrężne ruchu między maszynami hello.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since hello load balancer simply round-robins traffic across hello machines.</span></span> <span data-ttu-id="dd1f5-220">Można to zrobić przez ustawienie hello `InstanceCount` hello usługi toohello specjalne wartości "-1".</span><span class="sxs-lookup"><span data-stu-id="dd1f5-220">You can do this by setting hello `InstanceCount` for hello service toohello special value of "-1".</span></span>

<span data-ttu-id="dd1f5-221">Z kolei po uruchomieniu usługi sieci web lokalnie, należy tooensure tego tylko jedno wystąpienie usługi hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-221">By contrast, when you run a web service locally, you need tooensure that only one instance of hello service is running.</span></span> <span data-ttu-id="dd1f5-222">W przeciwnym razie wystąpiły konflikty z wielu procesów, które nasłuchują na powitania sama ścieżka i portu.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-222">Otherwise, you run into conflicts from multiple processes that are listening on hello same path and port.</span></span> <span data-ttu-id="dd1f5-223">W związku z tym liczba wystąpień usługi sieci web hello należy ustawić także wartość "1" dla wdrożenia lokalnego.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-223">As a result, hello web service instance count should be set too"1" for local deployments.</span></span>

<span data-ttu-id="dd1f5-224">toolearn tooconfigure różne wartości dla innego środowiska, zobacz temat [Zarządzanie parametry aplikacji dla wielu środowiskach](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="dd1f5-224">toolearn how tooconfigure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd1f5-225">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dd1f5-225">Next steps</span></span>
<span data-ttu-id="dd1f5-226">Teraz, gdy masz z przodu web przechodzili zestaw aplikacji z platformy ASP.NET Core, Dowiedz się więcej o [platformy ASP.NET Core w usługach niezawodnej usługi sieć szkieletowa](service-fabric-reliable-services-communication-aspnetcore.md) dla dobrej znajomości sposobu platformy ASP.NET Core współpracuje z sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="dd1f5-227">Następnie [Dowiedz się więcej o komunikacji z usługami](service-fabric-connect-and-communicate-with-services.md) ogólnie tooget a pełny obraz z jak usługi komunikacji działa w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="dd1f5-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general tooget a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="dd1f5-228">Po utworzeniu dobrą znajomością działania komunikacji usług [utworzyć klaster na platformie Azure i wdrażanie aplikacji chmury toohello](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dd1f5-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application toohello cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
