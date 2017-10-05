---
title: "Parametry wejściowe elementu Runbook | Dokumentacja firmy Microsoft"
description: "Parametry wejściowe elementu Runbook zwiększyć elastyczność elementów runbook, umożliwiając przekazywania danych do elementu runbook, gdy jest ona uruchamiana. W tym artykule opisano różne scenariusze, w których są używane parametry wejściowe w elementach runbook."
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
ms.openlocfilehash: 1ebf32338f5242e72eb2e2daa2da50d231f4b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="28e91-104">Parametry wejściowe elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="28e91-104">Runbook input parameters</span></span>
<span data-ttu-id="28e91-105">Parametry wejściowe elementu Runbook zwiększyć elastyczność elementów runbook, umożliwiając przekazywania danych do niej po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="28e91-105">Runbook input parameters increase the flexibility of runbooks by allowing you to pass data to it when it is started.</span></span> <span data-ttu-id="28e91-106">Parametry Zezwalaj na działania elementu runbook, które można zastosować dla określonych scenariuszach i środowiskach.</span><span class="sxs-lookup"><span data-stu-id="28e91-106">The parameters allow the runbook actions to be targeted for specific scenarios and environments.</span></span> <span data-ttu-id="28e91-107">W tym artykule firma Microsoft pomoże różnych scenariuszy gdzie parametry wejściowe są używane w elementach runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="28e91-108">Skonfiguruj parametry wejściowe</span><span class="sxs-lookup"><span data-stu-id="28e91-108">Configure input parameters</span></span>
<span data-ttu-id="28e91-109">Parametry wejściowe można skonfigurować w programie PowerShell, przepływu pracy programu PowerShell i graficznych elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="28e91-110">Element runbook może mieć wiele parametrów o różnych typach danych lub Brak parametrów w ogóle.</span><span class="sxs-lookup"><span data-stu-id="28e91-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="28e91-111">Parametry wejściowe mogą być wymagane lub opcjonalne i można przypisać wartości domyślnej dla parametrów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="28e91-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="28e91-112">Po ponownym uruchomieniu za pomocą jednego z dostępnych metod, można przypisać wartości do parametrów wejściowych dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-112">You can assign values to the input parameters for a runbook when you start it through one of the available methods.</span></span> <span data-ttu-id="28e91-113">Te metody obejmują uruchamianie elementu runbook z portalu lub usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="28e91-113">These methods include starting  a runbook from the portal  or a web service.</span></span> <span data-ttu-id="28e91-114">Można również uruchomić jako podrzędnego elementu runbook, wywoływaną wbudowanego innego elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="28e91-115">Skonfiguruj parametry wejściowe w elementach runbook programu PowerShell i przepływ pracy programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="28e91-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="28e91-116">Środowiska PowerShell i [elementach runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md) automatyzacji Azure obsługuje parametry wejściowe zdefiniowane za pomocą następujących atrybutów.</span><span class="sxs-lookup"><span data-stu-id="28e91-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through the following attributes.</span></span>  

| <span data-ttu-id="28e91-117">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="28e91-117">**Property**</span></span> | <span data-ttu-id="28e91-118">**Opis**</span><span class="sxs-lookup"><span data-stu-id="28e91-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="28e91-119">Typ</span><span class="sxs-lookup"><span data-stu-id="28e91-119">Type</span></span> |<span data-ttu-id="28e91-120">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="28e91-120">Required.</span></span> <span data-ttu-id="28e91-121">Typ danych dla wartości parametru.</span><span class="sxs-lookup"><span data-stu-id="28e91-121">The data type expected for the parameter value.</span></span> <span data-ttu-id="28e91-122">Dowolny typ .NET jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="28e91-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="28e91-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="28e91-123">Name</span></span> |<span data-ttu-id="28e91-124">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="28e91-124">Required.</span></span> <span data-ttu-id="28e91-125">Nazwa parametru.</span><span class="sxs-lookup"><span data-stu-id="28e91-125">The name of the parameter.</span></span> <span data-ttu-id="28e91-126">To musi być unikatowe w obrębie elementu runbook i mogą zawierać tylko litery, cyfry lub znaki podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="28e91-126">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="28e91-127">Musi ona rozpoczynać się od litery.</span><span class="sxs-lookup"><span data-stu-id="28e91-127">It must start with a letter.</span></span> |
| <span data-ttu-id="28e91-128">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="28e91-128">Mandatory</span></span> |<span data-ttu-id="28e91-129">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="28e91-129">Optional.</span></span> <span data-ttu-id="28e91-130">Określa, czy należy podać wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="28e91-130">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="28e91-131">Jeśli ustawisz to **$true**, a następnie po uruchomieniu elementu runbook, należy podać wartość.</span><span class="sxs-lookup"><span data-stu-id="28e91-131">If you set this to **$true**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="28e91-132">Jeśli ustawisz to **$false**, a następnie wartość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="28e91-132">If you set this to **$false**, then a value is optional.</span></span> |
| <span data-ttu-id="28e91-133">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="28e91-133">Default value</span></span> |<span data-ttu-id="28e91-134">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="28e91-134">Optional.</span></span>  <span data-ttu-id="28e91-135">Określa wartość, która będzie używana dla parametru, jeśli wartość nie zostanie przekazany, po uruchomieniu elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-135">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="28e91-136">Wartość domyślna można ustawić dla każdego parametru i automatycznie wprowadzi parametr opcjonalny niezależnie od ustawienia obowiązkowe.</span><span class="sxs-lookup"><span data-stu-id="28e91-136">A default value can be set for any parameter and will automatically make the parameter optional regardless of the Mandatory setting.</span></span> |

<span data-ttu-id="28e91-137">Program Windows PowerShell obsługuje więcej atrybutów parametrów wejściowych niż wymienione w tym miejscu, takich jak sprawdzanie poprawności, aliasy i zestawy parametrów.</span><span class="sxs-lookup"><span data-stu-id="28e91-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="28e91-138">Automatyzacja Azure obsługuje obecnie tylko parametry wejściowe wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="28e91-138">However, Azure Automation currently supports only the input parameters listed above.</span></span>

<span data-ttu-id="28e91-139">Definicję parametrów w elementach runbook przepływu pracy programu PowerShell ma następujący format Ogólne, gdzie wiele parametrów są oddzielone przecinkami.</span><span class="sxs-lookup"><span data-stu-id="28e91-139">A parameter definition in PowerShell Workflow runbooks has the following general form, where multiple parameters are separated by commas.</span></span>

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
> <span data-ttu-id="28e91-140">Podczas definiowania parametrów, jeśli nie określisz **obowiązkowe** atrybutu, a następnie domyślnie parametr są traktowane jako opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="28e91-140">When you're defining parameters, if you don’t specify the **Mandatory** attribute, then by default, the parameter is considered optional.</span></span> <span data-ttu-id="28e91-141">Ponadto jeśli ustawisz wartość domyślną dla parametru w elementach runbook przepływu pracy programu PowerShell, będzie traktowane przez programu PowerShell jako opcjonalny parametr niezależnie od tego **obowiązkowe** wartość atrybutu.</span><span class="sxs-lookup"><span data-stu-id="28e91-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of the **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="28e91-142">Na przykład Skonfigurujmy parametry wejściowe elementu runbook przepływu pracy programu PowerShell, która wyświetla szczegółowe informacje o maszynach wirtualnych, jednej maszyny Wirtualnej lub wszystkich maszyn wirtualnych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="28e91-142">As an example, let’s configure the input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="28e91-143">Ten element runbook zawiera dwa parametry, jak pokazano na poniższym zrzucie ekranu: Nazwa maszyny wirtualnej i nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="28e91-143">This runbook has two parameters as shown in the following screenshot: the name of virtual machine and the name of the resource group.</span></span>

![Automatyzacja przepływu pracy programu PowerShell](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="28e91-145">W definicji tego parametru, parametry **$VMName** i **$resourceGroupName** proste parametrów typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="28e91-145">In this parameter definition, the parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="28e91-146">Jednak elementów runbook programu PowerShell i przepływ pracy programu PowerShell obsługuje wszystkie typy proste i typów złożonych, takie jak **obiektu** lub **PSCredential** dla parametrów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="28e91-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="28e91-147">Jeśli element runbook ma parametru wejściowego typu obiektu, użyj tablicy skrótów programu PowerShell z (nazwa, wartość) pary do przekazania wartości.</span><span class="sxs-lookup"><span data-stu-id="28e91-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs to pass in a value.</span></span> <span data-ttu-id="28e91-148">Na przykład, jeśli masz następującego parametru w elemencie runbook:</span><span class="sxs-lookup"><span data-stu-id="28e91-148">For example, if you have the following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="28e91-149">Następnie można przekazać następującą wartość parametru:</span><span class="sxs-lookup"><span data-stu-id="28e91-149">Then you can pass the following value to the parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="28e91-150">Skonfiguruj parametry wejściowe w graficznych elementów runbook</span><span class="sxs-lookup"><span data-stu-id="28e91-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="28e91-151">Aby [skonfigurować graficznym elementem runbook](automation-first-runbook-graphical.md) z parametrami wejściowymi, Utwórzmy graficzny element runbook, która wyświetla szczegółowe informacje o maszynach wirtualnych, albo jednej maszyny Wirtualnej lub wszystkich maszyn wirtualnych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="28e91-151">To [configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="28e91-152">Konfigurowanie elementu runbook składa się z dwóch głównych działań, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="28e91-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="28e91-153">[**Uwierzytelniania elementów Runbook za pomocą konta Uruchom jako platformy Azure** ](automation-sec-configure-azure-runas-account.md) do uwierzytelniania w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="28e91-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) to authenticate with Azure.</span></span>

<span data-ttu-id="28e91-154">[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) można pobrać właściwości maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="28e91-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) to get the properties of a virtual machines.</span></span>

<span data-ttu-id="28e91-155">Można użyć [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) działania do wyjściowego nazwy maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="28e91-155">You can use the [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity to output the names of virtual machines.</span></span> <span data-ttu-id="28e91-156">Działanie **Get-AzureRmVm** akceptuje dwa parametry **nazwę maszyny wirtualnej** i **Nazwa grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="28e91-156">The activity **Get-AzureRmVm** accepts two parameters, the **virtual machine name** and the **resource group name**.</span></span> <span data-ttu-id="28e91-157">Ponieważ te parametry można wymaga różne wartości w każdym uruchomieniu elementu runbook, można dodać parametry wejściowe do elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-157">Since these parameters could require different values each time you start the runbook, you can add input parameters to your runbook.</span></span> <span data-ttu-id="28e91-158">Poniżej przedstawiono kroki, aby dodać parametry wejściowe:</span><span class="sxs-lookup"><span data-stu-id="28e91-158">Here are the steps to add input parameters:</span></span>

1. <span data-ttu-id="28e91-159">Wybierz graficzny element runbook z **Runbook** bloku, a następnie kliknij przycisk [ **Edytuj** ](automation-graphical-authoring-intro.md) go.</span><span class="sxs-lookup"><span data-stu-id="28e91-159">Select the graphical runbook from the **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="28e91-160">W edytorze elementów runbook, kliknij polecenie **dane wejściowe i wyjściowe** otworzyć **dane wejściowe i wyjściowe** bloku.</span><span class="sxs-lookup"><span data-stu-id="28e91-160">From the runbook editor, click **Input and output** to open the **Input and output** blade.</span></span>
   
    ![Graficzny element runbook automatyzacji](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="28e91-162">**Dane wejściowe i wyjściowe** bloku zostanie wyświetlona lista parametrów wejściowych, które są zdefiniowane dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-162">The **Input and output** blade displays a list of input parameters that are defined for the runbook.</span></span> <span data-ttu-id="28e91-163">W tym bloku należy dodać nowy parametr wejściowy lub Edytuj konfigurację istniejącego parametru wejściowego.</span><span class="sxs-lookup"><span data-stu-id="28e91-163">On this blade, you can either add a new input parameter or edit the configuration of an existing input parameter.</span></span> <span data-ttu-id="28e91-164">Aby dodać nowego parametru dla elementu runbook, kliknij przycisk **dodać dane wejściowe** otworzyć **parametr wejściowy elementu Runbook** bloku.</span><span class="sxs-lookup"><span data-stu-id="28e91-164">To add a new parameter for the runbook, click **Add input** to open the **Runbook input parameter** blade.</span></span> <span data-ttu-id="28e91-165">Istnieje można skonfigurować następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="28e91-165">There, you can configure the following parameters:</span></span>
   
   | <span data-ttu-id="28e91-166">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="28e91-166">**Property**</span></span> | <span data-ttu-id="28e91-167">**Opis**</span><span class="sxs-lookup"><span data-stu-id="28e91-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="28e91-168">Nazwa</span><span class="sxs-lookup"><span data-stu-id="28e91-168">Name</span></span> |<span data-ttu-id="28e91-169">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="28e91-169">Required.</span></span>  <span data-ttu-id="28e91-170">Nazwa parametru.</span><span class="sxs-lookup"><span data-stu-id="28e91-170">The name of the parameter.</span></span> <span data-ttu-id="28e91-171">To musi być unikatowe w obrębie elementu runbook i mogą zawierać tylko litery, cyfry lub znaki podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="28e91-171">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="28e91-172">Musi ona rozpoczynać się od litery.</span><span class="sxs-lookup"><span data-stu-id="28e91-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="28e91-173">Opis</span><span class="sxs-lookup"><span data-stu-id="28e91-173">Description</span></span> |<span data-ttu-id="28e91-174">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="28e91-174">Optional.</span></span> <span data-ttu-id="28e91-175">Opis przeznaczenia parametru wejściowego.</span><span class="sxs-lookup"><span data-stu-id="28e91-175">Description about the purpose of input parameter.</span></span> |
   | <span data-ttu-id="28e91-176">Typ</span><span class="sxs-lookup"><span data-stu-id="28e91-176">Type</span></span> |<span data-ttu-id="28e91-177">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="28e91-177">Optional.</span></span> <span data-ttu-id="28e91-178">Typ danych, który jest oczekiwany dla wartości parametru.</span><span class="sxs-lookup"><span data-stu-id="28e91-178">The data type that's expected for the parameter value.</span></span> <span data-ttu-id="28e91-179">Typy parametrów obsługiwanych są **ciąg**, **Int32**, **Int64**, **dziesiętną**, **logiczna**, **DateTime**, i **obiektu**.</span><span class="sxs-lookup"><span data-stu-id="28e91-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="28e91-180">Jeśli typem danych nie jest zaznaczone, domyślnie **ciąg**.</span><span class="sxs-lookup"><span data-stu-id="28e91-180">If a data type is not selected, it defaults to **String**.</span></span> |
   | <span data-ttu-id="28e91-181">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="28e91-181">Mandatory</span></span> |<span data-ttu-id="28e91-182">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="28e91-182">Optional.</span></span> <span data-ttu-id="28e91-183">Określa, czy należy podać wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="28e91-183">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="28e91-184">Jeśli wybierzesz **tak**, a następnie po uruchomieniu elementu runbook, należy podać wartość.</span><span class="sxs-lookup"><span data-stu-id="28e91-184">If you choose **yes**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="28e91-185">Jeśli wybierzesz **nie**, a następnie wartość nie jest wymagana podczas uruchamiania elementu runbook i może zostać ustawiona wartość domyślna.</span><span class="sxs-lookup"><span data-stu-id="28e91-185">If you choose **no**, then a value is not required when the runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="28e91-186">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="28e91-186">Default Value</span></span> |<span data-ttu-id="28e91-187">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="28e91-187">Optional.</span></span> <span data-ttu-id="28e91-188">Określa wartość, która będzie używana dla parametru, jeśli wartość nie zostanie przekazany, po uruchomieniu elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-188">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="28e91-189">Można ustawić wartości domyślnej dla parametru, który nie jest obowiązkowe.</span><span class="sxs-lookup"><span data-stu-id="28e91-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="28e91-190">Aby ustawić wartość domyślną, wybierz **niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="28e91-190">To set a default value, choose **Custom**.</span></span> <span data-ttu-id="28e91-191">Ta wartość jest używana, chyba że inna wartość zostanie podana podczas uruchamiania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-191">This value is used unless another value is provided when the runbook is started.</span></span> <span data-ttu-id="28e91-192">Wybierz **Brak** , jeśli nie chcesz podać wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="28e91-192">Choose **None** if you don’t want to provide any default value.</span></span> |
   
    ![Dodaj nowe dane wejściowe](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="28e91-194">Utwórz dwa parametry o następujących właściwościach, które będą używane przez **Get AzureRmVm** działania:</span><span class="sxs-lookup"><span data-stu-id="28e91-194">Create two parameters with the following properties that will be used by the **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="28e91-195">**Parametr1:**</span><span class="sxs-lookup"><span data-stu-id="28e91-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="28e91-196">Nazwa - VMName</span><span class="sxs-lookup"><span data-stu-id="28e91-196">Name - VMName</span></span>
     * <span data-ttu-id="28e91-197">Typ — ciąg</span><span class="sxs-lookup"><span data-stu-id="28e91-197">Type - String</span></span>
     * <span data-ttu-id="28e91-198">Obowiązkowy - nr</span><span class="sxs-lookup"><span data-stu-id="28e91-198">Mandatory - No</span></span>
   * <span data-ttu-id="28e91-199">**Parameter2:**</span><span class="sxs-lookup"><span data-stu-id="28e91-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="28e91-200">Nazwa - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="28e91-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="28e91-201">Typ — ciąg</span><span class="sxs-lookup"><span data-stu-id="28e91-201">Type - String</span></span>
     * <span data-ttu-id="28e91-202">Obowiązkowy - nr</span><span class="sxs-lookup"><span data-stu-id="28e91-202">Mandatory - No</span></span>
     * <span data-ttu-id="28e91-203">Wartość domyślna — niestandardowy</span><span class="sxs-lookup"><span data-stu-id="28e91-203">Default value - Custom</span></span>
     * <span data-ttu-id="28e91-204">Wartość domyślna niestandardowe — \<nazwę grupy zasobów, która zawiera maszyny wirtualnej ></span><span class="sxs-lookup"><span data-stu-id="28e91-204">Custom default value - \<Name of the resource group that contains the virtual machines></span></span>
5. <span data-ttu-id="28e91-205">Jeśli dodasz parametry, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="28e91-205">Once you add the parameters, click **OK**.</span></span>  <span data-ttu-id="28e91-206">Możesz teraz przeglądać w **danych wejściowych i wyjściowych bloku**.</span><span class="sxs-lookup"><span data-stu-id="28e91-206">You can now view them in the **Input and output blade**.</span></span> <span data-ttu-id="28e91-207">Kliknij przycisk **OK** ponownie, a następnie kliknij przycisk **zapisać** i **publikowania** elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-to-input-parameters-in-runbooks"></a><span data-ttu-id="28e91-208">Przypisywanie wartości do parametrów w elementach runbook wejściowych</span><span class="sxs-lookup"><span data-stu-id="28e91-208">Assign values to input parameters in runbooks</span></span>
<span data-ttu-id="28e91-209">Można przekazać wartości parametrów w elementach runbook w następujących scenariuszach wejściowych.</span><span class="sxs-lookup"><span data-stu-id="28e91-209">You can pass values to input parameters in runbooks in the following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="28e91-210">Uruchom element runbook i przypisz parametrów</span><span class="sxs-lookup"><span data-stu-id="28e91-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="28e91-211">Element runbook może zostać uruchomiona na wiele sposobów: za pośrednictwem portalu Azure, z elementu webhook, polecenia cmdlet programu PowerShell, przy użyciu interfejsu API REST lub przy użyciu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="28e91-211">A runbook can be started many ways: through the Azure portal, with a webhook, with PowerShell cmdlets, with the REST API, or with the SDK.</span></span> <span data-ttu-id="28e91-212">Poniżej omówiono różne metody uruchamiania elementu runbook i przypisywanie parametrów.</span><span class="sxs-lookup"><span data-stu-id="28e91-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-the-azure-portal-and-assign-parameters"></a><span data-ttu-id="28e91-213">Uruchom opublikowanego elementu runbook za pomocą portalu Azure i parametry</span><span class="sxs-lookup"><span data-stu-id="28e91-213">Start a published runbook by using the Azure portal and assign parameters</span></span>
<span data-ttu-id="28e91-214">Gdy użytkownik [uruchamiania elementu runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), **Uruchom element Runbook** zostanie otwarty blok i można skonfigurować wartości parametrów, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="28e91-214">When you [start the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), the **Start Runbook** blade opens and you can configure values for the parameters that you just created.</span></span>

![Rozpoczynanie korzystania z portalu](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="28e91-216">Etykieta poniżej pola wejściowego zawiera atrybuty, które zostały ustawione dla parametru.</span><span class="sxs-lookup"><span data-stu-id="28e91-216">In the label beneath the input box, you can see the attributes that have been set for the parameter.</span></span> <span data-ttu-id="28e91-217">Atrybuty obejmują obowiązkowe i opcjonalne, typ i wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="28e91-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="28e91-218">W dymku pomocy obok nazwy parametru wyświetlane są wszystkie kluczowe dane potrzebne do podejmowania decyzji o wartości wejściowe parametru.</span><span class="sxs-lookup"><span data-stu-id="28e91-218">In the help balloon next to the parameter name, you can see all the key information you need to make decisions about parameter input values.</span></span> <span data-ttu-id="28e91-219">Informacje te obejmują, czy parametr jest obowiązkowy lub opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="28e91-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="28e91-220">Zawiera również typ i wartość domyślną (jeśli istnieje), a inne przydatne informacje.</span><span class="sxs-lookup"><span data-stu-id="28e91-220">It also includes the type and default value (if any), and other helpful notes.</span></span>

![Dymek pomocy](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="28e91-222">Obsługa parametrów typu String **pusty** wartości ciągu.</span><span class="sxs-lookup"><span data-stu-id="28e91-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="28e91-223">Wprowadzanie **[ciąg EmptyString]** w parametrze wejściowym pole będzie przekazać pusty ciąg do parametru.</span><span class="sxs-lookup"><span data-stu-id="28e91-223">Entering **[EmptyString]** in the input parameter box will pass an empty string to the parameter.</span></span> <span data-ttu-id="28e91-224">Ponadto nie obsługują parametrów typu ciąg **Null** wartości były przekazywane.</span><span class="sxs-lookup"><span data-stu-id="28e91-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="28e91-225">Jeśli wartości nie są przekazywane do parametru ciągu, następnie programu PowerShell zostanie zinterpretuje ją jako wartości null.</span><span class="sxs-lookup"><span data-stu-id="28e91-225">If you don’t pass any value to the String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="28e91-226">Uruchom opublikowanego elementu runbook za pomocą poleceń cmdlet programu PowerShell i parametry</span><span class="sxs-lookup"><span data-stu-id="28e91-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="28e91-227">**Polecenia cmdlet Menedżera zasobów systemu Azure:** można uruchomić element runbook usługi Automatyzacja, który został utworzony w grupie zasobów za pomocą [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="28e91-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="28e91-228">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="28e91-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="28e91-229">**Polecenia cmdlet do zarządzania usługi Azure:** można uruchomić element runbook usługi Automatyzacja, który został utworzony w domyślnej grupie zasobów za pomocą [Start AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="28e91-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="28e91-230">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="28e91-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="28e91-231">Po uruchomieniu elementu runbook za pomocą poleceń cmdlet programu PowerShell, domyślnego parametru, **MicrosoftApplicationManagementStartedBy** jest tworzony z wartością **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="28e91-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with the value **PowerShell**.</span></span> <span data-ttu-id="28e91-232">Można wyświetlić tego parametru w **szczegóły zadania** bloku.</span><span class="sxs-lookup"><span data-stu-id="28e91-232">You can view this parameter in the **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="28e91-233">Uruchom element runbook przy użyciu zestawu SDK i przypisz parametrów</span><span class="sxs-lookup"><span data-stu-id="28e91-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="28e91-234">**Metoda Menedżera zasobów Azure:** można uruchomić elementu runbook przy użyciu zestawu SDK języka programowania.</span><span class="sxs-lookup"><span data-stu-id="28e91-234">**Azure Resource Manager method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="28e91-235">Poniżej przedstawiono fragment kodu C# dla uruchamianie elementu runbook na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="28e91-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="28e91-236">Można wyświetlić wszystkie kodu w naszym [repozytorium GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="28e91-236">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
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
* <span data-ttu-id="28e91-237">**Metoda zarządzania usługami platformy Azure:** można uruchomić elementu runbook przy użyciu zestawu SDK języka programowania.</span><span class="sxs-lookup"><span data-stu-id="28e91-237">**Azure Service Management method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="28e91-238">Poniżej przedstawiono fragment kodu C# dla uruchamianie elementu runbook na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="28e91-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="28e91-239">Można wyświetlić wszystkie kodu w naszym [repozytorium GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="28e91-239">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
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
  
  <span data-ttu-id="28e91-240">Aby uruchomić tę metodę, utworzyć słownika do przechowywania parametrów elementu runbook **VMName** i **resourceGroupName**i ich wartości.</span><span class="sxs-lookup"><span data-stu-id="28e91-240">To start this method, create a dictionary to store the runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="28e91-241">Następnie można uruchomić elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-241">Then start the runbook.</span></span> <span data-ttu-id="28e91-242">Poniżej znajduje się fragment kodu C# dla wywołania metody, który jest zdefiniowany powyżej.</span><span class="sxs-lookup"><span data-stu-id="28e91-242">Below is the C# code snippet for calling the method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters to the dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call the StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-the-rest-api-and-assign-parameters"></a><span data-ttu-id="28e91-243">Uruchom element runbook za pomocą interfejsu API REST i przypisz parametrów</span><span class="sxs-lookup"><span data-stu-id="28e91-243">Start a runbook by using the REST API and assign parameters</span></span>
<span data-ttu-id="28e91-244">Zadanie elementu runbook można tworzyć i wprowadzenie do interfejsu API REST usługi Automatyzacja Azure za pomocą **PUT** metody za pomocą następującego identyfikatora URI żądania.</span><span class="sxs-lookup"><span data-stu-id="28e91-244">A runbook job can be created and started with the Azure Automation REST API by using the **PUT** method with the following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="28e91-245">W identyfikatorze URI żądania Zamień następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="28e91-245">In the request URI, replace the following parameters:</span></span>

* <span data-ttu-id="28e91-246">**Identyfikator subskrypcji:** Twojego identyfikatora subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="28e91-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="28e91-247">**Nazwa usługi chmury:** nazwę chmury usługi, do którego mają być wysyłane żądania.</span><span class="sxs-lookup"><span data-stu-id="28e91-247">**cloud-service-name:** The name of the cloud service to which the request should be sent.</span></span>  
* <span data-ttu-id="28e91-248">**Automatyzacja account-name:** nazwa konta automatyzacji hostowanej w usłudze określonej chmury.</span><span class="sxs-lookup"><span data-stu-id="28e91-248">**automation-account-name:** The name of your automation account that's hosted within the specified cloud service.</span></span>  
* <span data-ttu-id="28e91-249">**Identyfikator zadania:** identyfikatora GUID dla zadania.</span><span class="sxs-lookup"><span data-stu-id="28e91-249">**job-id:** The GUID for the job.</span></span> <span data-ttu-id="28e91-250">Identyfikatory GUID w programie PowerShell można utworzyć przy użyciu **[GUID]::NewGuid(). ToString()** polecenia.</span><span class="sxs-lookup"><span data-stu-id="28e91-250">GUIDs in PowerShell can be created by using the **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="28e91-251">W celu przekazania parametrów do zadania elementu runbook, użyj treści żądania.</span><span class="sxs-lookup"><span data-stu-id="28e91-251">In order to pass parameters to the runbook job, use the request body.</span></span> <span data-ttu-id="28e91-252">Trwa następujące dwie właściwości podany w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="28e91-252">It takes the following two properties provided in JSON format:</span></span>

* <span data-ttu-id="28e91-253">**Nazwa elementu Runbook:** wymagane.</span><span class="sxs-lookup"><span data-stu-id="28e91-253">**Runbook name:** Required.</span></span> <span data-ttu-id="28e91-254">Nazwa elementu runbook można uruchomić zadania.</span><span class="sxs-lookup"><span data-stu-id="28e91-254">The name of the runbook for the job to start.</span></span>  
* <span data-ttu-id="28e91-255">**Parametry elementu Runbook:** opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="28e91-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="28e91-256">Słownik z listą parametrów w (nazwa, wartość) formatu, gdzie nazwa powinna być typu String, a wartość może być dowolną prawidłową wartość JSON.</span><span class="sxs-lookup"><span data-stu-id="28e91-256">A dictionary of the parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="28e91-257">Jeśli chcesz uruchomić **Get-AzureVMTextual** elementu runbook, który został utworzony wcześniej **VMName** i **resourceGroupName** jako parametry, użyj następującego formatu JSON w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="28e91-257">If you want to start the **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use the following JSON format for the request body.</span></span>

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

<span data-ttu-id="28e91-258">Kod stanu HTTP 201 jest zwracany, jeśli pomyślnie utworzono zadanie.</span><span class="sxs-lookup"><span data-stu-id="28e91-258">A HTTP status code 201 is returned if the job is successfully created.</span></span> <span data-ttu-id="28e91-259">Więcej informacji o nagłówki odpowiedzi i treść odpowiedzi, można znaleźć w artykule o sposobie [utworzyć zadanie elementu runbook za pomocą interfejsu API REST.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="28e91-259">For more information on response headers and the response body, refer to the article about how to [create a runbook job by using the REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="28e91-260">Testowanie elementu runbook i przypisz parametrów</span><span class="sxs-lookup"><span data-stu-id="28e91-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="28e91-261">Gdy zostanie [przetestować wersję roboczą elementu runbook](automation-testing-runbook.md) przy użyciu opcji testu **testu** zostanie otwarty blok i można skonfigurować wartości parametrów, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="28e91-261">When you [test the draft version of your runbook](automation-testing-runbook.md) by using the test option, the **Test** blade opens and you can configure values for the parameters that you just created.</span></span>

![Testowanie i parametry](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-to-a-runbook-and-assign-parameters"></a><span data-ttu-id="28e91-263">Połącz harmonogram z elementem runbook i przypisz parametrów</span><span class="sxs-lookup"><span data-stu-id="28e91-263">Link a schedule to a runbook and assign parameters</span></span>
<span data-ttu-id="28e91-264">Możesz [Połącz harmonogram](automation-schedules.md) do elementu runbook, aby element runbook zostanie uruchomiony w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="28e91-264">You can [link a schedule](automation-schedules.md) to your runbook so that the runbook starts at a specific time.</span></span> <span data-ttu-id="28e91-265">Podczas tworzenia harmonogramu, a element runbook będzie używać tych wartości, po uruchomieniu przez harmonogram można przypisać parametrów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="28e91-265">You assign input parameters when you create the schedule, and the runbook will use these values when it is started by the schedule.</span></span> <span data-ttu-id="28e91-266">Nie można zapisać harmonogram, zanim nie zostaną dostarczone wszystkie wartości parametrów obowiązkowych.</span><span class="sxs-lookup"><span data-stu-id="28e91-266">You can’t save the schedule until all mandatory parameter values are provided.</span></span>

![Planowanie i przydzielanie parametrów](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="28e91-268">Tworzenie elementu webhook dla elementu runbook i parametry</span><span class="sxs-lookup"><span data-stu-id="28e91-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="28e91-269">Można utworzyć [webhook](automation-webhooks.md) dla elementu runbook i skonfiguruj parametry wejściowe elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="28e91-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="28e91-270">Nie można zapisać elementu webhook, zanim nie zostaną dostarczone wszystkie wartości parametrów obowiązkowych.</span><span class="sxs-lookup"><span data-stu-id="28e91-270">You can’t save the webhook until all mandatory parameter values are provided.</span></span>

![Utwórz element webhook i przypisz parametrów](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="28e91-272">Podczas wykonywania elementu runbook przy użyciu elementu webhook wstępnie zdefiniowanych parametrów wejściowych  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  jest wysyłany razem z zdefiniowanych parametrów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="28e91-272">When you execute a runbook by using a webhook, the predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with the input parameters that you defined.</span></span> <span data-ttu-id="28e91-273">Można kliknąć, aby rozwinąć **WebhookData** parametr, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="28e91-273">You can click to expand the **WebhookData** parameter for more details.</span></span>

![Parametr WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="28e91-275">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="28e91-275">Next steps</span></span>
* <span data-ttu-id="28e91-276">Aby uzyskać więcej informacji na runbook przychodzących i wychodzących, zobacz [usługi Automatyzacja Azure: element runbook danych wejściowych, wyjściowych i zagnieżdżonych elementów rrunbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span><span class="sxs-lookup"><span data-stu-id="28e91-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="28e91-277">Aby uzyskać szczegółowe informacje o różnych sposobach uruchamiania elementu runbook, zobacz [uruchamianie elementu runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="28e91-277">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="28e91-278">Aby edytować element runbook tekstową, zajrzyj do [edytowania elementów runbook tekstową](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="28e91-278">To edit a textual runbook, refer to [Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="28e91-279">Aby edytować graficznego elementu runbook, należy zapoznać się [tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="28e91-279">To edit a graphical runbook, refer to [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

