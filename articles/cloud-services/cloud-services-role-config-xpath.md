---
title: "aaaCloud roli usługi konfiguracji XPath ściągawka | Dokumentacja firmy Microsoft"
description: "Witaj różne ustawienia języka XPath można używać jako zmienną środowiskową w hello chmury usługi roli config tooexpose ustawienia."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a>Udostępnianie ustawień konfiguracji roli jako zmiennej środowiskowej XPath
Proces roboczy usług chmury hello lub pliku definicji usługi roli sieci web mogą uwidaczniać wartości konfiguracji środowiska uruchomieniowego jako zmienne środowiskowe. następujące wartości XPath Hello są obsługiwane (co odpowiada wartości tooAPI).

Te wartości XPath są również dostępne za pośrednictwem hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) biblioteki. 

## <a name="app-running-in-emulator"></a>Aplikacji uruchomionej w emulatorze
Wskazuje, że danej aplikacji hello działa w emulatorze hello.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/RoleEnvironment/Deployment/@emulated" |
| Kod |var x = RoleEnvironment.IsEmulated; |

## <a name="deployment-id"></a>Identyfikator wdrożenia
Pobiera identyfikator wdrożenia hello hello wystąpienia.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/RoleEnvironment/Deployment/@id" |
| Kod |var deploymentId = RoleEnvironment.DeploymentId; |

## <a name="role-id"></a>Identyfikator roli
Pobiera bieżący identyfikator roli hello hello wystąpienia.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@id" |
| Kod |Identyfikator var = RoleEnvironment.CurrentRoleInstance.Id; |

## <a name="update-domain"></a>Aktualizowanie domeny
Pobiera domeny aktualizacji hello hello wystąpienia.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@updateDomain" |
| Kod |var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain; |

## <a name="fault-domain"></a>Domena awarii
Pobiera domeny błędów hello hello wystąpienia.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@faultDomain" |
| Kod |var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain; |

## <a name="role-name"></a>Nazwa roli
Pobiera nazwę roli hello hello wystąpień.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@roleName" |
| Kod |var rname = RoleEnvironment.CurrentRoleInstance.Role.Name; |

## <a name="config-setting"></a>Ustawienia konfiguracji
Pobiera wartość hello hello określone ustawienia konfiguracji.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/appSettings/ConfigurationSetting [@name="Setting1"]/@value" |
| Kod |Ustawienie var = RoleEnvironment.GetConfigurationSettingValue("Setting1"); |

## <a name="local-storage-path"></a>Ścieżki do lokalnego magazynu
Pobiera ścieżkę magazynu lokalnego hello hello wystąpienia.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name="LocalStore1"]/@path" |
| Kod |var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1"). Właściwość RootPath; |

## <a name="local-storage-size"></a>Rozmiar magazynu lokalnego
Pobiera rozmiar hello hello magazynu lokalnego wystąpienia hello.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name="LocalStore1"]/@sizeInMB" |
| Kod |var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1"). MaximumSizeInMegabytes; |

## <a name="endpoint-protocol"></a>Punkt końcowy protokołu
Pobiera protokół punktu końcowego hello hello wystąpienia.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/punkty końcowe/punktu końcowego [@name= 'Punk końcowy 1']/@protocol" |
| Kod |ochronę var = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"]. Protokół; |

## <a name="endpoint-ip"></a>Punkt końcowy IP
Pobiera hello określony adres IP punktu końcowego.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/punkty końcowe/punktu końcowego [@name= 'Punk końcowy 1']/@address" |
| Kod |adres var = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"]. IPEndpoint.Address |

## <a name="endpoint-port"></a>Port punktu końcowego
Pobiera hello port punktu końcowego dla hello wystąpienia.

| Typ | Przykład |
| --- | --- |
| Wyrażenie XPath |wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/punkty końcowe/punktu końcowego [@name= 'Punk końcowy 1']/@port" |
| Kod |var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"]. IPEndpoint.Port; |

## <a name="example"></a>Przykład
Oto przykład roli procesu roboczego, który tworzy zadanie uruchamiania przy użyciu zmiennej środowiskowej o nazwie `TestIsEmulated` ustawić toohello [ @emulated wartość wyrażenia xpath](#app-running-in-emulator). 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [pliku ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) pliku.

Utwórz [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) pakietu.

Włącz [pulpitu zdalnego](cloud-services-role-enable-remote-desktop.md) dla roli.

