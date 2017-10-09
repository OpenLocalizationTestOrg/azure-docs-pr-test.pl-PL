---
title: "aaaDeploy aplikacja sieć szkieletowa usług Azure o ciągłej integracji (Team Services) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset ciągłej integracji i wdrażania aplikacji sieci szkieletowej usług za pomocą programu Visual Studio Team Services.  Wdrażanie klastra usługi sieć szkieletowa tooa aplikacji na platformie Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a>Wdróż aplikację z klastra usługi sieć szkieletowa tooa CI/CD
W tym samouczku jest częścią trzy serii i opisano sposób tooset ciągłej integracji i wdrażania aplikacji sieci szkieletowej usług Azure przy użyciu programu Visual Studio Team Services.  Istniejącej aplikacji usługi sieć szkieletowa jest potrzebna, aplikacja hello utworzona w [tworzenia aplikacji .NET](service-fabric-tutorial-create-dotnet-app.md) służy jako przykład.

W trzech części hello serii, możesz dowiedzieć się, jak:

> [!div class="checklist"]
> * Dodaj projekt tooyour kontroli źródła
> * Utwórz definicję kompilacji w Team Services
> * Tworzenie definicji wersji w usłudze Team Services
> * Automatyczne wdrażanie i uaktualnianie aplikacji

W tym samouczku dowiesz się, jak:
> [!div class="checklist"]
> * [Tworzenie aplikacji sieci szkieletowej usług .NET](service-fabric-tutorial-create-dotnet-app.md)
> * [Wdrażanie klastra zdalnego tooa aplikacji hello](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * Konfigurowanie elementu konfiguracji/CD za pomocą programu Visual Studio Team Services

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka:
- Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Zainstaluj program Visual Studio 2017](https://www.visualstudio.com/) i zainstaluj hello **Azure programowanie** i **ASP.NET i sieć web development** obciążeń.
- [Zainstaluj hello zestawu SDK sieci szkieletowej usług](service-fabric-get-started.md)
- Tworzenie aplikacji usługi Service Fabric, na przykład przez [tego samouczka](service-fabric-tutorial-create-dotnet-app.md). 
- Tworzenie klastra sieci szkieletowej usług systemu Windows na platformie Azure, na przykład przez [tego samouczka](service-fabric-tutorial-create-cluster-azure-ps.md)
- Utwórz [konta usługi Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).

## <a name="download-hello-voting-sample-application"></a>Pobierz hello głosowania przykładowej aplikacji
Jeśli nie zbudować hello głosowania przykładowej aplikacji [część jednego z tego samouczka serii](service-fabric-tutorial-create-dotnet-app.md), można go pobrać. W oknie polecenie Uruchom hello następujące polecenia tooclone hello przykładowej aplikacji repozytorium tooyour komputera lokalnego.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>Przygotowanie profilu publikowania
Znasz [utworzona aplikacja](service-fabric-tutorial-create-dotnet-app.md) i mieć [wdrożone tooAzure aplikacji hello](service-fabric-tutorial-deploy-app-to-party-cluster.md), wszystko jest gotowe tooset się ciągłej integracji.  Najpierw przygotować profilu publikowania w aplikacji do użycia przez proces wdrażania hello wykonywanego Team Services.  profil publikowania Hello powinien być skonfigurowany tootarget hello klastra, który wcześniej utworzony.  Uruchom program Visual Studio i otworzyć istniejący projekt aplikacji sieci szkieletowej usług.  W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy aplikacji hello i wybierz **publikowania...** .

Wybierz profil docelowy w ramach Twojej aplikacji toouse projektu przepływu pracy ciągłej integracji, na przykład w chmurze.  Określ punktu końcowego połączenia klastra hello.  Sprawdź hello **hello uaktualniania aplikacji** pole wyboru, aby aplikacja uaktualnia dla każdego wdrożenia w Team Services.  Kliknij przycisk hello **Zapisz** hyperlink toosave hello ustawienia toohello profil publikowania, a następnie kliknij przycisk **anulować** hello tooclose — okno dialogowe.  

![Profil wypychania][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a>Udostępnianie programu Visual Studio rozwiązania tooa nowego zespołu usług repozytorium Git
Udostępnianie plików źródłowych aplikacji tooa projektu zespołowego Team Services, można wygenerować kompilacji.  

Utwórz nowe lokalne repozytorium Git dla projektu, zaznaczając **Dodaj formant tooSource** -> **Git** na pasku stanu hello hello prawym dolnym rogu programu Visual Studio. 

W hello **Push** wyświetlić w **Team Explorer**, wybierz pozycję hello **Publikuj repozytorium Git** przycisku w obszarze **Push tooVisual Studio Team Services**.

![Wypychanie repozytorium Git][push-git-repo]

Sprawdź pocztę i wybierz konto w hello **zespołu usług domenowych** listy rozwijanej. Wprowadź nazwę repozytorium i wybierz **Publikuj repozytorium**.

![Wypychanie repozytorium Git][publish-code]

Opublikowanie repozytorium hello powoduje utworzenie nowego projektu zespołowego na koncie z hello takie same nazwy jako repozytorium lokalne powitania. repozytorium hello toocreate w istniejącego projektu zespołowego, kliknij przycisk **zaawansowane** dalej zbyt**repozytorium** nazwę, a następnie wybierz projekt zespołowy. Kodu można wyświetlać w sieci web hello, wybierając **jest widoczny w sieci web hello**.

## <a name="configure-continuous-delivery-with-vsts"></a>Konfigurowanie ciągłego dostarczania przy użyciu programu VSTS
Definicja kompilacji Team Services zawiera opis przepływu pracy, który składa się z zestaw kroków kompilacji, które są wykonywane sekwencyjnie. Utwórz definicję kompilacji, który, który tworzy pakiet aplikacji sieci szkieletowej usług i innych artefaktów, klaster sieci szkieletowej usług tooa toodeploy. Dowiedz się więcej o [definicje kompilacji Team Services](https://www.visualstudio.com/docs/build/define/create). 

Definicja wersji Team Services opisano przepływ pracy, który wdraża klaster tooa pakietu aplikacji. Razem hello definicję kompilacji i wersji definicji wykonaj całego przepływu pracy hello począwszy od źródła tooending plików przy użyciu aplikacji uruchomionych w klastrze. Dowiedz się więcej na temat usługi Team Services [wersji definicji](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).

### <a name="create-a-build-definition"></a>Tworzenie definicji kompilacji
Otwórz przeglądarkę sieci web i przejdź tooyour nowego projektu zespołowego na: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting. 

Wybierz hello **kompilacji i wydania** karcie następnie **kompilacje**, następnie **+ nową definicję**.  W **wybierz szablon**, wybierz pozycję hello **aplikacji sieci szkieletowej usług Azure** szablon i kliknij przycisk **Zastosuj**. 

![Wybierz szablon kompilacji][select-build-template] 

głosowania aplikacji Hello zawiera projekt .NET Core, a więc Dodaj zadanie, które przywraca hello zależności. W hello **zadania** widok, wybierz opcję **+ Dodaj zadanie** w lewy dolny hello. Wyszukaj zadania wiersza polecenia hello toofind "Wiersza polecenia", a następnie kliknij przycisk **Dodaj**. 

![Dodaj zadanie][add-task] 

W hello nowe zadanie, wpisz "Uruchom dotnet.exe" w **Nazwa wyświetlana**, "dotnet.exe" w **narzędzie**, a "Przywróć" w **argumenty**. 

![Nowe zadanie][new-task] 

W hello **wyzwalaczy** wyświetlić, kliknij przycisk hello **włączyć tego wyzwalacza** przełącznika w obszarze **ciągłej integracji**. 

Wybierz **Zapisz & kolejka** i wprowadzili "VS2017 hostowanej" hello **kolejki agenta**. Wybierz **kolejki** toomanually uruchomić kompilacji.  Opisano również wyzwalacze wypychania lub zaewidencjonowania.

toocheck postęp kompilacji, przełącznik toohello **kompilacje** kartę.  Po upewnieniu się, czy hello kompilacji została wykonana pomyślnie, należy zdefiniować definicji wersji, która wdraża klaster tooa aplikacji. 

### <a name="create-a-release-definition"></a>Utwórz definicję zlecenia  

Wybierz hello **kompilacji i wydania** karcie następnie **wersje**, następnie **+ nową definicję**.  W **Tworzenie wersji definicji**, wybierz pozycję hello **wdrażania usługi Azure Service Fabric** szablon z listy hello i kliknij przycisk **dalej**.  Wybierz hello **kompilacji** źródło, sprawdź hello **ciągłe wdrażanie** i kliknij **Utwórz**. 

W hello **środowisk** wyświetlić, kliknij przycisk **Dodaj** toohello prawo **połączenia klastra**.  Określ nazwę połączenia "mysftestcluster" punktu końcowego klastra "tcp://mysftestcluster.westus.cloudapp.azure.com:19000" hello Azure Active Directory i poświadczeń certyfikatu dla klastra hello. Dla poświadczeń usługi Azure Active Directory, należy zdefiniować hello poświadczenia mają toouse tooconnect toohello klastra w hello **Username** i **hasło** pola. Do uwierzytelniania opartego na certyfikatach, zdefiniuj hello Base64 kodowanie pliku z certyfikatem klienta hello w hello **certyfikatu klienta** pola.  Zobacz hello pomocy w oknie podręcznym o to pole, aby uzyskać informacje na temat tooget, że wartość.  Jeśli certyfikat jest chroniony hasłem, należy określić hasło hello w hello **hasło** pola.  Kliknij przycisk **zapisać** toosave hello wersji definicji.

![Dodaj połączenie klastra][add-cluster-connection] 

Kliknij przycisk **Uruchom agenta**, a następnie wybierz pozycję **hostowane VS2017** dla **kolejki wdrożenia**. Kliknij przycisk **zapisać** toosave hello wersji definicji.

![Uruchom agenta][run-on-agent]

Wybierz **+ wersji** -> **Tworzenie wersji** -> **Utwórz** toomanually utworzyć wersję.  Sprawdź, czy Zakończono pomyślnie wdrażanie hello i aplikacja hello jest uruchomiona w klastrze hello.  Otwórz przeglądarkę sieci web i przejdź zbyt[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Należy pamiętać, wersja aplikacji hello, w tym przykładzie jest "1.0.0.20170616.3". 

## <a name="commit-and-push-changes-trigger-a-release"></a>Zatwierdź i Wypchnij zmiany, wyzwalanie wydania
tooverify, który hello potoku ciągłej integracji działa sprawdzając w pewnych zmian w kodzie tooTeam usług.    

Podczas pisania kodu zmiany automatycznie są śledzone przez program Visual Studio. Zatwierdź zmiany tooyour lokalnego repozytorium Git, wybierając hello oczekujące zmiany ikonę (![Oczekujące][pending]) z hello paska stanu w prawym dolnym rogu hello.

Na powitania **zmiany** wyświetlić w programie Team Explorer, Dodaj komunikat opisujący aktualizacji i zatwierdzić zmiany.

![Zatwierdź wszystko][changes]

Ikona paska stanu nieopublikowane zmiany wybierz hello (![nieopublikowane zmiany][unpublished-changes]) lub hello widoku synchronizacji w programie Team Explorer. Wybierz **Push** tooupdate kodu w Team Services/TFS.

![Wypchnij zmiany][push]

Wypychanie tooTeam zmiany hello usługi automatycznie wyzwalaczy kompilacji.  Po pomyślnym zakończeniu hello definicji kompilacji, zlecenia zostanie utworzona automatycznie i rozpoczyna uaktualnianie aplikacji hello na powitania klastra.

toocheck postęp kompilacji, przełącznik toohello **kompilacje** karcie **Team Explorer** w programie Visual Studio.  Po upewnieniu się, czy hello kompilacji została wykonana pomyślnie, należy zdefiniować definicji wersji, która wdraża klaster tooa aplikacji.

Sprawdź, czy Zakończono pomyślnie wdrażanie hello i aplikacja hello jest uruchomiona w klastrze hello.  Otwórz przeglądarkę sieci web i przejdź zbyt[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Należy pamiętać, wersja aplikacji hello, w tym przykładzie jest "1.0.0.20170815.3".

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a>Aplikacja hello aktualizacji
Zmiany kodu w aplikacji hello.  Zapisz i zatwierdź zmiany hello, po hello poprzednie kroki.

Gdy aktualizacja hello aplikacja hello zacznie, możesz obserwować postęp uaktualnienia hello w narzędziu Service Fabric Explorer:

![Service Fabric Explorer][sfx2]

Uaktualnianie aplikacji Hello może potrwać kilka minut. Po zakończeniu uaktualniania hello hello zostanie uruchomiona aplikacja hello następnej wersji.  W tym przykładzie "1.0.0.20170815.4".

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>Następne kroki
W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Dodaj projekt tooyour kontroli źródła
> * Tworzenie definicji kompilacji
> * Utwórz definicję zlecenia
> * Automatyczne wdrażanie i uaktualnianie aplikacji

Po wdrożeniu aplikacji i skonfigurować ciągłej integracji, wypróbować hello następujące czynności:
- [Uaktualnianie aplikacji](service-fabric-application-upgrade.md)
- [Testowanie aplikacji](service-fabric-testability-overview.md) 
- [Monitorowanie i diagnozowanie](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png