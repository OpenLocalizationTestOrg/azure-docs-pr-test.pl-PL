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
# <a name="enable-communication-for-role-instances-in-azure"></a>Włącz komunikację dla wystąpień roli w systemie azure
Role usługi w chmurze komunikują się za pośrednictwem połączeń wewnętrznych i zewnętrznych. Połączenia zewnętrzne są nazywane **wejściowych punktów końcowych** podczas połączenia wewnętrznego są nazywane **wewnętrznych punktów końcowych**. W tym temacie opisano sposób toomodify hello [definicji usługi](cloud-services-model-and-package.md#csdef) toocreate punktów końcowych.

## <a name="input-endpoint"></a>Wejściowy punkt końcowy
wejściowy punkt końcowy Hello jest używany, gdy chcesz tooexpose toohello portu, poza. Należy określić typ protokołu hello i port hello hello punktu końcowego, który następnie dotyczy obu hello zewnętrznych i wewnętrznych portów dla punktu końcowego hello. Jeśli chcesz, można określić inny port wewnętrzny dla punktu końcowego hello z hello [port lokalny](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) atrybutu.

wejściowy punkt końcowy Hello służy hello następujące protokoły: **http, https, tcp, udp**.

toocreate wejściowy punkt końcowy, Dodaj hello **InputEndpoint** toohello element podrzędny **punkty końcowe** element roli sieci web lub procesu roboczego.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a>Wystąpienie wejściowy punkt końcowy
Wystąpienie wejściowych punktów końcowych są podobne tooinput punktów końcowych, ale pozwala mapować określone porty publicznych dla poszczególnych wystąpień poszczególnych ról przy użyciu portu przekazywania na powitania modułu równoważenia obciążenia. Można określić jeden port publicznych, lub zakresem portów.

wejściowy punkt końcowy Hello wystąpienia można używać tylko **tcp** lub **udp** jako protokół hello.

toocreate wystąpienia wejściowy punkt końcowy, Dodaj hello **InstanceInputEndpoint** toohello element podrzędny **punkty końcowe** element roli sieci web lub procesu roboczego.

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a>Wewnętrzny punkt końcowy
Wewnętrznych punktów końcowych są dostępne dla komunikacji wystąpienie do wystąpienia. Hello port jest opcjonalny i pominięcie port dynamiczny jest przypisany toohello punktu końcowego. Zakres portów może służyć. Brak limitu pięciu wewnętrznych punktów końcowych dla każdej roli.

Wewnętrzny punkt końcowy Hello służy hello następujące protokoły: **http, tcp, udp, wszelkie**.

toocreate wewnętrzny wejściowy punkt końcowy, Dodaj hello **InternalEndpoint** toohello element podrzędny **punkty końcowe** element roli sieci web lub procesu roboczego.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

Można również użyć zakresu portów.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a>Vs role proces roboczy. Role sieci Web
Brak jednego niewielkiej różnicy z punktami końcowymi, podczas pracy z ról sieć web i proces roboczy. Witaj roli sieci web musi mieć co najmniej jeden wejściowy punkt końcowy za pomocą hello **HTTP** protokołu.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a>Przy użyciu hello zestawu .NET SDK tooaccess punktu końcowego
Hello biblioteki zarządzane Azure udostępnia metody dla toocommunicate wystąpień roli w czasie wykonywania. Z kodu uruchomionego w wystąpieniu roli można pobrać informacji na temat hello istnienie innych wystąpień roli i ich punkty końcowe, a także informacje o hello bieżącego wystąpienia roli.

> [!NOTE]
> Można tylko pobieranie informacji na temat wystąpień roli, które działają w usługi w chmurze i definiującą co najmniej jeden wewnętrzny punkt końcowy. Nie można uzyskać danych dotyczących wystąpień roli w innej usługi.
> 
> 

Można użyć hello [wystąpień](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) właściwości tooretrieve wystąpień roli. Należy najpierw użyć hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn bieżącej roli toohello odwołanie do wystąpienia, a następnie użyj hello [roli](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) tooreturn właściwości roli toohello odwołanie do samej siebie.

Po ustanowieniu połączenia wystąpienia roli tooa programowo przy użyciu zestawu .NET SDK hello jest stosunkowo łatwa tooaccess hello — informacje o punkcie końcowym. Na przykład po nawiązaniu połączenia już tooa określonej roli w środowisku, można uzyskać portu hello określonego punktu końcowego o tym kodzie:

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

Witaj **wystąpień** właściwość zwraca kolekcję **RoleInstance** obiektów. Ta kolekcja zawsze zawiera hello bieżącego wystąpienia. Jeśli rola hello nie definiuje wewnętrzny punkt końcowy, hello kolekcja zawiera hello bieżącego wystąpienia, ale żadne inne wystąpienia. Witaj liczby wystąpień roli w kolekcji hello będzie zawsze 1 w przypadku hello, których nie wewnętrzny punkt końcowy jest zdefiniowana dla roli hello. Jeśli rola hello definiuje wewnętrzny punkt końcowy, jego wystąpienia są wykrywalny w czasie wykonywania, a hello liczbę wystąpień w kolekcji hello będzie odpowiadać toohello liczbę wystąpień określone dla roli hello w pliku konfiguracji usługi hello.

> [!NOTE]
> Hello Azure zarządzane biblioteki nie zapewnia sposób określania kondycji hello innych wystąpień roli, ale jeśli usługa wymaga tej funkcji można wdrożyć w takiej oceny kondycji. Można użyć [diagnostyki Azure](cloud-services-dotnet-diagnostics.md) tooobtain informacji o uruchomionych wystąpień roli.
> 
> 

numer portu hello toodetermine wewnętrznego punktu końcowego wystąpienia roli, można użyć hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn właściwość dotyczy obiekt słownika zawierający nazwy punktu końcowego i ich odpowiedniego adresu IP i portów. Witaj [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) właściwość zwraca hello adresu IP i portu dla określonego punktu końcowego. Witaj **PublicIPEndpoint** właściwość zwraca hello port punktu końcowego o zrównoważonym obciążeniu. części adresu IP Hello hello **PublicIPEndpoint** właściwość nie jest używana.

Oto przykład, który iteruje po wystąpień roli.

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

Oto przykład roli procesu roboczego, która pobiera punktu końcowego hello udostępniane za pośrednictwem definicji usługi hello i rozpoczyna nasłuchiwanie dla połączenia.

> [!WARNING]
> Ten kod działa tylko dla wdrożonej usługi. Podczas uruchamiania w hello Azure obliczeniowe emulatora, usługi elementów konfiguracji, które utworzyć bezpośredniej portów punkty końcowe (**InstanceInputEndpoint** elementy) są ignorowane.
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

## <a name="network-traffic-rules-toocontrol-role-communication"></a>Ruch reguły toocontrol roli komunikacji sieciowej
Po zdefiniowaniu wewnętrznych punktów końcowych, możesz dodać toocontrol reguły (oparte na powitania punktów końcowych, które zostały utworzone) ruchu sieciowego jak wystąpień roli może komunikować się ze sobą. Witaj poniższym diagramie przedstawiono kilka typowych scenariuszy kontroli komunikacji roli:

![Scenariusze reguły ruchu sieciowego](./media/cloud-services-enable-communication-role-instances/scenarios.png "scenariusze reguły ruchu sieciowego")

Witaj Poniższy przykładowy kod przedstawia definicje ról dla ról hello pokazano hello poprzedni diagram. Każda definicja roli obejmuje co najmniej jeden wewnętrzny punkt końcowy zdefiniowany:

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
> Ograniczenia komunikacji między rolami może wystąpić z wewnętrznych punktów końcowych zarówno stały i przypisywane automatycznie portów.
> 
> 

Domyślnie po zdefiniowaniu wewnętrzny punkt końcowy komunikacji mogą przepływać z dowolnej roli toohello wewnętrzny punkt końcowy roli bez ograniczeń. Komunikacja toorestrict, należy dodać **NetworkTrafficRules** toohello elementu **ServiceDefinition** elementu w pliku definicji usługi hello.

### <a name="scenario-1"></a>Scenariusz 1
Zezwalaj tylko na ruch sieciowy z **WebRole1** za**WorkerRole1**.

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

### <a name="scenario-2"></a>Scenariusz 2
Zezwala na ruch sieciowy z **WebRole1** za**WorkerRole1** i **WorkerRole2**.

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

### <a name="scenario-3"></a>Scenariusz 3
Zezwala na ruch sieciowy z **WebRole1** za**WorkerRole1**, i **WorkerRole1** za**WorkerRole2**.

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

### <a name="scenario-4"></a>Scenariusz 4
Zezwala na ruch sieciowy z **WebRole1** za**WorkerRole1**, **WebRole1** za**WorkerRole2**, i  **WorkerRole1** za**WorkerRole2**.

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

Znajduje się odwołanie do schematu XML dla elementów hello powyżej [tutaj](https://msdn.microsoft.com/library/azure/gg557551.aspx).

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat hello usługi w chmurze [modelu](cloud-services-model-and-package.md).

