---
title: "rozwiązania do zarządzania aaaCreating w Operations Management Suite (OMS) | Dokumentacja firmy Microsoft"
description: "Rozwiązania do zarządzania rozszerzyć funkcjonalność hello z Operations Management Suite (OMS), zapewniając scenariusze zarządzania spakowanych dodać obszar roboczy OMS tootheir klientów.  Ten artykuł zawiera szczegóły dotyczące tworzenia toobe rozwiązań zarządzania używane we własnym środowisku lub wprowadzone dostępne tooyour klientów."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="8fa0f-104">Tworzenie pliku rozwiązania zarządzania w Operations Management Suite (OMS) (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="8fa0f-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="8fa0f-105">To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="8fa0f-106">Żadnego schematu opisanych poniżej jest toochange podmiotu.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-106">Any schema described below is subject toochange.</span></span>  

<span data-ttu-id="8fa0f-107">Rozwiązania do zarządzania w Operations Management Suite (OMS) są zaimplementowane jako [szablonów Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="8fa0f-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="8fa0f-108">głównym zadaniem Hello się dowiedzieć, jak learning tooauthor rozwiązania do zarządzania w sposób zbyt[Tworzenie szablonu](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8fa0f-108">hello main task in learning how tooauthor management solutions is learning how too[author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="8fa0f-109">W tym artykule przedstawiono szczegóły unikatowy szablony używane dla rozwiązań i w jaki sposób tooconfigure rozwiązania typowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-109">This article provides unique details of templates used for solutions and how tooconfigure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="8fa0f-110">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="8fa0f-110">Tools</span></span>

<span data-ttu-id="8fa0f-111">Można użyć dowolnego toowork Edytor tekstu z plików rozwiązania, ale zaleca się wykorzystaniu hello funkcje zawarte w Visual Studio lub Visual Studio Code, zgodnie z opisem w hello następujące artykuły.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-111">You can use any text editor toowork with solution files, but we recommend leveraging hello features provided in Visual Studio or Visual Studio Code as described in hello following articles.</span></span>

- [<span data-ttu-id="8fa0f-112">Tworzenie i wdrażanie grup zasobów platformy Azure za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8fa0f-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="8fa0f-113">Praca z szablony usługi Azure Resource Manager w kodzie programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8fa0f-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="8fa0f-114">Struktura</span><span class="sxs-lookup"><span data-stu-id="8fa0f-114">Structure</span></span>
<span data-ttu-id="8fa0f-115">Podstawowa struktura pliku rozwiązania zarządzania Hello jest hello sam, jak [szablonu usługi Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#template-format) czyli w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-115">hello basic structure of a management solution file is hello same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="8fa0f-116">Każdy z poniższych rozdziałach hello opisano elementy najwyższego poziomu hello i i ich zawartość w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-116">Each of hello sections below describes hello top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="8fa0f-117">Parametry</span><span class="sxs-lookup"><span data-stu-id="8fa0f-117">Parameters</span></span>
<span data-ttu-id="8fa0f-118">[Parametry](../azure-resource-manager/resource-group-authoring-templates.md#parameters) to wartości, które wymagają od użytkownika hello, podczas instalacji hello rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from hello user when they install hello management solution.</span></span>  <span data-ttu-id="8fa0f-119">Istnieją standardowe parametry, których wszystkie rozwiązania, a następnie można dodać dodatkowe parametry zgodnie z potrzebami dla określonego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="8fa0f-120">Jak użytkownicy będą podać wartości parametrów instalacji rozwiązanie będzie zależeć od określonego parametru hello i sposobu rozwiązania hello jest instalowany.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-120">How users will provide parameter values when they install your solution will depend on hello particular parameter and how hello solution is being installed.</span></span>

<span data-ttu-id="8fa0f-121">Kiedy użytkownik instaluje rozwiązania do zarządzania za pośrednictwem hello [portalu Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) lub [szablonów Szybki Start Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions) są zostanie wyświetlony monit o tooselect [OMS obszaru roboczego i konta automatyzacji ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="8fa0f-121">When a user installs your management solution through hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted tooselect an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="8fa0f-122">Są używane toopopulate hello wartości każdego hello standardowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-122">These are used toopopulate hello values of each of hello standard parameters.</span></span>  <span data-ttu-id="8fa0f-123">Witaj, użytkownik nie jest monitowany toodirectly Podaj wartości parametrów standardowe hello, ale są one tooprovide zostanie wyświetlony monit o wartości żadnych parametrów.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-123">hello user is not prompted toodirectly provide values for hello standard parameters, but they are prompted tooprovide values for any additional parameters.</span></span>

<span data-ttu-id="8fa0f-124">Po zainstalowaniu przez użytkownika hello rozwiązania [innej metody](operations-management-suite-solutions.md#finding-and-installing-management-solutions), użytkownik musi podać wartość dla wszystkich parametrów standardowe i wszystkie dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-124">When hello user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="8fa0f-125">Poniżej przedstawiono przykładowe parametru.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="8fa0f-126">Witaj w poniższej tabeli opisano atrybuty hello parametru.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-126">hello following table describes hello attributes of a parameter.</span></span>

| <span data-ttu-id="8fa0f-127">Atrybut</span><span class="sxs-lookup"><span data-stu-id="8fa0f-127">Attribute</span></span> | <span data-ttu-id="8fa0f-128">Opis</span><span class="sxs-lookup"><span data-stu-id="8fa0f-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8fa0f-129">type</span><span class="sxs-lookup"><span data-stu-id="8fa0f-129">type</span></span> |<span data-ttu-id="8fa0f-130">Typ danych parametru hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-130">Data type for hello parameter.</span></span> <span data-ttu-id="8fa0f-131">kontrolki wprowadzania Hello wyświetlane dla użytkownika hello zależy od typu danych hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-131">hello input control displayed for hello user depends on hello data type.</span></span><br><br><span data-ttu-id="8fa0f-132">bool — menu rozwijane</span><span class="sxs-lookup"><span data-stu-id="8fa0f-132">bool - Drop down box</span></span><br><span data-ttu-id="8fa0f-133">ciąg — pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="8fa0f-133">string - Text box</span></span><br><span data-ttu-id="8fa0f-134">int — pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="8fa0f-134">int - Text box</span></span><br><span data-ttu-id="8fa0f-135">SecureString — pole hasła</span><span class="sxs-lookup"><span data-stu-id="8fa0f-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="8fa0f-136">category</span><span class="sxs-lookup"><span data-stu-id="8fa0f-136">category</span></span> |<span data-ttu-id="8fa0f-137">Kategoria opcjonalny parametr hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-137">Optional category for hello parameter.</span></span>  <span data-ttu-id="8fa0f-138">Parametry w tej samej kategorii są zgrupowane hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-138">Parameters in hello same category are grouped together.</span></span> |
| <span data-ttu-id="8fa0f-139">Formant</span><span class="sxs-lookup"><span data-stu-id="8fa0f-139">control</span></span> |<span data-ttu-id="8fa0f-140">Dodatkowe funkcje dotyczące parametrów ciągu.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="8fa0f-141">DATETIME — formant daty i godziny są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="8fa0f-142">Identyfikator GUID - wartości identyfikatora Guid jest generowany automatycznie i hello parametru nie jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-142">guid - Guid value is automatically generated, and hello parameter is not displayed.</span></span> |
| <span data-ttu-id="8fa0f-143">description</span><span class="sxs-lookup"><span data-stu-id="8fa0f-143">description</span></span> |<span data-ttu-id="8fa0f-144">Opcjonalny opis dla parametru hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-144">Optional description for hello parameter.</span></span>  <span data-ttu-id="8fa0f-145">Wyświetlane informacje dymek dalej toohello parametr.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-145">Displayed in an information balloon next toohello parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="8fa0f-146">Standardowe parametry</span><span class="sxs-lookup"><span data-stu-id="8fa0f-146">Standard parameters</span></span>
<span data-ttu-id="8fa0f-147">Witaj poniższej tabeli wymieniono hello standardowe parametry dla wszystkich rozwiązań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-147">hello following table lists hello standard parameters for all management solutions.</span></span>  <span data-ttu-id="8fa0f-148">Te wartości zostaną wypełnione dla użytkownika hello zamiast monitowanie o rozwiązania jest zainstalowany za pomocą szablonów hello Azure Marketplace lub Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-148">These values are populated for hello user instead of prompting for them when your solution is installed from hello Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="8fa0f-149">Witaj użytkownik musi podać wartości dla nich, jeśli rozwiązanie hello jest zainstalowana z innej metody.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-149">hello user must provide values for them if hello solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="8fa0f-150">Interfejs użytkownika Hello w szablonach hello Azure Marketplace i szybkiego startu oczekuje nazwy parametrów hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-150">hello user interface in hello Azure Marketplace and Quickstart templates is expecting hello parameter names in hello table.</span></span>  <span data-ttu-id="8fa0f-151">Jeśli używasz różne nazwy parametrów następnie hello użytkownik będzie monitowany dla nich, a nie zostaną one automatycznie wypełnione.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-151">If you use different parameter names then hello user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="8fa0f-152">Parametr</span><span class="sxs-lookup"><span data-stu-id="8fa0f-152">Parameter</span></span> | <span data-ttu-id="8fa0f-153">Typ</span><span class="sxs-lookup"><span data-stu-id="8fa0f-153">Type</span></span> | <span data-ttu-id="8fa0f-154">Opis</span><span class="sxs-lookup"><span data-stu-id="8fa0f-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8fa0f-155">Nazwa konta</span><span class="sxs-lookup"><span data-stu-id="8fa0f-155">accountName</span></span> |<span data-ttu-id="8fa0f-156">Ciąg</span><span class="sxs-lookup"><span data-stu-id="8fa0f-156">string</span></span> |<span data-ttu-id="8fa0f-157">Nazwa konta automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="8fa0f-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="8fa0f-158">pricingTier</span></span> |<span data-ttu-id="8fa0f-159">Ciąg</span><span class="sxs-lookup"><span data-stu-id="8fa0f-159">string</span></span> |<span data-ttu-id="8fa0f-160">Warstwa cenowa obszaru roboczego analizy dzienników i konto usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="8fa0f-161">regionId</span><span class="sxs-lookup"><span data-stu-id="8fa0f-161">regionId</span></span> |<span data-ttu-id="8fa0f-162">Ciąg</span><span class="sxs-lookup"><span data-stu-id="8fa0f-162">string</span></span> |<span data-ttu-id="8fa0f-163">Region hello konto usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-163">Region of hello Azure Automation account.</span></span> |
| <span data-ttu-id="8fa0f-164">Nazwa rozwiązania</span><span class="sxs-lookup"><span data-stu-id="8fa0f-164">solutionName</span></span> |<span data-ttu-id="8fa0f-165">Ciąg</span><span class="sxs-lookup"><span data-stu-id="8fa0f-165">string</span></span> |<span data-ttu-id="8fa0f-166">Nazwa rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-166">Name of hello solution.</span></span>  <span data-ttu-id="8fa0f-167">Jeśli wdrażasz rozwiązania za pomocą szablonów Szybki Start, następnie należy zdefiniować Nazwa rozwiązania jako parametr, można zdefiniować zamiast konieczności toospecify użytkownika hello, jeden ciąg.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring hello user toospecify one.</span></span> |
| <span data-ttu-id="8fa0f-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="8fa0f-168">workspaceName</span></span> |<span data-ttu-id="8fa0f-169">Ciąg</span><span class="sxs-lookup"><span data-stu-id="8fa0f-169">string</span></span> |<span data-ttu-id="8fa0f-170">Nazwa obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="8fa0f-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="8fa0f-171">workspaceRegionId</span></span> |<span data-ttu-id="8fa0f-172">Ciąg</span><span class="sxs-lookup"><span data-stu-id="8fa0f-172">string</span></span> |<span data-ttu-id="8fa0f-173">Region hello obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-173">Region of hello Log Analytics workspace.</span></span> |


<span data-ttu-id="8fa0f-174">Poniżej znajduje się hello struktury hello standardowe parametry, które można skopiować i wkleić do pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-174">Following is hello structure of hello standard parameters that you can copy and paste into your solution file.</span></span>  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="8fa0f-175">W przypadku odwoływania się wartości tooparameter w innych elementach rozwiązania hello ze składnią hello **(parametr name) parametrów**.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-175">You refer tooparameter values in other elements of hello solution with hello syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="8fa0f-176">Na przykład tooaccess hello nazwa obszaru roboczego, należy użyć **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="8fa0f-176">For example, tooaccess hello workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="8fa0f-177">Zmienne</span><span class="sxs-lookup"><span data-stu-id="8fa0f-177">Variables</span></span>
<span data-ttu-id="8fa0f-178">[Zmienne](../azure-resource-manager/resource-group-authoring-templates.md#variables) wartości, które będą używane w rest hello hello rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in hello rest of hello management solution.</span></span>  <span data-ttu-id="8fa0f-179">Te wartości są uwidocznione toohello Użytkownik instalujący hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-179">These values are not exposed toohello user installing hello solution.</span></span>  <span data-ttu-id="8fa0f-180">Są one przeznaczone tooprovide hello autora z jednej lokalizacji, w którym można zarządzać wartości, które mogą być używane wielokrotnie w całym rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-180">They are intended tooprovide hello author with a single location where they can manage values that may be used multiple times throughout hello solution.</span></span> <span data-ttu-id="8fa0f-181">Żadne rozwiązanie tooyour określonej wartości należy umieścić w zmiennych jako min. toohard generowanie kodu hello **zasobów** elementu.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-181">You should put any values specific tooyour solution in variables as opposed toohard coding them in hello **resources** element.</span></span>  <span data-ttu-id="8fa0f-182">To czytelność kodu hello i pozwala tooeasily zmiany tych wartości w nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-182">This makes hello code more readable and allows you tooeasily change these values in later versions.</span></span>

<span data-ttu-id="8fa0f-183">Poniżej przedstawiono przykład **zmienne** element z typowych parametrów używanych w rozwiązaniach.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="8fa0f-184">Zobacz toovariable wartości za pośrednictwem rozwiązania hello ze składnią hello **zmienne ("Nazwa zmiennej")**.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-184">You refer toovariable values through hello solution with hello syntax **variables('variable name')**.</span></span>  <span data-ttu-id="8fa0f-185">Na przykład tooaccess hello zmiennej Nazwa rozwiązania, należy użyć **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-185">For example, tooaccess hello SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="8fa0f-186">Można również zdefiniować złożone zmienne ustawia wiele wartości.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="8fa0f-187">Są to szczególnie przydatne w rozwiązaniach do zarządzania gdzie definiujesz wiele właściwości dla różnych typów zasobów.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="8fa0f-188">Można na przykład restrukturyzacji zmienne rozwiązania hello pokazanym powyżej toohello poniżej.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-188">For example, you could restructure hello solution variables shown above toohello following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="8fa0f-189">W takim przypadku można znaleźć wartości toovariable za pośrednictwem rozwiązania hello ze składnią hello **variables('variable name').property**.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-189">In this case, you refer toovariable values through hello solution with hello syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="8fa0f-190">Na przykład tooaccess hello zmienna nazwy rozwiązania, należy użyć **variables('Solution'). Nazwa**.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-190">For example, tooaccess hello Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="8fa0f-191">Zasoby</span><span class="sxs-lookup"><span data-stu-id="8fa0f-191">Resources</span></span>
<span data-ttu-id="8fa0f-192">[Zasoby](../azure-resource-manager/resource-group-authoring-templates.md#resources) zdefiniuj hello różne zasoby, które zainstaluje i skonfiguruje rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define hello different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="8fa0f-193">Są to hello największy i najbardziej złożonych część hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-193">This will be hello largest and most complex portion of hello template.</span></span>  <span data-ttu-id="8fa0f-194">Można uzyskać hello struktury i pełny opis elementów zasobów w [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="8fa0f-194">You can get hello structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="8fa0f-195">Różne zasoby zdefiniowane przez użytkownika będzie zazwyczaj są wyszczególnione w inne artykuły w tej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="8fa0f-196">Zależności</span><span class="sxs-lookup"><span data-stu-id="8fa0f-196">Dependencies</span></span>
<span data-ttu-id="8fa0f-197">Witaj **dependsOn** określa elementy [zależności](../azure-resource-manager/resource-group-define-dependencies.md) na inny zasób.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-197">hello **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="8fa0f-198">Po zainstalowaniu rozwiązania hello zasób nie został utworzony, dopóki wszystkie jego zależności zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-198">When hello solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="8fa0f-199">Na przykład może rozwiązania [uruchomienia elementu runbook](operations-management-suite-solutions-resources-automation.md#runbooks) po zainstalowaniu przy użyciu [zadania zasobu](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="8fa0f-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="8fa0f-200">Hello zasobów zadania będzie zależna od hello runbook zasobów toomake się, że ten element runbook hello został utworzony przed utworzeniem hello zadania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-200">hello job resource would be dependent on hello runbook resource toomake sure that hello runbook is created before hello job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="8fa0f-201">Obszar roboczy OMS i konta automatyzacji</span><span class="sxs-lookup"><span data-stu-id="8fa0f-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="8fa0f-202">Rozwiązania do zarządzania wymagają [obszarem roboczym pakietu OMS](../log-analytics/log-analytics-manage-access.md) toocontain widoki i [konto automatyzacji](../automation/automation-security-overview.md#automation-account-overview) toocontain elementów runbook i powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span>  <span data-ttu-id="8fa0f-203">Muszą być dostępne przed hello zasobów w rozwiązaniu hello są tworzone i nie powinna być zdefiniowana w rozwiązaniu hello do samej siebie.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-203">These must be available before hello resources in hello solution are created and should not be defined in hello solution itself.</span></span>  <span data-ttu-id="8fa0f-204">Witaj użytkownika będzie [Określ obszar roboczy i konta](operations-management-suite-solutions.md#oms-workspace-and-automation-account) podczas ich wdrażania rozwiązania, ale jako autor hello należy rozważyć następujące punkty hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-204">hello user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as hello author you should consider hello following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="8fa0f-205">Rozwiązanie zasobów</span><span class="sxs-lookup"><span data-stu-id="8fa0f-205">Solution resource</span></span>
<span data-ttu-id="8fa0f-206">Każde rozwiązanie wymaga zapisu zasobów w hello **zasobów** element, który definiuje rozwiązania hello, sama.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-206">Each solution requires a resource entry in hello **resources** element that defines hello solution itself.</span></span>  <span data-ttu-id="8fa0f-207">Będzie to mieć typu **Microsoft.OperationsManagement/solutions** i mieć hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have hello following structure.</span></span> <span data-ttu-id="8fa0f-208">Obejmuje to [standardowe parametry](#parameters) i [zmienne](#variables) które są najczęściej używanymi toodefine właściwości hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used toodefine properties of hello solution.</span></span>


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a><span data-ttu-id="8fa0f-209">Zależności</span><span class="sxs-lookup"><span data-stu-id="8fa0f-209">Dependencies</span></span>
<span data-ttu-id="8fa0f-210">Hello rozwiązania zasobu musi mieć [zależności](../azure-resource-manager/resource-group-define-dependencies.md) na wszystkich innych zasobów w rozwiązaniu hello ponieważ potrzebują tooexist, aby można było utworzyć rozwiązanie hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-210">hello solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in hello solution since they need tooexist before hello solution can be created.</span></span>  <span data-ttu-id="8fa0f-211">Możesz to zrobić przez dodanie wpisu dla każdego zasobu hello **dependsOn** elementu.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-211">You do this by adding an entry for each resource in hello **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="8fa0f-212">Właściwości</span><span class="sxs-lookup"><span data-stu-id="8fa0f-212">Properties</span></span>
<span data-ttu-id="8fa0f-213">Witaj rozwiązania zasób ma właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-213">hello solution resource has hello properties in hello following table.</span></span>  <span data-ttu-id="8fa0f-214">Obejmują one zasoby hello przywoływany i zawarty w hello rozwiązania, który definiuje sposób zarządzania zasobów powitania po zainstalowaniu hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-214">This includes hello resources referenced and contained by hello solution which defines how hello resource is managed after hello solution is installed.</span></span>  <span data-ttu-id="8fa0f-215">Każdy zasób w rozwiązaniu hello powinien być wyświetlany w obu hello **referencedResources** lub hello **containedResources** właściwości.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-215">Each resource in hello solution should be listed in either hello **referencedResources** or hello **containedResources** property.</span></span>

| <span data-ttu-id="8fa0f-216">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8fa0f-216">Property</span></span> | <span data-ttu-id="8fa0f-217">Opis</span><span class="sxs-lookup"><span data-stu-id="8fa0f-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8fa0f-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="8fa0f-218">workspaceResourceId</span></span> |<span data-ttu-id="8fa0f-219">Identyfikator obszaru roboczego analizy dzienników hello w postaci hello  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<nazwa obszaru roboczego\>*.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-219">ID of hello Log Analytics workspace in hello form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="8fa0f-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="8fa0f-220">referencedResources</span></span> |<span data-ttu-id="8fa0f-221">Lista zasobów w rozwiązaniu hello, która nie powinna zostać usunięta po usunięciu hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-221">List of resources in hello solution that should not be removed when hello solution is removed.</span></span> |
| <span data-ttu-id="8fa0f-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="8fa0f-222">containedResources</span></span> |<span data-ttu-id="8fa0f-223">Lista zasobów w rozwiązaniu hello, która powinna zostać usunięta po usunięciu hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-223">List of resources in hello solution that should be removed when hello solution is removed.</span></span> |

<span data-ttu-id="8fa0f-224">w powyższym przykładzie Hello jest rozwiązania z elementu runbook, harmonogram i widoku.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-224">hello example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="8fa0f-225">Harmonogram Hello i runbook są *przywoływanego* w hello **właściwości** elementu, więc nie zostaną usunięte po usunięciu hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-225">hello schedule and runbook are *referenced* in hello  **properties**  element so they are not removed when hello solution is removed.</span></span>  <span data-ttu-id="8fa0f-226">Widok Hello jest *zawarte* , zostanie ono usunięte po usunięciu hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-226">hello view is *contained* so it is removed when hello solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="8fa0f-227">Planowanie</span><span class="sxs-lookup"><span data-stu-id="8fa0f-227">Plan</span></span>
<span data-ttu-id="8fa0f-228">Witaj **planu** jednostki hello rozwiązania zasobu ma właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-228">hello **plan** entity of hello solution resource has hello properties in hello following table.</span></span>

| <span data-ttu-id="8fa0f-229">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8fa0f-229">Property</span></span> | <span data-ttu-id="8fa0f-230">Opis</span><span class="sxs-lookup"><span data-stu-id="8fa0f-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8fa0f-231">name</span><span class="sxs-lookup"><span data-stu-id="8fa0f-231">name</span></span> |<span data-ttu-id="8fa0f-232">Nazwa rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-232">Name of hello solution.</span></span> |
| <span data-ttu-id="8fa0f-233">Wersja</span><span class="sxs-lookup"><span data-stu-id="8fa0f-233">version</span></span> |<span data-ttu-id="8fa0f-234">Wersja rozwiązania hello zgodnie z ustaleniami hello autora.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-234">Version of hello solution as determined by hello author.</span></span> |
| <span data-ttu-id="8fa0f-235">Produktu</span><span class="sxs-lookup"><span data-stu-id="8fa0f-235">product</span></span> |<span data-ttu-id="8fa0f-236">Rozwiązanie hello tooidentify unikatowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-236">Unique string tooidentify hello solution.</span></span> |
| <span data-ttu-id="8fa0f-237">Wydawcy</span><span class="sxs-lookup"><span data-stu-id="8fa0f-237">publisher</span></span> |<span data-ttu-id="8fa0f-238">Wydawca hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-238">Publisher of hello solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="8fa0f-239">Przykład</span><span class="sxs-lookup"><span data-stu-id="8fa0f-239">Sample</span></span>
<span data-ttu-id="8fa0f-240">Przykłady pliki rozwiązania z zasobem rozwiązania można przejrzeć hello następujących lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-240">You can view samples of solution files with a solution resource at hello following locations.</span></span>

- [<span data-ttu-id="8fa0f-241">Zasoby do automatyzacji</span><span class="sxs-lookup"><span data-stu-id="8fa0f-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="8fa0f-242">Zasoby wyszukiwania i alertów</span><span class="sxs-lookup"><span data-stu-id="8fa0f-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="8fa0f-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8fa0f-243">Next steps</span></span>
* <span data-ttu-id="8fa0f-244">[Dodaj zapisanych wyszukiwań i alerty](operations-management-suite-solutions-resources-searches-alerts.md) tooyour rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) tooyour management solution.</span></span>
* <span data-ttu-id="8fa0f-245">[Dodawanie widoków](operations-management-suite-solutions-resources-views.md) tooyour rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-245">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="8fa0f-246">[Dodawanie elementów runbook i innych zasobów automatyzacji](operations-management-suite-solutions-resources-automation.md) tooyour rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>
* <span data-ttu-id="8fa0f-247">Szczegóły dotyczące hello [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8fa0f-247">Learn hello details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8fa0f-248">Wyszukiwanie [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates) przykłady różnych szablonów usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8fa0f-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
