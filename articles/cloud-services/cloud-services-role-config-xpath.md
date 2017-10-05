---
title: "Chmura roli usługi konfiguracji XPath ściągawka | Dokumentacja firmy Microsoft"
description: "Różne ustawienia języka XPath można w konfiguracji roli usługi w chmurze uwidocznić ustawienia jako zmiennej środowiskowej."
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
ms.openlocfilehash: fd6efac829d3fd9e2840362b8d2ff423add566d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="30b8c-103">Udostępnianie ustawień konfiguracji roli jako zmiennej środowiskowej XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="30b8c-104">W chmurze usługi worker lub pliku definicji usługi roli sieci web można uwidocznić wartości konfiguracji środowiska uruchomieniowego jako zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="30b8c-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="30b8c-105">Obsługiwane są następujące wartości XPath, (które odpowiadają wartościom interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="30b8c-105">The following XPath values are supported (which correspond to API values).</span></span>

<span data-ttu-id="30b8c-106">Dostępne są także te wartości XPath [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) biblioteki.</span><span class="sxs-lookup"><span data-stu-id="30b8c-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="30b8c-107">Aplikacji uruchomionej w emulatorze</span><span class="sxs-lookup"><span data-stu-id="30b8c-107">App running in emulator</span></span>
<span data-ttu-id="30b8c-108">Wskazuje, że aplikacja działa w emulatorze.</span><span class="sxs-lookup"><span data-stu-id="30b8c-108">Indicates that the app is running in the emulator.</span></span>

| <span data-ttu-id="30b8c-109">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-109">Type</span></span> | <span data-ttu-id="30b8c-110">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-111">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-111">XPath</span></span> |<span data-ttu-id="30b8c-112">wyrażenie XPath = "/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="30b8c-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="30b8c-113">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-113">Code</span></span> |<span data-ttu-id="30b8c-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="30b8c-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="30b8c-115">Identyfikator wdrożenia</span><span class="sxs-lookup"><span data-stu-id="30b8c-115">Deployment ID</span></span>
<span data-ttu-id="30b8c-116">Pobiera identyfikator wdrożenia dla tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="30b8c-116">Retrieves the deployment ID for the instance.</span></span>

| <span data-ttu-id="30b8c-117">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-117">Type</span></span> | <span data-ttu-id="30b8c-118">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-119">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-119">XPath</span></span> |<span data-ttu-id="30b8c-120">wyrażenie XPath = "/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="30b8c-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="30b8c-121">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-121">Code</span></span> |<span data-ttu-id="30b8c-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="30b8c-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="30b8c-123">Identyfikator roli</span><span class="sxs-lookup"><span data-stu-id="30b8c-123">Role ID</span></span>
<span data-ttu-id="30b8c-124">Pobiera bieżący identyfikator roli dla tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="30b8c-124">Retrieves the current role ID for the instance.</span></span>

| <span data-ttu-id="30b8c-125">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-125">Type</span></span> | <span data-ttu-id="30b8c-126">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-127">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-127">XPath</span></span> |<span data-ttu-id="30b8c-128">wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="30b8c-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="30b8c-129">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-129">Code</span></span> |<span data-ttu-id="30b8c-130">Identyfikator var = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="30b8c-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="30b8c-131">Aktualizowanie domeny</span><span class="sxs-lookup"><span data-stu-id="30b8c-131">Update domain</span></span>
<span data-ttu-id="30b8c-132">Pobiera domeny aktualizacji wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="30b8c-132">Retrieves the update domain of the instance.</span></span>

| <span data-ttu-id="30b8c-133">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-133">Type</span></span> | <span data-ttu-id="30b8c-134">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-135">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-135">XPath</span></span> |<span data-ttu-id="30b8c-136">wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="30b8c-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="30b8c-137">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-137">Code</span></span> |<span data-ttu-id="30b8c-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="30b8c-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="30b8c-139">Domena awarii</span><span class="sxs-lookup"><span data-stu-id="30b8c-139">Fault domain</span></span>
<span data-ttu-id="30b8c-140">Pobiera wystąpienia domeny błędów.</span><span class="sxs-lookup"><span data-stu-id="30b8c-140">Retrieves the fault domain of the instance.</span></span>

| <span data-ttu-id="30b8c-141">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-141">Type</span></span> | <span data-ttu-id="30b8c-142">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-143">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-143">XPath</span></span> |<span data-ttu-id="30b8c-144">wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="30b8c-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="30b8c-145">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-145">Code</span></span> |<span data-ttu-id="30b8c-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="30b8c-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="30b8c-147">Nazwa roli</span><span class="sxs-lookup"><span data-stu-id="30b8c-147">Role name</span></span>
<span data-ttu-id="30b8c-148">Pobiera nazwę wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="30b8c-148">Retrieves the role name of the instances.</span></span>

| <span data-ttu-id="30b8c-149">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-149">Type</span></span> | <span data-ttu-id="30b8c-150">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-151">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-151">XPath</span></span> |<span data-ttu-id="30b8c-152">wyrażenie XPath = "/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="30b8c-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="30b8c-153">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-153">Code</span></span> |<span data-ttu-id="30b8c-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="30b8c-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="30b8c-155">Ustawienia konfiguracji</span><span class="sxs-lookup"><span data-stu-id="30b8c-155">Config setting</span></span>
<span data-ttu-id="30b8c-156">Pobiera wartość ustawienia określonej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="30b8c-156">Retrieves the value of the specified configuration setting.</span></span>

| <span data-ttu-id="30b8c-157">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-157">Type</span></span> | <span data-ttu-id="30b8c-158">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-159">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-159">XPath</span></span> |<span data-ttu-id="30b8c-160">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/appSettings/ConfigurationSetting [@name="Setting1"]/@value"</span><span class="sxs-lookup"><span data-stu-id="30b8c-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="30b8c-161">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-161">Code</span></span> |<span data-ttu-id="30b8c-162">Ustawienie var = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="30b8c-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="30b8c-163">Ścieżki do lokalnego magazynu</span><span class="sxs-lookup"><span data-stu-id="30b8c-163">Local storage path</span></span>
<span data-ttu-id="30b8c-164">Pobiera ścieżkę lokalnej pamięci masowej dla tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="30b8c-164">Retrieves the local storage path for the instance.</span></span>

| <span data-ttu-id="30b8c-165">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-165">Type</span></span> | <span data-ttu-id="30b8c-166">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-167">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-167">XPath</span></span> |<span data-ttu-id="30b8c-168">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name="LocalStore1"]/@path"</span><span class="sxs-lookup"><span data-stu-id="30b8c-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="30b8c-169">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-169">Code</span></span> |<span data-ttu-id="30b8c-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1"). Właściwość RootPath;</span><span class="sxs-lookup"><span data-stu-id="30b8c-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="30b8c-171">Rozmiar magazynu lokalnego</span><span class="sxs-lookup"><span data-stu-id="30b8c-171">Local storage size</span></span>
<span data-ttu-id="30b8c-172">Pobiera rozmiar magazynu lokalnego dla tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="30b8c-172">Retrieves the size of the local storage for the instance.</span></span>

| <span data-ttu-id="30b8c-173">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-173">Type</span></span> | <span data-ttu-id="30b8c-174">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-175">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-175">XPath</span></span> |<span data-ttu-id="30b8c-176">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name="LocalStore1"]/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="30b8c-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="30b8c-177">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-177">Code</span></span> |<span data-ttu-id="30b8c-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1"). MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="30b8c-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="30b8c-179">Punkt końcowy protokołu</span><span class="sxs-lookup"><span data-stu-id="30b8c-179">Endpoint protocol</span></span>
<span data-ttu-id="30b8c-180">Pobiera protokół punktu końcowego dla tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="30b8c-180">Retrieves the endpoint protocol for the instance.</span></span>

| <span data-ttu-id="30b8c-181">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-181">Type</span></span> | <span data-ttu-id="30b8c-182">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-183">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-183">XPath</span></span> |<span data-ttu-id="30b8c-184">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/punkty końcowe/punktu końcowego [@name= 'Punk końcowy 1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="30b8c-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="30b8c-185">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-185">Code</span></span> |<span data-ttu-id="30b8c-186">ochronę var = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"]. Protokół;</span><span class="sxs-lookup"><span data-stu-id="30b8c-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="30b8c-187">Punkt końcowy IP</span><span class="sxs-lookup"><span data-stu-id="30b8c-187">Endpoint IP</span></span>
<span data-ttu-id="30b8c-188">Pobiera określony punkt końcowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="30b8c-188">Gets the specified endpoint's IP address.</span></span>

| <span data-ttu-id="30b8c-189">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-189">Type</span></span> | <span data-ttu-id="30b8c-190">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-191">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-191">XPath</span></span> |<span data-ttu-id="30b8c-192">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/punkty końcowe/punktu końcowego [@name= 'Punk końcowy 1']/@address"</span><span class="sxs-lookup"><span data-stu-id="30b8c-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="30b8c-193">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-193">Code</span></span> |<span data-ttu-id="30b8c-194">adres var = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"]. IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="30b8c-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="30b8c-195">Port punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="30b8c-195">Endpoint port</span></span>
<span data-ttu-id="30b8c-196">Pobiera port punktu końcowego dla tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="30b8c-196">Retrieves the endpoint port for the instance.</span></span>

| <span data-ttu-id="30b8c-197">Typ</span><span class="sxs-lookup"><span data-stu-id="30b8c-197">Type</span></span> | <span data-ttu-id="30b8c-198">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="30b8c-199">Wyrażenie XPath</span><span class="sxs-lookup"><span data-stu-id="30b8c-199">XPath</span></span> |<span data-ttu-id="30b8c-200">wyrażenie XPath = "/ RoleEnvironment/CurrentInstance/punkty końcowe/punktu końcowego [@name= 'Punk końcowy 1']/@port"</span><span class="sxs-lookup"><span data-stu-id="30b8c-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="30b8c-201">Kod</span><span class="sxs-lookup"><span data-stu-id="30b8c-201">Code</span></span> |<span data-ttu-id="30b8c-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"]. IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="30b8c-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="30b8c-203">Przykład</span><span class="sxs-lookup"><span data-stu-id="30b8c-203">Example</span></span>
<span data-ttu-id="30b8c-204">Oto przykład roli procesu roboczego, który tworzy zadanie uruchamiania przy użyciu zmiennej środowiskowej o nazwie `TestIsEmulated` ustawioną [ @emulated wartość wyrażenia xpath](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="30b8c-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="30b8c-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30b8c-205">Next steps</span></span>
<span data-ttu-id="30b8c-206">Dowiedz się więcej o [pliku ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) pliku.</span><span class="sxs-lookup"><span data-stu-id="30b8c-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="30b8c-207">Utwórz [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) pakietu.</span><span class="sxs-lookup"><span data-stu-id="30b8c-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="30b8c-208">Włącz [pulpitu zdalnego](cloud-services-role-enable-remote-desktop.md) dla roli.</span><span class="sxs-lookup"><span data-stu-id="30b8c-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

