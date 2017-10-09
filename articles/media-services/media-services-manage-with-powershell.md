---
title: "aaaManage kont usługi Azure Media przy użyciu programu PowerShell"
description: "Dowiedz się, jak toomanage usługi Azure Media Services kont za pomocą poleceń cmdlet programu PowerShell."
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
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="380e1-103">Zarządzanie kontami usługi Azure Media przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="380e1-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="380e1-104">Portal</span><span class="sxs-lookup"><span data-stu-id="380e1-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="380e1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="380e1-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="380e1-106">REST</span><span class="sxs-lookup"><span data-stu-id="380e1-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="380e1-107">toobe stanie toocreate konta usługi Azure Media Services, musi mieć konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="380e1-107">toobe able toocreate an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="380e1-108">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="380e1-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="380e1-109">Aby uzyskać szczegółowe informacje, zobacz artykuł <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Bezpłatna wersja próbna platformy Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="380e1-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="380e1-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="380e1-110">Overview</span></span>
<span data-ttu-id="380e1-111">Ten artykuł zawiera listę poleceń cmdlet programu Azure PowerShell hello Azure Media Services (AMS) w ramach usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-111">This article lists hello Azure PowerShell cmdlets for Azure Media Services (AMS) in hello Azure Resource Manager framework.</span></span> <span data-ttu-id="380e1-112">polecenia cmdlet Hello istnieje w hello **Microsoft.Azure.Commands.Media** przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="380e1-112">hello cmdlets exist in hello **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="380e1-113">Wersje</span><span class="sxs-lookup"><span data-stu-id="380e1-113">Versions</span></span>
<span data-ttu-id="380e1-114">**ApiVersion**: "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="380e1-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="380e1-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="380e1-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="380e1-116">Tworzy usługę nośnika.</span><span class="sxs-lookup"><span data-stu-id="380e1-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="380e1-117">Składnia</span><span class="sxs-lookup"><span data-stu-id="380e1-117">Syntax</span></span>
<span data-ttu-id="380e1-118">Zestaw parametrów: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="380e1-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="380e1-119">Zestaw parametrów: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="380e1-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="380e1-120">Parametry</span><span class="sxs-lookup"><span data-stu-id="380e1-120">Parameters</span></span>
<span data-ttu-id="380e1-121">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-122">Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="380e1-122">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="380e1-123">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-123">Aliases</span></span> | <span data-ttu-id="380e1-124">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-125">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-125">Required?</span></span> |<span data-ttu-id="380e1-126">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-126">true</span></span> |
| <span data-ttu-id="380e1-127">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-127">Position?</span></span> |<span data-ttu-id="380e1-128">0</span><span class="sxs-lookup"><span data-stu-id="380e1-128">0</span></span> |
| <span data-ttu-id="380e1-129">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-129">Default value</span></span> |<span data-ttu-id="380e1-130">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-130">none</span></span> |
| <span data-ttu-id="380e1-131">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-131">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-132">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-133">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-133">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-134">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-134">false</span></span> |

<span data-ttu-id="380e1-135">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-136">Określa nazwę usługi multimediów hello hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-136">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="380e1-137">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-137">Aliases</span></span> | <span data-ttu-id="380e1-138">Nazwa</span><span class="sxs-lookup"><span data-stu-id="380e1-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-139">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-139">Required?</span></span> |<span data-ttu-id="380e1-140">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-140">true</span></span> |
| <span data-ttu-id="380e1-141">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-141">Position?</span></span> |<span data-ttu-id="380e1-142">1</span><span class="sxs-lookup"><span data-stu-id="380e1-142">1</span></span> |
| <span data-ttu-id="380e1-143">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-143">Default value</span></span> |<span data-ttu-id="380e1-144">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-144">none</span></span> |
| <span data-ttu-id="380e1-145">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-145">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-146">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-146">false</span></span> |
| <span data-ttu-id="380e1-147">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-147">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-148">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-148">false</span></span> |

<span data-ttu-id="380e1-149">**-Lokalizacji &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-150">Określa lokalizację zasobów hello hello media service.</span><span class="sxs-lookup"><span data-stu-id="380e1-150">Specifies hello resource location of hello media service.</span></span>

| <span data-ttu-id="380e1-151">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-151">Aliases</span></span> | <span data-ttu-id="380e1-152">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-153">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-153">Required?</span></span> |<span data-ttu-id="380e1-154">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-154">true</span></span> |
| <span data-ttu-id="380e1-155">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-155">Position?</span></span> |<span data-ttu-id="380e1-156">2</span><span class="sxs-lookup"><span data-stu-id="380e1-156">2</span></span> |
| <span data-ttu-id="380e1-157">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-157">Default value</span></span> |<span data-ttu-id="380e1-158">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-158">none</span></span> |
| <span data-ttu-id="380e1-159">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-159">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-160">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-161">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-161">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-162">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-162">false</span></span> |

<span data-ttu-id="380e1-163">**-StorageAccountId &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-164">Określa konto magazynu głównego, który skojarzony z usługą media hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-164">Specifies a primary storage account that associated with hello media service.</span></span>

* <span data-ttu-id="380e1-165">Nowe konto magazynu (utworzone z hello interfejsu API usługi Resource Manager) obsługiwany tylko przez system.</span><span class="sxs-lookup"><span data-stu-id="380e1-165">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="380e1-166">Witaj konta magazynu musi istnieć i ma hello tej samej lokalizacji z usługą media hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-166">hello storage account must exist and has hello same location with hello media service.</span></span>

| <span data-ttu-id="380e1-167">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-167">Aliases</span></span> | <span data-ttu-id="380e1-168">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-169">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-169">Required?</span></span> |<span data-ttu-id="380e1-170">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-170">true</span></span> |
| <span data-ttu-id="380e1-171">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-171">Position?</span></span> |<span data-ttu-id="380e1-172">3</span><span class="sxs-lookup"><span data-stu-id="380e1-172">3</span></span> |
| <span data-ttu-id="380e1-173">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-173">Default value</span></span> |<span data-ttu-id="380e1-174">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-174">none</span></span> |
| <span data-ttu-id="380e1-175">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-175">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-176">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-177">Nazwa zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="380e1-177">Parameter set name</span></span> |<span data-ttu-id="380e1-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="380e1-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="380e1-179">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-179">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-180">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-180">false</span></span> |

<span data-ttu-id="380e1-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="380e1-182">Określa kont magazynu, które są skojarzone z usługą media hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-182">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="380e1-183">Nowe konto magazynu (utworzone z hello interfejsu API usługi Resource Manager) obsługiwany tylko przez system.</span><span class="sxs-lookup"><span data-stu-id="380e1-183">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="380e1-184">Witaj konta magazynu musi istnieć i ma hello tej samej lokalizacji z usługą media hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-184">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="380e1-185">Tylko jedno konto magazynu można określić jako podstawowy.</span><span class="sxs-lookup"><span data-stu-id="380e1-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="380e1-186">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-186">Aliases</span></span> | <span data-ttu-id="380e1-187">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-188">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-188">Required?</span></span> |<span data-ttu-id="380e1-189">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-189">true</span></span> |
| <span data-ttu-id="380e1-190">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-190">Position?</span></span> |<span data-ttu-id="380e1-191">3</span><span class="sxs-lookup"><span data-stu-id="380e1-191">3</span></span> |
| <span data-ttu-id="380e1-192">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-192">Default value</span></span> |<span data-ttu-id="380e1-193">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-193">none</span></span> |
| <span data-ttu-id="380e1-194">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-194">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-195">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-196">Nazwa zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="380e1-196">Parameter set name</span></span> |<span data-ttu-id="380e1-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="380e1-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="380e1-198">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-198">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-199">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-199">false</span></span> |

<span data-ttu-id="380e1-200">**-Znaczniki &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="380e1-201">Określa tablicy skrótów hello tagów, które są skojarzone z usługą media hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-201">Specifies a hash table of hello tags that are associated with hello media service.</span></span>

* <span data-ttu-id="380e1-202">Przykład: @{"tag1"="wartość1";" tag2 "=: wartość2"}</span><span class="sxs-lookup"><span data-stu-id="380e1-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="380e1-203">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-203">Aliases</span></span> | <span data-ttu-id="380e1-204">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-205">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-205">Required?</span></span> |<span data-ttu-id="380e1-206">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-206">false</span></span> |
| <span data-ttu-id="380e1-207">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-207">Position?</span></span> |<span data-ttu-id="380e1-208">o nazwie</span><span class="sxs-lookup"><span data-stu-id="380e1-208">named</span></span> |
| <span data-ttu-id="380e1-209">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-209">Default value</span></span> |<span data-ttu-id="380e1-210">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-210">none</span></span> |
| <span data-ttu-id="380e1-211">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-211">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-212">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-212">false</span></span> |
| <span data-ttu-id="380e1-213">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-213">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-214">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-214">false</span></span> |

<span data-ttu-id="380e1-215">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="380e1-216">To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="380e1-216">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="380e1-217">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-217">Inputs</span></span>
<span data-ttu-id="380e1-218">Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-218">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="380e1-219">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-219">Outputs</span></span>
<span data-ttu-id="380e1-220">Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-220">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="380e1-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="380e1-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="380e1-222">Aktualizacje usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="380e1-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="380e1-223">Składnia</span><span class="sxs-lookup"><span data-stu-id="380e1-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="380e1-224">Parametry</span><span class="sxs-lookup"><span data-stu-id="380e1-224">Parameters</span></span>
<span data-ttu-id="380e1-225">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-226">Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="380e1-226">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="380e1-227">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-227">Aliases</span></span> | <span data-ttu-id="380e1-228">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-229">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-229">Required?</span></span> |<span data-ttu-id="380e1-230">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-230">true</span></span> |
| <span data-ttu-id="380e1-231">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-231">Position?</span></span> |<span data-ttu-id="380e1-232">0</span><span class="sxs-lookup"><span data-stu-id="380e1-232">0</span></span> |
| <span data-ttu-id="380e1-233">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-233">Default Value</span></span> |<span data-ttu-id="380e1-234">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-234">none</span></span> |
| <span data-ttu-id="380e1-235">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="380e1-236">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-237">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-237">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-238">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-238">false</span></span> |

<span data-ttu-id="380e1-239">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-240">Określa nazwę usługi multimediów hello hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-240">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="380e1-241">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-241">Aliases</span></span> | <span data-ttu-id="380e1-242">Nazwa</span><span class="sxs-lookup"><span data-stu-id="380e1-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-243">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-243">Required?</span></span> |<span data-ttu-id="380e1-244">True</span><span class="sxs-lookup"><span data-stu-id="380e1-244">True</span></span> |
| <span data-ttu-id="380e1-245">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-245">Position?</span></span> |<span data-ttu-id="380e1-246">1</span><span class="sxs-lookup"><span data-stu-id="380e1-246">1</span></span> |
| <span data-ttu-id="380e1-247">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-247">Default value</span></span> |<span data-ttu-id="380e1-248">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-248">None</span></span> |
| <span data-ttu-id="380e1-249">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-249">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-250">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-251">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-251">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-252">False</span><span class="sxs-lookup"><span data-stu-id="380e1-252">False</span></span> |

<span data-ttu-id="380e1-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="380e1-254">Określa kont magazynu, które są skojarzone z usługą media hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-254">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="380e1-255">Nowe konto magazynu (utworzone z hello interfejsu API usługi Resource Manager) obsługiwany tylko przez system.</span><span class="sxs-lookup"><span data-stu-id="380e1-255">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="380e1-256">Witaj konta magazynu musi istnieć i ma hello tej samej lokalizacji z usługą media hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-256">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="380e1-257">Tylko jedno konto magazynu można określić jako podstawowy.</span><span class="sxs-lookup"><span data-stu-id="380e1-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="380e1-258">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-258">Aliases</span></span> | <span data-ttu-id="380e1-259">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-260">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-260">Required?</span></span> |<span data-ttu-id="380e1-261">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-261">false</span></span> |
| <span data-ttu-id="380e1-262">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-262">Position?</span></span> |<span data-ttu-id="380e1-263">o nazwie</span><span class="sxs-lookup"><span data-stu-id="380e1-263">Named</span></span> |
| <span data-ttu-id="380e1-264">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-264">Default value</span></span> |<span data-ttu-id="380e1-265">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-265">none</span></span> |
| <span data-ttu-id="380e1-266">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-266">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-267">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-268">Nazwa zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="380e1-268">Parameter set name</span></span> |<span data-ttu-id="380e1-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="380e1-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="380e1-270">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-270">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-271">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-271">false</span></span> |

<span data-ttu-id="380e1-272">**-Znaczniki &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="380e1-273">Określa tablicy skrótów hello tagów, które są skojarzone z tą usługą media.</span><span class="sxs-lookup"><span data-stu-id="380e1-273">Specifies a hash table of hello tags that are associated with this media service.</span></span>

* <span data-ttu-id="380e1-274">Witaj tagi, które są skojarzone z usługą media hello są zastępowane wartość określoną przez powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="380e1-274">hello tags that are associated with hello media service are replaced with value specified by hello customer.</span></span>

| <span data-ttu-id="380e1-275">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-275">Aliases</span></span> | <span data-ttu-id="380e1-276">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-277">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-277">Required?</span></span> |<span data-ttu-id="380e1-278">False</span><span class="sxs-lookup"><span data-stu-id="380e1-278">False</span></span> |
| <span data-ttu-id="380e1-279">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-279">Position?</span></span> |<span data-ttu-id="380e1-280">o nazwie</span><span class="sxs-lookup"><span data-stu-id="380e1-280">Named</span></span> |
| <span data-ttu-id="380e1-281">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-281">Default value</span></span> |<span data-ttu-id="380e1-282">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-282">None</span></span> |
| <span data-ttu-id="380e1-283">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-283">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-284">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-285">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-285">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-286">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-286">false</span></span> |

<span data-ttu-id="380e1-287">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="380e1-288">To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="380e1-288">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="380e1-289">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-289">Inputs</span></span>
<span data-ttu-id="380e1-290">Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-290">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="380e1-291">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-291">Outputs</span></span>
<span data-ttu-id="380e1-292">Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-292">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="380e1-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="380e1-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="380e1-294">Usuwa usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="380e1-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="380e1-295">Składnia</span><span class="sxs-lookup"><span data-stu-id="380e1-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="380e1-296">Parametry</span><span class="sxs-lookup"><span data-stu-id="380e1-296">Parameters</span></span>
<span data-ttu-id="380e1-297">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-298">Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="380e1-298">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="380e1-299">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-299">Aliases</span></span> | <span data-ttu-id="380e1-300">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-301">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-301">Required?</span></span> |<span data-ttu-id="380e1-302">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-302">true</span></span> |
| <span data-ttu-id="380e1-303">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-303">Position?</span></span> |<span data-ttu-id="380e1-304">0</span><span class="sxs-lookup"><span data-stu-id="380e1-304">0</span></span> |
| <span data-ttu-id="380e1-305">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-305">Default value</span></span> |<span data-ttu-id="380e1-306">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-306">none</span></span> |
| <span data-ttu-id="380e1-307">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-307">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-308">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-309">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-309">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-310">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-310">false</span></span> |

<span data-ttu-id="380e1-311">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-312">Określa nazwę usługi multimediów hello hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-312">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="380e1-313">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-313">Aliases</span></span> | <span data-ttu-id="380e1-314">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-315">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-315">Required?</span></span> |<span data-ttu-id="380e1-316">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-316">true</span></span> |
| <span data-ttu-id="380e1-317">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-317">Position?</span></span> |<span data-ttu-id="380e1-318">2</span><span class="sxs-lookup"><span data-stu-id="380e1-318">2</span></span> |
| <span data-ttu-id="380e1-319">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-319">Default value</span></span> |<span data-ttu-id="380e1-320">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-320">None</span></span> |
| <span data-ttu-id="380e1-321">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-321">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-322">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-323">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-323">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-324">False</span><span class="sxs-lookup"><span data-stu-id="380e1-324">False</span></span> |

<span data-ttu-id="380e1-325">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="380e1-326">To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="380e1-326">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="380e1-327">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-327">Inputs</span></span>
<span data-ttu-id="380e1-328">Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-328">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="380e1-329">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-329">Outputs</span></span>
<span data-ttu-id="380e1-330">Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-330">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="380e1-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="380e1-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="380e1-332">Pobiera wszystkie usługi media services w grupie zasobów lub usług media o podanej nazwie.</span><span class="sxs-lookup"><span data-stu-id="380e1-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="380e1-333">Składnia</span><span class="sxs-lookup"><span data-stu-id="380e1-333">Syntax</span></span>
<span data-ttu-id="380e1-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="380e1-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="380e1-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="380e1-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="380e1-336">Parametry</span><span class="sxs-lookup"><span data-stu-id="380e1-336">Parameters</span></span>
<span data-ttu-id="380e1-337">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-338">Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="380e1-338">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="380e1-339">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-339">Aliases</span></span> | <span data-ttu-id="380e1-340">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-341">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-341">Required?</span></span> |<span data-ttu-id="380e1-342">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-342">true</span></span> |
| <span data-ttu-id="380e1-343">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-343">Position?</span></span> |<span data-ttu-id="380e1-344">0</span><span class="sxs-lookup"><span data-stu-id="380e1-344">0</span></span> |
| <span data-ttu-id="380e1-345">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-345">Default value</span></span> |<span data-ttu-id="380e1-346">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-346">none</span></span> |
| <span data-ttu-id="380e1-347">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-347">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-348">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-349">Nazwa zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="380e1-349">Parameter set name</span></span> |<span data-ttu-id="380e1-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="380e1-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="380e1-351">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-351">Accept wildcard characters?</span></span>   <span data-ttu-id="380e1-352">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-352">false</span></span>

<span data-ttu-id="380e1-353">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-354">Określa nazwę usługi multimediów hello hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-354">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="380e1-355">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-355">Aliases</span></span> | <span data-ttu-id="380e1-356">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-357">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-357">Required?</span></span> |<span data-ttu-id="380e1-358">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-358">true</span></span> |
| <span data-ttu-id="380e1-359">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-359">Position?</span></span> |<span data-ttu-id="380e1-360">1</span><span class="sxs-lookup"><span data-stu-id="380e1-360">1</span></span> |
| <span data-ttu-id="380e1-361">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-361">Default value</span></span> |<span data-ttu-id="380e1-362">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-362">none</span></span> |
| <span data-ttu-id="380e1-363">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-363">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-364">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-365">Nazwa zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="380e1-365">Parameter set name</span></span> |<span data-ttu-id="380e1-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="380e1-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="380e1-367">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-367">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-368">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-368">false</span></span> |

<span data-ttu-id="380e1-369">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="380e1-370">To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="380e1-370">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="380e1-371">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-371">Inputs</span></span>
<span data-ttu-id="380e1-372">Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-372">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="380e1-373">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-373">Outputs</span></span>
<span data-ttu-id="380e1-374">Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-374">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="380e1-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="380e1-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="380e1-376">Pobiera klucze usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="380e1-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="380e1-377">Składnia</span><span class="sxs-lookup"><span data-stu-id="380e1-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="380e1-378">Parametry</span><span class="sxs-lookup"><span data-stu-id="380e1-378">Parameters</span></span>
<span data-ttu-id="380e1-379">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-380">Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="380e1-380">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="380e1-381">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-381">Aliases</span></span> | <span data-ttu-id="380e1-382">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-383">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-383">Required?</span></span> |<span data-ttu-id="380e1-384">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-384">true</span></span> |
| <span data-ttu-id="380e1-385">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-385">Position?</span></span> |<span data-ttu-id="380e1-386">0</span><span class="sxs-lookup"><span data-stu-id="380e1-386">0</span></span> |
| <span data-ttu-id="380e1-387">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-387">Default value</span></span> |<span data-ttu-id="380e1-388">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-388">none</span></span> |
| <span data-ttu-id="380e1-389">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-389">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-390">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-391">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-391">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-392">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-392">false</span></span> |

<span data-ttu-id="380e1-393">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-394">Określa nazwę usługi multimediów hello hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-394">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="380e1-395">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-395">Aliases</span></span> | <span data-ttu-id="380e1-396">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-397">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-397">Required?</span></span> |<span data-ttu-id="380e1-398">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-398">true</span></span> |
| <span data-ttu-id="380e1-399">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-399">Position?</span></span> |<span data-ttu-id="380e1-400">1</span><span class="sxs-lookup"><span data-stu-id="380e1-400">1</span></span> |
| <span data-ttu-id="380e1-401">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-401">Default value</span></span> |<span data-ttu-id="380e1-402">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-402">none</span></span> |
| <span data-ttu-id="380e1-403">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-403">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-404">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-405">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-405">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-406">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-406">false</span></span> |

<span data-ttu-id="380e1-407">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="380e1-408">To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="380e1-408">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="380e1-409">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-409">Inputs</span></span>
<span data-ttu-id="380e1-410">Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-410">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="380e1-411">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-411">Outputs</span></span>
<span data-ttu-id="380e1-412">Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-412">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="380e1-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="380e1-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="380e1-414">Generuje ponownie klucz podstawowy lub pomocniczy usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="380e1-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="380e1-415">Składnia</span><span class="sxs-lookup"><span data-stu-id="380e1-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="380e1-416">Parametry</span><span class="sxs-lookup"><span data-stu-id="380e1-416">Parameters</span></span>
<span data-ttu-id="380e1-417">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-418">Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="380e1-418">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="380e1-419">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-419">Aliases</span></span> | <span data-ttu-id="380e1-420">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-421">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-421">Required?</span></span> |<span data-ttu-id="380e1-422">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-422">true</span></span> |
| <span data-ttu-id="380e1-423">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-423">Position?</span></span> |<span data-ttu-id="380e1-424">0</span><span class="sxs-lookup"><span data-stu-id="380e1-424">0</span></span> |
| <span data-ttu-id="380e1-425">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-425">Default value</span></span> |<span data-ttu-id="380e1-426">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-426">none</span></span> |
| <span data-ttu-id="380e1-427">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-427">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-428">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-429">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-429">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-430">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-430">false</span></span> |

<span data-ttu-id="380e1-431">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-432">Określa nazwę usługi multimediów hello hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-432">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="380e1-433">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-433">Aliases</span></span> | <span data-ttu-id="380e1-434">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-435">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-435">Required?</span></span> |<span data-ttu-id="380e1-436">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-436">true</span></span> |
| <span data-ttu-id="380e1-437">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-437">Position?</span></span> |<span data-ttu-id="380e1-438">1</span><span class="sxs-lookup"><span data-stu-id="380e1-438">1</span></span> |
| <span data-ttu-id="380e1-439">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-439">Default value</span></span> |<span data-ttu-id="380e1-440">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-440">none</span></span> |
| <span data-ttu-id="380e1-441">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-441">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-442">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-443">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-443">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-444">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-444">false</span></span> |

<span data-ttu-id="380e1-445">**-KeyType &lt;Właściwość KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="380e1-446">Określa typ klucza hello hello media service.</span><span class="sxs-lookup"><span data-stu-id="380e1-446">Specifies hello key type of hello media service.</span></span>

* <span data-ttu-id="380e1-447">Podstawowy lub pomocniczy</span><span class="sxs-lookup"><span data-stu-id="380e1-447">Primary or Secondary</span></span>

| <span data-ttu-id="380e1-448">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-448">Aliases</span></span> | <span data-ttu-id="380e1-449">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-450">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-450">Required?</span></span> |<span data-ttu-id="380e1-451">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-451">true</span></span> |
| <span data-ttu-id="380e1-452">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-452">Position?</span></span> |<span data-ttu-id="380e1-453">2</span><span class="sxs-lookup"><span data-stu-id="380e1-453">2</span></span> |
| <span data-ttu-id="380e1-454">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-454">Default value</span></span> |<span data-ttu-id="380e1-455">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-455">none</span></span> |
| <span data-ttu-id="380e1-456">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-456">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-457">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-457">false</span></span> |
| <span data-ttu-id="380e1-458">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-458">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-459">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-459">false</span></span> |

<span data-ttu-id="380e1-460">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="380e1-461">To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="380e1-461">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="380e1-462">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-462">Inputs</span></span>
<span data-ttu-id="380e1-463">Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toothe polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-463">hello input type is hello type of hello objects that you can pipe toothe cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="380e1-464">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-464">Outputs</span></span>
<span data-ttu-id="380e1-465">Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-465">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="380e1-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="380e1-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="380e1-467">Synchronizuje klucze konta magazynu dla konta magazynu skojarzone z usługą media hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-467">Synchronizes storage account keys for a storage account associated with hello media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="380e1-468">Składnia</span><span class="sxs-lookup"><span data-stu-id="380e1-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="380e1-469">Parametry</span><span class="sxs-lookup"><span data-stu-id="380e1-469">Parameters</span></span>
<span data-ttu-id="380e1-470">**-ResourceGroupName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-471">Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.</span><span class="sxs-lookup"><span data-stu-id="380e1-471">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="380e1-472">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-472">Aliases</span></span> | <span data-ttu-id="380e1-473">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-474">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-474">Required?</span></span> |<span data-ttu-id="380e1-475">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-475">true</span></span> |
| <span data-ttu-id="380e1-476">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-476">Position?</span></span> |<span data-ttu-id="380e1-477">0</span><span class="sxs-lookup"><span data-stu-id="380e1-477">0</span></span> |
| <span data-ttu-id="380e1-478">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-478">Default value</span></span> |<span data-ttu-id="380e1-479">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-479">none</span></span> |
| <span data-ttu-id="380e1-480">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-480">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-481">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-482">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-482">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-483">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-483">false</span></span> |

<span data-ttu-id="380e1-484">**-AccountName &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-485">Określa nazwę usługi multimediów hello hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-485">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="380e1-486">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-486">Aliases</span></span> | <span data-ttu-id="380e1-487">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-488">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-488">Required?</span></span> |<span data-ttu-id="380e1-489">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-489">true</span></span> |
| <span data-ttu-id="380e1-490">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-490">Position?</span></span> |<span data-ttu-id="380e1-491">1</span><span class="sxs-lookup"><span data-stu-id="380e1-491">1</span></span> |
| <span data-ttu-id="380e1-492">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-492">Default value</span></span> |<span data-ttu-id="380e1-493">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-493">none</span></span> |
| <span data-ttu-id="380e1-494">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-494">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-495">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-496">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-496">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-497">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-497">false</span></span> |

<span data-ttu-id="380e1-498">**-StorageAccountId &lt;ciągu&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="380e1-499">Określa konto magazynu hello skojarzonych z usługą media hello.</span><span class="sxs-lookup"><span data-stu-id="380e1-499">Specifies hello storage account associated with hello media service.</span></span>

| <span data-ttu-id="380e1-500">Aliasy</span><span class="sxs-lookup"><span data-stu-id="380e1-500">Aliases</span></span> | <span data-ttu-id="380e1-501">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="380e1-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="380e1-502">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="380e1-502">Required?</span></span> |<span data-ttu-id="380e1-503">Wartość true</span><span class="sxs-lookup"><span data-stu-id="380e1-503">true</span></span> |
| <span data-ttu-id="380e1-504">Pozycja?</span><span class="sxs-lookup"><span data-stu-id="380e1-504">Position?</span></span> |<span data-ttu-id="380e1-505">2</span><span class="sxs-lookup"><span data-stu-id="380e1-505">2</span></span> |
| <span data-ttu-id="380e1-506">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="380e1-506">Default value</span></span> |<span data-ttu-id="380e1-507">Brak</span><span class="sxs-lookup"><span data-stu-id="380e1-507">none</span></span> |
| <span data-ttu-id="380e1-508">Akceptowanie danych wejściowych potoku?</span><span class="sxs-lookup"><span data-stu-id="380e1-508">Accept pipeline input?</span></span> |<span data-ttu-id="380e1-509">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="380e1-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="380e1-510">Akceptowanie symboli wieloznacznych?</span><span class="sxs-lookup"><span data-stu-id="380e1-510">Accept wildcard characters?</span></span> |<span data-ttu-id="380e1-511">wartość false</span><span class="sxs-lookup"><span data-stu-id="380e1-511">false</span></span> |

<span data-ttu-id="380e1-512">**&lt;Właściwość CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="380e1-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="380e1-513">To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="380e1-513">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="380e1-514">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-514">Inputs</span></span>
<span data-ttu-id="380e1-515">Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-515">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="380e1-516">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="380e1-516">Outputs</span></span>
<span data-ttu-id="380e1-517">Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="380e1-517">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="380e1-518">Następny krok</span><span class="sxs-lookup"><span data-stu-id="380e1-518">Next step</span></span>
<span data-ttu-id="380e1-519">Zapoznaj się z ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="380e1-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="380e1-520">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="380e1-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

