---
title: aaaPublish WebApplicationVM | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toodeploy maszyny wirtualnej tooa aplikacji sieci web. Ten skrypt tworzy hello wymaganych zasobów w Twojej subskrypcji platformy Azure, jeśli nie istnieją."
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
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="4ecb7-104">Publikowanie WebApplicationVM (skrypt programu Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="4ecb7-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="4ecb7-105">Wdraża maszynę wirtualną tooa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-105">Deploys a web application tooa virtual machine.</span></span> <span data-ttu-id="4ecb7-106">Witaj skrypt tworzy hello wymaganych zasobów w Twojej subskrypcji platformy Azure, jeśli nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-106">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

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

### <a name="configuration"></a><span data-ttu-id="4ecb7-107">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="4ecb7-107">Configuration</span></span>
<span data-ttu-id="4ecb7-108">Witaj ścieżki toohello plik JSON konfiguracji opisujący szczegóły hello hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-108">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="4ecb7-109">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4ecb7-109">Aliases</span></span> | <span data-ttu-id="4ecb7-110">Brak</span><span class="sxs-lookup"><span data-stu-id="4ecb7-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ecb7-111">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-111">Required?</span></span> |<span data-ttu-id="4ecb7-112">Wartość true</span><span class="sxs-lookup"><span data-stu-id="4ecb7-112">true</span></span> |
| <span data-ttu-id="4ecb7-113">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4ecb7-113">Position</span></span> |<span data-ttu-id="4ecb7-114">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4ecb7-114">named</span></span> |
| <span data-ttu-id="4ecb7-115">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4ecb7-115">Default value</span></span> |<span data-ttu-id="4ecb7-116">Brak</span><span class="sxs-lookup"><span data-stu-id="4ecb7-116">none</span></span> |
| <span data-ttu-id="4ecb7-117">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-117">Accept pipeline input?</span></span> |<span data-ttu-id="4ecb7-118">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-118">false</span></span> |
| <span data-ttu-id="4ecb7-119">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-119">Accept wildcard characters?</span></span> |<span data-ttu-id="4ecb7-120">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="4ecb7-121">Nazwa subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4ecb7-121">SubscriptionName</span></span>
<span data-ttu-id="4ecb7-122">Nazwa Hello hello subskrypcji platformy Azure, w której ma zostać maszyny wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-122">hello name of hello Azure subscription in which you want toocreate hello virtual machine.</span></span>

| <span data-ttu-id="4ecb7-123">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4ecb7-123">Aliases</span></span> | <span data-ttu-id="4ecb7-124">Brak</span><span class="sxs-lookup"><span data-stu-id="4ecb7-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ecb7-125">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-125">Required?</span></span> |<span data-ttu-id="4ecb7-126">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-126">false</span></span> |
| <span data-ttu-id="4ecb7-127">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4ecb7-127">Position</span></span> |<span data-ttu-id="4ecb7-128">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4ecb7-128">named</span></span> |
| <span data-ttu-id="4ecb7-129">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4ecb7-129">Default value</span></span> |<span data-ttu-id="4ecb7-130">Używa pierwszej subskrypcji hello w pliku subskrypcji hello</span><span class="sxs-lookup"><span data-stu-id="4ecb7-130">Uses hello first subscription in hello subscription file</span></span> |
| <span data-ttu-id="4ecb7-131">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-131">Accept pipeline input?</span></span> |<span data-ttu-id="4ecb7-132">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-132">false</span></span> |
| <span data-ttu-id="4ecb7-133">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-133">Accept wildcard characters?</span></span> |<span data-ttu-id="4ecb7-134">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="4ecb7-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="4ecb7-135">WebDeployPackage</span></span>
<span data-ttu-id="4ecb7-136">Witaj ścieżki toohello sieci web wdrożenia pakietu toopublish toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-136">hello path toohello web deployment package toopublish toohello virtual machine.</span></span> <span data-ttu-id="4ecb7-137">Ten pakiet można utworzyć za pomocą kreatora Publikowanie w sieci Web hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-137">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="4ecb7-138">Zobacz [jak: utworzyć pakiet wdrożeniowy sieci Web w programie Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ecb7-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="4ecb7-139">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4ecb7-139">Aliases</span></span> | <span data-ttu-id="4ecb7-140">Brak</span><span class="sxs-lookup"><span data-stu-id="4ecb7-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ecb7-141">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-141">Required?</span></span> |<span data-ttu-id="4ecb7-142">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-142">false</span></span> |
| <span data-ttu-id="4ecb7-143">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4ecb7-143">Position</span></span> |<span data-ttu-id="4ecb7-144">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4ecb7-144">named</span></span> |
| <span data-ttu-id="4ecb7-145">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4ecb7-145">Default value</span></span> |<span data-ttu-id="4ecb7-146">Brak</span><span class="sxs-lookup"><span data-stu-id="4ecb7-146">none</span></span> |
| <span data-ttu-id="4ecb7-147">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-147">Accept pipeline input?</span></span> |<span data-ttu-id="4ecb7-148">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-148">false</span></span> |
| <span data-ttu-id="4ecb7-149">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-149">Accept wildcard characters?</span></span> |<span data-ttu-id="4ecb7-150">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="4ecb7-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="4ecb7-151">AllowUntrusted</span></span>
<span data-ttu-id="4ecb7-152">Jeśli PRAWDA, Zezwól hello korzystanie z certyfikatów, które nie są podpisane przez zaufanego głównego urzędu.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-152">If true, allow hello use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="4ecb7-153">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4ecb7-153">Aliases</span></span> | <span data-ttu-id="4ecb7-154">Brak</span><span class="sxs-lookup"><span data-stu-id="4ecb7-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ecb7-155">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-155">Required?</span></span> |<span data-ttu-id="4ecb7-156">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-156">false</span></span> |
| <span data-ttu-id="4ecb7-157">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4ecb7-157">Position</span></span> |<span data-ttu-id="4ecb7-158">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4ecb7-158">named</span></span> |
| <span data-ttu-id="4ecb7-159">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4ecb7-159">Default value</span></span> |<span data-ttu-id="4ecb7-160">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-160">false</span></span> |
| <span data-ttu-id="4ecb7-161">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-161">Accept pipeline input?</span></span> |<span data-ttu-id="4ecb7-162">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-162">false</span></span> |
| <span data-ttu-id="4ecb7-163">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-163">Accept wildcard characters?</span></span> |<span data-ttu-id="4ecb7-164">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="4ecb7-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="4ecb7-165">VMPassword</span></span>
<span data-ttu-id="4ecb7-166">poświadczenia Hello hello konta maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-166">hello credentials for hello virtual machine account.</span></span> <span data-ttu-id="4ecb7-167">Przykład: - VMPassword @{nazwa = "admin"; Hasło = "password"}</span><span class="sxs-lookup"><span data-stu-id="4ecb7-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="4ecb7-168">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4ecb7-168">Aliases</span></span> | <span data-ttu-id="4ecb7-169">Brak</span><span class="sxs-lookup"><span data-stu-id="4ecb7-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ecb7-170">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-170">Required?</span></span> |<span data-ttu-id="4ecb7-171">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-171">false</span></span> |
| <span data-ttu-id="4ecb7-172">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4ecb7-172">Position</span></span> |<span data-ttu-id="4ecb7-173">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4ecb7-173">named</span></span> |
| <span data-ttu-id="4ecb7-174">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4ecb7-174">Default value</span></span> |<span data-ttu-id="4ecb7-175">Brak</span><span class="sxs-lookup"><span data-stu-id="4ecb7-175">none</span></span> |
| <span data-ttu-id="4ecb7-176">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-176">Accept pipeline input?</span></span> |<span data-ttu-id="4ecb7-177">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-177">false</span></span> |
| <span data-ttu-id="4ecb7-178">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-178">Accept wildcard characters?</span></span> |<span data-ttu-id="4ecb7-179">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="4ecb7-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="4ecb7-180">DatabaseServerPassword</span></span>
<span data-ttu-id="4ecb7-181">poświadczenia Hello hello bazy danych SQL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-181">hello credentials for hello SQL database in Azure.</span></span> <span data-ttu-id="4ecb7-182">Przykład: - DatabaseServerPassword @{nazwa = "admin"; Hasło = "password"}</span><span class="sxs-lookup"><span data-stu-id="4ecb7-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="4ecb7-183">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4ecb7-183">Aliases</span></span> | <span data-ttu-id="4ecb7-184">Brak</span><span class="sxs-lookup"><span data-stu-id="4ecb7-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ecb7-185">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-185">Required?</span></span> |<span data-ttu-id="4ecb7-186">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-186">false</span></span> |
| <span data-ttu-id="4ecb7-187">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4ecb7-187">Position</span></span> |<span data-ttu-id="4ecb7-188">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4ecb7-188">named</span></span> |
| <span data-ttu-id="4ecb7-189">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4ecb7-189">Default value</span></span> |<span data-ttu-id="4ecb7-190">Brak</span><span class="sxs-lookup"><span data-stu-id="4ecb7-190">none</span></span> |
| <span data-ttu-id="4ecb7-191">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-191">Accept pipeline input?</span></span> |<span data-ttu-id="4ecb7-192">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-192">false</span></span> |
| <span data-ttu-id="4ecb7-193">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-193">Accept wildcard characters?</span></span> |<span data-ttu-id="4ecb7-194">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="4ecb7-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="4ecb7-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="4ecb7-196">Jeśli PRAWDA, drukowania wiadomości powitania skryptu toohello output strumienia.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-196">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="4ecb7-197">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4ecb7-197">Aliases</span></span> | <span data-ttu-id="4ecb7-198">Brak</span><span class="sxs-lookup"><span data-stu-id="4ecb7-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ecb7-199">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-199">Required?</span></span> |<span data-ttu-id="4ecb7-200">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-200">false</span></span> |
| <span data-ttu-id="4ecb7-201">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="4ecb7-201">Position</span></span> |<span data-ttu-id="4ecb7-202">o nazwie</span><span class="sxs-lookup"><span data-stu-id="4ecb7-202">named</span></span> |
| <span data-ttu-id="4ecb7-203">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="4ecb7-203">Default value</span></span> |<span data-ttu-id="4ecb7-204">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-204">false</span></span> |
| <span data-ttu-id="4ecb7-205">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-205">Accept pipeline input?</span></span> |<span data-ttu-id="4ecb7-206">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-206">false</span></span> |
| <span data-ttu-id="4ecb7-207">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="4ecb7-207">Accept wildcard characters?</span></span> |<span data-ttu-id="4ecb7-208">wartość false</span><span class="sxs-lookup"><span data-stu-id="4ecb7-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="4ecb7-209">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4ecb7-209">Remarks</span></span>
<span data-ttu-id="4ecb7-210">Pełny opis sposobu toouse hello skryptu toocreate deweloperów i środowisk testowych, zobacz [tooDev tooPublish przy użyciu skrypty programu Windows PowerShell i środowisk testowych](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="4ecb7-210">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="4ecb7-211">plik konfiguracji JSON Hello określa szczegóły hello co to jest toobe wdrożone.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-211">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="4ecb7-212">Zawiera informacje dotyczące hello podane podczas tworzenia projektu hello, takie jak nazwa hello, grupy koligacji, obrazu wirtualnego dysku twardego i rozmiar maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-212">It includes hello information that you specified when you created hello project, such as hello name, affinity group, VHD image, and size of hello virtual machine.</span></span> <span data-ttu-id="4ecb7-213">Także zawiera punkty końcowe hello na maszynie wirtualnej hello hello tooprovision baz danych, jeśli istnieje i parametry wdrażania w sieci web.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-213">It also includes hello endpoints on hello virtual machine, hello databases tooprovision, if any, and web deployment parameters.</span></span> <span data-ttu-id="4ecb7-214">Witaj następującego kodu przedstawiono przykładowy plik konfiguracji JSON:</span><span class="sxs-lookup"><span data-stu-id="4ecb7-214">hello following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="4ecb7-215">Co to jest administracyjnie hello JSON konfiguracji pliku toochange można edytować.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-215">You can edit hello JSON configuration file toochange what is provisioned.</span></span> <span data-ttu-id="4ecb7-216">Maszyny wirtualne i usługi w chmurze są wymagane, ale hello bazy danych sekcja jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="4ecb7-216">A virtual machine and a cloud service are required, but hello database section is optional.</span></span>

