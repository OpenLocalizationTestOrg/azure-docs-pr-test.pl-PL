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
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a>Zaawansowana konfiguracja naboru uniwersalnych aplikacji systemu Windows SDK
> [!div class="op_single_selector"]
> * [Platforma uniwersalna systemu Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
> 
> 

W tej procedurze opisano sposób tooconfigure różnych opcji konfiguracji dla usługi Azure Mobile Engagement aplikacji systemu Android.

## <a name="prerequisites"></a>Wymagania wstępne
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a>Konfiguracja zaawansowana
### <a name="disable-automatic-crash-reporting"></a>Wyłącz automatyczne zgłaszanie awarii
Możesz wyłączyć hello awarii automatyczne funkcję zaangażowania raportowania. Następnie gdy wystąpi nieobsługiwany wyjątek, Engagement nie działa.

> [!WARNING]
> Jeśli wyłączyć tę funkcję, a następnie w przypadku wystąpienia awarii nieobsługiwany w aplikacji zaangażowania nie wysyła awarii hello **i** nie zamknięcia sesji hello i zadania.
> 
> 

toodisable awarii automatycznego raportowania, Dostosuj konfigurację, w zależności od sposób hello należy zadeklarować jako:

#### <a name="from-engagementconfigurationxml-file"></a>Z `EngagementConfiguration.xml` pliku
Raport z ustawiania awaria zbyt`false` między `<reportCrash>` i `</reportCrash>` tagów.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Z `EngagementConfiguration` obiektu w czasie wykonywania
Ustaw przy użyciu obiektu EngagementConfiguration toofalse awarii raportu.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a>Wyłącz raportowanie w czasie rzeczywistym
Domyślnie raporty usługi Engagement hello rejestruje się w czasie rzeczywistym. Jeśli aplikacja zgłasza często dzienników, jest lepsze toobuffer hello dzienniki i tooreport ich jednocześnie na regularne czasowo. Jest on nazywany "Tryb szybki".

toodo należy wywołać metodę hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hello argument jest wartością w **milisekund**. Gdy użytkownicy rejestrowania w czasie rzeczywistym hello tooreactivate należy wywołać metodę hello bez parametrów lub z wartością hello 0.

Tryb serii nieco zwiększa hello czas pracy baterii, ale ma wpływ na powitania monitora usługi Engagement: wszystkie czas trwania sesji i zadań są zaokrąglone toohello serii próg (w związku z tym sesji i zadania krótsze niż próg serii hello może nie być widoczna). Firma Microsoft zaleca używanie próg w serii się niż 30000 (30s). Zapisane dzienniki są ograniczone too300 elementów. W przypadku wysyłania jest za długa, może spowodować utratę niektórych dzienników.

> [!WARNING]
> Próg serii Hello nie może być tooa skonfigurowanego okresu mniej niż drugi. Jeśli tak zrobisz, hello zestaw SDK zawiera śledzenia z powodu błędu hello i automatycznie resetuje wartość domyślna to toohello zero sekund. Ta wyzwalaczy hello SDK tooreport hello zaloguje się w czasie rzeczywistym.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
