---
title: "Azure CDN alertów w czasie rzeczywistym | Dokumentacja firmy Microsoft"
description: "Alertów w czasie rzeczywistym w usłudze Microsoft Azure CDN. Alerty w czasie rzeczywistym udostępniają powiadomienia dotyczące wydajności punktów końcowych w Twoim profilu CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6e66eb076ac7220823a848b5047f147d4101cd55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="32990-104">Alerty w czasie rzeczywistym w usłudze Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="32990-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="32990-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="32990-105">Overview</span></span>
<span data-ttu-id="32990-106">W tym dokumencie opisano alertów w czasie rzeczywistym w usłudze Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="32990-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="32990-107">Ta funkcja udostępnia w czasie rzeczywistym powiadomienia o wydajności z punktów końcowych w profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="32990-107">This functionality provides real-time notifications about the performance of the endpoints in your CDN profile.</span></span>  <span data-ttu-id="32990-108">Można skonfigurować adres e-mail lub alerty HTTP na podstawie:</span><span class="sxs-lookup"><span data-stu-id="32990-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="32990-109">Przepustowość</span><span class="sxs-lookup"><span data-stu-id="32990-109">Bandwidth</span></span>
* <span data-ttu-id="32990-110">Kody stanu</span><span class="sxs-lookup"><span data-stu-id="32990-110">Status Codes</span></span>
* <span data-ttu-id="32990-111">Stany pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="32990-111">Cache Statuses</span></span>
* <span data-ttu-id="32990-112">Połączenia</span><span class="sxs-lookup"><span data-stu-id="32990-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="32990-113">Tworzenie w czasie rzeczywistym alertu</span><span class="sxs-lookup"><span data-stu-id="32990-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="32990-114">W [Azure Portal](https://portal.azure.com), przejdź do swojego profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="32990-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Blok profilu CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="32990-116">Blok profilu CDN, kliknij **Zarządzaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="32990-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="32990-118">Zostanie otwarty w portalu zarządzania usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="32990-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="32990-119">Umieść kursor nad **Analytics** , a następnie umieść kursor nad **statystyki w czasie rzeczywistym** wysuwane okno.</span><span class="sxs-lookup"><span data-stu-id="32990-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="32990-120">Polecenie **alertów w czasie rzeczywistym**.</span><span class="sxs-lookup"><span data-stu-id="32990-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Portal zarządzania usługi CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="32990-122">Zostanie wyświetlona lista istniejących konfiguracji alertu (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="32990-122">The list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="32990-123">Kliknij przycisk **dodać alertu** przycisku.</span><span class="sxs-lookup"><span data-stu-id="32990-123">Click the **Add Alert** button.</span></span>
   
    ![Dodawanie przycisku alertu](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="32990-125">Zostanie wyświetlony formularz służący do tworzenia nowego alertu.</span><span class="sxs-lookup"><span data-stu-id="32990-125">A form for creating a new alert is displayed.</span></span>
   
    ![Nowy formularz alertu](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="32990-127">Jeśli chcesz, aby ten alert jest aktywne po kliknięciu **zapisać**, sprawdź **włączone Alert** wyboru.</span><span class="sxs-lookup"><span data-stu-id="32990-127">If you want this alert to be active when you click **Save**, check the **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="32990-128">Wprowadź nazwę opisową dla alertu w **nazwa** pola.</span><span class="sxs-lookup"><span data-stu-id="32990-128">Enter a descriptive name for your alert in the **Name** field.</span></span>
7. <span data-ttu-id="32990-129">W **typ nośnika** listy rozwijanej wybierz **HTTP dużego obiektu**.</span><span class="sxs-lookup"><span data-stu-id="32990-129">In the **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Typ nośnika z wybranego obiektu dużych HTTP](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="32990-131">Musisz wybrać **HTTP dużego obiektu** jako **typ nośnika**.</span><span class="sxs-lookup"><span data-stu-id="32990-131">You must select **HTTP Large Object** as the **Media Type**.</span></span>  <span data-ttu-id="32990-132">Inne opcje nie są używane przez **Azure CDN from Verizon**.</span><span class="sxs-lookup"><span data-stu-id="32990-132">The other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="32990-133">Nie można wybrać **HTTP dużego obiektu** spowoduje, że nigdy nie wyzwolenie alertu.</span><span class="sxs-lookup"><span data-stu-id="32990-133">Failure to select **HTTP Large Object** will cause your alert to never be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="32990-134">Utwórz **wyrażenie** do monitorowania, wybierając **Metryka**, **Operator**, i **wyzwolenia wartość**.</span><span class="sxs-lookup"><span data-stu-id="32990-134">Create an **Expression** to monitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="32990-135">Aby uzyskać **Metryka**, wybierz typ warunku, które mają być monitorowane.</span><span class="sxs-lookup"><span data-stu-id="32990-135">For **Metric**, select the type of condition you want monitored.</span></span>  <span data-ttu-id="32990-136">**MB/s przepustowości** ilość przepustowości w megabitach na sekundę.</span><span class="sxs-lookup"><span data-stu-id="32990-136">**Bandwidth Mbps** is the amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="32990-137">**Całkowita liczba połączeń** jest liczba równoczesnych połączeń HTTP nasze serwery krawędzi.</span><span class="sxs-lookup"><span data-stu-id="32990-137">**Total Connections** is the number of concurrent HTTP connections to our edge servers.</span></span>  <span data-ttu-id="32990-138">Definicje różne stany pamięci podręcznej i kodów stanu, zobacz [kodów stanu systemu Azure CDN pamięci podręcznej](https://msdn.microsoft.com/library/mt759237.aspx) i [kody stanu HTTP Azure w sieci CDN](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="32990-138">For definitions of the various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="32990-139">**Operator** jest operatorów matematycznych, która ustanawia relację między Metryka i wartość wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="32990-139">**Operator** is the mathematical operator that establishes the relationship between the metric and the trigger value.</span></span>
   * <span data-ttu-id="32990-140">**Wyzwalanie wartość** jest wartość progowa, które muszą zostać spełnione, zanim zostanie wysłane powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="32990-140">**Trigger Value** is the threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="32990-141">W poniższym przykładzie utworzono wyrażenie wskazuje, że chcę otrzymać powiadomienie, gdy liczba kodów stanu 404 jest większa niż 25.</span><span class="sxs-lookup"><span data-stu-id="32990-141">In the below example, the expression I have created indicates that I would like to be notified when the number of 404 status codes is greater than 25.</span></span>
     
     ![W czasie rzeczywistym alertu przykładowe wyrażenie](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="32990-143">Aby uzyskać **interwał**, wprowadź, jak często chcesz wyrażenia obliczonego.</span><span class="sxs-lookup"><span data-stu-id="32990-143">For **Interval**, enter how frequently you would like the expression evaluated.</span></span>
10. <span data-ttu-id="32990-144">W **powiadomienia na** listy rozwijanej wybierz opcję, jeśli chcesz otrzymać powiadomienie, gdy wyrażenie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="32990-144">In the **Notify on** dropdown, select when you would like to be notified when the expression is true.</span></span>
    
    * <span data-ttu-id="32990-145">**Warunkiem rozpoczęcia** wskazuje, że powiadomienia będą wysyłane po raz pierwszy wykryciu określony warunek.</span><span class="sxs-lookup"><span data-stu-id="32990-145">**Condition Start** indicates that a notification will be sent when the specified condition is first detected.</span></span>
    * <span data-ttu-id="32990-146">**Warunek zakończenia** wskazuje, że powiadomienie zostanie wysłane, gdy określony warunek nie zostanie wykryty.</span><span class="sxs-lookup"><span data-stu-id="32990-146">**Condition End** indicates that a notification will be sent when the specified condition is no longer detected.</span></span> <span data-ttu-id="32990-147">To powiadomienie można wywoływać tylko po naszej system monitorowania sieci wykrył, że wystąpił określony warunek.</span><span class="sxs-lookup"><span data-stu-id="32990-147">This notification can only be triggered after our network monitoring system detected that the specified condition occurred.</span></span>
    * <span data-ttu-id="32990-148">**Ciągłe** wskazuje, że powiadomienia będą wysyłane zawsze wykryje, że system monitorowania sieci określony warunek.</span><span class="sxs-lookup"><span data-stu-id="32990-148">**Continuous** indicates that a notification will be sent each time that the network monitoring system detects the specified condition.</span></span> <span data-ttu-id="32990-149">Należy pamiętać, że system monitorowania sieci sprawdza tylko raz na interwał określony warunek.</span><span class="sxs-lookup"><span data-stu-id="32990-149">Keep in mind that the network monitoring system will only check once per interval for the specified condition.</span></span>
    * <span data-ttu-id="32990-150">**Stan początkowy i końcowy** oznacza, że powiadomienie zostanie wysłane po raz pierwszy czy określony warunek zostanie wykryte, i ponownie, gdy nie jest już została wykryta warunku.</span><span class="sxs-lookup"><span data-stu-id="32990-150">**Condition Start and End** indicates that a notification will be sent the first time that the specified condition is detected and once again when the condition is no longer detected.</span></span>
11. <span data-ttu-id="32990-151">Jeśli chcesz otrzymywać powiadomienia pocztą e-mail, sprawdź **powiadamiania pocztą E-mail** wyboru.</span><span class="sxs-lookup"><span data-stu-id="32990-151">If you want to receive notifications by email, check the **Notify by Email** checkbox.</span></span>  
    
    ![Powiadomienia E-mail formularza](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="32990-153">W **do** wprowadź adres e-mail, gdzie ma powiadomienia wysyłane.</span><span class="sxs-lookup"><span data-stu-id="32990-153">In the **To** field, enter the email address you where you want notifications sent.</span></span> <span data-ttu-id="32990-154">Dla **podmiotu** i **treści**, może pozostaw wartość domyślną, lub możesz dostosować komunikat przy użyciu **dostępne słowa kluczowe** listy, aby dynamicznie wstawić dane alertów po wiadomości są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="32990-154">For **Subject** and **Body**, you may leave the default, or you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="32990-155">Powiadomienia e-mail można sprawdzić, klikając **testowe powiadomienie E-mail** przycisku, ale tylko po zapisaniu alertu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="32990-155">You can test the email notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="32990-156">Jeśli chcesz, aby powiadomienia można opublikować na serwerze sieci web, sprawdź **powiadamiania przez HTTP Post** wyboru.</span><span class="sxs-lookup"><span data-stu-id="32990-156">If you want notifications to be posted to a web server, check the **Notify by HTTP Post** checkbox.</span></span>
    
    ![Powiadom HTTP Post formularza](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="32990-158">W **adres Url** wprowadź adres URL, gdzie ma komunikat HTTP opublikowane.</span><span class="sxs-lookup"><span data-stu-id="32990-158">In the **Url** field, enter the URL you where you want the HTTP message posted.</span></span> <span data-ttu-id="32990-159">W **nagłówki** pole tekstowe, wprowadź nagłówki HTTP do wysłania w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="32990-159">In the **Headers** textbox, enter the HTTP headers to be sent in the request.</span></span>  <span data-ttu-id="32990-160">Dla **treści** można dostosować komunikat przy użyciu **dostępne słowa kluczowe** listy, aby dynamicznie wstawić dane alertów, gdy komunikat jest wysyłany.</span><span class="sxs-lookup"><span data-stu-id="32990-160">For **Body** you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>  <span data-ttu-id="32990-161">**Nagłówki** i **treści** domyślną ładunek XML, podobnie jak poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="32990-161">**Headers** and **Body** default to an XML payload similar to the below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="32990-162">Należy przetestować powiadomienia HTTP Post, klikając **testowe powiadomienie E-mail** przycisku, ale tylko po zapisaniu alertu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="32990-162">You can test the HTTP Post notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="32990-163">Kliknij przycisk **zapisać** przycisk, aby zapisać konfigurację alertu.</span><span class="sxs-lookup"><span data-stu-id="32990-163">Click the **Save** button to save your alert configuration.</span></span>  <span data-ttu-id="32990-164">Jeśli zaznaczono **włączone Alert** w kroku 5 alertu jest aktywna.</span><span class="sxs-lookup"><span data-stu-id="32990-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32990-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="32990-165">Next Steps</span></span>
* <span data-ttu-id="32990-166">Analizowanie [statystyki w czasie rzeczywistym w usłudze Azure CDN](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="32990-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="32990-167">Dig głębiej z [zaawansowane raporty HTTP](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="32990-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="32990-168">Analizowanie [wzorców użycia](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="32990-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

