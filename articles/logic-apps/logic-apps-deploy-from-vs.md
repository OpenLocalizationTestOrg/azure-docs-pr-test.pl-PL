---
title: "aaaCreate, tworzenie i wdrażanie aplikacji logiki w Visual Studio — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie projektów programu Visual Studio, projektowanie, tworzenie i wdrażanie usługi Azure Logic Apps."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="e85ea-103">Projektowanie, tworzenie i wdrażanie usługi Azure Logic Apps w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e85ea-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="e85ea-104">Mimo że hello [portalu Azure](https://portal.azure.com/) zapewnia to dobry sposób możesz toocreate i zarządzania usługi Azure Logic Apps, można użyć programu Visual Studio umożliwiające projektowanie, tworzenie i wdrażanie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e85ea-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toocreate and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="e85ea-105">Program Visual Studio udostępnia zaawansowane narzędzia, takie jak hello projektanta aplikacji logiki dla Ciebie aplikacje logiki toocreate, konfigurować szablony wdrażania i automatyzacji i wdrażania tooany środowiska.</span><span class="sxs-lookup"><span data-stu-id="e85ea-105">Visual Studio provides rich tools like hello Logic App Designer for you toocreate logic apps, configure deployment and automation templates, and deploy tooany environment.</span></span> 

<span data-ttu-id="e85ea-106">Dowiedz się tooget wprowadzenie do usługi Azure Logic Apps [jak toocreate pierwszej aplikacji logiki w portalu Azure hello](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e85ea-106">tooget started with Azure Logic Apps, learn [how toocreate your first logic app in hello Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="e85ea-107">Kroki instalacji</span><span class="sxs-lookup"><span data-stu-id="e85ea-107">Installation steps</span></span>

<span data-ttu-id="e85ea-108">tooinstall i Konfigurowanie narzędzi Visual Studio tools for Azure Logic Apps, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="e85ea-108">tooinstall and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e85ea-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e85ea-109">Prerequisites</span></span>

* <span data-ttu-id="e85ea-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) lub programu Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e85ea-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="e85ea-111">[Najnowszy zestaw Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 lub nowszej)</span><span class="sxs-lookup"><span data-stu-id="e85ea-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="e85ea-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e85ea-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="e85ea-113">Access toohello w sieci web używając projektanta osadzonych hello</span><span class="sxs-lookup"><span data-stu-id="e85ea-113">Access toohello web when using hello embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="e85ea-114">Instalowanie narzędzi Visual Studio tools for Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e85ea-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="e85ea-115">Po zainstalowaniu wymagań wstępnych hello:</span><span class="sxs-lookup"><span data-stu-id="e85ea-115">After you install hello prerequisites:</span></span>

1. <span data-ttu-id="e85ea-116">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e85ea-116">Open Visual Studio.</span></span> <span data-ttu-id="e85ea-117">Na powitania **narzędzia** menu, wybierz opcję **rozszerzenia i aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-117">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="e85ea-118">Rozwiń węzeł hello **Online** kategorii można wyszukiwać w tryb online.</span><span class="sxs-lookup"><span data-stu-id="e85ea-118">Expand hello **Online** category so you can search online.</span></span>
3. <span data-ttu-id="e85ea-119">Wyszukaj **Logic Apps** do momentu znalezienia **Azure Logic Apps Tools for Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="e85ea-120">toodownload i rozszerzenie hello instalacji, kliknij przycisk **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-120">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="e85ea-121">Po zakończeniu instalacji uruchom ponownie program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e85ea-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="e85ea-122">Możesz również pobrać [narzędzia aplikacje logiki platformy Azure dla programu Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) i hello [narzędzia aplikacje logiki platformy Azure dla programu Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) bezpośrednio z hello Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e85ea-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and hello [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from hello Visual Studio Marketplace.</span></span>

<span data-ttu-id="e85ea-123">Po zakończeniu instalacji, używając hello projektu grupy zasobów platformy Azure za pomocą projektanta aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e85ea-123">After you finish installation, you can use hello Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="e85ea-124">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="e85ea-124">Create your project</span></span>

1. <span data-ttu-id="e85ea-125">Na powitania **pliku** menu przejść za**nowy**i wybierz **projektu**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-125">On hello **File** menu, go too**New**, and select **Project**.</span></span> <span data-ttu-id="e85ea-126">Lub tooadd Twojego tooan projektu zbyt istniejącego rozwiązania, przejdź**Dodaj**i wybierz **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-126">Or tooadd your project tooan existing solution, go too**Add**, and select **New Project**.</span></span>

    ![Menu Plik](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="e85ea-128">W hello **nowy projekt** oknie Znajdź **chmury**i wybierz **grupy zasobów platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-128">In hello **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="e85ea-129">Nazwij swój projekt, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-129">Name your project, and click **OK**.</span></span>

    ![Dodaj nowy projekt](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="e85ea-131">Wybierz hello **aplikacji logiki** szablonu, który utworzy szablon wdrażania aplikacji logiki puste toouse.</span><span class="sxs-lookup"><span data-stu-id="e85ea-131">Select hello **Logic App** template, which creates a blank logic app deployment template for you toouse.</span></span> <span data-ttu-id="e85ea-132">Po wybraniu szablonu, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-132">After you select your template, click **OK**.</span></span>

    ![Wybierz szablon aplikacji logiki](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="e85ea-134">Teraz dodane rozwiązania tooyour projektu aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e85ea-134">You've now added your logic app project tooyour solution.</span></span> 
    <span data-ttu-id="e85ea-135">W Eksploratorze rozwiązań hello powinna zostać wyświetlona pliku wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e85ea-135">In hello Solution Explorer, your deployment file should appear.</span></span>

    ![Plik wdrożenia](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="e85ea-137">Tworzenie aplikacji logiki z projektanta aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="e85ea-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="e85ea-138">Jeśli projekt grupy zasobów platformy Azure, który zawiera aplikację logiki, możesz otworzyć hello projektanta aplikacji logiki w Visual Studio toocreate przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="e85ea-138">When you have an Azure Resource Group project that contains a logic app, you can open hello Logic App Designer in Visual Studio toocreate your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="e85ea-139">Projektant Hello wymaga połączenia internetowego za zapytania łączniki dla danych i dostępnych właściwości.</span><span class="sxs-lookup"><span data-stu-id="e85ea-139">hello designer requires an internet connection too query connectors for available properties and data.</span></span> <span data-ttu-id="e85ea-140">Na przykład jeśli używany jest łącznik usługi Dynamics CRM Online hello, hello projektanta zapytań programu CRM wystąpienia tooshow dostępne niestandardowe i domyślne właściwości.</span><span class="sxs-lookup"><span data-stu-id="e85ea-140">For example, if you use hello Dynamics CRM Online connector, hello designer queries your CRM instance tooshow available custom and default properties.</span></span>

1. <span data-ttu-id="e85ea-141">Kliknij prawym przyciskiem myszy użytkownika `<template>.json` pliku, a następnie wybierz **Otwórz w Projektancie aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="e85ea-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="e85ea-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="e85ea-143">Wybierz subskrypcję platformy Azure, grupy zasobów i lokalizacji szablonu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e85ea-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e85ea-144">Projektowanie aplikacji logiki tworzy połączenie z interfejsem API zasobów zapytania dla właściwości podczas projektowania.</span><span class="sxs-lookup"><span data-stu-id="e85ea-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="e85ea-145">Visual Studio będzie korzystać z wybranego zasobu grupy toocreate te połączenia w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="e85ea-145">Visual Studio uses your selected resource group toocreate those connections during design time.</span></span> <span data-ttu-id="e85ea-146">tooview lub Zmień wszystkie połączenia interfejsu API, przejdź toohello portalu Azure i Przeglądaj w poszukiwaniu **połączenia interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-146">tooview or change any API Connections, go toohello Azure portal, and browse for **API Connections**.</span></span>

    ![Selektor subskrypcji](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="e85ea-148">Projektant Hello używa definicji hello hello `<template>.json` pliku do renderowania.</span><span class="sxs-lookup"><span data-stu-id="e85ea-148">hello designer uses hello definition in hello `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="e85ea-149">Tworzenie i projektowanie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e85ea-149">Create and design your logic app.</span></span> <span data-ttu-id="e85ea-150">Szablon wdrożenia zostanie zaktualizowany z wprowadzonymi zmianami.</span><span class="sxs-lookup"><span data-stu-id="e85ea-150">Your deployment template is updated with your changes.</span></span>

    ![Projektant aplikacji logiki w programie Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="e85ea-152">Dodaje programu Visual Studio `Microsoft.Web/connections` zbyt zasobu pliku zasobów dla połączeń toofunction wymaga aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e85ea-152">Visual Studio adds `Microsoft.Web/connections` resources too your resource file for any connections your logic app needs toofunction.</span></span> <span data-ttu-id="e85ea-153">Te właściwości połączenia można ustawić podczas wdrażania i zarządzania po wdrożeniu w **połączenia interfejsu API** w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e85ea-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in hello Azure portal.</span></span>

### <a name="switch-toojson-code-view"></a><span data-ttu-id="e85ea-154">Przełącz do widoku kodu tooJSON</span><span class="sxs-lookup"><span data-stu-id="e85ea-154">Switch tooJSON code view</span></span>

<span data-ttu-id="e85ea-155">Witaj tooshow reprezentacja JSON aplikacji logiki, wybierz hello **widoku kodu** u dołu hello hello projektanta.</span><span class="sxs-lookup"><span data-stu-id="e85ea-155">tooshow hello JSON representation for your logic app, select hello **Code View** tab at hello bottom of hello designer.</span></span>

<span data-ttu-id="e85ea-156">tooswitch trybu toohello zasobów pełna JSON, kliknij prawym przyciskiem myszy hello `<template>.json` pliku, a następnie wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-156">tooswitch back toohello full resource JSON, right-click hello `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a><span data-ttu-id="e85ea-157">Dodaj odwołania do zasobów zależnych tooVisual Studio wdrażania szablonów</span><span class="sxs-lookup"><span data-stu-id="e85ea-157">Add references for dependent resources tooVisual Studio deployment templates</span></span>

<span data-ttu-id="e85ea-158">Należy zasobów zależnych tooreference logikę aplikacji, można użyć [funkcje szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) w szablonie wdrożenia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e85ea-158">When you want your logic app tooreference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="e85ea-159">Na przykład można Twojej tooreference aplikacji logiki konta funkcji platformy Azure lub integracji, które mają toodeploy równolegle z aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e85ea-159">For example, you might want your logic app tooreference an Azure Function or integration account that you want toodeploy alongside your logic app.</span></span> <span data-ttu-id="e85ea-160">Wykonaj te wskazówki dotyczące jak parametry toouse w szablonie wdrożenia, który hello projektanta aplikacji logiki renderuje poprawnie.</span><span class="sxs-lookup"><span data-stu-id="e85ea-160">Follow these guidelines about how toouse parameters in your deployment template so that hello Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="e85ea-161">Można używać parametrów aplikacji logiki w rodzaju wyzwalacze i akcje:</span><span class="sxs-lookup"><span data-stu-id="e85ea-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="e85ea-162">Podrzędny przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="e85ea-162">Child workflow</span></span>
*   <span data-ttu-id="e85ea-163">Funkcja aplikacji</span><span class="sxs-lookup"><span data-stu-id="e85ea-163">Function app</span></span>
*   <span data-ttu-id="e85ea-164">Wywołanie APIM</span><span class="sxs-lookup"><span data-stu-id="e85ea-164">APIM call</span></span>
*   <span data-ttu-id="e85ea-165">Adres URL wykonywania połączenia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e85ea-165">API connection runtime URL</span></span>
*   <span data-ttu-id="e85ea-166">Ścieżka połączenia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e85ea-166">API connection path</span></span>

<span data-ttu-id="e85ea-167">I możesz użyć funkcji szablonu, takie jak parametry, zmienne, resourceId, concat itp. Na przykład Oto jak można zastąpić identyfikator zasobu hello funkcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="e85ea-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace hello Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="e85ea-168">I użycia parametrów:</span><span class="sxs-lookup"><span data-stu-id="e85ea-168">And where you would use parameters:</span></span>

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
<span data-ttu-id="e85ea-169">Innym przykładem mogą parametryzacja hello komunikat operacji wysyłania usługi Service Bus:</span><span class="sxs-lookup"><span data-stu-id="e85ea-169">As another example you can parameterize hello Service Bus send message operation:</span></span>

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> <span data-ttu-id="e85ea-170">host.runtimeUrl jest opcjonalny i może być usunięty z szablonu, jeśli jest obecny.</span><span class="sxs-lookup"><span data-stu-id="e85ea-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="e85ea-171">Dla toowork projektanta aplikacji logiki hello użycia parametrów, należy podać wartości domyślnych, na przykład:</span><span class="sxs-lookup"><span data-stu-id="e85ea-171">For hello Logic App Designer toowork when you use parameters, you must provide default values, for example:</span></span>
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a><span data-ttu-id="e85ea-172">Zapisywanie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="e85ea-172">Save your logic app</span></span>

<span data-ttu-id="e85ea-173">toosave aplikację logiki w dowolnym momencie, przejdź zbyt**pliku** > **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-173">toosave your logic app at anytime, go too**File** > **Save**.</span></span> <span data-ttu-id="e85ea-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="e85ea-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="e85ea-175">Jeśli aplikację logiki ma błędy podczas zapisywania aplikacji, pojawią się one w Visual Studio hello **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="e85ea-175">If your logic app has any errors when you save your app, they appear in hello Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="e85ea-176">Wdrażanie aplikacji logiki w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e85ea-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="e85ea-177">Po skonfigurowaniu aplikacji, można wdrożyć bezpośrednio z programu Visual Studio w zaledwie kilku krokach.</span><span class="sxs-lookup"><span data-stu-id="e85ea-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="e85ea-178">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i przejść za**Wdróż** > **nowego wdrożenia...**</span><span class="sxs-lookup"><span data-stu-id="e85ea-178">In Solution Explorer, right-click your project, and go too**Deploy** > **New Deployment...**</span></span>

    ![Nowe wdrożenie](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="e85ea-180">Po wyświetleniu monitu zaloguj się tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e85ea-180">When you're prompted, sign in tooyour Azure subscription.</span></span> 

3. <span data-ttu-id="e85ea-181">Teraz musisz wybrać szczegóły hello grupy zasobów hello miejscu toodeploy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e85ea-181">Now you must select hello details for hello resource group where you want toodeploy your logic app.</span></span> <span data-ttu-id="e85ea-182">Gdy wszystko będzie gotowe, wybierz **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e85ea-183">Upewnij się, wybierz opcję hello prawidłowego szablonu i pliku parametrów hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e85ea-183">Make sure that you select hello correct template and parameters file for hello resource group.</span></span> <span data-ttu-id="e85ea-184">Na przykład środowiska produkcyjnego tooa toodeploy należy wybrać pliku parametrów hello produkcji.</span><span class="sxs-lookup"><span data-stu-id="e85ea-184">For example, if you want toodeploy tooa production environment, choose hello production parameters file.</span></span>

    ![Wdrożenie grupy tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="e85ea-186">Stan wdrożenia Hello jest wyświetlany w hello **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="e85ea-186">hello deployment status appears in hello **Output** window.</span></span> 
    <span data-ttu-id="e85ea-187">Może być tooselect **inicjowania obsługi usługi Azure** w hello **Pokaż dane wyjściowe z** listy.</span><span class="sxs-lookup"><span data-stu-id="e85ea-187">You might have tooselect **Azure Provisioning** in hello **Show output from** list.</span></span>

    ![Dane wyjściowe stanu wdrożenia](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="e85ea-189">W przyszłości hello można edytować aplikację logiki w kontroli źródła i użyj programu Visual Studio toodeploy nowe wersje.</span><span class="sxs-lookup"><span data-stu-id="e85ea-189">In hello future, you can edit your logic app in source control, and use Visual Studio toodeploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="e85ea-190">W przypadku zmiany definicji hello w portalu Azure hello bezpośrednio te zmiany zostaną zastąpione podczas wdrażania w programie Visual Studio następnym razem.</span><span class="sxs-lookup"><span data-stu-id="e85ea-190">If you change hello definition in hello Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a><span data-ttu-id="e85ea-191">Dodawanie logiki aplikacji tooan istniejącej grupy zasobów projektu</span><span class="sxs-lookup"><span data-stu-id="e85ea-191">Add your logic app tooan existing Resource Group project</span></span>

<span data-ttu-id="e85ea-192">Jeśli masz istniejący projekt grupy zasobów, można dodać projektu toothat logiki aplikacji hello okna konspekt pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="e85ea-192">If you have an existing Resource Group project, you can add your logic app toothat project in hello JSON Outline window.</span></span> <span data-ttu-id="e85ea-193">Można również dodać inną aplikację logiki obok aplikacji hello, utworzonych wcześniej.</span><span class="sxs-lookup"><span data-stu-id="e85ea-193">You can also add another logic app alongside hello app you previously created.</span></span>

1. <span data-ttu-id="e85ea-194">Otwórz hello `<template>.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="e85ea-194">Open hello `<template>.json` file.</span></span>

2. <span data-ttu-id="e85ea-195">tooopen hello okna konspekt pliku JSON, przejdź zbyt**widoku** > **inne okna** > **konspekt pliku JSON**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-195">tooopen hello JSON Outline window, go too**View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="e85ea-196">Kliknij tooadd plik zasobów toohello szablonu **dodawania zasobów** u góry okna konspekt pliku JSON hello hello.</span><span class="sxs-lookup"><span data-stu-id="e85ea-196">tooadd a resource toohello template file, click **Add Resource** at hello top of hello JSON Outline window.</span></span> <span data-ttu-id="e85ea-197">Witaj okna konspekt pliku JSON, kliknij prawym przyciskiem myszy **zasobów**i wybierz **Dodaj nowy zasób**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-197">Or in hello JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![Okna konspekt pliku JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="e85ea-199">W hello **dodawania zasobów** okno dialogowe, Znajdź i wybierz **aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-199">In hello **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="e85ea-200">Określ nazwę aplikacji logiki, a następnie wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="e85ea-200">Name your logic app, and choose **Add**.</span></span>

    ![Dodaj zasób](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="e85ea-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e85ea-202">Next Steps</span></span>

* [<span data-ttu-id="e85ea-203">Zarządzanie logiki aplikacji za pomocą programu Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="e85ea-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="e85ea-204">Wyświetlanie typowych przykładów i scenariuszy</span><span class="sxs-lookup"><span data-stu-id="e85ea-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="e85ea-205">Dowiedz się, jak przetwarza tooautomate firm z usługą Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e85ea-205">Learn how tooautomate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="e85ea-206">Dowiedz się, jak toointegrate systemy z usługą Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e85ea-206">Learn how toointegrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
