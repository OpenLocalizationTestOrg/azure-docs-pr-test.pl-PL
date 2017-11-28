---
title: "aaaAzure Mobile Engagement interfejsu użytkownika — osiągnąć kryterium"
description: "Dowiedz się, jak toouse docelowych kryteria toosend wypychania kampanii tooa wybiera podzbiór użytkowników przy użyciu usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a><span data-ttu-id="23cd2-103">Jak toouse docelowych kryteria toosend wypychania kampanii tooa wybiera podzestaw użytkowników</span><span class="sxs-lookup"><span data-stu-id="23cd2-103">How toouse targeting criteria toosend push campaigns tooa select subset of your users</span></span>
<span data-ttu-id="23cd2-104">Elementów docelowych odbiorców według określonych kryteriów z przycisku "Nowe kryterium" hello jest jednym z najbardziej zaawansowanych pojęcia hello w usłudze Azure Mobile Engagement czy pomaga wysyłanych odpowiednich wypychanie powiadomień, że klientom Witaj będzie odpowiadać tooinstead z spamem Wszyscy.</span><span class="sxs-lookup"><span data-stu-id="23cd2-104">Targeting your audience by specific criteria with hello "New Criteria" button is one of hello most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that hello customers will respond tooinstead of Spamming everyone.</span></span> <span data-ttu-id="23cd2-105">Można ograniczać na podstawie standardowego kryteriów odbiorców i symulacji toodetermine wypchnięć ile osób będą otrzymywać powiadomienia o hello.</span><span class="sxs-lookup"><span data-stu-id="23cd2-105">You can limit your audience based on standard criteria and simulate pushes toodetermine how many people will receive hello notification.</span></span>

<span data-ttu-id="23cd2-106">**Zobacz też:**</span><span class="sxs-lookup"><span data-stu-id="23cd2-106">**See also:**</span></span>

* <span data-ttu-id="23cd2-107">[Nową kampanię wypychania dokumentacji - Reach - interfejsu użytkownika][Link 27]</span><span class="sxs-lookup"><span data-stu-id="23cd2-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="23cd2-108">Kryteriów odbiorców narzędzia mogą obejmować:</span><span class="sxs-lookup"><span data-stu-id="23cd2-108">Audience criteria can include:</span></span>
* <span data-ttu-id="23cd2-109">** Technicals: ** można wskazać hello na podstawie tych samych informacji technicznych widać w sekcjach monitora i hello Analytics.</span><span class="sxs-lookup"><span data-stu-id="23cd2-109">**Technicals: ** You can target based on hello same technical information you can see in hello Analytics and Monitor sections.</span></span> <span data-ttu-id="23cd2-110">**Zobacz też:** [dokumentacji interfejsu użytkownika — Analytics][Link 15], [dokumentacji interfejsu użytkownika — Monitor][Link 16]</span><span class="sxs-lookup"><span data-stu-id="23cd2-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="23cd2-111">**Lokalizacja:** aplikacje, które Grodzenia za pomocą "Raportowanie lokalizacji czasu rzeczywistego" można używać lokalizacja geograficzna jako tootarget kryteriów odbiorców z hello GPS lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="23cd2-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria tootarget an audience from hello GPS location.</span></span> <span data-ttu-id="23cd2-112">Wywołanie "Lokalizacji opóźnieniem raportowania" być również używane tootarget odbiorców z lokalizacji telefonu komórkowego hello ("Raportowanie lokalizacji czasu rzeczywistego" i "Opóźnieniem raportowanie lokalizacji obszaru" musi być aktywowany z hello zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="23cd2-112">"Lazy Area Location Reporting" call also be used tootarget an audience from hello cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from hello SDK).</span></span> <span data-ttu-id="23cd2-113">**Zobacz też:** [dokumentacji zestawu SDK - iOS - integracji][Link 5], [dokumentacji zestawu SDK - Android - integracji][Link 5]</span><span class="sxs-lookup"><span data-stu-id="23cd2-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="23cd2-114">**Opinie reach:** można kierować na ich podstawie reach powiadomienia za pośrednictwem opinii reach anonse, ankiety i wypychanie danych odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="23cd2-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="23cd2-115">Dzięki temu toobetter docelowych odbiorców po dwóch lub trzech do kampanie, niż można hello po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="23cd2-115">This enables you toobetter target your audience after two or three reach campaigns than you could hello first time.</span></span> <span data-ttu-id="23cd2-116">Można również użyć toofilter użytkowników, którzy już odebrał powiadomienie o podobnych zawartości, ustawiając tooNOT kampanii wysłanie toousers, który już otrzymał określonej kampanii poprzedniej.</span><span class="sxs-lookup"><span data-stu-id="23cd2-116">It can also be used toofilter out users who already received a notification with similar content, by setting a campaign tooNOT be sent toousers who already received a specific previous campaign.</span></span> <span data-ttu-id="23cd2-117">Można nawet wyklucz użytkowników, który są uwzględniane określonej kampanii, które są nadal aktywne odbieranie nowych Wypchnięć.</span><span class="sxs-lookup"><span data-stu-id="23cd2-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="23cd2-118">**Zobacz też:** [zawartości przekazywanej - Reach — dokumentacja interfejsu użytkownika][Link 29]</span><span class="sxs-lookup"><span data-stu-id="23cd2-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="23cd2-119">**Instalacja śledzenia:** można śledzić informacje, na podstawie której użytkownicy zainstalowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23cd2-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="23cd2-120">**Zobacz też:** [dokumentacji interfejsu użytkownika — ustawienia][Link 20]</span><span class="sxs-lookup"><span data-stu-id="23cd2-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="23cd2-121">**Profil użytkownika:** możesz docelowym na podstawie informacji użytkownika standardowego i możesz docelowym oparte na informacje o niestandardowych aplikacji hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="23cd2-121">**User Profile:** You can target based on standard user information and you can target based on hello custom app info that you have created.</span></span> <span data-ttu-id="23cd2-122">Dotyczy to również użytkowników, którzy są aktualnie zalogowany i użytkowników, którzy mają odpowiedzi określonego pytania zażądano ich tooset w aplikacji hello sam zamiast podobnie jak ich odpowiedzieli tooprevious kampanii.</span><span class="sxs-lookup"><span data-stu-id="23cd2-122">This includes users who are currently logged in and users that have answered specific questions you have asked them tooset in hello app itself instead of just how they have responded tooprevious campaigns.</span></span> <span data-ttu-id="23cd2-123">Wszystkie informacje aplikacji zdefiniowane pokazu aplikacji się na tej liście.</span><span class="sxs-lookup"><span data-stu-id="23cd2-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="23cd2-124">Segmenty: Można również docelowym oparte na segmenty, które zostały utworzone na podstawie określonego użytkownika zachowania zawierający wiele kryteriów.</span><span class="sxs-lookup"><span data-stu-id="23cd2-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="23cd2-125">Wszystkie segmenty zdefiniowane dla aplikacji wyświetlane na tej liście.</span><span class="sxs-lookup"><span data-stu-id="23cd2-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="23cd2-126">**Zobacz też:** [dokumentacji interfejsu użytkownika — segmenty][Link 18]</span><span class="sxs-lookup"><span data-stu-id="23cd2-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="23cd2-127">**Informacje o aplikacji:** znaczniki informacje o aplikacji niestandardowe można tworzyć na podstawie zachowania użytkowników tootrack "Ustawienia".</span><span class="sxs-lookup"><span data-stu-id="23cd2-127">**App Info:** Custom App Info Tags can be created from “Settings” tootrack user behavior.</span></span> <span data-ttu-id="23cd2-128">**Zobacz też:** [dokumentacji interfejsu użytkownika — ustawienia][Link 20]</span><span class="sxs-lookup"><span data-stu-id="23cd2-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="23cd2-129">Przykład:</span><span class="sxs-lookup"><span data-stu-id="23cd2-129">Example:</span></span>
<span data-ttu-id="23cd2-130">Jeśli chcesz, aby toopush anonsu toohello tylko podzbioru użytkowników wykonywane w aplikacji zakupu akcji.</span><span class="sxs-lookup"><span data-stu-id="23cd2-130">If you want toopush an announcement only toohello sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="23cd2-131">Przejdź do strony ustawień aplikacji tooyour, wybierz menu "Informacje o aplikacji" hello i wybierz pozycję "Nowe informacje o aplikacji"</span><span class="sxs-lookup"><span data-stu-id="23cd2-131">Go tooyour application settings page, select hello "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="23cd2-132">Zarejestruj nowe informacje o aplikacji logiczną o nazwie "inAppPurchase"</span><span class="sxs-lookup"><span data-stu-id="23cd2-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="23cd2-133">Utworzyć aplikacji, ustawianie tych informacji o aplikacji zbyt "true" hello użytkownik wykonuje pomyślnie zakupu w aplikacji (przy użyciu hello sendAppInfo ("inAppPurchase",...) funkcja)</span><span class="sxs-lookup"><span data-stu-id="23cd2-133">Make your application set this app info too"true" when hello user successfully performs an in-app purchase (by using hello sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="23cd2-134">Jeśli nie chcesz toodo to z aplikacji, należy go z poziomu zaplecza przy użyciu interfejsu API urządzenia hello)</span><span class="sxs-lookup"><span data-stu-id="23cd2-134">If you don't want toodo this from your application, you can do it from your backend by using hello device API)</span></span>
5. <span data-ttu-id="23cd2-135">Następnie wystarczy toocreate anonsu, przy użyciu kryterium ograniczania sieci toousers odbiorców mających "inAppPurchase" ustawiony za "true")</span><span class="sxs-lookup"><span data-stu-id="23cd2-135">Then, you just need toocreate your announcement, with a criterion limiting your audience toousers having "inAppPurchase" set too"true")</span></span>

> [!NOTE]
> <span data-ttu-id="23cd2-136">Docelowy, na podstawie kryteriów innych niż tagi informacje o aplikacji wymaga usługi Azure Mobile Engagement toogather informacji z urządzeń użytkowników, zanim wypychania hello są wysyłane i może to spowodować opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="23cd2-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement toogather information from your users' devices before hello push is sent and so can cause a delay.</span></span> <span data-ttu-id="23cd2-137">Wypycha konfigurację złożonych wypychania opcje (np. aktualizowanie identyfikatory) również może opóźniać.</span><span class="sxs-lookup"><span data-stu-id="23cd2-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="23cd2-138">Używanie kampanii "zrzut jednym" od hello wypychania interfejsu API jest hello bezwzględną najszybszym metody wypychanej w usłudze Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="23cd2-138">Using a "one shot" campaign from hello Push API is hello absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="23cd2-139">Przy użyciu tylko tagi informacje o aplikacji jako kryterium wypychanej kampanii Reach (niezależnie od hello interfejsu API Reach lub hello interfejsu użytkownika) jest hello najszybszy sposób dalej, ponieważ tagi informacje o aplikacji są przechowywane na powitania po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="23cd2-139">Using only app info tags as push criteria for a Reach campaign (either from hello Reach API or hello UI) is hello next fastest method since app info tags are stored on hello server side.</span></span> <span data-ttu-id="23cd2-140">Przy użyciu innych kryteriów określania wartości docelowej w ramach kampanii wypychania jest hello najbardziej elastycznego, ale najwolniejsze push — metoda, ponieważ usługi Azure Mobile Engagement ma tooquery hello urządzenia w kolejności toosend hello kampanii.</span><span class="sxs-lookup"><span data-stu-id="23cd2-140">Using other targeting criteria for a push campaign is hello most flexible but slowest push method since Azure Mobile Engagement has tooquery hello devices in order toosend hello campaign.</span></span>

![Reach Criterion1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="23cd2-142">Opcje kryterium mają zastosowanie do:</span><span class="sxs-lookup"><span data-stu-id="23cd2-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="23cd2-143">**Technicals**</span><span class="sxs-lookup"><span data-stu-id="23cd2-143">**Technicals**</span></span>     
* <span data-ttu-id="23cd2-144">Nazwa oprogramowania układowego: nazwy oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="23cd2-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="23cd2-145">Wersja oprogramowania układowego: wersja oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="23cd2-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="23cd2-146">Model urządzenia: model urządzenia</span><span class="sxs-lookup"><span data-stu-id="23cd2-146">Device model:    Device model</span></span>
* <span data-ttu-id="23cd2-147">Producent urządzenia: producent urządzenia</span><span class="sxs-lookup"><span data-stu-id="23cd2-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="23cd2-148">Wersja aplikacji: wersja aplikacji</span><span class="sxs-lookup"><span data-stu-id="23cd2-148">Application version:    Application version</span></span>
* <span data-ttu-id="23cd2-149">Nazwa operatora: Nazwa operatora, niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="23cd2-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="23cd2-150">Operator kraju: operator kraju, niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="23cd2-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="23cd2-151">Typ sieci: typ sieci</span><span class="sxs-lookup"><span data-stu-id="23cd2-151">Network type:    Network type</span></span>
* <span data-ttu-id="23cd2-152">Ustawienia regionalne: ustawień regionalnych</span><span class="sxs-lookup"><span data-stu-id="23cd2-152">Locale:    Locale</span></span>
* <span data-ttu-id="23cd2-153">Rozmiar ekranu: rozmiaru ekranu</span><span class="sxs-lookup"><span data-stu-id="23cd2-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="23cd2-154">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="23cd2-154">**Location**</span></span>      
* <span data-ttu-id="23cd2-155">Ostatnia znana obszaru: Miejscowość województwo kraj, Region,</span><span class="sxs-lookup"><span data-stu-id="23cd2-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="23cd2-156">Grodzenia czasu rzeczywistego: Lista z liczba punktów POI (nazwa, akcje), cykliczne POI (nazwa, szerokości geograficznej, geograficzne, Radius metry)</span><span class="sxs-lookup"><span data-stu-id="23cd2-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="23cd2-157">**Osiągnąć opinii**</span><span class="sxs-lookup"><span data-stu-id="23cd2-157">**Reach feedback**</span></span>     
* <span data-ttu-id="23cd2-158">Opinie anonsu: anonsu, opinie</span><span class="sxs-lookup"><span data-stu-id="23cd2-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="23cd2-159">Sondowanie opinii: sondowania, opinie</span><span class="sxs-lookup"><span data-stu-id="23cd2-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="23cd2-160">Sondowanie odpowiedzi opinii: sondowanie opinii odpowiedzi, pytanie, wybór</span><span class="sxs-lookup"><span data-stu-id="23cd2-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="23cd2-161">Opinie wypychania danych: wypychane dane, opinii</span><span class="sxs-lookup"><span data-stu-id="23cd2-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="23cd2-162">**Zainstaluj śledzenia**</span><span class="sxs-lookup"><span data-stu-id="23cd2-162">**Install Tracking**</span></span>     
* <span data-ttu-id="23cd2-163">Magazyn: Magazyn, niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="23cd2-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="23cd2-164">Źródło: Źródło, niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="23cd2-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="23cd2-165">**Profil użytkownika**</span><span class="sxs-lookup"><span data-stu-id="23cd2-165">**User profile**</span></span>     
* <span data-ttu-id="23cd2-166">Płci: niezdefiniowana męskiego lub gniazdo,</span><span class="sxs-lookup"><span data-stu-id="23cd2-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="23cd2-167">Data urodzenia: operator, data niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="23cd2-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="23cd2-168">Opcjonalnych: PRAWDA lub FAŁSZ, niezdefiniowane</span><span class="sxs-lookup"><span data-stu-id="23cd2-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="23cd2-169">**Informacje o aplikacji**</span><span class="sxs-lookup"><span data-stu-id="23cd2-169">**App Info**</span></span>      
* <span data-ttu-id="23cd2-170">Ciąg: Ciąg, niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="23cd2-170">String:    String, undefined</span></span>
* <span data-ttu-id="23cd2-171">Data: operator, data niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="23cd2-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="23cd2-172">Całkowitą: operator, numer niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="23cd2-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="23cd2-173">Wartość logiczna: niezdefiniowana wartość PRAWDA lub FAŁSZ,</span><span class="sxs-lookup"><span data-stu-id="23cd2-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="23cd2-174">**Segment**</span><span class="sxs-lookup"><span data-stu-id="23cd2-174">**Segment**</span></span>    
* <span data-ttu-id="23cd2-175">Nazwa segmenty (z listy rozwijanej) wykluczeń (użytkownicy docelowi, którzy nie są częścią tego segmentu).</span><span class="sxs-lookup"><span data-stu-id="23cd2-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
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

