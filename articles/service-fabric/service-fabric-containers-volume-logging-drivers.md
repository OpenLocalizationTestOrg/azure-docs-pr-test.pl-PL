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
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a>Określanie woluminu dodatków plug-in i sterowniki rejestrowania dla Twojego kontenera

Sieć szkieletowa usług obsługuje określanie [wtyczek woluminu Docker](https://docs.docker.com/engine/extend/plugins_volume/) i [sterowniki rejestrowania Docker](https://docs.docker.com/engine/admin/logging/overview/) dla usługi kontenera. wtyczki Hello są określone w manifeście aplikacji hello pokazane na powitania po manifestu:


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

W hello poprzedzających przykład, hello `Source` tagu hello `Volume` odwołuje się toohello folderu źródłowego. folder źródłowy Hello może być folderem w hello maszynę Wirtualną, która obsługuje kontenery hello lub trwałego magazynu zdalnego. Witaj `Destination` tag jest lokalizacja hello hello `Source` hello zamapowanych toowithin działa kontenera. 

Podczas określania wtyczki woluminu, Service Fabric automatycznie tworzy hello woluminu przy użyciu określonych parametrów hello. Witaj `Source` tag jest nazwą hello hello woluminu i hello `Driver` tag określa dodatek sterownika hello woluminu. Opcje można określić za pomocą hello `DriverOption` tagu pokazane na powitania po fragment kodu:

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

Jeśli sterownik dziennika Docker jest określony, jest konieczne toodeploy, dzienniki w klastrze hello hello toohandle agentów (lub kontenery).  Witaj `DriverOption` tag może być także opcje sterownika dziennika używanych toospecify.

Zapoznaj się toohello po klastra sieci szkieletowej usług tooa kontenery toodeploy artykuły:


[Wdrażanie kontenera w sieci szkieletowej usług](service-fabric-deploy-container.md)

