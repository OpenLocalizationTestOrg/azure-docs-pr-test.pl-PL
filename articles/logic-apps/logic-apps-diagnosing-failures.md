---
title: "błędy aaaDiagnose — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Typowe toounderstand metody, gdzie aplikacje logiki kończą się niepowodzeniem"
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
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="1b46c-103">Diagnozowanie błędów aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="1b46c-103">Diagnose logic app failures</span></span>
<span data-ttu-id="1b46c-104">Jeśli wystąpią problemy lub awarie z aplikacji logiki istnieje kilka metod pomaga lepiej zrozumieć, w którym błędów hello pochodzą z.</span><span class="sxs-lookup"><span data-stu-id="1b46c-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where hello failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="1b46c-105">Narzędzia do portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1b46c-105">Azure portal tools</span></span>
<span data-ttu-id="1b46c-106">Hello portalu Azure udostępnia wiele narzędzi toodiagnose każdej aplikacji logiki w każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="1b46c-106">hello Azure portal provides many tools toodiagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="1b46c-107">Historia wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="1b46c-107">Trigger history</span></span>

<span data-ttu-id="1b46c-108">Każda aplikacja logiki ma przynajmniej jeden wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="1b46c-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="1b46c-109">Jeśli okaże się, że aplikacje nie są wyzwalania, przyjrzeć hello wyzwalacza historii, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="1b46c-109">If you notice that apps aren't firing, look first at hello trigger history for more information.</span></span> <span data-ttu-id="1b46c-110">Jest dostępna Historia wyzwalacza hello na powitania logiki app'ss głównego bloku.</span><span class="sxs-lookup"><span data-stu-id="1b46c-110">You can access hello trigger history on hello logic app'ss main blade.</span></span>

![Lokalizowanie hello wyzwalacza historii][1]

<span data-ttu-id="1b46c-112">Historia wyzwalacza Hello Wyświetla wszystkie próby wyzwalacza wprowadzone przez aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="1b46c-112">hello trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="1b46c-113">Po kliknięciu każdego toodrill próba wyzwalacza hello uzyskać szczegółowe informacje, w szczególności, wszelkie danych wejściowych lub wygenerowane dane wyjściowe, które hello próba wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="1b46c-113">You can click each trigger attempt toodrill into hello details, specifically, any inputs or outputs that hello trigger attempt generated.</span></span> <span data-ttu-id="1b46c-114">Jeśli okaże się wyzwalaczy nie powiodło się, zaznacz hello próba wyzwalacza i wybierz polecenie hello **dane wyjściowe** link tooreview wszelkie wygenerowane komunikaty o błędach, na przykład dla poświadczeń FTP, które nie są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="1b46c-114">If you find failed triggers, select hello trigger attempt and choose hello **Outputs** link tooreview any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="1b46c-115">Witaj różne stany, które można napotkać są:</span><span class="sxs-lookup"><span data-stu-id="1b46c-115">hello different statuses you might see are:</span></span>

* <span data-ttu-id="1b46c-116">**Pominięto**.</span><span class="sxs-lookup"><span data-stu-id="1b46c-116">**Skipped**.</span></span> <span data-ttu-id="1b46c-117">punkt końcowy Hello został toocheck próbkowania dla danych i Odebrano odpowiedź, że dane nie zostały dostępne.</span><span class="sxs-lookup"><span data-stu-id="1b46c-117">hello endpoint was polled toocheck for data and received a response that no data was available.</span></span>
* <span data-ttu-id="1b46c-118">**Pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="1b46c-118">**Succeeded**.</span></span> <span data-ttu-id="1b46c-119">wyzwalacz Hello odebrał odpowiedź, aby dane były dostępne.</span><span class="sxs-lookup"><span data-stu-id="1b46c-119">hello trigger received a response that data was available.</span></span> <span data-ttu-id="1b46c-120">Ten stan może wynikać z ręcznego wyzwalacza, wyzwalacz cyklu lub wyzwalacza sondowania.</span><span class="sxs-lookup"><span data-stu-id="1b46c-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="1b46c-121">Ten stan jest zazwyczaj towarzyszy hello **Fired** stanu, ale może nie być, jeśli masz warunku lub polecenia SplitOn w widoku kodu, który nie został spełniony.</span><span class="sxs-lookup"><span data-stu-id="1b46c-121">This status is usually accompanied by hello **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="1b46c-122">**Nie powiodło się**.</span><span class="sxs-lookup"><span data-stu-id="1b46c-122">**Failed**.</span></span> <span data-ttu-id="1b46c-123">Wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="1b46c-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="1b46c-124">Ręcznie uruchomić wyzwalacz</span><span class="sxs-lookup"><span data-stu-id="1b46c-124">Start a trigger manually</span></span>

<span data-ttu-id="1b46c-125">Toocheck aplikacji logiki hello wyzwalacza dostępne natychmiast bez oczekiwania na następne wystąpienie hello, kliknij przycisk **wybierz wyzwalacz** na powitania głównego bloku tooforce wyboru.</span><span class="sxs-lookup"><span data-stu-id="1b46c-125">If you want hello logic app toocheck for an available trigger immediately without waiting for hello next recurrence, click **Select Trigger** on hello main blade tooforce a check.</span></span> <span data-ttu-id="1b46c-126">Na przykład kliknięcie tego łącza z wyzwalaczem skrzynki powoduje, że przepływ pracy hello tooimmediately sondowania skrzynki dla nowych plików.</span><span class="sxs-lookup"><span data-stu-id="1b46c-126">For example, clicking this link with a Dropbox trigger causes hello workflow tooimmediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="1b46c-127">Historia uruchomień</span><span class="sxs-lookup"><span data-stu-id="1b46c-127">Run history</span></span>

<span data-ttu-id="1b46c-128">Każdy wypalane wyzwalacz powoduje do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="1b46c-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="1b46c-129">Można uzyskać dostępu do informacji o uruchamianiu w głównym bloku hello, zawierający wiele szczegółowe informacje, które mogą pomóc Ci zrozumieć, co się stało podczas hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="1b46c-129">You can access run information from hello main blade, which contains many details that can help you understand what happened during hello workflow.</span></span>

![Lokalizowanie hello Historia uruchomień][2]

<span data-ttu-id="1b46c-131">Uruchom wyświetli jeden z hello następujące stany:</span><span class="sxs-lookup"><span data-stu-id="1b46c-131">A run displays one of hello following statuses:</span></span>

* <span data-ttu-id="1b46c-132">**Pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="1b46c-132">**Succeeded**.</span></span> <span data-ttu-id="1b46c-133">Wszystkie akcje zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="1b46c-133">All actions succeeded.</span></span> <span data-ttu-id="1b46c-134">Jeśli wystąpił błąd, aby awaria była obsługiwana przez akcji, która wystąpiła w dalszej części hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="1b46c-134">If a failure happened, that failure was handled by an action that occurred later in hello workflow.</span></span> <span data-ttu-id="1b46c-135">Oznacza to błąd hello była obsługiwana przez akcję, która została ustawiona toorun po akcji nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="1b46c-135">That is, hello failure was handled by an action that was set toorun after a failed action.</span></span>
* <span data-ttu-id="1b46c-136">**Nie powiodło się**.</span><span class="sxs-lookup"><span data-stu-id="1b46c-136">**Failed**.</span></span> <span data-ttu-id="1b46c-137">Co najmniej jedną akcję wystąpił błąd, który nie został obsłużony przez akcję później w przepływie pracy hello.</span><span class="sxs-lookup"><span data-stu-id="1b46c-137">At least one action had a failure that was not handled by an action later in hello workflow.</span></span>
* <span data-ttu-id="1b46c-138">**Anulowane**.</span><span class="sxs-lookup"><span data-stu-id="1b46c-138">**Cancelled**.</span></span> <span data-ttu-id="1b46c-139">Hello przepływu pracy została uruchomiona, ale otrzymano żądanie anulowania.</span><span class="sxs-lookup"><span data-stu-id="1b46c-139">hello workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="1b46c-140">**Uruchomiona**.</span><span class="sxs-lookup"><span data-stu-id="1b46c-140">**Running**.</span></span> <span data-ttu-id="1b46c-141">Witaj w przepływie pracy jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="1b46c-141">hello workflow is currently running.</span></span> <span data-ttu-id="1b46c-142">Ten stan może wystąpić dla przepływów pracy z ograniczeniem przepustowości lub z powodu hello bieżącego cennika planu.</span><span class="sxs-lookup"><span data-stu-id="1b46c-142">This status might occur for throttled workflows, or because of hello current pricing plan.</span></span> <span data-ttu-id="1b46c-143">Aby uzyskać więcej informacji, zobacz [limity akcji na stronie dotyczącej cen hello](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="1b46c-143">For details, see [action limits on hello pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="1b46c-144">Konfigurowanie diagnostyki (hello wykresy, które są wyświetlane w obszarze Historia uruchomień hello) również może zawierają informacje dotyczące zdarzeń ograniczania zachodzące.</span><span class="sxs-lookup"><span data-stu-id="1b46c-144">Configuring diagnostics (hello charts that appear under hello run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="1b46c-145">Jeśli przeglądasz Historia uruchomień mogą przejść więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="1b46c-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="1b46c-146">Dane wyjściowe wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="1b46c-146">Trigger outputs</span></span>

<span data-ttu-id="1b46c-147">Wyzwalacz generuje hello danych pochodzi z hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="1b46c-147">Trigger outputs show hello data that came from hello trigger.</span></span> <span data-ttu-id="1b46c-148">Te dane wyjściowe może pomóc w określeniu, czy wszystkie właściwości zwracane zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="1b46c-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="1b46c-149">Jeśli widzisz zawartość, która nie rozumie, Dowiedz się, jak Azure Logic Apps [obsługuje różne typy zawartości](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="1b46c-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Przykładowe dane wyjściowe wyzwalacza][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="1b46c-151">Akcja wejścia i wyjścia</span><span class="sxs-lookup"><span data-stu-id="1b46c-151">Action inputs and outputs</span></span>

<span data-ttu-id="1b46c-152">Aby przejść do szczegółów w hello wejściach i wyjściach, które otrzymały akcji.</span><span class="sxs-lookup"><span data-stu-id="1b46c-152">You can drill into hello inputs and outputs that an action received.</span></span> <span data-ttu-id="1b46c-153">Dane te są przydatne dla zrozumienia hello wielkość i kształt hello wyniki, a także do znajdowania komunikaty o błędach, które mogą zostać wygenerowane.</span><span class="sxs-lookup"><span data-stu-id="1b46c-153">This data is useful for understanding hello size and shape of hello outputs, and also for finding any error messages that might have been generated.</span></span>

![Akcja wejścia i wyjścia][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="1b46c-155">Debugowanie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="1b46c-155">Debug workflow runtime</span></span>

<span data-ttu-id="1b46c-156">Wraz z monitorowania hello wejść, wyjść i wyzwalaczy Uruchom, można dodać niektóre kroki tooa przepływ pracy pomocy z debugowaniem.</span><span class="sxs-lookup"><span data-stu-id="1b46c-156">Along with monitoring hello inputs, outputs, and triggers of a run, you could add some steps tooa workflow that help with debugging.</span></span> 
<span data-ttu-id="1b46c-157">[RequestBin](http://requestb.in) jest zaawansowanym narzędziem, które można dodać krokiem w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="1b46c-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="1b46c-158">Przy użyciu RequestBin, można skonfigurować protokołu HTTP żądania inspektora toodetermine hello dokładny rozmiar, kształt i format żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="1b46c-158">By using RequestBin, you can set up an HTTP request inspector toodetermine hello exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="1b46c-159">Można tworzyć RequestBin i wklej adres URL hello w aplikacji logiki akcji HTTP POST z zawartości treści, które mają tootest, na przykład, wyrażenie lub inny krok danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="1b46c-159">You can create a RequestBin and paste hello URL in a logic app HTTP POST action with body content that you want tootest, for example, an expression or another step output.</span></span> <span data-ttu-id="1b46c-160">Po uruchomieniu aplikacji logiki hello można odświeżyć Twojej toosee RequestBin jak Żądanie hello został utworzony podczas generowania z hello aplikacje logiki aparatu.</span><span class="sxs-lookup"><span data-stu-id="1b46c-160">After you run hello logic app, you can refresh your RequestBin toosee how hello request was formed when generated from hello Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
