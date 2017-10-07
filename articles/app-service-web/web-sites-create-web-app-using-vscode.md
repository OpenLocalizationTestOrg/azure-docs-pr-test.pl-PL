---
title: aaaCreate aplikacji sieci web platformy ASP.NET Core w programie Visual Studio Code
description: "W tym samouczku przedstawiono, jak toocreate platformy ASP.NET Core sieci web przy użyciu programu Visual Studio Code aplikacji."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Tworzenie aplikacji sieci web platformy ASP.NET Core w programie Visual Studio Code
## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak toocreate platformy ASP.NET Core sieci web przy użyciu aplikacji [programu Visual Studio (kod VS)](http://code.visualstudio.com//Docs/whyvscode) i wdróż je za[usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md). 

> [!NOTE]
> Chociaż ten artykuł dotyczy aplikacji tooweb, ma również zastosowanie tooAPI aplikacji i aplikacji mobilnych. 
> 
> 

Platformy ASP.NET Core to znaczące one programu ASP.NET. Platformy ASP.NET Core to nowa open source i międzyplatformowa struktura do tworzenia aplikacji sieci web opartych na chmurze nowoczesnych przy użyciu platformy .NET. Aby uzyskać więcej informacji, zobacz [tooASP.NET wprowadzenie Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html). Informacje o aplikacji sieci web w usłudze Azure App Service, zobacz [Omówienie aplikacji sieci Web](app-service-web-overview.md).

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>Wymagania wstępne
* Zainstaluj [kodzie VS](http://code.visualstudio.com/Docs/setup).
* Zainstaluj usługę Git — można ją zainstalować, korzystając z jednej z tych lokalizacji: [Chocolatey](https://chocolatey.org/packages/git) lub [git scm.com](http://git-scm.com/downloads). W przypadku nowych tooGit wybierz [git scm.com](http://git-scm.com/downloads) i wybierz opcję hello zbyt**Git użycia z wiersza polecenia systemu Windows hello**. Po zainstalowaniu programu Git, należy również tooset hello Git użytkownika nazwę i adres e-mail jest wymagane później w samouczku hello (przeprowadzania zatwierdzenia z kodu VS).  

## <a name="install-aspnet-core"></a>Instalowanie platformy ASP.NET Core
Platformy ASP.NET Core jest gotowa stosu .NET do tworzenia nowoczesnych chmury i aplikacji sieci web, które można uruchamiać na OS X, Linux i Windows. Go został utworzony z hello tła się tooprovide platforma programistyczna zoptymalizowany dla aplikacji, które są albo chmury wdrożonej toohello lub lokalnie. Składa się z moduły składniki przy minimalnym obciążeniu, aby zachować elastyczność podczas konstruowania rozwiązań.

W tym samouczku jest zaprojektowana tooget rozpoczęciem tworzenia aplikacji hello najnowsze wersje rozwoju platformy ASP.NET Core. Witaj, postępując zgodnie z instrukcjami są określone tooWindows. Aby uzyskać instrukcje instalacji na OS X, Linux i Windows, zobacz [wprowadzenie do platformy ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started). 


> [!NOTE]
> Aby uzyskać szczegółowe instrukcje dotyczące instalacji, OS X, Linux i Windows, temacie [instalowanie platformy ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx). 
> 
> 

## <a name="create-hello-web-app"></a>Tworzenie aplikacji sieci web hello
W tej sekcji przedstawiono, jak tooscaffold nowej aplikacji platformy ASP.NET sieci web za pomocą narzędzia interfejsu wiersza polecenia .NET hello aplikacji. 

1. Wprowadź poniżej hello na powitania wiersza polecenia toocreate hello projektu folderu i szkieletu hello aplikacji.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![platformy CLI - generatora platformy ASP.NET Core DotNet](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. toorestore hello niezbędne pakiety NuGet, uruchom następujące polecenie hello:
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a>Uruchamianie aplikacji sieci web hello lokalnie
Teraz, utworzono aplikację sieci web hello i pobrać wszystkie pakiety NuGet hello aplikacji hello hello aplikacji sieci web można uruchomić lokalnie.

1. Uruchamianie aplikacji hello (hello `dotnet run` polecenia zostanie tworzenie aplikacji hello, gdy jest nieaktualny):
    ```terminal
    dotnet run
    ```
2. Otwórz przeglądarkę i przejdź toohello następującego adresu URL.
   
    **http://localhost: 5000**
   
    następujący zostanie wyświetlona strona domyślna Hello hello aplikacji sieci web.
   
    ![Aplikacji lokalnej sieci web w przeglądarce](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. Zamknij przeglądarkę. W hello **okno polecenia**, naciśnij klawisz **klawisze Ctrl + C** tooshut aplikacji hello i zamknij hello **okno polecenia**. 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Tworzenie aplikacji sieci web w hello portalu Azure
Witaj następujące kroki przeprowadzi Cię przez proces tworzenia aplikacji sieci web w hello portalu Azure.

1. Zaloguj się za toohello [Azure Portal](https://portal.azure.com).
2. Kliknij przycisk **nowy** na powitania lewym górnym rogu hello portalu.
3. Kliknij przycisk **Web Apps > sieci Web aplikacji**.
   
    ![Azure nowej aplikacji sieci web](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. Wprowadź wartość dla **nazwa**, takich jak **SampleWebAppDemo**. Należy pamiętać, że ta nazwa musi toobe unikatowy i hello portalu będzie wymuszać, który podczas próby tooenter hello nazwa. Dlatego w przypadku wybrania wprowadź inną wartość, konieczne będzie toosubstitute, że wartość dla każdego wystąpienia **SampleWebAppDemo** widoczny w tym samouczku. 
5. Wybierz istniejący **planu usługi App Service** lub Utwórz nową. Jeśli tworzysz nowy plan, wybierz hello warstwa cenowa, lokalizacji i inne opcje. Aby uzyskać więcej informacji na temat planów usługi aplikacji, zobacz artykuł hello [szczegółowe omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
   
    ![Azure nowego bloku aplikacja sieci web](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. Kliknij przycisk **Utwórz**.
   
    ![bloku aplikacja sieci Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a>Włączanie publikowania Git dla hello nowej aplikacji sieci web
Git to system kontroli wersji rozproszonej służącego toodeploy aplikacji sieci web w usłudze Azure App Service. Będą przechowywane kod powitania dla aplikacji sieci web w lokalnym repozytorium Git, a w przypadku wdrażania tooAzure Twojego kodu wypychając tooa zdalnego repozytorium.   

1. Zaloguj się do hello [Azure Portal](https://portal.azure.com).
2. Kliknij pozycję **Browse (Przeglądaj)**.
3. Kliknij przycisk **aplikacje sieci Web** tooview listę aplikacji sieci web hello skojarzone z subskrypcją platformy Azure.
4. Wybierz aplikację sieci web hello utworzony w tym samouczku.
5. W bloku aplikacja sieci web powitania kliknij **ustawienia** > **ciągłe wdrażanie**. 
   
    ![Host aplikacji sieci web platformy Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. Kliknij przycisk **wybierz źródło > lokalne repozytorium Git**.
7. Kliknij przycisk **OK**.
   
    ![Azure lokalnego repozytorium Git](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. Jeśli nie ma poświadczeń wdrożenia do publikowania aplikacji sieci web lub innych aplikacji usługi app Service, skonfiguruj je teraz:
   
   * Kliknij przycisk **ustawienia** > **poświadczenia wdrażania**. Witaj **ustawić poświadczenia wdrażania** zostanie wyświetlony blok.
   * Utwórz nazwę użytkownika i hasło.  To hasło będzie potrzebne później podczas konfigurowania Git.
   * Kliknij pozycję **Zapisz**.
9. W bloku aplikacja sieci web, kliknij przycisk **Ustawienia > właściwości**. adres URL Hello hello zdalnego repozytorium Git wdrażanego będzie wyświetlany w obszarze toois **adres URL GIT**.
10. Kopiuj hello **adres URL GIT** wartość do wykorzystania później w samouczku hello.
    
    ![Adres URL Git platformy Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a>Publikowanie tooAzure aplikacji sieci web usługi aplikacji
W tej sekcji utworzysz lokalne repozytorium Git i push z tego repozytorium tooAzure toodeploy tooAzure aplikacji sieci web.

1. W kodzie VS wybierz hello **Git** opcji hello lewym pasku nawigacyjnym.
   
    ![Ikona Git w kodzie VS](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. Wybierz **repozytorium git zainicjować** toomake się, że obszar roboczy jest pod kontrolą źródła git. 
   
    ![Inicjowanie Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Otwórz hello okno polecenia i zmień katalog toohello katalogów aplikacji sieci web. Następnie wprowadź następujące polecenie hello:
   
        git config core.autocrlf false
   
    To polecenie uniemożliwia problemu o tekstu, w którym są związane z zakończenia CRLF i LF zakończenia.
4. W kodzie VS Dodaj komunikat, zatwierdzania, a następnie kliknij przycisk hello **zatwierdzania wszystkich** Ikona znacznika wyboru.
   
    ![Git Zatwierdź wszystko](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Po zakończeniu przetwarzania Git zobaczysz, że nie ma żadnych plików wymienionych w oknie Git hello w obszarze **zmiany**. 
   
    ![Git żadne zmiany](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. Zmień wstecz toohello okno polecenia gdzie wiersza polecenia hello wskazuje katalog toohello, gdzie znajduje się aplikacja sieci web.
7. Utwórz zdalnego odwołania do wypychania aplikacji sieci web tooyour aktualizacje za pomocą hello URL Git (kończących ".git"), które wcześniej zostały skopiowane.
   
        git remote add azure [URL for remote repository]
8. Skonfiguruj poświadczenia Git toosave lokalnie, aby zostaną one automatycznie dołączany tooyour wypychania polecenia wygenerowane z kodu programu VS.
   
        git config credential.helper store
9. Wypchnij tooAzure Twoje zmiany, wprowadzając następujące polecenie hello. Po tym tooAzure wypychania początkowej będzie stanie toodo wypychania hello wszystkich poleceń z kodu programu VS. 
   
        git push -u azure master
   
    Zostanie wyświetlony monit o hasło hello utworzone wcześniej w usłudze Azure. **Uwaga: Hasła nie będą widoczne.**
   
    dane wyjściowe Hello hello powyżej polecenie kończy się z komunikatem, że wdrożenie zakończy się powodzeniem.
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> Jeśli wprowadzisz zmiany tooyour aplikacji, można ponownie opublikować bezpośrednio w kodzie VS za pomocą wbudowanej funkcji Git hello wybierając hello **zatwierdzić wszystkie** opcji następuje hello **Push** opcji. Można znaleźć hello **Push** opcja dostępna w hello menu rozwijanego dalej toohello **zatwierdzić wszystkie** i **Odśwież** przycisków.
> 
> 

Jeśli potrzebujesz toocollaborate w projekcie, należy rozważyć wypychanie tooGitHub Between wypychanie tooAzure.

## <a name="run-hello-app-in-azure"></a>Uruchamianie aplikacji hello na platformie Azure
Teraz, możesz wdrożyć aplikację sieci web umożliwia uruchamianie aplikacji hello podczas hostowana na platformie Azure. 

Można to zrobić na dwa sposoby:

* Otwórz przeglądarkę i wprowadź następujący hello nazwę aplikacji sieci web.   
  
        http://SampleWebAppDemo.azurewebsites.net
* W hello portalu Azure Znajdź hello bloku aplikacja sieci web dla aplikacji sieci web i kliknij przycisk **Przeglądaj** tooview aplikacji 
* w domyślnej przeglądarce.

![Aplikacja sieci web platformy Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>Podsumowanie
W tym samouczku można przedstawiono sposób toocreate aplikacji sieci web w kodzie VS i wdróż je tooAzure. Aby uzyskać więcej informacji o kodzie VS, zobacz artykuł hello, [Dlaczego Visual Studio Code?](https://code.visualstudio.com/Docs/) Informacje o aplikacjach sieci web usługi aplikacji, zobacz [Omówienie aplikacji sieci Web](app-service-web-overview.md). 

