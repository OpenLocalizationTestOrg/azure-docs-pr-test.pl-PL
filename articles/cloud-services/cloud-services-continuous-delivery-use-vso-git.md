---
title: "Ciągłego dostarczania Git i Visual Studio Team Services na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować projektach zespołowych Visual Studio Team Services, można użyć do automatycznego tworzenia i wdrażania dla funkcji aplikacji sieci Web w usłudze Azure App Service lub w chmurze usługi Git."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a>Ciągłe dostarczanie na platformę Azure za pomocą usługi Visual Studio Team Services i Git
Projekty zespołowe Visual Studio Team Services umożliwia hosta repozytorium Git do kodu źródłowego i automatycznie kompilacji i wdrażania aplikacji sieci web platformy Azure lub usługi w chmurze zawsze, gdy wypychanie zatwierdzeń do repozytorium.

Będziesz potrzebować programu Visual Studio 2013 oraz zainstalowany zestaw SDK platformy Azure. Jeśli nie masz jeszcze programu Visual Studio 2013, pobierz ją, wybierając **zacznij pracę bezpłatnie** łączenie z [www.visualstudio.com](http://www.visualstudio.com). Zainstaluj zestaw Azure SDK z [tutaj](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Musisz mieć konto usługi Visual Studio Team Services do ukończenia tego samouczka: możesz [otworzyć bezpłatne konto usługi Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

Aby skonfigurować usługi w chmurze spowoduje automatyczne utworzenie i wdrażanie na platformie Azure przy użyciu programu Visual Studio Team Services, wykonaj następujące kroki.

## <a name="1-create-a-git-repository"></a>1: Tworzenie repozytorium Git
1. Jeśli nie masz już konto usługi Visual Studio Team Services, możesz ją uzyskać, [tutaj](http://go.microsoft.com/fwlink/?LinkId=397665). Podczas tworzenia projektu zespołowego, wybierz Git jako system kontroli źródła. Postępuj zgodnie z instrukcjami, aby połączyć program Visual Studio do projektu zespołowego.
2. W **Team Explorer**, wybierz **Klonuj to repozytorium** łącza.
   
    ![][3]
3. Określ lokalizację kopii lokalnej, a następnie wybierz pozycję **klonowania** przycisku.

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a>2: utworzenie projektu i przekazać go do repozytorium
1. W **Team Explorer**w **rozwiązań** wybierz **nowy** łącze, aby utworzyć nowy projekt w lokalnym repozytorium.
   
    ![][4]
2. Wykonując kroki opisane w tym przewodniku można wdrożyć aplikację sieci web lub usługi w chmurze (Azure aplikacji). Utwórz nowy projekt usługi w chmurze Azure lub nowy projekt ASP.NET MVC. Upewnij się, że projekt jest przeznaczony dla programu .NET Framework 4 lub nowszy. W przypadku tworzenia projektu usługi w chmurze, Dodaj rolę sieci web programu ASP.NET MVC i roli proces roboczy.
   Jeśli chcesz utworzyć aplikację sieci web, wybierz **aplikacji sieci Web ASP.NET** projektu szablonu, a następnie wybierz pozycję **MVC**. Zobacz [tworzenie aplikacji sieci web platformy ASP.NET w usłudze Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) Aby uzyskać więcej informacji.
3. Otwórz menu skrótów dla rozwiązania i wybierz polecenie **zatwierdzić**.
   
    ![][7]
4. Jest to po raz pierwszy w programie Visual Studio Team Services użyto Git, należy podać niektóre informacje w celu identyfikacji w usłudze Git. W **oczekujących zmian** obszar **Team Explorer**, wprowadź nazwy użytkownika i adres e-mail. Wprowadź komentarz dotyczący zatwierdzenia, a następnie wybierz pozycję **zatwierdzania** przycisku.
   
    ![][8]
5. Należy pamiętać, opcje, aby dołączyć lub wykluczyć określone zmiany wprowadzone podczas ewidencjonowania. Jeśli odpowiednie zmiany, są wykluczone, wybierz **obejmują wszystkie**.
6. Zostały teraz zatwierdzone zmiany w lokalnej kopii repozytorium. Następnie zsynchronizować te zmiany z serwerem, wybierając **synchronizacji** łącza.

## <a name="3-connect-the-project-to-azure"></a>3: Połącz projekt na platformie Azure
1. Teraz, gdy masz repozytorium Git w Visual Studio Team Services z kodu źródłowego w nim można przystąpić do repozytorium git połączenia z platformą Azure.  W [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), wybierz użytkownika chmury usługi lub aplikacji sieci web lub Utwórz nową, wybierając pozycję + ikony na dole po lewej i wybierając polecenie **usługi w chmurze** lub **aplikacji sieci Web** , a następnie **szybkie tworzenie**.
   
    ![][9]
2. Usługi w chmurze, można wybrać **skonfigurować publikowanie za pomocą usługi Visual Studio Team Services** łącza. W przypadku aplikacji sieci web, wybierz **Konfigurowanie wdrażania z kontroli źródła** łącza.
   
    ![][10]
3. W kreatorze, w polu tekstowym wprowadź nazwę konta usługi Visual Studio Team Services, a następnie wybierz pozycję **autoryzować teraz** łącza. Może być konieczne podanie do logowania.
   
    ![][11]
4. W **żądania połączenia** podręczne okno dialogowe, wybierz **Akceptuj** do autoryzacji Azure, aby skonfigurować projekt zespołowy w programie Visual Studio Team Services.
   
    ![][12]
5. Po autoryzacji zakończy się powodzeniem, zostanie wyświetlona lista rozwijana zawierający projektach zespołowych Visual Studio Team Services.  Wybierz nazwę projektu zespołowego, który został utworzony w poprzednich krokach, a następnie wybierz przycisk wyboru w kreatorze.
   
    ![][13]
   
    Przy następnym wypychanie zatwierdzeń do repozytorium, Visual Studio Team Services skompiluje oraz wdrażanie projektu na platformie Azure.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: wyzwolenia kompilowania i wdrożenie projektu
1. W programie Visual Studio otwarcia pliku i zmodyfikuj go. Na przykład zmienić plik `_Layout.cshtml` pod widokami\\udostępniony folder w roli sieci web MVC.
   
    ![][17]
2. Edytuj tekst stopki dla lokacji i Zapisz plik.
   
    ![][18]
3. W **Eksploratora rozwiązań**, otwórz menu skrótów węzła rozwiązania, węzła projektu lub pliku zmienione, a następnie wybierz pozycję **zatwierdzić**.
4. Wpisz komentarz i wybierz **zatwierdzić**.
   
    ![][20]
5. Wybierz **synchronizacji** łącza.
   
    ![][38]
6. Wybierz **wypychania** łącze do wypychania Twojego zatwierdzenia w repozytorium w Visual Studio Team Services. (Można również użyć **synchronizacji** przycisk, aby skopiować zatwierdzenia w repozytorium. Różnica jest to, że **synchronizacji** również pobiera najnowsze zmiany z repozytorium.)
   
    ![][39]
7. Wybierz **macierzystego** przycisk, aby powrócić do **Team Explorer** strony głównej.
   
    ![][21]
8. Wybierz **kompilacje** Aby wyświetlić kompilacji w toku.
   
    ![][22]
   
    **Team Explorer** pokazuje, że zostało wyzwolone kompilacji do zaewidencjonowania.
   
    ![][23]
9. Aby wyświetlić szczegółowy dziennik w trakcie kompilacji, kliknij dwukrotnie nazwę kompilacji w toku.
10. Gdy kompilacja jest w toku, Przyjrzyjmy się definicję kompilacji, który został utworzony, gdy Kreator jest używany do łączenia na platformie Azure.  Otwórz menu skrótów dla definicji kompilacji i wybierz polecenie **edycji definicji kompilacji**.
    
    ![][25]
11. W **wyzwalacza** kartę, zobaczysz, że definicji kompilacji jest ustawiony na każdym zaewidencjonowania, domyślnie. (Dla usługi w chmurze programu Visual Studio Team Services tworzy i wdraża głównej gałęzi do środowiska pomostowego automatycznie. Nadal musisz wykonać krok wykonywany ręcznie do wdrożenia na stronie. Dla aplikacji sieci web, która nie ma w środowisku przemieszczania wdraża gałęzi głównej bezpośrednio do witryny na żywo.
    
    ![][26]
12. W **procesu** karcie widać środowiska wdrażania jest ustawiona na nazwę Twojej chmury usługi lub aplikacji sieci web.
    
     ![][27]
13. Określ wartości dla właściwości, jeśli chcesz, aby wartości innej niż wartości domyślne. Właściwości publikowania platformy Azure są w **wdrożenia** sekcji, a także mogą wymagać ustawić parametry MSBuild. Na przykład w chmurze projekt usługi, aby określić konfigurację usługi innego niż "Chmura" Ustaw MSbuild parametrów `/p:TargetProfile=[YourProfile]` gdzie *[YourProfile]* pasuje do pliku konfiguracji usługi z nazwą jak element ServiceConfiguration. *YourProfile*.cscfg.
    
     W poniższej tabeli przedstawiono dostępne właściwości w **wdrożenia** sekcji:
    
    | Właściwość | Wartość domyślna |
    | --- | --- |
    | Zezwalaj na niezaufane certyfikaty |W przypadku wartości FAŁSZ certyfikaty SSL muszą być podpisane przez urząd główny. |
    | Zezwalaj na uaktualnienie |Umożliwia wdrożenie, aby zaktualizować istniejące wdrożenie zamiast tworzenia nowej. Zachowuje adres IP. |
    | Nie usuwaj |Jeśli PRAWDA, nie zastępuj istniejącego wdrożenia niepowiązanych (uaktualnienia jest dozwolona). |
    | Ścieżka do ustawienia wdrożenia |Ścieżka do pliku .pubxml dla aplikacji sieci web, względem głównego folderu repozytorium. Ignorowane dla usługi w chmurze. |
    | Środowisko wdrażania SharePoint |Taka sama jak nazwa usługi. |
    | Środowisko wdrażania platformy Azure |Nazwa sieci web aplikacji lub w chmurze usługi. |
14. Do tego czasu kompilacji powinien zakończyło się pomyślnie.
    
     ![][28]
15. Dwukrotne kliknięcie nazwy kompilacji programu Visual Studio zawiera **podsumowanie kompilacji**, w tym wszystkie wyniki testu z skojarzone projektów testów jednostkowych.
    
     ![][29]
16. W [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), skojarzone wdrożenia można obejrzeć w **wdrożeń** karcie, gdy środowisko tymczasowe jest zaznaczone.
    
     ![][30]
17. Przejdź do adresu URL witryny. Dla aplikacji sieci web, wystarczy wybrać **Przeglądaj** przycisk w portalu. Usługi w chmurze, wybierz adres URL w **szybki przegląd** sekcji **pulpitu nawigacyjnego** strony zawierającej środowiska przemieszczania.
    
    Wdrożenia z ciągłej integracji usług w chmurze są publikowane w środowisku przemieszczania domyślnie. Możesz zmienić to ustawienie **alternatywny środowiska usługi w chmurze** właściwości **produkcji**. Oto, gdy adres URL witryny jest na stronie pulpitu nawigacyjnego usługi w chmurze.
    
    ![][31]
    
    Na nowej karcie przeglądarki będą otwierane w celu wyświetlenia uruchomionej witryny.
    
    ![][32]
18. Inne zmiany do projektu, możesz wyzwalacza więcej kompilacje i będą gromadzone wielu wdrożeń. Najnowszego jest oznaczony jako aktywny.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: należy ponownie wdrożyć wcześniejszą kompilację
Ten krok jest opcjonalny. W klasycznym portalu Azure, wybierz wcześniejsze wdrożenie, a następnie wybierz polecenie **ponownie wdrożyć** do tyłu witryny wcześniej zaewidencjonowania. Należy pamiętać, że spowoduje to wyzwalają nowej kompilacji w programie TFS i Utwórz nowy wpis w historii wdrożenia.

![][34]

## <a name="6-change-the-production-deployment"></a>6: Zmień wdrożenia produkcyjnego
Gdy wszystko będzie gotowe, możesz podwyższyć poziom środowiska przemieszczania do środowiska produkcyjnego, wybierając **wymiany** w klasycznym portalu Azure. Nowo wdrożonym środowiska przemieszczania jest podwyższany do środowiska produkcyjnego i poprzedniego środowiska produkcyjnego, jeśli taki występuje, staje się środowiska przemieszczania. Aktywne wdrożenie może się różnić w produkcyjne i przejściowe środowisk, ale Historia wdrażania ostatnie kompilacji jest taka sama niezależnie od środowiska.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7: wdrażanie z gałęzi roboczej.
Korzystając z narzędzia Git, zwykle wprowadzono zmiany w gałęzi roboczych i integracji w gałęzi głównej przy projektowaniu osiągnie stan zakończenia. Podczas fazy opracowywania projektu należy do tworzenia i wdrażania gałąź roboczą do platformy Azure.

1. W **Team Explorer**, wybierz **Home** przycisk, a następnie wybierz pozycję **gałęzie** przycisku.
   
    ![][40]
2. Wybierz **nowa gałąź** łącza.
   
    ![][41]
3. Wprowadź nazwę gałęzi, takie jak "działa", a następnie wybierz **utwórz gałąź**. Spowoduje to utworzenie nowej lokalnej gałęzi.
   
    ![][42]
4. Opublikuj gałęzi. Wybierz nazwę gałęzi w **nieopublikowanych gałęzi**i wybierz polecenie **publikowania**.
   
    ![][44]
5. Domyślnie tylko zmiany do gałęzi głównej wyzwolić kompilację ciągłe. Aby skonfigurować ciągłe kompilacji dla gałęzi roboczej, należy wybrać **kompilacje** strony **Team Explorer**i wybierz polecenie **edycji definicji kompilacji**.
6. Otwórz **ustawienia źródła** kartę. W obszarze **monitorowane gałęzi dla ciągłej integracji i kompilacji**, wybierz **kliknij tutaj, aby dodać nowy wiersz**.
   
    ![][47]
7. Określ gałęzi, z której zostały utworzone, takich jak system plików refs/głowic/pracy.
   
    ![][48]
8. Zmiany w kodzie, otwórz menu skrótów zmienionego pliku, a następnie wybierz **zatwierdzić**.
   
    ![][43]
9. Wybierz **niezsynchronizowane zatwierdzeń** łącza, a następnie wybierz pozycję **synchronizacji** przycisk lub **Push** łącza w celu skopiowania zmiany z kopią gałąź pracy w Visual Studio Team Services.
   
   ![][45]
10. Przejdź do **kompilacje** wyświetlić i Znajdź kompilacji, który właśnie został wywołany gałąź roboczą.

## <a name="next-steps"></a>Następne kroki
Aby dowiedzieć się więcej porad na przy użyciu narzędzia Git w usłudze Visual Studio Team Services, zobacz [opracowanie i udostępnianie kodu w programie Visual Studio w usłudze Git](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) oraz informacji dotyczących korzystania z repozytorium Git, który nie jest zarządzany przez program Visual Studio Team Services do publikowania na platformie Azure, zobacz [ciągłe wdrażanie w usłudze Azure App Service](../app-service-web/app-service-continuous-deployment.md). Aby uzyskać więcej informacji o programie Visual Studio Team Services, zobacz [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
