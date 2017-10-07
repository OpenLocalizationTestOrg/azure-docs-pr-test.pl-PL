---
title: "Usługi w chmurze Azure aplikacje toomicroservices aaaConvert | Dokumentacja firmy Microsoft"
description: "W tym przewodniku porównuje chmury usług sieci Web i roli proces roboczy i usługi sieć szkieletowa usług bezstanowych toohelp migracji z usługi w chmurze tooService sieci szkieletowej."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a><span data-ttu-id="e3529-103">Przewodnik dotyczący tooconverting usług sieci Web i roli proces roboczy tooService sieci szkieletowej bezstanowych</span><span class="sxs-lookup"><span data-stu-id="e3529-103">Guide tooconverting Web and Worker Roles tooService Fabric stateless services</span></span>
<span data-ttu-id="e3529-104">W tym artykule opisano sposób toomigrate chmury usług sieci Web i proces roboczy tooService sieci szkieletowej bezstanowych usług.</span><span class="sxs-lookup"><span data-stu-id="e3529-104">This article describes how toomigrate your Cloud Services Web and Worker Roles tooService Fabric stateless services.</span></span> <span data-ttu-id="e3529-105">Jest hello Najprostsza ścieżka migracji z usługi w chmurze tooService sieci szkieletowej dla aplikacji, których ogólna architektura będzie toostay około hello takie same.</span><span class="sxs-lookup"><span data-stu-id="e3529-105">This is hello simplest migration path from Cloud Services tooService Fabric for applications whose overall architecture is going toostay roughly hello same.</span></span>

## <a name="cloud-service-project-tooservice-fabric-application-project"></a><span data-ttu-id="e3529-106">Projekt aplikacji sieci szkieletowej tooService projektu usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="e3529-106">Cloud Service project tooService Fabric application project</span></span>
 <span data-ttu-id="e3529-107">Projektu usługi w chmurze i projektu aplikacji sieci szkieletowej usług mają podobną strukturę i jednostki zarówno reprezentują hello wdrożenia dla aplikacji — czyli każdy z nich określają hello pełny pakiet toorun wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3529-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent hello deployment unit for your application - that is, they each define hello complete package that is deployed toorun your application.</span></span> <span data-ttu-id="e3529-108">Projekt usługi w chmurze zawiera co najmniej jednej sieci Web lub roli proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="e3529-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="e3529-109">Podobnie projektu aplikacji sieci szkieletowej usług zawiera co najmniej jedna usługa.</span><span class="sxs-lookup"><span data-stu-id="e3529-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="e3529-110">Witaj różnica polega na tym pozamałżeńskie projektu usługi w chmurze hello hello wdrożenie aplikacji o wdrożeniu maszyny Wirtualnej w związku z tym zawiera ustawienia konfiguracji maszyny Wirtualnej w ramach tego projektu aplikacji sieci szkieletowej usług hello określa tylko aplikację, która zostanie wdrożona zestaw tooa istniejących maszyn wirtualnych w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="e3529-110">hello difference is that hello Cloud Service project couples hello application deployment with a VM deployment and thus contains VM configuration settings in it, whereas hello Service Fabric Application project only defines an application that will be deployed tooa set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="e3529-111">samego klastra usługi sieć szkieletowa Hello jest wdrożona tylko raz, albo za pomocą szablonu usługi Resource Manager lub hello portalu Azure i wiele sieci szkieletowej usług aplikacje mogą być wdrożone tooit.</span><span class="sxs-lookup"><span data-stu-id="e3529-111">hello Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through hello Azure portal, and multiple Service Fabric applications can be deployed tooit.</span></span>

![Porównanie projektu usługi Service Fabric i usług w chmurze][3]

## <a name="worker-role-toostateless-service"></a><span data-ttu-id="e3529-113">Usługa toostateless roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="e3529-113">Worker Role toostateless service</span></span>
<span data-ttu-id="e3529-114">Koncepcyjnie rolę procesu roboczego reprezentuje bezstanowego obciążenia, co oznacza każde wystąpienie obciążenia hello jest identyczne i żądania mogą być kierowany tooany wystąpienia w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="e3529-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of hello workload is identical and requests can be routed tooany instance at any time.</span></span> <span data-ttu-id="e3529-115">Każde wystąpienie nie jest oczekiwanym tooremember hello poprzedniego żądania.</span><span class="sxs-lookup"><span data-stu-id="e3529-115">Each instance is not expected tooremember hello previous request.</span></span> <span data-ttu-id="e3529-116">Stan, aby obciążenie hello działa z zarządzanych przez Magazyn stanów zewnętrzne, takie jak magazyn tabel Azure lub bazy danych dokumentów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e3529-116">State that hello workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="e3529-117">W sieci szkieletowej usług tego rodzaju obciążenia jest reprezentowany przez usługę bezstanową.</span><span class="sxs-lookup"><span data-stu-id="e3529-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="e3529-118">Hello najprostsza metoda toomigrating tooService roli procesu roboczego sieci szkieletowej można konwertowanie tooa kod roli proces roboczy usług bezstanowych.</span><span class="sxs-lookup"><span data-stu-id="e3529-118">hello simplest approach toomigrating a Worker Role tooService Fabric can be done by converting Worker Role code tooa Stateless Service.</span></span>

![TooStateless roli procesu roboczego usługi][4]

## <a name="web-role-toostateless-service"></a><span data-ttu-id="e3529-120">Rola toostateless usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="e3529-120">Web Role toostateless service</span></span>
<span data-ttu-id="e3529-121">Podobne tooWorker roli roli sieci Web również reprezentuje bezstanowego obciążenia, a więc koncepcyjnie zbyt może być zmapowane tooa usługi bezstanowej sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="e3529-121">Similar tooWorker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped tooa Service Fabric stateless service.</span></span> <span data-ttu-id="e3529-122">Jednak w przeciwieństwie do ról sieci Web, usługi Service Fabric nie obsługuje usług IIS.</span><span class="sxs-lookup"><span data-stu-id="e3529-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="e3529-123">toomigrate aplikacji sieci web z usługi bezstanowej tooa roli sieci Web wymaga pierwszego przenoszenie tooa platforma sieci web może być hostowana samodzielnie, który nie zależy od usług IIS lub System.Web, takich jak ASP.NET Core 1.</span><span class="sxs-lookup"><span data-stu-id="e3529-123">toomigrate a web application from a Web Role tooa stateless service requires first moving tooa web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="e3529-124">**Aplikacji**</span><span class="sxs-lookup"><span data-stu-id="e3529-124">**Application**</span></span> | <span data-ttu-id="e3529-125">**Obsługiwane**</span><span class="sxs-lookup"><span data-stu-id="e3529-125">**Supported**</span></span> | <span data-ttu-id="e3529-126">**Ścieżki migracji**</span><span class="sxs-lookup"><span data-stu-id="e3529-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3529-127">Formularze sieci Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e3529-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="e3529-128">Nie</span><span class="sxs-lookup"><span data-stu-id="e3529-128">No</span></span> |<span data-ttu-id="e3529-129">Konwertuj tooASP.NET podstawowe 1 MVC</span><span class="sxs-lookup"><span data-stu-id="e3529-129">Convert tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="e3529-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e3529-130">ASP.NET MVC</span></span> |<span data-ttu-id="e3529-131">Z migracją</span><span class="sxs-lookup"><span data-stu-id="e3529-131">With Migration</span></span> |<span data-ttu-id="e3529-132">Uaktualnienia tooASP.NET podstawowe 1 MVC</span><span class="sxs-lookup"><span data-stu-id="e3529-132">Upgrade tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="e3529-133">Składnik Web API platformy ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e3529-133">ASP.NET Web API</span></span> |<span data-ttu-id="e3529-134">Z migracją</span><span class="sxs-lookup"><span data-stu-id="e3529-134">With Migration</span></span> |<span data-ttu-id="e3529-135">Użyj serwera siebie lub platformy ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="e3529-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="e3529-136">Platformy ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="e3529-136">ASP.NET Core 1</span></span> |<span data-ttu-id="e3529-137">Tak</span><span class="sxs-lookup"><span data-stu-id="e3529-137">Yes</span></span> |<span data-ttu-id="e3529-138">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e3529-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="e3529-139">Interfejs API punktu wejścia i cykl życia</span><span class="sxs-lookup"><span data-stu-id="e3529-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="e3529-140">Rola proces roboczy i sieci szkieletowej usług usługi interfejsów API oferta podobne punkty wejścia:</span><span class="sxs-lookup"><span data-stu-id="e3529-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="e3529-141">**Punkt wejścia**</span><span class="sxs-lookup"><span data-stu-id="e3529-141">**Entry Point**</span></span> | <span data-ttu-id="e3529-142">**Rola procesu roboczego**</span><span class="sxs-lookup"><span data-stu-id="e3529-142">**Worker Role**</span></span> | <span data-ttu-id="e3529-143">**Usługa sieci szkieletowej usług**</span><span class="sxs-lookup"><span data-stu-id="e3529-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3529-144">Przetwarzanie</span><span class="sxs-lookup"><span data-stu-id="e3529-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="e3529-145">Początek maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e3529-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="e3529-146">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e3529-146">N/A</span></span> |
| <span data-ttu-id="e3529-147">Zatrzymanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e3529-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="e3529-148">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e3529-148">N/A</span></span> |
| <span data-ttu-id="e3529-149">Otwórz odbiornika dla żądań klientów</span><span class="sxs-lookup"><span data-stu-id="e3529-149">Open listener for client requests</span></span> |<span data-ttu-id="e3529-150">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e3529-150">N/A</span></span> |<ul><li> <span data-ttu-id="e3529-151">`CreateServiceInstanceListener()`Aby uzyskać bezstanowych</span><span class="sxs-lookup"><span data-stu-id="e3529-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="e3529-152">`CreateServiceReplicaListener()`dla stateful</span><span class="sxs-lookup"><span data-stu-id="e3529-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="e3529-153">Rola procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="e3529-153">Worker Role</span></span>
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="e3529-154">Usługa sieci szkieletowej usług bezstanowych</span><span class="sxs-lookup"><span data-stu-id="e3529-154">Service Fabric Stateless Service</span></span>
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

<span data-ttu-id="e3529-155">W których przetwarzanie toobegin mają zastąpienie podstawowego "Uruchom".</span><span class="sxs-lookup"><span data-stu-id="e3529-155">Both have a primary "Run" override in which toobegin processing.</span></span> <span data-ttu-id="e3529-156">Łączenie usługi sieć szkieletowa usług `Run`, `Start`, i `Stop` na jeden punkt wejścia, `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="e3529-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="e3529-157">Podczas pracy z usługą powinny one zacząć `RunAsync` uruchamia i powinna zostać przerwana w pracy, gdy hello `RunAsync` zostanie zasygnalizowane metody CancellationToken.</span><span class="sxs-lookup"><span data-stu-id="e3529-157">Your service should begin working when `RunAsync` starts, and should stop working when hello `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="e3529-158">Istnieje kilka klucza różnic między hello cykl życia i okresem istnienia usług roli proces roboczy i sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="e3529-158">There are several key differences between hello lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="e3529-159">**Cykl życia:** hello największych różnica polega na czy roli proces roboczy jest maszyny Wirtualnej i dlatego jego cyklem życia jest wiązanej toohello maszyny Wirtualnej, która obejmuje zdarzenia podczas uruchamiania i zatrzymywania w hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3529-159">**Lifecycle:** hello biggest difference is that a Worker Role is a VM and so its lifecycle is tied toohello VM, which includes events for when hello VM starts and stops.</span></span> <span data-ttu-id="e3529-160">Usługa Service Fabric ma cykl życia, która jest oddzielona od hello wirtualna cykl życia, więc nie zawiera zdarzeń związanych z gdy hello host maszyny Wirtualnej lub uruchomieniu maszyny i zakończenie, ponieważ nie są powiązane.</span><span class="sxs-lookup"><span data-stu-id="e3529-160">A Service Fabric service has a lifecycle that is separate from hello VM lifecycle, so it does not include events for when hello host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="e3529-161">**Okres istnienia:** odtwarzana wystąpienia roli proces roboczy, jeśli hello `Run` wyjścia metody.</span><span class="sxs-lookup"><span data-stu-id="e3529-161">**Lifetime:** A Worker Role instance will recycle if hello `Run` method exits.</span></span> <span data-ttu-id="e3529-162">Witaj `RunAsync` metody usługi sieci szkieletowej usług można uruchamiać toocompletion i wystąpienie usługi hello pozostaną w górę.</span><span class="sxs-lookup"><span data-stu-id="e3529-162">hello `RunAsync` method in a Service Fabric service however can run toocompletion and hello service instance will stay up.</span></span> 

<span data-ttu-id="e3529-163">Sieć szkieletowa usług udostępnia punkt wejścia instalacji komunikacji opcjonalne dla usług, które nasłuchuje żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="e3529-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="e3529-164">Zarówno hello RunAsync, jak i punktu wejścia komunikacji są opcjonalne zastąpień w usługach sieci szkieletowej usług - usługi może wybierz tooonly nasłuchiwania żądań tooclient lub uruchomić tylko w pętli przetwarzania i/lub -, które dlatego hello metodzie RunAsync jest dozwolone tooexit bez ponowne uruchamianie hello wystąpienie usługi, ponieważ może on nadal toolisten do obsługi żądań klientów.</span><span class="sxs-lookup"><span data-stu-id="e3529-164">Both hello RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose tooonly listen tooclient requests, or only run a processing loop, or both - which is why hello RunAsync method is allowed tooexit without restarting hello service instance, because it may continue toolisten for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="e3529-165">Interfejs API aplikacji i środowiska</span><span class="sxs-lookup"><span data-stu-id="e3529-165">Application API and environment</span></span>
<span data-ttu-id="e3529-166">Środowisko usługi w chmurze Hello interfejsu API zawiera informacje i funkcjonalność hello bieżące wystąpienie maszyny Wirtualnej, a także informacje o innych wystąpień roli maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3529-166">hello Cloud Services environment API provides information and functionality for hello current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="e3529-167">Sieć szkieletowa usług zawiera informacje dotyczące środowiska uruchomieniowego tooits i niektóre informacje o węźle hello usługi jest obecnie uruchomiony w.</span><span class="sxs-lookup"><span data-stu-id="e3529-167">Service Fabric provides information related tooits runtime and some information about hello node a service is currently running on.</span></span> 

| <span data-ttu-id="e3529-168">**Zadania środowiska**</span><span class="sxs-lookup"><span data-stu-id="e3529-168">**Environment Task**</span></span> | <span data-ttu-id="e3529-169">**Cloud Services**</span><span class="sxs-lookup"><span data-stu-id="e3529-169">**Cloud Services**</span></span> | <span data-ttu-id="e3529-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="e3529-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3529-171">Ustawienia konfiguracji i powiadomienia o zmianie</span><span class="sxs-lookup"><span data-stu-id="e3529-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="e3529-172">Magazyn lokalny</span><span class="sxs-lookup"><span data-stu-id="e3529-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="e3529-173">Informacje o punkcie końcowym</span><span class="sxs-lookup"><span data-stu-id="e3529-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="e3529-174">Bieżące wystąpienie:`RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="e3529-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="e3529-175">Inne role i wystąpienie:`RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="e3529-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="e3529-176">`NodeContext`dla bieżącego adresu węzła</span><span class="sxs-lookup"><span data-stu-id="e3529-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="e3529-177">`FabricClient`i `ServicePartitionResolver` do odnajdywania punktu końcowego usługi</span><span class="sxs-lookup"><span data-stu-id="e3529-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="e3529-178">Emulacja środowiska</span><span class="sxs-lookup"><span data-stu-id="e3529-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="e3529-179">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e3529-179">N/A</span></span> |
| <span data-ttu-id="e3529-180">Zdarzenie zmiany jednoczesnych</span><span class="sxs-lookup"><span data-stu-id="e3529-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="e3529-181">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e3529-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="e3529-182">Ustawienia konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e3529-182">Configuration settings</span></span>
<span data-ttu-id="e3529-183">Ustawienia konfiguracji usług w chmurze są ustawiane dla roli maszyny Wirtualnej i zastosować tooall wystąpień tej roli maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3529-183">Configuration settings in Cloud Services are set for a VM role and apply tooall instances of that VM role.</span></span> <span data-ttu-id="e3529-184">Te ustawienia są pary klucz wartość ustawiona w plikach ServiceConfiguration.*.cscfg i jest dostępny bezpośrednio za pomocą RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="e3529-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="e3529-185">W sieci szkieletowej usług ustawienia mają zastosowanie indywidualnie tooeach usług i aplikacji tooeach, zamiast tooa maszyny Wirtualnej, ponieważ maszyna wirtualna może obsługiwać wiele usług i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3529-185">In Service Fabric, settings apply individually tooeach service and tooeach application, rather than tooa VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="e3529-186">Usługa składa się z trzech pakietów:</span><span class="sxs-lookup"><span data-stu-id="e3529-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="e3529-187">**Kod:** zawiera pliki wykonywalne usługi hello, plików binarnych biblioteki dll i inne pliki wymagane przez usługę toorun.</span><span class="sxs-lookup"><span data-stu-id="e3529-187">**Code:** contains hello service executables, binaries, DLLs, and any other files a service needs toorun.</span></span>
* <span data-ttu-id="e3529-188">**Config:** wszystkich plików konfiguracji i ustawień usługi.</span><span class="sxs-lookup"><span data-stu-id="e3529-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="e3529-189">**Dane:** plików statycznych danych skojarzonych z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="e3529-189">**Data:** static data files associated with hello service.</span></span>

<span data-ttu-id="e3529-190">Każdy z tych pakietów można niezależnie określonej wersji, jak i uaktualnionych.</span><span class="sxs-lookup"><span data-stu-id="e3529-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="e3529-191">Podobne usługi tooCloud, pakietu konfiguracji można uzyskać programistycznie przy użyciu interfejsu API i zdarzenia są dostępne toonotify hello usługi o zmianie konfiguracji pakietu.</span><span class="sxs-lookup"><span data-stu-id="e3529-191">Similar tooCloud Services, a config package can be accessed programmatically through an API and events are available toonotify hello service of a config package change.</span></span> <span data-ttu-id="e3529-192">Pliku Settings.xml może służyć do konfiguracji klucz wartość, a dostęp programistyczny podobne toohello aplikacji ustawienia sekcji pliku App.config.</span><span class="sxs-lookup"><span data-stu-id="e3529-192">A Settings.xml file can be used for key-value configuration and programmatic access similar toohello app settings section of an App.config file.</span></span> <span data-ttu-id="e3529-193">Jednak w przeciwieństwie do usługi w chmurze, pakiet konfiguracji sieci szkieletowej usług może zawierać pliki konfiguracji w dowolnym formacie XML, JSON, yaml programu lub niestandardowy format binarny.</span><span class="sxs-lookup"><span data-stu-id="e3529-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="e3529-194">Uzyskiwanie dostępu do konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e3529-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="e3529-195">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e3529-195">Cloud Services</span></span>
<span data-ttu-id="e3529-196">Ustawienia konfiguracji z ServiceConfiguration.*.cscfg jest możliwy za pośrednictwem `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="e3529-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="e3529-197">Te ustawienia są globalnie dostępną tooall wystąpień roli w hello tego samego wdrożenia usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e3529-197">These settings are globally available tooall role instances in hello same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="e3529-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e3529-198">Service Fabric</span></span>
<span data-ttu-id="e3529-199">Każda usługa ma własny pakiet konfiguracji poszczególnych.</span><span class="sxs-lookup"><span data-stu-id="e3529-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="e3529-200">Nie istnieje wbudowany mechanizm dla globalne ustawienia konfiguracji dostępne przez wszystkie aplikacje w klastrze.</span><span class="sxs-lookup"><span data-stu-id="e3529-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="e3529-201">Podczas korzystania z usługi Service Fabric specjalne Settings.xml konfiguracji pliku w ramach pakietu konfiguracji wartości w pliku Settings.xml można zastąpić na poziomie aplikacji hello, umożliwiając ustawień konfiguracji na poziomie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3529-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at hello application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="e3529-202">Ustawienia konfiguracji są dostępu w ramach każdego wystąpienia usługi za pośrednictwem usługi hello `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="e3529-202">Configuration settings are accesses within each service instance through hello service's `CodePackageActivationContext`.</span></span>

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a><span data-ttu-id="e3529-203">Zdarzenia aktualizacji konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e3529-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="e3529-204">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e3529-204">Cloud Services</span></span>
<span data-ttu-id="e3529-205">Witaj `RoleEnvironment.Changed` zdarzenie jest używane toonotify występuje wszystkich wystąpień roli wprowadzania zmian w środowisku hello, np. o zmianie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e3529-205">hello `RoleEnvironment.Changed` event is used toonotify all role instances when a change occurs in hello environment, such as a configuration change.</span></span> <span data-ttu-id="e3529-206">Jest to używane tooconsume konfiguracji aktualizacji bez odtwarzania wystąpień roli lub ponowne uruchomienie procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="e3529-206">This is used tooconsume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="e3529-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e3529-207">Service Fabric</span></span>
<span data-ttu-id="e3529-208">Każdy z trzech typów pakietów hello w usłudze - kodu, konfiguracji i danych — mieć zdarzenia, które powiadamiają o wystąpieniu usługi, gdy pakiet zostanie zaktualizowany, dodany lub usunięty.</span><span class="sxs-lookup"><span data-stu-id="e3529-208">Each of hello three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="e3529-209">Usługa może zawierać wielu pakietów każdego typu.</span><span class="sxs-lookup"><span data-stu-id="e3529-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="e3529-210">Na przykład usługa może mieć wielu pakietów konfiguracji każdego indywidualnie numerów wersji i możliwej.</span><span class="sxs-lookup"><span data-stu-id="e3529-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="e3529-211">Te zdarzenia są dostępne tooconsume zmiany pakietów usług bez konieczności ponownego uruchamiania wystąpienie usługi hello.</span><span class="sxs-lookup"><span data-stu-id="e3529-211">These events are available tooconsume changes in service packages without restarting hello service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="e3529-212">Zadania uruchamiania</span><span class="sxs-lookup"><span data-stu-id="e3529-212">Startup tasks</span></span>
<span data-ttu-id="e3529-213">Uruchamianie zadania są działaniach wykonywanych przed uruchomieniem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3529-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="e3529-214">Zadanie uruchamiania jest najczęściej używanymi toorun skryptów instalacji przy użyciu podniesionych przywilejów.</span><span class="sxs-lookup"><span data-stu-id="e3529-214">A startup task is typically used toorun setup scripts using elevated privileges.</span></span> <span data-ttu-id="e3529-215">Usługa Service Fabric i usług w chmurze obsługuje zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="e3529-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="e3529-216">Witaj podstawowa różnica polega na tym w usługi w chmurze, zadanie uruchamiania jest wiązana tooa maszyny Wirtualnej, ponieważ jest częścią wystąpienia roli, w sieci szkieletowej usług zadanie uruchamiania jest wiązana tooa usługi, która nie jest związany tooany określonej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3529-216">hello main difference is that in Cloud Services, a startup task is tied tooa VM because it is part of a role instance, whereas in Service Fabric a startup task is tied tooa service, which is not tied tooany particular VM.</span></span>

| <span data-ttu-id="e3529-217">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e3529-217">Cloud Services</span></span> | <span data-ttu-id="e3529-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e3529-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3529-219">Lokalizacja konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e3529-219">Configuration location</span></span> |<span data-ttu-id="e3529-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="e3529-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="e3529-221">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="e3529-221">Privileges</span></span> |<span data-ttu-id="e3529-222">"ograniczony" lub "z podwyższonym poziomem uprawnień"</span><span class="sxs-lookup"><span data-stu-id="e3529-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="e3529-223">Sekwencjonowanie</span><span class="sxs-lookup"><span data-stu-id="e3529-223">Sequencing</span></span> |<span data-ttu-id="e3529-224">"prosty", "tła", "narzędzia"</span><span class="sxs-lookup"><span data-stu-id="e3529-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="e3529-225">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e3529-225">Cloud Services</span></span>
<span data-ttu-id="e3529-226">Usług w chmurze punktu wejścia uruchamiania jest skonfigurowany dla każdej roli w ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="e3529-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a><span data-ttu-id="e3529-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e3529-227">Service Fabric</span></span>
<span data-ttu-id="e3529-228">W sieci szkieletowej usług punktu wejścia uruchamiania jest skonfigurowany dla usługi w pliku ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="e3529-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a><span data-ttu-id="e3529-229">Uwagi dotyczące środowiska deweloperskiego</span><span class="sxs-lookup"><span data-stu-id="e3529-229">A note about development environment</span></span>
<span data-ttu-id="e3529-230">Usługi Service Fabric i usług w chmurze są zintegrowane z programem Visual Studio z szablonów projektu i obsługę debugowania, konfigurowanie i wdrażanie zarówno lokalnie i tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e3529-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and tooAzure.</span></span> <span data-ttu-id="e3529-231">Usługa Service Fabric i usług w chmurze udostępniają rozwoju lokalnego środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="e3529-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="e3529-232">Witaj różnicą jest to, że podczas hello emuluje programowanie środowiska uruchomieniowego usługi w chmurze hello środowiska platformy Azure, na którym jest uruchomiony, Service Fabric nie korzysta z emulatora — używa środowiska uruchomieniowego platformy Service Fabric pełną hello.</span><span class="sxs-lookup"><span data-stu-id="e3529-232">hello difference is that while hello Cloud Service development runtime emulates hello Azure environment on which it runs, Service Fabric does not use an emulator - it uses hello complete Service Fabric runtime.</span></span> <span data-ttu-id="e3529-233">Hello jest środowiska, które należy uruchomić na komputerze deweloperskim lokalnej sieci szkieletowej usług hello tym samym środowisku, który jest uruchamiany w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e3529-233">hello Service Fabric environment you run on your local development machine is hello same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3529-234">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3529-234">Next steps</span></span>
<span data-ttu-id="e3529-235">Dowiedz się więcej o usługach niezawodnej usługi sieci szkieletowej i hello podstawowych różnic między usługami w chmurze i architektura toounderstand aplikacji sieci szkieletowej usług, jak tootake zaletą hello pełny zestaw funkcji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="e3529-235">Read more about Service Fabric Reliable Services and hello fundamental differences between Cloud Services and Service Fabric application architecture toounderstand how tootake advantage of hello full set of Service Fabric features.</span></span>

* [<span data-ttu-id="e3529-236">Wprowadzenie do korzystania z usługi sieć szkieletowa niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="e3529-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="e3529-237">Przewodnik koncepcyjny toohello różnice między usługami w chmurze i sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="e3529-237">Conceptual guide toohello differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
