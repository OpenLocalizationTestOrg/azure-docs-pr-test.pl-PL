---
title: "aaaViews w rozwiązaniach do zarządzania Operations Management Suite (OMS) | Dokumentacja firmy Microsoft"
description: "Rozwiązania do zarządzania w Operations Management Suite (OMS) zwykle zawiera jeden lub więcej danych toovisualize widoków.  W tym artykule opisano, jak tooexport widok tworzony przez hello Widok projektanta i dołączyć go w rozwiązaniu do zarządzania. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="f5c91-104">Widoki w rozwiązaniach do zarządzania Operations Management Suite (OMS) (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="f5c91-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="f5c91-105">To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="f5c91-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="f5c91-106">Żadnego schematu opisanych poniżej jest toochange podmiotu.</span><span class="sxs-lookup"><span data-stu-id="f5c91-106">Any schema described below is subject toochange.</span></span>    
>
>

<span data-ttu-id="f5c91-107">[Rozwiązania do zarządzania w Operations Management Suite (OMS)](operations-management-suite-solutions.md) zwykle zawiera co najmniej jeden danych toovisualize widoków.</span><span class="sxs-lookup"><span data-stu-id="f5c91-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views toovisualize data.</span></span>  <span data-ttu-id="f5c91-108">W tym artykule opisano, jak tooexport widok tworzony przez hello [Widok projektanta](../log-analytics/log-analytics-view-designer.md) i uwzględnić go w rozwiązaniu do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f5c91-108">This article describes how tooexport a view created by hello [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="f5c91-109">cześć przykłady w tym artykule Użyj parametry i zmienne, które są albo toomanagement wymagane lub typowych rozwiązań i opisane w [tworzenia rozwiązań do zarządzania w Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="f5c91-109">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="f5c91-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f5c91-110">Prerequisites</span></span>
<span data-ttu-id="f5c91-111">W tym artykule przyjęto założenie, że znasz już jak zbyt[tworzenie rozwiązania do zarządzania](operations-management-suite-solutions-creating.md) i hello struktury pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f5c91-111">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="f5c91-112">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f5c91-112">Overview</span></span>
<span data-ttu-id="f5c91-113">tooinclude widoku w rozwiązaniu do zarządzania, tworzenia **zasobów** dla niego w hello [plik rozwiązania](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="f5c91-113">tooinclude a view in a management solution, you create a **resource** for it in hello [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="f5c91-114">Hello dane JSON, które opisano konfigurację szczegółowy widok hello jest zwykle złożone jednak i nie coś że autor rozwiązania typowych ręcznie będą mogli toocreate.</span><span class="sxs-lookup"><span data-stu-id="f5c91-114">hello JSON that describes hello view's detailed configuration is typically complex though and not something that a typical solution author would be able toocreate manually.</span></span>  <span data-ttu-id="f5c91-115">Witaj najczęściej spotykaną metodą jest toocreate hello widoku przy użyciu hello [Widok projektanta](../log-analytics/log-analytics-view-designer.md), go wyeksportować, a następnie Dodaj rozwiązanie toohello szczegółową konfigurację.</span><span class="sxs-lookup"><span data-stu-id="f5c91-115">hello most common method is toocreate hello view using hello [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration toohello solution.</span></span>

<span data-ttu-id="f5c91-116">dostępne są następujące Hello tooadd podstawowe kroki rozwiązania tooa widoku.</span><span class="sxs-lookup"><span data-stu-id="f5c91-116">hello basic steps tooadd a view tooa solution are as follows.</span></span>  <span data-ttu-id="f5c91-117">Każdy krok jest opisany bardziej szczegółowo w poniższych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="f5c91-117">Each step is described in further detail in hello sections below.</span></span>

1. <span data-ttu-id="f5c91-118">Eksportuj plik tooa widoku hello.</span><span class="sxs-lookup"><span data-stu-id="f5c91-118">Export hello view tooa file.</span></span>
2. <span data-ttu-id="f5c91-119">Utwórz zasób widoku hello w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="f5c91-119">Create hello view resource in hello solution.</span></span>
3. <span data-ttu-id="f5c91-120">Dodawanie hello widoku szczegółów.</span><span class="sxs-lookup"><span data-stu-id="f5c91-120">Add hello view details.</span></span>

## <a name="export-hello-view-tooa-file"></a><span data-ttu-id="f5c91-121">Eksportuj plik tooa widoku hello</span><span class="sxs-lookup"><span data-stu-id="f5c91-121">Export hello view tooa file</span></span>
<span data-ttu-id="f5c91-122">Postępuj zgodnie z instrukcjami hello w [Projektant widoków analizy dziennika](../log-analytics/log-analytics-view-designer.md) tooexport plik tooa widoku.</span><span class="sxs-lookup"><span data-stu-id="f5c91-122">Follow hello instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) tooexport a view tooa file.</span></span>  <span data-ttu-id="f5c91-123">Witaj wyeksportowany plik będzie można w formacie JSON z hello sam [elementów jako plik rozwiązania hello](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="f5c91-123">hello exported file will be in JSON format with hello same [elements as hello solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="f5c91-124">Witaj **zasobów** element hello widoku pliku będzie mieć zasobu o typie **Microsoft.OperationalInsights/workspaces** czy reprezentuje hello obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="f5c91-124">hello **resources** element of hello view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents hello OMS workspace.</span></span>  <span data-ttu-id="f5c91-125">Ten element będzie mieć podelement typu **widoków** który reprezentuje widok hello i zawiera szczegółowe konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f5c91-125">This element will have a subelement with a type of **views** that represents hello view and contains its detailed configuration.</span></span>  <span data-ttu-id="f5c91-126">Zostanie Kopiuj szczegóły hello tego elementu, a następnie skopiować go do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f5c91-126">You will copy hello details of this element and then copy it into your solution.</span></span>

## <a name="create-hello-view-resource-in-hello-solution"></a><span data-ttu-id="f5c91-127">Utwórz zasób widoku hello w rozwiązaniu hello</span><span class="sxs-lookup"><span data-stu-id="f5c91-127">Create hello view resource in hello solution</span></span>
<span data-ttu-id="f5c91-128">Dodaj powitania po widok zasobów toohello **zasobów** element pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f5c91-128">Add hello following view resource toohello **resources** element of your solution file.</span></span>  <span data-ttu-id="f5c91-129">Używa zmiennych, które są opisane poniżej, że należy również dodać.</span><span class="sxs-lookup"><span data-stu-id="f5c91-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="f5c91-130">Należy pamiętać, że hello **pulpitu nawigacyjnego** i **OverviewTile** właściwości symboli zastępczych, które spowoduje zastąpienie hello odpowiednie właściwości z hello widoku eksportowanego pliku.</span><span class="sxs-lookup"><span data-stu-id="f5c91-130">Note that hello **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with hello corresponding properties from hello exported view file.</span></span>

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

<span data-ttu-id="f5c91-131">Dodaj następujące zmienne toohello zmienne element pliku rozwiązania hello hello i Zastąp hello toothose wartości dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f5c91-131">Add hello following variables toohello variables element of hello solution file and replace hello values toothose for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


<span data-ttu-id="f5c91-132">Zauważ, że hello całego widoku zasobów można skopiować z widoku wyeksportowanego pliku, który będzie potrzebny hello toomake następujące zmiany dla niego toowork w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="f5c91-132">Note that you could copy hello entire view resource from your exported view file, but you would need toomake hello following changes for it toowork in your solution.</span></span>  

* <span data-ttu-id="f5c91-133">Witaj **typu** dla widoku hello zasobu musi toobe zmieniła się z **widoków** za**Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="f5c91-133">hello **type** for hello view resource needs toobe changed from **views** too**Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="f5c91-134">Witaj **nazwa** właściwości dla zasobu widoku hello wymaga nazwy obszaru roboczego hello tooinclude toobe zmienione.</span><span class="sxs-lookup"><span data-stu-id="f5c91-134">hello **name** property for hello view resource needs toobe changed tooinclude hello workspace name.</span></span>
* <span data-ttu-id="f5c91-135">zależności Hello w obszarze roboczym hello musi usunąć, ponieważ hello obszaru roboczego zasobu nie jest zdefiniowany w rozwiązaniu hello toobe.</span><span class="sxs-lookup"><span data-stu-id="f5c91-135">hello dependency on hello workspace needs toobe removed since hello workspace resource isn't defined in hello solution.</span></span>
* <span data-ttu-id="f5c91-136">**Nazwa wyświetlana** właściwości toobe potrzeb dodane toohello widoku.</span><span class="sxs-lookup"><span data-stu-id="f5c91-136">**DisplayName** property needs toobe added toohello view.</span></span>  <span data-ttu-id="f5c91-137">Witaj **identyfikator**, **nazwa**, i **DisplayName** musi wszystkie zgodne.</span><span class="sxs-lookup"><span data-stu-id="f5c91-137">hello **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="f5c91-138">Należy zmienić nazwy parametrów toomatch hello wymagany zestaw parametrów.</span><span class="sxs-lookup"><span data-stu-id="f5c91-138">Parameter names must be changed toomatch hello required set of parameters.</span></span>
* <span data-ttu-id="f5c91-139">Zmienne należy określić w rozwiązaniu hello i używane w hello odpowiednie właściwości.</span><span class="sxs-lookup"><span data-stu-id="f5c91-139">Variables should be defined in hello solution and used in hello appropriate properties.</span></span>

## <a name="add-hello-view-details"></a><span data-ttu-id="f5c91-140">Dodawanie hello widoku szczegółów</span><span class="sxs-lookup"><span data-stu-id="f5c91-140">Add hello view details</span></span>
<span data-ttu-id="f5c91-141">Hello widok zasobów w hello wyeksportowany plik zawiera dwa elementy w hello widoku **właściwości** elementu o nazwie **pulpitu nawigacyjnego** i **OverviewTile** zawierających hello szczegółową konfigurację hello widoku.</span><span class="sxs-lookup"><span data-stu-id="f5c91-141">hello view resource in hello exported view file will contain two elements in hello **properties** element named **Dashboard** and **OverviewTile** which contain hello detailed configuration of hello view.</span></span>  <span data-ttu-id="f5c91-142">Skopiuj następujące dwa elementy i ich zawartość do hello **właściwości** elementu hello widok zasobów w pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f5c91-142">Copy these two elements and their contents into hello **properties** element of hello view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="f5c91-143">Przykład</span><span class="sxs-lookup"><span data-stu-id="f5c91-143">Example</span></span>
<span data-ttu-id="f5c91-144">Na przykład następujące przykładowe hello przedstawiono plik prostym rozwiązaniem z widokiem.</span><span class="sxs-lookup"><span data-stu-id="f5c91-144">For example, hello following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="f5c91-145">Wielokropek (...) są wyświetlane dla hello **pulpitu nawigacyjnego** i **OverviewTile** zawartość ze względów miejsca.</span><span class="sxs-lookup"><span data-stu-id="f5c91-145">Ellipses (...) are shown for hello **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a><span data-ttu-id="f5c91-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f5c91-146">Next steps</span></span>
* <span data-ttu-id="f5c91-147">Dowiedz się, szczegółowe informacje dotyczące tworzenia [rozwiązań do zarządzania](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="f5c91-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="f5c91-148">Obejmują [elementu runbook usługi Automatyzacja w ramach rozwiązania do zarządzania](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="f5c91-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
