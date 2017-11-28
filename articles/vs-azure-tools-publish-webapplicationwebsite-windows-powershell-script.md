---
title: aaaPublish-WebApplicationWebSite (skrypt programu Windows PowerShell) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toopublish sieci web projektu tooan witryny sieci Web platformy Azure. Ten skrypt tworzy hello wymaganych zasobów w Twojej subskrypcji platformy Azure, jeśli nie istnieją."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="9c31b-104">Publikowanie WebApplicationWebSite (skrypt programu Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="9c31b-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="9c31b-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="9c31b-105">Syntax</span></span>
<span data-ttu-id="9c31b-106">Publikuje tooan projektu sieci web Azure witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9c31b-106">Publishes a web project tooan Azure website.</span></span> <span data-ttu-id="9c31b-107">Witaj skrypt tworzy hello wymaganych zasobów w Twojej subskrypcji platformy Azure, jeśli nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="9c31b-107">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="9c31b-108">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="9c31b-108">Configuration</span></span>
<span data-ttu-id="9c31b-109">Witaj ścieżki toohello plik JSON konfiguracji opisujący szczegóły hello hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9c31b-109">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="9c31b-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="9c31b-110">Parameter</span></span> | <span data-ttu-id="9c31b-111">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="9c31b-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="9c31b-112">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9c31b-112">Aliases</span></span> |<span data-ttu-id="9c31b-113">Brak</span><span class="sxs-lookup"><span data-stu-id="9c31b-113">none</span></span> |
| <span data-ttu-id="9c31b-114">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="9c31b-114">Required?</span></span> |<span data-ttu-id="9c31b-115">Wartość true</span><span class="sxs-lookup"><span data-stu-id="9c31b-115">true</span></span> |
| <span data-ttu-id="9c31b-116">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="9c31b-116">Position</span></span> |<span data-ttu-id="9c31b-117">o nazwie</span><span class="sxs-lookup"><span data-stu-id="9c31b-117">named</span></span> |
| <span data-ttu-id="9c31b-118">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="9c31b-118">Default value</span></span> |<span data-ttu-id="9c31b-119">Brak</span><span class="sxs-lookup"><span data-stu-id="9c31b-119">none</span></span> |
| <span data-ttu-id="9c31b-120">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="9c31b-120">Accept pipeline input?</span></span> |<span data-ttu-id="9c31b-121">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-121">false</span></span> |
| <span data-ttu-id="9c31b-122">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="9c31b-122">Accept wildcard characters?</span></span> |<span data-ttu-id="9c31b-123">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="9c31b-124">Nazwa subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9c31b-124">SubscriptionName</span></span>
<span data-ttu-id="9c31b-125">Nazwa Hello hello subskrypcji platformy Azure, który ma być toocreate hello witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9c31b-125">hello name of hello Azure subscription that you want toocreate hello website in.</span></span>

| <span data-ttu-id="9c31b-126">Parametr</span><span class="sxs-lookup"><span data-stu-id="9c31b-126">Parameter</span></span> | <span data-ttu-id="9c31b-127">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="9c31b-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="9c31b-128">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9c31b-128">Aliases</span></span> |<span data-ttu-id="9c31b-129">Brak</span><span class="sxs-lookup"><span data-stu-id="9c31b-129">none</span></span> |
| <span data-ttu-id="9c31b-130">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="9c31b-130">Required?</span></span> |<span data-ttu-id="9c31b-131">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-131">false</span></span> |
| <span data-ttu-id="9c31b-132">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="9c31b-132">Position</span></span> |<span data-ttu-id="9c31b-133">o nazwie</span><span class="sxs-lookup"><span data-stu-id="9c31b-133">named</span></span> |
| <span data-ttu-id="9c31b-134">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="9c31b-134">Default value</span></span> |<span data-ttu-id="9c31b-135">Brak</span><span class="sxs-lookup"><span data-stu-id="9c31b-135">none</span></span> |
| <span data-ttu-id="9c31b-136">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="9c31b-136">Accept pipeline input?</span></span> |<span data-ttu-id="9c31b-137">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-137">false</span></span> |
| <span data-ttu-id="9c31b-138">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="9c31b-138">Accept wildcard characters?</span></span> |<span data-ttu-id="9c31b-139">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="9c31b-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="9c31b-140">WebDeployPackage</span></span>
<span data-ttu-id="9c31b-141">Witaj ścieżki toohello sieci web wdrożenia pakietu toopublish toohello witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9c31b-141">hello path toohello web deployment package toopublish toohello website.</span></span> <span data-ttu-id="9c31b-142">Ten pakiet można utworzyć za pomocą kreatora Publikowanie w sieci Web hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9c31b-142">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="9c31b-143">Aby uzyskać więcej informacji, zobacz [wprowadzenie do usług Azure Cloud Services i platformy ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="9c31b-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="9c31b-144">Parametr</span><span class="sxs-lookup"><span data-stu-id="9c31b-144">Parameter</span></span> | <span data-ttu-id="9c31b-145">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="9c31b-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="9c31b-146">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9c31b-146">Aliases</span></span> |<span data-ttu-id="9c31b-147">Brak</span><span class="sxs-lookup"><span data-stu-id="9c31b-147">none</span></span> |
| <span data-ttu-id="9c31b-148">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="9c31b-148">Required?</span></span> |<span data-ttu-id="9c31b-149">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-149">false</span></span> |
| <span data-ttu-id="9c31b-150">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="9c31b-150">Position</span></span> |<span data-ttu-id="9c31b-151">o nazwie</span><span class="sxs-lookup"><span data-stu-id="9c31b-151">named</span></span> |
| <span data-ttu-id="9c31b-152">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="9c31b-152">Default value</span></span> |<span data-ttu-id="9c31b-153">Brak</span><span class="sxs-lookup"><span data-stu-id="9c31b-153">none</span></span> |
| <span data-ttu-id="9c31b-154">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="9c31b-154">Accept pipeline input?</span></span> |<span data-ttu-id="9c31b-155">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-155">false</span></span> |
| <span data-ttu-id="9c31b-156">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="9c31b-156">Accept wildcard characters?</span></span> |<span data-ttu-id="9c31b-157">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="9c31b-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="9c31b-158">DatabaseServerPassword</span></span>
<span data-ttu-id="9c31b-159">Hello nazwy użytkownika i hasło dla bazy danych SQL hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9c31b-159">hello username and password for hello SQL database in Azure.</span></span>

| <span data-ttu-id="9c31b-160">Parametr</span><span class="sxs-lookup"><span data-stu-id="9c31b-160">Parameter</span></span> | <span data-ttu-id="9c31b-161">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="9c31b-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="9c31b-162">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9c31b-162">Aliases</span></span> |<span data-ttu-id="9c31b-163">Brak</span><span class="sxs-lookup"><span data-stu-id="9c31b-163">none</span></span> |
| <span data-ttu-id="9c31b-164">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="9c31b-164">Required?</span></span> |<span data-ttu-id="9c31b-165">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-165">false</span></span> |
| <span data-ttu-id="9c31b-166">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="9c31b-166">Position</span></span> |<span data-ttu-id="9c31b-167">o nazwie</span><span class="sxs-lookup"><span data-stu-id="9c31b-167">named</span></span> |
| <span data-ttu-id="9c31b-168">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="9c31b-168">Default value</span></span> |<span data-ttu-id="9c31b-169">Brak</span><span class="sxs-lookup"><span data-stu-id="9c31b-169">none</span></span> |
| <span data-ttu-id="9c31b-170">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="9c31b-170">Accept pipeline input?</span></span> |<span data-ttu-id="9c31b-171">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-171">false</span></span> |
| <span data-ttu-id="9c31b-172">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="9c31b-172">Accept wildcard characters?</span></span> |<span data-ttu-id="9c31b-173">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="9c31b-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="9c31b-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="9c31b-175">Jeśli PRAWDA, drukowania wiadomości powitania skryptu toohello output strumienia.</span><span class="sxs-lookup"><span data-stu-id="9c31b-175">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="9c31b-176">Parametr</span><span class="sxs-lookup"><span data-stu-id="9c31b-176">Parameter</span></span> | <span data-ttu-id="9c31b-177">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="9c31b-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="9c31b-178">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9c31b-178">Aliases</span></span> |<span data-ttu-id="9c31b-179">Brak</span><span class="sxs-lookup"><span data-stu-id="9c31b-179">none</span></span> |
| <span data-ttu-id="9c31b-180">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="9c31b-180">Required?</span></span> |<span data-ttu-id="9c31b-181">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-181">false</span></span> |
| <span data-ttu-id="9c31b-182">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="9c31b-182">Position</span></span> |<span data-ttu-id="9c31b-183">o nazwie</span><span class="sxs-lookup"><span data-stu-id="9c31b-183">named</span></span> |
| <span data-ttu-id="9c31b-184">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="9c31b-184">Default value</span></span> |<span data-ttu-id="9c31b-185">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-185">false</span></span> |
| <span data-ttu-id="9c31b-186">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="9c31b-186">Accept pipeline input?</span></span> |<span data-ttu-id="9c31b-187">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-187">false</span></span> |
| <span data-ttu-id="9c31b-188">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="9c31b-188">Accept wildcard characters?</span></span> |<span data-ttu-id="9c31b-189">wartość false</span><span class="sxs-lookup"><span data-stu-id="9c31b-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="9c31b-190">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9c31b-190">Remarks</span></span>
<span data-ttu-id="9c31b-191">Pełny opis sposobu toouse hello skryptu toocreate deweloperów i środowisk testowych, zobacz [tooDev tooPublish przy użyciu skrypty programu Windows PowerShell i środowisk testowych](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="9c31b-191">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="9c31b-192">plik konfiguracji JSON Hello określa szczegóły hello co to jest toobe wdrożone.</span><span class="sxs-lookup"><span data-stu-id="9c31b-192">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="9c31b-193">Zawiera informacje dotyczące hello podane podczas tworzenia projektu hello, takie jak nazwa hello i nazwa użytkownika dla witryny sieci Web hello.</span><span class="sxs-lookup"><span data-stu-id="9c31b-193">It includes hello information that you specified when you created hello project, such as hello name and username for hello website.</span></span> <span data-ttu-id="9c31b-194">Obejmuje on też hello tooprovision bazy danych, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="9c31b-194">It also includes hello database tooprovision, if any.</span></span> <span data-ttu-id="9c31b-195">Witaj następującego kodu przedstawiono przykładowy plik konfiguracji JSON:</span><span class="sxs-lookup"><span data-stu-id="9c31b-195">hello following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="9c31b-196">Co to jest wdrażany hello JSON konfiguracji pliku toochange można edytować.</span><span class="sxs-lookup"><span data-stu-id="9c31b-196">You can edit hello JSON configuration file toochange what is deployed.</span></span> <span data-ttu-id="9c31b-197">Sekcja witryny sieci Web jest wymagana, ale hello bazy danych sekcja jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="9c31b-197">A webSite section is required, but hello database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c31b-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9c31b-198">Next steps</span></span>
<span data-ttu-id="9c31b-199">Aby uzyskać więcej informacji, zobacz [Publish-WebApplicationVM (skrypt programu Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="9c31b-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

