---
title: "aaaProvision i wdrażanie mikrousług przewidywalnego na platformie Azure"
description: "Dowiedz się, jak toodeploy aplikacja składa się z mikrousług w usłudze Azure App Service jako pojedyncza jednostka i w sposób przewidywalny przy użyciu szablonów grupy zasobów JSON i skrypty programu PowerShell."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: bb51e565-e462-4c60-929a-2ff90121f41d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2016
ms.author: cephalin
ms.openlocfilehash: d32c2fc82a8b09e89224ec437e5819b65b2e9e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-and-deploy-microservices-predictably-in-azure"></a>Aprowizacji i wdrażania mikrousług przewidywalnego na platformie Azure
Ten samouczek pokazuje, jak tooprovision i wdrażanie aplikacji składający się z [mikrousług](https://en.wikipedia.org/wiki/Microservices) w [usłudze Azure App Service](/services/app-service/) jako pojedyncza jednostka i w sposób przewidywalny za pomocą szablonów grupy zasobów JSON i Skrypty programu PowerShell. 

Podczas inicjowania obsługi i wdrożenie wysokiej skali aplikacji, które składają się z bardzo rozdzielonymi mikrousług, powtarzalność i przewidywalności są niezwykle istotne toosuccess. [Usługa aplikacji Azure](/services/app-service/) pozwala mikrousług toocreate, który zawiera aplikacje sieci web, aplikacje mobilne, aplikacje interfejsu API i aplikacje logiki. [Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) umożliwia możesz toomanage wszystkie mikrousług hello jako jednostki, wraz z zależności zasobów, takich jak ustawienia kontroli bazy danych i źródła. Teraz można także wdrożyć takiej aplikacji przy użyciu szablony JSON i proste skrypty środowiska PowerShell. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Będzie wykonywać
W samouczku hello zostanie wdrożona aplikacja, która obejmuje:

* Dwie sieci web aplikacji (tj. dwa mikrousług)
* Wewnętrznej bazy danych SQL Database
* Ustawienia aplikacji, parametry połączenia i kontroli źródła
* Usługa Application insights, alerty, ustawienia skalowania automatycznego

## <a name="tools-you-will-use"></a>Narzędzia, które będą używane
W tym samouczku użyjesz hello następujących narzędzi. Ponieważ nie jest kompleksowe omówienie narzędzia, I używam przechodzi toostick toohello end-to-end scenariusza i po prostu zapewniają tooeach krótkie wprowadzenie, i gdzie można znaleźć więcej informacji na nim. 

### <a name="azure-resource-manager-templates-json"></a>Szablony usługi Azure Resource Manager (JSON)
Za każdym razem, gdy utworzysz aplikację sieci web w usłudze Azure App Service, na przykład usługi Azure Resource Manager używa grupy zasobów całej hello toocreate szablonu JSON z zasobami składnika hello. Złożone szablonu z hello [portalu Azure Marketplace](/marketplace) jak hello [Scalable WordPress](/marketplace/partners/wordpress/scalablewordpress/) aplikacji mogą być hello baza danych MySQL, konta magazynu, hello planu usługi aplikacji, samej aplikacji sieci web hello, reguły alertów, aplikacji ustawienia, ustawienia skalowania automatycznego i więcej i wszystkie te szablony są dostępne tooyou za pomocą programu PowerShell. Aby uzyskać informacje dotyczące toodownload i używania tych szablonów, zobacz temat [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).

Aby uzyskać więcej informacji na powitania szablonów usługi Azure Resource Manager, zobacz [Authoring Azure Resource Manager szablonów](../azure-resource-manager/resource-group-authoring-templates.md)

### <a name="azure-sdk-26-for-visual-studio"></a>Zestaw Azure SDK 2.6 dla programu Visual Studio
Witaj najnowsze zestaw SDK zawiera ulepszenia toohello Obsługa szablonów usługi Resource Manager w edytorze JSON hello. Można użyć tego tooquickly tworzenia szablonu grupy zasobów od początku lub Otwórz istniejący szablon JSON (na przykład szablon pobrany galerii) do modyfikacji, wypełnij hello pliku parametrów i nawet wdrażania hello grupę zasobów bezpośrednio z platformy Azure Rozwiązanie grupy zasobów.

Aby uzyskać więcej informacji, zobacz [2.6 zestawu SDK platformy Azure dla programu Visual Studio](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/).

### <a name="azure-powershell-080-or-later"></a>Program Azure PowerShell 0.8.0 lub nowszy
Począwszy od wersji 0.8.0, hello instalacji programu Azure PowerShell zawiera moduł usługi Azure Resource Manager hello w toohello dodanie modułu platformy Azure. Ten nowy moduł umożliwia wdrożenie hello tooscript grup zasobów.

Aby uzyskać więcej informacji, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md)

### <a name="azure-resource-explorer"></a>Eksplorator zasobów Azure
To [narzędzia Podgląd](https://resources.azure.com) pozwala tooexplore hello JSON definicje wszystkich grup zasobów hello w Twojej subskrypcji i hello pojedynczych zasobów. W narzędziu hello można edytować hello JSON definicji zasobu, Usuń całej hierarchii zasobów i tworzenia nowych zasobów.  informacje Hello łatwo dostępne w tym narzędziu są bardzo przydatne do tworzenia szablonu, ponieważ przedstawiono co właściwości należy tooset dla określonego typu zasobu, hello Popraw wartości itd. Możesz nawet utworzyć grupy zasobów w hello [Azure Portal](https://portal.azure.com/), następnie sprawdź ich definicje JSON w toohelp narzędzia Eksplorator hello templatize hello grupy zasobów.

### <a name="deploy-tooazure-button"></a>TooAzure przycisk Wdrażaj
Jeśli używasz GitHub dla kontroli źródła, możesz umieścić [przycisk tooAzure Wdróż](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/) do Twojej Plik README. MD, dzięki czemu tooAzure interfejsu użytkownika wdrożenia gotowe. Czynności można wykonać dla dowolnej aplikacji sieci web proste, można rozszerzyć tego tooenable wdrażanie umieszczenie plik azuredeploy.json w katalogu głównym repozytorium hello całej grupy zasobów. Ten plik JSON, który zawiera szablon grupy zasobów hello, będzie używany przez grupę zasobów hello toocreate przycisk hello Wdróż tooAzure. Na przykład zobacz hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) próbki, który będzie używany w tym samouczku.

## <a name="get-hello-sample-resource-group-template"></a>Pobierz szablon grupy zasobów przykładowej hello
Tak teraz, zaloguj się tooit prawo.

1. Przejdź toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) przykładowej aplikacji usługi.
2. W readme.md, kliknij przycisk **wdrażanie tooAzure**.
3. Są podejmowane toohello [wdrożyć do azure](https://deploy.azure.com) lokacji i zadawane tooinput parametrów wdrożenia. Zwróć uwagę, że większość pól hello są wypełniane przy użyciu nazwy repozytorium hello i niektórych losowe ciągów dla Ciebie. Wszystkie pola hello można zmienić, ale hello rzeczy tylko masz tooenter administracyjne logowania programu SQL Server hello i hello hasła, a następnie kliknij **dalej**.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-1-deploybuttonui.png)
4. Następnie kliknij przycisk **Wdróż** procesu wdrażania hello toostart. Po hello proces działa toocompletion, kliknij przycisk hello http://todoapp*XXXX*. azurewebsites.net łącze toobrowse hello wdrożonych aplikacji. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-2-deployprogress.png)
   
   Hello interfejsu użytkownika będzie nieco powolne podczas najpierw przeglądania tooit ponieważ aplikacji hello są po prostu uruchamiania, ale przekonać się, jest pełnej funkcjonalności aplikacji.
5. Ponownie hello Wdróż na stronie kliknij hello **Zarządzaj** łącze nowej aplikacji hello toosee w hello portalu Azure.
6. W hello **Essentials** listy rozwijanej, kliknij łącze grupę zasobów hello. Pamiętaj również danej aplikacji sieci web hello jest już połączony repozytorium GitHub toohello w obszarze **projektu zewnętrznego**. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-3-portalresourcegroup.png)
7. W bloku grupy zasobów hello należy pamiętać, że już dwie aplikacje sieci web i jednej bazy danych SQL w grupie zasobów hello.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-4-portalresourcegroupclicked.png)

Wszystko, który został wyświetlony w ciągu kilku minut krótkich aplikacją pełni wdrożone mikrousługi dwa wszystkie składniki hello, zależności, ustawienia, bazy danych i ciągłe publikowanie skonfigurowany przez automatyczne aranżacji w usłudze Azure Resource Manager. Wszystko to zostało to zrobione przez dwie czynności:

* przycisk tooAzure Wdróż Hello
* azuredeploy.JSON w katalogu głównym repozytorium hello

Można wdrożyć tej samej aplikacji dziesiątki, setek lub tysięcy razy i mieć hello dokładnie tej samej konfiguracji zawsze. przewidywalność powtarzalność i hello Hello takie podejście umożliwia toodeploy wysokiej skali aplikacji mogliby łatwo i zaufania.

## <a name="examine-or-edit-azuredeployjson"></a>Sprawdź (lub edytować) AZUREDEPLOY. JSON
Teraz Przyjrzyjmy się konfiguracji hello repozytorium GitHub. Będziesz używać edytora JSON hello w hello Azure .NET SDK, tak więc jeśli nie została jeszcze zainstalowana [Azure .NET SDK w wersji 2.6](/downloads/), zrób to teraz.

1. Witaj w klonowania [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repozytorium narzędzie git ulubionych. W poniższym zrzucie ekranu hello robimy to w hello Team Explorer programu Visual Studio 2013.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-1-vsclone.png)
2. W katalogu głównym repozytorium hello Otwórz azuredeploy.json w programie Visual Studio. Jeśli nie widzisz hello okienku Konspekt pliku JSON, należy tooinstall zestawu Azure .NET SDK.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-2-vsjsoneditor.png)

Jestem nie będzie toodescribe co szczegółów hello formatu JSON, ale hello [więcej zasobów](#resources) sekcja zawiera łącza do uczenia język szablonu grupy zasobów hello. W tym miejscu wystarczy użyjemy rozpocząć tooshow Witaj, interesujące funkcje, które mogą pomóc Ci w podejmowaniu szablonu niestandardowego dla wdrożenia aplikacji.

### <a name="parameters"></a>Parametry
Spójrz na powitania parametry sekcji toosee że większość te parametry są jakie hello **wdrażanie tooAzure** przycisk monit tooinput. Witryna Hello za hello **wdrażanie tooAzure** przycisk wypełnia hello danych wejściowych interfejsu użytkownika przy użyciu hello parametrów zdefiniowanych w azuredeploy.json. Te parametry są używane w całej hello definicjach zasobów, takich jak nazwy zasobów, wartości właściwości, itd.

### <a name="resources"></a>Zasoby
W węźle zasobów hello widać, że są zdefiniowane 4 zasobów najwyższego poziomu, w tym wystąpienia programu SQL Server, plan usługi aplikacji i dwie aplikacje sieci web. 

#### <a name="app-service-plan"></a>Plan usługi App Service
Zacznijmy od prostego zasobu poziomu głównego w hello JSON. W hello konspekt pliku JSON, kliknij nazwę planu usługi aplikacji hello **[hostingPlanName]** toohighlight hello odpowiedniego kodu JSON. 

![](./media/app-service-deploy-complex-application-predictably/examinejson-3-appserviceplan.png)

Należy pamiętać, że hello `type` element określa ciąg hello planu usługi aplikacji (została wywołana farmy serwerów długie, długi czas temu) i inne elementy i właściwości są wypełniane przy użyciu hello parametrów zdefiniowanych w pliku JSON hello, a nie ma tego zasobu wszystkie zasoby zagnieżdżonych.

> [!NOTE]
> Należy też zauważyć tej wartości hello `apiVersion` informuje Azure, która wersja hello interfejsu API REST toouse hello JSON definicji zasobu z, a może mieć wpływ na sposób hello zasób powinien być sformatowany wewnątrz hello `{}`. 
> 
> 

#### <a name="sql-server"></a>Oprogramowanie SQL Server
Następnie kliknij przycisk na powitania zasobów programu SQL Server o nazwie **SQLServer** w hello konspekt pliku JSON.

![](./media/app-service-deploy-complex-application-predictably/examinejson-4-sqlserver.png)

Uwaga powitania po o hello wyróżniony kod JSON:

* Użycie parametrów Hello temu hello utworzone zasoby są o nazwie i skonfigurowane w sposób umożliwiający ich zgodne ze sobą.
* Witaj SQLServer zasobów ma dwa zagnieżdżonych zasobów, każdy ma inną wartość dla `type`.
* Hello zagnieżdżone zasoby wewnątrz `“resources”: […]`, gdzie są zdefiniowane hello bazy danych i jego reguły zapory hello, mieć `dependsOn` element, który określa identyfikator zasobu hello hello poziomu głównego SQLServer zasobu. Ta wartość informuje usługi Azure Resource Manager "przed utworzeniem tego zasobu, który innego zasobu musi już istnieć; i innych zasobu jest zdefiniowany w szablonie hello, następnie co najpierw utworzyć".
  
  > [!NOTE]
  > Aby uzyskać szczegółowe informacje na temat toouse hello `resourceId()` funkcji, zobacz [funkcje szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid).
  > 
  > 
* Witaj efekt hello `dependsOn` element jest, że usługi Azure Resource Manager może znać zasobów, do których można tworzyć równolegle i które zasoby muszą być tworzone po kolei. 

#### <a name="web-app"></a>Aplikacja internetowa
Teraz przejdziemy toohello rzeczywistej aplikacji sieci web, które są bardziej skomplikowane. Kliknij aplikację sieci web hello [variables('apiSiteName')] toohighlight konspekt pliku JSON hello jego kod JSON. Można zauważyć, że elementy stają się coraz bardziej interesujące. W tym celu I będzie komunikował funkcje hello jeden po drugim:

##### <a name="root-resource"></a>Zasób katalogu głównego
Aplikacja sieci web Hello zależy od dwóch różnych zasobów. Oznacza to, czy usługi Azure Resource Manager utworzy hello aplikacji sieci web dopiero po obu powitalne planu usługi aplikacji i hello wystąpienia programu SQL Server są tworzone.

![](./media/app-service-deploy-complex-application-predictably/examinejson-5-webapproot.png)

##### <a name="app-settings"></a>Ustawienia aplikacji
Ustawienia aplikacji Hello również są definiowane jako zagnieżdżonych zasobów.

![](./media/app-service-deploy-complex-application-predictably/examinejson-6-webappsettings.png)

W hello `properties` elementu `config/appsettings`, mają dwa ustawienia aplikacji w formacie hello `“<name>” : “<value>”`.

* `PROJECT`jest [ustawienie KUDU](https://github.com/projectkudu/kudu/wiki/Customizing-deployments) , który zawiadamia wdrożenia usługi Azure które toouse projektu w rozwiązaniu Visual Studio wielu projektów. I wyświetli później, jak jest skonfigurowany do kontroli źródła, ale ponieważ jest hello ToDoApp kodu w rozwiązaniu Visual Studio wielu projektów, potrzebujemy to ustawienie.
* `clientUrl`jest po prostu ustawienie kodu aplikacji hello aplikacja używa.

##### <a name="connection-strings"></a>Parametry połączeń
Parametry połączenia Hello również są zdefiniowane jako zasób zagnieżdżonych.

![](./media/app-service-deploy-complex-application-predictably/examinejson-7-webappconnstr.png)

W hello `properties` elementu `config/connectionstrings`, każdy ciąg połączenia jest również zdefiniowany jako pary nazwa: wartość w formacie określonym hello `“<name>” : {“value”: “…”, “type”: “…”}`. Dla hello `type` elementu, możliwe wartości to `MySql`, `SQLServer`, `SQLAzure`, i `Custom`.

> [!TIP]
> Ostateczne listę typów ciąg połączenia hello, uruchom następujące polecenie w programie Azure PowerShell hello: \[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")
> 
> 

##### <a name="source-control"></a>Kontrola źródła
Ustawienia kontroli źródła Hello również są definiowane jako zagnieżdżonych zasobów. Publikowanie ciągłego tooconfigure zasobów używa usługi Azure Resource Manager (zobacz zastrzeżenie: na `IsManualIntegration` później), a także tookick poza hello wdrażania kodu aplikacji automatycznie podczas przetwarzania hello hello pliku JSON.

![](./media/app-service-deploy-complex-application-predictably/examinejson-8-webappsourcecontrol.png)

`RepoUrl`i `branch` powinny być bardzo intuicyjne i powinny wskazywać toohello Git repozytorium i hello nazwy toopublish gałęzi hello z. Ponownie są one zdefiniowane przez parametry wejściowe. 

Zanotuj w hello `dependsOn` element, który w toohello dodanie zasobu aplikacji, sieci web `sourcecontrols/web` zależy również od `config/appsettings` i `config/connectionstrings`. Jest to spowodowane po `sourcecontrols/web` jest skonfigurowany, hello proces wdrożenia usługi Azure automatycznie podejmie próbę toodeploy, skompilować i uruchomić kod aplikacji hello. W związku z tym Wstawianie ta pomaga zależności należy upewnić się, tej aplikacji hello zawiera ustawienia aplikacji toohello wymagane dostępu i parametry połączenia przed uruchomieniem kodu aplikacji hello. 

> [!NOTE]
> Należy zauważyć, że `IsManualIntegration` ustawiono zbyt`true`. Ta właściwość jest niezbędne w tym samouczku, ponieważ nie ma faktycznego hello repozytorium GitHub i w związku z tym faktycznie nie można udzielić uprawnienia tooAzure tooconfigure ciągłego publikowania z [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) (tj. push automatyczne repozytorium tooAzure aktualizacji). Możesz użyć wartości domyślnej hello `false` hello repozytorium określony tylko wtedy, gdy skonfigurowano poświadczenia GitHub właściciela hello hello [portalu Azure](https://portal.azure.com/) przed. Innymi słowy Jeśli zdefiniowano tooGitHub kontroli źródła lub BitBucket dla wszystkich aplikacji w hello [Azure Portal](https://portal.azure.com/) wcześniej przy użyciu użytkownika poświadczeń, Azure będą Pamiętaj poświadczenia hello i ich używać wdrożenia dowolnej aplikacji Usługi GitHub lub BitBucket w przyszłości hello. Jednak jeśli użytkownik nie zostało to jeszcze zrobione, wdrożenia szablonu JSON hello zakończy się niepowodzeniem usługi Azure Resource Manager próbuje ustawień kontroli źródła dla aplikacji tooconfigure hello sieci web, ponieważ nie można zalogować do usługi GitHub lub BitBucket, z poświadczeniami właściciela repozytorium hello.
> 
> 

## <a name="compare-hello-json-template-with-deployed-resource-group"></a>Porównanie hello JSON szablonu z grupą wdrożonych zasobów
W tym miejscu, można przejść przez bloki wszystkich hello aplikacji sieci web w hello [Azure Portal](https://portal.azure.com/), ale innego narzędzia, która po prostu jako przydatne, jeśli nie jest więcej. Przejdź toohello [Eksploratora zasobów Azure](https://resources.azure.com) Podgląd narzędzia, które zapewnia JSON reprezentację wszystkich grup zasobów hello w subskrypcji, ponieważ faktycznie istnieją one hello wewnętrznej bazy danych Azure. Można również sprawdzić, jak grupy zasobów hello hierarchii JSON na platformie Azure odpowiada hierarchii hello w pliku szablonu hello, który został użyty toocreate go.

Na przykład po przejściu toohello [Eksploratora zasobów Azure](https://resources.azure.com) narzędzia i rozwiń węzły hello w Eksploratorze hello, widać hello grupy zasobów i hello poziomu głównego zasoby, które są zbierane w ich typów odpowiednich zasobów.

![](./media/app-service-deploy-complex-application-predictably/ARM-1-treeview.png)

Jeśli przechodzenie tooa aplikacji sieci web, powinny być możliwe toosee sieci web aplikacji konfiguracji szczegóły podobne toohello poniżej zrzut ekranu:

![](./media/app-service-deploy-complex-application-predictably/ARM-2-jsonview.png)

Ponownie, hello zagnieżdżonych zasobów powinien mieć toothose bardzo podobne hierarchii w pliku szablonu JSON i ustawień aplikacji hello, parametry połączenia, itp., prawidłowo odzwierciedlane w okienku JSON hello powinna zostać wyświetlona. Brak Hello tutaj ustawień może oznaczać problem z plikiem JSON i ułatwiają rozwiązywanie problemów z pliku szablonu JSON.

## <a name="deploy-hello-resource-group-template-yourself"></a>Wdrażanie szablonu grupy zasobów hello samodzielnie
Witaj **wdrażanie tooAzure** przycisk stanowi doskonałe rozwiązanie, ale pozwala szablon grupy zasobów hello toodeploy w azuredeploy.json tylko wtedy, gdy ma już przypisany azuredeploy.json tooGitHub. Hello Azure .NET SDK udostępnia także hello narzędzia można toodeploy dowolnego pliku szablonu JSON bezpośrednio z komputera lokalnego. toodo, wykonaj hello czynności:

1. W programie Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu**.
2. Kliknij przycisk **Visual C#** > **chmury** > **grupy zasobów platformy Azure**, następnie kliknij przycisk **OK**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-1-vsproject.png)
3. W **wybierz szablon Azure**, wybierz pozycję **pusty szablon** i kliknij przycisk **OK**.
4. Przeciągnij azuredeploy.json hello **szablonu** folderu nowego projektu.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-2-copyjson.png)
5. W Eksploratorze rozwiązań Otwórz azuredeploy.json hello skopiowane.
6. Tylko dla zapewnienia hello pokaz hello, możemy dodać niektóre standardowe szczegółowe informacje o aplikacji zasobów tooour pliku JSON, klikając **dodawania zasobów**. Jeśli interesuje Cię tylko wdrażania hello pliku JSON, pomiń kroki wdrażania toohello.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-3-newresource.png)
7. Wybierz **usługi Application Insights dla aplikacji sieci Web**, następnie upewnij się, istniejącą aplikację sieci web i plan usługi aplikacji jest zaznaczone, a następnie kliknij przycisk **Dodaj**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-4-newappinsight.png)
   
   Teraz możesz być stanie toosee kilka nowych zasobów, w zależności od zasobów hello i jakie operacje, mają zależności albo hello aplikacji sieci web planu lub hello usługi aplikacji. Te zasoby nie są włączone przez ich istniejącą definicję i zacząć toochange który.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-5-appinsightresources.png)
8. W hello konspekt pliku JSON, kliknij przycisk **appInsights skalowania automatycznego** toohighlight jego kod JSON. Jest to hello skalowanie ustawienia planu usługi aplikacji.
9. W hello wyróżniony kod JSON, Znajdź hello `location` i `enabled` właściwości i ustaw je, jak pokazano poniżej.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-6-autoscalesettings.png)
10. W hello konspekt pliku JSON, kliknij przycisk **CPUHigh appInsights** toohighlight jego kod JSON. To jest alert.
11. Zlokalizuj hello `location` i `isEnabled` właściwości i ustaw je, jak pokazano poniżej. Hello takie same dla hello pozostałe trzy alerty (purpurowy bulw).
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-7-alerts.png)
12. Możesz teraz gotowy toodeploy. Kliknij prawym przyciskiem myszy projekt hello i wybierz **Wdróż** > **nowe wdrożenie**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-8-newdeployment.png)
13. Zaloguj się do konta platformy Azure, jeśli jeszcze tego nie zrobiono.
14. Wybierz istniejącą grupę zasobów w ramach subskrypcji lub Utwórz nowe wybierz jedną, **azuredeploy.json**, a następnie kliknij przycisk **Edytuj parametry**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-9-deployconfig.png)
    
    Teraz będziesz w stanie tooedit wszystkie parametry hello zdefiniowane w pliku szablonu hello nieuprzywilejowany tabeli. Parametry, które definiują ustawienia domyślne mają już wartości domyślne, a parametry określające listę dozwolonych wartości będą wyświetlane jako listę rozwijaną.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-10-parametereditor.png)
15. Wypełnij wszystkie parametry pusty hello i użyj hello [adres repozytorium GitHub ToDoApp](https://github.com/azure-appservice-samples/ToDoApp.git) w **repoUrl**. Następnie kliknij przycisk **zapisać**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-11-parametereditorfilled.png)
    
    > [!NOTE]
    > Funkcję skalowania automatycznego jest funkcją oferowanych w **standardowe** warstwy lub nowszej i poziomu planu alerty są oferowane w funkcji **podstawowe** warstwę lub nowszego, będziesz potrzebować tooset hello **jednostki sku** Parametr zbyt**standardowe** lub **Premium** w celu toosee wszystkich nowych App Insights zasobów światła w górę.
    > 
    > 
16. Kliknij przycisk **wdrażanie**. W przypadku wybrania **zapisywanie haseł**, hello hasło zostanie zapisane w pliku parametrów hello **w postaci zwykłego tekstu**. W przeciwnym razie zostanie wyświetlony monit tooinput hello hasło podczas procesu wdrażania hello.

Gotowe. Teraz wystarczy toogo toohello [Azure Portal](https://portal.azure.com/) i hello [Eksploratora zasobów Azure](https://resources.azure.com) toosee narzędzie hello nowe alerty i ustawienia skalowania automatycznego dodane tooyour JSON wdrożonych aplikacji.

Wszystkie czynności w tej sekcji zrobić głównie hello następujące czynności:

1. Witaj przygotowanego pliku szablonu
2. Utworzony toogo pliku parametru za pomocą pliku szablonu hello
3. Plik szablonu hello wdrożone z pliku parametrów hello

ostatni krok Hello łatwo odbywa się przy użyciu polecenia cmdlet programu PowerShell. toosee co Visual Studio została ona wdrożona Twojej aplikacji, otwórz Scripts\Deploy-AzureResourceGroup.ps1. Wiele kodu istnieje, ale tylko użyjemy toohighlight cały kod stosowne hello należy plik szablonu hello toodeploy z pliku parametrów hello.

![](./media/app-service-deploy-complex-application-predictably/deploy-12-powershellsnippet.png)

Witaj ostatniego polecenia cmdlet, `New-AzureResourceGroup`, jest hello, który faktycznie wykonuje akcję hello. Wszystko to powinien pokazują, że hello z narzędzia pomocy, jest stosunkowo prosta toodeploy tooyou Twojego przewidywalnego aplikacji w chmurze. Zawsze należy uruchomić polecenie cmdlet hello na powitania tego samego szablonu z hello sam plik parametrów, który ma tooget hello takiego samego wyniku.

## <a name="summary"></a>Podsumowanie
W DevOps powtarzalność i przewidywalności są klucze tooany pomyślne wdrożenie aplikacji wysokiej skali składa się z mikrousług. W tym samouczku wdrożono tooAzure aplikacji mikrousługi dwa jako pojedyncza grupa zasobów przy użyciu szablonu usługi Azure Resource Manager hello. Mamy nadzieję, że jej przyznał Ci hello wiedzy w kolejności toostart konwertowania aplikacji na platformie Azure do szablonu i można udostępnić i przewidywalnego go wdrożyć. 

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak za[zastosowania metody agile i stale opublikować aplikację mikrousług z łatwością](app-service-agile-software-development.md) i zaawansowane techniki wdrażania, takie jak [flighting wdrożenia](app-service-web-test-in-production-controlled-test-flight.md) łatwe.

<a name="resources"></a>

## <a name="more-resources"></a>Więcej zasobów
* [Język szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [Azure Functions szablonu usługi Resource Manager](../azure-resource-manager/resource-group-template-functions.md)
* [Wdrażanie aplikacji przy użyciu szablonu Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md)
* [Używanie programu Azure PowerShell z usługą Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)
* [Rozwiązywanie problemów z wdrożeniami grup zasobów na platformie Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md)

