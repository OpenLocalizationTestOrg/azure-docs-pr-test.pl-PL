---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
description: "Rozwiązywanie problemów integracji zestawu SDK usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="0a92d-103">Przewodnik rozwiązywania problemów integracji zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="0a92d-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="0a92d-104">Witaj poniżej przedstawiono możliwe problemy, które mogą się pojawić w sposób integruje aplikacji usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="0a92d-104">hello following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="0a92d-105">Problemy z zestawu SDK odnalezione awaria w innym miejscu aplikacji</span><span class="sxs-lookup"><span data-stu-id="0a92d-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="0a92d-106">Problem</span><span class="sxs-lookup"><span data-stu-id="0a92d-106">Issue</span></span>
* <span data-ttu-id="0a92d-107">Błąd zbierania danych interfejsu użytkownika (w analizy, monitorowanie, segmentacji lub pulpity).</span><span class="sxs-lookup"><span data-stu-id="0a92d-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="0a92d-108">Wypychanie błędów (Wypchnięć nie działają w aplikacji poza aplikacji lub obie).</span><span class="sxs-lookup"><span data-stu-id="0a92d-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="0a92d-109">Zaawansowane błędy funkcji (śledzenia, używanie funkcji Geolokalizacji lub platformy, którą określonych Wypchnięć nie działają).</span><span class="sxs-lookup"><span data-stu-id="0a92d-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="0a92d-110">Błędy interfejsu API (interfejsy API niepowodzenie często trybie cichym bez komunikaty o błędach).</span><span class="sxs-lookup"><span data-stu-id="0a92d-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="0a92d-111">Awarie usługi (Brak usługi Azure Mobile Engagement działa w przypadku aplikacji).</span><span class="sxs-lookup"><span data-stu-id="0a92d-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="0a92d-112">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="0a92d-112">Causes</span></span>
* <span data-ttu-id="0a92d-113">Błąd w aplikacji (na przykład błąd zbierania danych interfejsu użytkownika, Niepowodzenie wypychania, Niepowodzenie zaawansowanych funkcji, błąd interfejsu API, awarii aplikacji lub usługi jawnego spowoduje odnalezienie większości problemów, które trzeba toobe został rozwiązany za pomocą hello zestaw SDK usługi Azure Mobile Engagement awarii).</span><span class="sxs-lookup"><span data-stu-id="0a92d-113">Most issues that need toobe resolved with hello Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="0a92d-114">Jeśli w aplikacji przed nigdy nie działał poszczególnych funkcji usługi Azure Mobile Engagement, należy toocomplete hello integracji.</span><span class="sxs-lookup"><span data-stu-id="0a92d-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need toocomplete hello integration.</span></span> 
* <span data-ttu-id="0a92d-115">Jeśli poszczególnych funkcji usługi Azure Mobile Engagement pracy i zatrzymanie, może być konieczne tooupgrade toohello ostatniej wersji z hello zestaw SDK usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="0a92d-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need tooupgrade toohello last version with hello Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="0a92d-116">Należy pamiętać, że jest inna wersja hello Azure Mobile Engagement SDK dla każdej platformy obsługiwane przez usługi Azure Mobile Engagement (Android, iOS, Windows i Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="0a92d-116">Remember that there is a different version of hello Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="0a92d-117">Integracja z zestawem SDK</span><span class="sxs-lookup"><span data-stu-id="0a92d-117">SDK Integration</span></span>
* <span data-ttu-id="0a92d-118">Usługa Azure Mobile Engagement prawidłowo zintegrowane w zestawie SDK (Analytics).</span><span class="sxs-lookup"><span data-stu-id="0a92d-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="0a92d-119">Łączność prawidłowo zintegrowany zestaw SDK (w aplikacji i poza wypchnięcia aplikacji).</span><span class="sxs-lookup"><span data-stu-id="0a92d-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="0a92d-120">Certyfikat wygasły lub niepoprawne vs produkcyjną. Deweloperów (tylko iOS).</span><span class="sxs-lookup"><span data-stu-id="0a92d-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="0a92d-121">GCM lub ADM prawidłowo zintegrowany zestaw SDK (Android tylko — usługa określonych wypchnięcia).</span><span class="sxs-lookup"><span data-stu-id="0a92d-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="0a92d-122">Śledzenie prawidłowo zintegrowane w zestawie SDK (magazyn instalacji śledzenia).</span><span class="sxs-lookup"><span data-stu-id="0a92d-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="0a92d-123">Opóźnieniem lokalizacji lub lokalizacji GPS prawidłowo zintegrowane w zestawie SDK (docelowych według lokalizacji geograficznej).</span><span class="sxs-lookup"><span data-stu-id="0a92d-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="0a92d-124">**Zobacz też:**</span><span class="sxs-lookup"><span data-stu-id="0a92d-124">**See also:**</span></span>

* <span data-ttu-id="0a92d-125">[Dokumentacja zestawu SDK — przewodniki integracji][Link 5]</span><span class="sxs-lookup"><span data-stu-id="0a92d-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="0a92d-126">[Przewodnik rozwiązywania problemów - wypychania][Link 23]</span><span class="sxs-lookup"><span data-stu-id="0a92d-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="0a92d-127">Uaktualnianie zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="0a92d-127">SDK Upgrade</span></span>
* <span data-ttu-id="0a92d-128">Należy tooupgrade SDK tooresolve problemy ze starszymi wersjami hello SDK (często powiązane toonewer wersje systemu operacyjnego urządzenia hello).</span><span class="sxs-lookup"><span data-stu-id="0a92d-128">Need tooupgrade SDK tooresolve issues with older versions of hello SDK (often related toonewer versions of hello device OS).</span></span>
* <span data-ttu-id="0a92d-129">Odinstaluj wszystkie wcześniejsze wersje aplikacji z urządzenia i zainstaluj ponownie najnowszą wersję aplikacji hello, hello ponownie zarejestrować identyfikator urządzenia z hello Azure Mobile Engagement UI tooconfirm urządzenie używa hello najnowszej wersji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a92d-129">Uninstall all previous versions of your app from your device and reinstall hello newest version of your app, hello re-register your Device ID from hello Azure Mobile Engagement UI tooconfirm that your device is using hello newest version of your app.</span></span>

<span data-ttu-id="0a92d-130">**Zobacz też:**</span><span class="sxs-lookup"><span data-stu-id="0a92d-130">**See also:**</span></span>

* [<span data-ttu-id="0a92d-131">Dokumentacja zestawu SDK — informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="0a92d-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="0a92d-132">Dokumentacja zestawu SDK — przewodniki uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="0a92d-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="0a92d-133">Zestaw SDK innych</span><span class="sxs-lookup"><span data-stu-id="0a92d-133">SDK Other</span></span>
* <span data-ttu-id="0a92d-134">Błędy w manifeście aplikacji "AndroidManifest.xml" może spowodować usługi Azure Mobile Engagement toowork (tylko Android).</span><span class="sxs-lookup"><span data-stu-id="0a92d-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not toowork (Android only).</span></span>
* <span data-ttu-id="0a92d-135">Typowym problemem z integracji zestawu SDK i użycia interfejsu API jest tooconfuse hello klucza zestawu SDK i hello klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="0a92d-135">A common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>

<span data-ttu-id="0a92d-136">**Zobacz też:**</span><span class="sxs-lookup"><span data-stu-id="0a92d-136">**See also:**</span></span>

* <span data-ttu-id="0a92d-137">[Pojęcia — słownik][Link 6]</span><span class="sxs-lookup"><span data-stu-id="0a92d-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="0a92d-138">Zaawansowane kodowania problemów</span><span class="sxs-lookup"><span data-stu-id="0a92d-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="0a92d-139">Problem</span><span class="sxs-lookup"><span data-stu-id="0a92d-139">Issue</span></span>
* <span data-ttu-id="0a92d-140">Kod platformy nie bezpośrednio powiązane tooAzure Mobile Engagement może spowodować problemy w systemie iOS, Android i Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="0a92d-140">Platform specific code not directly related tooAzure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="0a92d-141">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="0a92d-141">Causes</span></span>
* <span data-ttu-id="0a92d-142">Wiele zaawansowanych kodowania problemy z usługi Azure Mobile Engagement są spowodowane przez niepoprawnie napisane platformy określony kod nie są bezpośrednio związane z tooAzure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="0a92d-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related tooAzure Mobile Engagement.</span></span> <span data-ttu-id="0a92d-143">Konieczne będzie tooconsult dokumentacji toohello określonych platform opracowywanej dla dodatkowo dokumentacji usługi Mobile Engagement tooAzure (Android, iOS, sieci Web, Windows i Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="0a92d-143">You will need tooconsult documentation specific toohello platform you are developing for in addition tooAzure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="0a92d-144">Konfigurowanie prawidłowo "kategorie", uniemożliwia łączenie z lokalizacji tooanother powiadomień wewnątrz lub na zewnątrz aplikacji hello (tylko Android).</span><span class="sxs-lookup"><span data-stu-id="0a92d-144">Not correctly configuring "categories", prevents linking from a notification tooanother location either inside or outside of hello app (Android only).</span></span> 
* <span data-ttu-id="0a92d-145">To ustawienie nie zostanie "UIKit.framework" za "opcjonalne" w kodzie systemu iOS pokazuje "Błąd: nie odnaleziono symbolu" i/lub ulega awarii na starszych urządzeń z systemem iOS (tylko iOS).</span><span class="sxs-lookup"><span data-stu-id="0a92d-145">Not setting "UIKit.framework" too"optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="0a92d-146">Wygasłe certyfikaty lub prawidłowo przy użyciu hello deweloperów lub wersję produkcyjną hello certyfikatu, wypychania przyczyny problemów (tylko iOS).</span><span class="sxs-lookup"><span data-stu-id="0a92d-146">Expired certificates or not correctly using hello DEV or Prod version of hello cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="0a92d-147">Brak niektórych platforma związanego z używaniem tooa ograniczenia usługi Azure Mobile Engagement nie może kontrolować (tak jak wypycha działania hello system center dla aplikacji w systemach Android i iOS).</span><span class="sxs-lookup"><span data-stu-id="0a92d-147">There are some limitations inherent tooa platform that Azure Mobile Engagement can't control (like how hello system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="0a92d-148">Usługa Azure Mobile Engagement publikuje pełną listę hello pakietów wewnętrzny używany przez usługi Azure Mobile Engagement dla systemów iOS i Android odwołania.</span><span class="sxs-lookup"><span data-stu-id="0a92d-148">Azure Mobile Engagement publishes a full list of hello internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="0a92d-149">Należy pamiętać, że niektóre funkcje usługi Azure Mobile Engagement są toohello określonych platform (Android, iOS, sieci Web, Windows i Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="0a92d-149">Keep in mind that some features of Azure Mobile Engagement are specific toohello platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="0a92d-150">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="0a92d-150">See also</span></span>
* <span data-ttu-id="0a92d-151">[Przewodnik rozwiązywania problemów - wypychania][Link 23]</span><span class="sxs-lookup"><span data-stu-id="0a92d-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="0a92d-152">[Dokumentacja zestawu SDK — informacje o wersji][Link 5]</span><span class="sxs-lookup"><span data-stu-id="0a92d-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="0a92d-153">[Dokumentacja zestawu SDK — przewodniki uaktualnienia][Link 5]</span><span class="sxs-lookup"><span data-stu-id="0a92d-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="0a92d-154">Awarii aplikacji</span><span class="sxs-lookup"><span data-stu-id="0a92d-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="0a92d-155">Problem</span><span class="sxs-lookup"><span data-stu-id="0a92d-155">Issue</span></span>
* <span data-ttu-id="0a92d-156">Na urządzeniach użytkowników końcowych hello ulega awarii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a92d-156">Your application crashes on hello end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="0a92d-157">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="0a92d-157">Causes</span></span>
* <span data-ttu-id="0a92d-158">Informacje o awarii można wyświetlić w hello *interfejsu użytkownika analizy* lub hello *analizy interfejsu API*</span><span class="sxs-lookup"><span data-stu-id="0a92d-158">Crash information can be viewed in hello *Analytics UI* or hello *Analytics API*</span></span>
* <span data-ttu-id="0a92d-159">Witaj identyfikator urządzenia urządzenia testu i podjąć hello można znaleźć tę samą akcję, która spowodowała toocrash Twojej aplikacji dla użytkownika końcowego toohelp zidentyfikować hello przyczynę awarii sieci.</span><span class="sxs-lookup"><span data-stu-id="0a92d-159">You can find hello Device ID of your test device and take hello same action that caused your application toocrash for an end user toohelp identify hello cause of your crash.</span></span>
* <span data-ttu-id="0a92d-160">Znane problemy z hello Azure Mobile Engagement SDK, które powodują toocrash aplikacji są czasami rozwiązać przez uaktualnienie toohello najnowszą wersję hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="0a92d-160">Known issues with hello Azure Mobile Engagement SDK that cause applications toocrash are sometimes resolved by upgrading toohello latest version of hello SDK.</span></span> <span data-ttu-id="0a92d-161">Podczas badania awarii (Crash), upewnij się, że toocheck hello informacje o wersji dotyczące platformy.</span><span class="sxs-lookup"><span data-stu-id="0a92d-161">Make sure toocheck hello release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="0a92d-162">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="0a92d-162">See also</span></span>
* <span data-ttu-id="0a92d-163">[Dokumentacja zestawu SDK — informacje o wersji][Link 5]</span><span class="sxs-lookup"><span data-stu-id="0a92d-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="0a92d-164">[Dokumentacja zestawu SDK — przewodniki uaktualnienia][Link 5]</span><span class="sxs-lookup"><span data-stu-id="0a92d-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="0a92d-165">Aplikacji sklepu przekazywania błędów</span><span class="sxs-lookup"><span data-stu-id="0a92d-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="0a92d-166">Problem</span><span class="sxs-lookup"><span data-stu-id="0a92d-166">Issue</span></span>
* <span data-ttu-id="0a92d-167">Błędy związane z toouploading hello najnowszą wersję aplikacji tooApple, Google lub sklepu z aplikacjami systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0a92d-167">Errors related toouploading hello latest version of your app tooApple, Google, or hello Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="0a92d-168">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="0a92d-168">Causes</span></span>
* <span data-ttu-id="0a92d-169">Aplikacja przechowuje czasami blok aplikacje z niektórych z włączonymi funkcjami (np. hello sklepu Apple uniemożliwia użycie hello IDFV w aplikacjach w sklepie hello i uniemożliwia magazynu GooglePlay hello hello udostępnianie informacji o aplikacji między aplikacjami).</span><span class="sxs-lookup"><span data-stu-id="0a92d-169">App stores sometimes block apps with certain features enabled (e.g. hello Apple Store prevents hello use of IDFV in apps in hello store and hello GooglePlay store prevents hello sharing of application information between apps).</span></span> 
* <span data-ttu-id="0a92d-170">Upewnij się, sprawdź hello informacje o wersji dotyczące platformy i bieżącej wersji zestawu SDK hello, jeśli masz trudności przekazywania toohello sklepu z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="0a92d-170">Make sure that you check hello release notes about your platform and current version of hello SDK if you have difficulty uploading an app toohello store.</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

