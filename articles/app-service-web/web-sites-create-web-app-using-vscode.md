---
title: Tworzenie aplikacji sieci web platformy ASP.NET Core w programie Visual Studio Code
description: "W tym samouczku przedstawiono sposób tworzenia aplikacji sieci web platformy ASP.NET Core za pomocą programu Visual Studio Code."
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
ms.openlocfilehash: 46e3852dc84265de41bb358f482dec06608e7efa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Tworzenie aplikacji sieci web platformy ASP.NET Core w programie Visual Studio Code
## <a name="overview"></a>Omówienie
W tym samouczku przedstawiono sposób tworzenia platformy ASP.NET Core sieci web app przy użyciu [programu Visual Studio (kod VS)](http://code.visualstudio.com//Docs/whyvscode) i wdrożyć ją [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md). 

> [!NOTE]
> Mimo że ten artykuł dotyczy aplikacji sieci Web, ma również zastosowanie do aplikacji interfejsu API i aplikacji mobilnych. 
> 
> 

Platformy ASP.NET Core to znaczące one programu ASP.NET. Platformy ASP.NET Core to nowa open source i międzyplatformowa struktura do tworzenia aplikacji sieci web opartych na chmurze nowoczesnych przy użyciu platformy .NET. Aby uzyskać więcej informacji, zobacz [wprowadzenie do platformy ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html). Informacje o aplikacji sieci web w usłudze Azure App Service, zobacz [Omówienie aplikacji sieci Web](app-service-web-overview.md).

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>Wymagania wstępne
* Zainstaluj [kodzie VS](http://code.visualstudio.com/Docs/setup).
* Zainstaluj usługę Git — można ją zainstalować, korzystając z jednej z tych lokalizacji: [Chocolatey](https://chocolatey.org/packages/git) lub [git scm.com](http://git-scm.com/downloads). Jeśli jesteś nowym użytkownikiem Git, wybierz [git scm.com](http://git-scm.com/downloads) i wybierz opcję **Git użycia z wiersza polecenia systemu Windows**. Po zainstalowaniu programu Git, również należy ustawić nazwę użytkownika Git i poczty e-mail, ponieważ jest on niezbędny w dalszej części samouczka (przeprowadzania zatwierdzenia z kodu VS).  

## <a name="install-aspnet-core"></a>Instalowanie platformy ASP.NET Core
Platformy ASP.NET Core jest gotowa stosu .NET do tworzenia nowoczesnych chmury i aplikacji sieci web, które można uruchamiać na OS X, Linux i Windows. Go został utworzony od podstaw w zapewnia platforma programistyczna zoptymalizowany dla aplikacji, które są wdrożone w chmurze lub lokalnie. Składa się z moduły składniki przy minimalnym obciążeniu, aby zachować elastyczność podczas konstruowania rozwiązań.

Ten samouczek jest przeznaczony do Rozpoczęcie tworzenia aplikacji z najnowszej wersji rozwoju platformy ASP.NET Core. Poniższe instrukcje dotyczą systemu Windows. Aby uzyskać instrukcje instalacji na OS X, Linux i Windows, zobacz [wprowadzenie do platformy ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started). 


> [!NOTE]
> Aby uzyskać szczegółowe instrukcje dotyczące instalacji, OS X, Linux i Windows, temacie [instalowanie platformy ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx). 
> 
> 

## <a name="create-the-web-app"></a>Tworzenie aplikacji sieci Web
W tej sekcji przedstawiono sposób tworzenia szkieletu nowej aplikacji ASP.NET aplikacji sieci web za pomocą narzędzia interfejsu wiersza polecenia platformy .NET. 

1. Wprowadź w wierszu polecenia, aby utworzyć folder projektu i utworzyć szkielet aplikacji.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![platformy CLI - generatora platformy ASP.NET Core DotNet](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. Aby przywrócić wymaganych pakietów NuGet, uruchom następujące polecenie:
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a>Lokalne uruchamianie aplikacji sieci web
Teraz, utworzono aplikację sieci web i pobrać wszystkie pakiety NuGet aplikacji dla aplikacji sieci web można uruchomić lokalnie.

1. Uruchom aplikację ( `dotnet run` polecenia będzie kompilowania aplikacji, gdy jest nieaktualny):
    ```terminal
    dotnet run
    ```
2. Otwórz przeglądarkę i przejdź do następującego adresu URL.
   
    **http://localhost: 5000**
   
    Następujący zostanie wyświetlona strona domyślnej aplikacji sieci web.
   
    ![Aplikacji lokalnej sieci web w przeglądarce](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. Zamknij przeglądarkę. W **okno polecenia**, naciśnij klawisz **klawisze Ctrl + C** zamknięcia aplikacji i zamknąć **okno polecenia**. 

## <a name="create-a-web-app-in-the-azure-portal"></a>Tworzenie aplikacji sieci web w portalu Azure
Poniższe kroki przeprowadzi Cię przez proces tworzenia aplikacji sieci web w portalu Azure.

1. Zaloguj się do [Azure Portal](https://portal.azure.com).
2. Kliknij przycisk **nowy** u góry po lewej części portalu.
3. Kliknij przycisk **Web Apps > sieci Web aplikacji**.
   
    ![Azure nowej aplikacji sieci web](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. Wprowadź wartość dla **nazwa**, takich jak **SampleWebAppDemo**. Należy pamiętać, że ta nazwa musi być unikatowa i portalu będzie wymuszać który, podczas próby wprowadź nazwę. Dlatego w przypadku wybrania wprowadź inną wartość, należy zastąpić tę wartość dla każdego wystąpienia **SampleWebAppDemo** widoczny w tym samouczku. 
5. Wybierz istniejący **planu usługi App Service** lub Utwórz nową. Jeśli tworzysz nowy plan, wybierz warstwę cenową, lokalizacji i innych opcji. Aby uzyskać więcej informacji na temat planów usługi App Service, zobacz artykuł, [szczegółowe omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
   
    ![Azure nowego bloku aplikacja sieci web](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. Kliknij przycisk **Utwórz**.
   
    ![bloku aplikacja sieci Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a>Włączanie publikowania Git dla nowej aplikacji sieci web
Git to system kontroli wersji rozproszonej, który służy do wdrażania aplikacji sieci web w usłudze Azure App Service. Utworzony kod dla aplikacji sieci Web zostanie zapisany w lokalnym repozytorium Git i wdrożony na platformie Azure przez wypchnięcie do repozytorium zdalnego.   

1. Zaloguj się do [portalu Azure](https://portal.azure.com).
2. Kliknij pozycję **Browse (Przeglądaj)**.
3. Kliknij przycisk **aplikacje sieci Web** Aby wyświetlić listę aplikacji sieci web skojarzony z subskrypcją platformy Azure.
4. Wybierz utworzony w tym samouczku aplikacji sieci web.
5. W bloku aplikacja sieci web, kliknij przycisk **ustawienia** > **ciągłe wdrażanie**. 
   
    ![Host aplikacji sieci web platformy Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. Kliknij przycisk **wybierz źródło > lokalne repozytorium Git**.
7. Kliknij przycisk **OK**.
   
    ![Azure lokalnego repozytorium Git](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. Jeśli nie ma poświadczeń wdrożenia do publikowania aplikacji sieci web lub innych aplikacji usługi app Service, skonfiguruj je teraz:
   
   * Kliknij przycisk **ustawienia** > **poświadczenia wdrażania**. **Ustawić poświadczenia wdrażania** zostanie wyświetlony blok.
   * Utwórz nazwę użytkownika i hasło.  To hasło będzie potrzebne później podczas konfigurowania Git.
   * Kliknij pozycję **Zapisz**.
9. W bloku aplikacja sieci web, kliknij przycisk **Ustawienia > właściwości**. Adres URL zdalnego repozytorium Git, który będzie można wdrożyć do jest wyświetlany w obszarze **adres URL GIT**.
10. Kopiuj **adres URL GIT** wartość do wykorzystania później w samouczku.
    
    ![Adres URL Git platformy Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a>Publikowanie aplikacji sieci web w usłudze Azure App Service
W tej sekcji utworzysz lokalne repozytorium Git i wypychania z tego repozytorium na platformie Azure, aby wdrożyć aplikację sieci web na platformie Azure.

1. W kodzie VS wybierz **Git** opcji na pasku nawigacyjnym po lewej stronie.
   
    ![Ikona Git w kodzie VS](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. Wybierz **repozytorium git zainicjować** się upewnić, że obszar roboczy jest pod kontrolą źródła git. 
   
    ![Inicjowanie Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Otwórz okno polecenia i przejdź do katalogu aplikacji sieci web. Następnie wprowadź następujące polecenie:
   
        git config core.autocrlf false
   
    To polecenie uniemożliwia problemu o tekstu, w którym są związane z zakończenia CRLF i LF zakończenia.
4. W kodzie VS Dodaj komunikat, zatwierdzania, a następnie kliknij przycisk **zatwierdzania wszystkich** Ikona znacznika wyboru.
   
    ![Git Zatwierdź wszystko](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Po zakończeniu przetwarzania Git zobaczysz, że nie ma żadnych plików wymienionych w oknie Git **zmiany**. 
   
    ![Git żadne zmiany](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. Zmień okno polecenia gdzie wiersza polecenia wskazuje katalog, gdzie znajduje się aplikacja sieci web.
7. Utwórz zdalnego odwołania do wypychania aktualizacji do aplikacji sieci web za pomocą URL Git (kończących ".git"), które wcześniej zostały skopiowane.
   
        git remote add azure [URL for remote repository]
8. Skonfiguruj Git lokalnie zapisywanie poświadczeń, dzięki czemu będzie można automatycznie dołączane do poleceń wypychania wygenerowane z kodu programu VS.
   
        git config credential.helper store
9. Wypchnij zmiany na platformę Azure, wprowadzając następujące polecenie. Po tej początkowej wypychanych na platformie Azure będzie można wykonać polecenia wypychania za kodzie VS. 
   
        git push -u azure master
   
    Zostanie wyświetlony monit o podanie hasła utworzonego wcześniej w usłudze Azure. **Uwaga: Hasła nie będą widoczne.**
   
    Dane wyjściowe z powyższego polecenia kończy się z komunikatem, że wdrożenie zakończy się powodzeniem.
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> Jeśli wprowadzisz zmiany do aplikacji, można ponownie opublikować bezpośrednio w kodzie VS za pomocą wbudowanej funkcji Git, wybierając **zatwierdzić wszystkie** opcji następuje **Push** opcji. Można znaleźć **Push** opcji dostępnych w menu rozwijanym obok pozycji **zatwierdzić wszystkie** i **Odśwież** przycisków.
> 
> 

Jeśli potrzebujesz współpracować nad projektem, należy rozważyć wypychania w witrynie GitHub Between Wypychanie do platformy Azure.

## <a name="run-the-app-in-azure"></a>Uruchom aplikację na platformie Azure
Teraz, możesz wdrożyć aplikację sieci web umożliwia uruchamianie aplikacji podczas hostowana na platformie Azure. 

Można to zrobić na dwa sposoby:

* Otwórz przeglądarkę i wprowadź nazwę aplikacji sieci web w następujący sposób.   
  
        http://SampleWebAppDemo.azurewebsites.net
* W portalu Azure Znajdź bloku aplikacja sieci web dla aplikacji sieci web, a następnie kliknij przycisk **Przeglądaj** Aby wyświetlić aplikację 
* w domyślnej przeglądarce.

![Aplikacja sieci web platformy Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>Podsumowanie
W tym samouczku przedstawiono sposób tworzenia aplikacji sieci web w kodzie VS i wdrożyć go na platformie Azure. Aby uzyskać więcej informacji o kodzie VS, zobacz artykuł, [Dlaczego Visual Studio Code?](https://code.visualstudio.com/Docs/) Informacje o aplikacjach sieci web usługi aplikacji, zobacz [Omówienie aplikacji sieci Web](app-service-web-overview.md). 

