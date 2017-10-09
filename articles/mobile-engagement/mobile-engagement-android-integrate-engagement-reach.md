---
title: aaaAzure Mobile Engagement Android SDK integracji
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
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a><span data-ttu-id="3c660-103">W jaki sposób Reach usługi Engagement tooIntegrate w systemie Android</span><span class="sxs-lookup"><span data-stu-id="3c660-103">How tooIntegrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3c660-104">Musisz wykonać procedurę integracji hello opisanego w hello jak tooIntegrate zaangażowania w systemie Android dokumentu przed wykonaniem tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="3c660-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="3c660-105">Standardowa integracji</span><span class="sxs-lookup"><span data-stu-id="3c660-105">Standard integration</span></span>

<span data-ttu-id="3c660-106">Skopiuj pliki zasobów Reach z hello zestawu SDK w projekcie:</span><span class="sxs-lookup"><span data-stu-id="3c660-106">Copy Reach resource files from hello SDK in your project :</span></span>

* <span data-ttu-id="3c660-107">Skopiuj pliki hello z hello `res/layout` folderu oferowane przez hello zestawu SDK do hello `res/layout` folderu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c660-107">Copy hello files from hello `res/layout` folder delivered with hello SDK into hello `res/layout` folder of your application.</span></span>
* <span data-ttu-id="3c660-108">Skopiuj pliki hello z hello `res/drawable` folderu oferowane przez hello zestawu SDK do hello `res/drawable` folderu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c660-108">Copy hello files from hello `res/drawable` folder delivered with hello SDK into hello `res/drawable` folder of your application.</span></span>

<span data-ttu-id="3c660-109">Edytowanie użytkownika `AndroidManifest.xml` pliku:</span><span class="sxs-lookup"><span data-stu-id="3c660-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="3c660-110">Dodaj następujące sekcji hello (między hello `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="3c660-110">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
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
* <span data-ttu-id="3c660-111">Należy to uprawnienie tooreplay systemu powiadomień, które nie zostały kliknięty przy rozruchu (w przeciwnym razie będą znajdować się na dysku, ale nie będą już wyświetlane, naprawdę masz tooinclude to).</span><span class="sxs-lookup"><span data-stu-id="3c660-111">You need this permission tooreplay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have tooinclude this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="3c660-112">Określanie ikony używany do powiadomień, (zarówno w aplikacji oraz systemowe z nich) przez kopiowanie i edytowania powitania po sekcji (między hello `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="3c660-112">Specify an icon used for notifications (both in app and system ones) by copying and editing hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="3c660-113">Ta sekcja ma **obowiązkowe** Jeśli planujesz używanie powiadomień systemowych, tworząc kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="3c660-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="3c660-114">Android uniemożliwia powiadomień systemowych bez ikony wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="3c660-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="3c660-115">Dlatego w przypadku pominięcia tej sekcji, użytkownicy końcowi nie będą mogli tooreceive je.</span><span class="sxs-lookup"><span data-stu-id="3c660-115">So if you omit this section, your end users will not be able tooreceive them.</span></span>
> 
> 

* <span data-ttu-id="3c660-116">Po utworzeniu kampanii z powiadomień systemowych przy użyciu szerszej należy hello tooadd następujących uprawnień (po hello `</application>` tagu) Jeśli brak:</span><span class="sxs-lookup"><span data-stu-id="3c660-116">If you create campaigns with system notifications using big picture, you need tooadd hello following permissions (after hello `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="3c660-117">W systemie Android M i czy aplikacja korzysta poziom interfejsu API systemu Android 23 lub większą ``WRITE_EXTERNAL_STORAGE`` uprawnienia wymaga zatwierdzenia przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3c660-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="3c660-118">Przeczytaj [w tej sekcji](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="3c660-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="3c660-119">Dla powiadomień systemowych, które można również określić hello osiągnięto kampanii, jeśli urządzenie hello pierścienia i/lub należy też.</span><span class="sxs-lookup"><span data-stu-id="3c660-119">For system notifications you can also specify in hello Reach campaign if hello device should ring and/or vibrate.</span></span> <span data-ttu-id="3c660-120">Dla niego toowork, masz toomake się zadeklarowany hello następujące uprawnienia (po hello `</application>` tagu):</span><span class="sxs-lookup"><span data-stu-id="3c660-120">For it toowork, you have toomake sure you declared hello following permission (after hello `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="3c660-121">Bez tego uprawnienia Android uniemożliwia powiadomienia systemowe z jest pokazywany, gdy zaznaczono pierścień hello lub hello też opcji w Menedżerze osiągnąć kampanii hello.</span><span class="sxs-lookup"><span data-stu-id="3c660-121">Without this permission, Android prevents system notifications from being shown if you checked hello ring or hello vibrate option in hello Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="3c660-122">Natywnych powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="3c660-122">Native Push</span></span>
<span data-ttu-id="3c660-123">Teraz możesz skonfigurować moduł Reach, należy tooconfigure natywnych powiadomień wypychanych toobe tooreceive stanie hello kampanii na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="3c660-123">Now that you configured Reach module, you need tooconfigure native push toobe able tooreceive hello campaigns on hello device.</span></span>

<span data-ttu-id="3c660-124">W systemie Android firma Microsoft obsługuje dwie usługi:</span><span class="sxs-lookup"><span data-stu-id="3c660-124">We support two services on Android:</span></span>

* <span data-ttu-id="3c660-125">Urządzenia ze sklepu Google Play: Użyj [Google Cloud Messaging] przez następujące hello [jak GCM z Engagement tooIntegrate przewodnik](mobile-engagement-android-gcm-integrate.md) przewodnik.</span><span class="sxs-lookup"><span data-stu-id="3c660-125">Google Play devices: Use [Google Cloud Messaging] by following hello [How tooIntegrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="3c660-126">Urządzenia firmy Amazon: Użyj [usługi Amazon Device Messaging] przez następujące hello [jak przewodnik tooIntegrate ADM z Engagement](mobile-engagement-android-adm-integrate.md) przewodnik.</span><span class="sxs-lookup"><span data-stu-id="3c660-126">Amazon devices: Use [Amazon Device Messaging] by following hello [How tooIntegrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="3c660-127">Jeśli chcesz, aby tootarget zarówno Amazon, jak i sklepu Google Play urządzenia, jego możliwe toohave cała jego zawartość 1 AndroidManifest.xml/APK do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c660-127">If you want tootarget both Amazon and Google Play devices, its possible toohave everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="3c660-128">Jednak podczas przesyłania tooAmazon, mogą one odrzucić aplikacji, jeśli znajduje się kod usługi GCM.</span><span class="sxs-lookup"><span data-stu-id="3c660-128">But when submitting tooAmazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="3c660-129">W takim przypadku należy używać wielu APKs.</span><span class="sxs-lookup"><span data-stu-id="3c660-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="3c660-130">**Aplikacja jest teraz gotowy tooreceive i wyświetlanie osiągnąć kampanii!**</span><span class="sxs-lookup"><span data-stu-id="3c660-130">**Your application is now ready tooreceive and display reach campaigns!**</span></span>

## <a name="how-toohandle-data-push"></a><span data-ttu-id="3c660-131">Jak wypychania danych toohandle</span><span class="sxs-lookup"><span data-stu-id="3c660-131">How toohandle data push</span></span>
### <a name="integration"></a><span data-ttu-id="3c660-132">Integracja</span><span class="sxs-lookup"><span data-stu-id="3c660-132">Integration</span></span>
<span data-ttu-id="3c660-133">Jeśli chcesz toobe Twojej aplikacji może wypchnięcia tooreceive Reach danych, masz toocreate podklasą klasy `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` i odwoływać w hello `AndroidManifest.xml` pliku (między hello `<application>` i/lub `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="3c660-133">If you want your application toobe able tooreceive Reach data pushes, you have toocreate a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in hello `AndroidManifest.xml` file (between hello `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="3c660-134">Następnie można zastąpić hello `onDataPushStringReceived` i `onDataPushBase64Received` wywołań zwrotnych.</span><span class="sxs-lookup"><span data-stu-id="3c660-134">Then you can override hello `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="3c660-135">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="3c660-135">Here is an example:</span></span>

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

### <a name="category"></a><span data-ttu-id="3c660-136">Kategoria</span><span class="sxs-lookup"><span data-stu-id="3c660-136">Category</span></span>
<span data-ttu-id="3c660-137">Witaj kategorii parametr jest opcjonalny, podczas tworzenia kampanii wypychania danych i umożliwia wypychanie danych toofilter.</span><span class="sxs-lookup"><span data-stu-id="3c660-137">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="3c660-138">Jest to przydatne, jeśli masz wiele odbiorników emisji obsługi różnych typów wypychania danych, lub jeśli użytkownik chce różnych rodzajów toopush z `Base64` tooidentify danych i chcesz ich typu przed ich analizowania.</span><span class="sxs-lookup"><span data-stu-id="3c660-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="3c660-139">Parametr zwrotnego wywołania zwrotne</span><span class="sxs-lookup"><span data-stu-id="3c660-139">Callbacks' return parameter</span></span>
<span data-ttu-id="3c660-140">Poniżej przedstawiono niektóre wytyczne tooproperly dojście hello parametr zwrotny `onDataPushStringReceived` i `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="3c660-140">Here are some guidelines tooproperly handle hello return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="3c660-141">Odbiornik emisji powinien zwrócić `null` w hello wywołania zwrotnego, jeśli nie wiadomo, jak push toohandle danych.</span><span class="sxs-lookup"><span data-stu-id="3c660-141">A broadcast receiver should return `null` in hello callback if it does not know how toohandle a data push.</span></span> <span data-ttu-id="3c660-142">Należy używać hello toodetermine kategorii, czy odbiornik emisji powinna obsługiwać wypychanie danych hello, lub nie.</span><span class="sxs-lookup"><span data-stu-id="3c660-142">You should use hello category toodetermine whether your broadcast receiver should handle hello data push or not.</span></span>
* <span data-ttu-id="3c660-143">Jeden odbiornik emisji hello powinien zwrócić `true` w hello wywołania zwrotnego, jeśli akceptuje hello wypychanie danych.</span><span class="sxs-lookup"><span data-stu-id="3c660-143">One of hello broadcast receiver should return `true` in hello callback if it accepts hello data push.</span></span>
* <span data-ttu-id="3c660-144">Jeden odbiornik emisji hello powinien zwrócić `false` w hello wywołania zwrotnego, jeśli rozpoznaje hello wypychanie danych, ale odrzuca je z jakiegoś powodu.</span><span class="sxs-lookup"><span data-stu-id="3c660-144">One of hello broadcast receiver should return `false` in hello callback if it recognizes hello data push, but discards it for whatever reason.</span></span> <span data-ttu-id="3c660-145">Na przykład `false` po hello odebrane dane są nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="3c660-145">For example, return `false` when hello received data is invalid.</span></span>
* <span data-ttu-id="3c660-146">Jeśli emituje jeden odbiornik zwraca `true` podczas drugiego zwraca jedną `false` hello wypychanie danych sam, zachowanie hello jest niezdefiniowana, nigdy nie należy który.</span><span class="sxs-lookup"><span data-stu-id="3c660-146">If one broadcast receiver returns `true` while another one returns `false` for hello same data push, hello behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="3c660-147">Typ zwracany Hello jest używany tylko dla hello Reach statystyki:</span><span class="sxs-lookup"><span data-stu-id="3c660-147">hello return type is used only for hello Reach statistics:</span></span>

* <span data-ttu-id="3c660-148">`Replied`jest zwiększany, jeśli jeden z odbiorców emisji hello albo zwrócony `true` lub `false`.</span><span class="sxs-lookup"><span data-stu-id="3c660-148">`Replied` is incremented if one of hello broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="3c660-149">`Actioned`zwiększany jest tylko wtedy, gdy jeden hello emisji odbiorniki zwrócił `true`.</span><span class="sxs-lookup"><span data-stu-id="3c660-149">`Actioned` is incremented only if one of hello broadcast receivers returned `true`.</span></span>

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="3c660-150">Jak toocustomize kampanii</span><span class="sxs-lookup"><span data-stu-id="3c660-150">How toocustomize campaigns</span></span>
<span data-ttu-id="3c660-151">toocustomize kampanie, można zmodyfikować układów hello w hello osiągnąć zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="3c660-151">toocustomize campaigns, you can modify hello layouts provided in hello Reach SDK.</span></span>

<span data-ttu-id="3c660-152">Należy zachować wszystkie identyfikatory hello używane w układów hello i Zachowaj hello typy widoków hello, korzystających z identyfikatorem, szczególnie w przypadku widoków tekstu i obrazów.</span><span class="sxs-lookup"><span data-stu-id="3c660-152">You should keep all hello identifiers used in hello layouts and keep hello types of hello views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="3c660-153">Niektóre widoki są używane tylko toohide lub Pokaż obszary, więc ich typ może być zmieniony.</span><span class="sxs-lookup"><span data-stu-id="3c660-153">Some views are just used toohide or show areas so their type may be changed.</span></span> <span data-ttu-id="3c660-154">Sprawdź, czy kod źródłowy hello zamierzając toochange hello typ widoku w hello podane układów.</span><span class="sxs-lookup"><span data-stu-id="3c660-154">Please check hello source code if you intend toochange hello type of a view in hello provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="3c660-155">Powiadomienia</span><span class="sxs-lookup"><span data-stu-id="3c660-155">Notifications</span></span>
<span data-ttu-id="3c660-156">Istnieją dwa typy powiadomień: powiadomień systemu i w aplikacji, które pliki inny układ.</span><span class="sxs-lookup"><span data-stu-id="3c660-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="3c660-157">System powiadomień</span><span class="sxs-lookup"><span data-stu-id="3c660-157">System notifications</span></span>
<span data-ttu-id="3c660-158">należy toouse hello powiadomień systemowych toocustomize **kategorii**.</span><span class="sxs-lookup"><span data-stu-id="3c660-158">toocustomize system notifications you need toouse hello **categories**.</span></span> <span data-ttu-id="3c660-159">Można przejść za[kategorii](#categories).</span><span class="sxs-lookup"><span data-stu-id="3c660-159">You can jump too[Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="3c660-160">Powiadomienia w aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c660-160">In-app notifications</span></span>
<span data-ttu-id="3c660-161">Domyślnie powiadomienia w aplikacji jest widoku, który jest dodawane dynamicznie toohello bieżącego działania użytkownika dzięki toohello Android metody interfejsu `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="3c660-161">By default, an in-app notification is a view that is dynamically added toohello current activity user interface thanks toohello Android method `addContentView()`.</span></span> <span data-ttu-id="3c660-162">Jest to nakładce powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="3c660-162">This is called a notification overlay.</span></span> <span data-ttu-id="3c660-163">Nakładki powiadomienia są bardzo szybkiego integracji, ponieważ nie wymagają toomodify można dowolny układ w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c660-163">Notification overlays are great for a fast integration because they do not require you toomodify any layout in your application.</span></span>

<span data-ttu-id="3c660-164">wygląd hello toomodify Twojego nakładki powiadomień, wystarczy zmodyfikować plik hello `engagement_notification_area.xml` musi tooyour.</span><span class="sxs-lookup"><span data-stu-id="3c660-164">toomodify hello look of your notification overlays, you can simply modify hello file `engagement_notification_area.xml` tooyour needs.</span></span>

> [!NOTE]
> <span data-ttu-id="3c660-165">Plik Hello `engagement_notification_overlay.xml` jest hello jest używany toocreate w nakładce powiadomienia hello plik `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="3c660-165">hello file `engagement_notification_overlay.xml` is hello one that is used toocreate a notification overlay, it includes hello file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="3c660-166">Można również dostosować go toosuit potrzeb (np. dla obszaru powiadomień hello w nakładce hello rozmieszczania).</span><span class="sxs-lookup"><span data-stu-id="3c660-166">You can also customize it toosuit your needs (such as for positioning hello notification area within hello overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="3c660-167">Obejmują układu powiadomienia w ramach działania układu</span><span class="sxs-lookup"><span data-stu-id="3c660-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="3c660-168">Nakładki są bardzo szybkiego integracji, ale można niewygodne lub mieć skutki uboczne w szczególnych przypadkach.</span><span class="sxs-lookup"><span data-stu-id="3c660-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="3c660-169">można dostosować system nakładki Hello na poziomie działania, dzięki czemu można łatwo tooprevent efekty uboczne specjalnych działań.</span><span class="sxs-lookup"><span data-stu-id="3c660-169">hello overlay system can be customized at an activity level, making it easy tooprevent side effects for special activities.</span></span>

<span data-ttu-id="3c660-170">Można określić tooinclude naszych układu powiadomień w Twoje istniejące toohello Dziękujemy układu Android **obejmują** instrukcji.</span><span class="sxs-lookup"><span data-stu-id="3c660-170">You can decide tooinclude our notification layout in your existing layout thanks toohello Android **include** statement.</span></span> <span data-ttu-id="3c660-171">Witaj poniżej przedstawiono przykład zmodyfikowanych `ListActivity` układu zawierający tylko `ListView`.</span><span class="sxs-lookup"><span data-stu-id="3c660-171">hello following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="3c660-172">**Przed integracji usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="3c660-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="3c660-173">**Po integracji usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="3c660-173">**After Engagement integration :**</span></span>

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

<span data-ttu-id="3c660-174">W tym przykładzie dodano kontenera nadrzędnego ponieważ układ oryginalny hello stanowiły hello najwyższego poziomu elementu widoku listy.</span><span class="sxs-lookup"><span data-stu-id="3c660-174">In this example we added a parent container since hello original layout used a list view as hello top level element.</span></span> <span data-ttu-id="3c660-175">Dodaliśmy również `android:layout_weight="1"` toobe tooadd stanie skonfigurowano poniżej widoku listy widok `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="3c660-175">We also added `android:layout_weight="1"` toobe able tooadd a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="3c660-176">zestaw SDK Reach usługi Engagement Hello automatycznie wykrywa taki układ powiadomień hello jest dołączony do tego działania, a nie dodają nakładki dla tego działania.</span><span class="sxs-lookup"><span data-stu-id="3c660-176">hello Engagement Reach SDK automatically detects that hello notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="3c660-177">Jeśli używasz ListActivity w aplikacji widoczne nakładki Reach uniemożliwi dające dodatnią reakcję tooclicked elementów w widoku listy hello już.</span><span class="sxs-lookup"><span data-stu-id="3c660-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting tooclicked items in hello list view anymore.</span></span> <span data-ttu-id="3c660-178">Jest to znany problem.</span><span class="sxs-lookup"><span data-stu-id="3c660-178">This is a known issue.</span></span> <span data-ttu-id="3c660-179">toowork tego problemu zaleca się możesz tooembed hello powiadomień układ własne działania układ listy podobnie jak w poprzednim przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="3c660-179">toowork around this problem we suggest you tooembed hello notification layout in your own list activity layout like in hello previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="3c660-180">Wyłączanie aplikacji powiadomienia na działanie</span><span class="sxs-lookup"><span data-stu-id="3c660-180">Disabling application notification per activity</span></span>
<span data-ttu-id="3c660-181">Jeśli nie chcesz hello toobe nakładki dodać działanie tooyour i układu powiadomień hello nie zawiera własny układ, można wyłączyć hello nakładki dla tego działania w hello `AndroidManifest.xml` przez dodanie `meta-data` sekcji, takich jak w następujących hello przykład:</span><span class="sxs-lookup"><span data-stu-id="3c660-181">If you don't want hello overlay toobe added tooyour activity, and if you don't include hello notification layout in your own layout, you can disable hello overlay for this activity in hello `AndroidManifest.xml` by adding a `meta-data` section like in hello following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="3c660-182"><a name="categories"></a>Kategorie</span><span class="sxs-lookup"><span data-stu-id="3c660-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="3c660-183">Po zmodyfikowaniu hello podane układów możesz zmodyfikować wygląd hello wszystkich powiadomień.</span><span class="sxs-lookup"><span data-stu-id="3c660-183">When you modify hello provided layouts, you modify hello look of all your notifications.</span></span> <span data-ttu-id="3c660-184">Kategorie dopuszczać toodefine możesz przez różne docelowe szuka powiadomienia (prawdopodobnie zachowania).</span><span class="sxs-lookup"><span data-stu-id="3c660-184">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="3c660-185">Po utworzeniu kampanii Reach można określić kategorię.</span><span class="sxs-lookup"><span data-stu-id="3c660-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="3c660-186">Należy pamiętać, że kategorie pozwalają również dostosować anonsów i sond, opisane w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="3c660-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="3c660-187">tooregister kategorii Obsługa powiadomienia, należy tooadd wywołania po zainicjowaniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3c660-187">tooregister a category handler for your notifications, you need tooadd a call when hello application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c660-188">Przeczytaj hello ostrzeżenie dotyczące atrybutu android: proces hello \<android-sdk zaangażowania — proces\> w hello jak tooIntegrate zaangażowania na temat Android przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="3c660-188">Please read hello warning about hello android:process attribute \<android-sdk-engagement-process\> in hello How tooIntegrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="3c660-189">Witaj poniższym przykładzie założono potwierdzonych poprzedniego ostrzeżenie hello i użyj klasy `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="3c660-189">hello following example assumes you acknowledged hello previous warning and use a sub-class of `EngagementApplication`:</span></span>

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

<span data-ttu-id="3c660-190">Witaj `MyNotifier` obiektu jest implementacją hello hello powiadomień kategorii obsługi.</span><span class="sxs-lookup"><span data-stu-id="3c660-190">hello `MyNotifier` object is hello implementation of hello notification category handler.</span></span> <span data-ttu-id="3c660-191">Jest implementacja klasy hello `EngagementNotifier` interfejsu lub klasy podrzędnej implementacji domyślnej hello: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="3c660-191">It is either an implementation of hello `EngagementNotifier` interface or a sub class of hello default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="3c660-192">Należy pamiętać, że hello tego samego zgłaszający może obsługiwać kilka kategorii, zarejestruj je następująco:</span><span class="sxs-lookup"><span data-stu-id="3c660-192">Note that hello same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="3c660-193">tooreplace hello domyślną kategorii implementację można zarejestrować implementacji takich jak w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="3c660-193">tooreplace hello default category implementation, you can register your implementation like in hello following example:</span></span>

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

<span data-ttu-id="3c660-194">Hello bieżącej kategorii używany w procedurze obsługi jest przekazywana jako parametr w większości metod można zastąpić w `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="3c660-194">hello current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="3c660-195">Jest przekazywany jako `String` parametru lub pośrednio w `EngagementReachContent` obiektu, który ma `getCategory()` metody.</span><span class="sxs-lookup"><span data-stu-id="3c660-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="3c660-196">Można zmienić większość procesu tworzenia powiadomień hello na ponowne definiowanie metody `EngagementDefaultNotifier`dla bardziej zaawansowane dostosowania uznać wolnego tootake poszukaj w dokumentacji technicznej hello i na powitania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="3c660-196">You can change most of hello notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free tootake a look at hello technical documentation and at hello source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="3c660-197">Powiadomienia w aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c660-197">In-app notifications</span></span>
<span data-ttu-id="3c660-198">Jeśli chcesz alternatywne układy toouse dla określonej kategorii, można zaimplementować to jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="3c660-198">If you just want toouse alternate layouts for a specific category, you can implement this as in hello following example:</span></span>

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

<span data-ttu-id="3c660-199">**Przykład `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="3c660-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="3c660-200">Jak widać, hello nakładki widoku identyfikator różni się od standardowego hello jeden.</span><span class="sxs-lookup"><span data-stu-id="3c660-200">As you can see, hello overlay view identifier is different than hello standard one.</span></span> <span data-ttu-id="3c660-201">Należy pamiętać, że każdego układu dla nakładki używany unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="3c660-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="3c660-202">**Przykład `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="3c660-202">**Example of `my_notification_area.xml` :**</span></span>

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

<span data-ttu-id="3c660-203">Jak widać, identyfikator widoku obszaru powiadomień hello jest inny niż standardowe hello jeden.</span><span class="sxs-lookup"><span data-stu-id="3c660-203">As you can see, hello notification area view identifier is different than hello standard one.</span></span> <span data-ttu-id="3c660-204">Należy pamiętać, że każdy układ używa unikatowego identyfikatora obszarów powiadomień.</span><span class="sxs-lookup"><span data-stu-id="3c660-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="3c660-205">Ten prosty przykład kategorii sprawia, że powiadomienia aplikacji (lub w aplikacji) wyświetlany u góry hello hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="3c660-205">This simple example of category makes application (or in-app) notifications displayed at hello top of hello screen.</span></span> <span data-ttu-id="3c660-206">Nie został zmieniony hello identyfikatory standardowe używane w obszarze powiadomień hello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="3c660-206">We did not change hello standard identifiers used in hello notification area itself.</span></span>

<span data-ttu-id="3c660-207">Jeśli chcesz, aby toochange, że masz tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` metody.</span><span class="sxs-lookup"><span data-stu-id="3c660-207">If you want toochange that, you have tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="3c660-208">Zalecane jest toolook dokumentacji technicznej hello i kod źródłowy hello `EngagementNotifier` i `EngagementDefaultNotifier` Jeśli chcesz to poziomu zaawansowanego dostosowania.</span><span class="sxs-lookup"><span data-stu-id="3c660-208">It's recommended toolook at hello technical documentation and at hello source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="3c660-209">System powiadomień</span><span class="sxs-lookup"><span data-stu-id="3c660-209">System notifications</span></span>
<span data-ttu-id="3c660-210">Rozszerzając `EngagementDefaultNotifier`, można zastąpić `onNotificationPrepared` tooalter hello powiadomienia, który został przygotowany przez hello domyślną implementację.</span><span class="sxs-lookup"><span data-stu-id="3c660-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` tooalter hello notification that was prepared by hello default implementation.</span></span>

<span data-ttu-id="3c660-211">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="3c660-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="3c660-212">W tym przykładzie powoduje, że powiadomienie systemowe dla zawartości będzie wyświetlany jako zdarzenie uruchomione, gdy kategorii "stałe" hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="3c660-212">This example makes a system notification for a content being displayed as an ongoing event when hello "ongoing" category is used.</span></span>

<span data-ttu-id="3c660-213">Jeśli chcesz, aby toobuild hello `Notification` obiekt od początku, można powrócić `false` toohello — metoda i wywołanie `notify` samodzielnie na powitania `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="3c660-213">If you want toobuild hello `Notification` object from scratch, you can return `false` toohello method and call `notify` yourself on hello `NotificationManager`.</span></span> <span data-ttu-id="3c660-214">W takim przypadku należy pamiętać o jest `contentIntent`, `deleteIntent` i hello identyfikator powiadomienia, używany przez `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="3c660-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and hello notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="3c660-215">Oto przykład poprawnego takie implementacji:</span><span class="sxs-lookup"><span data-stu-id="3c660-215">Here is a correct example of such an implementation:</span></span>

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
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="3c660-216">Anonsów zawierających tylko powiadomienia</span><span class="sxs-lookup"><span data-stu-id="3c660-216">Notification only announcements</span></span>
<span data-ttu-id="3c660-217">Hello zarządzania powitania kliknij powiadomienie tylko anonsu można dostosowywać przez zastąpienie `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` hello toomodify przygotowane `Intent`.</span><span class="sxs-lookup"><span data-stu-id="3c660-217">hello management of hello click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello prepared `Intent`.</span></span> <span data-ttu-id="3c660-218">Za pomocą tej metody można łatwo tootune hello flagi.</span><span class="sxs-lookup"><span data-stu-id="3c660-218">Using this method allows you tootune hello flags easily.</span></span>

<span data-ttu-id="3c660-219">Na przykład tooadd hello `SINGLE_TOP` flagi:</span><span class="sxs-lookup"><span data-stu-id="3c660-219">For example tooadd hello `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="3c660-220">Dla starszych zaangażowania użytkowników należy pamiętać, że powiadomień systemowych bez akcji adresu URL teraz uruchamia aplikacji hello jeśli było w tle, więc ta metoda może być wywołany z anonsu bez adres URL akcji.</span><span class="sxs-lookup"><span data-stu-id="3c660-220">For legacy Engagement users, please note that system notifications without action URL now launches hello application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="3c660-221">Należy rozważyć który w przypadku zamiaru hello dostosowywania.</span><span class="sxs-lookup"><span data-stu-id="3c660-221">You should consider that when customizing hello intent.</span></span>

<span data-ttu-id="3c660-222">Można też wdrożyć `EngagementNotifier.executeNotifAnnouncementAction` od początku.</span><span class="sxs-lookup"><span data-stu-id="3c660-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="3c660-223">Cykl życia powiadomień</span><span class="sxs-lookup"><span data-stu-id="3c660-223">Notification life cycle</span></span>
<span data-ttu-id="3c660-224">Korzystając z kategorii domyślnej hello, w przypadku niektórych metod cyklu życia są nazywane na powitania `EngagementReachInteractiveContent` obiekt tooreport statystyk i aktualizacji hello kampanii stanu:</span><span class="sxs-lookup"><span data-stu-id="3c660-224">When using hello default category, some life cycle methods are called on hello `EngagementReachInteractiveContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="3c660-225">Gdy hello powiadomienia są wyświetlane w aplikacji lub umieść na pasku stanu hello, hello `displayNotification` metoda jest wywoływana (która statystyki) przez `EngagementReachAgent` Jeśli `handleNotification` zwraca `true`.</span><span class="sxs-lookup"><span data-stu-id="3c660-225">When hello notification is displayed in application or put in hello status bar, hello `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="3c660-226">Jeśli powiadomienia hello jest odrzucane, hello `exitNotification` metoda jest wywoływana, statystyka jest zgłaszany i dalej kampanii teraz mogą być przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="3c660-226">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="3c660-227">Po kliknięciu powiadomienia hello `actionNotification` jest nazywane, statystyka jest zgłaszany i celem hello skojarzone jest uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="3c660-227">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated intent is launched.</span></span>

<span data-ttu-id="3c660-228">Jeśli implementacji `EngagementNotifier` pomija hello domyślne zachowanie, należy toocall tych metod cyklu życia samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="3c660-228">If your implementation of `EngagementNotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="3c660-229">Hello następujące przykłady przedstawiają niektórych przypadkach, gdy pomijana jest hello domyślne zachowanie:</span><span class="sxs-lookup"><span data-stu-id="3c660-229">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="3c660-230">Nie można rozszerzyć `EngagementDefaultNotifier`, np. zaimplementowano obsługi kategorii od początku.</span><span class="sxs-lookup"><span data-stu-id="3c660-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="3c660-231">Dla powiadomień systemowych overrode hello `onNotificationPrepared` i możesz zmodyfikować `contentIntent` lub `deleteIntent` w hello `Notification` obiektu.</span><span class="sxs-lookup"><span data-stu-id="3c660-231">For system notifications, you overrode hello `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in hello `Notification` object.</span></span>
* <span data-ttu-id="3c660-232">Aby powiadomienia w aplikacji, overrode `prepareInAppArea`, toomap się, że co najmniej `actionNotification` tooone formantów U.I.</span><span class="sxs-lookup"><span data-stu-id="3c660-232">For in-app notifications, you overrode `prepareInAppArea`, be sure toomap at least `actionNotification` tooone of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="3c660-233">Jeśli `handleNotification` zwraca wyjątek, hello zawartości zostanie usunięty i `dropContent` jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="3c660-233">If `handleNotification` throws an exception, hello content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="3c660-234">Jest to raportowane w statystykach i dalej kampanii teraz mogą być przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="3c660-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="3c660-235">Anonsów i sond</span><span class="sxs-lookup"><span data-stu-id="3c660-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="3c660-236">Układy</span><span class="sxs-lookup"><span data-stu-id="3c660-236">Layouts</span></span>
<span data-ttu-id="3c660-237">Można zmodyfikować hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` i `engagement_poll.xml` pliki toocustomize tekst anonsów, web anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="3c660-237">You can modify hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files toocustomize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="3c660-238">Te pliki mają dwóch typowych układów hello tytuł i hello przycisk obszaru.</span><span class="sxs-lookup"><span data-stu-id="3c660-238">These files share two common layouts for hello title area and hello button area.</span></span> <span data-ttu-id="3c660-239">Układ Hello tytułu hello jest `engagement_content_title.xml` i używa hello gromadzący obiektów drawable plików w tle hello.</span><span class="sxs-lookup"><span data-stu-id="3c660-239">hello layout for hello title is `engagement_content_title.xml` and uses hello eponymous drawable file for hello background.</span></span> <span data-ttu-id="3c660-240">Witaj układ przycisków akcji i wyjścia hello jest `engagement_button_bar.xml` i używa hello gromadzący obiektów drawable plików w tle hello.</span><span class="sxs-lookup"><span data-stu-id="3c660-240">hello layout for hello action and exit buttons is `engagement_button_bar.xml` and uses hello eponymous drawable file for hello background.</span></span>

<span data-ttu-id="3c660-241">W sondowania hello układ pytanie i ich opcji są dynamicznie zwiększony, przy użyciu hello kilka razy `engagement_question.xml` pliku układu dla hello pytania i hello `engagement_choice.xml` hello wyborów w pliku.</span><span class="sxs-lookup"><span data-stu-id="3c660-241">In a poll, hello question layout and their choices are dynamically inflated using several times hello `engagement_question.xml` layout file for hello questions and hello `engagement_choice.xml` file for hello choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="3c660-242">Kategorie</span><span class="sxs-lookup"><span data-stu-id="3c660-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="3c660-243">Układy alternatywnej</span><span class="sxs-lookup"><span data-stu-id="3c660-243">Alternate layouts</span></span>
<span data-ttu-id="3c660-244">Jak powiadomienia Kategoria kampanii hello mogą być używane toohave alternatywne układy anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="3c660-244">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="3c660-245">Na przykład toocreate kategorii ogłoszenie tekstu, można rozszerzyć `EngagementTextAnnouncementActivity` i odwołaj hello `AndroidManifest.xml` pliku:</span><span class="sxs-lookup"><span data-stu-id="3c660-245">For example, toocreate a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it hello `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="3c660-246">Należy zwrócić uwagę tej kategorii hello w hello zamiar użyć filtru różnica hello toomake z hello domyślne działanie anonsu.</span><span class="sxs-lookup"><span data-stu-id="3c660-246">Note that hello category in hello intent filter is used toomake hello difference with hello default announcement activity.</span></span>

<span data-ttu-id="3c660-247">Hello osiągnąć SDK używa hello konwersji system tooresolve hello odpowiednim działaniu dla określonej kategorii i jego powraca na powitania domyślnej kategorii Jeśli rozwiązanie hello nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="3c660-247">hello Reach SDK uses hello intent system tooresolve hello right activity for a specific category and it falls back on hello default category if hello resolution failed.</span></span>

<span data-ttu-id="3c660-248">Następnie tooimplement `MyCustomTextAnnouncementActivity`, po prostu toochange hello układu (, ale zachować hello tego samego widoku identyfikatorów), wystarczy toodefine hello klasy, jak w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="3c660-248">Then you have tooimplement `MyCustomTextAnnouncementActivity`, if you just want toochange hello layout (but keep hello same view identifiers), you just have toodefine hello class like in hello following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

<span data-ttu-id="3c660-249">tooreplace hello domyślnej kategorii anonsów tekstu, po prostu zastąpić `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` przy implementacji.</span><span class="sxs-lookup"><span data-stu-id="3c660-249">tooreplace hello default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="3c660-250">W podobny sposób można dostosować Web anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="3c660-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="3c660-251">W przypadku anonsów zawierających sieci web można rozszerzyć `EngagementWebAnnouncementActivity` ani deklarować Twoich działaniach w hello `AndroidManifest.xml` w hello poniższy przykład, takich jak:</span><span class="sxs-lookup"><span data-stu-id="3c660-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="3c660-252">Ankiety można rozszerzyć `EngagementPollActivity` ani deklarować użytkownika w hello `AndroidManifest.xml` w hello poniższy przykład, takich jak:</span><span class="sxs-lookup"><span data-stu-id="3c660-252">For polls you can extend `EngagementPollActivity` and declare your in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="3c660-253">Implementacja od podstaw</span><span class="sxs-lookup"><span data-stu-id="3c660-253">Implementation from scratch</span></span>
<span data-ttu-id="3c660-254">Można zaimplementować kategorie działań anonsu (i sondowania) bez rozszerzenie jednej hello `Engagement*Activity` klasy podał hello osiągnąć zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="3c660-254">You can implement categories for your announcement (and poll) activities without extending one of hello `Engagement*Activity` classes provided by hello Reach SDK.</span></span> <span data-ttu-id="3c660-255">Jest to przydatne na przykład jeśli chcesz toodefine układu, które nie są używane hello sam widoków jako hello standardowych układów.</span><span class="sxs-lookup"><span data-stu-id="3c660-255">This is useful for example if you want toodefine a layout that does not use hello same views as hello standard layouts.</span></span>

<span data-ttu-id="3c660-256">Podobnie jak dostosowywania powiadomień zaawansowane, zalecane jest toolook na kod źródłowy hello hello standardowej implementacji.</span><span class="sxs-lookup"><span data-stu-id="3c660-256">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

<span data-ttu-id="3c660-257">Poniżej przedstawiono niektóre czynności tookeep pamiętać: Reach uruchomi hello działania z określonym profilem (odpowiedniego filtru konwersji toohello) oraz dodatkowy parametr, który jest hello identyfikator zawartości.</span><span class="sxs-lookup"><span data-stu-id="3c660-257">Here are some things tookeep in mind: Reach will launch hello activity with a specific intent (corresponding toohello intent filter) plus an extra parameter which is hello content identifier.</span></span>

<span data-ttu-id="3c660-258">tooretrieve hello zawartości obiektu, który zawiera pola hello określony podczas tworzenia hello kampanii w witrynie sieci web hello możesz to zrobić:</span><span class="sxs-lookup"><span data-stu-id="3c660-258">tooretrieve hello content object which contain hello fields you specified when creating hello campaign on hello web site you can do this:</span></span>

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

<span data-ttu-id="3c660-259">Statystyki, zgłoś hello zawartość jest wyświetlana w hello `onResume` zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="3c660-259">For statistics, you should report hello content is displayed in hello `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="3c660-260">Następnie, nie zapomnij albo toocall `actionContent(this)` lub `exitContent(this)` hello zawartości obiektu przed hello działanie przechodzi w tle.</span><span class="sxs-lookup"><span data-stu-id="3c660-260">Then, don't forget toocall either `actionContent(this)` or `exitContent(this)` on hello content object before hello activity goes into background.</span></span>

<span data-ttu-id="3c660-261">Nie można wywołać albo `actionContent` lub `exitContent`, statystyki nie zostaną wysłane (tzn. nie analizy kampanii hello) i więcej wszystkim hello dalej kampanii nie zostaną powiadomieni do ponownego uruchomienia procesu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3c660-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly, hello next campaigns will not be notified until hello application process is restarted.</span></span>

<span data-ttu-id="3c660-262">Orientacja lub innych zmian konfiguracji można upewnij toodetermine trudnych kodu hello czy hello działanie przechodzi w tle, lub nie, hello sprawia, że standardowej implementacji się, że zawartość hello jest raportowane jako zakończony, jeśli odejdzie użytkownik, hello działania hello, (albo przez Naciśnięcie przycisku `HOME` lub `BACK`), ale nie w przypadku zmiany orientacji hello.</span><span class="sxs-lookup"><span data-stu-id="3c660-262">Orientation or other configuration changes can make hello code tricky toodetermine whether hello activity goes into background or not, hello standard implementation makes sure hello content is reported as exited if hello user leaves hello activity (either by pressing `HOME` or `BACK`) but not if hello orientation changes.</span></span>

<span data-ttu-id="3c660-263">Oto hello interesujące część implementacji hello:</span><span class="sxs-lookup"><span data-stu-id="3c660-263">Here is hello interesting part of hello implementation:</span></span>

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
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="3c660-264">Jak widać, jeśli wywołujesz `actionContent(this)` , a następnie Zakończono działanie hello `exitContent(this)` można bezpiecznie wywołać bez żadnego efektu.</span><span class="sxs-lookup"><span data-stu-id="3c660-264">As you can see, if you called `actionContent(this)` then finished hello activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[usługi Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
