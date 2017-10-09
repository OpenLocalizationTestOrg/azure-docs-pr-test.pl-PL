---
title: "aaaCommunication dla ról, usług w chmurze | Dokumentacja firmy Microsoft"
description: "Wystąpienia roli usług w chmurze ma zdefiniowanych punktów końcowych (http, https, tcp, udp) dla nich komunikujących się z hello poza lub między innych wystąpień roli."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7008a083-acbe-4fb8-ae60-b837ef971ca1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 1fb39215ceb8a3f0381ef5e108c1149de115ff8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="51fa2-103">Włącz komunikację dla wystąpień roli w systemie azure</span><span class="sxs-lookup"><span data-stu-id="51fa2-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="51fa2-104">Role usługi w chmurze komunikują się za pośrednictwem połączeń wewnętrznych i zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="51fa2-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="51fa2-105">Połączenia zewnętrzne są nazywane **wejściowych punktów końcowych** podczas połączenia wewnętrznego są nazywane **wewnętrznych punktów końcowych**.</span><span class="sxs-lookup"><span data-stu-id="51fa2-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="51fa2-106">W tym temacie opisano sposób toomodify hello [definicji usługi](cloud-services-model-and-package.md#csdef) toocreate punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="51fa2-106">This topic describes how toomodify hello [service definition](cloud-services-model-and-package.md#csdef) toocreate endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="51fa2-107">Wejściowy punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="51fa2-107">Input endpoint</span></span>
<span data-ttu-id="51fa2-108">wejściowy punkt końcowy Hello jest używany, gdy chcesz tooexpose toohello portu, poza.</span><span class="sxs-lookup"><span data-stu-id="51fa2-108">hello input endpoint is used when you want tooexpose a port toohello outside.</span></span> <span data-ttu-id="51fa2-109">Należy określić typ protokołu hello i port hello hello punktu końcowego, który następnie dotyczy obu hello zewnętrznych i wewnętrznych portów dla punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="51fa2-109">You specify hello protocol type and hello port of hello endpoint which then applies for both hello external and internal ports for hello endpoint.</span></span> <span data-ttu-id="51fa2-110">Jeśli chcesz, można określić inny port wewnętrzny dla punktu końcowego hello z hello [port lokalny](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) atrybutu.</span><span class="sxs-lookup"><span data-stu-id="51fa2-110">If you want, you can specify a different internal port for hello endpoint with hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="51fa2-111">wejściowy punkt końcowy Hello służy hello następujące protokoły: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="51fa2-111">hello input endpoint can use hello following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="51fa2-112">toocreate wejściowy punkt końcowy, Dodaj hello **InputEndpoint** toohello element podrzędny **punkty końcowe** element roli sieci web lub procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="51fa2-112">toocreate an input endpoint, add hello **InputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="51fa2-113">Wystąpienie wejściowy punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="51fa2-113">Instance input endpoint</span></span>
<span data-ttu-id="51fa2-114">Wystąpienie wejściowych punktów końcowych są podobne tooinput punktów końcowych, ale pozwala mapować określone porty publicznych dla poszczególnych wystąpień poszczególnych ról przy użyciu portu przekazywania na powitania modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="51fa2-114">Instance input endpoints are similar tooinput endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on hello load balancer.</span></span> <span data-ttu-id="51fa2-115">Można określić jeden port publicznych, lub zakresem portów.</span><span class="sxs-lookup"><span data-stu-id="51fa2-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="51fa2-116">wejściowy punkt końcowy Hello wystąpienia można używać tylko **tcp** lub **udp** jako protokół hello.</span><span class="sxs-lookup"><span data-stu-id="51fa2-116">hello instance input endpoint can only use **tcp** or **udp** as hello protocol.</span></span>

<span data-ttu-id="51fa2-117">toocreate wystąpienia wejściowy punkt końcowy, Dodaj hello **InstanceInputEndpoint** toohello element podrzędny **punkty końcowe** element roli sieci web lub procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="51fa2-117">toocreate an instance input endpoint, add hello **InstanceInputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="51fa2-118">Wewnętrzny punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="51fa2-118">Internal endpoint</span></span>
<span data-ttu-id="51fa2-119">Wewnętrznych punktów końcowych są dostępne dla komunikacji wystąpienie do wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="51fa2-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="51fa2-120">Hello port jest opcjonalny i pominięcie port dynamiczny jest przypisany toohello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="51fa2-120">hello port is optional and if omitted, a dynamic port is assigned toohello endpoint.</span></span> <span data-ttu-id="51fa2-121">Zakres portów może służyć.</span><span class="sxs-lookup"><span data-stu-id="51fa2-121">A port range can be used.</span></span> <span data-ttu-id="51fa2-122">Brak limitu pięciu wewnętrznych punktów końcowych dla każdej roli.</span><span class="sxs-lookup"><span data-stu-id="51fa2-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="51fa2-123">Wewnętrzny punkt końcowy Hello służy hello następujące protokoły: **http, tcp, udp, wszelkie**.</span><span class="sxs-lookup"><span data-stu-id="51fa2-123">hello internal endpoint can use hello following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="51fa2-124">toocreate wewnętrzny wejściowy punkt końcowy, Dodaj hello **InternalEndpoint** toohello element podrzędny **punkty końcowe** element roli sieci web lub procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="51fa2-124">toocreate an internal input endpoint, add hello **InternalEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="51fa2-125">Można również użyć zakresu portów.</span><span class="sxs-lookup"><span data-stu-id="51fa2-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="51fa2-126">Vs role proces roboczy. Role sieci Web</span><span class="sxs-lookup"><span data-stu-id="51fa2-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="51fa2-127">Brak jednego niewielkiej różnicy z punktami końcowymi, podczas pracy z ról sieć web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="51fa2-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="51fa2-128">Witaj roli sieci web musi mieć co najmniej jeden wejściowy punkt końcowy za pomocą hello **HTTP** protokołu.</span><span class="sxs-lookup"><span data-stu-id="51fa2-128">hello web role must have at minimum a single input endpoint using hello **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a><span data-ttu-id="51fa2-129">Przy użyciu hello zestawu .NET SDK tooaccess punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="51fa2-129">Using hello .NET SDK tooaccess an endpoint</span></span>
<span data-ttu-id="51fa2-130">Hello biblioteki zarządzane Azure udostępnia metody dla toocommunicate wystąpień roli w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="51fa2-130">hello Azure Managed Library provides methods for role instances toocommunicate at runtime.</span></span> <span data-ttu-id="51fa2-131">Z kodu uruchomionego w wystąpieniu roli można pobrać informacji na temat hello istnienie innych wystąpień roli i ich punkty końcowe, a także informacje o hello bieżącego wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="51fa2-131">From code running within a role instance, you can retrieve information about hello existence of other role instances and their endpoints, as well as information about hello current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="51fa2-132">Można tylko pobieranie informacji na temat wystąpień roli, które działają w usługi w chmurze i definiującą co najmniej jeden wewnętrzny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="51fa2-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="51fa2-133">Nie można uzyskać danych dotyczących wystąpień roli w innej usługi.</span><span class="sxs-lookup"><span data-stu-id="51fa2-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="51fa2-134">Można użyć hello [wystąpień](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) właściwości tooretrieve wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="51fa2-134">You can use hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property tooretrieve instances of a role.</span></span> <span data-ttu-id="51fa2-135">Należy najpierw użyć hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn bieżącej roli toohello odwołanie do wystąpienia, a następnie użyj hello [roli](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) tooreturn właściwości roli toohello odwołanie do samej siebie.</span><span class="sxs-lookup"><span data-stu-id="51fa2-135">First use hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn a reference toohello current role instance, and then use hello [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property tooreturn a reference toohello role itself.</span></span>

<span data-ttu-id="51fa2-136">Po ustanowieniu połączenia wystąpienia roli tooa programowo przy użyciu zestawu .NET SDK hello jest stosunkowo łatwa tooaccess hello — informacje o punkcie końcowym.</span><span class="sxs-lookup"><span data-stu-id="51fa2-136">When you connect tooa role instance programmatically through hello .NET SDK, it's relatively easy tooaccess hello endpoint information.</span></span> <span data-ttu-id="51fa2-137">Na przykład po nawiązaniu połączenia już tooa określonej roli w środowisku, można uzyskać portu hello określonego punktu końcowego o tym kodzie:</span><span class="sxs-lookup"><span data-stu-id="51fa2-137">For example, after you've already connected tooa specific role environment, you can get hello port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="51fa2-138">Witaj **wystąpień** właściwość zwraca kolekcję **RoleInstance** obiektów.</span><span class="sxs-lookup"><span data-stu-id="51fa2-138">hello **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="51fa2-139">Ta kolekcja zawsze zawiera hello bieżącego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="51fa2-139">This collection always contains hello current instance.</span></span> <span data-ttu-id="51fa2-140">Jeśli rola hello nie definiuje wewnętrzny punkt końcowy, hello kolekcja zawiera hello bieżącego wystąpienia, ale żadne inne wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="51fa2-140">If hello role does not define an internal endpoint, hello collection includes hello current instance but no other instances.</span></span> <span data-ttu-id="51fa2-141">Witaj liczby wystąpień roli w kolekcji hello będzie zawsze 1 w przypadku hello, których nie wewnętrzny punkt końcowy jest zdefiniowana dla roli hello.</span><span class="sxs-lookup"><span data-stu-id="51fa2-141">hello number of role instances in hello collection will always be 1 in hello case where no internal endpoint is defined for hello role.</span></span> <span data-ttu-id="51fa2-142">Jeśli rola hello definiuje wewnętrzny punkt końcowy, jego wystąpienia są wykrywalny w czasie wykonywania, a hello liczbę wystąpień w kolekcji hello będzie odpowiadać toohello liczbę wystąpień określone dla roli hello w pliku konfiguracji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="51fa2-142">If hello role defines an internal endpoint, its instances are discoverable at runtime, and hello number of instances in hello collection will correspond toohello number of instances specified for hello role in hello service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="51fa2-143">Hello Azure zarządzane biblioteki nie zapewnia sposób określania kondycji hello innych wystąpień roli, ale jeśli usługa wymaga tej funkcji można wdrożyć w takiej oceny kondycji.</span><span class="sxs-lookup"><span data-stu-id="51fa2-143">hello Azure Managed Library does not provide a means of determining hello health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="51fa2-144">Można użyć [diagnostyki Azure](cloud-services-dotnet-diagnostics.md) tooobtain informacji o uruchomionych wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="51fa2-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="51fa2-145">numer portu hello toodetermine wewnętrznego punktu końcowego wystąpienia roli, można użyć hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn właściwość dotyczy obiekt słownika zawierający nazwy punktu końcowego i ich odpowiedniego adresu IP i portów.</span><span class="sxs-lookup"><span data-stu-id="51fa2-145">toodetermine hello port number for an internal endpoint on a role instance, you can use hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property tooreturn a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="51fa2-146">Witaj [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) właściwość zwraca hello adresu IP i portu dla określonego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="51fa2-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns hello IP address and port for a specified endpoint.</span></span> <span data-ttu-id="51fa2-147">Witaj **PublicIPEndpoint** właściwość zwraca hello port punktu końcowego o zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="51fa2-147">hello **PublicIPEndpoint** property returns hello port for a load balanced endpoint.</span></span> <span data-ttu-id="51fa2-148">części adresu IP Hello hello **PublicIPEndpoint** właściwość nie jest używana.</span><span class="sxs-lookup"><span data-stu-id="51fa2-148">hello IP address portion of hello **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="51fa2-149">Oto przykład, który iteruje po wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="51fa2-149">Here is an example that iterates role instances.</span></span>

```csharp
foreach (RoleInstance roleInst in RoleEnvironment.CurrentRoleInstance.Role.Instances)
{
    Trace.WriteLine("Instance ID: " + roleInst.Id);
    foreach (RoleInstanceEndpoint roleInstEndpoint in roleInst.InstanceEndpoints.Values)
    {
        Trace.WriteLine("Instance endpoint IP address and port: " + roleInstEndpoint.IPEndpoint);
    }
}
```

<span data-ttu-id="51fa2-150">Oto przykład roli procesu roboczego, która pobiera punktu końcowego hello udostępniane za pośrednictwem definicji usługi hello i rozpoczyna nasłuchiwanie dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="51fa2-150">Here is an example of a worker role that gets hello endpoint exposed through hello service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="51fa2-151">Ten kod działa tylko dla wdrożonej usługi.</span><span class="sxs-lookup"><span data-stu-id="51fa2-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="51fa2-152">Podczas uruchamiania w hello Azure obliczeniowe emulatora, usługi elementów konfiguracji, które utworzyć bezpośredniej portów punkty końcowe (**InstanceInputEndpoint** elementy) są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="51fa2-152">When running in hello Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
> 
> 

```csharp
using System;
using System.Diagnostics;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Threading;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Diagnostics;
using Microsoft.WindowsAzure.ServiceRuntime;
using Microsoft.WindowsAzure.StorageClient;

namespace WorkerRole1
{
  public class WorkerRole : RoleEntryPoint
  {
    public override void Run()
    {
      try
      {
        // Initialize method-wide variables
        var epName = "Endpoint1";
        var roleInstance = RoleEnvironment.CurrentRoleInstance;

        // Identify direct communication port
        var myPublicEp = roleInstance.InstanceEndpoints[epName].PublicIPEndpoint;
        Trace.TraceInformation("IP:{0}, Port:{1}", myPublicEp.Address, myPublicEp.Port);

        // Identify public endpoint
        var myInternalEp = roleInstance.InstanceEndpoints[epName].IPEndpoint;

        // Create socket listener
        var listener = new Socket(
          myInternalEp.AddressFamily, SocketType.Stream, ProtocolType.Tcp);

        // Bind socket listener toointernal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block hello thread and wait for a client request
          Socket handler = listener.Accept();
          Trace.TraceInformation("Client request received.");

          // Define body of socket handler
          var handlerThread = new Thread(
            new ParameterizedThreadStart(h =>
            {
              var socket = h as Socket;
              Trace.TraceInformation("Local:{0} Remote{1}",
                socket.LocalEndPoint, socket.RemoteEndPoint);

              // Shut down and close socket
              socket.Shutdown(SocketShutdown.Both);
              socket.Close();
            }
          ));

          // Start socket handler on new thread
          handlerThread.Start(handler);
        }
      }
      catch (Exception e)
      {
        Trace.TraceError("Caught exception in run. Details: {0}", e);
      }
    }

    public override bool OnStart()
    {
      // Set hello maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-toocontrol-role-communication"></a><span data-ttu-id="51fa2-153">Ruch reguły toocontrol roli komunikacji sieciowej</span><span class="sxs-lookup"><span data-stu-id="51fa2-153">Network traffic rules toocontrol role communication</span></span>
<span data-ttu-id="51fa2-154">Po zdefiniowaniu wewnętrznych punktów końcowych, możesz dodać toocontrol reguły (oparte na powitania punktów końcowych, które zostały utworzone) ruchu sieciowego jak wystąpień roli może komunikować się ze sobą.</span><span class="sxs-lookup"><span data-stu-id="51fa2-154">After you define internal endpoints, you can add network traffic rules (based on hello endpoints that you created) toocontrol how role instances can communicate with each other.</span></span> <span data-ttu-id="51fa2-155">Witaj poniższym diagramie przedstawiono kilka typowych scenariuszy kontroli komunikacji roli:</span><span class="sxs-lookup"><span data-stu-id="51fa2-155">hello following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="51fa2-156">![Scenariusze reguły ruchu sieciowego](./media/cloud-services-enable-communication-role-instances/scenarios.png "scenariusze reguły ruchu sieciowego")</span><span class="sxs-lookup"><span data-stu-id="51fa2-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="51fa2-157">Witaj Poniższy przykładowy kod przedstawia definicje ról dla ról hello pokazano hello poprzedni diagram.</span><span class="sxs-lookup"><span data-stu-id="51fa2-157">hello following code example shows role definitions for hello roles shown in hello previous diagram.</span></span> <span data-ttu-id="51fa2-158">Każda definicja roli obejmuje co najmniej jeden wewnętrzny punkt końcowy zdefiniowany:</span><span class="sxs-lookup"><span data-stu-id="51fa2-158">Each role definition includes at least one internal endpoint defined:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalTCP1" protocol="tcp" />
    </Endpoints>
  </WebRole>
  <WorkerRole name="WorkerRole1">
    <Endpoints>
      <InternalEndpoint name="InternalTCP2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
  <WorkerRole name="WorkerRole2">
    <Endpoints>
      <InternalEndpoint name="InternalTCP3" protocol="tcp" />
      <InternalEndpoint name="InternalTCP4" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

> [!NOTE]
> <span data-ttu-id="51fa2-159">Ograniczenia komunikacji między rolami może wystąpić z wewnętrznych punktów końcowych zarówno stały i przypisywane automatycznie portów.</span><span class="sxs-lookup"><span data-stu-id="51fa2-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="51fa2-160">Domyślnie po zdefiniowaniu wewnętrzny punkt końcowy komunikacji mogą przepływać z dowolnej roli toohello wewnętrzny punkt końcowy roli bez ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="51fa2-160">By default, after an internal endpoint is defined, communication can flow from any role toohello internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="51fa2-161">Komunikacja toorestrict, należy dodać **NetworkTrafficRules** toohello elementu **ServiceDefinition** elementu w pliku definicji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="51fa2-161">toorestrict communication, you must add a **NetworkTrafficRules** element toohello **ServiceDefinition** element in hello service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="51fa2-162">Scenariusz 1</span><span class="sxs-lookup"><span data-stu-id="51fa2-162">Scenario 1</span></span>
<span data-ttu-id="51fa2-163">Zezwalaj tylko na ruch sieciowy z **WebRole1** za**WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="51fa2-163">Only allow network traffic from **WebRole1** too**WorkerRole1**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-2"></a><span data-ttu-id="51fa2-164">Scenariusz 2</span><span class="sxs-lookup"><span data-stu-id="51fa2-164">Scenario 2</span></span>
<span data-ttu-id="51fa2-165">Zezwala na ruch sieciowy z **WebRole1** za**WorkerRole1** i **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="51fa2-165">Only allows network traffic from **WebRole1** too**WorkerRole1** and **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-3"></a><span data-ttu-id="51fa2-166">Scenariusz 3</span><span class="sxs-lookup"><span data-stu-id="51fa2-166">Scenario 3</span></span>
<span data-ttu-id="51fa2-167">Zezwala na ruch sieciowy z **WebRole1** za**WorkerRole1**, i **WorkerRole1** za**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="51fa2-167">Only allows network traffic from **WebRole1** too**WorkerRole1**, and **WorkerRole1** too**WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-4"></a><span data-ttu-id="51fa2-168">Scenariusz 4</span><span class="sxs-lookup"><span data-stu-id="51fa2-168">Scenario 4</span></span>
<span data-ttu-id="51fa2-169">Zezwala na ruch sieciowy z **WebRole1** za**WorkerRole1**, **WebRole1** za**WorkerRole2**, i  **WorkerRole1** za**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="51fa2-169">Only allows network traffic from **WebRole1** too**WorkerRole1**, **WebRole1** too**WorkerRole2**, and **WorkerRole1** too**WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP4" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

<span data-ttu-id="51fa2-170">Znajduje się odwołanie do schematu XML dla elementów hello powyżej [tutaj](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="51fa2-170">An XML schema reference for hello elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51fa2-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="51fa2-171">Next steps</span></span>
<span data-ttu-id="51fa2-172">Dowiedz się więcej na temat hello usługi w chmurze [modelu](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="51fa2-172">Read more about hello Cloud Service [model](cloud-services-model-and-package.md).</span></span>

