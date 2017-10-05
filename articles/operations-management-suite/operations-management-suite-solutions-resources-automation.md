---
title: "Zasobów usługi Automatyzacja Azure w rozwiązaniach pakietu OMS | Dokumentacja firmy Microsoft"
description: "Rozwiązania w OMS zazwyczaj uwzględnia elementy runbook automatyzacji Azure można zautomatyzować procesy, takie jak zbierania i przetwarzania danych monitorowania.  W tym artykule opisano, jak dołączyć elementy runbook i ich powiązane zasoby w rozwiązaniu."
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
ms.openlocfilehash: c1909183a33ed03d8165671cff25cc8b83b77733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="adding-azure-automation-resources-to-an-oms-management-solution-preview"></a><span data-ttu-id="670b8-104">Dodawanie zasobów usługi Automatyzacja Azure OMS rozwiązania do zarządzania (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="670b8-104">Adding Azure Automation resources to an OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="670b8-105">To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="670b8-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="670b8-106">Żadnego schematu opisanych poniżej może ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="670b8-106">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="670b8-107">[Rozwiązania do zarządzania w OMS](operations-management-suite-solutions.md) zazwyczaj uwzględnia elementy runbook automatyzacji Azure można zautomatyzować procesy, takie jak zbierania i przetwarzania danych monitorowania.</span><span class="sxs-lookup"><span data-stu-id="670b8-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="670b8-108">Oprócz elementów runbook kont automatyzacji zawiera zasoby, takie jak zmienne i harmonogramy, obsługujących elementy runbook używane w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="670b8-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span></span>  <span data-ttu-id="670b8-109">W tym artykule opisano, jak dołączyć elementy runbook i ich powiązane zasoby w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="670b8-109">This article describes how to include runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="670b8-110">Przykłady w tym artykule, użyj parametrów i zmiennych, które są wymagane ani wspólne dla rozwiązań do zarządzania i opisano w [tworzenia rozwiązań do zarządzania w Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="670b8-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="670b8-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="670b8-111">Prerequisites</span></span>
<span data-ttu-id="670b8-112">W tym artykule przyjęto założenie, że znasz już następujące informacje.</span><span class="sxs-lookup"><span data-stu-id="670b8-112">This article assumes that you're already familiar with the following information.</span></span>

- <span data-ttu-id="670b8-113">Jak [tworzenie rozwiązania do zarządzania](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="670b8-113">How to [create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="670b8-114">Struktura [plik rozwiązania](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="670b8-114">The structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="670b8-115">Jak [Tworzenie szablonów usługi Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="670b8-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="670b8-116">Konto usługi Automation</span><span class="sxs-lookup"><span data-stu-id="670b8-116">Automation account</span></span>
<span data-ttu-id="670b8-117">Wszystkie zasoby w automatyzacji Azure są zawarte w [konto automatyzacji](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="670b8-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="670b8-118">Zgodnie z opisem w [OMS obszaru roboczego i konto automatyzacji](operations-management-suite-solutions.md#oms-workspace-and-automation-account) konta automatyzacji nie jest zawarty w rozwiązaniu do zarządzania, ale musi istnieć przed zainstalowaniem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="670b8-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="670b8-119">Jeśli nie jest dostępny, nie będą instalacji rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="670b8-119">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="670b8-120">Nazwa każdego zasobu automatyzacji zawiera nazwę swojego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="670b8-120">The name of each Automation resource includes the name of its Automation account.</span></span>  <span data-ttu-id="670b8-121">Jest to rozwiązanie z **accountName** parametru, jak w poniższym przykładzie zasobu elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="670b8-122">Elementy Runbook</span><span class="sxs-lookup"><span data-stu-id="670b8-122">Runbooks</span></span>
<span data-ttu-id="670b8-123">Należy uwzględnić wszystkie elementy runbook, dzięki czemu są tworzone po zainstalowaniu rozwiązania już używana przez rozwiązania w pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="670b8-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span></span>  <span data-ttu-id="670b8-124">Treść elementu runbook w szablonie nie mogą zawierać jednak, należy opublikować element runbook do lokalizacji publicznej, gdzie jest dostępny przez dowolnego użytkownika instalowanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="670b8-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="670b8-125">[Element runbook automatyzacji Azure](../automation/automation-runbook-types.md) zasoby mają typ **Microsoft.Automation/automationAccounts/runbooks** i ma następującą strukturę.</span><span class="sxs-lookup"><span data-stu-id="670b8-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span></span> <span data-ttu-id="670b8-126">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="670b8-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="670b8-127">W poniższej tabeli opisano właściwości dla elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-127">The properties for runbooks are described in the following table.</span></span>

| <span data-ttu-id="670b8-128">Właściwość</span><span class="sxs-lookup"><span data-stu-id="670b8-128">Property</span></span> | <span data-ttu-id="670b8-129">Opis</span><span class="sxs-lookup"><span data-stu-id="670b8-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="670b8-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="670b8-130">runbookType</span></span> |<span data-ttu-id="670b8-131">Określa typy elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-131">Specifies the types of the runbook.</span></span> <br><br> <span data-ttu-id="670b8-132">Skrypt — skrypt programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="670b8-132">Script - PowerShell script</span></span> <br><span data-ttu-id="670b8-133">PowerShell — przepływ pracy programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="670b8-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="670b8-134">GraphPowerShell - runbook skryptu PowerShell graficznego</span><span class="sxs-lookup"><span data-stu-id="670b8-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="670b8-135">GraphPowerShellWorkflow - PowerShell graficzny element runbook przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="670b8-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="670b8-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="670b8-136">logProgress</span></span> |<span data-ttu-id="670b8-137">Określa, czy [rekordy postępu](../automation/automation-runbook-output-and-messages.md) ma być generowany dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="670b8-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="670b8-138">logVerbose</span></span> |<span data-ttu-id="670b8-139">Określa, czy [rekordów pełnych](../automation/automation-runbook-output-and-messages.md) ma być generowany dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="670b8-140">Opis elementu</span><span class="sxs-lookup"><span data-stu-id="670b8-140">description</span></span> |<span data-ttu-id="670b8-141">Opcjonalny opis dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-141">Optional description for the runbook.</span></span> |
| <span data-ttu-id="670b8-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="670b8-142">publishContentLink</span></span> |<span data-ttu-id="670b8-143">Określa zawartość elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-143">Specifies the content of the runbook.</span></span> <br><br><span data-ttu-id="670b8-144">Identyfikator URI - identyfikator Uri zawartości elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-144">uri - Uri to the content of the runbook.</span></span>  <span data-ttu-id="670b8-145">Są to plik .ps1 dla elementów runbook programu PowerShell i skryptów, a plik wyeksportowany element runbook graficzny element runbook wykresu.</span><span class="sxs-lookup"><span data-stu-id="670b8-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="670b8-146">Wersja — wersji elementu runbook do własnych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="670b8-146">version - Version of the runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="670b8-147">Automatyzacja zadań</span><span class="sxs-lookup"><span data-stu-id="670b8-147">Automation jobs</span></span>
<span data-ttu-id="670b8-148">Po uruchomieniu elementu runbook w automatyzacji Azure tworzy zadanie usługi Automatyzacja.</span><span class="sxs-lookup"><span data-stu-id="670b8-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="670b8-149">Można dodać zasobu Zadanie usługi Automatyzacja do rozwiązania, aby automatycznie uruchomić element runbook po zainstalowaniu rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="670b8-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span></span>  <span data-ttu-id="670b8-150">Ta metoda jest zwykle używana do uruchamiania elementów runbook, które są używane do początkowej konfiguracji rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="670b8-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span></span>  <span data-ttu-id="670b8-151">Aby uruchomić element runbook w regularnych odstępach czasu, należy utworzyć [harmonogram](#schedules) i [harmonogram zadań](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="670b8-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="670b8-152">Zasoby zadanie ma typ **Microsoft.Automation/automationAccounts/jobs** i ma następującą strukturę.</span><span class="sxs-lookup"><span data-stu-id="670b8-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span></span>  <span data-ttu-id="670b8-153">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="670b8-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="670b8-154">Właściwości automatyzacji zadań są opisane w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="670b8-154">The properties for automation jobs are described in the following table.</span></span>

| <span data-ttu-id="670b8-155">Właściwość</span><span class="sxs-lookup"><span data-stu-id="670b8-155">Property</span></span> | <span data-ttu-id="670b8-156">Opis</span><span class="sxs-lookup"><span data-stu-id="670b8-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="670b8-157">Element runbook</span><span class="sxs-lookup"><span data-stu-id="670b8-157">runbook</span></span> |<span data-ttu-id="670b8-158">Jedna nazwa jednostki o nazwie elementu runbook, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="670b8-158">Single name entity with the name of the runbook to start.</span></span> |
| <span data-ttu-id="670b8-159">Parametry</span><span class="sxs-lookup"><span data-stu-id="670b8-159">parameters</span></span> |<span data-ttu-id="670b8-160">Jednostki dla każdej wartości parametru wymagane przez element runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-160">Entity for each parameter value required by the runbook.</span></span> |

<span data-ttu-id="670b8-161">Zadanie zawiera nazwę elementu runbook i wartości parametrów do wysłania do elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span></span>  <span data-ttu-id="670b8-162">Zadanie powinno [są zależne od](operations-management-suite-solutions-solution-file.md#resources) elementu runbook, który jest uruchamiany od elementu runbook musi zostać utworzone przed zadania.</span><span class="sxs-lookup"><span data-stu-id="670b8-162">The job should [depend on](operations-management-suite-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span></span>  <span data-ttu-id="670b8-163">Jeśli masz wiele elementów runbook, który ma być uruchamiany przez zadanie, które są zależne od innych zadań, które powinny być uruchamiane w pierwszy można zdefiniować ich kolejność.</span><span class="sxs-lookup"><span data-stu-id="670b8-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="670b8-164">Nazwa zasobu zadania musi zawierać identyfikator GUID, który zazwyczaj jest przypisywany przez parametr.</span><span class="sxs-lookup"><span data-stu-id="670b8-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="670b8-165">Więcej o parametrach identyfikatora GUID w [tworzenie rozwiązań w Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="670b8-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="670b8-166">Certyfikaty</span><span class="sxs-lookup"><span data-stu-id="670b8-166">Certificates</span></span>
<span data-ttu-id="670b8-167">[Certyfikaty automatyzacji Azure](../automation/automation-certificates.md) typu **Microsoft.Automation/automationAccounts/certificates** i ma następującą strukturę.</span><span class="sxs-lookup"><span data-stu-id="670b8-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span></span> <span data-ttu-id="670b8-168">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="670b8-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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



<span data-ttu-id="670b8-169">W poniższej tabeli opisano właściwości zasobów certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="670b8-169">The properties for Certificates resources are described in the following table.</span></span>

| <span data-ttu-id="670b8-170">Właściwość</span><span class="sxs-lookup"><span data-stu-id="670b8-170">Property</span></span> | <span data-ttu-id="670b8-171">Opis</span><span class="sxs-lookup"><span data-stu-id="670b8-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="670b8-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="670b8-172">base64Value</span></span> |<span data-ttu-id="670b8-173">Wartość Base-64 dla certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="670b8-173">Base 64 value for the certificate.</span></span> |
| <span data-ttu-id="670b8-174">Odcisk palca</span><span class="sxs-lookup"><span data-stu-id="670b8-174">thumbprint</span></span> |<span data-ttu-id="670b8-175">Odcisk palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="670b8-175">Thumbprint for the certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="670b8-176">Poświadczenia</span><span class="sxs-lookup"><span data-stu-id="670b8-176">Credentials</span></span>
<span data-ttu-id="670b8-177">[Poświadczenia usługi Automatyzacja Azure](../automation/automation-credentials.md) typu **Microsoft.Automation/automationAccounts/credentials** i ma następującą strukturę.</span><span class="sxs-lookup"><span data-stu-id="670b8-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span></span>  <span data-ttu-id="670b8-178">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="670b8-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


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

<span data-ttu-id="670b8-179">W poniższej tabeli opisano właściwości zasobów poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="670b8-179">The properties for Credential resources are described in the following table.</span></span>

| <span data-ttu-id="670b8-180">Właściwość</span><span class="sxs-lookup"><span data-stu-id="670b8-180">Property</span></span> | <span data-ttu-id="670b8-181">Opis</span><span class="sxs-lookup"><span data-stu-id="670b8-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="670b8-182">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="670b8-182">userName</span></span> |<span data-ttu-id="670b8-183">Nazwa użytkownika dla poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="670b8-183">User name for the credential.</span></span> |
| <span data-ttu-id="670b8-184">hasło</span><span class="sxs-lookup"><span data-stu-id="670b8-184">password</span></span> |<span data-ttu-id="670b8-185">Hasło dla poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="670b8-185">Password for the credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="670b8-186">Harmonogramy</span><span class="sxs-lookup"><span data-stu-id="670b8-186">Schedules</span></span>
<span data-ttu-id="670b8-187">[Harmonogramy automatyzacji Azure](../automation/automation-schedules.md) typu **Microsoft.Automation/automationAccounts/schedules** i ma następującą strukturę.</span><span class="sxs-lookup"><span data-stu-id="670b8-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the the following structure.</span></span> <span data-ttu-id="670b8-188">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="670b8-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="670b8-189">W poniższej tabeli opisano właściwości planowania zasobów.</span><span class="sxs-lookup"><span data-stu-id="670b8-189">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="670b8-190">Właściwość</span><span class="sxs-lookup"><span data-stu-id="670b8-190">Property</span></span> | <span data-ttu-id="670b8-191">Opis</span><span class="sxs-lookup"><span data-stu-id="670b8-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="670b8-192">Opis elementu</span><span class="sxs-lookup"><span data-stu-id="670b8-192">description</span></span> |<span data-ttu-id="670b8-193">Opcjonalny opis dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="670b8-193">Optional description for the schedule.</span></span> |
| <span data-ttu-id="670b8-194">startTime</span><span class="sxs-lookup"><span data-stu-id="670b8-194">startTime</span></span> |<span data-ttu-id="670b8-195">Określa czas rozpoczęcia harmonogramu jako obiekt typu DateTime.</span><span class="sxs-lookup"><span data-stu-id="670b8-195">Specifies the start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="670b8-196">Jeśli można przekonwertować na prawidłowy element DateTime można podać ciąg.</span><span class="sxs-lookup"><span data-stu-id="670b8-196">A string can be provided if it can be converted to a valid DateTime.</span></span> |
| <span data-ttu-id="670b8-197">IsEnabled</span><span class="sxs-lookup"><span data-stu-id="670b8-197">isEnabled</span></span> |<span data-ttu-id="670b8-198">Określa, czy jest włączony harmonogram.</span><span class="sxs-lookup"><span data-stu-id="670b8-198">Specifies whether the schedule is enabled.</span></span> |
| <span data-ttu-id="670b8-199">Interwał</span><span class="sxs-lookup"><span data-stu-id="670b8-199">interval</span></span> |<span data-ttu-id="670b8-200">Typ interwału harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="670b8-200">The type of interval for the schedule.</span></span><br><br><span data-ttu-id="670b8-201">dzień</span><span class="sxs-lookup"><span data-stu-id="670b8-201">day</span></span><br><span data-ttu-id="670b8-202">godz.</span><span class="sxs-lookup"><span data-stu-id="670b8-202">hour</span></span> |
| <span data-ttu-id="670b8-203">częstotliwość</span><span class="sxs-lookup"><span data-stu-id="670b8-203">frequency</span></span> |<span data-ttu-id="670b8-204">Częstotliwość, z jaką harmonogram powinny wyzwalać w liczbie dni lub godzin.</span><span class="sxs-lookup"><span data-stu-id="670b8-204">Frequency that the schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="670b8-205">Harmonogramy musi mieć godzinę rozpoczęcia o wartości większej niż bieżący czas.</span><span class="sxs-lookup"><span data-stu-id="670b8-205">Schedules must have a start time with a value greater than the current time.</span></span>  <span data-ttu-id="670b8-206">Nie można podać tę wartość za pomocą zmiennych, ponieważ czy nie ma możliwości wiedzy, kiedy przechodzi do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="670b8-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span></span>

<span data-ttu-id="670b8-207">Za pomocą harmonogramu zasobów w rozwiązaniu, należy użyć jednej z następujących dwóch strategii.</span><span class="sxs-lookup"><span data-stu-id="670b8-207">Use one of the following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="670b8-208">Czas rozpoczęcia harmonogramu, należy użyć parametru.</span><span class="sxs-lookup"><span data-stu-id="670b8-208">Use a parameter for the start time of the schedule.</span></span>  <span data-ttu-id="670b8-209">To pojawi się monit podanie wartości podczas instalacji rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="670b8-209">This will prompt the user to provide a value when they install the solution.</span></span>  <span data-ttu-id="670b8-210">Jeśli masz wiele harmonogramów można używać wartości jeden parametr dla więcej niż jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="670b8-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="670b8-211">Tworzenie harmonogramów przy użyciu elementu runbook, który rozpoczyna się, gdy rozwiązanie jest zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="670b8-211">Create the schedules using a runbook that starts when the solution is installed.</span></span>  <span data-ttu-id="670b8-212">Spowoduje to usunięcie wymaganie użytkownika, aby określić godzinę, ale nie może zawierać harmonogram w rozwiązaniu, dlatego zostanie usunięta po usunięciu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="670b8-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="670b8-213">Harmonogramy zadań</span><span class="sxs-lookup"><span data-stu-id="670b8-213">Job schedules</span></span>
<span data-ttu-id="670b8-214">Zadania planowania zasobów powiązania elementu runbook z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="670b8-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="670b8-215">Mają one typu **Microsoft.Automation/automationAccounts/jobSchedules** i ma następującą strukturę.</span><span class="sxs-lookup"><span data-stu-id="670b8-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the the following structure.</span></span>  <span data-ttu-id="670b8-216">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="670b8-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="670b8-217">W poniższej tabeli opisano właściwości harmonogramy zadań.</span><span class="sxs-lookup"><span data-stu-id="670b8-217">The properties for job schedules are described in the following table.</span></span>

| <span data-ttu-id="670b8-218">Właściwość</span><span class="sxs-lookup"><span data-stu-id="670b8-218">Property</span></span> | <span data-ttu-id="670b8-219">Opis</span><span class="sxs-lookup"><span data-stu-id="670b8-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="670b8-220">Nazwa harmonogramu</span><span class="sxs-lookup"><span data-stu-id="670b8-220">schedule name</span></span> |<span data-ttu-id="670b8-221">Pojedynczy **nazwa** jednostki o nazwę harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="670b8-221">Single **name** entity with the name of the schedule.</span></span> |
| <span data-ttu-id="670b8-222">Nazwa elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="670b8-222">runbook name</span></span>  |<span data-ttu-id="670b8-223">Pojedynczy **nazwa** jednostki o nazwie elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-223">Single **name** entity with the name of the runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="670b8-224">Zmienne</span><span class="sxs-lookup"><span data-stu-id="670b8-224">Variables</span></span>
<span data-ttu-id="670b8-225">[Zmienne automatyzacji Azure](../automation/automation-variables.md) typu **Microsoft.Automation/automationAccounts/variables** i ma następującą strukturę.</span><span class="sxs-lookup"><span data-stu-id="670b8-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span></span>  <span data-ttu-id="670b8-226">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="670b8-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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

<span data-ttu-id="670b8-227">W poniższej tabeli opisano właściwości dla zmiennej zasobów.</span><span class="sxs-lookup"><span data-stu-id="670b8-227">The properties for variable resources are described in the following table.</span></span>

| <span data-ttu-id="670b8-228">Właściwość</span><span class="sxs-lookup"><span data-stu-id="670b8-228">Property</span></span> | <span data-ttu-id="670b8-229">Opis</span><span class="sxs-lookup"><span data-stu-id="670b8-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="670b8-230">Opis elementu</span><span class="sxs-lookup"><span data-stu-id="670b8-230">description</span></span> | <span data-ttu-id="670b8-231">Opcjonalny opis dla zmiennej.</span><span class="sxs-lookup"><span data-stu-id="670b8-231">Optional description for the variable.</span></span> |
| <span data-ttu-id="670b8-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="670b8-232">isEncrypted</span></span> | <span data-ttu-id="670b8-233">Określa, czy ma być szyfrowana zmienna.</span><span class="sxs-lookup"><span data-stu-id="670b8-233">Specifies whether the variable should be encrypted.</span></span> |
| <span data-ttu-id="670b8-234">type</span><span class="sxs-lookup"><span data-stu-id="670b8-234">type</span></span> | <span data-ttu-id="670b8-235">Ta właściwość obecnie nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="670b8-235">This property currently has no effect.</span></span>  <span data-ttu-id="670b8-236">Typ danych zmiennej będzie określana przez wartość początkowa.</span><span class="sxs-lookup"><span data-stu-id="670b8-236">The data type of the variable will be determined by the initial value.</span></span> |
| <span data-ttu-id="670b8-237">wartość</span><span class="sxs-lookup"><span data-stu-id="670b8-237">value</span></span> | <span data-ttu-id="670b8-238">Wartość zmiennej.</span><span class="sxs-lookup"><span data-stu-id="670b8-238">Value for the variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="670b8-239">**Typu** właściwości obecnie nie ma wpływu na zmiennej tworzona.</span><span class="sxs-lookup"><span data-stu-id="670b8-239">The **type** property currently has no effect on the variable being created.</span></span>  <span data-ttu-id="670b8-240">Typ danych zmiennej będzie określana przez wartość.</span><span class="sxs-lookup"><span data-stu-id="670b8-240">The data type for the variable will be determined by the value.</span></span>  

<span data-ttu-id="670b8-241">Jeśli ustawisz wartość początkowa zmiennej musi być skonfigurowany jako prawidłowy typ danych.</span><span class="sxs-lookup"><span data-stu-id="670b8-241">If you set the initial value for the variable, it must be configured as the correct data type.</span></span>  <span data-ttu-id="670b8-242">Poniższa tabela zawiera różne typy danych dopuszczalny i ich składni.</span><span class="sxs-lookup"><span data-stu-id="670b8-242">The following table provides the different data types allowable and their syntax.</span></span>  <span data-ttu-id="670b8-243">Należy pamiętać, że wartości w formacie JSON powinny zawsze być ujęte w cudzysłów z znaków specjalnych w cudzysłowy.</span><span class="sxs-lookup"><span data-stu-id="670b8-243">Note that values in JSON are expected to always be enclosed in quotes with any special characters within the quotes.</span></span>  <span data-ttu-id="670b8-244">Na przykład wartość ciągu zostałaby określona przez stawiać cudzysłów wokół ciąg (przy użyciu znaku ucieczki (\\)) podczas zostałaby określona wartość liczbową z jednego zestawu znaków cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="670b8-244">For example, a string value would be specified by quotes around the string (using the escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="670b8-245">Typ danych</span><span class="sxs-lookup"><span data-stu-id="670b8-245">Data type</span></span> | <span data-ttu-id="670b8-246">Opis</span><span class="sxs-lookup"><span data-stu-id="670b8-246">Description</span></span> | <span data-ttu-id="670b8-247">Przykład</span><span class="sxs-lookup"><span data-stu-id="670b8-247">Example</span></span> | <span data-ttu-id="670b8-248">Jest rozpoznawana jako</span><span class="sxs-lookup"><span data-stu-id="670b8-248">Resolves to</span></span> |
|:--|:--|:--|:--|
| <span data-ttu-id="670b8-249">Ciąg</span><span class="sxs-lookup"><span data-stu-id="670b8-249">string</span></span>   | <span data-ttu-id="670b8-250">Wartość należy ująć w cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="670b8-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="670b8-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="670b8-251">"\"Hello world\""</span></span> | <span data-ttu-id="670b8-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="670b8-252">"Hello world"</span></span> |
| <span data-ttu-id="670b8-253">numeryczne</span><span class="sxs-lookup"><span data-stu-id="670b8-253">numeric</span></span>  | <span data-ttu-id="670b8-254">Wartość liczbowa z apostrofy.</span><span class="sxs-lookup"><span data-stu-id="670b8-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="670b8-255">"64"</span><span class="sxs-lookup"><span data-stu-id="670b8-255">"64"</span></span> | <span data-ttu-id="670b8-256">64</span><span class="sxs-lookup"><span data-stu-id="670b8-256">64</span></span> |
| <span data-ttu-id="670b8-257">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="670b8-257">boolean</span></span>  | <span data-ttu-id="670b8-258">**wartość true,** lub **false** w cudzysłowy.</span><span class="sxs-lookup"><span data-stu-id="670b8-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="670b8-259">Należy pamiętać, że ta wartość musi być litera.</span><span class="sxs-lookup"><span data-stu-id="670b8-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="670b8-260">wartość "prawda"</span><span class="sxs-lookup"><span data-stu-id="670b8-260">"true"</span></span> | <span data-ttu-id="670b8-261">Wartość true</span><span class="sxs-lookup"><span data-stu-id="670b8-261">true</span></span> |
| <span data-ttu-id="670b8-262">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="670b8-262">datetime</span></span> | <span data-ttu-id="670b8-263">Serializacji wartości typu date.</span><span class="sxs-lookup"><span data-stu-id="670b8-263">Serialized date value.</span></span><br><span data-ttu-id="670b8-264">Polecenia cmdlet ConvertTo-Json w programie PowerShell służy do generowania wartości dla określonej daty.</span><span class="sxs-lookup"><span data-stu-id="670b8-264">You can use the ConvertTo-Json cmdlet in PowerShell to generate this value for a particular date.</span></span><br><span data-ttu-id="670b8-265">Przykład: get data "2017-5/24 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="670b8-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="670b8-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="670b8-266">ConvertTo-Json</span></span> | <span data-ttu-id="670b8-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="670b8-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="670b8-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="670b8-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="670b8-269">Moduły</span><span class="sxs-lookup"><span data-stu-id="670b8-269">Modules</span></span>
<span data-ttu-id="670b8-270">Rozwiązania do zarządzania, nie trzeba definiować [modułów globalnych](../automation/automation-integration-modules.md) używany przez elementy runbook, ponieważ zawsze będzie dostępna na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="670b8-270">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="670b8-271">Należy uwzględnić zasobów dla innych modułu używany przez elementy runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-271">You do need to include a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="670b8-272">[Moduły integracji](../automation/automation-integration-modules.md) typu **Microsoft.Automation/automationAccounts/modules** i ma następującą strukturę.</span><span class="sxs-lookup"><span data-stu-id="670b8-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span></span>  <span data-ttu-id="670b8-273">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="670b8-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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


<span data-ttu-id="670b8-274">W poniższej tabeli opisano właściwości zasobów modułu.</span><span class="sxs-lookup"><span data-stu-id="670b8-274">The properties for module resources are described in the following table.</span></span>

| <span data-ttu-id="670b8-275">Właściwość</span><span class="sxs-lookup"><span data-stu-id="670b8-275">Property</span></span> | <span data-ttu-id="670b8-276">Opis</span><span class="sxs-lookup"><span data-stu-id="670b8-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="670b8-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="670b8-277">contentLink</span></span> |<span data-ttu-id="670b8-278">Określa zawartość modułu.</span><span class="sxs-lookup"><span data-stu-id="670b8-278">Specifies the content of the module.</span></span> <br><br><span data-ttu-id="670b8-279">Identyfikator URI - identyfikator Uri zawartości modułu.</span><span class="sxs-lookup"><span data-stu-id="670b8-279">uri - Uri to the content of the module.</span></span>  <span data-ttu-id="670b8-280">Są to plik .ps1 dla elementów runbook programu PowerShell i skryptów, a plik wyeksportowany element runbook graficzny element runbook wykresu.</span><span class="sxs-lookup"><span data-stu-id="670b8-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="670b8-281">Wersja - modułu dla własnego śledzenia.</span><span class="sxs-lookup"><span data-stu-id="670b8-281">version - Version of the module for your own tracking.</span></span> |

<span data-ttu-id="670b8-282">Element runbook należy są zależne od zasobów modułu, aby upewnić się, że został utworzony przed elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-282">The runbook should depend on the module resource to ensure that it's created before the runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="670b8-283">Aktualizowanie modułów</span><span class="sxs-lookup"><span data-stu-id="670b8-283">Updating modules</span></span>
<span data-ttu-id="670b8-284">Aktualizacji rozwiązanie do zarządzania, które zawiera element runbook, który używa harmonogram, a nowa wersja rozwiązań ma nowy moduł używany przez ten element runbook, element runbook może używać starej wersji modułu.</span><span class="sxs-lookup"><span data-stu-id="670b8-284">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span></span>  <span data-ttu-id="670b8-285">Powinny obejmować następujące elementy runbook w rozwiązaniu i utworzyć zadanie, aby uruchomić je przed wszystkie inne elementy runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-285">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span></span>  <span data-ttu-id="670b8-286">Daje to pewność, że wszystkie moduły są aktualizowane, kiedy wymagana przed elementy runbook zostały załadowane.</span><span class="sxs-lookup"><span data-stu-id="670b8-286">This will ensure that any modules are updated as required before the runbooks are loaded.</span></span>

* <span data-ttu-id="670b8-287">[Aktualizacja ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) sprawdzi wszystkie moduły używane przez elementy runbook w rozwiązaniu do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="670b8-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span></span>  
* <span data-ttu-id="670b8-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) zostanie ponownie zarejestrować wszystkie zasoby harmonogram, aby upewnić się, że elementy runbook powiązane z nimi przy użyciu najnowszych modułów.</span><span class="sxs-lookup"><span data-stu-id="670b8-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="670b8-289">Przykład</span><span class="sxs-lookup"><span data-stu-id="670b8-289">Sample</span></span>
<span data-ttu-id="670b8-290">Poniżej przedstawiono przykładowe rozwiązanie obejmujące obejmuje następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="670b8-290">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="670b8-291">Element Runbook.</span><span class="sxs-lookup"><span data-stu-id="670b8-291">Runbook.</span></span>  <span data-ttu-id="670b8-292">To jest przykładowy element runbook, przechowywane w publicznych repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="670b8-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="670b8-293">Zadanie usługi Automatyzacja, który uruchomi element runbook, gdy rozwiązanie jest zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="670b8-293">Automation job that starts the runbook when the solution is installed.</span></span>
- <span data-ttu-id="670b8-294">Harmonogram i harmonogram uruchamiania elementu runbook w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="670b8-294">Schedule and job schedule to start the runbook at regular intervals.</span></span>
- <span data-ttu-id="670b8-295">Certyfikat.</span><span class="sxs-lookup"><span data-stu-id="670b8-295">Certificate.</span></span>
- <span data-ttu-id="670b8-296">Poświadczenie.</span><span class="sxs-lookup"><span data-stu-id="670b8-296">Credential.</span></span>
- <span data-ttu-id="670b8-297">Zmienna.</span><span class="sxs-lookup"><span data-stu-id="670b8-297">Variable.</span></span>
- <span data-ttu-id="670b8-298">Moduł.</span><span class="sxs-lookup"><span data-stu-id="670b8-298">Module.</span></span>  <span data-ttu-id="670b8-299">Jest to [modułu OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) do zapisywania danych do analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="670b8-299">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span></span> 

<span data-ttu-id="670b8-300">W przykładzie użyto [parametry standardowego rozwiązania](operations-management-suite-solutions-solution-file.md#parameters) zmiennych, które służy zwykle do rozwiązania, w przeciwieństwie do wartości hardcoding w definicji zasobu.</span><span class="sxs-lookup"><span data-stu-id="670b8-300">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>


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
            "description": "GUID for the schedule link to runbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the runbook job.",
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




## <a name="next-steps"></a><span data-ttu-id="670b8-301">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="670b8-301">Next steps</span></span>
* <span data-ttu-id="670b8-302">[Dodaj widok do rozwiązania](operations-management-suite-solutions-resources-views.md) do wizualizacji zebranych danych.</span><span class="sxs-lookup"><span data-stu-id="670b8-302">[Add a view to your solution](operations-management-suite-solutions-resources-views.md) to visualize collected data.</span></span>
