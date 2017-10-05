---
title: "Usługi Azure Mobile Engagement przewodnik - SDK rozwiązywania problemów"
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
ms.openlocfilehash: 4d9d6165deb4bd0c65f1841aa7c457363a1f2865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="b26fd-103">Przewodnik rozwiązywania problemów integracji zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="b26fd-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="b26fd-104">Poniżej przedstawiono możliwe problemy, które mogą się pojawić w sposób integruje aplikacji usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b26fd-104">The following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="b26fd-105">Problemy z zestawu SDK odnalezione awaria w innym miejscu aplikacji</span><span class="sxs-lookup"><span data-stu-id="b26fd-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="b26fd-106">Problem</span><span class="sxs-lookup"><span data-stu-id="b26fd-106">Issue</span></span>
* <span data-ttu-id="b26fd-107">Błąd zbierania danych interfejsu użytkownika (w analizy, monitorowanie, segmentacji lub pulpity).</span><span class="sxs-lookup"><span data-stu-id="b26fd-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="b26fd-108">Wypychanie błędów (Wypchnięć nie działają w aplikacji poza aplikacji lub obie).</span><span class="sxs-lookup"><span data-stu-id="b26fd-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="b26fd-109">Zaawansowane błędy funkcji (śledzenia, używanie funkcji Geolokalizacji lub platformy, którą określonych Wypchnięć nie działają).</span><span class="sxs-lookup"><span data-stu-id="b26fd-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="b26fd-110">Błędy interfejsu API (interfejsy API niepowodzenie często trybie cichym bez komunikaty o błędach).</span><span class="sxs-lookup"><span data-stu-id="b26fd-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="b26fd-111">Awarie usługi (Brak usługi Azure Mobile Engagement działa w przypadku aplikacji).</span><span class="sxs-lookup"><span data-stu-id="b26fd-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="b26fd-112">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="b26fd-112">Causes</span></span>
* <span data-ttu-id="b26fd-113">Błąd w aplikacji (np. Błąd zbierania danych interfejsu użytkownika, Niepowodzenie wypychania, Niepowodzenie zaawansowanych funkcji, błąd interfejsu API, awarii aplikacji lub awaria usługi jawnego) spowoduje odnalezienie większości problemów, które muszą zostać rozpoznane z zestawem Azure Mobile Engagement SDK .</span><span class="sxs-lookup"><span data-stu-id="b26fd-113">Most issues that need to be resolved with the Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="b26fd-114">Jeśli w aplikacji przed nigdy nie działał poszczególnych funkcji usługi Azure Mobile Engagement, należy ukończyć integracji.</span><span class="sxs-lookup"><span data-stu-id="b26fd-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need to complete the integration.</span></span> 
* <span data-ttu-id="b26fd-115">Jeśli poszczególnych funkcji usługi Azure Mobile Engagement pracy i zatrzymanie, może być konieczne uaktualnienie do ostatniej wersji z zestawem Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="b26fd-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need to upgrade to the last version with the Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="b26fd-116">Należy pamiętać, że jest inna wersja zestawem Azure Mobile Engagement SDK dla każdej platformy obsługiwane przez usługi Azure Mobile Engagement (Android, iOS, Windows i Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="b26fd-116">Remember that there is a different version of the Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="b26fd-117">Integracja z zestawem SDK</span><span class="sxs-lookup"><span data-stu-id="b26fd-117">SDK Integration</span></span>
* <span data-ttu-id="b26fd-118">Usługa Azure Mobile Engagement prawidłowo zintegrowane w zestawie SDK (Analytics).</span><span class="sxs-lookup"><span data-stu-id="b26fd-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="b26fd-119">Łączność prawidłowo zintegrowany zestaw SDK (w aplikacji i poza wypchnięcia aplikacji).</span><span class="sxs-lookup"><span data-stu-id="b26fd-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="b26fd-120">Certyfikat wygasły lub niepoprawne vs produkcyjną. Deweloperów (tylko iOS).</span><span class="sxs-lookup"><span data-stu-id="b26fd-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="b26fd-121">GCM lub ADM prawidłowo zintegrowany zestaw SDK (Android tylko — usługa określonych wypchnięcia).</span><span class="sxs-lookup"><span data-stu-id="b26fd-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="b26fd-122">Śledzenie prawidłowo zintegrowane w zestawie SDK (magazyn instalacji śledzenia).</span><span class="sxs-lookup"><span data-stu-id="b26fd-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="b26fd-123">Opóźnieniem lokalizacji lub lokalizacji GPS prawidłowo zintegrowane w zestawie SDK (docelowych według lokalizacji geograficznej).</span><span class="sxs-lookup"><span data-stu-id="b26fd-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="b26fd-124">**Zobacz też:**</span><span class="sxs-lookup"><span data-stu-id="b26fd-124">**See also:**</span></span>

* <span data-ttu-id="b26fd-125">[Dokumentacja zestawu SDK — przewodniki integracji][Link 5]</span><span class="sxs-lookup"><span data-stu-id="b26fd-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="b26fd-126">[Przewodnik rozwiązywania problemów - wypychania][Link 23]</span><span class="sxs-lookup"><span data-stu-id="b26fd-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="b26fd-127">Uaktualnianie zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="b26fd-127">SDK Upgrade</span></span>
* <span data-ttu-id="b26fd-128">Należy uaktualnić zestaw SDK, aby rozwiązać problemy ze starszymi wersjami SDK (często powiązane do nowszej wersji systemu operacyjnego urządzenia).</span><span class="sxs-lookup"><span data-stu-id="b26fd-128">Need to upgrade SDK to resolve issues with older versions of the SDK (often related to newer versions of the device OS).</span></span>
* <span data-ttu-id="b26fd-129">Odinstaluj wszystkie wcześniejsze wersje aplikacji z urządzenia, a następnie zainstaluj ponownie najnowszą wersję aplikacji, ponownie zarejestrować identyfikator urządzenia z usługi Azure Mobile Engagement interfejsu użytkownika aby upewnić się, że urządzenie jest używana najnowsza wersja aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b26fd-129">Uninstall all previous versions of your app from your device and reinstall the newest version of your app, the re-register your Device ID from the Azure Mobile Engagement UI to confirm that your device is using the newest version of your app.</span></span>

<span data-ttu-id="b26fd-130">**Zobacz też:**</span><span class="sxs-lookup"><span data-stu-id="b26fd-130">**See also:**</span></span>

* [<span data-ttu-id="b26fd-131">Dokumentacja zestawu SDK — informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="b26fd-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="b26fd-132">Dokumentacja zestawu SDK — przewodniki uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="b26fd-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="b26fd-133">Zestaw SDK innych</span><span class="sxs-lookup"><span data-stu-id="b26fd-133">SDK Other</span></span>
* <span data-ttu-id="b26fd-134">Błędy w manifeście aplikacji "AndroidManifest.xml" może spowodować usługi Azure Mobile Engagement nie będą działać (tylko Android).</span><span class="sxs-lookup"><span data-stu-id="b26fd-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not to work (Android only).</span></span>
* <span data-ttu-id="b26fd-135">Typowym problemem z integracji zestawu SDK i użycia interfejsu API jest mylenie klucza zestawu SDK i klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b26fd-135">A common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>

<span data-ttu-id="b26fd-136">**Zobacz też:**</span><span class="sxs-lookup"><span data-stu-id="b26fd-136">**See also:**</span></span>

* <span data-ttu-id="b26fd-137">[Pojęcia — słownik][Link 6]</span><span class="sxs-lookup"><span data-stu-id="b26fd-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="b26fd-138">Zaawansowane kodowania problemów</span><span class="sxs-lookup"><span data-stu-id="b26fd-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="b26fd-139">Problem</span><span class="sxs-lookup"><span data-stu-id="b26fd-139">Issue</span></span>
* <span data-ttu-id="b26fd-140">Określony kod platformy niepowiązane bezpośrednio z usługi Azure Mobile Engagement mogą powodować problemy w systemie iOS, Android i Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="b26fd-140">Platform specific code not directly related to Azure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="b26fd-141">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="b26fd-141">Causes</span></span>
* <span data-ttu-id="b26fd-142">Wiele zaawansowanych kodowania problemy z usługi Azure Mobile Engagement są spowodowane przez niepoprawnie napisane platformy kod niepowiązane bezpośrednio z usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b26fd-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related to Azure Mobile Engagement.</span></span> <span data-ttu-id="b26fd-143">Należy zapoznać się z dokumentacją specyficzną dla używanej platformy, które tworzysz dla oprócz dokumentacji usługi Azure Mobile Engagement (Android, iOS, sieci Web, Windows i Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="b26fd-143">You will need to consult documentation specific to the platform you are developing for in addition to Azure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="b26fd-144">Konfigurowanie prawidłowo "kategorie", uniemożliwia łączenie z powiadomienie do innej lokalizacji wewnątrz lub na zewnątrz aplikacji (tylko Android).</span><span class="sxs-lookup"><span data-stu-id="b26fd-144">Not correctly configuring "categories", prevents linking from a notification to another location either inside or outside of the app (Android only).</span></span> 
* <span data-ttu-id="b26fd-145">To ustawienie nie zostanie "UIKit.framework" "opcjonalne" w kodzie systemu iOS pokazuje "Błąd: nie odnaleziono symbolu" i/lub ulega awarii na starszych urządzeń z systemem iOS (tylko iOS).</span><span class="sxs-lookup"><span data-stu-id="b26fd-145">Not setting "UIKit.framework" to "optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="b26fd-146">Wygasłe certyfikaty lub prawidłowo przy użyciu wersji Programistycznych lub produkcyjną CERT przyczyny problemów wypychania (tylko iOS).</span><span class="sxs-lookup"><span data-stu-id="b26fd-146">Expired certificates or not correctly using the DEV or Prod version of the cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="b26fd-147">Istnieją pewne ograniczenia wbudowane w platformę Azure Mobile Engagement nie może kontrolować (tak jak wypycha działania programu system center dla aplikacji w systemach Android i iOS).</span><span class="sxs-lookup"><span data-stu-id="b26fd-147">There are some limitations inherent to a platform that Azure Mobile Engagement can't control (like how the system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="b26fd-148">Usługa Azure Mobile Engagement publikuje pełną listę pakietów wewnętrzny używany przez usługi Azure Mobile Engagement dla systemów iOS i Android odwołania.</span><span class="sxs-lookup"><span data-stu-id="b26fd-148">Azure Mobile Engagement publishes a full list of the internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="b26fd-149">Należy pamiętać, że niektóre funkcje usługi Azure Mobile Engagement są specyficzne dla platformy (Android, iOS, sieci Web, Windows i Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="b26fd-149">Keep in mind that some features of Azure Mobile Engagement are specific to the platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="b26fd-150">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b26fd-150">See also</span></span>
* <span data-ttu-id="b26fd-151">[Przewodnik rozwiązywania problemów - wypychania][Link 23]</span><span class="sxs-lookup"><span data-stu-id="b26fd-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="b26fd-152">[Dokumentacja zestawu SDK — informacje o wersji][Link 5]</span><span class="sxs-lookup"><span data-stu-id="b26fd-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="b26fd-153">[Dokumentacja zestawu SDK — przewodniki uaktualnienia][Link 5]</span><span class="sxs-lookup"><span data-stu-id="b26fd-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="b26fd-154">Awarii aplikacji</span><span class="sxs-lookup"><span data-stu-id="b26fd-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="b26fd-155">Problem</span><span class="sxs-lookup"><span data-stu-id="b26fd-155">Issue</span></span>
* <span data-ttu-id="b26fd-156">Aplikacja przestaje działać na urządzeniu użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="b26fd-156">Your application crashes on the end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="b26fd-157">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="b26fd-157">Causes</span></span>
* <span data-ttu-id="b26fd-158">Informacje o awarii można wyświetlić w *interfejsu użytkownika analizy* lub *analizy interfejsu API*</span><span class="sxs-lookup"><span data-stu-id="b26fd-158">Crash information can be viewed in the *Analytics UI* or the *Analytics API*</span></span>
* <span data-ttu-id="b26fd-159">Można znaleźć Identyfikatora urządzenia urządzenia testu i wykonać tę samą akcję, który spowodował awarię aplikacji dla użytkownika końcowego ułatwić identyfikację przyczyny awarii sieci.</span><span class="sxs-lookup"><span data-stu-id="b26fd-159">You can find the Device ID of your test device and take the same action that caused your application to crash for an end user to help identify the cause of your crash.</span></span>
* <span data-ttu-id="b26fd-160">Znane problemy z zestawem Azure Mobile Engagement SDK, które aplikacje awarii są czasami rozwiązać przez uaktualnienie do najnowszej wersji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="b26fd-160">Known issues with the Azure Mobile Engagement SDK that cause applications to crash are sometimes resolved by upgrading to the latest version of the SDK.</span></span> <span data-ttu-id="b26fd-161">Upewnij się, że podczas badania awarii (Crash), sprawdź informacje o wersji dotyczące platformy.</span><span class="sxs-lookup"><span data-stu-id="b26fd-161">Make sure to check the release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="b26fd-162">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b26fd-162">See also</span></span>
* <span data-ttu-id="b26fd-163">[Dokumentacja zestawu SDK — informacje o wersji][Link 5]</span><span class="sxs-lookup"><span data-stu-id="b26fd-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="b26fd-164">[Dokumentacja zestawu SDK — przewodniki uaktualnienia][Link 5]</span><span class="sxs-lookup"><span data-stu-id="b26fd-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="b26fd-165">Aplikacji sklepu przekazywania błędów</span><span class="sxs-lookup"><span data-stu-id="b26fd-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="b26fd-166">Problem</span><span class="sxs-lookup"><span data-stu-id="b26fd-166">Issue</span></span>
* <span data-ttu-id="b26fd-167">Błędy związane z przekazaniem najnowszą wersję aplikacji do sklepu z aplikacjami systemu Windows firmy Apple lub Google.</span><span class="sxs-lookup"><span data-stu-id="b26fd-167">Errors related to uploading the latest version of your app to Apple, Google, or the Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="b26fd-168">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="b26fd-168">Causes</span></span>
* <span data-ttu-id="b26fd-169">Aplikacja przechowuje czasami blok aplikacje z niektórych z włączonymi funkcjami (np. sklepu Apple zapobiega użyciu IDFV aplikacji w magazynie i magazynu GooglePlay uniemożliwia udostępnianie informacji o aplikacji między aplikacjami).</span><span class="sxs-lookup"><span data-stu-id="b26fd-169">App stores sometimes block apps with certain features enabled (e.g. the Apple Store prevents the use of IDFV in apps in the store and the GooglePlay store prevents the sharing of application information between apps).</span></span> 
* <span data-ttu-id="b26fd-170">Upewnij się, sprawdź informacje o wersji dotyczące platformy i bieżącej wersji zestawu SDK, jeśli masz trudności przekazywania aplikacji do sklepu.</span><span class="sxs-lookup"><span data-stu-id="b26fd-170">Make sure that you check the release notes about your platform and current version of the SDK if you have difficulty uploading an app to the store.</span></span>

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

