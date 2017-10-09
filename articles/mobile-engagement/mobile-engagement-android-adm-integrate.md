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
# <a name="how-toointegrate-adm-with-engagement"></a>Jak tooIntegrate ADM z zaangażowania
> [!IMPORTANT]
> Musisz wykonać procedurę integracji hello opisanego w hello jak tooIntegrate zaangażowania w systemie Android dokumentu przed wykonaniem tego przewodnika.
> 
> Ten dokument jest przydatny tylko wtedy, gdy jest już zintegrowana hello Reach moduł i plan toopush Amazon urządzeń. kampanie Zasięgowe toointegrate w aplikacji, przeczytaj najpierw jak tooIntegrate w systemie Android Reach usługi Engagement.
> 
> 

## <a name="introduction"></a>Wprowadzenie
Integrowanie usługi ADM umożliwia Twojej toobe aplikacji przypisany podczas przeznaczonych dla urządzeń z systemem Android firmy Amazon.

Ładunki ADM wypychana toohello SDK zawsze zawierają hello `azme` klucza w obiekcie danych hello. Dlatego jeśli używasz usługi ADM do innych celów w aplikacji można filtrować wypchnięć na podstawie tego klucza.

> [!IMPORTANT]
> Tylko Amazon Kindle urządzeń z systemem Android 4.0.3 lub nowszym są obsługiwane przez usługi Amazon Device Messaging; jednak można je zintegrować ten kod bezpiecznie na innych urządzeniach.
> 
> 

## <a name="sign-up-tooadm"></a>Zarejestruj się tooADM
Jeśli nie zostało już przeprowadzone, należy włączyć ADM na Twoje konto Amazon.

procedury Hello została szczegółowo opisana w: [ <https://developer.amazon.com/sdk/adm/credentials.html>].

Po wykonaniu procedury hello można uzyskać:

* OAuth poświadczeń (identyfikator klienta i klucz tajny klienta) dla toopush stanie toobe zaangażowania urządzenia.
* Klucz interfejsu API, które muszą zostać włączone do aplikacji.

## <a name="sdk-integration"></a>Integracja zestawu SDK
### <a name="managing-device-registrations"></a>Zarządzanie rejestracji urządzenia
Każde urządzenie musi wysłać toohello polecenie rejestracji ADM serwerów, w przeciwnym razie nie można połączyć.

Jeśli używasz już hello [biblioteki klienta usługi ADM], a jeszcze [zintegrowane usługi ADM] bezpośrednio przejść, tooandroid-sdk-adm-receive.

Jeśli nie jest zintegrowana ADM jeszcze, Engagement ma prostsze tooenable sposób go w aplikacji:

Edytowanie użytkownika `AndroidManifest.xml` pliku:

* Dodaj hello nazw Amazon, plik hello powinny one zacząć następująco:
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* Witaj wewnątrz `<application/>` tagu, należy dodać w tej sekcji:
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* Po dodaniu hello amazon tag, może być błąd kompilacji, jeżeli urządzenie docelowe kompilacji projektu jest niższy niż Android 2.1. Masz toouse **Android 2.1 +** kompilacji docelowego (nie martw się, może nadal mieć `minSdkVersion` ustawić too4).
* Integracja hello klucz interfejsu API usługi ADM jako zasób, postępując [tej procedury].

Następnie postępuj zgodnie z instrukcjami hello hello kolejnych sekcjach.

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Komunikacji usługi Engagement Push toohello identyfikator rejestracji i otrzymywać powiadomienia
W kolejności toocommunicate hello rejestracji identyfikator toohello urządzenia hello Push zaangażowania usługi i otrzymywać powiadomienia jej, Dodaj następujące tooyour hello `AndroidManifest.xml` pliku wewnątrz hello `<application/>` tagów (nawet jeśli używasz usługi ADM bez zaangażowania):

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

Upewnij się, masz hello następujących uprawnień w sieci `AndroidManifest.xml` (przed hello `</application>` tag).

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a>Poświadczenia GRANT zaangażowania OAuth
Przedstawia poświadczeń OAuth (identyfikator klienta i klucz tajny klienta) w portalu Engagement.

[< https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[biblioteki klienta usługi ADM]:https://developer.amazon.com/sdk/adm/setup.html
[zintegrowane usługi ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[tej procedury]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
