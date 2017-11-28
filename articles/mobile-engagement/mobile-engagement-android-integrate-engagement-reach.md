---
title: "Integracja zestawu SDK systemu Android z usługi Azure Mobile Engagement"
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK systemu Android dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 26ba47b19f3a503693d60d344ad39b9eba74fe99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-reach-on-android"></a><span data-ttu-id="dbc38-103">Integrowanie Reach usługi Engagement w systemie Android</span><span class="sxs-lookup"><span data-stu-id="dbc38-103">How to Integrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dbc38-104">Musi występować po integracji procedury opisane w sekcji sposobu integracji usługi Engagement Android dokumentu przed wykonaniem tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="dbc38-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="dbc38-105">Standardowa integracji</span><span class="sxs-lookup"><span data-stu-id="dbc38-105">Standard integration</span></span>

<span data-ttu-id="dbc38-106">Skopiuj pliki zasobów Reach z zestawu SDK w projekcie:</span><span class="sxs-lookup"><span data-stu-id="dbc38-106">Copy Reach resource files from the SDK in your project :</span></span>

* <span data-ttu-id="dbc38-107">Skopiuj pliki z `res/layout` folderu dostarczane przy użyciu zestawu SDK do `res/layout` folderu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-107">Copy the files from the `res/layout` folder delivered with the SDK into the `res/layout` folder of your application.</span></span>
* <span data-ttu-id="dbc38-108">Skopiuj pliki z `res/drawable` folderu dostarczane przy użyciu zestawu SDK do `res/drawable` folderu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-108">Copy the files from the `res/drawable` folder delivered with the SDK into the `res/drawable` folder of your application.</span></span>

<span data-ttu-id="dbc38-109">Edytowanie użytkownika `AndroidManifest.xml` pliku:</span><span class="sxs-lookup"><span data-stu-id="dbc38-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="dbc38-110">Dodaj poniższą sekcję (między `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="dbc38-110">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/plain" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/html" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
              <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
              <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
          </activity>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
              <action android:name="android.intent.action.BOOT_COMPLETED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
          </receiver>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
              <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
          </receiver>
* <span data-ttu-id="dbc38-111">Należy to uprawnienie do powtarzania powiadomień systemowych, które nie zostały kliknięty przy rozruchu (w przeciwnym razie będą znajdować się na dysku, ale nie będą już wyświetlane, które trzeba uwzględniać to).</span><span class="sxs-lookup"><span data-stu-id="dbc38-111">You need this permission to replay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have to include this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="dbc38-112">Określanie ikony używany do powiadomień, (zarówno w aplikacji oraz systemowe z nich) przez kopiowanie i edytowania poniższej sekcji (między `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="dbc38-112">Specify an icon used for notifications (both in app and system ones) by copying and editing the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="dbc38-113">Ta sekcja ma **obowiązkowe** Jeśli planujesz używanie powiadomień systemowych, tworząc kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="dbc38-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="dbc38-114">Android uniemożliwia powiadomień systemowych bez ikony wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="dbc38-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="dbc38-115">Dlatego w przypadku pominięcia tej sekcji, użytkownicy końcowi uniemożliwi do ich odbierania.</span><span class="sxs-lookup"><span data-stu-id="dbc38-115">So if you omit this section, your end users will not be able to receive them.</span></span>
> 
> 

* <span data-ttu-id="dbc38-116">Jeśli tworzysz kampanie z powiadomień systemowych przy użyciu duży obraz, należy dodać następujące uprawnienia (po `</application>` tagu) Jeśli brak:</span><span class="sxs-lookup"><span data-stu-id="dbc38-116">If you create campaigns with system notifications using big picture, you need to add the following permissions (after the `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="dbc38-117">W systemie Android M i czy aplikacja korzysta poziom interfejsu API systemu Android 23 lub większą ``WRITE_EXTERNAL_STORAGE`` uprawnienia wymaga zatwierdzenia przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dbc38-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="dbc38-118">Przeczytaj [w tej sekcji](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="dbc38-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="dbc38-119">Dla powiadomień systemowych można również określić w kampanii Reach Jeśli urządzenie powinno pierścienia i/lub też.</span><span class="sxs-lookup"><span data-stu-id="dbc38-119">For system notifications you can also specify in the Reach campaign if the device should ring and/or vibrate.</span></span> <span data-ttu-id="dbc38-120">Dla tej funkcji, musisz upewnij się, że zadeklarowany następujących uprawnień (po `</application>` tagu):</span><span class="sxs-lookup"><span data-stu-id="dbc38-120">For it to work, you have to make sure you declared the following permission (after the `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="dbc38-121">Bez tego uprawnienia Android uniemożliwia powiadomień systemowych jest wyświetlany, jeśli zaznaczono pierścienia lub opcji vibrate w Menedżerze osiągnąć kampanii.</span><span class="sxs-lookup"><span data-stu-id="dbc38-121">Without this permission, Android prevents system notifications from being shown if you checked the ring or the vibrate option in the Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="dbc38-122">Natywnych powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="dbc38-122">Native Push</span></span>
<span data-ttu-id="dbc38-123">Teraz, możesz skonfigurować moduł Reach, należy skonfigurować natywnych powiadomień wypychanych, aby móc odbierać kampanii na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="dbc38-123">Now that you configured Reach module, you need to configure native push to be able to receive the campaigns on the device.</span></span>

<span data-ttu-id="dbc38-124">W systemie Android firma Microsoft obsługuje dwie usługi:</span><span class="sxs-lookup"><span data-stu-id="dbc38-124">We support two services on Android:</span></span>

* <span data-ttu-id="dbc38-125">Urządzenia ze sklepu Google Play: Użyj [Google Cloud Messaging] wykonując [jak GCM zintegrować z przewodnika zaangażowania](mobile-engagement-android-gcm-integrate.md) przewodnik.</span><span class="sxs-lookup"><span data-stu-id="dbc38-125">Google Play devices: Use [Google Cloud Messaging] by following the [How to Integrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="dbc38-126">Urządzenia firmy Amazon: Użyj [usługi Amazon Device Messaging] wykonując [jak zintegrować ADM prowadnicy zaangażowania](mobile-engagement-android-adm-integrate.md) przewodnik.</span><span class="sxs-lookup"><span data-stu-id="dbc38-126">Amazon devices: Use [Amazon Device Messaging] by following the [How to Integrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="dbc38-127">Jeśli chcesz przeanalizować urządzeń zarówno Amazon, jak i Google Play, można mieć wszystkie elementy wewnątrz 1 AndroidManifest.xml/APK do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-127">If you want to target both Amazon and Google Play devices, its possible to have everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="dbc38-128">Jednak podczas przesyłania do Amazon, mogą one odrzucić aplikacji, jeśli znajduje się kod usługi GCM.</span><span class="sxs-lookup"><span data-stu-id="dbc38-128">But when submitting to Amazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="dbc38-129">W takim przypadku należy używać wielu APKs.</span><span class="sxs-lookup"><span data-stu-id="dbc38-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="dbc38-130">**Aplikacja jest teraz gotowa do odbierania i wyświetlić kampanie zasięgowe!**</span><span class="sxs-lookup"><span data-stu-id="dbc38-130">**Your application is now ready to receive and display reach campaigns!**</span></span>

## <a name="how-to-handle-data-push"></a><span data-ttu-id="dbc38-131">Sposób obsługi wypychanie danych</span><span class="sxs-lookup"><span data-stu-id="dbc38-131">How to handle data push</span></span>
### <a name="integration"></a><span data-ttu-id="dbc38-132">Integracja</span><span class="sxs-lookup"><span data-stu-id="dbc38-132">Integration</span></span>
<span data-ttu-id="dbc38-133">Jeśli chcesz otrzymywać Reach wypychania danych aplikacji, należy utworzyć podklasą klasy `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` i odwołuje się on w `AndroidManifest.xml` pliku (między `<application>` i/lub `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="dbc38-133">If you want your application to be able to receive Reach data pushes, you have to create a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in the `AndroidManifest.xml` file (between the `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="dbc38-134">Następnie można zastąpić `onDataPushStringReceived` i `onDataPushBase64Received` wywołań zwrotnych.</span><span class="sxs-lookup"><span data-stu-id="dbc38-134">Then you can override the `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="dbc38-135">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="dbc38-135">Here is an example:</span></span>

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a><span data-ttu-id="dbc38-136">Kategoria</span><span class="sxs-lookup"><span data-stu-id="dbc38-136">Category</span></span>
<span data-ttu-id="dbc38-137">Parametr kategorii jest opcjonalny, podczas tworzenia kampanii wypychania danych i umożliwia Wypychanie do filtrowania danych.</span><span class="sxs-lookup"><span data-stu-id="dbc38-137">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="dbc38-138">Jest to przydatne, jeśli masz wiele odbiorników emisji obsługi różnych typów wypychania danych, lub jeśli chcesz dystrybuować różnych rodzajów z `Base64` danych, aby zidentyfikować ich typu przed ich analizowania.</span><span class="sxs-lookup"><span data-stu-id="dbc38-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="dbc38-139">Parametr zwrotnego wywołania zwrotne</span><span class="sxs-lookup"><span data-stu-id="dbc38-139">Callbacks' return parameter</span></span>
<span data-ttu-id="dbc38-140">Poniżej przedstawiono kilka wskazówek, aby poprawnie obsługiwać parametr zwrotny `onDataPushStringReceived` i `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="dbc38-140">Here are some guidelines to properly handle the return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="dbc38-141">Odbiornik emisji powinien zwrócić `null` podczas wywołania zwrotnego, jeśli nie może określić sposób obsługi wypychanie danych.</span><span class="sxs-lookup"><span data-stu-id="dbc38-141">A broadcast receiver should return `null` in the callback if it does not know how to handle a data push.</span></span> <span data-ttu-id="dbc38-142">Aby ustalić, czy odbiornik emisji powinna obsługiwać wypychanie danych lub nie należy używać tej kategorii.</span><span class="sxs-lookup"><span data-stu-id="dbc38-142">You should use the category to determine whether your broadcast receiver should handle the data push or not.</span></span>
* <span data-ttu-id="dbc38-143">Jeden odbiornik emisji powinien zwrócić `true` podczas wywołania zwrotnego, jeśli akceptuje wypychanie danych.</span><span class="sxs-lookup"><span data-stu-id="dbc38-143">One of the broadcast receiver should return `true` in the callback if it accepts the data push.</span></span>
* <span data-ttu-id="dbc38-144">Jeden odbiornik emisji powinien zwrócić `false` podczas wywołania zwrotnego, jeśli rozpoznaje wypychania danych, ale odrzuca je niezależnie od przyczyn.</span><span class="sxs-lookup"><span data-stu-id="dbc38-144">One of the broadcast receiver should return `false` in the callback if it recognizes the data push, but discards it for whatever reason.</span></span> <span data-ttu-id="dbc38-145">Na przykład `false` po otrzymaniu danych jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="dbc38-145">For example, return `false` when the received data is invalid.</span></span>
* <span data-ttu-id="dbc38-146">Jeśli emituje jeden odbiornik zwraca `true` podczas drugiego zwraca jedną `false` do tego samego wypychania danych, jest niezdefiniowane zachowanie, nigdy nie należy to zrobić.</span><span class="sxs-lookup"><span data-stu-id="dbc38-146">If one broadcast receiver returns `true` while another one returns `false` for the same data push, the behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="dbc38-147">Zwracany typ jest używany tylko dla statystyki zasięgu:</span><span class="sxs-lookup"><span data-stu-id="dbc38-147">The return type is used only for the Reach statistics:</span></span>

* <span data-ttu-id="dbc38-148">`Replied`jest zwiększany, jeśli jeden z odbiorców emisji albo zwrócony `true` lub `false`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-148">`Replied` is incremented if one of the broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="dbc38-149">`Actioned`zwiększany jest tylko wtedy, gdy jeden z odbiorców emisji zwrócił `true`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-149">`Actioned` is incremented only if one of the broadcast receivers returned `true`.</span></span>

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="dbc38-150">Dostosowywanie kampanii</span><span class="sxs-lookup"><span data-stu-id="dbc38-150">How to customize campaigns</span></span>
<span data-ttu-id="dbc38-151">Aby dostosować kampanii, można zmodyfikować układy określone w zestawie SDK Reach.</span><span class="sxs-lookup"><span data-stu-id="dbc38-151">To customize campaigns, you can modify the layouts provided in the Reach SDK.</span></span>

<span data-ttu-id="dbc38-152">Należy zachować wszystkie identyfikatory, które są używane w układów i Zachowaj typy widoków, korzystających z identyfikatorem, szczególnie w przypadku widoków tekstu i obrazów.</span><span class="sxs-lookup"><span data-stu-id="dbc38-152">You should keep all the identifiers used in the layouts and keep the types of the views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="dbc38-153">Niektóre widoki właśnie są używane do ukrywania lub pokazywania obszarów, aby ich typ może być zmieniony.</span><span class="sxs-lookup"><span data-stu-id="dbc38-153">Some views are just used to hide or show areas so their type may be changed.</span></span> <span data-ttu-id="dbc38-154">Sprawdź kod źródłowy, jeśli chcesz zmienić typ widoku w podanych układów.</span><span class="sxs-lookup"><span data-stu-id="dbc38-154">Please check the source code if you intend to change the type of a view in the provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="dbc38-155">Powiadomienia</span><span class="sxs-lookup"><span data-stu-id="dbc38-155">Notifications</span></span>
<span data-ttu-id="dbc38-156">Istnieją dwa typy powiadomień: powiadomień systemu i w aplikacji, które pliki inny układ.</span><span class="sxs-lookup"><span data-stu-id="dbc38-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="dbc38-157">System powiadomień</span><span class="sxs-lookup"><span data-stu-id="dbc38-157">System notifications</span></span>
<span data-ttu-id="dbc38-158">Aby dostosować powiadomień systemowych, należy użyć **kategorii**.</span><span class="sxs-lookup"><span data-stu-id="dbc38-158">To customize system notifications you need to use the **categories**.</span></span> <span data-ttu-id="dbc38-159">Można przejść do [kategorii](#categories).</span><span class="sxs-lookup"><span data-stu-id="dbc38-159">You can jump to [Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="dbc38-160">Powiadomienia w aplikacji</span><span class="sxs-lookup"><span data-stu-id="dbc38-160">In-app notifications</span></span>
<span data-ttu-id="dbc38-161">Domyślnie powiadomienia w aplikacji jest widok dynamicznie dodawane do bieżącego działania interfejsu użytkownika dzięki użyciu Android — metoda `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-161">By default, an in-app notification is a view that is dynamically added to the current activity user interface thanks to the Android method `addContentView()`.</span></span> <span data-ttu-id="dbc38-162">Jest to nakładce powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="dbc38-162">This is called a notification overlay.</span></span> <span data-ttu-id="dbc38-163">Nakładki powiadomienia są bardzo szybkiego integracji, ponieważ nie wymagają modyfikacji dowolny układ w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-163">Notification overlays are great for a fast integration because they do not require you to modify any layout in your application.</span></span>

<span data-ttu-id="dbc38-164">Aby zmodyfikować wygląd sieci nakładki powiadomień, wystarczy zmodyfikować plik `engagement_notification_area.xml` do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="dbc38-164">To modify the look of your notification overlays, you can simply modify the file `engagement_notification_area.xml` to your needs.</span></span>

> [!NOTE]
> <span data-ttu-id="dbc38-165">Plik `engagement_notification_overlay.xml` jest ten, który jest używany do tworzenia w nakładce powiadomienia, w tym plik `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-165">The file `engagement_notification_overlay.xml` is the one that is used to create a notification overlay, it includes the file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="dbc38-166">Można również dostosować do własnych potrzeb (np. dla obszaru powiadomień w nakładce rozmieszczania).</span><span class="sxs-lookup"><span data-stu-id="dbc38-166">You can also customize it to suit your needs (such as for positioning the notification area within the overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="dbc38-167">Obejmują układu powiadomienia w ramach działania układu</span><span class="sxs-lookup"><span data-stu-id="dbc38-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="dbc38-168">Nakładki są bardzo szybkiego integracji, ale można niewygodne lub mieć skutki uboczne w szczególnych przypadkach.</span><span class="sxs-lookup"><span data-stu-id="dbc38-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="dbc38-169">Można dostosować system nakładki na poziomie działania, co ułatwia zapobieganie efekty uboczne specjalnych działań.</span><span class="sxs-lookup"><span data-stu-id="dbc38-169">The overlay system can be customized at an activity level, making it easy to prevent side effects for special activities.</span></span>

<span data-ttu-id="dbc38-170">Można wybrać obejmują naszych układu powiadomień w układzie istniejących dzięki użyciu Android **obejmują** instrukcji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-170">You can decide to include our notification layout in your existing layout thanks to the Android **include** statement.</span></span> <span data-ttu-id="dbc38-171">Poniżej przedstawiono przykład zmodyfikowanych `ListActivity` układu zawierający tylko `ListView`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-171">The following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="dbc38-172">**Przed integracji usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="dbc38-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="dbc38-173">**Po integracji usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="dbc38-173">**After Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

<span data-ttu-id="dbc38-174">W tym przykładzie dodano kontenera nadrzędnego ponieważ układ oryginalny używany widok listy jako elementu najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="dbc38-174">In this example we added a parent container since the original layout used a list view as the top level element.</span></span> <span data-ttu-id="dbc38-175">Dodaliśmy również `android:layout_weight="1"` aby można było dodać widok poniżej skonfigurowany z widoku listy `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-175">We also added `android:layout_weight="1"` to be able to add a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="dbc38-176">Zestaw SDK Reach usługi Engagement automatycznie wykrywa, czy układ powiadomień jest dołączony do tego działania, a nie dodają nakładki dla tego działania.</span><span class="sxs-lookup"><span data-stu-id="dbc38-176">The Engagement Reach SDK automatically detects that the notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="dbc38-177">Jeśli używasz ListActivity w aplikacji widoczne nakładki Reach uniemożliwi reagowanie na już kliknięte elementy w widoku listy.</span><span class="sxs-lookup"><span data-stu-id="dbc38-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting to clicked items in the list view anymore.</span></span> <span data-ttu-id="dbc38-178">Jest to znany problem.</span><span class="sxs-lookup"><span data-stu-id="dbc38-178">This is a known issue.</span></span> <span data-ttu-id="dbc38-179">Aby obejść ten problem Sugerujemy można osadzić układu powiadomień w własne działania układ listy podobnie jak w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="dbc38-179">To work around this problem we suggest you to embed the notification layout in your own list activity layout like in the previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="dbc38-180">Wyłączanie aplikacji powiadomienia na działanie</span><span class="sxs-lookup"><span data-stu-id="dbc38-180">Disabling application notification per activity</span></span>
<span data-ttu-id="dbc38-181">Jeśli nie chcesz, aby nakładki ma zostać dodany do Twoich działaniach i układu powiadomienia nie zawiera własny układ, można wyłączyć nakładki dla tego działania w `AndroidManifest.xml` przez dodanie `meta-data` sekcji, takich jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="dbc38-181">If you don't want the overlay to be added to your activity, and if you don't include the notification layout in your own layout, you can disable the overlay for this activity in the `AndroidManifest.xml` by adding a `meta-data` section like in the following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="dbc38-182"><a name="categories"></a>Kategorie</span><span class="sxs-lookup"><span data-stu-id="dbc38-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="dbc38-183">Po zmodyfikowaniu podana układów możesz zmodyfikować wygląd wszystkich powiadomień.</span><span class="sxs-lookup"><span data-stu-id="dbc38-183">When you modify the provided layouts, you modify the look of all your notifications.</span></span> <span data-ttu-id="dbc38-184">Kategorie umożliwiają definiowanie różnych wygląda docelowej (prawdopodobnie zachowania) dla powiadomień.</span><span class="sxs-lookup"><span data-stu-id="dbc38-184">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="dbc38-185">Po utworzeniu kampanii Reach można określić kategorię.</span><span class="sxs-lookup"><span data-stu-id="dbc38-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="dbc38-186">Należy pamiętać, że kategorie pozwalają również dostosować anonsów i sond, opisane w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="dbc38-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="dbc38-187">Aby zarejestrować kategorii Obsługa powiadomienia, należy dodać wywołanie po zainicjowaniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-187">To register a category handler for your notifications, you need to add a call when the application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbc38-188">Przeczytaj ostrzeżenie o atrybucie android: proces \<android-sdk zaangażowania — proces\> w sposób integracji zaangażowania na temat Android przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="dbc38-188">Please read the warning about the android:process attribute \<android-sdk-engagement-process\> in the How to Integrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="dbc38-189">W poniższym przykładzie założono potwierdzonych poprzedniego ostrzeżenie i użyj klasy `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="dbc38-189">The following example assumes you acknowledged the previous warning and use a sub-class of `EngagementApplication`:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

<span data-ttu-id="dbc38-190">`MyNotifier` Obiektu jest implementacją obsługi kategorii powiadomień.</span><span class="sxs-lookup"><span data-stu-id="dbc38-190">The `MyNotifier` object is the implementation of the notification category handler.</span></span> <span data-ttu-id="dbc38-191">Jest implementacja klasy `EngagementNotifier` interfejsu lub klasy podrzędnej implementacji domyślnej: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-191">It is either an implementation of the `EngagementNotifier` interface or a sub class of the default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="dbc38-192">Należy pamiętać, że tego samego zgłaszający może obsługiwać kilka kategorii można je zarejestrować następująco:</span><span class="sxs-lookup"><span data-stu-id="dbc38-192">Note that the same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="dbc38-193">Aby zastąpić domyślną implementację kategorii, możesz zarejestrować implementacji takich jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="dbc38-193">To replace the default category implementation, you can register your implementation like in the following example:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

<span data-ttu-id="dbc38-194">Bieżącej kategorii używany w procedurze obsługi jest przekazywana jako parametr w większości metod można zastąpić w `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-194">The current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="dbc38-195">Jest przekazywany jako `String` parametru lub pośrednio w `EngagementReachContent` obiektu, który ma `getCategory()` metody.</span><span class="sxs-lookup"><span data-stu-id="dbc38-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="dbc38-196">Można zmienić większość procesu tworzenia powiadomień na ponowne definiowanie metod `EngagementDefaultNotifier`, do bardziej zaawansowanych dostosowania swobodnie zapoznaj się z dokumentacją techniczną i kod źródłowy.</span><span class="sxs-lookup"><span data-stu-id="dbc38-196">You can change most of the notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free to take a look at the technical documentation and at the source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="dbc38-197">Powiadomienia w aplikacji</span><span class="sxs-lookup"><span data-stu-id="dbc38-197">In-app notifications</span></span>
<span data-ttu-id="dbc38-198">Jeśli chcesz użyć alternatywnych układów dla określonej kategorii, można zaimplementować to jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="dbc38-198">If you just want to use alternate layouts for a specific category, you can implement this as in the following example:</span></span>

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

<span data-ttu-id="dbc38-199">**Przykład `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="dbc38-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="dbc38-200">Jak widać, identyfikator widoku nakładki jest inne niż standardowe.</span><span class="sxs-lookup"><span data-stu-id="dbc38-200">As you can see, the overlay view identifier is different than the standard one.</span></span> <span data-ttu-id="dbc38-201">Należy pamiętać, że każdego układu dla nakładki używany unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="dbc38-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="dbc38-202">**Przykład `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="dbc38-202">**Example of `my_notification_area.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

<span data-ttu-id="dbc38-203">Jak widać, innej niż standardowe jest identyfikator widoku obszaru powiadomień.</span><span class="sxs-lookup"><span data-stu-id="dbc38-203">As you can see, the notification area view identifier is different than the standard one.</span></span> <span data-ttu-id="dbc38-204">Należy pamiętać, że każdy układ używa unikatowego identyfikatora obszarów powiadomień.</span><span class="sxs-lookup"><span data-stu-id="dbc38-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="dbc38-205">Ten prosty przykład kategorii sprawia, że aplikacja (lub w aplikacji) powiadomienia wyświetlane w górnej części ekranu.</span><span class="sxs-lookup"><span data-stu-id="dbc38-205">This simple example of category makes application (or in-app) notifications displayed at the top of the screen.</span></span> <span data-ttu-id="dbc38-206">Nie został zmieniony standardowych identyfikatorów używane w obszarze powiadomień, się.</span><span class="sxs-lookup"><span data-stu-id="dbc38-206">We did not change the standard identifiers used in the notification area itself.</span></span>

<span data-ttu-id="dbc38-207">Jeśli chcesz zmienić, konieczne będzie ponownie zdefiniować `EngagementDefaultNotifier.prepareInAppArea` metody.</span><span class="sxs-lookup"><span data-stu-id="dbc38-207">If you want to change that, you have to redefine the `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="dbc38-208">Zaleca się znaleźć dokumentację techniczną i kod źródłowy `EngagementNotifier` i `EngagementDefaultNotifier` Jeśli chcesz to poziomu zaawansowanego dostosowania.</span><span class="sxs-lookup"><span data-stu-id="dbc38-208">It's recommended to look at the technical documentation and at the source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="dbc38-209">System powiadomień</span><span class="sxs-lookup"><span data-stu-id="dbc38-209">System notifications</span></span>
<span data-ttu-id="dbc38-210">Rozszerzając `EngagementDefaultNotifier`, można zastąpić `onNotificationPrepared` do zmiany powiadomienia, który został przygotowany przez domyślną implementację.</span><span class="sxs-lookup"><span data-stu-id="dbc38-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` to alter the notification that was prepared by the default implementation.</span></span>

<span data-ttu-id="dbc38-211">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="dbc38-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="dbc38-212">W tym przykładzie powoduje, że powiadomienie systemowe dla zawartości będzie wyświetlany jako zdarzenie uruchomione, gdy kategoria "stałe" jest używana.</span><span class="sxs-lookup"><span data-stu-id="dbc38-212">This example makes a system notification for a content being displayed as an ongoing event when the "ongoing" category is used.</span></span>

<span data-ttu-id="dbc38-213">Jeśli chcesz utworzyć `Notification` obiekt od początku, można powrócić `false` — metoda i wywołanie `notify` samodzielnie na `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-213">If you want to build the `Notification` object from scratch, you can return `false` to the method and call `notify` yourself on the `NotificationManager`.</span></span> <span data-ttu-id="dbc38-214">W takim przypadku należy pamiętać o jest `contentIntent`, `deleteIntent` i identyfikator powiadomienia, używany przez `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and the notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="dbc38-215">Oto przykład poprawnego takie implementacji:</span><span class="sxs-lookup"><span data-stu-id="dbc38-215">Here is a correct example of such an implementation:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice the call to get the right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="dbc38-216">Anonsów zawierających tylko powiadomienia</span><span class="sxs-lookup"><span data-stu-id="dbc38-216">Notification only announcements</span></span>
<span data-ttu-id="dbc38-217">Zarządzanie kliknięcie powiadomienia tylko anonsu można dostosowywać przez zastąpienie `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` do modyfikowania przygotowanej `Intent`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-217">The management of the click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` to modify the prepared `Intent`.</span></span> <span data-ttu-id="dbc38-218">Za pomocą tej metody pozwala łatwo dostosować flag.</span><span class="sxs-lookup"><span data-stu-id="dbc38-218">Using this method allows you to tune the flags easily.</span></span>

<span data-ttu-id="dbc38-219">Na przykład aby dodać `SINGLE_TOP` flagi:</span><span class="sxs-lookup"><span data-stu-id="dbc38-219">For example to add the `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="dbc38-220">W przypadku starszych zaangażowania użytkowników należy pamiętać, że powiadomień systemowych bez akcji URL teraz uruchamia aplikację jeśli było w tle, więc ta metoda może być wywołany z anonsu bez adres URL akcji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-220">For legacy Engagement users, please note that system notifications without action URL now launches the application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="dbc38-221">Które należy rozważyć w przypadku dostosowywania celem.</span><span class="sxs-lookup"><span data-stu-id="dbc38-221">You should consider that when customizing the intent.</span></span>

<span data-ttu-id="dbc38-222">Można też wdrożyć `EngagementNotifier.executeNotifAnnouncementAction` od początku.</span><span class="sxs-lookup"><span data-stu-id="dbc38-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="dbc38-223">Cykl życia powiadomień</span><span class="sxs-lookup"><span data-stu-id="dbc38-223">Notification life cycle</span></span>
<span data-ttu-id="dbc38-224">Podczas korzystania z domyślnej kategorii, w przypadku niektórych metod cyklu życia są nazywane na `EngagementReachInteractiveContent` obiektu do raportu statystyk i zaktualizować stan kampanii:</span><span class="sxs-lookup"><span data-stu-id="dbc38-224">When using the default category, some life cycle methods are called on the `EngagementReachInteractiveContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="dbc38-225">Jeśli powiadomienia są wyświetlane w aplikacji lub umieść w pasku stanu `displayNotification` metoda jest wywoływana (która statystyki) przez `EngagementReachAgent` Jeśli `handleNotification` zwraca `true`.</span><span class="sxs-lookup"><span data-stu-id="dbc38-225">When the notification is displayed in application or put in the status bar, the `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="dbc38-226">Jeśli powiadomienie jest odrzucane, `exitNotification` metoda jest wywoływana, statystyka jest zgłaszany i dalej kampanii teraz mogą być przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="dbc38-226">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="dbc38-227">Po kliknięciu powiadomienia `actionNotification` jest wywoływana, statystyka zostaje zgłoszone i skojarzone celem jest uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="dbc38-227">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated intent is launched.</span></span>

<span data-ttu-id="dbc38-228">Jeśli implementacji `EngagementNotifier` pomija domyślne zachowanie, należy wywołać metody te cyklu życia samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="dbc38-228">If your implementation of `EngagementNotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="dbc38-229">Poniższe przykłady przedstawiają w niektórych przypadkach, gdy pomijane jest domyślne zachowanie:</span><span class="sxs-lookup"><span data-stu-id="dbc38-229">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="dbc38-230">Nie można rozszerzyć `EngagementDefaultNotifier`, np. zaimplementowano obsługi kategorii od początku.</span><span class="sxs-lookup"><span data-stu-id="dbc38-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="dbc38-231">Dla powiadomień systemowych overrode `onNotificationPrepared` i możesz zmodyfikować `contentIntent` lub `deleteIntent` w `Notification` obiektu.</span><span class="sxs-lookup"><span data-stu-id="dbc38-231">For system notifications, you overrode the `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in the `Notification` object.</span></span>
* <span data-ttu-id="dbc38-232">Aby powiadomienia w aplikacji, overrode `prepareInAppArea`, należy zamapować co najmniej `actionNotification` do jednego z U.I kontrolki.</span><span class="sxs-lookup"><span data-stu-id="dbc38-232">For in-app notifications, you overrode `prepareInAppArea`, be sure to map at least `actionNotification` to one of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="dbc38-233">Jeśli `handleNotification` zgłasza wyjątek, zawartość zostanie usunięta i `dropContent` jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="dbc38-233">If `handleNotification` throws an exception, the content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="dbc38-234">Jest to raportowane w statystykach i dalej kampanii teraz mogą być przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="dbc38-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="dbc38-235">Anonsów i sond</span><span class="sxs-lookup"><span data-stu-id="dbc38-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="dbc38-236">Układy</span><span class="sxs-lookup"><span data-stu-id="dbc38-236">Layouts</span></span>
<span data-ttu-id="dbc38-237">Można zmodyfikować `engagement_text_announcement.xml`, `engagement_web_announcement.xml` i `engagement_poll.xml` pliki, aby dostosować tekst anonsów, web anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="dbc38-237">You can modify the `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files to customize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="dbc38-238">Te pliki mają dwóch typowych układów obszar tytułu i obszar przycisku.</span><span class="sxs-lookup"><span data-stu-id="dbc38-238">These files share two common layouts for the title area and the button area.</span></span> <span data-ttu-id="dbc38-239">Układ tytułu jest `engagement_content_title.xml` i używa gromadzący pliku obiektów drawable tła.</span><span class="sxs-lookup"><span data-stu-id="dbc38-239">The layout for the title is `engagement_content_title.xml` and uses the eponymous drawable file for the background.</span></span> <span data-ttu-id="dbc38-240">Układ przycisków akcji i wyjścia jest `engagement_button_bar.xml` i używa gromadzący pliku obiektów drawable tła.</span><span class="sxs-lookup"><span data-stu-id="dbc38-240">The layout for the action and exit buttons is `engagement_button_bar.xml` and uses the eponymous drawable file for the background.</span></span>

<span data-ttu-id="dbc38-241">W sondowania, układ pytanie i ich możliwości są dynamicznie zwiększony przy użyciu kilka razy `engagement_question.xml` pliku układu dla pytań i `engagement_choice.xml` pliku dla opcji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-241">In a poll, the question layout and their choices are dynamically inflated using several times the `engagement_question.xml` layout file for the questions and the `engagement_choice.xml` file for the choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="dbc38-242">Kategorie</span><span class="sxs-lookup"><span data-stu-id="dbc38-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="dbc38-243">Układy alternatywnej</span><span class="sxs-lookup"><span data-stu-id="dbc38-243">Alternate layouts</span></span>
<span data-ttu-id="dbc38-244">Takich jak powiadomienia Kategoria kampanii można mieć alternatywne układy anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="dbc38-244">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="dbc38-245">Na przykład, aby utworzyć kategorii ogłoszenie tekstu, można rozszerzyć `EngagementTextAnnouncementActivity` i odwołaj `AndroidManifest.xml` pliku:</span><span class="sxs-lookup"><span data-stu-id="dbc38-245">For example, to create a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it the `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="dbc38-246">Należy pamiętać, że kategorii w filtrze konwersji umożliwia różnica w stosunku do domyślne działanie anonsu.</span><span class="sxs-lookup"><span data-stu-id="dbc38-246">Note that the category in the intent filter is used to make the difference with the default announcement activity.</span></span>

<span data-ttu-id="dbc38-247">SDK osiągnąć używa konwersji system do rozpoznania odpowiednim działaniu dla określonej kategorii i go powraca na domyślnej kategorii Jeśli niepowodzenie rozpoznawania.</span><span class="sxs-lookup"><span data-stu-id="dbc38-247">The Reach SDK uses the intent system to resolve the right activity for a specific category and it falls back on the default category if the resolution failed.</span></span>

<span data-ttu-id="dbc38-248">Musisz zaimplementować `MyCustomTextAnnouncementActivity`, jeśli chcesz zmienić układ (, zachowując tego samego identyfikatory widok), wystarczy zdefiniować klasy, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="dbc38-248">Then you have to implement `MyCustomTextAnnouncementActivity`, if you just want to change the layout (but keep the same view identifiers), you just have to define the class like in the following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class to use R.layout.my_text_announcement
              }
            }

<span data-ttu-id="dbc38-249">Aby zastąpić kategorii domyślny tekst anonsów, po prostu zastąpić `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` przy implementacji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-249">To replace the default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="dbc38-250">W podobny sposób można dostosować Web anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="dbc38-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="dbc38-251">W przypadku anonsów zawierających sieci web można rozszerzyć `EngagementWebAnnouncementActivity` ani deklarować Twoich działaniach w `AndroidManifest.xml` , takich jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="dbc38-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in the intent is the data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="dbc38-252">Ankiety można rozszerzyć `EngagementPollActivity` ani deklarować sieci w `AndroidManifest.xml` , takich jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="dbc38-252">For polls you can extend `EngagementPollActivity` and declare your in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="dbc38-253">Implementacja od podstaw</span><span class="sxs-lookup"><span data-stu-id="dbc38-253">Implementation from scratch</span></span>
<span data-ttu-id="dbc38-254">Można zaimplementować kategorie działań anonsu (i sondowania) bez rozszerzenie jednej z `Engagement*Activity` klasy udostępniane przez zestaw SDK Reach.</span><span class="sxs-lookup"><span data-stu-id="dbc38-254">You can implement categories for your announcement (and poll) activities without extending one of the `Engagement*Activity` classes provided by the Reach SDK.</span></span> <span data-ttu-id="dbc38-255">Jest to przydatne na przykład jeśli chcesz zdefiniować układu, który nie używa tego samego widoków jako standardowych układów.</span><span class="sxs-lookup"><span data-stu-id="dbc38-255">This is useful for example if you want to define a layout that does not use the same views as the standard layouts.</span></span>

<span data-ttu-id="dbc38-256">Podobnie jak dostosowywania powiadomień zaawansowane zalecane jest aby przyjrzeć się kodu źródłowego standardowej implementacji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-256">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

<span data-ttu-id="dbc38-257">Poniżej przedstawiono niektóre czynności, które należy wziąć pod uwagę: Reach spowoduje uruchomienie działania o określonych zamiar (odpowiadający filtru konwersji) oraz dodatkowy parametr, który jest identyfikatorem zawartości.</span><span class="sxs-lookup"><span data-stu-id="dbc38-257">Here are some things to keep in mind: Reach will launch the activity with a specific intent (corresponding to the intent filter) plus an extra parameter which is the content identifier.</span></span>

<span data-ttu-id="dbc38-258">Można pobrać zawartości obiektu, który zawiera pola, które można określić podczas tworzenia kampanii w witrynie sieci web można to zrobić:</span><span class="sxs-lookup"><span data-stu-id="dbc38-258">To retrieve the content object which contain the fields you specified when creating the campaign on the web site you can do this:</span></span>

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

<span data-ttu-id="dbc38-259">Statystyki, zgłoś zawartość jest wyświetlana w `onResume` zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="dbc38-259">For statistics, you should report the content is displayed in the `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark the content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="dbc38-260">Następnie, nie zapomnij wywołań albo `actionContent(this)` lub `exitContent(this)` zawartości obiektu przed działanie przechodzi w tle.</span><span class="sxs-lookup"><span data-stu-id="dbc38-260">Then, don't forget to call either `actionContent(this)` or `exitContent(this)` on the content object before the activity goes into background.</span></span>

<span data-ttu-id="dbc38-261">Nie można wywołać albo `actionContent` lub `exitContent`, statystyki nie zostaną wysłane (tzn. nie analytics kampanii) i co ważniejsze, dalej kampanii nie będzie powiadamiany, aż do ponownego uruchomienia procesu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on the campaign) and more importantly, the next campaigns will not be notified until the application process is restarted.</span></span>

<span data-ttu-id="dbc38-262">Orientacja lub innych zmian konfiguracji może wykonać kod trudnych do określenia, czy działanie przechodzi w tle lub nie, standardowej implementacji upewnia się, zawartość jest zgłaszana jako zakończony, gdy użytkownik opuści działania (albo przez naciśnięcie przycisku `HOME`lub `BACK`), ale nie w przypadku zmiany orientacji.</span><span class="sxs-lookup"><span data-stu-id="dbc38-262">Orientation or other configuration changes can make the code tricky to determine whether the activity goes into background or not, the standard implementation makes sure the content is reported as exited if the user leaves the activity (either by pressing `HOME` or `BACK`) but not if the orientation changes.</span></span>

<span data-ttu-id="dbc38-263">Oto interesujące część implementacji:</span><span class="sxs-lookup"><span data-stu-id="dbc38-263">Here is the interesting part of the implementation:</span></span>

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have to check anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="dbc38-264">Jak widać, jeśli wywołujesz `actionContent(this)` zakończyła działanie, a następnie `exitContent(this)` można bezpiecznie wywołać bez żadnego efektu.</span><span class="sxs-lookup"><span data-stu-id="dbc38-264">As you can see, if you called `actionContent(this)` then finished the activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
<span data-ttu-id="dbc38-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span><span class="sxs-lookup"><span data-stu-id="dbc38-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span></span>
<span data-ttu-id="dbc38-266">[usługi Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span><span class="sxs-lookup"><span data-stu-id="dbc38-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span></span>
