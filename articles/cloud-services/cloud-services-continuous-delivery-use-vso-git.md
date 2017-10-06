---
title: dostarczanie aaaContinuous Git i Visual Studio Team Services na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconfigure programu Visual Studio Team Services projekty zespołowe toouse Git tooautomatically tworzenie i wdrażanie toohello funkcji aplikacji sieci Web w usługach Azure App Service lub w chmurze."
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
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a>TooAzure ciągłego dostarczania przy użyciu programu Visual Studio Team Services i Git
Można użyć toohost projektów programu Visual Studio Team Services team repozytorium Git do kodu źródłowego i automatycznie tworzenie i wdrażanie aplikacji sieci web tooAzure lub usług w chmurze przy każdym push repozytorium toohello zatwierdzania.

Będziesz potrzebować programu Visual Studio 2013 oraz hello zainstalowany zestaw SDK platformy Azure. Jeśli nie masz jeszcze programu Visual Studio 2013, pobierz ją, wybierając hello **zacznij pracę bezpłatnie** łączenie z [www.visualstudio.com](http://www.visualstudio.com). Zainstaluj hello zestawu Azure SDK w [tutaj](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Należy toocomplete konta usługi Visual Studio Team Services w tym samouczku: możesz [otworzyć bezpłatne konto usługi Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset się tooautomatically usługi chmury tworzenie i wdrażanie tooAzure przy użyciu programu Visual Studio Team Services, wykonaj następujące kroki.

## <a name="1-create-a-git-repository"></a>1: Tworzenie repozytorium Git
1. Jeśli nie masz już konto usługi Visual Studio Team Services, możesz ją uzyskać, [tutaj](http://go.microsoft.com/fwlink/?LinkId=397665). Podczas tworzenia projektu zespołowego, wybierz Git jako system kontroli źródła. Postępuj zgodnie z projektu zespołowego tooyour hello instrukcje tooconnect programu Visual Studio.
2. W **Team Explorer**, wybierz hello **Klonuj to repozytorium** łącza.
   
    ![][3]
3. Określ lokalizację hello hello kopii lokalnej, a następnie wybierz pozycję hello **klonowania** przycisku.

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a>2: utworzenie projektu i przekazać go toohello repozytorium
1. W **Team Explorer**, w hello **rozwiązań** wybierz hello **nowy** toocreate nowy projekt w repozytorium lokalne powitania łącza.
   
    ![][4]
2. Możesz wdrożyć aplikację sieci web lub usługi w chmurze (Azure aplikacja) przez hello następujące kroki w tym przewodniku. Utwórz nowy projekt usługi w chmurze Azure lub nowy projekt ASP.NET MVC. Upewnij się, że elementy docelowe projektu hello hello .NET Framework 4 lub nowszy. W przypadku tworzenia projektu usługi w chmurze, Dodaj rolę sieci web programu ASP.NET MVC i roli proces roboczy.
   Toocreate aplikacji sieci web, wybierz opcję hello **aplikacji sieci Web ASP.NET** projektu szablonu, a następnie wybierz pozycję **MVC**. Zobacz [tworzenie aplikacji sieci web platformy ASP.NET w usłudze Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) Aby uzyskać więcej informacji.
3. Otwórz menu skrótów hello hello rozwiązania i wybierz polecenie **zatwierdzić**.
   
    ![][7]
4. Jeśli jest to hello używano Git w Visual Studio Team Services po raz pierwszy, musisz tooprovide tooidentify niektórych informacji samodzielnie w usłudze Git. W hello **oczekujących zmian** obszar **Team Explorer**, wprowadź nazwy użytkownika i adres e-mail. Wprowadź komentarz dotyczący hello zatwierdzania, a następnie wybierz pozycję hello **zatwierdzania** przycisku.
   
    ![][8]
5. Należy zwrócić uwagę tooinclude opcje hello lub wykluczyć określone zmiany wprowadzone podczas ewidencjonowania. Jeśli zmiany hello chcesz są wyłączone, wybierz **obejmują wszystkie**.
6. Masz teraz hello zatwierdzić zmiany w lokalnej kopii hello repozytorium. Następnie synchronizacji wprowadzonych zmian z serwera hello, wybierając hello **synchronizacji** łącza.

## <a name="3-connect-hello-project-tooazure"></a>3: łączenie hello tooAzure projektu
1. Teraz, gdy masz repozytorium Git w Visual Studio Team Services z kodu źródłowego w nim są gotowe tooconnect Twojego tooAzure repozytorium git.  W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), wybierz użytkownika chmury usługi lub aplikacji sieci web lub Utwórz nową, wybierając Witaj + ikonę w lewy dolny hello i wybierając polecenie **usługi w chmurze** lub **aplikacji sieci Web**, a następnie **szybkie tworzenie**.
   
    ![][9]
2. Usługi w chmurze, wybrać hello **skonfigurować publikowanie za pomocą usługi Visual Studio Team Services** łącza. W przypadku aplikacji sieci web, wybierz hello **Konfigurowanie wdrażania z kontroli źródła** łącza.
   
    ![][10]
3. W Kreatorze hello, wpisz nazwę hello Twojego konta Visual Studio Team Services w polu tekstowym hello i wybierz polecenie hello **autoryzować teraz** łącza. Użytkownik może zostać poproszony toosign w.
   
    ![][11]
4. W hello **żądania połączenia** podręczne okno dialogowe, wybierz **Akceptuj** tooauthorize Azure tooconfigure Twojego zespołu projektu w programie Visual Studio Team Services.
   
    ![][12]
5. Po autoryzacji zakończy się powodzeniem, zostanie wyświetlona lista rozwijana zawierający projektach zespołowych Visual Studio Team Services.  Wybierz nazwę projektu zespołowego, który został utworzony w poprzednich krokach hello hello, a następnie wybierz przycisk znacznika wyboru hello kreatora.
   
    ![][13]
   
    Hello następnym push repozytorium tooyour zatwierdzania, Visual Studio Team Services skompiluje oraz wdrożyć tooAzure Twojego projektu.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: wyzwolenia kompilowania i wdrożenie projektu
1. W programie Visual Studio otwarcia pliku i zmodyfikuj go. Na przykład zmienić plik hello `_Layout.cshtml` w obszarze widoki hello\\udostępniony folder w roli sieci web MVC.
   
    ![][17]
2. Edytuj tekst stopki hello hello lokacji i Zapisz plik hello.
   
    ![][18]
3. W **Eksploratora rozwiązań**, otwórz menu skrótów hello hello rozwiązania węzła, węzeł projektu lub hello plików można zmienić, a następnie wybierz **zatwierdzić**.
4. Wpisz komentarz i wybierz **zatwierdzić**.
   
    ![][20]
5. Wybierz hello **synchronizacji** łącza.
   
    ![][38]
6. Wybierz hello **Push** link toopush repozytorium toohello zatwierdzania w Visual Studio Team Services. (Można również użyć hello **synchronizacji** przycisk toocopy repozytorium toohello zatwierdzeń. Hello różnicą jest to, że **synchronizacji** również ściąga hello najnowsze zmiany z repozytorium hello.)
   
    ![][39]
7. Wybierz hello **macierzystego** toohello tooreturn przycisk **Team Explorer** strony głównej.
   
    ![][21]
8. Wybierz **kompilacje** tooview hello kompilacje w toku.
   
    ![][22]
   
    **Team Explorer** pokazuje, że zostało wyzwolone kompilacji do zaewidencjonowania.
   
    ![][23]
9. tooview szczegółowy dziennik jako hello kompilacji realizowany, kliknij dwukrotnie nazwę hello hello kompilacji w toku.
10. Podczas kompilacji hello jest w toku, Przyjrzyjmy się hello definicji kompilacji, która została utworzona stosowania hello kreatora toolink tooAzure.  Otwórz menu skrótów powitania dla definicji kompilacji hello i wybierz polecenie **edycji definicji kompilacji**.
    
    ![][25]
11. W hello **wyzwalacza** kartę, zobaczysz, że hello definicji kompilacji jest domyślnie toobuild na każdym zaewidencjonowania. (Dla usługi w chmurze, Visual Studio Team Services tworzy i wdraża toohello głównej gałęzi hello automatycznie przemieszczania środowiska. Nadal masz toodo lokacji na żywo toohello toodeploy krok wykonywany ręcznie. Dla aplikacji sieci web, która nie ma w środowisku przemieszczania wdrażania hello głównej gałęzi bezpośrednio toohello live lokacji.
    
    ![][26]
12. W hello **procesu** karcie widać środowiska wdrażania hello jest ustawiona na nazwę toohello Twojego chmury usługi lub aplikacji sieci web.
    
     ![][27]
13. Określ wartości dla właściwości hello, jeśli chcesz, aby wartości innej niż domyślne hello. Witaj właściwości publikowania platformy Azure znajdują się w hello **wdrożenia** sekcji, a także mogą wymagać tooset MSBuild parametrów. Na przykład w projektu usługi w chmurze, toospecify konfiguracji usługi, innych niż "Chmura" Ustaw parametry MSbuild hello zbyt`/p:TargetProfile=[YourProfile]` gdzie *[YourProfile]* pasuje do pliku konfiguracji usługi z nazwą, np. Element ServiceConfiguration. *YourProfile*.cscfg.
    
     Witaj poniższej tabeli przedstawiono dostępne właściwości hello hello **wdrożenia** sekcji:
    
    | Właściwość | Wartość domyślna |
    | --- | --- |
    | Zezwalaj na niezaufane certyfikaty |W przypadku wartości FAŁSZ certyfikaty SSL muszą być podpisane przez urząd główny. |
    | Zezwalaj na uaktualnienie |Umożliwia tooupdate wdrożenia hello istniejącego wdrożenia zamiast tworzenia nowej. Zachowuje hello adresu IP. |
    | Nie usuwaj |Jeśli PRAWDA, nie zastępuj istniejącego wdrożenia niepowiązanych (uaktualnienia jest dozwolona). |
    | Ścieżka tooDeployment ustawienia |Witaj ścieżki tooyour .pubxml pliku dla aplikacji sieci web, toohello względną głównego folderu repozytorium hello. Ignorowane dla usługi w chmurze. |
    | Środowisko wdrażania SharePoint |Witaj takie same jak nazwa usługi hello. |
    | Środowisko wdrażania platformy Azure |Witaj aplikacji lub w chmurze nazwę usługi sieci web. |
14. Do tego czasu kompilacji powinien zakończyło się pomyślnie.
    
     ![][28]
15. Dwukrotne kliknięcie nazwy kompilacji hello Visual Studio zawiera **podsumowanie kompilacji**, w tym wszystkie wyniki testu z skojarzone projektów testów jednostkowych.
    
     ![][29]
16. W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), można wyświetlić hello skojarzone wdrożenie na powitania **wdrożeń** karcie po wybraniu hello przemieszczania środowiska.
    
     ![][30]
17. Adres URL witryny tooyour przeglądania. Dla aplikacji sieci web, wystarczy wybrać hello **Przeglądaj** przycisk w portalu hello. Usługi w chmurze, wybierz adres URL hello hello **szybki przegląd** sekcji hello **pulpitu nawigacyjnego** strony zawierającej hello środowiska przemieszczania.
    
    Wdrożenia z ciągłej integracji usług w chmurze są środowiska przemieszczania opublikowanych toohello domyślnie. Można zmienić to ustawienie hello **alternatywny środowiska usługi w chmurze** właściwości zbyt**produkcji**. Oto, gdy adres URL witryny hello znajduje się na stronie pulpitu nawigacyjnego usługi chmury hello.
    
    ![][31]
    
    Na nowej karcie przeglądarki zostanie otwarty tooreveal uruchomionej witryny.
    
    ![][32]
18. Po wprowadzeniu innych zmian projektu tooyour, możesz wyzwalacza więcej kompilacje i będą gromadzone wielu wdrożeń. Witaj najnowszych jeden jest oznaczony jako aktywny.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: należy ponownie wdrożyć wcześniejszą kompilację
Ten krok jest opcjonalny. Witaj klasycznego portalu Azure, wybierz wcześniejsze wdrożenie i wybierz **ponownie wdrożyć** toorewind tooan Twojego lokacji do wcześniej w zaewidencjonowania. Należy pamiętać, że spowoduje to wyzwalają nowej kompilacji w programie TFS i Utwórz nowy wpis w historii wdrożenia.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: Zmień hello wdrożenia produkcyjnego
Gdy wszystko będzie gotowe, możesz podwyższyć poziom środowiska produkcyjnego toohello dla hello przemieszczania, wybierając **wymiany** w hello klasycznego portalu Azure. Hello nowo wdrożone środowiska przemieszczania jest awansowana tooProduction i hello poprzedniego środowiska produkcyjnego, jeśli taki występuje, staje się środowiska przemieszczania. Hello aktywnych wdrożeń mogą być różne dla środowisk przemieszczania i hello produkcji, ale Historia wdrażania hello ostatnie kompilacji jest hello sama niezależnie od tego środowiska.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7: wdrażanie z gałęzi roboczej.
Korzystając z narzędzia Git, zwykle wprowadzono zmiany w gałęzi roboczych i integrowanie hello głównej gałęzi przy projektowaniu osiągnie stan zakończenia. W fazie hello rozwoju projektu możesz mają toobuild i wdrożyć tooAzure gałęzi roboczych hello.

1. W **Team Explorer**, wybierz hello **Home** przycisk, a następnie wybierz pozycję hello **gałęzie** przycisku.
   
    ![][40]
2. Wybierz hello **nowa gałąź** łącza.
   
    ![][41]
3. Wprowadź nazwę hello hello gałęzi, takie jak "działa" i wybierz polecenie **utwórz gałąź**. Spowoduje to utworzenie nowej lokalnej gałęzi.
   
    ![][42]
4. Opublikuj gałęzi hello. Wybierz nazwę gałęzi hello w **nieopublikowanych gałęzi**i wybierz polecenie **publikowania**.
   
    ![][44]
5. Domyślnie tylko zmiany toohello głównej gałęzi wyzwalacza ciągłego kompilacji. tooset się ciągłe kompilacji dla gałęzi roboczej, wybierz hello **kompilacje** strony **Team Explorer**i wybierz polecenie **edycji definicji kompilacji**.
6. Otwórz hello **ustawienia źródła** kartę. W obszarze **monitorowane gałęzi dla ciągłej integracji i kompilacji**, wybierz **kliknij tutaj tooadd nowy wiersz**.
   
    ![][47]
7. Określ hello gałęzi, z której zostały utworzone, takich jak system plików refs/głowic/pracy.
   
    ![][48]
8. Zmiany w kodzie hello hello Otwórz menu skrótów dla pliku hello zmienione, a następnie wybierz pozycję **zatwierdzić**.
   
    ![][43]
9. Wybierz hello **niezsynchronizowane zatwierdzeń** łącza, a następnie wybierz pozycję hello **synchronizacji** przycisku lub hello **Push** link toocopy hello zmienia toohello kopię gałąź roboczą hello w programie Visual Studio Usługi Team Services.
   
   ![][45]
10. Przejdź toohello **kompilacje** wyświetlić i Znajdź gałąź roboczą hello hello kompilacji, który właśnie został wywołany.

## <a name="next-steps"></a>Następne kroki
Zobacz więcej porad w usłudze Visual Studio Team Services przy użyciu narzędzia Git toolearn [opracowanie i udostępnianie kodu w usłudze Git przy użyciu programu Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) oraz aby uzyskać informacje dotyczące korzystania z repozytorium Git, który nie jest zarządzany przez toopublish Visual Studio Team Services tooAzure, zobacz [tooAzure ciągłego wdrażania aplikacji usługi](../app-service-web/app-service-continuous-deployment.md). Aby uzyskać więcej informacji o programie Visual Studio Team Services, zobacz [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

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
