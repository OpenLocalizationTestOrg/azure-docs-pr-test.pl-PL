---
title: Komunikacja aaaService z hello interfejsu API sieci Web programu ASP.NET | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak krok po kroku przy użyciu komunikacji usługi tooimplement hello interfejsu API sieci Web platformy ASP.NET z OWIN hostingu samodzielnego w hello niezawodnej usługi interfejsu API."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="9a172-103">Wprowadzenie: usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN</span><span class="sxs-lookup"><span data-stu-id="9a172-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="9a172-104">Sieć szkieletowa usług Azure umieszcza hello zasilania w dłoni podczas wybierania jest sposób toocommunicate Twojego usług z użytkownikami i ze sobą.</span><span class="sxs-lookup"><span data-stu-id="9a172-104">Azure Service Fabric puts hello power in your hands when you're deciding how you want your services toocommunicate with users and with each other.</span></span> <span data-ttu-id="9a172-105">Ten samouczek koncentruje się na implementacji komunikacji usług za pomocą interfejsu API sieci Web platformy ASP.NET z interfejsu Open Web dla interfejsu API usługi Service Fabric niezawodnej usługi hostingu samodzielnego .NET (OWIN).</span><span class="sxs-lookup"><span data-stu-id="9a172-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="9a172-106">Firma Microsoft będzie poznaj dok³adniejsze opisy wybranych głęboko do hello podłączany komunikacji niezawodnej usługi interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9a172-106">We'll delve deeply into hello Reliable Services pluggable communication API.</span></span> <span data-ttu-id="9a172-107">Użyjemy interfejsu API sieci Web w tooshow krok po kroku przykładu możesz jak tooset się odbiornik komunikacji niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="9a172-107">We'll also use Web API in a step-by-step example tooshow you how tooset up a custom communication listener.</span></span>

## <a name="introduction-tooweb-api-in-service-fabric"></a><span data-ttu-id="9a172-108">Wprowadzenie tooWeb interfejsu API w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="9a172-108">Introduction tooWeb API in Service Fabric</span></span>
<span data-ttu-id="9a172-109">Interfejs API sieci Web platformy ASP.NET to platforma popularnych i wydajne do tworzenia interfejsów API HTTP na powitania .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9a172-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of hello .NET Framework.</span></span> <span data-ttu-id="9a172-110">Jeśli nie masz już znasz hello framework, zobacz [wprowadzenie do korzystania z programu ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn więcej.</span><span class="sxs-lookup"><span data-stu-id="9a172-110">If you're not already familiar with hello framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn more.</span></span>

<span data-ttu-id="9a172-111">Interfejs API sieci Web w sieci szkieletowej usług jest hello tej samej sieci Web interfejsu API platformy ASP.NET znają i lubią.</span><span class="sxs-lookup"><span data-stu-id="9a172-111">Web API in Service Fabric is hello same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="9a172-112">Witaj różnicą jest sposób możesz *hosta* aplikacji interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9a172-112">hello difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="9a172-113">Microsoft Internet Information Services (IIS) nie będzie używany.</span><span class="sxs-lookup"><span data-stu-id="9a172-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="9a172-114">toobetter zrozumieć różnicę hello, możemy podzielić je na dwie części:</span><span class="sxs-lookup"><span data-stu-id="9a172-114">toobetter understand hello difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="9a172-115">Witaj aplikacji interfejsu API sieci Web (w tym kontrolerów i modeli)</span><span class="sxs-lookup"><span data-stu-id="9a172-115">hello Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="9a172-116">Witaj hosta (powitania serwera sieci web, zazwyczaj usług IIS)</span><span class="sxs-lookup"><span data-stu-id="9a172-116">hello host (hello web server, usually IIS)</span></span>

<span data-ttu-id="9a172-117">Nie zmienia samej aplikacji interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9a172-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="9a172-118">Go nie różni się od aplikacji interfejsu API sieci Web, które zostały zapisane w przeszłości hello i Przenieś stanie toosimply powinien być w większości kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9a172-118">It's no different from Web API applications you may have written in hello past, and you should be able toosimply move over most of your application code.</span></span> <span data-ttu-id="9a172-119">Ale jeśli już zostało hosting w usługach IIS, w których host aplikacji hello może być nieco inne niż czego umożliwia.</span><span class="sxs-lookup"><span data-stu-id="9a172-119">But if you've been hosting on IIS, where you host hello application may be a little different from what you're used to.</span></span> <span data-ttu-id="9a172-120">Przed uzyskujemy toohello hosting części Zacznijmy coś więcej dobrze znany: hello aplikacji interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9a172-120">Before we get toohello hosting part, let's start with something more familiar: hello Web API application.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="9a172-121">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="9a172-121">Create hello application</span></span>
<span data-ttu-id="9a172-122">Rozpocznij od utworzenia nowej aplikacji platformy Service Fabric przy użyciu jednej usługi bezstanowej w programie Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9a172-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="9a172-123">Szablon programu Visual Studio dla usługi bezstanowej przy użyciu interfejsu API sieci Web jest dostępna tooyou.</span><span class="sxs-lookup"><span data-stu-id="9a172-123">A Visual Studio template for a stateless service using Web API is available tooyou.</span></span> <span data-ttu-id="9a172-124">W tym samouczku firma Microsoft będzie zbudować projekt interfejsu API sieci Web od podstaw, którego wynikiem co otrzyma, w przypadku wybrania tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="9a172-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="9a172-125">Wybierz puste toolearn projektu usługi bezstanowej jak toobuild projekt interfejsu API sieci Web od podstaw, lub można rozpoczynać się od usługi bezstanowej hello szablonu interfejsu API sieci Web i po prostu odbiorze.</span><span class="sxs-lookup"><span data-stu-id="9a172-125">Select a blank Stateless Service project toolearn how toobuild a Web API project from scratch, or you can start with hello stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="9a172-126">pierwszym krokiem Hello jest toopull w niektórych pakietów NuGet dla interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9a172-126">hello first step is toopull in some NuGet packages for Web API.</span></span> <span data-ttu-id="9a172-127">chcemy toouse pakietów Hello jest Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="9a172-127">hello package we want toouse is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="9a172-128">Ten pakiet zawiera wszystkie hello wymaganych pakietów interfejsu API sieci Web i hello *hosta* pakietów.</span><span class="sxs-lookup"><span data-stu-id="9a172-128">This package includes all hello necessary Web API packages and hello *host* packages.</span></span> <span data-ttu-id="9a172-129">Jest to ważne później.</span><span class="sxs-lookup"><span data-stu-id="9a172-129">This will be important later.</span></span>

<span data-ttu-id="9a172-130">Po zainstalowaniu pakietów hello można rozpocząć zbudowaniu hello podstawowej struktury projektu interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9a172-130">After hello packages have been installed, you can begin building out hello basic Web API project structure.</span></span> <span data-ttu-id="9a172-131">Jeśli używano interfejsu API sieci Web, hello struktury projektu powinna wyglądać bardzo znajomo.</span><span class="sxs-lookup"><span data-stu-id="9a172-131">If you've used Web API, hello project structure should look very familiar.</span></span> <span data-ttu-id="9a172-132">Rozpocznij od dodania `Controllers` katalogu i kontrolera proste wartości:</span><span class="sxs-lookup"><span data-stu-id="9a172-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="9a172-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="9a172-133">**ValuesController.cs**</span></span>

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

<span data-ttu-id="9a172-134">Następnie Dodaj klasę uruchamiania routingu hello projektu głównego tooregister hello, elementy formatujące i inne ustawienia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9a172-134">Next, add a Startup class at hello project root tooregister hello routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="9a172-135">Dotyczy to również gdzie interfejsu API sieci Web podłącza toohello *hosta*, który będzie można uruchomić ponownie później.</span><span class="sxs-lookup"><span data-stu-id="9a172-135">This is also where Web API plugs in toohello *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="9a172-136">**Startup.CS**</span><span class="sxs-lookup"><span data-stu-id="9a172-136">**Startup.cs**</span></span>

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

<span data-ttu-id="9a172-137">To wszystko dla części aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9a172-137">That's it for hello application part.</span></span> <span data-ttu-id="9a172-138">W tym momencie skonfigurowaliśmy tylko hello podstawowy interfejs API sieci Web projektu układ.</span><span class="sxs-lookup"><span data-stu-id="9a172-138">At this point, we've set up just hello basic Web API project layout.</span></span> <span data-ttu-id="9a172-139">Do tej pory nie powinien wyglądać wiele różnych z projektów interfejsu API sieci Web, które zostały zapisane w przeszłości hello lub hello podstawowy szablon interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9a172-139">So far, it shouldn't look much different from Web API projects you may have written in hello past or from hello basic Web API template.</span></span> <span data-ttu-id="9a172-140">Logiki biznesowej przechodzi w kontrolerach hello i modeli w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="9a172-140">Your business logic goes in hello controllers and models as usual.</span></span>

<span data-ttu-id="9a172-141">Teraz możemy czego o hostingu, aby firma Microsoft może faktycznie uruchomić?</span><span class="sxs-lookup"><span data-stu-id="9a172-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="9a172-142">Usługa hostingu</span><span class="sxs-lookup"><span data-stu-id="9a172-142">Service hosting</span></span>
<span data-ttu-id="9a172-143">W sieci szkieletowej usług, usługa jest uruchomiona *procesu hosta usługi*, plik wykonywalny, który uruchamia kodu usługi.</span><span class="sxs-lookup"><span data-stu-id="9a172-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="9a172-144">Podczas pisania usługi za pomocą hello niezawodnej usługi interfejsu API projekt usługi właśnie kompiluje tooan plik wykonywalny, który rejestruje danego typu usługi i uruchamia kod.</span><span class="sxs-lookup"><span data-stu-id="9a172-144">When you write a service by using hello Reliable Services API, your service project just compiles tooan executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="9a172-145">Dotyczy to w większości przypadków podczas pisania usługi w sieci szkieletowej usług w programie .NET.</span><span class="sxs-lookup"><span data-stu-id="9a172-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="9a172-146">Po otwarciu pliku Program.cs w projekcie usługi bezstanowej hello powinien zostać wyświetlony:</span><span class="sxs-lookup"><span data-stu-id="9a172-146">When you open Program.cs in hello stateless service project, you should see:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="9a172-147">Jeśli to wygląda podejrzanie aplikacji konsoli tooa punktu wejścia hello, który jest ponieważ jest on.</span><span class="sxs-lookup"><span data-stu-id="9a172-147">If that looks suspiciously like hello entry point tooa console application, that's because it is.</span></span>

<span data-ttu-id="9a172-148">Szczegółowe informacje na temat hello procesu hosta usługi i usługi rejestracji wykraczają poza zakres tego artykułu hello.</span><span class="sxs-lookup"><span data-stu-id="9a172-148">Further details about hello service host process and service registration are beyond hello scope of this article.</span></span> <span data-ttu-id="9a172-149">Jednak jest ważne tooknow dla teraz, gdy *kodu usługi działa we własnym procesie*.</span><span class="sxs-lookup"><span data-stu-id="9a172-149">But it's important tooknow for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="9a172-150">Host samodzielny interfejsu API sieci Web z hostem OWIN</span><span class="sxs-lookup"><span data-stu-id="9a172-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="9a172-151">Biorąc pod uwagę, że kod aplikacji interfejsu API sieci Web znajduje się w swoim własnym procesie, jak możesz Podłączanie go tooa serwera sieci web?</span><span class="sxs-lookup"><span data-stu-id="9a172-151">Given that your Web API application code is hosted in its own process, how do you hook it up tooa web server?</span></span> <span data-ttu-id="9a172-152">Wprowadź [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="9a172-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="9a172-153">OWIN jest po prostu Umowa między serwerami sieci web i aplikacji sieci web platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="9a172-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="9a172-154">Tradycyjnie użycie programu ASP.NET (w górę tooMVC 5), aplikacji sieci web hello jest silnie sprzężonego tooIIS za pośrednictwem System.Web.</span><span class="sxs-lookup"><span data-stu-id="9a172-154">Traditionally when ASP.NET (up tooMVC 5) is used, hello web application is tightly coupled tooIIS through System.Web.</span></span> <span data-ttu-id="9a172-155">Jednak interfejsu API sieci Web implementuje OWIN, więc pisania aplikacji sieci web, która jest całkowicie niezależna od hello serwera sieci web, który go obsługuje.</span><span class="sxs-lookup"><span data-stu-id="9a172-155">However, Web API implements OWIN, so you can write a web application that is decoupled from hello web server that hosts it.</span></span> <span data-ttu-id="9a172-156">W związku z tym można użyć *hosta samodzielnego* OWIN serwera sieci web można uruchomić w własnego procesu.</span><span class="sxs-lookup"><span data-stu-id="9a172-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="9a172-157">To jest dopasowany hello sieci szkieletowej usług hostingu model firma opisana.</span><span class="sxs-lookup"><span data-stu-id="9a172-157">This fits perfectly with hello Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="9a172-158">W tym artykule użyjemy Katana jako hello OWIN hosta dla hello aplikacji interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9a172-158">In this article, we'll use Katana as hello OWIN host for hello Web API application.</span></span> <span data-ttu-id="9a172-159">Katana jest implementacją hosta OWIN open source oparty na [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) i hello Windows [interfejsu API serwera HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span><span class="sxs-lookup"><span data-stu-id="9a172-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="9a172-160">więcej informacji na temat Katana, przejdź toohello toolearn [lokacji Katana](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="9a172-160">toolearn more about Katana, go toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="9a172-161">Aby uzyskać szybki przegląd jak toouse Katana tooself hosta sieci Web interfejsu API, zobacz [OWIN Użyj hosta tooSelf ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span><span class="sxs-lookup"><span data-stu-id="9a172-161">For a quick overview of how toouse Katana tooself-host Web API, see [Use OWIN tooSelf-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-hello-web-server"></a><span data-ttu-id="9a172-162">Konfigurowanie serwera sieci web hello</span><span class="sxs-lookup"><span data-stu-id="9a172-162">Set up hello web server</span></span>
<span data-ttu-id="9a172-163">Hello niezawodnej usługi interfejsu API zapewnia punkt wejścia komunikacji, gdzie można podłączyć stosach komunikacji, które umożliwiają użytkownikom i klientów tooconnect toohello usługi:</span><span class="sxs-lookup"><span data-stu-id="9a172-163">hello Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients tooconnect toohello service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="9a172-164">powitania serwera sieci web (i innych stosu komunikacji używanych w przyszłych, takie jak protokół WebSockets hello) należy używać hello ICommunicationListener interfejsu toointegrate poprawnie hello systemu.</span><span class="sxs-lookup"><span data-stu-id="9a172-164">hello web server (and any other communication stack you use in hello future, such as WebSockets) should use hello ICommunicationListener interface toointegrate correctly with hello system.</span></span> <span data-ttu-id="9a172-165">Witaj przyczyn tej staną się bardziej widoczne w hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="9a172-165">hello reasons for this will become more apparent in hello following steps.</span></span>

<span data-ttu-id="9a172-166">Najpierw Utwórz klasę o nazwie OwinCommunicationListener, który implementuje ICommunicationListener:</span><span class="sxs-lookup"><span data-stu-id="9a172-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="9a172-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="9a172-167">**OwinCommunicationListener.cs**</span></span>

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

<span data-ttu-id="9a172-168">Interfejs ICommunicationListener Hello udostępnia trzy metody toomanage odbiornik komunikacji usługi:</span><span class="sxs-lookup"><span data-stu-id="9a172-168">hello ICommunicationListener interface provides three methods toomanage a communication listener for your service:</span></span>

* <span data-ttu-id="9a172-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="9a172-169">*OpenAsync*.</span></span> <span data-ttu-id="9a172-170">Rozpocznij nasłuchiwanie żądań.</span><span class="sxs-lookup"><span data-stu-id="9a172-170">Start listening for requests.</span></span>
* <span data-ttu-id="9a172-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="9a172-171">*CloseAsync*.</span></span> <span data-ttu-id="9a172-172">Zatrzymaj nasłuchiwanie żądań, Zakończ wszystkie żądania locie i bezpiecznie zamknąć.</span><span class="sxs-lookup"><span data-stu-id="9a172-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="9a172-173">*Przerwij*.</span><span class="sxs-lookup"><span data-stu-id="9a172-173">*Abort*.</span></span> <span data-ttu-id="9a172-174">Anulować wszystkie i zatrzymać natychmiast.</span><span class="sxs-lookup"><span data-stu-id="9a172-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="9a172-175">tooget pracę, dodawanie członków prywatnych klasy, do odbiornika hello rzeczy, należy toofunction.</span><span class="sxs-lookup"><span data-stu-id="9a172-175">tooget started, add private class members for things hello listener will need toofunction.</span></span> <span data-ttu-id="9a172-176">Te zostanie zainicjowany przez Konstruktor hello i będzie używana później podczas konfigurowania hello nasłuchiwania adresu URL.</span><span class="sxs-lookup"><span data-stu-id="9a172-176">These will be initialized through hello constructor and used later when you set up hello listening URL.</span></span>

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a><span data-ttu-id="9a172-177">Implementowanie OpenAsync</span><span class="sxs-lookup"><span data-stu-id="9a172-177">Implement OpenAsync</span></span>
<span data-ttu-id="9a172-178">tooset powitania serwera sieci web, potrzebne informacje:</span><span class="sxs-lookup"><span data-stu-id="9a172-178">tooset up hello web server, you need two pieces of information:</span></span>

* <span data-ttu-id="9a172-179">*Prefiks adresu URL ścieżki*.</span><span class="sxs-lookup"><span data-stu-id="9a172-179">*A URL path prefix*.</span></span> <span data-ttu-id="9a172-180">Mimo że jest to opcjonalne, jest dobra dla tooset możesz tego teraz up, dzięki czemu można bezpiecznie obsługiwać wiele usług sieci web w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9a172-180">Although this is optional, it's good for you tooset this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="9a172-181">*Port*.</span><span class="sxs-lookup"><span data-stu-id="9a172-181">*A port*.</span></span>

<span data-ttu-id="9a172-182">Przed uzyskanie portu dla serwera sieci web hello jest ważne, że rozumiesz, że Usługa Service Fabric realizuje warstwa aplikacji, która pełni rolę bufora między aplikacji i hello podstawowego systemu operacyjnego, który jest uruchamiany na.</span><span class="sxs-lookup"><span data-stu-id="9a172-182">Before you get a port for hello web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and hello underlying operating system that it runs on.</span></span> <span data-ttu-id="9a172-183">W efekcie Usługa Service Fabric realizuje tooconfigure sposób *punkty końcowe* dla usług.</span><span class="sxs-lookup"><span data-stu-id="9a172-183">As such, Service Fabric provides a way tooconfigure *endpoints* for your services.</span></span> <span data-ttu-id="9a172-184">Sieci szkieletowej usług gwarantuje, że punkty końcowe są dostępne dla Twojej toouse usługi.</span><span class="sxs-lookup"><span data-stu-id="9a172-184">Service Fabric ensures that endpoints are available for your service toouse.</span></span> <span data-ttu-id="9a172-185">Dzięki temu masz tooconfigure je samodzielnie w hello podstawowego środowiska systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="9a172-185">This way, you don't have tooconfigure them yourself in hello underlying OS environment.</span></span> <span data-ttu-id="9a172-186">Można łatwo hostowania aplikacji usługi Service Fabric w różnych środowiskach bez konieczności toomake aplikacji tooyour żadnych zmian.</span><span class="sxs-lookup"><span data-stu-id="9a172-186">You can easily host your Service Fabric application in different environments without having toomake any changes tooyour application.</span></span> <span data-ttu-id="9a172-187">(Na przykład można obsługiwać hello tej samej aplikacji na platformie Azure lub we własnym centrum danych.)</span><span class="sxs-lookup"><span data-stu-id="9a172-187">(For example, you can host hello same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="9a172-188">Skonfiguruj punkt końcowy HTTP w PackageRoot\ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="9a172-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="9a172-189">Ten krok jest ważne, ponieważ proces hosta usługi hello jest uruchamiany w ograniczonym poświadczeń (Usługa sieciowa w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="9a172-189">This step is important because hello service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="9a172-190">Oznacza to, z usługą nie będziesz mieć dostępu tooset się punkt końcowy HTTP samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="9a172-190">This means that your service won't have access tooset up an HTTP endpoint on its own.</span></span> <span data-ttu-id="9a172-191">Przy użyciu konfiguracji punktu końcowego hello, usługi Service Fabric wie tooset się hello odpowiednią listę kontroli dostępu (ACL) dla adresu URL, który hello usługi będzie nasłuchiwać powitalne.</span><span class="sxs-lookup"><span data-stu-id="9a172-191">By using hello endpoint configuration, Service Fabric knows tooset up hello proper access control list (ACL) for hello URL that hello service will listen on.</span></span> <span data-ttu-id="9a172-192">Sieć szkieletowa usług również miejsce na standardowej tooconfigure punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="9a172-192">Service Fabric also provides a standard place tooconfigure endpoints.</span></span>

<span data-ttu-id="9a172-193">W OwinCommunicationListener.cs można uruchomić implementacji OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="9a172-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="9a172-194">Jest to, gdzie uruchomić powitania serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="9a172-194">This is where you start hello web server.</span></span> <span data-ttu-id="9a172-195">Najpierw Pobierz informacje o punkcie końcowym hello i Utwórz hello adres URL, który będzie nasłuchiwać hello usługi.</span><span class="sxs-lookup"><span data-stu-id="9a172-195">First, get hello endpoint information and create hello URL that hello service will listen on.</span></span> <span data-ttu-id="9a172-196">adres URL Hello może się różnić w zależności od tego, czy odbiornik hello jest używany w usługi bezstanowej lub usługi stanowej.</span><span class="sxs-lookup"><span data-stu-id="9a172-196">hello URL will be different depending on whether hello listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="9a172-197">Dla usługi stanowej hello odbiornika musi toocreate unikatowy adres dla każdej repliki usługi stanowej go wykrywa w.</span><span class="sxs-lookup"><span data-stu-id="9a172-197">For a stateful service, hello listener needs toocreate a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="9a172-198">W przypadku usług bezstanowych adresów hello może być znacznie prostsze.</span><span class="sxs-lookup"><span data-stu-id="9a172-198">For stateless services, hello address can be much simpler.</span></span> 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

<span data-ttu-id="9a172-199">Należy pamiętać, że "http://+" jest używana w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="9a172-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="9a172-200">Jest to toomake się, że tego serwera sieci web hello nasłuchuje na wszystkich dostępnych adresów, w tym localhost, nazwy FQDN i hello IP komputera.</span><span class="sxs-lookup"><span data-stu-id="9a172-200">This is toomake sure that hello web server is listening on all available addresses, including localhost, FQDN, and hello machine IP.</span></span>

<span data-ttu-id="9a172-201">Witaj OpenAsync implementacja jest najważniejsze przyczyny hello, dlaczego powitania serwera sieci web (lub dowolnego stosu komunikacji) została wdrożona jako ICommunicationListener, a nie tylko go otworzyć go bezpośrednio z `RunAsync()` hello usługi.</span><span class="sxs-lookup"><span data-stu-id="9a172-201">hello OpenAsync implementation is one of hello most important reasons why hello web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in hello service.</span></span> <span data-ttu-id="9a172-202">Witaj wartość zwrotną z elementu OpenAsync jest nasłuchuje adres hello hello serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="9a172-202">hello return value from OpenAsync is hello address that hello web server is listening on.</span></span> <span data-ttu-id="9a172-203">Gdy ten adres jest zwracany toohello systemu, rejestruje hello adresu z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="9a172-203">When this address is returned toohello system, it registers hello address with hello service.</span></span> <span data-ttu-id="9a172-204">Usługa sieci szkieletowej udostępnia interfejs API umożliwiający klientów i innych usług toothen poprosić dla tego adresu według nazwy usługi.</span><span class="sxs-lookup"><span data-stu-id="9a172-204">Service Fabric provides an API that allows clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="9a172-205">Jest to ważne, ponieważ adres usługi hello nie jest statyczne.</span><span class="sxs-lookup"><span data-stu-id="9a172-205">This is important because hello service address is not static.</span></span> <span data-ttu-id="9a172-206">Usługi są przenoszone w klastrze hello do celów dostępności i równoważenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="9a172-206">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="9a172-207">Jest to mechanizm hello, który umożliwia klientom Witaj tooresolve nasłuchiwania adresów dla usługi.</span><span class="sxs-lookup"><span data-stu-id="9a172-207">This is hello mechanism that allows clients tooresolve hello listening address for a service.</span></span>

<span data-ttu-id="9a172-208">Ten fakt OpenAsync uruchamia serwer sieci web hello i zwraca hello adres, który jest nasłuchiwanie.</span><span class="sxs-lookup"><span data-stu-id="9a172-208">With that in mind, OpenAsync starts hello web server and returns hello address that it's listening on.</span></span> <span data-ttu-id="9a172-209">Należy pamiętać, że nasłuchuje "http://+", ale przed OpenAsync zwraca adres hello, Witaj "+" jest zastępowany hello adres IP lub nazwa FQDN węzła hello, który jest obecnie na.</span><span class="sxs-lookup"><span data-stu-id="9a172-209">Note that it listens on "http://+", but before OpenAsync returns hello address, hello "+" is replaced with hello IP or FQDN of hello node it is currently on.</span></span> <span data-ttu-id="9a172-210">Hello adres, który jest zwracany przez tę metodę jest, co jest zarejestrowany w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="9a172-210">hello address that is returned by this method is what's registered with hello system.</span></span> <span data-ttu-id="9a172-211">Istnieje również jakie klientów i innych usług, wyświetlać, gdy został poproszony o adresu usługi.</span><span class="sxs-lookup"><span data-stu-id="9a172-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="9a172-212">Dla klientów toocorrectly połączenia tooit, potrzebują rzeczywisty adres IP lub nazwę FQDN adresu hello.</span><span class="sxs-lookup"><span data-stu-id="9a172-212">For clients toocorrectly connect tooit, they need an actual IP or FQDN in hello address.</span></span>

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="9a172-213">Należy pamiętać, że to odwołuje się do klasy uruchamiania hello, która została przekazana toohello OwinCommunicationListener w Konstruktorze hello.</span><span class="sxs-lookup"><span data-stu-id="9a172-213">Note that this references hello Startup class that was passed in toohello OwinCommunicationListener in hello constructor.</span></span> <span data-ttu-id="9a172-214">To wystąpienie uruchamiania jest używany przez hello powitania toobootstrap serwera sieci web aplikacji interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9a172-214">This startup instance is used by hello web server toobootstrap hello Web API application.</span></span>

<span data-ttu-id="9a172-215">Witaj `ServiceEventSource.Current.Message()` wiersza zostaną wyświetlone w oknie zdarzeń diagnostycznych hello później, po uruchomieniu tooconfirm aplikacji hello tego serwera sieci web hello została uruchomiona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="9a172-215">hello `ServiceEventSource.Current.Message()` line will appear in hello Diagnostic Events window later, when you run hello application tooconfirm that hello web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="9a172-216">Implementowanie CloseAsync i przerwania</span><span class="sxs-lookup"><span data-stu-id="9a172-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="9a172-217">Ponadto wdrożenie zarówno CloseAsync i Abort serwera sieci web hello toostop.</span><span class="sxs-lookup"><span data-stu-id="9a172-217">Finally, implement both CloseAsync and Abort toostop hello web server.</span></span> <span data-ttu-id="9a172-218">serwer sieci web Hello może zostać zatrzymana przez usuwanie hello dojścia serwera, który został utworzony podczas OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="9a172-218">hello web server can be stopped by disposing hello server handle that was created during OpenAsync.</span></span>

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

<span data-ttu-id="9a172-219">W tym przykładzie implementacji zarówno CloseAsync, jak i przerwania po prostu Zatrzymaj powitania serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="9a172-219">In this implementation example, both CloseAsync and Abort simply stop hello web server.</span></span> <span data-ttu-id="9a172-220">Można wybrać opcję tooperform bardziej bezpiecznie skoordynowany sposób wyłączania powitania serwera sieci web w CloseAsync.</span><span class="sxs-lookup"><span data-stu-id="9a172-220">You may opt tooperform a more gracefully coordinated shutdown of hello web server in CloseAsync.</span></span> <span data-ttu-id="9a172-221">Na przykład zamykania hello można poczekaj zakończona, zanim zwracać hello toobe locie żądań.</span><span class="sxs-lookup"><span data-stu-id="9a172-221">For example, hello shutdown could wait for in-flight requests toobe completed before hello return.</span></span>

## <a name="start-hello-web-server"></a><span data-ttu-id="9a172-222">Uruchamianie powitania serwera sieci web</span><span class="sxs-lookup"><span data-stu-id="9a172-222">Start hello web server</span></span>
<span data-ttu-id="9a172-223">Jest teraz gotowy toocreate i zwrócić wystąpienia serwera sieci web hello toostart OwinCommunicationListener.</span><span class="sxs-lookup"><span data-stu-id="9a172-223">You're now ready toocreate and return an instance of OwinCommunicationListener toostart hello web server.</span></span> <span data-ttu-id="9a172-224">Po powrocie do hello klasy usługi (WebService.cs), należy zastąpić hello `CreateServiceInstanceListeners()` metody:</span><span class="sxs-lookup"><span data-stu-id="9a172-224">Back in hello Service class (WebService.cs), override hello `CreateServiceInstanceListeners()` method:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

<span data-ttu-id="9a172-225">Gdzie jest to hello interfejsu API sieci Web *aplikacji* i hello OWIN *hosta* spełnia finally.</span><span class="sxs-lookup"><span data-stu-id="9a172-225">This is where hello Web API *application* and hello OWIN *host* finally meet.</span></span> <span data-ttu-id="9a172-226">Witaj hosta (OwinCommunicationListener) znajduje się wystąpienie hello *aplikacji* (interfejs API sieci Web) za pośrednictwem hello klasy początkowej.</span><span class="sxs-lookup"><span data-stu-id="9a172-226">hello host (OwinCommunicationListener) is given an instance of hello *application* (Web API) via hello Startup class.</span></span> <span data-ttu-id="9a172-227">Usługa Service Fabric zarządza następnie cykl życia.</span><span class="sxs-lookup"><span data-stu-id="9a172-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="9a172-228">Tego samego wzorca zwykle można wykonać z dowolnego stosu komunikacji.</span><span class="sxs-lookup"><span data-stu-id="9a172-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="9a172-229">Zebranie wszystkich elementów</span><span class="sxs-lookup"><span data-stu-id="9a172-229">Put it all together</span></span>
<span data-ttu-id="9a172-230">W tym przykładzie, nie potrzebujesz toodo cokolwiek w hello `RunAsync()` metody, więc po prostu można usunąć tego zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="9a172-230">In this example, you don't need toodo anything in hello `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="9a172-231">implementacji usługi końcowego Hello powinny być bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="9a172-231">hello final service implementation should be very simple.</span></span> <span data-ttu-id="9a172-232">Wymaga tylko odbiornik komunikacji hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="9a172-232">It only needs toocreate hello communication listener:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

<span data-ttu-id="9a172-233">Witaj pełną `OwinCommunicationListener` klasy:</span><span class="sxs-lookup"><span data-stu-id="9a172-233">hello complete `OwinCommunicationListener` class:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

<span data-ttu-id="9a172-234">Teraz, gdy wszystkie elementy hello zostało umieszczone w miejscu, projektu powinna wyglądać Typowa aplikacja interfejsu API sieci Web z punktów wejścia niezawodnej usługi interfejsu API i OWIN hosta.</span><span class="sxs-lookup"><span data-stu-id="9a172-234">Now that you have put all hello pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="9a172-235">Uruchom i łączenie się za pośrednictwem przeglądarki sieci web</span><span class="sxs-lookup"><span data-stu-id="9a172-235">Run and connect through a web browser</span></span>
<span data-ttu-id="9a172-236">Jeśli nie zostało to jeszcze zrobione, [Konfigurowanie środowiska deweloperskiego](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9a172-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="9a172-237">Teraz możesz skompilować i wdrożyć usługę.</span><span class="sxs-lookup"><span data-stu-id="9a172-237">You can now build and deploy your service.</span></span> <span data-ttu-id="9a172-238">Naciśnij klawisz **F5** w toobuild programu Visual Studio i wdrażanie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9a172-238">Press **F5** in Visual Studio toobuild and deploy hello application.</span></span> <span data-ttu-id="9a172-239">W oknie zdarzeń diagnostycznych hello, powinien zostać wyświetlony komunikat wskazujący tego serwera sieci web hello otwarte na http://localhost:8281 /.</span><span class="sxs-lookup"><span data-stu-id="9a172-239">In hello Diagnostic Events window, you should see a message that indicates that hello web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="9a172-240">Jeśli hello port został już otwarty przez inny proces na komputerze, może zostać wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="9a172-240">If hello port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="9a172-241">Oznacza to, że nie można otworzyć tego odbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="9a172-241">This indicates that hello listener couldn't be opened.</span></span> <span data-ttu-id="9a172-242">Jeśli jest przypadek hello, spróbuj użyć innego portu dla konfiguracji punktu końcowego hello w pliku ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="9a172-242">If that's hello case, try using a different port for hello endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="9a172-243">Po uruchomieniu usługi hello, otwórz przeglądarkę i przejdź zbyt[http://localhost:8281/api/wartości](http://localhost:8281/api/values) tootest go.</span><span class="sxs-lookup"><span data-stu-id="9a172-243">Once hello service is running, open a browser and navigate too[http://localhost:8281/api/values](http://localhost:8281/api/values) tootest it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="9a172-244">Skalowanie go</span><span class="sxs-lookup"><span data-stu-id="9a172-244">Scale it out</span></span>
<span data-ttu-id="9a172-245">Skalowania aplikacji sieci web bezstanowych zwykle oznacza dodanie więcej maszyn i kręci się hello aplikacje sieci web na nich.</span><span class="sxs-lookup"><span data-stu-id="9a172-245">Scaling out stateless web apps typically means adding more machines and spinning up hello web apps on them.</span></span> <span data-ttu-id="9a172-246">Aparat aranżacji usługi sieć szkieletowa można to zrobić dla Ciebie zawsze, gdy tooa klastra zostaną dodane nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="9a172-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added tooa cluster.</span></span> <span data-ttu-id="9a172-247">Podczas tworzenia wystąpienia usługi bezstanowej, można określić numer hello wystąpień ma toocreate.</span><span class="sxs-lookup"><span data-stu-id="9a172-247">When you create instances of a stateless service, you can specify hello number of instances you want toocreate.</span></span> <span data-ttu-id="9a172-248">Sieć szkieletowa usług umieszcza tej liczby wystąpień na węzłach w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="9a172-248">Service Fabric places that number of instances on nodes in hello cluster.</span></span> <span data-ttu-id="9a172-249">I pozwala sprawdzić toocreate nie więcej niż jednego wystąpienia na dowolnego pojedynczego węzła.</span><span class="sxs-lookup"><span data-stu-id="9a172-249">And it makes sure not toocreate more than one instance on any one node.</span></span> <span data-ttu-id="9a172-250">Można także skonfigurować usługi sieć szkieletowa tooalways Utwórz wystąpienie w każdym węźle, określając **-1** hello wystąpienia licznika.</span><span class="sxs-lookup"><span data-stu-id="9a172-250">You can also instruct Service Fabric tooalways create an instance on every node by specifying **-1** for hello instance count.</span></span> <span data-ttu-id="9a172-251">Gwarantuje to, że po dodaniu tooscale węzłów poza klastrem, wystąpienie usługi bezstanowej zostanie utworzony na powitania nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="9a172-251">This guarantees that whenever you add nodes tooscale out your cluster, an instance of your stateless service will be created on hello new nodes.</span></span> <span data-ttu-id="9a172-252">Ta wartość jest właściwością wystąpienia usługi hello, więc jest ustawiana podczas tworzenia wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="9a172-252">This value is a property of hello service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="9a172-253">Można to zrobić za pomocą programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9a172-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="9a172-254">Ponadto można to zrobić, po zdefiniowaniu domyślnej usługi w projekcie usługi bezstanowej programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="9a172-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="9a172-255">Aby uzyskać więcej informacji na temat sposobu toocreate aplikacji i wystąpienie usługi, zobacz [wdrażania aplikacji](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="9a172-255">For more information on how toocreate application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a172-256">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9a172-256">Next steps</span></span>
[<span data-ttu-id="9a172-257">Debugowanie aplikacji sieci szkieletowej usług za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9a172-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

