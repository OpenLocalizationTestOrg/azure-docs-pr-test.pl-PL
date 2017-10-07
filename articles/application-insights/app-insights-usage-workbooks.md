---
title: "dane użycia aaaInvestigate i udziału z interaktywnego skoroszytów w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Analiza demograficznych użytkowników aplikacji sieci web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="97209-103">Badanie i udostępniać dane użycia interakcyjne skoroszytów w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="97209-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="97209-104">Łączenie skoroszytów [Azure Application Insights](app-insights-overview.md) wizualizacje danych [zapytania analityczne](app-insights-analytics.md)i tekstu w dokumentach interaktywnego.</span><span class="sxs-lookup"><span data-stu-id="97209-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="97209-105">Skoroszyty jest edytowany przez innych członków zespołu z toohello dostępu do tego samego zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="97209-105">Workbooks are editable by other team members with access toohello same Azure resource.</span></span> <span data-ttu-id="97209-106">Oznacza to, hello zapytania i formanty używane toocreate skoroszytu osób dostępne tooother odczytywania hello skoroszytu, dzięki czemu można je łatwo tooexplore, rozszerzać i sprawdź, czy błędy.</span><span class="sxs-lookup"><span data-stu-id="97209-106">This means hello queries and controls used toocreate a workbook are available tooother people reading hello workbook, making them easy tooexplore, extend, and check for mistakes.</span></span>

<span data-ttu-id="97209-107">Skoroszyty są przydatne w scenariuszach, takich jak:</span><span class="sxs-lookup"><span data-stu-id="97209-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="97209-108">Eksploracji hello użycia aplikacji, jeśli nie wiesz wcześniej metryki hello zainteresowania: liczby użytkowników, stawki przechowywania, kursy wymiany itp. W przeciwieństwie do innych narzędzi analizy użycia w usłudze Application Insights skoroszytów umożliwiają łączenie wielu rodzajów wizualizacje i analiz nadawania doskonałe rozwiązanie dla tego rodzaju dowolnych eksploracji.</span><span class="sxs-lookup"><span data-stu-id="97209-108">Exploring hello usage of your app when you don't know hello metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="97209-109">Wyjaśniający, jak działa funkcja nowo wydanego zespołu tooyour, przez użytkownika przedstawiający Liczba interakcji klucza i innych metryk.</span><span class="sxs-lookup"><span data-stu-id="97209-109">Explaining tooyour team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="97209-110">Udostępnianie wyników hello a / B eksperymentu w Twojej aplikacji za pomocą innych członków zespołu.</span><span class="sxs-lookup"><span data-stu-id="97209-110">Sharing hello results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="97209-111">Można wyjaśnić hello cele hello eksperymentować tekstu, a następnie Pokaż wszystkie metryki użycia i Analytics zapytanie użyte tooevaluate hello eksperymentu, wraz z wyczyść dokumentów wywołania do tego, czy wszystkie metryki został powyżej lub poniżej docelowe.</span><span class="sxs-lookup"><span data-stu-id="97209-111">You can explain hello goals for hello experiment with text, then show each usage metric and Analytics query used tooevaluate hello experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="97209-112">Raportowanie hello wpływ awarii na powitania użycia aplikacji, połączenie danych, wyjaśnienie tekstu i omówienie dalej awarie tooprevent kroki w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="97209-112">Reporting hello impact of an outage on hello usage of your app, combining data, text explanation, and a discussion of next steps tooprevent outages in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="97209-113">Zasób usługi Application Insights musi zawierać wyświetleń strony lub skoroszytów toouse zdarzeń niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="97209-113">Your Application Insights resource must contain page views or custom events toouse workbooks.</span></span> <span data-ttu-id="97209-114">[Dowiedz się, jak tooset Twojego stronę toocollect aplikacji automatycznie widoków z hello zestaw SDK usługi Application Insights JavaScript](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="97209-114">[Learn how tooset up your app toocollect page views automatically with hello Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="97209-115">Edytowanie, zmienianie rozmieszczenia klonowania i usuwanie sekcji skoroszytu</span><span class="sxs-lookup"><span data-stu-id="97209-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="97209-116">Skoroszyt jest wprowadzonych sekcji: wizualizacje można edytować niezależnie użycia, wykresów, tabel, tekst i analiza wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="97209-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="97209-117">tooedit hello zawartości sekcji skoroszytu, kliknij przycisk hello **Edytuj** poniżej i toohello prawej części hello skoroszytu.</span><span class="sxs-lookup"><span data-stu-id="97209-117">tooedit hello contents of a workbook section, click hello **Edit** button below and toohello right of hello workbook section.</span></span>

![Formanty edycji sekcji Application Insights skoroszytów](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="97209-119">Po zakończeniu edycji sekcji, kliknij **przeprowadzić edycję** w hello lewym dolnym rogu sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="97209-119">When you're done editing a section, click **Done Editing** in hello bottom left corner of hello section.</span></span>

2. <span data-ttu-id="97209-120">toocreate duplikat sekcji, kliknij przycisk hello **klonowania w tej sekcji** ikony.</span><span class="sxs-lookup"><span data-stu-id="97209-120">toocreate a duplicate of a section, click hello **Clone this section** icon.</span></span> <span data-ttu-id="97209-121">Tworzenie duplikatów sekcji jest doskonały tooway tooiterate na zapytanie bez utraty poprzedniej iteracji.</span><span class="sxs-lookup"><span data-stu-id="97209-121">Creating duplicate sections is a great tooway tooiterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="97209-122">toomove się sekcji w skoroszycie, kliknij przycisk hello **Przenieś w górę** lub **Przenieś w dół** ikony.</span><span class="sxs-lookup"><span data-stu-id="97209-122">toomove up a section in a workbook, click hello **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="97209-123">tooremove sekcji stałe, kliknij przycisk hello **Usuń** ikony.</span><span class="sxs-lookup"><span data-stu-id="97209-123">tooremove a section permanently, click hello **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="97209-124">Dodawanie sekcji wizualizacji danych użycia</span><span class="sxs-lookup"><span data-stu-id="97209-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="97209-125">Skoroszyty oferuje cztery typy wizualizacji analizy użycia wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="97209-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="97209-126">Każdy odpowiedzi na często zadawane pytania dotyczące użycia hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97209-126">Each answers a common question about hello usage of your app.</span></span> <span data-ttu-id="97209-127">tooadd tabel i wykresów innych niż te cztery sekcje dodać Analytics query sekcje (patrz poniżej).</span><span class="sxs-lookup"><span data-stu-id="97209-127">tooadd tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="97209-128">tooadd użytkowników, sesji, zdarzeń i przechowywania sekcji tooyour skoroszytu, użyj hello **Dodaj użytkowników** lub innych odpowiedni przycisk u dołu hello hello skoroszytu lub u dołu hello dowolnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="97209-128">tooadd a Users, Sessions, Events, or Retention section tooyour workbook, use hello **Add Users** or other corresponding button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

![Sekcja użytkownicy w skoroszytach](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="97209-130">**Użytkownicy** sekcje odpowiedzi "ilu użytkowników wyświetli stronę niektórych lub używać niektórych funkcji Moja witryna"?</span><span class="sxs-lookup"><span data-stu-id="97209-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="97209-131">**Sesje** sekcje odpowiedzi "ile sesji użytkownicy poświęcają wyświetlanie niektórych strony lub funkcji z mojej lokacji?"</span><span class="sxs-lookup"><span data-stu-id="97209-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="97209-132">**Zdarzenia** sekcje odpowiedzi "ile razy użytkowników wyświetlania niektóre strony lub funkcja witryny sieci?"</span><span class="sxs-lookup"><span data-stu-id="97209-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="97209-133">Oferuje każdego z tych typów sekcji trzy hello tego samego zestawy kontrolek i wizualizacji:</span><span class="sxs-lookup"><span data-stu-id="97209-133">Each of these three section types offers hello same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="97209-134">Więcej informacji na temat edytowania sekcje użytkownikami, sesjami i zdarzenia</span><span class="sxs-lookup"><span data-stu-id="97209-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="97209-135">Przełącz hello wykresu głównego, siatki histogram, automatyczne insights i przykładowej wizualizacji użytkowników przy użyciu hello **Pokaż wykres**, **Pokaż siatkę**, **Pokaż Insights**i **Przykładowych tych użytkowników** pola wyboru u góry hello każdej sekcji.</span><span class="sxs-lookup"><span data-stu-id="97209-135">Toggle hello main chart, histogram grids, automatic insights, and sample users visualizations using hello **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at hello top of each section.</span></span>

![Przechowywania części skoroszytów](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="97209-137">**Przechowywania** sekcje odpowiedzi "Osób, które są wyświetlane niektóre strony lub używać niektórych funkcji w ciągu jednego dnia lub tygodnia, ile wrócił następnego dnia lub tygodnia?"</span><span class="sxs-lookup"><span data-stu-id="97209-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="97209-138">Dowiedz się więcej na temat edytowania sekcje przechowywania</span><span class="sxs-lookup"><span data-stu-id="97209-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="97209-139">Przełącz hello opcjonalne ogólną przechowywania wykresu przy użyciu hello **Pokaż ogólną przechowywania wykresu** wyboru u góry hello hello sekcji.</span><span class="sxs-lookup"><span data-stu-id="97209-139">Toggle hello optional Overall Retention chart using hello **Show overall retention chart** checkbox at hello top of hello section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="97209-140">Dodawanie sekcji Application Insights analityka</span><span class="sxs-lookup"><span data-stu-id="97209-140">Adding Application Insights Analytics sections</span></span>

![Analiza części skoroszytów](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="97209-142">tooadd Application Insights Analytics zapytania sekcja tooyour skoroszytu, użyj hello **dodać Analytics query** przycisk u dołu hello hello skoroszytu lub u dołu hello dowolnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="97209-142">tooadd an Application Insights Analytics query section tooyour workbook, use hello **Add Analytics query** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

<span data-ttu-id="97209-143">Analiza zapytania sekcje umożliwiają dodawanie zapytań o dowolnego przez dane usługi Application Insights do skoroszytów.</span><span class="sxs-lookup"><span data-stu-id="97209-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="97209-144">Taka elastyczność oznacza, że sekcje zapytania Analytics powinna być Twoje Przejdź toofor udzielenie odpowiedzi na pytania dotyczące witryny innej niż hello czterech wymienionych powyżej dla użytkowników, sesji zdarzeń i przechowywania, takich jak:</span><span class="sxs-lookup"><span data-stu-id="97209-144">This flexibility means Analytics query sections should be your go-toofor answering any questions about your site other than hello four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="97209-145">Jak wiele wyjątków została throw Twojej lokacji podczas hello sam okresu jako spadek użycia?</span><span class="sxs-lookup"><span data-stu-id="97209-145">How many exceptions did your site throw during hello same time period as a decline in usage?</span></span>
* <span data-ttu-id="97209-146">Jaki był hello dystrybucji czas ładowania strony dla użytkowników, którzy przeglądają niektóre strony?</span><span class="sxs-lookup"><span data-stu-id="97209-146">What was hello distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="97209-147">Ilu użytkowników wyświetlić niektórych zbiór stron w witrynie, ale nie innymi zestaw stron?</span><span class="sxs-lookup"><span data-stu-id="97209-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="97209-148">Może to być przydatne toounderstand, jeśli masz klastrów użytkowników, którzy korzystają z różnych podzbiory funkcji witryny sieci (Użyj hello `join` operatora z hello `kind=leftanti` modyfikator w hello język zapytań usługi Analiza dzienników).</span><span class="sxs-lookup"><span data-stu-id="97209-148">This can be useful toounderstand if you have clusters of users who use different subsets of your site's functionality (use hello `join` operator with hello `kind=leftanti` modifier in hello Log Analytics query language).</span></span>

<span data-ttu-id="97209-149">Użyj hello [materiały referencyjne dotyczące języka zapytań usługi Analiza dzienników](https://docs.loganalytics.io/) toolearn więcej informacji na temat Pisanie zapytań.</span><span class="sxs-lookup"><span data-stu-id="97209-149">Use hello [Log Analytics query language reference](https://docs.loganalytics.io/) toolearn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="97209-150">Dodawanie tekstu i sekcji języka znaczników Markdown</span><span class="sxs-lookup"><span data-stu-id="97209-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="97209-151">Dodawanie nagłówków, wyjaśnienia i komentarzami tooyour skoroszytów pomaga przekształcić zestaw tabel i wykresów udostępniono.</span><span class="sxs-lookup"><span data-stu-id="97209-151">Adding headings, explanations, and commentary tooyour workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="97209-152">Sekcje tekstu w skoroszytach obsługuje hello [składni języka Markdown](https://daringfireball.net/projects/markdown/) tekstu formatowania, takich jak nagłówki pogrubienie, kursywa i listy punktowane.</span><span class="sxs-lookup"><span data-stu-id="97209-152">Text sections in workbooks support hello [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="97209-153">tooadd skoroszytu tooyour sekcji tekstu, użyj hello **Dodawanie tekstu** przycisk u dołu hello hello skoroszytu lub u dołu hello dowolnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="97209-153">tooadd a text section tooyour workbook, use hello **Add text** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="97209-154">Zapisywanie i udostępnianie skoroszytów z zespołem</span><span class="sxs-lookup"><span data-stu-id="97209-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="97209-155">Skoroszyty są zapisywane w ramach zasobu usługi Application Insights w hello **Moje raporty** sekcja, która jest prywatny tooyou lub hello **udostępnionych raportów** sekcja, która jest dostępna tooeveryone z dostępem toohello zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="97209-155">Workbooks are saved within an Application Insights resource, either in hello **My Reports** section that's private tooyou or in hello **Shared Reports** section that's accessible tooeveryone with access toohello Application Insights resource.</span></span> <span data-ttu-id="97209-156">tooview hello skoroszytów w zasobie powitania kliknij hello **Otwórz** przycisku w pasku akcji hello.</span><span class="sxs-lookup"><span data-stu-id="97209-156">tooview all hello workbooks in hello resource, click hello **Open** button in hello action bar.</span></span>

<span data-ttu-id="97209-157">tooshare skoroszytu, który jest aktualnie **Moje raporty**:</span><span class="sxs-lookup"><span data-stu-id="97209-157">tooshare a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="97209-158">Kliknij przycisk **Otwórz** na pasku akcji hello</span><span class="sxs-lookup"><span data-stu-id="97209-158">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="97209-159">Kliknij przycisk "..." hello obok skoroszytu hello ma tooshare</span><span class="sxs-lookup"><span data-stu-id="97209-159">Click hello "..." button beside hello workbook you want tooshare</span></span>
3. <span data-ttu-id="97209-160">Kliknij przycisk **Przenieś raporty tooShared**.</span><span class="sxs-lookup"><span data-stu-id="97209-160">Click **Move tooShared Reports**.</span></span>

<span data-ttu-id="97209-161">tooshare skoroszytu z łączem lub za pośrednictwem poczty e-mail, kliknij przycisk **udziału** hello pasku akcji.</span><span class="sxs-lookup"><span data-stu-id="97209-161">tooshare a workbook with a link or via email, click **Share** in hello action bar.</span></span> <span data-ttu-id="97209-162">Należy pamiętać, że adresaci łącza hello muszą mieć dostęp do zasobu toothis hello Azure tooview portalu hello skoroszytu.</span><span class="sxs-lookup"><span data-stu-id="97209-162">Keep in mind that recipients of hello link need access toothis resource in hello Azure portal tooview hello workbook.</span></span> <span data-ttu-id="97209-163">zmiany toomake adresatów muszą mieć co najmniej uprawnienia współautora hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="97209-163">toomake edits, recipients need at least Contributor permissions for hello resource.</span></span>

<span data-ttu-id="97209-164">toopin łącze tooan skoroszytu tooa pulpitu nawigacyjnego platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="97209-164">toopin a link tooa workbook tooan Azure Dashboard:</span></span>

1. <span data-ttu-id="97209-165">Kliknij przycisk **Otwórz** na pasku akcji hello</span><span class="sxs-lookup"><span data-stu-id="97209-165">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="97209-166">Kliknij przycisk "..." hello obok skoroszytu hello ma toopin</span><span class="sxs-lookup"><span data-stu-id="97209-166">Click hello "..." button beside hello workbook you want toopin</span></span>
3. <span data-ttu-id="97209-167">Kliknij przycisk **toodashboard numeru Pin**.</span><span class="sxs-lookup"><span data-stu-id="97209-167">Click **Pin toodashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97209-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="97209-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="97209-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="97209-169">Next steps</span></span>
- <span data-ttu-id="97209-170">Użycie tooenable napotyka, Rozpocznij wysyłanie [zdarzeń niestandardowych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) lub [wyświetlenia strony](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="97209-170">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="97209-171">Jeśli już wysyłania zdarzeń niestandardowych lub wyświetleń strony Eksploruj hello użycia narzędzia toolearn użytkowników wykorzystania usługi.</span><span class="sxs-lookup"><span data-stu-id="97209-171">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="97209-172">Użytkownicy, sesje, zdarzenia</span><span class="sxs-lookup"><span data-stu-id="97209-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="97209-173">Lejki</span><span class="sxs-lookup"><span data-stu-id="97209-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="97209-174">Przechowywanie</span><span class="sxs-lookup"><span data-stu-id="97209-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="97209-175">User Flows (Przepływy użytkowników)</span><span class="sxs-lookup"><span data-stu-id="97209-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="97209-176">Dodaj kontekstu użytkownika</span><span class="sxs-lookup"><span data-stu-id="97209-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
