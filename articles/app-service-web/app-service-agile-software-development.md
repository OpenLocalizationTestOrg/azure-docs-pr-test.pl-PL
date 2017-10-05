---
title: "Programowanie zwinne oprogramowania z usługi aplikacji Azure"
description: "Dowiedz się, jak utworzyć wysokiej skali złożonych aplikacji z usługi Azure App Service w taki sposób, który obsługuje programowanie zwinne oprogramowania."
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
ms.openlocfilehash: 5ed888cbb422766cf2094f5980dfd1c599bd431c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Programowanie zwinne oprogramowania z usługi aplikacji Azure
Z tego samouczka, dowiesz tworzenie złożonych aplikacji wysokiej skali z [usłudze Azure App Service](/azure/app-service/) w taki sposób, który obsługuje [agile software development](https://en.wikipedia.org/wiki/Agile_software_development). Przyjęto założenie, że już wiesz, jak [wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md).

Ograniczenia w procesach techniczne często może stanowić przeszkodę dla pomyślnego wykonania metody agile. Azure App Service przy użyciu funkcji, takich jak [ciągłego publikowanie](app-service-continuous-deployment.md), [środowiska przejściowe](web-sites-staged-publishing.md) (gniazda) i [monitorowania](web-sites-monitor.md)po połączeniu rozsądny sposób z aranżacji i zarządzanie wdrożenia w [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), może być częścią doskonałe rozwiązanie dla deweloperów, którzy przyjęli agile software development.

Poniższa tabela jest krótką listę wymagań skojarzonych z elastyczne programowanie i w jaki sposób usługi Azure umożliwiają każdego z nich.

| Wymaganie | Jak Azure umożliwia |
| --- | --- |
| -Kompilacji z każdym zatwierdzeniem<br>-Automatycznie utworzyć i szybkie |Gdy skonfigurowano ciągłe wdrażanie, usługi Azure App Service może działać jako kompilacji na żywo działa oparte na gałąź deweloperów. Za każdym razem, gdy kod zostanie przypisany do gałęzi, automatycznie wbudowanych i jest uruchomiona na platformie Azure. |
| — Upewnić samokontroli kompilacji |Załaduj testy, testy sieci web, itp., można wdrożyć przy użyciu szablonu usługi Azure Resource Manager. |
| -Wykonywania testów w klonowania środowiska produkcyjnego |Szablony usługi Azure Resource Manager może służyć do tworzenia klony środowiska Azure środowiska produkcyjnego (w tym ustawienia aplikacji, szablony ciąg połączenia, skalowanie, itp.) do testowania szybko i właściwie. |
| -Wyświetl wyniki ostatniej kompilacji łatwo |Ciągłe wdrażanie na platformie Azure z repozytorium oznacza, że można przetestować nowy kod w działającej aplikacji natychmiast po zatwierdzeniu zmian. |
| -Przekazać do gałęzi głównej codziennie<br>-Zautomatyzowanie wdrożenia. |Ciągła integracja aplikacji produkcyjnych z gałęzi głównej z repozytorium jest wdrażana automatycznie co commit/merge do gałęzi głównej w środowisku produkcyjnym. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Będzie wykonywać
Przeprowadzi przez typowy przepływ pracy etapie produkcji, deweloperów testu w — w celu publikowania nowych zmian [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) przykładowej aplikacji, która składa się z dwóch [sieci web apps](/services/app-service/web/), co trwa frontonu (FE), a druga jest interfejs API sieci Web wewnętrznej bazy danych (BE) i [bazy danych SQL](/services/sql-database/). Pracy z architekturą następujące wdrożenia:

![](./media/app-service-agile-software-development/what-1-architecture.png)

Aby wprowadzić obraz na słowa:

* Architektura wdrażania jest podzielone na trzy różne środowiska (lub [grup zasobów](../azure-resource-manager/resource-group-overview.md) na platformie Azure), każdy z własną [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [skalowanie](web-sites-scale.md) ustawienia i bazy danych SQL. 
* Każde środowisko mogą być zarządzane oddzielnie. Nawet mogą istnieć w ramach różnych subskrypcji.
* Tymczasowych i produkcyjnych są zaimplementowane jako dwa gniazda z tej samej aplikacji usługi aplikacji. Skonfigurowano głównej gałęzi dla ciągłej integracji z miejsca przemieszczania.
* Podczas przekazywania do głównej gałęzi jest weryfikowany na miejsce wystawiania (z danymi produkcyjnymi), zweryfikowano aplikacji przemieszczania jest zamieniane do miejsca produkcji [bez przestojów](web-sites-staged-publishing.md).

W środowisku produkcyjnym i pomostowym jest definiowana za pomocą szablonu w [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).

W środowiskach programistycznych i testowych są definiowane przez szablon w [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).

Typowy strategii rozgałęziania, będą też używać z kodem przenoszenie z deweloperów gałęzi do gałęzi testu, następnie do gałęzi głównej (przeniesienie w górę jakości, więc do speak).

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>Co jest potrzebne
* Konto platformy Azure
* A [GitHub](https://github.com/) konta
* Powłoka Git (zainstalowaną z [GitHub dla systemu Windows](https://windows.github.com/)) — umożliwia uruchamianie poleceń programu PowerShell i Git w tej samej sesji 
* Najnowsze [programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) usługi bits
* Podstawową wiedzę na temat następujących narzędzi:
  * [Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) wdrażania szablonu (Zobacz też [wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Do ukończenia tego samouczka jest potrzebne konto platformy Azure.
> 
> * Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/) — otrzymasz kredyt służy do wypróbowania płatnych usług Azure, a nawet po wyczerpaniu możesz zachować konto i korzystać z bezpłatnych usług platformy Azure, takich jak aplikacje sieci Web.
> * Możesz [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -Your Visual Studio subskrypcji otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.
> 
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="set-up-your-production-environment"></a>Konfigurowanie środowiska produkcyjnego
> [!NOTE]
> Skrypt używany w tym samouczku automatycznie konfiguruje ciągłego publikowania z repozytorium GitHub. Wymaga to, czy Twoje poświadczenia GitHub są już przechowywane na platformie Azure, w przeciwnym razie inicjowanych przez skrypty wdrażania zakończy się niepowodzeniem podczas próby skonfigurowania ustawień kontroli źródła dla aplikacji sieci web. 
> 
> Aby przechowywać swoje poświadczenia usługi GitHub na platformie Azure, tworzenie aplikacji sieci web w [portalu Azure](https://portal.azure.com/) i [skonfigurować wdrożenie GitHub](app-service-continuous-deployment.md). Wystarczy wykonać jeden raz. 
> 
> 

W typowy scenariusz DevOps masz aplikację, która działa na platformie Azure, i chcesz wprowadzić zmiany poprzez publikowanie ciągłe. W tym scenariuszu należy szablon, który rozwinięte, testowana i używana do wdrażania w środowisku produkcyjnym. Można będzie skonfigurować go w tej sekcji.

1. Tworzenie własnych rozwidlenia [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repozytorium. Aby uzyskać informacje dotyczące tworzenia rozwidlenia, zobacz [rozwidlania repozytorium](https://help.github.com/articles/fork-a-repo/). Po utworzeniu rozwidlenia, można to sprawdzić w przeglądarce.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Otwórz sesję powłoki Git. Jeśli nie masz jeszcze powłoki Git, zainstaluj [GitHub dla systemu Windows](https://windows.github.com/) teraz.
3. Utwórz lokalne Sklonowanie rozwidlenia, wykonując następujące polecenie:

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. Po utworzeniu sieci lokalnej klonowania, przejdź do  *&lt;repository_root >*\ARMTemplates i uruchomić deploy.ps1 skrypt w następujący sposób:
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. Po wyświetleniu monitu wpisz odpowiednią nazwę użytkownika i hasło dostępu do bazy danych.
   
   Postęp inicjowania obsługi administracyjnej z różnymi zasobami Azure powinna zostać wyświetlona. Po zakończeniu wdrażania, skrypt uruchamia aplikację w przeglądarce i podamy przyjazne sygnału dźwiękowego.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > Spójrz na  *&lt;repository_root >*\ARMTemplates\Deploy.ps1, aby zobaczyć, jak generuje zasobów przy użyciu unikatowych identyfikatorów. Te same podejście umożliwia utworzenie klony tego samego wdrożenia bez obaw o powodujące konflikt nazw zasobów.
   > 
   > 
6. Ponownie w sesji programu Git powłoki, uruchom polecenie:
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Po zakończeniu działania skryptu, przejdź wstecz, aby przejść do adresu serwera sieci Web (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) aby zobaczyć aplikacja była uruchomiona w środowisku produkcyjnym.
8. Zaloguj się do [portalu Azure](https://portal.azure.com/) i spójrz na to, co jest tworzony.
   
   Powinny być widoczne dwie aplikacje sieci web w tej samej grupie zasobów, z `Api` sufiksu w nazwie. Jeśli przyjrzymy się widok grupy zasobów, można również sprawdzić bazy danych SQL i serwera, plan usługi aplikacji i tymczasowej miejsc aplikacji sieci web. Przechodzenie przez różne zasoby i porównaj je z  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json aby zobaczyć, jak są konfigurowane w szablonie.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

Teraz można zainstalować w środowisku produkcyjnym. Następnie zostanie należy rozpocząć poza nowe aktualizacje do aplikacji.

## <a name="create-dev-and-test-branches"></a>Tworzenie deweloperów i testowanie gałęzi
Teraz, gdy masz złożonej aplikacji uruchomionych w środowisku produkcyjnym na platformie Azure będzie aktualizacji do aplikacji zgodnie z metodologii elastyczne. W tej sekcji utworzysz deweloperów i przetestować gałęzie, które należy udostępnić wymagane aktualizacje.

1. Najpierw utwórz środowiska testowego. W sesji programu Git powłoki, uruchom następujące polecenia, aby utworzyć środowisko dla nowej gałęzi o nazwie **NewUpdate**. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. Po wyświetleniu monitu wpisz odpowiednią nazwę użytkownika i hasło dostępu do bazy danych. 
   
   Po zakończeniu wdrażania, skrypt uruchamia aplikację w przeglądarce i podamy przyjazne sygnału dźwiękowego. Masz teraz nowa gałąź z własnego środowiska testowego. Poświęć chwilę, aby sprawdzić kilka rzeczy, o tego środowiska testowego:
   
   * Można go utworzyć w dowolnej subskrypcji platformy Azure. Oznacza to, że w środowisku produkcyjnym może być zarządzane oddzielnie od środowiska testowego.
   * Środowiska testowego jest uruchomiona na platformie Azure.
   * Środowiska testowego jest identyczne do środowiska produkcyjnego, z wyjątkiem miejsc przemieszczania i ustawień. Należy znać ponieważ są one tylko różnice między ProdandStage.json i Dev.json.
   * Środowiska testowego można zarządzać w własnego planu usługi aplikacji z warstwą inną cenę (takich jak **wolne**).
   * Usunięcie tego środowiska testowego jest tak proste, jak usunięcie grupy zasobów. Okaże się, jak to zrobić [później](#delete).
3. Przejdź do utwórz gałąź deweloperów, uruchamiając następujące polecenia:
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. Po wyświetleniu monitu wpisz odpowiednią nazwę użytkownika i hasło dostępu do bazy danych. 
   
   Poświęć chwilę, aby sprawdzić kilka rzeczy, o tym środowisku testowym: 
   
   * Środowisko deweloperów ma konfigurację identyczne do środowiska testowego, ponieważ nie została wdrożona przy użyciu tego samego szablonu.
   * Można utworzyć każdego środowiska deweloperskiego w subskrypcji platformy Azure dla deweloperów, pozostawiając środowiska testowego, które mają być zarządzane oddzielnie.
   * Środowisko deweloperów jest uruchomiona na platformie Azure.
   * Usunięcie środowiska deweloperskiego jest tak proste, jak usunięcie grupy zasobów. Okaże się, jak to zrobić [później](#delete).

> [!NOTE]
> Jeśli masz wiele deweloperów pracujących na nową aktualizację każdego z nich łatwo utworzyć gałęzi i środowiska deweloperskiego dedykowanych następujące czynności:
> 
> 1. Tworzenie własnych rozwidlenia repozytorium w usłudze GitHub (zobacz [rozwidlania repozytorium](https://help.github.com/articles/fork-a-repo/)).
> 2. Klonowanie rozwidlenia na komputerze lokalnym
> 3. Uruchom te same polecenia do tworzenia własnych gałęzi deweloperów i środowiska.
> 
> 

Gdy wszystko będzie gotowe, rozwidlenia GitHub powinny mieć trzy gałęzie:

![](./media/app-service-agile-software-development/test-1-github-view.png)

I powinien mieć sześć aplikacji sieci web (trzy zestawy dwóch) w trzech oddzielnych grup zasobów:

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> W środowisku produkcyjnym używanie określa ProdandStage.json **standardowe** cenowym, który jest odpowiedni do skalowania aplikacji produkcyjnej.
> 
> 

## <a name="build-and-test-every-commit"></a>Tworzenie i testowanie każdym zatwierdzeniem
Pliki szablonów ProdAndStage.json i Dev.json już Określ parametry kontroli źródła, która domyślnie konfiguruje ciągłego publikowania aplikacji sieci web. W związku z tym każdym zatwierdzeniem do gałęzi GitHub wyzwala automatycznego wdrażania na platformie Azure z tym gałęzi. Zobaczmy, jak ustawienia działa teraz.

1. Upewnij się, że jesteś w gałęzi deweloperów lokalnego repozytorium. Aby to zrobić, uruchom następujące polecenie w powłoce Git:
   
        git checkout Dev
2. Zmiany warstwy interfejsu użytkownika aplikacji, zmieniając kod, aby użyć [Bootstrap](http://getbootstrap.com/components/) listy. Otwórz  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml i udostępnić wyróżnione następujące zmiany:
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > Jeśli nie można odczytać poprzednich obrazu: 
    > 
    > * W wierszu 18 Zmień `check-list` do `list-group`.
    > * W wierszu 19 Zmień `class="check-list-item"` do `class="list-group-item"`.
    > 
    > 
3. Zapisz zmiany. Ponownie w powłoce Git, uruchom następujące polecenia:
   
        cd <repository_root>
        git add .
        git commit -m "changed to bootstrap style"
        git push origin Dev
   
   Te polecenia git są podobne do "Sprawdzanie w kodzie" w inny system kontroli źródła, takich jak TFS. Po uruchomieniu `git push`, nowe zatwierdzenia wyzwala wypychania automatyczne kodu na platformie Azure, która spowoduje odbudowanie aplikacji w celu odzwierciedlenia zmian w środowisku testowym.
4. Aby sprawdzić wystąpił wypychania ten kod do środowiska standardowego, przejdź do strony aplikacji sieci web w środowisku deweloperów i przyjrzyj się **wdrożenia** części. Można wyświetlić Twojej najnowsze wiadomości zatwierdzania.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. Z tego miejsca, kliknij przycisk **Przeglądaj** aby zobaczyć nowe zmiany w działającej aplikacji na platformie Azure.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   Jest drobne zmiany do aplikacji. Jednak wiele razy nowych zmian do aplikacji sieci web złożonych ma niezamierzone i niepożądane skutki uboczne. Możliwość łatwego testowania każdym zatwierdzeniem w kompilacjach na żywo umożliwia catch te problemy, zanim klienci widoczne.

Chwili powinna być doświadczenia w realizacji który Deweloper na **NewUpdate** projektu, można utworzyć środowiska deweloperskiego dla siebie, a następnie kompilacji każdym zatwierdzeniem i testowania każdej kompilacji.

## <a name="merge-code-into-test-environment"></a>Scalanie kodu w środowisku testowym
Gdy wszystko jest gotowe wypchnąć kod deweloperów gałęzi do gałęzi NewUpdate, jest proces standardowe git:

1. Scal wszystkie nowe zatwierdzenia do NewUpdate w gałęzi deweloperów w witrynie GitHub, takich jak zatwierdzeń tworzone przez innych. Wszelkie nowe zatwierdzenia na GitHub wyzwalacze wypychania kodu i kompilacji w środowisku testowym. Można następnie upewnij się, że kod w gałęzi deweloperów wciąż działa z najnowszą bitami NewUpdate gałęzi.
2. Scal wszystkie nowe zatwierdzenia z gałęzi deweloperów w gałęzi NewUpdate w witrynie GitHub. Ta akcja wyzwala wypychania kodu i kompilacji w środowisku testowym. 

Pamiętaj, że ponieważ ciągłego wdrażania jest już skonfigurowane z tymi gałęziami git, nie trzeba podejmować żadnych działań, takich jak kompilacje z integracją. Należy po prostu wykonać rozwiązań formantu standardowego źródła przy użyciu usługi git i Azure wykonuje wszystkie procesy kompilacji.

Teraz załóżmy wypchnąć kod do **NewUpdate** gałęzi. W powłoce Git uruchom następujące polecenia:

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

Gotowe. 

Przejdź do strony aplikacji sieci web dla danego środowiska testowego zobaczyć Twoje nowe zatwierdzenia (scalone do gałęzi NewUpdate) teraz wypychana do środowiska testowego. Następnie kliknij przycisk **Przeglądaj** czy zmiana stylu jest teraz uruchomione na platformie Azure.

## <a name="deploy-update-to-production"></a>Wdrażanie aktualizacji do środowiska produkcyjnego
Wypychanie kodu do środowiska tymczasowych i produkcyjnych należy uznać nie różni się od co zostało już wykonane po naciśnięciu kodu do środowiska testowego. Jest naprawdę proste. 

W powłoce Git uruchom następujące polecenia:

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

Należy pamiętać, że zależne od środowiska przemieszczania i produkcji jest ustawiany w ProdandStage.json, zostanie przypisany nowy kod **przemieszczania** gniazdo i działa. Dlatego jeśli przejdziesz do adresu URL miejsca przemieszczania, zostanie wyświetlony nowy kod systemem. Aby to zrobić, uruchom następujące polecenie cmdlet w powłoce Git.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

I teraz, po zweryfikowaniu aktualizacji w miejsce przemieszczania jest jedynym elementem do wykonania można zamienić go w środowisku produkcyjnym. W powłoce Git uruchom następujące polecenia:

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

Gratulacje! Został pomyślnie opublikowany nowe aktualizacje do aplikacji sieci web w środowisku produkcyjnym. Co więcej jest który czy przez łatwe tworzenie środowisk tworzenia i testowania i tworzenia i testowania każdym zatwierdzeniem. Są to kluczowe bloków konstrukcyjnych dla rozwoju oprogramowania elastyczne.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>Usuń deweloperów i przetestować środowisk
Ponieważ celowo efekt środowiska do tworzenia i testowania być grup zasobów niezależne, to proste do ich usunięcia. Aby usunąć te tworzone w tym samouczku gałęzie GitHub i artefaktów Azure, uruchom następujące polecenia w powłoce Git:

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>Podsumowanie
Programowanie zwinne oprogramowania jest obowiązkowa dla wielu firm, które chcą wdrożyć usługę Azure jako ich platformę aplikacji. W tym samouczku ma przedstawiono sposób tworzenia i usunąć z łatwością, nawet w przypadku złożonych aplikacji dokładne replik w dół lub w jego pobliżu repliki środowiska produkcyjnego. Ma również przedstawiono sposób wykorzystać tę możliwość, można utworzyć procesu projektowanie, tworzenie i testowanie co jednego zatwierdzenia na platformie Azure. W tym samouczku wykazało miejmy nadzieję, jak najlepiej umożliwia usłudze Azure App Service i usługi Azure Resource Manager razem tworzenie rozwiązania DevOps przeznaczoną do metody agile. Następnie można tworzyć w tym scenariuszu, wykonując takie jak zaawansowane techniki DevOps [testowanie w produkcji](app-service-web-test-in-production-get-start.md). Dla typowego scenariusza testowanie w produkcji, zobacz [Flighting wdrożenia (testowania wersji beta) w usłudze Azure App Service](app-service-web-test-in-production-controlled-test-flight.md).

## <a name="more-resources"></a>Więcej zasobów
* [Wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md)
* [Elastyczne programowanie w praktyce: porady i wskazówki dotyczące cyklu zmodernizowanej programowanie](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [Strategie zaawansowanego wdrożenia dla aplikacji sieci Web platformy Azure przy użyciu szablonów usługi Resource Manager](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint — moduł sprawdzania poprawności JSON](http://jsonlint.com/)
* [ARMClient — Konfigurowanie publikowania GitHub do lokacji](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [Rozgałęzianie Git — podstawowe rozgałęzianie i scalanie](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Blog Dominik Ebbo](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Narzędzi wiersza polecenia platformy Azure i Platform](../cli-install-nodejs.md)
* [Tworzenie lub edytowanie użytkowników w usłudze Azure AD](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [Witryna typu Wiki Kudu projektu](https://github.com/projectkudu/kudu/wiki)

