---
title: "aaaDeploy zadań Webjob przy użyciu programu Visual Studio"
description: "Dowiedz się, jak toodeploy tooAzure zadań Webjob Azure Web Apps App Service przy użyciu programu Visual Studio."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a>Wdrażanie zadań WebJob za pomocą programu Visual Studio
## <a name="overview"></a>Omówienie
W tym temacie wyjaśniono, jak toouse Visual Studio toodeploy aplikacji konsoli projektu aplikacji sieci web tooa w [usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) jako [zadań WebJob Azure](http://go.microsoft.com/fwlink/?LinkId=390226). Aby dowiedzieć się jak hello toodeploy zadań Webjob przy użyciu [Azure Portal](https://portal.azure.com), zobacz [zadania w tle uruchom z zadań Webjob](web-sites-create-web-jobs.md).

Gdy program Visual Studio wdroży projekt aplikacji konsoli włączone zadań Webjob, wykonuje dwie czynności:

* Pliki środowiska uruchomieniowego kopie toohello odpowiedni folder w aplikacji sieci web hello (*App_Data/zadania/ciągłego* dla ciągłe zadania Webjob, *App_Data/zadania/wyzwalane* dla zadań Webjob zaplanowanych, jak i na żądanie).
* Konfiguruje [zadania harmonogramu Azure](#scheduler) dla zadań Webjob, które są zaplanowane toorun w określonym czasie. (To nie potrzebne do ciągłe zadania Webjob.)

Projekt z obsługą zadań Webjob ma powitania po tooit dodanych elementów:

* Witaj [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) pakietu NuGet.
* A [zadania webjob publikowania settings.json](#publishsettings) plik zawierający ustawienia wdrażania i harmonogramu. 

![Diagram przedstawiający, co jest dodawana tooa aplikacji konsoli tooenable wdrożenia jako zadanie WebJob](./media/websites-dotnet-deploy-webjobs/convert.png)

Można dodać te tooan elementów istniejący projekt aplikacji konsoli lub użyj szablonu toocreate nowy projekt aplikacji konsoli włączone zadań Webjob. 

Wdróż projekt jako zadanie WebJob samodzielnie lub połączyć ją tooa projektu sieci web tak, aby automatycznie wdraża przy każdym wdrożeniem hello projektu sieci web. projekty toolink programu Visual Studio zawiera nazwę hello hello włączone zadań Webjob projektu w [list.json webjob](#webjobslist) plik w projekcie sieci web hello.

![Diagram przedstawiający projektu zadania WebJob łączenie tooweb projektu](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a>Wymagania wstępne
Funkcje wdrażania zadania Webjob są dostępne w programie Visual Studio, po zainstalowaniu hello Azure SDK dla platformy .NET:

* [Zestaw Azure SDK dla platformy .NET (Visual Studio)](https://azure.microsoft.com/downloads/).

## <a id="convert"></a>Włącz wdrożenie zadań Webjob dla istniejący projekt aplikacji konsoli
Dostępne są dwie opcje:

* [Włącz automatyczne wdrażanie projektu sieci web](#convertlink).
  
    Skonfiguruj istniejący projekt aplikacji konsoli, aby go automatycznie wdraża jako zadanie WebJob podczas wdrażania projektu sieci web. Użyj tej opcji, jeśli chcesz toorun WebJob w hello tej samej aplikacji sieci web, w którym można uruchomić hello związane z aplikacji sieci web.
* [Włącz wdrożenie bez projektu sieci web](#convertnolink).
  
    Należy skonfigurować samodzielnie, istniejące toodeploy projekt aplikacji konsoli jako zadanie WebJob z żadnego projektu sieci web tooa łącza. Ta opcja ma toorun zadania WebJob w aplikacji sieci web, z żadnej aplikacji sieci web w aplikacji sieci web hello. Toodo może być to w celu tooscale stanie toobe zasobami zadania WebJob, niezależnie od zasobów aplikacji sieci web.

### <a id="convertlink"></a>Włącz automatyczne wdrażanie zadań Webjob z projektu sieci web
1. Kliknij prawym przyciskiem myszy projekt sieci web hello w **Eksploratora rozwiązań**, a następnie kliknij przycisk **Dodaj** > **istniejący projekt jako zadanie WebJob Azure**.
   
    ![Istniejący projekt jako zadanie WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    Witaj [dodać zadania WebJob Azure](#configure) zostanie wyświetlone okno dialogowe.
2. W hello **Nazwa projektu** listy rozwijanej, tooadd projekt aplikacji konsoli wybierz hello jako zadanie WebJob.
   
    ![Wybieranie projektu w oknie dialogowym Dodawanie zadania WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. Zakończenie hello [dodać zadania WebJob Azure](#configure) okna dialogowego, a następnie kliknij przycisk **OK**. 

### <a id="convertnolink"></a>Włącz wdrożenie zadań Webjob bez projektu sieci web
1. Kliknij prawym przyciskiem myszy projekt aplikacji konsoli hello w **Eksploratora rozwiązań**, a następnie kliknij przycisk **Publikuj jako zadanie WebJob platformy Azure...** . 
   
    ![Publikuj jako zadanie WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    Witaj [dodać zadania WebJob Azure](#configure) zostanie wyświetlone okno dialogowe z hello projekt wybrany w hello **Nazwa projektu** pole.
2. Zakończenie hello [dodać zadania WebJob Azure](#configure) , a następnie kliknij przycisk **OK**.
   
   Witaj **publikowanie w sieci Web** zostanie wyświetlony Kreator.  Jeśli nie chcesz od razu toopublish, zamknij kreatora hello. Hello ustawień, które zostały wprowadzone są zapisywane dla należy zbyt[wdrażanie projektu hello](#deploy).

## <a id="create"></a>Utwórz nowy projekt z obsługą zadań Webjob
toocreate nowy projekt z obsługą zadań Webjob, można użyć hello konsoli projektu szablonu i włączyć zadania Webjob wdrożenia aplikacji zgodnie z objaśnieniem w [hello poprzedniej sekcji](#convert). Alternatywnie można użyć szablonu nowy projekt zadania Webjob hello:

* [Szablon hello zadań Webjob nowy projekt dla niezależnych zadania WebJob](#createnolink)
  
    Tworzenie projektu i skonfiguruj go toodeploy przez samego siebie jako zadanie WebJob z żadnego projektu sieci web tooa łącza. Ta opcja ma toorun zadania WebJob w aplikacji sieci web, z żadnej aplikacji sieci web w aplikacji sieci web hello. Toodo może być to w celu tooscale stanie toobe zasobami zadania WebJob, niezależnie od zasobów aplikacji sieci web.
* [Szablon hello zadań Webjob nowego projektu dla projektu sieci web połączonej tooa zadania WebJob](#createlink)
  
    Utwórz projekt, który jest skonfigurowany toodeploy automatycznie jako zadanie WebJob, gdy projekt sieci web w hello wdrożonej tego samego rozwiązania. Użyj tej opcji, jeśli chcesz toorun WebJob w hello tej samej aplikacji sieci web, w którym można uruchomić hello związane z aplikacji sieci web.

> [!NOTE]
> Szablon nowego projektu zadania Webjob Hello automatycznie instaluje pakiety NuGet i zawiera kod w *Program.cs* dla hello [zestaw SDK zadań Webjob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs). Jeśli nie chcesz hello toouse zestaw SDK zadań Webjob, usunąć ani zmienić hello `host.RunAndBlock` instrukcji w *Program.cs*.
> 
> 

### <a id="createnolink"></a>Szablon hello zadań Webjob nowy projekt dla niezależnych zadania WebJob
1. Kliknij przycisk **pliku** > **nowy projekt**, a następnie w hello **nowy projekt** kliknij okno dialogowe **chmury**  >   **Zadanie WebJob platformy Azure (.NET Framework)**.
   
    ![Okno dialogowe nowego projektu przedstawiający szablonu zadania WebJob](./media/websites-dotnet-deploy-webjobs/np.png)
2. Postępuj zgodnie ze wskazówkami hello przedstawiona wcześniej zbyt[upewnij hello projekt aplikacji konsoli niezależne projektu zadania Webjob](#convertnolink).

### <a id="createlink"></a>Szablon hello zadań Webjob nowego projektu dla projektu sieci web połączonej tooa zadania WebJob
1. Kliknij prawym przyciskiem myszy projekt sieci web hello w **Eksploratora rozwiązań**, a następnie kliknij przycisk **Dodaj** > **nowy projekt zadania WebJob Azure**.
   
    ![Nowy wpis menu projektu zadania WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    Witaj [dodać zadania WebJob Azure](#configure) zostanie wyświetlone okno dialogowe.
2. Zakończenie hello [dodać zadania WebJob Azure](#configure) , a następnie kliknij przycisk **OK**.

## <a id="configure"></a>okno dialogowe Dodawanie zadania WebJob Azure Hello
Witaj **dodać zadania WebJob Azure** oknie dialogowym można wprowadzić nazwę zadania WebJob hello i uruchom tryb WebJob. 

![Dodawanie zadania WebJob Azure w oknie dialogowym](./media/websites-dotnet-deploy-webjobs/aaw2.png)

Witaj pola w tym oknie dialogowym odpowiadają toofields na powitania **nowe zadanie** dialogowe hello portalu Azure. Aby uzyskać więcej informacji, zobacz [zadania w tle uruchom z zadań Webjob](web-sites-create-web-jobs.md).

> [!NOTE]
> * Informacji o wdrażaniu wiersza polecenia, zobacz [Włączanie wiersza polecenia lub ciągłego dostarczania Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).
> * Jeśli zdecydujesz się toochange hello typu zadania WebJob i utwórz je ponownie po wdrożeniu zadanie WebJob, konieczne będzie toodelete hello zadań webjob publikowania settings.json pliku. Spowoduje to Visual Studio Pokaż hello opcje publikowania, dzięki czemu można zmieniać hello typu zadania WebJob.
> * Jeśli zadanie WebJob wdrożyć, a później zmieni hello w trybie uruchamiania z ciągłego ciągłego toonon lub odwrotnie, Visual Studio tworzy nowe zadania WebJob na platformie Azure podczas ponownego wdrażania. Jeśli zmienisz inne ustawienia harmonogramu, ale pozostaw Uruchom tryb hello takie same lub przełączać się między zaplanowane i na żądanie, aktualizacji programu Visual Studio hello istniejące zadanie zamiast tworzyć nowy.
> 
> 

## <a id="publishsettings"></a>zadania webjob — Opublikuj settings.json
Po skonfigurowaniu aplikacji konsoli dla zadań Webjob wdrożenia programu Visual Studio instaluje hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet pakietu i planowania informacji w magazynach *zadania webjob publikowania settings.json*  plik w projekcie hello *właściwości* folderu projektu zadania Webjob hello. Oto przykład tego pliku:

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

Ten plik można edytować bezpośrednio, a program Visual Studio udostępnia IntelliSense. Schemat pliku Hello jest przechowywany w [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) i można wyświetlić.  

## <a id="webjobslist"></a>list.json zadań webjob
Po połączeniu projektu sieci web tooa włączone zadań Webjob projektu programu Visual Studio przechowuje hello Nazwa projektu zadania Webjob hello w *list.json webjob* plik w projekcie sieci web hello *właściwości* folderu. listy Hello może zawierać wiele projektów zadań Webjob, jak pokazano w hello poniższy przykład:

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

Ten plik można edytować bezpośrednio, a program Visual Studio udostępnia IntelliSense. Schemat pliku Hello jest przechowywany w [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) i można wyświetlić.

## <a id="deploy"></a>Wdrażanie projektu zadania Webjob
Dołączono tooa projektu sieci web projektu zadania Webjob automatycznie wdraża z hello projektu sieci web. Aby uzyskać informacje dotyczące wdrażania projektu sieci web, zobacz [jak tooWeb toodeploy aplikacji](web-sites-deploy.md).

toodeploy projektu zadania Webjob przez siebie, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** i kliknij przycisk **Publikuj jako zadanie WebJob platformy Azure...** . 

![Publikuj jako zadanie WebJob platformy Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

Niezależnie od zadania WebJob hello sam **publikowanie w sieci Web** kreatora, który jest używany dla projektów sieci web jest wyświetlana, ale mniej toochange dostępne ustawienia.

## <a id="nextsteps"></a>Następne kroki
Ten artykuł zawiera opis sposobu toodeploy zadań Webjob za pomocą programu Visual Studio. Aby uzyskać więcej informacji na temat toodeploy zadań Webjob Azure, zobacz temat [zadań Webjob Azure - zalecane zasoby — wdrożenia](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).

