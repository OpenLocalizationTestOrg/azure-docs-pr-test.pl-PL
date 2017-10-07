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
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a>Jak toouse docelowych kryteria toosend wypychania kampanii tooa wybiera podzestaw użytkowników
Elementów docelowych odbiorców według określonych kryteriów z przycisku "Nowe kryterium" hello jest jednym z najbardziej zaawansowanych pojęcia hello w usłudze Azure Mobile Engagement czy pomaga wysyłanych odpowiednich wypychanie powiadomień, że klientom Witaj będzie odpowiadać tooinstead z spamem Wszyscy. Można ograniczać na podstawie standardowego kryteriów odbiorców i symulacji toodetermine wypchnięć ile osób będą otrzymywać powiadomienia o hello.

**Zobacz też:**

* [Nową kampanię wypychania dokumentacji - Reach - interfejsu użytkownika][Link 27]

## <a name="audience-criteria-can-include"></a>Kryteriów odbiorców narzędzia mogą obejmować:
* ** Technicals: ** można wskazać hello na podstawie tych samych informacji technicznych widać w sekcjach monitora i hello Analytics. **Zobacz też:** [dokumentacji interfejsu użytkownika — Analytics][Link 15], [dokumentacji interfejsu użytkownika — Monitor][Link 16]
* **Lokalizacja:** aplikacje, które Grodzenia za pomocą "Raportowanie lokalizacji czasu rzeczywistego" można używać lokalizacja geograficzna jako tootarget kryteriów odbiorców z hello GPS lokalizacji. Wywołanie "Lokalizacji opóźnieniem raportowania" być również używane tootarget odbiorców z lokalizacji telefonu komórkowego hello ("Raportowanie lokalizacji czasu rzeczywistego" i "Opóźnieniem raportowanie lokalizacji obszaru" musi być aktywowany z hello zestawu SDK). **Zobacz też:** [dokumentacji zestawu SDK - iOS - integracji][Link 5], [dokumentacji zestawu SDK - Android - integracji][Link 5]
* **Opinie reach:** można kierować na ich podstawie reach powiadomienia za pośrednictwem opinii reach anonse, ankiety i wypychanie danych odbiorcy. Dzięki temu toobetter docelowych odbiorców po dwóch lub trzech do kampanie, niż można hello po raz pierwszy. Można również użyć toofilter użytkowników, którzy już odebrał powiadomienie o podobnych zawartości, ustawiając tooNOT kampanii wysłanie toousers, który już otrzymał określonej kampanii poprzedniej. Można nawet wyklucz użytkowników, który są uwzględniane określonej kampanii, które są nadal aktywne odbieranie nowych Wypchnięć. **Zobacz też:** [zawartości przekazywanej - Reach — dokumentacja interfejsu użytkownika][Link 29]
* **Instalacja śledzenia:** można śledzić informacje, na podstawie której użytkownicy zainstalowanych aplikacji. **Zobacz też:** [dokumentacji interfejsu użytkownika — ustawienia][Link 20]
* **Profil użytkownika:** możesz docelowym na podstawie informacji użytkownika standardowego i możesz docelowym oparte na informacje o niestandardowych aplikacji hello utworzony. Dotyczy to również użytkowników, którzy są aktualnie zalogowany i użytkowników, którzy mają odpowiedzi określonego pytania zażądano ich tooset w aplikacji hello sam zamiast podobnie jak ich odpowiedzieli tooprevious kampanii. Wszystkie informacje aplikacji zdefiniowane pokazu aplikacji się na tej liście.
* Segmenty: Można również docelowym oparte na segmenty, które zostały utworzone na podstawie określonego użytkownika zachowania zawierający wiele kryteriów. Wszystkie segmenty zdefiniowane dla aplikacji wyświetlane na tej liście. **Zobacz też:** [dokumentacji interfejsu użytkownika — segmenty][Link 18]
* **Informacje o aplikacji:** znaczniki informacje o aplikacji niestandardowe można tworzyć na podstawie zachowania użytkowników tootrack "Ustawienia". **Zobacz też:** [dokumentacji interfejsu użytkownika — ustawienia][Link 20]

## <a name="example"></a>Przykład:
Jeśli chcesz, aby toopush anonsu toohello tylko podzbioru użytkowników wykonywane w aplikacji zakupu akcji.

1. Przejdź do strony ustawień aplikacji tooyour, wybierz menu "Informacje o aplikacji" hello i wybierz pozycję "Nowe informacje o aplikacji"
2. Zarejestruj nowe informacje o aplikacji logiczną o nazwie "inAppPurchase"
3. Utworzyć aplikacji, ustawianie tych informacji o aplikacji zbyt "true" hello użytkownik wykonuje pomyślnie zakupu w aplikacji (przy użyciu hello sendAppInfo ("inAppPurchase",...) funkcja)
4. Jeśli nie chcesz toodo to z aplikacji, należy go z poziomu zaplecza przy użyciu interfejsu API urządzenia hello)
5. Następnie wystarczy toocreate anonsu, przy użyciu kryterium ograniczania sieci toousers odbiorców mających "inAppPurchase" ustawiony za "true")

> [!NOTE]
> Docelowy, na podstawie kryteriów innych niż tagi informacje o aplikacji wymaga usługi Azure Mobile Engagement toogather informacji z urządzeń użytkowników, zanim wypychania hello są wysyłane i może to spowodować opóźnienia. Wypycha konfigurację złożonych wypychania opcje (np. aktualizowanie identyfikatory) również może opóźniać. Używanie kampanii "zrzut jednym" od hello wypychania interfejsu API jest hello bezwzględną najszybszym metody wypychanej w usłudze Azure Mobile Engagement. Przy użyciu tylko tagi informacje o aplikacji jako kryterium wypychanej kampanii Reach (niezależnie od hello interfejsu API Reach lub hello interfejsu użytkownika) jest hello najszybszy sposób dalej, ponieważ tagi informacje o aplikacji są przechowywane na powitania po stronie serwera. Przy użyciu innych kryteriów określania wartości docelowej w ramach kampanii wypychania jest hello najbardziej elastycznego, ale najwolniejsze push — metoda, ponieważ usługi Azure Mobile Engagement ma tooquery hello urządzenia w kolejności toosend hello kampanii.

![Reach Criterion1][29] 

## <a name="criterion-options-apply-to"></a>Opcje kryterium mają zastosowanie do:
* **Technicals**     
* Nazwa oprogramowania układowego: nazwy oprogramowania układowego
* Wersja oprogramowania układowego: wersja oprogramowania układowego
* Model urządzenia: model urządzenia
* Producent urządzenia: producent urządzenia
* Wersja aplikacji: wersja aplikacji
* Nazwa operatora: Nazwa operatora, niezdefiniowana
* Operator kraju: operator kraju, niezdefiniowana
* Typ sieci: typ sieci
* Ustawienia regionalne: ustawień regionalnych
* Rozmiar ekranu: rozmiaru ekranu
* **Lokalizacja**      
* Ostatnia znana obszaru: Miejscowość województwo kraj, Region,
* Grodzenia czasu rzeczywistego: Lista z liczba punktów POI (nazwa, akcje), cykliczne POI (nazwa, szerokości geograficznej, geograficzne, Radius metry)
* **Osiągnąć opinii**     
* Opinie anonsu: anonsu, opinie
* Sondowanie opinii: sondowania, opinie
* Sondowanie odpowiedzi opinii: sondowanie opinii odpowiedzi, pytanie, wybór
* Opinie wypychania danych: wypychane dane, opinii
* **Zainstaluj śledzenia**     
* Magazyn: Magazyn, niezdefiniowana
* Źródło: Źródło, niezdefiniowana
* **Profil użytkownika**     
* Płci: niezdefiniowana męskiego lub gniazdo,
* Data urodzenia: operator, data niezdefiniowana
* Opcjonalnych: PRAWDA lub FAŁSZ, niezdefiniowane
* **Informacje o aplikacji**      
* Ciąg: Ciąg, niezdefiniowana
* Data: operator, data niezdefiniowana
* Całkowitą: operator, numer niezdefiniowana
* Wartość logiczna: niezdefiniowana wartość PRAWDA lub FAŁSZ,
* **Segment**    
* Nazwa segmenty (z listy rozwijanej) wykluczeń (użytkownicy docelowi, którzy nie są częścią tego segmentu).

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

