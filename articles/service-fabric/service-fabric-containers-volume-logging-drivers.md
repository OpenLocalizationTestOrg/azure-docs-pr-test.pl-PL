---
title: "Usługa Azure sieci szkieletowej z rozwiązania Docker Compose w wersji zapoznawczej | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług Azure akceptuje rozwiązania Docker Compose format, aby ułatwić organizowanie kontenery exsiting przy użyciu sieci szkieletowej usług. Ta obsługa jest obecnie w przeglądzie."
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
ms.openlocfilehash: b12ef95add6347621f7d4865fac46568f91a1e12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="bdb01-104">Określanie woluminu dodatków plug-in i sterowniki rejestrowania dla Twojego kontenera</span><span class="sxs-lookup"><span data-stu-id="bdb01-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="bdb01-105">Sieć szkieletowa usług obsługuje określanie [wtyczek woluminu Docker](https://docs.docker.com/engine/extend/plugins_volume/) i [sterowniki rejestrowania Docker](https://docs.docker.com/engine/admin/logging/overview/) dla usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="bdb01-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="bdb01-106">Wtyczki są określone w manifeście aplikacji, jak pokazano w manifeście następujące:</span><span class="sxs-lookup"><span data-stu-id="bdb01-106">The plugins are specified in the application manifest as shown in the following manifest:</span></span>


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

<span data-ttu-id="bdb01-107">W powyższym przykładzie `Source` znacznika `Volume` odwołuje się do folderu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="bdb01-107">In the preceding example, the `Source` tag for the `Volume` refers to the source folder.</span></span> <span data-ttu-id="bdb01-108">Folder źródłowy może być folderem w maszynie Wirtualnej, która obsługuje kontenery lub trwałego magazynu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="bdb01-108">The source folder could be a folder in the VM that hosts the containers or a persistent remote store.</span></span> <span data-ttu-id="bdb01-109">`Destination` Tag to lokalizacja, w który `Source` jest mapowany w kontenerze uruchomione.</span><span class="sxs-lookup"><span data-stu-id="bdb01-109">The `Destination` tag is the location that the `Source` is mapped to within the running container.</span></span> 

<span data-ttu-id="bdb01-110">Podczas określania wtyczki woluminu, Service Fabric automatycznie tworzy woluminu przy użyciu określonych parametrów.</span><span class="sxs-lookup"><span data-stu-id="bdb01-110">When specifying a volume plugin, Service Fabric automatically creates the volume using the parameters specified.</span></span> <span data-ttu-id="bdb01-111">`Source` Tag jest nazwa woluminu, a `Driver` tag określa dodatek sterownika woluminu.</span><span class="sxs-lookup"><span data-stu-id="bdb01-111">The `Source` tag is the name of the volume, and the `Driver` tag specifies the volume driver plugin.</span></span> <span data-ttu-id="bdb01-112">Opcje można określić za pomocą `DriverOption` tagów, jak pokazano w poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="bdb01-112">Options can be specified using the `DriverOption` tag as shown in the following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="bdb01-113">Jeśli sterownik dziennika Docker jest określony, jest wymagane do wdrożenia agentów (lub kontenery) do obsługi dzienników w klastrze.</span><span class="sxs-lookup"><span data-stu-id="bdb01-113">If a Docker log driver is specified, it is necessary to deploy agents (or containers) to handle the logs in the cluster.</span></span>  <span data-ttu-id="bdb01-114">`DriverOption` Tag może służyć do określ także opcje sterownika dziennika.</span><span class="sxs-lookup"><span data-stu-id="bdb01-114">The `DriverOption` tag can be used to specify log driver options as well.</span></span>

<span data-ttu-id="bdb01-115">Zobacz następujące artykuły, aby wdrażanie kontenerów do klastra usługi sieć szkieletowa usług:</span><span class="sxs-lookup"><span data-stu-id="bdb01-115">Refer to the following articles to deploy containers to a Service Fabric cluster:</span></span>


[<span data-ttu-id="bdb01-116">Wdrażanie kontenera w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="bdb01-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

