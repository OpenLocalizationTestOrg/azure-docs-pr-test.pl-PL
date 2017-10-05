---
title: "Badanie i udostępniać dane użycia interakcyjne skoroszytów w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 75028b4fbda43d90f56690a33c7eb624fce049c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="4f88b-103">Badanie i udostępniać dane użycia interakcyjne skoroszytów w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="4f88b-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="4f88b-104">Łączenie skoroszytów [Azure Application Insights](app-insights-overview.md) wizualizacje danych [zapytania analityczne](app-insights-analytics.md)i tekstu w dokumentach interaktywnego.</span><span class="sxs-lookup"><span data-stu-id="4f88b-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="4f88b-105">Skoroszyty są edytowany przez innych członków zespołu dostęp do tego samego zasobu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4f88b-105">Workbooks are editable by other team members with access to the same Azure resource.</span></span> <span data-ttu-id="4f88b-106">Oznacza to, że zapytania i formanty używane do tworzenia skoroszytu, są dostępne dla innych osób odczytujących skoroszytu, dzięki czemu można je łatwo eksplorować, rozszerzać i sprawdź, czy błędy.</span><span class="sxs-lookup"><span data-stu-id="4f88b-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span></span>

<span data-ttu-id="4f88b-107">Skoroszyty są przydatne w scenariuszach, takich jak:</span><span class="sxs-lookup"><span data-stu-id="4f88b-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="4f88b-108">Eksplorowanie użycia aplikacji, jeśli nie wiesz wcześniej metryki zainteresowania: liczby użytkowników, stawki przechowywania, kursy wymiany itp. W przeciwieństwie do innych narzędzi analizy użycia w usłudze Application Insights skoroszytów umożliwiają łączenie wielu rodzajów wizualizacje i analiz nadawania doskonałe rozwiązanie dla tego rodzaju dowolnych eksploracji.</span><span class="sxs-lookup"><span data-stu-id="4f88b-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="4f88b-109">Do zespołu wyjaśniający, jak działa funkcja nowo wydanego, przez użytkownika przedstawiający Liczba interakcji klucza i innych metryk.</span><span class="sxs-lookup"><span data-stu-id="4f88b-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="4f88b-110">Udostępnianie wyników A / B eksperymentu w Twojej aplikacji za pomocą innych członków zespołu.</span><span class="sxs-lookup"><span data-stu-id="4f88b-110">Sharing the results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="4f88b-111">Można wyjaśnić cele dotyczące eksperymentów z tekstem, a następnie Pokaż każdy pomiar użycia i zapytania Analytics używane do analizowania eksperymentu, wraz z wyczyść dokumentów wywołania do tego, czy wszystkie metryki został powyżej lub poniżej docelowe.</span><span class="sxs-lookup"><span data-stu-id="4f88b-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="4f88b-112">Raportowanie wpływ awarii na użycie aplikacji, połączenie danych, wyjaśnienie tekstu i omówienie kolejne kroki, aby uniknąć awarii w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="4f88b-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="4f88b-113">Zasób usługi Application Insights musi zawierać wyświetleń strony lub zdarzeń niestandardowych w celu użycia skoroszytów.</span><span class="sxs-lookup"><span data-stu-id="4f88b-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span></span> <span data-ttu-id="4f88b-114">[Dowiedz się, jak skonfigurować aplikację do zbierania wyświetleń strony automatycznie z zestawu SDK usługi Application Insights JavaScript](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="4f88b-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="4f88b-115">Edytowanie, zmienianie rozmieszczenia klonowania i usuwanie sekcji skoroszytu</span><span class="sxs-lookup"><span data-stu-id="4f88b-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="4f88b-116">Skoroszyt jest wprowadzonych sekcji: wizualizacje można edytować niezależnie użycia, wykresów, tabel, tekst i analiza wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="4f88b-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="4f88b-117">Aby edytować zawartość sekcji skoroszytu, kliknij przycisk **Edytuj** przycisk w dół i w prawo w sekcji skoroszytu.</span><span class="sxs-lookup"><span data-stu-id="4f88b-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span></span>

![Formanty edycji sekcji Application Insights skoroszytów](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="4f88b-119">Po zakończeniu edycji sekcji, kliknij **przeprowadzić edycję** w lewym dolnym rogu sekcji.</span><span class="sxs-lookup"><span data-stu-id="4f88b-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span></span>

2. <span data-ttu-id="4f88b-120">Aby utworzyć kopię sekcji, kliknij przycisk **klonowania w tej sekcji** ikony.</span><span class="sxs-lookup"><span data-stu-id="4f88b-120">To create a duplicate of a section, click the **Clone this section** icon.</span></span> <span data-ttu-id="4f88b-121">Tworzenie duplikatów sekcji to doskonały sposób w celu wykonania iteracji w zapytaniu bez utraty poprzedniej iteracji.</span><span class="sxs-lookup"><span data-stu-id="4f88b-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="4f88b-122">Aby przenieść w górę sekcji w skoroszycie, kliknij przycisk **Przenieś w górę** lub **Przenieś w dół** ikony.</span><span class="sxs-lookup"><span data-stu-id="4f88b-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="4f88b-123">Aby trwale usunąć sekcję, kliknij przycisk **Usuń** ikony.</span><span class="sxs-lookup"><span data-stu-id="4f88b-123">To remove a section permanently, click the **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="4f88b-124">Dodawanie sekcji wizualizacji danych użycia</span><span class="sxs-lookup"><span data-stu-id="4f88b-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="4f88b-125">Skoroszyty oferuje cztery typy wizualizacji analizy użycia wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="4f88b-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="4f88b-126">Każdy odpowiedzi na typowe pytania dotyczące użycia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4f88b-126">Each answers a common question about the usage of your app.</span></span> <span data-ttu-id="4f88b-127">Aby dodać tabel i wykresów innych niż te cztery sekcje, Dodaj Analytics query sekcje (patrz poniżej).</span><span class="sxs-lookup"><span data-stu-id="4f88b-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="4f88b-128">Aby dodać użytkowników, sesji zdarzeń i przechowywania sekcji do skoroszytu, użyj **Dodaj użytkowników** lub innych odpowiedni przycisk w dolnej części skoroszytu lub u dołu dowolnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="4f88b-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span></span>

![Sekcja użytkownicy w skoroszytach](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="4f88b-130">**Użytkownicy** sekcje odpowiedzi "ilu użytkowników wyświetli stronę niektórych lub używać niektórych funkcji Moja witryna"?</span><span class="sxs-lookup"><span data-stu-id="4f88b-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="4f88b-131">**Sesje** sekcje odpowiedzi "ile sesji użytkownicy poświęcają wyświetlanie niektórych strony lub funkcji z mojej lokacji?"</span><span class="sxs-lookup"><span data-stu-id="4f88b-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="4f88b-132">**Zdarzenia** sekcje odpowiedzi "ile razy użytkowników wyświetlania niektóre strony lub funkcja witryny sieci?"</span><span class="sxs-lookup"><span data-stu-id="4f88b-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="4f88b-133">Oferuje każdego z tych typów trzy sekcji tego samego zbioru kontrolek i wizualizacji:</span><span class="sxs-lookup"><span data-stu-id="4f88b-133">Each of these three section types offers the same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="4f88b-134">Więcej informacji na temat edytowania sekcje użytkownikami, sesjami i zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4f88b-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="4f88b-135">Przełącz wykresu głównego, siatki histogram, automatyczne insights i przykładowej wizualizacji użytkowników przy użyciu **Pokaż wykres**, **Pokaż siatkę**, **Pokaż Insights**, i **przykładowych tych użytkowników** pola wyboru na początku każdej sekcji.</span><span class="sxs-lookup"><span data-stu-id="4f88b-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span></span>

![Przechowywania części skoroszytów](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="4f88b-137">**Przechowywania** sekcje odpowiedzi "Osób, które są wyświetlane niektóre strony lub używać niektórych funkcji w ciągu jednego dnia lub tygodnia, ile wrócił następnego dnia lub tygodnia?"</span><span class="sxs-lookup"><span data-stu-id="4f88b-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="4f88b-138">Dowiedz się więcej na temat edytowania sekcje przechowywania</span><span class="sxs-lookup"><span data-stu-id="4f88b-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="4f88b-139">Przełącz opcjonalne użycie ogólnej przechowywania wykresu **Pokaż ogólną przechowywania wykresu** wyboru w górnej części sekcji.</span><span class="sxs-lookup"><span data-stu-id="4f88b-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="4f88b-140">Dodawanie sekcji Application Insights analityka</span><span class="sxs-lookup"><span data-stu-id="4f88b-140">Adding Application Insights Analytics sections</span></span>

![Analiza części skoroszytów](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="4f88b-142">Aby dodać sekcję zapytania analizy aplikacji wgląd do skoroszytu, użyj **dodać Analytics query** przycisk w dolnej części skoroszytu lub u dołu dowolnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="4f88b-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span></span>

<span data-ttu-id="4f88b-143">Analiza zapytania sekcje umożliwiają dodawanie zapytań o dowolnego przez dane usługi Application Insights do skoroszytów.</span><span class="sxs-lookup"><span data-stu-id="4f88b-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="4f88b-144">Taka elastyczność oznacza, że sekcje zapytania Analytics powinna być Twoje przejdź do odpowiedzi na pytania dotyczące witryny innej niż cztery wymienione powyżej dla użytkowników, sesji zdarzeń i przechowywania, takich jak:</span><span class="sxs-lookup"><span data-stu-id="4f88b-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="4f88b-145">Jak wiele wyjątków throw witryny w okresie czasu jako spadek użycia?</span><span class="sxs-lookup"><span data-stu-id="4f88b-145">How many exceptions did your site throw during the same time period as a decline in usage?</span></span>
* <span data-ttu-id="4f88b-146">Jaki był dystrybucji czas ładowania strony dla użytkowników, którzy przeglądają niektóre strony?</span><span class="sxs-lookup"><span data-stu-id="4f88b-146">What was the distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="4f88b-147">Ilu użytkowników wyświetlić niektórych zbiór stron w witrynie, ale nie innymi zestaw stron?</span><span class="sxs-lookup"><span data-stu-id="4f88b-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="4f88b-148">Może to być przydatne zrozumieć, jeśli masz klastrów użytkowników, którzy korzystają z różnych podzbiory funkcji witryny (Użyj `join` operatora z `kind=leftanti` modyfikator w języku zapytań usługi Analiza dzienników).</span><span class="sxs-lookup"><span data-stu-id="4f88b-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span></span>

<span data-ttu-id="4f88b-149">Użyj [materiały referencyjne dotyczące języka zapytań usługi Analiza dzienników](https://docs.loganalytics.io/) Aby dowiedzieć się więcej o pisaniu zapytań.</span><span class="sxs-lookup"><span data-stu-id="4f88b-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="4f88b-150">Dodawanie tekstu i sekcji języka znaczników Markdown</span><span class="sxs-lookup"><span data-stu-id="4f88b-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="4f88b-151">Dodawanie nagłówków, wyjaśnienia i komentarzami do skoroszytów pomaga przekształcić zestaw tabel i wykresów udostępniono.</span><span class="sxs-lookup"><span data-stu-id="4f88b-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="4f88b-152">Sekcje tekstu w pomocy technicznej skoroszyty [składni języka Markdown](https://daringfireball.net/projects/markdown/) tekstu formatowania, takich jak nagłówki pogrubienie, kursywa i listy punktowane.</span><span class="sxs-lookup"><span data-stu-id="4f88b-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="4f88b-153">Aby dodać sekcję tekstu do skoroszytu, użyj **Dodawanie tekstu** przycisk w dolnej części skoroszytu lub u dołu dowolnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="4f88b-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="4f88b-154">Zapisywanie i udostępnianie skoroszytów z zespołem</span><span class="sxs-lookup"><span data-stu-id="4f88b-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="4f88b-155">Skoroszyty są zapisywane w ramach zasobu usługi Application Insights w **Moje raporty** sekcja, która jest prywatny, w przypadku lub **udostępnionych raportów** sekcji, który jest dostępny dla wszystkich użytkowników mających dostęp do zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4f88b-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span></span> <span data-ttu-id="4f88b-156">Aby wyświetlić wszystkie skoroszyty w zasobie, kliknij przycisk **Otwórz** na pasku akcji.</span><span class="sxs-lookup"><span data-stu-id="4f88b-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span></span>

<span data-ttu-id="4f88b-157">Aby udostępnić skoroszytu, który jest aktualnie **Moje raporty**:</span><span class="sxs-lookup"><span data-stu-id="4f88b-157">To share a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="4f88b-158">Kliknij przycisk **Otwórz** na pasku akcji</span><span class="sxs-lookup"><span data-stu-id="4f88b-158">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="4f88b-159">Kliknij przycisk "..." obok skoroszytu, który chcesz udostępnić</span><span class="sxs-lookup"><span data-stu-id="4f88b-159">Click the "..." button beside the workbook you want to share</span></span>
3. <span data-ttu-id="4f88b-160">Kliknij przycisk **Przenieś do raportów udostępnionych**.</span><span class="sxs-lookup"><span data-stu-id="4f88b-160">Click **Move to Shared Reports**.</span></span>

<span data-ttu-id="4f88b-161">Aby udostępnić skoroszyt z łączem lub za pośrednictwem poczty e-mail, kliknij przycisk **udostępnianie** na pasku akcji.</span><span class="sxs-lookup"><span data-stu-id="4f88b-161">To share a workbook with a link or via email, click **Share** in the action bar.</span></span> <span data-ttu-id="4f88b-162">Należy pamiętać, że adresaci łącza muszą mieć dostęp do tego zasobu w portalu Azure, aby wyświetlić skoroszytu.</span><span class="sxs-lookup"><span data-stu-id="4f88b-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span></span> <span data-ttu-id="4f88b-163">Aby dokonać edycji, odbiorców, muszą mieć co najmniej uprawnienia współautora dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="4f88b-163">To make edits, recipients need at least Contributor permissions for the resource.</span></span>

<span data-ttu-id="4f88b-164">Aby przypiąć łącze do skoroszytu do pulpitu nawigacyjnego platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="4f88b-164">To pin a link to a workbook to an Azure Dashboard:</span></span>

1. <span data-ttu-id="4f88b-165">Kliknij przycisk **Otwórz** na pasku akcji</span><span class="sxs-lookup"><span data-stu-id="4f88b-165">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="4f88b-166">Kliknij przycisk "..." obok skoroszytu, który chcesz przypiąć</span><span class="sxs-lookup"><span data-stu-id="4f88b-166">Click the "..." button beside the workbook you want to pin</span></span>
3. <span data-ttu-id="4f88b-167">Kliknij przycisk **Przypnij do pulpitu nawigacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="4f88b-167">Click **Pin to dashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f88b-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f88b-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f88b-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f88b-169">Next steps</span></span>
- <span data-ttu-id="4f88b-170">Aby umożliwić korzystanie z użycia, Rozpocznij wysyłanie [zdarzeń niestandardowych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) lub [wyświetlenia strony](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="4f88b-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="4f88b-171">Jeżeli już zdarzeń niestandardowych lub wyświetleń strony, Poznaj narzędzia użycia, aby dowiedzieć się, jak używać usługi przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4f88b-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="4f88b-172">Użytkownicy, sesje, zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4f88b-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="4f88b-173">Lejki</span><span class="sxs-lookup"><span data-stu-id="4f88b-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="4f88b-174">Przechowywanie</span><span class="sxs-lookup"><span data-stu-id="4f88b-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="4f88b-175">User Flows (Przepływy użytkowników)</span><span class="sxs-lookup"><span data-stu-id="4f88b-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="4f88b-176">Dodaj kontekstu użytkownika</span><span class="sxs-lookup"><span data-stu-id="4f88b-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
