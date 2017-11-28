---
title: "Komunikacji dla ról, usług w chmurze | Dokumentacja firmy Microsoft"
description: "Wystąpienia roli usług w chmurze ma zdefiniowanych punktów końcowych (http, https, tcp, udp) dla nich komunikujących się z zewnątrz lub między innych wystąpień roli."
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
ms.openlocfilehash: 8e171d56bb67c971337fa383014988074ec828b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="3d8a5-103">Włącz komunikację dla wystąpień roli w systemie azure</span><span class="sxs-lookup"><span data-stu-id="3d8a5-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="3d8a5-104">Role usługi w chmurze komunikują się za pośrednictwem połączeń wewnętrznych i zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="3d8a5-105">Połączenia zewnętrzne są nazywane **wejściowych punktów końcowych** podczas połączenia wewnętrznego są nazywane **wewnętrznych punktów końcowych**.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="3d8a5-106">W tym temacie opisano sposób modyfikowania [definicji usługi](cloud-services-model-and-package.md#csdef) do utworzenia punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="3d8a5-107">Wejściowy punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="3d8a5-107">Input endpoint</span></span>
<span data-ttu-id="3d8a5-108">Wejściowy punkt końcowy jest używany, gdy chcesz udostępnić portu na zewnątrz.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-108">The input endpoint is used when you want to expose a port to the outside.</span></span> <span data-ttu-id="3d8a5-109">Należy określić typ protokół i port punktu końcowego, który następnie dotyczy zarówno wewnętrznych i zewnętrznych portów dla punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span></span> <span data-ttu-id="3d8a5-110">Jeśli chcesz, można określić inny port wewnętrzny dla punktu końcowego o [port lokalny](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) atrybutu.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="3d8a5-111">Wejściowy punkt końcowy, można użyć następujących protokołów: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="3d8a5-112">Aby utworzyć wejściowy punkt końcowy, dodać **InputEndpoint** elementu podrzędnego do **punkty końcowe** element roli sieci web lub procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="3d8a5-113">Wystąpienie wejściowy punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="3d8a5-113">Instance input endpoint</span></span>
<span data-ttu-id="3d8a5-114">Wystąpienie wejściowych punktów końcowych są podobne do danych wejściowych punktów końcowych, ale można mapować określone porty publicznych dla poszczególnych wystąpień poszczególnych ról przy użyciu portu przekazywania modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span></span> <span data-ttu-id="3d8a5-115">Można określić jeden port publicznych, lub zakresem portów.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="3d8a5-116">Wejściowy punkt końcowy wystąpienia można używać tylko **tcp** lub **udp** jako protokół.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span></span>

<span data-ttu-id="3d8a5-117">Aby utworzyć wystąpienie wejściowy punkt końcowy, Dodaj **InstanceInputEndpoint** elementu podrzędnego do **punkty końcowe** element roli sieci web lub procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="3d8a5-118">Wewnętrzny punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="3d8a5-118">Internal endpoint</span></span>
<span data-ttu-id="3d8a5-119">Wewnętrznych punktów końcowych są dostępne dla komunikacji wystąpienie do wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="3d8a5-120">Port jest opcjonalna i pominięcie port dynamiczny jest przypisana do punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span></span> <span data-ttu-id="3d8a5-121">Zakres portów może służyć.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-121">A port range can be used.</span></span> <span data-ttu-id="3d8a5-122">Brak limitu pięciu wewnętrznych punktów końcowych dla każdej roli.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="3d8a5-123">Wewnętrzny punkt końcowy, można użyć następujących protokołów: **http, tcp, udp, wszelkie**.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="3d8a5-124">Aby utworzyć wewnętrznego wejściowy punkt końcowy, Dodaj **InternalEndpoint** elementu podrzędnego do **punkty końcowe** element roli sieci web lub procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="3d8a5-125">Można również użyć zakresu portów.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="3d8a5-126">Vs role proces roboczy. Role sieci Web</span><span class="sxs-lookup"><span data-stu-id="3d8a5-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="3d8a5-127">Brak jednego niewielkiej różnicy z punktami końcowymi, podczas pracy z ról sieć web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="3d8a5-128">Rola sieci web musi mieć co najmniej jeden wejściowy punkt końcowy za pomocą **HTTP** protokołu.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after the first InputEndPoint -->
</Endpoints>
```

## <a name="using-the-net-sdk-to-access-an-endpoint"></a><span data-ttu-id="3d8a5-129">Otwieranie punktu końcowego za pomocą zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3d8a5-129">Using the .NET SDK to access an endpoint</span></span>
<span data-ttu-id="3d8a5-130">Biblioteki zarządzane Azure udostępnia metody dla wystąpień roli do komunikacji w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span></span> <span data-ttu-id="3d8a5-131">Z kodu uruchomionego w wystąpieniu roli można pobrać informacji na temat innych wystąpień roli i ich punktów końcowych, a także informacje o bieżącym wystąpieniu roli.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="3d8a5-132">Można tylko pobieranie informacji na temat wystąpień roli, które działają w usługi w chmurze i definiującą co najmniej jeden wewnętrzny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="3d8a5-133">Nie można uzyskać danych dotyczących wystąpień roli w innej usługi.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="3d8a5-134">Można użyć [wystąpień](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) właściwości można pobrać wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span></span> <span data-ttu-id="3d8a5-135">Należy najpierw użyć [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) zwraca odwołanie do bieżącego wystąpienia roli, a następnie użyć [roli](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) właściwość zwraca odwołanie do samej siebie roli.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span></span>

<span data-ttu-id="3d8a5-136">Po podłączeniu do wystąpienia roli, programowo przy użyciu zestawu .NET SDK jest stosunkowo łatwa do uzyskania dostępu do informacji punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span></span> <span data-ttu-id="3d8a5-137">Na przykład po nawiązaniu połączenia już w środowisku określoną rolę, możesz uzyskać portu określonego punktu końcowego o tym kodzie:</span><span class="sxs-lookup"><span data-stu-id="3d8a5-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="3d8a5-138">**Wystąpień** właściwość zwraca kolekcję **RoleInstance** obiektów.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-138">The **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="3d8a5-139">Ta kolekcja zawsze zawiera bieżącego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-139">This collection always contains the current instance.</span></span> <span data-ttu-id="3d8a5-140">Jeśli rola nie ma zdefiniowanej wewnętrzny punkt końcowy, Kolekcja zawiera bieżącego wystąpienia, ale żadne inne wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span></span> <span data-ttu-id="3d8a5-141">Liczba wystąpień roli w kolekcji będą zawsze miały 1 w przypadku, gdy żaden wewnętrzny punkt końcowy jest zdefiniowany dla roli.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span></span> <span data-ttu-id="3d8a5-142">Jeśli rola definiuje wewnętrzny punkt końcowy, jego wystąpienia są wykrywalny w czasie wykonywania, a liczba wystąpień w kolekcji odpowiada liczba wystąpień określone dla roli w pliku konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="3d8a5-143">Biblioteki zarządzane Azure zapewnia sposób określania kondycji innych wystąpień roli, ale jeśli usługa wymaga tej funkcji można wdrożyć w takiej oceny kondycji.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="3d8a5-144">Można użyć [diagnostyki Azure](cloud-services-dotnet-diagnostics.md) można uzyskać informacji o uruchomionych wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="3d8a5-145">Aby określić numer portu wewnętrzny punkt końcowy w wystąpieniu roli, można użyć [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) właściwości, aby zwrócić obiekt słownika zawierający nazwy punktu końcowego i ich odpowiedniego adresu IP, adresy i porty.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="3d8a5-146">[IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) właściwość zwraca adres IP i port dla określonego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span></span> <span data-ttu-id="3d8a5-147">**PublicIPEndpoint** właściwość zwraca port punktu końcowego o zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span></span> <span data-ttu-id="3d8a5-148">Adres IP część **PublicIPEndpoint** właściwość nie jest używana.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="3d8a5-149">Oto przykład, który iteruje po wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="3d8a5-150">Oto przykład roli procesu roboczego, która pobiera punktu końcowego udostępniane za pośrednictwem definicji usługi i rozpoczyna nasłuchiwanie dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="3d8a5-151">Ten kod działa tylko dla wdrożonej usługi.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="3d8a5-152">Podczas uruchamiania w emulatorze obliczeniowe Azure, elementy konfiguracji, które utworzyć bezpośredniej portów punkty końcowe usługi (**InstanceInputEndpoint** elementy) są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

        // Bind socket listener to internal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block the thread and wait for a client request
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
      // Set the maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-to-control-role-communication"></a><span data-ttu-id="3d8a5-153">Reguły ruchu sieciowego do kontrolowania komunikacji roli</span><span class="sxs-lookup"><span data-stu-id="3d8a5-153">Network traffic rules to control role communication</span></span>
<span data-ttu-id="3d8a5-154">Po zdefiniowaniu wewnętrznych punktów końcowych, można dodać do kontroli, jak wystąpień roli może komunikować się ze sobą reguły ruchu sieciowego (w oparciu punktów końcowych, które zostały utworzone).</span><span class="sxs-lookup"><span data-stu-id="3d8a5-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span></span> <span data-ttu-id="3d8a5-155">Na poniższym diagramie przedstawiono kilka typowych scenariuszy kontroli komunikacji roli:</span><span class="sxs-lookup"><span data-stu-id="3d8a5-155">The following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="3d8a5-156">![Scenariusze reguły ruchu sieciowego](./media/cloud-services-enable-communication-role-instances/scenarios.png "scenariusze reguły ruchu sieciowego")</span><span class="sxs-lookup"><span data-stu-id="3d8a5-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="3d8a5-157">Poniższy przykład kodu pokazuje definicje ról dla ról przedstawione na diagramie poprzedniej.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-157">The following code example shows role definitions for the roles shown in the previous diagram.</span></span> <span data-ttu-id="3d8a5-158">Każda definicja roli obejmuje co najmniej jeden wewnętrzny punkt końcowy zdefiniowany:</span><span class="sxs-lookup"><span data-stu-id="3d8a5-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="3d8a5-159">Ograniczenia komunikacji między rolami może wystąpić z wewnętrznych punktów końcowych zarówno stały i przypisywane automatycznie portów.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="3d8a5-160">Domyślnie po zdefiniowaniu wewnętrzny punkt końcowy komunikacji mogą przepływać z dowolnej roli do wewnętrzny punkt końcowy roli bez ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="3d8a5-161">Aby ograniczyć komunikacji, należy dodać **NetworkTrafficRules** elementu **ServiceDefinition** elementu w pliku definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="3d8a5-162">Scenariusz 1</span><span class="sxs-lookup"><span data-stu-id="3d8a5-162">Scenario 1</span></span>
<span data-ttu-id="3d8a5-163">Zezwalaj tylko na ruch sieciowy z **WebRole1** do **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="3d8a5-164">Scenariusz 2</span><span class="sxs-lookup"><span data-stu-id="3d8a5-164">Scenario 2</span></span>
<span data-ttu-id="3d8a5-165">Zezwala na ruch sieciowy z **WebRole1** do **WorkerRole1** i **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="3d8a5-166">Scenariusz 3</span><span class="sxs-lookup"><span data-stu-id="3d8a5-166">Scenario 3</span></span>
<span data-ttu-id="3d8a5-167">Zezwala na ruch sieciowy z **WebRole1** do **WorkerRole1**, i **WorkerRole1** do **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="3d8a5-168">Scenariusz 4</span><span class="sxs-lookup"><span data-stu-id="3d8a5-168">Scenario 4</span></span>
<span data-ttu-id="3d8a5-169">Zezwala na ruch sieciowy z **WebRole1** do **WorkerRole1**, **WebRole1** do **WorkerRole2**, i **WorkerRole1**  do **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="3d8a5-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span></span>

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

<span data-ttu-id="3d8a5-170">Znajduje się odwołanie do schematu XML dla elementów użyta powyżej [tutaj](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d8a5-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d8a5-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d8a5-171">Next steps</span></span>
<span data-ttu-id="3d8a5-172">Dowiedz się więcej o usługę w chmurze [modelu](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="3d8a5-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span></span>

