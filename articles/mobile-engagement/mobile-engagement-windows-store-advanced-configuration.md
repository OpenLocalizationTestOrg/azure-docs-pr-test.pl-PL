---
title: aaaAdvanced konfiguracji dla zestawu Windows Universal aplikacji Engagement SDK
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
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="7a38c-103">Zaawansowana konfiguracja naboru uniwersalnych aplikacji systemu Windows SDK</span><span class="sxs-lookup"><span data-stu-id="7a38c-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a38c-104">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="7a38c-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="7a38c-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="7a38c-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="7a38c-106">iOS</span><span class="sxs-lookup"><span data-stu-id="7a38c-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="7a38c-107">Android</span><span class="sxs-lookup"><span data-stu-id="7a38c-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="7a38c-108">W tej procedurze opisano sposób tooconfigure różnych opcji konfiguracji dla usługi Azure Mobile Engagement aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="7a38c-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a38c-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7a38c-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="7a38c-110">Konfiguracja zaawansowana</span><span class="sxs-lookup"><span data-stu-id="7a38c-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="7a38c-111">Wyłącz automatyczne zgłaszanie awarii</span><span class="sxs-lookup"><span data-stu-id="7a38c-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="7a38c-112">Możesz wyłączyć hello awarii automatyczne funkcję zaangażowania raportowania.</span><span class="sxs-lookup"><span data-stu-id="7a38c-112">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="7a38c-113">Następnie gdy wystąpi nieobsługiwany wyjątek, Engagement nie działa.</span><span class="sxs-lookup"><span data-stu-id="7a38c-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="7a38c-114">Jeśli wyłączyć tę funkcję, a następnie w przypadku wystąpienia awarii nieobsługiwany w aplikacji zaangażowania nie wysyła awarii hello **i** nie zamknięcia sesji hello i zadania.</span><span class="sxs-lookup"><span data-stu-id="7a38c-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send hello crash **AND** does not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="7a38c-115">toodisable awarii automatycznego raportowania, Dostosuj konfigurację, w zależności od sposób hello należy zadeklarować jako:</span><span class="sxs-lookup"><span data-stu-id="7a38c-115">toodisable automatic crash reporting, customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="7a38c-116">Z `EngagementConfiguration.xml` pliku</span><span class="sxs-lookup"><span data-stu-id="7a38c-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="7a38c-117">Raport z ustawiania awaria zbyt`false` między `<reportCrash>` i `</reportCrash>` tagów.</span><span class="sxs-lookup"><span data-stu-id="7a38c-117">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="7a38c-118">Z `EngagementConfiguration` obiektu w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="7a38c-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="7a38c-119">Ustaw przy użyciu obiektu EngagementConfiguration toofalse awarii raportu.</span><span class="sxs-lookup"><span data-stu-id="7a38c-119">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="7a38c-120">Wyłącz raportowanie w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="7a38c-120">Disable real time reporting</span></span>
<span data-ttu-id="7a38c-121">Domyślnie raporty usługi Engagement hello rejestruje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="7a38c-121">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="7a38c-122">Jeśli aplikacja zgłasza często dzienników, jest lepsze toobuffer hello dzienniki i tooreport ich jednocześnie na regularne czasowo.</span><span class="sxs-lookup"><span data-stu-id="7a38c-122">If your application reports logs frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time basis.</span></span> <span data-ttu-id="7a38c-123">Jest on nazywany "Tryb szybki".</span><span class="sxs-lookup"><span data-stu-id="7a38c-123">This is called “burst mode”.</span></span>

<span data-ttu-id="7a38c-124">toodo należy wywołać metodę hello:</span><span class="sxs-lookup"><span data-stu-id="7a38c-124">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="7a38c-125">Hello argument jest wartością w **milisekund**.</span><span class="sxs-lookup"><span data-stu-id="7a38c-125">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="7a38c-126">Gdy użytkownicy rejestrowania w czasie rzeczywistym hello tooreactivate należy wywołać metodę hello bez parametrów lub z wartością hello 0.</span><span class="sxs-lookup"><span data-stu-id="7a38c-126">Whenever you want tooreactivate hello real-time logging, call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="7a38c-127">Tryb serii nieco zwiększa hello czas pracy baterii, ale ma wpływ na powitania monitora usługi Engagement: wszystkie czas trwania sesji i zadań są zaokrąglone toohello serii próg (w związku z tym sesji i zadania krótsze niż próg serii hello może nie być widoczna).</span><span class="sxs-lookup"><span data-stu-id="7a38c-127">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="7a38c-128">Firma Microsoft zaleca używanie próg w serii się niż 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="7a38c-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="7a38c-129">Zapisane dzienniki są ograniczone too300 elementów.</span><span class="sxs-lookup"><span data-stu-id="7a38c-129">Saved logs are limited too300 items.</span></span> <span data-ttu-id="7a38c-130">W przypadku wysyłania jest za długa, może spowodować utratę niektórych dzienników.</span><span class="sxs-lookup"><span data-stu-id="7a38c-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="7a38c-131">Próg serii Hello nie może być tooa skonfigurowanego okresu mniej niż drugi.</span><span class="sxs-lookup"><span data-stu-id="7a38c-131">hello burst threshold cannot be configured tooa period less than one second.</span></span> <span data-ttu-id="7a38c-132">Jeśli tak zrobisz, hello zestaw SDK zawiera śledzenia z powodu błędu hello i automatycznie resetuje wartość domyślna to toohello zero sekund.</span><span class="sxs-lookup"><span data-stu-id="7a38c-132">If you do so, hello SDK shows a trace with hello error and automatically resets toohello default value, zero seconds.</span></span> <span data-ttu-id="7a38c-133">Ta wyzwalaczy hello SDK tooreport hello zaloguje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="7a38c-133">This triggers hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
