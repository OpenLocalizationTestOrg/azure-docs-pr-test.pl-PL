---
title: "aaaTroubleshoot analizy w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Problemy z analizy usługi Application Insights? Zacznij tutaj. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="aaf00-104">Rozwiązywanie problemów z analizą w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="aaf00-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="aaf00-105">Problemy z [Application Insights Analytics](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="aaf00-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="aaf00-106">Zacznij tutaj.</span><span class="sxs-lookup"><span data-stu-id="aaf00-106">Start here.</span></span> <span data-ttu-id="aaf00-107">Analytics to narzędzie wyszukiwania zaawansowanego hello Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aaf00-107">Analytics is hello powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="aaf00-108">Limity</span><span class="sxs-lookup"><span data-stu-id="aaf00-108">Limits</span></span>
* <span data-ttu-id="aaf00-109">Obecnie wyniki zapytania są ograniczone toojust dłużej niż przez tydzień w ciągu ostatnich danych.</span><span class="sxs-lookup"><span data-stu-id="aaf00-109">At present, query results are limited toojust over a week of past data.</span></span>
* <span data-ttu-id="aaf00-110">Firma Microsoft testuje w przeglądarkach: najnowsze wersje programu Chrome, Edge i przeglądarki Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="aaf00-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="aaf00-111">Rozszerzenia znanych niezgodne przeglądarki</span><span class="sxs-lookup"><span data-stu-id="aaf00-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="aaf00-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="aaf00-112">Ghostery</span></span>

<span data-ttu-id="aaf00-113">Wyłącz rozszerzenia hello, lub użyj innej przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="aaf00-113">Disable hello extension or use a different browser.</span></span>

## <span data-ttu-id="aaf00-114"><a name="e-a"></a>"Nieoczekiwany błąd"</span><span class="sxs-lookup"><span data-stu-id="aaf00-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Wystąpił nieoczekiwany błąd ekranu](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="aaf00-116">Wystąpił błąd wewnętrzny podczas wykonywania portalu — nieobsługiwany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="aaf00-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="aaf00-117">Czyszczenie pamięci podręcznej przeglądarki hello.</span><span class="sxs-lookup"><span data-stu-id="aaf00-117">Clean hello browser's cache.</span></span> 

## <span data-ttu-id="aaf00-118"><a name="e-b"></a>403... Spróbuj tooreload</span><span class="sxs-lookup"><span data-stu-id="aaf00-118"><a name="e-b"></a>403 ... please try tooreload</span></span>
![403... Spróbuj tooreload](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="aaf00-120">Wystąpił błąd (podczas uwierzytelniania lub podczas generowania tokenu dostępu) związanych z uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="aaf00-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="aaf00-121">Hello portal może nie ma możliwości zbyt odzyskać bez zmiany ustawienia przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="aaf00-121">hello portal may have no way too recover without changing browser settings.</span></span>

* <span data-ttu-id="aaf00-122">Sprawdź [pliki cookie innych firm są włączone](#cookies) w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="aaf00-122">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 

## <span data-ttu-id="aaf00-123"><a name="authentication"></a>403... Sprawdź strefy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="aaf00-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403.. podjęciem ponownej próby upewnij strefy zabezpieczeń](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="aaf00-125">Wystąpił błąd (podczas uwierzytelniania lub podczas generowania tokenu dostępu) związanych z uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="aaf00-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="aaf00-126">Hello portal może nie ma możliwości zbyt odzyskać bez zmiany ustawienia przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="aaf00-126">hello portal may have no way too recover without changing browser settings.</span></span>

1. <span data-ttu-id="aaf00-127">Sprawdź [pliki cookie innych firm są włączone](#cookies) w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="aaf00-127">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 
2. <span data-ttu-id="aaf00-128">Czy użyto Ulubione, zakładki lub portal analityka hello tooopen zapisane łącze?</span><span class="sxs-lookup"><span data-stu-id="aaf00-128">Did you use a favorite, bookmark or saved link tooopen hello Analytics portal?</span></span> <span data-ttu-id="aaf00-129">Zalogowano się przy użyciu innych poświadczeń niż użyte podczas zapisywania hello łącze?</span><span class="sxs-lookup"><span data-stu-id="aaf00-129">Are you signed in with different credentials than you used when you saved hello link?</span></span>
3. <span data-ttu-id="aaf00-130">Spróbuj użyć okna przeglądarki w prywatnego/incognito (po zamknięciu wszystkich tych okien).</span><span class="sxs-lookup"><span data-stu-id="aaf00-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="aaf00-131">Tooprovide będziesz mieć swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="aaf00-131">You'll have tooprovide your credentials.</span></span> 
4. <span data-ttu-id="aaf00-132">Otwiera inne okno przeglądarki (zwykłej) i przejdź zbyt[Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aaf00-132">Open another (ordinary) browser window and go too[Azure](https://portal.azure.com).</span></span> <span data-ttu-id="aaf00-133">Wyloguj. Następnie otwórz łącze i zaloguj się przy użyciu hello poprawne poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="aaf00-133">Sign out. Then open your link and sign in with hello correct credentials.</span></span>
5. <span data-ttu-id="aaf00-134">Użytkownicy Edge i przeglądarki Internet Explorer można również uzyskać ten błąd, gdy ustawienia zaufanej strefy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="aaf00-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="aaf00-135">Sprawdź zarówno [portal analityka](https://analytics.applicationinsights.io) i [portalu usługi Azure Active Directory](https://portal.azure.com) w hello tej samej strefie zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="aaf00-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in hello same security zone:</span></span>
   
   * <span data-ttu-id="aaf00-136">W programie Internet Explorer Otwórz **Opcje internetowe**, **zabezpieczeń**, **Zaufane witryny**, **witryny**:</span><span class="sxs-lookup"><span data-stu-id="aaf00-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Okno dialogowe Opcje internetowe, dodanie lokacji tooTrusted witryn](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="aaf00-138">Hello listy witryn sieci Web, jeśli którekolwiek z hello następujące adresy URL są uwzględnione, upewnij się, że hello inne są uwzględniane:</span><span class="sxs-lookup"><span data-stu-id="aaf00-138">In hello Websites list, if any of hello following URLs are included, make sure that hello others are included also:</span></span>
     
     <span data-ttu-id="aaf00-139">https://Analytics.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="aaf00-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="aaf00-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="aaf00-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="aaf00-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="aaf00-141">https://login.windows.net</span></span>

## <span data-ttu-id="aaf00-142"><a name="e-d"></a>404 ... Nie znaleziono zasobu</span><span class="sxs-lookup"><span data-stu-id="aaf00-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404... nie można odnaleźć zasobu](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="aaf00-144">Zasób aplikacji została usunięta z usługi Application Insights i nie jest już dostępny.</span><span class="sxs-lookup"><span data-stu-id="aaf00-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="aaf00-145">Może to nastąpić po zapisaniu hello adresu URL toohello analizy strony.</span><span class="sxs-lookup"><span data-stu-id="aaf00-145">This can happen if you saved hello URL toohello Analytics page.</span></span>

## <span data-ttu-id="aaf00-146"><a name="e-e"></a>403 ... Brak autoryzacji</span><span class="sxs-lookup"><span data-stu-id="aaf00-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403... nieautoryzowane](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="aaf00-148">Nie masz uprawnień tooopen tej aplikacji w module analiz.</span><span class="sxs-lookup"><span data-stu-id="aaf00-148">You don't have permission tooopen this application in Analytics.</span></span>

* <span data-ttu-id="aaf00-149">Czy został wyświetlony link powitania od kogoś innego</span><span class="sxs-lookup"><span data-stu-id="aaf00-149">Did you get hello link from someone else?</span></span> <span data-ttu-id="aaf00-150">Poproś toomake się, że jesteś w hello [czytniki lub współautorzy dla tej grupy zasobów](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="aaf00-150">Ask them toomake sure you are in hello [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="aaf00-151">Został zapisany przy użyciu innych poświadczeń łącze hello?</span><span class="sxs-lookup"><span data-stu-id="aaf00-151">Did you save hello link using different credentials?</span></span> <span data-ttu-id="aaf00-152">Otwórz hello [portalu Azure](https://portal.azure.com), wyloguj się, a następnie spróbuj to łącze ponownie, podając hello poprawne poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="aaf00-152">Open hello [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing hello correct credentials.</span></span>

## <span data-ttu-id="aaf00-153"><a name="html-storage"></a>403 ... Magazyn HTML5</span><span class="sxs-lookup"><span data-stu-id="aaf00-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="aaf00-154">Portalu używa HTML5 localStorage i sessionStorage.</span><span class="sxs-lookup"><span data-stu-id="aaf00-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="aaf00-155">Przeglądarki Chrome: Ustawienia, ochrony prywatności, ustawienia zawartości.</span><span class="sxs-lookup"><span data-stu-id="aaf00-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="aaf00-156">Internet Explorer: Opcje internetowe, karta Zaawansowane, zabezpieczeń, Włącz Magazyn DOM</span><span class="sxs-lookup"><span data-stu-id="aaf00-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... Spróbuj tooenable HTML5 magazynu](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="aaf00-158"><a name="e-g"></a>404 ... Nie znaleziono subskrypcji</span><span class="sxs-lookup"><span data-stu-id="aaf00-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... Nie znaleziono subskrypcji](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="aaf00-160">adres URL Hello jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="aaf00-160">hello URL is invalid.</span></span> 

* <span data-ttu-id="aaf00-161">Otwórz zasób aplikacji hello w [portalu Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aaf00-161">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="aaf00-162">Następnie użyj przycisku Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="aaf00-162">Then use hello Analytics button.</span></span>

## <span data-ttu-id="aaf00-163"><a name="e-h"></a>404... strona nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="aaf00-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... Strona nie istnieje.](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="aaf00-165">adres URL Hello jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="aaf00-165">hello URL is invalid.</span></span>

* <span data-ttu-id="aaf00-166">Otwórz zasób aplikacji hello w [portalu Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aaf00-166">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="aaf00-167">Następnie użyj przycisku Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="aaf00-167">Then use hello Analytics button.</span></span>

## <span data-ttu-id="aaf00-168"><a name="cookies"></a>Włącz pliki cookie innych firm</span><span class="sxs-lookup"><span data-stu-id="aaf00-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="aaf00-169">Zobacz [jak toodisable innej firmy plików cookie](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), ale Zwróć uwagę, potrzebujemy zbyt**włączyć** je.</span><span class="sxs-lookup"><span data-stu-id="aaf00-169">See [how toodisable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need too**enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

