---
title: "Rozwiązywanie problemów z błędami klienta Docker w systemie Windows za pomocą programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów występujących podczas tworzenia i wdrażania aplikacji sieci web do Docker w systemie Windows za pomocą programu Visual Studio przy użyciu programu Visual Studio."
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
ms.openlocfilehash: 89fa04a1107b6abb49aefd68066443717ac9b731
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="135bf-103">Rozwiązywanie problemów z programu Visual Studio Docker programowanie</span><span class="sxs-lookup"><span data-stu-id="135bf-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="135bf-104">Podczas pracy z programu Visual Studio Tools dla platformy Docker w wersji zapoznawczej, mogą wystąpić problemy z powodu charakteru wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="135bf-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of the nature of the preview.</span></span>
<span data-ttu-id="135bf-105">Poniżej przedstawiono niektóre typowe problemy i rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="135bf-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="135bf-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="135bf-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="135bf-107">**Kontenery systemu Linux**</span><span class="sxs-lookup"><span data-stu-id="135bf-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="135bf-108">Tworzenie występują błędy podczas debugowania aplikacji sieci web lub konsoli .NET Core</span><span class="sxs-lookup"><span data-stu-id="135bf-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="135bf-109">Może to być związane z nie udostępnianie dysku, na którym znajduje się projekt Docker dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="135bf-109">This could be related to not sharing the drive where the project resides with Docker for Windows.</span></span>  <span data-ttu-id="135bf-110">Może zostać wyświetlony następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="135bf-110">You may receive an error like the following:</span></span>

```
The "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with the default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="135bf-111">Aby rozwiązać ten problem:</span><span class="sxs-lookup"><span data-stu-id="135bf-111">To resolve this issue:</span></span>

1. <span data-ttu-id="135bf-112">Kliknij prawym przyciskiem myszy **Docker dla systemu Windows** w obszarze powiadomień, a następnie wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="135bf-112">Right-click **Docker for Windows** in the notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="135bf-113">Wybierz **udostępnione dyski** i udostępnić dysk, na którym znajduje się projekt.</span><span class="sxs-lookup"><span data-stu-id="135bf-113">Select **Shared Drives** and share the drive where the project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="135bf-114">**Kontenery systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="135bf-114">**Windows containers**</span></span>

<span data-ttu-id="135bf-115">Następujące problemy są specyficzne dla aplikacji sieci web i konsoli w kontenerach Windows .NET Framework — profilowanie.</span><span class="sxs-lookup"><span data-stu-id="135bf-115">The following issues are specific to debugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="135bf-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="135bf-116">Prerequisites</span></span>

1. <span data-ttu-id="135bf-117">Visual Studio 2017 RC (lub nowsza) .NET Core i Podgląd Docker obciążenia musi być zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="135bf-117">Visual Studio 2017 RC (or later) with the .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="135bf-118">Poprawek systemu Windows 10 Anniversary aktualizacji za pomocą najnowszej Windows Update.</span><span class="sxs-lookup"><span data-stu-id="135bf-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="135bf-119">W szczególności [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) musi być zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="135bf-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="135bf-120">[Docker dla systemu Windows](https://docs.docker.com/docker-for-windows/) (kompilacji 1.13.0 lub nowszym) musi być zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="135bf-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="135bf-121">**Przełącz się do systemu Windows kontenery** musi być zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="135bf-121">**Switch to Windows containers** must be selected.</span></span> <span data-ttu-id="135bf-122">W obszarze powiadomień, kliknij przycisk **Docker dla systemu Windows**, a następnie wybierz **przełączyć się do systemu Windows kontenery**.</span><span class="sxs-lookup"><span data-stu-id="135bf-122">In the notification area, click **Docker for Windows**, and then select **Switch to Windows containers**.</span></span> <span data-ttu-id="135bf-123">Po ponownym uruchomieniu komputera, upewnij się, że to ustawienie jest zachowywane.</span><span class="sxs-lookup"><span data-stu-id="135bf-123">After the machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="135bf-124">Dane wyjściowe konsoli nie jest wyświetlany w oknie danych wyjściowych programu Visual Studio podczas debugowania aplikacji konsoli</span><span class="sxs-lookup"><span data-stu-id="135bf-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="135bf-125">Jest to znany problem dotyczący debuger programu Visual Studio (msvsmon.exe), który obecnie nie jest przeznaczony dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="135bf-125">This is a known issue with the Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="135bf-126">Obsługa tego scenariusza, mogą zostać dołączone w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="135bf-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="135bf-127">Aby wyświetlić dane wyjściowe z aplikacji konsoli w programie Visual Studio, użyj **Docker: Uruchom projekt**, który jest odpowiednikiem **uruchomić bez debugowania**.</span><span class="sxs-lookup"><span data-stu-id="135bf-127">To see output from the console application in Visual Studio, use **Docker: Start Project**, which is equivalent to **Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-the-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="135bf-128">Debugowanie aplikacji sieci web z wersji konfiguracji nie powiodło się błędem (403) zabroniony</span><span class="sxs-lookup"><span data-stu-id="135bf-128">Debugging web applications with the release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="135bf-129">Aby obejść ten problem, otwórz web.release.config w rozwiązaniu i Oznacz jako komentarz lub usunąć następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="135bf-129">To work around this issue, open web.release.config in the solution and comment out or delete the following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="135bf-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="135bf-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="135bf-131">**Kontenery systemu Linux**</span><span class="sxs-lookup"><span data-stu-id="135bf-131">**Linux containers**</span></span>

#### <a name="unable-to-validate-volume-mapping"></a><span data-ttu-id="135bf-132">Nie można sprawdzić poprawności mapowania woluminu</span><span class="sxs-lookup"><span data-stu-id="135bf-132">Unable to validate volume mapping</span></span>
<span data-ttu-id="135bf-133">Mapowanie woluminu jest wymagane na udostępnianie folderu aplikacji w kontenerze kod źródłowy i plików binarnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="135bf-133">Volume mapping is required to share the source code and binaries of your application with the app folder in the container.</span></span>  <span data-ttu-id="135bf-134">Określony wolumin mapowania są zawarte w docker compose.dev.debug.yml i docker compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="135bf-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="135bf-135">Jak na komputerze hosta zostały zmienione pliki, kontenery odzwierciedlenia tych zmian w strukturze folderu podobne.</span><span class="sxs-lookup"><span data-stu-id="135bf-135">As files are changed on your host machine, the containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="135bf-136">Aby włączyć mapowanie woluminu:</span><span class="sxs-lookup"><span data-stu-id="135bf-136">To enable volume mapping:</span></span>

1. <span data-ttu-id="135bf-137">Kliknij przycisk **Moby** w obszarze powiadomień, a następnie wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="135bf-137">Click **Moby** in the notification area and select **Settings**.</span></span>
2. <span data-ttu-id="135bf-138">Wybierz **udostępnionych dysków**.</span><span class="sxs-lookup"><span data-stu-id="135bf-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="135bf-139">Wybierz dysk, który jest hostem projektu i dysku, na którym znajduje się % USERPROFILE %.</span><span class="sxs-lookup"><span data-stu-id="135bf-139">Select the drive that hosts your project and the drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="135bf-140">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="135bf-140">Click **Apply**.</span></span>

<span data-ttu-id="135bf-141">Aby sprawdzić, czy działa mapowanie woluminu, ponowne skompilowanie i wybierz F5 z poziomu programu Visual Studio po co najmniej jednej stacji zostały udostępnione, lub uruchom polecenie w wierszu polecenia następujący kod.</span><span class="sxs-lookup"><span data-stu-id="135bf-141">To test if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run the following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="135bf-142">W tym przykładzie przyjęto założenie, że folder użytkowników znajduje się na dysku C i został udostępniony.</span><span class="sxs-lookup"><span data-stu-id="135bf-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="135bf-143">Sprawdź, czy w razie potrzeby, jeśli udostępniasz inny dysk.</span><span class="sxs-lookup"><span data-stu-id="135bf-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="135bf-144">Uruchom poniższy kod w kontenerze systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="135bf-144">Run the following code in the Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="135bf-145">Powinny pojawić się katalogu z folderu publicznego i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="135bf-145">You should see a directory listing from the Users/Public folder.</span></span> <span data-ttu-id="135bf-146">Jeśli żadne pliki nie są wyświetlane i folderze /c/Users/Public nie jest pusta, mapowanie wolumin nie jest prawidłowo skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="135bf-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="135bf-147">Przejdź do katalogu tunel, aby wyświetlić zawartość `/c/Users/Public` katalogu:</span><span class="sxs-lookup"><span data-stu-id="135bf-147">Change to the wormhole directory to see the contents of the `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="135bf-148">Podczas pracy z maszyn wirtualnych systemu Linux kontenera systemu plików jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="135bf-148">When you're working with Linux VMs, the container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="135bf-149">Kompilacji: Wystąpił nieoczekiwany błąd zadania "PrepareForBuild"</span><span class="sxs-lookup"><span data-stu-id="135bf-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="135bf-150">Microsoft.DotNet.Docker.CommandLine.ClientException: Wystąpił błąd podczas próby nawiązania połączenia.</span><span class="sxs-lookup"><span data-stu-id="135bf-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying to connect.</span></span>

<span data-ttu-id="135bf-151">Sprawdź, czy działa host Docker domyślne.</span><span class="sxs-lookup"><span data-stu-id="135bf-151">Verify that the default Docker host is running.</span></span> <span data-ttu-id="135bf-152">Otwórz wiersz polecenia i wykonać:</span><span class="sxs-lookup"><span data-stu-id="135bf-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="135bf-153">Jeśli to zwraca błąd, spróbuj uruchomić **Docker dla systemu Windows** aplikacji komputerowej.</span><span class="sxs-lookup"><span data-stu-id="135bf-153">If this returns an error, then attempt to start the **Docker for Windows** desktop app.</span></span> <span data-ttu-id="135bf-154">Jeśli aplikacja klasyczna jest uruchomiona, następnie **Moby** powinny być widoczne w obszarze powiadomień.</span><span class="sxs-lookup"><span data-stu-id="135bf-154">If the desktop app is running, then **Moby** should be visible in the notification area.</span></span> <span data-ttu-id="135bf-155">Kliknij prawym przyciskiem myszy **Moby** , a następnie otwórz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="135bf-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="135bf-156">Kliknij przycisk **zresetować**, a następnie ponownie uruchom Docker.</span><span class="sxs-lookup"><span data-stu-id="135bf-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-to-add-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="135bf-157">Występuje okna dialogowego błędu, gdy próbuje dodać obsługę Docker lub debugowania aplikacji platformy ASP.NET Core w kontenerze (F5)</span><span class="sxs-lookup"><span data-stu-id="135bf-157">An error dialog occurs when attempting to add Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="135bf-158">Po odinstalowaniu i instalowanie rozszerzeń, pamięć podręczna Managed Extensibility Framework (MEF) w programie Visual Studio może ulec uszkodzeniu.</span><span class="sxs-lookup"><span data-stu-id="135bf-158">After uninstalling and installing extensions, the Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="135bf-159">W takiej sytuacji może spowodować różnych komunikaty o błędach, gdy użytkownik jest dodanie obsługi Docker i/lub próby uruchamiania lub debugowania aplikacji ASP.NET Core (F5).</span><span class="sxs-lookup"><span data-stu-id="135bf-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting to run or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="135bf-160">Jako celu tymczasowego obejścia problemu wykonaj następujące kroki, aby usunąć i ponownie wygenerować pamięć podręczna MEF.</span><span class="sxs-lookup"><span data-stu-id="135bf-160">As a temporary workaround, use the following steps to delete and regenerate the MEF cache.</span></span>

1. <span data-ttu-id="135bf-161">Zamknij wszystkie wystąpienia programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="135bf-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="135bf-162">Otwórz % USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="135bf-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="135bf-163">Usuń następujące foldery:</span><span class="sxs-lookup"><span data-stu-id="135bf-163">Delete the following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="135bf-164">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="135bf-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="135bf-165">Spróbuj ponownie wykonać scenariusz.</span><span class="sxs-lookup"><span data-stu-id="135bf-165">Attempt the scenario again.</span></span>
