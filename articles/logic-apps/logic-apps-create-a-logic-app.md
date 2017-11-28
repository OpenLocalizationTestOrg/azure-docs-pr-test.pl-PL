---
title: "aaaCreate pierwszy przepływ pracy między aplikacji w chmurze i usługi w chmurze — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Automatyzacja procesów biznesowych na potrzeby scenariuszy integracji systemów i usługi Enterprise Application Integration (EAI) przez tworzenie i uruchamianie przepływów pracy w usłudze Azure Logic Apps"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: workflow, cloud apps, cloud services, business processes, system integration, enterprise application integration, EAI
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="0952b-104">Tworzenie pierwszej aplikacji logiki procesów tooautomate przepływu pracy między aplikacji w chmurze i usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="0952b-104">Create your first logic app workflow tooautomate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="0952b-105">Procesy biznesowe możesz zautomatyzować bez konieczności pisania kodu łatwiej i szybciej, jeśli utworzysz i uruchomisz przepływy pracy za pomocą usługi [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="0952b-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="0952b-106">Pierwszym przykładzie pokazano, jak toocreate przepływu pracy aplikacji logiki podstawowego, który sprawdza RSS źródła danych dla nowej zawartości w witrynie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0952b-106">This first example shows how toocreate a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="0952b-107">Pojawieniu się nowych elementów w źródle strumieniowym hello witryny, aplikacji logiki hello wysyła wiadomości e-mail z konta programu Outlook lub Gmail.</span><span class="sxs-lookup"><span data-stu-id="0952b-107">When new items appear in hello website's feed, hello logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="0952b-108">toocreate i uruchom aplikację logiki, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0952b-108">toocreate and run a logic app, you need these items:</span></span>

* <span data-ttu-id="0952b-109">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0952b-109">An Azure subscription.</span></span> <span data-ttu-id="0952b-110">Jeśli nie masz subskrypcji, możesz [rozpocząć pracę z bezpłatnym kontem platformy Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="0952b-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="0952b-111">W przeciwnym razie możesz [skorzystać z subskrypcji z płatnością zgodnie z rzeczywistym użyciem](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="0952b-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="0952b-112">Subskrypcja platformy Azure jest używana do rozliczania użycia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="0952b-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="0952b-113">Dowiedz się, jak działają [pomiary użycia](../logic-apps/logic-apps-pricing.md) i jak wyglądają [ceny](https://azure.microsoft.com/pricing/details/logic-apps) w usłudze Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="0952b-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="0952b-114">Przykład wymaga także następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="0952b-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="0952b-115">Konto usługi Outlook.com, Office 365 Outlook lub Gmail</span><span class="sxs-lookup"><span data-stu-id="0952b-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="0952b-116">Jeśli masz osobiste [konto Microsoft](https://account.microsoft.com/account), masz także konto usługi Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="0952b-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="0952b-117">W przeciwnym razie, jeśli masz służbowe konto platformy Azure, masz konto usługi **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="0952b-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="0952b-118">Tooa łącze witryny sieci Web źródła danych RSS.</span><span class="sxs-lookup"><span data-stu-id="0952b-118">A link tooa website's RSS feed.</span></span> <span data-ttu-id="0952b-119">W tym przykładzie użyto hello [źródło danych RSS dla najważniejszych artykułów z witryny sieci Web hello CNN.com](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="0952b-119">This example uses hello [RSS feed for top stories from hello CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="0952b-120">Dodawanie wyzwalacza uruchamiającego przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="0952b-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="0952b-121">A [ *wyzwalacza* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) jest zdarzenie, która uruchamia przepływ pracy aplikacji logiki i hello pierwszy element, który wymaga aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="0952b-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is hello first item that your logic app needs.</span></span>

1. <span data-ttu-id="0952b-122">Zaloguj się toohello [portalu Azure](https://portal.azure.com "portalu Azure").</span><span class="sxs-lookup"><span data-stu-id="0952b-122">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="0952b-123">Z menu po lewej stronie powitania, wybierz **nowy** > **integracji przedsiębiorstwa** > **aplikacji logiki** w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="0952b-123">From hello left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Azure Portal, Nowy, Integracja w przedsiębiorstwie, Aplikacja logiki](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="0952b-125">Można również wybrać **nowy**, następnie w polu wyszukiwania hello wpisz `logic app`, i naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="0952b-125">You can also choose **New**, then in hello search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="0952b-126">Następnie wybierz kolejno pozycje **Aplikacja logiki** > **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0952b-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="0952b-127">Nadaj nazwę aplikacji logiki i wybierz subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0952b-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="0952b-128">Teraz utwórz lub wybierz grupę zasobów platformy Azure, która ułatwi organizowanie powiązanych zasobów platformy Azure i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="0952b-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="0952b-129">Na koniec wybierz lokalizację centrum danych hello do hostowania aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="0952b-129">Finally, select hello datacenter location for hosting your logic app.</span></span> <span data-ttu-id="0952b-130">Gdy wszystko jest gotowe, wybierz pozycję **toodashboard numeru Pin** , a następnie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0952b-130">When you're ready, choose **Pin toodashboard** and then **Create**.</span></span>

     ![Szczegóły aplikacji logiki](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="0952b-132">Po wybraniu **toodashboard numeru Pin**, aplikację logiki pojawią się na hello Azure pulpitu nawigacyjnego po wdrożeniu i otwierany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="0952b-132">When you select **Pin toodashboard**, your logic app appears on hello Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="0952b-133">Jeśli aplikację logiki nie jest wyświetlane na pulpicie nawigacyjnym hello i na powitania **wszystkie zasoby** kafelka, wybierz **Zobacz więcej**i wybierz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="0952b-133">If your logic app doesn't appear on hello dashboard, on hello **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="0952b-134">Lub w menu po lewej stronie powitania, wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="0952b-134">Or on hello left menu, choose **More services**.</span></span> <span data-ttu-id="0952b-135">W obszarze **Integracja w przedsiębiorstwie** wybierz pozycję **Aplikacje logiki** i wybierz swoją aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="0952b-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="0952b-136">Po otwarciu aplikacji logiki na powitania po raz pierwszy, hello projektanta aplikacji logiki zawiera szablony służy tooget uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="0952b-136">When you open your logic app for hello first time, hello Logic App Designer shows templates that you can use tooget started.</span></span> <span data-ttu-id="0952b-137">Na razie wybierz pozycję **Pusta aplikacja logiki**, aby rozpocząć tworzenie aplikacji logiki od podstaw.</span><span class="sxs-lookup"><span data-stu-id="0952b-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="0952b-138">Witaj projektanta aplikacji logiki otwiera i pokazuje dostępnych usług i *wyzwalaczy* używanego w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="0952b-138">hello Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="0952b-139">W polu wyszukiwania hello wpisz `RSS`i wybierz wyzwalacz: **RSS — po opublikowaniu element źródła**</span><span class="sxs-lookup"><span data-stu-id="0952b-139">In hello search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![Wyzwalacz kanału informacyjnego RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="0952b-141">Wprowadź hello link do witryny sieci Web hello źródło danych RSS, które mają tootrack.</span><span class="sxs-lookup"><span data-stu-id="0952b-141">Enter hello link for hello website's RSS feed that you want tootrack.</span></span> 

     <span data-ttu-id="0952b-142">Dodatkowo możesz zmienić **Częstotliwość** i **Interwał**.</span><span class="sxs-lookup"><span data-stu-id="0952b-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="0952b-143">Te ustawienia umożliwiają określenie, jak często aplikacja logiki ma sprawdzać istnienie nowych elementów i zwracać wszystkie elementy z tego okresu.</span><span class="sxs-lookup"><span data-stu-id="0952b-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="0952b-144">Na przykład załóżmy Sprawdź codziennie dla najważniejszych artykułów zaksięgowany toohello CNN witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0952b-144">For this example, let's check every day for   top stories posted toohello CNN website.</span></span>

     ![Konfigurowanie kanału informacyjnego RSS, częstotliwości i interwału dla wyzwalacza](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="0952b-146">Zapisz swoją pracę.</span><span class="sxs-lookup"><span data-stu-id="0952b-146">Save your work for now.</span></span> <span data-ttu-id="0952b-147">(Na pasku poleceń projektanta hello wybierz **zapisać**.)</span><span class="sxs-lookup"><span data-stu-id="0952b-147">(On hello designer command bar, choose **Save**.)</span></span>

   ![Zapisywanie aplikacji logiki](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="0952b-149">Po zapisaniu, aplikację logiki przechodzi na żywo, ale obecnie aplikację logiki sprawdza tylko dla nowych elementów w hello określone źródło danych RSS.</span><span class="sxs-lookup"><span data-stu-id="0952b-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in hello specified RSS feed.</span></span> 
   <span data-ttu-id="0952b-150">toomake generowane w tym przykładzie bardziej użyteczna, możemy dodać akcję, która wykonuje aplikację logiki po wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="0952b-150">toomake this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-tooyour-trigger"></a><span data-ttu-id="0952b-151">Dodaj akcję, która odpowiada tooyour wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="0952b-151">Add an action that responds tooyour trigger</span></span>

<span data-ttu-id="0952b-152">[*Akcja*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) to zadanie wykonywane przez przepływ pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="0952b-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="0952b-153">Po dodaniu aplikacji logiki wyzwalacza tooyour, można dodać operacji tooperform akcji z danych wygenerowanych przez tego wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="0952b-153">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="0952b-154">W naszym przykładzie mamy teraz dodać akcję, która wysyła wiadomości e-mail, gdy pojawią się nowe elementy w kanału informacyjnego RSS hello witryny.</span><span class="sxs-lookup"><span data-stu-id="0952b-154">For our example, we now add an action that sends email when new items appear in hello website's RSS feed.</span></span>

1. <span data-ttu-id="0952b-155">W Projektancie hello, w obszarze wyzwalacz, wybierz **nowy krok** > **Dodaj akcję** w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="0952b-155">In hello designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Dodawanie akcji](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="0952b-157">Witaj projektanta pokazuje [dostępnych łączników](../connectors/apis-list.md) , w którym można wybrać tooperform akcji po wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="0952b-157">hello designer shows [available connectors](../connectors/apis-list.md) so that you can select an action tooperform when your trigger fires.</span></span>

2. <span data-ttu-id="0952b-158">W oparciu o Twoje konto e-mail, wykonaj kroki powitania dla programu Outlook lub Gmail.</span><span class="sxs-lookup"><span data-stu-id="0952b-158">Based on your email account, follow hello steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="0952b-159">Wprowadź toosend poczty e-mail, z Twojego konta programu Outlook, w polu wyszukiwania hello `outlook`.</span><span class="sxs-lookup"><span data-stu-id="0952b-159">toosend email from your Outlook account, in hello search box, enter `outlook`.</span></span> <span data-ttu-id="0952b-160">W obszarze **Usługi** wybierz pozycję **Outlook.com** w przypadku osobistych kont Microsoft lub pozycję **Office 365 Outlook** w przypadku kont służbowych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0952b-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="0952b-161">W obszarze **Akcje** wybierz pozycję **Wyślij wiadomość e-mail**.</span><span class="sxs-lookup"><span data-stu-id="0952b-161">Under **Actions**, select **Send an email**.</span></span>

       ![Wybieranie akcji programu Outlook „Wyślij wiadomość e-mail”](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="0952b-163">Wprowadź toosend poczty e-mail, z Twojego konta usługi Gmail, w polu wyszukiwania hello `gmail`.</span><span class="sxs-lookup"><span data-stu-id="0952b-163">toosend email from your Gmail account, in hello search box, enter `gmail`.</span></span> 
   <span data-ttu-id="0952b-164">W obszarze **Akcje** wybierz pozycję **Wyślij wiadomość e-mail**.</span><span class="sxs-lookup"><span data-stu-id="0952b-164">Under **Actions**, select **Send email**.</span></span>

       ![Wybieranie pozycji „Gmail — Wyślij wiadomość e-mail”](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="0952b-166">Po wyświetleniu monitu o poświadczenia, zaloguj się hello nazwę użytkownika i hasło dla swojego konta poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="0952b-166">When you're prompted for credentials, sign in with hello username and password for your email account.</span></span> 

4. <span data-ttu-id="0952b-167">Podaj dane hello dotyczących tej akcji, takich jak hello adresu e-mail i wybierz parametry hello tooinclude danych hello w hello poczty e-mail, na przykład:</span><span class="sxs-lookup"><span data-stu-id="0952b-167">Provide hello details for this action, like hello destination email address, and choose hello parameters for hello data tooinclude in hello email, for example:</span></span>

   ![Wybierz tooinclude danych w wiadomości e-mail](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="0952b-169">Jeśli wybrano program Outlook, aplikacja logiki może wyglądać jak w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="0952b-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Ukończona aplikacja logiki](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="0952b-171">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="0952b-171">Save your changes.</span></span> <span data-ttu-id="0952b-172">(Na pasku poleceń projektanta hello wybierz **zapisać**.)</span><span class="sxs-lookup"><span data-stu-id="0952b-172">(On hello designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="0952b-173">Teraz możesz ręcznie uruchomić aplikację logiki na potrzeby testowania.</span><span class="sxs-lookup"><span data-stu-id="0952b-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="0952b-174">Na pasku poleceń projektanta hello wybierz **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="0952b-174">On hello designer command bar, choose **Run**.</span></span> <span data-ttu-id="0952b-175">W przeciwnym razie możesz pozwolić, aby aplikację logiki, sprawdź, czy hello określona na podstawie harmonogramu hello, które można skonfigurować źródło danych RSS.</span><span class="sxs-lookup"><span data-stu-id="0952b-175">Otherwise, you can let your logic app check hello specified RSS feed based on hello schedule that you set up.</span></span>

   <span data-ttu-id="0952b-176">Jeśli odnalezionej nowej aplikacji logiki aplikacji logiki hello wysyła wiadomości e-mail zawierające wybranych danych.</span><span class="sxs-lookup"><span data-stu-id="0952b-176">If your logic app finds new items, hello logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="0952b-177">W przypadku znalezienia nowych elementów aplikację logiki pomija hello akcję, która wysyła wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="0952b-177">If no new items are found, your logic app skips hello action that sends email.</span></span>

7. <span data-ttu-id="0952b-178">toomonitor i Sprawdź aplikację logiki do uruchomienia i wyzwolić historii, w menu aplikacji logiki, wybierz opcję **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="0952b-178">toomonitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Monitorowanie i wyświetlanie historii wyzwalania oraz uruchamiania aplikacji logiki](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="0952b-180">Jeśli nie znajdziesz hello dane, które należy oczekiwać na pasku poleceń hello, spróbuj wybrać **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="0952b-180">If you don't find hello data that you expect, on hello command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="0952b-181">więcej informacji na temat stanu aplikacji logiki toolearn lub uruchamianie i wyzwolić historii lub toodiagnose aplikację logiki, zobacz [rozwiązywania problemów z aplikacją logiki](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="0952b-181">toolearn more about your logic app's status or run and trigger history, or toodiagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="0952b-182">Aplikacja logiki będzie działać do momentu jej wyłączenia.</span><span class="sxs-lookup"><span data-stu-id="0952b-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="0952b-183">tooturn poza aplikacji teraz, w menu aplikacji logiki, wybierz **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="0952b-183">tooturn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="0952b-184">Na pasku poleceń hello, wybierz **wyłączyć**.</span><span class="sxs-lookup"><span data-stu-id="0952b-184">On hello command bar, choose **Disable**.</span></span>

<span data-ttu-id="0952b-185">Gratulacje, udało Ci się skonfigurować i uruchomić Twoją pierwszą podstawową aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="0952b-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="0952b-186">Wiesz już, jak łatwe jest tworzenie przepływów pracy automatyzujących procesy oraz integrowanie aplikacji w chmurze i usług w chmurze — a wszystko to bez konieczności pisania kodu.</span><span class="sxs-lookup"><span data-stu-id="0952b-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="0952b-187">Zarządzanie aplikacją logiki</span><span class="sxs-lookup"><span data-stu-id="0952b-187">Manage your logic app</span></span>

<span data-ttu-id="0952b-188">toomanage aplikacji, można wykonać zadania, takie jak sprawdzić stan hello, edytować, wyświetlanie historii, wyłączyć lub usunąć aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="0952b-188">toomanage your app, you can perform tasks like check hello status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="0952b-189">Zaloguj się toohello [portalu Azure](https://portal.azure.com "portalu Azure").</span><span class="sxs-lookup"><span data-stu-id="0952b-189">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="0952b-190">W menu po lewej stronie powitania, wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="0952b-190">On hello left menu, choose **More services**.</span></span> <span data-ttu-id="0952b-191">W obszarze **Integracja w przedsiębiorstwie** wybierz pozycję **Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="0952b-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="0952b-192">Wybierz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="0952b-192">Select your logic app.</span></span> 

   <span data-ttu-id="0952b-193">W menu aplikacji logiki hello można znaleźć w tych zadań zarządzania aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="0952b-193">In hello logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="0952b-194">Zadanie</span><span class="sxs-lookup"><span data-stu-id="0952b-194">Task</span></span>|<span data-ttu-id="0952b-195">Kroki</span><span class="sxs-lookup"><span data-stu-id="0952b-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="0952b-196">Wyświetlenie stanu aplikacji, historii wykonywania i informacji ogólnych</span><span class="sxs-lookup"><span data-stu-id="0952b-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="0952b-197">Wybierz pozycję **Przegląd**.</span><span class="sxs-lookup"><span data-stu-id="0952b-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="0952b-198">Edytowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0952b-198">Edit your app</span></span> | <span data-ttu-id="0952b-199">Wybierz pozycję **Projektant aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="0952b-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="0952b-200">Wyświetlenie definicji kodu JSON przepływu pracy aplikacji</span><span class="sxs-lookup"><span data-stu-id="0952b-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="0952b-201">Wybierz pozycję **Widok kodu aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="0952b-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="0952b-202">Wyświetlenie operacji wykonywanych względem aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="0952b-202">View operations performed on your logic app</span></span> | <span data-ttu-id="0952b-203">Wybierz pozycję **Dziennik aktywności**.</span><span class="sxs-lookup"><span data-stu-id="0952b-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="0952b-204">Wyświetlenie wcześniejszych wersji aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="0952b-204">View past versions for your logic app</span></span> | <span data-ttu-id="0952b-205">Wybierz pozycję **Wersje**.</span><span class="sxs-lookup"><span data-stu-id="0952b-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="0952b-206">Tymczasowe wyłączenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0952b-206">Turn off your app temporarily</span></span> | <span data-ttu-id="0952b-207">Wybierz **omówienie**, następnie na pasku poleceń hello, wybierz pozycję **wyłączyć**.</span><span class="sxs-lookup"><span data-stu-id="0952b-207">Choose **Overview**, then on hello command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="0952b-208">Usunięcie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0952b-208">Delete your app</span></span> | <span data-ttu-id="0952b-209">Wybierz **omówienie**, następnie na pasku poleceń hello, wybierz pozycję **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="0952b-209">Choose **Overview**, then on hello command bar, choose **Delete**.</span></span> <span data-ttu-id="0952b-210">Wprowadź nazwę aplikacji logiki, a następnie wybierz pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="0952b-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="0952b-211">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="0952b-211">Get help</span></span>

<span data-ttu-id="0952b-212">pytania tooask odpowiedzi na pytania i Dowiedz się, jakie inne usługi Azure Logic Apps robią użytkownicy, odwiedź stronę hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="0952b-212">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="0952b-213">toohelp poprawy usługi Azure Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="0952b-213">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0952b-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0952b-214">Next steps</span></span>

*  [<span data-ttu-id="0952b-215">Dodawanie warunków i uruchamianie przepływów pracy</span><span class="sxs-lookup"><span data-stu-id="0952b-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="0952b-216">Szablony aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="0952b-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="0952b-217">Tworzenie aplikacji logiki z szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0952b-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
