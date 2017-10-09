---
title: "aaaCI/CD z Wpięć tooAzure maszyn wirtualnych o Team Services | Dokumentacja firmy Microsoft"
description: "Konfigurowanie ciągłej integracji (CI), jak i ciągłe wdrażanie (CD) aplikacji Node.js przy użyciu maszyn wirtualnych tooAzure Wpięć z zarządzania zleceniami w programie Visual Studio Team Services (VSTS) lub programu Microsoft Team Foundation Server (TFS)"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a>Wdrażanie Twojej aplikacji tooLinux maszyn wirtualnych przy użyciu Wpięć i usługi Team Services

Ciągłej integracji (CI), jak i ciągłe wdrażanie (CD) jest potoku, za pomocą którego można kompilacji, wersji i wdrażanie kodu. Usługi Team Services zapewnia pełną, kompletny zestaw narzędzi automatyzacji CI/CD dla tooAzure wdrożenia. Wpięć to popularnych 3rd firm CI/CD serwerowych narzędzie, które udostępnia również automatyzacji CI/CD. Można użyć obu razem toocustomize sposób dostarczania Twojej aplikacji w chmurze lub usługi.

W tym samouczku, użyj toobuild Wpięć **aplikacji sieci web Node.js**i Visual Studio Team Services toodeploy on tooa [grupę wdrożenia](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) zawierających maszyny wirtualne systemu Linux.

Wykonasz następujące zadania:

> [!div class="checklist"]
> * Tworzenie aplikacji w Wpięć
> * Skonfiguruj Wpięć integracji usługi Team Services
> * Utwórz grupę wdrożenia dla hello maszyn wirtualnych platformy Azure
> * Tworzenie definicji wersji, która konfiguruje hello maszyn wirtualnych i wdrożenie aplikacji hello

## <a name="before-you-begin"></a>Przed rozpoczęciem

* Musisz mieć konto Wpięć tooa dostępu. Jeśli jeszcze nie utworzono serwera Wpięć, zobacz [dokumentacji Wpięć](https://jenkins.io/doc/). 

* Zaloguj się tooyour konta usługi Team Services (`https://{youraccount}.visualstudio.com`). 
  Możesz uzyskać [bezpłatnego konta usługi Team Services](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).

  > [!NOTE]
  > Aby uzyskać więcej informacji, zobacz [połączenia usług tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).

* Utwórz osobisty token dostępu (PAWEŁ) w ramach konta usługi Team Services, jeśli nie został wcześniej. Wpięć wymaga tego tooaccess informacji konta usługi Team Services.
  Odczyt [jak utworzyć osobisty token dostępu dla usługi Team Services i TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn jak toogenerate jeden.

## <a name="get-hello-sample-app"></a>Pobierz hello przykładowej aplikacji

Należy toodeploy aplikacji przechowywanych w repozytorium Git.
W tym samouczku, zalecane jest użycie [tej przykładowej aplikacji dostępne w serwisie GitHub](https://github.com/azooinmyluggage/fabrikam-node).

1. Utwórz rozwidlenia tej aplikacji i zanotuj lokalizację hello (URL) do użycia w kolejnych krokach tego samouczka.

1. Wprowadź rozwidlenia hello **publicznego** toosimplify tooGitHub połączyć się później.

> [!NOTE]
> Aby uzyskać więcej informacji, zobacz [rozwidlania repozytorium](https://help.github.com/articles/fork-a-repo/) i [ujawnianie prywatnym repozytorium](https://help.github.com/articles/making-a-private-repository-public/).

> [!NOTE]
> Aplikacja Hello został zbudowany przy użyciu [narzędzia Yeoman](http://yeoman.io/learning/index.html); używa **Express**, **bower**, i **grunt**; i zawiera niektóre **npm**pakietów jako zależności.
> Witaj przykładowej aplikacji zawiera zestaw [szablonów usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) , są używane toodynamically utworzyć hello maszyn wirtualnych do wdrożenia na platformie Azure. Te szablony są używane przez zadania w hello [Team Services wersji definicji](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).
> Szablon głównego Hello tworzy sieciową grupę zabezpieczeń, maszyny wirtualnej i sieci wirtualnej. Przypisuje publicznego adresu IP, a otwiera przychodzący port 80. Dodaje tag, który jest używany przez wdrożenie hello tooreceive maszyny zbyt wybierz hello hello wdrożenia grupy.
>
> przykład Witaj zawiera także skrypt, który konfiguruje Nginx i wdraża aplikacji hello. Wykonaniem na każdym hello maszyn wirtualnych. W szczególności skryptu hello instaluje węzła, Nginx i PM2; Konfiguruje Nginx i PM2; następnie uruchamia hello węzła aplikacji.

## <a name="configure-jenkins-plugins"></a>Skonfiguruj Wpięć wtyczek

Najpierw należy skonfigurować dwa wtyczek Wpięć dla **NodeJS** i **integracji z usługami zespołu**.

1. Otwórz konta Wpięć i wybierz polecenie **Zarządzanie Wpięć**.

1. W hello **Zarządzanie Wpięć** wybierz pozycję **Zarządzanie wtyczkami**.

1. Filtr hello listy toolocate hello **NodeJS** wtyczki i zainstaluj go bez ponownego uruchamiania.

   ![Dodawanie hello NodeJS wtyczki tooJenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. Filtr hello listy toofind hello **Team Foundation Server** wtyczki i zainstaluj go. (Ta wtyczka dotyczy Team Foundation Server i usługi Team Services.) Ponowne uruchamianie Wpięć nie jest konieczne.

## <a name="configure-jenkins-build-for-nodejs"></a>Konfigurowanie kompilowania Wpięć dla środowiska Node.js

W Wpięć Utwórz nowy projekt kompilacji i skonfigurować w następujący sposób:

1. W hello **ogólne** wprowadź nazwę dla projektu kompilacji.

1. W hello **zarządzania kodem źródłowym** wybierz opcję **Git** , a następnie wprowadź szczegóły hello hello repozytorium i gałęzi hello zawierający kod aplikacji.

   ![Dodaj kompilacji tooyour repozytorium](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > Jeśli repozytorium nie jest publiczny, wybierz **Dodaj** i podaj poświadczenia tooconnect tooit.

1. W hello **kompilacji wyzwalaczy** wybierz opcję **SCM sondowania** , a następnie wprowadź harmonogram hello `H/03 * * * *` repozytorium Git hello toopoll zmiany co trzy minuty. 

1. W hello **Build Environment** wybierz opcję **Podaj węzła &amp; npm bin / ŚCIEŻKĘ folderu** , a następnie wprowadź `NodeJS` dla hello wartość Node JS instalacji. Pozostaw **pliku npmrc** ustawioną wartość "Użyj domyślnej system."

1. W hello **kompilacji** wprowadź polecenie hello `npm install` tooensure wszystkie zależności są aktualizowane.

## <a name="configure-jenkins-for-team-services-integration"></a>Skonfiguruj Wpięć integracji usługi Team Services

1. W hello **akcje postkompilacyjnego** karcie dla **tooarchive pliki**, wprowadź `**/*` tooinclude wszystkich plików.

1. Dla **wyzwalanie wydania w TFS/Team Services**, wprowadź pełny adres URL hello konta (takie jak `https://your-account-name.visualstudio.com`), hello nazwę projektu, nazwę definicji wersji hello (utworzone później), i hello poświadczenia tooconnect tooyour konta.
   Należy swoją nazwę użytkownika i hello PAWEŁ utworzony wcześniej. 

   ![Konfigurowanie Wpięć działania mające miejsce po kompilacji](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. Zapisz hello kompilacji projektu.

## <a name="create-a-jenkins-service-endpoint"></a>Tworzenie punktu końcowego usługi Wpięć

Punkt końcowy usługi umożliwia tooJenkins tooconnect Team Services.

1. Otwórz hello **usług** strony w Team Services, otwórz hello **nowy punkt końcowy usługi** listy, a następnie wybierz pozycję **Wpięć**.

   ![Dodawanie punktu końcowego Wpięć](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. Wprowadź nazwę użyje toorefer toothis połączenia.

1. Wprowadź adres URL powitania serwera Wpięć i znaczników hello **zaakceptować niezaufane certyfikaty protokołu SSL** opcji.

1. Wprowadź hello nazwę użytkownika i hasło do konta Wpięć.

1. Wybierz **sprawdzić połączenie** toocheck, który hello informacje są poprawne.

1. Wybierz **OK** punktu końcowego usługi hello toocreate.

## <a name="create-a-deployment-group"></a>Utwórz grupę wdrożenia

Należy [grupę wdrożenia](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) zbyt zawierają hello maszyn wirtualnych.

1. Otwórz hello **wersje** kartę hello **kompilacji &amp; wersji** koncentratora, a następnie otwórz hello **grupy wdrożenia** , a następnie wybierz **+ nowy**.

1. Wprowadź nazwę grupy wdrożenia hello i opcjonalny opis.
   Następnie wybierz pozycję **Utwórz**.

Zadanie wdrażania grupy zasobów Azure Hello tworzy i rejestruje hello maszyn wirtualnych, gdy jest uruchamiany przy użyciu szablonu usługi Azure Resource Manager hello.
Nie należy toocreate i samodzielnie zarejestrować hello maszyn wirtualnych.

## <a name="create-a-release-definition"></a>Utwórz definicję zlecenia

Proces hello Team Services będą wykonywane aplikacji hello toodeploy określa definicji wersji.
toocreate hello wersji definicji w Team Services:

1. Otwórz hello **wersje** kartę hello **kompilacji &amp; wersji** koncentratora, otwórz hello  **+**  listy rozwijanej liście hello definicji wersji, a następnie wybierz pozycję Witaj **Tworzenie wersji definicji**. 

1. Wybierz hello **pusty** szablonu i wybierz polecenie **dalej**.

1. W hello **artefakty** kliknij na **Link artefaktu** i wybierz polecenie **Wpięć**. Wybierz połączenie Wpięć usługi punktu końcowego. Następnie wybierz zadanie źródła Wpięć hello i wybierz **Utwórz**. 

1. W hello nowych definicji wersji, wybierz polecenie **+ Dodaj zadania** i Dodaj **wdrożenie grupy zasobów Azure** zadań toohello domyślnego środowiska.

1. Wybierz hello listy rozwijanej strzałkę dalej toohello **+ Dodaj zadania** Dodaj definicję toohello fazy wdrożenia grupy i łącza.

   ![Dodawanie grupy faza wdrożenia](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. W katalogu zadania hello, otwórz hello **narzędzie** i Dodaj wystąpienia hello **skrypt powłoki** zadań.

1. Hello parametrów szablonu używanego w hello wdrożenie grupy zasobów Azure zadań ustawia hello admin hasło używane tooconnect toohello maszyn wirtualnych.
   Podaj hasło ze zmienną hello **$(adminpassword)**:
   
   - Otwórz hello **zmienne** kartę, a w hello **zmienne** sekcji, wprowadź nazwę hello `adminpassword`.

   - Wprowadź hasło administratora hello.

   - Wybierz hello "kłódki" ikona dalej toohello wartości tekstowe tooprotect hello hasło. 

## <a name="configure-hello-azure-resource-group-deployment-task"></a>Zadanie wdrażania grupy zasobów Azure hello konfiguracji

Witaj **wdrożenie grupy zasobów Azure** zadań jest używane toocreate hello wdrożenia grupy. Skonfiguruj w następujący sposób:

* **Subskrypcja platformy Azure:** wybierz połączenie z listy hello w obszarze **dostępne połączenia usługi Azure**. 
  Jeśli widoczne żadne połączenia, wybierz polecenie **Zarządzaj**, wybierz pozycję **nowy punkt końcowy usługi** następnie **usługi Azure Resource Manager**i postępuj zgodnie z monitami hello.
  Zwraca tooyour wersji definicji, hello odświeżania **AzureRM subskrypcji** listy i utworzone połączenie select hello.

* **Grupa zasobów**: Wprowadź nazwę grupy zasobów hello utworzony wcześniej.

* **Lokalizacja**: Wybierz region hello wdrożenia.

  ![Utworzenie nowej grupy zasobów](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* **Lokalizacja szablonów**:`URL of hello file`

* **Łącze szablonu**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`

* **Łącze parametrów szablonu**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`

* **Zastąp parametry szablonu**: Lista hello zastępowania wartości, na przykład: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.<br />Wstaw wartości określonej dla hello {symbole zastępcze}. 

* **Wymagania wstępne włączyć**:`Configure with Deployment Group agent`

* **Punkt końcowy TFS/VSTS**: Wybierz **Dodaj** , a następnie w oknie dialogowym "Dodaj nowe połączenie usługi Team Foundation Server/zespołu" hello, zaznacz **Token uwierzytelniania na podstawie**. Wprowadź nazwę połączenia hello i adres URL hello projektu zespołowego. Następnie generowanie i wprowadź [osobistych dostępu tokenu (PAWEŁ)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) projektu zespołowego tooyour tooauthenticate hello połączenia.

  ![Tworzenie osobistego tokenu dostępu](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* **Projekt zespołowy**: Wybierz bieżącego projektu.

* **Grupa wdrożenia**: Wprowadź hello tej samej nazwy grupy wdrożenia jako używaną na potrzeby hello **grupy zasobów** parametru.

ustawienia domyślne Hello hello zadania wdrażania grupy zasobów platformy Azure są toocreate lub tak przyrostowo aktualizować zasobu i toodo. zadanie Hello tworzy Witaj Witaj maszyn wirtualnych po raz pierwszy uruchamia, a następnie wystarczy zaktualizować je.

## <a name="configure-hello-shell-script-task"></a>Skonfiguruj zadania skryptu powłoki hello

Witaj **skrypt powłoki** zadań jest używane tooprovide Konfiguracja hello toorun skryptu, na każdy serwer tooinstall Node.js i rozpocząć hello aplikacji. Skonfiguruj w następujący sposób:

* **Ścieżka skryptu**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`

* **Określ pracy katalogu**:`Checked`

* **Katalog roboczy**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node`
   
## <a name="rename-and-save-hello-release-definition"></a>Zmień nazwę i zapisać hello wersji definicji

1. Edytuj nazwę hello hello wersji definicji toohello nazwy określone w **działania mające miejsce po kompilacji** kartę hello kompilacji w Wpięć. Wpięć wymaga to nazwa toobe stanie tootrigger nową wersję, po zaktualizowaniu hello źródła artefaktów.

1. Opcjonalnie można zmienić nazwy hello hello środowiska, klikając nazwę hello. 

1. Wybierz **zapisać**i wybierz polecenie **OK**.

## <a name="start-a-manual-deployment"></a>Rozpocznij wdrażanie ręczne

1. Wybierz **+ wersji** i wybierz **Tworzenie wersji**.

1. Zaznacz kompilacji hello ukończono hello wyróżnione listy rozwijanej i wybierz polecenie **Utwórz**.

1. Wybierz łącze wersji hello hello komunikatu podręcznego. Na przykład: "wersji **wersji 1** został utworzony."

1. Otwórz hello **dzienniki** karcie toowatch hello wersji konsoli w danych wyjściowych.

1. W przeglądarce otwórz adres URL hello jednego z serwerów hello dodana grupa wdrożenia tooyour. Na przykład wprowadź`http://{your-server-ip-address}`

## <a name="start-a-cicd-deployment"></a>Rozpocząć wdrażanie elementu konfiguracji/CD

1. W hello wersji definicji, usuń zaznaczenie pola wyboru hello **włączone** checkbox w hello **opcje sterowania** części ustawień hello hello zadania wdrażania grupy zasobów platformy Azure.
   Dla przyszłych wdrożeń toohello istniejącego wdrożenia grupy, nie trzeba toore — wykonanie tego zadania.

1. Przejdź do repozytorium Git źródła toohello i modyfikować zawartość hello hello **h1** pozycji w pliku hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).

1. Zatwierdź zmiany.

1. Po kilku minutach, pojawi się nowe wydanie utworzone w hello **wersje** strona Team Services lub TFS. Otwórz miejsce hello wersji toosee hello wdrożenia. Gratulacje!

## <a name="next-steps"></a>Następne kroki

Ten samouczek służy do automatycznego wdrożenia hello tooAzure aplikacji przy użyciu Wpięć kompilacji i usługi Team Services w wersji. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie aplikacji w Wpięć
> * Skonfiguruj Wpięć integracji usługi Team Services
> * Utwórz grupę wdrożenia dla hello maszyn wirtualnych platformy Azure
> * Tworzenie definicji wersji, która konfiguruje hello maszyn wirtualnych i wdrożenie aplikacji hello

Więcej informacji na temat sposobu stosu toodeploy światło (Linux, Apache MySQL i PHP) poprawić toohello dalej toolearn samouczka.

> [!div class="nextstepaction"]
> [Wdrażanie stosu LAMP](tutorial-lamp-stack.md)