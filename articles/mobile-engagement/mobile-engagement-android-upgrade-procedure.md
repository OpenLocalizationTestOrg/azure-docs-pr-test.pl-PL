---
title: "Integracja zestawu SDK systemu Android z usługi Azure Mobile Engagement"
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
ms.openlocfilehash: 1f047f93fa8bc852b28c86e91d0c007a94fb4299
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="caec0-103">Procedury uaktualniania</span><span class="sxs-lookup"><span data-stu-id="caec0-103">Upgrade procedures</span></span>
<span data-ttu-id="caec0-104">Jeśli już jest zintegrowany starszej wersji naszego zestawu SDK do aplikacji, należy wziąć pod uwagę następujące kwestie, podczas uaktualniania zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="caec0-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="caec0-105">Należy wykonać kilka procedur, jeśli pominięte kilka wersji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="caec0-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="caec0-106">Na przykład w przypadku migrowania z 1.4.0 do 1.6.0, należy najpierw wykonać procedurę "od 1.4.0 do 1.5.0" następnie procedury "od 1.5.0 do 1.6.0".</span><span class="sxs-lookup"><span data-stu-id="caec0-106">For example if you migrate from 1.4.0 to 1.6.0 you have to first follow the "from 1.4.0 to 1.5.0" procedure then the "from 1.5.0 to 1.6.0" procedure.</span></span>

<span data-ttu-id="caec0-107">Niezależnie od wersji uaktualnienia, należy zastąpić `mobile-engagement-VERSION.jar` nowym.</span><span class="sxs-lookup"><span data-stu-id="caec0-107">Whatever the version you upgrade from, you have to replace the `mobile-engagement-VERSION.jar` with the new one.</span></span>

## <a name="from-420-to-421"></a><span data-ttu-id="caec0-108">Z 4.2.0 do 4.2.1</span><span class="sxs-lookup"><span data-stu-id="caec0-108">From 4.2.0 to 4.2.1</span></span>
<span data-ttu-id="caec0-109">Ten krok faktycznie można zrobić w dowolnej wersji zestawu SDK, jest do poprawy zabezpieczeń po zintegrowaniu Reach działań.</span><span class="sxs-lookup"><span data-stu-id="caec0-109">This step can actually be done on any version of the SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="caec0-110">Teraz należy dodać `exported="false"` dla wszystkich działań Reach.</span><span class="sxs-lookup"><span data-stu-id="caec0-110">You should now add `exported="false"` to all Reach activities.</span></span>

<span data-ttu-id="caec0-111">Działania reach powinna wyglądać tak jak to Twojej `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="caec0-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-to-410"></a><span data-ttu-id="caec0-112">Z 4.0.0 do 4.1.0</span><span class="sxs-lookup"><span data-stu-id="caec0-112">From 4.0.0 to 4.1.0</span></span>
<span data-ttu-id="caec0-113">Zestaw SDK teraz dojścia nowe uprawnienia modelu z systemem Android M.</span><span class="sxs-lookup"><span data-stu-id="caec0-113">The SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="caec0-114">Jeśli lokalizacja funkcji lub powiadomienia szerszej przeczytaj [w tej sekcji](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="caec0-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="caec0-115">Oprócz nowego modelu uprawnień obsługujemy są teraz skonfigurować funkcje lokalizacji w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="caec0-115">In addition to the new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="caec0-116">Firma Microsoft są nadal zgodne z parametrami manifestu dla lokalizacji, ale jest już przestarzały.</span><span class="sxs-lookup"><span data-stu-id="caec0-116">We are still compatible with the manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="caec0-117">Aby użyć konfiguracji środowiska uruchomieniowego, Usuń z następującymi sekcjami w Twojej ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="caec0-117">To use runtime configuration, remove the following sections from your ``AndroidManifest.xml``:</span></span>

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

<span data-ttu-id="caec0-118">i odczytu [to zaktualizowane procedury](mobile-engagement-android-integrate-engagement.md#location-reporting) zamiast tego użyć konfiguracji środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="caec0-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) to use runtime configuration instead.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="caec0-119">Z 3.0.0 do 4.0.0</span><span class="sxs-lookup"><span data-stu-id="caec0-119">From 3.0.0 to 4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="caec0-120">Natywnych powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="caec0-120">Native push</span></span>
<span data-ttu-id="caec0-121">Natywnych powiadomień wypychanych (GCM/ADM) teraz służy także do w powiadomieniach wewnętrznych aplikacji, musisz skonfigurować poświadczenia natywnych powiadomień wypychanych dla dowolnego typu wypychania kampanii.</span><span class="sxs-lookup"><span data-stu-id="caec0-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="caec0-122">Jeśli nie jest już wykonaj [tej procedury](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="caec0-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="caec0-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="caec0-123">AndroidManifest.xml</span></span>
<span data-ttu-id="caec0-124">Integracja reach został zmodyfikowany w ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="caec0-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="caec0-125">Zastąp to:</span><span class="sxs-lookup"><span data-stu-id="caec0-125">Replace this:</span></span>

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

<span data-ttu-id="caec0-126">Od</span><span class="sxs-lookup"><span data-stu-id="caec0-126">By</span></span>

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

<span data-ttu-id="caec0-127">Brak prawdopodobnie ekranu ładowania teraz kliknięcie powiadomienia (tekstu/sieci web z zawartością) lub sonda.</span><span class="sxs-lookup"><span data-stu-id="caec0-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="caec0-128">Należy dodać to dla tych kampanii do pracy w 4.0.0:</span><span class="sxs-lookup"><span data-stu-id="caec0-128">You have to add this for those campaigns to work in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="caec0-129">Zasoby</span><span class="sxs-lookup"><span data-stu-id="caec0-129">Resources</span></span>
<span data-ttu-id="caec0-130">Osadzić nowy `res/layout/engagement_loading.xml` plik do projektu.</span><span class="sxs-lookup"><span data-stu-id="caec0-130">Embed the new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-to-300"></a><span data-ttu-id="caec0-131">Z 2.4.0 do 3.0.0</span><span class="sxs-lookup"><span data-stu-id="caec0-131">From 2.4.0 to 3.0.0</span></span>
<span data-ttu-id="caec0-132">Poniżej opisano sposób migracji integracji zestawu SDK usługi Capptain oferowane przez Capptain SAS w aplikacji obsługiwane przez usługę Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="caec0-132">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="caec0-133">W przypadku migracji z wcześniejszej wersji, przejrzyj witrynę sieci web Capptain, aby przeprowadzić migrację do 2.4.0, a następnie zastosować następującą procedurę.</span><span class="sxs-lookup"><span data-stu-id="caec0-133">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 2.4.0 first and then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="caec0-134">Capptain i usługi Mobile Engagement nie są takie same usługi i procedury przedstawionej poniżej tylko prezentuje sposób migracji aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="caec0-134">Capptain and Mobile Engagement are not the same services, and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="caec0-135">Migrowanie zestawu SDK w aplikacji nie będą migrowane dane z serwerów Capptain do serwerów usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="caec0-135">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="caec0-136">Plik JAR</span><span class="sxs-lookup"><span data-stu-id="caec0-136">JAR file</span></span>
<span data-ttu-id="caec0-137">Zastąp `capptain.jar` przez `mobile-engagement-VERSION.jar` w Twojej `libs` folderu.</span><span class="sxs-lookup"><span data-stu-id="caec0-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="caec0-138">Pliki zasobów</span><span class="sxs-lookup"><span data-stu-id="caec0-138">Resource files</span></span>
<span data-ttu-id="caec0-139">Każdy plik zasobu podaliśmy (poprzedzony `capptain_`) musi zostać zastąpione przez nowe (prefiksem `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="caec0-139">Every resource file that we provided (prefixed by `capptain_`) has to be replaced by the new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="caec0-140">Po dostosowaniu tych plików, należy ponownie zastosować dostosowanie na nowe pliki **również zmieniono identyfikatorów plików zasobów**.</span><span class="sxs-lookup"><span data-stu-id="caec0-140">If you customized those files, you have to re-apply your customization on the new files, **all the identifiers in the resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="caec0-141">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="caec0-141">Application ID</span></span>
<span data-ttu-id="caec0-142">Teraz zaangażowania używa parametrów połączenia do konfigurowania identyfikatory zestawu SDK, takich jak identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="caec0-142">Now Engagement uses a connection string to configure the SDK identifiers such as the application identifier.</span></span>

<span data-ttu-id="caec0-143">Należy użyć `EngagementAgent.init` metody w działanie uruchamiania następująco:</span><span class="sxs-lookup"><span data-stu-id="caec0-143">You have to use `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="caec0-144">Ciąg połączenia dla aplikacji jest wyświetlana w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="caec0-144">The connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="caec0-145">Usuń wszystkie wywołania `CapptainAgent.configure` jako `EngagementAgent.init` zastępuje tę metodę.</span><span class="sxs-lookup"><span data-stu-id="caec0-145">Please remove any call to `CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="caec0-146">`appId` Nie będzie można skonfigurować przy użyciu `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="caec0-146">The `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="caec0-147">Usuń w tej sekcji z Twojej `AndroidManifest.xml` Jeśli została ona:</span><span class="sxs-lookup"><span data-stu-id="caec0-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="caec0-148">Interfejs API języka Java</span><span class="sxs-lookup"><span data-stu-id="caec0-148">Java API</span></span>
<span data-ttu-id="caec0-149">Każdego wywołania dla każdej klasy Java naszego zestawu SDK ma zostać zmienione; na przykład `CapptainAgent.getInstance(this)` można zmienić nazwy `EngagementAgent.getInstance(this)`, `extends CapptainActivity` można zmienić nazwy `extends EngagementActivity` itp...</span><span class="sxs-lookup"><span data-stu-id="caec0-149">Every call to any Java class of our SDK has to be renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="caec0-150">Jeśli zostały zintegrowany z domyślnych plików preferencji agenta, domyślna nazwa pliku jest teraz `engagement.agent` , jak klucz `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="caec0-150">If you were integrated with default agent preference files, the default file name is now `engagement.agent` and the key is `engagement:agent`.</span></span>

<span data-ttu-id="caec0-151">Podczas tworzenia sieci web anonsów, integratora Javascript jest teraz `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="caec0-151">When creating web announcements, the Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="caec0-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="caec0-152">AndroidManifest.xml</span></span>
<span data-ttu-id="caec0-153">Wiele zmian się stało, usługa nie jest już udostępniony i wiele odbiorników nie są już możliwy do eksportu.</span><span class="sxs-lookup"><span data-stu-id="caec0-153">A lot of changes happened there, the service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="caec0-154">Deklaracja usługa jest teraz prostsze; Usuń filtr konwersji i wszystkie metadane w nim, a następnie dodaj `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="caec0-154">The service declaration is now simpler; remove the intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="caec0-155">Dodatkowo wszystko, co jest zmieniana za pomocą engagement.</span><span class="sxs-lookup"><span data-stu-id="caec0-155">Plus everything is renamed to use engagement.</span></span>

<span data-ttu-id="caec0-156">Teraz wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="caec0-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="caec0-157">Jeśli chcesz włączyć dzienników testu meta-data teraz został przeniesiony do tagu aplikacji i została zmieniona:</span><span class="sxs-lookup"><span data-stu-id="caec0-157">When you want to enable test logs, the meta-data has now been moved to the application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="caec0-158">Zmieniono tylko wszystkie inne metadane, poniżej przedstawiono pełną listę (zmiana nazwy kursu tylko te, które są używane):</span><span class="sxs-lookup"><span data-stu-id="caec0-158">All other meta-data have just been renamed, here is the full list (of course rename only the ones you use):</span></span>

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

<span data-ttu-id="caec0-159">Google Play i SmartAd śledzenia został usunięty z zestawu SDK, należy usunąć to bez zastępowania:</span><span class="sxs-lookup"><span data-stu-id="caec0-159">Google Play and SmartAd tracking has been removed from SDK you just have to remove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="caec0-160">Działania Reach są obecnie deklarowane następująco:</span><span class="sxs-lookup"><span data-stu-id="caec0-160">The Reach activities are now declared like this:</span></span>

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

<span data-ttu-id="caec0-161">Jeśli masz działań niestandardowych Reach musisz tylko zmienić akcje konwersji do pasuje do żadnej `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` lub `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="caec0-161">If you have custom Reach activities, you need only to change the intent actions to match either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="caec0-162">Zmieniono emisji odbiornikami, a także teraz dodać `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="caec0-162">The broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="caec0-163">Poniżej przedstawiono pełną listę odbiorcy z nowego specyfikacji, (zmiana nazwy kursu tylko te, które są używane):</span><span class="sxs-lookup"><span data-stu-id="caec0-163">Here is the full list of the receivers with the new specification, (of course rename only the ones you use):</span></span>

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

<span data-ttu-id="caec0-164">Odbiornik śledzenia zostały usunięte, więc musisz usunąć w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="caec0-164">Tracking receiver has been removed, so you have to remove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="caec0-165">Należy pamiętać, że deklaracji w implementacji emisji odbiornika **EngagementMessageReceiver** została zmieniona w `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="caec0-165">Note that the declaration of your implementation of the broadcast receiver **EngagementMessageReceiver** has changed in the `AndroidManifest.xml`.</span></span> <span data-ttu-id="caec0-166">Jest to spowodowane usunięto interfejs API do wysyłania i usunąć dowolnego XMPP wiadomości z dowolnego XMPP jednostek i interfejsu API do wysyłania i odbierania wiadomości między urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="caec0-166">This is because the API to send and remove arbitrary XMPP messages from arbitrary XMPP entities and the API to send and receive messages between devices have been removed.</span></span> <span data-ttu-id="caec0-167">W związku z tym należy również usunąć następujące wywołania zwrotne z Twojej **EngagementMessageReceiver** implementacji:</span><span class="sxs-lookup"><span data-stu-id="caec0-167">Thus, you have also to delete the following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="caec0-168">i</span><span class="sxs-lookup"><span data-stu-id="caec0-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="caec0-169">Usuń wszystkie wywołania na **EngagementAgent** dla:</span><span class="sxs-lookup"><span data-stu-id="caec0-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="caec0-170">i</span><span class="sxs-lookup"><span data-stu-id="caec0-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="caec0-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="caec0-171">Proguard</span></span>
<span data-ttu-id="caec0-172">Konfiguracja proguard może mieć wpływ rebranding, reguły teraz chce się dowiedzieć, jak:</span><span class="sxs-lookup"><span data-stu-id="caec0-172">Proguard configuration can be impacted by rebranding, the rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

