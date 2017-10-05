---
title: Konfiguracja zaawansowana dla zestawem Azure Mobile Engagement Android SDK
description: "W tym artykule opisano opcje konfiguracji zaawansowanej, łącznie z manifestu systemu Android z zestawem Azure Mobile Engagement Android SDK"
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
ms.openlocfilehash: 0301f71c76872714aa1bf727a6c21dd7a63db036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="589a4-103">Konfiguracja zaawansowana dla zestawem Azure Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="589a4-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="589a4-104">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="589a4-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="589a4-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="589a4-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="589a4-106">iOS</span><span class="sxs-lookup"><span data-stu-id="589a4-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="589a4-107">Android</span><span class="sxs-lookup"><span data-stu-id="589a4-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="589a4-108">W tej procedurze opisano sposób konfigurowania różnych opcji konfiguracji dla usługi Azure Mobile Engagement aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="589a4-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="589a4-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="589a4-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="589a4-110">Wymagania dotyczące uprawnień</span><span class="sxs-lookup"><span data-stu-id="589a4-110">Permission Requirements</span></span>
<span data-ttu-id="589a4-111">Niektóre opcje wymaga określonych uprawnień, które są wymienione wszystkie tutaj odwołania i wiersza w określonej funkcji.</span><span class="sxs-lookup"><span data-stu-id="589a4-111">Some options require specific permissions, all of which are listed here for reference, and in-line in the specific feature.</span></span> <span data-ttu-id="589a4-112">Dodaj te uprawnienia do pliku AndroidManifest.xml projektu bezpośrednio przed lub po `<application>` tagu.</span><span class="sxs-lookup"><span data-stu-id="589a4-112">Add these permissions to the AndroidManifest.xml of your project immediately before or after the `<application>` tag.</span></span>

<span data-ttu-id="589a4-113">Kod uprawnień musi wyglądać podobnie do poniższego, w którym Wypełnij odpowiednie uprawnienia z poniższą tabelą.</span><span class="sxs-lookup"><span data-stu-id="589a4-113">The permission code needs to look like the following, where you fill in the appropriate permission from the table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="589a4-114">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="589a4-114">Permission</span></span> | <span data-ttu-id="589a4-115">Gdy jest używany</span><span class="sxs-lookup"><span data-stu-id="589a4-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="589a4-116">INTERNET</span><span class="sxs-lookup"><span data-stu-id="589a4-116">INTERNET</span></span> |<span data-ttu-id="589a4-117">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="589a4-117">Required.</span></span> <span data-ttu-id="589a4-118">Na podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="589a4-118">For basic reporting</span></span> |
| <span data-ttu-id="589a4-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="589a4-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="589a4-120">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="589a4-120">Required.</span></span> <span data-ttu-id="589a4-121">Na podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="589a4-121">For basic reporting</span></span> |
| <span data-ttu-id="589a4-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="589a4-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="589a4-123">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="589a4-123">Required.</span></span> <span data-ttu-id="589a4-124">Wyświetlani Centrum powiadomień po ponownym uruchomieniu urządzenia</span><span class="sxs-lookup"><span data-stu-id="589a4-124">To show up the notifications center after device reboot</span></span> |
| <span data-ttu-id="589a4-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="589a4-125">WAKE_LOCK</span></span> |<span data-ttu-id="589a4-126">Zalecane.</span><span class="sxs-lookup"><span data-stu-id="589a4-126">Recommended.</span></span> <span data-ttu-id="589a4-127">Umożliwia zbieranie danych przy użyciu sieci Wi-Fi lub gdy ekran jest wyłączony</span><span class="sxs-lookup"><span data-stu-id="589a4-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="589a4-128">WŁĄCZ WIBRACJĘ</span><span class="sxs-lookup"><span data-stu-id="589a4-128">VIBRATE</span></span> |<span data-ttu-id="589a4-129">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="589a4-129">Optional.</span></span> <span data-ttu-id="589a4-130">Włącza wibrację po otrzymaniu powiadomienia</span><span class="sxs-lookup"><span data-stu-id="589a4-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="589a4-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="589a4-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="589a4-132">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="589a4-132">Optional.</span></span> <span data-ttu-id="589a4-133">Włącza powiadomień systemu Android duży obraz.</span><span class="sxs-lookup"><span data-stu-id="589a4-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="589a4-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="589a4-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="589a4-135">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="589a4-135">Optional.</span></span> <span data-ttu-id="589a4-136">Włącza powiadomień systemu Android duży obraz.</span><span class="sxs-lookup"><span data-stu-id="589a4-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="589a4-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="589a4-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="589a4-138">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="589a4-138">Optional.</span></span> <span data-ttu-id="589a4-139">Włącza raportowanie lokalizacji w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="589a4-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="589a4-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="589a4-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="589a4-141">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="589a4-141">Optional.</span></span> <span data-ttu-id="589a4-142">Włącza raportowanie oparte na GPS lokalizacji</span><span class="sxs-lookup"><span data-stu-id="589a4-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="589a4-143">Począwszy od systemu Android M [niektóre uprawnienia są zarządzane w czasie wykonywania](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="589a4-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="589a4-144">Jeśli korzystasz już z ``ACCESS_FINE_LOCATION``, a następnie nie należy również użyć ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="589a4-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need to also use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="589a4-145">Opcje konfiguracji manifestu systemu android</span><span class="sxs-lookup"><span data-stu-id="589a4-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="589a4-146">Raport o awarii</span><span class="sxs-lookup"><span data-stu-id="589a4-146">Crash report</span></span>
<span data-ttu-id="589a4-147">Aby wyłączyć raporty awarii, Dodaj ten kod między `<application>` i `</application>` tagów:</span><span class="sxs-lookup"><span data-stu-id="589a4-147">To disable crash reports, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="589a4-148">Próg serii</span><span class="sxs-lookup"><span data-stu-id="589a4-148">Burst threshold</span></span>
<span data-ttu-id="589a4-149">Domyślnie raporty usługi Engagement rejestruje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="589a4-149">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="589a4-150">Jeśli dzienniki raportu Twojej aplikacji różnią się często, lepiej jest buforu dzienniki i raportuj je w całości na regularne podstawy czasu (nazywanych "Tryb szybki").</span><span class="sxs-lookup"><span data-stu-id="589a4-150">If your application report logs vary frequently, it is better to buffer the logs and to report them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="589a4-151">Aby to zrobić, Dodaj ten kod między `<application>` i `</application>` tagów:</span><span class="sxs-lookup"><span data-stu-id="589a4-151">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="589a4-152">Tryb serii nieco zwiększa czas pracy baterii, ale ma wpływ na monitorowanie usługi Engagement: wszystkie czas trwania sesji i zadań są zaokrąglane do serii wartość progową (w związku z tym sesji i zadania krótsze niż próg serii może nie być widoczna).</span><span class="sxs-lookup"><span data-stu-id="589a4-152">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="589a4-153">Próg z serii powinna być dłuższa niż 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="589a4-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="589a4-154">Limit czasu sesji</span><span class="sxs-lookup"><span data-stu-id="589a4-154">Session timeout</span></span>
 <span data-ttu-id="589a4-155">Działanie może być zakończona, naciskając klawisz **Home** lub **ponownie** klucza przez ustawienie bezczynności telefonu lub przejście do innej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="589a4-155">You can end an activity by pressing the **Home** or **Back** key, by setting the phone idle or by jumping into another application.</span></span> <span data-ttu-id="589a4-156">Domyślnie jest zakończenie sesji dziesięć sekund po zakończeniu jego ostatniej aktywności.</span><span class="sxs-lookup"><span data-stu-id="589a4-156">By default, a session is ended ten seconds after the end of its last activity.</span></span> <span data-ttu-id="589a4-157">Pozwala to uniknąć podziału sesji zawsze użytkownik opuszcza i zwraca do aplikacji szybkie, która może wystąpić, gdy użytkownik wybiera obrazu, sprawdza powiadomienia itp. Można modyfikować tego parametru.</span><span class="sxs-lookup"><span data-stu-id="589a4-157">This avoids a session split each time the user exits and returns to the application quickly, which can happen when the user picks up an image, checks a notification, etc. You may want to modify this parameter.</span></span> <span data-ttu-id="589a4-158">Aby to zrobić, Dodaj ten kod między `<application>` i `</application>` tagów:</span><span class="sxs-lookup"><span data-stu-id="589a4-158">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="589a4-159">Wyłączanie dziennika raportowania</span><span class="sxs-lookup"><span data-stu-id="589a4-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="589a4-160">Przy użyciu wywołania metody</span><span class="sxs-lookup"><span data-stu-id="589a4-160">Using a method call</span></span>
<span data-ttu-id="589a4-161">Jeśli chcesz zaangażowania, aby zatrzymać wysyłanie dzienników można wywołać:</span><span class="sxs-lookup"><span data-stu-id="589a4-161">If you want Engagement to stop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="589a4-162">To wywołanie jest trwały: używa plików udostępnionych preferencji.</span><span class="sxs-lookup"><span data-stu-id="589a4-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="589a4-163">Jeśli zaangażowania jest aktywny, gdy wywołanie tej funkcji, może zająć jedną minutę na zatrzymanie usługi.</span><span class="sxs-lookup"><span data-stu-id="589a4-163">If Engagement is active when you call this function, it may take one minute for the service to stop.</span></span> <span data-ttu-id="589a4-164">Jednak go nie Uruchom usługę na wszystkich przy następnym uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="589a4-164">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="589a4-165">Możesz włączyć ponownie raportowania przez wywołanie tej samej funkcji z dziennika `true`.</span><span class="sxs-lookup"><span data-stu-id="589a4-165">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="589a4-166">Integracja z własną`PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="589a4-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="589a4-167">Zamiast wywoływania tej funkcji, to ustawienie można również zintegrować bezpośrednio w istniejącą `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="589a4-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="589a4-168">Zaangażowania, aby użyć pliku preferencji (z odpowiednią tryb) można skonfigurować w `AndroidManifest.xml` pliku z `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="589a4-168">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="589a4-169">`engagement:agent:settings:name` Klucz służy do definiowania nazwę pliku udostępnionych preferencji.</span><span class="sxs-lookup"><span data-stu-id="589a4-169">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="589a4-170">`engagement:agent:settings:mode` Klucz służy do definiowania trybu plików udostępnionych preferencji.</span><span class="sxs-lookup"><span data-stu-id="589a4-170">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file.</span></span> <span data-ttu-id="589a4-171">Użyj tego samego trybu jako w Twojej `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="589a4-171">Use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="589a4-172">Tryb muszą być przekazywane w postaci liczby: Jeśli korzystasz z kombinacją flag stałej w kodzie, sprawdź wartość całkowita.</span><span class="sxs-lookup"><span data-stu-id="589a4-172">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="589a4-173">Zaangażowania zawsze używa `engagement:key` logiczna klucz w pliku preferencji zarządzania to ustawienie.</span><span class="sxs-lookup"><span data-stu-id="589a4-173">Engagement always uses the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="589a4-174">Poniższy przykład przedstawia `AndroidManifest.xml` przedstawiono wartości domyślne:</span><span class="sxs-lookup"><span data-stu-id="589a4-174">The following example of `AndroidManifest.xml` shows the default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="589a4-175">Następnie można dodać `CheckBoxPreference` w układzie preferencji podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="589a4-175">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
