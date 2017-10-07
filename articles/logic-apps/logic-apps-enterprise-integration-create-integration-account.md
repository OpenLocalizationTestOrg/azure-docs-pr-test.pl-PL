---
title: "aaaCreate, link, usunąć lub przenieść konta integracji w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Sposób integracji toocreate konta, a następnie połącz go tooyour logic apps"
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
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="e00e8-103">Co to jest konto integracji?</span><span class="sxs-lookup"><span data-stu-id="e00e8-103">What is an integration account?</span></span>

<span data-ttu-id="e00e8-104">Konta integracji umożliwia aplikacjom integracji przedsiębiorstwa artefaktów toomanage, w tym schematów, map, certyfikaty, partnerzy i umów.</span><span class="sxs-lookup"><span data-stu-id="e00e8-104">An integration account allows enterprise integration apps toomanage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="e00e8-105">Dowolną aplikację integracji, które możesz utworzyć używa tooaccess konta integracji tych schematów, map, certyfikaty i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="e00e8-105">Any integration app you create uses an integration account tooaccess these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="e00e8-106">Tworzenie konta usługi integracji</span><span class="sxs-lookup"><span data-stu-id="e00e8-106">Create an integration account</span></span>

1.  <span data-ttu-id="e00e8-107">Zaloguj się toohello [portalu Azure](http://portal.azure.com "portalu Azure").</span><span class="sxs-lookup"><span data-stu-id="e00e8-107">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="e00e8-108">Wybierz z menu po lewej stronie powitania **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-108">From hello left menu, select **More services**.</span></span>

    ![Wybierz pozycję "Więcej usług"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="e00e8-110">W polu wyszukiwania hello wpisz "Integracja" filtru.</span><span class="sxs-lookup"><span data-stu-id="e00e8-110">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="e00e8-111">Na liście wyników hello, wybierz **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-111">In hello results list, select **Integration Accounts**.</span></span>

    ![Odfiltruj "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="e00e8-113">U góry hello hello strony, wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-113">At hello top of hello page, choose **Add**.</span></span>

    ![Wybierz opcję Dodaj](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="e00e8-115">Nadaj nazwę swojego konta integracji i wybierz hello subskrypcji platformy Azure, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="e00e8-115">Name your integration account and select hello Azure subscription that you want toouse.</span></span> <span data-ttu-id="e00e8-116">Możesz utworzyć nową **grupy zasobów** lub wybierz istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="e00e8-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="e00e8-117">Następnie wybierz **lokalizacji** dla Twojego konta integracji hostingu i **warstwy cenowej**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="e00e8-118">Gdy wszystko jest gotowe, wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-118">When you're ready, choose **Create**.</span></span>

    ![Podaj szczegóły konta integracji](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="e00e8-120">Azure udostępnia konta integracji w lokalizacji hello wybrany powinno zakończyć się w ciągu 1 minuty.</span><span class="sxs-lookup"><span data-stu-id="e00e8-120">Azure provisions your integration account  in hello selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="e00e8-121">Odśwież stronę hello.</span><span class="sxs-lookup"><span data-stu-id="e00e8-121">Refresh hello page.</span></span> <span data-ttu-id="e00e8-122">Widzisz konta integracji na liście.</span><span class="sxs-lookup"><span data-stu-id="e00e8-122">You see your new integration account listed.</span></span>

    ![Pojawi się nowego konta integracji](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="e00e8-124">Następnie połącz konto integracji hello za ten zostanie utworzony tooyour aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e00e8-124">Next, link hello integration account that you created tooyour logic app.</span></span> 

## <a name="link-an-integration-account-tooa-logic-app"></a><span data-ttu-id="e00e8-125">Łączenie aplikacji logiki tooa konta integracji</span><span class="sxs-lookup"><span data-stu-id="e00e8-125">Link an integration account tooa logic app</span></span>

<span data-ttu-id="e00e8-126">toogive aplikacje logiki dostępu toomaps, schematów, umów oraz pozostałych artefaktów na koncie integracji aplikacji logiki tooyour konta integracji hello łącza.</span><span class="sxs-lookup"><span data-stu-id="e00e8-126">toogive your logic apps access toomaps, schemas, agreements, and other artifacts in your integration account, link hello integration account tooyour logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e00e8-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e00e8-127">Prerequisites</span></span>

* <span data-ttu-id="e00e8-128">Konta integracji</span><span class="sxs-lookup"><span data-stu-id="e00e8-128">An integration account</span></span>
* <span data-ttu-id="e00e8-129">Aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="e00e8-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="e00e8-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello *tej samej lokalizacji platformy Azure* przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="e00e8-130">Make sure your integration account and logic app are in hello *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="e00e8-131">W hello portalu Azure wybierz aplikację logiki i sprawdź lokalizację aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="e00e8-131">In hello Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Wybierz aplikację logiki, sprawdź lokalizację](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="e00e8-133">W obszarze **ustawienia**, wybierz pozycję **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Wybierz opcję "Konto Integration"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="e00e8-135">Z hello **wybierz konto integracji** listy, wybierz hello integracji konta toolink tooyour logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e00e8-135">From hello **Select an Integration account** list, select hello integration account you want toolink tooyour logic app.</span></span> <span data-ttu-id="e00e8-136">Wybierz toofinish połączeń, **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-136">toofinish linking, choose **Save**.</span></span>

    ![Wybierz konto integracji](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="e00e8-138">Otrzymasz powiadomienie, które pokazuje integracją konta jest tooyour połączonej aplikacji logiki, a wszystkie artefakty na koncie integracji są teraz dostępne tooyour aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e00e8-138">You get a notification that shows your integration account is linked tooyour logic app,  and that all artifacts in your integration account are now available tooyour logic app.</span></span>

    ![Aplikację logiki jest połączony tooyour konta integracji](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="e00e8-140">Teraz, Twoje konto integracji jest tooyour połączonej aplikacji logiki, można użyć łączników hello B2B w aplikacjach logiki.</span><span class="sxs-lookup"><span data-stu-id="e00e8-140">Now that your integration account is linked tooyour logic app, you can use hello B2B connectors in your logic apps.</span></span> <span data-ttu-id="e00e8-141">Niektóre typowe łączniki B2B obejmują sprawdzanie poprawności kodu XML i pliku prostego kodowania/dekodowania.</span><span class="sxs-lookup"><span data-stu-id="e00e8-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="e00e8-142">Usuwanie konta integracji</span><span class="sxs-lookup"><span data-stu-id="e00e8-142">Delete your integration account</span></span>

1. <span data-ttu-id="e00e8-143">Wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-143">Select **More services**.</span></span>

    ![Wybierz pozycję "Więcej usług"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="e00e8-145">W polu wyszukiwania hello wpisz "Integracja" filtru.</span><span class="sxs-lookup"><span data-stu-id="e00e8-145">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="e00e8-146">Na liście wyników hello, wybierz **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-146">In hello results list, select **Integration Accounts**.</span></span>

    ![Odfiltruj "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="e00e8-148">Wybierz konto integracji hello, które mają toodelete.</span><span class="sxs-lookup"><span data-stu-id="e00e8-148">Select hello integration account that you want toodelete.</span></span>

    ![Wybierz toodelete konta integracji](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="e00e8-150">W hello menu wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-150">On hello menu, choose **Delete**.</span></span>

    ![Wybierz pozycję "Delete"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="e00e8-152">Potwierdź konto integracji hello choice toodelete.</span><span class="sxs-lookup"><span data-stu-id="e00e8-152">Confirm your choice toodelete hello integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="e00e8-153">Przenoszenie konta integracji</span><span class="sxs-lookup"><span data-stu-id="e00e8-153">Move your integration account</span></span>

<span data-ttu-id="e00e8-154">toomove integracji tooanother konta Azure subskrypcji lub grupy zasobów, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="e00e8-154">toomove an integration account tooanother Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e00e8-155">Należy zaktualizować wszystkie skrypty toouse hello nowy zasób identyfikatory po przeniesieniu konta integracji.</span><span class="sxs-lookup"><span data-stu-id="e00e8-155">You must update all scripts toouse hello new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="e00e8-156">Wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-156">Select **More services**.</span></span>

    ![Wybierz pozycję "Więcej usług"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="e00e8-158">W polu wyszukiwania hello wpisz "Integracja" filtru.</span><span class="sxs-lookup"><span data-stu-id="e00e8-158">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="e00e8-159">Na liście wyników hello, wybierz **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-159">In hello results list, select **Integration Accounts**.</span></span>

    ![Odfiltruj "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="e00e8-161">Wybierz konto integracji hello, które mają toomove.</span><span class="sxs-lookup"><span data-stu-id="e00e8-161">Select hello integration account that you want toomove.</span></span> <span data-ttu-id="e00e8-162">W obszarze **ustawienia**, wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="e00e8-162">Under **Settings**, choose **Properties**.</span></span>

    ![Wybierz toomove konta integracji.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="e00e8-165">Zmień hello grupy zasobów lub subskrypcji platformy Azure, który został skojarzony z Twoim kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="e00e8-165">Change hello resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Wybierz opcję Zmień grupę zasobów lub zmiany subskrypcji](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="e00e8-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e00e8-167">Next Steps</span></span>
* [<span data-ttu-id="e00e8-168">Dowiedz się więcej na temat umów</span><span class="sxs-lookup"><span data-stu-id="e00e8-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  

