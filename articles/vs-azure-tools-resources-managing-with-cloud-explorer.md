---
title: "aaaManaging Azure zasobami za pomocą Eksploratora chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toobrowse Eksplorator chmury toouse i zarządzania zasobami Azure w programie Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="83493-103">Zarządzanie zasobami hello skojarzone z konta platformy Azure w Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="83493-103">Manage hello resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="83493-104">Eksplorator chmury umożliwia możesz tooview zasobów platformy Azure i grup zasobów, sprawdzić ich właściwości i akcje developer klucza diagnostycznych z poziomu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83493-104">Cloud Explorer enables you tooview your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="83493-105">Podobnie jak hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Eksplorator chmury jest zbudowany na powitania stosu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="83493-105">Like hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on hello Azure Resource Manager stack.</span></span> <span data-ttu-id="83493-106">W związku z tym Eksplorator chmury rozumie zasobów, takich jak grupy zasobów platformy Azure i usług Azure, takich jak aplikacje logiki i interfejsu API apps i obsługuje [kontroli dostępu opartej na rolach](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="83493-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="83493-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="83493-107">Prerequisites</span></span>
- <span data-ttu-id="83493-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) z hello **obciążenia Azure** zaznaczone, lub starszej wersji programu Visual Studio z hello [Microsoft Azure SDK dla programu .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="83493-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello **Azure workload** selected, or an earlier version of Visual Studio with hello [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="83493-109">Konto Microsoft Azure — Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](http://go.microsoft.com/fwlink/?LinkId=623901) lub [aktywować korzyści dla subskrybentów programu Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="83493-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="83493-110">Wybierz tooview Eksplorator chmury **widoku** > **Eksplorator chmury** hello paska menu.</span><span class="sxs-lookup"><span data-stu-id="83493-110">tooview Cloud Explorer, select **View** > **Cloud Explorer** on hello menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a><span data-ttu-id="83493-111">Dodaj konto platformy Azure tooCloud Explorer</span><span class="sxs-lookup"><span data-stu-id="83493-111">Add an Azure account tooCloud Explorer</span></span>
<span data-ttu-id="83493-112">zasoby hello tooview skojarzone z kontem platformy Azure, należy najpierw dodać hello konta tooCloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="83493-112">tooview hello resources associated with an Azure account, you must first add hello account tooCloud Explorer.</span></span> 

1. <span data-ttu-id="83493-113">W **Eksplorator chmury**, wybierz pozycję **ustawienia konta Azure**.</span><span class="sxs-lookup"><span data-stu-id="83493-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Ikona ustawienia konta Azure Eksplorator chmury](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="83493-115">Wybierz **Dodaj nowe konto**.</span><span class="sxs-lookup"><span data-stu-id="83493-115">Select **Add new account**.</span></span> 

    ![Łącze Eksploratora Dodaj konto w chmurze](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="83493-117">Zaloguj się za toohello konto platformy Azure, którego zasoby mają toobrowse.</span><span class="sxs-lookup"><span data-stu-id="83493-117">Log in toohello Azure account whose resources you want toobrowse.</span></span> 

1. <span data-ttu-id="83493-118">Po zalogowaniu tooan konto platformy Azure, wyświetlanie subskrypcji hello skojarzonych z tym kontem.</span><span class="sxs-lookup"><span data-stu-id="83493-118">Once logged in tooan Azure account, hello subscriptions associated with that account display.</span></span> <span data-ttu-id="83493-119">Wybierz hello pola wyboru dla subskrypcji kont hello mają toobrowse, a następnie wybierz **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="83493-119">Select hello check boxes for hello account subscriptions you want toobrowse and then select **Apply**.</span></span> 
 
    ![Eksplorator chmury: Wybierz toodisplay subskrypcji platformy Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="83493-121">Po wybraniu subskrypcji hello którego zasoby mają toobrowse, te subskrypcje i zasobów wyświetlane w hello Eksplorator chmury.</span><span class="sxs-lookup"><span data-stu-id="83493-121">After selecting hello subscriptions whose resources you want toobrowse, those subscriptions and resources display in hello Cloud Explorer.</span></span>

    ![Eksplorator zasobów dla konta platformy Azure w chmurze](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="83493-123">Usuń konto platformy Azure w Eksploratorze chmury</span><span class="sxs-lookup"><span data-stu-id="83493-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="83493-124">W **Eksplorator chmury**, wybierz pozycję **ustawienia konta Azure**.</span><span class="sxs-lookup"><span data-stu-id="83493-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Ikona ustawienia konta Azure Eksplorator chmury](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="83493-126">Wybierz następny toohello konta tooremove, **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="83493-126">Next toohello account you want tooremove, select **Remove**.</span></span>

    ![Ikona ustawienia konta Azure Eksplorator chmury](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="83493-128">Wyświetlanie typów zasobów lub grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="83493-128">View resource types or resource groups</span></span>
<span data-ttu-id="83493-129">tooview zasobów platformy Azure, można wybrać jedną **typów zasobów** lub **grup zasobów** widoku.</span><span class="sxs-lookup"><span data-stu-id="83493-129">tooview your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="83493-130">W **Eksplorator chmury**, wybierz hello lista rozwijana widok zasobów.</span><span class="sxs-lookup"><span data-stu-id="83493-130">In **Cloud Explorer**, select hello resource view dropdown.</span></span>

    ![Cloud Explorer listy rozwijanej liście tooselect hello żądany widok zasobów](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="83493-132">Z menu kontekstowego hello wybierz widok hello potrzeby:</span><span class="sxs-lookup"><span data-stu-id="83493-132">From hello context menu, select hello desired view:</span></span> 

    - <span data-ttu-id="83493-133">**Typy zasobów** widok - hello widok typowych używany na powitania [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), pokazuje zasobów platformy Azure podzielone według typu, takich jak aplikacje sieci web, konta magazynu i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="83493-133">**Resource Types** view - hello common view used on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="83493-134">**Grupy zasobów** view - zasobów Azure kategoryzuje przez hello grupy zasobów platformy Azure, z którym są powiązane.</span><span class="sxs-lookup"><span data-stu-id="83493-134">**Resource Groups** view - Categorizes Azure resources by hello Azure resource group with which they're associated.</span></span> <span data-ttu-id="83493-135">Grupa zasobów to pakiet zasobów platformy Azure, zwykle używanych przez określoną aplikację.</span><span class="sxs-lookup"><span data-stu-id="83493-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="83493-136">toolearn więcej informacji na temat grup zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="83493-136">toolearn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="83493-137">Witaj poniższej ilustracji przedstawiono porównanie hello dwa widoki zasobów:</span><span class="sxs-lookup"><span data-stu-id="83493-137">hello following image shows a comparison of hello two resource views:</span></span>

    ![Eksplorator zasobów widoków porównania w chmurze](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="83493-139">Wyświetlanie i przejdź do zasobów w Eksploratorze chmury</span><span class="sxs-lookup"><span data-stu-id="83493-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="83493-140">tooan toonavigate zasobów platformy Azure i wyświetlić informacje o nim w Eksploratorze chmury, rozwiń element hello typu lub grupy zasobów, a następnie wybierz hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="83493-140">toonavigate tooan Azure resource and view its information in Cloud Explorer, expand hello item's type or associated resource group and then select hello resource.</span></span> <span data-ttu-id="83493-141">Po wybraniu zasobu informacje są wyświetlane na kartach hello dwu - **akcje** i **właściwości** — u dołu hello Eksplorator chmury.</span><span class="sxs-lookup"><span data-stu-id="83493-141">When you select a resource, information appears in hello two tabs - **Actions** and **Properties** - at hello bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="83493-142">**Akcje** karcie - list hello akcje można wykonać w Eksploratorze chmury dla zasobu hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="83493-142">**Actions** tab - Lists hello actions you can take in Cloud Explorer for hello selected resource.</span></span> <span data-ttu-id="83493-143">Można również wyświetlić te opcje przez kliknięcie prawym przyciskiem myszy tooview zasobów hello jego menu kontekstowego.</span><span class="sxs-lookup"><span data-stu-id="83493-143">You can also view these options by right-clicking hello resource tooview its context menu.</span></span>

- <span data-ttu-id="83493-144">**Właściwości** karcie — pokazuje hello właściwości zasobu hello, takich jak grupy jego typu, ustawienia regionalne i zasobów, z którym jest skojarzona.</span><span class="sxs-lookup"><span data-stu-id="83493-144">**Properties** tab - Shows hello properties of hello resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="83493-145">Witaj poniższej ilustracji przedstawiono przykład porównanie informacje wyświetlane na każdej karcie usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="83493-145">hello following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="83493-146">Każdy zasób istnieje akcja hello **Otwórz w portalu**.</span><span class="sxs-lookup"><span data-stu-id="83493-146">Every resource has hello action **Open in portal**.</span></span> <span data-ttu-id="83493-147">Po wybraniu tej akcji, Eksplorator chmury Wyświetla zasobów hello wybrane w hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="83493-147">When you choose this action, Cloud Explorer displays hello selected resource in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="83493-148">Witaj **Otwórz w portalu** funkcja jest przydatna do nawigowania toodeeply zagnieżdżone zasoby.</span><span class="sxs-lookup"><span data-stu-id="83493-148">hello **Open in portal** feature is handy for navigating toodeeply nested resources.</span></span>

<span data-ttu-id="83493-149">Dodatkowe akcje i wartości właściwości mogą również wyświetlane w zależności od hello zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="83493-149">Additional actions and property values may also appear based on hello Azure resource.</span></span> <span data-ttu-id="83493-150">Na przykład aplikacje sieci web i aplikacje logiki również mieć akcje hello **Otwórz w przeglądarce** i **dołączyć debuger** dodatkowo zbyt**Otwórz w portalu**.</span><span class="sxs-lookup"><span data-stu-id="83493-150">For example, web apps and logic apps also have hello actions **Open in browser** and **Attach debugger** in addition too**Open in portal**.</span></span> <span data-ttu-id="83493-151">Edytory tooopen akcje są wyświetlane po wybraniu obiektu blob z konta magazynu, kolejki lub tabeli.</span><span class="sxs-lookup"><span data-stu-id="83493-151">Actions tooopen editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="83493-152">Aplikacje platformy Azure ma **adres URL** i **stan** właściwości, gdy zasobów magazynu ma właściwości parametrów połączenia i klucza.</span><span class="sxs-lookup"><span data-stu-id="83493-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="83493-153">Znajdź zasoby w Eksploratorze chmury</span><span class="sxs-lookup"><span data-stu-id="83493-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="83493-154">zasoby toolocate o określonej nazwie w subskrypcji konto platformy Azure, wprowadź nazwę hello w hello **wyszukiwania** pole w Eksploratorze chmury.</span><span class="sxs-lookup"><span data-stu-id="83493-154">toolocate resources with a specific name in your Azure account subscriptions, enter hello name in hello **Search** box in Cloud Explorer.</span></span>

![Znajdowanie zasobów w Eksploratorze chmury](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="83493-156">Podczas wprowadzania znaków hello **wyszukiwania** okno, tylko zasoby, spełniające te znaki są wyświetlane w drzewie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="83493-156">As you enter characters in hello **Search** box, only resources that match those characters appear in hello resource tree.</span></span>
