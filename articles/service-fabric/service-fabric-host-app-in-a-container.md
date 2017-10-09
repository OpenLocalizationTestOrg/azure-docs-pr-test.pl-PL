---
title: "aaaDeploy aplikacji .NET w kontenerze tooAzure sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Przedstawienie sposobu toopackage aplikacji .NET w programie Visual Studio w kontenerze Docker. Ta nowa aplikacja \"kontener\" jest następnie wdrażana tooa klastra sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a>Wdrażanie aplikacji .NET w Windows tooAzure kontenera sieci szkieletowej usług

W tym samouczku przedstawiono sposób toodeploy istniejącej aplikacji ASP.NET w kontenerze systemu Windows Azure.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie projektu platformy Docker w programie Visual Studio
> * Containerize istniejącej aplikacji
> * Instalator ciągłej integracji z programu Visual Studio i VSTS

## <a name="prerequisites"></a>Wymagania wstępne

1. Zainstaluj [CE Docker dla systemu Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) , co umożliwia uruchamianie kontenerów w systemie Windows 10.
2. Zapoznaj się z hello [Szybki Start systemu Windows 10 kontenery][link-container-quickstart].
3. Pobierz hello [Fabrikam Fiber CallCenter] [ link-fabrikam-github] przykładowej aplikacji.
4. Zainstaluj [programu Azure PowerShell][link-azure-powershell-install]
5. Zainstaluj hello [rozszerzenie ciągłego dostarczania narzędzi dla programu Visual Studio 2017 r.][link-visualstudio-cd-extension]
6. Utwórz [subskrypcji platformy Azure] [ link-azure-subscription] i [konto usługi Visual Studio Team Services][link-vsts-account]. 
7. [Tworzenie klastra na platformie Azure](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a>Containerize aplikacji hello

Teraz, gdy masz [klastra sieci szkieletowej usług jest uruchomiona na platformie Azure](service-fabric-tutorial-create-cluster-azure-ps.md) są gotowe toocreate i wdrażania konteneryzowanych aplikacji. toostart uruchamiania aplikacji w kontenerze, potrzebujemy tooadd **Obsługa Docker** toohello projektu programu Visual Studio. Po dodaniu **Obsługa Docker** aplikacji toohello dwie czynności stanie. Najpierw _plik Dockerfile_ dodaniu toohello projektu. Ten nowy plik opisano hello kontener obrazu toobe skompilowany. Następnie po drugie, nowy _rozwiązania docker compose_ projekt zostanie dodany toohello rozwiązania. Witaj nowy projekt zawiera kilka rozwiązania docker compose plików. Rozwiązania docker compose pliki mogą być używane toodescribe sposób uruchamiania hello kontenera.

Więcej informacji na temat pracy z [programu Visual Studio Tools kontenera][link-visualstudio-container-tools].

>[!NOTE]
>Jeśli jest hello obrazów kontenera systemu Windows są uruchomione na komputerze po raz pierwszy, Docker CE musi rozwiń hello obrazy podstawowe dla kontenerów. obrazy Hello używane w tym samouczku są 14 GB. Przejdź dalej i uruchom następujące obrazy podstawowe polecenia terminali toopull hello hello:
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a>Dodawanie obsługi Docker

Otwórz hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] pliku w programie Visual Studio.

Kliknij prawym przyciskiem myszy hello **FabrikamFiber.Web** projektu > **Dodaj** > **Obsługa Docker**.

### <a name="add-support-for-sql"></a>Dodawanie obsługi SQL

Ta aplikacja używa SQL na powitania dostawcy danych, więc programu SQL server jest wymagane toorun aplikacji hello. Odwołuje się obraz kontenera programu SQL Server w naszym pliku docker compose.override.yml.

W programie Visual Studio Otwórz **Eksploratora rozwiązań**, Znajdź **rozwiązania docker compose**i otwórz hello pliku **docker compose.override.yml**.

Przejdź toohello `services:` węzła, Dodaj węzeł o nazwie `db:` definiuje hello wpis programu SQL Server dla hello kontenera.

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
>Można użyć dowolnego wolisz dla debugowania lokalnego programu SQL Server, tak długo, jak jest dostępny z hosta. Jednak **localdb** nie obsługuje `container -> host` komunikacji.

>[!WARNING]
>Programem SQL Server w kontenerze nie obsługuje trwałych danych. Po zatrzymaniu kontenera hello wymazaniu danych. Nie używaj tej konfiguracji w środowisku produkcyjnym.

Przejdź toohello `fabrikamfiber.web:` węzeł i Dodaj węzeł podrzędny o nazwie `depends_on:`. Gwarantuje to, że hello `db` usługi (kontenera hello programu SQL Server), który rozpoczyna się przed naszej aplikacji sieci web (fabrikamfiber.web).

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a>Aktualizacja konfiguracji sieci web hello

Po powrocie do hello **FabrikamFiber.Web** projektu, ciąg połączenia hello aktualizacji w hello **web.config** pliku toohello toopoint programu SQL Server w kontenerze hello.

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
>Jeśli toouse inny serwer SQL podczas kompilowania zlecenia tworzenie aplikacji sieci web, należy dodać innego pliku web.release.config tooyour parametrów połączenia.

### <a name="test-your-container"></a>Twoje kontener testu

Naciśnij klawisz **F5** toorun i debugowania aplikacji hello w kontenerze sieci.

Krawędź otwiera stronę zdefiniowanych uruchamiania aplikacji przy użyciu adresu IP hello kontenera hello na powitania wewnętrzny translatora adresów Sieciowych sieci (zazwyczaj 172.x.x.x). Zobacz toolearn więcej informacji o debugowaniu aplikacji w kontenerach przy użyciu programu Visual Studio 2017 r. [w tym artykule][link-debug-container].

![przykład firma fabrikam w kontenerze][image-web-preview]

kontener Hello jest teraz gotowy toobe wbudowany i opakowane w aplikacji sieci szkieletowej usług. Po utworzeniu obrazu kontenera hello oparty na tym komputerze, możesz wypchnąć go tooany kontenera rejestru i rozwiń tooany toorun hosta.

## <a name="get-hello-application-ready-for-hello-cloud"></a>Przygotowanie aplikacji hello hello chmury

gotowy do uruchomienia w sieci szkieletowej usług na platformie Azure aplikacji hello tooget, potrzebujemy toocomplete należy wykonać dwie czynności:

1. Udostępnianie portu hello, gdy chcemy tooreach stanie toobe naszej aplikacji sieci web w klastrze usługi sieć szkieletowa hello.
2. Podaj produkcji gotowy bazy danych SQL dla naszej aplikacji.

### <a name="expose-hello-port-for-hello-app"></a>Udostępnianie portów hello aplikacji hello
Możemy skonfigurowano klaster sieci szkieletowej usług Hello ma port *80* otwarty domyślnie hello modułu równoważenia obciążenia Azure, która równoważy przychodzącego ruchu toohello klastra. Uwidaczniamy naszych kontenera na tym porcie za pośrednictwem naszego plik docker-compose.yml.

W programie Visual Studio Otwórz **Eksploratora rozwiązań**, Znajdź **rozwiązania docker compose**i otwórz hello pliku **docker compose.override.yml**.

Modyfikowanie hello `fabrikamfiber.web:` węzła, Dodaj węzeł podrzędny o nazwie `ports:`.

Dodaj wpis ciąg `- "80:80"`.

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a>Użyj produkcyjną bazę danych SQL
Podczas uruchamiania w środowisku produkcyjnym, potrzebujemy nasze dane utrwalone w naszej bazie danych. Nie ma obecnie żadnych danych trwałych tooguarantee sposób w kontenerze, dlatego nie można zapisać danych produkcyjnych w programie SQL Server w kontenerze.

Zaleca się korzystanie z bazy danych SQL Azure. tooset zapasowej i uruchamiania zarządzanego serwera SQL na platformie Azure, odwiedź hello [Quickstarts bazy danych SQL Azure] [ link-azure-sql] artykułu.

>[!NOTE]
>Pamiętaj toochange hello połączenie ciągów toohello programu SQL server w hello **web.release.config** pliku w hello **FabrikamFiber.Web** projektu.
>
>Ta aplikacja powiedzie się, jeśli baza danych SQL jest osiągalny. Można wybrać toogo wyprzedzeniem i wdrażanie aplikacji hello bez serwera SQL.

## <a name="deploy-with-visual-studio-team-services"></a>Rozmieszczanie za pomocą programu Visual Studio Team Services

tooset wdrożenia przy użyciu programu Visual Studio Team Services, potrzebne tooinstall hello [rozszerzenie ciągłego dostarczania narzędzi dla programu Visual Studio 2017][link-visualstudio-cd-extension]. To rozszerzenie umożliwia łatwe toodeploy tooAzure przez skonfigurowanie Visual Studio Team Services i korzystaj z klastra usługi sieć szkieletowa tooyour wdrożonych aplikacji.

tooget pracę, kod musi być hostowany w kontroli źródła. Witaj pozostałej części tej sekcji założono **git** jest używany.

### <a name="set-up-a-vsts-repo"></a>Konfigurowanie repozytorium VSTS
W prawym dolnym rogu hello programu Visual Studio, kliknij **Dodaj formant tooSource** > **Git** (lub użyć jednego z tych opcji).

![Naciśnij przycisk kontroli źródła hello][image-source-control]

W hello _Team Explorer_ okienka, naciśnij klawisz **Publikuj repozytorium Git**.

Wybierz nazwę repozytorium VSTS i naciśnij klawisz **repozytorium**.

![Publikowanie tooVSTS repozytorium][image-publish-repo]

Teraz, gdy kod jest zsynchronizowany z repozytorium źródłowe VSTS, można skonfigurować ciągłej integracji i ciągłego dostarczania.

### <a name="setup-continuous-delivery"></a>Instalator ciągłego dostarczania

W _Eksploratora rozwiązań_, kliknij prawym przyciskiem myszy hello **rozwiązania** > **skonfigurować ciągłego dostarczania**.

Wybierz hello subskrypcji platformy Azure.

Ustaw **typ hosta** za**klastra sieci szkieletowej usług**.

Ustaw **hosta docelowego** klastra sieci szkieletowej usług toohello utworzony w poprzedniej sekcji hello.

Wybierz **rejestru kontenera** toopublish Twojego kontenera do.

>[!TIP]
>Użyj hello **Edytuj** toocreate przycisk rejestru kontenera.

Naciśnij przycisk **OK**.

![Instalator usługi sieci szkieletowej ciągłej integracji][image-setup-ci]
   
   Po zakończeniu konfiguracji hello z kontenera jest wdrożony tooService sieci szkieletowej. Zawsze, gdy wypychanie aktualizacji toohello repozytorium jest wykonywany nowej kompilacji i wydania.
   
   >[!NOTE]
   >Kompilowanie hello kontener obrazów potrwać około 15 minut.
   >klaster sieci szkieletowej usług toohello pierwszego wdrożenia Hello powoduje, że hello podstawowej systemu Windows Server Core kontener obrazów toobe pobrane. Pobieranie Hello przyjmuje toocomplete dodatkowe 5 – 10 minut.

Przeglądaj toohello Fabrikam biurem aplikacji przy użyciu adresu url hello klastra: na przykład *http://mycluster.westeurope.cloudapp.azure.com*

Teraz, gdy masz konteneryzowanych i wdrożyć rozwiązanie firmy Fabrikam biurem hello, możesz otworzyć hello [portalu Azure] [ link-azure-portal] i aplikacja hello w sieci szkieletowej usług. Aplikacja hello tootry, otwórz przeglądarkę sieci web i przejdź toohello adres URL klastra usługi sieć szkieletowa usług.

## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie projektu platformy Docker w programie Visual Studio
> * Containerize istniejącej aplikacji
> * Instalator ciągłej integracji z programu Visual Studio i VSTS

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
