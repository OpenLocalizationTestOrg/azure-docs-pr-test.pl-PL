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
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="2c891-103">Zaawansowane raporty dzięki zaangażowania w systemie Android</span><span class="sxs-lookup"><span data-stu-id="2c891-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c891-104">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="2c891-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="2c891-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="2c891-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="2c891-106">iOS</span><span class="sxs-lookup"><span data-stu-id="2c891-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="2c891-107">Android</span><span class="sxs-lookup"><span data-stu-id="2c891-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="2c891-108">W tym temacie opisano dodatkowe scenariusze raportowania w aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="2c891-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="2c891-109">Można zastosować tych aplikacji toohello opcje utworzone w hello [wprowadzenie](mobile-engagement-android-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="2c891-109">You can apply these options toohello app created in hello [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c891-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2c891-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="2c891-111">Samouczek Hello, które zostały ukończone został celowo bezpośredniego i prostego, ale są zaawansowane opcje, które można wybrać.</span><span class="sxs-lookup"><span data-stu-id="2c891-111">hello tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="2c891-112">Modyfikowanie użytkownika `Activity` klas</span><span class="sxs-lookup"><span data-stu-id="2c891-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="2c891-113">W hello [Wprowadzenie — samouczek](mobile-engagement-android-get-started.md), wszystkie miał toodo zostały toomake Twojego `*Activity` podklasy dziedziczyć odpowiadającego hello `Engagement*Activity` klasy.</span><span class="sxs-lookup"><span data-stu-id="2c891-113">In hello [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had toodo was toomake your `*Activity` subclasses inherit from hello corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="2c891-114">Na przykład jeśli Twoje działanie starszej wersji rozszerzony `ListActivity`, możesz spowodowałoby, że rozszerzenie `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="2c891-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c891-115">Korzystając z `EngagementListActivity` lub `EngagementExpandableListActivity`, upewnij się, że w żadnym wywołaniu zbyt`requestWindowFeature(...);` dokonane przed wywołaniem hello zbyt`super.onCreate(...);`, w przeciwnym razie wystąpi awaria.</span><span class="sxs-lookup"><span data-stu-id="2c891-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="2c891-116">Te klasy można znaleźć w hello `src` folderu i skopiować je do projektu.</span><span class="sxs-lookup"><span data-stu-id="2c891-116">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="2c891-117">klasy Hello znajdują się również w hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="2c891-117">hello classes are also in hello **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="2c891-118">Alternatywna metoda: wywołanie `startActivity()` i `endActivity()` ręcznie</span><span class="sxs-lookup"><span data-stu-id="2c891-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="2c891-119">Jeśli nie możesz lub nie ma toooverload Twojego `Activity` klas, można zamiast tego rozpoczęcia i zakończenia działań przez wywołanie metody hello `EngagementAgent`przez metody bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="2c891-119">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling hello `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c891-120">zestaw SDK systemu Android Hello nigdy nie wywołuje hello `endActivity()` metody, nawet wtedy, gdy aplikacja hello jest zamknięta (w systemie Android, aplikacje są nigdy nie zamknięte).</span><span class="sxs-lookup"><span data-stu-id="2c891-120">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="2c891-121">W związku z tym jest *wysokiej* zalecane toocall hello `startActivity()` metoda hello `onResume` wywołania zwrotnego z *wszystkie* działań i hello `endActivity()` metoda hello `onPause()` Wywołanie zwrotne z *wszystkie* działań.</span><span class="sxs-lookup"><span data-stu-id="2c891-121">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="2c891-122">Jest to hello tylko sposób toobe się, że nie przedostają sesji.</span><span class="sxs-lookup"><span data-stu-id="2c891-122">This is hello only way toobe sure that sessions are not leaked.</span></span> <span data-ttu-id="2c891-123">Jeśli przeciek sesji hello usługi Engagement nigdy nie zostanie przerwane z zapleczem usługi Engagement hello (ponieważ usługa hello połączono tak długo, jak długo trwa oczekiwanie na sesji).</span><span class="sxs-lookup"><span data-stu-id="2c891-123">If a session is leaked, hello Engagement service never disconnects from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="2c891-124">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="2c891-124">Here is an example:</span></span>

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

<span data-ttu-id="2c891-125">W tym przykładzie jest podobne toohello `EngagementActivity` klasy i jej wariantów, którego kod źródłowy jest udostępniany w hello `src` folderu.</span><span class="sxs-lookup"><span data-stu-id="2c891-125">This example is similar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="2c891-126">Przy użyciu Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="2c891-126">Using Application.onCreate()</span></span>
<span data-ttu-id="2c891-127">Kod umieszczony w `Application.onCreate()` i w innej aplikacji dla procesów wszystkich aplikacji, w tym usługi Engagement hello jest uruchamiane wywołań zwrotnych.</span><span class="sxs-lookup"><span data-stu-id="2c891-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="2c891-128">Może mieć niepożądane efekty uboczne, takich jak przydziału pamięci niepotrzebnych i wątków w procesie zaangażowania hello, lub zduplikowane emisji odbiorcy lub usług.</span><span class="sxs-lookup"><span data-stu-id="2c891-128">It may have unwanted side effects, like unneeded memory allocations and threads in hello Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="2c891-129">Jeśli można zastąpić `Application.onCreate()`, zaleca się dodawania hello następującego fragmentu kodu na początku hello Twojej `Application.onCreate()` funkcji:</span><span class="sxs-lookup"><span data-stu-id="2c891-129">If you override `Application.onCreate()`, we recommend adding hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="2c891-130">Możesz zrobić hello samo dla `Application.onTerminate()`, `Application.onLowMemory()`, i `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="2c891-130">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="2c891-131">Można również rozszerzyć zasięg `EngagementApplication` zamiast rozszerzanie `Application`: hello wywołania zwrotnego `Application.onCreate()` hello procesu wyboru i wywołania `Application.onApplicationProcessCreate()` tylko jeśli hello bieżący proces jest nie hello jeden hello zaangażowania Usługa hostingu, hello te same zasady stosowane dla Witaj innych wywołań zwrotnych.</span><span class="sxs-lookup"><span data-stu-id="2c891-131">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="tags-in-hello-androidmanifestxml-file"></a><span data-ttu-id="2c891-132">Tagi w pliku AndroidManifest.xml hello</span><span class="sxs-lookup"><span data-stu-id="2c891-132">Tags in hello AndroidManifest.xml file</span></span>
<span data-ttu-id="2c891-133">W tagu usługi hello w pliku AndroidManifest.xml hello hello `android:label` atrybutu pozwala toochoose nazwę hello hello usługi Engagement wyświetlaną ekranie "Uruchamianie usługi" hello telefon tooend użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2c891-133">In hello service tag in hello AndroidManifest.xml file, hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it appears tooend users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="2c891-134">Firma Microsoft zaleca ustawienie tego atrybutu zbyt`"<Your application name>Service"` (na przykład `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="2c891-134">We recommended setting this attribute too`"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="2c891-135">Określanie hello `android:process` atrybutu zapewnia tego hello uruchamia usługi Engagement we własnym procesie (uruchomionego zaangażowania w hello tego samego procesu jak aplikacja sprawia, że Twoje main/wątku interfejsu użytkownika jest potencjalnie mniej reakcji).</span><span class="sxs-lookup"><span data-stu-id="2c891-135">Specifying hello `android:process` attribute ensures that hello Engagement service runs in its own process (running Engagement in hello same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="2c891-136">Kompilowanie z użyciem ProGuard</span><span class="sxs-lookup"><span data-stu-id="2c891-136">Building with ProGuard</span></span>
<span data-ttu-id="2c891-137">Tworzenie pakietu aplikacji z narzędzia ProGuard, należy najpierw tookeep niektórych klas.</span><span class="sxs-lookup"><span data-stu-id="2c891-137">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="2c891-138">Program hello następującego fragmentu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="2c891-138">You can use hello following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
