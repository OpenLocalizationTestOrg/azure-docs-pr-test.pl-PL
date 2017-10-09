---
title: "aaaAzure Mobile Engagement interfejsu użytkownika — segmenty"
description: "Dowiedz się, jak toocreate i zarządzanie segmentami wzorców użycia tooidentify użytkowników przy użyciu usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a>Jak toocreate i zarządzanie segmentami wzorców użycia tooidentify użytkowników
W tym artykule opisano hello **segmentów** kartę hello **Mobile Engagement** portalu. Użyj hello **Mobile Engagement** toomonitor portalu i zarządzania aplikacjami mobilnymi.

sekcja segmentów Hello hello interfejsu użytkownika umożliwia toowork na segmentacji użytkowników na podstawie inaczej hello i analiz, można uzyskać z aplikacji hello przez użytkownika, który można również uzyskać dostęp za pośrednictwem hello segmentów interfejsu API. Segmenty najpierw są obliczane 24 godziny po ich tworzenia i są one przeliczane co 24 godziny na podstawie najnowszych informacji analytics hello. Po obliczeniu segment on wyświetla "Dzień tooday historii" wykres każdego dnia.

> [!NOTE]
> Wiele sekcji hello **Mobile Engagement** interfejsu użytkownika portalu zawierają hello **Pokaż Pomoc** przycisku. Naciśnij ten przycisk tooget więcej informacje kontekstowe dotyczące sekcji.
> 
> 

## <a name="create-segments"></a>Tworzyć segmenty
Można utworzyć na podstawie kryteriów too10 określonego okresu się too60 dni w hello segment przeszłości z sekcji analytics hello. Na przykład można utworzyć segment oparte na osoby hello wyświetlanie określonych stron lub wyszukiwane określonej zawartości w Twojej aplikacji w ramach hello ostatnich 10 dni. Te informacje są dostępne w sekcji analytics hello. Tak, można go użyć toocreate segment, a następnie ponowne skonfigurowanie tootarget powiadomień wypychanych ten podzestaw użytkowników tooget ich toocome wstecz toohello aplikacji. 

> [!NOTE]
> Po obliczeniu segmentu nie może być edytowany; można tylko sklonować (skopiowanych) lub zniszczony (usunięty). W ramach hello można sklonować segmentu tej samej aplikacji (z hello tego samego AppID), i można go również sklonować do innych aplikacji (z różnych AppID). 

 ![segments1][35] 

## <a name="examples-segments"></a>Przykłady segmentów
 ![segments2][36]

Segmenty pozwalają użytkownikom końcowym hello toosegment aplikacji.
Segmentacji użytkowników jest ważne strategii marketingowej. Usługa Azure Mobile Engagement pozwala tooget danych historycznych i tworzyć segmenty niestandardowych. To narzędzie zaawansowane umożliwia toolearn o obsługi klientów w aplikacji. Można łatwo analizować segmentów i używać segmentów jako miejsca docelowe wypychania.
Typowe przypadek użycia jest mają toosend tooencourage powiadomień wypychanych toorate Twojego użytkownicy końcowi aplikacji w sklepie hello. Zamiast wysyłania tooall powiadomienie użytkowników końcowych, możesz utworzyć segment, który określa tylko w przypadku użytkowników, którzy używanych aplikacji codziennie dla hello ostatniego miesiąca i miały dużą interfejs użytkownika. Podczas wysyłania powiadomień wypychanych mniej, wysokiej docelowej, możesz uzyskać lepsze ROI.

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a>Segmentów, które można tworzyć oparte na powitania główne elementy usługi Azure Mobile Engagement:
* Zdarzenie: utworzyć segment tego cele jednego określonego zdarzenia aplikacji hello, który wystąpił więcej niż dwa razy w tygodniu. 
* Sesji: utworzenia segment użytkowników, którzy używali aplikacji hello więcej niż 5 razy w ostatnim tygodniu.
* Działania: Utwórz segment użytkowników, którzy używali jedną stronę lub zawartość większa lub mniejsza niż 10 czas ostatniego miesiąca.
* Zadania: Utwórz segment użytkowników, które zostały wykonane zadania więcej niż dwa razy dziennie.
* Awarii: segmentem wszyscy użytkownicy hello, które miały awarii więcej niż 10 razy w ostatnim tygodniu. (Ten segment Przeprosiny lub nawet papieru wartościowego można push)!
* Błąd: segmentem wszyscy użytkownicy hello, które miały błąd więcej niż 100 razy ostatnich 3 dni.
* Informacje o aplikacji: utworzyć segment przeznaczonego dla niestandardowych informacji o aplikacji, które wystąpiły podczas hello ostatnich dni 25.
  
  ![segments4][38]

toouse segmentu w optymalny sposób, musisz przeprowadzić dostosowane integracji hello zestawu SDK w aplikacji z planem znakowania tagów "Informacje o aplikacji".
Następnie przejdź toohello strona główna interfejsu hello, wybierz aplikacji hello i kliknij w sekcji "Segmentów" hello.

1. Wybierz sekcję "Segmentów" hello.
2. Kliknij przycisk "Nowy segment" hello przycisk toocreate nowy segment.

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a>Rzeczywiste życia przykład: Tworzenie prostego segmentu, na podstawie informacji "Session"
Utwórz segment wszystkim użytkownikom końcowym hello, którzy używali aplikacji co najmniej 50 razy w ostatnim tygodniu hello. Z tego miejsca Znajdź tylko hello użytkownicy końcowi, którzy poświęcony co najmniej 30 sekund w aplikacji na sesję. Wyświetli wszystkim użytkownikom końcowym hello mających pozytywne doświadczenia w aplikacji. Następnie segmentu hello utworzone może być używane toopush tooask użytkownicy końcowi toothese powiadomienia ich przechowywania aplikacji w hello toorate.

 ![segments5][39]

1. Nadaj nazwę segmentu w kolejności toofind ją szybko liście hello "Segment".
2. Powitania kliknij przycisk "Utwórz".
   
   ![segments6][40]

Wybierz sesji.

 ![segments7][41]

1. Wybierz okres hello "W ostatnim tygodniu".
2. Kliknij przycisk Dalej.
   
   ![segments8][42]
3. Witaj wybierz Operator, który jest odpowiedni liście hello: =; ≥, ≤.
4. Wprowadź hello liczba ma.
5. Wybierz wystąpienie ma hello. 
6. Kliknij przycisk Dalej.
   W tym przykładzie jest ustawiona, tak że over hello ostatniego tygodnia, dopasowanie użytkowników, którzy zostały wykonane co najmniej 50 sesji.
   
   ![segments9][43]

Witaj segmentacji sesji można hello długości sesji jako kryterium.

1. Wybierz hello operatora z listy hello.
2. Podaj hello długości sesji.
3. Kliknij przycisk Dalej.
   W tym przykładzie mówi to, że na wszystkich hello sesji, które zostały podzielone na powitania wystąpienia sekcji, wybierz tylko hello użytkowników, którzy poświęcony ponad 30 sekund na sesję.
   
   ![segments10][44]

Nazwa kryterium w kolejności tooretrieve w hello ukończyć Lejkowy, a następnie kliknij przycisk Zakończ.

 ![segments11][45]

Jeśli ukończono konfigurowanie kryterium, zostanie wyświetlony na powitania segmentów lejka.
Ponieważ segment jest oparta na dane analityczne, segmentów są obliczane raz dziennie.
W tym przykładzie 47,7% całkowitej użytkownicy końcowi hello dopasowane hello kryterium. Powinny one być hello użytkowników, którzy miały dobrej środowisko i będzie można prawdopodobnie tooprovide klasyfikacji wyższej, jeśli wypychanie ich powiadomienie prośbą toorate hello aplikacji w sklepie hello.

## <a name="see-also"></a>Zobacz też
* [Pojęcia][Link 6]
* [Usługa Przewodnik rozwiązywania problemów][Link 24]

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

