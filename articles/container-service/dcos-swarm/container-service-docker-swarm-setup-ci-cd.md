---
title: "aaaCI/CD z usługą kontenera Azure i Swarm | Dokumentacja firmy Microsoft"
description: "Użyj usługi kontenera platformy Azure z toodeliver stale aplikacji .NET Core wielu kontenera Docker Swarm, rejestru kontenera Azure i Visual Studio Team Services"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, kontenerów, Micro-services, Swarm, Azure, programu Visual Studio Team Services, opracowywania oprogramowania"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a>Pełna CI/CD toodeploy potoku aplikacji usługi kontenera w usłudze kontenera platformy Azure przy użyciu rozwiązania Docker Swarm przy użyciu programu Visual Studio Team Services

Jeden z hello największych wyzwań po opracowywanie nowoczesnych aplikacji w chmurze hello jest możliwe toodeliver te aplikacje stale. W tym artykule Dowiedz się, jak zbudować tooimplement pełnej ciągłej integracji i wdrażania (CI/CD) potoku Docker Swarm, rejestru kontenera Azure i Visual Studio Team Services za pomocą usługi kontenera platformy Azure i zarządzania zleceniami.

Ten artykuł jest oparty na prostej aplikacji, dostępnych na [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), rozwinięte z platformy ASP.NET Core. Aplikacja Hello składa się z czterech różnych usług: trzy sieci web, interfejsów API i frontonu sieci web co:

![MyShop przykładowej aplikacji](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

cel Hello jest toodeliver tej aplikacji stale w klastrze Docker Swarm, za pomocą programu Visual Studio Team Services. następujące Hello rysunek szczegóły tego potoku ciągłego dostarczania:

![MyShop przykładowej aplikacji](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

Poniżej przedstawiono krótki opis kroków hello:

1. Zmiany kodu są repozytorium kodu źródłowego zatwierdzone toohello (tutaj GitHub) 
2. GitHub uaktywnia kompilację w Visual Studio Team Services 
3. Visual Studio Team Services pobiera najnowsza wersja źródła hello hello i tworzy wszystkie obrazy hello tworzące aplikacji hello 
4. Visual Studio Team Services wypchnięcia każdego obrazu tooa Docker rejestru utworzone za pomocą usługi Azure kontenera rejestru hello 
5. Visual Studio Team Services wyzwala nową wersją 
6. Niektóre polecenia przy użyciu protokołu SSH w węźle głównym klastra usługi kontenera platformy Azure hello uruchamia Hello zlecenia 
7. Rozwiązanie docker Swarm hello klastra ściąga hello najnowszą wersją hello obrazów 
8. nową wersję aplikacji hello Hello wdrażania przy użyciu rozwiązania Docker Compose 

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem tego samouczka potrzebne hello toocomplete następujące zadania:

- [Utworzenie klastra Swarm usługi Azure Container Service](container-service-deployment.md)
- [Połącz z klastrem Swarm hello usługi kontenera platformy Azure](../container-service-connect.md)
- [Tworzenie rejestru kontenera platformy Azure](../../container-registry/container-registry-get-started-portal.md)
- [Utworzony projekt konta i zespołu Visual Studio Team Services](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Rozwidlania tooyour repozytorium GitHub hello konto GitHub](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Należy również maszyny Ubuntu (14.04 i 16.04) z Docker zainstalowane. Ten komputer jest używany przez Visual Studio Team Services podczas hello kompilacji i wydania procesów. Jednym ze sposobów toocreate ten komputer jest dostępna w hello obraz powitania toouse [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/). 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Krok 1: Skonfiguruj konto usługi Visual Studio Team Services 

W tej sekcji należy skonfigurować konto w Visual Studio Team Services.

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a>Konfigurowanie agenta kompilacji programu Visual Studio Team Services Linux

obrazy usługi Docker toocreate i wypychania tworzenia tych obrazów w rejestrze kontenera platformy Azure z Visual Studio Team Services, należy tooregister agenta systemu Linux. Masz następujące opcje instalacji:

* [Wdrażanie agenta w systemie Linux](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [Użyj agenta programu VSTS hello toorun Docker](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a>Zainstaluj rozszerzenie VSTS integracji Docker hello

Firma Microsoft udostępnia usługi VSTS rozszerzenia toowork z rozwiązaniem Docker z kompilacji i wydania procesów. To rozszerzenie jest dostępna w hello [Marketplace programu VSTS](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker). Kliknij przycisk **zainstalować** tooadd tego konta usługi VSTS tooyour rozszerzenia:

![Zainstaluj hello Integracja z rozwiązaniem Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

Zostanie wyświetlona prośba konta usługi VSTS tooyour tooconnect przy użyciu poświadczeń. 

### <a name="connect-visual-studio-team-services-and-github"></a>Połączenie usługi Visual Studio Team Services i GitHub

Skonfiguruj połączenie między projektu programu VSTS oraz konto GitHub.

1. W projekcie programu Visual Studio Team Services, kliknij przycisk hello **ustawienia** ikonę w hello narzędzi i wybierz **usług**.

    ![Visual Studio Team Services — połączenie zewnętrzne](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. Powitania po lewej stronie, kliknij przycisk **nowy punkt końcowy usługi** > **GitHub**.

    ![Visual Studio Team Services — usługi GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. Kliknij tooauthorize toowork programu VSTS z Twoim kontem usługi GitHub **autoryzacji** i wykonaj procedurę hello w otwartym oknie hello.

    ![Visual Studio Team Services — autoryzować GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a>Połącz rejestru programu VSTS tooyour kontenera platformy Azure i klastrem usługi kontenera platformy Azure

ostatnie etapy Hello przed przejściem do potoku CI/CD hello są tooconfigure połączeń zewnętrznych tooyour kontenera rejestru i klastrem Docker Swarm w usłudze Azure. 

1. W hello **usług** ustawień projektu Visual Studio Team Services, Dodaj punkt końcowy usługi typu **Docker rejestru**. 

2. W menu podręcznym hello, który zostanie otwarty wprowadź adres URL hello i poświadczenia hello rejestru kontenera platformy Azure.

    ![Visual Studio Team Services — Docker rejestru](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. Klaster Docker Swarm hello Dodawanie punktu końcowego typu **SSH**. Następnie wprowadź informacje o połączeniu SSH hello klastra Swarm.

    ![Visual Studio Team Services — SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

Cała konfiguracja hello odbywa się teraz. W następnych krokach hello możesz utworzyć hello CI/CD potok, który tworzy i wdraża klaster Docker Swarm toohello aplikacji hello. 

## <a name="step-2-create-hello-build-definition"></a>Krok 2: Tworzenie definicji kompilacji hello

W tym kroku konfiguracji definitionfor kompilacji projektu programu VSTS i zdefiniuj hello przepływu pracy kompilacji dla obrazów kontenera

### <a name="initial-definition-setup"></a>Definicja początkowej instalacji

1. tooyour projektu Visual Studio Team Services i kliknij przycisk Połącz toocreate definicję kompilacji **kompilacji i wydania**. 

2. W hello **definicje kompilacji** kliknij **+ nowy**. Wybierz hello **pusty** szablonu.

    ![Visual Studio Team Services — nowej definicji kompilacji](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. Skonfiguruj nową kompilację hello ze źródłem repozytorium GitHub wyboru **ciągłej integracji**i wybierz hello kolejki agenta rejestracji agenta systemu Linux. Kliknij przycisk **Utwórz** toocreate hello definicji kompilacji.

    ![Visual Studio Team Services — Tworzenie definicji kompilacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. Na powitania **definicji kompilacji** strony, należy najpierw otworzyć hello **repozytorium** i skonfiguruj hello kompilacji toouse hello rozwidlenia hello MyShop projektu, który został utworzony w hello wymagania wstępne. Upewnij się, że wybrano *acs docs* jako hello **gałąź domyślną**.

    ![Visual Studio Team Services — Konfiguracja repozytorium kompilacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. Na powitania **wyzwalaczy** skonfiguruj toobe kompilacji hello wyzwalane po każdym zatwierdzeniu. Wybierz **ciągłej integracji** i **partii zmian**.

    ![Visual Studio Team Services — Konfiguracja wyzwalacza kompilacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a>Zdefiniuj hello przepływu pracy kompilacji
Następne kroki Hello zdefiniuj hello przepływu pracy kompilacji. Istnieje pięć toobuild obrazów kontener dla hello *MyShop* aplikacji. Obraz jest utworzony przy użyciu powitalne plik Dockerfile znajdujących się w folderach projektu hello:

* ProductsApi
* Serwer proxy
* RatingsApi
* RecommandationsApi
* Sklepu

Należy tooadd dwa kroki Docker dla każdego obrazu, jeden obraz powitania toobuild i jeden obraz powitania toopush hello rejestru kontenera platformy Azure. 

1. tooadd etapem hello przepływu pracy kompilacji, kliknij przycisk **+ Dodaj krok kompilacji** i wybierz **Docker**.

    ![Visual Studio Team Services — dodać kroki procesu kompilacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. Dla każdego obrazu, należy skonfigurować jeden krok, który używa hello `docker build` polecenia.

    ![Visual Studio Team Services — Docker kompilacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    Na powitania utworzyć operację, wybierz rejestru kontenera platformy Azure, hello **kompilacji obrazu** akcji i hello plik Dockerfile, który definiuje każdego obrazu. Zestaw hello **kontekst kompilacji** hello plik Dockerfile katalogu głównego, a także definiują hello **nazwa obrazu**. 
    
    Jak pokazano na powitania ekranu poprzedzającym, zaczynać się nazwa obrazu hello hello URI rejestru kontenera platformy Azure. (Możesz również użyć kompilacji zmiennej tooparameterize hello tag obrazu hello, takich jak identyfikator kompilacji hello w tym przykładzie).

3. Dla każdego obrazu, skonfiguruj drugi krok, który używa hello `docker push` polecenia.

    ![Visual Studio Team Services — Docker Push](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    Dla operacji wypychania hello, wybierz rejestru kontenera platformy Azure, hello **Push obrazu** akcji, a następnie wprowadź hello **nazwa obrazu** wbudowane w poprzednim kroku hello.

4. Po skonfigurowaniu hello kompilacji i push kroki dla każdego z pięciu obrazów hello, dodaj dwa kroki więcej w hello kompilacji przepływu pracy.

    a. Zadania wiersza polecenia, które używa hello tooreplace skryptu bash *BuildNumber* wystąpienie w pliku docker-compose.yml hello hello bieżącej kompilacji identyfikatora. Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.

    ![Visual Studio Team Services — plik Redaguj aktualizacji](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    b. Zadanie porzuca hello aktualizowana tworzenia pliku jako artefaktów kompilacji dzięki mogą być używane w hello wersji. Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.

    ![Usługi Visual Studio Team - publikowania tworzenia pliku](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. Kliknij przycisk **zapisać** i nazwij definicję kompilacji.

## <a name="step-3-create-hello-release-definition"></a>Krok 3: Tworzenie definicji wersji hello

Visual Studio Team Services służy za[zarządzania wersjami w środowiskach](https://www.visualstudio.com/team-services/release-management/). Można włączyć się, że aplikacja jest wdrożony na Twoje różnych środowiskach (np. dev, test produkcji wstępnej i produkcji) w sposób toomake ciągłego wdrażania. Można utworzyć nowego środowiska reprezentujący klastra Azure kontenera usługi Docker Swarm.

![Visual Studio Team Services — tooACS zlecenia](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Początkowa wersja Instalatora

1. toocreate definicji wersji, kliknij przycisk **wersje** > **+ zlecenia**

2. tooconfigure hello artefaktu źródłowego, kliknij przycisk **artefakty** > **połączenia źródła artefaktu**. W tym miejscu łącze nowej wersji definicji toohello kompilacji zdefiniowanego w poprzednim kroku hello. Dzięki temu plik docker-compose.yml hello jest dostępna w hello procesu publikacji.

    ![Visual Studio Team Services - wersja artefaktów](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. wyzwalacz wersji hello tooconfigure, kliknij przycisk **wyzwalaczy** i wybierz **ciągłe wdrażanie**. Zestaw wyzwalacza hello na powitania tego samego źródła artefaktu. To ustawienie zapewni, jak hello kompilacja zostaje ukończona pomyślnie rozpoczyna się nowej wersji.

    ![Visual Studio Team Services — wyzwalaczy zlecenia](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a>Zdefiniuj hello wersji w przepływie pracy

przepływ pracy wersji Hello składa się z dwóch zadań, które można dodać.

1. Konfigurowanie zadań toosecurely kopiowania hello utworzenie pliku tooa *wdrażania* folderu na powitania Docker Swarm węzła głównego, przy użyciu połączenia SSH hello został wcześniej skonfigurowany. Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.

    ![Visual Studio Team Services - wersja punkt połączenia usługi](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. Skonfiguruj drugi tooexecute zadań toorun polecenia bash `docker` i `docker-compose` poleceń na powitania węzła głównego. Zobacz powitania po ekranie, aby uzyskać szczegółowe informacje.

    ![Visual Studio Team Services — Bash zlecenia](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    polecenie Hello wykonane na powitania hello wzorca użycia interfejsu wiersza polecenia Docker i hello toodo rozwiązania Docker Compose CLI hello następujące zadania:

    - Logowania toohello kontenera platformy Azure rejestru (używa trzech variab'les kompilacji, które są zdefiniowane w hello **zmienne** kartę)
    - Zdefiniuj hello **DOCKER_HOST** toowork zmiennej z punktu końcowego Swarm hello (: 2375)
    - Przejdź toohello *wdrażanie* folderu, który został utworzony przez hello poprzedzających zadanie kopiowania bezpiecznego i który zawiera plik docker-compose.yml hello 
    - Wykonanie `docker-compose` poleceń ściągnięcia nowych obrazów hello, Zatrzymaj usługi hello, Usuń usługi hello i utworzyć hello kontenerów.

    >[!IMPORTANT]
    > Jak pokazano na powitania ekranu poprzedzającym, pozostaw hello **zakończyć się niepowodzeniem ze strumienia STDERR** niezaznaczone pole wyboru. To ustawienie ważne, ponieważ `docker-compose` wyświetla komunikaty diagnostyczne, takie jak kontenery są zatrzymywanie lub usuwany na powitania błędów w danych wyjściowych. Po zaznaczeniu pola wyboru hello Visual Studio Team Services raporty błędów, które wystąpiły podczas wersji hello, nawet jeśli wszystko przebiegnie poprawnie.
    >
3. Zapisz ten nowej definicji wersji.


>[!NOTE]
>Tego wdrożenia zawiera pewien Przestój, ponieważ jesteśmy zatrzymywanie usług starego hello i systemem hello nową. Jego jest to możliwe tooavoid wykonując wdrożenie zielony niebieski.
>

## <a name="step-4-test-hello-cicd-pipeline"></a>Krok 4. Test hello CI/CD potoku

Teraz, po zakończeniu konfiguracji hello, jest czas tootest nowy potok CI/CD. Hello Najprostszym sposobem tootest jest tooupdate hello źródła kodu i zatwierdzania hello zmienia się w repozytorium GitHub. Kilka sekund po wypchnąć kod hello, zobaczysz nowej kompilacji uruchomionych w Visual Studio Team Services. Po pomyślnym ukończeniu nowej wersji zostanie wywołane i wdroży hello nowej wersji aplikacji hello na powitania klastra usługi kontenera platformy Azure.

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji na temat CI/CD z Visual Studio Team Services, zobacz hello [kompilacji programu VSTS omówienie](https://www.visualstudio.com/docs/build/overview).
