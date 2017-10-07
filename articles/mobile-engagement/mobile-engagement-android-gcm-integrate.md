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
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a><span data-ttu-id="bc8e1-103">Jak tooIntegrate GCM z usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="bc8e1-103">How tooIntegrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bc8e1-104">Musisz wykonać procedurę integracji hello opisanego w hello jak tooIntegrate zaangażowania w systemie Android dokumentu przed wykonaniem tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="bc8e1-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="bc8e1-105">Ten dokument jest przydatny tylko wtedy, gdy już zintegrowane hello osiągnąć modułu i plan toopush Google Play urządzeń.</span><span class="sxs-lookup"><span data-stu-id="bc8e1-105">This document is useful only if you already integrated hello Reach module and plan toopush Google Play devices.</span></span> <span data-ttu-id="bc8e1-106">kampanie Zasięgowe toointegrate w aplikacji, przeczytaj najpierw jak tooIntegrate w systemie Android Reach usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="bc8e1-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="bc8e1-107">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="bc8e1-107">Introduction</span></span>
<span data-ttu-id="bc8e1-108">Integrowanie usługi GCM umożliwia Twojej toobe aplikacji naciśnięty.</span><span class="sxs-lookup"><span data-stu-id="bc8e1-108">Integrating GCM allows your application toobe pushed.</span></span>

<span data-ttu-id="bc8e1-109">Ładunki GCM wypychana toohello SDK zawsze zawierają hello `azme` klucza w obiekcie danych hello.</span><span class="sxs-lookup"><span data-stu-id="bc8e1-109">GCM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="bc8e1-110">Dlatego jeśli używasz usługi GCM dla innego celu w aplikacji można filtrować wypchnięć na podstawie tego klucza.</span><span class="sxs-lookup"><span data-stu-id="bc8e1-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc8e1-111">Tylko urządzenia z systemem Android w wersji 2.2 lub powyżej, o Google Play zainstalowane i o Google włączono połączenia tła może zostać umieszczony przy użyciu usługi GCM; jednak można je zintegrować kod bezpiecznie na nieobsługiwany urządzenia (tylko używa intencje).</span><span class="sxs-lookup"><span data-stu-id="bc8e1-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="bc8e1-112">Tworzenie projektu usługi Google Cloud Messaging przy użyciu klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bc8e1-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="bc8e1-113">Integracja zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="bc8e1-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="bc8e1-114">Zarządzanie rejestracji urządzenia</span><span class="sxs-lookup"><span data-stu-id="bc8e1-114">Managing device registrations</span></span>
<span data-ttu-id="bc8e1-115">Każde urządzenie musi wysłać toohello polecenie rejestracji serwerów firmy Google, w przeciwnym razie nie można połączyć.</span><span class="sxs-lookup"><span data-stu-id="bc8e1-115">Each device must send a registration command toohello Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="bc8e1-116">Urządzenia można także wyrejestrować z powiadomienia usługi GCM (hello urządzenie jest automatycznie wyrejestrować odinstalowanie aplikacji hello).</span><span class="sxs-lookup"><span data-stu-id="bc8e1-116">A device can also unregister from GCM notifications (hello device is automatically unregistered if hello application is uninstalled).</span></span>

<span data-ttu-id="bc8e1-117">Jeśli nie używasz [zestaw SDK Google Play] lub możesz już wysyłaj zamiar rejestracji hello samodzielnie, należy zaangażowania automatycznej rejestracji urządzeń hello za Ciebie.</span><span class="sxs-lookup"><span data-stu-id="bc8e1-117">If you don't use [Google Play SDK] or you don't already send hello registration intent yourself, you can make Engagement register hello device automatically for you.</span></span>

<span data-ttu-id="bc8e1-118">tooenable, Dodaj następujące tooyour hello `AndroidManifest.xml` pliku wewnątrz hello `<application/>` tagu:</span><span class="sxs-lookup"><span data-stu-id="bc8e1-118">tooenable this, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="bc8e1-119">Komunikacji usługi Engagement Push toohello identyfikator rejestracji i otrzymywać powiadomienia</span><span class="sxs-lookup"><span data-stu-id="bc8e1-119">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="bc8e1-120">W kolejności toocommunicate hello rejestracji identyfikator toohello urządzenia hello Push zaangażowania usługi i otrzymywać powiadomienia jej, Dodaj następujące tooyour hello `AndroidManifest.xml` pliku wewnątrz hello `<application/>` tagów (nawet jeśli zarządzasz rejestracji urządzenia samodzielnie):</span><span class="sxs-lookup"><span data-stu-id="bc8e1-120">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you manage device registrations yourself):</span></span>

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

<span data-ttu-id="bc8e1-121">Upewnij się, masz hello następujących uprawnień w sieci `AndroidManifest.xml` (po hello `</application>` tag).</span><span class="sxs-lookup"><span data-stu-id="bc8e1-121">Ensure you have hello following permissions in your `AndroidManifest.xml` (after hello `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="bc8e1-122">Udziel Mobile Engagement tooyour dostępu do klucza interfejsu API usługi GCM</span><span class="sxs-lookup"><span data-stu-id="bc8e1-122">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="bc8e1-123">Postępuj zgodnie z [w tym przewodniku](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) tooyour dostępu do usługi Mobile Engagement toogrant klucz interfejsu API usługi GCM.</span><span class="sxs-lookup"><span data-stu-id="bc8e1-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement access tooyour GCM API Key.</span></span>

[zestaw SDK Google Play]:https://developers.google.com/cloud-messaging/android/start
