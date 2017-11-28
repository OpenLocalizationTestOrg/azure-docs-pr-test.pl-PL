---
title: Zaawansowana konfiguracja naboru uniwersalnych aplikacji systemu Windows SDK
description: "Zaawansowane opcje konfiguracji dla usługi Azure Mobile Engagement z uniwersalnych aplikacji systemu Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: cb9454212c94cf65093219c3d24c71277ede7877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="ba868-103">Zaawansowana konfiguracja naboru uniwersalnych aplikacji systemu Windows SDK</span><span class="sxs-lookup"><span data-stu-id="ba868-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba868-104">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="ba868-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="ba868-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="ba868-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="ba868-106">iOS</span><span class="sxs-lookup"><span data-stu-id="ba868-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="ba868-107">Android</span><span class="sxs-lookup"><span data-stu-id="ba868-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="ba868-108">W tej procedurze opisano sposób konfigurowania różnych opcji konfiguracji dla usługi Azure Mobile Engagement aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="ba868-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba868-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ba868-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="ba868-110">Konfiguracja zaawansowana</span><span class="sxs-lookup"><span data-stu-id="ba868-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="ba868-111">Wyłącz automatyczne zgłaszanie awarii</span><span class="sxs-lookup"><span data-stu-id="ba868-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="ba868-112">Możesz wyłączyć automatyczne awarii, funkcję zaangażowania raportowania.</span><span class="sxs-lookup"><span data-stu-id="ba868-112">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="ba868-113">Następnie gdy wystąpi nieobsługiwany wyjątek, Engagement nie działa.</span><span class="sxs-lookup"><span data-stu-id="ba868-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="ba868-114">Jeśli wyłączyć tę funkcję, a następnie w przypadku wystąpienia awarii nieobsługiwany w aplikacji zaangażowania nie wysyła awarii **i** nie zamknięcia sesji i zadania.</span><span class="sxs-lookup"><span data-stu-id="ba868-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send the crash **AND** does not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="ba868-115">Aby wyłączyć automatyczne zgłaszanie awarii, Dostosuj konfigurację, w zależności od sposobu należy zadeklarować jako:</span><span class="sxs-lookup"><span data-stu-id="ba868-115">To disable automatic crash reporting, customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="ba868-116">Z `EngagementConfiguration.xml` pliku</span><span class="sxs-lookup"><span data-stu-id="ba868-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="ba868-117">Ustaw awarii raport `false` między `<reportCrash>` i `</reportCrash>` tagów.</span><span class="sxs-lookup"><span data-stu-id="ba868-117">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="ba868-118">Z `EngagementConfiguration` obiektu w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="ba868-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="ba868-119">Ustaw awarii raportu przy użyciu obiektu EngagementConfiguration wartość false.</span><span class="sxs-lookup"><span data-stu-id="ba868-119">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="ba868-120">Wyłącz raportowanie w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="ba868-120">Disable real time reporting</span></span>
<span data-ttu-id="ba868-121">Domyślnie raporty usługi Engagement rejestruje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="ba868-121">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="ba868-122">Jeśli aplikacja zgłasza często dzienniki, lepiej jest buforu dzienniki i raportuj je w całości na podstawie czasu regularne.</span><span class="sxs-lookup"><span data-stu-id="ba868-122">If your application reports logs frequently, it is better to buffer the logs and to report them all at once on a regular time basis.</span></span> <span data-ttu-id="ba868-123">Jest on nazywany "Tryb szybki".</span><span class="sxs-lookup"><span data-stu-id="ba868-123">This is called “burst mode”.</span></span>

<span data-ttu-id="ba868-124">Aby to zrobić, należy wywołać metodę:</span><span class="sxs-lookup"><span data-stu-id="ba868-124">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="ba868-125">Argument jest wartością w **milisekund**.</span><span class="sxs-lookup"><span data-stu-id="ba868-125">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="ba868-126">Zawsze, gdy chcesz ponownie uaktywnić rejestrowania w czasie rzeczywistym, wywołaj metodę bez parametrów, lub wartość 0.</span><span class="sxs-lookup"><span data-stu-id="ba868-126">Whenever you want to reactivate the real-time logging, call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="ba868-127">Tryb serii nieco zwiększa czas pracy baterii, ale ma wpływ na monitorowanie usługi Engagement: wszystkie czas trwania sesji i zadań są zaokrąglane do serii wartość progową (w związku z tym sesji i zadania krótsze niż próg serii może nie być widoczna).</span><span class="sxs-lookup"><span data-stu-id="ba868-127">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="ba868-128">Firma Microsoft zaleca używanie próg w serii się niż 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="ba868-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="ba868-129">Zapisane dzienniki są ograniczone do 300 elementów.</span><span class="sxs-lookup"><span data-stu-id="ba868-129">Saved logs are limited to 300 items.</span></span> <span data-ttu-id="ba868-130">W przypadku wysyłania jest za długa, może spowodować utratę niektórych dzienników.</span><span class="sxs-lookup"><span data-stu-id="ba868-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="ba868-131">Próg serii nie można skonfigurować do okresu mniej niż 1 sekunda.</span><span class="sxs-lookup"><span data-stu-id="ba868-131">The burst threshold cannot be configured to a period less than one second.</span></span> <span data-ttu-id="ba868-132">Jeśli tak zrobisz, zestawu SDK zawiera śledzenia z powodu błędu i automatycznie przywraca wartość domyślna to zero sekund.</span><span class="sxs-lookup"><span data-stu-id="ba868-132">If you do so, the SDK shows a trace with the error and automatically resets to the default value, zero seconds.</span></span> <span data-ttu-id="ba868-133">Spowoduje to zainicjowanie zestaw SDK, aby zgłosić dzienniki w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="ba868-133">This triggers the SDK to report the logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
