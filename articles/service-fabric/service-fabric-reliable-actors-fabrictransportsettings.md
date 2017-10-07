---
title: "Ustawienia FabricTransport aaaChange w Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o konfigurowaniu ustawień komunikacji aktora sieci szkieletowej usług Azure."
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: e312b475407eb95a435b93d80c0f2e9618b9ea1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="5fee8-103">Skonfiguruj ustawienia FabricTransport Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="5fee8-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="5fee8-104">Poniżej przedstawiono ustawienia hello, które można skonfigurować:</span><span class="sxs-lookup"><span data-stu-id="5fee8-104">Here are hello settings that you can configure:</span></span>
- <span data-ttu-id="5fee8-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="5fee8-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="5fee8-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="5fee8-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="5fee8-107">Można zmodyfikować domyślną konfigurację hello FabricTransport w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="5fee8-107">You can modify hello default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="5fee8-108">Atrybut zestawu</span><span class="sxs-lookup"><span data-stu-id="5fee8-108">Assembly attribute</span></span>

<span data-ttu-id="5fee8-109">Witaj [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) atrybut wymaga toobe zastosowane na powitania aktora klienta i aktora zestawy usług.</span><span class="sxs-lookup"><span data-stu-id="5fee8-109">hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs toobe applied on hello actor client and actor service assemblies.</span></span>

<span data-ttu-id="5fee8-110">Witaj poniższy przykład pokazuje, jak toochange hello wartość domyślną ustawienia FabricTransport OperationTimeout:</span><span class="sxs-lookup"><span data-stu-id="5fee8-110">hello following example shows how toochange hello default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="5fee8-111">Drugi przykład zmienia domyślne wartości FabricTransport MaxMessageSize i OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="5fee8-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="5fee8-112">Pakiet konfiguracji</span><span class="sxs-lookup"><span data-stu-id="5fee8-112">Config package</span></span>

<span data-ttu-id="5fee8-113">Można użyć [pakietu konfiguracji](service-fabric-application-model.md) toomodify hello domyślnej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5fee8-113">You can use a [config package](service-fabric-application-model.md) toomodify hello default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-hello-actor-service"></a><span data-ttu-id="5fee8-114">Skonfiguruj ustawienia FabricTransport dla usługi aktora hello</span><span class="sxs-lookup"><span data-stu-id="5fee8-114">Configure FabricTransport settings for hello actor service</span></span>

<span data-ttu-id="5fee8-115">Dodaj sekcję TransportSettings w pliku settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="5fee8-115">Add a TransportSettings section in hello settings.xml file.</span></span>

<span data-ttu-id="5fee8-116">Domyślnie kod aktora szuka SectionName jako "&lt;ActorName&gt;TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="5fee8-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="5fee8-117">Jeśli nie zostanie znaleziony, sprawdza SectionName jako "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="5fee8-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-hello-actor-client-assembly"></a><span data-ttu-id="5fee8-118">Skonfiguruj ustawienia FabricTransport hello aktora klienta zestawu</span><span class="sxs-lookup"><span data-stu-id="5fee8-118">Configure FabricTransport settings for hello actor client assembly</span></span>

<span data-ttu-id="5fee8-119">Jeśli powitania klienta nie jest uruchomiony jako część usługi, możesz utworzyć "&lt;nazwa Exe klienta&gt;. settings.xml" w pliku hello sam lokalizacji co plik .exe powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="5fee8-119">If hello client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in hello same location as hello client .exe file.</span></span> <span data-ttu-id="5fee8-120">Następnie dodaj sekcję TransportSettings w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="5fee8-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="5fee8-121">SectionName powinien być "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="5fee8-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="5fee8-122">Konfigurowanie ustawień FabricTransport dla klienta usługi aktora bezpiecznego za pomocą dodatkowego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="5fee8-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="5fee8-123">Informacje o certyfikacie dodatkowej można dodać, dodając parametr CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="5fee8-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="5fee8-124">Poniżej znajduje się przykład hello hello TransportSettings odbiornika.</span><span class="sxs-lookup"><span data-stu-id="5fee8-124">Below is hello example for hello Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="5fee8-125">Poniżej znajduje się przykład hello hello TransportSettings klienta.</span><span class="sxs-lookup"><span data-stu-id="5fee8-125">Below is hello example for hello Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="5fee8-126">Konfigurowanie ustawień FabricTransport zabezpieczania aktora/klient usługi za pomocą nazwy podmiotu.</span><span class="sxs-lookup"><span data-stu-id="5fee8-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="5fee8-127">Użytkownik musi tooprovide findType jako FindBySubjectName, Dodaj CertificateIssuerThumbprints i CertificateRemoteCommonNames wartości.</span><span class="sxs-lookup"><span data-stu-id="5fee8-127">User needs tooprovide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="5fee8-128">Poniżej znajduje się przykład hello hello TransportSettings odbiornika.</span><span class="sxs-lookup"><span data-stu-id="5fee8-128">Below is hello example for hello Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="5fee8-129">Poniżej znajduje się przykład hello hello TransportSettings klienta.</span><span class="sxs-lookup"><span data-stu-id="5fee8-129">Below is hello example for hello Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
