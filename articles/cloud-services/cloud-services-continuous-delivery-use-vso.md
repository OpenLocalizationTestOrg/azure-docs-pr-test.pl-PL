---
title: dostarczanie aaaContinuous z Visual Studio Team Services na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconfigure programu Visual Studio Team Services projekty zespołowe tooautomatically tworzenia i wdrażania toohello funkcji aplikacji sieci Web w usługach Azure App Service lub w chmurze."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a>TooAzure ciągłego dostarczania przy użyciu programu Visual Studio Team Services
Możesz skonfigurować kompilację tooautomatically projektów zespołowych Visual Studio Team Services i wdrażanie aplikacji sieci web tooAzure lub usług w chmurze.  (Informacji na temat sposobu tooset kompilacji ciągłego konfigurację i wdrażanie przy użyciu systemu *lokalnymi* Team Foundation Server, zobacz [ciągłego dostarczania dla usług w chmurze na platformie Azure](cloud-services-dotnet-continuous-delivery.md).)

W tym samouczku założono, że masz program Visual Studio 2013 i hello zainstalowany zestaw SDK platformy Azure. Jeśli nie masz jeszcze programu Visual Studio 2013, pobierz ją, wybierając hello **zacznij pracę bezpłatnie** łączenie z [www.visualstudio.com](http://www.visualstudio.com). Zainstaluj hello zestawu Azure SDK w [tutaj](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Należy toocomplete konta usługi Visual Studio Team Services w tym samouczku: możesz [otworzyć bezpłatne konto usługi Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset się tooautomatically usługi chmury tworzenie i wdrażanie tooAzure przy użyciu programu Visual Studio Team Services, wykonaj następujące kroki.

## <a name="1-create-a-team-project"></a>1: Tworzenie projektu zespołowego
Postępuj zgodnie z instrukcjami hello [tutaj](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate Twojego zespołu projektu i połączyć ją tooVisual Studio. W tym przewodniku przyjęto założenie, że używasz kontroli wersji typu Team Foundation (TFVC) jako rozwiązania do kontroli źródła. Jeśli chcesz toouse Git kontroli wersji, zobacz [wersji Git hello tego przewodnika](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-toosource-control"></a>2: Sprawdź w formancie toosource projektu
1. W programie Visual Studio Otwórz rozwiązanie hello mają toodeploy lub Utwórz nową.
   Możesz wdrożyć aplikację sieci web lub usługi w chmurze (Azure aplikacja) przez hello następujące kroki w tym przewodniku.
   Jeśli toocreate nowe rozwiązanie, należy utworzyć nowy projekt usługi w chmurze Azure lub nowy projekt ASP.NET MVC. Upewnij się, że hello elementy docelowe projektu platformy .NET Framework 4 lub 4.5, a w przypadku tworzenia projektu usługi w chmurze, Dodaj rolę sieci web platformy ASP.NET MVC i roli proces roboczy i wybierz polecenie aplikacji internetowej dla roli sieci web hello. Po wyświetleniu monitu wybierz **aplikacji internetowej**.
   Jeśli chcesz toocreate aplikacji sieci web, wybierz szablon projektu aplikacji sieci Web ASP.NET hello, a następnie wybierz MVC. Zobacz [tworzenie aplikacji sieci web platformy ASP.NET w usłudze Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > Visual Studio Team Services obsługuje tylko CI wdrożenia aplikacji sieci Web w usłudze Visual Studio w tej chwili. Projekt witryny sieci Web jest poza zakresem.
   > 
   > 
2. Otwórz menu kontekstowe hello hello rozwiązania i wybierz polecenie **tooSource rozwiązania Dodaj formant**.
   
    ![][5]
3. Zaakceptuj lub zmień ustawienia domyślne hello i wybierz hello **OK** przycisku. Po zakończeniu procesu hello ikony kontroli źródła są wyświetlane w **Eksploratora rozwiązań**.
   
    ![][6]
4. Otwórz menu skrótów hello hello rozwiązania i wybierz polecenie **Zaewidencjonuj**.
   
    ![][7]
5. W hello **oczekujących zmian** obszar **Team Explorer**, wpisz komentarz do zaewidencjonowania hello i wybierz hello **Zaewidencjonuj** przycisku.
   
    ![][8]
   
    Należy zwrócić uwagę tooinclude opcje hello lub wykluczyć określone zmiany wprowadzone podczas ewidencjonowania. Jeśli to konieczne, zmian są wyłączone, wybierz hello **obejmują wszystkie** łącza.
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a>3: łączenie hello tooAzure projektu
1. Teraz, gdy masz projektu zespołowego VS Team Services z kodu źródłowego w nim są gotowe tooconnect Twojego zespołu projektu tooAzure.  W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), wybierz użytkownika chmury usługi lub aplikacji sieci web lub Utwórz nową, wybierając hello  **+**  ikonę w lewy dolny hello i wybierając polecenie **usługiwchmurze** lub **sieci Web aplikacji** , a następnie **szybkie tworzenie**. Wybierz hello **skonfigurować publikowanie za pomocą usługi Visual Studio Team Services** łącza.
   
    ![][10]
2. W Kreatorze hello hello nazwę konta usługi Visual Studio Team Services w polu tekstowym hello i kliknąć przycisk hello **autoryzować teraz** łącza. Użytkownik może zostać poproszony toosign w.
   
    ![][11]
3. W hello **żądania połączenia** podręczne okno dialogowe, wybierz hello **Akceptuj** tooauthorize przycisk Azure tooconfigure Twojego zespołu projektu w programie VS Team Services.
   
    ![][12]
4. Po autoryzacji zakończy się powodzeniem, użytkownik widzi listy rozwijanej zawierającego listę projektach zespołowych Visual Studio Team Services. Wybierz nazwę projektu zespołowego, który został utworzony w poprzednich krokach hello hello, a następnie wybierz przycisk znacznika wyboru hello kreatora.
   
    ![][13]
5. Po projektu, pojawi się instrukcje dotyczące ewidencjonowania projektu zespołowego Visual Studio Team Services tooyour zmiany.  Na następnego zaewidencjonowania Visual Studio Team Services Skompiluj i wdróż tooAzure Twojego projektu.  Spróbuj teraz tego klikając hello **Zaewidencjonuj, z programu Visual Studio** połączyć, a następnie hello **Uruchom Visual Studio** link (lub równoważne hello **programu Visual Studio** u dołu hello Witaj ekranu portalu).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: wyzwolenia kompilowania i wdrożenie projektu
1. W programie Visual Studio **Team Explorer**, wybierz hello **Eksploratora kontroli źródła** łącza.
   
    ![][15]
2. Przejdź do pliku rozwiązania tooyour i otwórz go.
   
    ![][16]
3. W **Eksploratora rozwiązań**, otwarcie pliku i go zmienić. Na przykład zmienić plik hello `_Layout.cshtml` w obszarze widoki hello\\udostępniony folder w roli sieci web MVC.
   
    ![][17]
4. Edytuj logo hello hello witryny i wybierz **Ctrl + S** toosave hello pliku.
   
    ![][18]
5. W **Team Explorer**, wybierz hello **oczekujących zmian** łącza.
   
    ![][19]
6. Wprowadź komentarz, a następnie wybierz pozycję hello **Zaewidencjonuj** przycisku.
   
    ![][20]
7. Wybierz hello **macierzystego** toohello tooreturn przycisk **Team Explorer** strony głównej.
   
    ![][21]
8. Wybierz hello **kompilacje** hello tooview łącze kompilacje w toku.
   
    ![][22]
   
    **Team Explorer** pokazuje, że zostało wyzwolone kompilacji do zaewidencjonowania.
   
    ![][23]
9. Kliknij dwukrotnie nazwę hello hello kompilacji w toku tooview szczegółowy dziennik w miarę postępów kompilacji hello.
   
    ![][24]
10. Podczas kompilacji hello jest w toku, Przyjrzyjmy się hello definicji kompilacji, który został utworzony, gdy są połączone TFS tooAzure przy użyciu Kreatora hello.  Otwórz menu skrótów powitania dla definicji kompilacji hello i wybierz polecenie **edycji definicji kompilacji**.
    
     ![][25]
    
     W hello **wyzwalacza** kartę, zobaczysz, że hello definicji kompilacji jest domyślnie toobuild na każdym zaewidencjonowania.
    
     ![][26]
    
     W hello **procesu** karcie widać środowiska wdrażania hello jest ustawiona na nazwę toohello Twojego chmury usługi lub aplikacji sieci web. Podczas pracy z aplikacjami sieci web, właściwości hello, widocznej może się różnić z tymi, które przedstawiono w tym miejscu.
    
     ![][27]
11. Określ wartości dla właściwości hello, jeśli chcesz, aby wartości innej niż domyślne hello. Witaj właściwości publikowania platformy Azure znajdują się w hello **wdrożenia** sekcji.
    
     Witaj poniższej tabeli przedstawiono dostępne właściwości hello hello **wdrożenia** sekcji:
    
    | Właściwość | Wartość domyślna |
    | --- | --- |
    | Zezwalaj na niezaufane certyfikaty |W przypadku wartości FAŁSZ certyfikaty SSL muszą być podpisane przez urząd główny. |
    | Zezwalaj na uaktualnienie |Umożliwia tooupdate wdrożenia hello istniejącego wdrożenia zamiast tworzenia nowej. Zachowuje hello adresu IP. |
    | Nie usuwaj |Jeśli PRAWDA, nie zastępuj istniejącego wdrożenia niepowiązanych (uaktualnienia jest dozwolona). |
    | Ścieżka tooDeployment ustawienia |Witaj ścieżki tooyour .pubxml pliku dla aplikacji sieci web, toohello względną głównego folderu repozytorium hello. Ignorowane dla usługi w chmurze. |
    | Środowisko wdrażania SharePoint |Witaj takie same jak nazwa usługi hello. |
    | Środowisko wdrażania platformy Azure |Witaj aplikacji lub w chmurze nazwę usługi sieci web. |
12. Jeśli używasz wielu konfiguracji usługi (.cscfg pliki), można będzie określić konfigurację żądanej usługi hello w hello **kompilacji, zaawansowane, argumenty programu MSBuild** ustawienie. Na przykład toouse ServiceConfiguration.Test.cscfg, ustawić argumenty programu MSBuild opcji wiersza `/p:TargetProfile=Test`.
    
     ![][38]
    
     Do tego czasu kompilacji powinien zakończyło się pomyślnie.
    
     ![][28]
13. Dwukrotne kliknięcie nazwy kompilacji hello Visual Studio zawiera **podsumowanie kompilacji**, w tym wszystkie wyniki testu z skojarzone projektów testów jednostkowych.
    
     ![][29]
14. W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), można wyświetlić hello skojarzone wdrożenie na powitania **wdrożeń** karcie po wybraniu hello przemieszczania środowiska.
    
     ![][30]
15. Adres URL witryny tooyour przeglądania. Dla aplikacji sieci web, wystarczy kliknąć hello **Przeglądaj** przycisk na powitania paska poleceń. Usługi w chmurze, wybierz adres URL hello hello **szybki przegląd** sekcji hello **pulpitu nawigacyjnego** strony zawierającej hello środowiska przemieszczania dla usługi w chmurze. Wdrożenia z ciągłej integracji usług w chmurze są środowiska przemieszczania opublikowanych toohello domyślnie. Można zmienić to ustawienie hello **alternatywny środowiska usługi w chmurze** właściwości zbyt**produkcji**. Ten zrzut ekranu pokazuje gdzie hello na stronie pulpitu nawigacyjnego usługi chmury hello jest adres URL witryny.
    
    ![][31]
    
    Na nowej karcie przeglądarki zostanie otwarty tooreveal uruchomionej witryny.
    
    ![][32]
    
    Dla usług w chmurze wprowadzenie innych zmian tooyour projektu, możesz wyzwalacza więcej kompilacje i będą gromadzone wielu wdrożeń. Witaj najnowszego oznaczony jako aktywny.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: należy ponownie wdrożyć wcześniejszą kompilację
Ten krok ma zastosowanie toocloud usług i jest opcjonalna. W hello klasycznego portalu Azure, wybierz wcześniejsze wdrożenie, a następnie wybierz hello **ponownie wdrożyć** przycisk toorewind tooan Twojego lokacji do wcześniej w zaewidencjonowania.  Należy pamiętać, że spowoduje to wyzwalają nowej kompilacji w programie TFS i Utwórz nowy wpis w historii wdrożenia.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: Zmień hello wdrożenia produkcyjnego
Ten krok ma zastosowanie tylko toocloud usługi, nie aplikacje sieci web. Gdy wszystko będzie gotowe, możesz podwyższyć poziom środowiska produkcyjnego toohello dla hello przemieszczania, wybierając hello **wymiany** przycisku na powitania klasycznego portalu Azure. Hello nowo wdrożone środowiska przemieszczania jest awansowana tooProduction i hello poprzedniego środowiska produkcyjnego, jeśli taki występuje, staje się środowiska przemieszczania. Hello aktywnych wdrożeń mogą być różne dla środowisk przemieszczania i hello produkcji, ale Historia wdrażania hello ostatnie kompilacji jest hello sama niezależnie od tego środowiska.

![][35]

## <a name="7-run-unit-tests"></a>7: Uruchom testy jednostkowe
Ten krok ma zastosowanie tylko tooweb aplikacji, nie usługi w chmurze. tooput bramki jakości, wdrażania, można uruchomić testów jednostkowych i w razie awarii, można zatrzymać hello wdrożenia.

1. W programie Visual Studio Dodaj jednostkowy projekt testowy.
   
   ![][39]
2. Dodaj odwołania toohello projekt ma tootest.
   
   ![][40]
3. Dodanie niektórych testów jednostkowych. tooget uruchomiona, spróbuj fikcyjny test, który będzie zawsze przekazuj.
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. Przeprowadź edycję definicji kompilacji hello, wybierz hello **procesu** , a następnie rozwiń węzeł hello **testu** węzła.
5. Zestaw hello **niepowodzenie kompilacji w przypadku niepowodzenia testu** tooTrue. Oznacza to, że hello wdrożenia nie występują, chyba że hello testów przebiegu.
   
   ![][41]
6. Kolejka jest nowa kompilacja.
   
   ![][42]
   
   ![][43]
7. Podczas kompilacji hello jest kontynuowanie, sprawdzić postęp.
   
    ![][44]
   
    ![][45]
8. Po zakończeniu kompilacji hello Sprawdź hello wyników testu.
   
    ![][46]
   
    ![][47]
9. Spróbuj utworzyć test, który zakończy się niepowodzeniem. Dodaj nowego testu przez skopiowanie hello pierwszego z nich, zmień jego nazwę, a w komentarz wiersz hello kodu, stwierdzający, że notimplementedexception — jest oczekiwany wyjątek.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Sprawdź w tooqueue zmiany hello nowej kompilacji.
    
     ![][48]
11. Wyświetl szczegóły toosee wyników testu hello o niepowodzeniu hello.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat testowania w programie Visual Studio Team Services jednostek, zobacz [Uruchom testy jednostkowe w kompilacji](http://go.microsoft.com/fwlink/p/?LinkId=510474). Jeśli używasz programu Git, zobacz [udostępnianie kodu w usłudze Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) i [tooAzure ciągłego wdrażania aplikacji usługi](../app-service-web/app-service-continuous-deployment.md).  Aby uzyskać więcej informacji na temat programu Visual Studio Team Services, zobacz [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
