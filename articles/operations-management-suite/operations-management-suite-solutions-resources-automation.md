---
title: "aaaAzure automatyzacji zasobów w rozwiązaniach pakietu OMS | Dokumentacja firmy Microsoft"
description: "Rozwiązania w OMS zazwyczaj uwzględnia elementów runbook w automatyzacji Azure tooautomate procesy, takie jak zbierania i przetwarzania danych monitorowania.  W tym artykule opisano sposób tooinclude elementów runbook i ich powiązane zasoby w rozwiązaniu."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a><span data-ttu-id="eebf5-104">Dodawanie usługi Automatyzacja Azure zasobów tooan OMS rozwiązania do zarządzania (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="eebf5-104">Adding Azure Automation resources tooan OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="eebf5-105">To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="eebf5-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="eebf5-106">Żadnego schematu opisanych poniżej jest toochange podmiotu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-106">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="eebf5-107">[Rozwiązania do zarządzania w OMS](operations-management-suite-solutions.md) zazwyczaj uwzględnia elementów runbook w automatyzacji Azure tooautomate procesy, takie jak zbierania i przetwarzania danych monitorowania.</span><span class="sxs-lookup"><span data-stu-id="eebf5-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation tooautomate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="eebf5-108">Ponadto toorunbooks, kont automatyzacji zawiera zasoby, takie jak zmienne i harmonogramy obsługuje hello elementów runbook używane w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-108">In addition toorunbooks, Automation accounts includes assets such as variables and schedules that support hello runbooks used in hello solution.</span></span>  <span data-ttu-id="eebf5-109">W tym artykule opisano sposób tooinclude elementów runbook i ich powiązane zasoby w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-109">This article describes how tooinclude runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="eebf5-110">cześć przykłady w tym artykule Użyj parametry i zmienne, które są albo toomanagement wymagane lub typowych rozwiązań i opisane w [tworzenia rozwiązań do zarządzania w Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="eebf5-110">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="eebf5-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eebf5-111">Prerequisites</span></span>
<span data-ttu-id="eebf5-112">W tym artykule przyjęto założenie, że znasz już hello następujących informacji.</span><span class="sxs-lookup"><span data-stu-id="eebf5-112">This article assumes that you're already familiar with hello following information.</span></span>

- <span data-ttu-id="eebf5-113">Jak zbyt[tworzenie rozwiązania do zarządzania](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="eebf5-113">How too[create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="eebf5-114">Witaj struktury [plik rozwiązania](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="eebf5-114">hello structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="eebf5-115">Jak zbyt[Tworzenie szablonów usługi Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="eebf5-115">How too[author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="eebf5-116">Konto usługi Automation</span><span class="sxs-lookup"><span data-stu-id="eebf5-116">Automation account</span></span>
<span data-ttu-id="eebf5-117">Wszystkie zasoby w automatyzacji Azure są zawarte w [konto automatyzacji](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="eebf5-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="eebf5-118">Zgodnie z opisem w [OMS obszaru roboczego i konto automatyzacji](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello konta automatyzacji nie jest zawarty w rozwiązaniu do zarządzania hello, ale musi istnieć przed zainstalowaniem hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="eebf5-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Automation account isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="eebf5-119">Jeśli nie jest dostępna, następnie hello rozwiązania instalacja zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="eebf5-119">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="eebf5-120">Nazwa Hello każdego zasobu automatyzacji zawiera nazwę hello jego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="eebf5-120">hello name of each Automation resource includes hello name of its Automation account.</span></span>  <span data-ttu-id="eebf5-121">Odbywa się w rozwiązaniu hello hello **accountName** parametru jak hello poniższy przykład zasobu elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-121">This is done in hello solution with hello **accountName** parameter as in hello following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="eebf5-122">Elementy Runbook</span><span class="sxs-lookup"><span data-stu-id="eebf5-122">Runbooks</span></span>
<span data-ttu-id="eebf5-123">Należy uwzględnić wszystkie elementy runbook używana przez rozwiązania hello w pliku rozwiązania hello, dzięki czemu są tworzone po zainstalowaniu hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="eebf5-123">You should include any runbooks used by hello solution in hello solution file so that they're created when hello solution is installed.</span></span>  <span data-ttu-id="eebf5-124">Hello treści elementu runbook hello hello szablonu nie może zawierać jednak, należy opublikować hello runbook tooa lokalizacji publicznej gdzie jest dostępny przez dowolnego użytkownika instalowanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="eebf5-124">You cannot contain hello body of hello runbook in hello template though, so you should publish hello runbook tooa public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="eebf5-125">[Element runbook automatyzacji Azure](../automation/automation-runbook-types.md) zasoby mają typ **Microsoft.Automation/automationAccounts/runbooks** i mieć hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="eebf5-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have hello following structure.</span></span> <span data-ttu-id="eebf5-126">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


<span data-ttu-id="eebf5-127">w hello w poniższej tabeli opisano Hello właściwości dla elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-127">hello properties for runbooks are described in hello following table.</span></span>

| <span data-ttu-id="eebf5-128">Właściwość</span><span class="sxs-lookup"><span data-stu-id="eebf5-128">Property</span></span> | <span data-ttu-id="eebf5-129">Opis</span><span class="sxs-lookup"><span data-stu-id="eebf5-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eebf5-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="eebf5-130">runbookType</span></span> |<span data-ttu-id="eebf5-131">Określa typy hello hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-131">Specifies hello types of hello runbook.</span></span> <br><br> <span data-ttu-id="eebf5-132">Skrypt — skrypt programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="eebf5-132">Script - PowerShell script</span></span> <br><span data-ttu-id="eebf5-133">PowerShell — przepływ pracy programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="eebf5-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="eebf5-134">GraphPowerShell - runbook skryptu PowerShell graficznego</span><span class="sxs-lookup"><span data-stu-id="eebf5-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="eebf5-135">GraphPowerShellWorkflow - PowerShell graficzny element runbook przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="eebf5-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="eebf5-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="eebf5-136">logProgress</span></span> |<span data-ttu-id="eebf5-137">Określa, czy [rekordy postępu](../automation/automation-runbook-output-and-messages.md) ma być generowany dla hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="eebf5-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="eebf5-138">logVerbose</span></span> |<span data-ttu-id="eebf5-139">Określa, czy [rekordów pełnych](../automation/automation-runbook-output-and-messages.md) ma być generowany dla hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="eebf5-140">description</span><span class="sxs-lookup"><span data-stu-id="eebf5-140">description</span></span> |<span data-ttu-id="eebf5-141">Opcjonalny opis hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-141">Optional description for hello runbook.</span></span> |
| <span data-ttu-id="eebf5-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="eebf5-142">publishContentLink</span></span> |<span data-ttu-id="eebf5-143">Określa hello zawartość elementu hello runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-143">Specifies hello content of hello runbook.</span></span> <br><br><span data-ttu-id="eebf5-144">Identyfikator URI - Uri toohello zawartość elementu hello runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-144">uri - Uri toohello content of hello runbook.</span></span>  <span data-ttu-id="eebf5-145">Są to plik .ps1 dla elementów runbook programu PowerShell i skryptów, a plik wyeksportowany element runbook graficzny element runbook wykresu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="eebf5-146">Wersja — wersji elementu runbook hello własne śledzenia.</span><span class="sxs-lookup"><span data-stu-id="eebf5-146">version - Version of hello runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="eebf5-147">Automatyzacja zadań</span><span class="sxs-lookup"><span data-stu-id="eebf5-147">Automation jobs</span></span>
<span data-ttu-id="eebf5-148">Po uruchomieniu elementu runbook w automatyzacji Azure tworzy zadanie usługi Automatyzacja.</span><span class="sxs-lookup"><span data-stu-id="eebf5-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="eebf5-149">Możesz dodać automatyzacji zadań zasobów tooyour rozwiązania tooautomatically start element runbook po zainstalowaniu hello rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="eebf5-149">You can add an automation job resource tooyour solution tooautomatically start a runbook when hello management solution is installed.</span></span>  <span data-ttu-id="eebf5-150">Ta metoda jest najczęściej używanymi toostart elementy runbook, które służą do konfiguracji początkowej hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="eebf5-150">This method is typically used toostart runbooks that are used for initial configuration of hello solution.</span></span>  <span data-ttu-id="eebf5-151">Utwórz toostart elementu runbook w regularnych odstępach czasu, [harmonogram](#schedules) i [harmonogram zadań](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="eebf5-151">toostart a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="eebf5-152">Zasoby zadanie ma typ **Microsoft.Automation/automationAccounts/jobs** i mieć hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="eebf5-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have hello following structure.</span></span>  <span data-ttu-id="eebf5-153">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

<span data-ttu-id="eebf5-154">w hello w poniższej tabeli opisano właściwości Hello automatyzacji zadań.</span><span class="sxs-lookup"><span data-stu-id="eebf5-154">hello properties for automation jobs are described in hello following table.</span></span>

| <span data-ttu-id="eebf5-155">Właściwość</span><span class="sxs-lookup"><span data-stu-id="eebf5-155">Property</span></span> | <span data-ttu-id="eebf5-156">Opis</span><span class="sxs-lookup"><span data-stu-id="eebf5-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eebf5-157">Element runbook</span><span class="sxs-lookup"><span data-stu-id="eebf5-157">runbook</span></span> |<span data-ttu-id="eebf5-158">Jedna nazwa jednostki o nazwie hello hello toostart elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-158">Single name entity with hello name of hello runbook toostart.</span></span> |
| <span data-ttu-id="eebf5-159">parameters</span><span class="sxs-lookup"><span data-stu-id="eebf5-159">parameters</span></span> |<span data-ttu-id="eebf5-160">Jednostki dla każdej wartości parametru wymagane przez element runbook hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-160">Entity for each parameter value required by hello runbook.</span></span> |

<span data-ttu-id="eebf5-161">Witaj zadania obejmują hello nazwy elementu runbook i wszelkie toobe wartości parametru wysyłane toohello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-161">hello job includes hello runbook name and any parameter values toobe sent toohello runbook.</span></span>  <span data-ttu-id="eebf5-162">zadanie Hello powinien [są zależne od](operations-management-suite-solutions-solution-file.md#resources) hello elementu runbook, który jest uruchamiany od elementu runbook hello musi zostać utworzone przed hello zadania.</span><span class="sxs-lookup"><span data-stu-id="eebf5-162">hello job should [depend on](operations-management-suite-solutions-solution-file.md#resources) hello runbook that it's starting since hello runbook must be created before hello job.</span></span>  <span data-ttu-id="eebf5-163">Jeśli masz wiele elementów runbook, który ma być uruchamiany przez zadanie, które są zależne od innych zadań, które powinny być uruchamiane w pierwszy można zdefiniować ich kolejność.</span><span class="sxs-lookup"><span data-stu-id="eebf5-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="eebf5-164">Nazwa zasobu zadania Hello musi zawierać identyfikator GUID, który zazwyczaj jest przypisywany przez parametr.</span><span class="sxs-lookup"><span data-stu-id="eebf5-164">hello name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="eebf5-165">Więcej o parametrach identyfikatora GUID w [tworzenie rozwiązań w Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="eebf5-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="eebf5-166">Certyfikaty</span><span class="sxs-lookup"><span data-stu-id="eebf5-166">Certificates</span></span>
<span data-ttu-id="eebf5-167">[Certyfikaty automatyzacji Azure](../automation/automation-certificates.md) typu **Microsoft.Automation/automationAccounts/certificates** i mieć hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="eebf5-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have hello following structure.</span></span> <span data-ttu-id="eebf5-168">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



<span data-ttu-id="eebf5-169">w hello w poniższej tabeli opisano Hello właściwości zasobów certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="eebf5-169">hello properties for Certificates resources are described in hello following table.</span></span>

| <span data-ttu-id="eebf5-170">Właściwość</span><span class="sxs-lookup"><span data-stu-id="eebf5-170">Property</span></span> | <span data-ttu-id="eebf5-171">Opis</span><span class="sxs-lookup"><span data-stu-id="eebf5-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eebf5-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="eebf5-172">base64Value</span></span> |<span data-ttu-id="eebf5-173">Wartość Base-64 hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-173">Base 64 value for hello certificate.</span></span> |
| <span data-ttu-id="eebf5-174">Odcisk palca</span><span class="sxs-lookup"><span data-stu-id="eebf5-174">thumbprint</span></span> |<span data-ttu-id="eebf5-175">Odcisk palca certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-175">Thumbprint for hello certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="eebf5-176">Poświadczenia</span><span class="sxs-lookup"><span data-stu-id="eebf5-176">Credentials</span></span>
<span data-ttu-id="eebf5-177">[Poświadczenia usługi Automatyzacja Azure](../automation/automation-credentials.md) typu **Microsoft.Automation/automationAccounts/credentials** i mieć hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="eebf5-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have hello following structure.</span></span>  <span data-ttu-id="eebf5-178">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

<span data-ttu-id="eebf5-179">w hello w poniższej tabeli opisano Hello właściwości zasobów poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="eebf5-179">hello properties for Credential resources are described in hello following table.</span></span>

| <span data-ttu-id="eebf5-180">Właściwość</span><span class="sxs-lookup"><span data-stu-id="eebf5-180">Property</span></span> | <span data-ttu-id="eebf5-181">Opis</span><span class="sxs-lookup"><span data-stu-id="eebf5-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eebf5-182">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="eebf5-182">userName</span></span> |<span data-ttu-id="eebf5-183">Nazwa użytkownika dla hello poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="eebf5-183">User name for hello credential.</span></span> |
| <span data-ttu-id="eebf5-184">hasło</span><span class="sxs-lookup"><span data-stu-id="eebf5-184">password</span></span> |<span data-ttu-id="eebf5-185">Hasło dla poświadczeń hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-185">Password for hello credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="eebf5-186">Harmonogramy</span><span class="sxs-lookup"><span data-stu-id="eebf5-186">Schedules</span></span>
<span data-ttu-id="eebf5-187">[Harmonogramy automatyzacji Azure](../automation/automation-schedules.md) typu **Microsoft.Automation/automationAccounts/schedules** i mieć hello hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="eebf5-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have hello hello following structure.</span></span> <span data-ttu-id="eebf5-188">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

<span data-ttu-id="eebf5-189">w hello w poniższej tabeli opisano Hello właściwości harmonogramu zasobów.</span><span class="sxs-lookup"><span data-stu-id="eebf5-189">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="eebf5-190">Właściwość</span><span class="sxs-lookup"><span data-stu-id="eebf5-190">Property</span></span> | <span data-ttu-id="eebf5-191">Opis</span><span class="sxs-lookup"><span data-stu-id="eebf5-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eebf5-192">description</span><span class="sxs-lookup"><span data-stu-id="eebf5-192">description</span></span> |<span data-ttu-id="eebf5-193">Opcjonalny opis hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-193">Optional description for hello schedule.</span></span> |
| <span data-ttu-id="eebf5-194">startTime</span><span class="sxs-lookup"><span data-stu-id="eebf5-194">startTime</span></span> |<span data-ttu-id="eebf5-195">Określa czas rozpoczęcia harmonogramu hello jako obiekt typu DateTime.</span><span class="sxs-lookup"><span data-stu-id="eebf5-195">Specifies hello start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="eebf5-196">Jeśli może zostać przekonwertowany tooa można podać ciąg prawidłowy element DateTime.</span><span class="sxs-lookup"><span data-stu-id="eebf5-196">A string can be provided if it can be converted tooa valid DateTime.</span></span> |
| <span data-ttu-id="eebf5-197">IsEnabled</span><span class="sxs-lookup"><span data-stu-id="eebf5-197">isEnabled</span></span> |<span data-ttu-id="eebf5-198">Określa, czy harmonogram hello jest włączone.</span><span class="sxs-lookup"><span data-stu-id="eebf5-198">Specifies whether hello schedule is enabled.</span></span> |
| <span data-ttu-id="eebf5-199">interval</span><span class="sxs-lookup"><span data-stu-id="eebf5-199">interval</span></span> |<span data-ttu-id="eebf5-200">Typ Hello Interwał harmonogramu hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-200">hello type of interval for hello schedule.</span></span><br><br><span data-ttu-id="eebf5-201">dzień</span><span class="sxs-lookup"><span data-stu-id="eebf5-201">day</span></span><br><span data-ttu-id="eebf5-202">godz.</span><span class="sxs-lookup"><span data-stu-id="eebf5-202">hour</span></span> |
| <span data-ttu-id="eebf5-203">frequency</span><span class="sxs-lookup"><span data-stu-id="eebf5-203">frequency</span></span> |<span data-ttu-id="eebf5-204">Witaj harmonogram częstotliwości powinna wyzwalać w liczbie dni lub godzin.</span><span class="sxs-lookup"><span data-stu-id="eebf5-204">Frequency that hello schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="eebf5-205">Harmonogramy musi mieć godzinę rozpoczęcia o wartości większej niż hello bieżącego czasu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-205">Schedules must have a start time with a value greater than hello current time.</span></span>  <span data-ttu-id="eebf5-206">Nie można podać tę wartość za pomocą zmiennych, ponieważ czy nie ma możliwości wiedzy, gdy jest zainstalowany toobe będzie.</span><span class="sxs-lookup"><span data-stu-id="eebf5-206">You cannot provide this value with a variable since you would have no way of knowing when it's going toobe installed.</span></span>

<span data-ttu-id="eebf5-207">Użyj jednej z powitania po dwóch strategii, korzystając z harmonogramu zasobów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-207">Use one of hello following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="eebf5-208">Użyj parametru hello czas rozpoczęcia harmonogramu hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-208">Use a parameter for hello start time of hello schedule.</span></span>  <span data-ttu-id="eebf5-209">Monit hello użytkownika tooprovide wartość przy instalacji hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="eebf5-209">This will prompt hello user tooprovide a value when they install hello solution.</span></span>  <span data-ttu-id="eebf5-210">Jeśli masz wiele harmonogramów można używać wartości jeden parametr dla więcej niż jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="eebf5-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="eebf5-211">Utwórz harmonogramy hello przy użyciu elementu runbook, który rozpoczyna się, gdy rozwiązanie hello jest zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="eebf5-211">Create hello schedules using a runbook that starts when hello solution is installed.</span></span>  <span data-ttu-id="eebf5-212">Spowoduje to usunięcie hello wymaganie toospecify użytkownika hello raz, ale nie może zawierać harmonogram hello w rozwiązaniu, dlatego zostanie usunięta po usunięciu hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="eebf5-212">This removes hello requirement of hello user toospecify a time, but you can't contain hello schedule in your solution so it will be removed when hello solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="eebf5-213">Harmonogramy zadań</span><span class="sxs-lookup"><span data-stu-id="eebf5-213">Job schedules</span></span>
<span data-ttu-id="eebf5-214">Zadania planowania zasobów powiązania elementu runbook z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="eebf5-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="eebf5-215">Mają one typu **Microsoft.Automation/automationAccounts/jobSchedules** i mieć hello hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="eebf5-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have hello hello following structure.</span></span>  <span data-ttu-id="eebf5-216">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


<span data-ttu-id="eebf5-217">w hello w poniższej tabeli opisano właściwości Hello harmonogramy zadań.</span><span class="sxs-lookup"><span data-stu-id="eebf5-217">hello properties for job schedules are described in hello following table.</span></span>

| <span data-ttu-id="eebf5-218">Właściwość</span><span class="sxs-lookup"><span data-stu-id="eebf5-218">Property</span></span> | <span data-ttu-id="eebf5-219">Opis</span><span class="sxs-lookup"><span data-stu-id="eebf5-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eebf5-220">Nazwa harmonogramu</span><span class="sxs-lookup"><span data-stu-id="eebf5-220">schedule name</span></span> |<span data-ttu-id="eebf5-221">Pojedynczy **nazwa** jednostki o nazwie hello hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-221">Single **name** entity with hello name of hello schedule.</span></span> |
| <span data-ttu-id="eebf5-222">Nazwa elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="eebf5-222">runbook name</span></span>  |<span data-ttu-id="eebf5-223">Pojedynczy **nazwa** jednostki o nazwie hello hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-223">Single **name** entity with hello name of hello runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="eebf5-224">Zmienne</span><span class="sxs-lookup"><span data-stu-id="eebf5-224">Variables</span></span>
<span data-ttu-id="eebf5-225">[Zmienne automatyzacji Azure](../automation/automation-variables.md) typu **Microsoft.Automation/automationAccounts/variables** i mieć hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="eebf5-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have hello following structure.</span></span>  <span data-ttu-id="eebf5-226">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

<span data-ttu-id="eebf5-227">w hello w poniższej tabeli opisano Hello właściwości zasobów zmiennej.</span><span class="sxs-lookup"><span data-stu-id="eebf5-227">hello properties for variable resources are described in hello following table.</span></span>

| <span data-ttu-id="eebf5-228">Właściwość</span><span class="sxs-lookup"><span data-stu-id="eebf5-228">Property</span></span> | <span data-ttu-id="eebf5-229">Opis</span><span class="sxs-lookup"><span data-stu-id="eebf5-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eebf5-230">description</span><span class="sxs-lookup"><span data-stu-id="eebf5-230">description</span></span> | <span data-ttu-id="eebf5-231">Opcjonalny opis hello zmiennej.</span><span class="sxs-lookup"><span data-stu-id="eebf5-231">Optional description for hello variable.</span></span> |
| <span data-ttu-id="eebf5-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="eebf5-232">isEncrypted</span></span> | <span data-ttu-id="eebf5-233">Określa, czy ma być szyfrowana zmienna hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-233">Specifies whether hello variable should be encrypted.</span></span> |
| <span data-ttu-id="eebf5-234">type</span><span class="sxs-lookup"><span data-stu-id="eebf5-234">type</span></span> | <span data-ttu-id="eebf5-235">Ta właściwość obecnie nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="eebf5-235">This property currently has no effect.</span></span>  <span data-ttu-id="eebf5-236">Typ danych zmiennej hello Hello będzie określana przez wartość początkowa hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-236">hello data type of hello variable will be determined by hello initial value.</span></span> |
| <span data-ttu-id="eebf5-237">wartość</span><span class="sxs-lookup"><span data-stu-id="eebf5-237">value</span></span> | <span data-ttu-id="eebf5-238">Wartość zmiennej hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-238">Value for hello variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="eebf5-239">Witaj **typu** właściwości obecnie nie ma wpływu na powitania zmiennej tworzona.</span><span class="sxs-lookup"><span data-stu-id="eebf5-239">hello **type** property currently has no effect on hello variable being created.</span></span>  <span data-ttu-id="eebf5-240">Typ danych zmiennej hello Hello będzie określana przez wartość hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-240">hello data type for hello variable will be determined by hello value.</span></span>  

<span data-ttu-id="eebf5-241">Jeśli ustawisz hello początkowej wartości zmiennej hello musi być skonfigurowany jako hello prawidłowy typ danych.</span><span class="sxs-lookup"><span data-stu-id="eebf5-241">If you set hello initial value for hello variable, it must be configured as hello correct data type.</span></span>  <span data-ttu-id="eebf5-242">Witaj w poniższej tabeli zawiera hello różne typy danych dopuszczalny i ich składni.</span><span class="sxs-lookup"><span data-stu-id="eebf5-242">hello following table provides hello different data types allowable and their syntax.</span></span>  <span data-ttu-id="eebf5-243">Należy pamiętać, że wartości w formacie JSON są oczekiwane tooalways być ujęte w cudzysłów z znaków specjalnych w cudzysłowy hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-243">Note that values in JSON are expected tooalways be enclosed in quotes with any special characters within hello quotes.</span></span>  <span data-ttu-id="eebf5-244">Na przykład wartość ciągu zostałaby określona przez stawiać cudzysłów wokół ciąg hello (przy użyciu znaku ucieczki hello (\\)) podczas zostałaby określona wartość liczbową z jednego zestawu znaków cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-244">For example, a string value would be specified by quotes around hello string (using hello escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="eebf5-245">Typ danych</span><span class="sxs-lookup"><span data-stu-id="eebf5-245">Data type</span></span> | <span data-ttu-id="eebf5-246">Opis</span><span class="sxs-lookup"><span data-stu-id="eebf5-246">Description</span></span> | <span data-ttu-id="eebf5-247">Przykład</span><span class="sxs-lookup"><span data-stu-id="eebf5-247">Example</span></span> | <span data-ttu-id="eebf5-248">Usuwa zbyt</span><span class="sxs-lookup"><span data-stu-id="eebf5-248">Resolves too</span></span>|
|:--|:--|:--|:--|
| <span data-ttu-id="eebf5-249">Ciąg</span><span class="sxs-lookup"><span data-stu-id="eebf5-249">string</span></span>   | <span data-ttu-id="eebf5-250">Wartość należy ująć w cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="eebf5-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="eebf5-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="eebf5-251">"\"Hello world\""</span></span> | <span data-ttu-id="eebf5-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="eebf5-252">"Hello world"</span></span> |
| <span data-ttu-id="eebf5-253">numeryczne</span><span class="sxs-lookup"><span data-stu-id="eebf5-253">numeric</span></span>  | <span data-ttu-id="eebf5-254">Wartość liczbowa z apostrofy.</span><span class="sxs-lookup"><span data-stu-id="eebf5-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="eebf5-255">"64"</span><span class="sxs-lookup"><span data-stu-id="eebf5-255">"64"</span></span> | <span data-ttu-id="eebf5-256">64</span><span class="sxs-lookup"><span data-stu-id="eebf5-256">64</span></span> |
| <span data-ttu-id="eebf5-257">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="eebf5-257">boolean</span></span>  | <span data-ttu-id="eebf5-258">**wartość true,** lub **false** w cudzysłowy.</span><span class="sxs-lookup"><span data-stu-id="eebf5-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="eebf5-259">Należy pamiętać, że ta wartość musi być litera.</span><span class="sxs-lookup"><span data-stu-id="eebf5-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="eebf5-260">wartość "prawda"</span><span class="sxs-lookup"><span data-stu-id="eebf5-260">"true"</span></span> | <span data-ttu-id="eebf5-261">Wartość true</span><span class="sxs-lookup"><span data-stu-id="eebf5-261">true</span></span> |
| <span data-ttu-id="eebf5-262">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="eebf5-262">datetime</span></span> | <span data-ttu-id="eebf5-263">Serializacji wartości typu date.</span><span class="sxs-lookup"><span data-stu-id="eebf5-263">Serialized date value.</span></span><br><span data-ttu-id="eebf5-264">Tej wartości można użyć polecenia cmdlet ConvertTo-Json hello w toogenerate środowiska PowerShell dla określonej daty.</span><span class="sxs-lookup"><span data-stu-id="eebf5-264">You can use hello ConvertTo-Json cmdlet in PowerShell toogenerate this value for a particular date.</span></span><br><span data-ttu-id="eebf5-265">Przykład: get data "2017-5/24 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="eebf5-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="eebf5-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="eebf5-266">ConvertTo-Json</span></span> | <span data-ttu-id="eebf5-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="eebf5-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="eebf5-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="eebf5-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="eebf5-269">Moduły</span><span class="sxs-lookup"><span data-stu-id="eebf5-269">Modules</span></span>
<span data-ttu-id="eebf5-270">Rozwiązania do zarządzania nie jest konieczne toodefine [modułów globalnych](../automation/automation-integration-modules.md) używany przez elementy runbook, ponieważ zawsze będzie dostępna na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="eebf5-270">Your management solution does not need toodefine [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="eebf5-271">Trzeba tooinclude zasobów dla innych modułu używany przez elementy runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-271">You do need tooinclude a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="eebf5-272">[Moduły integracji](../automation/automation-integration-modules.md) typu **Microsoft.Automation/automationAccounts/modules** i mieć hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="eebf5-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have hello following structure.</span></span>  <span data-ttu-id="eebf5-273">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


<span data-ttu-id="eebf5-274">w hello w poniższej tabeli opisano Hello właściwości zasobów modułu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-274">hello properties for module resources are described in hello following table.</span></span>

| <span data-ttu-id="eebf5-275">Właściwość</span><span class="sxs-lookup"><span data-stu-id="eebf5-275">Property</span></span> | <span data-ttu-id="eebf5-276">Opis</span><span class="sxs-lookup"><span data-stu-id="eebf5-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eebf5-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="eebf5-277">contentLink</span></span> |<span data-ttu-id="eebf5-278">Określa zawartość hello hello modułu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-278">Specifies hello content of hello module.</span></span> <br><br><span data-ttu-id="eebf5-279">Identyfikator URI - identyfikator Uri zawartości toohello hello modułu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-279">uri - Uri toohello content of hello module.</span></span>  <span data-ttu-id="eebf5-280">Są to plik .ps1 dla elementów runbook programu PowerShell i skryptów, a plik wyeksportowany element runbook graficzny element runbook wykresu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="eebf5-281">Wersja — wersja modułu hello własne śledzenia.</span><span class="sxs-lookup"><span data-stu-id="eebf5-281">version - Version of hello module for your own tracking.</span></span> |

<span data-ttu-id="eebf5-282">Hello runbook powinien zależą od hello modułu zasobów tooensure utworzony przed hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-282">hello runbook should depend on hello module resource tooensure that it's created before hello runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="eebf5-283">Aktualizowanie modułów</span><span class="sxs-lookup"><span data-stu-id="eebf5-283">Updating modules</span></span>
<span data-ttu-id="eebf5-284">Aktualizacji rozwiązanie do zarządzania, które zawiera element runbook, który używa harmonogram, a nowej wersji hello rozwiązań ma nowy moduł używany przez ten element runbook, hello runbook może używać hello starą wersję hello modułu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-284">If you update a management solution that includes a runbook that uses a schedule, and hello new version of your solution has a new module used by that runbook, then hello runbook may use hello old version of hello module.</span></span>  <span data-ttu-id="eebf5-285">Należy uwzględnić następujące elementy runbook w rozwiązaniu hello i utworzyć toorun zadania je przed wszystkie inne elementy runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-285">You should include hello following runbooks in your solution and create a job toorun them before any other runbooks.</span></span>  <span data-ttu-id="eebf5-286">Daje to pewność, że wszystkie moduły są aktualizowane jako wymagany przed powitalne elementy runbook są ładowane.</span><span class="sxs-lookup"><span data-stu-id="eebf5-286">This will ensure that any modules are updated as required before hello runbooks are loaded.</span></span>

* <span data-ttu-id="eebf5-287">[Aktualizacja ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) sprawdzi wszystkie moduły hello używany przez elementy runbook w rozwiązaniu hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="eebf5-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of hello modules used by runbooks in your solution are hello latest version.</span></span>  
* <span data-ttu-id="eebf5-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) zostanie ponownie zarejestrować wszystkie hello harmonogramu zasobów tooensure, że hello elementy runbook połączone toothem z modułami najnowsze hello użycia.</span><span class="sxs-lookup"><span data-stu-id="eebf5-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of hello schedule resources tooensure that hello runbooks linked toothem with use hello latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="eebf5-289">Przykład</span><span class="sxs-lookup"><span data-stu-id="eebf5-289">Sample</span></span>
<span data-ttu-id="eebf5-290">Poniżej przedstawiono przykładowe rozwiązanie obejmujące obejmuje hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="eebf5-290">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="eebf5-291">Element Runbook.</span><span class="sxs-lookup"><span data-stu-id="eebf5-291">Runbook.</span></span>  <span data-ttu-id="eebf5-292">To jest przykładowy element runbook, przechowywane w publicznych repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="eebf5-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="eebf5-293">Zadanie usługi Automatyzacja rozpoczynającej się od elementu runbook hello rozwiązania hello jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="eebf5-293">Automation job that starts hello runbook when hello solution is installed.</span></span>
- <span data-ttu-id="eebf5-294">Harmonogram i zadania harmonogramu toostart hello runbook w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="eebf5-294">Schedule and job schedule toostart hello runbook at regular intervals.</span></span>
- <span data-ttu-id="eebf5-295">Certyfikat.</span><span class="sxs-lookup"><span data-stu-id="eebf5-295">Certificate.</span></span>
- <span data-ttu-id="eebf5-296">Poświadczenie.</span><span class="sxs-lookup"><span data-stu-id="eebf5-296">Credential.</span></span>
- <span data-ttu-id="eebf5-297">Zmienna.</span><span class="sxs-lookup"><span data-stu-id="eebf5-297">Variable.</span></span>
- <span data-ttu-id="eebf5-298">Moduł.</span><span class="sxs-lookup"><span data-stu-id="eebf5-298">Module.</span></span>  <span data-ttu-id="eebf5-299">Jest to hello [modułu OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) do zapisywania danych tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="eebf5-299">This is hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data tooLog Analytics.</span></span> 

<span data-ttu-id="eebf5-300">Witaj używa próbki [parametry standardowego rozwiązania](operations-management-suite-solutions-solution-file.md#parameters) zmiennych, które służy zwykle do rozwiązania jako przeciwieństwie wartości toohardcoding w definicjach zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="eebf5-300">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a><span data-ttu-id="eebf5-301">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eebf5-301">Next steps</span></span>
* <span data-ttu-id="eebf5-302">[Dodaj rozwiązanie tooyour widoku](operations-management-suite-solutions-resources-views.md) toovisualize zbieranych danych.</span><span class="sxs-lookup"><span data-stu-id="eebf5-302">[Add a view tooyour solution](operations-management-suite-solutions-resources-views.md) toovisualize collected data.</span></span>
