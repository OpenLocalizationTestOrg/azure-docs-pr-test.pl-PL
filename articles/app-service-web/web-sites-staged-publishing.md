---
title: "aaaSet się przemieszczania środowiska dla aplikacji sieci web w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse przemieszczane publikowania dla aplikacji sieci web w usłudze Azure App Service."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>Konfigurowanie środowisk w usłudze Azure App Service przejściowych
<a name="Overview"></a>

Podczas wdrażania aplikację sieci web, aplikacji sieci web w systemie Linux, przenośne zaplecza i aplikacji interfejsu API za[usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714), można wdrożyć miejsce wdrożenia oddzielnych tooa zamiast miejsca produkcji domyślne hello podczas uruchamiania w hello **Standard**lub **Premium** tryb planu usługi aplikacji. Miejsca wdrożenia są faktycznie na żywo aplikacji za pomocą ich własnych nazwy hostów. Elementy zawartości i konfiguracji aplikacji może być zamieniona między dwóch miejsc wdrożenia, w tym hello miejsca produkcji. Wdrażanie przedział czasu wdrożenia tooa aplikacji ma hello następujące korzyści:

* Zmiany przemieszczania miejsce wdrożenia aplikacji może sprawdzać przed zamienienie go z miejscem produkcyjnym hello.
* Najpierw wdrażania miejsca tooa aplikacji i zamienienie go w środowisku produkcyjnym gwarantuje, że wszystkie wystąpienia miejsca hello są przygotowaniu miejsca przed wymieniane w środowisku produkcyjnym. Eliminuje to czas przestoju, podczas wdrażania aplikacji. przekierowywanie ruchu Hello jest łatwego i żadne żądania są usuwane w wyniku operacji wymiany. Ta całego przepływu pracy można zautomatyzować poprzez skonfigurowanie [automatycznej wymiany](#Auto-Swap) podczas weryfikacji przed wymiany nie jest wymagana.
* Po wymiany hello gniazda z wcześniej przygotowanych aplikacji ma hello poprzedniej aplikacji produkcyjnej. Jeśli zmiany hello miejscami do miejsca produkcji hello są niezgodne z oczekiwaniami, możesz wykonać powitalne sam zamiana natychmiast utworzyć kopię tooget "ostatniej znanej dobrej witryny".

Każdego trybu planu usługi aplikacji obsługuje różne liczby miejsc wdrożenia. obsługuje tryb aplikacji toofind hello liczbę miejsc, zobacz [App Service — ceny](https://azure.microsoft.com/pricing/details/app-service/).

* Gdy aplikacja ma wiele miejsc, nie można zmienić trybu hello.
* Skalowanie jest niedostępna dla gniazda nieprodukcyjnych.
* Zarządzanie połączonego zasobu nie jest obsługiwane dla gniazda nieprodukcyjnych. W hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) , można uniknąć ten potencjalny wpływ na gnieździe produkcyjnym przenosząc tymczasowo hello miejsca nieprodukcyjnych tooa różnych aplikacji planu tryb usługi. Uwaga gniazdo nieprodukcyjnych hello ponownie udostępnić hello tego samego trybu z miejscem produkcyjnym hello przed można zamienić miejsc hello dwa.

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>Dodaj miejsce wdrożenia
Aplikacja Hello musi być uruchomiona w hello **standardowe** lub **Premium** trybu w kolejności dla tooenable możesz wielu miejsc wdrożenia.

1. W hello [Azure Portal](https://portal.azure.com/), otwórz aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Wybierz hello **miejsc wdrożenia** opcji, a następnie kliknij przycisk **Dodaj miejsce**.
   
    ![Dodaj nowe miejsce wdrożenia][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > Jeśli aplikacja hello nie jest już hello **standardowe** lub **Premium** tryb, zostanie wyświetlony komunikat informujący o włączenie publikowania przemieszczanego tryby hello obsługiwane. W tym momencie masz hello opcja tooselect **uaktualnienia** i przejdź toohello **skali** kartę aplikacji przed kontynuowaniem.
   > 
   > 
3. W hello **dodać gniazdo** bloku, nadaj nazwę hello miejsca i wybierz czy tooclone konfiguracji aplikacji z innego istniejącego miejsca wdrożenia. Kliknij przycisk hello toocontinue znacznik wyboru.
   
    ![Źródło konfiguracji][ConfigurationSource1]
   
    Hello po raz pierwszy Dodaj miejsce, będziesz korzystać tylko z dwóch opcji: klonowania konfiguracji z gniazda domyślne hello w środowisku produkcyjnym lub w ogóle.
    Po utworzeniu miejsc kilka będą mogli tooclone konfiguracji z miejsca niż jeden hello w środowisku produkcyjnym:
   
    ![Konfiguracja źródła][MultipleConfigurationSources]
4. W bloku zasobów aplikacji, kliknij przycisk **miejsc wdrożenia**, kliknij przycisk tooopen miejsca wdrożenia bloku zasobów z miejsca, przy użyciu zestawu metryki i konfiguracji, tak jak każda inna aplikacja. Hello nazwa miejsca hello jest wyświetlany u góry hello tooremind bloku hello możesz przeglądanym hello miejsca wdrożenia.
   
    ![Tytuł miejsca wdrożenia][StagingTitle]
5. Kliknij adres URL aplikacji hello w bloku hello miejsca. Miejsce wdrożenia hello powiadomienie ma własną nazwę hosta i jest również aktywnej aplikacji. miejsce wdrożenia toohello dostępu publicznego toolimit, zobacz [aplikacji sieci Web usługi aplikacji — miejsc wdrożenia produkcyjnego toonon dostępu do sieci web bloku](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).

Brak zawartości po utworzeniu miejsca wdrożenia. Można wdrożyć toohello gniazda z gałęzi repozytorium różnych lub całkowicie innego repozytorium. Można również zmienić konfiguracji hello miejsca. Użyj hello publikowania profilu lub wdrożenia poświadczeń skojarzonych z hello miejsce wdrożenia aktualizacji zawartości.  Można na przykład [Opublikuj gnieździe toothis za pomocą narzędzia git](app-service-deploy-local-git.md).

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>Konfiguracja dla miejsc wdrożenia
Gdy Klonuj konfiguracji z innego miejsca wdrożenia, konfiguracja sklonowany hello jest można edytować. Ponadto niektóre elementy konfiguracji będzie śledzić hello zawartości między swap (nie gniazdo określonych), podczas gdy inne elementy konfiguracji, pozostanie na powitania sam gniazdo po swap (gniazdo określonych). Witaj następujące przedstawiono konfigurację hello ulegnie zmianie po zamienić miejsc.

**Ustawienia, które są zamienione**:

* Ustawienia ogólne — takie jak gniazda sieci Web 32/64-bitowych wersji framework
* Ustawienia aplikacji (może być skonfigurowany toostick tooa miejsca)
* Parametry połączenia (może być skonfigurowany toostick tooa miejsca)
* Mapowania programu obsługi
* Ustawienia monitorowania i diagnostyki
* Zawartość zadań Webjob

**Ustawienia, które nie są zamienione**:

* Publikowanie punktów końcowych
* Niestandardowa nazwa domeny
* Certyfikaty SSL i powiązań
* Ustawienia skali
* Planiści zadań Webjob

tooconfigure połączenie lub ustawienie ciągu toostick tooa miejsca aplikacji (nie miejscami), dostęp hello **ustawienia aplikacji** bloku do określonego miejsca, a następnie wybierz hello **ustawienie miejsca** pole hello elementy konfiguracji, które powinny trzymaj hello miejsca. Należy pamiętać, że oznaczenie element konfiguracji jako miejsca określonego ma wpływ hello ustanowienie tego elementu jako nie swappable wszystkich miejsc wdrożenia hello skojarzone z aplikacją hello.

![Ustawienia gniazda][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>Zamienić miejsc wdrażania 
Można zamienić miejsc wdrożenia w hello **omówienie** lub **miejsc wdrożenia** widok bloku zasobów aplikacji.

> [!IMPORTANT]
> Przed możesz zamienić aplikację z miejsce wdrożenia do środowiska produkcyjnego, upewnij się, że wszystkie z systemem innym niż miejsce określone ustawienia są skonfigurowane zgodnie z oczekiwaniami toohave go w celu wymiany hello.
> 
> 

1. tooswap miejsc wdrożenia, kliknij przycisk hello **wymiany** przycisk na pasku poleceń hello aplikacji hello lub na pasku poleceń hello miejsca wdrożenia.
   
    ![Przycisk wymiany][SwapButtonBar]

2. Upewnij się, że kierowanych źródła i wymiany wymiany hello są poprawnie ustawione. Zazwyczaj obiekt docelowy wymiany hello jest hello miejsca produkcji. Kliknij przycisk **OK** toocomplete hello operacji. Po zakończeniu działania hello zostały zamieniono hello miejsc wdrożenia.

    ![Ukończ zamianę](./media/web-sites-staged-publishing/SwapImmediately.png)

    Dla hello **zamiany z podglądem** wymiany typu, zobacz [zamiany z podglądem (faza wielu wymiany)](#Multi-Phase).  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>Zamiana z podglądem (faza wielu wymiany)

Zamiany z podglądem lub wielu faza wymiany uprościć weryfikacji konfiguracji specyficznych dla miejsca elementów, takich jak parametry połączenia.
W przypadku obciążeń krytycznym mają toovalidate, która aplikacja hello działa zgodnie z oczekiwaniami, po zastosowaniu konfiguracji gniazda produkcyjnego hello i należy wykonać takie weryfikacji *przed* aplikacji hello jest zamieniane w środowisku produkcyjnym. Zamiany z podglądem jest, co jest potrzebne.

> [!NOTE]
> Zamiany z podglądem jest nieobsługiwana w aplikacjach sieci web w systemie Linux.

Jeśli używasz hello **zamiana z podglądem** opcji (zobacz [zamienić miejsc wdrożenia](#Swap)), usługi aplikacji hello następujące:

- Nie ma wpływu na przechowuje hello docelowego miejsca niezmienione tak istniejących obciążenie gniazdo (np. produkcja).
- Dotyczy elementów konfiguracji hello hello miejsca toohello źródła miejsca docelowego, w tym parametry połączenia specyficzne dla miejsca hello i ustawień aplikacji.
- Uruchamia ponownie hello procesów roboczych na powitania miejsca źródłowego przy użyciu tych elementów konfiguracji wyżej.
- Po zakończeniu wymiany hello: miejsca źródłowego wstępnie przygotowany warmed up hello przenosi do miejsca docelowego hello. miejsca docelowego Hello jest przenoszony do miejsca źródłowego hello jak ręczne wymiany.
- Jeśli anulujesz wymiany hello: ponowne zastosowanie hello elementy konfiguracji z miejsca źródłowego toohello hello źródła miejsca.

Można przejrzeć, dokładnie tak jak aplikacji hello będzie się odbywać z konfiguracją hello z miejsca docelowego. Po ukończeniu sprawdzania poprawności zakończeniu wymiany hello w osobnym kroku. Ten krok ma hello dodatkową zaletę hello jest już przygotowaniu miejsca źródłowego z odpowiednią konfiguracją hello, czy klienci nie będzie działać z żadnych przestojów.  

Przykłady dotyczące hello poleceń cmdlet programu Azure PowerShell dostępne dla wielu faza wymiany znajdują się w hello poleceń cmdlet programu PowerShell systemu Azure dla sekcji miejsc wdrożenia.

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>Konfigurowanie automatycznej wymiany (MB)
Automatycznej wymiany usprawnia DevOps scenariuszy, w którym ma toocontinuously wdrażania aplikacji za pomocą zero zimny start i przestojów dla klientów końcowych aplikacji hello. Jeśli miejsce wdrożenia jest skonfigurowany do automatycznej wymiany do produkcji, zawsze push Twoje miejsce toothat aktualizacji kodu, usługi aplikacji — automatycznie wymiany aplikacji hello w środowisku produkcyjnym po już ma przygotowaniu miejsca w gnieździe hello.

> [!IMPORTANT]
> Po włączeniu automatycznej wymiany dla miejsca, upewnij się, że konfiguracja miejsca hello jest dokładnie hello konfiguracji przeznaczonych dla miejsca docelowego hello (zazwyczaj hello gniazda produkcyjnego).
> 
> 

> [!NOTE]
> Automatycznej wymiany nie jest obsługiwana w aplikacjach sieci web w systemie Linux.

Konfigurowanie automatycznej wymiany gnieździe jest bardzo proste. Wykonaj poniższe kroki hello:

1. W **miejsc wdrożenia**, a następnie wybierz gniazdo nieprodukcyjnych i wybierz **ustawienia aplikacji** w bloku zasobów z tego miejsca.  
   
    ![][Autoswap1]
2. Wybierz **na** dla **automatycznej wymiany**, wybierz pozycję gniazda docelowy hello **automatycznej wymiany miejsca**i kliknij przycisk **zapisać** na pasku poleceń hello. Upewnij się, że konfiguracja miejsca hello jest dokładnie hello konfiguracji przeznaczonych dla miejsca docelowego hello.
   
    Witaj **powiadomienia** kartę będzie flash zielona **Powodzenie** po zakończeniu operacji hello.
   
    ![][Autoswap2]
   
   > [!NOTE]
   > tootest automatycznej wymiany dla aplikacji, należy najpierw zaznaczyć gnieździe docelowym nieprodukcyjnych **automatycznej wymiany miejsca** toobecome zapoznać się z funkcją hello.  
   > 
   > 
3. Wykonanie miejsca wdrożenia toothat wypychania kodu. Automatycznej wymiany nastąpi po pewnym czasie, a aktualizacja hello zostaną odzwierciedlone pod adresem URL z miejsca docelowego.

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a>toorollback aplikacji produkcyjnej po wymiany
Jeśli błędy są identyfikowane w środowisku produkcyjnym po zakończeniu wymiany gniazd, wdrażanie miejsc hello stanów wstępne wymiany tootheir wstecz przez zamianę natychmiast hello tego samego dwóch miejsc.

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>Niestandardowe rozgrzewania przed wymiany
Niektóre aplikacje mogą wymagać akcje niestandardowe rozgrzewania. Witaj `applicationInitialization` umożliwia element konfiguracji w pliku web.config można toospecify niestandardową inicjalizację akcje toobe wykonać zanim żądanie zostanie odebrane. Operacja zamiany Hello będzie oczekiwał na ten toocomplete rozgrzewania niestandardowych. Oto przykładowe fragment pliku web.config.

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a>toodelete miejsce wdrożenia
W bloku hello miejsce wdrożenia, miejsce wdrożenia Otwórz hello bloku, kliknij przycisk **omówienie** (hello domyślnej strony) i kliknij przycisk **usunąć** na pasku poleceń hello.  

![Usuń miejsce wdrożenia][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>Polecenia cmdlet programu PowerShell systemu Azure dla miejsc wdrożenia
Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet toomanage Azure za pomocą środowiska Windows PowerShell, włącznie z obsługą zarządzania miejsc wdrożenia w usłudze Azure App Service.

* Aby uzyskać informacje na temat instalowania i konfigurowania programu Azure PowerShell, a na uwierzytelniania programu Azure PowerShell z subskrypcją platformy Azure, zobacz [jak tooinstall i konfigurowanie programu Microsoft Azure PowerShell](/powershell/azure/overview).  

- - -
### <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a>Tworzenie miejsca wdrożenia
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a>Zainicjuj wymiany z przeglądem (faza wielu wymiany) i zastosować gniazda toosource konfiguracji miejsca docelowego
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a>Anuluj oczekująca zamiana (obszar wymiany z przeglądem) i przywracanie konfiguracji miejsca źródłowego
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a>Zamienić miejsc wdrażania
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a>Usuń miejsce wdrożenia
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a>Azure polecenia interfejsu wiersza polecenia (Azure CLI) dla miejsc wdrożenia
Hello interfejsu wiersza polecenia Azure udostępnia polecenia i platform do pracy z platformą Azure, w tym obsługę zarządzania miejsc wdrożenia usługi aplikacji.

* Aby uzyskać instrukcje dotyczące instalowania i konfigurowania hello Azure CLI, wraz z informacjami na temat tooconnect interfejsu wiersza polecenia Azure tooyour subskrypcji platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md).
* Wywołanie polecenia hello toolist dostępne dla usługi Azure App Service w hello Azure CLI `azure site -h`.

> [!NOTE] 
> Dla [Azure CLI 2.0](https://github.com/Azure/azure-cli) poleceń dla miejsc wdrożenia, zobacz [miejsce wdrożenia sieci web appservice az](/cli/azure/appservice/web/deployment/slot).

- - -
### <a name="azure-site-list"></a>Lista witryn platformy Azure
Informacje o aplikacji hello w bieżącej subskrypcji hello, można wywołać **listy witryn azure**w hello poniższy przykład.

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>Tworzenie usługi Azure site
Wywołanie toocreate miejsce wdrożenia, **Tworzenie usługi azure site** i określ nazwę istniejącej aplikacji hello oraz nazwę hello hello toocreate miejsca, tak jak hello poniższy przykład.

`azure site create webappslotstest --slot staging`

tooenable kontroli źródła dla hello nowe miejsce, użyj hello **— git** opcja tak jak hello poniższy przykład.

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>usługi Azure site wymiany (MB)
toomake hello aplikacji produkcyjnej hello miejsca wdrażania aktualizacji, użyj hello **wymiany usługi azure site** tooperform polecenia operację zamiany, tak jak hello poniższy przykład. aplikacji produkcyjnej Hello nie będą występować dowolne czas przestoju, nie zostaną poddane zimny start.

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>Usuwanie witryny platformy Azure
toodelete miejsce wdrożenia, która nie jest już konieczne Użyj hello **usuwanie witryny azure** poleceń, tak jak hello poniższy przykład.

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> Zobacz działającą aplikację sieci Web. [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/) natychmiast i tej utworzyć początkową aplikację — bez karty kredytowej i bez zobowiązań.
> 
> 

## <a name="next-steps"></a>Następne kroki
[Usługa Azure App Service aplikacji sieci Web — Blokuj miejsc wdrożenia produkcyjnego toonon dostępu do sieci web](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[tooApp wprowadzenie usługi w systemie Linux](./app-service-linux-intro.md)
[bezpłatna wersja próbna programu Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

