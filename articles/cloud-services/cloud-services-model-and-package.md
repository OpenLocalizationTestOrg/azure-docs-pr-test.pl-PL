---
title: "Co to jest usługa w chmurze modelu i pakietu | Dokumentacja firmy Microsoft"
description: "Opisuje modelem usługi chmury (pliki csdef, .cscfg) i pakietu (cspkg) na platformie Azure"
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
ms.openlocfilehash: 21fbdbc4c24440c6fbbd7487cfbb2e0a3140aa96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="2b307-103">Co to jest model usługi w chmurze i jak jest pakiet?</span><span class="sxs-lookup"><span data-stu-id="2b307-103">What is the Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="2b307-104">Usługi w chmurze jest tworzona na podstawie trzech składników, definicji usługi *(csdef)*, konfiguracji usługi *(cscfg)*, a pakiet usługi *(cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="2b307-104">A cloud service is created from three components, the service definition *(.csdef)*, the service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="2b307-105">Zarówno **ServiceDefinition.csdef** i **ServiceConfig.cscfg** plików są oparte na języku XML i opisano strukturę usługi w chmurze i sposobu jego konfiguracji; nazywane modelu.</span><span class="sxs-lookup"><span data-stu-id="2b307-105">Both the **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe the structure of the cloud service and how it's configured; collectively called the model.</span></span> <span data-ttu-id="2b307-106">**ServicePackage.cspkg** plik zip, który jest generowany na podstawie **ServiceDefinition.csdef** i między innymi zawiera wszystkie zależności wymagane formacie binarnym.</span><span class="sxs-lookup"><span data-stu-id="2b307-106">The **ServicePackage.cspkg** is a zip file that is generated from the **ServiceDefinition.csdef** and among other things, contains all the required binary-based dependencies.</span></span> <span data-ttu-id="2b307-107">Platforma Azure tworzy usługi w chmurze z obu **ServicePackage.cspkg** i **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="2b307-107">Azure creates a cloud service from both the **ServicePackage.cspkg** and the **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="2b307-108">Gdy usługa w chmurze jest uruchomiona na platformie Azure, można ponownie skonfigurować go za pośrednictwem **ServiceConfig.cscfg** pliku, ale nie można zmienić definicji.</span><span class="sxs-lookup"><span data-stu-id="2b307-108">Once the cloud service is running in Azure, you can reconfigure it through the **ServiceConfig.cscfg** file, but you cannot alter the definition.</span></span>

## <a name="what-would-you-like-to-know-more-about"></a><span data-ttu-id="2b307-109">Co chcesz dowiedzieć się więcej o?</span><span class="sxs-lookup"><span data-stu-id="2b307-109">What would you like to know more about?</span></span>
* <span data-ttu-id="2b307-110">Chcę, aby dowiedzieć się więcej o [ServiceDefinition.csdef](#csdef) i [ServiceConfig.cscfg](#cscfg) plików.</span><span class="sxs-lookup"><span data-stu-id="2b307-110">I want to know more about the [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="2b307-111">Już wiem, temat, który można uzyskać [przykłady](#next-steps) na to, co można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="2b307-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="2b307-112">Utwórz [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="2b307-112">I want to create the [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="2b307-113">Używam programu Visual Studio i chcę...</span><span class="sxs-lookup"><span data-stu-id="2b307-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="2b307-114">[Tworzenie usługi w chmurze][vs_create]</span><span class="sxs-lookup"><span data-stu-id="2b307-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="2b307-115">[Skonfiguruj ponownie istniejącej usługi w chmurze][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="2b307-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="2b307-116">[Wdrażanie projektu usługi w chmurze][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="2b307-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="2b307-117">[Pulpit zdalny w wystąpieniu usługi chmury][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="2b307-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="2b307-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="2b307-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="2b307-119">**ServiceDefinition.csdef** pliku określa ustawienia, które są używane przez usługi Azure, aby skonfigurować usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2b307-119">The **ServiceDefinition.csdef** file specifies the settings that are used by Azure to configure a cloud service.</span></span> <span data-ttu-id="2b307-120">[Schematu definicji usługi Azure (pliki csdef pliku)](https://msdn.microsoft.com/library/azure/ee758711.aspx) zapewnia dopuszczalny formatu pliku definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="2b307-120">The [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides the allowable format for a service definition file.</span></span> <span data-ttu-id="2b307-121">W poniższym przykładzie przedstawiono ustawienia, które mogą być definiowane dla ról sieć Web i procesu roboczego:</span><span class="sxs-lookup"><span data-stu-id="2b307-121">The following example shows the settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="2b307-122">Można to sprawdzić [schematu definicji usługi](https://msdn.microsoft.com/library/azure/ee758711.aspx) w celu lepszego zrozumienia schematu XML używane w tym miejscu, jednak w tym miejscu jest szybkie wyjaśnienie niektórych elementów:</span><span class="sxs-lookup"><span data-stu-id="2b307-122">You can refer to the [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of the XML schema used here, however, here is a quick explanation of some of the elements:</span></span>

<span data-ttu-id="2b307-123">**Lokacje**</span><span class="sxs-lookup"><span data-stu-id="2b307-123">**Sites**</span></span>  
<span data-ttu-id="2b307-124">Zawiera definicje dla witryn sieci Web lub sieci web aplikacji, które są obsługiwane w programie IIS7.</span><span class="sxs-lookup"><span data-stu-id="2b307-124">Contains the definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="2b307-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="2b307-125">**InputEndpoints**</span></span>  
<span data-ttu-id="2b307-126">Zawiera definicje dla punktów końcowych, które są używane do kontaktowania się z usługą w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2b307-126">Contains the definitions for endpoints that are used to contact the cloud service.</span></span>

<span data-ttu-id="2b307-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="2b307-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="2b307-128">Zawiera definicje dla punktów końcowych, które są używane przez wystąpień roli do komunikowania się ze sobą.</span><span class="sxs-lookup"><span data-stu-id="2b307-128">Contains the definitions for endpoints that are used by role instances to communicate with each other.</span></span>

<span data-ttu-id="2b307-129">**AppSettings**</span><span class="sxs-lookup"><span data-stu-id="2b307-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="2b307-130">Zawiera definicje ustawienie funkcji określonej roli.</span><span class="sxs-lookup"><span data-stu-id="2b307-130">Contains the setting definitions for features of a specific role.</span></span>

<span data-ttu-id="2b307-131">**Certyfikaty**</span><span class="sxs-lookup"><span data-stu-id="2b307-131">**Certificates**</span></span>  
<span data-ttu-id="2b307-132">Zawiera definicje dla certyfikatów, które są wymagane przez rolę.</span><span class="sxs-lookup"><span data-stu-id="2b307-132">Contains the definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="2b307-133">W poprzednim przykładzie kodu przedstawiono certyfikatu, który służy do konfiguracji połączenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2b307-133">The previous code example shows a certificate that is used for the configuration of Azure Connect.</span></span>

<span data-ttu-id="2b307-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="2b307-134">**LocalResources**</span></span>  
<span data-ttu-id="2b307-135">Zawiera definicje dla zasobów magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="2b307-135">Contains the definitions for local storage resources.</span></span> <span data-ttu-id="2b307-136">Zasób Magazyn lokalny jest zastrzeżony katalogu w systemie plików, w którym jest uruchomione wystąpienie roli maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b307-136">A local storage resource is a reserved directory on the file system of the virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="2b307-137">**Importy**</span><span class="sxs-lookup"><span data-stu-id="2b307-137">**Imports**</span></span>  
<span data-ttu-id="2b307-138">Zawiera definicje dla zaimportowanych modułów.</span><span class="sxs-lookup"><span data-stu-id="2b307-138">Contains the definitions for imported modules.</span></span> <span data-ttu-id="2b307-139">W poprzednim przykładzie kodu pokazuje modułów dla usługi Podłączanie pulpitu zdalnego i połącz Azure.</span><span class="sxs-lookup"><span data-stu-id="2b307-139">The previous code example shows the modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="2b307-140">**Uruchamianie**</span><span class="sxs-lookup"><span data-stu-id="2b307-140">**Startup**</span></span>  
<span data-ttu-id="2b307-141">Zawiera zadania, które są uruchamiane podczas uruchamiania roli.</span><span class="sxs-lookup"><span data-stu-id="2b307-141">Contains tasks that are run when the role starts.</span></span> <span data-ttu-id="2b307-142">Zadania są definiowane w .cmd lub pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="2b307-142">The tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="2b307-143">Pliku ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="2b307-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="2b307-144">Konfiguracja ustawień usługi w chmurze jest określany przez wartości **pliku ServiceConfiguration.cscfg** pliku.</span><span class="sxs-lookup"><span data-stu-id="2b307-144">The configuration of the settings for your cloud service is determined by the values in the **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="2b307-145">Możesz określić liczbę wystąpień, które mają zostać wdrożone dla każdej roli, w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="2b307-145">You specify the number of instances that you want to deploy for each role in this file.</span></span> <span data-ttu-id="2b307-146">Wartości ustawienia konfiguracji, które zostały zdefiniowane w pliku definicji usługi są dodawane do pliku konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="2b307-146">The values for the configuration settings that you defined in the service definition file are added to the service configuration file.</span></span> <span data-ttu-id="2b307-147">Odciski palców wszelkich certyfikatów zarządzania, które są skojarzone z usługą w chmurze, również są dodawane do pliku.</span><span class="sxs-lookup"><span data-stu-id="2b307-147">The thumbprints for any management certificates that are associated with the cloud service are also added to the file.</span></span> <span data-ttu-id="2b307-148">[Schemat konfiguracji usługi Azure (cscfg pliku)](https://msdn.microsoft.com/library/azure/ee758710.aspx) zapewnia dozwolony format pliku konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="2b307-148">The [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides the allowable format for a service configuration file.</span></span>

<span data-ttu-id="2b307-149">Pliku konfiguracji usługi nie jest dostarczana z aplikacją, ale zostało załadowane na platformie Azure jako osobny plik i służy do konfigurowania usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2b307-149">The service configuration file is not packaged with the application, but is uploaded to Azure as a separate file and is used to configure the cloud service.</span></span> <span data-ttu-id="2b307-150">Możesz przekazać plik konfiguracji usługi bez ponownego wdrożenia usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2b307-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="2b307-151">Można zmienić wartości konfiguracji dla usługi w chmurze jest uruchomiona usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2b307-151">The configuration values for the cloud service can be changed while the cloud service is running.</span></span> <span data-ttu-id="2b307-152">W poniższym przykładzie przedstawiono ustawienia konfiguracji, które mogą być definiowane dla ról sieć Web i procesu roboczego:</span><span class="sxs-lookup"><span data-stu-id="2b307-152">The following example shows the configuration settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="2b307-153">Można to sprawdzić [schemat konfiguracji usługi](https://msdn.microsoft.com/library/azure/ee758710.aspx) dla lepiej zrozumieć schematu XML używane w tym miejscu, jednak w tym miejscu jest szybkie wyjaśnienie elementów:</span><span class="sxs-lookup"><span data-stu-id="2b307-153">You can refer to the [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding the XML schema used here, however, here is a quick explanation of the elements:</span></span>

<span data-ttu-id="2b307-154">**Wystąpienia**</span><span class="sxs-lookup"><span data-stu-id="2b307-154">**Instances**</span></span>  
<span data-ttu-id="2b307-155">Umożliwia skonfigurowanie liczby uruchomionych wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="2b307-155">Configures the number of running instances for the role.</span></span> <span data-ttu-id="2b307-156">Aby zapobiec potencjalnie stać się niedostępne podczas uaktualniania usługi w chmurze, zaleca się wdrożenie więcej niż jednego wystąpienia ról udostępnianych w sieci web.</span><span class="sxs-lookup"><span data-stu-id="2b307-156">To prevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="2b307-157">Przez wdrożenie więcej niż jedno wystąpienie, są spełnione wskazówki zawarte w [Azure obliczeniowe poziom Umowa dotycząca usług (SLA)](http://azure.microsoft.com/support/legal/sla/), który zapewnia łączność zewnętrzną 99,95% dla ról połączonych z Internetem, gdy dwie lub więcej wystąpień roli są wdrażane dla usługi.</span><span class="sxs-lookup"><span data-stu-id="2b307-157">By deploying more than one instance, you are adhering to the guidelines in the [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="2b307-158">**AppSettings**</span><span class="sxs-lookup"><span data-stu-id="2b307-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="2b307-159">Konfiguruje ustawienia dla uruchomionych wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="2b307-159">Configures the settings for the running instances for a role.</span></span> <span data-ttu-id="2b307-160">Nazwa `<Setting>` elementy muszą być zgodne definicji ustawień w pliku definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="2b307-160">The name of the `<Setting>` elements must match the setting definitions in the service definition file.</span></span>

<span data-ttu-id="2b307-161">**Certyfikaty**</span><span class="sxs-lookup"><span data-stu-id="2b307-161">**Certificates**</span></span>  
<span data-ttu-id="2b307-162">Konfiguruje certyfikaty, które są używane przez usługę.</span><span class="sxs-lookup"><span data-stu-id="2b307-162">Configures the certificates that are used by the service.</span></span> <span data-ttu-id="2b307-163">W poprzednim przykładzie kodu pokazano, jak można zdefiniować certyfikat dla modułu dostęp zdalny.</span><span class="sxs-lookup"><span data-stu-id="2b307-163">The previous code example shows how to define the certificate for the RemoteAccess module.</span></span> <span data-ttu-id="2b307-164">Wartość *odcisk palca* atrybut musi mieć ustawioną odcisk palca certyfikatu do użycia.</span><span class="sxs-lookup"><span data-stu-id="2b307-164">The value of the *thumbprint* attribute must be set to the thumbprint of the certificate to use.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="2b307-165">Odcisk palca certyfikatu można dodać do pliku konfiguracji za pomocą edytora tekstu.</span><span class="sxs-lookup"><span data-stu-id="2b307-165">The thumbprint for the certificate can be added to the configuration file by using a text editor.</span></span> <span data-ttu-id="2b307-166">Lub może zostać dodana wartość na **certyfikaty** karcie **właściwości** strony roli w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b307-166">Or, the value can be added on the **Certificates** tab of the **Properties** page of the role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="2b307-167">Definiowanie portów dla wystąpień roli</span><span class="sxs-lookup"><span data-stu-id="2b307-167">Defining ports for role instances</span></span>
<span data-ttu-id="2b307-168">Azure umożliwia tylko jeden wpis wskaż roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="2b307-168">Azure allows only one entry point to a web role.</span></span> <span data-ttu-id="2b307-169">Co oznacza, że cały ruch odbywa się przez jeden adres IP.</span><span class="sxs-lookup"><span data-stu-id="2b307-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="2b307-170">Można skonfigurować witryny sieci Web, aby udostępnić portu przez skonfigurowanie nagłówek hosta, należy przekierować żądania do poprawnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="2b307-170">You can configure your websites to share a port by configuring the host header to direct the request to the correct location.</span></span> <span data-ttu-id="2b307-171">Można również skonfigurować aplikacje słuchać dobrze znanych portów na adres IP.</span><span class="sxs-lookup"><span data-stu-id="2b307-171">You can also configure your applications to listen to well-known ports on the IP address.</span></span>

<span data-ttu-id="2b307-172">Poniższy przykład przedstawia konfigurację dla roli sieci web z aplikacji sieci web i witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2b307-172">The following sample shows the configuration for a web role with a website and web application.</span></span> <span data-ttu-id="2b307-173">Witryna sieci Web jest skonfigurowana jako domyślną lokalizację zapisu na porcie 80, a aplikacje sieci web są skonfigurowane do odbierania żądań z nagłówka alternatywnego hosta, który jest nazywany "mail.mysite.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="2b307-173">The website is configured as the default entry location on port 80, and the web applications are configured to receive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

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


## <a name="changing-the-configuration-of-a-role"></a><span data-ttu-id="2b307-174">Zmienianie konfiguracji roli</span><span class="sxs-lookup"><span data-stu-id="2b307-174">Changing the configuration of a role</span></span>
<span data-ttu-id="2b307-175">Należy zaktualizować konfiguracji usługi w chmurze, jest uruchomiona na platformie Azure, bez konieczności przełączania w tryb offline usługa.</span><span class="sxs-lookup"><span data-stu-id="2b307-175">You can update the configuration of your cloud service while it is running in Azure, without taking the service offline.</span></span> <span data-ttu-id="2b307-176">Aby zmienić informacje o konfiguracji, użytkownik może albo Przekaż nowy plik konfiguracji, lub edytować plik konfiguracji w miejscu i zastosować je do uruchomionej usługi.</span><span class="sxs-lookup"><span data-stu-id="2b307-176">To change configuration information, you can either upload a new configuration file, or edit the configuration file in place and apply it to your running service.</span></span> <span data-ttu-id="2b307-177">W konfiguracji usługi mogą być wprowadzone następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="2b307-177">The following changes can be made to the configuration of a service:</span></span>

* <span data-ttu-id="2b307-178">**Zmiana wartości ustawienia konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="2b307-178">**Changing the values of configuration settings**</span></span>  
  <span data-ttu-id="2b307-179">Gdy ustawienie zmian konfiguracji, wystąpienia roli można zastosować zmiany, gdy wystąpienie jest w trybie online lub bezpiecznie Odtwórz wystąpienie do zastosowania zmiany podczas wystąpienie jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="2b307-179">When a configuration setting changes, a role instance can choose to apply the change while the instance is online, or to recycle the instance gracefully and apply the change while the instance is offline.</span></span>
* <span data-ttu-id="2b307-180">**Zmiany topologii usługa wystąpień roli**</span><span class="sxs-lookup"><span data-stu-id="2b307-180">**Changing the service topology of role instances**</span></span>  
  <span data-ttu-id="2b307-181">Topologia zmiany nie wpływają na uruchomione wystąpienia, z wyjątkiem przypadków, gdy wystąpienie jest usuwana.</span><span class="sxs-lookup"><span data-stu-id="2b307-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="2b307-182">Wszystkie pozostałe wystąpienia zwykle nie trzeba będzie wykonywane; można jednak odzyskać wystąpień roli w odpowiedzi na zmianę topologii.</span><span class="sxs-lookup"><span data-stu-id="2b307-182">All remaining instances generally do not need to be recycled; however, you can choose to recycle role instances in response to a topology change.</span></span>
* <span data-ttu-id="2b307-183">**Zmiana odcisk palca certyfikatu**</span><span class="sxs-lookup"><span data-stu-id="2b307-183">**Changing the certificate thumbprint**</span></span>  
  <span data-ttu-id="2b307-184">Certyfikat można aktualizować tylko wtedy, gdy wystąpienie roli jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="2b307-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="2b307-185">Jeśli certyfikat jest dodany, usunięty lub zmieniony, gdy wystąpienie roli jest w trybie online, Azure bezpiecznie powoduje wystąpienie w trybie offline do Aktualizuj certyfikat i przełączyć do trybu online po zakończeniu zmiany.</span><span class="sxs-lookup"><span data-stu-id="2b307-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes the instance offline to update the certificate and bring it back online after the change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="2b307-186">Obsługa zmiany w konfiguracji o zdarzeniach środowiska uruchomieniowego usługi</span><span class="sxs-lookup"><span data-stu-id="2b307-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="2b307-187">[Biblioteki wykonawczej Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) obejmuje [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) przestrzeni nazw, która udostępnia klasy do interakcji z środowiska platformy Azure z roli.</span><span class="sxs-lookup"><span data-stu-id="2b307-187">The [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with the Azure environment from a role.</span></span> <span data-ttu-id="2b307-188">[RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) klasa definiuje następujące zdarzenia, które są wywoływane przed i po zmianie konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="2b307-188">The [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines the following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="2b307-189">**[Zmiana](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="2b307-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="2b307-190">Dzieje się tak, przed zastosowaniem zmian w konfiguracji do określonego wystąpienia roli, co daje możliwość wyłączyć wystąpienia roli, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2b307-190">This occurs before the configuration change is applied to a specified instance of a role giving you a chance to take down the role instances if necessary.</span></span>
* <span data-ttu-id="2b307-191">**[Zmienione](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="2b307-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="2b307-192">Występuje po zmianie konfiguracji jest stosowane do określonego wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="2b307-192">Occurs after the configuration change is applied to a specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="2b307-193">Ponieważ zmiany certyfikatu zawsze pobierają wystąpień roli w tryb offline, nie wygenerował RoleEnvironment.Changing lub RoleEnvironment.Changed zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="2b307-193">Because certificate changes always take the instances of a role offline, they do not raise the RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="2b307-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="2b307-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="2b307-195">Aby wdrożyć aplikację jako usługa w chmurze na platformie Azure, najpierw należy utworzyć pakiet aplikacji w odpowiednim formacie.</span><span class="sxs-lookup"><span data-stu-id="2b307-195">To deploy an application as a cloud service in Azure, you must first package the application in the appropriate format.</span></span> <span data-ttu-id="2b307-196">Można użyć **CSPack** narzędzia wiersza polecenia (zainstalowaną z [zestawu Azure SDK](https://azure.microsoft.com/downloads/)) można utworzyć pliku pakietu jako alternatywę dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b307-196">You can use the **CSPack** command-line tool (installed with the [Azure SDK](https://azure.microsoft.com/downloads/)) to create the package file as an alternative to Visual Studio.</span></span>

<span data-ttu-id="2b307-197">**CSPack** zawartość pliku definicji usługi i pliku konfiguracji usługi jest używana do definiowania zawartości pakietu.</span><span class="sxs-lookup"><span data-stu-id="2b307-197">**CSPack** uses the contents of the service definition file and service configuration file to define the contents of the package.</span></span> <span data-ttu-id="2b307-198">**CSPack** generuje plik pakietu aplikacji (cspkg) można przekazać go do platformy Azure przy użyciu [portalu Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="2b307-198">**CSPack** generates an application package file (.cspkg) that you can upload to Azure by using the [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="2b307-199">Domyślnie pakiet o nazwie `[ServiceDefinitionFileName].cspkg`, ale możesz określić inną nazwę przy użyciu `/out` opcji **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="2b307-199">By default, the package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using the `/out` option of **CSPack**.</span></span>

<span data-ttu-id="2b307-200">**CSPack** znajduje się pod adresem</span><span class="sxs-lookup"><span data-stu-id="2b307-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="2b307-201">CSPack.exe (w systemie windows) jest dostępny, uruchamiając **wiersza polecenia usługi Microsoft Azure** skrót, który został zainstalowany przy użyciu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="2b307-201">CSPack.exe (on windows) is available by running the **Microsoft Azure Command Prompt** shortcut that is installed with the SDK.</span></span>  
> 
> <span data-ttu-id="2b307-202">Uruchom CSPack.exe program samodzielnie dokumentacji dotyczące wszystkich możliwych przełączników i poleceń.</span><span class="sxs-lookup"><span data-stu-id="2b307-202">Run the CSPack.exe program by itself to see documentation about all the possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="2b307-203">Uruchamianie usługi w chmurze lokalnie w **Microsoft Azure obliczeniowe emulatora**, użyj **/copyonly** opcji.</span><span class="sxs-lookup"><span data-stu-id="2b307-203">Run your cloud service locally in the **Microsoft Azure Compute Emulator**, use the **/copyonly** option.</span></span> <span data-ttu-id="2b307-204">Ta opcja powoduje skopiowanie plików binarnych dla aplikacji do układu katalogu, z którego może działać w emulatorze obliczeń.</span><span class="sxs-lookup"><span data-stu-id="2b307-204">This option copies the binary files for the application to a directory layout from which they can be run in the compute emulator.</span></span>
> 
> 

### <a name="example-command-to-package-a-cloud-service"></a><span data-ttu-id="2b307-205">Przykładowe polecenie, aby pakiet usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="2b307-205">Example command to package a cloud service</span></span>
<span data-ttu-id="2b307-206">W poniższym przykładzie jest tworzony pakiet aplikacji zawierający informacje dla roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="2b307-206">The following example creates an application package that contains the information for a web role.</span></span> <span data-ttu-id="2b307-207">Polecenie określa pliku definicji usługi do użycia, katalog, w którym można znaleźć plików binarnych, a nazwa pliku pakietu.</span><span class="sxs-lookup"><span data-stu-id="2b307-207">The command specifies the service definition file to use, the directory where binary files can be found, and the name of the package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="2b307-208">Jeśli aplikacja zawiera rolę sieci web i roli proces roboczy, służy następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2b307-208">If the application contains both a web role and a worker role, the following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="2b307-209">Gdzie zmienne są zdefiniowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2b307-209">Where the variables are defined as follows:</span></span>

| <span data-ttu-id="2b307-210">Zmienna</span><span class="sxs-lookup"><span data-stu-id="2b307-210">Variable</span></span> | <span data-ttu-id="2b307-211">Wartość</span><span class="sxs-lookup"><span data-stu-id="2b307-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2b307-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="2b307-212">\[DirectoryName\]</span></span> |<span data-ttu-id="2b307-213">Podkatalogu w katalogu głównym projektu zawierającego plik csdef projektu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2b307-213">The subdirectory under the root project directory that contains the .csdef file of the Azure project.</span></span> |
| <span data-ttu-id="2b307-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="2b307-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="2b307-215">Nazwa pliku definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="2b307-215">The name of the service definition file.</span></span> <span data-ttu-id="2b307-216">Domyślnie ten plik ma nazwę ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="2b307-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="2b307-217">\[Nazwa_pliku_wyjściowego\]</span><span class="sxs-lookup"><span data-stu-id="2b307-217">\[OutputFileName\]</span></span> |<span data-ttu-id="2b307-218">Nazwa pliku wygenerowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="2b307-218">The name for the generated package file.</span></span> <span data-ttu-id="2b307-219">Zwykle ta jest ustawiona na nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b307-219">Typically, this is set to the name of the application.</span></span> <span data-ttu-id="2b307-220">Jeśli nazwa pliku nie jest określona, pakiet aplikacji jest tworzony jako \[ApplicationName\]cspkg.</span><span class="sxs-lookup"><span data-stu-id="2b307-220">If no file name is specified, the application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="2b307-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="2b307-221">\[RoleName\]</span></span> |<span data-ttu-id="2b307-222">Nazwa roli, zgodnie z definicją w pliku definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="2b307-222">The name of the role as defined in the service definition file.</span></span> |
| <span data-ttu-id="2b307-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="2b307-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="2b307-224">Lokalizacja plików binarnych roli.</span><span class="sxs-lookup"><span data-stu-id="2b307-224">The location of the binary files for the role.</span></span> |
| <span data-ttu-id="2b307-225">\[Właściwość VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="2b307-225">\[VirtualPath\]</span></span> |<span data-ttu-id="2b307-226">Katalogi fizyczne dla każdej ścieżki wirtualnej określona w sekcji witryn definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="2b307-226">The physical directories for each virtual path defined in the Sites section of the service definition.</span></span> |
| <span data-ttu-id="2b307-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="2b307-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="2b307-228">Katalogi fizyczne zawartości dla każdej ścieżki wirtualnej zdefiniowany w węźle lokacji definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="2b307-228">The physical directories of the contents for each virtual path defined in the site node of the service definition.</span></span> |
| <span data-ttu-id="2b307-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="2b307-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="2b307-230">Nazwa pliku binarnego dla roli.</span><span class="sxs-lookup"><span data-stu-id="2b307-230">The name of the binary file for the role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2b307-231">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2b307-231">Next steps</span></span>
<span data-ttu-id="2b307-232">Tworzenia pakietu usług chmury i chcę...</span><span class="sxs-lookup"><span data-stu-id="2b307-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="2b307-233">[Ustawienia pulpitu zdalnego dla wystąpienia usługi chmury][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="2b307-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="2b307-234">[Wdrażanie projektu usługi w chmurze][deploy]</span><span class="sxs-lookup"><span data-stu-id="2b307-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="2b307-235">Używam programu Visual Studio i chcę...</span><span class="sxs-lookup"><span data-stu-id="2b307-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="2b307-236">[Utwórz nową usługę w chmurze][vs_create]</span><span class="sxs-lookup"><span data-stu-id="2b307-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="2b307-237">[Skonfiguruj ponownie istniejącej usługi w chmurze][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="2b307-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="2b307-238">[Wdrażanie projektu usługi w chmurze][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="2b307-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="2b307-239">[Ustawienia pulpitu zdalnego dla wystąpienia usługi chmury][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="2b307-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
