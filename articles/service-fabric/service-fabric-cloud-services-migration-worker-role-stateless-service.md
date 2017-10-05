---
title: "Konwertowanie aplikacji usługi w chmurze Azure do mikrousług | Dokumentacja firmy Microsoft"
description: "Ten przewodnik zawiera porównanie bezstanowych usługi sieci Web usługi w chmurze i roli proces roboczy i sieci szkieletowej usług ułatwia migrację z usług chmury do sieci szkieletowej usług."
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
ms.openlocfilehash: 4ab1f83e88b262b1752300b2786340d9abca8154
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="guide-to-converting-web-and-worker-roles-to-service-fabric-stateless-services"></a><span data-ttu-id="20628-103">Przewodnik po konwersji sieci Web i proces roboczy usług bezstanowych sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="20628-103">Guide to converting Web and Worker Roles to Service Fabric stateless services</span></span>
<span data-ttu-id="20628-104">W tym artykule opisano sposób migracji z usług chmury w sieci Web i proces roboczy do usługi sieć szkieletowa usług bezstanowych.</span><span class="sxs-lookup"><span data-stu-id="20628-104">This article describes how to migrate your Cloud Services Web and Worker Roles to Service Fabric stateless services.</span></span> <span data-ttu-id="20628-105">Jest to najprostsza ścieżka migracji z usług w chmurze sieci szkieletowej usług dla aplikacji, których ogólna architektura ma około pozostają takie same.</span><span class="sxs-lookup"><span data-stu-id="20628-105">This is the simplest migration path from Cloud Services to Service Fabric for applications whose overall architecture is going to stay roughly the same.</span></span>

## <a name="cloud-service-project-to-service-fabric-application-project"></a><span data-ttu-id="20628-106">Projekt usługi w chmurze do projektu aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="20628-106">Cloud Service project to Service Fabric application project</span></span>
 <span data-ttu-id="20628-107">Projektu usługi w chmurze i projektu aplikacji sieci szkieletowej usług mają podobną strukturę i reprezentuje zarówno jednostki wdrożenia aplikacji — czyli każdy z nich zdefiniuj pełny pakiet, który jest wdrażany do uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="20628-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent the deployment unit for your application - that is, they each define the complete package that is deployed to run your application.</span></span> <span data-ttu-id="20628-108">Projekt usługi w chmurze zawiera co najmniej jednej sieci Web lub roli proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="20628-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="20628-109">Podobnie projektu aplikacji sieci szkieletowej usług zawiera co najmniej jedna usługa.</span><span class="sxs-lookup"><span data-stu-id="20628-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="20628-110">Różnica polega na tym że projektu usługi w chmurze couples wdrożenie aplikacji z wdrożenia maszyny Wirtualnej, a w związku z tym zawiera ustawienia konfiguracji maszyny Wirtualnej w ramach tego projektu aplikacji sieci szkieletowej usług określa tylko aplikację, która zostanie wdrożona do zestawu istniejące maszyny wirtualne w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="20628-110">The difference is that the Cloud Service project couples the application deployment with a VM deployment and thus contains VM configuration settings in it, whereas the Service Fabric Application project only defines an application that will be deployed to a set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="20628-111">Samego klastra usługi sieć szkieletowa jest wdrożona tylko raz, za pomocą szablonu usługi Resource Manager lub za pośrednictwem portalu Azure i można do niego wdrożyć wielu aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="20628-111">The Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through the Azure portal, and multiple Service Fabric applications can be deployed to it.</span></span>

![Porównanie projektu usługi Service Fabric i usług w chmurze][3]

## <a name="worker-role-to-stateless-service"></a><span data-ttu-id="20628-113">Rola proces roboczy do usługi bezstanowej</span><span class="sxs-lookup"><span data-stu-id="20628-113">Worker Role to stateless service</span></span>
<span data-ttu-id="20628-114">Koncepcyjnie rolę procesu roboczego reprezentuje bezstanowego obciążenia, co oznacza każde wystąpienie obciążenie jest identyczne i żądania mogą być kierowane do dowolnego wystąpienia w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="20628-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of the workload is identical and requests can be routed to any instance at any time.</span></span> <span data-ttu-id="20628-115">Każde wystąpienie nie jest oczekiwany do zapamiętania poprzedniego żądania.</span><span class="sxs-lookup"><span data-stu-id="20628-115">Each instance is not expected to remember the previous request.</span></span> <span data-ttu-id="20628-116">Stan, który obciążenie działa na jest zarządzana przez Magazyn stanów zewnętrzne, takie jak magazyn tabel Azure lub bazy danych dokumentów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="20628-116">State that the workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="20628-117">W sieci szkieletowej usług tego rodzaju obciążenia jest reprezentowany przez usługę bezstanową.</span><span class="sxs-lookup"><span data-stu-id="20628-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="20628-118">Najprostsza metoda migrowania roli procesu roboczego platformy Service Fabric może odbywać się konwertując kod roli proces roboczy usług bezstanowych.</span><span class="sxs-lookup"><span data-stu-id="20628-118">The simplest approach to migrating a Worker Role to Service Fabric can be done by converting Worker Role code to a Stateless Service.</span></span>

![Rola proces roboczy do usługi bezstanowej][4]

## <a name="web-role-to-stateless-service"></a><span data-ttu-id="20628-120">Rola sieci Web do usługi bezstanowej</span><span class="sxs-lookup"><span data-stu-id="20628-120">Web Role to stateless service</span></span>
<span data-ttu-id="20628-121">Podobnie jak rola proces roboczy, rolę sieci Web również reprezentuje bezstanowego obciążenia, a więc koncepcyjnie on zbyt mogą być mapowane na usługę bezstanową sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="20628-121">Similar to Worker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped to a Service Fabric stateless service.</span></span> <span data-ttu-id="20628-122">Jednak w przeciwieństwie do ról sieci Web, usługi Service Fabric nie obsługuje usług IIS.</span><span class="sxs-lookup"><span data-stu-id="20628-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="20628-123">Aby przeprowadzić migrację sieci web aplikacji z roli sieci Web do usługi bezstanowej wymaga przenoszenia najpierw do platforma sieci web, która może być hostowana samodzielnie i nie zależą od usług IIS lub System.Web, takich jak ASP.NET Core 1.</span><span class="sxs-lookup"><span data-stu-id="20628-123">To migrate a web application from a Web Role to a stateless service requires first moving to a web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="20628-124">**Aplikacji**</span><span class="sxs-lookup"><span data-stu-id="20628-124">**Application**</span></span> | <span data-ttu-id="20628-125">**Obsługiwane**</span><span class="sxs-lookup"><span data-stu-id="20628-125">**Supported**</span></span> | <span data-ttu-id="20628-126">**Ścieżki migracji**</span><span class="sxs-lookup"><span data-stu-id="20628-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="20628-127">Formularze sieci Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="20628-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="20628-128">Nie</span><span class="sxs-lookup"><span data-stu-id="20628-128">No</span></span> |<span data-ttu-id="20628-129">Konwertuj na MVC ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="20628-129">Convert to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="20628-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="20628-130">ASP.NET MVC</span></span> |<span data-ttu-id="20628-131">Z migracją</span><span class="sxs-lookup"><span data-stu-id="20628-131">With Migration</span></span> |<span data-ttu-id="20628-132">Uaktualnienie do platformy ASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="20628-132">Upgrade to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="20628-133">Składnik Web API platformy ASP.NET</span><span class="sxs-lookup"><span data-stu-id="20628-133">ASP.NET Web API</span></span> |<span data-ttu-id="20628-134">Z migracją</span><span class="sxs-lookup"><span data-stu-id="20628-134">With Migration</span></span> |<span data-ttu-id="20628-135">Użyj serwera siebie lub platformy ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="20628-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="20628-136">Platformy ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="20628-136">ASP.NET Core 1</span></span> |<span data-ttu-id="20628-137">Tak</span><span class="sxs-lookup"><span data-stu-id="20628-137">Yes</span></span> |<span data-ttu-id="20628-138">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="20628-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="20628-139">Interfejs API punktu wejścia i cykl życia</span><span class="sxs-lookup"><span data-stu-id="20628-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="20628-140">Rola proces roboczy i sieci szkieletowej usług usługi interfejsów API oferta podobne punkty wejścia:</span><span class="sxs-lookup"><span data-stu-id="20628-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="20628-141">**Punkt wejścia**</span><span class="sxs-lookup"><span data-stu-id="20628-141">**Entry Point**</span></span> | <span data-ttu-id="20628-142">**Rola procesu roboczego**</span><span class="sxs-lookup"><span data-stu-id="20628-142">**Worker Role**</span></span> | <span data-ttu-id="20628-143">**Usługa sieci szkieletowej usług**</span><span class="sxs-lookup"><span data-stu-id="20628-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="20628-144">Przetwarzanie</span><span class="sxs-lookup"><span data-stu-id="20628-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="20628-145">Początek maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="20628-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="20628-146">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="20628-146">N/A</span></span> |
| <span data-ttu-id="20628-147">Zatrzymanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="20628-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="20628-148">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="20628-148">N/A</span></span> |
| <span data-ttu-id="20628-149">Otwórz odbiornika dla żądań klientów</span><span class="sxs-lookup"><span data-stu-id="20628-149">Open listener for client requests</span></span> |<span data-ttu-id="20628-150">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="20628-150">N/A</span></span> |<ul><li> <span data-ttu-id="20628-151">`CreateServiceInstanceListener()`Aby uzyskać bezstanowych</span><span class="sxs-lookup"><span data-stu-id="20628-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="20628-152">`CreateServiceReplicaListener()`dla stateful</span><span class="sxs-lookup"><span data-stu-id="20628-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="20628-153">Rola procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="20628-153">Worker Role</span></span>
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

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="20628-154">Usługa sieci szkieletowej usług bezstanowych</span><span class="sxs-lookup"><span data-stu-id="20628-154">Service Fabric Stateless Service</span></span>
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

<span data-ttu-id="20628-155">Mają zastąpienie podstawowego "Uruchom", w którym na przetworzenie.</span><span class="sxs-lookup"><span data-stu-id="20628-155">Both have a primary "Run" override in which to begin processing.</span></span> <span data-ttu-id="20628-156">Łączenie usługi sieć szkieletowa usług `Run`, `Start`, i `Stop` na jeden punkt wejścia, `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="20628-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="20628-157">Podczas pracy z usługą powinny one zacząć `RunAsync` uruchamia i ma zostać zatrzymana, gdy praca `RunAsync` zostanie zasygnalizowane metody CancellationToken.</span><span class="sxs-lookup"><span data-stu-id="20628-157">Your service should begin working when `RunAsync` starts, and should stop working when the `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="20628-158">Istnieje kilka podstawowych różnic między cykl życia i okresem istnienia usług roli proces roboczy i sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="20628-158">There are several key differences between the lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="20628-159">**Cykl życia:** największych różnica polega na roli proces roboczy jest maszyny Wirtualnej, a więc cykl życia jest związany z maszyny Wirtualnej, która obejmuje zdarzenia podczas uruchamiania i zatrzymywania w Maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="20628-159">**Lifecycle:** The biggest difference is that a Worker Role is a VM and so its lifecycle is tied to the VM, which includes events for when the VM starts and stops.</span></span> <span data-ttu-id="20628-160">Usługa Service Fabric ma cykl życia, która jest oddzielona od maszyny Wirtualnej cykl życia, więc nie zawiera zdarzenia po hosta maszyny Wirtualnej lub maszyny uruchamia i zatrzymać, ponieważ nie są powiązane.</span><span class="sxs-lookup"><span data-stu-id="20628-160">A Service Fabric service has a lifecycle that is separate from the VM lifecycle, so it does not include events for when the host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="20628-161">**Okres istnienia:** odtwarzana wystąpienia roli proces roboczy, jeśli `Run` wyjścia metody.</span><span class="sxs-lookup"><span data-stu-id="20628-161">**Lifetime:** A Worker Role instance will recycle if the `Run` method exits.</span></span> <span data-ttu-id="20628-162">`RunAsync` Metody usługi sieci szkieletowej usług jednak można uruchomić w celu ukończenia i wystąpienie usługi będą przechowywane w górę.</span><span class="sxs-lookup"><span data-stu-id="20628-162">The `RunAsync` method in a Service Fabric service however can run to completion and the service instance will stay up.</span></span> 

<span data-ttu-id="20628-163">Sieć szkieletowa usług udostępnia punkt wejścia instalacji komunikacji opcjonalne dla usług, które nasłuchuje żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="20628-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="20628-164">Punkt wejścia zarówno RunAsync, jak i komunikacji są opcjonalne zastąpień w - usługi wybrać nasłuchiwał tylko na żądania klientów, lub uruchomić tylko w pętli przetwarzania i/lub - usługi sieć szkieletowa usług, które dlatego metodzie RunAsync będzie mógł zamknąć bez ponownego uruchamiania Usługa wystąpienia, ponieważ mogą nadal nasłuchuje żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="20628-164">Both the RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose to only listen to client requests, or only run a processing loop, or both - which is why the RunAsync method is allowed to exit without restarting the service instance, because it may continue to listen for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="20628-165">Interfejs API aplikacji i środowiska</span><span class="sxs-lookup"><span data-stu-id="20628-165">Application API and environment</span></span>
<span data-ttu-id="20628-166">Interfejs API środowiska usługi w chmurze zawiera informacje oraz funkcje dla bieżącego wystąpienia maszyny Wirtualnej, a także informacje o innych wystąpień roli maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="20628-166">The Cloud Services environment API provides information and functionality for the current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="20628-167">Usługi Service Fabric zawiera informacje dotyczące jego środowiska uruchomieniowego i niektóre informacje o węźle usługi jest obecnie uruchomiony w.</span><span class="sxs-lookup"><span data-stu-id="20628-167">Service Fabric provides information related to its runtime and some information about the node a service is currently running on.</span></span> 

| <span data-ttu-id="20628-168">**Zadania środowiska**</span><span class="sxs-lookup"><span data-stu-id="20628-168">**Environment Task**</span></span> | <span data-ttu-id="20628-169">**Cloud Services**</span><span class="sxs-lookup"><span data-stu-id="20628-169">**Cloud Services**</span></span> | <span data-ttu-id="20628-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="20628-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="20628-171">Ustawienia konfiguracji i powiadomienia o zmianie</span><span class="sxs-lookup"><span data-stu-id="20628-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="20628-172">Magazyn lokalny</span><span class="sxs-lookup"><span data-stu-id="20628-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="20628-173">Informacje o punkcie końcowym</span><span class="sxs-lookup"><span data-stu-id="20628-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="20628-174">Bieżące wystąpienie:`RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="20628-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="20628-175">Inne role i wystąpienie:`RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="20628-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="20628-176">`NodeContext`dla bieżącego adresu węzła</span><span class="sxs-lookup"><span data-stu-id="20628-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="20628-177">`FabricClient`i `ServicePartitionResolver` do odnajdywania punktu końcowego usługi</span><span class="sxs-lookup"><span data-stu-id="20628-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="20628-178">Emulacja środowiska</span><span class="sxs-lookup"><span data-stu-id="20628-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="20628-179">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="20628-179">N/A</span></span> |
| <span data-ttu-id="20628-180">Zdarzenie zmiany jednoczesnych</span><span class="sxs-lookup"><span data-stu-id="20628-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="20628-181">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="20628-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="20628-182">Ustawienia konfiguracji</span><span class="sxs-lookup"><span data-stu-id="20628-182">Configuration settings</span></span>
<span data-ttu-id="20628-183">Ustawienia konfiguracji usług w chmurze są ustawiane dla roli maszyny Wirtualnej i dotyczą wszystkich wystąpień tej roli maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="20628-183">Configuration settings in Cloud Services are set for a VM role and apply to all instances of that VM role.</span></span> <span data-ttu-id="20628-184">Te ustawienia są pary klucz wartość ustawiona w plikach ServiceConfiguration.*.cscfg i jest dostępny bezpośrednio za pomocą RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="20628-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="20628-185">W sieci szkieletowej usług ustawienia stosowane osobno do każdej usługi i dla każdej aplikacji, a nie do maszyny Wirtualnej, ponieważ maszyna wirtualna może obsługiwać wiele usług i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="20628-185">In Service Fabric, settings apply individually to each service and to each application, rather than to a VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="20628-186">Usługa składa się z trzech pakietów:</span><span class="sxs-lookup"><span data-stu-id="20628-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="20628-187">**Kod:** zawiera pliki wykonywalne usługi, plików binarnych biblioteki dll i inne pliki wymagane do uruchomienia usługę.</span><span class="sxs-lookup"><span data-stu-id="20628-187">**Code:** contains the service executables, binaries, DLLs, and any other files a service needs to run.</span></span>
* <span data-ttu-id="20628-188">**Config:** wszystkich plików konfiguracji i ustawień usługi.</span><span class="sxs-lookup"><span data-stu-id="20628-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="20628-189">**Dane:** plików statycznych danych skojarzony z usługą.</span><span class="sxs-lookup"><span data-stu-id="20628-189">**Data:** static data files associated with the service.</span></span>

<span data-ttu-id="20628-190">Każdy z tych pakietów można niezależnie określonej wersji, jak i uaktualnionych.</span><span class="sxs-lookup"><span data-stu-id="20628-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="20628-191">Podobnie jak usługi w chmurze, pakietu konfiguracji można uzyskać programistycznie przy użyciu interfejsu API i zdarzenia są dostępne do powiadamiania usługi o zmianie konfiguracji pakietu.</span><span class="sxs-lookup"><span data-stu-id="20628-191">Similar to Cloud Services, a config package can be accessed programmatically through an API and events are available to notify the service of a config package change.</span></span> <span data-ttu-id="20628-192">Pliku Settings.xml może służyć do kluczy i wartości konfiguracji i dostęp programistyczny podobne w sekcji Ustawienia aplikacji w pliku App.config.</span><span class="sxs-lookup"><span data-stu-id="20628-192">A Settings.xml file can be used for key-value configuration and programmatic access similar to the app settings section of an App.config file.</span></span> <span data-ttu-id="20628-193">Jednak w przeciwieństwie do usługi w chmurze, pakiet konfiguracji sieci szkieletowej usług może zawierać pliki konfiguracji w dowolnym formacie XML, JSON, yaml programu lub niestandardowy format binarny.</span><span class="sxs-lookup"><span data-stu-id="20628-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="20628-194">Uzyskiwanie dostępu do konfiguracji</span><span class="sxs-lookup"><span data-stu-id="20628-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="20628-195">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="20628-195">Cloud Services</span></span>
<span data-ttu-id="20628-196">Ustawienia konfiguracji z ServiceConfiguration.*.cscfg jest możliwy za pośrednictwem `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="20628-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="20628-197">Te ustawienia są ogólnie dostępna dla wszystkich wystąpień roli w ramach tego samego wdrożenia usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="20628-197">These settings are globally available to all role instances in the same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="20628-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="20628-198">Service Fabric</span></span>
<span data-ttu-id="20628-199">Każda usługa ma własny pakiet konfiguracji poszczególnych.</span><span class="sxs-lookup"><span data-stu-id="20628-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="20628-200">Nie istnieje wbudowany mechanizm dla globalne ustawienia konfiguracji dostępne przez wszystkie aplikacje w klastrze.</span><span class="sxs-lookup"><span data-stu-id="20628-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="20628-201">Podczas korzystania z usługi Service Fabric specjalne Settings.xml konfiguracji pliku w ramach pakietu konfiguracji wartości w pliku Settings.xml można zastąpić na poziomie aplikacji, umożliwiając ustawień konfiguracji na poziomie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="20628-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at the application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="20628-202">Ustawienia konfiguracji są dostępu w ramach każdego wystąpienia usługi za pośrednictwem usługi `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="20628-202">Configuration settings are accesses within each service instance through the service's `CodePackageActivationContext`.</span></span>

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

### <a name="configuration-update-events"></a><span data-ttu-id="20628-203">Zdarzenia aktualizacji konfiguracji</span><span class="sxs-lookup"><span data-stu-id="20628-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="20628-204">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="20628-204">Cloud Services</span></span>
<span data-ttu-id="20628-205">`RoleEnvironment.Changed` Zdarzeń jest używana do powiadamiania wszystkich wystąpień roli w przypadku zmiany w środowisku, np. o zmianie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="20628-205">The `RoleEnvironment.Changed` event is used to notify all role instances when a change occurs in the environment, such as a configuration change.</span></span> <span data-ttu-id="20628-206">Służy to użycie konfiguracji aktualizacji bez odtwarzania wystąpień roli lub ponowne uruchomienie procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="20628-206">This is used to consume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get the list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="20628-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="20628-207">Service Fabric</span></span>
<span data-ttu-id="20628-208">Poszczególnych typów pakietu trzy usługi kodu, konfiguracji i danych - ma zdarzeń, które powiadamiają o wystąpieniu usługi, gdy pakiet zostanie zaktualizowany, dodany lub usunięty.</span><span class="sxs-lookup"><span data-stu-id="20628-208">Each of the three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="20628-209">Usługa może zawierać wielu pakietów każdego typu.</span><span class="sxs-lookup"><span data-stu-id="20628-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="20628-210">Na przykład usługa może mieć wielu pakietów konfiguracji każdego indywidualnie numerów wersji i możliwej.</span><span class="sxs-lookup"><span data-stu-id="20628-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="20628-211">Te zdarzenia są dostępne zużyje zmiany pakietów usług bez konieczności ponownego uruchamiania wystąpienie usługi.</span><span class="sxs-lookup"><span data-stu-id="20628-211">These events are available to consume changes in service packages without restarting the service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="20628-212">Zadania uruchamiania</span><span class="sxs-lookup"><span data-stu-id="20628-212">Startup tasks</span></span>
<span data-ttu-id="20628-213">Uruchamianie zadania są działaniach wykonywanych przed uruchomieniem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="20628-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="20628-214">Zadanie uruchamiania jest zwykle używany do uruchamiania skryptów instalacji, korzystając z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="20628-214">A startup task is typically used to run setup scripts using elevated privileges.</span></span> <span data-ttu-id="20628-215">Usługa Service Fabric i usług w chmurze obsługuje zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="20628-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="20628-216">Główna różnica polega na tym, że usług w chmurze, zadanie uruchamiania jest związany z maszyny Wirtualnej, ponieważ jest ona częścią wystąpienia roli, natomiast w sieci szkieletowej usług zadanie uruchamiania jest związany z usługą, które nie są powiązane do żadnej określonej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="20628-216">The main difference is that in Cloud Services, a startup task is tied to a VM because it is part of a role instance, whereas in Service Fabric a startup task is tied to a service, which is not tied to any particular VM.</span></span>

| <span data-ttu-id="20628-217">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="20628-217">Cloud Services</span></span> | <span data-ttu-id="20628-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="20628-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="20628-219">Lokalizacja konfiguracji</span><span class="sxs-lookup"><span data-stu-id="20628-219">Configuration location</span></span> |<span data-ttu-id="20628-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="20628-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="20628-221">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="20628-221">Privileges</span></span> |<span data-ttu-id="20628-222">"ograniczony" lub "z podwyższonym poziomem uprawnień"</span><span class="sxs-lookup"><span data-stu-id="20628-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="20628-223">Sekwencjonowanie</span><span class="sxs-lookup"><span data-stu-id="20628-223">Sequencing</span></span> |<span data-ttu-id="20628-224">"prosty", "tła", "narzędzia"</span><span class="sxs-lookup"><span data-stu-id="20628-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="20628-225">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="20628-225">Cloud Services</span></span>
<span data-ttu-id="20628-226">Usług w chmurze punktu wejścia uruchamiania jest skonfigurowany dla każdej roli w ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="20628-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

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

### <a name="service-fabric"></a><span data-ttu-id="20628-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="20628-227">Service Fabric</span></span>
<span data-ttu-id="20628-228">W sieci szkieletowej usług punktu wejścia uruchamiania jest skonfigurowany dla usługi w pliku ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="20628-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

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

## <a name="a-note-about-development-environment"></a><span data-ttu-id="20628-229">Uwagi dotyczące środowiska deweloperskiego</span><span class="sxs-lookup"><span data-stu-id="20628-229">A note about development environment</span></span>
<span data-ttu-id="20628-230">Usługi Service Fabric i usług w chmurze są zintegrowane z programem Visual Studio z szablonów projektu i obsługę debugowania, konfigurowanie i wdrażanie, zarówno lokalnie, jak i na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="20628-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and to Azure.</span></span> <span data-ttu-id="20628-231">Usługa Service Fabric i usług w chmurze udostępniają rozwoju lokalnego środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="20628-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="20628-232">Różnica polega na podczas rozwoju środowiska uruchomieniowego usługi w chmurze emuluje środowiska platformy Azure, na którym jest uruchomiony, Service Fabric nie korzysta z emulatora — używa pełne środowisko uruchomieniowe usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="20628-232">The difference is that while the Cloud Service development runtime emulates the Azure environment on which it runs, Service Fabric does not use an emulator - it uses the complete Service Fabric runtime.</span></span> <span data-ttu-id="20628-233">Środowisko sieci szkieletowej usług uruchomionych na komputerze deweloperskim lokalnego jest tym samym środowisku, który jest uruchamiany w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="20628-233">The Service Fabric environment you run on your local development machine is the same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20628-234">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="20628-234">Next steps</span></span>
<span data-ttu-id="20628-235">Przeczytaj więcej na temat usługi sieci szkieletowej usług niezawodnych i podstawowe różnice między usługi w chmurze i architektury aplikacji usługi Service Fabric, zrozumienie, jak korzystać z pełnego zestawu funkcji usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="20628-235">Read more about Service Fabric Reliable Services and the fundamental differences between Cloud Services and Service Fabric application architecture to understand how to take advantage of the full set of Service Fabric features.</span></span>

* [<span data-ttu-id="20628-236">Wprowadzenie do korzystania z usługi sieć szkieletowa niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="20628-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="20628-237">Przewodnik koncepcyjny różnice między usługami w chmurze i sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="20628-237">Conceptual guide to the differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
