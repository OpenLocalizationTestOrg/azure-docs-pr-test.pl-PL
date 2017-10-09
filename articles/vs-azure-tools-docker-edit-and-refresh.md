---
title: aplikacje aaaDebugging w kontenerze Docker lokalnym | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toomodify aplikacji, która jest uruchomiona w kontenerze Docker lokalnego, Odśwież hello kontenera za pomocą edycji i Odśwież i ustaw punkty przerwania debugowania"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a>Debugowanie aplikacji w lokalnym kontenerze platformy Docker
## <a name="overview"></a>Omówienie
Hello Visual Studio Tools for Docker zapewnia spójny sposób toodevelop w i zweryfikować Twojej aplikacji lokalnie w kontenerze Docker systemu Linux.
Nie masz kontenera hello toorestart zawsze, gdy należy zmienić kod.
W tym artykule przedstawiono sposób toostart funkcji "Edytuj i Odśwież" hello toouse aplikacji sieci Web platformy ASP.NET Core w kontenerze Docker lokalnym, wprowadź niezbędne zmiany, a następnie Odśwież toosee przeglądarki hello te zmiany.
Ten artykuł zawiera także jak punkty przerwania tooset do debugowania.

> [!NOTE]
> Obsługa kontenera systemu Windows zostanie udostępniona w przyszłej wersji
>
>

## <a name="prerequisites"></a>Wymagania wstępne
następujące narzędzia Hello musi być zainstalowany.

* [Najnowszą wersję programu Visual Studio](https://www.visualstudio.com/downloads/)
* [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)

lokalnie toorun Docker kontenerów, będziesz potrzebować klienta lokalnego docker.
Można użyć hello [przybornika Docker](https://www.docker.com/products/docker-toolbox), co wymaga funkcji Hyper-V toobe wyłączone lub można użyć [Docker dla systemu Windows](https://www.docker.com/get-docker), który korzysta z funkcji Hyper-V i wymaga systemu Windows 10.

Jeśli przy użyciu rozwiązania Docker przybornika, konieczne będzie zbyt[skonfigurować powitania klienta Docker](vs-azure-tools-docker-setup.md)

## <a name="1-create-a-web-app"></a>1. Tworzenie aplikacji sieci Web
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Dodawanie obsługi Docker
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a>3. Edytuj kod i odświeżanie
tooquickly iteracyjne zmiany, możesz uruchomić aplikację w kontenerze i kontynuować toomake zmian, ich wyświetlania, jak w przypadku z programem IIS Express.

1. Ustaw hello konfiguracji rozwiązania za`Debug` i naciśnij klawisz  **&lt;CTRL + F5 >** toobuild Twojego docker obrazu i uruchom lokalnie.

    Po hello kontenera obraz został utworzony i działa w kontenerze Docker, Visual Studio uruchomi hello aplikacji sieci Web w domyślnej przeglądarce.
    Jeśli używasz przeglądarki Microsoft Edge hello lub w przeciwnym razie zawiera błędy, zobacz [Rozwiązywanie problemów](vs-azure-tools-docker-troubleshooting-docker-errors.md) sekcji.
2. Przejdź toohello o stronę, czyli gdzie zamierzamy toomake naszych zmiany.
3. Zwraca tooVisual Studio i Otwórz `Views\Home\About.cshtml`.
4. Dodaj hello toohello zawartości HTML końca pliku hello i Zapisz zmiany hello.

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. Wyświetlanie hello okno danych wyjściowych, po ukończeniu hello kompilacji platformy .NET i wyświetlić te wiersze, Przełącz tooyour Wstecz przeglądarki i Odśwież hello o stronie.

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. Zmiany zostały zastosowane!

## <a name="4-debug-with-breakpoints"></a>4. Debugowanie przy użyciu punktów przerwania
Często zmiany należy dalszych kontroli, wykorzystując hello funkcji programu Visual Studio do debugowania.

1. Zwraca tooVisual Studio i Otwórz`Controllers\HomeController.cs`
2. Zastąp zawartość hello metody About() hello hello poniżej:

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. Zestaw toohello punktu przerwania rogu hello `string message`... wiersza.
4. Trafienia  **&lt;F5 >** toostart debugowania.
5. Przejdź toohello o toohit strony punkt przerwania.
6. Przełącz tooVisual Studio tooview hello przerwania i sprawdzić wartość wiadomość hello.

   ![][2]

## <a name="summary"></a>Podsumowanie
Z [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), możesz uzyskać produktywność hello lokalnie, Praca z wzrostu produkcji hello rozwijających się w kontenerze Docker.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
[Rozwiązywanie problemów z tworzenia Docker Visual Studio](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>Więcej informacji na temat rozwiązania Docker z programu Visual Studio, Windows i Azure
* [Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) — tworzenie kodu platformy .NET Core w kontenerze
* [Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) — tworzenie i wdrażanie kontenerów docker
* [Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) -języka usługi do edycji plików docker z scenariuszy e2e pochodzących
* [Informacje o kontenerze Windows](http://aka.ms/containers)— informacje o systemie Windows Server i Nano Server
* [Usługa kontenera platformy Azure](https://azure.microsoft.com/services/container-service/) - [zawartości usługi kontenera platformy Azure](http://aka.ms/AzureContainerService)
* Więcej przykładów dotyczących pracy z rozwiązaniem Docker, zobacz [pracy z rozwiązaniem Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) z hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [pokaz](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/). Przewodniki Szybki Start więcej z hello HealthClinic.biz demonstracyjnej, aby zapoznać [Przewodniki Szybki Start Azure Developer Tools](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).

## <a name="various-docker-tools"></a>Różne narzędzia Docker
[Niektóre narzędzia dużą docker (blog Steve'a Lasker)](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a>Artykuły dobra
[Wprowadzenie tooMicroservices z NGINX](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a>Prezentacje
* [Steve Lasker: VS Wyszków 2016 - Docker e2e na żywo](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [Wprowadzenie tooASP.NET Core @ kompilacji 2016 - gdzie możesz w pokaz](https://channel9.msdn.com/Events/Build/2016/B810)
* [Tworzenie aplikacji .NET w kontenerach, Channel 9](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
