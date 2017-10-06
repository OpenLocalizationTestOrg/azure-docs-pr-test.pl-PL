---
title: aaaUse .NET Core w aplikacji sieci Web w systemie Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>Używanie .NET Core w aplikacji sieci web platformy Azure w systemie Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Sieci Web aplikacji](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) w systemie Linux udostępnia usługi hostingu sieci web wysoce skalowalną, własnym stosowania poprawek za pomocą systemu operacyjnego Linux hello. Ten samouczek zawiera instrukcje krok po kroku przedstawiający sposób toocreate [.NET Core](https://docs.microsoft.com/aspnet/core/) aplikacji w aplikacji sieci web platformy Azure w systemie Linux. 

![Aplikacja sieci Web w systemie Linux][10]

Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux.

## <a name="prerequisites"></a>Wymagania wstępne ##

toocomplete tego samouczka: 

* Zainstaluj hello [.NET Core SDK](https://www.microsoft.com/net/download/core).
* Zainstaluj [Git](https://git-scm.com/downloads).

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>Tworzenie aplikacji platformy .NET Core lokalnej ##

Rozpocznij nową sesję terminala. Utwórz katalog o nazwie `hellodotnetcore`i zmień hello bieżącego katalogu tooit. Następnie wpisz następujące hello: 

```
dotnet new web
``` 

  To polecenie tworzy trzy pliki (*hellodotnetcore.csproj*, *Program.cs*, i *Startup.cs*) i jeden pusty folder (*wwwroot /*) w obszarze hello bieżącego katalogu. Witaj zawartości `.csproj` plik powinien wyglądać jak poniżej hello: 

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

Ponieważ ta aplikacja to aplikacja sieci web, tooan odwołanie do pakietu platformy ASP.NET Core została automatycznie dodana toohello *hellodotnetcore.csproj* pliku. numer wersji pakietu hello Hello jest ustawiona zgodnie z toohello wybrany framework. W tym przykładzie odwołuje się do platformy ASP.NET Core wersji 1.1.2 ponieważ .NET Core 1.1 jest używany.

## <a name="build-and-test-hello-application-locally"></a>Tworzenie i testowanie aplikacji hello lokalnie ##

Możesz skompilować i uruchamianie aplikacji .NET Core hello `dotnet restore` polecenia następuje hello `dotnet run` polecenia, jak pokazano poniżej:

```
dotnet restore
dotnet run
```


Po uruchomieniu aplikacji hello wyświetla komunikat informujący, że aplikacja hello nasłuchuje żądań tooincoming w porcie. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

Ją przetestować, przeglądając zbyt`http://localhost:5000/` przy użyciu przeglądarki. Jeśli wszystko działa prawidłowo, zobacz "Witaj świecie!" jako tekst wynikowy hello.

![Test z przeglądarki][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a>Tworzenie aplikacji platformy .NET Core w hello portalu Azure ##

Najpierw należy toocreate pustą aplikację sieci web. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/) i utworzyć nową [aplikacji sieci Web w systemie Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).

![Tworzenie aplikacji sieci web][1]

Gdy hello **Utwórz** zostanie otwarta strona, zawierają szczegółowe informacje o aplikacji sieci web:

![Wybieranie stosu środowiska uruchomieniowego .NET Core][2]

Użyj hello poniższej tabeli jako toofill przewodnik, limit hello **Utwórz** strony, a następnie wybierz **OK** i **Utwórz** toocreate hello aplikacji.

| Ustawienie      | Sugerowana wartość  | Opis                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| Nazwa aplikacji | hellodotnetcore  | Witaj Nazwa aplikacji. Ta nazwa musi być unikatowa. |
| Subskrypcja | Wybierz istniejącą subskrypcję | Witaj subskrypcji platformy Azure. |
| Grupa zasobów | myResourceGroup |  Witaj zasobów platformy Azure grupy toocontain hello aplikacji sieci web. |
| Plan usługi App Service | Nazwę istniejącego planu usługi App Service |  Witaj planu usługi aplikacji.  |
| Skonfiguruj kontener | Oprogramowanie .NET core 1.1 | Typ kontenera dla tej aplikacji sieci web Hello: rejestru wbudowanych, Docker lub prywatnych. |
| Źródło obrazu  | Wbudowane  |  Źródło Hello hello obrazu. |
| Środowisko uruchomieniowe stosu  | Oprogramowanie .NET core 1.1  | stos środowiska uruchomieniowego Hello i wersji.  |

## <a name="deploy-your-application-via-git"></a>Wdrażanie aplikacji przy użyciu narzędzia Git ##

Git toodeploy hello .NET Core aplikacji tooAzure aplikację usługi aplikacji sieci Web w systemie Linux.

Hello nowej aplikacji sieci web platformy Azure jest już skonfigurowany wdrożenia usługi Git. Adres URL wdrożenia Git hello znajdziesz przechodząc toohello następującego adresu URL po wstawieniu nazwę aplikacji sieci web:

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

adres URL Git Hello ma powitania po formularz bazujący na nazwę aplikacji sieci web:

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Uruchom następujące polecenia toodeploy hello miejscowego tooyour aplikacji sieci web Azure hello: 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

Nie ma potrzeby toopush wszystkie pliki w obszarze *bin /* lub *obj /* katalogów aplikacji są wbudowane w chmurze powitania po hello aplikacji tooAzure przesyłanych plików źródłowych. Po zakończeniu procesu kompilacji hello pliki binarne są kopiowane do katalogu aplikacji hello */home/lokacji/wwwroot/*.

Upewnij się, że operacje zdalnego wdrażania hello Raport powodzenie. Operacje wypychania może potrwać od pakietu rozwiązania i uruchomić w chmurze hello proces kompilacji. Zobaczysz kilka komunikatów o stanie, między innymi informujący, że pliki zostały skopiowane. Witaj dane wyjściowe powinny wyglądać podobnie toohello następujące:

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
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Po zakończeniu wdrażania hello, ponownie uruchom aplikację sieci web dla efektu tootake wdrożenia hello. toodo, przejdź toohello portalu Azure i przejdź toohello **omówienie** strony aplikacji sieci web. Wybierz hello **ponowne uruchomienie** przycisk na stronie powitania. Gdy w oknie podręcznym zostaną wyświetlone, wybierz **tak** tooconfirm. Następnie można przeglądać aplikacji sieci web, jak pokazano poniżej:

![Przeglądanie .NET Core aplikacja wdrożona tooAzure usługi aplikacji w systemie Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Następne kroki
* [Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
