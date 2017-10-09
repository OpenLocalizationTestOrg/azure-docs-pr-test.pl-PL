---
title: aaaAzure Mobile Engagement Android SDK integracji
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK systemu Android dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a><span data-ttu-id="b97b6-103">Jak tooIntegrate ADM z zaangażowania</span><span class="sxs-lookup"><span data-stu-id="b97b6-103">How tooIntegrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b97b6-104">Musisz wykonać procedurę integracji hello opisanego w hello jak tooIntegrate zaangażowania w systemie Android dokumentu przed wykonaniem tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="b97b6-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="b97b6-105">Ten dokument jest przydatny tylko wtedy, gdy jest już zintegrowana hello Reach moduł i plan toopush Amazon urządzeń.</span><span class="sxs-lookup"><span data-stu-id="b97b6-105">This document is useful only if you already integrated hello Reach module and plan toopush Amazon devices.</span></span> <span data-ttu-id="b97b6-106">kampanie Zasięgowe toointegrate w aplikacji, przeczytaj najpierw jak tooIntegrate w systemie Android Reach usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="b97b6-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="b97b6-107">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="b97b6-107">Introduction</span></span>
<span data-ttu-id="b97b6-108">Integrowanie usługi ADM umożliwia Twojej toobe aplikacji przypisany podczas przeznaczonych dla urządzeń z systemem Android firmy Amazon.</span><span class="sxs-lookup"><span data-stu-id="b97b6-108">Integrating ADM allows your application toobe pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="b97b6-109">Ładunki ADM wypychana toohello SDK zawsze zawierają hello `azme` klucza w obiekcie danych hello.</span><span class="sxs-lookup"><span data-stu-id="b97b6-109">ADM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="b97b6-110">Dlatego jeśli używasz usługi ADM do innych celów w aplikacji można filtrować wypchnięć na podstawie tego klucza.</span><span class="sxs-lookup"><span data-stu-id="b97b6-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b97b6-111">Tylko Amazon Kindle urządzeń z systemem Android 4.0.3 lub nowszym są obsługiwane przez usługi Amazon Device Messaging; jednak można je zintegrować ten kod bezpiecznie na innych urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="b97b6-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-tooadm"></a><span data-ttu-id="b97b6-112">Zarejestruj się tooADM</span><span class="sxs-lookup"><span data-stu-id="b97b6-112">Sign up tooADM</span></span>
<span data-ttu-id="b97b6-113">Jeśli nie zostało już przeprowadzone, należy włączyć ADM na Twoje konto Amazon.</span><span class="sxs-lookup"><span data-stu-id="b97b6-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="b97b6-114">procedury Hello została szczegółowo opisana w: [ <https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="b97b6-114">hello procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="b97b6-115">Po wykonaniu procedury hello można uzyskać:</span><span class="sxs-lookup"><span data-stu-id="b97b6-115">Upon completing hello procedure, you get:</span></span>

* <span data-ttu-id="b97b6-116">OAuth poświadczeń (identyfikator klienta i klucz tajny klienta) dla toopush stanie toobe zaangażowania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b97b6-116">OAuth credentials (a Client ID and a Client Secret) for Engagement toobe able toopush your devices.</span></span>
* <span data-ttu-id="b97b6-117">Klucz interfejsu API, które muszą zostać włączone do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b97b6-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="b97b6-118">Integracja zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="b97b6-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="b97b6-119">Zarządzanie rejestracji urządzenia</span><span class="sxs-lookup"><span data-stu-id="b97b6-119">Managing device registrations</span></span>
<span data-ttu-id="b97b6-120">Każde urządzenie musi wysłać toohello polecenie rejestracji ADM serwerów, w przeciwnym razie nie można połączyć.</span><span class="sxs-lookup"><span data-stu-id="b97b6-120">Each device must send a registration command toohello ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="b97b6-121">Jeśli używasz już hello [biblioteki klienta usługi ADM], a jeszcze [zintegrowane usługi ADM] bezpośrednio przejść, tooandroid-sdk-adm-receive.</span><span class="sxs-lookup"><span data-stu-id="b97b6-121">If you already use hello [ADM client library], and already have [integrated ADM] you can directly go tooandroid-sdk-adm-receive.</span></span>

<span data-ttu-id="b97b6-122">Jeśli nie jest zintegrowana ADM jeszcze, Engagement ma prostsze tooenable sposób go w aplikacji:</span><span class="sxs-lookup"><span data-stu-id="b97b6-122">If you have not integrated ADM yet, Engagement has a simpler way tooenable it in your application:</span></span>

<span data-ttu-id="b97b6-123">Edytowanie użytkownika `AndroidManifest.xml` pliku:</span><span class="sxs-lookup"><span data-stu-id="b97b6-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="b97b6-124">Dodaj hello nazw Amazon, plik hello powinny one zacząć następująco:</span><span class="sxs-lookup"><span data-stu-id="b97b6-124">Add hello Amazon namespace, hello file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="b97b6-125">Witaj wewnątrz `<application/>` tagu, należy dodać w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="b97b6-125">Inside hello `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="b97b6-126">Po dodaniu hello amazon tag, może być błąd kompilacji, jeżeli urządzenie docelowe kompilacji projektu jest niższy niż Android 2.1.</span><span class="sxs-lookup"><span data-stu-id="b97b6-126">After adding hello amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="b97b6-127">Masz toouse **Android 2.1 +** kompilacji docelowego (nie martw się, może nadal mieć `minSdkVersion` ustawić too4).</span><span class="sxs-lookup"><span data-stu-id="b97b6-127">You have toouse an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set too4).</span></span>
* <span data-ttu-id="b97b6-128">Integracja hello klucz interfejsu API usługi ADM jako zasób, postępując [tej procedury].</span><span class="sxs-lookup"><span data-stu-id="b97b6-128">Integrate hello ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="b97b6-129">Następnie postępuj zgodnie z instrukcjami hello hello kolejnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="b97b6-129">Then follow hello instructions of hello next sections.</span></span>

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="b97b6-130">Komunikacji usługi Engagement Push toohello identyfikator rejestracji i otrzymywać powiadomienia</span><span class="sxs-lookup"><span data-stu-id="b97b6-130">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="b97b6-131">W kolejności toocommunicate hello rejestracji identyfikator toohello urządzenia hello Push zaangażowania usługi i otrzymywać powiadomienia jej, Dodaj następujące tooyour hello `AndroidManifest.xml` pliku wewnątrz hello `<application/>` tagów (nawet jeśli używasz usługi ADM bez zaangażowania):</span><span class="sxs-lookup"><span data-stu-id="b97b6-131">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you use ADM without Engagement):</span></span>

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

<span data-ttu-id="b97b6-132">Upewnij się, masz hello następujących uprawnień w sieci `AndroidManifest.xml` (przed hello `</application>` tag).</span><span class="sxs-lookup"><span data-stu-id="b97b6-132">Ensure you have hello following permissions in your `AndroidManifest.xml` (before hello `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="b97b6-133">Poświadczenia GRANT zaangażowania OAuth</span><span class="sxs-lookup"><span data-stu-id="b97b6-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="b97b6-134">Przedstawia poświadczeń OAuth (identyfikator klienta i klucz tajny klienta) w portalu Engagement.</span><span class="sxs-lookup"><span data-stu-id="b97b6-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

[< https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[biblioteki klienta usługi ADM]:https://developer.amazon.com/sdk/adm/setup.html
[zintegrowane usługi ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[tej procedury]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
