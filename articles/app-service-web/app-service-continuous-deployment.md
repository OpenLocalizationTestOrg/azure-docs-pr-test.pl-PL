---
title: "aaaContinuous tooAzure wdrożenia usługi App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable tooAzure ciągłego wdrażania usługi aplikacji."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a>Ciągłe wdrażanie tooAzure usługi aplikacji
W tym samouczku przedstawiono sposób tooconfigure przepływu pracy ciągłego wdrażania dla użytkownika [usłudze Azure App Service] aplikacji. Usługi aplikacji integracji z BitBucket, GitHub, i [programu Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) umożliwia ciągłego przepływ pracy wdrożenia, którym Azure ściąga hello najnowsze aktualizacje z projektu opublikowane tooone tych usług. Ciągłe wdrażanie to doskonałe rozwiązanie dla projektów, w których ma miejsce częste współtworzenie wielu treści.

toofind się jak tooconfigure ciągłe wdrażanie ręcznie z repozytorium chmury nie są wyświetlane według hello portalu Azure (takich jak [GitLab](https://gitlab.com/)), zobacz [Konfigurowanie ciągłego wdrażania przy użyciu ręczne](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="overview"></a>Włącz ciągłe wdrażanie
tooenable ciągłe wdrażanie

1. Publikuj repozytorium zawartości toohello aplikacji, która będzie służyć do ciągłego wdrażania.  
    Aby uzyskać więcej informacji na temat publikowania usług toothese projektu, zobacz [Tworzenie repozytorium (GitHub)], [Tworzenie repozytorium (BitBucket)], i [wprowadzenie do programu VSTS].
2. W bloku menu aplikacji w hello [portalu Azure], kliknij przycisk **wdrażania aplikacji > Opcje wdrażania**. Kliknij przycisk **wybierz źródło**, a następnie wybierz pozycję hello źródło wdrożenia.  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > tooconfigure konto programu VSTS dla wdrożenia usługi App Service można znaleźć pod adresem to [samouczek](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).
   > 
   > 
3. Hello pełny przepływ pracy autoryzacji.
4. W hello **źródło wdrożenia** bloku, wybierz projekt hello i toodeploy z gałęzi. Gdy skończysz, kliknij przycisk **OK**.
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > Podczas włączania ciągłego wdrażania za pomocą usługi GitHub lub BitBucket zostaną wyświetlone zarówno projekty publiczne, jak i prywatne.
   > 
   > 
   
    Usługi aplikacji tworzy skojarzenie z repozytorium wybranego hello, w przypadku plików hello hello określonej gałęzi i obsługuje klonowania repozytorium na aplikację usługi aplikacji. Podczas konfigurowania programu VSTS ciągłego wdrażania od hello portalu Azure hello integracji używa usługi aplikacji hello [aparat wdrażania Kudu](https://github.com/projectkudu/kudu/wiki), który już automatyzuje zadania kompilacji i wdrażania związane z każdego `git push`. Nie trzeba tooseparately skonfigurowano ciągłe wdrażanie w VSTS. Po zakończeniu tego procesu, hello **opcje wdrażania** bloku aplikacji będą wyświetlane aktywne wdrożenie wskazującą wdrażania zakończyła się pomyślnie.
5. Aplikacja hello tooverify zostanie pomyślnie wdrożona, kliknij przycisk hello **adres URL** u góry bloku aplikacji hello w portalu Azure hello hello.
6. tooverify ciągłe wdrażanie informacji związanych z repozytorium hello wybranym push repozytorium toohello zmiany. Aplikację należy zaktualizować zmiany hello tooreflect wkrótce po zakończeniu hello wypychania toohello repozytorium. Możesz sprawdzić, czy ma pobierane w aktualizacji hello w hello **opcje wdrażania** bloku aplikacji.

## <a name="VSsolution"></a>Ciągłe wdrażanie za pomocą rozwiązania Visual Studio
Wypychanie tooAzure rozwiązania Visual Studio usługi aplikacji jest równie proste jak naciśnięcie plik index.html proste. proces wdrażania usługi aplikacji Hello usprawnia wszystkich szczegółów hello, takich jak przywracanie zależności NuGet i tworzenia plików binarnych aplikacji hello. Można stosować najlepsze rozwiązania kontroli źródła hello obsługi kodu tylko w repozytorium Git i umożliwić zajmie się hello rest wdrożenia usługi App Service.

Witaj kroki do wypychania tooApp rozwiązania programu Visual Studio, są usługi hello takie same jak hello [poprzedniej sekcji](#overview), pod warunkiem, że możesz skonfigurować rozwiązanie i repozytorium w następujący sposób:

* Użyj hello Visual Studio źródła formantu opcja toogenerate `.gitignore` plików, takich jak hello obraz poniżej lub ręcznie Dodaj `.gitignore` pliku w katalogu głównym repozytorium, z zawartości toothis podobne [próbki .gitignore](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* Dodaj hello całego rozwiązania katalogu drzewa tooyour repozytorium z hello plik .sln w katalogu głównym repozytorium hello.

Po Konfigurowanie repozytorium, zgodnie z opisem i skonfigurowany aplikacji na platformie Azure do ciągłego publikowania z jednego z hello online repozytoria Git, mogą tworzyć aplikacji ASP.NET lokalnie w programie Visual Studio i stale po prostu przez wdrażanie kodu Wypychanie zmiany tooyour online repozytorium Git.

## <a name="disableCD"></a>Wyłączanie ciągłego wdrażania
toodisable ciągłe wdrażanie

1. W bloku menu aplikacji w hello [portalu Azure], kliknij przycisk **wdrażania aplikacji > Opcje wdrażania**. Następnie kliknij przycisk **rozłączenia** w hello **opcje wdrażania** bloku.
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. Po odebraniu **tak** toohello komunikat potwierdzający, możesz wrócić bloku tooyour aplikacji i kliknij przycisk **wdrażania aplikacji > Opcje wdrażania** Jeśli chcesz tooset się publikowanie z innego źródła.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Jak tooinvestigate typowe problemy związane z ciągłe wdrażanie](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [Jak toouse programu PowerShell dla usługi Azure]
* [Jak toouse hello narzędzia wiersza polecenia platformy Azure dla komputerów Mac i Linux]
* [Dokumentacja usługi Git]
* [Projekt Kudu](https://github.com/projectkudu/kudu/wiki)
* [Użyj Azure tooautomatically Generowanie CI/CD potoku toodeploy ASP.NET 4 aplikacji](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

[usłudze Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[portalu Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Jak toouse programu PowerShell dla usługi Azure]: /powershell/azureps-cmdlets-docs
[Jak toouse hello narzędzia wiersza polecenia platformy Azure dla komputerów Mac i Linux]:../cli-install-nodejs.md
[Dokumentacja usługi Git]: http://git-scm.com/documentation

[Tworzenie repozytorium (GitHub)]: https://help.github.com/articles/create-a-repo
[Tworzenie repozytorium (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[wprowadzenie do programu VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
