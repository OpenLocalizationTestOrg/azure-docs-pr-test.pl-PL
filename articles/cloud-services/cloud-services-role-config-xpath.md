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
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="22d03-103">Udostępnianie ustawień konfiguracji roli jako zmiennej środowiskowej XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="22d03-104">Proces roboczy usług chmury hello lub pliku definicji usługi roli sieci web mogą uwidaczniać wartości konfiguracji środowiska uruchomieniowego jako zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="22d03-104">In hello cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="22d03-105">następujące wartości XPath Hello są obsługiwane (co odpowiada wartości tooAPI).</span><span class="sxs-lookup"><span data-stu-id="22d03-105">hello following XPath values are supported (which correspond tooAPI values).</span></span>

<span data-ttu-id="22d03-106">Te wartości XPath są również dostępne za pośrednictwem hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) biblioteki.</span><span class="sxs-lookup"><span data-stu-id="22d03-106">These XPath values are also available through hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="22d03-107">Aplikacji uruchomionej w emulatorze</span><span class="sxs-lookup"><span data-stu-id="22d03-107">App running in emulator</span></span>
<span data-ttu-id="22d03-108">Wskazuje, że danej aplikacji hello działa w emulatorze hello.</span><span class="sxs-lookup"><span data-stu-id="22d03-108">Indicates that hello app is running in hello emulator.</span></span>

| <span data-ttu-id="22d03-109">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-109">Type</span></span> | <span data-ttu-id="22d03-110">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-111">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-111">XPath</span></span> |<span data-ttu-id="22d03-112">wyrażenie XPath = "/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="22d03-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="22d03-113">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-113">Code</span></span> |<span data-ttu-id="22d03-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="22d03-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="22d03-115">Identyfikator wdrożenia</span><span class="sxs-lookup"><span data-stu-id="22d03-115">Deployment ID</span></span>
<span data-ttu-id="22d03-116">Pobiera identyfikator wdrożenia hello hello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="22d03-116">Retrieves hello deployment ID for hello instance.</span></span>

| <span data-ttu-id="22d03-117">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-117">Type</span></span> | <span data-ttu-id="22d03-118">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-119">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-119">XPath</span></span> |<span data-ttu-id="22d03-120">wyrażenie XPath = "/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="22d03-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="22d03-121">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-121">Code</span></span> |<span data-ttu-id="22d03-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="22d03-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="22d03-123">Identyfikator roli</span><span class="sxs-lookup"><span data-stu-id="22d03-123">Role ID</span></span>
<span data-ttu-id="22d03-124">Pobiera bieżący identyfikator roli hello hello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="22d03-124">Retrieves hello current role ID for hello instance.</span></span>

| <span data-ttu-id="22d03-125">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-125">Type</span></span> | <span data-ttu-id="22d03-126">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-127">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-127">XPath</span></span> |<span data-ttu-id="22d03-128">wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="22d03-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="22d03-129">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-129">Code</span></span> |<span data-ttu-id="22d03-130">Identyfikator var = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="22d03-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="22d03-131">Aktualizowanie domeny</span><span class="sxs-lookup"><span data-stu-id="22d03-131">Update domain</span></span>
<span data-ttu-id="22d03-132">Pobiera domeny aktualizacji hello hello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="22d03-132">Retrieves hello update domain of hello instance.</span></span>

| <span data-ttu-id="22d03-133">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-133">Type</span></span> | <span data-ttu-id="22d03-134">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-135">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-135">XPath</span></span> |<span data-ttu-id="22d03-136">wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="22d03-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="22d03-137">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-137">Code</span></span> |<span data-ttu-id="22d03-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="22d03-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="22d03-139">Domena awarii</span><span class="sxs-lookup"><span data-stu-id="22d03-139">Fault domain</span></span>
<span data-ttu-id="22d03-140">Pobiera domeny błędów hello hello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="22d03-140">Retrieves hello fault domain of hello instance.</span></span>

| <span data-ttu-id="22d03-141">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-141">Type</span></span> | <span data-ttu-id="22d03-142">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-143">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-143">XPath</span></span> |<span data-ttu-id="22d03-144">wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="22d03-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="22d03-145">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-145">Code</span></span> |<span data-ttu-id="22d03-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="22d03-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="22d03-147">Nazwa roli</span><span class="sxs-lookup"><span data-stu-id="22d03-147">Role name</span></span>
<span data-ttu-id="22d03-148">Pobiera nazwę roli hello hello wystąpień.</span><span class="sxs-lookup"><span data-stu-id="22d03-148">Retrieves hello role name of hello instances.</span></span>

| <span data-ttu-id="22d03-149">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-149">Type</span></span> | <span data-ttu-id="22d03-150">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-151">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-151">XPath</span></span> |<span data-ttu-id="22d03-152">wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="22d03-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="22d03-153">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-153">Code</span></span> |<span data-ttu-id="22d03-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="22d03-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="22d03-155">Ustawienia konfiguracji</span><span class="sxs-lookup"><span data-stu-id="22d03-155">Config setting</span></span>
<span data-ttu-id="22d03-156">Pobiera wartość hello hello określone ustawienia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="22d03-156">Retrieves hello value of hello specified configuration setting.</span></span>

| <span data-ttu-id="22d03-157">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-157">Type</span></span> | <span data-ttu-id="22d03-158">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-159">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-159">XPath</span></span> |<span data-ttu-id="22d03-160">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/appSettings/ConfigurationSetting [@name="Setting1"]/@value"</span><span class="sxs-lookup"><span data-stu-id="22d03-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="22d03-161">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-161">Code</span></span> |<span data-ttu-id="22d03-162">Ustawienie var = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="22d03-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="22d03-163">Ścieżki do lokalnego magazynu</span><span class="sxs-lookup"><span data-stu-id="22d03-163">Local storage path</span></span>
<span data-ttu-id="22d03-164">Pobiera ścieżkę magazynu lokalnego hello hello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="22d03-164">Retrieves hello local storage path for hello instance.</span></span>

| <span data-ttu-id="22d03-165">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-165">Type</span></span> | <span data-ttu-id="22d03-166">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-167">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-167">XPath</span></span> |<span data-ttu-id="22d03-168">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name="LocalStore1"]/@path"</span><span class="sxs-lookup"><span data-stu-id="22d03-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="22d03-169">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-169">Code</span></span> |<span data-ttu-id="22d03-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1"). Właściwość RootPath;</span><span class="sxs-lookup"><span data-stu-id="22d03-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="22d03-171">Rozmiar magazynu lokalnego</span><span class="sxs-lookup"><span data-stu-id="22d03-171">Local storage size</span></span>
<span data-ttu-id="22d03-172">Pobiera rozmiar hello hello magazynu lokalnego wystąpienia hello.</span><span class="sxs-lookup"><span data-stu-id="22d03-172">Retrieves hello size of hello local storage for hello instance.</span></span>

| <span data-ttu-id="22d03-173">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-173">Type</span></span> | <span data-ttu-id="22d03-174">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-175">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-175">XPath</span></span> |<span data-ttu-id="22d03-176">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name="LocalStore1"]/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="22d03-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="22d03-177">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-177">Code</span></span> |<span data-ttu-id="22d03-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1"). MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="22d03-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="22d03-179">Punkt końcowy protokołu</span><span class="sxs-lookup"><span data-stu-id="22d03-179">Endpoint protocol</span></span>
<span data-ttu-id="22d03-180">Pobiera protokół punktu końcowego hello hello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="22d03-180">Retrieves hello endpoint protocol for hello instance.</span></span>

| <span data-ttu-id="22d03-181">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-181">Type</span></span> | <span data-ttu-id="22d03-182">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-183">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-183">XPath</span></span> |<span data-ttu-id="22d03-184">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/punkty końcowe/punktu końcowego [@name= 'Punk końcowy 1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="22d03-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="22d03-185">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-185">Code</span></span> |<span data-ttu-id="22d03-186">ochronę var = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"]. Protokół;</span><span class="sxs-lookup"><span data-stu-id="22d03-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="22d03-187">Punkt końcowy IP</span><span class="sxs-lookup"><span data-stu-id="22d03-187">Endpoint IP</span></span>
<span data-ttu-id="22d03-188">Pobiera hello określony adres IP punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="22d03-188">Gets hello specified endpoint's IP address.</span></span>

| <span data-ttu-id="22d03-189">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-189">Type</span></span> | <span data-ttu-id="22d03-190">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-191">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-191">XPath</span></span> |<span data-ttu-id="22d03-192">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/punkty końcowe/punktu końcowego [@name= 'Punk końcowy 1']/@address"</span><span class="sxs-lookup"><span data-stu-id="22d03-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="22d03-193">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-193">Code</span></span> |<span data-ttu-id="22d03-194">adres var = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"]. IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="22d03-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="22d03-195">Port punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="22d03-195">Endpoint port</span></span>
<span data-ttu-id="22d03-196">Pobiera hello port punktu końcowego dla hello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="22d03-196">Retrieves hello endpoint port for hello instance.</span></span>

| <span data-ttu-id="22d03-197">Typ</span><span class="sxs-lookup"><span data-stu-id="22d03-197">Type</span></span> | <span data-ttu-id="22d03-198">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="22d03-199">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="22d03-199">XPath</span></span> |<span data-ttu-id="22d03-200">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/punkty końcowe/punktu końcowego [@name= 'Punk końcowy 1']/@port"</span><span class="sxs-lookup"><span data-stu-id="22d03-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="22d03-201">Kod</span><span class="sxs-lookup"><span data-stu-id="22d03-201">Code</span></span> |<span data-ttu-id="22d03-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"]. IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="22d03-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="22d03-203">Przykład</span><span class="sxs-lookup"><span data-stu-id="22d03-203">Example</span></span>
<span data-ttu-id="22d03-204">Oto przykład roli procesu roboczego, który tworzy zadanie uruchamiania przy użyciu zmiennej środowiskowej o nazwie `TestIsEmulated` ustawić toohello [ @emulated wartość wyrażenia xpath](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="22d03-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set toohello [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="22d03-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22d03-205">Next steps</span></span>
<span data-ttu-id="22d03-206">Dowiedz się więcej o hello [pliku ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) pliku.</span><span class="sxs-lookup"><span data-stu-id="22d03-206">Learn more about hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="22d03-207">Utwórz [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) pakietu.</span><span class="sxs-lookup"><span data-stu-id="22d03-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="22d03-208">Włącz [pulpitu zdalnego](cloud-services-role-enable-remote-desktop.md) dla roli.</span><span class="sxs-lookup"><span data-stu-id="22d03-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

