---
title: "Tworzenie, link, usunąć lub przenieść konta integracji w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak utworzyć konto integracji i połącz go z aplikacji logiki"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 716e7b5bab8725dea0fd2b760d0e46e8e892c5b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="dae32-103">Co to jest konto integracji?</span><span class="sxs-lookup"><span data-stu-id="dae32-103">What is an integration account?</span></span>

<span data-ttu-id="dae32-104">Konta integracji umożliwia enterprise integracji aplikacji do zarządzania artefaktów, w tym schematów, map, certyfikaty, partnerzy i umów.</span><span class="sxs-lookup"><span data-stu-id="dae32-104">An integration account allows enterprise integration apps to manage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="dae32-105">Dowolną aplikację integracji, tworzonych przy użyciu konta integracji dostęp do tych schematów, map, certyfikaty i itd.</span><span class="sxs-lookup"><span data-stu-id="dae32-105">Any integration app you create uses an integration account to access these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="dae32-106">Tworzenie konta usługi integracji</span><span class="sxs-lookup"><span data-stu-id="dae32-106">Create an integration account</span></span>

1.  <span data-ttu-id="dae32-107">Zaloguj się w witrynie [Azure Portal](http://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="dae32-107">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="dae32-108">Wybierz z menu po lewej stronie **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="dae32-108">From the left menu, select **More services**.</span></span>

    ![Wybierz pozycję "Więcej usług"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="dae32-110">W polu wyszukiwania wpisz "Integracja" filtru.</span><span class="sxs-lookup"><span data-stu-id="dae32-110">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="dae32-111">Na liście wyników wybierz **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="dae32-111">In the results list, select **Integration Accounts**.</span></span>

    ![Odfiltruj "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="dae32-113">W górnej części strony, wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="dae32-113">At the top of the page, choose **Add**.</span></span>

    ![Wybierz opcję Dodaj](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="dae32-115">Nazwa konta integracji i wybierz subskrypcję platformy Azure, którego chcesz używać.</span><span class="sxs-lookup"><span data-stu-id="dae32-115">Name your integration account and select the Azure subscription that you want to use.</span></span> <span data-ttu-id="dae32-116">Możesz utworzyć nową **grupy zasobów** lub wybierz istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="dae32-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="dae32-117">Następnie wybierz **lokalizacji** dla Twojego konta integracji hostingu i **warstwy cenowej**.</span><span class="sxs-lookup"><span data-stu-id="dae32-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="dae32-118">Gdy wszystko jest gotowe, wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="dae32-118">When you're ready, choose **Create**.</span></span>

    ![Podaj szczegóły konta integracji](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="dae32-120">Azure udostępnia konta integracji w wybranej lokalizacji, która powinna zakończyć się w ciągu 1 minuty.</span><span class="sxs-lookup"><span data-stu-id="dae32-120">Azure provisions your integration account  in the selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="dae32-121">Odśwież stronę.</span><span class="sxs-lookup"><span data-stu-id="dae32-121">Refresh the page.</span></span> <span data-ttu-id="dae32-122">Widzisz konta integracji na liście.</span><span class="sxs-lookup"><span data-stu-id="dae32-122">You see your new integration account listed.</span></span>

    ![Pojawi się nowego konta integracji](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="dae32-124">Następnie połącz konto integracji utworzoną aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="dae32-124">Next, link the integration account that you created to your logic app.</span></span> 

## <a name="link-an-integration-account-to-a-logic-app"></a><span data-ttu-id="dae32-125">Połącz konto integracji aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="dae32-125">Link an integration account to a logic app</span></span>

<span data-ttu-id="dae32-126">Aby zapewnić logiki aplikacji dostęp do map, schematów, umów oraz pozostałych artefaktów na koncie integracji Połącz konto integracji aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="dae32-126">To give your logic apps access to maps, schemas, agreements, and other artifacts in your integration account, link the integration account to your logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="dae32-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dae32-127">Prerequisites</span></span>

* <span data-ttu-id="dae32-128">Konta integracji</span><span class="sxs-lookup"><span data-stu-id="dae32-128">An integration account</span></span>
* <span data-ttu-id="dae32-129">Aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="dae32-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="dae32-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w *tej samej lokalizacji platformy Azure* przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="dae32-130">Make sure your integration account and logic app are in the *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="dae32-131">W portalu Azure wybierz aplikację logiki i sprawdź lokalizację aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="dae32-131">In the Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Wybierz aplikację logiki, sprawdź lokalizację](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="dae32-133">W obszarze **ustawienia**, wybierz pozycję **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="dae32-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Wybierz opcję "Konto Integration"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="dae32-135">Z **wybierz konto integracji** listy, wybierz konto integracji, aby połączyć aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="dae32-135">From the **Select an Integration account** list, select the integration account you want to link to your logic app.</span></span> <span data-ttu-id="dae32-136">Aby zakończyć połączenie, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="dae32-136">To finish linking, choose **Save**.</span></span>

    ![Wybierz konto integracji](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="dae32-138">Otrzymasz powiadomienie, które pokazuje integracją konto jest połączone z aplikacji logiki, a wszystkie artefakty na koncie integracji są teraz dostępne dla aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="dae32-138">You get a notification that shows your integration account is linked to your logic app,  and that all artifacts in your integration account are now available to your logic app.</span></span>

    ![Aplikację logiki jest połączony z kontem integracji](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="dae32-140">Teraz, kiedy Twoje konto integracji jest połączone z aplikacji logiki, można użyć łączniki B2B w aplikacjach logiki.</span><span class="sxs-lookup"><span data-stu-id="dae32-140">Now that your integration account is linked to your logic app, you can use the B2B connectors in your logic apps.</span></span> <span data-ttu-id="dae32-141">Niektóre typowe łączniki B2B obejmują sprawdzanie poprawności kodu XML i pliku prostego kodowania/dekodowania.</span><span class="sxs-lookup"><span data-stu-id="dae32-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="dae32-142">Usuwanie konta integracji</span><span class="sxs-lookup"><span data-stu-id="dae32-142">Delete your integration account</span></span>

1. <span data-ttu-id="dae32-143">Wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="dae32-143">Select **More services**.</span></span>

    ![Wybierz pozycję "Więcej usług"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="dae32-145">W polu wyszukiwania wpisz "Integracja" filtru.</span><span class="sxs-lookup"><span data-stu-id="dae32-145">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="dae32-146">Na liście wyników wybierz **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="dae32-146">In the results list, select **Integration Accounts**.</span></span>

    ![Odfiltruj "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="dae32-148">Wybierz konto integracji, które chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="dae32-148">Select the integration account that you want to delete.</span></span>

    ![Wybierz konto integracji do usunięcia](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="dae32-150">W menu, wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="dae32-150">On the menu, choose **Delete**.</span></span>

    ![Wybierz pozycję "Delete"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="dae32-152">Potwierdź zamiar usunięcia konta integracji.</span><span class="sxs-lookup"><span data-stu-id="dae32-152">Confirm your choice to delete the integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="dae32-153">Przenoszenie konta integracji</span><span class="sxs-lookup"><span data-stu-id="dae32-153">Move your integration account</span></span>

<span data-ttu-id="dae32-154">Aby przenieść konta integracji innego Azure subskrypcji lub grupy zasobów, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="dae32-154">To move an integration account to another Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dae32-155">Należy zaktualizować wszystkie skrypty do używania nowych identyfikatorów zasobów. po przeniesieniu konta integracji.</span><span class="sxs-lookup"><span data-stu-id="dae32-155">You must update all scripts to use the new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="dae32-156">Wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="dae32-156">Select **More services**.</span></span>

    ![Wybierz pozycję "Więcej usług"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="dae32-158">W polu wyszukiwania wpisz "Integracja" filtru.</span><span class="sxs-lookup"><span data-stu-id="dae32-158">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="dae32-159">Na liście wyników wybierz **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="dae32-159">In the results list, select **Integration Accounts**.</span></span>

    ![Odfiltruj "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="dae32-161">Wybierz konto integracji, które mają zostać przeniesione.</span><span class="sxs-lookup"><span data-stu-id="dae32-161">Select the integration account that you want to move.</span></span> <span data-ttu-id="dae32-162">W obszarze **ustawienia**, wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="dae32-162">Under **Settings**, choose **Properties**.</span></span>

    ![Wybierz konto integracji można przenieść.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="dae32-165">Zmiana grupy zasobów lub subskrypcji platformy Azure, który został skojarzony z Twoim kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="dae32-165">Change the resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Wybierz opcję Zmień grupę zasobów lub zmiany subskrypcji](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="dae32-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dae32-167">Next Steps</span></span>
* [<span data-ttu-id="dae32-168">Dowiedz się więcej na temat umów</span><span class="sxs-lookup"><span data-stu-id="dae32-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  

