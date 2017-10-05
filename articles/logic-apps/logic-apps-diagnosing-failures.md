---
title: "Diagnozowanie błędów - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Typowe sposoby zrozumieć, w którym aplikacje logiki kończą się niepowodzeniem"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 814e6f93088cdd96b0a663d2a7494b5a11470d99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="8197c-103">Diagnozowanie błędów aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="8197c-103">Diagnose logic app failures</span></span>
<span data-ttu-id="8197c-104">Występują problemy lub awarie z aplikacji logiki, istnieje kilka metod pomaga lepiej zrozumieć, w których pochodzą z błędami.</span><span class="sxs-lookup"><span data-stu-id="8197c-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where the failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="8197c-105">Narzędzia do portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8197c-105">Azure portal tools</span></span>
<span data-ttu-id="8197c-106">Azure portal udostępnia wiele narzędzi do diagnozowania każdej aplikacji logiki w każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="8197c-106">The Azure portal provides many tools to diagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="8197c-107">Historia wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="8197c-107">Trigger history</span></span>

<span data-ttu-id="8197c-108">Każda aplikacja logiki ma przynajmniej jeden wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="8197c-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="8197c-109">Jeśli okaże się, że aplikacje nie są wyzwalania, przyjrzeć historii wyzwalacza, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="8197c-109">If you notice that apps aren't firing, look first at the trigger history for more information.</span></span> <span data-ttu-id="8197c-110">Jest dostępna Historia wyzwalacza w głównym bloku app'ss logiki.</span><span class="sxs-lookup"><span data-stu-id="8197c-110">You can access the trigger history on the logic app'ss main blade.</span></span>

![Lokalizowanie historii wyzwalacza][1]

<span data-ttu-id="8197c-112">Historia wyzwalacza zawiera listę wszystkich prób wyzwalacza wprowadzone przez aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="8197c-112">The trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="8197c-113">Możesz kliknąć każdej próbie wyzwalacza informacji szczegółowych, w szczególności, wszystkie dane wejściowe lub danych wyjściowych wygenerowanych przy próbie wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="8197c-113">You can click each trigger attempt to drill into the details, specifically, any inputs or outputs that the trigger attempt generated.</span></span> <span data-ttu-id="8197c-114">Jeśli okaże się wyzwalaczy nie powiodło się, zaznacz próba wyzwalacza i wybierz polecenie **dane wyjściowe** łącze, aby wyświetlić wygenerowany komunikaty o błędach, na przykład dla poświadczeń FTP, które nie są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="8197c-114">If you find failed triggers, select the trigger attempt and choose the **Outputs** link to review any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="8197c-115">Różne stany, które można napotkać są:</span><span class="sxs-lookup"><span data-stu-id="8197c-115">The different statuses you might see are:</span></span>

* <span data-ttu-id="8197c-116">**Pominięto**.</span><span class="sxs-lookup"><span data-stu-id="8197c-116">**Skipped**.</span></span> <span data-ttu-id="8197c-117">Punkt końcowy został sondowane do sprawdzenia danych i Odebrano odpowiedź, że dane nie zostały dostępne.</span><span class="sxs-lookup"><span data-stu-id="8197c-117">The endpoint was polled to check for data and received a response that no data was available.</span></span>
* <span data-ttu-id="8197c-118">**Pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="8197c-118">**Succeeded**.</span></span> <span data-ttu-id="8197c-119">Wyzwalacz odebrał odpowiedź, aby dane były dostępne.</span><span class="sxs-lookup"><span data-stu-id="8197c-119">The trigger received a response that data was available.</span></span> <span data-ttu-id="8197c-120">Ten stan może wynikać z ręcznego wyzwalacza, wyzwalacz cyklu lub wyzwalacza sondowania.</span><span class="sxs-lookup"><span data-stu-id="8197c-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="8197c-121">Ten stan jest zazwyczaj towarzyszy **Fired** stanu, ale może nie być, jeśli masz warunku lub polecenia SplitOn w widoku kodu, który nie został spełniony.</span><span class="sxs-lookup"><span data-stu-id="8197c-121">This status is usually accompanied by the **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="8197c-122">**Nie powiodło się**.</span><span class="sxs-lookup"><span data-stu-id="8197c-122">**Failed**.</span></span> <span data-ttu-id="8197c-123">Wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="8197c-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="8197c-124">Ręcznie uruchomić wyzwalacz</span><span class="sxs-lookup"><span data-stu-id="8197c-124">Start a trigger manually</span></span>

<span data-ttu-id="8197c-125">Sprawdź, czy wyzwalacz dostępne natychmiast bez oczekiwania na następne wystąpienie aplikacji logiki, kliknij przycisk **wybierz wyzwalacz** w głównym bloku, aby wymusić sprawdzenie.</span><span class="sxs-lookup"><span data-stu-id="8197c-125">If you want the logic app to check for an available trigger immediately without waiting for the next recurrence, click **Select Trigger** on the main blade to force a check.</span></span> <span data-ttu-id="8197c-126">Na przykład kliknięcie tego łącza z wyzwalaczem skrzynki powoduje przepływu pracy natychmiast wykonać sondowanie skrzynki dla nowych plików.</span><span class="sxs-lookup"><span data-stu-id="8197c-126">For example, clicking this link with a Dropbox trigger causes the workflow to immediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="8197c-127">Historia uruchomień</span><span class="sxs-lookup"><span data-stu-id="8197c-127">Run history</span></span>

<span data-ttu-id="8197c-128">Każdy wypalane wyzwalacz powoduje do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="8197c-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="8197c-129">Można uzyskać dostępu do informacji o uruchamianiu w głównym bloku zawierający wiele szczegółowe informacje, które mogą pomóc Ci zrozumieć, co się stało podczas przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="8197c-129">You can access run information from the main blade, which contains many details that can help you understand what happened during the workflow.</span></span>

![Lokalizowanie Historia uruchomień][2]

<span data-ttu-id="8197c-131">Uruchom zawiera jedną z następujących stanów:</span><span class="sxs-lookup"><span data-stu-id="8197c-131">A run displays one of the following statuses:</span></span>

* <span data-ttu-id="8197c-132">**Pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="8197c-132">**Succeeded**.</span></span> <span data-ttu-id="8197c-133">Wszystkie akcje zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="8197c-133">All actions succeeded.</span></span> <span data-ttu-id="8197c-134">Jeśli wystąpił błąd, aby awaria była obsługiwana przez akcję, który wystąpił w dalszej części przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="8197c-134">If a failure happened, that failure was handled by an action that occurred later in the workflow.</span></span> <span data-ttu-id="8197c-135">Oznacza to błąd była obsługiwana przez akcję, która została ustawiona do uruchomienia po akcji nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="8197c-135">That is, the failure was handled by an action that was set to run after a failed action.</span></span>
* <span data-ttu-id="8197c-136">**Nie powiodło się**.</span><span class="sxs-lookup"><span data-stu-id="8197c-136">**Failed**.</span></span> <span data-ttu-id="8197c-137">Co najmniej jedną akcję wystąpił błąd, który nie został obsłużony przez akcję później w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="8197c-137">At least one action had a failure that was not handled by an action later in the workflow.</span></span>
* <span data-ttu-id="8197c-138">**Anulowane**.</span><span class="sxs-lookup"><span data-stu-id="8197c-138">**Cancelled**.</span></span> <span data-ttu-id="8197c-139">Przepływ pracy był uruchomiony, ale Odebrano żądanie anulowania.</span><span class="sxs-lookup"><span data-stu-id="8197c-139">The workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="8197c-140">**Uruchomiona**.</span><span class="sxs-lookup"><span data-stu-id="8197c-140">**Running**.</span></span> <span data-ttu-id="8197c-141">Przepływ pracy jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="8197c-141">The workflow is currently running.</span></span> <span data-ttu-id="8197c-142">Ten stan może wystąpić dla przepływów pracy z ograniczeniem przepustowości lub z powodu bieżącego planu cenowego.</span><span class="sxs-lookup"><span data-stu-id="8197c-142">This status might occur for throttled workflows, or because of the current pricing plan.</span></span> <span data-ttu-id="8197c-143">Aby uzyskać więcej informacji, zobacz [limity akcji na stronie cen](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="8197c-143">For details, see [action limits on the pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="8197c-144">Konfigurowanie diagnostyki (wykresy, które są wyświetlane w obszarze Historia uruchomień) również może zawierają informacje dotyczące zdarzeń ograniczania zachodzące.</span><span class="sxs-lookup"><span data-stu-id="8197c-144">Configuring diagnostics (the charts that appear under the run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="8197c-145">Jeśli przeglądasz Historia uruchomień mogą przejść więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="8197c-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="8197c-146">Dane wyjściowe wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="8197c-146">Trigger outputs</span></span>

<span data-ttu-id="8197c-147">Dane wyjściowe wyzwalacza Pokaż dane, które nadeszły z wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="8197c-147">Trigger outputs show the data that came from the trigger.</span></span> <span data-ttu-id="8197c-148">Te dane wyjściowe może pomóc w określeniu, czy wszystkie właściwości zwracane zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="8197c-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="8197c-149">Jeśli widzisz zawartość, która nie rozumie, Dowiedz się, jak Azure Logic Apps [obsługuje różne typy zawartości](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="8197c-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Przykładowe dane wyjściowe wyzwalacza][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="8197c-151">Akcja wejścia i wyjścia</span><span class="sxs-lookup"><span data-stu-id="8197c-151">Action inputs and outputs</span></span>

<span data-ttu-id="8197c-152">Aby przejść do szczegółów w wejściach i wyjściach, które otrzymały akcji.</span><span class="sxs-lookup"><span data-stu-id="8197c-152">You can drill into the inputs and outputs that an action received.</span></span> <span data-ttu-id="8197c-153">Dane te są przydatne, aby zrozumieć wielkość i kształt dane wyjściowe, a także do znajdowania komunikaty o błędach, które mogą zostać wygenerowane.</span><span class="sxs-lookup"><span data-stu-id="8197c-153">This data is useful for understanding the size and shape of the outputs, and also for finding any error messages that might have been generated.</span></span>

![Akcja wejścia i wyjścia][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="8197c-155">Debugowanie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="8197c-155">Debug workflow runtime</span></span>

<span data-ttu-id="8197c-156">Wraz z monitorowania wejść, wyjść i wyzwalaczy Uruchom, niektóre kroki można dodać do przepływu pracy, które pomagają z debugowaniem.</span><span class="sxs-lookup"><span data-stu-id="8197c-156">Along with monitoring the inputs, outputs, and triggers of a run, you could add some steps to a workflow that help with debugging.</span></span> 
<span data-ttu-id="8197c-157">[RequestBin](http://requestb.in) jest zaawansowanym narzędziem, które można dodać krokiem w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="8197c-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="8197c-158">Przy użyciu RequestBin, można skonfigurować inspektora żądania HTTP do określenia dokładnej rozmiar, kształt i format żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="8197c-158">By using RequestBin, you can set up an HTTP request inspector to determine the exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="8197c-159">Można tworzyć RequestBin i wklej adres URL w aplikacji logiki akcji HTTP POST z zawartość treści, która ma zostać przetestowana, na przykład, wyrażenie lub inny krok danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="8197c-159">You can create a RequestBin and paste the URL in a logic app HTTP POST action with body content that you want to test, for example, an expression or another step output.</span></span> <span data-ttu-id="8197c-160">Po uruchomieniu aplikacji logiki możesz odświeżyć Twojej RequestBin, aby zobaczyć, jak żądania został utworzony podczas generowania z aparatu Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="8197c-160">After you run the logic app, you can refresh your RequestBin to see how the request was formed when generated from the Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
