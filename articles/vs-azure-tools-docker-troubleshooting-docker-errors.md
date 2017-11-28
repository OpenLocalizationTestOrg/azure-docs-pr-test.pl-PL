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
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="664a1-103">Rozwiązywanie problemów z programu Visual Studio Docker programowanie</span><span class="sxs-lookup"><span data-stu-id="664a1-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="664a1-104">Podczas pracy z programu Visual Studio Tools dla platformy Docker w wersji zapoznawczej, mogą wystąpić problemy z powodu hello rodzaj hello podglądu.</span><span class="sxs-lookup"><span data-stu-id="664a1-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of hello nature of hello preview.</span></span>
<span data-ttu-id="664a1-105">Poniżej przedstawiono niektóre typowe problemy i rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="664a1-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="664a1-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="664a1-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="664a1-107">**Kontenery systemu Linux**</span><span class="sxs-lookup"><span data-stu-id="664a1-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="664a1-108">Tworzenie występują błędy podczas debugowania aplikacji sieci web lub konsoli .NET Core</span><span class="sxs-lookup"><span data-stu-id="664a1-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="664a1-109">Może to być powiązane toonot udostępnianie dysku hello, gdzie znajduje się projekt hello Docker dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="664a1-109">This could be related toonot sharing hello drive where hello project resides with Docker for Windows.</span></span>  <span data-ttu-id="664a1-110">Może zostać wyświetlony błąd, podobnie jak poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="664a1-110">You may receive an error like hello following:</span></span>

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="664a1-111">tooresolve tego problemu:</span><span class="sxs-lookup"><span data-stu-id="664a1-111">tooresolve this issue:</span></span>

1. <span data-ttu-id="664a1-112">Kliknij prawym przyciskiem myszy **Docker dla systemu Windows** w hello w obszarze powiadomień, a następnie wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="664a1-112">Right-click **Docker for Windows** in hello notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="664a1-113">Wybierz **udostępnione dyski** i udostępnianie dysku hello, gdzie znajduje się projekt hello.</span><span class="sxs-lookup"><span data-stu-id="664a1-113">Select **Shared Drives** and share hello drive where hello project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="664a1-114">**Kontenery systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="664a1-114">**Windows containers**</span></span>

<span data-ttu-id="664a1-115">Witaj następujące problemy są toodebugging określonych aplikacji sieci web i konsoli .NET Framework w kontenerach systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="664a1-115">hello following issues are specific toodebugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="664a1-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="664a1-116">Prerequisites</span></span>

1. <span data-ttu-id="664a1-117">Visual Studio 2017 RC (lub nowszym) z hello .NET Core i musi zostać zainstalowany obciążenia Docker w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="664a1-117">Visual Studio 2017 RC (or later) with hello .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="664a1-118">Poprawek systemu Windows 10 Anniversary aktualizacji za pomocą najnowszej Windows Update.</span><span class="sxs-lookup"><span data-stu-id="664a1-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="664a1-119">W szczególności [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) musi być zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="664a1-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="664a1-120">[Docker dla systemu Windows](https://docs.docker.com/docker-for-windows/) (kompilacji 1.13.0 lub nowszym) musi być zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="664a1-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="664a1-121">**Przełącz kontenery tooWindows** musi być zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="664a1-121">**Switch tooWindows containers** must be selected.</span></span> <span data-ttu-id="664a1-122">W obszarze powiadomień hello, kliknij przycisk **Docker dla systemu Windows**, a następnie wybierz **przełącznika kontenery tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="664a1-122">In hello notification area, click **Docker for Windows**, and then select **Switch tooWindows containers**.</span></span> <span data-ttu-id="664a1-123">Po ponownym uruchomieniu komputera hello, upewnij się, że to ustawienie jest zachowywane.</span><span class="sxs-lookup"><span data-stu-id="664a1-123">After hello machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="664a1-124">Dane wyjściowe konsoli nie jest wyświetlany w oknie danych wyjściowych programu Visual Studio podczas debugowania aplikacji konsoli</span><span class="sxs-lookup"><span data-stu-id="664a1-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="664a1-125">Jest to znany problem dotyczący debuger programu Visual Studio hello (msvsmon.exe), który obecnie nie jest przeznaczony dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="664a1-125">This is a known issue with hello Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="664a1-126">Obsługa tego scenariusza, mogą zostać dołączone w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="664a1-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="664a1-127">dane wyjściowe toosee hello aplikacji konsoli w programie Visual Studio, użyj **Docker: uruchomić projekt**, który jest równoważne zbyt**uruchomić bez debugowania**.</span><span class="sxs-lookup"><span data-stu-id="664a1-127">toosee output from hello console application in Visual Studio, use **Docker: Start Project**, which is equivalent too**Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="664a1-128">Debugowanie aplikacji sieci web z hello wersji konfiguracji nie powiodło się błędem (403) zabroniony</span><span class="sxs-lookup"><span data-stu-id="664a1-128">Debugging web applications with hello release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="664a1-129">toowork rozwiązać ten problem, otwórz web.release.config w rozwiązaniu hello i Oznacz jako komentarz lub usuń hello następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="664a1-129">toowork around this issue, open web.release.config in hello solution and comment out or delete hello following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="664a1-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="664a1-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="664a1-131">**Kontenery systemu Linux**</span><span class="sxs-lookup"><span data-stu-id="664a1-131">**Linux containers**</span></span>

#### <a name="unable-toovalidate-volume-mapping"></a><span data-ttu-id="664a1-132">Nie można toovalidate woluminu mapowania</span><span class="sxs-lookup"><span data-stu-id="664a1-132">Unable toovalidate volume mapping</span></span>
<span data-ttu-id="664a1-133">Mapowanie woluminu jest kod źródłowy hello wymagane tooshare i pliki binarne z folderu aplikacji hello w kontenerze hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="664a1-133">Volume mapping is required tooshare hello source code and binaries of your application with hello app folder in hello container.</span></span>  <span data-ttu-id="664a1-134">Określony wolumin mapowania są zawarte w docker compose.dev.debug.yml i docker compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="664a1-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="664a1-135">Jak na komputerze hosta zostały zmienione pliki, kontenery hello odzwierciedlenia tych zmian w strukturze folderu podobne.</span><span class="sxs-lookup"><span data-stu-id="664a1-135">As files are changed on your host machine, hello containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="664a1-136">Mapowanie woluminu tooenable:</span><span class="sxs-lookup"><span data-stu-id="664a1-136">tooenable volume mapping:</span></span>

1. <span data-ttu-id="664a1-137">Kliknij przycisk **Moby** w obszarze powiadomień hello i wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="664a1-137">Click **Moby** in hello notification area and select **Settings**.</span></span>
2. <span data-ttu-id="664a1-138">Wybierz **udostępnionych dysków**.</span><span class="sxs-lookup"><span data-stu-id="664a1-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="664a1-139">Wybierz dysk hello, który jest hostem dysku projektu i hello, w którym znajduje się % USERPROFILE %.</span><span class="sxs-lookup"><span data-stu-id="664a1-139">Select hello drive that hosts your project and hello drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="664a1-140">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="664a1-140">Click **Apply**.</span></span>

<span data-ttu-id="664a1-141">tootest działa mapowanie woluminu, skompiluj ponownie i wybierz F5 z poziomu programu Visual Studio po co najmniej jednej stacji zostały udostępnione, lub uruchom hello następującego kodu w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="664a1-141">tootest if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run hello following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="664a1-142">W tym przykładzie przyjęto założenie, że folder użytkowników znajduje się na dysku C i został udostępniony.</span><span class="sxs-lookup"><span data-stu-id="664a1-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="664a1-143">Sprawdź, czy w razie potrzeby, jeśli udostępniasz inny dysk.</span><span class="sxs-lookup"><span data-stu-id="664a1-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="664a1-144">Uruchom hello następującego kodu w kontenerze systemu Linux hello.</span><span class="sxs-lookup"><span data-stu-id="664a1-144">Run hello following code in hello Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="664a1-145">Listę z folderu publicznego i użytkownicy hello katalogów powinno być widoczne.</span><span class="sxs-lookup"><span data-stu-id="664a1-145">You should see a directory listing from hello Users/Public folder.</span></span> <span data-ttu-id="664a1-146">Jeśli żadne pliki nie są wyświetlane i folderze /c/Users/Public nie jest pusta, mapowanie wolumin nie jest prawidłowo skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="664a1-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="664a1-147">Zmień toohello tunel katalogu toosee hello zawartość hello `/c/Users/Public` katalogu:</span><span class="sxs-lookup"><span data-stu-id="664a1-147">Change toohello wormhole directory toosee hello contents of hello `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="664a1-148">Podczas pracy z maszyn wirtualnych systemu Linux, system plików kontenera hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="664a1-148">When you're working with Linux VMs, hello container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="664a1-149">Kompilacji: Wystąpił nieoczekiwany błąd zadania "PrepareForBuild"</span><span class="sxs-lookup"><span data-stu-id="664a1-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="664a1-150">Microsoft.DotNet.Docker.CommandLine.ClientException: Wystąpił błąd w trakcie tooconnect.</span><span class="sxs-lookup"><span data-stu-id="664a1-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying tooconnect.</span></span>

<span data-ttu-id="664a1-151">Sprawdź, czy działa hostujących hello domyślne Docker.</span><span class="sxs-lookup"><span data-stu-id="664a1-151">Verify that hello default Docker host is running.</span></span> <span data-ttu-id="664a1-152">Otwórz wiersz polecenia i wykonać:</span><span class="sxs-lookup"><span data-stu-id="664a1-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="664a1-153">Jeśli to zwraca błąd, spróbuj toostart hello **Docker dla systemu Windows** aplikacji komputerowej.</span><span class="sxs-lookup"><span data-stu-id="664a1-153">If this returns an error, then attempt toostart hello **Docker for Windows** desktop app.</span></span> <span data-ttu-id="664a1-154">Jeśli aplikacja klasyczna hello jest uruchomiona, następnie **Moby** powinny być widoczne w obszarze powiadomień hello.</span><span class="sxs-lookup"><span data-stu-id="664a1-154">If hello desktop app is running, then **Moby** should be visible in hello notification area.</span></span> <span data-ttu-id="664a1-155">Kliknij prawym przyciskiem myszy **Moby** , a następnie otwórz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="664a1-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="664a1-156">Kliknij przycisk **zresetować**, a następnie ponownie uruchom Docker.</span><span class="sxs-lookup"><span data-stu-id="664a1-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="664a1-157">Okna dialogowego błędu występuje podczas próby tooadd Docker pomocy technicznej lub debugowania aplikacji platformy ASP.NET Core w kontenerze (F5)</span><span class="sxs-lookup"><span data-stu-id="664a1-157">An error dialog occurs when attempting tooadd Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="664a1-158">Po odinstalowaniu i instalowanie rozszerzeń, hello pamięci podręcznej Managed Extensibility Framework (MEF) w programie Visual Studio może ulec uszkodzeniu.</span><span class="sxs-lookup"><span data-stu-id="664a1-158">After uninstalling and installing extensions, hello Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="664a1-159">W takiej sytuacji może spowodować różnych komunikaty o błędach, gdy użytkownik jest dodanie obsługi Docker i/lub próby toorun lub debugowania aplikacji ASP.NET Core (F5).</span><span class="sxs-lookup"><span data-stu-id="664a1-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting toorun or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="664a1-160">Tymczasowo Użyj hello następujące kroki toodelete i regenerate hello pamięć podręczna MEF.</span><span class="sxs-lookup"><span data-stu-id="664a1-160">As a temporary workaround, use hello following steps toodelete and regenerate hello MEF cache.</span></span>

1. <span data-ttu-id="664a1-161">Zamknij wszystkie wystąpienia programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="664a1-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="664a1-162">Otwórz % USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="664a1-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="664a1-163">Usuń następujące foldery hello:</span><span class="sxs-lookup"><span data-stu-id="664a1-163">Delete hello following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="664a1-164">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="664a1-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="664a1-165">Spróbuj ponownie wykonać hello scenariusza.</span><span class="sxs-lookup"><span data-stu-id="664a1-165">Attempt hello scenario again.</span></span>
