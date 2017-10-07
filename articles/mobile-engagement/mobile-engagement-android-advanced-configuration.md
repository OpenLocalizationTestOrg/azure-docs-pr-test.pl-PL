---
title: Konfiguracja aaaAdvanced zestawem Azure Mobile Engagement Android SDK
description: W tym artykule opisano hello zaawansowane opcje konfiguracji, w tym hello manifestu systemu Android z zestawem Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="d2cba-103">Konfiguracja zaawansowana dla zestawem Azure Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="d2cba-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2cba-104">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d2cba-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="d2cba-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d2cba-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="d2cba-106">iOS</span><span class="sxs-lookup"><span data-stu-id="d2cba-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="d2cba-107">Android</span><span class="sxs-lookup"><span data-stu-id="d2cba-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="d2cba-108">W tej procedurze opisano sposób tooconfigure różnych opcji konfiguracji dla usługi Azure Mobile Engagement aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="d2cba-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2cba-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d2cba-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="d2cba-110">Wymagania dotyczące uprawnień</span><span class="sxs-lookup"><span data-stu-id="d2cba-110">Permission Requirements</span></span>
<span data-ttu-id="d2cba-111">Niektóre opcje muszą mieć określone uprawnienia, które są wymienione wszystkie tutaj odwołania i wiersza w określonej funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="d2cba-111">Some options require specific permissions, all of which are listed here for reference, and in-line in hello specific feature.</span></span> <span data-ttu-id="d2cba-112">Dodaj te uprawnienia toohello AndroidManifest.xml projektu bezpośrednio przed lub po hello `<application>` tagu.</span><span class="sxs-lookup"><span data-stu-id="d2cba-112">Add these permissions toohello AndroidManifest.xml of your project immediately before or after hello `<application>` tag.</span></span>

<span data-ttu-id="d2cba-113">kod uprawnień Hello musi toolook, takich jak hello poniższe polecenie, gdzie Wypełnij hello odpowiednich uprawnień z poniższą tabelą hello.</span><span class="sxs-lookup"><span data-stu-id="d2cba-113">hello permission code needs toolook like hello following, where you fill in hello appropriate permission from hello table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="d2cba-114">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="d2cba-114">Permission</span></span> | <span data-ttu-id="d2cba-115">Gdy jest używany</span><span class="sxs-lookup"><span data-stu-id="d2cba-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="d2cba-116">INTERNET</span><span class="sxs-lookup"><span data-stu-id="d2cba-116">INTERNET</span></span> |<span data-ttu-id="d2cba-117">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="d2cba-117">Required.</span></span> <span data-ttu-id="d2cba-118">Na podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="d2cba-118">For basic reporting</span></span> |
| <span data-ttu-id="d2cba-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="d2cba-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="d2cba-120">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="d2cba-120">Required.</span></span> <span data-ttu-id="d2cba-121">Na podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="d2cba-121">For basic reporting</span></span> |
| <span data-ttu-id="d2cba-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="d2cba-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="d2cba-123">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="d2cba-123">Required.</span></span> <span data-ttu-id="d2cba-124">tooshow się Centrum powiadomień powitania po ponownym uruchomieniu urządzenia</span><span class="sxs-lookup"><span data-stu-id="d2cba-124">tooshow up hello notifications center after device reboot</span></span> |
| <span data-ttu-id="d2cba-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="d2cba-125">WAKE_LOCK</span></span> |<span data-ttu-id="d2cba-126">Zalecane.</span><span class="sxs-lookup"><span data-stu-id="d2cba-126">Recommended.</span></span> <span data-ttu-id="d2cba-127">Umożliwia zbieranie danych przy użyciu sieci Wi-Fi lub gdy ekran jest wyłączony</span><span class="sxs-lookup"><span data-stu-id="d2cba-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="d2cba-128">WŁĄCZ WIBRACJĘ</span><span class="sxs-lookup"><span data-stu-id="d2cba-128">VIBRATE</span></span> |<span data-ttu-id="d2cba-129">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d2cba-129">Optional.</span></span> <span data-ttu-id="d2cba-130">Włącza wibrację po otrzymaniu powiadomienia</span><span class="sxs-lookup"><span data-stu-id="d2cba-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="d2cba-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="d2cba-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="d2cba-132">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d2cba-132">Optional.</span></span> <span data-ttu-id="d2cba-133">Włącza powiadomień systemu Android duży obraz.</span><span class="sxs-lookup"><span data-stu-id="d2cba-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="d2cba-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="d2cba-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="d2cba-135">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d2cba-135">Optional.</span></span> <span data-ttu-id="d2cba-136">Włącza powiadomień systemu Android duży obraz.</span><span class="sxs-lookup"><span data-stu-id="d2cba-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="d2cba-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="d2cba-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="d2cba-138">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d2cba-138">Optional.</span></span> <span data-ttu-id="d2cba-139">Włącza raportowanie lokalizacji w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="d2cba-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="d2cba-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="d2cba-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="d2cba-141">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d2cba-141">Optional.</span></span> <span data-ttu-id="d2cba-142">Włącza raportowanie oparte na GPS lokalizacji</span><span class="sxs-lookup"><span data-stu-id="d2cba-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="d2cba-143">Począwszy od systemu Android M [niektóre uprawnienia są zarządzane w czasie wykonywania](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="d2cba-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="d2cba-144">Jeśli korzystasz już z ``ACCESS_FINE_LOCATION``, nie potrzebujesz tooalso, a następnie użyć ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="d2cba-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need tooalso use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="d2cba-145">Opcje konfiguracji manifestu systemu android</span><span class="sxs-lookup"><span data-stu-id="d2cba-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="d2cba-146">Raport o awarii</span><span class="sxs-lookup"><span data-stu-id="d2cba-146">Crash report</span></span>
<span data-ttu-id="d2cba-147">Raporty awarii toodisable, Dodaj ten kod między hello `<application>` i `</application>` tagów:</span><span class="sxs-lookup"><span data-stu-id="d2cba-147">toodisable crash reports, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="d2cba-148">Próg serii</span><span class="sxs-lookup"><span data-stu-id="d2cba-148">Burst threshold</span></span>
<span data-ttu-id="d2cba-149">Domyślnie raporty usługi Engagement hello rejestruje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="d2cba-149">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="d2cba-150">Jeśli dzienniki raportu Twojej aplikacji różnią się często, jest lepsze toobuffer hello dzienniki i tooreport ich jednocześnie na regularne podstawy czasu (nazywanych "Tryb szybki").</span><span class="sxs-lookup"><span data-stu-id="d2cba-150">If your application report logs vary frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="d2cba-151">toodo tak, Dodaj ten kod między hello `<application>` i `</application>` tagów:</span><span class="sxs-lookup"><span data-stu-id="d2cba-151">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="d2cba-152">Tryb serii nieco zwiększa hello czas pracy baterii, ale ma wpływ na powitania monitora usługi Engagement: wszystkie czas trwania sesji i zadań są zaokrąglone toohello serii próg (w związku z tym sesji i zadania krótsze niż próg serii hello może nie być widoczna).</span><span class="sxs-lookup"><span data-stu-id="d2cba-152">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="d2cba-153">Próg z serii powinna być dłuższa niż 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="d2cba-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="d2cba-154">Limit czasu sesji</span><span class="sxs-lookup"><span data-stu-id="d2cba-154">Session timeout</span></span>
 <span data-ttu-id="d2cba-155">Działanie może być zakończona przez naciśnięcie przycisku hello **Home** lub **ponownie** klucza przez ustawienie hello phone bezczynności lub przejście do innej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2cba-155">You can end an activity by pressing hello **Home** or **Back** key, by setting hello phone idle or by jumping into another application.</span></span> <span data-ttu-id="d2cba-156">Domyślnie jest zakończenie sesji dziesięć sekund po zakończeniu hello jego ostatniej aktywności.</span><span class="sxs-lookup"><span data-stu-id="d2cba-156">By default, a session is ended ten seconds after hello end of its last activity.</span></span> <span data-ttu-id="d2cba-157">Pozwala to uniknąć podziału sesji każdego użytkownika w czasie hello opuszcza i zwraca aplikacji toohello szybkie, które mogą wystąpić podczas użytkownika hello przejmuje obrazu sprawdza powiadomienia itp. Ten parametr może być toomodify.</span><span class="sxs-lookup"><span data-stu-id="d2cba-157">This avoids a session split each time hello user exits and returns toohello application quickly, which can happen when hello user picks up an image, checks a notification, etc. You may want toomodify this parameter.</span></span> <span data-ttu-id="d2cba-158">toodo tak, Dodaj ten kod między hello `<application>` i `</application>` tagów:</span><span class="sxs-lookup"><span data-stu-id="d2cba-158">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="d2cba-159">Wyłączanie dziennika raportowania</span><span class="sxs-lookup"><span data-stu-id="d2cba-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="d2cba-160">Przy użyciu wywołania metody</span><span class="sxs-lookup"><span data-stu-id="d2cba-160">Using a method call</span></span>
<span data-ttu-id="d2cba-161">Jeśli chcesz toostop zaangażowania wysyłania dzienników, można wywołać:</span><span class="sxs-lookup"><span data-stu-id="d2cba-161">If you want Engagement toostop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="d2cba-162">To wywołanie jest trwały: używa plików udostępnionych preferencji.</span><span class="sxs-lookup"><span data-stu-id="d2cba-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="d2cba-163">Jeśli zaangażowania jest aktywny, gdy wywołanie tej funkcji, może zająć jedną minutę na powitania toostop usługi.</span><span class="sxs-lookup"><span data-stu-id="d2cba-163">If Engagement is active when you call this function, it may take one minute for hello service toostop.</span></span> <span data-ttu-id="d2cba-164">Jednak nie będzie uruchomić usługi hello na wszystkich hello następnym uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d2cba-164">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="d2cba-165">Możesz włączyć ponownie raportowania przez wywołanie metody hello sam działać z dziennika `true`.</span><span class="sxs-lookup"><span data-stu-id="d2cba-165">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="d2cba-166">Integracja z własną`PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="d2cba-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="d2cba-167">Zamiast wywoływania tej funkcji, to ustawienie można również zintegrować bezpośrednio w istniejącą `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="d2cba-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="d2cba-168">Toouse zaangażowania preferencje plików (w trybie żądaną hello) można skonfigurować w hello `AndroidManifest.xml` pliku z `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="d2cba-168">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="d2cba-169">Witaj `engagement:agent:settings:name` klucz to nazwa hello toodefine używanych plików udostępnionych preferencji hello.</span><span class="sxs-lookup"><span data-stu-id="d2cba-169">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="d2cba-170">Witaj `engagement:agent:settings:mode` klucza jest tryb hello toodefine używanych plików udostępnionych preferencji hello.</span><span class="sxs-lookup"><span data-stu-id="d2cba-170">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file.</span></span> <span data-ttu-id="d2cba-171">Użyj hello sam tryb jako w Twojej `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="d2cba-171">Use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="d2cba-172">Tryb Hello muszą być przekazywane w postaci liczby: Jeśli korzystasz z kombinacją flag stałej w kodzie, sprawdź wartość całkowita hello.</span><span class="sxs-lookup"><span data-stu-id="d2cba-172">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="d2cba-173">Zaangażowania zawsze używa hello `engagement:key` logiczna klucz w pliku preferencji hello zarządzania to ustawienie.</span><span class="sxs-lookup"><span data-stu-id="d2cba-173">Engagement always uses hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="d2cba-174">Witaj następujący przykład `AndroidManifest.xml` pokazuje hello wartości domyślne:</span><span class="sxs-lookup"><span data-stu-id="d2cba-174">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="d2cba-175">Następnie można dodać `CheckBoxPreference` w układzie preferencji, takich jak hello jednym następującego:</span><span class="sxs-lookup"><span data-stu-id="d2cba-175">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
