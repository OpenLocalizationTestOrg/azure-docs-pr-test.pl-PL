---
title: alerty w czasie rzeczywistym CDN aaaAzure | Dokumentacja firmy Microsoft
description: "Alertów w czasie rzeczywistym w usłudze Microsoft Azure CDN. Alerty w czasie rzeczywistym udostępniają powiadomienia dotyczące wydajności hello punktów końcowych hello w Twoim profilu CDN."
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
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="79e5c-104">Alerty w czasie rzeczywistym w usłudze Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="79e5c-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="79e5c-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="79e5c-105">Overview</span></span>
<span data-ttu-id="79e5c-106">W tym dokumencie opisano alertów w czasie rzeczywistym w usłudze Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="79e5c-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="79e5c-107">Ta funkcja udostępnia w czasie rzeczywistym powiadomienia dotyczące wydajności hello punktów końcowych hello w Twoim profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="79e5c-107">This functionality provides real-time notifications about hello performance of hello endpoints in your CDN profile.</span></span>  <span data-ttu-id="79e5c-108">Można skonfigurować adres e-mail lub alerty HTTP na podstawie:</span><span class="sxs-lookup"><span data-stu-id="79e5c-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="79e5c-109">Przepustowość</span><span class="sxs-lookup"><span data-stu-id="79e5c-109">Bandwidth</span></span>
* <span data-ttu-id="79e5c-110">Kody stanu</span><span class="sxs-lookup"><span data-stu-id="79e5c-110">Status Codes</span></span>
* <span data-ttu-id="79e5c-111">Stany pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="79e5c-111">Cache Statuses</span></span>
* <span data-ttu-id="79e5c-112">Połączenia</span><span class="sxs-lookup"><span data-stu-id="79e5c-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="79e5c-113">Tworzenie w czasie rzeczywistym alertu</span><span class="sxs-lookup"><span data-stu-id="79e5c-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="79e5c-114">W hello [Azure Portal](https://portal.azure.com), Przeglądaj tooyour profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="79e5c-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Blok profilu CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="79e5c-116">Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="79e5c-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="79e5c-118">Otwiera portalu zarządzania Hello CDN.</span><span class="sxs-lookup"><span data-stu-id="79e5c-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="79e5c-119">Przesuń kursor myszy hello **Analytics** kartę, a następnie przesuń kursor myszy hello **statystyki w czasie rzeczywistym** wysuwane okno.</span><span class="sxs-lookup"><span data-stu-id="79e5c-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="79e5c-120">Polecenie **alertów w czasie rzeczywistym**.</span><span class="sxs-lookup"><span data-stu-id="79e5c-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Portal zarządzania usługi CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="79e5c-122">zostanie wyświetlona lista Hello istniejącej konfiguracji alertu (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="79e5c-122">hello list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="79e5c-123">Kliknij przycisk hello **dodać alertu** przycisku.</span><span class="sxs-lookup"><span data-stu-id="79e5c-123">Click hello **Add Alert** button.</span></span>
   
    ![Dodawanie przycisku alertu](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="79e5c-125">Zostanie wyświetlony formularz służący do tworzenia nowego alertu.</span><span class="sxs-lookup"><span data-stu-id="79e5c-125">A form for creating a new alert is displayed.</span></span>
   
    ![Nowy formularz alertu](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="79e5c-127">Jeśli chcesz ten alert toobe active po kliknięciu **zapisać**, sprawdź hello **włączone Alert** wyboru.</span><span class="sxs-lookup"><span data-stu-id="79e5c-127">If you want this alert toobe active when you click **Save**, check hello **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="79e5c-128">Wprowadź opisową nazwę alertu w hello **nazwa** pola.</span><span class="sxs-lookup"><span data-stu-id="79e5c-128">Enter a descriptive name for your alert in hello **Name** field.</span></span>
7. <span data-ttu-id="79e5c-129">W hello **typ nośnika** listy rozwijanej wybierz **HTTP dużego obiektu**.</span><span class="sxs-lookup"><span data-stu-id="79e5c-129">In hello **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Typ nośnika z wybranego obiektu dużych HTTP](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="79e5c-131">Musisz wybrać **HTTP dużego obiektu** jako hello **typ nośnika**.</span><span class="sxs-lookup"><span data-stu-id="79e5c-131">You must select **HTTP Large Object** as hello **Media Type**.</span></span>  <span data-ttu-id="79e5c-132">Witaj inne opcje nie są używane przez **Azure CDN from Verizon**.</span><span class="sxs-lookup"><span data-stu-id="79e5c-132">hello other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="79e5c-133">Błąd tooselect **HTTP dużego obiektu** spowoduje, że alert wyzwalane toonever.</span><span class="sxs-lookup"><span data-stu-id="79e5c-133">Failure tooselect **HTTP Large Object** will cause your alert toonever be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="79e5c-134">Utwórz **wyrażenie** toomonitor wybierając **Metryka**, **Operator**, i **wyzwolenia wartość**.</span><span class="sxs-lookup"><span data-stu-id="79e5c-134">Create an **Expression** toomonitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="79e5c-135">Aby uzyskać **Metryka**, wybierz typ hello warunku, które mają być monitorowane.</span><span class="sxs-lookup"><span data-stu-id="79e5c-135">For **Metric**, select hello type of condition you want monitored.</span></span>  <span data-ttu-id="79e5c-136">**MB/s przepustowości** jest hello wielkość przepustowości w megabitach na sekundę.</span><span class="sxs-lookup"><span data-stu-id="79e5c-136">**Bandwidth Mbps** is hello amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="79e5c-137">**Całkowita liczba połączeń** jest hello liczba równoczesnych tooour połączenia HTTP serwery krawędzi.</span><span class="sxs-lookup"><span data-stu-id="79e5c-137">**Total Connections** is hello number of concurrent HTTP connections tooour edge servers.</span></span>  <span data-ttu-id="79e5c-138">Definicje hello różne stany pamięci podręcznej i kodów stanu, zobacz [kodów stanu systemu Azure CDN pamięci podręcznej](https://msdn.microsoft.com/library/mt759237.aspx) i [kody stanu HTTP Azure w sieci CDN](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="79e5c-138">For definitions of hello various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="79e5c-139">**Operator** jest hello operatorów matematycznych ustanawia hello relację Metryka hello hello wyzwalacza wartość.</span><span class="sxs-lookup"><span data-stu-id="79e5c-139">**Operator** is hello mathematical operator that establishes hello relationship between hello metric and hello trigger value.</span></span>
   * <span data-ttu-id="79e5c-140">**Wyzwalanie wartość** jest wartość progu hello, które muszą zostać spełnione, zanim zostanie wysłane powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="79e5c-140">**Trigger Value** is hello threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="79e5c-141">W hello w poniższym przykładzie hello wyrażenie, które utworzono wskazuje, że chcę toobe powiadomienie, gdy liczba hello 404 kodów stanu jest większa niż 25.</span><span class="sxs-lookup"><span data-stu-id="79e5c-141">In hello below example, hello expression I have created indicates that I would like toobe notified when hello number of 404 status codes is greater than 25.</span></span>
     
     ![W czasie rzeczywistym alertu przykładowe wyrażenie](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="79e5c-143">Aby uzyskać **interwał**, wprowadź, jak często chcesz hello wyrażenia obliczonego.</span><span class="sxs-lookup"><span data-stu-id="79e5c-143">For **Interval**, enter how frequently you would like hello expression evaluated.</span></span>
10. <span data-ttu-id="79e5c-144">W hello **powiadomienia na** listy rozwijanej wybierz opcję, jeśli chcesz toobe powiadomienie, gdy hello wyrażenie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="79e5c-144">In hello **Notify on** dropdown, select when you would like toobe notified when hello expression is true.</span></span>
    
    * <span data-ttu-id="79e5c-145">**Warunkiem rozpoczęcia** wskazuje, że powiadomienie zostanie wysłane po hello określony warunek jest pierwszy wykryty.</span><span class="sxs-lookup"><span data-stu-id="79e5c-145">**Condition Start** indicates that a notification will be sent when hello specified condition is first detected.</span></span>
    * <span data-ttu-id="79e5c-146">**Warunek zakończenia** wskazuje, że powiadomienie zostanie wysłane po hello określony warunek nie zostanie wykryta.</span><span class="sxs-lookup"><span data-stu-id="79e5c-146">**Condition End** indicates that a notification will be sent when hello specified condition is no longer detected.</span></span> <span data-ttu-id="79e5c-147">To powiadomienie może być uruchomiona tylko po naszej sieci monitorowania system wykrył hello, że określony warunek.</span><span class="sxs-lookup"><span data-stu-id="79e5c-147">This notification can only be triggered after our network monitoring system detected that hello specified condition occurred.</span></span>
    * <span data-ttu-id="79e5c-148">**Ciągłe** wskazuje, że powiadomienie zostanie wysłane za każdym razem hello system monitorowania sieci wykrywa hello określony warunek.</span><span class="sxs-lookup"><span data-stu-id="79e5c-148">**Continuous** indicates that a notification will be sent each time that hello network monitoring system detects hello specified condition.</span></span> <span data-ttu-id="79e5c-149">Należy pamiętać sieci hello monitorowania system będzie tylko wyboru raz na interwał hello określony warunek.</span><span class="sxs-lookup"><span data-stu-id="79e5c-149">Keep in mind that hello network monitoring system will only check once per interval for hello specified condition.</span></span>
    * <span data-ttu-id="79e5c-150">**Stan początkowy i końcowy** oznacza, że powiadomienie zostanie wysłane hello wykryte po raz pierwszy hello określony warunek i jeszcze raz, jeżeli nie zostały wykryte hello warunku.</span><span class="sxs-lookup"><span data-stu-id="79e5c-150">**Condition Start and End** indicates that a notification will be sent hello first time that hello specified condition is detected and once again when hello condition is no longer detected.</span></span>
11. <span data-ttu-id="79e5c-151">Jeśli chcesz tooreceive powiadomienia pocztą e-mail, sprawdź hello **powiadamiania pocztą E-mail** wyboru.</span><span class="sxs-lookup"><span data-stu-id="79e5c-151">If you want tooreceive notifications by email, check hello **Notify by Email** checkbox.</span></span>  
    
    ![Powiadomienia E-mail formularza](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="79e5c-153">W hello **do** wprowadź adres e-mail hello miejscu powiadomienia wysłane.</span><span class="sxs-lookup"><span data-stu-id="79e5c-153">In hello **To** field, enter hello email address you where you want notifications sent.</span></span> <span data-ttu-id="79e5c-154">Dla **podmiotu** i **treści**, można pozostawić domyślne hello, lub można dostosować za pomocą hello wiadomość hello **dostępne słowa kluczowe** toodynamically lista wstawiania danych alertu po zostanie wysłana wiadomość Hello.</span><span class="sxs-lookup"><span data-stu-id="79e5c-154">For **Subject** and **Body**, you may leave hello default, or you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="79e5c-155">Powiadomienie e-mail hello można sprawdzić, klikając hello **testowe powiadomienie E-mail** przycisku, jednak tylko po zapisaniu hello konfiguracji alertu.</span><span class="sxs-lookup"><span data-stu-id="79e5c-155">You can test hello email notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="79e5c-156">Toobe powiadomienia zaksięgowany tooa serwera sieci web, sprawdzić hello **powiadamiania przez HTTP Post** wyboru.</span><span class="sxs-lookup"><span data-stu-id="79e5c-156">If you want notifications toobe posted tooa web server, check hello **Notify by HTTP Post** checkbox.</span></span>
    
    ![Powiadom HTTP Post formularza](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="79e5c-158">W hello **adres Url** wprowadź adres URL hello miejscu wiadomość hello HTTP zaksięgowania.</span><span class="sxs-lookup"><span data-stu-id="79e5c-158">In hello **Url** field, enter hello URL you where you want hello HTTP message posted.</span></span> <span data-ttu-id="79e5c-159">W hello **nagłówki** pole tekstowe, wprowadź wysłanych w żądaniu hello toobe nagłówki hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="79e5c-159">In hello **Headers** textbox, enter hello HTTP headers toobe sent in hello request.</span></span>  <span data-ttu-id="79e5c-160">Dla **treści** można dostosować za pomocą hello wiadomość hello **dostępne słowa kluczowe** toodynamically listy wstawiania danych alertu, gdy zostanie wysłana wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="79e5c-160">For **Body** you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>  <span data-ttu-id="79e5c-161">**Nagłówki** i **treści** domyślne podobne toohello ładunek XML tooan poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="79e5c-161">**Headers** and **Body** default tooan XML payload similar toohello below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="79e5c-162">Można sprawdzić hello powiadomień HTTP Post, klikając hello **testowe powiadomienie E-mail** przycisku, jednak tylko po zapisaniu hello konfiguracji alertu.</span><span class="sxs-lookup"><span data-stu-id="79e5c-162">You can test hello HTTP Post notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="79e5c-163">Kliknij przycisk hello **zapisać** przycisk toosave konfiguracji alertu.</span><span class="sxs-lookup"><span data-stu-id="79e5c-163">Click hello **Save** button toosave your alert configuration.</span></span>  <span data-ttu-id="79e5c-164">Jeśli zaznaczono **włączone Alert** w kroku 5 alertu jest aktywna.</span><span class="sxs-lookup"><span data-stu-id="79e5c-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79e5c-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="79e5c-165">Next Steps</span></span>
* <span data-ttu-id="79e5c-166">Analizowanie [statystyki w czasie rzeczywistym w usłudze Azure CDN](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="79e5c-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="79e5c-167">Dig głębiej z [zaawansowane raporty HTTP](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="79e5c-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="79e5c-168">Analizowanie [wzorców użycia](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="79e5c-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

