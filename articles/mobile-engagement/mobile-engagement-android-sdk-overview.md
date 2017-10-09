---
title: "aaaAndroid integracji zestawu SDK dla usługi Azure Mobile Engagement"
description: "Opisuje sposób toointegrate zestawem Azure Mobile Engagement SDK w aplikacji systemu Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a>Integracja zestawu SDK systemu android dla usługi Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Platforma uniwersalna systemu Windows](mobile-engagement-windows-store-sdk-overview.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-sdk-overview.md)
> * [iOS](mobile-engagement-ios-sdk-overview.md)
> * [Android](mobile-engagement-android-sdk-overview.md)
> 
> 

W tym dokumencie opisano wszystkie hello integracji i opcje konfiguracji dostępne dla zestawem Azure Mobile Engagement Android SDK.

## <a name="prerequisites"></a>Wymagania wstępne
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a>Funkcje zaawansowane
### <a name="reporting-features"></a>Funkcje raportowania
Można dodać następujące funkcje:

1. [Zaawansowane opcje raportowania](mobile-engagement-android-advanced-reporting.md)
2. [Opcje raportowania lokalizacji](mobile-engagement-android-location-reporting.md)
3. [Zaawansowane opcje konfiguracji](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a>Powiadomienia:
[Jak toointegrate Reach (powiadomienia) w aplikacji systemu Android](mobile-engagement-android-integrate-engagement-reach.md)

1. Google Cloud Messaging (GCM): [jak tooIntegrate GCM z usługi Mobile Engagement](mobile-engagement-android-gcm-integrate.md)
2. Amazon urządzenia Messaging (ADM): [jak tooIntegrate ADM z usługi Mobile Engagement](mobile-engagement-android-adm-integrate.md)

### <a name="tag-plan-implementation"></a>Tag plan implementacji:
[Jak toouse hello zaawansowane usługi Mobile Engagement znakowanie interfejsu API w aplikacji systemu Android](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a>Informacje o wersji

### <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Usuń awarii rzadko może się zdarzyć podczas wywoływania metody `EngagementAgentUtils.isInDedicatedEngagementProcess`, która jest już używana przez hello `EngagementApplication` klasy.

### <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Obsługa 8 systemu android (poprzednie wersje powitalne zestawu SDK nie będą działać na 8 dla systemu Android).
* Nie więcej zależności biblioteki pomocy technicznej.
* Usuń `EngagementFragmentActivity` klasy.
* Z powodu zbyt[limity wykonywania tła](https://developer.android.com/preview/features/background.html) na 8 dla systemu Android, dzienniki w tle mogą zostać opóźnione aż hello użytkownik wchodzi w interakcję z urządzeniem hello, będzie to mieć wpływ na Push kampanii **dostarczone** i **Powiadomienie systemowe wyświetlane** statystyki opóźnieniu, jeśli został uśpiony hello urządzenia (hello powiadomienia będą nadal wyświetlane, będzie pierścienia i Włącz wibrację w czasie rzeczywistym bez problemów).
* Z powodu zbyt[ograniczenia lokalizacji tła](https://developer.android.com/preview/features/background-location-limits.html), hello czasu rzeczywistego lokalizacji w tle nie zostanie zaktualizowany często na 8 dla systemu Android.

Wszystkie wersje, można znaleźć w sekcji hello [ukończyć wersji](mobile-engagement-android-release-notes.md).

## <a name="upgrade-procedures"></a>Procedury uaktualniania
Jeśli już jest zintegrowany starszej wersji naszego zestawu SDK do aplikacji, należy skontaktować się [procedur uaktualniania](mobile-engagement-android-upgrade-procedure.md).

