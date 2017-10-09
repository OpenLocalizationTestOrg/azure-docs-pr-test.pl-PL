---
title: "aaaDeploy i uaktualnić Azure mikrousług lokalnie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrożyć istniejących tooit aplikacji tooset instalacji klastra lokalnego sieci szkieletowej usług, a następnie Uaktualnianie tej aplikacji."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a>Pierwsze kroki wdrażania i aktualizowania aplikacji w klastrze lokalnym
Hello zestawu SDK usługi Azure Service Fabric zawiera pełne lokalne środowisko, którego można używać tooquickly wprowadzenie do wdrażania aplikacji i zarządzanie nimi w klastrze lokalnym. W tym artykule możesz utworzyć klaster lokalny, wdrożyć istniejącą tooit aplikacji, a następnie Uaktualnij aplikacji tooa nowej wersji, wszystkie ze środowiska Windows PowerShell.

> [!NOTE]
> W tym artykule przyjęto, że czynności [konfigurowania środowiska deweloperskiego](service-fabric-get-started.md) zostały już ukończone.
> 
> 

## <a name="create-a-local-cluster"></a>Tworzenie klastra lokalnego
Klaster usługi Service Fabric stanowi zestaw zasobów sprzętowych, w którym można wdrażać aplikacje. Zazwyczaj klaster składa się z dowolnym z pięciu toomany tysięcy komputerów. Jednak hello zestawu SDK usług sieci szkieletowej obejmuje konfigurację klastra, który można uruchomić na jednym komputerze.

Jest ważne, czy toounderstand, który hello lokalnego klastra usługi sieć szkieletowa nie jest emulatorem ani symulatorem. Go uruchamia hello sam kod platformy, która znajduje się w klastrach obejmujących wiele maszyn. Witaj jedyna różnica polega na tym, że będzie ono przeprowadzane hello procesy platformowe, które standardowo są rozmieszczone na pięciu maszynach na jednej maszynie.

Hello SDK udostępnia dwa sposoby tooset instalacji klastra lokalnego: środowiska Windows PowerShell skrypt i hello Menedżera klastra lokalnego systemu na pasku aplikacji. W tym samouczku używamy skryptu programu PowerShell hello.

> [!NOTE]
> Jeśli utworzono już klaster lokalny poprzez wdrożenie aplikacji z programu Visual Studio, tę sekcję można pominąć.
> 
> 

1. Uruchom nowe okno programu PowerShell jako administrator.
2. Uruchom skrypt instalacji klastra hello z folderu zestawu SDK hello:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    Instalacja klastra trwa kilka chwil. Po zakończeniu instalacji powinny być widoczne dane wyjściowe podobne do poniższych:
   
    ![Dane wyjściowe instalacji klastra][cluster-setup-success]
   
    Wszystko jest teraz gotowy tootry wdrażanie klastra tooyour aplikacji.

## <a name="deploy-an-application"></a>Wdrażanie aplikacji
Hello zestaw SDK usługi Service Fabric zawiera bogaty zestaw struktur i narzędzi do tworzenia aplikacji programistycznych. Jeśli interesuje Cię w uczeniu toocreate aplikacji w programie Visual Studio, zobacz temat [tworzenie pierwszej aplikacji platformy Service Fabric w programie Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).

W tym samouczku, można użyć istniejącej aplikacji przykładowej (o nazwie WordCount), dzięki czemu można skupić się na aspektach zarządzania hello platformy hello: wdrażanie, monitorowanie i uaktualnianie.

1. Uruchom nowe okno programu PowerShell jako administrator.
2. Zaimportuj moduł programu PowerShell zestawu SDK sieci szkieletowej usług hello.
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. Tworzenie aplikacji hello toostore katalogu, który można pobrać i wdrożyć, na przykład C:\ServiceFabric.
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. [Pobierz aplikację WordCount hello](http://aka.ms/servicefabric-wordcountapp) toohello lokalizacji został utworzony.  Uwaga: hello przeglądarki Microsoft Edge zapisuje plik hello o *.zip* rozszerzenia.  Zmień rozszerzenie pliku hello zbyt*.sfpkg*.
5. Połącz klaster lokalny toohello:
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. Utwórz nową aplikację za pomocą polecenia wdrażania hello SDK z nazwą i pakiet aplikacji toohello ścieżki.
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    Jeśli wszystko przebiegnie poprawnie, powinny być widoczne następujące dane wyjściowe hello:
   
    ![Wdrożenie klastra lokalnego toohello aplikacji][deploy-app-to-local-cluster]
7. Aplikacja hello toosee akcji, uruchom hello przeglądarki i przejdź zbyt[http://localhost: 8081/WordCount/index.HTML](http://localhost:8081/wordcount/index.html). Powinien zostać wyświetlony następujący ekran:
   
    ![Interfejs użytkownika wdrożonej aplikacji][deployed-app-ui]
   
    Witaj aplikacja WordCount jest proste. Obejmuje on po stronie klienta JavaScript kodu toogenerate losowe pięć znaków "wyrazy", które są następnie przekazywane toohello aplikacji za pomocą interfejsu API sieci Web platformy ASP.NET. Usługa stanowa śledzi hello liczbę zliczonych słów. Są one dzielone oparte na powitania pierwszego znaku słowa hello. Kod źródłowy hello można znaleźć aplikacji WordCount hello w hello [klasycznego wprowadzenie przykłady](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).
   
    Aplikacja Hello, którą wdrożyliśmy, zawiera cztery partycje. Dlatego wyrazów rozpoczynających się od A do G są przechowywane w pierwszej partycji hello, wyrazów rozpoczynających się od H do N są przechowywane w hello drugiej partycji i tak dalej.

## <a name="view-application-details-and-status"></a>Wyświetlanie szczegółów i stanu aplikacji
Teraz, gdy wdrożyliśmy aplikacji hello, Przyjrzyjmy się niektóre szczegóły aplikacji hello w programie PowerShell.

1. Zapytanie wszystkich aplikacji wdrożonych w klastrze hello:
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    Przy założeniu, że została wdrożona tylko aplikacja WordCount hello, zobacz polecenie podobne do następującego:
   
    ![Zapytanie dotyczące wszystkich wdrożonych aplikacji w powłoce PowerShell][ps-getsfapp]
2. Przejdź toohello następny poziom, badając hello zestawu usług zawartych w aplikacji WordCount hello.
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Lista usług dla aplikacji hello w programie PowerShell][ps-getsfsvc]
   
    Aplikacja Hello składa się z dwóch usług, frontonu sieci web hello i hello usługi stanowej, która zarządza hello słów.
3. Na koniec przyjrzeć się hello listę partycji dla usługi WordCountService:
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Widok partycji usługi hello w programie PowerShell][ps-getsfpartitions]
   
    Witaj zestaw poleceń, których używasz, podobnie jak wszystkie polecenia programu PowerShell usługi Service Fabric, są dostępne dla dowolnego klastra, podłączoną do lokalnego lub zdalnego.
   
    Bardziej wizualny toointeract sposób hello klastra, można użyć narzędzia Service Fabric Explorer opartych na sieci web hello przechodząc zbyt[http://localhost: 19080/Explorer](http://localhost:19080/Explorer) w przeglądarce hello.
   
    ![Wyświetlanie szczegółów aplikacji w narzędziu Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > toolearn więcej informacji o narzędziu Service Fabric Explorer, zobacz [wizualizacja klastra za pomocą Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).
   > 
   > 

## <a name="upgrade-an-application"></a>Uaktualnianie aplikacji
Usługa Service Fabric realizuje uaktualnienia bez przestojów przez monitorowanie kondycji hello aplikacji hello wdrażanej w klastrze hello. Uaktualnienie hello aplikacji WordCount.

Witaj nowej wersji aplikacji hello teraz zlicza tylko słowa zaczynające się od samogłosek. Jak uaktualnienie hello wprowadza, przedstawiono dwie zmiany w zachowaniu aplikacji hello. Po pierwsze szybkość hello jaką zwiększania liczby hello powinna być mniejsza, ponieważ zliczane są mniej słów. Po drugie ponieważ hello pierwszej partycji znajdują się dwie samogłoski (A i E), a wszystkie pozostałe partycje zawierają po jednej sylabie, licznika po pewnym czasie rozpocząć toooutpace hello innych.

1. [Pobierz pakiet w wersji 2 WordCount hello](http://aka.ms/servicefabric-wordcountappv2) toohello tej samej lokalizacji, w której pobrano pakiet w wersji 1 hello.
2. Zwraca tooyour okno programu PowerShell i użyć hello SDK polecenia uaktualniania tooregister hello nową wersję w klastrze hello. Następnie Rozpocznij uaktualnianie hello fabric: / WordCount aplikacji.
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    Powinna zostać wyświetlona zaczyna hello następujące dane wyjściowe w programie PowerShell, ponieważ hello uaktualnienia.
   
    ![Postęp uaktualniania w programie PowerShell][ps-appupgradeprogress]
3. Podczas uaktualniania hello może być łatwiejsze toomonitor stanu z Eksploratora usługi sieć szkieletowa. Uruchom okno przeglądarki i przejdź zbyt[http://localhost: 19080/Explorer](http://localhost:19080/Explorer). Rozwiń węzeł **aplikacji** hello drzewa po lewej stronie powitania, następnie wybierz pozycję **WordCount**, a na końcu **sieci szkieletowej: / WordCount**. Na karcie essentials hello Zobacz stan hello hello uaktualnienia obejmującego domeny uaktualnienia klastra hello.
   
    ![Postęp uaktualniania w narzędziu Service Fabric Explorer][sfx-upgradeprogress]
   
    W trakcie wykonywania uaktualnienia hello za pośrednictwem każdej domeny kontroli kondycji są wykonywane tooensure, która aplikacja hello zachowuje się poprawnie.
4. Jeśli uruchomisz hello wcześniej kwerendy hello zbiór usług w sieci szkieletowej hello: / WordCount aplikacji, zwróć uwagę, że hello wersja usługi wordcountservice uległa zmianie, ale hello wersji WordCountWebService nie:
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Zapytanie dotyczące usług aplikacji po uaktualnieniu][ps-getsfsvc-postupgrade]
   
    W tym przykładzie podkreślono sposób, w jaki usługa Service Fabric zarządza uaktualnieniami aplikacji. Krawędzi tylko hello zestawu usług (albo pakietów kodu/konfiguracji w tych usługach) czy uległy zmianie, co sprawia, że proces hello uaktualniania szybszy i bardziej niezawodny.
5. Na koniec wróć toohello przeglądarki tooobserve hello zachowanie hello nowej wersji aplikacji. Zgodnie z oczekiwaniami, hello realizowany liczba wolniej, a hello pierwszej partycji kończy nieznacznie większa ilość hello.
   
    ![Widok hello nowej wersji aplikacji hello w przeglądarce hello][deployed-app-ui-v2]

## <a name="cleaning-up"></a>Czyszczenie
Przed zakończeniem, ważne jest tooremember, który hello klaster lokalny jest prawdziwe. Aplikacje nadal toorun w tle hello, chyba że zostaną usunięte.  W zależności od charakteru aplikacji hello uruchomionej aplikacji może zajmować znaczące ilości zasobów na tym komputerze. Masz kilka opcji toomanage aplikacji i hello klastra:

1. tooremove poszczególnych aplikacji i wszystkich swoich danych, uruchom następujące polecenie hello:
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    Lub usuwanie aplikacji hello z hello Service Fabric Explorer **akcje** menu lub menu kontekstowego hello w widoku listy aplikacji po lewej stronie powitania.
   
    ![Usuwanie aplikacji w narzędziu Service Fabric Explorer][sfe-delete-application]
2. Po usunięciu aplikacji hello z hello klastra, należy wyrejestrować w wersji 1.0.0 i 2.0.0 hello typ aplikacji WordCount. Usuwanie usuwa pakiety aplikacji hello, w tym kod hello i konfiguracji z magazynu obrazu klastra hello.
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    Lub, w narzędziu Service Fabric Explorer, wybierz **Cofnij Aprowizację typu** dla aplikacji hello.
3. tooshut hello klastra, ale dane aplikacji hello keep i ślady, kliknij przycisk **Zatrzymaj klaster lokalny** w aplikacji na pasku zadań systemu hello.
4. klaster hello toodelete całkowicie, kliknij przycisk **Usuń klaster lokalny** w aplikacji na pasku zadań systemu hello. Ta opcja spowoduje innego hello powolne wdrożenie po następnym naciśnięciu klawisza F5 w programie Visual Studio. Usuń klaster lokalny hello tylko wtedy, gdy nie będziesz toouse go przez pewien czas lub jeśli potrzebujesz tooreclaim zasobów.

## <a name="one-node-and-five-node-cluster-mode"></a>Tryb klastra z jednym węzłem i pięcioma węzłami
Podczas opracowywania aplikacji często są wykonywane szybkie iteracje podczas pisania kodu, debugowania, zmiany kodu i debugowania. toohelp zoptymalizować ten proces, hello klastra lokalnego można uruchomić w dwóch trybach: jednym węzłem lub pięcioma węzłami. Oba tryby klastra mają swoje zalety. Tryb pięcioma węzłami klastra umożliwia toowork z klastrem prawdziwe. Można przetestować scenariusze pracy awaryjnej i pracować z większą liczbą wystąpień i replik usług. Tryb klastra z jednym węzłem jest zoptymalizowany toodo szybkiego wdrożenia i rejestracji usługi, toohelp szybko sprawdzić poprawność kodu za pomocą środowiska uruchomieniowego platformy Service Fabric hello.

Tryby klastra z jednym węzłem i z pięcioma węzłami nie są emulatorami ani symulatorami. Witaj lokalnego klastra projektowego uruchamia hello sam kod platformy, która znajduje się w klastrach obejmujących wiele maszyn.

> [!WARNING]
> Jeśli zmienisz tryb klastra hello hello bieżący klaster zostanie usunięty z systemu i jest tworzony nowy klaster. Hello danych przechowywanych w klastrze hello jest usunięte w przypadku zmiany trybu klastra.
> 
> 

toochange hello tryb tooone węzła klastra, wybierz opcję **Przełącz tryb klastra** w hello usługi sieć szkieletowa Local Cluster Manager.

![Przełączanie trybu klastra][switch-cluster-mode]

Lub zmień tryb klastra hello przy użyciu programu PowerShell:

1. Uruchom nowe okno programu PowerShell jako administrator.
2. Uruchom skrypt instalacji klastra hello z folderu zestawu SDK hello:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    Instalacja klastra trwa kilka chwil. Po zakończeniu instalacji powinny być widoczne dane wyjściowe podobne do poniższych:
   
    ![Dane wyjściowe instalacji klastra][cluster-setup-success-1-node]

## <a name="next-steps"></a>Następne kroki
* Po wdrożeniu i uaktualnieniu wstępnie przygotowanych aplikacji możesz [spróbować utworzyć własne aplikacje w programie Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).
* Wszystkie operacje hello hello klaster lokalny w tym artykule można wykonać na [Azure klastra](service-fabric-cluster-creation-via-portal.md) również.
* podstawowa została Hello uaktualnienie wykonane w tym artykule. Zobacz hello [dokumentacji uaktualnienia](service-fabric-application-upgrade.md) toolearn więcej informacji na temat hello możliwościach i elastyczności uaktualnień sieci szkieletowej usług.

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
