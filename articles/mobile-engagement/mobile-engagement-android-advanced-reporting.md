---
title: aaaAdvanced raportowania opcji Azure Mobile Engagement Android SDK
description: W tym artykule opisano, jak toodo zaawansowanej analizy toocapture raportowania dla zestawem Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a>Zaawansowane raporty dzięki zaangażowania w systemie Android
> [!div class="op_single_selector"]
> * [Platforma uniwersalna systemu Windows](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

W tym temacie opisano dodatkowe scenariusze raportowania w aplikacji systemu Android. Można zastosować tych aplikacji toohello opcje utworzone w hello [wprowadzenie](mobile-engagement-android-get-started.md) samouczka.

## <a name="prerequisites"></a>Wymagania wstępne
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

Samouczek Hello, które zostały ukończone został celowo bezpośredniego i prostego, ale są zaawansowane opcje, które można wybrać.

## <a name="modifying-your-activity-classes"></a>Modyfikowanie użytkownika `Activity` klas
W hello [Wprowadzenie — samouczek](mobile-engagement-android-get-started.md), wszystkie miał toodo zostały toomake Twojego `*Activity` podklasy dziedziczyć odpowiadającego hello `Engagement*Activity` klasy. Na przykład jeśli Twoje działanie starszej wersji rozszerzony `ListActivity`, możesz spowodowałoby, że rozszerzenie `EngagementListActivity`.

> [!IMPORTANT]
> Korzystając z `EngagementListActivity` lub `EngagementExpandableListActivity`, upewnij się, że w żadnym wywołaniu zbyt`requestWindowFeature(...);` dokonane przed wywołaniem hello zbyt`super.onCreate(...);`, w przeciwnym razie wystąpi awaria.
> 
> 

Te klasy można znaleźć w hello `src` folderu i skopiować je do projektu. klasy Hello znajdują się również w hello **JavaDoc**.

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Alternatywna metoda: wywołanie `startActivity()` i `endActivity()` ręcznie
Jeśli nie możesz lub nie ma toooverload Twojego `Activity` klas, można zamiast tego rozpoczęcia i zakończenia działań przez wywołanie metody hello `EngagementAgent`przez metody bezpośrednio.

> [!IMPORTANT]
> zestaw SDK systemu Android Hello nigdy nie wywołuje hello `endActivity()` metody, nawet wtedy, gdy aplikacja hello jest zamknięta (w systemie Android, aplikacje są nigdy nie zamknięte). W związku z tym jest *wysokiej* zalecane toocall hello `startActivity()` metoda hello `onResume` wywołania zwrotnego z *wszystkie* działań i hello `endActivity()` metoda hello `onPause()` Wywołanie zwrotne z *wszystkie* działań. Jest to hello tylko sposób toobe się, że nie przedostają sesji. Jeśli przeciek sesji hello usługi Engagement nigdy nie zostanie przerwane z zapleczem usługi Engagement hello (ponieważ usługa hello połączono tak długo, jak długo trwa oczekiwanie na sesji).
> 
> 

Oto przykład:

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

W tym przykładzie jest podobne toohello `EngagementActivity` klasy i jej wariantów, którego kod źródłowy jest udostępniany w hello `src` folderu.

## <a name="using-applicationoncreate"></a>Przy użyciu Application.onCreate()
Kod umieszczony w `Application.onCreate()` i w innej aplikacji dla procesów wszystkich aplikacji, w tym usługi Engagement hello jest uruchamiane wywołań zwrotnych. Może mieć niepożądane efekty uboczne, takich jak przydziału pamięci niepotrzebnych i wątków w procesie zaangażowania hello, lub zduplikowane emisji odbiorcy lub usług.

Jeśli można zastąpić `Application.onCreate()`, zaleca się dodawania hello następującego fragmentu kodu na początku hello Twojej `Application.onCreate()` funkcji:

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

Możesz zrobić hello samo dla `Application.onTerminate()`, `Application.onLowMemory()`, i `Application.onConfigurationChanged(...)`.

Można również rozszerzyć zasięg `EngagementApplication` zamiast rozszerzanie `Application`: hello wywołania zwrotnego `Application.onCreate()` hello procesu wyboru i wywołania `Application.onApplicationProcessCreate()` tylko jeśli hello bieżący proces jest nie hello jeden hello zaangażowania Usługa hostingu, hello te same zasady stosowane dla Witaj innych wywołań zwrotnych.

## <a name="tags-in-hello-androidmanifestxml-file"></a>Tagi w pliku AndroidManifest.xml hello
W tagu usługi hello w pliku AndroidManifest.xml hello hello `android:label` atrybutu pozwala toochoose nazwę hello hello usługi Engagement wyświetlaną ekranie "Uruchamianie usługi" hello telefon tooend użytkowników. Firma Microsoft zaleca ustawienie tego atrybutu zbyt`"<Your application name>Service"` (na przykład `"AcmeFunGameService"`).

Określanie hello `android:process` atrybutu zapewnia tego hello uruchamia usługi Engagement we własnym procesie (uruchomionego zaangażowania w hello tego samego procesu jak aplikacja sprawia, że Twoje main/wątku interfejsu użytkownika jest potencjalnie mniej reakcji).

## <a name="building-with-proguard"></a>Kompilowanie z użyciem ProGuard
Tworzenie pakietu aplikacji z narzędzia ProGuard, należy najpierw tookeep niektórych klas. Program hello następującego fragmentu konfiguracji:

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
