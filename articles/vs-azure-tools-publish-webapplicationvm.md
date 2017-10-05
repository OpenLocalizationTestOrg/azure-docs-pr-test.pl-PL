---
title: Publikowanie WebApplicationVM | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak wdrożyć aplikację sieci web do maszyny wirtualnej. Ten skrypt tworzy wymaganych zasobów w Twojej subskrypcji platformy Azure, jeśli nie istnieją."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 2738fc1dff50a177a227ae2c7719bd9a192d82ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="4379b-104">Publikowanie WebApplicationVM (skrypt programu Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="4379b-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="4379b-105">Wdraża aplikację sieci web do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4379b-105">Deploys a web application to a virtual machine.</span></span> <span data-ttu-id="4379b-106">Skrypt tworzy wymaganych zasobów w Twojej subskrypcji platformy Azure, jeśli nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="4379b-106">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="4379b-107">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="4379b-107">Configuration</span></span>
<span data-ttu-id="4379b-108">Ścieżka do pliku konfiguracji JSON, który opisuje szczegóły wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4379b-108">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="4379b-109">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4379b-109">Aliases</span></span> | <span data-ttu-id="4379b-110">Brak</span><span class="sxs-lookup"><span data-stu-id="4379b-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="4379b-111">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="4379b-111">Required?</span></span> |<span data-ttu-id="4379b-112">Wartość true</span><span class="sxs-lookup"><span data-stu-id="4379b-112">true</span></span> |
| <span data-ttu-id="4379b-113">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4379b-113">Position</span></span> |<span data-ttu-id="4379b-114">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4379b-114">named</span></span> |
| <span data-ttu-id="4379b-115">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4379b-115">Default value</span></span> |<span data-ttu-id="4379b-116">Brak</span><span class="sxs-lookup"><span data-stu-id="4379b-116">none</span></span> |
| <span data-ttu-id="4379b-117">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4379b-117">Accept pipeline input?</span></span> |<span data-ttu-id="4379b-118">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-118">false</span></span> |
| <span data-ttu-id="4379b-119">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4379b-119">Accept wildcard characters?</span></span> |<span data-ttu-id="4379b-120">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="4379b-121">Nazwa subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4379b-121">SubscriptionName</span></span>
<span data-ttu-id="4379b-122">Nazwa subskrypcji platformy Azure, w którym chcesz utworzyć maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="4379b-122">The name of the Azure subscription in which you want to create the virtual machine.</span></span>

| <span data-ttu-id="4379b-123">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4379b-123">Aliases</span></span> | <span data-ttu-id="4379b-124">Brak</span><span class="sxs-lookup"><span data-stu-id="4379b-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="4379b-125">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="4379b-125">Required?</span></span> |<span data-ttu-id="4379b-126">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-126">false</span></span> |
| <span data-ttu-id="4379b-127">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4379b-127">Position</span></span> |<span data-ttu-id="4379b-128">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4379b-128">named</span></span> |
| <span data-ttu-id="4379b-129">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4379b-129">Default value</span></span> |<span data-ttu-id="4379b-130">Używa pierwszej subskrypcji w pliku subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4379b-130">Uses the first subscription in the subscription file</span></span> |
| <span data-ttu-id="4379b-131">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4379b-131">Accept pipeline input?</span></span> |<span data-ttu-id="4379b-132">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-132">false</span></span> |
| <span data-ttu-id="4379b-133">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4379b-133">Accept wildcard characters?</span></span> |<span data-ttu-id="4379b-134">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="4379b-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="4379b-135">WebDeployPackage</span></span>
<span data-ttu-id="4379b-136">Ścieżka do pakietu wdrożeniowego sieci web do publikowania do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4379b-136">The path to the web deployment package to publish to the virtual machine.</span></span> <span data-ttu-id="4379b-137">Ten pakiet można utworzyć za pomocą kreatora Publikowanie w sieci Web w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4379b-137">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="4379b-138">Zobacz [jak: utworzyć pakiet wdrożeniowy sieci Web w programie Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="4379b-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="4379b-139">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4379b-139">Aliases</span></span> | <span data-ttu-id="4379b-140">Brak</span><span class="sxs-lookup"><span data-stu-id="4379b-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="4379b-141">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="4379b-141">Required?</span></span> |<span data-ttu-id="4379b-142">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-142">false</span></span> |
| <span data-ttu-id="4379b-143">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4379b-143">Position</span></span> |<span data-ttu-id="4379b-144">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4379b-144">named</span></span> |
| <span data-ttu-id="4379b-145">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4379b-145">Default value</span></span> |<span data-ttu-id="4379b-146">Brak</span><span class="sxs-lookup"><span data-stu-id="4379b-146">none</span></span> |
| <span data-ttu-id="4379b-147">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4379b-147">Accept pipeline input?</span></span> |<span data-ttu-id="4379b-148">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-148">false</span></span> |
| <span data-ttu-id="4379b-149">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4379b-149">Accept wildcard characters?</span></span> |<span data-ttu-id="4379b-150">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="4379b-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="4379b-151">AllowUntrusted</span></span>
<span data-ttu-id="4379b-152">Jeśli PRAWDA, Zezwalaj na korzystanie z certyfikatów, które nie są podpisane przez zaufanego głównego urzędu.</span><span class="sxs-lookup"><span data-stu-id="4379b-152">If true, allow the use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="4379b-153">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4379b-153">Aliases</span></span> | <span data-ttu-id="4379b-154">Brak</span><span class="sxs-lookup"><span data-stu-id="4379b-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="4379b-155">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="4379b-155">Required?</span></span> |<span data-ttu-id="4379b-156">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-156">false</span></span> |
| <span data-ttu-id="4379b-157">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4379b-157">Position</span></span> |<span data-ttu-id="4379b-158">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4379b-158">named</span></span> |
| <span data-ttu-id="4379b-159">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4379b-159">Default value</span></span> |<span data-ttu-id="4379b-160">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-160">false</span></span> |
| <span data-ttu-id="4379b-161">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4379b-161">Accept pipeline input?</span></span> |<span data-ttu-id="4379b-162">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-162">false</span></span> |
| <span data-ttu-id="4379b-163">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4379b-163">Accept wildcard characters?</span></span> |<span data-ttu-id="4379b-164">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="4379b-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="4379b-165">VMPassword</span></span>
<span data-ttu-id="4379b-166">Poświadczenia dla konta maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4379b-166">The credentials for the virtual machine account.</span></span> <span data-ttu-id="4379b-167">Przykład: - VMPassword @{nazwa = "admin"; Hasło = "password"}</span><span class="sxs-lookup"><span data-stu-id="4379b-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="4379b-168">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4379b-168">Aliases</span></span> | <span data-ttu-id="4379b-169">Brak</span><span class="sxs-lookup"><span data-stu-id="4379b-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="4379b-170">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="4379b-170">Required?</span></span> |<span data-ttu-id="4379b-171">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-171">false</span></span> |
| <span data-ttu-id="4379b-172">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4379b-172">Position</span></span> |<span data-ttu-id="4379b-173">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4379b-173">named</span></span> |
| <span data-ttu-id="4379b-174">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4379b-174">Default value</span></span> |<span data-ttu-id="4379b-175">Brak</span><span class="sxs-lookup"><span data-stu-id="4379b-175">none</span></span> |
| <span data-ttu-id="4379b-176">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4379b-176">Accept pipeline input?</span></span> |<span data-ttu-id="4379b-177">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-177">false</span></span> |
| <span data-ttu-id="4379b-178">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4379b-178">Accept wildcard characters?</span></span> |<span data-ttu-id="4379b-179">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="4379b-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="4379b-180">DatabaseServerPassword</span></span>
<span data-ttu-id="4379b-181">Poświadczenia bazy danych SQL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4379b-181">The credentials for the SQL database in Azure.</span></span> <span data-ttu-id="4379b-182">Przykład: - DatabaseServerPassword @{nazwa = "admin"; Hasło = "password"}</span><span class="sxs-lookup"><span data-stu-id="4379b-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="4379b-183">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4379b-183">Aliases</span></span> | <span data-ttu-id="4379b-184">Brak</span><span class="sxs-lookup"><span data-stu-id="4379b-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="4379b-185">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="4379b-185">Required?</span></span> |<span data-ttu-id="4379b-186">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-186">false</span></span> |
| <span data-ttu-id="4379b-187">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4379b-187">Position</span></span> |<span data-ttu-id="4379b-188">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4379b-188">named</span></span> |
| <span data-ttu-id="4379b-189">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4379b-189">Default value</span></span> |<span data-ttu-id="4379b-190">Brak</span><span class="sxs-lookup"><span data-stu-id="4379b-190">none</span></span> |
| <span data-ttu-id="4379b-191">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4379b-191">Accept pipeline input?</span></span> |<span data-ttu-id="4379b-192">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-192">false</span></span> |
| <span data-ttu-id="4379b-193">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4379b-193">Accept wildcard characters?</span></span> |<span data-ttu-id="4379b-194">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="4379b-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="4379b-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="4379b-196">Jeśli PRAWDA, Drukuj komunikaty z skrypt do strumienia wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="4379b-196">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="4379b-197">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4379b-197">Aliases</span></span> | <span data-ttu-id="4379b-198">Brak</span><span class="sxs-lookup"><span data-stu-id="4379b-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="4379b-199">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="4379b-199">Required?</span></span> |<span data-ttu-id="4379b-200">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-200">false</span></span> |
| <span data-ttu-id="4379b-201">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4379b-201">Position</span></span> |<span data-ttu-id="4379b-202">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4379b-202">named</span></span> |
| <span data-ttu-id="4379b-203">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4379b-203">Default value</span></span> |<span data-ttu-id="4379b-204">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-204">false</span></span> |
| <span data-ttu-id="4379b-205">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4379b-205">Accept pipeline input?</span></span> |<span data-ttu-id="4379b-206">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-206">false</span></span> |
| <span data-ttu-id="4379b-207">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4379b-207">Accept wildcard characters?</span></span> |<span data-ttu-id="4379b-208">wartość false</span><span class="sxs-lookup"><span data-stu-id="4379b-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="4379b-209">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4379b-209">Remarks</span></span>
<span data-ttu-id="4379b-210">Pełny opis sposobów użycia skryptu do tworzenia środowisk do tworzenia i testowania, zobacz [za pomocą skryptów programu PowerShell systemu Windows do opublikowania deweloperów i środowisk testowych](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="4379b-210">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="4379b-211">Plik JSON konfiguracji określa szczegóły co ma zostać wdrożona.</span><span class="sxs-lookup"><span data-stu-id="4379b-211">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="4379b-212">Zawiera informacje, które zostało określone podczas tworzenia projektu, takie jak nazwa grupy koligacji, obrazu wirtualnego dysku twardego i rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4379b-212">It includes the information that you specified when you created the project, such as the name, affinity group, VHD image, and size of the virtual machine.</span></span> <span data-ttu-id="4379b-213">Także zawiera punkty końcowe na maszynie wirtualnej, baz danych, aby było możliwe, jeśli istnieje i parametry wdrażania w sieci web.</span><span class="sxs-lookup"><span data-stu-id="4379b-213">It also includes the endpoints on the virtual machine, the databases to provision, if any, and web deployment parameters.</span></span> <span data-ttu-id="4379b-214">Poniższy kod przedstawia przykładowy plik konfiguracji JSON:</span><span class="sxs-lookup"><span data-stu-id="4379b-214">The following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="4379b-215">Można edytować plik JSON konfiguracji do zmiany, jakie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="4379b-215">You can edit the JSON configuration file to change what is provisioned.</span></span> <span data-ttu-id="4379b-216">Maszyny wirtualne i usługi w chmurze są wymagane, ale w sekcji bazy danych jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="4379b-216">A virtual machine and a cloud service are required, but the database section is optional.</span></span>

