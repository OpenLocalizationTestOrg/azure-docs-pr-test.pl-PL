---
title: "aaaManage wiele środowisk w sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług aplikacji może działać w klastrach, w zakresie rozmiaru z jednego komputera toothousands maszyn. W niektórych przypadkach można tooconfigure aplikacji inaczej w przypadku tych środowisk zróżnicowane. W tym artykule opisano sposób toodefine parametry różnych aplikacji dla środowiska."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a>Parametry aplikacji dla wielu środowisk zarządzania
Można utworzyć klastry z sieci szkieletowej usług Azure przy użyciu dowolnego miejsca, z jedną toomany tysięcy komputerów. Podczas plików binarnych aplikacji można uruchomić bez żadnych modyfikacji w tym szerokie spektrum środowisk, często mają aplikacji hello tooconfigure inaczej, w zależności od numer hello maszyny, które jest wdrażany do.

Jako przykład prostego, należy wziąć pod uwagę `InstanceCount` usługi bezstanowej. Po uruchomieniu aplikacji na platformie Azure, zazwyczaj mają tooset wartości tego parametru toohello specjalne-"1". Taka konfiguracja powoduje, że usługa działa na każdym węźle w klastrze hello (lub każdego węzła w hello typu węzła, jeśli ustawiono ograniczenia umieszczania). Jednak ta konfiguracja nie jest odpowiedni dla pojedynczego komputera klastrów, ponieważ nie może mieć wiele procesów nasłuchiwania na powitania sam punkt końcowy na jednym komputerze. Zamiast tego należy zwykle ustawić `InstanceCount` zbyt "1".

## <a name="specifying-environment-specific-parameters"></a>Określanie parametrów określonego środowiska
problem z konfiguracją toothis Hello rozwiązanie to zestaw usług domyślnych sparametryzowanych i pliki parametrów aplikacji, które wypełnić wartości tych parametrów dla danego środowiska. Parametry aplikacji i usług domyślnych są konfigurowane w aplikacji hello i manifestów usługi. Witaj definicji schematu dla plików ServiceManifest.xml i ApplicationManifest.xml hello jest instalowany z hello zestawu SDK sieci szkieletowej usług i narzędzi zbyt*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

### <a name="default-services"></a>Domyślne usługi
Aplikacje usługi sieć szkieletowa składają się z kolekcji wystąpień usługi. Podczas umożliwiające toocreate pustą aplikację, a następnie dynamicznie utworzyć wszystkich wystąpień usługi, większość aplikacji ma zestaw podstawowe usługi, które należy zawsze utworzyć podczas tworzenia wystąpienia klasy aplikacji hello. Są to określonego tooas "domyślne usługi". Są one określone w manifeście aplikacji hello z symbole zastępcze-środowisko konfiguracji zawarte w nawiasach kwadratowych:

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

Każdy z hello nazwanych parametrów musi być zdefiniowana w elemencie parametry hello manifestu aplikacji hello:

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

Atrybut DefaultValue Hello określa toobe wartość hello używane w braku hello parametru bardziej specyficzne dla danego środowiska.

> [!NOTE]
> Nie wszystkie parametry wystąpienia usługi są odpowiednie dla konfiguracji poszczególnych środowiska. W powyższym przykładzie hello hello LowKey i HighKey dla schemat partycjonowania usługi hello są jawnie zdefiniowane wartości dla wszystkich wystąpień usługi hello ponieważ zakres partycji hello jest funkcją hello danych domeny, nie hello środowiska.
> 
> 

### <a name="per-environment-service-configuration-settings"></a>Ustawienia konfiguracji usługi na środowisko
Witaj [model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md) umożliwia usług tooinclude konfiguracji pakiety, które zawierają niestandardowe pary klucz wartość, które są do odczytu w czasie wykonywania. Witaj wartości tych ustawień można również zróżnicowane przez środowisko, określając `ConfigOverride` w manifeście aplikacji hello.

Załóżmy, że masz następujące ustawienia w pliku Config\Settings.xml hello hello hello `Stateful1` usługi:

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
Utwórz tę wartość dla pary określonych aplikacji środowiskową toooverride `ConfigOverride` podczas importowania manifestu usługi hello w manifeście aplikacji hello.

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
Ten parametr może zostać następnie skonfigurowane przez środowisko zgodnie z powyższym. Można to zrobić, deklarowanie go w sekcji parametrów hello manifest aplikacji hello i określając wartości określonego środowiska w pliki parametrów aplikacji hello.

> [!NOTE]
> W przypadku hello ustawienia konfiguracji usługi, istnieją trzy miejsca, w którym można ustawić wartości hello klucza: pakiet konfiguracji usługi hello manifest aplikacji hello i pliku parametrów aplikacji hello. Sieci szkieletowej usług będzie zawsze wybierz z pliku parametrów aplikacji hello najpierw (Jeśli określono), następnie hello manifest aplikacji, a na koniec hello pakiet konfiguracji.
> 
> 

### <a name="setting-and-using-environment-variables"></a>Ustawianie i za pomocą zmiennych środowiskowych 
Można określić i ustaw zmienne środowiskowe w pliku ServiceManifest.xml hello i następnie zastąpić je w pliku ApplicationManifest.xml powitania dla poszczególnych wystąpień.
Witaj w poniższym przykładzie przedstawiono dwie zmienne środowiskowe, ustawić jedną z wartości i hello innych zostanie zastąpiona. Można używać parametrów aplikacji, zmienne środowiskowe tooset wartości w hello sam sposób że powyższe użyto do konfiguracji zastąpień.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
zmienne środowiskowe hello toooverride w pliku ApplicationManifest.xml, pakiet kodu hello odwołania w hello ServiceManifest z hello hello `EnvironmentOverrides` elementu.

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 Po utworzeniu hello nazwane wystąpienie usługi dostępne zmienne środowiskowe hello z kodu. np. W języku C# można wykonać następujące hello

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a>Zmienne środowiskowe sieci szkieletowej usług
Sieć szkieletowa usług są wbudowane zmienne środowiskowe ustawione dla każdego wystąpienia usługi. Witaj pełną listę zmiennych środowiskowych jest poniżej, gdzie hello tych w są pogrubione hello używanych w usłudze hello innych są używane przez środowisko uruchomieniowe usługi sieć szkieletowa. 

* Fabric_ApplicationHostId
* Fabric_ApplicationHostType
* Fabric_ApplicationId
* **Fabric_ApplicationName**
* Fabric_CodePackageInstanceId
* **Fabric_CodePackageName**
* **TypeEndpoint Fabric_Endpoint_ [YourServiceName]**
* **Fabric_Folder_App_Log**
* **Fabric_Folder_App_Temp**
* **Fabric_Folder_App_Work**
* **Fabric_Folder_Application**
* Fabric_NodeId
* **Fabric_NodeIPOrFQDN**
* **Fabric_NodeName**
* Fabric_RuntimeConnectionAddress
* Fabric_ServicePackageInstanceId
* Fabric_ServicePackageName
* Fabric_ServicePackageVersionInstance
* FabricPackageFileName

Witaj belows kodu pokazuje, jak toolist hello zmiennych środowiskowych sieci szkieletowej usług
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
Witaj poniżej przedstawiono przykłady zmiennych środowiskowych dla typu aplikacji o nazwie `GuestExe.Application` z typem usługi o nazwie `FrontEndService` uruchomienia na komputerze deweloperskim lokalnego.

* **Fabric_ApplicationName = fabric:/GuestExe.Application**
* **Fabric_CodePackageName = kod**
* **Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**
* **Fabric_NodeIPOrFQDN = localhost**
* **Fabric_NodeName = to węzeł _Node_2**

### <a name="application-parameter-files"></a>Pliki parametrów aplikacji
Projekt aplikacji Hello sieci szkieletowej usług mogą zawierać jeden lub więcej plików parametr aplikacji. Każde z nich definiuje hello określonych wartości dla parametrów hello, które są zdefiniowane w manifeście aplikacji hello:

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
Domyślnie nowa aplikacja obejmuje trzy pliki parametrów aplikacji, o nazwie Local.1Node.xml, Local.5Node.xml i Cloud.xml:

![Pliki parametrów aplikacji w Eksploratorze rozwiązań][app-parameters-solution-explorer]

toocreate pliku parametrów po prostu skopiuj i Wklej istniejący i nadaj mu nazwę.

## <a name="identifying-environment-specific-parameters-during-deployment"></a>Identyfikowanie określonego środowiska parametrów podczas wdrażania
W czasie wdrażania należy toochoose hello odpowiedni parametr pliku tooapply z aplikacją. Można to zrobić za pomocą okna dialogowego publikowanie hello w programie Visual Studio lub za pomocą programu PowerShell.

### <a name="deploy-from-visual-studio"></a>Wdrażanie w programie Visual Studio
Można wybierać spośród hello listę dostępnych parametrów plików podczas publikowania aplikacji w programie Visual Studio.

![Wybierz plik parametrów w oknie dialogowym Publikowanie hello][publishdialog]

### <a name="deploy-from-powershell"></a>Wdrażanie z programu PowerShell
Witaj `Deploy-FabricApplication.ps1` profil publikowania, jako parametr akceptuje zawarte w szablonie projektu aplikacji hello skrypt programu PowerShell i hello PublishProfile zawiera plik parametrów aplikacji toohello odwołania.

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat niektórych hello podstawowe koncepcje, które zostały omówione w tym temacie, zobacz hello [omówienie techniczne sieci szkieletowej usług](service-fabric-technical-overview.md). Aby uzyskać informacje o inne funkcje zarządzania aplikacjami, które są dostępne w programie Visual Studio, zobacz [Zarządzaj aplikacjami sieci szkieletowej usług w programie Visual Studio](service-fabric-manage-application-in-visual-studio.md).

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
