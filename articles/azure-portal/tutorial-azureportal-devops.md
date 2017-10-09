---
title: 'Samouczek: DevOps z hello portalu Azure | Dokumentacja firmy Microsoft'
description: "Dowiedz się hello różnych przepływy DevOps hello portalu Azure."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a>Samouczek: DevOps z hello portalu Azure
Witaj platformy Azure jest pełny elastyczne DevOps przepływów pracy. Z tego samouczka dowiesz się, jak tooleverage możliwości hello hello toodevelop portalu Azure, testów, wdrażania, rozwiązywanie problemów z, monitorowania i zarządzania uruchomionych aplikacji. Ten samouczek koncentruje się na następujących hello:

1. Tworzenie aplikacji sieci Web i włączanie ciągłego wdrażania
2. Tworzenie i testowanie aplikacji
3. Monitorowanie aplikacji i rozwiązywanie problemów z nią związanych
4. Ogólne zadania zarządzania aplikacją

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a>Tworzenie aplikacji sieci Web i włączanie ciągłego wdrażania
Tworzenie aplikacji sieci Web z [usłudze Azure App Service](https://azure.microsoft.com/services/app-service/), który zostanie użyty w hello pozostałej części tego samouczka. Na początku zostanie włączone ciągłe wdrażanie z repozytorium kodu źródłowego do uruchomionego środowiska platformy Azure.

1. Zaloguj się do hello portalu Azure
2. Wybierz **usługi aplikacji** &gt; **ikonę Dodaj** i wprowadź nazwę, wybierz subskrypcję i Utwórz nowe tooserve grupy zasobów jako kontener hello hello usługi.
   
   Grupy zasobów umożliwiają toomanage różnych aspektów hello rozwiązania, takich jak rozliczenia, wdrożenia i monitorowania wszystkich jako pojedynczej grupy za pomocą [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
   
   ![image1][image1]
3. Po chwil zostanie utworzona usługa aplikacji. W portalu hello, należy wykonać kilka minut tooexplore hello różnych opcji menu hello usługi.
   
   ![image2][image2]    
4. Kliknij przycisk hello adresu URL. Zwróć uwagę, hello różnych dostępnych narzędzi i repozytoriów sposobów. Można również użyć hello języków i struktur wybranego w tym .NET, Java i Ruby.
   
   ![image3][image3]    
5. Witaj portalu Azure sprawia, że ciągłe wdrażanie prosty proces obejmuje kilka prostych kroków. W portalu Azure hello wybierz ustawienia z hello ikonę usługi aplikacji hello utworzony.
   
   ![image4][image4]
   
   W bloku hello otwartym na powitania prawo przewiń toohello publikowania sekcji.
   
   ![image5][image5]
6. Następnie należy skonfigurować niektóre ustawienia tooenable ciągłe wdrażanie dla aplikacji hello. Kliknij kolejno pozycje Źródło wdrożenia i Wybierz źródło. Zwróć uwagę, hello różnych opcji dla źródeł repozytorium.
   
   ![image6][image6]
7. W tym przykładzie należy wybrać serwis GitHub. Opcjonalnie wybierz repozytorium hello wybranych przez użytkownika i skonfigurować poświadczenia autoryzacji hello.
   
   ![image7][image7]
8. Po autoryzacji tooyour repozytorium można wybrać projekt i chcesz toodeploy gałęzi. Poniżej znajduje się kilka fikcyjnych przykładów.
   
   ![image8][image8]
9. Po wybraniu projektu i gałęzi kliknij przycisk OK. Należy rozpocząć toosee powiadomienia o wdrożeniu.
   
   ![image9][image9]
10. Przejdź wstecz tooGitHub toosee hello webhook utworzonego repozytorium kontroli źródła hello toointegrate przy użyciu usługi Azure. Witaj portalu Azure umożliwia integrację z usługi GitHub z kilku prostych krokach.
    
    ![image10][image10]
11. ciągłe wdrażanie toodemonstrate szybko dodać niektóre toohello zawartości repozytorium. Na przykład prosty Dodaj repozytorium GitHub tooa plik przykładowy tekst. Jesteś toouse wolnego .NET, Ruby, Python lub inny rodzaj aplikacji z usługi aplikacji. Możesz wolnego tooadd pliku tekstowego, ASP.NET MVC, Java lub Ruby repozytorium toohello aplikacji wybranych przez użytkownika.
    
    ![image11][image11]
12. Po zatwierdzania zmian tooyour repozytorium, zostanie wyświetlony nowy zainicjowanie wdrożenia w obszarze powiadomień portalu hello. Kliknij przycisk synchronizacji, jeśli nie szybko ma zmiany po zatwierdzania tooyour repozytorium.
    
    ![image12][image12]
13. W tym momencie Jeśli spróbuj i załadowania strony hello usługi aplikacji hello, może zostać wyświetlony błąd 403. W tym przykładzie jest ponieważ nie istnieje żadne ustawienia dokumentu typowy domyślny dla strony hello, takie jak plików, takich jak index.htm lub default.html. Można szybko rozwiązać ten z hello narzędzi w hello portalu Azure.  W portalu Azure hello wybierz ustawienia &gt; ustawienia aplikacji.
    
     ![image13][image13]
14. Zostanie otwarty blok ustawień aplikacji. Wprowadź nazwę hello strony powitania "SamplePage.html", a następnie kliknij przycisk Zapisz. Potrwać kilka minut tooexplore hello innych ustawień.
    
    ![image14][image14]
15. Opcjonalnie można odświeżyć tooensure adres URL z przeglądarki, zobacz hello oczekiwano zmiany. W takim przypadku jest prosty tekst teraz wypełnianie hello strony. Każdego repozytorium toohello dodatkowe zmiany spowoduje automatyczne nowego wdrożenia.
    
    ![image15][image15]
    
    Włączanie ciągłego wdrażania z hello Azure Portal to środowisko łatwe. Można również utworzyć bardziej złożoną potoki wersji i użyć innych technik istniejących kontroli źródła i ciągłej integracji tooAzure toodeploy systemów, takich jak wykorzystaniu automatycznych kompilacji oraz wersji systemów zarządzania.

## <a name="develop-and-test-an-app"></a>Tworzenie i testowanie aplikacji
Następnie wprowadzić kilka zmian kodu toohello podstawowej i szybko wdrożyć tych zmian. Zostanie również skonfigurować niektóre testowanie wydajnościowe na potrzeby aplikacji sieci Web hello.

1. W portalu Azure hello wybrać aplikacji usługi z okienka nawigacji hello, a następnie zlokalizuj usługi aplikacji.
   
   ![image16][image16]
2. Kliknij pozycję Narzędzia.
   
   ![image17][image17]
3. Zwróć uwagę, hello opracowanie kategorię w menu Narzędzia. Istnieje kilka przydatne narzędzi, w tym miejscu pozwalających nam toowork z aplikacji bez opuszczania hello portalu Azure. Kliknij pozycję Konsola.
   
   ![image18][image18]
4. W oknie konsoli hello możesz wykonywać poleceń na żywo dla aplikacji. Typ hello dir polecenie i naciśnij klawisz enter. Pamiętaj o tym, że polecenia wymagające podwyższonego poziomu uprawnień nie będą działać.
   
   ![image19][image19]
5. Powrót toohello opracowanie kategorii, a następnie wybierz pozycję Visual Studio Online. Uwaga: usługa Visual Studio Online nosi teraz nazwę Visual Studio Team Services.
   
   ![image20][image20]
6. Przełącz na powitania proces edycji w przeglądarce dla twojej aplikacji.
   
   ![image21][image21]
7. Dla aplikacji zostanie zainstalowane rozszerzenie sieci Web. Rozszerzenia szybkie i łatwe do dodawania tooapps funkcji na platformie Azure. Zwróć uwagę, niektóre hello inne typy rozszerzeń dostępnych hello poniższym zrzucie ekranu.
   
   ![image22][image22]
8. Po zainstalowaniu hello rozszerzenia usługi Visual Studio Online, kliknij Go.
   
   ![image23][image23]
9. Przeglądarki karcie której występuje programowanie IDE bezpośrednio w przeglądarce hello zostanie otwarta. Środowisko hello Uwaga poniżej znajduje się w Chrome.
   
   ![image24][image24]
10. Można wykonać kilka czynności, takie jak edytować pliki, dodać pliki i foldery i pobieranie zawartości z lokacji na żywo hello. Udostępnij plik SamplePage.html toohello szybkie edycji.
    
    ![image25][image25]
11. Za chwilę zmiany hello są automatycznie zapisywane. Jeśli przejdziesz toohello tylnej strony widać hello zmiany. Warto pamiętać, że takie wprowadzanie zmian „na żywo” nie jest zalecane w środowiskach produkcyjnych. Jednak narzędzi hello go łatwo toomake szybko wprowadź zmiany dla deweloperów i przetestować środowisk.
    
    ![image26][image26]
    
    ![image27][image27]
12. Powrót toohello narzędzia bloku i kategorii opracowanie powitania kliknij testu wydajności.
    
    ![image28][image28]
13. Należy tooset konta usług team. Więcej informacji można znaleźć w artykule [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) (Tworzenie konta usług Team Services).
14. Kliknij nowy toocreate testów wydajności sieci.
    
    ![image29][image29]
    
    Skonfiguruj hello różne wartości, a następnie kliknij przycisk Uruchom Test u dołu hello tooinitiate dialogu hello testów wydajności sieci.
    
    ![image30][image30]
    
    ![image31][image31]
15. Gdy hello test zacznie działać, można monitorować stan hello.
    
    ![image32][image32]
    
    Po zakończeniu testu hello, klikając hello wynik zawiera więcej szczegółowych informacji.
    
    ![image33][image33]
16. W tym przykładzie utworzono małych testy, więc istnieje tooanalyze ograniczoną ilość danych, ale można zobaczyć różnych metryk oraz jak ponowne uruchomienie testu z tego widoku. Hello Azure Portal sprawia, że tworzenie, wykonywanie i analizowanie łatwy testów wydajności sieci web. Poniższe zrzuty ekranu Hello przedstawia hello dane wydajności.
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a>Monitorowanie aplikacji i rozwiązywanie problemów z nią związanych
Platforma Azure udostępnia wiele możliwości monitorowania uruchomionych aplikacji i rozwiązywania problemów z nimi związanych.

1. W hello Azure Portal dla aplikacji sieci Web wybierz narzędzia.
   
   ![image37][image37]
2. Rozwiązywanie problemów z kategorii hello Zwróć uwagę hello różnych opcji przy użyciu narzędzia tootroubleshoot potencjalnych problemów z uruchomionej aplikacji. Można wykonywać takie czynności, jak na przykład monitorowanie bieżącego ruchu HTTP, włączanie samonaprawiania czy wyświetlanie dzienników.
   
   ![image38][image38]
3. Wybierz widok niektórych kodów HTTP get tooquickly metryki lokacji.
   
   ![image39][image39]
4. Wybierz pozycję Diagnostyka jako usługa. Wybierz typ aplikacji, a następnie wybierz przycisk Uruchom.
   
   ![image40][image40]
   
   Rozpocznie się zbieranie danych.
   
   ![image41][image41]
5. Możesz wybrać odpowiedni dziennik hello toodiagnose potencjalnych problemów. Należy toosee rejestrowania tooenable wszystkie dostępne dane hello opcje, takie jak dzienniki HTTP.
   
   ![image42][image42]
   
   Klikając plik zrzutu pamięci hello można pobrać i przeanalizować DebugDiag toohelp raportu analizy odnaleźć potencjalne problemy.
   
   ![image43][image43]
6. tooview większej ilości danych, należy tooenable dodatkowe rejestrowanie. Hello portalu Azure przejdź do aplikacji sieci Web toohello i wybierz polecenie Ustawienia.
   
   ![image44][image44]
7. Przewiń w dół toohello funkcje kategorii, a następnie wybierz pozycję dzienników diagnostycznych.
   
      ![image45][image45]
8. Zwróć uwagę, hello różne opcje rejestrowania. Włącz opcję Rejestrowanie serwera sieci Web i kliknij przycisk Zapisz.
   
   ![image46][image46]
9. Powrót toohello obszaru narzędzia dla aplikacji hello i wybierz diagnostyki jako usługi, a następnie kliknij przycisk Uruchom toorerun hello danych kolekcji.
   
   ![image47][image47]
10. Ustawienie rejestrowania hello HTTP jest włączone, pojawi się dane zbierane w dziennikach HTTP.
    
    ![image48][image48]
11. Klikając hello HTML pliku dziennika, należy utworzyć rozbudowany raport przeglądarki w celu dokładniejszego zbadania.
    
    ![image49][image49]
12. Powrót toohello narzędzia części hello Azure Portal dla aplikacji hello. Przewiń do sekcji narzędzia toohello, a następnie wybierz Eksploratora procesów.
    
    ![image50][image50]
13. Eksplorator procesów pozwala wyświetlić szczegółowe informacje o uruchomionych procesach. Uwagi poniżej można przejść do procesów i nawet kill wszystkie procesy hello portalu Azure.
    
    ![image51][image51]
    
    ![image52][image52]
14. Powrót bloku ustawienia toohello powitania po lewej stronie. Kliknij pozycję Nowe żądanie obsługi.
    
    ![image53][image53]
15. W bloku hello na powitania prawo wypełniania szczegółowe informacje o problemach hello, wprowadź informacje kontaktowe, a nawet przekazywanie danych diagnostycznych. Hello Azure Portal umożliwia współpracę z pomocy technicznej firmy Microsoft nie zakłóca pracy.
    
    ![image54][image54]
    
    ![image55][image55]
    
    Hello Azure Portal zapewnia wydajne i znanych narzędzi monitor toohelp środowiska i rozwiązywanie problemów z naszych uruchamianie aplikacji. Ma również akcji tootake mogli szybko przez wykonywanie zadań takich jak odtwarzanie procesów, włączanie i wyłączanie różnych zbierania danych i nawet integracji z professional pomocy technicznej firmy Microsoft.

## <a name="general-application-management"></a>Ogólne zarządzanie aplikacjami
Jeśli zarządzanie aplikacjami, często konieczne tooperform szerokiej gamy działania, takie jak konfigurowanie strategii tworzenia kopii zapasowych, wdrażanie i zarządzanie dostawców tożsamości i konfigurowania kontroli dostępu opartej na rolach. Zgodnie z hello inne środowiska DevOps, hello platformy Azure integruje te zadania bezpośrednio w portalu hello.

1. tooensure są utrzymywanie hello aplikacji sieci Web przed utratą danych należy tooconfigure kopii zapasowych. Przejdź toohello obszaru Ustawienia dla aplikacji sieci Web.
   
   ![image56][image56]
2. W bloku hello na powitania prawo przewiń w dół toohello funkcje kategorii.
   
    ![image57][image57]
3. Wybierz kopie zapasowe; zostanie otwarty blok na powitania prawo.
   
   ![image58][image58]
4. Kliknij przycisk Konfiguruj, wybierz konto magazynu z bloku hello na powitania prawo.
   
   ![image59][image59]
5. Teraz można tworzyć i wybierz toohold kontenera magazynu kopii zapasowych. Kliknij przycisk Utwórz u dołu hello hello bloku. Następnie wybierz kontener hello.
   
   ![image60][image60]
6. Po wybraniu opcji kontenera hello, można skonfigurować harmonogramy, a także ustawienia kopii zapasowych baz danych. W tym scenariuszu kliknij hello Zapisz ikony.
   
    ![image61][image61]
7. Po zapisaniu, przewiń blok toohello wstecz po lewej stronie powitania kopii zapasowych. Kliknij przycisk Utwórz kopię zapasową teraz tooback hello aplikacji.
   
    ![image62][image62]
8. Po chwili zostanie utworzona kopia zapasowa. Powiadomienie hello Przywróć teraz opcję hello zrzut ekranu poniżej.
   
    ![image63][image63]
9. Wybierz polecenie Przywróć teraz i sprawdź, czy blok toohello opcje hello na powitania prawo. Możesz wybrać odpowiednie kopii zapasowej i łatwo tooan przywracania wcześniej stanu niezbędne. Witaj portalu Azure pomógł nam go łatwo uaktywnić strategię odzyskiwania po awarii proste aplikacji hello.
   
    ![image64][image64]
10. Powrót bloku ustawienia toohello powitania po lewej stronie, a w obszarze funkcje, a następnie wybierz uwierzytelniania/autoryzacji.
    
     ![image65][image65]
11. W bloku hello na powitania prawo wybierz Uwierzytelnianie usługi aplikacji. Zwróć uwagę, hello różne opcje, które można skonfigurować z popularnych dostawców.
    
     ![image66][image66]
12. Wybierz dostawcę hello wybranych przez użytkownika i zwróć uwagę, opcje hello hello zakresu. Można podać identyfikator aplikacji i klucz tajny aplikacji i szybko włączyć uwierzytelniania serwisu Facebook dla aplikacji hello. Witaj Azure Portal umożliwia użycie uwierzytelniania, gotowe rozwiązanie dla aplikacji.
    
     ![image67][image67]
13. Powrót toohello bloku ustawienia, a następnie wybierz użytkowników w kategorii zarządzanie zasobami hello.
    
     ![image68][image68]
14. W bloku hello na powitania prawo Sprawdź hello różnych opcji dodawania ról i użytkowników. Witaj Azure Portal pozwala łatwo zarządzać RBAC (kontrola dostępu oparta na rolach) dla aplikacji hello.
    
     ![image69][image69]

## <a name="summary"></a>Podsumowanie
W tym samouczku przedstawiono niektóre hello zasilania z hello platformy Azure szybko włączając ciągłe wdrażanie dla aplikacji sieci web, wykonywanie różnych programowanie i testowania czynności, monitorowania i rozwiązywania problemów w aktywnej aplikacji i na koniec zarządzania kluczem Strategie odzyskiwania po awarii, tożsamości i kontroli dostępu opartej na rolach. Witaj platformy Azure umożliwia zintegrowane środowisko dla tych przepływów pracy DevOps oraz można pracować wydajnie pozostając w kontekście dla wykonywanego zadania hello.

## <a name="next-steps"></a>Następne kroki
* Usługa Azure Resource Manager jest ważne w przypadku włączania DevOps na powitania platformy Azure.  więcej odwiedź toolearn [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
* więcej informacji na temat wdrażania usługi Azure App Service można znaleźć toolearn [wdrażanie tooAzure Twojego aplikację usługi aplikacji](../app-service-web/web-sites-deploy.md)

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
