---
title: "Usługa sieci szkieletowej rozwiązania Docker Compose Podgląd aaaAzure | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług Azure akceptuje rozwiązania Docker Compose toomake format go łatwiejsze tooorchestrate exsiting kontenerów przy użyciu sieci szkieletowej usług. Ta obsługa jest obecnie w przeglądzie."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 824044fd698f0ed94c4212722bc82187905315dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="060f0-104">Określanie woluminu dodatków plug-in i sterowniki rejestrowania dla Twojego kontenera</span><span class="sxs-lookup"><span data-stu-id="060f0-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="060f0-105">Sieć szkieletowa usług obsługuje określanie [wtyczek woluminu Docker](https://docs.docker.com/engine/extend/plugins_volume/) i [sterowniki rejestrowania Docker](https://docs.docker.com/engine/admin/logging/overview/) dla usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="060f0-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="060f0-106">wtyczki Hello są określone w manifeście aplikacji hello pokazane na powitania po manifestu:</span><span class="sxs-lookup"><span data-stu-id="060f0-106">hello plugins are specified in hello application manifest as shown in hello following manifest:</span></span>


```xml
?xml version="1.0" encoding="UTF-8"?>
<ApplicationManifest ApplicationTypeName="WinNodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Description>Calculator Application</Description>
    <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
      <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
    </Parameters>
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeServicePackage" ServiceManifestVersion="1.0"/>
     <Policies>
       <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv"> 
        <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
        <RepositoryCredentials PasswordEncrypted="false" Password="****" AccountName="test"/>
        <LogConfig Driver="etwlogs" >
          <DriverOption Name="test" Value="vale"/>
        </LogConfig>
        <Volume Source="c:\workspace" Destination="c:\testmountlocation1" IsReadOnly="false"></Volume>
        <Volume Source="d:\myfolder" Destination="c:\testmountlocation2" IsReadOnly="true"> </Volume>
        <Volume Source="myexternalvolume" Destination="c:\testmountlocation3" Driver="sf" IsReadOnly="true"></Volume>
       </ContainerHostPolicies>
   </Policies>
    </ServiceManifestImport>
    <ServiceTemplates>
        <StatelessService ServiceTypeName="StatelessNodeService" InstanceCount="5">
            <SingletonPartition></SingletonPartition>
        </StatelessService>
    </ServiceTemplates>
</ApplicationManifest>
```

<span data-ttu-id="060f0-107">W hello poprzedzających przykład, hello `Source` tagu hello `Volume` odwołuje się toohello folderu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="060f0-107">In hello preceding example, hello `Source` tag for hello `Volume` refers toohello source folder.</span></span> <span data-ttu-id="060f0-108">folder źródłowy Hello może być folderem w hello maszynę Wirtualną, która obsługuje kontenery hello lub trwałego magazynu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="060f0-108">hello source folder could be a folder in hello VM that hosts hello containers or a persistent remote store.</span></span> <span data-ttu-id="060f0-109">Witaj `Destination` tag jest lokalizacja hello hello `Source` hello zamapowanych toowithin działa kontenera.</span><span class="sxs-lookup"><span data-stu-id="060f0-109">hello `Destination` tag is hello location that hello `Source` is mapped toowithin hello running container.</span></span> 

<span data-ttu-id="060f0-110">Podczas określania wtyczki woluminu, Service Fabric automatycznie tworzy hello woluminu przy użyciu określonych parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="060f0-110">When specifying a volume plugin, Service Fabric automatically creates hello volume using hello parameters specified.</span></span> <span data-ttu-id="060f0-111">Witaj `Source` tag jest nazwą hello hello woluminu i hello `Driver` tag określa dodatek sterownika hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="060f0-111">hello `Source` tag is hello name of hello volume, and hello `Driver` tag specifies hello volume driver plugin.</span></span> <span data-ttu-id="060f0-112">Opcje można określić za pomocą hello `DriverOption` tagu pokazane na powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="060f0-112">Options can be specified using hello `DriverOption` tag as shown in hello following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="060f0-113">Jeśli sterownik dziennika Docker jest określony, jest konieczne toodeploy, dzienniki w klastrze hello hello toohandle agentów (lub kontenery).</span><span class="sxs-lookup"><span data-stu-id="060f0-113">If a Docker log driver is specified, it is necessary toodeploy agents (or containers) toohandle hello logs in hello cluster.</span></span>  <span data-ttu-id="060f0-114">Witaj `DriverOption` tag może być także opcje sterownika dziennika używanych toospecify.</span><span class="sxs-lookup"><span data-stu-id="060f0-114">hello `DriverOption` tag can be used toospecify log driver options as well.</span></span>

<span data-ttu-id="060f0-115">Zapoznaj się toohello po klastra sieci szkieletowej usług tooa kontenery toodeploy artykuły:</span><span class="sxs-lookup"><span data-stu-id="060f0-115">Refer toohello following articles toodeploy containers tooa Service Fabric cluster:</span></span>


[<span data-ttu-id="060f0-116">Wdrażanie kontenera w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="060f0-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

