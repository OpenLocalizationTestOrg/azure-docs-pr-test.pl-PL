---
title: aaaAzure Mobile Engagement Android SDK integracji
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK systemu Android dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="63da3-103">Procedury uaktualniania</span><span class="sxs-lookup"><span data-stu-id="63da3-103">Upgrade procedures</span></span>
<span data-ttu-id="63da3-104">Jeśli już jest zintegrowany starszej wersji naszego zestawu SDK do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="63da3-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="63da3-105">Masz toofollow kilka procedur Jeśli pominięte różne wersje hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="63da3-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="63da3-106">Na przykład w przypadku migracji z 1.4.0 too1.6.0 masz toofirst wykonaj hello "z 1.4.0 too1.5.0" procedury, a następnie hello "z 1.5.0 too1.6.0" procedury.</span><span class="sxs-lookup"><span data-stu-id="63da3-106">For example if you migrate from 1.4.0 too1.6.0 you have toofirst follow hello "from 1.4.0 too1.5.0" procedure then hello "from 1.5.0 too1.6.0" procedure.</span></span>

<span data-ttu-id="63da3-107">Uaktualnienie z wersji hello masz tooreplace hello `mobile-engagement-VERSION.jar` z hello nową.</span><span class="sxs-lookup"><span data-stu-id="63da3-107">Whatever hello version you upgrade from, you have tooreplace hello `mobile-engagement-VERSION.jar` with hello new one.</span></span>

## <a name="from-420-too421"></a><span data-ttu-id="63da3-108">Z 4.2.0 too4.2.1</span><span class="sxs-lookup"><span data-stu-id="63da3-108">From 4.2.0 too4.2.1</span></span>
<span data-ttu-id="63da3-109">Ten krok faktycznie można zrobić w dowolnej wersji hello zestawu SDK, jest poprawy zabezpieczeń po zintegrowaniu Reach działań.</span><span class="sxs-lookup"><span data-stu-id="63da3-109">This step can actually be done on any version of hello SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="63da3-110">Teraz należy dodać `exported="false"` tooall Reach działań.</span><span class="sxs-lookup"><span data-stu-id="63da3-110">You should now add `exported="false"` tooall Reach activities.</span></span>

<span data-ttu-id="63da3-111">Działania reach powinna wyglądać tak jak to Twojej `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="63da3-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-too410"></a><span data-ttu-id="63da3-112">Z 4.0.0 too4.1.0</span><span class="sxs-lookup"><span data-stu-id="63da3-112">From 4.0.0 too4.1.0</span></span>
<span data-ttu-id="63da3-113">Hello SDK teraz dojścia nowe uprawnienia modelu z systemem Android M.</span><span class="sxs-lookup"><span data-stu-id="63da3-113">hello SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="63da3-114">Jeśli lokalizacja funkcji lub powiadomienia szerszej przeczytaj [w tej sekcji](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="63da3-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="63da3-115">Ponadto nowy model uprawnień toohello obsługujemy teraz konfigurowania lokalizacji funkcji w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="63da3-115">In addition toohello new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="63da3-116">Firma Microsoft są nadal zgodne z parametrami manifestu hello lokalizacji, ale jest już przestarzały.</span><span class="sxs-lookup"><span data-stu-id="63da3-116">We are still compatible with hello manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="63da3-117">Konfiguracja środowiska uruchomieniowego toouse, Usuń hello poniższych sekcjach przedstawiono z Twojej ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="63da3-117">toouse runtime configuration, remove hello following sections from your ``AndroidManifest.xml``:</span></span>

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

<span data-ttu-id="63da3-118">i odczytu [to zaktualizowane procedury](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse Konfiguracja środowiska uruchomieniowego zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="63da3-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime configuration instead.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="63da3-119">Z 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="63da3-119">From 3.0.0 too4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="63da3-120">Natywnych powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="63da3-120">Native push</span></span>
<span data-ttu-id="63da3-121">Natywnych powiadomień wypychanych (GCM/ADM) teraz służy także do w powiadomieniach wewnętrznych aplikacji, musisz skonfigurować poświadczenia natywnych powiadomień wypychanych powitania dla dowolnego typu wypychania kampanii.</span><span class="sxs-lookup"><span data-stu-id="63da3-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="63da3-122">Jeśli nie jest już wykonaj [tej procedury](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="63da3-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="63da3-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="63da3-123">AndroidManifest.xml</span></span>
<span data-ttu-id="63da3-124">Integracja reach został zmodyfikowany w ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="63da3-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="63da3-125">Zastąp to:</span><span class="sxs-lookup"><span data-stu-id="63da3-125">Replace this:</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="63da3-126">Od</span><span class="sxs-lookup"><span data-stu-id="63da3-126">By</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
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

<span data-ttu-id="63da3-127">Brak prawdopodobnie ekranu ładowania teraz kliknięcie powiadomienia (tekstu/sieci web z zawartością) lub sonda.</span><span class="sxs-lookup"><span data-stu-id="63da3-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="63da3-128">Masz tooadd to dla tych toowork kampanii w 4.0.0:</span><span class="sxs-lookup"><span data-stu-id="63da3-128">You have tooadd this for those campaigns toowork in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="63da3-129">Zasoby</span><span class="sxs-lookup"><span data-stu-id="63da3-129">Resources</span></span>
<span data-ttu-id="63da3-130">Osadź hello nowe `res/layout/engagement_loading.xml` plik do projektu.</span><span class="sxs-lookup"><span data-stu-id="63da3-130">Embed hello new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-too300"></a><span data-ttu-id="63da3-131">Z 2.4.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="63da3-131">From 2.4.0 too3.0.0</span></span>
<span data-ttu-id="63da3-132">Witaj poniżej opisano sposób toomigrate integracji zestawu SDK z hello Capptain usługi oferowane przez Capptain SAS w aplikacji obsługiwane przez usługę Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="63da3-132">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="63da3-133">W przypadku migracji z wcześniejszej wersji, należy najpierw zapoznać się hello Capptain witryny sieci web toomigrate too2.4.0, a następnie Zastosuj hello procedury.</span><span class="sxs-lookup"><span data-stu-id="63da3-133">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too2.4.0 first and then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63da3-134">Capptain Mobile Engagement są takie same usługi nie hello i hello procedury przedstawionej poniżej tylko highlights jak toomigrate hello aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="63da3-134">Capptain and Mobile Engagement are not hello same services, and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="63da3-135">Migrowanie hello zestawu SDK w aplikacji hello nie będą migrowane dane z hello Capptain serwerów toohello Mobile Engagement serwerów.</span><span class="sxs-lookup"><span data-stu-id="63da3-135">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="63da3-136">Plik JAR</span><span class="sxs-lookup"><span data-stu-id="63da3-136">JAR file</span></span>
<span data-ttu-id="63da3-137">Zastąp `capptain.jar` przez `mobile-engagement-VERSION.jar` w Twojej `libs` folderu.</span><span class="sxs-lookup"><span data-stu-id="63da3-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="63da3-138">Pliki zasobów</span><span class="sxs-lookup"><span data-stu-id="63da3-138">Resource files</span></span>
<span data-ttu-id="63da3-139">Każdy plik zasobu podaliśmy (poprzedzony `capptain_`) ma toobe zastąpione przez nowe hello (prefiksem `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="63da3-139">Every resource file that we provided (prefixed by `capptain_`) has toobe replaced by hello new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="63da3-140">Jeśli dostosowano te pliki mają toore — zastosować dostosowanie hello nowych plików, **zmieniono również wszystkie identyfikatory hello w plikach zasobów hello**.</span><span class="sxs-lookup"><span data-stu-id="63da3-140">If you customized those files, you have toore-apply your customization on hello new files, **all hello identifiers in hello resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="63da3-141">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="63da3-141">Application ID</span></span>
<span data-ttu-id="63da3-142">Teraz zaangażowania używa połączenia ciąg tooconfigure hello SDK takie identyfikatory jak identyfikator aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="63da3-142">Now Engagement uses a connection string tooconfigure hello SDK identifiers such as hello application identifier.</span></span>

<span data-ttu-id="63da3-143">Masz toouse `EngagementAgent.init` metody w działanie uruchamiania następująco:</span><span class="sxs-lookup"><span data-stu-id="63da3-143">You have toouse `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="63da3-144">Parametry połączenia Hello aplikacji jest wyświetlana w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="63da3-144">hello connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="63da3-145">Usuń wszystkie wywołania zbyt`CapptainAgent.configure` jako `EngagementAgent.init` zastępuje tę metodę.</span><span class="sxs-lookup"><span data-stu-id="63da3-145">Please remove any call too`CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="63da3-146">Witaj `appId` nie będzie można skonfigurować przy użyciu `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="63da3-146">hello `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="63da3-147">Usuń w tej sekcji z Twojej `AndroidManifest.xml` Jeśli została ona:</span><span class="sxs-lookup"><span data-stu-id="63da3-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="63da3-148">Interfejs API języka Java</span><span class="sxs-lookup"><span data-stu-id="63da3-148">Java API</span></span>
<span data-ttu-id="63da3-149">Co wywołanie tooany Klasa Java naszego zestawu SDK ma toobe zmieniona; na przykład `CapptainAgent.getInstance(this)` można zmienić nazwy `EngagementAgent.getInstance(this)`, `extends CapptainActivity` można zmienić nazwy `extends EngagementActivity` itp...</span><span class="sxs-lookup"><span data-stu-id="63da3-149">Every call tooany Java class of our SDK has toobe renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="63da3-150">Jeśli zostały zintegrowany z domyślnych plików preferencji agenta, hello domyślna nazwa pliku jest teraz `engagement.agent` , klucz hello `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="63da3-150">If you were integrated with default agent preference files, hello default file name is now `engagement.agent` and hello key is `engagement:agent`.</span></span>

<span data-ttu-id="63da3-151">Podczas tworzenia sieci web anonsów, hello integratora Javascript jest teraz `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="63da3-151">When creating web announcements, hello Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="63da3-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="63da3-152">AndroidManifest.xml</span></span>
<span data-ttu-id="63da3-153">Wiele zmian się stało, hello usługi nie jest już udostępniony i wiele odbiorników nie są już możliwy do eksportu.</span><span class="sxs-lookup"><span data-stu-id="63da3-153">A lot of changes happened there, hello service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="63da3-154">Deklaracja usługi Hello jest teraz prostsze; Usuń filtr konwersji hello i wszystkie metadane w nim, a następnie dodaj `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="63da3-154">hello service declaration is now simpler; remove hello intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="63da3-155">Oprócz wszystko, co jest zaangażowania toouse zmienioną nazwę.</span><span class="sxs-lookup"><span data-stu-id="63da3-155">Plus everything is renamed toouse engagement.</span></span>

<span data-ttu-id="63da3-156">Teraz wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="63da3-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="63da3-157">Tooenable dzienników testu, należy hello meta-data została przeniesiona toohello aplikacji tagu i została zmieniona:</span><span class="sxs-lookup"><span data-stu-id="63da3-157">When you want tooenable test logs, hello meta-data has now been moved toohello application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="63da3-158">Zmieniono tylko wszystkie inne metadane, w tym miejscu jest pełna lista hello (oczywiście rename tylko hello te używasz):</span><span class="sxs-lookup"><span data-stu-id="63da3-158">All other meta-data have just been renamed, here is hello full list (of course rename only hello ones you use):</span></span>

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

<span data-ttu-id="63da3-159">Śledzenie Google Play i SmartAd została usunięta z pakietu SDK wystarczy tooremove to bez zastępowania:</span><span class="sxs-lookup"><span data-stu-id="63da3-159">Google Play and SmartAd tracking has been removed from SDK you just have tooremove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="63da3-160">działania Reach Hello są obecnie deklarowane następująco:</span><span class="sxs-lookup"><span data-stu-id="63da3-160">hello Reach activities are now declared like this:</span></span>

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

<span data-ttu-id="63da3-161">Jeśli masz działań niestandardowych Reach albo należy tylko toochange hello konwersji akcje toomatch `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` lub `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="63da3-161">If you have custom Reach activities, you need only toochange hello intent actions toomatch either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="63da3-162">Hello emisji odbiorniki zmieniono plus teraz dodać `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="63da3-162">hello broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="63da3-163">Poniżej przedstawiono pełną listę hello hello odbiorcy z hello nowej specyfikacji (oczywiście rename tylko hello te używasz):</span><span class="sxs-lookup"><span data-stu-id="63da3-163">Here is hello full list of hello receivers with hello new specification, (of course rename only hello ones you use):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

<span data-ttu-id="63da3-164">Śledzenie odbiornika zostały usunięte, tak aby było tooremove w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="63da3-164">Tracking receiver has been removed, so you have tooremove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="63da3-165">Należy pamiętać, że deklaracja hello implementacji hello emisji odbiornika **EngagementMessageReceiver** została zmieniona w hello `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="63da3-165">Note that hello declaration of your implementation of hello broadcast receiver **EngagementMessageReceiver** has changed in hello `AndroidManifest.xml`.</span></span> <span data-ttu-id="63da3-166">To jest ponieważ toosend hello interfejsu API i usunięcie dowolnego XMPP komunikaty z dowolnego jednostek XMPP i hello toosend interfejsu API i odbierania wiadomości między urządzeniami zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="63da3-166">This is because hello API toosend and remove arbitrary XMPP messages from arbitrary XMPP entities and hello API toosend and receive messages between devices have been removed.</span></span> <span data-ttu-id="63da3-167">W związku z tym również masz hello toodelete następujące wywołania zwrotne z Twojej **EngagementMessageReceiver** implementacji:</span><span class="sxs-lookup"><span data-stu-id="63da3-167">Thus, you have also toodelete hello following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="63da3-168">i</span><span class="sxs-lookup"><span data-stu-id="63da3-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="63da3-169">Usuń wszystkie wywołania na **EngagementAgent** dla:</span><span class="sxs-lookup"><span data-stu-id="63da3-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="63da3-170">i</span><span class="sxs-lookup"><span data-stu-id="63da3-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="63da3-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="63da3-171">Proguard</span></span>
<span data-ttu-id="63da3-172">Proguard konfiguracji może mieć wpływ rebranding powitalne reguły teraz chce się dowiedzieć, jak:</span><span class="sxs-lookup"><span data-stu-id="63da3-172">Proguard configuration can be impacted by rebranding, hello rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

