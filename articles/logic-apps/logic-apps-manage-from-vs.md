---
title: "aplikacje logiki aaaManage w programie Visual Studio — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Zarządzanie logiki aplikacji i innych zasobów platformy Azure z programu Visual Studio Cloud Explorer"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="6b7b8-103">Zarządzanie aplikacjami logiki za pomocą programu Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="6b7b8-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="6b7b8-104">Mimo że hello [portalu Azure](https://portal.azure.com/) zapewnia to dobry sposób możesz toodesign i zarządzać aplikacje logiki platformy Azure, programu Visual Studio Cloud Explorer można użyć do zarządzania wielu zasobów platformy Azure, w tym aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toodesign and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="6b7b8-105">Visual Studio Cloud Explorer umożliwia przeglądanie, zarządzanie, edytowanie i pobierania opublikowane aplikacje logiki.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="6b7b8-106">Zadania zarządzania obejmują Włącz, wyłącz i uruchom wyświetlanie historii.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="6b7b8-107">Można było uzyskać dostęp i zarządzać aplikacji logiki w programie Visual Studio, zainstalować i skonfigurować te narzędzia Visual Studio dla usługi Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6b7b8-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6b7b8-108">Prerequisites</span></span>

* [<span data-ttu-id="6b7b8-109">Visual Studio 2015 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="6b7b8-110">[Najnowszy zestaw Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 lub nowszej)</span><span class="sxs-lookup"><span data-stu-id="6b7b8-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="6b7b8-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="6b7b8-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="6b7b8-112">Access toohello w sieci web używając projektanta osadzonych hello</span><span class="sxs-lookup"><span data-stu-id="6b7b8-112">Access toohello web when using hello embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="6b7b8-113">Instalowanie narzędzi Visual Studio tools for Logic Apps</span><span class="sxs-lookup"><span data-stu-id="6b7b8-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="6b7b8-114">Po zainstalowaniu wymagań wstępnych hello, Pobierz i zainstaluj hello Azure logiki aplikacji Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-114">After you install hello prerequisites, download and install hello Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="6b7b8-115">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-115">Open Visual Studio.</span></span> <span data-ttu-id="6b7b8-116">Na powitania **narzędzia** menu, wybierz opcję **rozszerzenia i aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-116">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="6b7b8-117">Rozwiń węzeł hello **Online** kategorii, Wyszukaj w trybie online w hello galerii programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-117">Expand hello **Online** category so you can search online in hello Visual Studio Gallery.</span></span>
3. <span data-ttu-id="6b7b8-118">Wyszukaj **Logic Apps** do momentu znalezienia **Azure Logic Apps Tools for Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="6b7b8-119">toodownload i rozszerzenie hello instalacji, kliknij przycisk **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-119">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="6b7b8-120">Po zakończeniu instalacji uruchom ponownie program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="6b7b8-121">toodownload hello Azure Logic Apps Tools for Visual Studio przejdź bezpośrednio, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="6b7b8-121">toodownload hello Azure Logic Apps Tools for Visual Studio directly, go toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="6b7b8-122">Przeglądaj w poszukiwaniu aplikacji logiki w Eksploratorze chmury</span><span class="sxs-lookup"><span data-stu-id="6b7b8-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="6b7b8-123">tooopen Eksplorator chmury na powitania **widoku** menu, wybierz **Eksplorator chmury**.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-123">tooopen Cloud Explorer, on hello **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="6b7b8-124">Przeglądaj w poszukiwaniu aplikacji logiki, grupy zasobów lub typ zasobu.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="6b7b8-125">Jeśli możesz przeglądać według typów zasobów, wybierz subskrypcję platformy Azure, rozwiń hello **Logic Apps** sekcji, a następnie wybierz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-125">If you browse by resource type, select your Azure subscription, expand hello **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="6b7b8-126">Jeśli możesz przeglądać według grupy zasobów, rozwiń hello grupy zasobów aplikacji logiki, a następnie wybierz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-126">If you browse by resource group, expand hello resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="6b7b8-127">polecenia tooview aplikacji logiki, kliknij prawym przyciskiem myszy aplikację logiki, albo u dołu hello Eksplorator chmury, wybierz jedną z hello **akcje** menu.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-127">tooview commands for your logic app, either right-click your logic app, or at hello bottom of Cloud Explorer, choose from hello **Actions** menu.</span></span>

    ![Przeglądaj w poszukiwaniu aplikacji logiki](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="6b7b8-129">Edytuj w Projektancie aplikacji logiki aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="6b7b8-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="6b7b8-130">W Eksploratorze chmury, możesz otworzyć aplikację logiki aktualnie wdrożonych w hello tego samego projektanta, używanego w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-130">From Cloud Explorer, you can open a currently deployed logic app in hello same designer that you use in hello Azure portal.</span></span> 

* <span data-ttu-id="6b7b8-131">tooedit aplikację logiki w Eksploratorze chmury, kliknij prawym przyciskiem myszy aplikację logiki, a następnie wybierz **otwarty przy użyciu edytora aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-131">tooedit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="6b7b8-132">toopublish Twojego toohello aktualizacje w chmurze, wybrać **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-132">toopublish your updates toohello cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="6b7b8-133">Wybierz toostart nowy przebieg **uruchomić wyzwalacz**.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-133">toostart a new run, choose **Run Trigger**.</span></span>

![Projektant aplikacji logiki](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="6b7b8-135">Przy użyciu projektanta hello, możesz również **Pobierz** aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-135">From hello designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="6b7b8-136">Ta akcja automatycznie parameterizes definicję aplikacji logiki hello i definicji hello jest zapisywany jako szablon wdrożenia usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-136">This action automatically parameterizes hello logic app definition, and saves hello definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="6b7b8-137">Możesz dodać ten projekt wdrożenia szablonu tooyour grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-137">You can add this deployment template tooyour Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="6b7b8-138">Przeglądaj Historia uruchomień aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="6b7b8-138">Browse your logic app run history</span></span>

<span data-ttu-id="6b7b8-139">hello tooview Uruchom historii aplikacji logiki, kliknij prawym przyciskiem myszy aplikację logiki, a następnie wybierz **Historia uruchomień Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-139">tooview hello run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="6b7b8-140">tooreorder historii wykonywania oparte na żadnym z nagłówka kolumny hello pokazano, wybierz pozycję Właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-140">tooreorder your run history based on any of hello properties shown, select hello column header.</span></span>

![Historia uruchomień](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="6b7b8-142">Witaj tooshow Uruchom historii dla wystąpienia, aby przejrzeć hello Uruchom wynikami, w tym hello wejścia i wyjścia z każdym kroku, kliknij dwukrotnie jeden z hello uruchomionych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="6b7b8-142">tooshow hello run history for an instance so you can review hello run results, including hello inputs and outputs from each step, double-click one of hello run instances.</span></span>

![Uruchom wyników historii, wejścia i wyjścia z kroków](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="6b7b8-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6b7b8-144">Next steps</span></span>

* [<span data-ttu-id="6b7b8-145">Tworzenie pierwszej aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="6b7b8-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="6b7b8-146">Projektowanie, tworzenie i wdrażanie aplikacji logiki w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b7b8-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="6b7b8-147">Wyświetlanie typowych przykładów i scenariuszy</span><span class="sxs-lookup"><span data-stu-id="6b7b8-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="6b7b8-148">Wideo: Automatyzować procesy biznesowe z usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="6b7b8-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="6b7b8-149">Wideo: Integrować systemy z usługą Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="6b7b8-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
