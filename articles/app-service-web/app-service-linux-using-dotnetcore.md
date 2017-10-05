---
title: "Używanie .NET Core w aplikacji sieci Web w systemie Linux | Dokumentacja firmy Microsoft"
description: "Użyj platformy .NET Core w aplikacji sieci Web w systemie Linux."
keywords: "Usługa aplikacji Azure, aplikacji sieci web, dotnet, core, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9226dfb90e52ac2cae2cfc4af7c0705a93f56b44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>Używanie .NET Core w aplikacji sieci web platformy Azure w systemie Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Sieci Web aplikacji](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) w systemie Linux oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web przy użyciu systemu operacyjnego Linux. Ten samouczek zawiera instrukcje krok po kroku, pokazujący sposób tworzenia [.NET Core](https://docs.microsoft.com/aspnet/core/) aplikacji w aplikacji sieci web platformy Azure w systemie Linux. 

![Aplikacja sieci Web w systemie Linux][10]

Poniższe kroki możesz wykonać przy użyciu komputera z systemem Mac, Windows lub Linux.

## <a name="prerequisites"></a>Wymagania wstępne ##

W celu ukończenia tego samouczka: 

* Zainstaluj [.NET Core SDK](https://www.microsoft.com/net/download/core).
* Zainstaluj [Git](https://git-scm.com/downloads).

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>Tworzenie aplikacji platformy .NET Core lokalnej ##

Rozpocznij nową sesję terminala. Utwórz katalog o nazwie `hellodotnetcore`i zmień bieżący katalog. Następnie wpisz następujące polecenie: 

```
dotnet new web
``` 

  To polecenie tworzy trzy pliki (*hellodotnetcore.csproj*, *Program.cs*, i *Startup.cs*) i jeden pusty folder (*wwwroot /*) w bieżącym katalogu. Zawartość `.csproj` pliku powinna wyglądać następująco: 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

Ponieważ ta aplikacja to aplikacja sieci web, odwołanie do pakietu platformy ASP.NET Core została automatycznie dodana do *hellodotnetcore.csproj* pliku. Numer wersji pakietu jest ustawiona zgodnie z wybranym framework. W tym przykładzie odwołuje się do platformy ASP.NET Core wersji 1.1.2 ponieważ .NET Core 1.1 jest używany.

## <a name="build-and-test-the-application-locally"></a>Tworzenie i testowanie aplikacji lokalnie ##

Możesz skompilować i uruchomić aplikację .NET Core z `dotnet restore` polecenia następuje `dotnet run` polecenia, jak pokazano poniżej:

```
dotnet restore
dotnet run
```


Podczas uruchamiania aplikacji, wyświetla komunikat informujący, że aplikacja nasłuchuje żądań przychodzących do portu. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

Ją przetestować, przechodząc do `http://localhost:5000/` przy użyciu przeglądarki. Jeśli wszystko działa prawidłowo, zobacz "Witaj świecie!" jako tekst wynik.

![Test z przeglądarki][7]

## <a name="create-a-net-core-app-in-the-azure-portal"></a>Utwórz .NET Core aplikacji w portalu Azure ##

Najpierw należy utworzyć pustą aplikację sieci web. Zaloguj się do [portalu Azure](https://portal.azure.com/) i utworzyć nową [aplikacji sieci Web w systemie Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).

![Tworzenie aplikacji sieci web][1]

Gdy **Utwórz** zostanie otwarta strona, zawierają szczegółowe informacje o aplikacji sieci web:

![Wybieranie stosu środowiska uruchomieniowego .NET Core][2]

Skorzystaj z poniższej tabeli przedstawiono wskazówki do wypełniania **Utwórz** strony, a następnie wybierz **OK** i **Utwórz** do utworzenia aplikacji.

| Ustawienie      | Sugerowana wartość  | Opis                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| Nazwa aplikacji | hellodotnetcore  | Nazwa aplikacji. Ta nazwa musi być unikatowa. |
| Subskrypcja | Wybierz istniejącą subskrypcję | Subskrypcja platformy Azure. |
| Grupa zasobów | myResourceGroup |  Grupy zasobów platformy Azure w celu uwzględnienia aplikacji sieci web. |
| Plan usługi App Service | Nazwę istniejącego planu usługi App Service |  Plan usługi aplikacji.  |
| Skonfiguruj kontener | Oprogramowanie .NET core 1.1 | Typ kontenera dla tej aplikacji sieci web: rejestru wbudowanych, Docker lub prywatnych. |
| Źródło obrazu  | Wbudowane  |  Źródło obrazu. |
| Środowisko uruchomieniowe stosu  | Oprogramowanie .NET core 1.1  | Stos środowiska uruchomieniowego i wersji.  |

## <a name="deploy-your-application-via-git"></a>Wdrażanie aplikacji przy użyciu narzędzia Git ##

Git umożliwia wdrażanie aplikacji .NET Core aplikację sieci Web usługi aplikacji Azure w systemie Linux.

W nowej aplikacji sieci web platformy Azure jest już wdrażanie Git jest skonfigurowany. Adres URL wdrożenia Git znajdziesz przechodząc pod następujący adres URL po wstawieniu nazwę aplikacji sieci web:

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

Adres URL Git ma następujący format oparte na nazwę aplikacji sieci web:

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Uruchom następujące polecenia, aby wdrożyć aplikację lokalną do aplikacji sieci web platformy Azure: 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

Nie trzeba push wszystkie pliki w obszarze *bin /* lub *obj /* katalogów aplikacji są wbudowane w chmurze, gdy pliki źródłowe aplikacji są przenoszone do platformy Azure. Po zakończeniu procesu kompilacji plików binarnych, są kopiowane do katalogu aplikacji na */home/lokacji/wwwroot/*.

Upewnij się, że operacje zdalnego wdrażania raportu Powodzenie. Operacje wypychania może potrwać od pakietu rozwiązania i działają w chmurze proces kompilacji. Zobaczysz kilka komunikatów o stanie, między innymi informujący, że pliki zostały skopiowane. Dane wyjściowe powinny wyglądać podobnie do poniższej:

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
To https://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Po zakończeniu wdrożenia należy ponownie uruchomić aplikacji sieci web do wdrożenia zaczęły obowiązywać. Aby to zrobić, przejdź do portalu Azure i przejdź do **omówienie** strony aplikacji sieci web. Wybierz **ponowne uruchomienie** przycisku na stronie. Gdy w oknie podręcznym zostaną wyświetlone, wybierz **tak** o potwierdzenie. Następnie można przeglądać aplikacji sieci web, jak pokazano poniżej:

![Przeglądanie aplikacji .NET Core wdrożony w usłudze Azure App Service w systemie Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Następne kroki
* [Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
