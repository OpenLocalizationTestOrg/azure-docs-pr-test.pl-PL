---
title: "aaaTroubleshooting Docker klienta błędów w systemie Windows za pomocą programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów występujących podczas korzystania z programu Visual Studio toocreate i wdrażanie tooDocker aplikacji sieci web w systemie Windows za pomocą programu Visual Studio."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a>Rozwiązywanie problemów z programu Visual Studio Docker programowanie

Podczas pracy z programu Visual Studio Tools dla platformy Docker w wersji zapoznawczej, mogą wystąpić problemy z powodu hello rodzaj hello podglądu.
Poniżej przedstawiono niektóre typowe problemy i rozwiązania.  

## <a name="visual-studio-2017-rc"></a>Visual Studio 2017 RC

### <a name="linux-containers"></a>**Kontenery systemu Linux**

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a>Tworzenie występują błędy podczas debugowania aplikacji sieci web lub konsoli .NET Core  

Może to być powiązane toonot udostępnianie dysku hello, gdzie znajduje się projekt hello Docker dla systemu Windows.  Może zostać wyświetlony błąd, podobnie jak poniżej hello:

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
tooresolve tego problemu:

1. Kliknij prawym przyciskiem myszy **Docker dla systemu Windows** w hello w obszarze powiadomień, a następnie wybierz **ustawienia**.  
2. Wybierz **udostępnione dyski** i udostępnianie dysku hello, gdzie znajduje się projekt hello.

### <a name="windows-containers"></a>**Kontenery systemu Windows**

Witaj następujące problemy są toodebugging określonych aplikacji sieci web i konsoli .NET Framework w kontenerach systemu Windows.

#### <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2017 RC (lub nowszym) z hello .NET Core i musi zostać zainstalowany obciążenia Docker w wersji zapoznawczej.
2. Poprawek systemu Windows 10 Anniversary aktualizacji za pomocą najnowszej Windows Update. W szczególności [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) musi być zainstalowany. 
3. [Docker dla systemu Windows](https://docs.docker.com/docker-for-windows/) (kompilacji 1.13.0 lub nowszym) musi być zainstalowany.
4. **Przełącz kontenery tooWindows** musi być zaznaczone. W obszarze powiadomień hello, kliknij przycisk **Docker dla systemu Windows**, a następnie wybierz **przełącznika kontenery tooWindows**. Po ponownym uruchomieniu komputera hello, upewnij się, że to ustawienie jest zachowywane.

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a>Dane wyjściowe konsoli nie jest wyświetlany w oknie danych wyjściowych programu Visual Studio podczas debugowania aplikacji konsoli

Jest to znany problem dotyczący debuger programu Visual Studio hello (msvsmon.exe), który obecnie nie jest przeznaczony dla tego scenariusza. Obsługa tego scenariusza, mogą zostać dołączone w przyszłej wersji. dane wyjściowe toosee hello aplikacji konsoli w programie Visual Studio, użyj **Docker: uruchomić projekt**, który jest równoważne zbyt**uruchomić bez debugowania**.

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a>Debugowanie aplikacji sieci web z hello wersji konfiguracji nie powiodło się błędem (403) zabroniony

toowork rozwiązać ten problem, otwórz web.release.config w rozwiązaniu hello i Oznacz jako komentarz lub usuń hello następujące wiersze:

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a>Visual Studio 2015

### <a name="linux-containers"></a>**Kontenery systemu Linux**

#### <a name="unable-toovalidate-volume-mapping"></a>Nie można toovalidate woluminu mapowania
Mapowanie woluminu jest kod źródłowy hello wymagane tooshare i pliki binarne z folderu aplikacji hello w kontenerze hello aplikacji.  Określony wolumin mapowania są zawarte w docker compose.dev.debug.yml i docker compose.dev.release.yml. Jak na komputerze hosta zostały zmienione pliki, kontenery hello odzwierciedlenia tych zmian w strukturze folderu podobne.

Mapowanie woluminu tooenable:

1. Kliknij przycisk **Moby** w obszarze powiadomień hello i wybierz **ustawienia**.
2. Wybierz **udostępnionych dysków**.
3. Wybierz dysk hello, który jest hostem dysku projektu i hello, w którym znajduje się % USERPROFILE %.
4. Kliknij przycisk **Zastosuj**.

tootest działa mapowanie woluminu, skompiluj ponownie i wybierz F5 z poziomu programu Visual Studio po co najmniej jednej stacji zostały udostępnione, lub uruchom hello następującego kodu w wierszu polecenia.

> [!NOTE]
> W tym przykładzie przyjęto założenie, że folder użytkowników znajduje się na dysku C i został udostępniony.
> Sprawdź, czy w razie potrzeby, jeśli udostępniasz inny dysk.

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

Uruchom hello następującego kodu w kontenerze systemu Linux hello.

```
/ # ls
```

Listę z folderu publicznego i użytkownicy hello katalogów powinno być widoczne. Jeśli żadne pliki nie są wyświetlane i folderze /c/Users/Public nie jest pusta, mapowanie wolumin nie jest prawidłowo skonfigurowany.

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

Zmień toohello tunel katalogu toosee hello zawartość hello `/c/Users/Public` katalogu:

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> Podczas pracy z maszyn wirtualnych systemu Linux, system plików kontenera hello jest rozróżniana wielkość liter.

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a>Kompilacji: Wystąpił nieoczekiwany błąd zadania "PrepareForBuild"

Microsoft.DotNet.Docker.CommandLine.ClientException: Wystąpił błąd w trakcie tooconnect.

Sprawdź, czy działa hostujących hello domyślne Docker. Otwórz wiersz polecenia i wykonać:

```
docker info
```

Jeśli to zwraca błąd, spróbuj toostart hello **Docker dla systemu Windows** aplikacji komputerowej. Jeśli aplikacja klasyczna hello jest uruchomiona, następnie **Moby** powinny być widoczne w obszarze powiadomień hello. Kliknij prawym przyciskiem myszy **Moby** , a następnie otwórz **ustawienia**. Kliknij przycisk **zresetować**, a następnie ponownie uruchom Docker.

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a>Okna dialogowego błędu występuje podczas próby tooadd Docker pomocy technicznej lub debugowania aplikacji platformy ASP.NET Core w kontenerze (F5)

Po odinstalowaniu i instalowanie rozszerzeń, hello pamięci podręcznej Managed Extensibility Framework (MEF) w programie Visual Studio może ulec uszkodzeniu. W takiej sytuacji może spowodować różnych komunikaty o błędach, gdy użytkownik jest dodanie obsługi Docker i/lub próby toorun lub debugowania aplikacji ASP.NET Core (F5). Tymczasowo Użyj hello następujące kroki toodelete i regenerate hello pamięć podręczna MEF.

1. Zamknij wszystkie wystąpienia programu Visual Studio.
1. Otwórz % USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.
1. Usuń następujące foldery hello:
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. Otwórz program Visual Studio.
1. Spróbuj ponownie wykonać hello scenariusza.
