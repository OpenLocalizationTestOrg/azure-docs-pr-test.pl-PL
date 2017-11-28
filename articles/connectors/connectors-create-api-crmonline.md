---
title: "aaaConnect tooDynamics 365 (online) z usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie przepływów pracy aplikacji, które zarządzają Dynamics 365 jednostek (online) za pośrednictwem interfejsu API dostarczonych przez łącznik hello Dynamics 365 hello logiki"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a><span data-ttu-id="893b0-103">Łączenie z tooDynamics 365 z przepływów pracy aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="893b0-103">Connect tooDynamics 365 from logic app workflows</span></span>

<span data-ttu-id="893b0-104">Z usługą Logic Apps możesz łączyć tooDynamics 365 (online) i tworzyć przepływy przydatne biznesowe, które tworzenie rekordów, aktualizowania elementów lub powrócić do listy rekordów.</span><span class="sxs-lookup"><span data-stu-id="893b0-104">With Logic Apps, you can connect tooDynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="893b0-105">Łącznik hello Dynamics 365 możesz:</span><span class="sxs-lookup"><span data-stu-id="893b0-105">With hello Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="893b0-106">Tworzenie sieci przepływu biznesowe na podstawie danych hello, uzyskasz od Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="893b0-106">Build your business flow based on hello data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="893b0-107">Użyj akcji, które odpowiedzi, a następnie wprowadź dane wyjściowe hello dostępne dla innych działań.</span><span class="sxs-lookup"><span data-stu-id="893b0-107">Use actions that get a response and then make hello output available for other actions.</span></span> <span data-ttu-id="893b0-108">Na przykład po zaktualizowaniu elementu w 365 Dynamics (online), możesz wysłać wiadomość e-mail przy użyciu usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="893b0-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="893b0-109">W tym temacie pokazano, jak toocreate aplikacji logiki tworzącą zadania w Dynamics 365 po każdej zmianie nowego potencjalnego klienta jest tworzony w Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="893b0-109">This topic shows you how toocreate a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="893b0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="893b0-110">Prerequisites</span></span>
* <span data-ttu-id="893b0-111">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="893b0-111">An Azure account.</span></span>
* <span data-ttu-id="893b0-112">Dynamics 365 konta (online).</span><span class="sxs-lookup"><span data-stu-id="893b0-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="893b0-113">Utwórz zadania, podczas tworzenia nowego potencjalnego klienta w Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="893b0-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="893b0-114">[Zaloguj się tooAzure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="893b0-114">[Sign in tooAzure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="893b0-115">W usłudze Azure search hello, wpisz `Logic apps`, i naciśnij klawisz ENTER.</span><span class="sxs-lookup"><span data-stu-id="893b0-115">In hello Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Znajdź Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="893b0-117">W obszarze **Logic apps**, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="893b0-117">Under **Logic apps**, click **Add**.</span></span>

      ![Dodaj LogicApp](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="893b0-119">toocreate hello logiki aplikacji hello pełną **nazwa**, **subskrypcji**, **grupy zasobów**, i **lokalizacji** pola, a następnie kliknij przycisk  **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="893b0-119">toocreate hello logic app, complete hello **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="893b0-120">Wybierz hello nowej aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="893b0-120">Select hello new logic app.</span></span> <span data-ttu-id="893b0-121">Po otrzymaniu hello **Zakończono pomyślnie wdrażanie** powiadomień, kliknij przycisk **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="893b0-121">When you receive hello **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="893b0-122">W obszarze **narzędzi programistycznych**, kliknij przycisk **projektanta aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="893b0-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="893b0-123">Kliknij na liście szablon hello **pustą aplikację logiki**.</span><span class="sxs-lookup"><span data-stu-id="893b0-123">In hello template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="893b0-124">W polu wyszukiwania hello wpisz `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="893b0-124">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="893b0-125">Z hello Dynamics 365 wyzwala listy, wybierz **Dynamics 365 — po utworzeniu rekordu**.</span><span class="sxs-lookup"><span data-stu-id="893b0-125">From hello Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="893b0-126">Jeśli zostanie wyświetlony monit o toosign w tooDynamics 365, należy to zrobić teraz.</span><span class="sxs-lookup"><span data-stu-id="893b0-126">If you are prompted toosign in tooDynamics 365, do so now.</span></span>

9.  <span data-ttu-id="893b0-127">W szczegółach wyzwalacza hello wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="893b0-127">In hello trigger details, enter hello following information:</span></span>

  * <span data-ttu-id="893b0-128">**Nazwa organizacji**.</span><span class="sxs-lookup"><span data-stu-id="893b0-128">**Organization Name**.</span></span> <span data-ttu-id="893b0-129">Wybierz wystąpienia Dynamics 365 hello, które ma toolisten aplikacji logiki hello do.</span><span class="sxs-lookup"><span data-stu-id="893b0-129">Select hello Dynamics 365 instance that you want hello logic app toolisten to.</span></span>

  * <span data-ttu-id="893b0-130">**Nazwa jednostki**.</span><span class="sxs-lookup"><span data-stu-id="893b0-130">**Entity Name**.</span></span> <span data-ttu-id="893b0-131">Wybierz jednostki hello, który ma toolisten do.</span><span class="sxs-lookup"><span data-stu-id="893b0-131">Select hello entity that you want toolisten to.</span></span> <span data-ttu-id="893b0-132">To zdarzenie działa jako aplikacji logiki hello toostart wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="893b0-132">This event acts as a trigger toostart hello logic app.</span></span> 
  <span data-ttu-id="893b0-133">W tym przewodniku **prowadzi** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="893b0-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="893b0-134">**Jak często mają toocheck dla elementów**</span><span class="sxs-lookup"><span data-stu-id="893b0-134">**How often do you want toocheck for items?**</span></span> <span data-ttu-id="893b0-135">Te wartości Ustaw częstotliwość aplikacji logiki hello sprawdza, czy aktualizacje pokrewne toohello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="893b0-135">These values set how often hello logic app checks for updates related toohello trigger.</span></span> <span data-ttu-id="893b0-136">ustawienie domyślne Hello jest toocheck aktualizacje co trzy minuty.</span><span class="sxs-lookup"><span data-stu-id="893b0-136">hello default setting is toocheck for updates every three minutes.</span></span>

    * <span data-ttu-id="893b0-137">**Częstotliwość**.</span><span class="sxs-lookup"><span data-stu-id="893b0-137">**Frequency**.</span></span> <span data-ttu-id="893b0-138">Wybierz sekundy, minuty, godziny lub dni.</span><span class="sxs-lookup"><span data-stu-id="893b0-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="893b0-139">**Interwał**.</span><span class="sxs-lookup"><span data-stu-id="893b0-139">**Interval**.</span></span> <span data-ttu-id="893b0-140">Wprowadź liczbę hello sekundy, minuty, godziny lub dni, które mają toopass przed hello następnego zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="893b0-140">Enter hello number of seconds, minutes, hours, or days that you want toopass before hello next check.</span></span>

      ![Szczegóły wyzwalaczem aplikacji logiki](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="893b0-142">Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="893b0-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="893b0-143">W polu wyszukiwania hello wpisz `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="893b0-143">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="893b0-144">Wybierz z listy akcji hello **Dynamics 365 — Utwórz nowy rekord**.</span><span class="sxs-lookup"><span data-stu-id="893b0-144">From hello actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="893b0-145">Wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="893b0-145">Enter hello following information:</span></span>

    * <span data-ttu-id="893b0-146">**Nazwa organizacji**.</span><span class="sxs-lookup"><span data-stu-id="893b0-146">**Organization Name**.</span></span> <span data-ttu-id="893b0-147">Wybierz wystąpienie hello Dynamics 365 miejscu hello przepływu toocreate hello rekordu.</span><span class="sxs-lookup"><span data-stu-id="893b0-147">Select hello Dynamics 365 instance where you want hello flow toocreate hello record.</span></span> 
    <span data-ttu-id="893b0-148">Powiadomienie, że to wystąpienie nie ma toobe hello sam gdzie hello zdarzenie zostanie wyzwolone z wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="893b0-148">Notice that this instance doesn’t have toobe hello same instance where hello event is triggered from.</span></span>

    * <span data-ttu-id="893b0-149">**Nazwa jednostki**.</span><span class="sxs-lookup"><span data-stu-id="893b0-149">**Entity Name**.</span></span> <span data-ttu-id="893b0-150">Wybierz jednostki hello mają toocreate rekordu, po wyzwoleniu hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="893b0-150">Select hello entity that you want toocreate a record when hello event is triggered.</span></span> 
    <span data-ttu-id="893b0-151">W tym przewodniku **zadania** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="893b0-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="893b0-152">Kliknij hello **podmiotu** pojawi się okno.</span><span class="sxs-lookup"><span data-stu-id="893b0-152">Click in hello **Subject** box that appears.</span></span> <span data-ttu-id="893b0-153">Z hello dynamicznej zawartości listy możesz wybrać jedną z tych pól:</span><span class="sxs-lookup"><span data-stu-id="893b0-153">From hello dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="893b0-154">**Nazwisko**.</span><span class="sxs-lookup"><span data-stu-id="893b0-154">**Last Name**.</span></span> <span data-ttu-id="893b0-155">Zaznaczenie tego pola wstawia hello nazwisko potencjalnego powitania klienta do hello pole tematu dla zadania hello, po utworzeniu rekordu zadań hello.</span><span class="sxs-lookup"><span data-stu-id="893b0-155">Selecting this field inserts hello last name for hello lead into hello Subject field for hello task, when hello task record is created.</span></span>
    * <span data-ttu-id="893b0-156">**Temat**.</span><span class="sxs-lookup"><span data-stu-id="893b0-156">**Topic**.</span></span> <span data-ttu-id="893b0-157">Zaznaczenie tego pola pola wstawia hello tematu dla realizacji hello w polu podmiotu hello hello zadania po hello zadań zostaje utworzony rekord.</span><span class="sxs-lookup"><span data-stu-id="893b0-157">Selecting this field inserts hello Topic field for hello lead into hello Subject field for hello task, when hello task record is created.</span></span> 
    <span data-ttu-id="893b0-158">Kliknij przycisk **tematu** tooadd tego toohello **podmiotu** pole.</span><span class="sxs-lookup"><span data-stu-id="893b0-158">Click **Topic** tooadd that toohello **Subject** box.</span></span>

      ![Logiki aplikacji Utwórz nowe szczegóły rekordu](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="893b0-160">Na powitania narzędzi Projektanta aplikacji logiki, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="893b0-160">On hello Logic App Designer toolbar, click **Save**.</span></span>

    ![Narzędzi Projektanta aplikacji logiki Zapisz](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="893b0-162">Witaj toostart aplikacji logiki, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="893b0-162">toostart hello Logic App, click **Run**.</span></span>

    ![Narzędzi Projektanta aplikacji logiki Zapisz](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="893b0-164">Teraz Utwórz rekord realizacji w 365 Dynamics działu sprzedaży i zobacz Twojej przepływu w akcji!</span><span class="sxs-lookup"><span data-stu-id="893b0-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="893b0-165">Ustaw opcje zaawansowane kroku aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="893b0-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="893b0-166">toospecify jak toofilter danych w kroku aplikacji logiki, kliknij przycisk **Pokaż zaawansowane opcje** w tym kroku, następnie dodać filtr lub kolejności przez zapytanie.</span><span class="sxs-lookup"><span data-stu-id="893b0-166">toospecify how toofilter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="893b0-167">Na przykład można użyć filtru kont tylko aktywnych tooget zapytania i kolejność według nazwy konta hello.</span><span class="sxs-lookup"><span data-stu-id="893b0-167">For example, you can use a filter query tooget only active accounts and order by hello account name.</span></span> <span data-ttu-id="893b0-168">tooperform to zadanie, wprowadź zapytanie filtru OData hello `statuscode eq 1`i wybierz **nazwa konta** z hello listy zawartości dynamicznej.</span><span class="sxs-lookup"><span data-stu-id="893b0-168">tooperform this task, enter hello OData filter query `statuscode eq 1`, and select **Account Name** from hello dynamic content list.</span></span> <span data-ttu-id="893b0-169">Więcej informacji: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) i [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="893b0-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Zaawansowane opcje aplikacji logiki](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="893b0-171">Najlepsze rozwiązania przy użyciu opcji zaawansowanych</span><span class="sxs-lookup"><span data-stu-id="893b0-171">Best practices when using advanced options</span></span>

<span data-ttu-id="893b0-172">Po dodaniu pola tooa wartości musi odpowiadać typowi pola hello, wpisz wartość lub wybierz wartość z listy hello dynamicznej zawartości.</span><span class="sxs-lookup"><span data-stu-id="893b0-172">When you add a value tooa field, you must match hello field type whether you type a value or select a value from hello dynamic content list.</span></span>

<span data-ttu-id="893b0-173">Typ pola</span><span class="sxs-lookup"><span data-stu-id="893b0-173">Field type</span></span>  |<span data-ttu-id="893b0-174">Jak toouse</span><span class="sxs-lookup"><span data-stu-id="893b0-174">How toouse</span></span>  |<span data-ttu-id="893b0-175">Gdzie toofind</span><span class="sxs-lookup"><span data-stu-id="893b0-175">Where toofind</span></span>  |<span data-ttu-id="893b0-176">Nazwa</span><span class="sxs-lookup"><span data-stu-id="893b0-176">Name</span></span>  |<span data-ttu-id="893b0-177">Typ danych</span><span class="sxs-lookup"><span data-stu-id="893b0-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="893b0-178">Pola tekstowe</span><span class="sxs-lookup"><span data-stu-id="893b0-178">Text fields</span></span>|<span data-ttu-id="893b0-179">Pola tekstowe wymagają pojedynczy wiersz tekstu lub zawartość dynamiczną, która jest polem typu tekst.</span><span class="sxs-lookup"><span data-stu-id="893b0-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="893b0-180">Przykładami pola kategorii i podkategorii hello.</span><span class="sxs-lookup"><span data-stu-id="893b0-180">Examples include hello Category and Sub-Category fields.</span></span>|<span data-ttu-id="893b0-181">Ustawienia > dostosowania > Dostosuj hello systemu > jednostki > zadań > pól</span><span class="sxs-lookup"><span data-stu-id="893b0-181">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="893b0-182">category</span><span class="sxs-lookup"><span data-stu-id="893b0-182">category</span></span> |<span data-ttu-id="893b0-183">Pojedynczy wiersz tekstu</span><span class="sxs-lookup"><span data-stu-id="893b0-183">Single Line of Text</span></span>        
<span data-ttu-id="893b0-184">Pola Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="893b0-184">Integer fields</span></span> | <span data-ttu-id="893b0-185">Niektóre pola wymagają liczbą całkowitą lub zawartość dynamiczną, która jest typu Integer.</span><span class="sxs-lookup"><span data-stu-id="893b0-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="893b0-186">Przykładami procent wykonania i czasu trwania.</span><span class="sxs-lookup"><span data-stu-id="893b0-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="893b0-187">Ustawienia > dostosowania > Dostosuj hello systemu > jednostki > zadań > pól</span><span class="sxs-lookup"><span data-stu-id="893b0-187">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="893b0-188">ProcentWykonania</span><span class="sxs-lookup"><span data-stu-id="893b0-188">percentcomplete</span></span> |<span data-ttu-id="893b0-189">Liczby całkowitej</span><span class="sxs-lookup"><span data-stu-id="893b0-189">Whole Number</span></span>         
<span data-ttu-id="893b0-190">Pola dat</span><span class="sxs-lookup"><span data-stu-id="893b0-190">Date fields</span></span> | <span data-ttu-id="893b0-191">Niektóre pola wymagają datę wprowadzenia w formacie mm/dd/rrrr lub zawartość dynamiczną, która jest pola typu daty.</span><span class="sxs-lookup"><span data-stu-id="893b0-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="893b0-192">Przykładami utworzenia, datę rozpoczęcia, Rozpoczęcie rzeczywiste ostatnio na czas przechowywania, rzeczywiste zakończenie i terminu.</span><span class="sxs-lookup"><span data-stu-id="893b0-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="893b0-193">Ustawienia > dostosowania > Dostosuj hello systemu > jednostki > zadań > pól</span><span class="sxs-lookup"><span data-stu-id="893b0-193">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="893b0-194">pól createdon</span><span class="sxs-lookup"><span data-stu-id="893b0-194">createdon</span></span> |<span data-ttu-id="893b0-195">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="893b0-195">Date and Time</span></span>
<span data-ttu-id="893b0-196">Typ pola, które wymagają zarówno Identyfikatora rekordu i wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="893b0-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="893b0-197">Niektóre pola, które odwołują się do innego rekordu jednostki wymagają zarówno identyfikator rekordu hello i hello typ wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="893b0-197">Some fields that reference another entity record require both hello record ID and hello lookup type.</span></span> |<span data-ttu-id="893b0-198">Ustawienia > dostosowania > Dostosuj hello systemu > jednostki > konto > pól</span><span class="sxs-lookup"><span data-stu-id="893b0-198">Settings > Customizations > Customize hello System > Entities > Account > Fields</span></span>  | <span data-ttu-id="893b0-199">AccountID</span><span class="sxs-lookup"><span data-stu-id="893b0-199">accountid</span></span>  | <span data-ttu-id="893b0-200">Klucz podstawowy</span><span class="sxs-lookup"><span data-stu-id="893b0-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="893b0-201">Wpisz więcej przykładów dotyczących pola, które wymagają identyfikator rekordu i wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="893b0-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="893b0-202">Rozszerzając hello poprzedniej tabeli, Oto przykłady więcej pól, które nie działają z wartościami wybrany z listy zawartości dynamicznej hello.</span><span class="sxs-lookup"><span data-stu-id="893b0-202">Expanding on hello previous table, here are more examples of fields that don't work with values selected from hello dynamic content list.</span></span> <span data-ttu-id="893b0-203">Zamiast tego te pola wymagają zarówno identyfikator i wyszukiwania typ rekordu wprowadzany do pól hello w rozwiązaniu PowerApps.</span><span class="sxs-lookup"><span data-stu-id="893b0-203">Instead, these fields require both a record ID and lookup type entered into hello fields in PowerApps.</span></span>  
* <span data-ttu-id="893b0-204">Właściciel i typ właściciela.</span><span class="sxs-lookup"><span data-stu-id="893b0-204">Owner and Owner Type.</span></span> <span data-ttu-id="893b0-205">pole właściciela Hello musi zawierać prawidłowy identyfikator rekordu użytkownika lub zespołu</span><span class="sxs-lookup"><span data-stu-id="893b0-205">hello Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="893b0-206">Hello właściciela typu musi być równa albo **systemusers** lub **zespołów**.</span><span class="sxs-lookup"><span data-stu-id="893b0-206">hello Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="893b0-207">Klienta i typ klienta.</span><span class="sxs-lookup"><span data-stu-id="893b0-207">Customer and Customer Type.</span></span> <span data-ttu-id="893b0-208">powitania klienta pola musi być prawidłowym kontem lub skontaktuj się z identyfikator rekordu.</span><span class="sxs-lookup"><span data-stu-id="893b0-208">hello Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="893b0-209">Hello właściciela typu musi być równa albo **kont** lub **kontaktów**.</span><span class="sxs-lookup"><span data-stu-id="893b0-209">hello Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="893b0-210">Dotyczące oraz dotyczące typu.</span><span class="sxs-lookup"><span data-stu-id="893b0-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="893b0-211">Witaj dotyczących pola musi być prawidłowy rekord identyfikator, takie jak konto lub skontaktuj się z identyfikator rekordu.</span><span class="sxs-lookup"><span data-stu-id="893b0-211">hello Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="893b0-212">Hello dotyczące typ musi być typ wyszukiwania hello hello rekordu, takich jak **kont** lub **kontaktów**.</span><span class="sxs-lookup"><span data-stu-id="893b0-212">hello Regarding Type must be hello lookup type for hello record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="893b0-213">Witaj poniższy przykład akcji tworzenia zadań dodaje odpowiadający toohello identyfikator rekordu, dodając toohello dotyczących pola hello zadania konta.</span><span class="sxs-lookup"><span data-stu-id="893b0-213">hello following task creation action example adds an account record that corresponds toohello record ID adding it toohello regarding field of hello task.</span></span>

![Konto przepływu recordId i typ](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="893b0-215">W tym przykładzie przypisuje także hello zadań tooa określonego użytkownika na podstawie identyfikatora użytkownika hello rekordu.</span><span class="sxs-lookup"><span data-stu-id="893b0-215">This example also assigns hello task tooa specific user based on hello user's record ID.</span></span>

![Konto przepływu recordId i typ](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="893b0-217">toofind rekordu przez identyfikator, zobacz hello następujących sekcji: *Znajdź identyfikator rekordu hello*</span><span class="sxs-lookup"><span data-stu-id="893b0-217">toofind a record's ID, see hello following section: *Find hello record ID*</span></span>

## <a name="find-hello-record-id"></a><span data-ttu-id="893b0-218">Znajdź identyfikator rekordu hello</span><span class="sxs-lookup"><span data-stu-id="893b0-218">Find hello record ID</span></span>

1. <span data-ttu-id="893b0-219">Otwórz rekord, takich jak konta.</span><span class="sxs-lookup"><span data-stu-id="893b0-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="893b0-220">Na pasku narzędzi Akcje hello, kliknij przycisk **Pop limit** ![rekordu podręczne](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="893b0-220">On hello actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="893b0-221">Alternatywnie na powitania akcje narzędzi toocopy hello pełny adres URL do domyślnego programu poczty e-mail, kliknij **łącze E-mail**.</span><span class="sxs-lookup"><span data-stu-id="893b0-221">Alternatively, on hello actions toolbar, toocopy hello full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="893b0-222">Identyfikator rekordu Hello jest wyświetlany Between hello % 7b i %7 d kodowania znaków hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="893b0-222">hello record ID is displayed in between hello %7b and %7d encoding characters of hello URL.</span></span>

   ![Konto przepływu recordId i typ](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="893b0-224">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="893b0-224">Troubleshooting</span></span>
<span data-ttu-id="893b0-225">tootroubleshoot krok zakończony niepowodzeniem w aplikacji logiki, Wyświetl szczegóły stanu hello hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="893b0-225">tootroubleshoot a failed step in a logic app, view hello status details of hello event.</span></span>

1. <span data-ttu-id="893b0-226">W obszarze **Logic Apps**, wybierz aplikację logiki, a następnie kliknij przycisk **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="893b0-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="893b0-227">Hello obszar Podsumowanie zawiera stan hello uruchamiania dla aplikacji logiki hello, jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="893b0-227">hello Summary area is shown and provides hello run status for hello logic app.</span></span> 

   ![Stan uruchomienia aplikacji logiki](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="893b0-229">tooview więcej informacji na temat dowolnego przebiegów nie powiodło się, kliknij przycisk hello nie powiodło się zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="893b0-229">tooview more information about any failed runs, click hello failed event.</span></span> <span data-ttu-id="893b0-230">tooexpand krok zakończony niepowodzeniem, kliknij ten krok.</span><span class="sxs-lookup"><span data-stu-id="893b0-230">tooexpand a failed step, click that step.</span></span>

   ![Rozwiń węzeł krok zakończony niepowodzeniem](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="893b0-232">szczegółowe informacje krok Hello wyświetlane i mogą pomóc rozwiązać hello przyczynę błędu na powitania.</span><span class="sxs-lookup"><span data-stu-id="893b0-232">hello step details appear and can help troubleshoot hello cause of hello failure.</span></span>

   ![Nie można uzyskać szczegółowe informacje krok](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="893b0-234">Aby uzyskać więcej informacji na temat rozwiązywania problemów z aplikacji logiki, zobacz [diagnozowanie błędów aplikacji logiki](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="893b0-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="893b0-235">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="893b0-235">Connector-specific details</span></span>

<span data-ttu-id="893b0-236">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="893b0-236">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="893b0-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="893b0-237">Next steps</span></span>
<span data-ttu-id="893b0-238">Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="893b0-238">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
