---
title: "aaaWhat jest modelem usługi chmury, a pakiet | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano model hello chmury usługi (csdef, .cscfg) i pakietu (cspkg) na platformie Azure"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a>Co to jest model usługi w chmurze hello i jak jest pakiet?
Usługi w chmurze jest tworzona na podstawie trzech składników, definicji usługi hello *(csdef)*, hello konfiguracji usługi *(cscfg)*, a pakiet usługi *(cspkg)*. Zarówno hello **ServiceDefinition.csdef** i **ServiceConfig.cscfg** plików są oparte na języku XML i opisano strukturę hello hello usługi w chmurze i sposobu jego konfiguracji; nazywane hello modelu. Witaj **ServicePackage.cspkg** plik zip, który jest generowany na podstawie hello **ServiceDefinition.csdef** i między innymi zawiera wszystkie wymagane hello zależności formacie binarnym. Platforma Azure tworzy usługi w chmurze z obu hello **ServicePackage.cspkg** i hello **ServiceConfig.cscfg**.

Po uruchomieniu usługi chmury hello na platformie Azure, można ponownie skonfigurować go za pośrednictwem hello **ServiceConfig.cscfg** pliku, ale nie można zmienić definicji hello.

## <a name="what-would-you-like-tooknow-more-about"></a>Co chcesz tooknow więcej informacji na temat?
* Chcę uzyskać więcej informacji na temat hello tooknow [ServiceDefinition.csdef](#csdef) i [ServiceConfig.cscfg](#cscfg) plików.
* Już wiem, temat, który można uzyskać [przykłady](#next-steps) na to, co można skonfigurować.
* Chcę toocreate hello [ServicePackage.cspkg](#cspkg).
* Używam programu Visual Studio i chcę...
  * [Tworzenie usługi w chmurze][vs_create]
  * [Skonfiguruj ponownie istniejącej usługi w chmurze][vs_reconfigure]
  * [Wdrażanie projektu usługi w chmurze][vs_deploy]
  * [Pulpit zdalny w wystąpieniu usługi chmury][remotedesktop]

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a>ServiceDefinition.csdef
Witaj **ServiceDefinition.csdef** pliku określa hello ustawienia, które są używane przez Azure tooconfigure usługa w chmurze. Witaj [schematu definicji usługi Azure (pliki csdef pliku)](https://msdn.microsoft.com/library/azure/ee758711.aspx) zapewnia hello dopuszczalny formatu pliku definicji usługi. Witaj poniższym przykładzie przedstawiono hello ustawień, które mogą być definiowane dla hello sieci Web i proces roboczy.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
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
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

Może się odwoływać toohello [schematu definicji usługi](https://msdn.microsoft.com/library/azure/ee758711.aspx) w celu lepszego zrozumienia hello schematu XML używane w tym miejscu, jednak w tym miejscu jest szybkie wyjaśnienie niektórych elementów hello:

**Lokacje**  
Zawiera definicje hello witryn sieci Web lub sieci web aplikacji, które są obsługiwane w programie IIS7.

**InputEndpoints**  
Zawiera definicje hello punktów końcowych, które są używane usługi w chmurze hello toocontact.

**InternalEndpoints**  
Zawiera definicje hello punktów końcowych, które są używane przez toocommunicate wystąpień roli ze sobą.

**AppSettings**  
Zawiera definicje ustawienie hello funkcji określoną rolę.

**Certyfikaty**  
Zawiera definicje hello certyfikaty, które są wymagane przez rolę. Witaj poprzednim przykładzie kodu przedstawiono certyfikatu, który służy do konfiguracji hello Azure Connect.

**LocalResources**  
Zawiera definicje hello zasoby magazynu lokalnego. Zasób Magazyn lokalny jest zastrzeżony katalogu w systemie plików hello hello maszyny wirtualnej, w którym jest uruchomione wystąpienie roli.

**Importy**  
Zawiera definicje hello zaimportowanych modułów. Witaj poprzednim przykładzie kodu pokazują moduły hello Podłączanie pulpitu zdalnego i Azure Connect.

**Uruchamianie**  
Zawiera zadania, które są uruchamiane podczas uruchamiania hello roli. zadania Hello są definiowane w .cmd lub pliku wykonywalnego.

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a>Pliku ServiceConfiguration.cscfg
Konfiguracja Hello hello ustawień usługi w chmurze zależy od wartości hello hello **pliku ServiceConfiguration.cscfg** pliku. Można określić numer hello wystąpień mają toodeploy dla każdej roli, w tym pliku. wartości ustawienia konfiguracji hello zdefiniowane w pliku definicji usługi hello Hello są dodawane pliku konfiguracji usługi toohello. odciski palców Hello dotyczące wszystkich certyfikatów zarządzania skojarzonych z usługą w chmurze hello dodawane są także toohello pliku. Witaj [schemat konfiguracji usługi Azure (cscfg pliku)](https://msdn.microsoft.com/library/azure/ee758710.aspx) zapewnia hello dozwolony format pliku konfiguracji usługi.

Hello pliku konfiguracji usługi nie jest dostarczana z aplikacji hello, ale jest tooAzure przekazany jako osobny plik i hello tooconfigure używana jest usługa w chmurze. Możesz przekazać plik konfiguracji usługi bez ponownego wdrożenia usługi w chmurze. można zmienić Hello wartości konfiguracji dla usługi w chmurze hello jest uruchomiona usługa w chmurze hello. Witaj poniższym przykładzie przedstawiono hello ustawienia konfiguracji, które mogą być definiowane dla hello sieci Web i proces roboczy.

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

Może się odwoływać toohello [schemat konfiguracji usługi](https://msdn.microsoft.com/library/azure/ee758710.aspx) do lepszego zrozumienia hello schematu XML używane w tym miejscu, jednak w tym miejscu jest szybkie wyjaśnienie hello elementów:

**Wystąpienia**  
Umożliwia skonfigurowanie liczby hello uruchomionych wystąpień roli hello. tooprevent usługi chmury z potencjalnie stać się niedostępne podczas uaktualniania, zaleca się wdrożenie więcej niż jednego wystąpienia ról udostępnianych w sieci web. Przez wdrożenie więcej niż jedno wystąpienie, są spełnione wytyczne toohello w hello [Azure obliczeniowe poziom Umowa dotycząca usług (SLA)](http://azure.microsoft.com/support/legal/sla/), który zapewnia łączność zewnętrzną 99,95% dla ról połączonych z Internetem, gdy dwie lub więcej ról wystąpienia są wdrażane dla usługi.

**AppSettings**  
Konfiguruje ustawienia hello hello uruchomionych wystąpień roli. Nazwa Hello hello `<Setting>` elementy muszą być zgodne hello definicji ustawień w pliku definicji usługi hello.

**Certyfikaty**  
Konfiguruje hello certyfikaty, które są używane przez usługę hello. Hello poprzednim przykładzie kodu pokazano, jak toodefine hello certyfikat dla hello RemoteAccess modułu. Witaj wartość hello *odcisk palca* należy ustawić atrybut toohello odcisk palca hello toouse certyfikatu.

<p/>

> [!NOTE]
> Witaj odcisk palca certyfikatu hello można dodać plik konfiguracji toohello za pomocą edytora tekstu. Lub wartość hello można dodać na powitania **certyfikaty** kartę hello **właściwości** strony roli hello w programie Visual Studio.
> 
> 

## <a name="defining-ports-for-role-instances"></a>Definiowanie portów dla wystąpień roli
Azure umożliwia tylko jedna rola sieci web tooa punktu wejścia. Co oznacza, że cały ruch odbywa się przez jeden adres IP. Można skonfigurować z witryn sieci Web tooshare port konfigurując hello hosta nagłówka toodirect hello żądania toohello poprawnej lokalizacji. Można także skonfigurować porty znane toowell toolisten Twojej aplikacji hello adresu IP.

Witaj poniższy przykład przedstawia hello konfigurację dla roli sieci web z aplikacji sieci web i witryny sieci Web. Hello witryny sieci Web jest skonfigurowana jako hello domyślny wpis lokalizacji na porcie 80, a aplikacje sieci web hello są żądania tooreceive skonfigurowany z nagłówka alternatywnego hosta, który jest nazywany "mail.mysite.cloudapp.net".

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a>Zmiana konfiguracji hello roli
Należy zaktualizować hello konfiguracji usługi w chmurze, jest uruchomiona na platformie Azure, bez konieczności przełączania w tryb offline usługa hello. toochange informacje o konfiguracji, należy albo Przekaż nowy plik konfiguracji, lub edycji pliku konfiguracji hello w Umieść i zastosować je tooyour, na którym działa usługa. Witaj następujących zmian w konfiguracji toohello usługi:

* **Zmiana wartości hello ustawień konfiguracji**  
  Podczas konfiguracji zmiany, ustawień wystąpienia roli można bezpiecznie wybierz tooapply hello zmiany podczas hello wystąpienie jest w trybie online lub toorecycle hello wystąpienia i stosować zmiany hello podczas hello wystąpienie jest w trybie offline.
* **Zmiany topologii usługa hello wystąpień roli**  
  Topologia zmiany nie wpływają na uruchomione wystąpienia, z wyjątkiem przypadków, gdy wystąpienie jest usuwana. Wszystkie pozostałe wystąpienia zazwyczaj nie są toobe ponownego przetworzenia; jednak można wybrać toorecycle wystąpień roli w przypadku zmiany topologii tooa odpowiedzi.
* **Zmiana hello odcisk palca certyfikatu**  
  Certyfikat można aktualizować tylko wtedy, gdy wystąpienie roli jest w trybie offline. Jeśli certyfikat jest dodany, usunięty lub zmieniony, gdy wystąpienie roli jest w trybie online, Azure bezpiecznie ma hello wystąpienia w trybie offline tooupdate hello certyfikatu i przełączenie go do trybu online po zakończeniu zmiany hello.

### <a name="handling-configuration-changes-with-service-runtime-events"></a>Obsługa zmiany w konfiguracji o zdarzeniach środowiska uruchomieniowego usługi
Witaj [biblioteki środowiska uruchomieniowego usługi Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) obejmuje hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) przestrzeni nazw, która udostępnia klasy do interakcji z hello środowiska platformy Azure z roli. Witaj [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) klasa definiuje hello następujące zdarzenia, które są wywoływane przed i po zmianie konfiguracji:

* **[Zmiana](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) zdarzeń**  
  Dzieje się tak, zanim zmiana konfiguracji hello jest stosowane tooa określonego wystąpienia roli, umożliwiając tootake szansy, dół hello wystąpień roli w razie potrzeby.
* **[Zmienione](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) zdarzeń**  
  Występuje, gdy zmiana konfiguracji hello jest stosowane tooa określonego wystąpienia roli.

> [!NOTE]
> Ponieważ zmiany certyfikatu zawsze pobierają hello wystąpień roli w tryb offline, nie wygenerował hello RoleEnvironment.Changing lub RoleEnvironment.Changed zdarzeń.
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a>ServicePackage.cspkg
toodeploy aplikacji jako usługa w chmurze na platformie Azure, należy najpierw pierwszej aplikacji hello pakietu w odpowiednim formacie hello. Można użyć hello **CSPack** narzędzia wiersza polecenia (zainstalowaną z hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/)) pliku pakietu hello toocreate jako alternatywne tooVisual w Studio.

**CSPack** używa hello zawartość hello usługi definicji usługi plików i konfiguracji toodefine hello zawartość pliku hello pakietu. **CSPack** generuje plik pakietu aplikacji (cspkg) przekazać tooAzure przy użyciu hello [portalu Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy). Domyślnie hello pakietu o nazwie `[ServiceDefinitionFileName].cspkg`, ale możesz określić inną nazwę przy użyciu hello `/out` opcji **CSPack**.

**CSPack** znajduje się pod adresem  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> CSPack.exe (w systemie windows) jest dostępny, uruchamiając hello **wiersza polecenia usługi Microsoft Azure** skrót, który jest instalowany z hello zestawu SDK.  
> 
> Uruchom hello CSPack.exe program samodzielnie dokumentacji toosee wszystkie przełączniki możliwe hello i poleceń.
> 
> 

<p />

> [!TIP]
> Uruchamianie usługi w chmurze lokalnie w hello **Microsoft Azure obliczeniowe emulatora**, użyj hello **/copyonly** opcji. Ta opcja powoduje skopiowanie plików binarnych hello aplikacji hello tooa katalogu układu z którego może działać w emulatorze obliczeń hello.
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a>Przykład polecenia toopackage usługi w chmurze
Witaj poniższym przykładzie jest tworzony pakiet aplikacji zawierający informacje powitania dla roli sieci web. polecenie Hello określa toouse pliku definicji usługi hello, hello katalogu, gdzie mogą być pliki binarne znaleziono i nazwa pliku pakietu hello hello.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

Jeśli aplikacja hello zawiera zarówno rola sieci web i roli proces roboczy, hello następujące polecenie służy:

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

Gdzie hello zmienne są zdefiniowane w następujący sposób:

| Zmienna | Wartość |
| --- | --- |
| \[DirectoryName\] |Witaj podkatalogu w katalogu projektu na głównym hello zawierający plik csdef hello hello Azure projektu. |
| \[ServiceDefinition\] |Nazwa pliku definicji usługi hello Hello. Domyślnie ten plik ma nazwę ServiceDefinition.csdef. |
| \[Nazwa_pliku_wyjściowego\] |Nazwa Hello hello wygenerowany plik pakietu. Zazwyczaj jest to ustawienie toohello Nazwa aplikacji hello. Jeśli nazwa pliku nie jest określona, pakiet aplikacji hello jest tworzony jako \[ApplicationName\]cspkg. |
| \[RoleName\] |Nazwa Hello roli hello zgodnie z definicją w pliku definicji usługi hello. |
| \[RoleBinariesDirectory] |Lokalizacja Hello hello plików binarnych roli hello. |
| \[Właściwość VirtualPath\] |Witaj katalogów fizycznych dla każdej ścieżki wirtualnej określona w sekcji witryn hello hello definicji usługi. |
| \[PhysicalPath\] |katalogi fizyczne Hello hello zawartości dla każdej ścieżki wirtualnej zdefiniowany w węźle lokacji hello hello definicji usługi. |
| \[RoleAssemblyName\] |Nazwa Hello hello pliku binarnego hello roli. |

## <a name="next-steps"></a>Następne kroki
Tworzenia pakietu usług chmury i chcę...

* [Ustawienia pulpitu zdalnego dla wystąpienia usługi chmury][remotedesktop]
* [Wdrażanie projektu usługi w chmurze][deploy]

Używam programu Visual Studio i chcę...

* [Utwórz nową usługę w chmurze][vs_create]
* [Skonfiguruj ponownie istniejącej usługi w chmurze][vs_reconfigure]
* [Wdrażanie projektu usługi w chmurze][vs_deploy]
* [Ustawienia pulpitu zdalnego dla wystąpienia usługi chmury][vs_remote]

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
