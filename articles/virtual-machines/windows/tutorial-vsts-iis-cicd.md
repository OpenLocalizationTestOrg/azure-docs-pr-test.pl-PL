---
title: "aaaCreate potok CI/CD w platformie Azure za pomocą usługi Team Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Visual Studio Team Services potoku dla ciągłej integracji i dostarczania, która wdraża tooIIS aplikacji sieci web, na maszynie Wirtualnej systemu Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a>Tworzenie potoku ciągłej integracji z Visual Studio Team Services i IIS
tooautomate hello kompilację, testów i wdrożenia etapy tworzenia aplikacji, można użyć ciągłej integracji i wdrażania (CI/CD) potoku. W tym samouczku utworzysz potok CI/CD przy użyciu programu Visual Studio Team Services i Windows maszyny wirtualnej (VM) na platformie Azure z uruchomionymi usługami IIS. Omawiane kwestie:

> [!div class="checklist"]
> * Publikuj projekt usługi Team Services tooa aplikacji sieci web ASP.NET
> * Tworzenie definicji kompilacji, która jest wyzwalany przez kod zatwierdzenia
> * Instalowanie i konfigurowanie usług IIS na maszynie wirtualnej na platformie Azure
> * Dodaj grupę wdrożenia tooa wystąpienia usług IIS hello w Team Services
> * Utwórz nową web toopublish definicji wersji tooIIS pakiety wdrażania
> * Test hello CI/CD potoku

Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom `Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="create-project-in-team-services"></a>Tworzenie projektu na Team Services
Visual Studio Team Services umożliwia łatwe współpracy i rozwoju bez zachowania to rozwiązanie do zarządzania lokalnymi kodu. Usługi Team Services zapewnia testowania kodu w chmurze, kompilacji i usługi application insights. Można wybrać repozytorium kontroli wersji i IDE, która najlepiej pasuje do programowania kodu. W tym samouczku można użyć bezpłatnego konta toocreate Podstawowa aplikacja sieci web ASP.NET i CI/CD potoku. Jeśli nie masz już konto usługi Team Services [utworzyć](http://go.microsoft.com/fwlink/?LinkId=307137).

toomanage hello kod proces, definicje, kompilacji i wydania definicje, tworzenie projektu na Team Services w następujący sposób:

1. Otwórz pulpit nawigacyjny usługi Team Services w przeglądarce sieci web i wybierz polecenie **nowy projekt**.
2. Wprowadź *myWebApp* dla hello **Nazwa projektu**. Pozostaw wszystkie inne toouse wartości domyślne *Git* kontroli wersji i *Agile* elementów roboczych procesu.
3. Wybierz opcję hello zbyt**udostępniać** *członków zespołu*, a następnie wybierz pozycję **Utwórz**.
5. Po utworzeniu projektu, wybierz opcję hello zbyt**zainicjować README lub gitignore**, następnie **zainicjować**.
6. Wewnątrz nowego projektu, wybierz **pulpity nawigacyjne** górze hello, następnie wybierz **Otwórz w programie Visual Studio**.


## <a name="create-aspnet-web-application"></a>Tworzenie aplikacji sieci web ASP.NET
W poprzednim kroku hello utworzonego projektu w Team Services. Ostatnim krokiem Hello zostanie otwarty nowy projekt w programie Visual Studio. Zarządzanie zatwierdzenia kodu w hello **Team Explorer** okna. Utwórz lokalną kopię nowego projektu, a następnie utworzyć aplikację sieci web platformy ASP.NET na podstawie szablonu w następujący sposób:

1. Wybierz **klonowania** toocreate repozytorium git lokalnego projektu Team Services.
    
    ![Klonowanie repozytorium z projektu Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. W obszarze **rozwiązań**, wybierz pozycję **nowy**.

    ![Utwórz rozwiązanie aplikacji sieci web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. Wybierz **sieci Web** szablonów, a następnie wybierz pozycję hello **aplikacji sieci Web ASP.NET** szablonu.
    1. Wprowadź nazwę aplikacji, takich jak *myWebApp*i usuń zaznaczenie pola hello **Utwórz katalog rozwiązania**.
    2. Jeśli jest dostępna opcja hello, hello Usuń zaznaczenie pola wyboru zbyt**tooproject Dodaj usługę Application Insights**. Usługa Application Insights wymaga tooauthorize użytkownik aplikacji sieci web z usługą Azure Application Insights. tookeep prostotę, w tym samouczku, Pomiń ten proces.
    3. Kliknij przycisk **OK**.
4. Wybierz **MVC** z listy szablonów hello.
    1. Wybierz **Zmień uwierzytelnianie**, wybierz **bez uwierzytelniania**, a następnie wybierz pozycję **OK**.
    2. Wybierz **OK** toocreate rozwiązania.
5. W hello **Team Explorer** okna, wybierz **zmiany**.

    ![Zatwierdź repozytorium git usługi tooTeam lokalne zmiany](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. W polu tekstowym zatwierdzania hello, wpisz wiadomość, takich jak *zatwierdzania początkowego*. Wybierz **zatwierdzić wszystkie i synchronizacji** z menu rozwijanego hello.


## <a name="create-build-definition"></a>Tworzenie definicji kompilacji
W Team Services należy użyć toooutline definicji kompilacji, jak powinny zostać skompilowane aplikacji. W tym samouczku utworzymy podstawową definicję przyjmuje naszego kodu źródłowego buduje rozwiązanie hello, a następnie tworzy sieci web do wdrożenia pakietu aplikacji sieci web hello toorun możemy użyć na serwerze IIS.

1. W projekcie usługi Team Services, wybierz **kompilacji i wydania** górze hello, następnie wybierz **kompilacje**.
3. Wybierz **+ nową definicję**.
4. Wybierz hello **ASP.NET (wersja ZAPOZNAWCZA)** szablonu, a następnie wybierz **Zastosuj**.
5. Pozostaw wszystkie domyślne hello wartości zadania. W obszarze **Pobierz źródła**, upewnij się, że hello *myWebApp* repozytorium i *wzorca* są zaznaczone oddziału.

    ![Utwórz definicję kompilacji w projekcie usługi Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. Na powitania **wyzwalaczy** karcie, przesuń suwak hello **włączyć tego wyzwalacza** za*włączone*.
7. Zapisz definicję kompilacji hello i kolejki nowej kompilacji, wybierając **Zapisz & kolejka** , następnie **Zapisz & kolejka** ponownie. Pozostaw wartości domyślne hello i wybierz **kolejki**.

Obejrzyj jako kompilacji hello jest zaplanowane na agencie hostowanej, następnie rozpoczyna toobuild. Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

![Pomyślnie kompilacji projektu Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej
tooprovide toorun platforma aplikacji sieci web ASP.NET, należy maszyny wirtualnej systemu Windows z uruchomionymi usługami IIS. Usługi Team Services używa toointeract agenta z wystąpieniem usług IIS hello zatwierdzisz kod i kompilacje są wyzwalane.

Tworzenie maszyny Wirtualnej systemu Windows Server 2016 przy użyciu [w tym przykładzie skrypt](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json). Go zajmuje kilka minut dla hello skryptu toorun i Utwórz hello maszyny Wirtualnej. Po utworzeniu hello maszyny Wirtualnej, należy otworzyć port 80 dla ruchu w sieci web z [AzureRmNetworkSecurityRuleConfig Dodaj](/powershell/module/azurerm.resources/new-azurermresourcegroup) w następujący sposób:

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

tooyour tooconnect maszyny Wirtualnej, Uzyskaj hello publicznego adresu IP z [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) w następujący sposób:

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

Tworzenie sesji usług pulpitu zdalnego tooyour maszyny Wirtualnej:

```cmd
mstsc /v:<publicIpAddress>
```

Na powitania maszyny Wirtualnej, otwórz **administratora programu PowerShell** wiersza polecenia. Zainstaluj usługi IIS i wymagane funkcje platformy .NET:

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a>Utwórz grupę wdrożenia
toopush limit hello web wdrażanie serwera IIS toohello pakietu, zdefiniuj grupę wdrożenia w Team Services. Ta grupa umożliwia toospecify serwerów, które są hello docelowy nowych kompilacji, jak zatwierdzić tooTeam kodu usługi i kompilacji zostały zakończone.

1. W usłudze Team Services, wybierz **kompilacji i wydania** , a następnie wybierz **grupy wdrożenia**.
2. Wybierz **Dodaj wdrożenie grupy**.
3. Wprowadź nazwę grupy hello, takich jak *Mój_iis*, a następnie wybierz pozycję **Utwórz**.
4. W hello **rejestrowania maszyn** upewnij się, *Windows* jest zaznaczone, a następnie zaznacz pole hello zbyt**używania osobisty token dostępu w skrypcie hello w celu uwierzytelniania**.
5. Wybierz **Skopiuj skrypt tooclipboard**.


### <a name="add-iis-vm-toohello-deployment-group"></a>Dodaj grupę wdrożenia toohello maszyn wirtualnych usług IIS
Witaj utworzoną grupę wdrożenia dodawać każdej grupy toohello wystąpienia usług IIS. Usługi Team Services generuje skrypt, który pobiera i konfiguruje agenta na powitania wdrożyć maszynę Wirtualną, która odbiera nowej sieci web pakiety, a następnie stosuje je tooIIS.

1. Po powrocie do hello **administratora programu PowerShell** sesji na maszynie Wirtualnej, Wklej i uruchom skrypt hello skopiowanych z usługi Team Services.
2. Gdy zostanie wyświetlony monit o tooconfigure tagi dla agenta hello wybierz *Y* , a następnie wprowadź *web*.
3. Po wyświetleniu monitu dla konta użytkownika hello, naciśnij klawisz *zwracać* tooaccept hello domyślne.
4. Poczekaj, aż hello toofinish skryptu z następującym komunikatem *vstsagent.account.computername usługa została uruchomiona pomyślnie*.
5. W hello **grupy wdrożenia** strony hello **kompilacji i wydania** menu, otwórz hello *Mój_iis* grupę wdrożenia. Na powitania **maszyny** karcie, sprawdź, czy maszyna wirtualna jest wyświetlane.

    ![Maszyna wirtualna pomyślnie dodano grupę wdrożenia usług tooTeam](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a>Utwórz definicję zlecenia
toopublish kompilacji, możesz utworzyć definicję wersji w Team Services. Ta definicja jest automatycznie wyzwalane przez to pomyślnego utworzenia kompilacji aplikacji. Wybierz toopush grupy wdrożenia hello pakiet do wdrożenia sieci web, a następnie zdefiniuj hello odpowiednie ustawienia usług IIS.

1. Wybierz **kompilacji i wydania**, a następnie wybierz pozycję **kompilacje**. Wybierz definicję kompilacji hello utworzony w poprzednim kroku.
2. W obszarze **niedawno ukończoną**, wybierz hello ostatniej kompilacji, a następnie wybierz **wersji**.
3. Wybierz **tak** toocreate definicji wersji.
4. Wybierz hello **pusty** szablonu, następnie wybierz **dalej**.
5. Sprawdź definicję kompilacji projektu i źródło hello są wypełniane przy użyciu projektu.
6. Wybierz hello **ciągłe wdrażanie** pole wyboru, a następnie wybierz **Utwórz**.
7. Zaznacz pole listy rozwijanej hello obok zbyt**+ Dodaj zadania** i wybierz polecenie *dodać faza wdrożenia grupy*.
    
    ![Dodaj definicję toorelease zadania w usłudze Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. Wybierz **Dodaj** dalej zbyt**Deploy(Preview) aplikacji sieci Web usług IIS**, a następnie wybierz pozycję **Zamknij**.
9. Wybierz hello **Uruchom na grupę wdrożenia** zadaniem nadrzędnym.
    1. Dla **grupę wdrożenia**, wybierz pozycję hello wdrożenia grupy utworzonej wcześniej, takich jak *Mój_iis*.
    2. W hello **komputera tagi** wybierz opcję **Dodaj** i wybierz polecenie hello *web* tagu.
    
    ![Zwolnij definicji zadania wdrażania w grupie dla usług IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. Wybierz hello **Wdróż: Wdrażanie aplikacji sieci Web usług IIS** tooconfigure zadań programu IIS wystąpienia następujące ustawienia:
    1. Aby uzyskać **nazwa witryny sieci Web**, wprowadź *domyślna witryna sieci Web*.
    2. Pozostaw hello wszystkie inne ustawienia domyślne.
12. Wybierz **zapisać**, a następnie wybierz pozycję **OK** dwa razy.


## <a name="create-a-release-and-publish"></a>Tworzenie zlecenia i publikowanie
Teraz możesz wypchnąć sieci web wdrażanie pakietu jako nową wersję. Ten krok komunikuje się z agentem hello na każdego wystąpienia, które jest częścią grupy wdrożenia hello, wypchnięcia hello web wdrożenia pakietu, a następnie konfiguruje aplikacji sieci web programu IIS toorun hello zaktualizowane.

1. W definicji wersji, wybierz **+ wersji**, a następnie wybierz **Tworzenie wersji**.
2. Sprawdź, czy hello ostatniej kompilacji jest zaznaczony na liście rozwijanej hello wraz z **automatycznego wdrożenia: po utworzeniu wersji**. Wybierz pozycję **Utwórz**.
3. Transparent małych hello górze wyświetlany definicję zlecenia, takie jak *wersji "Wersji 1" utworzył*. Wybierz hello wersji łącze.
4. Otwórz hello **dzienniki** karcie toowatch hello wersji postępu.
    
    ![Pomyślne wersji Team Services i sieci web wdrażanie pakietu wypychania](media/tutorial-vsts-iis-cicd/successful_release.png)

5. Po zakończeniu wersji hello Otwórz przeglądarkę sieci web, a następnie wprowadź hello publiczny adres OPS maszyny wirtualnej. Aplikacja sieci web programu ASP.NET jest uruchomiona.

    ![Uruchomiona na maszynie Wirtualnej IIS aplikacji sieci web ASP.NET](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a>Test hello całego elementu konfiguracji/CD potoku
Z aplikacji sieci web uruchomionej na serwerze IIS teraz spróbuj hello całego elementu konfiguracji/CD potoku. Po wprowadzeniu zmiany w Visual Studio i zatwierdzania wyzwolenia kodu, kompilacji, następnie wyzwalające zlecenia sieci web zaktualizowane wdrożyć tooIIS pakietu:

1. W programie Visual Studio Otwórz hello **Eksploratora rozwiązań** okna.
2. Przejdź Otwórz tooand *myWebApp | Widoki | Strona główna | Index.cshtml*
3. Edytuj tooread wiersz 6:

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. Zapisz plik hello.
5. Otwórz hello **Team Explorer** okna, wybierz hello *myWebApp* projektu, a następnie wybierz pozycję **zmiany**.
6. Wpisz wiadomość, zatwierdzania, takich jak *potoku testowania CI/CD*, a następnie wybierz **wszystkie zatwierdzenia i synchronizacji** z menu rozwijanego hello.
7. W obszarze roboczym Team Services nowej kompilacji zostanie wywołany z hello kod zatwierdzenia. 
    - Wybierz **kompilacji i wydania**, a następnie wybierz pozycję **kompilacje**. 
    - Wybierz definicję kompilacji, a następnie wybierz hello **w kolejce & uruchomiona** toowatch kompilacji jako hello kompilacji realizowany.
9. Po kompilacji hello zakończy się pomyślnie, zostanie wywołany nowej wersji.
    - Wybierz **kompilacji i wydania**, następnie **wersje** toosee hello web wdrożyć pakiet wypychana tooyour maszyn wirtualnych usług IIS. 
    - Wybierz hello **Odśwież** ikona tooupdate hello stanu. Gdy hello *środowisk* kolumna zawiera zielony znacznik wyboru, wersji hello zostało pomyślnie wdrożone tooIIS.
11. toosee zastosować zmian użytkownika, Odśwież witryny usług IIS w przeglądarce sieci Web.

    ![Uruchamianie na IIS maszyny Wirtualnej na podstawie elementu konfiguracji/CD potoku aplikacji sieci web ASP.NET](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a>Następne kroki

W tym samouczku utworzono aplikację sieci web platformy ASP.NET w Team Services i skonfigurowany kompilacji i wersji definicji toodeploy nowej sieci web wdrażanie pakietów tooIIS na każdym zatwierdzeniu kodu. W tym samouczku omówiono:

> [!div class="checklist"]
> * Publikuj projekt usługi Team Services tooa aplikacji sieci web ASP.NET
> * Tworzenie definicji kompilacji, która jest wyzwalany przez kod zatwierdzenia
> * Instalowanie i konfigurowanie usług IIS na maszynie wirtualnej na platformie Azure
> * Dodaj grupę wdrożenia tooa wystąpienia usług IIS hello w Team Services
> * Utwórz nową web toopublish definicji wersji tooIIS pakiety wdrażania
> * Test hello CI/CD potoku

Jak przejść dalej toolearn samouczka toohello toosecure serwera sieci web z certyfikatów SSL.

> [!div class="nextstepaction"]
> [Zabezpieczenia serwera sieci web przy użyciu protokołu SSL](tutorial-secure-web-server.md)