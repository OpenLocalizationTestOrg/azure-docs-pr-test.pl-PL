---
title: "toomonitor aaaHow konta usługi Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor konta magazynu na platformie Azure przy użyciu hello portalu Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 9a939e0b5db687c1b7b7857399321f681df2056a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a><span data-ttu-id="251d3-103">Monitor konta magazynu w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="251d3-103">Monitor a storage account in hello Azure portal</span></span>

<span data-ttu-id="251d3-104">[Analizy usługi Azure Storage](../storage-analytics.md) dostarcza metryki dla wszystkich usług magazynu i dzienniki dla obiektów blob, kolejek i tabel.</span><span class="sxs-lookup"><span data-stu-id="251d3-104">[Azure Storage Analytics](../storage-analytics.md) provides metrics for all storage services, and logs for blobs, queues, and tables.</span></span> <span data-ttu-id="251d3-105">Można użyć hello [portalu Azure](https://portal.azure.com) tooconfigure dzienniki i metryk, które są rejestrowane dla Twojego konta i skonfiguruj wykresy, które zapewniają wizualnej reprezentacji danych metryki.</span><span class="sxs-lookup"><span data-stu-id="251d3-105">You can use hello [Azure portal](https://portal.azure.com) tooconfigure which metrics and logs are recorded for your account, and configure charts that provide visual representations of your metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="251d3-106">Brak kosztów związanych z badanie danych monitorowania w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="251d3-106">There are costs associated with examining monitoring data in hello Azure portal.</span></span> <span data-ttu-id="251d3-107">Aby uzyskać więcej informacji, zobacz [analizy magazynu i rozliczeń](/rest/api/storageservices/Storage-Analytics-and-Billing).</span><span class="sxs-lookup"><span data-stu-id="251d3-107">For more information, see [Storage Analytics and Billing](/rest/api/storageservices/Storage-Analytics-and-Billing).</span></span>
>
> <span data-ttu-id="251d3-108">Magazyn plików Azure obecnie obsługuje metryki analityka magazynu, ale jeszcze nie obsługuje rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="251d3-108">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>
> <span data-ttu-id="251d3-109">Konta magazynu z typu replikacji z magazynu Strefowo nadmiarowy (ZRS) aktualnie nie masz metryki hello lub włączona funkcja rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="251d3-109">Storage accounts with a replication type of Zone-Redundant Storage (ZRS) currently do not have hello metrics or logging capability enabled.</span></span>
> 
> <span data-ttu-id="251d3-110">Szczegółowy przewodnik przy użyciu analizy magazynu i inne narzędzia tooidentify, diagnozowanie i rozwiązywanie problemów związanych z usługą Azure Storage, zobacz [monitorowanie, diagnozowanie i rozwiązywanie problemów z usługi Magazyn Microsoft Azure](../storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="251d3-110">For an in-depth guide on using Storage Analytics and other tools tooidentify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>
>

## <a name="configure-monitoring-for-a-storage-account"></a><span data-ttu-id="251d3-111">Konfigurowanie monitorowania dla konta magazynu</span><span class="sxs-lookup"><span data-stu-id="251d3-111">Configure monitoring for a storage account</span></span>

1. <span data-ttu-id="251d3-112">W hello [portalu Azure](https://portal.azure.com), wybierz pozycję **kont magazynu**, a następnie hello magazynu konta Nazwa tooopen hello konta pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="251d3-112">In hello [Azure portal](https://portal.azure.com), select **Storage accounts**, then hello storage account name tooopen hello account dashboard.</span></span>
1. <span data-ttu-id="251d3-113">Wybierz **diagnostyki** w hello **monitorowanie** sekcji hello menu bloku.</span><span class="sxs-lookup"><span data-stu-id="251d3-113">Select **Diagnostics** in hello **MONITORING** section of hello menu blade.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. <span data-ttu-id="251d3-115">Wybierz hello **typu** danych metryki dla każdego **usługi** konieczność toomonitor i hello **zasady przechowywania** hello danych.</span><span class="sxs-lookup"><span data-stu-id="251d3-115">Select hello **type** of metrics data for each **service** you wish toomonitor, and hello **retention policy** for hello data.</span></span> <span data-ttu-id="251d3-116">Można również wyłączyć monitorowanie przez ustawienie **stan** za**poza**.</span><span class="sxs-lookup"><span data-stu-id="251d3-116">You can also disable monitoring by setting **Status** too**Off**.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   <span data-ttu-id="251d3-118">Istnieją dwa typy metryk, które można włączyć dla poszczególnych usług, które są domyślnie włączone dla nowego konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="251d3-118">There are two types of metrics you can enable for each service, both of which are enabled by default for new storage accounts:</span></span>

   * <span data-ttu-id="251d3-119">**Łączny**: umożliwia zbieranie metryk, takich jak wejście/wyjście, dostępności, opóźnienia i Powodzenie wartości procentowe.</span><span class="sxs-lookup"><span data-stu-id="251d3-119">**Aggregate**: Collects metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="251d3-120">Te metryki są agregowane dla hello obiektów blob, kolejki, tabeli i usług plików.</span><span class="sxs-lookup"><span data-stu-id="251d3-120">These metrics are aggregated for hello blob, queue, table, and file services.</span></span>
   * <span data-ttu-id="251d3-121">**Dla interfejsu API**: W dodanie toohello agregacji metryki zbiera hello tego samego zestawu metryki dla każdej operacji magazynu w hello interfejsu API usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="251d3-121">**Per API**: In addition toohello aggregate metrics, collects hello same set of metrics for each storage operation in hello Azure Storage service API.</span></span>

   <span data-ttu-id="251d3-122">zasady przechowywania danych tooset hello, Przenieś hello **przechowywania (dni)** suwak lub wprowadź hello liczbę dni tooretain danych, z 1 too365.</span><span class="sxs-lookup"><span data-stu-id="251d3-122">tooset hello data retention policy, move hello **Retention (days)** slider or enter hello number of days of data tooretain, from 1 too365.</span></span> <span data-ttu-id="251d3-123">Witaj domyślne dla nowych kont magazynu wynosi siedem dni.</span><span class="sxs-lookup"><span data-stu-id="251d3-123">hello default for new storage accounts is seven days.</span></span> <span data-ttu-id="251d3-124">Jeśli nie chcesz, aby tooset zasady przechowywania, wprowadź wartość zero.</span><span class="sxs-lookup"><span data-stu-id="251d3-124">If you do not want tooset a retention policy, enter zero.</span></span> <span data-ttu-id="251d3-125">Jeśli nie ma żadnych zasad przechowywania, działa hello toodelete tooyou danych monitorowania.</span><span class="sxs-lookup"><span data-stu-id="251d3-125">If there is no retention policy, it is up tooyou toodelete hello monitoring data.</span></span>

   > [!WARNING]
   > <span data-ttu-id="251d3-126">Są naliczane, gdy należy ręcznie usunąć dane metryk.</span><span class="sxs-lookup"><span data-stu-id="251d3-126">You are charged when you manually delete metrics data.</span></span> <span data-ttu-id="251d3-127">System hello bezpłatnie usunięcie danych starych analytics (dane starsze niż zasady przechowywania).</span><span class="sxs-lookup"><span data-stu-id="251d3-127">Stale analytics data (data older than your retention policy) is deleted by hello system at no cost.</span></span> <span data-ttu-id="251d3-128">Firma Microsoft zaleca ustawienie zasady przechowywania oparte na jak długo mają dane analityczne tooretain magazynu dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="251d3-128">We recommend setting a retention policy based on how long you want tooretain storage analytics data for your account.</span></span> <span data-ttu-id="251d3-129">Zobacz [co opłat, czy ponosisz, po włączeniu metryk storage?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="251d3-129">See [What charges do you incur when you enable storage metrics?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) for more information.</span></span>
   >

1. <span data-ttu-id="251d3-130">Po zakończeniu konfiguracji monitorowania hello wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="251d3-130">When you finish hello monitoring configuration, select **Save**.</span></span>

<span data-ttu-id="251d3-131">Domyślny zestaw miar jest wyświetlany na wykresach w bloku konto magazynu hello, a także hello pojedynczej usługi bloki (obiektu blob, kolejki, tabel i plików).</span><span class="sxs-lookup"><span data-stu-id="251d3-131">A default set of metrics is displayed in charts on hello storage account blade, as well as hello individual service blades (blob, queue, table, and file).</span></span> <span data-ttu-id="251d3-132">Po aktywowaniu metryki dla usługi może potrwać do godziny tooan tooappear danych w wykresy.</span><span class="sxs-lookup"><span data-stu-id="251d3-132">Once you've enabled metrics for a service, it may take up tooan hour for data tooappear in its charts.</span></span> <span data-ttu-id="251d3-133">Możesz wybrać **Edytuj** na wszystkie metryki wykresu zbyt[skonfiguruj metrykę, które](#how-to-customize-metrics-charts) są wyświetlane na wykresie hello.</span><span class="sxs-lookup"><span data-stu-id="251d3-133">You can select **Edit** on any metric chart too[configure which metrics](#how-to-customize-metrics-charts) are displayed in hello chart.</span></span>

<span data-ttu-id="251d3-134">Zbieranie metryk i rejestrowania można wyłączyć, ustawiając **stan** za**poza**.</span><span class="sxs-lookup"><span data-stu-id="251d3-134">You can disable metrics collection and logging by setting **Status** too**Off**.</span></span>

> [!NOTE]
> <span data-ttu-id="251d3-135">Usługa Azure Storage korzysta [tabeli magazynu](../common/storage-introduction.md#table-storage) toostore hello metryki dla konta magazynu i magazyny hello metryki tabel na koncie.</span><span class="sxs-lookup"><span data-stu-id="251d3-135">Azure Storage uses [table storage](../common/storage-introduction.md#table-storage) toostore hello metrics for your storage account, and stores hello metrics in tables in your account.</span></span> <span data-ttu-id="251d3-136">Aby uzyskać więcej informacji zobacz.</span><span class="sxs-lookup"><span data-stu-id="251d3-136">For more information, see.</span></span> <span data-ttu-id="251d3-137">[Jak są przechowywane metryki](../common/storage-analytics.md#how-metrics-are-stored).</span><span class="sxs-lookup"><span data-stu-id="251d3-137">[How metrics are stored](../common/storage-analytics.md#how-metrics-are-stored).</span></span>
>

## <a name="customize-metrics-charts"></a><span data-ttu-id="251d3-138">Dostosowanie metryk wykresów</span><span class="sxs-lookup"><span data-stu-id="251d3-138">Customize metrics charts</span></span>

<span data-ttu-id="251d3-139">Użyj hello następujące procedury toochoose które tooview metryki magazynu na wykresie metryki.</span><span class="sxs-lookup"><span data-stu-id="251d3-139">Use hello following procedure toochoose which storage metrics tooview in a metrics chart.</span></span> 

1. <span data-ttu-id="251d3-140">Rozpocznij od wyświetlanie wykresu metryki magazynu w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="251d3-140">Start by displaying a storage metric chart in hello Azure portal.</span></span> <span data-ttu-id="251d3-141">Można znaleźć wykresów na powitania **bloku konto magazynu** w hello **metryki** bloku dla poszczególnych usług (obiektu blob, kolejki, tabeli, plik).</span><span class="sxs-lookup"><span data-stu-id="251d3-141">You can find charts on hello **storage account blade** and in hello **Metrics** blade for an individual service (blob, queue, table, file).</span></span>

   <span data-ttu-id="251d3-142">W tym przykładzie współpracujemy z powitania po wykresu, który pojawia się na powitania **bloku konto magazynu**:</span><span class="sxs-lookup"><span data-stu-id="251d3-142">In this example, we work with hello following chart that appears on hello **storage account blade**:</span></span>

   ![Wybór wykresu w portalu Azure](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. <span data-ttu-id="251d3-144">Następnie kliknij w dowolnym miejscu w hello wykresu tooopen hello **Metryka** bloku.</span><span class="sxs-lookup"><span data-stu-id="251d3-144">Next, click anywhere within hello chart tooopen hello **Metric** blade.</span></span> <span data-ttu-id="251d3-145">Wybierz **Edytuj wykres** tooopen hello **Edytuj wykres** bloku.</span><span class="sxs-lookup"><span data-stu-id="251d3-145">Select **Edit chart** tooopen hello **Edit Chart** blade.</span></span>

   ![Edytuj przycisk Wykres w bloku wykresu](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. <span data-ttu-id="251d3-147">Na powitania **Edytuj wykres** bloku, wybierz hello **zakres czasu** z toodisplay metryki hello na wykresie hello i hello **usługi** (obiektu blob, kolejek, tabeli, pliku) metryki, którego chcesz toodisplay.</span><span class="sxs-lookup"><span data-stu-id="251d3-147">On hello **Edit Chart** blade, select hello **Time Range** of hello metrics toodisplay in hello chart, and hello **service** (blob, queue, table, file) whose metrics you wish toodisplay.</span></span> <span data-ttu-id="251d3-148">W tym miejscu Wybraliśmy hello toodisplay poza tygodnia metryki dla usługi blob hello:</span><span class="sxs-lookup"><span data-stu-id="251d3-148">Here we've selected toodisplay hello past week's metrics for hello blob service:</span></span>

   ![Wybór zakresu i Usługa czasu w bloku Edytuj wykres hello](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. <span data-ttu-id="251d3-150">Wybierz hello osoba **metryki** można tak samo, jak gdyby wyświetlany na wykresie hello, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="251d3-150">Select hello individual **metrics** you'd like displayed in hello chart, then click **OK**.</span></span> <span data-ttu-id="251d3-151">Na przykład, w tym miejscu możemy wybraną toodisplay hello *ContainerCount* i *ObjectCount* metryki:</span><span class="sxs-lookup"><span data-stu-id="251d3-151">For example, here we've chosen toodisplay hello *ContainerCount* and *ObjectCount* metrics:</span></span>

   ![Poszczególne metryki zaznaczenia w bloku Edytuj wykres](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

<span data-ttu-id="251d3-153">Ustawienia wykresu nie dotyczy kolekcji hello, agregacji i magazynu danych na koncie magazynu hello monitorowania, tylko hello wyświetlanie danych metryk.</span><span class="sxs-lookup"><span data-stu-id="251d3-153">Your chart settings do not affect hello collection, aggregation, or storage of monitoring data in hello storage account, only hello viewing of metrics data.</span></span>

### <a name="metrics-availability-in-charts"></a><span data-ttu-id="251d3-154">Metryki dostępności na wykresach</span><span class="sxs-lookup"><span data-stu-id="251d3-154">Metrics availability in charts</span></span>

<span data-ttu-id="251d3-155">Hello listy zmian dostępne metryki oparte na usługi, która została wybrana w hello listy rozwijanej, a typ jednostki hello wykresu hello jest edytowany.</span><span class="sxs-lookup"><span data-stu-id="251d3-155">hello list of available metrics changes based on which service you've chosen in hello drop-down, and hello unit type of hello chart you're editing.</span></span> <span data-ttu-id="251d3-156">Na przykład można wybrać procent metryk, takich jak *PercentNetworkError* i *PercentThrottlingError* tylko wtedy, gdy edycji wykres wyświetlający jednostki w procentach:</span><span class="sxs-lookup"><span data-stu-id="251d3-156">For example, you can select percentage metrics like *PercentNetworkError* and *PercentThrottlingError* only if you're editing a chart that displays units in percentage:</span></span>

![Żądanie błąd wartość procentową wykresu w hello portalu Azure](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a><span data-ttu-id="251d3-158">Rozdzielczość metryk</span><span class="sxs-lookup"><span data-stu-id="251d3-158">Metrics resolution</span></span>

<span data-ttu-id="251d3-159">Hello metryk, które wybrano w diagnostyce Określa rozdzielczość hello hello metryki, które są dostępne dla Twojego konta:</span><span class="sxs-lookup"><span data-stu-id="251d3-159">hello metrics you selected in Diagnostics determines hello resolution of hello metrics that are available for your account:</span></span>

* <span data-ttu-id="251d3-160">**Łączny** monitorowania udostępnia metryk, takich jak wejście/wyjście, dostępności, opóźnienia i Powodzenie wartości procentowe.</span><span class="sxs-lookup"><span data-stu-id="251d3-160">**Aggregate** monitoring provides metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="251d3-161">Te metryki są agregowane z hello obiektów blob, tabeli, usług plików i kolejki.</span><span class="sxs-lookup"><span data-stu-id="251d3-161">These metrics are aggregated from hello blob, table, file, and queue services.</span></span>
* <span data-ttu-id="251d3-162">**Dla interfejsu API** zapewnia bardziej precyzyjną rozpoznawania metryk dostępnych dla operacji magazynu dodatkowo toohello agreguje poziomu usług.</span><span class="sxs-lookup"><span data-stu-id="251d3-162">**Per API** provides finer resolution, with metrics available for individual storage operations, in addition toohello service-level aggregates.</span></span>

## <a name="configure-metrics-alerts"></a><span data-ttu-id="251d3-163">Konfigurowanie alertów metryk</span><span class="sxs-lookup"><span data-stu-id="251d3-163">Configure metrics alerts</span></span>

<span data-ttu-id="251d3-164">Można tworzyć alerty toonotify podczas osiągnięto progi dla metryki zasobów magazynu.</span><span class="sxs-lookup"><span data-stu-id="251d3-164">You can create alerts toonotify you when thresholds have been reached for storage resource metrics.</span></span>

1. <span data-ttu-id="251d3-165">Witaj tooopen **bloku reguły alertów**, przewiń w dół toohello **monitorowanie** sekcji hello **bloku Menu** i wybierz **reguły alertów**.</span><span class="sxs-lookup"><span data-stu-id="251d3-165">tooopen hello **Alert rules blade**, scroll down toohello **MONITORING** section of hello **Menu blade** and select **Alert rules**.</span></span>
1. <span data-ttu-id="251d3-166">Wybierz **Dodaj alert** tooopen hello **dodać regułę alertu** bloku</span><span class="sxs-lookup"><span data-stu-id="251d3-166">Select **Add alert** tooopen hello **Add an alert rule** blade</span></span>
1. <span data-ttu-id="251d3-167">Wybierz **zasobów** (obiektu blob, plików, kolejka, tabela) z listy rozwijanej Witaj, a następnie wprowadź **nazwa** i **opis** nowej reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="251d3-167">Select a **Resource** (blob, file, queue, table) from hello drop-down, and enter a **Name** and **Description** for your new alert rule.</span></span>
1. <span data-ttu-id="251d3-168">Wybierz hello **Metryka** dla którego chcesz tooadd alert, alert **warunku**, a **próg**.</span><span class="sxs-lookup"><span data-stu-id="251d3-168">Select hello **Metric** for which you'd like tooadd an alert, an alert **Condition**, and a **Threshold**.</span></span> <span data-ttu-id="251d3-169">Witaj próg jednostki typu różnić w zależności od Metryka hello została wybrana.</span><span class="sxs-lookup"><span data-stu-id="251d3-169">hello threshold unit type changes depending on hello metric you've chosen.</span></span> <span data-ttu-id="251d3-170">Na przykład "count" jest typem jednostki hello *ContainerCount*, podczas hello jednostki hello *PercentNetworkError* Metryka to wartość procentową.</span><span class="sxs-lookup"><span data-stu-id="251d3-170">For example, "count" is hello unit type for *ContainerCount*, while hello unit for hello *PercentNetworkError* metric is a percentage.</span></span>
1. <span data-ttu-id="251d3-171">Wybierz hello **okresu**.</span><span class="sxs-lookup"><span data-stu-id="251d3-171">Select hello **Period**.</span></span> <span data-ttu-id="251d3-172">Metryki, które osiągną lub przekroczą hello próg w ramach wyzwalacza okresu hello alertu.</span><span class="sxs-lookup"><span data-stu-id="251d3-172">Metrics that reach or exceed hello Threshold within hello period trigger an alert.</span></span>
1. <span data-ttu-id="251d3-173">(Opcjonalnie) Skonfiguruj **E-mail** i **Webhook** powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="251d3-173">(Optional) Configure **Email** and **Webhook** notifications.</span></span> <span data-ttu-id="251d3-174">Aby uzyskać więcej informacji dotyczących elementów webhook, zobacz [skonfigurować elementu webhook na alert metryki Azure](../../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="251d3-174">For more information on webhooks, see [Configure a webhook on an Azure metric alert](../../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="251d3-175">Jeśli nie zostanie skonfigurowane powiadomienia e-mail lub elementu webhook, alerty będą wyświetlane tylko w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="251d3-175">If you do not configure email or webhook notifications, alerts will appear only in hello Azure portal.</span></span>

!["Dodaj regułę alertu" bloku w hello portalu Azure](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a><span data-ttu-id="251d3-177">Dodawanie pulpitu nawigacyjnego portalu toohello wykresy metryk</span><span class="sxs-lookup"><span data-stu-id="251d3-177">Add metrics charts toohello portal dashboard</span></span>

<span data-ttu-id="251d3-178">Wykresy metryk usługi Azure Storage można dodać dla dowolnego magazynu kont tooyour portalu pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="251d3-178">You can add Azure Storage metrics charts for any of your storage accounts tooyour portal dashboard.</span></span>

1. <span data-ttu-id="251d3-179">Kliknij przycisk Wybierz **edycji pulpitu nawigacyjnego** podczas wyświetlania pulpitu nawigacyjnego w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="251d3-179">Select click **Edit dashboard** while viewing your dashboard in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="251d3-180">W hello **galerii kafelka**, wybierz pozycję **Znajdź Kafelki przez** > **typu**.</span><span class="sxs-lookup"><span data-stu-id="251d3-180">In hello **Tile Gallery**, select **Find tiles by** > **Type**.</span></span>
1. <span data-ttu-id="251d3-181">Wybierz **typu** > **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="251d3-181">Select **Type** > **Storage accounts**.</span></span>
1. <span data-ttu-id="251d3-182">W **zasobów**, wybierz konto magazynu hello metryki, którego chcesz tooadd toohello z pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="251d3-182">In **Resources**, select hello storage account whose metrics you wish tooadd toohello dashboard.</span></span>
1. <span data-ttu-id="251d3-183">Wybierz **kategorii** > **monitorowania**.</span><span class="sxs-lookup"><span data-stu-id="251d3-183">Select **Categories** > **Monitoring**.</span></span>
1. <span data-ttu-id="251d3-184">Przeciągnij i upuść hello wykresu kafelka na pulpicie nawigacyjnym metryki hello, którą chcesz wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="251d3-184">Drag-and-drop hello chart tile onto your dashboard for hello metric you'd like displayed.</span></span> <span data-ttu-id="251d3-185">Powtórz dla wszystkich metryki którego chciałbyś wyświetlane na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="251d3-185">Repeat for all metrics you'd like displayed on hello dashboard.</span></span> <span data-ttu-id="251d3-186">W hello po obrazu zostanie wyróżniona wykresu "Obiekty BLOB — łączna liczba żądań" hello, na przykład, ale wszystkie wykresy hello są dostępne do umieszczenia na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="251d3-186">In hello following image, hello "Blobs - Total requests" chart is highlighted as an example, but all hello charts are available for placement on your dashboard.</span></span>

   ![Galeria kafelka w portalu Azure](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. <span data-ttu-id="251d3-188">Wybierz **gotowe dostosowywanie** górze hello hello pulpitu nawigacyjnego, gdy użytkownik zakończy dodawanie wykresów.</span><span class="sxs-lookup"><span data-stu-id="251d3-188">Select **Done customizing** near hello top of hello dashboard when you're done adding charts.</span></span>

<span data-ttu-id="251d3-189">Po dodaniu pulpitu nawigacyjnego tooyour wykresy, można dostosować je zgodnie z opisem w [dostosowanie metryk wykresy](#how-to-customize-metrics-charts).</span><span class="sxs-lookup"><span data-stu-id="251d3-189">Once you've added charts tooyour dashboard, you can further customize them as described in [Customize metrics charts](#how-to-customize-metrics-charts).</span></span>

## <a name="configure-logging"></a><span data-ttu-id="251d3-190">Konfigurowanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="251d3-190">Configure logging</span></span>

<span data-ttu-id="251d3-191">Możesz wydać dzienników diagnostycznych toosave usługi Azure Storage dla odczytu, zapisu i usuwania żądania hello obiektów blob, tabel i usługi kolejkowania.</span><span class="sxs-lookup"><span data-stu-id="251d3-191">You can instruct Azure Storage toosave diagnostics logs for read, write, and delete requests for hello blob, table, and queue services.</span></span> <span data-ttu-id="251d3-192">zasady przechowywania danych Hello ustawionych ma również zastosowanie toothese dzienniki.</span><span class="sxs-lookup"><span data-stu-id="251d3-192">hello data retention policy you set also applies toothese logs.</span></span>

> [!NOTE]
> <span data-ttu-id="251d3-193">Magazyn plików Azure obecnie obsługuje metryki analityka magazynu, ale jeszcze nie obsługuje rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="251d3-193">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>

1. <span data-ttu-id="251d3-194">W hello [portalu Azure](https://portal.azure.com), wybierz pozycję **kont magazynu**, nazwę konta magazynu hello tooopen bloku konto magazynu hello hello.</span><span class="sxs-lookup"><span data-stu-id="251d3-194">In hello [Azure portal](https://portal.azure.com), select **Storage accounts**, then hello name of hello storage account tooopen hello storage account blade.</span></span>
1. <span data-ttu-id="251d3-195">Wybierz **diagnostyki** w hello **monitorowanie** sekcji hello menu bloku.</span><span class="sxs-lookup"><span data-stu-id="251d3-195">Select **Diagnostics** in hello **MONITORING** section of hello menu blade.</span></span>

    ![Diagnostyka elementu menu w obszarze monitorowania w hello portalu Azure.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. <span data-ttu-id="251d3-197">Upewnij się, **stan** ustawiono zbyt**na**i wybierz hello **usług** dla którego chcesz tooenable rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="251d3-197">Ensure **Status** is set too**On**, and select hello **services** for which you'd like tooenable logging.</span></span>

    ![Konfigurowanie rejestrowania w hello portalu Azure.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. <span data-ttu-id="251d3-199">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="251d3-199">Click **Save**.</span></span>

<span data-ttu-id="251d3-200">dzienniki diagnostyczne Hello są zapisywane w kontenerze obiektu blob o nazwie $logs na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="251d3-200">hello diagnostics logs are saved in a blob container named $logs in your storage account.</span></span> <span data-ttu-id="251d3-201">Można wyświetlić dane dziennika hello za pomocą Eksploratora magazynu, takich jak hello [Eksploratora magazynu](http://storageexplorer.com), albo programowo z użyciem biblioteki klienta usługi storage hello lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="251d3-201">You can view hello log data using a storage explorer like hello [Microsoft Storage Explorer](http://storageexplorer.com), or programmatically using hello storage client library or PowerShell.</span></span>

<span data-ttu-id="251d3-202">Informacje dotyczące uzyskiwania dostępu do kontenera hello $logs, zobacz [Włączanie rejestrowania magazynu i uzyskiwanie dostępu do danych dziennika](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span><span class="sxs-lookup"><span data-stu-id="251d3-202">For information about accessing hello $logs container, see [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span></span>

## <a name="next-steps"></a><span data-ttu-id="251d3-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="251d3-203">Next steps</span></span>

* <span data-ttu-id="251d3-204">Uzyskać więcej informacji na temat [metryki, rejestrowania i rozliczeń](../storage-analytics.md) analizy magazynu.</span><span class="sxs-lookup"><span data-stu-id="251d3-204">Find more details about [metrics, logging, and billing](../storage-analytics.md) for Storage Analytics.</span></span>
* <span data-ttu-id="251d3-205">[Włącz dane metryk usługi Azure Storage metryki i widoku](../storage-enable-and-view-metrics.md) przy użyciu programu PowerShell i programowo w języku C#.</span><span class="sxs-lookup"><span data-stu-id="251d3-205">[Enable Azure Storage metrics and view metrics data](../storage-enable-and-view-metrics.md) by using PowerShell and programmatically with C#.</span></span>
