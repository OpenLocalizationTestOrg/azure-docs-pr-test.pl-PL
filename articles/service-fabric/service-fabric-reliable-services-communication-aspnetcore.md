---
title: Komunikacja aaaService z hello platformy ASP.NET Core | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse platformy ASP.NET Core w bezstanowe i stanowe niezawodne usługi."
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
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="e8bf7-103">Platformy ASP.NET Core w niezawodnej usługi sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="e8bf7-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="e8bf7-104">Platformy ASP.NET Core to nowa open source i międzyplatformowa struktura do tworzenia nowoczesnych aplikacji działających w chmurze podłączonej do Internetu, takich jak aplikacje sieci web, aplikacji IoT i przenośnych zapleczy.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="e8bf7-105">W tym artykule jest toohosting szczegółowy przewodnik platformy ASP.NET Core services w sieci szkieletowej niezawodnej usługi za pomocą hello **Microsoft.ServiceFabric.AspNetCore.** * zestaw pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-105">This article is an in-depth guide toohosting ASP.NET Core services in Service Fabric Reliable Services using hello **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="e8bf7-106">Samouczek wprowadzający platformy ASP.NET Core w sieci szkieletowej usług i instrukcje dotyczące konfigurowania środowiska deweloperskiego, konfigurowanie, zobacz [tworzenie frontonu aplikacji przy użyciu platformy ASP.NET Core sieci web](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="e8bf7-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="e8bf7-107">pozostałe Hello w tym artykule przyjęto założenie, że już znasz platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-107">hello rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="e8bf7-108">Jeśli nie, firma Microsoft zaleca odczytywania za pośrednictwem hello [podstawowe informacje na temat platformy ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span><span class="sxs-lookup"><span data-stu-id="e8bf7-108">If not, we recommend reading through hello [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-hello-service-fabric-environment"></a><span data-ttu-id="e8bf7-109">Platformy ASP.NET Core w środowisku sieci szkieletowej usług hello</span><span class="sxs-lookup"><span data-stu-id="e8bf7-109">ASP.NET Core in hello Service Fabric environment</span></span>

<span data-ttu-id="e8bf7-110">Gdy aplikacji platformy ASP.NET Core można uruchomić na .NET Core lub powitalne pełnego środowiska .NET Framework, obecnie usługi sieć szkieletowa usług można uruchomić tylko na hello pełna platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-110">While ASP.NET Core apps can run on .NET Core or on hello full .NET Framework, Service Fabric services currently can only run on hello full .NET Framework.</span></span> <span data-ttu-id="e8bf7-111">Oznacza to, podczas tworzenia usługi platformy ASP.NET Core Service Fabric, należy nadal wskazać hello pełna platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target hello full .NET Framework.</span></span>

<span data-ttu-id="e8bf7-112">Platformy ASP.NET Core mogą być używane w sieci szkieletowej usług na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="e8bf7-113">**Hostowany jako pliku wykonywalnego gościa**.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="e8bf7-114">To jest głównie używane toorun platformy ASP.NET Core aplikacji w sieci szkieletowej usług bez zmian kodu.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-114">This is primarily used toorun existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="e8bf7-115">**Uruchom wewnątrz niezawodnej usługi**.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="e8bf7-116">Umożliwia lepszą integrację ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello i umożliwia stanowe platformy ASP.NET Core services.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-116">This allows better integration with hello Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="e8bf7-117">Hello dalszej części tego artykułu opisano, jak hello toouse platformy ASP.NET Core wewnątrz niezawodnej usługi za pomocą platformy ASP.NET Core składniki integracji, które są dostarczane z hello zestawu SDK usług sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-117">hello rest of this article explains how toouse ASP.NET Core inside a Reliable Service using hello ASP.NET Core integration components that ship with hello Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="e8bf7-118">Hosting usług sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="e8bf7-118">Service Fabric service hosting</span></span>

<span data-ttu-id="e8bf7-119">W sieci szkieletowej usług, jeden lub więcej wystąpień i/lub repliki usługi uruchamiane w *procesu hosta usługi*, plik wykonywalny, który uruchamia kodu usługi.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="e8bf7-120">Jako autor usługi, własnej procesu hosta usługi hello i sieci szkieletowej usług aktywuje i monitorowanie go dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-120">You, as a service author, own hello service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="e8bf7-121">Tradycyjny ASP.NET (w górę tooMVC 5) jest silnie sprzężonego tooIIS za pośrednictwem System.Web.dll.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-121">Traditional ASP.NET (up tooMVC 5) is tightly coupled tooIIS through System.Web.dll.</span></span> <span data-ttu-id="e8bf7-122">Platformy ASP.NET Core rozdzielenie między powitania serwera sieci web i aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-122">ASP.NET Core provides a separation between hello web server and your web application.</span></span> <span data-ttu-id="e8bf7-123">Umożliwia przenośny między serwerami sieci web inną toobe aplikacji sieci web i pozwala również toobe serwerów sieci web *hosta samodzielnego*, co oznacza można uruchomić serwera sieci web w własnego procesu jako procesu min. tooa, którego właścicielem jest dedykowanych sieci web oprogramowanie serwera, takich jak usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-123">This allows web applications toobe portable between different web servers and also allows web servers toobe *self-hosted*, which means you can start a web server in your own process, as opposed tooa process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="e8bf7-124">W kolejności toocombine usługi Service Fabric i ASP.NET, jako pliku wykonywalnego gościa lub w niezawodnej usługi, musi być możliwe toostart ASP.NET wewnątrz procesu hosta usługi.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-124">In order toocombine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able toostart ASP.NET inside your service host process.</span></span> <span data-ttu-id="e8bf7-125">Platformy ASP.NET Core hostingu samodzielnego umożliwia toodo to.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-125">ASP.NET Core self-hosting allows you toodo this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="e8bf7-126">Hosting platformy ASP.NET Core w niezawodnej usługi</span><span class="sxs-lookup"><span data-stu-id="e8bf7-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="e8bf7-127">Zazwyczaj własnym obsługiwanych aplikacji platformy ASP.NET Core utworzyć WebHost w punkcie wejścia aplikacji, takich jak hello `static void Main()` metoda `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as hello `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="e8bf7-128">W takim przypadku hello cyklem życia hello WebHost jest cyklu życia związanych toohello hello procesu.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-128">In this case, hello lifecycle of hello WebHost is bound toohello lifecycle of hello process.</span></span>

![Hosting platformy ASP.NET Core w procesie][0]

<span data-ttu-id="e8bf7-130">Jednak punkt wejścia aplikacji hello nie jest toocreate odpowiednim miejscu hello WebHost w niezawodnej usługi, ponieważ punkt wejścia aplikacji hello jest używany tylko tooregister usługi wpisz ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello, dzięki czemu może tworzyć wystąpienia tej usługi Typ.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-130">However, hello application entry point is not hello right place toocreate a WebHost in a Reliable Service, because hello application entry point is only used tooregister a service type with hello Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="e8bf7-131">Witaj WebHost powinny zostać utworzone w niezawodnej usługi samej siebie.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-131">hello WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="e8bf7-132">W ramach procesu hosta usługi hello wystąpień usługi i/lub repliki można przejść przez wiele cyklów.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-132">Within hello service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="e8bf7-133">Wystąpienie usługi niezawodnego jest reprezentowana przez usługi klasy wywodzące się z `StatelessService` lub `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="e8bf7-134">Witaj stosu komunikacji usługi znajduje się w `ICommunicationListener` wdrażania w klasie usługi.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-134">hello communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="e8bf7-135">Witaj `Microsoft.ServiceFabric.Services.AspNetCore.*` pakietów NuGet zawiera implementacje `ICommunicationListener` czy start i zarządzanie hello hosta sieci Web platformy ASP.NET Core dla Kestrel lub WebListener w niezawodnej usługi.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-135">hello `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage hello ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![Hosting platformy ASP.NET Core w niezawodnej usługi][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="e8bf7-137">ICommunicationListeners platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e8bf7-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="e8bf7-138">Witaj `ICommunicationListener` implementacje Kestrel i WebListener w hello `Microsoft.ServiceFabric.Services.AspNetCore.*` pakietów NuGet mają podobne wzorce użycia, ale serwer sieci web określonego tooeach nieco inne akcje do wykonania.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-138">hello `ICommunicationListener` implementations for Kestrel and WebListener in hello  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific tooeach web server.</span></span> 

<span data-ttu-id="e8bf7-139">Zarówno odbiorników komunikacji zawierają konstruktora przyjmującego hello następujące argumenty:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-139">Both communication listeners provide a constructor that takes hello following arguments:</span></span>
 - <span data-ttu-id="e8bf7-140">**`ServiceContext serviceContext`**: hello `ServiceContext` obiekt, który zawiera informacje o hello usługi.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-140">**`ServiceContext serviceContext`**: hello `ServiceContext` object that contains information about hello running service.</span></span>
 - <span data-ttu-id="e8bf7-141">**`string endpointName`**: Nazwa hello `Endpoint` konfiguracji w pliku ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-141">**`string endpointName`**: hello name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="e8bf7-142">To przede wszystkim których różnią się odbiorników komunikacji hello dwa: WebListener **wymaga** `Endpoint` konfiguracji, a nie Kestrel.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-142">This is primarily where hello two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="e8bf7-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: lambda, który implementuje, w którym można utworzyć i zwracany `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="e8bf7-144">Dzięki temu można tooconfigure `IWebHost` sposób hello zwykle w aplikacji platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-144">This allows you tooconfigure `IWebHost` hello way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="e8bf7-145">Witaj lambda zawiera adres URL, który jest generowany dla można w zależności od hello sieci szkieletowej usług integracji opcje użycia i hello `Endpoint` konfiguracji należy podać.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-145">hello lambda provides a URL which is generated for you depending on hello Service Fabric integration options you use and hello `Endpoint` configuration you provide.</span></span> <span data-ttu-id="e8bf7-146">Adres URL następnie można zmodyfikować lub używane jako — serwer sieci web hello toostart.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-146">That URL can then be modified or used as-is toostart hello web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="e8bf7-147">Oprogramowanie pośredniczące integracji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="e8bf7-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="e8bf7-148">Witaj `Microsoft.ServiceFabric.Services.AspNetCore` pakiet NuGet zawiera hello `UseServiceFabricIntegration` — metoda rozszerzenia na `IWebHostBuilder` dodaje oprogramowanie pośredniczące obsługujący usługi sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-148">hello `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes hello `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="e8bf7-149">To oprogramowanie pośredniczące konfiguruje hello Kestrel lub WebListener `ICommunicationListener` tooregister usługi unikatowy adres URL z hello Usługa nazewnictwa sieci szkieletowej, a następnie weryfikuje łączą usługowy toohello klienci tooensure żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-149">This middleware configures hello Kestrel or WebListener `ICommunicationListener` tooregister a unique service URL with hello Service Fabric Naming Service and then validates client requests tooensure clients are connecting toohello right service.</span></span> <span data-ttu-id="e8bf7-150">Jest to konieczne w środowisku udostępnionych hosta, na przykład sieci szkieletowej usług, gdy wiele aplikacji sieci web mogą być uruchamiane na powitania same fizyczne lub maszyny wirtualnej, ale nie należy używać nazw unikatowy hosta, klienci tooprevent przez pomyłkę łączenie toohello niewłaściwej usługi.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on hello same physical or virtual machine but do not use unique host names, tooprevent clients from mistakenly connecting toohello wrong service.</span></span> <span data-ttu-id="e8bf7-151">Ten scenariusz jest opisany bardziej szczegółowo w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-151">This scenario is described in more detail in hello next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="e8bf7-152">Przypadek omyłkowo wystąpiła tożsamości</span><span class="sxs-lookup"><span data-stu-id="e8bf7-152">A case of mistaken identity</span></span>
<span data-ttu-id="e8bf7-153">Repliki usługi, niezależnie od protokołu, nasłuchiwania IP:port unikatowych kombinacji.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="e8bf7-154">Po repliki usługi rozpoczął nasłuchiwanie na punkt końcowy IP:port, raporty toohello adres tego punktu końcowego usługi nazewnictwa sieci szkieletowej usług gdzie mogły być odnajdowane przez klientów lub innych usług.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address toohello Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="e8bf7-155">Jeśli używany przez usługi używanych aplikacji dynamicznie przypisywane porty, repliki usługi mogą przypadkowo hello samego IP:port punktu końcowego innej usługi, który został wcześniej na hello same fizyczne lub maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-155">If services use dynamically-assigned application ports, a service replica may coincidentally use hello same IP:port endpoint of another service that was previously on hello same physical or virtual machine.</span></span> <span data-ttu-id="e8bf7-156">To może spowodować, że klient toomistakely połączyć toohello niewłaściwej usługi.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-156">This can cause a client toomistakely connect toohello wrong service.</span></span> <span data-ttu-id="e8bf7-157">To może nastąpić, jeśli występują powitania po sekwencja zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-157">This can happen if hello following sequence of events occur:</span></span>

 1. <span data-ttu-id="e8bf7-158">Usługa A nasłuchuje 10.0.0.1:30000 za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="e8bf7-159">Klient rozpoznaje Service A i pobiera adres 10.0.0.1:30000</span><span class="sxs-lookup"><span data-stu-id="e8bf7-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="e8bf7-160">Usługi przenosi tooa inny węzeł.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-160">Service A moves tooa different node.</span></span>
 4. <span data-ttu-id="e8bf7-161">Usługi B znajduje się na 10.0.0.1 i przypadkowo używa hello tego samego portu 30000.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-161">Service B is placed on 10.0.0.1 and coincidentally uses hello same port 30000.</span></span>
 5. <span data-ttu-id="e8bf7-162">Klient próbuje wykonać tooconnect tooservice A z 10.0.0.1:30000 adres pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-162">Client attempts tooconnect tooservice A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="e8bf7-163">Klient jest teraz pomyślnie połączono tooservice B wiedzy nie jest podłączony toohello niewłaściwej usługi.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-163">Client is now successfully connected tooservice B not realizing it is connected toohello wrong service.</span></span>

<span data-ttu-id="e8bf7-164">Może to powodować błędy w czasie losowych, które mogą być trudne toodiagnose.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-164">This can cause bugs at random times that can be difficult toodiagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="e8bf7-165">Przy użyciu usługi unikatowe adresy URL</span><span class="sxs-lookup"><span data-stu-id="e8bf7-165">Using unique service URLs</span></span>
<span data-ttu-id="e8bf7-166">tooprevent, usług post toohello punktu końcowego usługi nazw z unikatowym identyfikatorem, a następnie zweryfikować Unikatowy identyfikator podczas żądania klienta.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-166">tooprevent this, services can post an endpoint toohello Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="e8bf7-167">To jest akcją współpracy między usługami w zaufanym środowisku — dzierżawy szkodliwy.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="e8bf7-168">Zapewnia to usługa bezpiecznego uwierzytelniania w środowisku szkodliwy dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="e8bf7-169">W zaufanym środowisku hello oprogramowanie pośredniczące, który jest dodawany przez hello `UseServiceFabricIntegration` metody dołącza automatycznie adres toohello Unikatowy identyfikator, który jest przesyłana toohello nazw usługi i sprawdza poprawność identyfikator dla każdego żądania.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-169">In a trusted environment, hello middleware that's added by hello `UseServiceFabricIntegration` method automatically appends a unique identifier toohello address that is posted toohello Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="e8bf7-170">Jeśli identyfikator hello nie jest zgodny, oprogramowanie pośredniczące hello natychmiast zwraca odpowiedź HTTP 410 — Przeniesiono.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-170">If hello identifier does not match, hello middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="e8bf7-171">Usługi używające należy się upewnić, port przypisywane dynamicznie używać tego oprogramowania pośredniczącego.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="e8bf7-172">W środowisku współpracy usług korzystających z stały port unikatowy nie mają ten problem.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="e8bf7-173">Stały port unikatowy jest zwykle używany dla usługi uwzględniającym zewnętrznie, które wymagają dobrze znanego portu dla tooconnect aplikacji klienta do.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications tooconnect to.</span></span> <span data-ttu-id="e8bf7-174">Na przykład większość aplikacji sieci web skierowane do Internetu będzie używać portu 80 i 443 dla połączeń przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="e8bf7-175">W takim przypadku hello Unikatowy identyfikator nie powinna być włączona.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-175">In this case, hello unique identifier should not be enabled.</span></span>

<span data-ttu-id="e8bf7-176">Witaj Poniższy diagram przedstawia przepływ żądania hello z oprogramowania pośredniczącego hello włączone:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-176">hello following diagram shows hello request flow with hello middleware enabled:</span></span>

![Integracja usługi sieci szkieletowej platformy ASP.NET Core][2]

<span data-ttu-id="e8bf7-178">Zarówno Kestrel i WebListener `ICommunicationListener` implementacje użycie tego mechanizmu hello dokładnie tak samo.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly hello same way.</span></span> <span data-ttu-id="e8bf7-179">Mimo że WebListener wewnętrznie pozwala odróżnić żądań oparte na unikatowych ścieżki adresu URL przy użyciu podstawowego hello *http.sys* funkcji, które są funkcji współużytkowania portów *nie* używane przez hello WebListener `ICommunicationListener` implementacji ponieważ skutkiem będzie HTTP 503 i HTTP 404 kodów stanu błędu w scenariuszu hello opisany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-179">Although WebListener can internally differentiate requests based on unique URL paths using hello underlying *http.sys* port sharing feature, that functionality is *not* used by hello WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in hello scenario described earlier.</span></span> <span data-ttu-id="e8bf7-180">Które z kolei utrudnia bardzo klientów toodetermine hello celem błąd hello, ponieważ HTTP 503 i 404 protokołu HTTP są już tooindicate często używane inne błędy.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-180">That in turn makes it very difficult for clients toodetermine hello intent of hello error, as HTTP 503 and HTTP 404 are already commonly used tooindicate other errors.</span></span> <span data-ttu-id="e8bf7-181">W związku z tym zarówno Kestrel i WebListener `ICommunicationListener` implementacje normalizacji na oprogramowanie pośredniczące hello podał hello `UseServiceFabricIntegration` — metoda rozszerzenia, dzięki czemu klienci muszą tylko tooperform punkt końcowy usługi ponownie rozwiązać akcji na odpowiedzi HTTP 410.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on hello middleware provided by hello `UseServiceFabricIntegration` extension method so that clients only need tooperform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="e8bf7-182">WebListener w niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="e8bf7-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="e8bf7-183">WebListener mogą być używane w niezawodnej usługi przez importowanie hello **Microsoft.ServiceFabric.AspNetCore.WebListener** pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-183">WebListener can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="e8bf7-184">Ten pakiet zawiera `WebListenerCommunicationListener`, implementacja `ICommunicationListener`, które pozwala toocreate WebHost Core ASP.NET wewnątrz niezawodnej usługi za pomocą WebListener jako serwera sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using WebListener as hello web server.</span></span>

<span data-ttu-id="e8bf7-185">WebListener jest zbudowany na powitania [interfejsu API serwera HTTP systemu Windows](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="e8bf7-185">WebListener is built on hello [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="e8bf7-186">Ta metoda korzysta hello *http.sys* sterownik jądra używane przez usługi IIS tooprocess HTTP żądania i kierowania ich tooprocesses uruchamiania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-186">This uses hello *http.sys* kernel driver used by IIS tooprocess HTTP requests and route them tooprocesses running web applications.</span></span> <span data-ttu-id="e8bf7-187">Dzięki temu wiele procesów na powitania tej samej maszynie fizycznej lub wirtualnej aplikacji toohost w sieci web na powitania tego samego portu rozróżniane unikatowej ścieżki adresu URL lub nazwa hosta.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-187">This allows multiple processes on hello same physical or virtual machine toohost web applications on hello same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="e8bf7-188">Funkcje te są przydatne w sieci szkieletowej usług do obsługi wielu witryn sieci Web w hello tego samego klastra.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-188">These features are useful in Service Fabric for hosting multiple websites in hello same cluster.</span></span>

<span data-ttu-id="e8bf7-189">Witaj poniższym diagramie przedstawiono sposób WebListener używa hello *http.sys* sterownik jądra w systemie Windows Udostępnianie portów:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-189">hello following diagram illustrates how WebListener uses hello *http.sys* kernel driver on Windows for port sharing:</span></span>

![Sterownik HTTP.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="e8bf7-191">WebListener usługi bezstanowej</span><span class="sxs-lookup"><span data-stu-id="e8bf7-191">WebListener in a stateless service</span></span>
<span data-ttu-id="e8bf7-192">toouse `WebListener` za pośrednictwem usługi bezstanowej, Zastąp hello `CreateServiceInstanceListeners` — metoda i przywracać `WebListenerCommunicationListener` wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-192">toouse `WebListener` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="e8bf7-193">WebListener w usługi stanowej</span><span class="sxs-lookup"><span data-stu-id="e8bf7-193">WebListener in a stateful service</span></span>

<span data-ttu-id="e8bf7-194">`WebListenerCommunicationListener`obecnie nie jest przeznaczony do użytku w usługach stanowych z powodu toocomplications z podstawowej hello *http.sys* funkcji współużytkowania portów.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due toocomplications with hello underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="e8bf7-195">Aby uzyskać więcej informacji zobacz powitania po sekcji alokacją portów dynamicznych z WebListener.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-195">For more information, see hello following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="e8bf7-196">Dla stanowych usług Kestrel jest hello zalecane serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-196">For stateful services, Kestrel is hello recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="e8bf7-197">Konfiguracja punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="e8bf7-197">Endpoint configuration</span></span>

<span data-ttu-id="e8bf7-198">`Endpoint` Konfiguracja jest wymagana dla serwerów sieci web, które używają hello API serwera HTTP systemu Windows, w tym WebListener.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-198">An `Endpoint` configuration is required for web servers that use hello Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="e8bf7-199">Serwery sieci Web, które używają interfejsu API serwera HTTP systemu Windows hello musi najpierw zarezerwować swojego adresu URL z *http.sys* (zwykle jest to realizowane przy użyciu hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) narzędzia).</span><span class="sxs-lookup"><span data-stu-id="e8bf7-199">Web servers that use hello Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="e8bf7-200">Ta akcja wymaga podniesione uprawnienia, które nie mają domyślnie usług.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="e8bf7-201">Witaj opcje "http" lub "https" hello `Protocol` właściwości hello `Endpoint` konfiguracji w *ServiceManifest.xml* są używane w szczególności tooinstruct hello tooregister środowiska uruchomieniowego platformy Service Fabric adresu URL za *http.sys* w Twoim imieniu przy użyciu hello [ *silne symbolu wieloznacznego* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) prefiksu adresu URL.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-201">hello "http" or "https" options for hello `Protocol` property of hello `Endpoint` configuration in *ServiceManifest.xml* are used specifically tooinstruct hello Service Fabric runtime tooregister a URL with *http.sys* on your behalf using hello [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="e8bf7-202">Na przykład tooreserve `http://+:80` dla usługi, hello następującej konfiguracji powinny być używane w pliku ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-202">For example, tooreserve `http://+:80` for a service, hello following configuration should be used in ServiceManifest.xml:</span></span>

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

<span data-ttu-id="e8bf7-203">I nazwa punktu końcowego hello muszą być przekazywane toohello `WebListenerCommunicationListener` konstruktora:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-203">And hello endpoint name must be passed toohello `WebListenerCommunicationListener` constructor:</span></span>

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="e8bf7-204">WebListener za pomocą portu statycznego</span><span class="sxs-lookup"><span data-stu-id="e8bf7-204">Use WebListener with a static port</span></span>
<span data-ttu-id="e8bf7-205">toouse portu statycznego z WebListener, podaj numer portu hello w hello `Endpoint` konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-205">toouse a static port with WebListener, provide hello port number in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="e8bf7-206">Użyj WebListener z portów dynamicznych</span><span class="sxs-lookup"><span data-stu-id="e8bf7-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="e8bf7-207">toouse dynamicznie przypisywanego port o WebListener, Pomiń hello `Port` właściwości w hello `Endpoint` konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-207">toouse a dynamically assigned port with WebListener, omit hello `Port` property in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="e8bf7-208">Należy pamiętać, że port dynamiczny przydzielonej przez `Endpoint` konfiguracji zawiera tylko jeden port *na proces hosta*.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="e8bf7-209">Witaj bieżącej sieci szkieletowej usług hostingu modelu umożliwia wielu usługi wystąpień i/lub replik toobe hostowanych w hello tego samego procesu, co oznacza, że każdej z nich będzie udostępniać hello sam portu podczas przydzielane za pośrednictwem hello `Endpoint` konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-209">hello current Service Fabric hosting model allows multiple service instances and/or replicas toobe hosted in hello same process, meaning that each one will share hello same port when allocated through hello `Endpoint` configuration.</span></span> <span data-ttu-id="e8bf7-210">Wiele wystąpień WebListener można współużytkować port przy użyciu podstawowego hello *http.sys* portu udostępniania funkcji, ale nie jest obsługiwana przez `WebListenerCommunicationListener` powodu komplikacji toohello wprowadza się ona do obsługi żądań klientów.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-210">Multiple WebListener instances can share a port using hello underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due toohello complications it introduces for client requests.</span></span> <span data-ttu-id="e8bf7-211">W przypadku użycia portów dynamicznych Kestrel jest hello zalecane serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-211">For dynamic port usage, Kestrel is hello recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="e8bf7-212">Kestrel w niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="e8bf7-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="e8bf7-213">Kestrel mogą być używane w niezawodnej usługi przez importowanie hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-213">Kestrel can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="e8bf7-214">Ten pakiet zawiera `KestrelCommunicationListener`, implementacja `ICommunicationListener`, które pozwala toocreate WebHost Core ASP.NET wewnątrz niezawodnej usługi za pomocą Kestrel jako serwera sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using Kestrel as hello web server.</span></span>

<span data-ttu-id="e8bf7-215">Kestrel to serwer sieci web i platform dla platformy ASP.NET Core oparta na libuv, biblioteki i platform asynchroniczne We/Wy.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="e8bf7-216">W odróżnieniu od WebListener, Kestrel nie używa Menedżera scentralizowane punktu końcowego takich jak *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="e8bf7-217">I w przeciwieństwie do WebListener, Kestrel nie obsługuje udostępniania portów między wiele procesów.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="e8bf7-218">Każde wystąpienie Kestrel musi używać portu unikatowy.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="e8bf7-220">Kestrel usługi bezstanowej</span><span class="sxs-lookup"><span data-stu-id="e8bf7-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="e8bf7-221">toouse `Kestrel` za pośrednictwem usługi bezstanowej, Zastąp hello `CreateServiceInstanceListeners` — metoda i przywracać `KestrelCommunicationListener` wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-221">toouse `Kestrel` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="e8bf7-222">Kestrel w usługi stanowej</span><span class="sxs-lookup"><span data-stu-id="e8bf7-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="e8bf7-223">toouse `Kestrel` w usługi stanowej, Zastąp hello `CreateServiceReplicaListeners` — metoda i przywracać `KestrelCommunicationListener` wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-223">toouse `Kestrel` in a stateful service, override hello `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

<span data-ttu-id="e8bf7-224">W tym przykładzie pojedyncze wystąpienie `IReliableStateManager` podano kontenera iniekcji zależności WebHost toohello.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-224">In this example, a singleton instance of `IReliableStateManager` is provided toohello WebHost dependency injection container.</span></span> <span data-ttu-id="e8bf7-225">To nie jest to niezbędne, ale pozwala toouse `IReliableStateManager` i niezawodne kolekcji w metody akcji kontrolera MVC.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-225">This is not strictly necessary, but it allows you toouse `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="e8bf7-226">Należy pamiętać, że `Endpoint` Nazwa konfiguracji jest **nie** podano zbyt`KestrelCommunicationListener` w usługi stanowej.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-226">Note that an `Endpoint` configuration name is **not** provided too`KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="e8bf7-227">Jest to wyjaśnić bardziej szczegółowo w hello następujących sekcji.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-227">This is explained in more detail in hello following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="e8bf7-228">Konfiguracja punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="e8bf7-228">Endpoint configuration</span></span>
<span data-ttu-id="e8bf7-229">`Endpoint` Konfiguracja nie jest wymagane toouse Kestrel.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-229">An `Endpoint` configuration is not required toouse Kestrel.</span></span> 

<span data-ttu-id="e8bf7-230">Kestrel jest prosty autonomiczny serwer sieci web; w odróżnieniu od WebListener (lub HttpListener), nie musi `Endpoint` konfiguracji w *ServiceManifest.xml* , ponieważ nie jest konieczne wcześniejsze toostarting rejestracji adresu URL.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior toostarting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="e8bf7-231">Kestrel za pomocą portu statycznego</span><span class="sxs-lookup"><span data-stu-id="e8bf7-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="e8bf7-232">Można skonfigurować port statyczny w hello `Endpoint` konfiguracji ServiceManifest.xml do użytku z Kestrel.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-232">A static port can be configured in hello `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="e8bf7-233">Chociaż nie jest to niezbędne, zawiera dwa potencjalnych korzyści:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="e8bf7-234">Jeśli hello port nie należy do zakresu portów aplikacji hello, plik jest otwarty przez zaporę systemu operacyjnego hello przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-234">If hello port does not fall in hello application port range, it is opened through hello OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="e8bf7-235">Witaj tooyou podanego adresu URL za pośrednictwem `KestrelCommunicationListener` użyje tego portu.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-235">hello URL provided tooyou through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="e8bf7-236">Jeśli `Endpoint` jest skonfigurowany, jego nazwa muszą być przekazywane do hello `KestrelCommunicationListener` konstruktora:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-236">If an `Endpoint` is configured, its name must be passed into hello `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="e8bf7-237">Jeśli `Endpoint` konfiguracji nie jest używany, Pomiń nazwę hello w hello `KestrelCommunicationListener` konstruktora.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-237">If an `Endpoint` configuration is not used, omit hello name in hello `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="e8bf7-238">W takim przypadku będzie używany port dynamiczny.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="e8bf7-239">Zobacz następną sekcję hello, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-239">See hello next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="e8bf7-240">Użyj Kestrel z portów dynamicznych</span><span class="sxs-lookup"><span data-stu-id="e8bf7-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="e8bf7-241">Kestrel nie można użyć przypisania portów automatyczne hello hello `Endpoint` konfiguracji w pliku ServiceManifest.xml, ponieważ port automatyczne przypisanie z `Endpoint` konfiguracji przypisuje unikatowy portu na *proces hosta* , i procesem jednego hosta może zawierać wiele wystąpień Kestrel.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-241">Kestrel cannot use hello automatic port assignment from hello `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="e8bf7-242">Ponieważ Kestrel nie obsługuje udostępniania portów, to nie działa jako każde wystąpienie Kestrel muszą być otwarte na porcie unikatowy.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="e8bf7-243">toouse dynamiczne przypisywanie portów z Kestrel, po prostu pominąć hello `Endpoint` konfiguracji w pliku ServiceManifest.xml całkowicie i nie są przekazywane toohello Nazwa punktu końcowego `KestrelCommunicationListener` konstruktora:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-243">toouse dynamic port assignment with Kestrel, simply omit hello `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name toohello `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="e8bf7-244">W tej konfiguracji `KestrelCommunicationListener` będzie automatycznie wybierać nieużywanego portu z zakresu portów aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from hello application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="e8bf7-245">Scenariusze i konfiguracje</span><span class="sxs-lookup"><span data-stu-id="e8bf7-245">Scenarios and configurations</span></span>
<span data-ttu-id="e8bf7-246">W tej sekcji opisano hello następujące scenariusze i zapewnia hello zalecane kombinację serwera sieci web, konfiguracji portów sieci szkieletowej usług integracji opcje i tooachieve różne ustawienia usługi działa prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-246">This section describes hello following scenarios and provides hello recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings tooachieve a properly functioning service:</span></span>
 - <span data-ttu-id="e8bf7-247">Zewnętrznie udostępnione usługi bezstanowej platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e8bf7-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="e8bf7-248">Tylko wewnętrznie usługi bezstanowej platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e8bf7-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="e8bf7-249">Tylko wewnętrznie usługi stanowej platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e8bf7-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="e8bf7-250">**Zewnętrznie udostępnione** usługi jest taki, który udostępnia punkt końcowy dostępny spoza klastra hello, zwykle za pomocą modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-250">An **externally exposed** service is one that exposes an endpoint reachable from outside hello cluster, usually through a load balancer.</span></span>

<span data-ttu-id="e8bf7-251">**Wyłącznie wewnętrznym** usługi jest jednym tylko jest dostępny w ramach klastra hello których punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-251">An **internal-only** service is one whose endpoint is only reachable from within hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="e8bf7-252">Usługi stanowej, które punkty końcowe zazwyczaj nie powinna być widoczne toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-252">Stateful service endpoints generally should not be exposed toohello Internet.</span></span> <span data-ttu-id="e8bf7-253">Klastry, które znajdują się za usługi równoważenia obciążenia, które znają rozpoznawania usługi sieć szkieletowa usług, takich jak hello Azure Load Balancer będzie tooexpose stanowych usług, ponieważ usługi równoważenia obciążenia hello zostanie nie mogli toolocate i kierowania ruchu toohello odpowiednie usługi stanowej repliki.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as hello Azure Load Balancer, will be unable tooexpose stateful services because hello load balancer will not be able toolocate and route traffic toohello appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="e8bf7-254">Zewnętrznie udostępnione usług bezstanowych platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e8bf7-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="e8bf7-255">WebListener jest zalecane, serwer sieci web dla usług frontonu, które udostępniają zewnętrznych, internetowy punktów końcowych HTTP w systemie Windows hello.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-255">WebListener is hello recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="e8bf7-256">Zapewnia lepszą ochronę przed atakami, a obsługuje funkcje, które nie Kestrel, na przykład uwierzytelnianie systemu Windows i udostępnianie portów.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="e8bf7-257">Kestrel nie jest obsługiwany jako serwer graniczny (internetowy) w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="e8bf7-258">Należy użyć zwrotnego serwera proxy, takich jak IIS lub Nginx toohandle ruch z hello publicznej sieci Internet.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-258">A reverse proxy server such as IIS or Nginx must be used toohandle traffic from hello public Internet.</span></span>
 
<span data-ttu-id="e8bf7-259">Gdy narażonych toohello Internet, usługi bezstanowej należy używać punktu końcowego dobrze znanych i stabilny, który jest dostępny za pośrednictwem usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-259">When exposed toohello Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="e8bf7-260">Jest to adres URL hello zapewni toousers aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-260">This is hello URL you will provide toousers of your application.</span></span> <span data-ttu-id="e8bf7-261">Zaleca się Hello następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-261">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="e8bf7-262">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="e8bf7-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8bf7-263">Serwer sieci Web</span><span class="sxs-lookup"><span data-stu-id="e8bf7-263">Web server</span></span> | <span data-ttu-id="e8bf7-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="e8bf7-264">WebListener</span></span> | <span data-ttu-id="e8bf7-265">Jeśli usługa hello jest tylko narażonych tooa zaufanej sieci, intranet, Kestrel może być używany.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-265">If hello service is only exposed tooa trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="e8bf7-266">W przeciwnym razie WebListener jest opcją hello preferowany.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-266">Otherwise, WebListener is hello preferred option.</span></span> |
| <span data-ttu-id="e8bf7-267">Konfiguracja portów</span><span class="sxs-lookup"><span data-stu-id="e8bf7-267">Port configuration</span></span> | <span data-ttu-id="e8bf7-268">Statyczne</span><span class="sxs-lookup"><span data-stu-id="e8bf7-268">static</span></span> | <span data-ttu-id="e8bf7-269">Dobrze znanego portu statycznego powinna być skonfigurowana w hello `Endpoints` konfiguracji ServiceManifest.xml, takie jak 80 dla protokołu HTTP i 443 dla protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-269">A well-known static port should be configured in hello `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="e8bf7-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="e8bf7-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="e8bf7-271">Brak</span><span class="sxs-lookup"><span data-stu-id="e8bf7-271">None</span></span> | <span data-ttu-id="e8bf7-272">Witaj `ServiceFabricIntegrationOptions.None` opcja powinna być używana podczas konfigurowania sieci szkieletowej usług integracji w oprogramowaniu pośredniczącym, aby usługa hello zrezygnować z przychodzącego żądania toovalidate Unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-272">hello `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that hello service does not attempt toovalidate incoming requests for a unique identifier.</span></span> <span data-ttu-id="e8bf7-273">Użytkownicy zewnętrzni aplikacji nie będzie wiedzieć, hello unikatowe informacje identyfikacyjne używane przez oprogramowanie pośredniczące hello.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-273">External users of your application will not know hello unique identifying information used by hello middleware.</span></span> |
| <span data-ttu-id="e8bf7-274">Liczba wystąpień</span><span class="sxs-lookup"><span data-stu-id="e8bf7-274">Instance Count</span></span> | <span data-ttu-id="e8bf7-275">-1</span><span class="sxs-lookup"><span data-stu-id="e8bf7-275">-1</span></span> | <span data-ttu-id="e8bf7-276">W typowych przypadkach ustawiania liczby wystąpień hello powinna być ustawiona zbyt-"1", aby wystąpienie jest dostępna we wszystkich węzłach, które odbierać dane z usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-276">In typical use cases, hello instance count setting should be set too"-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="e8bf7-277">Jeśli wiele usług zewnętrznie narażonych udostępniać hello sam zestaw węzłów, należy używać unikalny, ale stabilna ścieżki adresu URL.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-277">If multiple externally exposed services share hello same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="e8bf7-278">Można to zrobić przez zmodyfikowanie hello adres URL podany podczas konfigurowania IWebHost.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-278">This can be accomplished by modifying hello URL provided when configuring IWebHost.</span></span> <span data-ttu-id="e8bf7-279">Należy pamiętać, że ma to zastosowanie tylko tooWebListener.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-279">Note this applies tooWebListener only.</span></span>

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="e8bf7-280">Tylko wewnętrznie usługi bezstanowej platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e8bf7-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="e8bf7-281">Usługi bezstanowej, wywoływane tylko z wewnątrz klastra hello należy używać unikatowe adresy URL i dynamicznie przypisywane porty tooensure współpracy między wieloma usługami.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-281">Stateless services that are only called from within hello cluster should use unique URLs and dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="e8bf7-282">Zaleca się Hello następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-282">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="e8bf7-283">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="e8bf7-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8bf7-284">Serwer sieci Web</span><span class="sxs-lookup"><span data-stu-id="e8bf7-284">Web server</span></span> | <span data-ttu-id="e8bf7-285">kestrel</span><span class="sxs-lookup"><span data-stu-id="e8bf7-285">Kestrel</span></span> | <span data-ttu-id="e8bf7-286">Mimo że WebListener może służyć do wewnętrznych usług bezstanowych, Kestrel jest hello zalecane tooallow serwera wielu tooshare wystąpień usługi hosta.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-286">Although WebListener may be used for internal stateless services, Kestrel is hello recommended server tooallow multiple service instances tooshare a host.</span></span>  |
| <span data-ttu-id="e8bf7-287">Konfiguracja portów</span><span class="sxs-lookup"><span data-stu-id="e8bf7-287">Port configuration</span></span> | <span data-ttu-id="e8bf7-288">przypisywane dynamicznie</span><span class="sxs-lookup"><span data-stu-id="e8bf7-288">dynamically assigned</span></span> | <span data-ttu-id="e8bf7-289">Wiele replik usługi stanowej może udostępnić procesu hosta lub systemu operacyjnego hosta i w związku z tym należy unikatowych portów.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="e8bf7-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="e8bf7-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="e8bf7-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="e8bf7-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="e8bf7-292">Z dynamiczne przypisywanie portów to ustawienie zapobiega hello pomylone tożsamości problem opisany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-292">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="e8bf7-293">Wartość InstanceCount</span><span class="sxs-lookup"><span data-stu-id="e8bf7-293">InstanceCount</span></span> | <span data-ttu-id="e8bf7-294">wszystkie</span><span class="sxs-lookup"><span data-stu-id="e8bf7-294">any</span></span> | <span data-ttu-id="e8bf7-295">Liczba wystąpień Hello ustawienie można skonfigurować tooany wartość niezbędne toooperate hello usługi.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-295">hello instance count setting can be set tooany value necessary toooperate hello service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="e8bf7-296">Tylko wewnętrznie usługi stanowej platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e8bf7-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="e8bf7-297">Stanowe usług, które są wywoływać tylko z wewnątrz klastra hello należy używać portów przypisywany dynamicznie tooensure współpracy między wieloma usługami.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-297">Stateful services that are only called from within hello cluster should use dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="e8bf7-298">Zaleca się Hello następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="e8bf7-298">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="e8bf7-299">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="e8bf7-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8bf7-300">Serwer sieci Web</span><span class="sxs-lookup"><span data-stu-id="e8bf7-300">Web server</span></span> | <span data-ttu-id="e8bf7-301">kestrel</span><span class="sxs-lookup"><span data-stu-id="e8bf7-301">Kestrel</span></span> | <span data-ttu-id="e8bf7-302">Witaj `WebListenerCommunicationListener` nie jest przeznaczony do użytku przez usługi stanowej w których replik udziału procesu hosta.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-302">hello `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="e8bf7-303">Konfiguracja portów</span><span class="sxs-lookup"><span data-stu-id="e8bf7-303">Port configuration</span></span> | <span data-ttu-id="e8bf7-304">przypisywane dynamicznie</span><span class="sxs-lookup"><span data-stu-id="e8bf7-304">dynamically assigned</span></span> | <span data-ttu-id="e8bf7-305">Wiele replik usługi stanowej może udostępnić procesu hosta lub systemu operacyjnego hosta i w związku z tym należy unikatowych portów.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="e8bf7-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="e8bf7-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="e8bf7-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="e8bf7-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="e8bf7-308">Z dynamiczne przypisywanie portów to ustawienie zapobiega hello pomylone tożsamości problem opisany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="e8bf7-308">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e8bf7-309">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8bf7-309">Next steps</span></span>
[<span data-ttu-id="e8bf7-310">Debugowanie aplikacji sieci szkieletowej usług za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e8bf7-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
