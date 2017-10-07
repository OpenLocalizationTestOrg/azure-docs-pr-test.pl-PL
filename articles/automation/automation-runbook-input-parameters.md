---
title: "Parametry wejściowe aaaRunbook | Dokumentacja firmy Microsoft"
description: "Parametry wejściowe elementu Runbook zwiększyć elastyczność hello elementów runbook, zezwalając toopass danych tooa runbook po jego uruchomieniu. W tym artykule opisano różne scenariusze, w których są używane parametry wejściowe w elementach runbook."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="cfcb6-104">Parametry wejściowe elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="cfcb6-104">Runbook input parameters</span></span>
<span data-ttu-id="cfcb6-105">Parametry wejściowe elementu Runbook zwiększyć elastyczność hello elementów runbook, zezwalając toopass tooit danych podczas jej uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-105">Runbook input parameters increase hello flexibility of runbooks by allowing you toopass data tooit when it is started.</span></span> <span data-ttu-id="cfcb6-106">Parametry Hello mogą zostać toobe działania elementu runbook hello przeznaczone dla określonych scenariuszach i środowiskach.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-106">hello parameters allow hello runbook actions toobe targeted for specific scenarios and environments.</span></span> <span data-ttu-id="cfcb6-107">W tym artykule firma Microsoft pomoże różnych scenariuszy gdzie parametry wejściowe są używane w elementach runbook.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="cfcb6-108">Skonfiguruj parametry wejściowe</span><span class="sxs-lookup"><span data-stu-id="cfcb6-108">Configure input parameters</span></span>
<span data-ttu-id="cfcb6-109">Parametry wejściowe można skonfigurować w programie PowerShell, przepływu pracy programu PowerShell i graficznych elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="cfcb6-110">Element runbook może mieć wiele parametrów o różnych typach danych lub Brak parametrów w ogóle.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="cfcb6-111">Parametry wejściowe mogą być wymagane lub opcjonalne i można przypisać wartości domyślnej dla parametrów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="cfcb6-112">Można przypisać wartości na toohello parametry wejściowe elementu runbook podczas uruchamiania za pomocą jednego z dostępnych metod hello.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-112">You can assign values toohello input parameters for a runbook when you start it through one of hello available methods.</span></span> <span data-ttu-id="cfcb6-113">Te metody obejmują uruchamianie elementu runbook z portalu hello lub usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-113">These methods include starting  a runbook from hello portal  or a web service.</span></span> <span data-ttu-id="cfcb6-114">Można również uruchomić jako podrzędnego elementu runbook, wywoływaną wbudowanego innego elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="cfcb6-115">Skonfiguruj parametry wejściowe w elementach runbook programu PowerShell i przepływ pracy programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="cfcb6-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="cfcb6-116">Środowiska PowerShell i [elementach runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md) automatyzacji Azure obsługuje parametry wejściowe zdefiniowane za pomocą hello następujące atrybuty.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through hello following attributes.</span></span>  

| <span data-ttu-id="cfcb6-117">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="cfcb6-117">**Property**</span></span> | <span data-ttu-id="cfcb6-118">**Opis**</span><span class="sxs-lookup"><span data-stu-id="cfcb6-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="cfcb6-119">Typ</span><span class="sxs-lookup"><span data-stu-id="cfcb6-119">Type</span></span> |<span data-ttu-id="cfcb6-120">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-120">Required.</span></span> <span data-ttu-id="cfcb6-121">Oczekiwano wartości parametru hello typu danych Hello.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-121">hello data type expected for hello parameter value.</span></span> <span data-ttu-id="cfcb6-122">Dowolny typ .NET jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="cfcb6-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cfcb6-123">Name</span></span> |<span data-ttu-id="cfcb6-124">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-124">Required.</span></span> <span data-ttu-id="cfcb6-125">Nazwa Hello hello parametru.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-125">hello name of hello parameter.</span></span> <span data-ttu-id="cfcb6-126">To musi być unikatowe w obrębie hello elementu runbook i może zawierać tylko litery, cyfry lub znaki podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-126">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="cfcb6-127">Musi ona rozpoczynać się od litery.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-127">It must start with a letter.</span></span> |
| <span data-ttu-id="cfcb6-128">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="cfcb6-128">Mandatory</span></span> |<span data-ttu-id="cfcb6-129">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-129">Optional.</span></span> <span data-ttu-id="cfcb6-130">Określa, czy należy podać wartość parametru hello.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-130">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="cfcb6-131">Jeśli ustawisz to zbyt**$true**, a następnie po uruchomieniu elementu runbook hello, należy podać wartość.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-131">If you set this too**$true**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="cfcb6-132">Jeśli ustawisz to zbyt**$false**, a następnie wartość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-132">If you set this too**$false**, then a value is optional.</span></span> |
| <span data-ttu-id="cfcb6-133">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="cfcb6-133">Default value</span></span> |<span data-ttu-id="cfcb6-134">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-134">Optional.</span></span>  <span data-ttu-id="cfcb6-135">Określa wartość, która będzie służyć hello parametru, jeśli wartość nie zostanie przekazany, po uruchomieniu elementu runbook hello.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-135">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="cfcb6-136">Wartość domyślna można ustawić dla każdego parametru i automatycznie wprowadzi hello parametr opcjonalny niezależnie od hello obowiązkowego ustawienia.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-136">A default value can be set for any parameter and will automatically make hello parameter optional regardless of hello Mandatory setting.</span></span> |

<span data-ttu-id="cfcb6-137">Program Windows PowerShell obsługuje więcej atrybutów parametrów wejściowych niż wymienione w tym miejscu, takich jak sprawdzanie poprawności, aliasy i zestawy parametrów.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="cfcb6-138">Automatyzacja Azure obsługuje obecnie tylko hello parametrów wejściowych wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-138">However, Azure Automation currently supports only hello input parameters listed above.</span></span>

<span data-ttu-id="cfcb6-139">Definicję parametrów w elementach runbook przepływu pracy programu PowerShell ma hello następujące ogólne formularza, gdzie wiele parametrów są oddzielone przecinkami.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-139">A parameter definition in PowerShell Workflow runbooks has hello following general form, where multiple parameters are separated by commas.</span></span>

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> <span data-ttu-id="cfcb6-140">Podczas definiowania parametrów, jeśli nie określisz hello **obowiązkowe** atrybutu, a następnie domyślnie parametr hello są traktowane jako opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-140">When you're defining parameters, if you don’t specify hello **Mandatory** attribute, then by default, hello parameter is considered optional.</span></span> <span data-ttu-id="cfcb6-141">Ponadto jeśli ustawisz wartość domyślną dla parametru w elementach runbook przepływu pracy programu PowerShell, będzie traktowane przez programu PowerShell jako opcjonalny parametr, niezależnie od hello **obowiązkowe** wartość atrybutu.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of hello **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="cfcb6-142">Na przykład Skonfigurujmy hello parametry wejściowe elementu runbook przepływu pracy programu PowerShell, która wyświetla szczegółowe informacje o maszynach wirtualnych, jednej maszyny Wirtualnej lub wszystkich maszyn wirtualnych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-142">As an example, let’s configure hello input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="cfcb6-143">Ten element runbook zawiera dwa parametry, jak pokazano w powitania po zrzut ekranu: hello nazwy maszyny wirtualnej oraz nazwy hello hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-143">This runbook has two parameters as shown in hello following screenshot: hello name of virtual machine and hello name of hello resource group.</span></span>

![Automatyzacja przepływu pracy programu PowerShell](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="cfcb6-145">W tej definicji parametru hello parametry **$VMName** i **$resourceGroupName** proste parametrów typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-145">In this parameter definition, hello parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="cfcb6-146">Jednak elementów runbook programu PowerShell i przepływ pracy programu PowerShell obsługuje wszystkie typy proste i typów złożonych, takie jak **obiektu** lub **PSCredential** dla parametrów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="cfcb6-147">Jeśli element runbook ma parametru wejściowego typu obiektu, skorzystaj z tablicy skrótów programu PowerShell z (nazwa, wartość) pary toopass wartości.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs toopass in a value.</span></span> <span data-ttu-id="cfcb6-148">Na przykład, jeśli masz hello następującego parametru w elemencie runbook:</span><span class="sxs-lookup"><span data-stu-id="cfcb6-148">For example, if you have hello following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="cfcb6-149">Następnie można przekazać następującego parametru toohello wartości hello:</span><span class="sxs-lookup"><span data-stu-id="cfcb6-149">Then you can pass hello following value toohello parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="cfcb6-150">Skonfiguruj parametry wejściowe w graficznych elementów runbook</span><span class="sxs-lookup"><span data-stu-id="cfcb6-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="cfcb6-151">zbyt[skonfigurować graficznym elementem runbook](automation-first-runbook-graphical.md) z parametrami wejściowymi, Utwórzmy graficzny element runbook, która wyświetla szczegółowe informacje o maszynach wirtualnych, albo jednej maszyny Wirtualnej lub wszystkich maszyn wirtualnych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-151">too[configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="cfcb6-152">Konfigurowanie elementu runbook składa się z dwóch głównych działań, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="cfcb6-153">[**Uwierzytelniania elementów Runbook za pomocą konta Uruchom jako platformy Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) tooauthenticate with Azure.</span></span>

<span data-ttu-id="cfcb6-154">[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello właściwości maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello properties of a virtual machines.</span></span>

<span data-ttu-id="cfcb6-155">Można użyć hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) nazwy hello toooutput działań maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-155">You can use hello [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity toooutput hello names of virtual machines.</span></span> <span data-ttu-id="cfcb6-156">Witaj działania **Get-AzureRmVm** akceptuje dwa parametry hello **nazwę maszyny wirtualnej** i hello **Nazwa grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-156">hello activity **Get-AzureRmVm** accepts two parameters, hello **virtual machine name** and hello **resource group name**.</span></span> <span data-ttu-id="cfcb6-157">Ponieważ te parametry może wymagać różnych wartości w każdym uruchomieniu elementu runbook hello, można dodać elementu runbook tooyour parametrów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-157">Since these parameters could require different values each time you start hello runbook, you can add input parameters tooyour runbook.</span></span> <span data-ttu-id="cfcb6-158">Poniżej przedstawiono parametry wejściowe tooadd hello kroki:</span><span class="sxs-lookup"><span data-stu-id="cfcb6-158">Here are hello steps tooadd input parameters:</span></span>

1. <span data-ttu-id="cfcb6-159">Wybierz hello graficzny element runbook z hello **Runbook** bloku, a następnie kliknij przycisk [ **Edytuj** ](automation-graphical-authoring-intro.md) go.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-159">Select hello graphical runbook from hello **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="cfcb6-160">W edytorze elementów runbook hello, kliknij polecenie **dane wejściowe i wyjściowe** tooopen hello **dane wejściowe i wyjściowe** bloku.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-160">From hello runbook editor, click **Input and output** tooopen hello **Input and output** blade.</span></span>
   
    ![Graficzny element runbook automatyzacji](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="cfcb6-162">Witaj **dane wejściowe i wyjściowe** bloku zostanie wyświetlona lista parametry wejściowe zdefiniowane dla hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-162">hello **Input and output** blade displays a list of input parameters that are defined for hello runbook.</span></span> <span data-ttu-id="cfcb6-163">W tym bloku możesz dodać nowego parametru wejściowego lub Edytuj konfigurację hello istniejących parametru wejściowego.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-163">On this blade, you can either add a new input parameter or edit hello configuration of an existing input parameter.</span></span> <span data-ttu-id="cfcb6-164">tooadd nowy parametr hello elementu runbook, kliknij przycisk **dodać dane wejściowe** tooopen hello **parametr wejściowy elementu Runbook** bloku.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-164">tooadd a new parameter for hello runbook, click **Add input** tooopen hello **Runbook input parameter** blade.</span></span> <span data-ttu-id="cfcb6-165">Istnieje można skonfigurować hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="cfcb6-165">There, you can configure hello following parameters:</span></span>
   
   | <span data-ttu-id="cfcb6-166">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="cfcb6-166">**Property**</span></span> | <span data-ttu-id="cfcb6-167">**Opis**</span><span class="sxs-lookup"><span data-stu-id="cfcb6-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="cfcb6-168">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cfcb6-168">Name</span></span> |<span data-ttu-id="cfcb6-169">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-169">Required.</span></span>  <span data-ttu-id="cfcb6-170">Nazwa Hello hello parametru.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-170">hello name of hello parameter.</span></span> <span data-ttu-id="cfcb6-171">To musi być unikatowe w obrębie hello elementu runbook i może zawierać tylko litery, cyfry lub znaki podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-171">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="cfcb6-172">Musi ona rozpoczynać się od litery.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="cfcb6-173">Opis</span><span class="sxs-lookup"><span data-stu-id="cfcb6-173">Description</span></span> |<span data-ttu-id="cfcb6-174">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-174">Optional.</span></span> <span data-ttu-id="cfcb6-175">Opis przeznaczenia hello parametru wejściowego.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-175">Description about hello purpose of input parameter.</span></span> |
   | <span data-ttu-id="cfcb6-176">Typ</span><span class="sxs-lookup"><span data-stu-id="cfcb6-176">Type</span></span> |<span data-ttu-id="cfcb6-177">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-177">Optional.</span></span> <span data-ttu-id="cfcb6-178">Typ danych Hello są oczekiwane w przypadku hello wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-178">hello data type that's expected for hello parameter value.</span></span> <span data-ttu-id="cfcb6-179">Typy parametrów obsługiwanych są **ciąg**, **Int32**, **Int64**, **dziesiętną**, **logiczna**, **DateTime**, i **obiektu**.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="cfcb6-180">Jeśli typem danych nie jest zaznaczone, domyślnie zbyt**ciąg**.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-180">If a data type is not selected, it defaults too**String**.</span></span> |
   | <span data-ttu-id="cfcb6-181">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="cfcb6-181">Mandatory</span></span> |<span data-ttu-id="cfcb6-182">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-182">Optional.</span></span> <span data-ttu-id="cfcb6-183">Określa, czy należy podać wartość parametru hello.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-183">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="cfcb6-184">Jeśli wybierzesz **tak**, a następnie po uruchomieniu elementu runbook hello, należy podać wartość.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-184">If you choose **yes**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="cfcb6-185">Jeśli wybierzesz **nie**, a następnie wartość nie jest wymagana, gdy element runbook hello jest uruchomiony i może zostać ustawiona wartość domyślna.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-185">If you choose **no**, then a value is not required when hello runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="cfcb6-186">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="cfcb6-186">Default Value</span></span> |<span data-ttu-id="cfcb6-187">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-187">Optional.</span></span> <span data-ttu-id="cfcb6-188">Określa wartość, która będzie służyć hello parametru, jeśli wartość nie zostanie przekazany, po uruchomieniu elementu runbook hello.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-188">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="cfcb6-189">Można ustawić wartości domyślnej dla parametru, który nie jest obowiązkowe.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="cfcb6-190">Wybierz wartość domyślną tooset **niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-190">tooset a default value, choose **Custom**.</span></span> <span data-ttu-id="cfcb6-191">Ta wartość jest używana, chyba że inna wartość zostanie podana przy uruchamianiu elementu runbook hello.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-191">This value is used unless another value is provided when hello runbook is started.</span></span> <span data-ttu-id="cfcb6-192">Wybierz **Brak** Jeśli nie chcesz tooprovide dowolną wartość domyślna.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-192">Choose **None** if you don’t want tooprovide any default value.</span></span> |
   
    ![Dodaj nowe dane wejściowe](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="cfcb6-194">Utwórz dwa parametry o następujących właściwościach, które będą używane przez hello hello **Get AzureRmVm** działania:</span><span class="sxs-lookup"><span data-stu-id="cfcb6-194">Create two parameters with hello following properties that will be used by hello **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="cfcb6-195">**Parametr1:**</span><span class="sxs-lookup"><span data-stu-id="cfcb6-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="cfcb6-196">Nazwa - VMName</span><span class="sxs-lookup"><span data-stu-id="cfcb6-196">Name - VMName</span></span>
     * <span data-ttu-id="cfcb6-197">Typ — ciąg</span><span class="sxs-lookup"><span data-stu-id="cfcb6-197">Type - String</span></span>
     * <span data-ttu-id="cfcb6-198">Obowiązkowy - nr</span><span class="sxs-lookup"><span data-stu-id="cfcb6-198">Mandatory - No</span></span>
   * <span data-ttu-id="cfcb6-199">**Parameter2:**</span><span class="sxs-lookup"><span data-stu-id="cfcb6-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="cfcb6-200">Nazwa - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="cfcb6-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="cfcb6-201">Typ — ciąg</span><span class="sxs-lookup"><span data-stu-id="cfcb6-201">Type - String</span></span>
     * <span data-ttu-id="cfcb6-202">Obowiązkowy - nr</span><span class="sxs-lookup"><span data-stu-id="cfcb6-202">Mandatory - No</span></span>
     * <span data-ttu-id="cfcb6-203">Wartość domyślna — niestandardowy</span><span class="sxs-lookup"><span data-stu-id="cfcb6-203">Default value - Custom</span></span>
     * <span data-ttu-id="cfcb6-204">Wartość domyślna niestandardowe — \<nazwę grupy zasobów hello, która zawiera maszyny wirtualne hello ></span><span class="sxs-lookup"><span data-stu-id="cfcb6-204">Custom default value - \<Name of hello resource group that contains hello virtual machines></span></span>
5. <span data-ttu-id="cfcb6-205">Po dodaniu parametry powitania kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-205">Once you add hello parameters, click **OK**.</span></span>  <span data-ttu-id="cfcb6-206">Możesz teraz przeglądać w hello **danych wejściowych i wyjściowych bloku**.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-206">You can now view them in hello **Input and output blade**.</span></span> <span data-ttu-id="cfcb6-207">Kliknij przycisk **OK** ponownie, a następnie kliknij przycisk **zapisać** i **publikowania** elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-tooinput-parameters-in-runbooks"></a><span data-ttu-id="cfcb6-208">Przypisz wartości tooinput parametrów w elementach runbook</span><span class="sxs-lookup"><span data-stu-id="cfcb6-208">Assign values tooinput parameters in runbooks</span></span>
<span data-ttu-id="cfcb6-209">Można jednak przekazać wartości tooinput parametrów w elementach runbook w hello następujące scenariusze.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-209">You can pass values tooinput parameters in runbooks in hello following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="cfcb6-210">Uruchom element runbook i przypisz parametrów</span><span class="sxs-lookup"><span data-stu-id="cfcb6-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="cfcb6-211">Element runbook może zostać uruchomiona na wiele sposobów: przez hello portalu Azure, z elementu webhook, polecenia cmdlet programu PowerShell, interfejsu API REST hello lub hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-211">A runbook can be started many ways: through hello Azure portal, with a webhook, with PowerShell cmdlets, with hello REST API, or with hello SDK.</span></span> <span data-ttu-id="cfcb6-212">Poniżej omówiono różne metody uruchamiania elementu runbook i przypisywanie parametrów.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a><span data-ttu-id="cfcb6-213">Uruchom opublikowanego elementu runbook za pomocą portalu Azure hello i parametry</span><span class="sxs-lookup"><span data-stu-id="cfcb6-213">Start a published runbook by using hello Azure portal and assign parameters</span></span>
<span data-ttu-id="cfcb6-214">Gdy zostanie [uruchomić elementu runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Uruchom element Runbook** zostanie otwarty blok i można skonfigurować wartości parametrów hello, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-214">When you [start hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Start Runbook** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Rozpoczynanie korzystania z portalu hello](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="cfcb6-216">Etykieta hello poniżej pola wejściowego hello zawiera atrybuty hello, które zostały ustawione dla parametru hello.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-216">In hello label beneath hello input box, you can see hello attributes that have been set for hello parameter.</span></span> <span data-ttu-id="cfcb6-217">Atrybuty obejmują obowiązkowe i opcjonalne, typ i wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="cfcb6-218">Witaj pomocy dymek dalej toohello nazwę parametru zawiera wszystkie informacje klucza hello potrzebne toomake decyzji o wartości wejściowe parametru.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-218">In hello help balloon next toohello parameter name, you can see all hello key information you need toomake decisions about parameter input values.</span></span> <span data-ttu-id="cfcb6-219">Informacje te obejmują, czy parametr jest obowiązkowy lub opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="cfcb6-220">Zawiera także hello typ i wartość domyślną (jeśli istnieje) i inne przydatne informacje.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-220">It also includes hello type and default value (if any), and other helpful notes.</span></span>

![Dymek pomocy](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="cfcb6-222">Obsługa parametrów typu String **pusty** wartości ciągu.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="cfcb6-223">Wprowadzanie **[ciąg EmptyString]** w parametru wejściowego hello pole zostanie przekazany parametr toohello pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-223">Entering **[EmptyString]** in hello input parameter box will pass an empty string toohello parameter.</span></span> <span data-ttu-id="cfcb6-224">Ponadto nie obsługują parametrów typu ciąg **Null** wartości były przekazywane.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="cfcb6-225">Jeśli nie zostanie przekazany żadnego parametru ciągu toohello wartość, następnie programu PowerShell zostanie zinterpretować go jako wartości null.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-225">If you don’t pass any value toohello String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="cfcb6-226">Uruchom opublikowanego elementu runbook za pomocą poleceń cmdlet programu PowerShell i parametry</span><span class="sxs-lookup"><span data-stu-id="cfcb6-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="cfcb6-227">**Polecenia cmdlet Menedżera zasobów systemu Azure:** można uruchomić element runbook usługi Automatyzacja, który został utworzony w grupie zasobów za pomocą [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfcb6-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="cfcb6-228">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="cfcb6-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="cfcb6-229">**Polecenia cmdlet do zarządzania usługi Azure:** można uruchomić element runbook usługi Automatyzacja, który został utworzony w domyślnej grupie zasobów za pomocą [Start AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfcb6-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="cfcb6-230">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="cfcb6-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="cfcb6-231">Po uruchomieniu elementu runbook za pomocą poleceń cmdlet programu PowerShell, domyślnego parametru, **MicrosoftApplicationManagementStartedBy** jest tworzony z wartością hello **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with hello value **PowerShell**.</span></span> <span data-ttu-id="cfcb6-232">Ten parametr można wyświetlić w hello **szczegóły zadania** bloku.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-232">You can view this parameter in hello **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="cfcb6-233">Uruchom element runbook przy użyciu zestawu SDK i przypisz parametrów</span><span class="sxs-lookup"><span data-stu-id="cfcb6-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="cfcb6-234">**Metoda Menedżera zasobów Azure:** można uruchomić elementu runbook za pomocą hello zestawu SDK języka programowania.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-234">**Azure Resource Manager method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="cfcb6-235">Poniżej przedstawiono fragment kodu C# dla uruchamianie elementu runbook na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="cfcb6-236">Możesz wyświetlić cały kod hello w naszym [repozytorium GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="cfcb6-236">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* <span data-ttu-id="cfcb6-237">**Metoda zarządzania usługami platformy Azure:** można uruchomić elementu runbook za pomocą hello zestawu SDK języka programowania.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-237">**Azure Service Management method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="cfcb6-238">Poniżej przedstawiono fragment kodu C# dla uruchamianie elementu runbook na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="cfcb6-239">Możesz wyświetlić cały kod hello w naszym [repozytorium GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="cfcb6-239">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  <span data-ttu-id="cfcb6-240">toostart tej metody Utwórz hello toostore słownik parametrów elementu runbook **VMName** i **resourceGroupName**i ich wartości.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-240">toostart this method, create a dictionary toostore hello runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="cfcb6-241">Następnie uruchom hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-241">Then start hello runbook.</span></span> <span data-ttu-id="cfcb6-242">Poniżej znajduje się fragment hello C# kodu dla wywołania metody hello, który jest zdefiniowany powyżej.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-242">Below is hello C# code snippet for calling hello method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a><span data-ttu-id="cfcb6-243">Uruchom element runbook za pomocą hello interfejsu API REST i przypisz parametrów</span><span class="sxs-lookup"><span data-stu-id="cfcb6-243">Start a runbook by using hello REST API and assign parameters</span></span>
<span data-ttu-id="cfcb6-244">Zadanie elementu runbook można tworzyć i pracy z hello interfejsu API REST usługi Automatyzacja Azure przy użyciu hello **PUT** metody za pomocą następującego hello żądanie identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-244">A runbook job can be created and started with hello Azure Automation REST API by using hello **PUT** method with hello following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="cfcb6-245">W identyfikatorze URI żądania hello Zastąp hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="cfcb6-245">In hello request URI, replace hello following parameters:</span></span>

* <span data-ttu-id="cfcb6-246">**Identyfikator subskrypcji:** Twojego identyfikatora subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="cfcb6-247">**Nazwa usługi chmury:** nazwa hello hello chmury usługi toowhich hello żądania, które mają być wysyłane.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-247">**cloud-service-name:** hello name of hello cloud service toowhich hello request should be sent.</span></span>  
* <span data-ttu-id="cfcb6-248">**Automatyzacja account-name:** hello nazwa konta automatyzacji, który znajduje się w obrębie hello określona usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-248">**automation-account-name:** hello name of your automation account that's hosted within hello specified cloud service.</span></span>  
* <span data-ttu-id="cfcb6-249">**Identyfikator zadania:** hello identyfikatora GUID dla hello zadania.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-249">**job-id:** hello GUID for hello job.</span></span> <span data-ttu-id="cfcb6-250">Identyfikatory GUID w programie PowerShell można utworzyć przy użyciu hello **[GUID]::NewGuid(). ToString()** polecenia.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-250">GUIDs in PowerShell can be created by using hello **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="cfcb6-251">W kolejności toopass parametry toohello runbook zadania należy użyć hello treści żądania.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-251">In order toopass parameters toohello runbook job, use hello request body.</span></span> <span data-ttu-id="cfcb6-252">Trwa hello następujące dwie właściwości podany w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="cfcb6-252">It takes hello following two properties provided in JSON format:</span></span>

* <span data-ttu-id="cfcb6-253">**Nazwa elementu Runbook:** wymagane.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-253">**Runbook name:** Required.</span></span> <span data-ttu-id="cfcb6-254">Hello nazwa elementu hello runbook hello toostart zadania.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-254">hello name of hello runbook for hello job toostart.</span></span>  
* <span data-ttu-id="cfcb6-255">**Parametry elementu Runbook:** opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="cfcb6-256">Słownik hello listy parametrów w (nazwa, wartość) formatu, gdzie nazwa powinna być typu String, a wartość może być dowolną prawidłową wartość JSON.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-256">A dictionary of hello parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="cfcb6-257">Jeśli chcesz, aby toostart hello **Get-AzureVMTextual** elementu runbook, który został utworzony wcześniej **VMName** i **resourceGroupName** jako parametry, użyj następującego formatu JSON hello Witaj treści żądania.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-257">If you want toostart hello **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use hello following JSON format for hello request body.</span></span>

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

<span data-ttu-id="cfcb6-258">Jeśli pomyślnie utworzono zadanie hello, zwracany jest kod stanu HTTP 201.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-258">A HTTP status code 201 is returned if hello job is successfully created.</span></span> <span data-ttu-id="cfcb6-259">Więcej informacji o nagłówki odpowiedzi i treść odpowiedzi hello, można znaleźć w artykule toohello temat zbyt[utworzyć zadanie elementu runbook za pomocą hello interfejsu API REST.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="cfcb6-259">For more information on response headers and hello response body, refer toohello article about how too[create a runbook job by using hello REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="cfcb6-260">Testowanie elementu runbook i przypisz parametrów</span><span class="sxs-lookup"><span data-stu-id="cfcb6-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="cfcb6-261">Gdy możesz [testu hello wersję roboczą elementu runbook](automation-testing-runbook.md) przy użyciu opcji testu hello, hello **Test** zostanie otwarty blok i można skonfigurować wartości parametrów hello, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-261">When you [test hello draft version of your runbook](automation-testing-runbook.md) by using hello test option, hello **Test** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Testowanie i parametry](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a><span data-ttu-id="cfcb6-263">Łączenie elementu runbook tooa harmonogram i parametry</span><span class="sxs-lookup"><span data-stu-id="cfcb6-263">Link a schedule tooa runbook and assign parameters</span></span>
<span data-ttu-id="cfcb6-264">Możesz [Połącz harmonogram](automation-schedules.md) runbook tooyour tak hello elementu runbook rozpoczyna się w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-264">You can [link a schedule](automation-schedules.md) tooyour runbook so that hello runbook starts at a specific time.</span></span> <span data-ttu-id="cfcb6-265">Po utworzeniu harmonogramu hello i hello runbook użyje tych wartości, gdy jest ona uruchamiana zgodnie z harmonogramem hello przypisaniu parametrów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-265">You assign input parameters when you create hello schedule, and hello runbook will use these values when it is started by hello schedule.</span></span> <span data-ttu-id="cfcb6-266">Nie można zapisać harmonogramu hello, zanim nie zostaną dostarczone wszystkie wartości parametrów obowiązkowych.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-266">You can’t save hello schedule until all mandatory parameter values are provided.</span></span>

![Planowanie i przydzielanie parametrów](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="cfcb6-268">Tworzenie elementu webhook dla elementu runbook i parametry</span><span class="sxs-lookup"><span data-stu-id="cfcb6-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="cfcb6-269">Można utworzyć [webhook](automation-webhooks.md) dla elementu runbook i skonfiguruj parametry wejściowe elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="cfcb6-270">Nie można zapisać elementu webhook hello, zanim nie zostaną dostarczone wszystkie wartości parametrów obowiązkowych.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-270">You can’t save hello webhook until all mandatory parameter values are provided.</span></span>

![Utwórz element webhook i przypisz parametrów](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="cfcb6-272">Podczas wykonywania elementu runbook przy użyciu elementu webhook, hello wstępnie zdefiniowanych parametrów wejściowych  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  jest wysyłany razem z hello parametry wejściowe zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-272">When you execute a runbook by using a webhook, hello predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with hello input parameters that you defined.</span></span> <span data-ttu-id="cfcb6-273">Możesz kliknąć tooexpand hello **WebhookData** parametr, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="cfcb6-273">You can click tooexpand hello **WebhookData** parameter for more details.</span></span>

![Parametr WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="cfcb6-275">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cfcb6-275">Next steps</span></span>
* <span data-ttu-id="cfcb6-276">Aby uzyskać więcej informacji na runbook przychodzących i wychodzących, zobacz [usługi Automatyzacja Azure: element runbook danych wejściowych, wyjściowych i zagnieżdżonych elementów rrunbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span><span class="sxs-lookup"><span data-stu-id="cfcb6-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="cfcb6-277">Aby uzyskać więcej informacji o różnych sposobów toostart elementu runbook, zobacz [uruchamianie elementu runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="cfcb6-277">For details about different ways toostart a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="cfcb6-278">tooedit tekstowa elementu runbook, można znaleźć zbyt[edytowania elementów runbook tekstową](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="cfcb6-278">tooedit a textual runbook, refer too[Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="cfcb6-279">tooedit graficznym elementem runbook można znaleźć zbyt[tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="cfcb6-279">tooedit a graphical runbook, refer too[Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

