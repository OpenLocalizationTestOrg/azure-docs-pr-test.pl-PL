---
title: "Zarządzanie kontami usługi Azure Media przy użyciu programu PowerShell"
description: "Dowiedz się, jak zarządzać kontami usługi Azure Media Services za pomocą poleceń cmdlet programu PowerShell."
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: 3d999d9e27844bc0164cc3572522b9ec022118a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="51ecf-103">Zarządzanie kontami usługi Azure Media przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ecf-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="51ecf-104">Portal</span><span class="sxs-lookup"><span data-stu-id="51ecf-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="51ecf-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ecf-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="51ecf-106">REST</span><span class="sxs-lookup"><span data-stu-id="51ecf-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="51ecf-107">Aby można było utworzyć konto usługi Azure Media Services, musi mieć konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="51ecf-107">To be able to create an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="51ecf-108">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="51ecf-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="51ecf-109">Aby uzyskać szczegółowe informacje, zobacz artykuł <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Bezpłatna wersja próbna platformy Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="51ecf-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="51ecf-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="51ecf-110">Overview</span></span>
<span data-ttu-id="51ecf-111">Ten artykuł zawiera listę poleceń cmdlet programu Azure PowerShell dla usługi Azure Media Services (AMS) w ramach usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="51ecf-111">This article lists the Azure PowerShell cmdlets for Azure Media Services (AMS) in the Azure Resource Manager framework.</span></span> <span data-ttu-id="51ecf-112">Istnieją polecenia cmdlet w **Microsoft.Azure.Commands.Media** przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="51ecf-112">The cmdlets exist in the **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="51ecf-113">Wersje</span><span class="sxs-lookup"><span data-stu-id="51ecf-113">Versions</span></span>
<span data-ttu-id="51ecf-114">**ApiVersion**: "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="51ecf-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="51ecf-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="51ecf-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="51ecf-116">Tworzy usługę nośnika.</span><span class="sxs-lookup"><span data-stu-id="51ecf-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="51ecf-117">Składnia</span><span class="sxs-lookup"><span data-stu-id="51ecf-117">Syntax</span></span>
<span data-ttu-id="51ecf-118">Zestaw parametrów: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="51ecf-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="51ecf-119">Zestaw parametrów: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="51ecf-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="51ecf-120">Parametry</span><span class="sxs-lookup"><span data-stu-id="51ecf-120">Parameters</span></span>
<span data-ttu-id="51ecf-121">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-122">Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-122">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="51ecf-123">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-123">Aliases</span></span> | <span data-ttu-id="51ecf-124">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-125">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-125">Required?</span></span> |<span data-ttu-id="51ecf-126">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-126">true</span></span> |
| <span data-ttu-id="51ecf-127">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-127">Position?</span></span> |<span data-ttu-id="51ecf-128">0</span><span class="sxs-lookup"><span data-stu-id="51ecf-128">0</span></span> |
| <span data-ttu-id="51ecf-129">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-129">Default value</span></span> |<span data-ttu-id="51ecf-130">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-130">none</span></span> |
| <span data-ttu-id="51ecf-131">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-131">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-132">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-133">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-133">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-134">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-134">false</span></span> |

<span data-ttu-id="51ecf-135">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-136">Określa nazwę usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-136">Specifies the name of the media service.</span></span>

| <span data-ttu-id="51ecf-137">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-137">Aliases</span></span> | <span data-ttu-id="51ecf-138">Nazwa</span><span class="sxs-lookup"><span data-stu-id="51ecf-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-139">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-139">Required?</span></span> |<span data-ttu-id="51ecf-140">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-140">true</span></span> |
| <span data-ttu-id="51ecf-141">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-141">Position?</span></span> |<span data-ttu-id="51ecf-142">1</span><span class="sxs-lookup"><span data-stu-id="51ecf-142">1</span></span> |
| <span data-ttu-id="51ecf-143">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-143">Default value</span></span> |<span data-ttu-id="51ecf-144">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-144">none</span></span> |
| <span data-ttu-id="51ecf-145">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-145">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-146">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-146">false</span></span> |
| <span data-ttu-id="51ecf-147">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-147">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-148">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-148">false</span></span> |

<span data-ttu-id="51ecf-149">**-Lokalizacji &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-150">Określa lokalizację zasobów usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-150">Specifies the resource location of the media service.</span></span>

| <span data-ttu-id="51ecf-151">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-151">Aliases</span></span> | <span data-ttu-id="51ecf-152">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-153">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-153">Required?</span></span> |<span data-ttu-id="51ecf-154">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-154">true</span></span> |
| <span data-ttu-id="51ecf-155">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-155">Position?</span></span> |<span data-ttu-id="51ecf-156">2</span><span class="sxs-lookup"><span data-stu-id="51ecf-156">2</span></span> |
| <span data-ttu-id="51ecf-157">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-157">Default value</span></span> |<span data-ttu-id="51ecf-158">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-158">none</span></span> |
| <span data-ttu-id="51ecf-159">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-159">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-160">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-161">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-161">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-162">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-162">false</span></span> |

<span data-ttu-id="51ecf-163">**-StorageAccountId &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-164">Określa konto magazynu głównego, który skojarzony z usługą media.</span><span class="sxs-lookup"><span data-stu-id="51ecf-164">Specifies a primary storage account that associated with the media service.</span></span>

* <span data-ttu-id="51ecf-165">Nowe konto magazynu (utworzone przy użyciu interfejsu API usługi Resource Manager) obsługiwany tylko przez system.</span><span class="sxs-lookup"><span data-stu-id="51ecf-165">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="51ecf-166">Konto magazynu musi istnieć i ma tę samą lokalizację w usłudze media.</span><span class="sxs-lookup"><span data-stu-id="51ecf-166">The storage account must exist and has the same location with the media service.</span></span>

| <span data-ttu-id="51ecf-167">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-167">Aliases</span></span> | <span data-ttu-id="51ecf-168">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-169">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-169">Required?</span></span> |<span data-ttu-id="51ecf-170">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-170">true</span></span> |
| <span data-ttu-id="51ecf-171">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-171">Position?</span></span> |<span data-ttu-id="51ecf-172">3</span><span class="sxs-lookup"><span data-stu-id="51ecf-172">3</span></span> |
| <span data-ttu-id="51ecf-173">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-173">Default value</span></span> |<span data-ttu-id="51ecf-174">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-174">none</span></span> |
| <span data-ttu-id="51ecf-175">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-175">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-176">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-177">Nazwa zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="51ecf-177">Parameter set name</span></span> |<span data-ttu-id="51ecf-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="51ecf-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="51ecf-179">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-179">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-180">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-180">false</span></span> |

<span data-ttu-id="51ecf-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="51ecf-182">Określa kont magazynu, które są skojarzone z usługą media.</span><span class="sxs-lookup"><span data-stu-id="51ecf-182">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="51ecf-183">Nowe konto magazynu (utworzone przy użyciu interfejsu API usługi Resource Manager) obsługiwany tylko przez system.</span><span class="sxs-lookup"><span data-stu-id="51ecf-183">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="51ecf-184">Konto magazynu musi istnieć i ma tę samą lokalizację w usłudze media.</span><span class="sxs-lookup"><span data-stu-id="51ecf-184">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="51ecf-185">Tylko jedno konto magazynu można określić jako podstawowy.</span><span class="sxs-lookup"><span data-stu-id="51ecf-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="51ecf-186">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-186">Aliases</span></span> | <span data-ttu-id="51ecf-187">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-188">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-188">Required?</span></span> |<span data-ttu-id="51ecf-189">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-189">true</span></span> |
| <span data-ttu-id="51ecf-190">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-190">Position?</span></span> |<span data-ttu-id="51ecf-191">3</span><span class="sxs-lookup"><span data-stu-id="51ecf-191">3</span></span> |
| <span data-ttu-id="51ecf-192">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-192">Default value</span></span> |<span data-ttu-id="51ecf-193">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-193">none</span></span> |
| <span data-ttu-id="51ecf-194">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-194">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-195">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-196">Nazwa zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="51ecf-196">Parameter set name</span></span> |<span data-ttu-id="51ecf-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="51ecf-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="51ecf-198">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-198">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-199">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-199">false</span></span> |

<span data-ttu-id="51ecf-200">**-Znaczniki &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="51ecf-201">Określa tablicy skrótów tagów, które są skojarzone z usługą media.</span><span class="sxs-lookup"><span data-stu-id="51ecf-201">Specifies a hash table of the tags that are associated with the media service.</span></span>

* <span data-ttu-id="51ecf-202">Przykład: @{"tag1"="wartość1";" tag2 "=: wartość2"}</span><span class="sxs-lookup"><span data-stu-id="51ecf-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="51ecf-203">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-203">Aliases</span></span> | <span data-ttu-id="51ecf-204">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-205">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-205">Required?</span></span> |<span data-ttu-id="51ecf-206">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-206">false</span></span> |
| <span data-ttu-id="51ecf-207">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-207">Position?</span></span> |<span data-ttu-id="51ecf-208">o nazwie</span><span class="sxs-lookup"><span data-stu-id="51ecf-208">named</span></span> |
| <span data-ttu-id="51ecf-209">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-209">Default value</span></span> |<span data-ttu-id="51ecf-210">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-210">none</span></span> |
| <span data-ttu-id="51ecf-211">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-211">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-212">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-212">false</span></span> |
| <span data-ttu-id="51ecf-213">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-213">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-214">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-214">false</span></span> |

<span data-ttu-id="51ecf-215">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="51ecf-216">To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="51ecf-216">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="51ecf-217">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-217">Inputs</span></span>
<span data-ttu-id="51ecf-218">Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-218">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="51ecf-219">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-219">Outputs</span></span>
<span data-ttu-id="51ecf-220">Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-220">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="51ecf-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="51ecf-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="51ecf-222">Aktualizacje usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="51ecf-223">Składnia</span><span class="sxs-lookup"><span data-stu-id="51ecf-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="51ecf-224">Parametry</span><span class="sxs-lookup"><span data-stu-id="51ecf-224">Parameters</span></span>
<span data-ttu-id="51ecf-225">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-226">Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-226">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="51ecf-227">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-227">Aliases</span></span> | <span data-ttu-id="51ecf-228">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-229">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-229">Required?</span></span> |<span data-ttu-id="51ecf-230">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-230">true</span></span> |
| <span data-ttu-id="51ecf-231">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-231">Position?</span></span> |<span data-ttu-id="51ecf-232">0</span><span class="sxs-lookup"><span data-stu-id="51ecf-232">0</span></span> |
| <span data-ttu-id="51ecf-233">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-233">Default Value</span></span> |<span data-ttu-id="51ecf-234">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-234">none</span></span> |
| <span data-ttu-id="51ecf-235">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="51ecf-236">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-237">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-237">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-238">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-238">false</span></span> |

<span data-ttu-id="51ecf-239">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-240">Określa nazwę usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-240">Specifies the name of the media service.</span></span>

| <span data-ttu-id="51ecf-241">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-241">Aliases</span></span> | <span data-ttu-id="51ecf-242">Nazwa</span><span class="sxs-lookup"><span data-stu-id="51ecf-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-243">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-243">Required?</span></span> |<span data-ttu-id="51ecf-244">True</span><span class="sxs-lookup"><span data-stu-id="51ecf-244">True</span></span> |
| <span data-ttu-id="51ecf-245">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-245">Position?</span></span> |<span data-ttu-id="51ecf-246">1</span><span class="sxs-lookup"><span data-stu-id="51ecf-246">1</span></span> |
| <span data-ttu-id="51ecf-247">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-247">Default value</span></span> |<span data-ttu-id="51ecf-248">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-248">None</span></span> |
| <span data-ttu-id="51ecf-249">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-249">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-250">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-251">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-251">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-252">False</span><span class="sxs-lookup"><span data-stu-id="51ecf-252">False</span></span> |

<span data-ttu-id="51ecf-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="51ecf-254">Określa kont magazynu, które są skojarzone z usługą media.</span><span class="sxs-lookup"><span data-stu-id="51ecf-254">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="51ecf-255">Nowe konto magazynu (utworzone przy użyciu interfejsu API usługi Resource Manager) obsługiwany tylko przez system.</span><span class="sxs-lookup"><span data-stu-id="51ecf-255">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="51ecf-256">Konto magazynu musi istnieć i ma tę samą lokalizację w usłudze media.</span><span class="sxs-lookup"><span data-stu-id="51ecf-256">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="51ecf-257">Tylko jedno konto magazynu można określić jako podstawowy.</span><span class="sxs-lookup"><span data-stu-id="51ecf-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="51ecf-258">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-258">Aliases</span></span> | <span data-ttu-id="51ecf-259">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-260">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-260">Required?</span></span> |<span data-ttu-id="51ecf-261">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-261">false</span></span> |
| <span data-ttu-id="51ecf-262">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-262">Position?</span></span> |<span data-ttu-id="51ecf-263">o nazwie</span><span class="sxs-lookup"><span data-stu-id="51ecf-263">Named</span></span> |
| <span data-ttu-id="51ecf-264">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-264">Default value</span></span> |<span data-ttu-id="51ecf-265">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-265">none</span></span> |
| <span data-ttu-id="51ecf-266">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-266">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-267">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-268">Nazwa zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="51ecf-268">Parameter set name</span></span> |<span data-ttu-id="51ecf-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="51ecf-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="51ecf-270">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-270">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-271">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-271">false</span></span> |

<span data-ttu-id="51ecf-272">**-Znaczniki &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="51ecf-273">Określa tablicy skrótów tagów, które są skojarzone z tą usługą multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-273">Specifies a hash table of the tags that are associated with this media service.</span></span>

* <span data-ttu-id="51ecf-274">Tagi, które są skojarzone z usługą media są zastępowane podana przez klienta.</span><span class="sxs-lookup"><span data-stu-id="51ecf-274">The tags that are associated with the media service are replaced with value specified by the customer.</span></span>

| <span data-ttu-id="51ecf-275">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-275">Aliases</span></span> | <span data-ttu-id="51ecf-276">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-277">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-277">Required?</span></span> |<span data-ttu-id="51ecf-278">False</span><span class="sxs-lookup"><span data-stu-id="51ecf-278">False</span></span> |
| <span data-ttu-id="51ecf-279">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-279">Position?</span></span> |<span data-ttu-id="51ecf-280">o nazwie</span><span class="sxs-lookup"><span data-stu-id="51ecf-280">Named</span></span> |
| <span data-ttu-id="51ecf-281">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-281">Default value</span></span> |<span data-ttu-id="51ecf-282">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-282">None</span></span> |
| <span data-ttu-id="51ecf-283">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-283">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-284">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-285">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-285">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-286">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-286">false</span></span> |

<span data-ttu-id="51ecf-287">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="51ecf-288">To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="51ecf-288">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="51ecf-289">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-289">Inputs</span></span>
<span data-ttu-id="51ecf-290">Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-290">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="51ecf-291">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-291">Outputs</span></span>
<span data-ttu-id="51ecf-292">Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-292">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="51ecf-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="51ecf-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="51ecf-294">Usuwa usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="51ecf-295">Składnia</span><span class="sxs-lookup"><span data-stu-id="51ecf-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="51ecf-296">Parametry</span><span class="sxs-lookup"><span data-stu-id="51ecf-296">Parameters</span></span>
<span data-ttu-id="51ecf-297">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-298">Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-298">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="51ecf-299">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-299">Aliases</span></span> | <span data-ttu-id="51ecf-300">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-301">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-301">Required?</span></span> |<span data-ttu-id="51ecf-302">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-302">true</span></span> |
| <span data-ttu-id="51ecf-303">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-303">Position?</span></span> |<span data-ttu-id="51ecf-304">0</span><span class="sxs-lookup"><span data-stu-id="51ecf-304">0</span></span> |
| <span data-ttu-id="51ecf-305">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-305">Default value</span></span> |<span data-ttu-id="51ecf-306">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-306">none</span></span> |
| <span data-ttu-id="51ecf-307">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-307">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-308">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-309">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-309">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-310">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-310">false</span></span> |

<span data-ttu-id="51ecf-311">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-312">Określa nazwę usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-312">Specifies the name of the media service.</span></span>

| <span data-ttu-id="51ecf-313">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-313">Aliases</span></span> | <span data-ttu-id="51ecf-314">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-315">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-315">Required?</span></span> |<span data-ttu-id="51ecf-316">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-316">true</span></span> |
| <span data-ttu-id="51ecf-317">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-317">Position?</span></span> |<span data-ttu-id="51ecf-318">2</span><span class="sxs-lookup"><span data-stu-id="51ecf-318">2</span></span> |
| <span data-ttu-id="51ecf-319">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-319">Default value</span></span> |<span data-ttu-id="51ecf-320">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-320">None</span></span> |
| <span data-ttu-id="51ecf-321">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-321">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-322">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-323">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-323">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-324">False</span><span class="sxs-lookup"><span data-stu-id="51ecf-324">False</span></span> |

<span data-ttu-id="51ecf-325">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="51ecf-326">To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="51ecf-326">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="51ecf-327">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-327">Inputs</span></span>
<span data-ttu-id="51ecf-328">Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-328">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="51ecf-329">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-329">Outputs</span></span>
<span data-ttu-id="51ecf-330">Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-330">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="51ecf-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="51ecf-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="51ecf-332">Pobiera wszystkie usługi media services w grupie zasobów lub usług media o podanej nazwie.</span><span class="sxs-lookup"><span data-stu-id="51ecf-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="51ecf-333">Składnia</span><span class="sxs-lookup"><span data-stu-id="51ecf-333">Syntax</span></span>
<span data-ttu-id="51ecf-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="51ecf-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="51ecf-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="51ecf-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="51ecf-336">Parametry</span><span class="sxs-lookup"><span data-stu-id="51ecf-336">Parameters</span></span>
<span data-ttu-id="51ecf-337">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-338">Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-338">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="51ecf-339">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-339">Aliases</span></span> | <span data-ttu-id="51ecf-340">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-341">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-341">Required?</span></span> |<span data-ttu-id="51ecf-342">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-342">true</span></span> |
| <span data-ttu-id="51ecf-343">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-343">Position?</span></span> |<span data-ttu-id="51ecf-344">0</span><span class="sxs-lookup"><span data-stu-id="51ecf-344">0</span></span> |
| <span data-ttu-id="51ecf-345">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-345">Default value</span></span> |<span data-ttu-id="51ecf-346">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-346">none</span></span> |
| <span data-ttu-id="51ecf-347">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-347">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-348">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-349">Nazwa zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="51ecf-349">Parameter set name</span></span> |<span data-ttu-id="51ecf-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="51ecf-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="51ecf-351">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-351">Accept wildcard characters?</span></span>   <span data-ttu-id="51ecf-352">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-352">false</span></span>

<span data-ttu-id="51ecf-353">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-354">Określa nazwę usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-354">Specifies the name of the media service.</span></span>

| <span data-ttu-id="51ecf-355">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-355">Aliases</span></span> | <span data-ttu-id="51ecf-356">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-357">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-357">Required?</span></span> |<span data-ttu-id="51ecf-358">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-358">true</span></span> |
| <span data-ttu-id="51ecf-359">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-359">Position?</span></span> |<span data-ttu-id="51ecf-360">1</span><span class="sxs-lookup"><span data-stu-id="51ecf-360">1</span></span> |
| <span data-ttu-id="51ecf-361">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-361">Default value</span></span> |<span data-ttu-id="51ecf-362">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-362">none</span></span> |
| <span data-ttu-id="51ecf-363">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-363">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-364">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-365">Nazwa zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="51ecf-365">Parameter set name</span></span> |<span data-ttu-id="51ecf-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="51ecf-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="51ecf-367">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-367">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-368">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-368">false</span></span> |

<span data-ttu-id="51ecf-369">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="51ecf-370">To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="51ecf-370">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="51ecf-371">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-371">Inputs</span></span>
<span data-ttu-id="51ecf-372">Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-372">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="51ecf-373">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-373">Outputs</span></span>
<span data-ttu-id="51ecf-374">Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-374">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="51ecf-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="51ecf-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="51ecf-376">Pobiera klucze usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="51ecf-377">Składnia</span><span class="sxs-lookup"><span data-stu-id="51ecf-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="51ecf-378">Parametry</span><span class="sxs-lookup"><span data-stu-id="51ecf-378">Parameters</span></span>
<span data-ttu-id="51ecf-379">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-380">Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-380">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="51ecf-381">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-381">Aliases</span></span> | <span data-ttu-id="51ecf-382">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-383">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-383">Required?</span></span> |<span data-ttu-id="51ecf-384">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-384">true</span></span> |
| <span data-ttu-id="51ecf-385">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-385">Position?</span></span> |<span data-ttu-id="51ecf-386">0</span><span class="sxs-lookup"><span data-stu-id="51ecf-386">0</span></span> |
| <span data-ttu-id="51ecf-387">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-387">Default value</span></span> |<span data-ttu-id="51ecf-388">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-388">none</span></span> |
| <span data-ttu-id="51ecf-389">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-389">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-390">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-391">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-391">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-392">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-392">false</span></span> |

<span data-ttu-id="51ecf-393">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-394">Określa nazwę usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-394">Specifies the name of the media service.</span></span>

| <span data-ttu-id="51ecf-395">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-395">Aliases</span></span> | <span data-ttu-id="51ecf-396">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-397">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-397">Required?</span></span> |<span data-ttu-id="51ecf-398">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-398">true</span></span> |
| <span data-ttu-id="51ecf-399">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-399">Position?</span></span> |<span data-ttu-id="51ecf-400">1</span><span class="sxs-lookup"><span data-stu-id="51ecf-400">1</span></span> |
| <span data-ttu-id="51ecf-401">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-401">Default value</span></span> |<span data-ttu-id="51ecf-402">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-402">none</span></span> |
| <span data-ttu-id="51ecf-403">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-403">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-404">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-405">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-405">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-406">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-406">false</span></span> |

<span data-ttu-id="51ecf-407">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="51ecf-408">To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="51ecf-408">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="51ecf-409">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-409">Inputs</span></span>
<span data-ttu-id="51ecf-410">Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-410">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="51ecf-411">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-411">Outputs</span></span>
<span data-ttu-id="51ecf-412">Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-412">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="51ecf-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="51ecf-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="51ecf-414">Generuje ponownie klucz podstawowy lub pomocniczy usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="51ecf-415">Składnia</span><span class="sxs-lookup"><span data-stu-id="51ecf-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="51ecf-416">Parametry</span><span class="sxs-lookup"><span data-stu-id="51ecf-416">Parameters</span></span>
<span data-ttu-id="51ecf-417">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-418">Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-418">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="51ecf-419">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-419">Aliases</span></span> | <span data-ttu-id="51ecf-420">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-421">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-421">Required?</span></span> |<span data-ttu-id="51ecf-422">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-422">true</span></span> |
| <span data-ttu-id="51ecf-423">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-423">Position?</span></span> |<span data-ttu-id="51ecf-424">0</span><span class="sxs-lookup"><span data-stu-id="51ecf-424">0</span></span> |
| <span data-ttu-id="51ecf-425">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-425">Default value</span></span> |<span data-ttu-id="51ecf-426">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-426">none</span></span> |
| <span data-ttu-id="51ecf-427">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-427">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-428">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-429">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-429">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-430">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-430">false</span></span> |

<span data-ttu-id="51ecf-431">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-432">Określa nazwę usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-432">Specifies the name of the media service.</span></span>

| <span data-ttu-id="51ecf-433">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-433">Aliases</span></span> | <span data-ttu-id="51ecf-434">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-435">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-435">Required?</span></span> |<span data-ttu-id="51ecf-436">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-436">true</span></span> |
| <span data-ttu-id="51ecf-437">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-437">Position?</span></span> |<span data-ttu-id="51ecf-438">1</span><span class="sxs-lookup"><span data-stu-id="51ecf-438">1</span></span> |
| <span data-ttu-id="51ecf-439">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-439">Default value</span></span> |<span data-ttu-id="51ecf-440">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-440">none</span></span> |
| <span data-ttu-id="51ecf-441">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-441">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-442">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-443">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-443">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-444">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-444">false</span></span> |

<span data-ttu-id="51ecf-445">**-KeyType &lt;Właściwość KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="51ecf-446">Określa typ klucza usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-446">Specifies the key type of the media service.</span></span>

* <span data-ttu-id="51ecf-447">Podstawowy lub pomocniczy</span><span class="sxs-lookup"><span data-stu-id="51ecf-447">Primary or Secondary</span></span>

| <span data-ttu-id="51ecf-448">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-448">Aliases</span></span> | <span data-ttu-id="51ecf-449">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-450">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-450">Required?</span></span> |<span data-ttu-id="51ecf-451">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-451">true</span></span> |
| <span data-ttu-id="51ecf-452">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-452">Position?</span></span> |<span data-ttu-id="51ecf-453">2</span><span class="sxs-lookup"><span data-stu-id="51ecf-453">2</span></span> |
| <span data-ttu-id="51ecf-454">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-454">Default value</span></span> |<span data-ttu-id="51ecf-455">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-455">none</span></span> |
| <span data-ttu-id="51ecf-456">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-456">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-457">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-457">false</span></span> |
| <span data-ttu-id="51ecf-458">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-458">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-459">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-459">false</span></span> |

<span data-ttu-id="51ecf-460">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="51ecf-461">To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="51ecf-461">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="51ecf-462">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-462">Inputs</span></span>
<span data-ttu-id="51ecf-463">Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-463">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="51ecf-464">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-464">Outputs</span></span>
<span data-ttu-id="51ecf-465">Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-465">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="51ecf-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="51ecf-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="51ecf-467">Synchronizuje klucze konta magazynu dla konta magazynu skojarzone z usługą media.</span><span class="sxs-lookup"><span data-stu-id="51ecf-467">Synchronizes storage account keys for a storage account associated with the media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="51ecf-468">Składnia</span><span class="sxs-lookup"><span data-stu-id="51ecf-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="51ecf-469">Parametry</span><span class="sxs-lookup"><span data-stu-id="51ecf-469">Parameters</span></span>
<span data-ttu-id="51ecf-470">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-471">Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-471">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="51ecf-472">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-472">Aliases</span></span> | <span data-ttu-id="51ecf-473">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-474">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-474">Required?</span></span> |<span data-ttu-id="51ecf-475">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-475">true</span></span> |
| <span data-ttu-id="51ecf-476">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-476">Position?</span></span> |<span data-ttu-id="51ecf-477">0</span><span class="sxs-lookup"><span data-stu-id="51ecf-477">0</span></span> |
| <span data-ttu-id="51ecf-478">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-478">Default value</span></span> |<span data-ttu-id="51ecf-479">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-479">none</span></span> |
| <span data-ttu-id="51ecf-480">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-480">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-481">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-482">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-482">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-483">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-483">false</span></span> |

<span data-ttu-id="51ecf-484">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-485">Określa nazwę usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="51ecf-485">Specifies the name of the media service.</span></span>

| <span data-ttu-id="51ecf-486">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-486">Aliases</span></span> | <span data-ttu-id="51ecf-487">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-488">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-488">Required?</span></span> |<span data-ttu-id="51ecf-489">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-489">true</span></span> |
| <span data-ttu-id="51ecf-490">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-490">Position?</span></span> |<span data-ttu-id="51ecf-491">1</span><span class="sxs-lookup"><span data-stu-id="51ecf-491">1</span></span> |
| <span data-ttu-id="51ecf-492">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-492">Default value</span></span> |<span data-ttu-id="51ecf-493">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-493">none</span></span> |
| <span data-ttu-id="51ecf-494">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-494">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-495">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-496">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-496">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-497">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-497">false</span></span> |

<span data-ttu-id="51ecf-498">**-StorageAccountId &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="51ecf-499">Określa konto magazynu skojarzonych z usługą media.</span><span class="sxs-lookup"><span data-stu-id="51ecf-499">Specifies the storage account associated with the media service.</span></span>

| <span data-ttu-id="51ecf-500">Aliasy</span><span class="sxs-lookup"><span data-stu-id="51ecf-500">Aliases</span></span> | <span data-ttu-id="51ecf-501">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="51ecf-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="51ecf-502">Wymagane?</span><span class="sxs-lookup"><span data-stu-id="51ecf-502">Required?</span></span> |<span data-ttu-id="51ecf-503">Wartość true</span><span class="sxs-lookup"><span data-stu-id="51ecf-503">true</span></span> |
| <span data-ttu-id="51ecf-504">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="51ecf-504">Position?</span></span> |<span data-ttu-id="51ecf-505">2</span><span class="sxs-lookup"><span data-stu-id="51ecf-505">2</span></span> |
| <span data-ttu-id="51ecf-506">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="51ecf-506">Default value</span></span> |<span data-ttu-id="51ecf-507">Brak</span><span class="sxs-lookup"><span data-stu-id="51ecf-507">none</span></span> |
| <span data-ttu-id="51ecf-508">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="51ecf-508">Accept pipeline input?</span></span> |<span data-ttu-id="51ecf-509">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="51ecf-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="51ecf-510">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="51ecf-510">Accept wildcard characters?</span></span> |<span data-ttu-id="51ecf-511">wartość false</span><span class="sxs-lookup"><span data-stu-id="51ecf-511">false</span></span> |

<span data-ttu-id="51ecf-512">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="51ecf-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="51ecf-513">To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="51ecf-513">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="51ecf-514">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-514">Inputs</span></span>
<span data-ttu-id="51ecf-515">Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-515">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="51ecf-516">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="51ecf-516">Outputs</span></span>
<span data-ttu-id="51ecf-517">Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51ecf-517">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="51ecf-518">Następny krok</span><span class="sxs-lookup"><span data-stu-id="51ecf-518">Next step</span></span>
<span data-ttu-id="51ecf-519">Zapoznaj się z ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="51ecf-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="51ecf-520">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="51ecf-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

