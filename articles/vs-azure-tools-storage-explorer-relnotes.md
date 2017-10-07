---
title: "informacje o wersji aaaMicrosoft Eksploratora usługi Azure Storage (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Informacje o wersji dla Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="d9aab-103">Informacje o wersji Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d9aab-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="d9aab-104">Ten artykuł zawiera Zwolnij hello uwagi 0.8.16 Eksploratora usługi Azure Storage (wersja zapoznawcza) wersji, a także informacje o wersji w poprzednich wersjach.</span><span class="sxs-lookup"><span data-stu-id="d9aab-104">This article contains hello release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="d9aab-105">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](./vs-azure-tools-storage-manage-with-storage-explorer.md) jest aplikacją autonomiczną, która umożliwia tooeasily pracy z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="d9aab-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="d9aab-106">Wersja 0.8.16 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d9aab-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="d9aab-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="d9aab-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="d9aab-108">Pobierz Eksploratora usługi Azure Storage 0.8.16 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d9aab-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="d9aab-109">Eksplorator usługi Azure Storage 0.8.16 (wersja zapoznawcza) dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d9aab-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="d9aab-110">Eksplorator usługi Azure Storage 0.8.16 (wersja zapoznawcza) dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="d9aab-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="d9aab-111">Eksplorator usługi Azure Storage 0.8.16 (wersja zapoznawcza) dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="d9aab-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="d9aab-112">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-112">New</span></span>
* <span data-ttu-id="d9aab-113">Po otwarciu obiektu blob Eksploratora usługi Storage spowoduje wyświetlenie monitu tooupload hello pobrany plik po wykryciu zmiany</span><span class="sxs-lookup"><span data-stu-id="d9aab-113">When you open a blob, Storage Explorer will prompt you tooupload hello downloaded file if a change is detected</span></span>
* <span data-ttu-id="d9aab-114">Rozszerzony stos Azure logowania</span><span class="sxs-lookup"><span data-stu-id="d9aab-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="d9aab-115">Hello lepszą wydajność przekazywania/pobieranie wiele małych plików na powitania sam czas</span><span class="sxs-lookup"><span data-stu-id="d9aab-115">Improved hello performance of uploading/downloading many small files at hello same time</span></span>


### <a name="fixes"></a><span data-ttu-id="d9aab-116">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-116">Fixes</span></span>
* <span data-ttu-id="d9aab-117">Dla niektórych typów obiektów blob wybierając zbyt "replace" podczas przekazywania konflikt czasami spowoduje przekazywania hello uruchamiany ponownie.</span><span class="sxs-lookup"><span data-stu-id="d9aab-117">For some blob types, choosing too"replace" during an upload conflict would sometimes result in hello upload being restarted.</span></span> 
* <span data-ttu-id="d9aab-118">W wersji 0.8.15 przekazywania czasami spowoduje zatrzymania 99%.</span><span class="sxs-lookup"><span data-stu-id="d9aab-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="d9aab-119">Podczas przekazywania plików tooa udziału plików, jeśli została wybrana opcja directory tooa tooupload, która jeszcze nie istnieje, przekazania nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="d9aab-119">When uploading files tooa file share, if you chose tooupload tooa directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="d9aab-120">Eksploratora usługi Storage został niepoprawnie generowania sygnatury czasowe dla sygnatur dostępu współdzielonego i tabeli zapytania.</span><span class="sxs-lookup"><span data-stu-id="d9aab-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="d9aab-121">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-121">Known Issues</span></span>
* <span data-ttu-id="d9aab-122">Przy użyciu nazwy i parametry połączenia klucza aktualnie nie działa.</span><span class="sxs-lookup"><span data-stu-id="d9aab-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="d9aab-123">Zostanie on rozwiązany w następnej wersji hello.</span><span class="sxs-lookup"><span data-stu-id="d9aab-123">It will be fixed in hello next release.</span></span> <span data-ttu-id="d9aab-124">Do tego czasu można dołączyć z nazwy i klucza.</span><span class="sxs-lookup"><span data-stu-id="d9aab-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="d9aab-125">Jeśli spróbujesz tooopen pliku o nieprawidłowej nazwie pliku systemu Windows hello pobierania spowoduje błąd: nie odnaleziono pliku.</span><span class="sxs-lookup"><span data-stu-id="d9aab-125">If you try tooopen a file with an invalid Windows file name, hello download will result in a file not found error.</span></span>
* <span data-ttu-id="d9aab-126">Po dla zadania, klikając przycisk "Anuluj", może upłynąć trochę czasu zanim toocancel tego zadania.</span><span class="sxs-lookup"><span data-stu-id="d9aab-126">After clicking "Cancel" on a task, it may take a while for that task toocancel.</span></span> <span data-ttu-id="d9aab-127">Jest to ograniczenie hello biblioteki węzła magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d9aab-127">This is a limitation of hello Azure Storage Node library.</span></span>
* <span data-ttu-id="d9aab-128">Po zakończeniu przekazywania obiektów blob, karta hello, który zainicjował przekazywania hello jest odświeżany.</span><span class="sxs-lookup"><span data-stu-id="d9aab-128">After completing a blob upload, hello tab which initiated hello upload is refreshed.</span></span> <span data-ttu-id="d9aab-129">Zmiana z poprzednich zachowanie, a także spowoduje toobe wycofać głównego toohello kontenera hello, które znajdują się w.</span><span class="sxs-lookup"><span data-stu-id="d9aab-129">This is a change from previous behavior, and will also cause you toobe taken back toohello root of hello container you are in.</span></span>
* <span data-ttu-id="d9aab-130">Jeśli wybierzesz hello niewłaściwy kod PIN/certyfikatu karty inteligentnej, a następnie konieczne będzie toorestart w kolejności toohave Eksploratora usługi Storage zapomnij tej decyzji.</span><span class="sxs-lookup"><span data-stu-id="d9aab-130">If you choose hello wrong PIN/Smartcard certificate, then you will need toorestart in order toohave Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="d9aab-131">panel ustawień konta Hello mogą być wyświetlane, należy tooreenter poświadczenia toofilter subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d9aab-131">hello account settings panel may show that you need tooreenter credentials toofilter subscriptions.</span></span>
* <span data-ttu-id="d9aab-132">Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki.</span><span class="sxs-lookup"><span data-stu-id="d9aab-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="d9aab-133">Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.</span><span class="sxs-lookup"><span data-stu-id="d9aab-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="d9aab-134">Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu.</span><span class="sxs-lookup"><span data-stu-id="d9aab-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="d9aab-135">Dla użytkowników na Ubuntu 14.04, konieczne będzie tooensure GCC działa toodate — można to zrobić, uruchamiając hello następujące polecenia, a następnie ponownym uruchomieniu komputera:</span><span class="sxs-lookup"><span data-stu-id="d9aab-135">For users on Ubuntu 14.04, you will need tooensure GCC is up toodate - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="d9aab-136">Dla użytkowników Ubuntu 17.04 konieczne będzie tooinstall GConf — można to zrobić systemem hello następujące polecenia, a następnie ponownym uruchomieniu komputera:</span><span class="sxs-lookup"><span data-stu-id="d9aab-136">For users on Ubuntu 17.04, you will need tooinstall GConf - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="d9aab-137">Wersja 0.8.14 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d9aab-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="d9aab-138">06/22/2017</span><span class="sxs-lookup"><span data-stu-id="d9aab-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="d9aab-139">Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d9aab-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="d9aab-140">Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza) dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d9aab-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="d9aab-141">Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza) dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="d9aab-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="d9aab-142">Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza) dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="d9aab-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="d9aab-143">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-143">New</span></span>

* <span data-ttu-id="d9aab-144">Zaktualizowano too1.7.2 wersji elektronów w kolejności tootake zaletą kilka aktualizacji krytycznych</span><span class="sxs-lookup"><span data-stu-id="d9aab-144">Updated Electron version too1.7.2 in order tootake advantage of several critical security updates</span></span>
* <span data-ttu-id="d9aab-145">Teraz szybko dostępne hello online przewodnik rozwiązywania problemów z menu Pomoc hello</span><span class="sxs-lookup"><span data-stu-id="d9aab-145">You can now quickly access hello online troubleshooting guide from hello help menu</span></span>
* <span data-ttu-id="d9aab-146">Rozwiązywanie problemów z Eksploratora usługi Storage [przewodnik][2]</span><span class="sxs-lookup"><span data-stu-id="d9aab-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="d9aab-147">[Instrukcje] [ 3] łączyć się z subskrypcji Azure stosu tooan</span><span class="sxs-lookup"><span data-stu-id="d9aab-147">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="d9aab-148">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-148">Known Issues</span></span>

* <span data-ttu-id="d9aab-149">Przyciski na powitania usuwania folderu — okno dialogowe potwierdzenia nie zarejestrować kliknięć myszą hello w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="d9aab-149">Buttons on hello delete folder confirmation dialog don't register with hello mouse clicks on Linux.</span></span> <span data-ttu-id="d9aab-150">Obejście jest klawisz Enter hello toouse</span><span class="sxs-lookup"><span data-stu-id="d9aab-150">Workaround is toouse hello Enter key</span></span>
* <span data-ttu-id="d9aab-151">Jeśli wybierzesz hello niewłaściwy kod PIN/certyfikatu karty inteligentnej, a następnie konieczne będzie toorestart w kolejności toohave Eksploratora usługi Storage zapomnij hello decyzji</span><span class="sxs-lookup"><span data-stu-id="d9aab-151">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="d9aab-152">Mając więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może powodować błędy</span><span class="sxs-lookup"><span data-stu-id="d9aab-152">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="d9aab-153">panel ustawień konta Hello mogą być wyświetlane, należy tooreenter poświadczenia w kolejności toofilter subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d9aab-153">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="d9aab-154">Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki.</span><span class="sxs-lookup"><span data-stu-id="d9aab-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="d9aab-155">Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.</span><span class="sxs-lookup"><span data-stu-id="d9aab-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="d9aab-156">Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu.</span><span class="sxs-lookup"><span data-stu-id="d9aab-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="d9aab-157">Ubuntu 14.04 instalacji potrzeb wersji gcc zaktualizowane lub uaktualnione — tooupgrade kroki są poniżej:</span><span class="sxs-lookup"><span data-stu-id="d9aab-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="d9aab-158">Poprzednie wersje</span><span class="sxs-lookup"><span data-stu-id="d9aab-158">Previous releases</span></span>

* [<span data-ttu-id="d9aab-159">Wersja 0.8.13</span><span class="sxs-lookup"><span data-stu-id="d9aab-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="d9aab-160">Wersja 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="d9aab-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="d9aab-161">Wersja 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="d9aab-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="d9aab-162">Wersja 0.8.7</span><span class="sxs-lookup"><span data-stu-id="d9aab-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="d9aab-163">Wersja 0.8.6</span><span class="sxs-lookup"><span data-stu-id="d9aab-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="d9aab-164">Wersja 0.8.5</span><span class="sxs-lookup"><span data-stu-id="d9aab-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="d9aab-165">Wersja 0.8.4</span><span class="sxs-lookup"><span data-stu-id="d9aab-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="d9aab-166">Wersja 0.8.3</span><span class="sxs-lookup"><span data-stu-id="d9aab-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="d9aab-167">Wersja 0.8.2</span><span class="sxs-lookup"><span data-stu-id="d9aab-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="d9aab-168">Wersja 0.8.0</span><span class="sxs-lookup"><span data-stu-id="d9aab-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="d9aab-169">Wersja 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="d9aab-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="d9aab-170">Wersja 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="d9aab-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="d9aab-171">Wersja 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="d9aab-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="d9aab-172">Wersja 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="d9aab-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="d9aab-173">Wersja 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="d9aab-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="d9aab-174">Wersja 0.8.13</span><span class="sxs-lookup"><span data-stu-id="d9aab-174">Version 0.8.13</span></span>
<span data-ttu-id="d9aab-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="d9aab-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="d9aab-176">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-176">New</span></span>

* <span data-ttu-id="d9aab-177">Rozwiązywanie problemów z Eksploratora usługi Storage [przewodnik][2]</span><span class="sxs-lookup"><span data-stu-id="d9aab-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="d9aab-178">[Instrukcje] [ 3] łączyć się z subskrypcji Azure stosu tooan</span><span class="sxs-lookup"><span data-stu-id="d9aab-178">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-179">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-179">Fixes</span></span>

* <span data-ttu-id="d9aab-180">Stała: Przekazywanie pliku wypróbowana wysokiej spowodować błąd braku pamięci</span><span class="sxs-lookup"><span data-stu-id="d9aab-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="d9aab-181">Stały: Można teraz zalogować się przy użyciu kodu PIN/za pomocą kart inteligentnych</span><span class="sxs-lookup"><span data-stu-id="d9aab-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="d9aab-182">Stałe: Otwórz w portalu teraz współpracuje z Chińskiej wersji platformy Azure, platformy Azure w Niemczech Azure instytucji rządowych Stanów Zjednoczonych i stosu Azure</span><span class="sxs-lookup"><span data-stu-id="d9aab-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="d9aab-183">Stała: Podczas przekazywania kontenera obiektów blob tooa folderu, błąd "Niedozwolonej operacji" czasami wystąpiłyby</span><span class="sxs-lookup"><span data-stu-id="d9aab-183">Fixed: While uploading a folder tooa blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="d9aab-184">Stałej: Zaznacz wszystko zostało wyłączone podczas zarządzania migawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="d9aab-185">Stały: hello metadane obiektu blob podstawowej hello może spowodować zastąpienie po wyświetleniu właściwości hello jego migawek.</span><span class="sxs-lookup"><span data-stu-id="d9aab-185">Fixed: hello metadata of hello base blob might get overwritten after viewing hello properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d9aab-186">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-186">Known Issues</span></span>

* <span data-ttu-id="d9aab-187">Jeśli wybierzesz hello niewłaściwy kod PIN/certyfikatu karty inteligentnej, a następnie konieczne będzie toorestart w kolejności toohave Eksploratora usługi Storage zapomnij hello decyzji</span><span class="sxs-lookup"><span data-stu-id="d9aab-187">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="d9aab-188">Gdy jest powiększony przychodzący lub wychodzący, poziom powiększenia hello na chwilę może zresetować toohello domyślny poziom</span><span class="sxs-lookup"><span data-stu-id="d9aab-188">While zoomed in or out, hello zoom level may momentarily reset toohello default level</span></span>
* <span data-ttu-id="d9aab-189">Mając więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może powodować błędy</span><span class="sxs-lookup"><span data-stu-id="d9aab-189">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="d9aab-190">panel ustawień konta Hello mogą być wyświetlane, należy tooreenter poświadczenia w kolejności toofilter subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d9aab-190">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="d9aab-191">Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki.</span><span class="sxs-lookup"><span data-stu-id="d9aab-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="d9aab-192">Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.</span><span class="sxs-lookup"><span data-stu-id="d9aab-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="d9aab-193">Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu.</span><span class="sxs-lookup"><span data-stu-id="d9aab-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="d9aab-194">Ubuntu 14.04 instalacji potrzeb wersji gcc zaktualizowane lub uaktualnione — tooupgrade kroki są poniżej:</span><span class="sxs-lookup"><span data-stu-id="d9aab-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="d9aab-195">Wersja 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="d9aab-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="d9aab-196">04/07/2017</span><span class="sxs-lookup"><span data-stu-id="d9aab-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="d9aab-197">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-197">New</span></span>

* <span data-ttu-id="d9aab-198">Eksplorator usługi Storage teraz zostanie automatycznie zamknięte podczas instalacji aktualizacji z hello powiadomienie o aktualizacji</span><span class="sxs-lookup"><span data-stu-id="d9aab-198">Storage Explorer will now automatically close when you install an update from hello update notification</span></span>
* <span data-ttu-id="d9aab-199">Szybki dostęp w miejscu udostępnia udoskonalone środowisko do pracy z często używanych zasobów</span><span class="sxs-lookup"><span data-stu-id="d9aab-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="d9aab-200">W edytorze kontenera obiektów Blob hello możesz teraz przeglądać maszyny wirtualnej, które dzierżawionych obiektu blob należy do</span><span class="sxs-lookup"><span data-stu-id="d9aab-200">In hello Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="d9aab-201">Teraz można zwinąć powitania po lewej stronie panelu</span><span class="sxs-lookup"><span data-stu-id="d9aab-201">You can now collapse hello left side panel</span></span>
* <span data-ttu-id="d9aab-202">Odnajdywanie teraz działa na powitania sam czas pobrania</span><span class="sxs-lookup"><span data-stu-id="d9aab-202">Discovery now runs at hello same time as download</span></span>
* <span data-ttu-id="d9aab-203">Statystyk użycia w hello kontenera obiektów Blob, udziału plików, a tabela edytory toosee hello rozmiar zasobu lub zaznaczenia</span><span class="sxs-lookup"><span data-stu-id="d9aab-203">Use Statistics in hello Blob Container, File Share, and Table editors toosee hello size of your resource or selection</span></span>
* <span data-ttu-id="d9aab-204">Możesz teraz tooAzure logowania w usłudze Active Directory (AAD) na podstawie konta Azure stosu.</span><span class="sxs-lookup"><span data-stu-id="d9aab-204">You can now sign-in tooAzure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="d9aab-205">Można teraz archiwum przekazywania plików ponad 32 MB tooPremium magazynu kont</span><span class="sxs-lookup"><span data-stu-id="d9aab-205">You can now upload archive files over 32MB tooPremium storage accounts</span></span>
* <span data-ttu-id="d9aab-206">Udoskonalona obsługa ułatwień dostępu</span><span class="sxs-lookup"><span data-stu-id="d9aab-206">Improved accessibility support</span></span>
* <span data-ttu-id="d9aab-207">Można teraz dodawać zaufanych Base-64 zakodowane certyfikatów X.509 SSL przez przejście tooEdit -&gt; certyfikaty SSL -&gt; importu certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d9aab-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going tooEdit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-208">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-208">Fixes</span></span>

* <span data-ttu-id="d9aab-209">Stały: po odświeżeniu poświadczenia konta, widok drzewa hello czy czasami nie automatycznie odświeżenia</span><span class="sxs-lookup"><span data-stu-id="d9aab-209">Fixed: after refreshing an account's credentials, hello tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="d9aab-210">Stała: Generowanie sygnatury dostępu Współdzielonego dla kolejki emulatora i tabele dadzą w wyniku nieprawidłowy adres URL</span><span class="sxs-lookup"><span data-stu-id="d9aab-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="d9aab-211">Stały: konta premium magazynu teraz można rozszerzyć, gdy włączone jest serwer proxy</span><span class="sxs-lookup"><span data-stu-id="d9aab-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="d9aab-212">Stała: hello przycisk Zastosuj na powitania konta, które strony zarządzania nie będzie działać, jeśli masz 1 lub 0 konta zaznaczone</span><span class="sxs-lookup"><span data-stu-id="d9aab-212">Fixed: hello apply button on hello accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="d9aab-213">Stały: przekazywanie obiektów blob, które wymagają rozwiązania konfliktu może zakończyć się niepowodzeniem — stała 0.8.11</span><span class="sxs-lookup"><span data-stu-id="d9aab-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="d9aab-214">Stałe: wysyłanie opinii został przerwany w 0.8.11 — stała 0.8.12</span><span class="sxs-lookup"><span data-stu-id="d9aab-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="d9aab-215">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-215">Known Issues</span></span>

* <span data-ttu-id="d9aab-216">Po uaktualnieniu too0.8.10, konieczne będzie toorefresh wszystkie swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="d9aab-216">After upgrading too0.8.10, you will need toorefresh all of your credentials.</span></span>
* <span data-ttu-id="d9aab-217">Gdy jest powiększony przychodzący lub wychodzący, poziom powiększenia hello na chwilę może zresetować toohello domyślny poziom.</span><span class="sxs-lookup"><span data-stu-id="d9aab-217">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="d9aab-218">Więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może spowodować błędy.</span><span class="sxs-lookup"><span data-stu-id="d9aab-218">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>
* <span data-ttu-id="d9aab-219">panel ustawień konta Hello mogą być wyświetlane, należy tooreenter poświadczenia w kolejności toofilter subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d9aab-219">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions.</span></span>
* <span data-ttu-id="d9aab-220">Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki.</span><span class="sxs-lookup"><span data-stu-id="d9aab-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="d9aab-221">Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.</span><span class="sxs-lookup"><span data-stu-id="d9aab-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="d9aab-222">Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu.</span><span class="sxs-lookup"><span data-stu-id="d9aab-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="d9aab-223">Ubuntu 14.04 instalacji potrzeb wersji gcc zaktualizowane lub uaktualnione — tooupgrade kroki są poniżej:</span><span class="sxs-lookup"><span data-stu-id="d9aab-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="d9aab-224">Wersja 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="d9aab-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="d9aab-225">02/23/2017</span><span class="sxs-lookup"><span data-stu-id="d9aab-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="d9aab-226">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-226">New</span></span>

* <span data-ttu-id="d9aab-227">Eksplorator usługi Storage 0.8.9 będzie automatycznie pobierał hello najnowszej wersji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="d9aab-227">Storage Explorer 0.8.9 will automatically download hello latest version for updates.</span></span>
* <span data-ttu-id="d9aab-228">Poprawka: przy użyciu portalu sieci generowane tooattach identyfikatora URI połączenia SAS, konto magazynu może spowodować błąd.</span><span class="sxs-lookup"><span data-stu-id="d9aab-228">Hotfix: using a portal generated SAS URI tooattach a storage account would result in an error.</span></span>
* <span data-ttu-id="d9aab-229">Teraz można tworzyć, zarządzanie i wspierania migawki obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d9aab-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="d9aab-230">Można teraz zalogować konta tooAzure Chin, platformy Azure w Niemczech i Azure instytucji rządowych Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="d9aab-230">You can now sign in tooAzure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="d9aab-231">Można teraz zmienić poziom powiększenia hello.</span><span class="sxs-lookup"><span data-stu-id="d9aab-231">You can now change hello zoom level.</span></span> <span data-ttu-id="d9aab-232">Użyj opcji hello w tooZoom menu Widok hello Pomniejsz i zresetować powiększenie.</span><span class="sxs-lookup"><span data-stu-id="d9aab-232">Use hello options in hello View menu tooZoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="d9aab-233">Znaki Unicode są teraz obsługiwane w metadanych użytkownika do obiektów blob i plików.</span><span class="sxs-lookup"><span data-stu-id="d9aab-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="d9aab-234">Zwiększona dostępność.</span><span class="sxs-lookup"><span data-stu-id="d9aab-234">Accessibility improvements.</span></span>
* <span data-ttu-id="d9aab-235">informacje o wersji Hello następnej wersji mogą być wyświetlane z hello powiadomienie o aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="d9aab-235">hello next version's release notes can be viewed from hello update notification.</span></span> <span data-ttu-id="d9aab-236">Można również wyświetlić hello bieżącej wersji hello menu Pomoc.</span><span class="sxs-lookup"><span data-stu-id="d9aab-236">You can also view hello current release notes from hello Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-237">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-237">Fixes</span></span>

* <span data-ttu-id="d9aab-238">Stały: numer wersji hello jest teraz prawidłowo wyświetlany w Panelu sterowania w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="d9aab-238">Fixed: hello version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="d9aab-239">Stałe: wyszukiwania nie jest już ograniczona too50, 000 węzłów</span><span class="sxs-lookup"><span data-stu-id="d9aab-239">Fixed: search is no longer limited too50,000 nodes</span></span>
* <span data-ttu-id="d9aab-240">Stały: udział plików tooa przekazywania wykonana nieskończona Jeśli hello katalog docelowy już nie istnieje</span><span class="sxs-lookup"><span data-stu-id="d9aab-240">Fixed: upload tooa file share spun forever if hello destination directory did not already exist</span></span>
* <span data-ttu-id="d9aab-241">Stały: lepszą stabilność dla długich przekazywania i pobierania</span><span class="sxs-lookup"><span data-stu-id="d9aab-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d9aab-242">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-242">Known Issues</span></span>

* <span data-ttu-id="d9aab-243">Gdy jest powiększony przychodzący lub wychodzący, poziom powiększenia hello na chwilę może zresetować toohello domyślny poziom.</span><span class="sxs-lookup"><span data-stu-id="d9aab-243">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="d9aab-244">Szybki dostęp działa tylko z elementami subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d9aab-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="d9aab-245">Zasobów lokalnych lub zasobów dołączonych za pomocą klucza lub tokenu sygnatury dostępu Współdzielonego nie są obsługiwane w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="d9aab-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="d9aab-246">Może potrwać kilka sekund toonavigate toohello zasobu docelowego, w zależności od liczby zasobów, należy mieć szybki dostęp.</span><span class="sxs-lookup"><span data-stu-id="d9aab-246">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="d9aab-247">Więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może spowodować błędy.</span><span class="sxs-lookup"><span data-stu-id="d9aab-247">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>

<span data-ttu-id="d9aab-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="d9aab-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="d9aab-249">Wersja 0.8.7</span><span class="sxs-lookup"><span data-stu-id="d9aab-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="d9aab-250">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-250">New</span></span>

* <span data-ttu-id="d9aab-251">Można wybrać sposób tooresolve konfliktów na początku hello aktualizacji, Pobierz lub skopiuj sesji w oknie działania hello</span><span class="sxs-lookup"><span data-stu-id="d9aab-251">You can choose how tooresolve conflicts at hello beginning of an update, download or copy session in hello Activities window</span></span>
* <span data-ttu-id="d9aab-252">Umieść kursor nad kartę toosee hello pełną ścieżkę hello zasobu magazynu</span><span class="sxs-lookup"><span data-stu-id="d9aab-252">Hover over a tab toosee hello full path of hello storage resource</span></span>
* <span data-ttu-id="d9aab-253">Po kliknięciu na karcie synchronizacji z lokalizacji, w okienku nawigacji po lewej stronie powitania</span><span class="sxs-lookup"><span data-stu-id="d9aab-253">When you click on a tab, it synchronizes with its location in hello left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-254">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-254">Fixes</span></span>

* <span data-ttu-id="d9aab-255">Stały: Eksploratora usługi Storage jest teraz zaufanych aplikacji dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="d9aab-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="d9aab-256">Stały: Ubuntu 14.04 jest ponownie obsługiwane</span><span class="sxs-lookup"><span data-stu-id="d9aab-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="d9aab-257">Stały: Czasami hello Dodaj konto, które miga interfejsu użytkownika podczas ładowania subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d9aab-257">Fixed: Sometimes hello add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="d9aab-258">Stały: Czasami nie wszystkie zasoby magazynu zostały wymienione w okienku nawigacji po lewej stronie powitania</span><span class="sxs-lookup"><span data-stu-id="d9aab-258">Fixed: Sometimes not all storage resources were listed in hello left side navigation pane</span></span>
* <span data-ttu-id="d9aab-259">Stały: hello w okienku akcji czasami wyświetlane akcje pusty</span><span class="sxs-lookup"><span data-stu-id="d9aab-259">Fixed: hello action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="d9aab-260">Stały: rozmiar okna hello z hello ostatniego zamknięcia sesji są teraz przechowywane</span><span class="sxs-lookup"><span data-stu-id="d9aab-260">Fixed: hello window size from hello last closed session is now retained</span></span>
* <span data-ttu-id="d9aab-261">Stałe: Można otworzyć wiele kart dla hello tego samego zasobu za pomocą menu kontekstowe hello</span><span class="sxs-lookup"><span data-stu-id="d9aab-261">Fixed: You can open multiple tabs for hello same resource using hello context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d9aab-262">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-262">Known Issues</span></span>

* <span data-ttu-id="d9aab-263">Szybki dostęp działa tylko z elementami subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d9aab-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="d9aab-264">Zasobów lokalnych lub dołączonych za pomocą klucza lub tokenu sygnatury dostępu Współdzielonego zasobów nie są obsługiwane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="d9aab-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="d9aab-265">Szybki dostęp może potrwać kilka sekund toonavigate toohello zasobu docelowego, w zależności od liczby zasobów, masz</span><span class="sxs-lookup"><span data-stu-id="d9aab-265">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="d9aab-266">Mając więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może powodować błędy</span><span class="sxs-lookup"><span data-stu-id="d9aab-266">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="d9aab-267">Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 — po to, może to mieć wpływ na wydajność lub może spowodować nieobsługiwany wyjątek</span><span class="sxs-lookup"><span data-stu-id="d9aab-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="d9aab-268">Dla hello pierwsze logowanie przy użyciu Eksploratora usługi Storage hello na macOS, może pojawić się wiele wyświetla monit podanie łańcucha kluczy tooaccess uprawnień użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d9aab-268">For hello first time using hello Storage Explorer on macOS, you might see multiple prompts asking for user's permission tooaccess keychain.</span></span> <span data-ttu-id="d9aab-269">Zalecamy użycie wybierz zawsze Zezwalaj tak hello wiersza nie będą widoczne ponownie</span><span class="sxs-lookup"><span data-stu-id="d9aab-269">We suggest you select Always Allow so hello prompt won't show up again</span></span>

<span data-ttu-id="d9aab-270">11/18/2016</span><span class="sxs-lookup"><span data-stu-id="d9aab-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="d9aab-271">Wersja 0.8.6</span><span class="sxs-lookup"><span data-stu-id="d9aab-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="d9aab-272">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-272">New</span></span>

* <span data-ttu-id="d9aab-273">Można teraz numer pin najczęściej używane usług toohello szybki dostęp do ułatwienia nawigacji</span><span class="sxs-lookup"><span data-stu-id="d9aab-273">You can now pin most frequently used services toohello Quick Access for easy navigation</span></span>
* <span data-ttu-id="d9aab-274">Teraz możesz otworzyć wiele edytorów na różnych kartach.</span><span class="sxs-lookup"><span data-stu-id="d9aab-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="d9aab-275">Jednym kliknięciem tooopen kartę tymczasowego; Kliknij dwukrotnie pozycję tooopen kartę trwałych. Możesz również kliknąć na toomake tymczasowego kartę hello go stałe kartę</span><span class="sxs-lookup"><span data-stu-id="d9aab-275">Single click tooopen a temporary tab; double click tooopen a permanent tab. You can also click on hello temporary tab toomake it a permanent tab</span></span>
* <span data-ttu-id="d9aab-276">Wprowadziliśmy zauważalna zmiana wydajności i stabilności ulepszenia przekazywania i pobierania, zwłaszcza w przypadku dużych plików na maszynach fast</span><span class="sxs-lookup"><span data-stu-id="d9aab-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="d9aab-277">Teraz można tworzyć foldery "wirtualne" pusta w kontenerów obiektów blob</span><span class="sxs-lookup"><span data-stu-id="d9aab-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="d9aab-278">Ma ponownie wprowadzono ukierunkowane wyszukiwanie z naszego nowego wyszukiwania podciągu rozszerzonego, teraz są dwie opcje wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="d9aab-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="d9aab-279">Globalne wyszukiwanie - w hello tekstowym wyszukiwania wpisz wyszukiwany termin</span><span class="sxs-lookup"><span data-stu-id="d9aab-279">Global search - just enter a search term into hello search textbox</span></span>
    * <span data-ttu-id="d9aab-280">Wyszukiwania zakresowego - kliknij hello Lupa ikona następnego tooa węzła, a następnie dodaj końcu toohello terminu wyszukiwania ścieżki hello, lub kliknij prawym przyciskiem myszy i wybierz pozycję "Wyszukiwania z tutaj"</span><span class="sxs-lookup"><span data-stu-id="d9aab-280">Scoped search - click hello magnifying glass icon next tooa node, then add a search term toohello end of hello path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="d9aab-281">Dodano różne kompozycje: jasny (ustawienie domyślne), ciemny, wysoki kontrast czarne i wysoki kontrast biały.</span><span class="sxs-lookup"><span data-stu-id="d9aab-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="d9aab-282">Przejdź tooEdit -&gt; toochange motywów preferencje motywów</span><span class="sxs-lookup"><span data-stu-id="d9aab-282">Go tooEdit -&gt; Themes toochange your theming preference</span></span>
* <span data-ttu-id="d9aab-283">Można zmodyfikować właściwości obiektów Blob i plików</span><span class="sxs-lookup"><span data-stu-id="d9aab-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="d9aab-284">Firma Microsoft obsługuje teraz zakodowanego (base64) i niekodowany kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="d9aab-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="d9aab-285">W systemie Linux, 64-bitowego systemu operacyjnego jest teraz wymagane.</span><span class="sxs-lookup"><span data-stu-id="d9aab-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="d9aab-286">W tej wersji obsługiwany jest tylko 64-bitowych Ubuntu 16.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="d9aab-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="d9aab-287">Zaktualizowaliśmy naszych logo!</span><span class="sxs-lookup"><span data-stu-id="d9aab-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-288">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-288">Fixes</span></span>

* <span data-ttu-id="d9aab-289">Stała: Ekranu zamrożenia problemów</span><span class="sxs-lookup"><span data-stu-id="d9aab-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="d9aab-290">Stały: Zwiększonych zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="d9aab-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="d9aab-291">Stałe: Może być czasami zduplikowane dołączonego konta</span><span class="sxs-lookup"><span data-stu-id="d9aab-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="d9aab-292">Stały: Obiektów blob z niezdefiniowanego typu zawartości można wygenerować wyjątek</span><span class="sxs-lookup"><span data-stu-id="d9aab-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="d9aab-293">Stały: Hello otwierania panelu zapytania na pusta tabela nie było możliwe</span><span class="sxs-lookup"><span data-stu-id="d9aab-293">Fixed: Opening hello Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="d9aab-294">Stały: Zmienia się usterki podczas wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d9aab-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="d9aab-295">Stały: Zwiększenie hello liczby zasobów, załadowane z 50 too100 po kliknięciu przycisku "Obciążenia więcej"</span><span class="sxs-lookup"><span data-stu-id="d9aab-295">Fixed: Increased hello number of resources loaded from 50 too100 when clicking "Load More"</span></span>
* <span data-ttu-id="d9aab-296">Stałe: Przy pierwszym uruchomieniu, jeśli konto jest podpisana, możemy teraz wybrać wszystkie subskrypcje dla tego konta domyślnie</span><span class="sxs-lookup"><span data-stu-id="d9aab-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="d9aab-297">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-297">Known Issues</span></span>

* <span data-ttu-id="d9aab-298">Ta wersja hello Eksploratora magazynu nie działa w Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="d9aab-298">This release of hello Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="d9aab-299">tooopen wielu kartach powitania kliknij tego samego zasobu nie stale czy hello tego samego zasobu.</span><span class="sxs-lookup"><span data-stu-id="d9aab-299">tooopen multiple tabs for hello same resource, do not continuously click on hello same resource.</span></span> <span data-ttu-id="d9aab-300">Kliknij na inny zasób i następnie wrócić do poprzedniej strony i kliknij przycisk na powitania oryginalnego tooopen zasobów go ponownie w innej karty</span><span class="sxs-lookup"><span data-stu-id="d9aab-300">Click on another resource and then go back and then click on hello original resource tooopen it again in another tab</span></span> 
* <span data-ttu-id="d9aab-301">Szybki dostęp działa tylko z elementami subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d9aab-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="d9aab-302">Zasobów lokalnych lub dołączonych za pomocą klucza lub tokenu sygnatury dostępu Współdzielonego zasobów nie są obsługiwane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="d9aab-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="d9aab-303">Szybki dostęp może potrwać kilka sekund toonavigate toohello zasobu docelowego, w zależności od liczby zasobów, masz</span><span class="sxs-lookup"><span data-stu-id="d9aab-303">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="d9aab-304">Mając więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może powodować błędy</span><span class="sxs-lookup"><span data-stu-id="d9aab-304">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="d9aab-305">Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 — po to, może to mieć wpływ na wydajność lub może spowodować nieobsługiwany wyjątek</span><span class="sxs-lookup"><span data-stu-id="d9aab-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="d9aab-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="d9aab-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="d9aab-307">Wersja 0.8.5</span><span class="sxs-lookup"><span data-stu-id="d9aab-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="d9aab-308">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-308">New</span></span>

* <span data-ttu-id="d9aab-309">Można teraz Użyj generowanych przez Portal SAS kluczy tooattach tooStorage kont i zasobów</span><span class="sxs-lookup"><span data-stu-id="d9aab-309">Can now use Portal-generated SAS keys tooattach tooStorage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-310">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-310">Fixes</span></span>

* <span data-ttu-id="d9aab-311">Stała: wyścigu podczas wyszukiwania czasami spowodował toobecome węzłów z systemem innym niż rozwijania</span><span class="sxs-lookup"><span data-stu-id="d9aab-311">Fixed: race condition during search sometimes caused nodes toobecome non-expandable</span></span>
* <span data-ttu-id="d9aab-312">Stałych: "Użyj protokołu HTTP" nie działa, gdy połączenie tooStorage kont z nazwą konta i klucz</span><span class="sxs-lookup"><span data-stu-id="d9aab-312">Fixed: "Use HTTP" doesn't work when connecting tooStorage Accounts with account name and key</span></span>
* <span data-ttu-id="d9aab-313">Stały: Klucze SAS (wygenerowany specjalnie portalu te) zwracają błąd "ukośnikiem na końcu"</span><span class="sxs-lookup"><span data-stu-id="d9aab-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="d9aab-314">Stały: Importowanie tabeli problemów</span><span class="sxs-lookup"><span data-stu-id="d9aab-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="d9aab-315">Czasami klucz partycji i klucz wiersza zostały cofnięte</span><span class="sxs-lookup"><span data-stu-id="d9aab-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="d9aab-316">Nie można tooread "null" kluczy partycji</span><span class="sxs-lookup"><span data-stu-id="d9aab-316">Unable tooread "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d9aab-317">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-317">Known Issues</span></span>

* <span data-ttu-id="d9aab-318">Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 -, wydajność może mieć wpływ na</span><span class="sxs-lookup"><span data-stu-id="d9aab-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="d9aab-319">Stos Azure aktualnie nie obsługuje plików, więc tooexpand plików w trakcie wyświetli błąd</span><span class="sxs-lookup"><span data-stu-id="d9aab-319">Azure Stack doesn't currently support Files, so trying tooexpand Files will show an error</span></span>

<span data-ttu-id="d9aab-320">09/12/2016</span><span class="sxs-lookup"><span data-stu-id="d9aab-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="d9aab-321">Wersja 0.8.4</span><span class="sxs-lookup"><span data-stu-id="d9aab-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="d9aab-322">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-322">New</span></span>

* <span data-ttu-id="d9aab-323">Generowanie linki bezpośrednie toostorage kont, kontenerów, kolejek, tabel, lub udziały plików do udostępniania i łatwo uzyskiwać dostęp do zasobów tooyour - systemu Windows i obsługi systemu Mac OS</span><span class="sxs-lookup"><span data-stu-id="d9aab-323">Generate direct links toostorage accounts, containers, queues, tables, or file shares for sharing and easy access tooyour resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="d9aab-324">Wyszukaj kontenerów obiektów blob, tabel, kolejek, udziałów plików lub kont magazynu w polu wyszukiwania hello</span><span class="sxs-lookup"><span data-stu-id="d9aab-324">Search for your blob containers, tables, queues, file shares, or storage accounts from hello search box</span></span>
* <span data-ttu-id="d9aab-325">Teraz można pogrupować klauzul konstruktora zapytań hello tabeli</span><span class="sxs-lookup"><span data-stu-id="d9aab-325">You can now group clauses in hello table query builder</span></span>
* <span data-ttu-id="d9aab-326">Zmień nazwę i kopiowania/wklejania kontenerów obiektów blob, udziałów plików, tabel, obiektów blob, obiektów blob folderów, plików i katalogów z wewnątrz dołączone sygnatury dostępu Współdzielonego konta i kontenerów</span><span class="sxs-lookup"><span data-stu-id="d9aab-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="d9aab-327">Zmiana nazwy i kopiowania obiektu blob kontenery i udziały plików teraz zachować właściwości i metadane</span><span class="sxs-lookup"><span data-stu-id="d9aab-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-328">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-328">Fixes</span></span>

* <span data-ttu-id="d9aab-329">Stały: nie można edytować jednostek tabeli, gdy właściwości boolean lub binarne</span><span class="sxs-lookup"><span data-stu-id="d9aab-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d9aab-330">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-330">Known Issues</span></span>

* <span data-ttu-id="d9aab-331">Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 -, wydajność może mieć wpływ na</span><span class="sxs-lookup"><span data-stu-id="d9aab-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="d9aab-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="d9aab-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="d9aab-333">Wersja 0.8.3</span><span class="sxs-lookup"><span data-stu-id="d9aab-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="d9aab-334">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-334">New</span></span>

* <span data-ttu-id="d9aab-335">Zmień nazwę kontenerów, tabel, udziałów plików</span><span class="sxs-lookup"><span data-stu-id="d9aab-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="d9aab-336">Udoskonalone środowisko konstruktora zapytań</span><span class="sxs-lookup"><span data-stu-id="d9aab-336">Improved Query builder experience</span></span>
* <span data-ttu-id="d9aab-337">Możliwości toosave i ładowanie zapytań</span><span class="sxs-lookup"><span data-stu-id="d9aab-337">Ability toosave and load queries</span></span>
* <span data-ttu-id="d9aab-338">Bezpośrednie łącza toostorage kont lub kontenery, kolejek, tabel lub udziały do udostępniania i łatwe uzyskiwanie dostępu do zasobów plików (tylko Windows - macOS obsługuje wkrótce!)</span><span class="sxs-lookup"><span data-stu-id="d9aab-338">Direct links toostorage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="d9aab-339">Możliwość toomanage i skonfigurować zasady CORS</span><span class="sxs-lookup"><span data-stu-id="d9aab-339">Ability toomanage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-340">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-340">Fixes</span></span>

* <span data-ttu-id="d9aab-341">Stały: Accounts Microsoft wymagają ponowne uwierzytelnianie co 8 – 12 godzin</span><span class="sxs-lookup"><span data-stu-id="d9aab-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d9aab-342">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-342">Known Issues</span></span>

* <span data-ttu-id="d9aab-343">Czasami hello interfejsu użytkownika mogą sprawiać wrażenie — maksymalizacja okna hello pomaga rozwiązać ten problem</span><span class="sxs-lookup"><span data-stu-id="d9aab-343">Sometimes hello UI might appear frozen - maximizing hello window helps resolve this issue</span></span>
* <span data-ttu-id="d9aab-344">System macOS instalacji może wymagać podniesionego poziomu uprawnień</span><span class="sxs-lookup"><span data-stu-id="d9aab-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="d9aab-345">Panel ustawień konta mogą być wyświetlane, należy tooreenter poświadczenia w kolejności toofilter subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d9aab-345">Account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="d9aab-346">Zmiana nazwy udziałów plików, kontenerów obiektów blob i tabele nie zachowuje metadane lub innych właściwości w kontenerze hello, takie jak przydziału udziału plików, poziom dostępu publicznego lub zasady dostępu</span><span class="sxs-lookup"><span data-stu-id="d9aab-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on hello container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="d9aab-347">Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki.</span><span class="sxs-lookup"><span data-stu-id="d9aab-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="d9aab-348">Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy</span><span class="sxs-lookup"><span data-stu-id="d9aab-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="d9aab-349">Kopiowanie lub zmiana nazwy zasobów nie działa w ramach konta dołączone sygnatury dostępu Współdzielonego</span><span class="sxs-lookup"><span data-stu-id="d9aab-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="d9aab-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="d9aab-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="d9aab-351">Wersja 0.8.2</span><span class="sxs-lookup"><span data-stu-id="d9aab-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="d9aab-352">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-352">New</span></span>

* <span data-ttu-id="d9aab-353">Konta magazynu są pogrupowane według subskrypcji; Programowanie magazynu i zasobów dołączonych za pomocą klucza lub SAS są wyświetlane w węźle (lokalny i załączone)</span><span class="sxs-lookup"><span data-stu-id="d9aab-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="d9aab-354">Wyloguj z konta w panelu "Ustawienia konta Azure"</span><span class="sxs-lookup"><span data-stu-id="d9aab-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="d9aab-355">Konfigurowanie tooenable ustawienia serwera proxy i zarządzanie nimi logowania</span><span class="sxs-lookup"><span data-stu-id="d9aab-355">Configure proxy settings tooenable and manage sign-in</span></span>
* <span data-ttu-id="d9aab-356">Tworzenie i przerwać dzierżawy obiektów blob</span><span class="sxs-lookup"><span data-stu-id="d9aab-356">Create and break blob leases</span></span>
* <span data-ttu-id="d9aab-357">Kontenery Otwórz obiektów blob, kolejek, tabel i pliki z jednym kliknięciem</span><span class="sxs-lookup"><span data-stu-id="d9aab-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-358">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-358">Fixes</span></span>

* <span data-ttu-id="d9aab-359">Stała: dodaje z bibliotekami .NET lub Java wiadomości w kolejce są nie prawidłowo zdekodować z formatu base64</span><span class="sxs-lookup"><span data-stu-id="d9aab-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="d9aab-360">Stały: $metrics tabele nie są wyświetlane w przypadku kont magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="d9aab-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="d9aab-361">Stały: węzeł tabele nie działa dla lokalnej pamięci masowej (Programowanie)</span><span class="sxs-lookup"><span data-stu-id="d9aab-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d9aab-362">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-362">Known Issues</span></span>

* <span data-ttu-id="d9aab-363">System macOS instalacji może wymagać podniesionego poziomu uprawnień</span><span class="sxs-lookup"><span data-stu-id="d9aab-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="d9aab-364">06/15/2016</span><span class="sxs-lookup"><span data-stu-id="d9aab-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="d9aab-365">Wersja 0.8.0</span><span class="sxs-lookup"><span data-stu-id="d9aab-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="d9aab-366">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-366">New</span></span>

* <span data-ttu-id="d9aab-367">Obsługa udziału plików: wyświetlanie, przekazywanie, pobieranie, kopiowania plików i katalogów, identyfikatory URI SAS (Tworzenie i łączenie)</span><span class="sxs-lookup"><span data-stu-id="d9aab-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="d9aab-368">Udoskonalona obsługa łączenie tooStorage identyfikatorów URI SAS lub klucze konta</span><span class="sxs-lookup"><span data-stu-id="d9aab-368">Improved user experience for connecting tooStorage with SAS URIs or account keys</span></span>
* <span data-ttu-id="d9aab-369">Eksportowanie tabeli wyników zapytania</span><span class="sxs-lookup"><span data-stu-id="d9aab-369">Export table query results</span></span>
* <span data-ttu-id="d9aab-370">Zmienianie kolejności kolumn w tabeli i dostosowywania</span><span class="sxs-lookup"><span data-stu-id="d9aab-370">Table column reordering and customization</span></span>
* <span data-ttu-id="d9aab-371">Wyświetlanie $logs kontenerów obiektów blob i tabelach $metrics dla konta magazynu o metryki włączone</span><span class="sxs-lookup"><span data-stu-id="d9aab-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="d9aab-372">Ulepszone eksportowania i importowania zachowanie, zawiera teraz typ wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="d9aab-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-373">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-373">Fixes</span></span>

* <span data-ttu-id="d9aab-374">Stały: przekazanie lub pobranie dużych obiektów blob może spowodować niekompletne przekazywania/pobieranie</span><span class="sxs-lookup"><span data-stu-id="d9aab-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="d9aab-375">Stały: Edycja, dodanie lub zaimportowanie jednostki z wartością liczbową ciągu ("1") spowoduje to przekonwertowanie go toodouble</span><span class="sxs-lookup"><span data-stu-id="d9aab-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it toodouble</span></span>
* <span data-ttu-id="d9aab-376">Stały: Tooexpand hello tabeli w węźle hello lokalne Środowisko deweloperskie</span><span class="sxs-lookup"><span data-stu-id="d9aab-376">Fixed: Unable tooexpand hello table node in hello local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d9aab-377">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-377">Known Issues</span></span>

* <span data-ttu-id="d9aab-378">$metrics tabele nie są widoczne dla kont magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="d9aab-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="d9aab-379">Wiadomości w kolejce dodać programistycznie mogą nie być wyświetlane prawidłowo, jeśli wiadomości powitania są zakodowane przy użyciu kodowania Base64</span><span class="sxs-lookup"><span data-stu-id="d9aab-379">Queue messages added programmatically may not be displayed correctly if hello messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="d9aab-380">05/17/2016</span><span class="sxs-lookup"><span data-stu-id="d9aab-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="d9aab-381">Wersja 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="d9aab-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="d9aab-382">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-382">New</span></span>

* <span data-ttu-id="d9aab-383">Awarie lepszą obsługę błędów dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="d9aab-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-384">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-384">Fixes</span></span>

* <span data-ttu-id="d9aab-385">Usunięte usterki gdzie komunikaty paska informacyjnego czasami nie są wyświetlane podczas logowania były wymagane</span><span class="sxs-lookup"><span data-stu-id="d9aab-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d9aab-386">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-386">Known Issues</span></span>

* <span data-ttu-id="d9aab-387">Tabele: Dodawanie, edytowanie, lub importowanie jednostki, która ma właściwość z wartością ambiguously liczbowego, takie jak "1" lub "1.0" i hello toosend prób użytkownika jako `Edm.String`, wartość hello będzie Wróć za pośrednictwem powitania klienta interfejsu API jako Edm.Double</span><span class="sxs-lookup"><span data-stu-id="d9aab-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>

<span data-ttu-id="d9aab-388">03/31/2016</span><span class="sxs-lookup"><span data-stu-id="d9aab-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="d9aab-389">Wersja 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="d9aab-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="d9aab-390">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-390">New</span></span>

* <span data-ttu-id="d9aab-391">Tabela wsparcia: przeglądanie, wyszukiwanie, eksportu, importowania i operacji CRUD dla jednostek</span><span class="sxs-lookup"><span data-stu-id="d9aab-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="d9aab-392">Kolejka pomocy technicznej: przeglądanie, dodawanie dequeueing wiadomości</span><span class="sxs-lookup"><span data-stu-id="d9aab-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="d9aab-393">Generowanie identyfikatorów URI sygnatury dostępu Współdzielonego dla konta magazynu</span><span class="sxs-lookup"><span data-stu-id="d9aab-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="d9aab-394">Łączenie kont tooStorage identyfikatory URI sygnatury dostępu Współdzielonego</span><span class="sxs-lookup"><span data-stu-id="d9aab-394">Connecting tooStorage Accounts with SAS URIs</span></span>
* <span data-ttu-id="d9aab-395">Powiadomienia o aktualizacji dla przyszłych aktualizacji tooStorage Explorer</span><span class="sxs-lookup"><span data-stu-id="d9aab-395">Update notifications for future updates tooStorage Explorer</span></span>
* <span data-ttu-id="d9aab-396">Zaktualizowano wygląd i działanie</span><span class="sxs-lookup"><span data-stu-id="d9aab-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-397">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-397">Fixes</span></span>

* <span data-ttu-id="d9aab-398">Ulepszenia wydajności i niezawodności</span><span class="sxs-lookup"><span data-stu-id="d9aab-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="d9aab-399">Znane problemy &amp; środki zaradcze</span><span class="sxs-lookup"><span data-stu-id="d9aab-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="d9aab-400">Pobieranie plików dużych obiektów blob nie działa prawidłowo — zaleca się używanie AzCopy, podczas gdy ten problem można rozwiązać</span><span class="sxs-lookup"><span data-stu-id="d9aab-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="d9aab-401">Poświadczenia konta nie zostaną pobrane ani hello folder macierzysty nie można odnaleźć lub nie można zapisać w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="d9aab-401">Account credentials will not be retrieved nor cached if hello home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="d9aab-402">Jeśli firma Microsoft Dodawanie, edytowanie lub importowanie jednostki, która ma właściwość z wartością ambiguously liczbowego, takie jak "1" lub "1.0" i hello użytkownik spróbuje toosend go jako `Edm.String`, wartość hello będzie Wróć za pośrednictwem powitania klienta interfejsu API jako Edm.Double</span><span class="sxs-lookup"><span data-stu-id="d9aab-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>
* <span data-ttu-id="d9aab-403">Podczas importowania plików CSV z rekordami wielowierszowe, dane hello może pobrać kostki lub zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="d9aab-403">When importing CSV files with multiline records, hello data may get chopped or scrambled</span></span>

<span data-ttu-id="d9aab-404">02/03/2016</span><span class="sxs-lookup"><span data-stu-id="d9aab-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="d9aab-405">Wersja 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="d9aab-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-406">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-406">Fixes</span></span>

* <span data-ttu-id="d9aab-407">Poprawia ogólną wydajność podczas przekazywanie, pobieranie i kopiowania obiektów blob</span><span class="sxs-lookup"><span data-stu-id="d9aab-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="d9aab-408">01/14/2016</span><span class="sxs-lookup"><span data-stu-id="d9aab-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="d9aab-409">Wersja 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="d9aab-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="d9aab-410">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-410">New</span></span>

* <span data-ttu-id="d9aab-411">Obsługa systemu Linux (parzystość funkcji tooOSX)</span><span class="sxs-lookup"><span data-stu-id="d9aab-411">Linux support (parity features tooOSX)</span></span>
* <span data-ttu-id="d9aab-412">Dodaj kontenerów obiektów blob z kluczem dostępu sygnatur dostępu Współdzielonego</span><span class="sxs-lookup"><span data-stu-id="d9aab-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="d9aab-413">Dodawanie konta magazynu dla Chin Azure</span><span class="sxs-lookup"><span data-stu-id="d9aab-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="d9aab-414">Dodawanie konta magazynu z niestandardowe punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="d9aab-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="d9aab-415">Otwieranie i wyświetlanie hello zawartość tekstu i obrazów obiektów blob</span><span class="sxs-lookup"><span data-stu-id="d9aab-415">Open and view hello contents text and picture blobs</span></span>
* <span data-ttu-id="d9aab-416">Wyświetlanie i edytowanie właściwości obiektów blob i metadanych</span><span class="sxs-lookup"><span data-stu-id="d9aab-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="d9aab-417">Poprawki</span><span class="sxs-lookup"><span data-stu-id="d9aab-417">Fixes</span></span>

* <span data-ttu-id="d9aab-418">Stała: przekazywanie i pobieranie dużą liczbę obiektów blob (500 +) może wywoływać toohave aplikacji hello biały ekran</span><span class="sxs-lookup"><span data-stu-id="d9aab-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause hello app toohave a white screen</span></span> 
* <span data-ttu-id="d9aab-419">Stałym: podczas ustawiania poziomu dostępu publicznego kontenera obiektów blob, hello nową wartość nie jest aktualizowana dopiero po ustawieniu ponownie hello skupić się na powitania kontenera.</span><span class="sxs-lookup"><span data-stu-id="d9aab-419">Fixed: when setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container.</span></span> <span data-ttu-id="d9aab-420">Ponadto okno hello zawsze domyślnie konfiguruje zbyt "dostępu do żadnego elementu publicznego public" i nie hello rzeczywiste bieżącą wartość.</span><span class="sxs-lookup"><span data-stu-id="d9aab-420">Also, hello dialog always defaults too"No public access", and not hello actual current value.</span></span>
* <span data-ttu-id="d9aab-421">Obsługa lepszej ogólnej klawiatury/ułatwień dostępu i interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="d9aab-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="d9aab-422">Obszar nawigacji historii zawijany, gdy jest długa z białą przestrzenią</span><span class="sxs-lookup"><span data-stu-id="d9aab-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="d9aab-423">Okno dialogowe SAS obsługuje sprawdzania poprawności danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="d9aab-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="d9aab-424">Magazyn lokalny nadal toobe dostępne, nawet jeśli wygasły poświadczenia użytkownika</span><span class="sxs-lookup"><span data-stu-id="d9aab-424">Local storage continues toobe available even if user credentials have expired</span></span>
* <span data-ttu-id="d9aab-425">Usunięcie kontenera obiektów blob otwarty Eksplorator obiektów blob hello hello prawej strony jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="d9aab-425">When an opened blob container is deleted, hello blob explorer on hello right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d9aab-426">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-426">Known Issues</span></span>

* <span data-ttu-id="d9aab-427">Wymagania instalacji Linux wersji gcc zaktualizowane lub uaktualnione — tooupgrade kroki są poniżej:</span><span class="sxs-lookup"><span data-stu-id="d9aab-427">Linux install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="d9aab-428">11/18/2015</span><span class="sxs-lookup"><span data-stu-id="d9aab-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="d9aab-429">Wersja 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="d9aab-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="d9aab-430">Nowy</span><span class="sxs-lookup"><span data-stu-id="d9aab-430">New</span></span>

* <span data-ttu-id="d9aab-431">System macOS i wersji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d9aab-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="d9aab-432">Zaloguj się tooview kont magazynu — użyć konta organizacji, Account firmy Microsoft, 2FA itp.</span><span class="sxs-lookup"><span data-stu-id="d9aab-432">Sign in tooview your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="d9aab-433">Lokalne działania projektowe magazynu (użyć emulatora magazynu systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="d9aab-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="d9aab-434">Usługa Azure Resource Manager i Model Klasyczny zasobów pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="d9aab-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="d9aab-435">Tworzenie i usuwanie obiektów blob, kolejek i tabel</span><span class="sxs-lookup"><span data-stu-id="d9aab-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="d9aab-436">Wyszukiwanie określonych obiektów blob, kolejek i tabel</span><span class="sxs-lookup"><span data-stu-id="d9aab-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="d9aab-437">Przejrzyj zawartość hello kontenerów obiektów blob</span><span class="sxs-lookup"><span data-stu-id="d9aab-437">Explore hello contents of blob containers</span></span>
* <span data-ttu-id="d9aab-438">Wyświetlanie i przeglądanie katalogów</span><span class="sxs-lookup"><span data-stu-id="d9aab-438">View and navigate through directories</span></span>
* <span data-ttu-id="d9aab-439">Przekazywanie, pobieranie i usuwanie obiektów blob i folderów</span><span class="sxs-lookup"><span data-stu-id="d9aab-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="d9aab-440">Wyświetlanie i edytowanie właściwości obiektów blob i metadanych</span><span class="sxs-lookup"><span data-stu-id="d9aab-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="d9aab-441">Generuj klucze SAS</span><span class="sxs-lookup"><span data-stu-id="d9aab-441">Generate SAS keys</span></span>
* <span data-ttu-id="d9aab-442">Zarządzanie i utworzyć przechowywane zasad dostępu (SAP)</span><span class="sxs-lookup"><span data-stu-id="d9aab-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="d9aab-443">Wyszukaj obiekty BLOB według prefiksu</span><span class="sxs-lookup"><span data-stu-id="d9aab-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="d9aab-444">Przeciągnij n Porzuć tooupload plików lub pobrać</span><span class="sxs-lookup"><span data-stu-id="d9aab-444">Drag 'n drop files tooupload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d9aab-445">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d9aab-445">Known Issues</span></span>

* <span data-ttu-id="d9aab-446">Podczas ustawiania poziomu dostępu publicznego kontenera obiektów blob, dopóki nie zostanie ponownie ustawiony fokus hello w kontenerze hello hello nowa wartość nie jest aktualizowany</span><span class="sxs-lookup"><span data-stu-id="d9aab-446">When setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container</span></span>
* <span data-ttu-id="d9aab-447">Po otwarciu hello okna dialogowego tooset hello dostępu publicznego poziom zawsze widoczny "Brak dostępu publicznego" hello domyślnej i nie hello bieżąca wartość rzeczywista</span><span class="sxs-lookup"><span data-stu-id="d9aab-447">When you open hello dialog tooset hello public access level, it always shows "No public access" as hello default, and not hello actual current value</span></span>
* <span data-ttu-id="d9aab-448">Nie można zmienić nazwy pobrany obiektów blob</span><span class="sxs-lookup"><span data-stu-id="d9aab-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="d9aab-449">Wpisy dziennika aktywności będą czasami "zatrzymywane" w toku stanu, gdy wystąpi błąd i nie zostanie wyświetlony błąd hello</span><span class="sxs-lookup"><span data-stu-id="d9aab-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and hello error is not displayed</span></span>
* <span data-ttu-id="d9aab-450">Czasami awarii lub włącza całkowicie biały podczas próby tooupload lub pobrać dużą liczbę obiektów blob</span><span class="sxs-lookup"><span data-stu-id="d9aab-450">Sometimes crashes or turns completely white when trying tooupload or download a large number of blobs</span></span>
* <span data-ttu-id="d9aab-451">Czasami anulowanie operacji kopiowania nie działa</span><span class="sxs-lookup"><span data-stu-id="d9aab-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="d9aab-452">Podczas tworzenia kontenera (tabeli-obiekt blob/kolejki), jeśli wejściowy nieprawidłową nazwę i kontynuować toocreate drugiego, w ramach typu innego kontenera nie można ustawić fokusu na nowy typ hello</span><span class="sxs-lookup"><span data-stu-id="d9aab-452">During creating a container (blob/queue/table), if you input an invalid name and proceed toocreate another under a different container type you cannot set focus on hello new type</span></span>
* <span data-ttu-id="d9aab-453">Nie można utworzyć nowego folderu, lub zmień nazwę folderu</span><span class="sxs-lookup"><span data-stu-id="d9aab-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md