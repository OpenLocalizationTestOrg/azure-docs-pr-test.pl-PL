---
title: "aaaCI/CD z aparatem usługi kontenera Azure i tryb Swarm | Dokumentacja firmy Microsoft"
description: "Aparat usługi kontenera Azure za pomocą toodeliver stale aplikacji .NET Core wielu kontenera Docker Swarm tryb rejestru kontenera Azure i Visual Studio Team Services"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Docker, kontenerów, Micro-services, Swarm, Azure, programu Visual Studio Team usług, metodyki DevOps, aparat ACS"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a>Pełna CI/CD toodeploy potoku aplikacji usługi kontenera w usłudze kontenera platformy Azure z aparatem ACS i Docker Swarm trybie przy użyciu programu Visual Studio Team Services

*Ten artykuł jest oparty na [CI pełnej/CD potoku toodeploy aplikacji usługi kontenera w usłudze kontenera platformy Azure przy użyciu rozwiązania Docker Swarm przy użyciu programu Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) dokumentacji*

Dzisiaj jeden z hello największych wyzwań po opracowywanie nowoczesnych aplikacji w chmurze hello jest możliwe toodeliver te aplikacje stale. W tym artykule dowiesz się, jak tooimplement pełnej ciągłej integracji i wdrażania (CI/CD) potoku, przy użyciu: 
* Aparat usługi kontenera platformy Azure z Docker Swarm trybem
* Azure Container Registry
* Visual Studio Team Services

Ten artykuł jest oparty na prostej aplikacji, dostępnych na [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), rozwinięte z platformy ASP.NET Core. Aplikacja Hello składa się z czterech różnych usług: trzy sieci web, interfejsów API i frontonu sieci web co:

![MyShop przykładowej aplikacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

cel Hello jest toodeliver tej aplikacji stale w klastrze Docker Swarm tryb, za pomocą programu Visual Studio Team Services. następujące Hello rysunek szczegóły tego potoku ciągłego dostarczania:

![MyShop przykładowej aplikacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

Poniżej przedstawiono krótki opis kroków hello:

1. Zmiany kodu są repozytorium kodu źródłowego zatwierdzone toohello (tutaj GitHub) 
2. GitHub uaktywnia kompilację w Visual Studio Team Services 
3. Visual Studio Team Services pobiera najnowsza wersja źródła hello hello i tworzy wszystkie obrazy hello tworzące aplikacji hello 
4. Visual Studio Team Services wypchnięcia każdego obrazu tooa Docker rejestru utworzone za pomocą usługi Azure kontenera rejestru hello 
5. Visual Studio Team Services wyzwala nową wersją 
6. Niektóre polecenia przy użyciu protokołu SSH w węźle głównym klastra usługi kontenera platformy Azure hello uruchamia Hello zlecenia 
7. Tryb docker Swarm w klastrze hello ściąga hello najnowszej wersji hello obrazów 
8. nową wersję aplikacji hello Hello jest wdrażane za pomocą Docker stosu 

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem tego samouczka potrzebne hello toocomplete następujące zadania:

- [Tworzenie klastra trybu Swarm usługi kontenera platformy Azure z aparatem ACS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [Połącz z klastrem Swarm hello usługi kontenera platformy Azure](../container-service-connect.md)
- [Tworzenie rejestru kontenera platformy Azure](../../container-registry/container-registry-get-started-portal.md)
- [Utworzony projekt konta i zespołu Visual Studio Team Services](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Rozwidlania tooyour repozytorium GitHub hello konto GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> Witaj orchestrator Docker Swarm usługi kontenera platformy Azure używa starszej wersji autonomicznej Swarm. Obecnie zintegrowane hello [tryb Swarm](https://docs.docker.com/engine/swarm/) (w Docker 1.12 lub nowszej) nie jest obsługiwane orchestrator w usłudze kontenera platformy Azure. Z tego powodu używamy [aparat ACS](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), przyczyniły się społeczności [szablon szybkiego startu](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), lub rozwiązania Docker w hello [portalu Azure Marketplace](https://azuremarketplace.microsoft.com).
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Krok 1: Skonfiguruj konto usługi Visual Studio Team Services 

W tej sekcji należy skonfigurować konto w Visual Studio Team Services. tooconfigure VSTS usługi punktów końcowych, projektu Visual Studio Team Services, kliknij przycisk hello **ustawienia** ikonę w hello narzędzi i wybierz **usług**.

![Punkt końcowy usługi otwarte](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a>Połącz konto usługi Visual Studio Team Services i platformy Azure

Skonfiguruj połączenie między projektu programu VSTS i konta platformy Azure.

1. Powitania po lewej stronie, kliknij przycisk **nowy punkt końcowy usługi** > **usługi Azure Resource Manager**.
2. tooauthorize toowork programu VSTS z Twoim kontem platformy Azure, wybierz użytkownika **subskrypcji** i kliknij przycisk **OK**.

    ![Visual Studio Team Services — autoryzować Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a>Połączenie usługi Visual Studio Team Services i GitHub

Skonfiguruj połączenie między projektu programu VSTS oraz konto GitHub.

1. Powitania po lewej stronie, kliknij przycisk **nowy punkt końcowy usługi** > **GitHub**.
2. Kliknij tooauthorize toowork programu VSTS z Twoim kontem usługi GitHub **autoryzacji** i wykonaj procedurę hello w otwartym oknie hello.

    ![Visual Studio Team Services — autoryzować GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a>Łączenie programu VSTS tooyour klastra usługi kontenera Azure

kroki ostatniego Hello przed przejściem do potoku CI/CD hello są tooconfigure połączeń zewnętrznych tooyour Docker Swarm klastra na platformie Azure. 

1. Klaster Docker Swarm hello Dodawanie punktu końcowego typu **SSH**. Następnie wprowadź informacje o połączeniu SSH hello klastra Swarm (węzeł główny).

    ![Visual Studio Team Services — SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

Cała konfiguracja hello odbywa się teraz. W następnych krokach hello możesz utworzyć hello CI/CD potok, który tworzy i wdraża klaster Docker Swarm toohello aplikacji hello. 

## <a name="step-2-create-hello-build-definition"></a>Krok 2: Tworzenie definicji kompilacji hello

W tym kroku skonfigurować definicję kompilacji projektu programu VSTS i zdefiniuj hello przepływu pracy kompilacji dla obrazów kontenera

### <a name="initial-definition-setup"></a>Definicja początkowej instalacji

1. tooyour projektu Visual Studio Team Services i kliknij przycisk Połącz toocreate definicję kompilacji **kompilacji i wydania**. W hello **definicje kompilacji** kliknij **+ nowy**. 

    ![Visual Studio Team Services — nowej definicji kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. Wybierz hello **pusta procesu**.

    ![Definicja kompilacji programu Visual Studio Team Services — nowy pusty](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. Następnie kliknij przycisk hello **zmienne** karcie i Utwórz dwa nowe zmienne: **RegistryURL** i **AgentURL**. Wklej hello wartości rejestru i DNS agentów klastra.

    ![Visual Studio Team Services — Konfiguracja zmienne kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. Na powitania **definicji kompilacji** strony, otwórz hello **wyzwalaczy** i skonfiguruj hello kompilacji toouse ciągłej integracji z rozwidlenia hello hello MyShop projektu, który został utworzony w hello wymagania wstępne. Następnie wybierz opcję **partii zmian**. Upewnij się, że wybrano *docker linux* jako hello **gałęzi specyfikacji**.

    ![Visual Studio Team Services — Konfiguracja repozytorium kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. Na koniec kliknij hello **opcje** i skonfiguruj hello domyślnej agenta kolejki zbyt**Podgląd Linux hostowanych**.

    ![Visual Studio Team Services — konfiguracja agenta hosta](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a>Zdefiniuj hello przepływu pracy kompilacji
Następne kroki Hello zdefiniuj hello przepływu pracy kompilacji. Najpierw należy tooconfigure hello źródła hello kodu. toodo go, wybierz opcję **GitHub** i **repozytorium** i **gałęzi** (docker linux).

![Konfigurowanie programu Visual Studio Team Services — kodu źródłowego](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

Istnieje pięć toobuild obrazów kontener dla hello *MyShop* aplikacji. Obraz jest utworzony przy użyciu powitalne plik Dockerfile znajdujących się w folderach projektu hello:

* ProductsApi
* Serwer proxy
* RatingsApi
* RecommandationsApi
* Sklepu

Należy dwa kroki Docker dla każdego obrazu, jeden obraz powitania toobuild i jeden obraz powitania toopush hello rejestru kontenera platformy Azure. 

1. tooadd etapem hello przepływu pracy kompilacji, kliknij przycisk **+ Dodaj krok kompilacji** i wybierz **Docker**.

    ![Visual Studio Team Services — dodać kroki procesu kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. Dla każdego obrazu, należy skonfigurować jeden krok, który używa hello `docker build` polecenia.

    ![Visual Studio Team Services — Docker kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    Na powitania utworzyć operację, wybierz rejestru kontenera platformy Azure, hello **kompilacji obrazu** akcji i hello plik Dockerfile, który definiuje każdego obrazu. Zestaw hello **katalog roboczy** jako katalog główny plik Dockerfile hello, zdefiniuj hello **nazwa obrazu**i wybierz **zawierają najnowsze tagu**.
    
    Nazwa obrazu Hello ma toobe w następującym formacie: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```. Zastąp **[nazwa]** o nazwie obrazu hello:
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. Dla każdego obrazu, skonfiguruj drugi krok, który używa hello `docker push` polecenia.

    ![Visual Studio Team Services — Docker Push](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    Dla operacji wypychania hello, wybierz rejestru kontenera platformy Azure, hello **Push obrazu** akcji, wprowadź hello **nazwa obrazu** wbudowane w poprzednim kroku hello i wybierz **zawierają najnowsze Tag** .

4. Po skonfigurowaniu hello kompilacji i push kroki dla każdego z pięciu obrazów hello, Dodaj trzy kroki więcej w hello kompilacji przepływu pracy.

   ![Visual Studio Team Services — Dodaj zadania wiersza polecenia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. Zadania wiersza polecenia, które używa hello tooreplace skryptu bash *RegistryURL* wystąpienie w plik docker-compose.yml hello hello RegistryURL zmienną. 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services — plik Redaguj aktualizacji z adresem URL rejestru](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. Zadania wiersza polecenia, które używa hello tooreplace skryptu bash *AgentURL* wystąpienie w plik docker-compose.yml hello hello AgentURL zmienną.
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. Zadanie porzuca hello aktualizowana tworzenia pliku jako artefaktów kompilacji dzięki mogą być używane w hello wersji. Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.

         ![Visual Studio Team Services — Opublikuj artefaktów](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Usługi Visual Studio Team - publikowania tworzenia pliku](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. Kliknij przycisk **Zapisz & kolejka** tootest definicję kompilacji.

   ![Visual Studio Team Services — zapisywanie i kolejki](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services — nowej kolejki](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. Jeśli hello **kompilacji** jest poprawna, masz toosee ten ekran:

  ![Visual Studio Team Services — kompilacja powiodła się](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a>Krok 3: Tworzenie definicji wersji hello

Visual Studio Team Services służy za[zarządzania wersjami w środowiskach](https://www.visualstudio.com/team-services/release-management/). Można włączyć się, że aplikacja jest wdrożony na Twoje różnych środowiskach (np. dev, test produkcji wstępnej i produkcji) w sposób toomake ciągłego wdrażania. Można utworzyć środowisko, które reprezentuje klastra tryb Azure kontenera usługi Docker Swarm.

![Visual Studio Team Services — tooACS zlecenia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Początkowa wersja Instalatora

1. toocreate definicji wersji, kliknij przycisk **wersje** > **+ zlecenia**

2. tooconfigure hello artefaktu źródłowego, kliknij przycisk **artefakty** > **połączenia źródła artefaktu**. W tym miejscu łącze nowej wersji definicji toohello kompilacji zdefiniowanego w poprzednim kroku hello. Po wykonaniu tej plik docker-compose.yml hello jest dostępna w procesie zlecenia hello.

    ![Visual Studio Team Services - wersja artefaktów](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. wyzwalacz wersji hello tooconfigure, kliknij przycisk **wyzwalaczy** i wybierz **ciągłe wdrażanie**. Zestaw wyzwalacza hello na powitania tego samego źródła artefaktu. To ustawienie zapewnia, że rozpoczyna się nowej wersji, gdy hello kompilacja zostaje ukończona pomyślnie.

    ![Visual Studio Team Services — wyzwalaczy zlecenia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. zmienne wersji hello tooconfigure, kliknij przycisk **zmienne** i wybierz **+ zmiennej** toocreate trzy nowe zmienne z użyciem informacji hello rejestru hello: **docker.username**, **docker.password**, i **docker.registry**. Wklej hello wartości rejestru i DNS agentów klastra.

    ![Visual Studio Team Services — Konfiguracja repozytorium kompilacji](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > Jak pokazano na poprzednich ekranie powitania, kliknij przycisk hello **blokady** checkbox w docker.password. To ustawienie jest ważne toorestrict hello hasła.
    >

### <a name="define-hello-release-workflow"></a>Zdefiniuj hello wersji w przepływie pracy

przepływ pracy wersji Hello składa się z dwóch zadań, które można dodać.

1. Konfigurowanie zadań toosecurely kopiowania hello utworzenie pliku tooa *wdrażania* folderu na powitania Docker Swarm węzła głównego, przy użyciu połączenia SSH hello został wcześniej skonfigurowany. Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.
    
    Folder źródłowy:```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```

    ![Visual Studio Team Services - wersja punkt połączenia usługi](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. Skonfiguruj drugi tooexecute zadań toorun polecenia bash `docker` i `docker stack deploy` poleceń na powitania węzła głównego. Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services — Bash zlecenia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    polecenie Hello wykonane na wzorcu hello używa hello interfejsu wiersza polecenia Docker i hello toodo rozwiązania Docker Compose CLI hello następujące zadania:

    - Zaloguj się w rejestrze kontenera platformy Azure toohello (używa trzech zmiennych kompilacji, które są zdefiniowane w hello **zmienne** kartę)
    - Zdefiniuj hello **DOCKER_HOST** toowork zmiennej z punktu końcowego Swarm hello (: 2375)
    - Przejdź toohello *wdrażanie* folderu, który został utworzony przez hello poprzedzających zadanie kopiowania bezpiecznego i który zawiera plik docker-compose.yml hello 
    - Wykonanie `docker stack deploy` poleceń ściągnięcia nowych obrazów hello i utworzyć hello kontenerów.

    >[!IMPORTANT]
    > Jak pokazano na poprzednich ekranie powitania, pozostaw hello **zakończyć się niepowodzeniem ze strumienia STDERR** niezaznaczone pole wyboru. To ustawienie pozwala nam procesu publikacji hello toocomplete powodu zbyt`docker-compose` wyświetla komunikaty diagnostyczne, takie jak kontenery są zatrzymywanie lub usuwany na powitania błędów w danych wyjściowych. Po zaznaczeniu pola wyboru hello Visual Studio Team Services raporty błędów, które wystąpiły podczas wersji hello, nawet jeśli wszystko przebiegnie poprawnie.
    >
3. Zapisz ten nowej definicji wersji.

## <a name="step-4-test-hello-cicd-pipeline"></a>Krok 4: Testowanie hello CI/CD potoku

Teraz, po zakończeniu konfiguracji hello, jest czas tootest nowy potok CI/CD. Hello Najprostszym sposobem tootest jest tooupdate hello źródła kodu i zatwierdzania hello zmienia się w repozytorium GitHub. Kilka sekund po wypchnąć kod hello, zobaczysz nowej kompilacji uruchomionych w Visual Studio Team Services. Po pomyślnym ukończeniu nowej wersji wyzwoleniu i wdrożyć hello nowej wersji aplikacji hello na powitania klastra usługi kontenera platformy Azure.

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji na temat CI/CD z Visual Studio Team Services, zobacz hello [kompilacji programu VSTS omówienie](https://www.visualstudio.com/docs/build/overview).
* Aby uzyskać więcej informacji na temat aparatu ACS, zobacz hello [repozytorium GitHub aparat ACS](https://github.com/Azure/acs-engine).
* Aby uzyskać więcej informacji o trybie Docker Swarm, zobacz hello [Docker Swarm Omówienie trybu](https://docs.docker.com/engine/swarm/).
