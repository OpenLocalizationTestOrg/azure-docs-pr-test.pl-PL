---
title: Zaawansowane opcje raportowania zestawem Azure Mobile Engagement Android SDK
description: Opis sposobu wykonywania zaawansowane raportowanie w celu przechwytywania analytics dla zestawem Azure Mobile Engagement Android SDK
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
ms.openlocfilehash: 2a1445afa2c2fca1a31ad9c012b9c8a917ebf65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="871a3-103">Zaawansowane raporty dzięki zaangażowania w systemie Android</span><span class="sxs-lookup"><span data-stu-id="871a3-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="871a3-104">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="871a3-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="871a3-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="871a3-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="871a3-106">iOS</span><span class="sxs-lookup"><span data-stu-id="871a3-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="871a3-107">Android</span><span class="sxs-lookup"><span data-stu-id="871a3-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="871a3-108">W tym temacie opisano dodatkowe scenariusze raportowania w aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="871a3-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="871a3-109">Te opcje można zastosować do aplikacji utworzonych w [wprowadzenie](mobile-engagement-android-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="871a3-109">You can apply these options to the app created in the [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="871a3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="871a3-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="871a3-111">Samouczek, które zostały ukończone został celowo bezpośredniego i prostego, ale są zaawansowane opcje, które można wybrać.</span><span class="sxs-lookup"><span data-stu-id="871a3-111">The tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="871a3-112">Modyfikowanie użytkownika `Activity` klas</span><span class="sxs-lookup"><span data-stu-id="871a3-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="871a3-113">W [Wprowadzenie — samouczek](mobile-engagement-android-get-started.md), wszystkie musiał wykonać było Twojej `*Activity` podklasy dziedziczyć odpowiadającego `Engagement*Activity` klasy.</span><span class="sxs-lookup"><span data-stu-id="871a3-113">In the [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had to do was to make your `*Activity` subclasses inherit from the corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="871a3-114">Na przykład jeśli Twoje działanie starszej wersji rozszerzony `ListActivity`, możesz spowodowałoby, że rozszerzenie `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="871a3-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="871a3-115">Korzystając z `EngagementListActivity` lub `EngagementExpandableListActivity`, upewnij się, że wszelkie wywołanie `requestWindowFeature(...);` staje się przed wywołaniem do `super.onCreate(...);`, w przeciwnym razie wystąpi awaria.</span><span class="sxs-lookup"><span data-stu-id="871a3-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="871a3-116">Te klasy w można znaleźć `src` folderu i skopiować je do projektu.</span><span class="sxs-lookup"><span data-stu-id="871a3-116">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="871a3-117">Klasy są również w **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="871a3-117">The classes are also in the **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="871a3-118">Alternatywna metoda: wywołanie `startActivity()` i `endActivity()` ręcznie</span><span class="sxs-lookup"><span data-stu-id="871a3-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="871a3-119">Jeśli nie możesz lub nie było przeciążyć Twojej `Activity` klas, można zamiast tego rozpoczęcia i zakończenia działań przez wywołanie metody `EngagementAgent`przez metody bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="871a3-119">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling the `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="871a3-120">Zestaw SDK systemu Android nigdy nie wywołuje `endActivity()` metody, nawet wtedy, gdy aplikacja zostanie zamknięta (w systemie Android, aplikacje są nigdy nie zamknięte).</span><span class="sxs-lookup"><span data-stu-id="871a3-120">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="871a3-121">W związku z tym jest *wysokiej* zaleca, aby wywołać `startActivity()` metody w `onResume` wywołania zwrotnego z *wszystkie* działaniami i `endActivity()` metody w `onPause()` wywołania zwrotnego z *wszystkie* działań.</span><span class="sxs-lookup"><span data-stu-id="871a3-121">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="871a3-122">To jest jedynym sposobem należy upewnić się, że nie przedostają sesji.</span><span class="sxs-lookup"><span data-stu-id="871a3-122">This is the only way to be sure that sessions are not leaked.</span></span> <span data-ttu-id="871a3-123">Jeśli przeciek sesji usługi Engagement nigdy nie zakończy połączenie z zapleczem usługi Engagement (ponieważ usługa połączono tak długo, jak długo trwa oczekiwanie na sesji).</span><span class="sxs-lookup"><span data-stu-id="871a3-123">If a session is leaked, the Engagement service never disconnects from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="871a3-124">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="871a3-124">Here is an example:</span></span>

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

<span data-ttu-id="871a3-125">W tym przykładzie jest podobny do `EngagementActivity` klasy i jej wariantów, którego kod źródłowy jest udostępniany w `src` folderu.</span><span class="sxs-lookup"><span data-stu-id="871a3-125">This example is similar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="871a3-126">Przy użyciu Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="871a3-126">Using Application.onCreate()</span></span>
<span data-ttu-id="871a3-127">Kod umieszczony w `Application.onCreate()` i w innej aplikacji wywołania zwrotne jest wykonywane dla procesów wszystkich aplikacji, w tym usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="871a3-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="871a3-128">Może mieć niepożądane efekty uboczne, takich jak przydziału pamięci niepotrzebnych i wątków w procesie stopnia zaangażowania, lub zduplikowane odbiorniki emisji lub usługi.</span><span class="sxs-lookup"><span data-stu-id="871a3-128">It may have unwanted side effects, like unneeded memory allocations and threads in the Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="871a3-129">Jeśli można zastąpić `Application.onCreate()`, zaleca się dodawania poniższy fragment kodu na początku Twojej `Application.onCreate()` funkcji:</span><span class="sxs-lookup"><span data-stu-id="871a3-129">If you override `Application.onCreate()`, we recommend adding the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="871a3-130">Tak samo postąpić w `Application.onTerminate()`, `Application.onLowMemory()`, i `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="871a3-130">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="871a3-131">Można rozszerzać `EngagementApplication` zamiast rozszerzanie `Application`: wywołanie zwrotne `Application.onCreate()` jest wyboru procesu i wywołania `Application.onApplicationProcessCreate()` tylko jeśli bieżący proces nie jest obsługującym usługę zaangażowania, te same zasady poprosić o innych wywołań zwrotnych.</span><span class="sxs-lookup"><span data-stu-id="871a3-131">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="tags-in-the-androidmanifestxml-file"></a><span data-ttu-id="871a3-132">Tagi w pliku AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="871a3-132">Tags in the AndroidManifest.xml file</span></span>
<span data-ttu-id="871a3-133">W tagu usługi w pliku AndroidManifest.xml `android:label` atrybutu umożliwia wybór nazwy usługi Engagement wyświetlaną użytkownikom końcowym na ekranie telefon "Uruchamianie usługi".</span><span class="sxs-lookup"><span data-stu-id="871a3-133">In the service tag in the AndroidManifest.xml file, the `android:label` attribute allows you to choose the name of the Engagement service as it appears to end users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="871a3-134">Firma Microsoft zaleca ustawienie tego atrybutu na `"<Your application name>Service"` (na przykład `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="871a3-134">We recommended setting this attribute to `"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="871a3-135">Określanie `android:process` atrybutu zapewnia, że usługi Engagement działa we własnym procesie (uruchamianie zaangażowania w ramach tego samego procesu, zgodnie z aplikacji sprawia, że Twoje main/wątku interfejsu użytkownika jest potencjalnie mniej dynamiczne).</span><span class="sxs-lookup"><span data-stu-id="871a3-135">Specifying the `android:process` attribute ensures that the Engagement service runs in its own process (running Engagement in the same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="871a3-136">Kompilowanie z użyciem ProGuard</span><span class="sxs-lookup"><span data-stu-id="871a3-136">Building with ProGuard</span></span>
<span data-ttu-id="871a3-137">W przypadku tworzenia pakietu aplikacji z narzędzia ProGuard, należy zachować niektóre klasy.</span><span class="sxs-lookup"><span data-stu-id="871a3-137">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="871a3-138">Możesz użyć następującego fragmentu kodu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="871a3-138">You can use the following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
