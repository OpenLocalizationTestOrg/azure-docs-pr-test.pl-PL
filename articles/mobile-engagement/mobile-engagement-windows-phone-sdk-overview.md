---
title: "aaaAzure Mobile Engagement Windows Phone Silverlight SDK omówienie | Dokumentacja firmy Microsoft"
description: "Omówienie hello systemu Windows Phone Silverlight SDK dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0e3d2420-0509-4952-8891-392e3dad9aaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: ff2febed2202127e0538373ebbabe674993ce39d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-overview-for-azure-mobile-engagement"></a>Windows Phone Silverlight SDK — omówienie dla usługi Azure Mobile Engagement
Zacznij tutaj tooget hello uzyskać szczegółowe informacje na temat toointegrate usługi Azure Mobile Engagement w aplikacji Windows Phone Silverlight. Jeśli chcesz toogive go try najpierw upewnij się, zakończeniu naszych [samouczek 15 minut](mobile-engagement-windows-phone-get-started.md).

Kliknij przycisk toosee hello [zawartość zestawu SDK](mobile-engagement-windows-phone-sdk-content.md)

## <a name="integration-procedures"></a>Procedury integracji
1. Zacznij tutaj: [jak toointegrate Mobile Engagement w aplikacji Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
2. Dla powiadomień: [jak toointegrate Reach (powiadomienia) w aplikacji Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement-reach.md)
3. Tag plan implementacji: [jak toouse hello zaawansowane usługi Mobile Engagement znakowanie interfejsu API w aplikacji Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md)

## <a name="release-notes"></a>Informacje o wersji
###<a name="331-11032016"></a>3.3.1 (11/03/2016)
Część hello *MicrosoftAzure.MobileEngagement* pakietu Nuget **v3.4.1**

* Ulepszenia.

Starsza wersja Zobacz hello [ukończyć informacje o wersji](mobile-engagement-windows-phone-release-notes.md)

## <a name="upgrade-procedures"></a>Procedury uaktualniania
Jeśli już jest zintegrowany starszej wersji naszego zestawu SDK do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.

Masz toofollow kilka procedur Jeśli pominięte różne wersje hello zestawu SDK. Zobacz pełną hello [procedur uaktualniania](mobile-engagement-windows-phone-upgrade-procedure.md). Na przykład w przypadku migracji z 0.10.1 too0.11.0 masz toofirst wykonaj hello "z 0.9.0 too0.10.1" procedury, a następnie hello "z 0.10.1 too0.11.0" procedury.

### <a name="from-200-too330"></a>Z 2.0.0 too3.3.0
#### <a name="test-logs"></a>Dzienniki testów
Dzienniki konsoli utworzonego przez zestaw SDK hello można teraz włączone/wyłączone/odfiltrowane. toocustomize ta, właściwość hello aktualizacji `EngagementAgent.Instance.TestLogEnabled` tooone hello wartość dostępna hello `EngagementTestLogLevel` wyliczenia, na przykład:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="upgrade-from-older-versions"></a>Uaktualnij ze starszych wersji
Zobacz [procedur uaktualniania](mobile-engagement-windows-phone-upgrade-procedure.md)

