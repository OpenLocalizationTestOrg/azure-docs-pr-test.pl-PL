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
# <a name="troubleshoot-analytics-in-application-insights"></a>Rozwiązywanie problemów z analizą w usłudze Application Insights
Problemy z [Application Insights Analytics](app-insights-analytics.md)? Zacznij tutaj. Analytics to narzędzie wyszukiwania zaawansowanego hello Azure Application Insights.

## <a name="limits"></a>Limity
* Obecnie wyniki zapytania są ograniczone toojust dłużej niż przez tydzień w ciągu ostatnich danych.
* Firma Microsoft testuje w przeglądarkach: najnowsze wersje programu Chrome, Edge i przeglądarki Internet Explorer.

## <a name="known-incompatible-browser-extensions"></a>Rozszerzenia znanych niezgodne przeglądarki
* Ghostery

Wyłącz rozszerzenia hello, lub użyj innej przeglądarki.

## <a name="e-a"></a>"Nieoczekiwany błąd"
![Wystąpił nieoczekiwany błąd ekranu](./media/app-insights-analytics-troubleshooting/010.png)

Wystąpił błąd wewnętrzny podczas wykonywania portalu — nieobsługiwany wyjątek.

* Czyszczenie pamięci podręcznej przeglądarki hello. 

## <a name="e-b"></a>403... Spróbuj tooreload
![403... Spróbuj tooreload](./media/app-insights-analytics-troubleshooting/020.png)

Wystąpił błąd (podczas uwierzytelniania lub podczas generowania tokenu dostępu) związanych z uwierzytelniania. Hello portal może nie ma możliwości zbyt odzyskać bez zmiany ustawienia przeglądarki.

* Sprawdź [pliki cookie innych firm są włączone](#cookies) w przeglądarce hello. 

## <a name="authentication"></a>403... Sprawdź strefy zabezpieczeń
![403.. podjęciem ponownej próby upewnij strefy zabezpieczeń](./media/app-insights-analytics-troubleshooting/030.png)

Wystąpił błąd (podczas uwierzytelniania lub podczas generowania tokenu dostępu) związanych z uwierzytelniania. Hello portal może nie ma możliwości zbyt odzyskać bez zmiany ustawienia przeglądarki.

1. Sprawdź [pliki cookie innych firm są włączone](#cookies) w przeglądarce hello. 
2. Czy użyto Ulubione, zakładki lub portal analityka hello tooopen zapisane łącze? Zalogowano się przy użyciu innych poświadczeń niż użyte podczas zapisywania hello łącze?
3. Spróbuj użyć okna przeglądarki w prywatnego/incognito (po zamknięciu wszystkich tych okien). Tooprovide będziesz mieć swoje poświadczenia. 
4. Otwiera inne okno przeglądarki (zwykłej) i przejdź zbyt[Azure](https://portal.azure.com). Wyloguj. Następnie otwórz łącze i zaloguj się przy użyciu hello poprawne poświadczenia.
5. Użytkownicy Edge i przeglądarki Internet Explorer można również uzyskać ten błąd, gdy ustawienia zaufanej strefy nie są obsługiwane.
   
    Sprawdź zarówno [portal analityka](https://analytics.applicationinsights.io) i [portalu usługi Azure Active Directory](https://portal.azure.com) w hello tej samej strefie zabezpieczeń:
   
   * W programie Internet Explorer Otwórz **Opcje internetowe**, **zabezpieczeń**, **Zaufane witryny**, **witryny**:
     
     ![Okno dialogowe Opcje internetowe, dodanie lokacji tooTrusted witryn](./media/app-insights-analytics-troubleshooting/033.png)
     
     Hello listy witryn sieci Web, jeśli którekolwiek z hello następujące adresy URL są uwzględnione, upewnij się, że hello inne są uwzględniane:
     
     https://Analytics.applicationinsights.IO<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404 ... Nie znaleziono zasobu
![404... nie można odnaleźć zasobu](./media/app-insights-analytics-troubleshooting/040.png)

Zasób aplikacji została usunięta z usługi Application Insights i nie jest już dostępny. Może to nastąpić po zapisaniu hello adresu URL toohello analizy strony.

## <a name="e-e"></a>403 ... Brak autoryzacji
![403... nieautoryzowane](./media/app-insights-analytics-troubleshooting/050.png)

Nie masz uprawnień tooopen tej aplikacji w module analiz.

* Czy został wyświetlony link powitania od kogoś innego Poproś toomake się, że jesteś w hello [czytniki lub współautorzy dla tej grupy zasobów](app-insights-resources-roles-access-control.md).
* Został zapisany przy użyciu innych poświadczeń łącze hello? Otwórz hello [portalu Azure](https://portal.azure.com), wyloguj się, a następnie spróbuj to łącze ponownie, podając hello poprawne poświadczenia.

## <a name="html-storage"></a>403 ... Magazyn HTML5
Portalu używa HTML5 localStorage i sessionStorage.

* Przeglądarki Chrome: Ustawienia, ochrony prywatności, ustawienia zawartości.
* Internet Explorer: Opcje internetowe, karta Zaawansowane, zabezpieczeń, Włącz Magazyn DOM

![403... Spróbuj tooenable HTML5 magazynu](./media/app-insights-analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ... Nie znaleziono subskrypcji
![404 ... Nie znaleziono subskrypcji](./media/app-insights-analytics-troubleshooting/070.png)

adres URL Hello jest nieprawidłowy. 

* Otwórz zasób aplikacji hello w [portalu Application Insights](https://portal.azure.com). Następnie użyj przycisku Analytics hello.

## <a name="e-h"></a>404... strona nie istnieje.
![404 ... Strona nie istnieje.](./media/app-insights-analytics-troubleshooting/080.png)

adres URL Hello jest nieprawidłowy.

* Otwórz zasób aplikacji hello w [portalu Application Insights](https://portal.azure.com). Następnie użyj przycisku Analytics hello.

## <a name="cookies"></a>Włącz pliki cookie innych firm
  Zobacz [jak toodisable innej firmy plików cookie](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), ale Zwróć uwagę, potrzebujemy zbyt**włączyć** je.


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

