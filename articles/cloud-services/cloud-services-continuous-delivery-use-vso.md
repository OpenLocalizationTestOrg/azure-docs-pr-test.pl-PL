---
title: "Ciągłego dostarczania z Visual Studio Team Services na platformie Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania programu Visual Studio Team Services projektów zespołowych do automatycznego tworzenia i wdrażania dla funkcji aplikacji sieci Web w usługach Azure App Service lub w chmurze."
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
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a>Ciągłe dostarczanie na platformę Azure za pomocą usługi Visual Studio Team Services
Można skonfigurować programu Visual Studio Team Services projektów zespołowych do automatycznego tworzenia i wdrażania aplikacji sieci web platformy Azure lub usługi w chmurze.  (Informacje o tym, jak skonfigurować ciągłe kompilacji i wdrożyć przy użyciu systemu *lokalnymi* Team Foundation Server, zobacz [ciągłego dostarczania dla usług w chmurze na platformie Azure](cloud-services-dotnet-continuous-delivery.md).)

Ten samouczek zakłada, że używasz programu Visual Studio 2013 i zainstalować zestaw Azure SDK. Jeśli nie masz jeszcze programu Visual Studio 2013, pobierz ją, wybierając **zacznij pracę bezpłatnie** łączenie z [www.visualstudio.com](http://www.visualstudio.com). Zainstaluj zestaw Azure SDK z [tutaj](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Musisz mieć konto usługi Visual Studio Team Services do ukończenia tego samouczka: możesz [otworzyć bezpłatne konto usługi Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

Aby skonfigurować usługi w chmurze spowoduje automatyczne utworzenie i wdrażanie na platformie Azure przy użyciu programu Visual Studio Team Services, wykonaj następujące kroki.

## <a name="1-create-a-team-project"></a>1: Tworzenie projektu zespołowego
Postępuj zgodnie z instrukcjami [tutaj](http://go.microsoft.com/fwlink/?LinkId=512980) do tworzenia projektu zespołowego i połączyć je z programu Visual Studio. W tym przewodniku przyjęto założenie, że używasz kontroli wersji typu Team Foundation (TFVC) jako rozwiązania do kontroli źródła. Jeśli chcesz użyć do kontroli wersji Git, zobacz [wersji Git tego przewodnika](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-to-source-control"></a>2: projektów z kontrolą źródła
1. W programie Visual Studio Otwórz rozwiązanie, które mają zostać wdrożone lub Utwórz nową.
   Wykonując kroki opisane w tym przewodniku można wdrożyć aplikację sieci web lub usługi w chmurze (Azure aplikacji).
   Jeśli chcesz utworzyć nowe rozwiązanie, Utwórz nowy projekt usługi w chmurze Azure lub nowy projekt ASP.NET MVC. Upewnij się, że projekt jest przeznaczony dla platformy .NET Framework 4 lub 4.5, a w przypadku tworzenia projektu usługi w chmurze, Dodaj rolę sieci web platformy ASP.NET MVC i roli proces roboczy i wybierz polecenie aplikacji internetowej dla roli sieci web. Po wyświetleniu monitu wybierz **aplikacji internetowej**.
   Jeśli chcesz utworzyć aplikację sieci web, wybierz szablon projektu aplikacji sieci Web ASP.NET, a następnie wybierz MVC. Zobacz [tworzenie aplikacji sieci web platformy ASP.NET w usłudze Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > Visual Studio Team Services obsługuje tylko CI wdrożenia aplikacji sieci Web w usłudze Visual Studio w tej chwili. Projekt witryny sieci Web jest poza zakresem.
   > 
   > 
2. Otwórz menu kontekstowe dla rozwiązania i wybierz polecenie **Dodaj rozwiązanie do kontroli źródła**.
   
    ![][5]
3. Zaakceptuj lub zmień ustawienia domyślne i wybierz **OK** przycisku. Po zakończeniu procesu ikony kontroli źródła są wyświetlane w **Eksploratora rozwiązań**.
   
    ![][6]
4. Otwórz menu skrótów dla rozwiązania i wybierz polecenie **Zaewidencjonuj**.
   
    ![][7]
5. W **oczekujących zmian** obszar **Team Explorer**, wpisz komentarz do zaewidencjonowania i wybierz **Zaewidencjonuj** przycisku.
   
    ![][8]
   
    Należy pamiętać, opcje, aby dołączyć lub wykluczyć określone zmiany wprowadzone podczas ewidencjonowania. Jeśli to konieczne, zmian są wyłączone, wybierz **obejmują wszystkie** łącza.
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a>3: Połącz projekt na platformie Azure
1. Teraz, gdy masz projektu zespołowego VS Team Services z kodu źródłowego w nim można przystąpić do projektu zespołowego połączenia z platformą Azure.  W [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), wybierz użytkownika chmury usługi lub aplikacji sieci web lub Utwórz nową, wybierając  **+**  ikony na dole po lewej i wybierając polecenie **usługi w chmurze**lub **sieci Web aplikacji** , a następnie **szybkie tworzenie**. Wybierz **skonfigurować publikowanie za pomocą usługi Visual Studio Team Services** łącza.
   
    ![][10]
2. W kreatorze, wpisz nazwę konta usługi Visual Studio Team Services w pliku tekstowym i kliknij przycisk **autoryzować teraz** łącza. Może być konieczne podanie do logowania.
   
    ![][11]
3. W **żądania połączenia** podręczne okno dialogowe, wybierz **Akceptuj** przycisk, aby autoryzować Azure, aby skonfigurować projekt zespołowy w programie VS Team Services.
   
    ![][12]
4. Po autoryzacji zakończy się powodzeniem, użytkownik widzi listy rozwijanej zawierającego listę projektach zespołowych Visual Studio Team Services. Wybierz nazwę projektu zespołowego, który został utworzony w poprzednich krokach, a następnie wybierz przycisk wyboru w kreatorze.
   
    ![][13]
5. Po projektu, pojawi się instrukcje dotyczące ewidencjonowania zmiany do projektu zespołowego Visual Studio Team Services.  Na następnym zaewidencjonowania Visual Studio Team Services skompiluje oraz wdrażanie projektu na platformie Azure.  Spróbuj to teraz po kliknięciu **Zaewidencjonuj, z programu Visual Studio** łącza, a następnie **Uruchom Visual Studio** łącza (lub równoważne **Visual Studio** przycisk w dolnej części ekran portalu).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: wyzwolenia kompilowania i wdrożenie projektu
1. W programie Visual Studio **Team Explorer**, wybierz **Eksploratora kontroli źródła** łącza.
   
    ![][15]
2. Przejdź do pliku rozwiązania, a następnie otwórz go.
   
    ![][16]
3. W **Eksploratora rozwiązań**, otwarcie pliku i go zmienić. Na przykład zmienić plik `_Layout.cshtml` pod widokami\\udostępniony folder w roli sieci web MVC.
   
    ![][17]
4. Edytuj logo witryny i wybierz **Ctrl + S** można zapisać pliku.
   
    ![][18]
5. W **Team Explorer**, wybierz **oczekujących zmian** łącza.
   
    ![][19]
6. Wprowadź komentarz, a następnie wybierz pozycję **Zaewidencjonuj** przycisku.
   
    ![][20]
7. Wybierz **macierzystego** przycisk, aby powrócić do **Team Explorer** strony głównej.
   
    ![][21]
8. Wybierz **kompilacje** łącze, aby wyświetlić kompilacji w toku.
   
    ![][22]
   
    **Team Explorer** pokazuje, że zostało wyzwolone kompilacji do zaewidencjonowania.
   
    ![][23]
9. Kliknij dwukrotnie nazwę kompilacji w toku, aby wyświetlić szczegółowy dziennik w trakcie kompilacji.
   
    ![][24]
10. Gdy kompilacja jest w toku, Przyjrzyjmy się definicję kompilacji, który został utworzony, gdy są połączone TFS na platformie Azure za pomocą kreatora.  Otwórz menu skrótów dla definicji kompilacji i wybierz polecenie **edycji definicji kompilacji**.
    
     ![][25]
    
     W **wyzwalacza** kartę, zobaczysz, że definicji kompilacji jest ustawiony na każdym zaewidencjonowania domyślnie.
    
     ![][26]
    
     W **procesu** karcie widać środowiska wdrażania jest ustawiona na nazwę Twojej chmury usługi lub aplikacji sieci web. Podczas pracy z aplikacjami sieci web, właściwości, które widać może się różnić od tych przedstawionych w tym miejscu.
    
     ![][27]
11. Określ wartości dla właściwości, jeśli chcesz, aby wartości innej niż wartości domyślne. Właściwości publikowania platformy Azure są w **wdrożenia** sekcji.
    
     W poniższej tabeli przedstawiono dostępne właściwości w **wdrożenia** sekcji:
    
    | Właściwość | Wartość domyślna |
    | --- | --- |
    | Zezwalaj na niezaufane certyfikaty |W przypadku wartości FAŁSZ certyfikaty SSL muszą być podpisane przez urząd główny. |
    | Zezwalaj na uaktualnienie |Umożliwia wdrożenie, aby zaktualizować istniejące wdrożenie zamiast tworzenia nowej. Zachowuje adres IP. |
    | Nie usuwaj |Jeśli PRAWDA, nie zastępuj istniejącego wdrożenia niepowiązanych (uaktualnienia jest dozwolona). |
    | Ścieżka do ustawienia wdrożenia |Ścieżka do pliku .pubxml dla aplikacji sieci web, względem głównego folderu repozytorium. Ignorowane dla usługi w chmurze. |
    | Środowisko wdrażania SharePoint |Taka sama jak nazwa usługi. |
    | Środowisko wdrażania platformy Azure |Nazwa sieci web aplikacji lub w chmurze usługi. |
12. Jeśli używasz wielu konfiguracji usługi (.cscfg pliki), można będzie określić konfigurację żądanej usługi w **kompilacji, zaawansowane, argumenty programu MSBuild** ustawienie. Na przykład, aby używać ServiceConfiguration.Test.cscfg, ustaw argumenty programu MSBuild opcji wiersza `/p:TargetProfile=Test`.
    
     ![][38]
    
     Do tego czasu kompilacji powinien zakończyło się pomyślnie.
    
     ![][28]
13. Dwukrotne kliknięcie nazwy kompilacji programu Visual Studio zawiera **podsumowanie kompilacji**, w tym wszystkie wyniki testu z skojarzone projektów testów jednostkowych.
    
     ![][29]
14. W [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), skojarzone wdrożenia można obejrzeć w **wdrożeń** karcie, gdy środowisko tymczasowe jest zaznaczone.
    
     ![][30]
15. Przejdź do adresu URL witryny. Dla aplikacji sieci web, wystarczy kliknąć **Przeglądaj** przycisk paska poleceń. Usługi w chmurze, wybierz adres URL w **szybki przegląd** sekcji **pulpitu nawigacyjnego** strony zawierającej środowiska przemieszczania dla usługi w chmurze. Wdrożenia z ciągłej integracji usług w chmurze są publikowane w środowisku przemieszczania domyślnie. Możesz zmienić to ustawienie **alternatywny środowiska usługi w chmurze** właściwości **produkcji**. Zrzut ekranu przedstawia, gdy adres URL witryny jest na stronie pulpitu nawigacyjnego usługi w chmurze.
    
    ![][31]
    
    Na nowej karcie przeglądarki będą otwierane w celu wyświetlenia uruchomionej witryny.
    
    ![][32]
    
    Dla usług w chmurze, jeśli inne zmiany do projektu, możesz wyzwalacza więcej kompilacje i będą gromadzone wielu wdrożeń. Najnowszego oznaczony jako aktywny.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: należy ponownie wdrożyć wcześniejszą kompilację
Ten krok ma zastosowanie do usługi w chmurze i jest opcjonalna. W klasycznym portalu Azure, wybierz wcześniejsze wdrożenie, a następnie wybierz **ponownie wdrożyć** przycisku do tyłu witryny wcześniej zaewidencjonowania.  Należy pamiętać, że spowoduje to wyzwalają nowej kompilacji w programie TFS i Utwórz nowy wpis w historii wdrożenia.

![][34]

## <a name="6-change-the-production-deployment"></a>6: Zmień wdrożenia produkcyjnego
Ten krok ma zastosowanie tylko do usługi w chmurze, nie aplikacje sieci web. Gdy wszystko będzie gotowe, możesz podwyższyć poziom środowiska przemieszczania do środowiska produkcyjnego, wybierając **wymiany** przycisk w klasycznym portalu Azure. Nowo wdrożonym środowiska przemieszczania jest podwyższany do środowiska produkcyjnego i poprzedniego środowiska produkcyjnego, jeśli taki występuje, staje się środowiska przemieszczania. Aktywne wdrożenie może się różnić w produkcyjne i przejściowe środowisk, ale Historia wdrażania ostatnie kompilacji jest taka sama niezależnie od środowiska.

![][35]

## <a name="7-run-unit-tests"></a>7: Uruchom testy jednostkowe
Ten krok dotyczy tylko sieci web apps, nie usług w chmurze. Aby zawiesić bramki jakości wdrożenia, można uruchomić testów jednostkowych i w razie awarii, można zatrzymać wdrożenia.

1. W programie Visual Studio Dodaj jednostkowy projekt testowy.
   
   ![][39]
2. Dodaj odwołania projektu do projektu, który ma zostać przetestowana.
   
   ![][40]
3. Dodanie niektórych testów jednostkowych. Aby rozpocząć, spróbuj fikcyjny test, który będzie zawsze przekazuj.
   
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
4. Przeprowadź edycję definicji kompilacji, wybierz **procesu** , a następnie rozwiń węzeł **testu** węzła.
5. Ustaw **niepowodzenie kompilacji w przypadku niepowodzenia testu** na wartość True. Oznacza to, że wdrożenie nie zostanie przeprowadzone, chyba, że testy zostały zaliczone pomyślnie.
   
   ![][41]
6. Kolejka jest nowa kompilacja.
   
   ![][42]
   
   ![][43]
7. Podczas kompilacji jest kontynuowanie, sprawdzić postęp.
   
    ![][44]
   
    ![][45]
8. Po zakończeniu kompilacji, sprawdź wyniki testu.
   
    ![][46]
   
    ![][47]
9. Spróbuj utworzyć test, który zakończy się niepowodzeniem. Dodaj nowego testu przez skopiowanie pierwsza z nich, zmień jego nazwę, a w komentarz wiersz kodu, stwierdzający, że notimplementedexception — jest oczekiwany wyjątek.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Zaewidencjonuj zmiany do kolejki nowej kompilacji.
    
     ![][48]
11. Wyświetlić wyniki testów, aby zobaczyć szczegóły dotyczące błędu.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat testowania w programie Visual Studio Team Services jednostek, zobacz [Uruchom testy jednostkowe w kompilacji](http://go.microsoft.com/fwlink/p/?LinkId=510474). Jeśli używasz programu Git, zobacz [udostępnianie kodu w usłudze Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) i [ciągłe wdrażanie w usłudze Azure App Service](../app-service-web/app-service-continuous-deployment.md).  Aby uzyskać więcej informacji na temat programu Visual Studio Team Services, zobacz [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

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
