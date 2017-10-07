---
title: aaaAzure Mobile Engagement Windows Universal SDK integracji | Dokumentacja firmy Microsoft
description: "Integracja uniwersalnego systemu Windows dla zestawu SDK dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a>Integracja uniwersalnego zestawu SDK systemu Windows dla usługi Azure Mobile Engagement
W tym dokumencie opisano wszystkie hello integracji i opcje konfiguracji dostępne dla hello zestawem Azure Mobile Engagement Windows Universal SDK.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka, należy najpierw wykonać naszych [samouczek 15 minut](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="advanced-features"></a>Funkcje zaawansowane
### <a name="reporting-features"></a>Funkcje raportowania
Można dodać następujące funkcje:

1. [Zaawansowane opcje raportowania](mobile-engagement-windows-store-advanced-reporting.md)
2. [Zaawansowane opcje konfiguracji](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a>Powiadomienia
[Jak toointegrate Reach (powiadomienia) w aplikacji uniwersalnych systemu Windows](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a>Tag plan implementacji:
[Jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji uniwersalnych systemu Windows usługi Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a>Informacje o wersji
### <a name="341-11032016"></a>3.4.1 (11/03/2016)

* Ulepszenia.

W przypadku wcześniejszych wersji, zobacz hello [ukończyć informacje o wersji](mobile-engagement-windows-store-release-notes.md)

## <a name="upgrade-procedures"></a>Procedury uaktualniania
Jeśli już jest zintegrowany starszą wersję programu zaangażowania do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.

Jeśli pominięte różne wersje hello SDK może być toofollow kilka procedur. Zobacz pełną hello [procedur uaktualniania](mobile-engagement-windows-store-upgrade-procedure.md). Na przykład w przypadku migracji z 0.10.1 too0.11.0 masz toofirst wykonaj hello "z 0.9.0 too0.10.1" procedury, a następnie hello "z 0.10.1 too0.11.0" procedury.

### <a name="from-330-too340"></a>Z 3.3.0 too3.4.0
#### <a name="test-logs"></a>Dzienniki testów
Dzienniki konsoli utworzonego przez zestaw SDK hello można teraz włączone/wyłączone/odfiltrowane. toocustomize, właściwość hello aktualizacji `EngagementAgent.Instance.TestLogEnabled` tooone wartości hello dostępnej w sklepie hello `EngagementTestLogLevel` wyliczenia, na przykład:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a>Zasoby
udoskonalono Hello Reach nakładki. Jest ona częścią zasoby pakietu SDK NuGet hello.

Podczas uaktualniania toohello nowej wersji zestawu SDK hello, można wybrać, czy ma tookeep istniejących plików z hello nakładki folderu zasobów:

* Nakładki poprzedniej hello działa automatycznie, czy jest integrowany hello `WebView` elementy ręcznie, następnie można określić tookeep Twojego zamykanie plików, będą nadal działać.
* tooupdate toohello nowe nakładki, Zastąp hello całego `overlay` folder z Twoich zasobów z hello nową z pakietu SDK hello (aplikacji platformy uniwersalnej systemu Windows: po uaktualnieniu hello, możesz pobrać ze strony % USERPROFILE % hello nowy folder na nakładce\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Przy użyciu nowego nakładki hello zastępuje wszelkie zmiany wprowadzone na powitania poprzedniej wersji.
> 
> 

### <a name="upgrade-from-older-versions"></a>Uaktualnij ze starszych wersji
Zobacz [procedur uaktualniania](mobile-engagement-windows-store-upgrade-procedure.md)

