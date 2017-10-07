---
title: "aaaSet alerty dla zapytań w Stream Analytics | Dokumentacja firmy Microsoft"
description: "Opis usługi Stream Analytics alertów"
keywords: "Konfigurowanie alertów"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="084a2-104">Ustawianie alertów dla zadania usługi analiza strumienia Azure</span><span class="sxs-lookup"><span data-stu-id="084a2-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="084a2-105">Wprowadzenie: Strona Monitor</span><span class="sxs-lookup"><span data-stu-id="084a2-105">Introduction: Monitor page</span></span>
<span data-ttu-id="084a2-106">Można skonfigurować alerty tootrigger alert po metrykę warunek, który określisz.</span><span class="sxs-lookup"><span data-stu-id="084a2-106">You can set up alerts tootrigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="084a2-107">Na przykład skonfigurować alert dla warunku, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="084a2-107">For example, you might set up an alert for a condition like hello following:</span></span>

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

<span data-ttu-id="084a2-108">Reguły można skonfigurować na metryki za pośrednictwem portalu hello, lub można skonfigurować [programowo](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) na dane dzienników operacji.</span><span class="sxs-lookup"><span data-stu-id="084a2-108">Rules can be set up on metrics through hello portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-hello-azure-portal"></a><span data-ttu-id="084a2-109">Konfigurowanie alertów w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="084a2-109">Set up alerts in hello Azure portal</span></span>
1. <span data-ttu-id="084a2-110">Otwórz zadanie usługi Stream Analytics hello, który ma toocreate alert dla hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="084a2-110">In hello Azure portal, open hello Stream Analytics job you want toocreate an alert for.</span></span> 

2. <span data-ttu-id="084a2-111">W hello **zadania** bloku, kliknij przycisk hello **monitorowanie** sekcji.</span><span class="sxs-lookup"><span data-stu-id="084a2-111">In hello **Job** blade, click hello **Monitoring** section.</span></span>  

3. <span data-ttu-id="084a2-112">W hello **Metryka** bloku, kliknij przycisk hello **Dodaj alert** polecenia.</span><span class="sxs-lookup"><span data-stu-id="084a2-112">In hello **Metric** blade, click hello **Add alert** command.</span></span>

      ![Instalacja portalu usługi Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="084a2-114">Wprowadź nazwę i opis.</span><span class="sxs-lookup"><span data-stu-id="084a2-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="084a2-115">Użyj hello selektorów toodefine hello warunku w obszarze hello, które będą wysyłane alerty.</span><span class="sxs-lookup"><span data-stu-id="084a2-115">Use hello selectors toodefine hello condition under which hello alert will be sent.</span></span>

6. <span data-ttu-id="084a2-116">Podaj informacje o gdzie hello alertu.</span><span class="sxs-lookup"><span data-stu-id="084a2-116">Provide information about where hello alert should go.</span></span>

      ![Konfigurowanie alertu dla zadania usługi analiza strumienia Azure](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="084a2-118">Aby uzyskać więcej szczegółów na temat konfigurowania alertów w hello portalu Azure, zobacz [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="084a2-118">For more detail on configuring alerts in hello Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="084a2-119">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="084a2-119">Get help</span></span>
<span data-ttu-id="084a2-120">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="084a2-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="084a2-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="084a2-121">Next steps</span></span>
* [<span data-ttu-id="084a2-122">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="084a2-122">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="084a2-123">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="084a2-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="084a2-124">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="084a2-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="084a2-125">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="084a2-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="084a2-126">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="084a2-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

