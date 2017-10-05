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
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a>Określanie woluminu dodatków plug-in i sterowniki rejestrowania dla Twojego kontenera

Sieć szkieletowa usług obsługuje określanie [wtyczek woluminu Docker](https://docs.docker.com/engine/extend/plugins_volume/) i [sterowniki rejestrowania Docker](https://docs.docker.com/engine/admin/logging/overview/) dla usługi kontenera. Wtyczki są określone w manifeście aplikacji, jak pokazano w manifeście następujące:


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

W powyższym przykładzie `Source` znacznika `Volume` odwołuje się do folderu źródłowego. Folder źródłowy może być folderem w maszynie Wirtualnej, która obsługuje kontenery lub trwałego magazynu zdalnego. `Destination` Tag to lokalizacja, w który `Source` jest mapowany w kontenerze uruchomione. 

Podczas określania wtyczki woluminu, Service Fabric automatycznie tworzy woluminu przy użyciu określonych parametrów. `Source` Tag jest nazwa woluminu, a `Driver` tag określa dodatek sterownika woluminu. Opcje można określić za pomocą `DriverOption` tagów, jak pokazano w poniższy fragment kodu:

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

Jeśli sterownik dziennika Docker jest określony, jest wymagane do wdrożenia agentów (lub kontenery) do obsługi dzienników w klastrze.  `DriverOption` Tag może służyć do określ także opcje sterownika dziennika.

Zobacz następujące artykuły, aby wdrażanie kontenerów do klastra usługi sieć szkieletowa usług:


[Wdrażanie kontenera w sieci szkieletowej usług](service-fabric-deploy-container.md)

