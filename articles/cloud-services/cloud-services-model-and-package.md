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
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="456bd-103">Co to jest model usługi w chmurze hello i jak jest pakiet?</span><span class="sxs-lookup"><span data-stu-id="456bd-103">What is hello Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="456bd-104">Usługi w chmurze jest tworzona na podstawie trzech składników, definicji usługi hello *(csdef)*, hello konfiguracji usługi *(cscfg)*, a pakiet usługi *(cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="456bd-104">A cloud service is created from three components, hello service definition *(.csdef)*, hello service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="456bd-105">Zarówno hello **ServiceDefinition.csdef** i **ServiceConfig.cscfg** plików są oparte na języku XML i opisano strukturę hello hello usługi w chmurze i sposobu jego konfiguracji; nazywane hello modelu.</span><span class="sxs-lookup"><span data-stu-id="456bd-105">Both hello **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe hello structure of hello cloud service and how it's configured; collectively called hello model.</span></span> <span data-ttu-id="456bd-106">Witaj **ServicePackage.cspkg** plik zip, który jest generowany na podstawie hello **ServiceDefinition.csdef** i między innymi zawiera wszystkie wymagane hello zależności formacie binarnym.</span><span class="sxs-lookup"><span data-stu-id="456bd-106">hello **ServicePackage.cspkg** is a zip file that is generated from hello **ServiceDefinition.csdef** and among other things, contains all hello required binary-based dependencies.</span></span> <span data-ttu-id="456bd-107">Platforma Azure tworzy usługi w chmurze z obu hello **ServicePackage.cspkg** i hello **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="456bd-107">Azure creates a cloud service from both hello **ServicePackage.cspkg** and hello **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="456bd-108">Po uruchomieniu usługi chmury hello na platformie Azure, można ponownie skonfigurować go za pośrednictwem hello **ServiceConfig.cscfg** pliku, ale nie można zmienić definicji hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-108">Once hello cloud service is running in Azure, you can reconfigure it through hello **ServiceConfig.cscfg** file, but you cannot alter hello definition.</span></span>

## <a name="what-would-you-like-tooknow-more-about"></a><span data-ttu-id="456bd-109">Co chcesz tooknow więcej informacji na temat?</span><span class="sxs-lookup"><span data-stu-id="456bd-109">What would you like tooknow more about?</span></span>
* <span data-ttu-id="456bd-110">Chcę uzyskać więcej informacji na temat hello tooknow [ServiceDefinition.csdef](#csdef) i [ServiceConfig.cscfg](#cscfg) plików.</span><span class="sxs-lookup"><span data-stu-id="456bd-110">I want tooknow more about hello [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="456bd-111">Już wiem, temat, który można uzyskać [przykłady](#next-steps) na to, co można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="456bd-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="456bd-112">Chcę toocreate hello [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="456bd-112">I want toocreate hello [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="456bd-113">Używam programu Visual Studio i chcę...</span><span class="sxs-lookup"><span data-stu-id="456bd-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="456bd-114">[Tworzenie usługi w chmurze][vs_create]</span><span class="sxs-lookup"><span data-stu-id="456bd-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="456bd-115">[Skonfiguruj ponownie istniejącej usługi w chmurze][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="456bd-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="456bd-116">[Wdrażanie projektu usługi w chmurze][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="456bd-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="456bd-117">[Pulpit zdalny w wystąpieniu usługi chmury][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="456bd-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="456bd-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="456bd-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="456bd-119">Witaj **ServiceDefinition.csdef** pliku określa hello ustawienia, które są używane przez Azure tooconfigure usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="456bd-119">hello **ServiceDefinition.csdef** file specifies hello settings that are used by Azure tooconfigure a cloud service.</span></span> <span data-ttu-id="456bd-120">Witaj [schematu definicji usługi Azure (pliki csdef pliku)](https://msdn.microsoft.com/library/azure/ee758711.aspx) zapewnia hello dopuszczalny formatu pliku definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="456bd-120">hello [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides hello allowable format for a service definition file.</span></span> <span data-ttu-id="456bd-121">Witaj poniższym przykładzie przedstawiono hello ustawień, które mogą być definiowane dla hello sieci Web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="456bd-121">hello following example shows hello settings that can be defined for hello Web and Worker roles:</span></span>

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

<span data-ttu-id="456bd-122">Może się odwoływać toohello [schematu definicji usługi](https://msdn.microsoft.com/library/azure/ee758711.aspx) w celu lepszego zrozumienia hello schematu XML używane w tym miejscu, jednak w tym miejscu jest szybkie wyjaśnienie niektórych elementów hello:</span><span class="sxs-lookup"><span data-stu-id="456bd-122">You can refer toohello [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of hello XML schema used here, however, here is a quick explanation of some of hello elements:</span></span>

<span data-ttu-id="456bd-123">**Lokacje**</span><span class="sxs-lookup"><span data-stu-id="456bd-123">**Sites**</span></span>  
<span data-ttu-id="456bd-124">Zawiera definicje hello witryn sieci Web lub sieci web aplikacji, które są obsługiwane w programie IIS7.</span><span class="sxs-lookup"><span data-stu-id="456bd-124">Contains hello definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="456bd-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="456bd-125">**InputEndpoints**</span></span>  
<span data-ttu-id="456bd-126">Zawiera definicje hello punktów końcowych, które są używane usługi w chmurze hello toocontact.</span><span class="sxs-lookup"><span data-stu-id="456bd-126">Contains hello definitions for endpoints that are used toocontact hello cloud service.</span></span>

<span data-ttu-id="456bd-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="456bd-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="456bd-128">Zawiera definicje hello punktów końcowych, które są używane przez toocommunicate wystąpień roli ze sobą.</span><span class="sxs-lookup"><span data-stu-id="456bd-128">Contains hello definitions for endpoints that are used by role instances toocommunicate with each other.</span></span>

<span data-ttu-id="456bd-129">**AppSettings**</span><span class="sxs-lookup"><span data-stu-id="456bd-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="456bd-130">Zawiera definicje ustawienie hello funkcji określoną rolę.</span><span class="sxs-lookup"><span data-stu-id="456bd-130">Contains hello setting definitions for features of a specific role.</span></span>

<span data-ttu-id="456bd-131">**Certyfikaty**</span><span class="sxs-lookup"><span data-stu-id="456bd-131">**Certificates**</span></span>  
<span data-ttu-id="456bd-132">Zawiera definicje hello certyfikaty, które są wymagane przez rolę.</span><span class="sxs-lookup"><span data-stu-id="456bd-132">Contains hello definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="456bd-133">Witaj poprzednim przykładzie kodu przedstawiono certyfikatu, który służy do konfiguracji hello Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="456bd-133">hello previous code example shows a certificate that is used for hello configuration of Azure Connect.</span></span>

<span data-ttu-id="456bd-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="456bd-134">**LocalResources**</span></span>  
<span data-ttu-id="456bd-135">Zawiera definicje hello zasoby magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="456bd-135">Contains hello definitions for local storage resources.</span></span> <span data-ttu-id="456bd-136">Zasób Magazyn lokalny jest zastrzeżony katalogu w systemie plików hello hello maszyny wirtualnej, w którym jest uruchomione wystąpienie roli.</span><span class="sxs-lookup"><span data-stu-id="456bd-136">A local storage resource is a reserved directory on hello file system of hello virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="456bd-137">**Importy**</span><span class="sxs-lookup"><span data-stu-id="456bd-137">**Imports**</span></span>  
<span data-ttu-id="456bd-138">Zawiera definicje hello zaimportowanych modułów.</span><span class="sxs-lookup"><span data-stu-id="456bd-138">Contains hello definitions for imported modules.</span></span> <span data-ttu-id="456bd-139">Witaj poprzednim przykładzie kodu pokazują moduły hello Podłączanie pulpitu zdalnego i Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="456bd-139">hello previous code example shows hello modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="456bd-140">**Uruchamianie**</span><span class="sxs-lookup"><span data-stu-id="456bd-140">**Startup**</span></span>  
<span data-ttu-id="456bd-141">Zawiera zadania, które są uruchamiane podczas uruchamiania hello roli.</span><span class="sxs-lookup"><span data-stu-id="456bd-141">Contains tasks that are run when hello role starts.</span></span> <span data-ttu-id="456bd-142">zadania Hello są definiowane w .cmd lub pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="456bd-142">hello tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="456bd-143">Pliku ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="456bd-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="456bd-144">Konfiguracja Hello hello ustawień usługi w chmurze zależy od wartości hello hello **pliku ServiceConfiguration.cscfg** pliku.</span><span class="sxs-lookup"><span data-stu-id="456bd-144">hello configuration of hello settings for your cloud service is determined by hello values in hello **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="456bd-145">Można określić numer hello wystąpień mają toodeploy dla każdej roli, w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="456bd-145">You specify hello number of instances that you want toodeploy for each role in this file.</span></span> <span data-ttu-id="456bd-146">wartości ustawienia konfiguracji hello zdefiniowane w pliku definicji usługi hello Hello są dodawane pliku konfiguracji usługi toohello.</span><span class="sxs-lookup"><span data-stu-id="456bd-146">hello values for hello configuration settings that you defined in hello service definition file are added toohello service configuration file.</span></span> <span data-ttu-id="456bd-147">odciski palców Hello dotyczące wszystkich certyfikatów zarządzania skojarzonych z usługą w chmurze hello dodawane są także toohello pliku.</span><span class="sxs-lookup"><span data-stu-id="456bd-147">hello thumbprints for any management certificates that are associated with hello cloud service are also added toohello file.</span></span> <span data-ttu-id="456bd-148">Witaj [schemat konfiguracji usługi Azure (cscfg pliku)](https://msdn.microsoft.com/library/azure/ee758710.aspx) zapewnia hello dozwolony format pliku konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="456bd-148">hello [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides hello allowable format for a service configuration file.</span></span>

<span data-ttu-id="456bd-149">Hello pliku konfiguracji usługi nie jest dostarczana z aplikacji hello, ale jest tooAzure przekazany jako osobny plik i hello tooconfigure używana jest usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="456bd-149">hello service configuration file is not packaged with hello application, but is uploaded tooAzure as a separate file and is used tooconfigure hello cloud service.</span></span> <span data-ttu-id="456bd-150">Możesz przekazać plik konfiguracji usługi bez ponownego wdrożenia usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="456bd-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="456bd-151">można zmienić Hello wartości konfiguracji dla usługi w chmurze hello jest uruchomiona usługa w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-151">hello configuration values for hello cloud service can be changed while hello cloud service is running.</span></span> <span data-ttu-id="456bd-152">Witaj poniższym przykładzie przedstawiono hello ustawienia konfiguracji, które mogą być definiowane dla hello sieci Web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="456bd-152">hello following example shows hello configuration settings that can be defined for hello Web and Worker roles:</span></span>

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

<span data-ttu-id="456bd-153">Może się odwoływać toohello [schemat konfiguracji usługi](https://msdn.microsoft.com/library/azure/ee758710.aspx) do lepszego zrozumienia hello schematu XML używane w tym miejscu, jednak w tym miejscu jest szybkie wyjaśnienie hello elementów:</span><span class="sxs-lookup"><span data-stu-id="456bd-153">You can refer toohello [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding hello XML schema used here, however, here is a quick explanation of hello elements:</span></span>

<span data-ttu-id="456bd-154">**Wystąpienia**</span><span class="sxs-lookup"><span data-stu-id="456bd-154">**Instances**</span></span>  
<span data-ttu-id="456bd-155">Umożliwia skonfigurowanie liczby hello uruchomionych wystąpień roli hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-155">Configures hello number of running instances for hello role.</span></span> <span data-ttu-id="456bd-156">tooprevent usługi chmury z potencjalnie stać się niedostępne podczas uaktualniania, zaleca się wdrożenie więcej niż jednego wystąpienia ról udostępnianych w sieci web.</span><span class="sxs-lookup"><span data-stu-id="456bd-156">tooprevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="456bd-157">Przez wdrożenie więcej niż jedno wystąpienie, są spełnione wytyczne toohello w hello [Azure obliczeniowe poziom Umowa dotycząca usług (SLA)](http://azure.microsoft.com/support/legal/sla/), który zapewnia łączność zewnętrzną 99,95% dla ról połączonych z Internetem, gdy dwie lub więcej ról wystąpienia są wdrażane dla usługi.</span><span class="sxs-lookup"><span data-stu-id="456bd-157">By deploying more than one instance, you are adhering toohello guidelines in hello [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="456bd-158">**AppSettings**</span><span class="sxs-lookup"><span data-stu-id="456bd-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="456bd-159">Konfiguruje ustawienia hello hello uruchomionych wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="456bd-159">Configures hello settings for hello running instances for a role.</span></span> <span data-ttu-id="456bd-160">Nazwa Hello hello `<Setting>` elementy muszą być zgodne hello definicji ustawień w pliku definicji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-160">hello name of hello `<Setting>` elements must match hello setting definitions in hello service definition file.</span></span>

<span data-ttu-id="456bd-161">**Certyfikaty**</span><span class="sxs-lookup"><span data-stu-id="456bd-161">**Certificates**</span></span>  
<span data-ttu-id="456bd-162">Konfiguruje hello certyfikaty, które są używane przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-162">Configures hello certificates that are used by hello service.</span></span> <span data-ttu-id="456bd-163">Hello poprzednim przykładzie kodu pokazano, jak toodefine hello certyfikat dla hello RemoteAccess modułu.</span><span class="sxs-lookup"><span data-stu-id="456bd-163">hello previous code example shows how toodefine hello certificate for hello RemoteAccess module.</span></span> <span data-ttu-id="456bd-164">Witaj wartość hello *odcisk palca* należy ustawić atrybut toohello odcisk palca hello toouse certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="456bd-164">hello value of hello *thumbprint* attribute must be set toohello thumbprint of hello certificate toouse.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="456bd-165">Witaj odcisk palca certyfikatu hello można dodać plik konfiguracji toohello za pomocą edytora tekstu.</span><span class="sxs-lookup"><span data-stu-id="456bd-165">hello thumbprint for hello certificate can be added toohello configuration file by using a text editor.</span></span> <span data-ttu-id="456bd-166">Lub wartość hello można dodać na powitania **certyfikaty** kartę hello **właściwości** strony roli hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="456bd-166">Or, hello value can be added on hello **Certificates** tab of hello **Properties** page of hello role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="456bd-167">Definiowanie portów dla wystąpień roli</span><span class="sxs-lookup"><span data-stu-id="456bd-167">Defining ports for role instances</span></span>
<span data-ttu-id="456bd-168">Azure umożliwia tylko jedna rola sieci web tooa punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="456bd-168">Azure allows only one entry point tooa web role.</span></span> <span data-ttu-id="456bd-169">Co oznacza, że cały ruch odbywa się przez jeden adres IP.</span><span class="sxs-lookup"><span data-stu-id="456bd-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="456bd-170">Można skonfigurować z witryn sieci Web tooshare port konfigurując hello hosta nagłówka toodirect hello żądania toohello poprawnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="456bd-170">You can configure your websites tooshare a port by configuring hello host header toodirect hello request toohello correct location.</span></span> <span data-ttu-id="456bd-171">Można także skonfigurować porty znane toowell toolisten Twojej aplikacji hello adresu IP.</span><span class="sxs-lookup"><span data-stu-id="456bd-171">You can also configure your applications toolisten toowell-known ports on hello IP address.</span></span>

<span data-ttu-id="456bd-172">Witaj poniższy przykład przedstawia hello konfigurację dla roli sieci web z aplikacji sieci web i witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="456bd-172">hello following sample shows hello configuration for a web role with a website and web application.</span></span> <span data-ttu-id="456bd-173">Hello witryny sieci Web jest skonfigurowana jako hello domyślny wpis lokalizacji na porcie 80, a aplikacje sieci web hello są żądania tooreceive skonfigurowany z nagłówka alternatywnego hosta, który jest nazywany "mail.mysite.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="456bd-173">hello website is configured as hello default entry location on port 80, and hello web applications are configured tooreceive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

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


## <a name="changing-hello-configuration-of-a-role"></a><span data-ttu-id="456bd-174">Zmiana konfiguracji hello roli</span><span class="sxs-lookup"><span data-stu-id="456bd-174">Changing hello configuration of a role</span></span>
<span data-ttu-id="456bd-175">Należy zaktualizować hello konfiguracji usługi w chmurze, jest uruchomiona na platformie Azure, bez konieczności przełączania w tryb offline usługa hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-175">You can update hello configuration of your cloud service while it is running in Azure, without taking hello service offline.</span></span> <span data-ttu-id="456bd-176">toochange informacje o konfiguracji, należy albo Przekaż nowy plik konfiguracji, lub edycji pliku konfiguracji hello w Umieść i zastosować je tooyour, na którym działa usługa.</span><span class="sxs-lookup"><span data-stu-id="456bd-176">toochange configuration information, you can either upload a new configuration file, or edit hello configuration file in place and apply it tooyour running service.</span></span> <span data-ttu-id="456bd-177">Witaj następujących zmian w konfiguracji toohello usługi:</span><span class="sxs-lookup"><span data-stu-id="456bd-177">hello following changes can be made toohello configuration of a service:</span></span>

* <span data-ttu-id="456bd-178">**Zmiana wartości hello ustawień konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="456bd-178">**Changing hello values of configuration settings**</span></span>  
  <span data-ttu-id="456bd-179">Podczas konfiguracji zmiany, ustawień wystąpienia roli można bezpiecznie wybierz tooapply hello zmiany podczas hello wystąpienie jest w trybie online lub toorecycle hello wystąpienia i stosować zmiany hello podczas hello wystąpienie jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="456bd-179">When a configuration setting changes, a role instance can choose tooapply hello change while hello instance is online, or toorecycle hello instance gracefully and apply hello change while hello instance is offline.</span></span>
* <span data-ttu-id="456bd-180">**Zmiany topologii usługa hello wystąpień roli**</span><span class="sxs-lookup"><span data-stu-id="456bd-180">**Changing hello service topology of role instances**</span></span>  
  <span data-ttu-id="456bd-181">Topologia zmiany nie wpływają na uruchomione wystąpienia, z wyjątkiem przypadków, gdy wystąpienie jest usuwana.</span><span class="sxs-lookup"><span data-stu-id="456bd-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="456bd-182">Wszystkie pozostałe wystąpienia zazwyczaj nie są toobe ponownego przetworzenia; jednak można wybrać toorecycle wystąpień roli w przypadku zmiany topologii tooa odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="456bd-182">All remaining instances generally do not need toobe recycled; however, you can choose toorecycle role instances in response tooa topology change.</span></span>
* <span data-ttu-id="456bd-183">**Zmiana hello odcisk palca certyfikatu**</span><span class="sxs-lookup"><span data-stu-id="456bd-183">**Changing hello certificate thumbprint**</span></span>  
  <span data-ttu-id="456bd-184">Certyfikat można aktualizować tylko wtedy, gdy wystąpienie roli jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="456bd-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="456bd-185">Jeśli certyfikat jest dodany, usunięty lub zmieniony, gdy wystąpienie roli jest w trybie online, Azure bezpiecznie ma hello wystąpienia w trybie offline tooupdate hello certyfikatu i przełączenie go do trybu online po zakończeniu zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes hello instance offline tooupdate hello certificate and bring it back online after hello change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="456bd-186">Obsługa zmiany w konfiguracji o zdarzeniach środowiska uruchomieniowego usługi</span><span class="sxs-lookup"><span data-stu-id="456bd-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="456bd-187">Witaj [biblioteki środowiska uruchomieniowego usługi Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) obejmuje hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) przestrzeni nazw, która udostępnia klasy do interakcji z hello środowiska platformy Azure z roli.</span><span class="sxs-lookup"><span data-stu-id="456bd-187">hello [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with hello Azure environment from a role.</span></span> <span data-ttu-id="456bd-188">Witaj [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) klasa definiuje hello następujące zdarzenia, które są wywoływane przed i po zmianie konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="456bd-188">hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines hello following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="456bd-189">**[Zmiana](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="456bd-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="456bd-190">Dzieje się tak, zanim zmiana konfiguracji hello jest stosowane tooa określonego wystąpienia roli, umożliwiając tootake szansy, dół hello wystąpień roli w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="456bd-190">This occurs before hello configuration change is applied tooa specified instance of a role giving you a chance tootake down hello role instances if necessary.</span></span>
* <span data-ttu-id="456bd-191">**[Zmienione](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="456bd-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="456bd-192">Występuje, gdy zmiana konfiguracji hello jest stosowane tooa określonego wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="456bd-192">Occurs after hello configuration change is applied tooa specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="456bd-193">Ponieważ zmiany certyfikatu zawsze pobierają hello wystąpień roli w tryb offline, nie wygenerował hello RoleEnvironment.Changing lub RoleEnvironment.Changed zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="456bd-193">Because certificate changes always take hello instances of a role offline, they do not raise hello RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="456bd-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="456bd-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="456bd-195">toodeploy aplikacji jako usługa w chmurze na platformie Azure, należy najpierw pierwszej aplikacji hello pakietu w odpowiednim formacie hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-195">toodeploy an application as a cloud service in Azure, you must first package hello application in hello appropriate format.</span></span> <span data-ttu-id="456bd-196">Można użyć hello **CSPack** narzędzia wiersza polecenia (zainstalowaną z hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/)) pliku pakietu hello toocreate jako alternatywne tooVisual w Studio.</span><span class="sxs-lookup"><span data-stu-id="456bd-196">You can use hello **CSPack** command-line tool (installed with hello [Azure SDK](https://azure.microsoft.com/downloads/)) toocreate hello package file as an alternative tooVisual Studio.</span></span>

<span data-ttu-id="456bd-197">**CSPack** używa hello zawartość hello usługi definicji usługi plików i konfiguracji toodefine hello zawartość pliku hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="456bd-197">**CSPack** uses hello contents of hello service definition file and service configuration file toodefine hello contents of hello package.</span></span> <span data-ttu-id="456bd-198">**CSPack** generuje plik pakietu aplikacji (cspkg) przekazać tooAzure przy użyciu hello [portalu Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="456bd-198">**CSPack** generates an application package file (.cspkg) that you can upload tooAzure by using hello [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="456bd-199">Domyślnie hello pakietu o nazwie `[ServiceDefinitionFileName].cspkg`, ale możesz określić inną nazwę przy użyciu hello `/out` opcji **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="456bd-199">By default, hello package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using hello `/out` option of **CSPack**.</span></span>

<span data-ttu-id="456bd-200">**CSPack** znajduje się pod adresem</span><span class="sxs-lookup"><span data-stu-id="456bd-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="456bd-201">CSPack.exe (w systemie windows) jest dostępny, uruchamiając hello **wiersza polecenia usługi Microsoft Azure** skrót, który jest instalowany z hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="456bd-201">CSPack.exe (on windows) is available by running hello **Microsoft Azure Command Prompt** shortcut that is installed with hello SDK.</span></span>  
> 
> <span data-ttu-id="456bd-202">Uruchom hello CSPack.exe program samodzielnie dokumentacji toosee wszystkie przełączniki możliwe hello i poleceń.</span><span class="sxs-lookup"><span data-stu-id="456bd-202">Run hello CSPack.exe program by itself toosee documentation about all hello possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="456bd-203">Uruchamianie usługi w chmurze lokalnie w hello **Microsoft Azure obliczeniowe emulatora**, użyj hello **/copyonly** opcji.</span><span class="sxs-lookup"><span data-stu-id="456bd-203">Run your cloud service locally in hello **Microsoft Azure Compute Emulator**, use hello **/copyonly** option.</span></span> <span data-ttu-id="456bd-204">Ta opcja powoduje skopiowanie plików binarnych hello aplikacji hello tooa katalogu układu z którego może działać w emulatorze obliczeń hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-204">This option copies hello binary files for hello application tooa directory layout from which they can be run in hello compute emulator.</span></span>
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a><span data-ttu-id="456bd-205">Przykład polecenia toopackage usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="456bd-205">Example command toopackage a cloud service</span></span>
<span data-ttu-id="456bd-206">Witaj poniższym przykładzie jest tworzony pakiet aplikacji zawierający informacje powitania dla roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="456bd-206">hello following example creates an application package that contains hello information for a web role.</span></span> <span data-ttu-id="456bd-207">polecenie Hello określa toouse pliku definicji usługi hello, hello katalogu, gdzie mogą być pliki binarne znaleziono i nazwa pliku pakietu hello hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-207">hello command specifies hello service definition file toouse, hello directory where binary files can be found, and hello name of hello package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="456bd-208">Jeśli aplikacja hello zawiera zarówno rola sieci web i roli proces roboczy, hello następujące polecenie służy:</span><span class="sxs-lookup"><span data-stu-id="456bd-208">If hello application contains both a web role and a worker role, hello following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="456bd-209">Gdzie hello zmienne są zdefiniowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="456bd-209">Where hello variables are defined as follows:</span></span>

| <span data-ttu-id="456bd-210">Zmienna</span><span class="sxs-lookup"><span data-stu-id="456bd-210">Variable</span></span> | <span data-ttu-id="456bd-211">Wartość</span><span class="sxs-lookup"><span data-stu-id="456bd-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="456bd-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="456bd-212">\[DirectoryName\]</span></span> |<span data-ttu-id="456bd-213">Witaj podkatalogu w katalogu projektu na głównym hello zawierający plik csdef hello hello Azure projektu.</span><span class="sxs-lookup"><span data-stu-id="456bd-213">hello subdirectory under hello root project directory that contains hello .csdef file of hello Azure project.</span></span> |
| <span data-ttu-id="456bd-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="456bd-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="456bd-215">Nazwa pliku definicji usługi hello Hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-215">hello name of hello service definition file.</span></span> <span data-ttu-id="456bd-216">Domyślnie ten plik ma nazwę ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="456bd-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="456bd-217">\[Nazwa_pliku_wyjściowego\]</span><span class="sxs-lookup"><span data-stu-id="456bd-217">\[OutputFileName\]</span></span> |<span data-ttu-id="456bd-218">Nazwa Hello hello wygenerowany plik pakietu.</span><span class="sxs-lookup"><span data-stu-id="456bd-218">hello name for hello generated package file.</span></span> <span data-ttu-id="456bd-219">Zazwyczaj jest to ustawienie toohello Nazwa aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-219">Typically, this is set toohello name of hello application.</span></span> <span data-ttu-id="456bd-220">Jeśli nazwa pliku nie jest określona, pakiet aplikacji hello jest tworzony jako \[ApplicationName\]cspkg.</span><span class="sxs-lookup"><span data-stu-id="456bd-220">If no file name is specified, hello application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="456bd-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="456bd-221">\[RoleName\]</span></span> |<span data-ttu-id="456bd-222">Nazwa Hello roli hello zgodnie z definicją w pliku definicji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-222">hello name of hello role as defined in hello service definition file.</span></span> |
| <span data-ttu-id="456bd-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="456bd-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="456bd-224">Lokalizacja Hello hello plików binarnych roli hello.</span><span class="sxs-lookup"><span data-stu-id="456bd-224">hello location of hello binary files for hello role.</span></span> |
| <span data-ttu-id="456bd-225">\[Właściwość VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="456bd-225">\[VirtualPath\]</span></span> |<span data-ttu-id="456bd-226">Witaj katalogów fizycznych dla każdej ścieżki wirtualnej określona w sekcji witryn hello hello definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="456bd-226">hello physical directories for each virtual path defined in hello Sites section of hello service definition.</span></span> |
| <span data-ttu-id="456bd-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="456bd-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="456bd-228">katalogi fizyczne Hello hello zawartości dla każdej ścieżki wirtualnej zdefiniowany w węźle lokacji hello hello definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="456bd-228">hello physical directories of hello contents for each virtual path defined in hello site node of hello service definition.</span></span> |
| <span data-ttu-id="456bd-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="456bd-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="456bd-230">Nazwa Hello hello pliku binarnego hello roli.</span><span class="sxs-lookup"><span data-stu-id="456bd-230">hello name of hello binary file for hello role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="456bd-231">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="456bd-231">Next steps</span></span>
<span data-ttu-id="456bd-232">Tworzenia pakietu usług chmury i chcę...</span><span class="sxs-lookup"><span data-stu-id="456bd-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="456bd-233">[Ustawienia pulpitu zdalnego dla wystąpienia usługi chmury][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="456bd-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="456bd-234">[Wdrażanie projektu usługi w chmurze][deploy]</span><span class="sxs-lookup"><span data-stu-id="456bd-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="456bd-235">Używam programu Visual Studio i chcę...</span><span class="sxs-lookup"><span data-stu-id="456bd-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="456bd-236">[Utwórz nową usługę w chmurze][vs_create]</span><span class="sxs-lookup"><span data-stu-id="456bd-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="456bd-237">[Skonfiguruj ponownie istniejącej usługi w chmurze][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="456bd-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="456bd-238">[Wdrażanie projektu usługi w chmurze][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="456bd-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="456bd-239">[Ustawienia pulpitu zdalnego dla wystąpienia usługi chmury][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="456bd-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
