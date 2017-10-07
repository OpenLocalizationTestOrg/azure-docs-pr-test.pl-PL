---
title: "aaaAgile rozwoju oprogramowania z usługi aplikacji Azure"
description: "Dowiedz się, jak toocreate wysokiej skali złożonych aplikacji z usługi Azure App Service w taki sposób, który obsługuje programowanie zwinne oprogramowania."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Programowanie zwinne oprogramowania z usługi aplikacji Azure
W tym samouczku przedstawiono sposób toocreate wysokiej skali złożonych aplikacji z [usłudze Azure App Service](/azure/app-service/) w taki sposób, który obsługuje [agile software development](https://en.wikipedia.org/wiki/Agile_software_development). Przyjęto założenie, że już wiesz, jak za[wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md).

Ograniczeń technicznych procesów często może występować w sposób hello pomyślnego wykonania metody agile. Azure App Service przy użyciu funkcji, takich jak [ciągłego publikowanie](app-service-continuous-deployment.md), [środowiska przejściowe](web-sites-staged-publishing.md) (miejsca) i [monitorowania](web-sites-monitor.md), gdy rozsądny sposób połączone z hello aranżacji i Zarządzanie wdrożenia w [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), może być częścią doskonałe rozwiązanie dla deweloperów, którzy przyjęli zwinnego programowania.

Witaj poniższej tabeli znajduje się krótki lista wymagania związane z elastyczne programowanie i w jaki sposób usługi Azure umożliwiają każdego z nich.

| Wymaganie | Jak Azure umożliwia |
| --- | --- |
| -Kompilacji z każdym zatwierdzeniem<br>-Automatycznie utworzyć i szybkie |Gdy skonfigurowano ciągłe wdrażanie, usługi Azure App Service może działać jako kompilacji na żywo działa oparte na gałąź deweloperów. Za każdym razem, gdy kod spoczywa toohello gałęzi, jest automatycznie wbudowanych i uruchomiona na żywo na platformie Azure. |
| — Upewnić samokontroli kompilacji |Załaduj testy, testy sieci web, itp., można wdrożyć przy użyciu szablonu usługi Azure Resource Manager hello. |
| -Wykonywania testów w klonowania środowiska produkcyjnego |Szablony usługi Azure Resource Manager mogą być używane toocreate klony środowiska hello Azure środowiska produkcyjnego (w tym ustawienia aplikacji, szablony ciąg połączenia, skalowanie, itp.) do testowania szybko i przewidywalnego. |
| -Wyświetl wyniki ostatniej kompilacji łatwo |Ciągłe wdrażanie tooAzure z repozytorium oznacza, że można przetestować nowy kod w działającej aplikacji natychmiast po zatwierdzeniu zmian. |
| -Zatwierdzić gałęzi głównej toohello codziennie<br>-Zautomatyzowanie wdrożenia. |Ciągła integracja aplikacji produkcyjnych z gałęzi głównej z repozytorium jest wdrażana automatycznie co tooproduction commit/merge toohello gałęzi głównej. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Będzie wykonywać
Możesz przeprowadzi Typowy przepływ pracy deweloperów testu — etap produkcji w kolejności toopublish nowe zmiany toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) przykładowej aplikacji, która składa się z dwóch [sieci web apps](/services/app-service/web/), jeden frontonu (FE) i Witaj, inne są interfejsu API sieci Web wewnętrznej bazy danych (BE), a [bazy danych SQL](/services/sql-database/). Pracy z powitania po architektura wdrażania:

![](./media/app-service-agile-software-development/what-1-architecture.png)

Obraz powitania tooput na słowa:

* Architektura wdrażania Hello jest podzielone na trzy różne środowiska (lub [grup zasobów](../azure-resource-manager/resource-group-overview.md) na platformie Azure), każdy z własną [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [skalowanie](web-sites-scale.md) ustawienia, i bazy danych SQL. 
* Każde środowisko mogą być zarządzane oddzielnie. Nawet mogą istnieć w ramach różnych subskrypcji.
* Tymczasowych i produkcyjnych są zaimplementowane jako dwa gniazda hello tej samej aplikacji usługi app Service. Konfigurowanie Hello głównej gałęzi dla ciągłej integracji z hello miejsca.
* Gałąź toomaster zatwierdzania zostanie zweryfikowany na powitania miejsca (z danymi produkcyjnymi), hello zweryfikować tymczasowej aplikacjami jest zamieniane w gnieździe produkcyjnym hello [bez przestojów](web-sites-staged-publishing.md).

Witaj środowiska produkcyjnego i przejściowego jest definiowana za pomocą szablonu hello w [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).

Witaj deweloperów i środowisk testowych są definiowane przez szablon hello w [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).

Typowy strategii rozgałęziania hello, będą też używać z kodem przenoszenie z gałęzi deweloperów hello zapasową toohello testu gałęzi, a następnie toohello gałęzi głównej (przesunięcie w górę jakości, tak toospeak).

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>Co jest potrzebne
* Konto platformy Azure
* A [GitHub](https://github.com/) konta
* Powłoki Git (zainstalowaną z [GitHub dla systemu Windows](https://windows.github.com/)) — umożliwia można toorun, zarówno hello Git i programu PowerShell poleceń w hello sam sesji 
* Najnowsze [programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) usługi bits
* Podstawową wiedzę na temat hello następujące narzędzia:
  * [Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) wdrażania szablonu (Zobacz też [wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Należy toocomplete konto platformy Azure w tym samouczku:
> 
> * Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/) — otrzymasz kredyt płatnej usług platformy Azure można użyć tootry wychodzących, a nawet po wyczerpaniu można zachować konta hello i korzystać z bezpłatnych usług platformy Azure, takich jak aplikacje sieci Web.
> * Możesz [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -Your Visual Studio subskrypcji otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.
> 
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="set-up-your-production-environment"></a>Konfigurowanie środowiska produkcyjnego
> [!NOTE]
> skrypt Hello używane w tym samouczku automatycznie konfiguruje ciągłego publikowania z repozytorium GitHub. Wymaga to, że Twoje poświadczenia GitHub są już przechowywane na platformie Azure, w przeciwnym razie hello inicjowanych przez skrypty wdrażania kończy się niepowodzeniem podczas próby ustawienia kontroli źródła tooconfigure hello aplikacji sieci web. 
> 
> toostore Twojego GitHub poświadczenia na platformie Azure, tworzenie aplikacji sieci web w hello [portalu Azure](https://portal.azure.com/) i [skonfigurować wdrożenie GitHub](app-service-continuous-deployment.md). Wystarczy toodo raz. 
> 
> 

W typowy scenariusz DevOps masz aplikację, która działa na platformie Azure i mają toomake tooit zmiany poprzez publikowanie ciągłe. W tym scenariuszu ma szablonu tego możesz toodeploy rozwinięte, przetestowany i używany hello środowiska produkcyjnego. Można będzie skonfigurować go w tej sekcji.

1. Tworzenie własnych rozwidlenia hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repozytorium. Aby uzyskać informacje dotyczące tworzenia rozwidlenia, zobacz [rozwidlania repozytorium](https://help.github.com/articles/fork-a-repo/). Po utworzeniu rozwidlenia, można to sprawdzić w przeglądarce.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Otwórz sesję powłoki Git. Jeśli nie masz jeszcze powłoki Git, zainstaluj [GitHub dla systemu Windows](https://windows.github.com/) teraz.
3. Utwórz lokalne Sklonowanie rozwidlenia, wykonując następujące polecenia hello:

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. Po utworzeniu sieci lokalnej klonowania, przejdź zbyt*&lt;repository_root >*\ARMTemplates i deploy.ps1 hello Uruchom skrypt w następujący sposób:
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. Po wyświetleniu monitu wpisz hello Żądana nazwa użytkownika i hasło, aby uzyskać dostęp do bazy danych.
   
   Powinny pojawić się hello inicjowania obsługi administracyjnej postęp różnych zasobów platformy Azure. Po zakończeniu wdrożenia skryptu hello uruchamia aplikacji hello w przeglądarce hello i podamy przyjazne sygnału dźwiękowego.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > Spójrz na  *&lt;repository_root >*\ARMTemplates\Deploy.ps1, toosee jak generuje zasobów przy użyciu unikatowych identyfikatorów. Można użyć hello tego samego toocreate podejście klonów z hello tego samego wdrożenia bez obaw o powodujące konflikt nazw zasobów.
   > 
   > 
6. Ponownie w sesji programu Git powłoki, uruchom polecenie:
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Po zakończeniu działania skryptu hello, przejdź wstecz adres frontonu toohello toobrowse (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) toosee hello aplikacja była uruchomiona w środowisku produkcyjnym.
8. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/) i spójrz na to, co jest tworzony.
   
   Będziesz w stanie toosee dwie aplikacje sieci web w hello tej samej grupie zasobów, z hello `Api` sufiksu w nazwie hello. Jeśli przyjrzymy się widok grupy zasobów hello, możesz również Zobacz hello bazy danych SQL server, hello planu usługi aplikacji i hello przemieszczania miejsc aplikacji sieci web hello. Przeglądanie hello różne zasoby i porównaj je z  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json sposobu ich konfiguracji w szablonie hello.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

Po skonfigurowaniu teraz hello środowiska produkcyjnego. Następnie zostanie należy rozpocząć poza aplikacją toohello aktualizacji.

## <a name="create-dev-and-test-branches"></a>Tworzenie deweloperów i testowanie gałęzi
Teraz, gdy masz złożonej aplikacji uruchomionych w środowisku produkcyjnym na platformie Azure, można utworzyć aplikacji tooyour aktualizacji zgodnie z metodologii elastyczne. W tej sekcji utworzysz hello gałęzie tworzenia i testowania należy toomake hello wymagane aktualizacje.

1. Najpierw utwórz hello środowiska testowego. W sesji programu Git powłoki hello uruchom następujące polecenia środowiska hello toocreate dla nowej gałęzi o nazwie **NewUpdate**. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. Po wyświetleniu monitu wpisz hello Żądana nazwa użytkownika i hasło, aby uzyskać dostęp do bazy danych. 
   
   Po zakończeniu wdrożenia skryptu hello uruchamia aplikacji hello w przeglądarce hello i podamy przyjazne sygnału dźwiękowego. Masz teraz nowa gałąź z własnego środowiska testowego. Wykonaj tooreview obecnie kilku kwestii dotyczących tego środowiska testowego:
   
   * Można go utworzyć w dowolnej subskrypcji platformy Azure. Oznacza to, że środowiska produkcyjnego hello mogą być zarządzane oddzielnie od środowiska testowego.
   * Środowiska testowego jest uruchomiona na platformie Azure.
   * Środowiska testowego jest identyczne toohello środowiska produkcyjnego, z wyjątkiem hello przemieszczania miejsc i hello Ustawienia skalowania. Należy znać ponieważ są one hello tylko różnice między ProdandStage.json i Dev.json.
   * Środowiska testowego można zarządzać w własnego planu usługi aplikacji z warstwą inną cenę (takich jak **wolne**).
   * Usunięcie tego środowiska testowego jest tak proste, jak usuwanie hello grupy zasobów. Okaże się, jak toodo to [później](#delete).
3. Przejdź na toocreate hello gałąź deweloperów, uruchamiając następujące polecenia:
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. Po wyświetleniu monitu wpisz hello Żądana nazwa użytkownika i hasło, aby uzyskać dostęp do bazy danych. 
   
   Wykonaj kilka rzeczy, o tym środowiska deweloperskiego tooreview obecnie: 
   
   * Deweloperów środowiska pod kątem środowiska testowego identyczne toohello konfiguracji, ponieważ jest wdrożony za pomocą hello tego samego szablonu.
   * Można utworzyć każdego środowiska deweloperskiego w subskrypcji platformy Azure dla deweloperów hello, pozostawiając toobe środowiska testowego hello zarządzane oddzielnie.
   * Środowisko deweloperów jest uruchomiona na platformie Azure.
   * Usunięcie hello deweloperów środowiska jest tak proste, jak usunięcie grupy zasobów hello. Okaże się, jak toodo to [później](#delete).

> [!NOTE]
> Jeśli masz wiele deweloperów pracujących na nową aktualizację hello każdego z nich prosty sposób tworzyć gałęzi i środowiska deweloperskiego dedykowanych z hello następujące kroki:
> 
> 1. Tworzenie własnych rozwidlenia hello repozytorium w usłudze GitHub (zobacz [rozwidlania repozytorium](https://help.github.com/articles/fork-a-repo/)).
> 2. Klonowanie rozwidlenia hello na komputerze lokalnym
> 3. Uruchom hello same polecenia toocreate własnych gałęzi deweloperów i środowiska.
> 
> 

Gdy wszystko będzie gotowe, rozwidlenia GitHub powinny mieć trzy gałęzie:

![](./media/app-service-agile-software-development/test-1-github-view.png)

I powinien mieć sześć aplikacji sieci web (trzy zestawy dwóch) w trzech oddzielnych grup zasobów:

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json określa hello toouse środowiska produkcyjnego hello **standardowe** cenowym, który jest odpowiedni do skalowania aplikacji produkcyjnej hello.
> 
> 

## <a name="build-and-test-every-commit"></a>Tworzenie i testowanie każdym zatwierdzeniem
Witaj pliki szablonów ProdAndStage.json i Dev.json już Określ hello parametry kontroli źródła, która domyślnie konfiguruje ciągłego publikowania dla aplikacji sieci web hello. W związku z tym każdy oddział GitHub toohello zatwierdzania wyzwala tooAzure automatyczne wdrożenie tej gałęzi. Zobaczmy, jak ustawienia działa teraz.

1. Upewnij się, że jesteś w gałęzi deweloperów hello hello lokalnego repozytorium. toodo tego hello uruchom następujące polecenie w powłoce Git:
   
        git checkout Dev
2. Wprowadzić warstwy interfejsu użytkownika aplikacji toohello zmiany, zmieniając hello kodu toouse [Bootstrap](http://getbootstrap.com/components/) listy. Otwórz  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml i udostępnić hello po podświetlony zmiany:
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > Jeśli nie można odczytać hello poprzedzających obrazu: 
    > 
    > * W wierszu 18 Zmień `check-list` zbyt`list-group`.
    > * W wierszu 19 Zmień `class="check-list-item"` zbyt`class="list-group-item"`.
    > 
    > 
3. Zapisz zmiany hello. Ponownie uruchom hello następujące polecenia w powłoce Git:
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   Te polecenia git są podobne, zbyt "Sprawdzanie w kodzie" w inny system kontroli źródła, takich jak TFS. Po uruchomieniu `git push`, zatwierdzania nowych hello wyzwala tooAzure wypychania automatyczne kodu, który następnie odtwarza hello zmiana hello tooreflect aplikacji hello deweloperów środowiska.
4. tooverify, która nastąpiła środowiska deweloperskiego tooyour ten kod wypychania, przejdź na stronę aplikacji sieci web środowiska deweloperskiego tooyour i przyjrzyj się hello **wdrożenia** części. Powinno być możliwe toosee Twojego najnowszym zatwierdzeniu komunikatu.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. Z tego miejsca, kliknij przycisk **Przeglądaj** toosee hello nową zmianę w działającej aplikacji hello na platformie Azure.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   Jest to aplikacja toohello drobne zmiany. Jednak wiele razy nowej zmiany tooa złożonych aplikacji sieci web ma niezamierzone i niepożądane skutki uboczne. Trwa testu stanie tooeasily każdym zatwierdzeniem w kompilacjach na żywo umożliwia toocatch można te problemy przed klientów widoczne.

Chwili powinna być doświadczenia z realizacją hello który dewelopera na powitania **NewUpdate** projektu, można utworzyć środowiska deweloperskiego dla siebie, a następnie kompilacji każdym zatwierdzeniem i testowania każdej kompilacji.

## <a name="merge-code-into-test-environment"></a>Scalanie kodu w środowisku testowym
Jeśli wszystko jest gotowe toopush kodu z deweloperów gałęzi zapasową tooNewUpdate gałęzi, jest hello git standardowy proces:

1. Scala wszystkie nowe tooNewUpdate zatwierdzeń hello gałęzi deweloperów w witrynie GitHub, takich jak zatwierdzeń tworzone przez innych. Wszystkie nowe zatwierdzenia w serwisie GitHub wyzwala wypychania kodu i kompilacji w środowisku testowym hello. Można następnie upewnij się, że kod w gałęzi deweloperów wciąż działa z bitami najnowsze hello NewUpdate gałęzi.
2. Scal wszystkie nowe zatwierdzenia z gałęzi deweloperów w gałęzi NewUpdate w witrynie GitHub. Ta akcja wyzwala wypychania kodu i kompilacji w środowisku testowym hello. 

Pamiętaj, że ponieważ ciągłego wdrażania jest już skonfigurowane z tymi gałęziami git, nie potrzebujesz tootake kompilacje innych działań, takich jak z integracją. Należy po prostu rozwiązań formantu standardowego źródła tooperform przy użyciu usługi git i Azure wykonuje wszystkie procesy kompilacji hello.

Teraz załóżmy zbyt wypchnąć kod**NewUpdate** gałęzi. W powłoce Git uruchom następujące polecenia hello:

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

Gotowe. 

Strony aplikacji sieci web przejdź toohello dla Twojego toosee środowiska testowego Twoje nowe zatwierdzenia (scalone do gałęzi NewUpdate) teraz wypychana toohello środowiska testowego. Następnie kliknij przycisk **Przeglądaj** toosee, który hello Zmień styl jest teraz uruchomiona na platformie Azure.

## <a name="deploy-update-tooproduction"></a>Wdrażanie aktualizacji tooproduction
Wypychanie kodu toohello środowiska przemieszczania i produkcji powinien uznać nie różni się od co zostało już wykonane po naciśnięciu środowiska testowego toohello kodu. Jest naprawdę proste. 

W powłoce Git uruchom następujące polecenia hello:

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

Należy pamiętać, że oparte na środowisku przemieszczania i produkcji hello jest ustawiany w ProdandStage.json sposób hello, nowy kod spoczywa toohello **przemieszczania** gniazdo i działa. Tak w przypadku przejścia miejsca przemieszczania toohello adres URL, zostanie wyświetlony kod nowego hello istnieje uruchomiona. toodo tego hello uruchom następujące polecenia cmdlet w powłoce Git.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

I teraz, po zweryfikowaniu hello aktualizacji w hello miejsca hello tylko po lewej toodo się tooswap go w środowisku produkcyjnym. W powłoce Git uruchom następujące polecenia hello:

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

Gratulacje! Został pomyślnie opublikowany nowej aplikacji sieci web produkcji tooyour aktualizacji. Co więcej jest który czy przez łatwe tworzenie środowisk tworzenia i testowania i tworzenia i testowania każdym zatwierdzeniem. Są to kluczowe bloków konstrukcyjnych dla rozwoju oprogramowania elastyczne.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>Usuń deweloperów i przetestować środowisk
Ponieważ celowo efekt programu deweloperów i przetestować grup zasobów niezależne toobe środowiskach, jest łatwe toodelete je. toodelete hello te, które są tworzone w tym samouczku, zarówno hello GitHub gałęzie i artefaktów Azure, uruchom następujące polecenia w powłoce Git hello:

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>Podsumowanie
Programowanie zwinne oprogramowania jest obowiązkowa wielu firm, którzy chcą tooadopt Azure jako ich platformę aplikacji. W tym samouczku uzyskanych jak toocreate i zakończenia dokładne replik w dół lub w jego pobliżu repliki hello środowiska produkcyjnego z łatwością, nawet w przypadku złożonych aplikacji. Również wiesz już, jak tooleverage toocreate tej możliwości programowania przetworzyć który można zbudowanie i przetestowanie co jednego zatwierdzenia na platformie Azure. W tym samouczku wykazało miejmy nadzieję, najlepiej korzystania z usługi aplikacji Azure i usługi Azure Resource Manager razem toocreate przeznaczoną metodologii tooagile rozwiązania DevOps. Następnie można tworzyć w tym scenariuszu, wykonując takie jak zaawansowane techniki DevOps [testowanie w produkcji](app-service-web-test-in-production-get-start.md). Dla typowego scenariusza testowanie w produkcji, zobacz [Flighting wdrożenia (testowania wersji beta) w usłudze Azure App Service](app-service-web-test-in-production-controlled-test-flight.md).

## <a name="more-resources"></a>Więcej zasobów
* [Wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md)
* [Elastyczne programowanie w praktyce: porady i wskazówki dotyczące cyklu zmodernizowanej programowanie](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [Strategie zaawansowanego wdrożenia dla aplikacji sieci Web platformy Azure przy użyciu szablonów usługi Resource Manager](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - hello JSON modułu sprawdzania poprawności](http://jsonlint.com/)
* [ARMClient — Konfigurowanie publikowania toosite GitHub](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [Rozgałęzianie Git — podstawowe rozgałęzianie i scalanie](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Blog Dominik Ebbo](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Narzędzi wiersza polecenia platformy Azure i Platform](../cli-install-nodejs.md)
* [Tworzenie lub edytowanie użytkowników w usłudze Azure AD](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [Witryna typu Wiki Kudu projektu](https://github.com/projectkudu/kudu/wiki)

