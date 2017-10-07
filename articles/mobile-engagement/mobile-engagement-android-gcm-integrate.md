---
title: aaaAzure Mobile Engagement Android SDK integracji
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK systemu Android dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a>Jak tooIntegrate GCM z usługi Mobile Engagement
> [!IMPORTANT]
> Musisz wykonać procedurę integracji hello opisanego w hello jak tooIntegrate zaangażowania w systemie Android dokumentu przed wykonaniem tego przewodnika.
> 
> Ten dokument jest przydatny tylko wtedy, gdy już zintegrowane hello osiągnąć modułu i plan toopush Google Play urządzeń. kampanie Zasięgowe toointegrate w aplikacji, przeczytaj najpierw jak tooIntegrate w systemie Android Reach usługi Engagement.
> 
> 

## <a name="introduction"></a>Wprowadzenie
Integrowanie usługi GCM umożliwia Twojej toobe aplikacji naciśnięty.

Ładunki GCM wypychana toohello SDK zawsze zawierają hello `azme` klucza w obiekcie danych hello. Dlatego jeśli używasz usługi GCM dla innego celu w aplikacji można filtrować wypchnięć na podstawie tego klucza.

> [!IMPORTANT]
> Tylko urządzenia z systemem Android w wersji 2.2 lub powyżej, o Google Play zainstalowane i o Google włączono połączenia tła może zostać umieszczony przy użyciu usługi GCM; jednak można je zintegrować kod bezpiecznie na nieobsługiwany urządzenia (tylko używa intencje).
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a>Tworzenie projektu usługi Google Cloud Messaging przy użyciu klucza interfejsu API
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a>Integracja zestawu SDK
### <a name="managing-device-registrations"></a>Zarządzanie rejestracji urządzenia
Każde urządzenie musi wysłać toohello polecenie rejestracji serwerów firmy Google, w przeciwnym razie nie można połączyć.

Urządzenia można także wyrejestrować z powiadomienia usługi GCM (hello urządzenie jest automatycznie wyrejestrować odinstalowanie aplikacji hello).

Jeśli nie używasz [zestaw SDK Google Play] lub możesz już wysyłaj zamiar rejestracji hello samodzielnie, należy zaangażowania automatycznej rejestracji urządzeń hello za Ciebie.

tooenable, Dodaj następujące tooyour hello `AndroidManifest.xml` pliku wewnątrz hello `<application/>` tagu:

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Komunikacji usługi Engagement Push toohello identyfikator rejestracji i otrzymywać powiadomienia
W kolejności toocommunicate hello rejestracji identyfikator toohello urządzenia hello Push zaangażowania usługi i otrzymywać powiadomienia jej, Dodaj następujące tooyour hello `AndroidManifest.xml` pliku wewnątrz hello `<application/>` tagów (nawet jeśli zarządzasz rejestracji urządzenia samodzielnie):

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

Upewnij się, masz hello następujących uprawnień w sieci `AndroidManifest.xml` (po hello `</application>` tag).

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Udziel Mobile Engagement tooyour dostępu do klucza interfejsu API usługi GCM
Postępuj zgodnie z [w tym przewodniku](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) tooyour dostępu do usługi Mobile Engagement toogrant klucz interfejsu API usługi GCM.

[zestaw SDK Google Play]:https://developers.google.com/cloud-messaging/android/start
