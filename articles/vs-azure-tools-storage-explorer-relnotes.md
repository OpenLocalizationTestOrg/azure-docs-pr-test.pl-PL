---
title: "Informacje o wersji Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 63a24f6b153390533bba0888fd1051508c65bf6e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="a59bf-103">Informacje o wersji Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="a59bf-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="a59bf-104">Ten artykuł zawiera zlecenia, które uwagi 0.8.16 Eksploratora usługi Azure Storage (wersja zapoznawcza) wersji, a także informacje o wersji w poprzednich wersjach.</span><span class="sxs-lookup"><span data-stu-id="a59bf-104">This article contains the release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="a59bf-105">[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](./vs-azure-tools-storage-manage-with-storage-explorer.md) jest aplikacją autonomiczną, która pozwala łatwo pracować z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="a59bf-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="a59bf-106">Wersja 0.8.16 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="a59bf-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="a59bf-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="a59bf-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="a59bf-108">Pobierz Eksploratora usługi Azure Storage 0.8.16 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="a59bf-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="a59bf-109">Eksplorator usługi Azure Storage 0.8.16 (wersja zapoznawcza) dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a59bf-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="a59bf-110">Eksplorator usługi Azure Storage 0.8.16 (wersja zapoznawcza) dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="a59bf-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="a59bf-111">Eksplorator usługi Azure Storage 0.8.16 (wersja zapoznawcza) dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="a59bf-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="a59bf-112">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-112">New</span></span>
* <span data-ttu-id="a59bf-113">Po otwarciu obiektu blob Eksploratora usługi Storage spowoduje wyświetlenie monitu o Przekaż pobrany plik, jeśli zmiana zostaje wykryta</span><span class="sxs-lookup"><span data-stu-id="a59bf-113">When you open a blob, Storage Explorer will prompt you to upload the downloaded file if a change is detected</span></span>
* <span data-ttu-id="a59bf-114">Rozszerzony stos Azure logowania</span><span class="sxs-lookup"><span data-stu-id="a59bf-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="a59bf-115">Zwiększono wydajność przekazywania/pobieranie wiele małych plików w tym samym czasie</span><span class="sxs-lookup"><span data-stu-id="a59bf-115">Improved the performance of uploading/downloading many small files at the same time</span></span>


### <a name="fixes"></a><span data-ttu-id="a59bf-116">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-116">Fixes</span></span>
* <span data-ttu-id="a59bf-117">Dla niektórych typów obiektów blob wybierając pozycję "replace" podczas przekazywania konflikt czasami spowoduje przekazywania uruchamiany ponownie.</span><span class="sxs-lookup"><span data-stu-id="a59bf-117">For some blob types, choosing to "replace" during an upload conflict would sometimes result in the upload being restarted.</span></span> 
* <span data-ttu-id="a59bf-118">W wersji 0.8.15 przekazywania czasami spowoduje zatrzymania 99%.</span><span class="sxs-lookup"><span data-stu-id="a59bf-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="a59bf-119">Przekazywanie plików do udziału plików, jeśli chcesz przekazać do katalogu, które nie zostały jeszcze istnieje, przekazania może zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="a59bf-119">When uploading files to a file share, if you chose to upload to a directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="a59bf-120">Eksploratora usługi Storage został niepoprawnie generowania sygnatury czasowe dla sygnatur dostępu współdzielonego i tabeli zapytania.</span><span class="sxs-lookup"><span data-stu-id="a59bf-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="a59bf-121">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-121">Known Issues</span></span>
* <span data-ttu-id="a59bf-122">Przy użyciu nazwy i parametry połączenia klucza aktualnie nie działa.</span><span class="sxs-lookup"><span data-stu-id="a59bf-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="a59bf-123">Zostanie on rozwiązany w następnej wersji.</span><span class="sxs-lookup"><span data-stu-id="a59bf-123">It will be fixed in the next release.</span></span> <span data-ttu-id="a59bf-124">Do tego czasu można dołączyć z nazwy i klucza.</span><span class="sxs-lookup"><span data-stu-id="a59bf-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="a59bf-125">Próba otwarcia pliku o nieprawidłowej nazwie pliku systemu Windows, pobierania spowoduje błąd: nie odnaleziono pliku.</span><span class="sxs-lookup"><span data-stu-id="a59bf-125">If you try to open a file with an invalid Windows file name, the download will result in a file not found error.</span></span>
* <span data-ttu-id="a59bf-126">Po kliknięciu przycisku "Anuluj" dla zadania, może upłynąć trochę czasu dla tego zadania anulować.</span><span class="sxs-lookup"><span data-stu-id="a59bf-126">After clicking "Cancel" on a task, it may take a while for that task to cancel.</span></span> <span data-ttu-id="a59bf-127">Jest to ograniczenie biblioteki węzła magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="a59bf-127">This is a limitation of the Azure Storage Node library.</span></span>
* <span data-ttu-id="a59bf-128">Po zakończeniu przekazywania obiektów blob, jest odświeżany kartę, który zainicjował przekazywania.</span><span class="sxs-lookup"><span data-stu-id="a59bf-128">After completing a blob upload, the tab which initiated the upload is refreshed.</span></span> <span data-ttu-id="a59bf-129">Została zmieniona z poprzedniego działania, a także spowoduje przyjmowana z powrotem do głównego kontenera, które znajdują się w.</span><span class="sxs-lookup"><span data-stu-id="a59bf-129">This is a change from previous behavior, and will also cause you to be taken back to the root of the container you are in.</span></span>
* <span data-ttu-id="a59bf-130">Jeśli wybierzesz nieprawidłowy certyfikat kodu PIN/karty inteligentnej, będzie konieczne ponowne uruchomienie w celu Eksploratora usługi Storage zapomnij tej decyzji.</span><span class="sxs-lookup"><span data-stu-id="a59bf-130">If you choose the wrong PIN/Smartcard certificate, then you will need to restart in order to have Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="a59bf-131">Panel ustawień konta mogą być wyświetlane, należy ponownie wprowadzić poświadczenia, aby filtrować subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a59bf-131">The account settings panel may show that you need to reenter credentials to filter subscriptions.</span></span>
* <span data-ttu-id="a59bf-132">Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki.</span><span class="sxs-lookup"><span data-stu-id="a59bf-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="a59bf-133">Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.</span><span class="sxs-lookup"><span data-stu-id="a59bf-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="a59bf-134">Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu.</span><span class="sxs-lookup"><span data-stu-id="a59bf-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="a59bf-135">Dla użytkowników Ubuntu 14.04, konieczne będzie zapewnienia GCC jest aktualny — można to zrobić, uruchamiając następujące polecenia i ponownym uruchomieniu komputera:</span><span class="sxs-lookup"><span data-stu-id="a59bf-135">For users on Ubuntu 14.04, you will need to ensure GCC is up to date - this can be done by running the following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="a59bf-136">Dla użytkowników Ubuntu 17.04 będą musieli zainstalować GConf — można to zrobić, uruchamiając następujące polecenia i ponownym uruchomieniu komputera:</span><span class="sxs-lookup"><span data-stu-id="a59bf-136">For users on Ubuntu 17.04, you will need to install GConf - this can be done by running the following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="a59bf-137">Wersja 0.8.14 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="a59bf-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="a59bf-138">06/22/2017</span><span class="sxs-lookup"><span data-stu-id="a59bf-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="a59bf-139">Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="a59bf-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="a59bf-140">Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza) dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a59bf-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="a59bf-141">Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza) dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="a59bf-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="a59bf-142">Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza) dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="a59bf-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="a59bf-143">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-143">New</span></span>

* <span data-ttu-id="a59bf-144">Zaktualizowana wersja elektronów do 1.7.2, aby można było skorzystać z kilku aktualizacji krytycznych</span><span class="sxs-lookup"><span data-stu-id="a59bf-144">Updated Electron version to 1.7.2 in order to take advantage of several critical security updates</span></span>
* <span data-ttu-id="a59bf-145">Możesz teraz szybko uzyskiwać dostęp online przewodnik rozwiązywania problemów z menu Pomoc</span><span class="sxs-lookup"><span data-stu-id="a59bf-145">You can now quickly access the online troubleshooting guide from the help menu</span></span>
* <span data-ttu-id="a59bf-146">Rozwiązywanie problemów z Eksploratora usługi Storage [przewodnik][2]</span><span class="sxs-lookup"><span data-stu-id="a59bf-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="a59bf-147">[Instrukcje] [ 3] na nawiązywanie połączenia z subskrypcją platformy Azure stosu</span><span class="sxs-lookup"><span data-stu-id="a59bf-147">[Instructions][3] on connecting to an Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="a59bf-148">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-148">Known Issues</span></span>

* <span data-ttu-id="a59bf-149">Przyciski w oknie dialogowym potwierdzenia usunięcia folderu nie zarejestrować kliknięć myszą w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="a59bf-149">Buttons on the delete folder confirmation dialog don't register with the mouse clicks on Linux.</span></span> <span data-ttu-id="a59bf-150">Obejście tego problemu jest użycie klawisza Enter</span><span class="sxs-lookup"><span data-stu-id="a59bf-150">Workaround is to use the Enter key</span></span>
* <span data-ttu-id="a59bf-151">Po wybraniu zły certyfikat karty inteligentnej na kodu PIN/następnie konieczne będzie ponowne uruchomienie w celu Eksploratora usługi Storage zapomnij decyzji</span><span class="sxs-lookup"><span data-stu-id="a59bf-151">If you choose the wrong PIN/Smartcard certificate then you will need to restart in order to have Storage Explorer forget the decision</span></span>
* <span data-ttu-id="a59bf-152">Mając więcej niż 3 grup obiektów blob lub przekazywania w tym samym czasie plików może powodować błędy</span><span class="sxs-lookup"><span data-stu-id="a59bf-152">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="a59bf-153">Panel ustawień konta mogą być wyświetlane konieczne ponowne wprowadzenie poświadczeń, aby filtrować subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a59bf-153">The account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="a59bf-154">Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki.</span><span class="sxs-lookup"><span data-stu-id="a59bf-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="a59bf-155">Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.</span><span class="sxs-lookup"><span data-stu-id="a59bf-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="a59bf-156">Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu.</span><span class="sxs-lookup"><span data-stu-id="a59bf-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="a59bf-157">Ubuntu 14.04 instalacji wymaga wersji gcc zaktualizowane lub uaktualnione — kroki niezbędne do uaktualnienia jest poniżej:</span><span class="sxs-lookup"><span data-stu-id="a59bf-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="a59bf-158">Poprzednie wersje</span><span class="sxs-lookup"><span data-stu-id="a59bf-158">Previous releases</span></span>

* [<span data-ttu-id="a59bf-159">Wersja 0.8.13</span><span class="sxs-lookup"><span data-stu-id="a59bf-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="a59bf-160">Wersja 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="a59bf-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="a59bf-161">Wersja 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="a59bf-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="a59bf-162">Wersja 0.8.7</span><span class="sxs-lookup"><span data-stu-id="a59bf-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="a59bf-163">Wersja 0.8.6</span><span class="sxs-lookup"><span data-stu-id="a59bf-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="a59bf-164">Wersja 0.8.5</span><span class="sxs-lookup"><span data-stu-id="a59bf-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="a59bf-165">Wersja 0.8.4</span><span class="sxs-lookup"><span data-stu-id="a59bf-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="a59bf-166">Wersja 0.8.3</span><span class="sxs-lookup"><span data-stu-id="a59bf-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="a59bf-167">Wersja 0.8.2</span><span class="sxs-lookup"><span data-stu-id="a59bf-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="a59bf-168">Wersja 0.8.0</span><span class="sxs-lookup"><span data-stu-id="a59bf-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="a59bf-169">Wersja 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="a59bf-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="a59bf-170">Wersja 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="a59bf-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="a59bf-171">Wersja 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="a59bf-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="a59bf-172">Wersja 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="a59bf-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="a59bf-173">Wersja 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="a59bf-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="a59bf-174">Wersja 0.8.13</span><span class="sxs-lookup"><span data-stu-id="a59bf-174">Version 0.8.13</span></span>
<span data-ttu-id="a59bf-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="a59bf-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="a59bf-176">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-176">New</span></span>

* <span data-ttu-id="a59bf-177">Rozwiązywanie problemów z Eksploratora usługi Storage [przewodnik][2]</span><span class="sxs-lookup"><span data-stu-id="a59bf-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="a59bf-178">[Instrukcje] [ 3] na nawiązywanie połączenia z subskrypcją platformy Azure stosu</span><span class="sxs-lookup"><span data-stu-id="a59bf-178">[Instructions][3] on connecting to an Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-179">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-179">Fixes</span></span>

* <span data-ttu-id="a59bf-180">Stała: Przekazywanie pliku wypróbowana wysokiej spowodować błąd braku pamięci</span><span class="sxs-lookup"><span data-stu-id="a59bf-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="a59bf-181">Stały: Można teraz zalogować się przy użyciu kodu PIN/za pomocą kart inteligentnych</span><span class="sxs-lookup"><span data-stu-id="a59bf-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="a59bf-182">Stałe: Otwórz w portalu teraz współpracuje z Chińskiej wersji platformy Azure, platformy Azure w Niemczech Azure instytucji rządowych Stanów Zjednoczonych i stosu Azure</span><span class="sxs-lookup"><span data-stu-id="a59bf-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="a59bf-183">Stała: Podczas przekazywania folder do kontenera obiektów blob, błąd "Niedozwolonej operacji" czasami wystąpiłyby</span><span class="sxs-lookup"><span data-stu-id="a59bf-183">Fixed: While uploading a folder to a blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="a59bf-184">Stałej: Zaznacz wszystko zostało wyłączone podczas zarządzania migawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="a59bf-185">Stały: Metadane obiektu blob podstawowej może spowodować zastąpienie po wyświetleniu właściwości jego migawek.</span><span class="sxs-lookup"><span data-stu-id="a59bf-185">Fixed: The metadata of the base blob might get overwritten after viewing the properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a59bf-186">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-186">Known Issues</span></span>

* <span data-ttu-id="a59bf-187">Po wybraniu zły certyfikat karty inteligentnej na kodu PIN/następnie konieczne będzie ponowne uruchomienie w celu Eksploratora usługi Storage zapomnij decyzji</span><span class="sxs-lookup"><span data-stu-id="a59bf-187">If you choose the wrong PIN/Smartcard certificate then you will need to restart in order to have Storage Explorer forget the decision</span></span>
* <span data-ttu-id="a59bf-188">Gdy jest powiększony przychodzący lub wychodzący, poziom powiększenia na chwilę może zresetować domyślnego poziomu</span><span class="sxs-lookup"><span data-stu-id="a59bf-188">While zoomed in or out, the zoom level may momentarily reset to the default level</span></span>
* <span data-ttu-id="a59bf-189">Mając więcej niż 3 grup obiektów blob lub przekazywania w tym samym czasie plików może powodować błędy</span><span class="sxs-lookup"><span data-stu-id="a59bf-189">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="a59bf-190">Panel ustawień konta mogą być wyświetlane konieczne ponowne wprowadzenie poświadczeń, aby filtrować subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a59bf-190">The account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="a59bf-191">Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki.</span><span class="sxs-lookup"><span data-stu-id="a59bf-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="a59bf-192">Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.</span><span class="sxs-lookup"><span data-stu-id="a59bf-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="a59bf-193">Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu.</span><span class="sxs-lookup"><span data-stu-id="a59bf-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="a59bf-194">Ubuntu 14.04 instalacji wymaga wersji gcc zaktualizowane lub uaktualnione — kroki niezbędne do uaktualnienia jest poniżej:</span><span class="sxs-lookup"><span data-stu-id="a59bf-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="a59bf-195">Wersja 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="a59bf-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="a59bf-196">04/07/2017</span><span class="sxs-lookup"><span data-stu-id="a59bf-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="a59bf-197">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-197">New</span></span>

* <span data-ttu-id="a59bf-198">Eksplorator usługi Storage teraz zostanie automatycznie zamknięte podczas instalacji aktualizacji z powiadomienie o aktualizacji</span><span class="sxs-lookup"><span data-stu-id="a59bf-198">Storage Explorer will now automatically close when you install an update from the update notification</span></span>
* <span data-ttu-id="a59bf-199">Szybki dostęp w miejscu udostępnia udoskonalone środowisko do pracy z często używanych zasobów</span><span class="sxs-lookup"><span data-stu-id="a59bf-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="a59bf-200">W edytorze kontenera obiektów Blob można przeglądać maszyny wirtualnej, które dzierżawionych obiektu blob należy do</span><span class="sxs-lookup"><span data-stu-id="a59bf-200">In the Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="a59bf-201">Teraz można zwinąć panelu po lewej stronie</span><span class="sxs-lookup"><span data-stu-id="a59bf-201">You can now collapse the left side panel</span></span>
* <span data-ttu-id="a59bf-202">Odnajdywanie teraz odbywa się w tym samym czasie jako plik do pobrania</span><span class="sxs-lookup"><span data-stu-id="a59bf-202">Discovery now runs at the same time as download</span></span>
* <span data-ttu-id="a59bf-203">Użyj statystyk w edytorach kontenera obiektów Blob, udziału plików i tabeli, aby wyświetlić rozmiar zasobu lub zaznaczenia</span><span class="sxs-lookup"><span data-stu-id="a59bf-203">Use Statistics in the Blob Container, File Share, and Table editors to see the size of your resource or selection</span></span>
* <span data-ttu-id="a59bf-204">Możesz teraz logowania do usługi Azure Active Directory (AAD) na podstawie konta Azure stosu.</span><span class="sxs-lookup"><span data-stu-id="a59bf-204">You can now sign-in to Azure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="a59bf-205">Możesz teraz przekazać pliki archiwum przekracza 32MB do kont magazynu w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="a59bf-205">You can now upload archive files over 32MB to Premium storage accounts</span></span>
* <span data-ttu-id="a59bf-206">Udoskonalona obsługa ułatwień dostępu</span><span class="sxs-lookup"><span data-stu-id="a59bf-206">Improved accessibility support</span></span>
* <span data-ttu-id="a59bf-207">Można teraz dodawać zaufanych Base-64 zakodowane certyfikatów X.509 SSL, przechodząc do edycji —&gt; certyfikaty SSL -&gt; importu certyfikatów</span><span class="sxs-lookup"><span data-stu-id="a59bf-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going to Edit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-208">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-208">Fixes</span></span>

* <span data-ttu-id="a59bf-209">Stała: po odświeżeniu poświadczenia konta, widok drzewa czy czasami nie automatycznie odświeżenia</span><span class="sxs-lookup"><span data-stu-id="a59bf-209">Fixed: after refreshing an account's credentials, the tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="a59bf-210">Stała: Generowanie sygnatury dostępu Współdzielonego dla kolejki emulatora i tabele dadzą w wyniku nieprawidłowy adres URL</span><span class="sxs-lookup"><span data-stu-id="a59bf-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="a59bf-211">Stały: konta premium magazynu teraz można rozszerzyć, gdy włączone jest serwer proxy</span><span class="sxs-lookup"><span data-stu-id="a59bf-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="a59bf-212">Stałe: przycisk Zastosuj, na stronie Zarządzanie kont nie będzie działać gdyby 1 lub 0 konta zaznaczone</span><span class="sxs-lookup"><span data-stu-id="a59bf-212">Fixed: the apply button on the accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="a59bf-213">Stały: przekazywanie obiektów blob, które wymagają rozwiązania konfliktu może zakończyć się niepowodzeniem — stała 0.8.11</span><span class="sxs-lookup"><span data-stu-id="a59bf-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="a59bf-214">Stałe: wysyłanie opinii został przerwany w 0.8.11 — stała 0.8.12</span><span class="sxs-lookup"><span data-stu-id="a59bf-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="a59bf-215">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-215">Known Issues</span></span>

* <span data-ttu-id="a59bf-216">Po uaktualnieniu do wersji 0.8.10, należy odświeżyć wszystkie swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="a59bf-216">After upgrading to 0.8.10, you will need to refresh all of your credentials.</span></span>
* <span data-ttu-id="a59bf-217">Gdy jest powiększony przychodzący lub wychodzący, poziom powiększenia na chwilę może zresetować domyślnego poziomu.</span><span class="sxs-lookup"><span data-stu-id="a59bf-217">While zoomed in or out, the zoom level may momentarily reset to the default level.</span></span>
* <span data-ttu-id="a59bf-218">Mając więcej niż 3 grup obiektów blob lub przekazywania w tym samym czasie plików może powodować błędy.</span><span class="sxs-lookup"><span data-stu-id="a59bf-218">Having more than 3 groups of blobs or files uploading at the same time may cause errors.</span></span>
* <span data-ttu-id="a59bf-219">Panel ustawień konta mogą być wyświetlane, należy ponownie wprowadzić poświadczenia, aby filtrować subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a59bf-219">The account settings panel may show that you need to reenter credentials in order to filter subscriptions.</span></span>
* <span data-ttu-id="a59bf-220">Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki.</span><span class="sxs-lookup"><span data-stu-id="a59bf-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="a59bf-221">Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.</span><span class="sxs-lookup"><span data-stu-id="a59bf-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="a59bf-222">Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu.</span><span class="sxs-lookup"><span data-stu-id="a59bf-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="a59bf-223">Ubuntu 14.04 instalacji wymaga wersji gcc zaktualizowane lub uaktualnione — kroki niezbędne do uaktualnienia jest poniżej:</span><span class="sxs-lookup"><span data-stu-id="a59bf-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="a59bf-224">Wersja 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="a59bf-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="a59bf-225">02/23/2017</span><span class="sxs-lookup"><span data-stu-id="a59bf-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="a59bf-226">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-226">New</span></span>

* <span data-ttu-id="a59bf-227">Eksplorator usługi Storage 0.8.9 automatycznie pobierze najnowszą wersję aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="a59bf-227">Storage Explorer 0.8.9 will automatically download the latest version for updates.</span></span>
* <span data-ttu-id="a59bf-228">Poprawka: przy użyciu portalu wygenerowanego identyfikatora URI połączenia SAS do podłączenia konta magazynu spowoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="a59bf-228">Hotfix: using a portal generated SAS URI to attach a storage account would result in an error.</span></span>
* <span data-ttu-id="a59bf-229">Teraz można tworzyć, zarządzanie i wspierania migawki obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="a59bf-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="a59bf-230">Można teraz logowania się do konta chińskiej wersji platformy Azure, platformy Azure w Niemczech i Azure instytucji rządowych Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="a59bf-230">You can now sign in to Azure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="a59bf-231">Można teraz zmienić poziom powiększenia.</span><span class="sxs-lookup"><span data-stu-id="a59bf-231">You can now change the zoom level.</span></span> <span data-ttu-id="a59bf-232">Opcje w menu Widok powiększanie, zmniejszanie i zresetować powiększenie.</span><span class="sxs-lookup"><span data-stu-id="a59bf-232">Use the options in the View menu to Zoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="a59bf-233">Znaki Unicode są teraz obsługiwane w metadanych użytkownika do obiektów blob i plików.</span><span class="sxs-lookup"><span data-stu-id="a59bf-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="a59bf-234">Zwiększona dostępność.</span><span class="sxs-lookup"><span data-stu-id="a59bf-234">Accessibility improvements.</span></span>
* <span data-ttu-id="a59bf-235">Z powiadomienie o aktualizacji można wyświetlić informacje o wersji w następnej wersji.</span><span class="sxs-lookup"><span data-stu-id="a59bf-235">The next version's release notes can be viewed from the update notification.</span></span> <span data-ttu-id="a59bf-236">Można również wyświetlić bieżące informacje o wersji w menu Pomoc.</span><span class="sxs-lookup"><span data-stu-id="a59bf-236">You can also view the current release notes from the Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-237">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-237">Fixes</span></span>

* <span data-ttu-id="a59bf-238">Stały: numer wersji jest teraz prawidłowo wyświetlany w Panelu sterowania w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="a59bf-238">Fixed: the version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="a59bf-239">Stały: wyszukiwanie nie jest już ograniczona do 50 000 węzłów</span><span class="sxs-lookup"><span data-stu-id="a59bf-239">Fixed: search is no longer limited to 50,000 nodes</span></span>
* <span data-ttu-id="a59bf-240">Stały: Przekaż do udziału plików zawsze wykonana, jeśli katalog docelowy już nie istnieje</span><span class="sxs-lookup"><span data-stu-id="a59bf-240">Fixed: upload to a file share spun forever if the destination directory did not already exist</span></span>
* <span data-ttu-id="a59bf-241">Stały: lepszą stabilność dla długich przekazywania i pobierania</span><span class="sxs-lookup"><span data-stu-id="a59bf-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a59bf-242">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-242">Known Issues</span></span>

* <span data-ttu-id="a59bf-243">Gdy jest powiększony przychodzący lub wychodzący, poziom powiększenia na chwilę może zresetować domyślnego poziomu.</span><span class="sxs-lookup"><span data-stu-id="a59bf-243">While zoomed in or out, the zoom level may momentarily reset to the default level.</span></span>
* <span data-ttu-id="a59bf-244">Szybki dostęp działa tylko z elementami subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a59bf-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="a59bf-245">Zasobów lokalnych lub zasobów dołączonych za pomocą klucza lub tokenu sygnatury dostępu Współdzielonego nie są obsługiwane w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="a59bf-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="a59bf-246">Może upłynąć w kilka sekund, aby przejść do zasobu docelowego, w zależności od liczby zasobów, należy mieć szybki dostęp.</span><span class="sxs-lookup"><span data-stu-id="a59bf-246">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="a59bf-247">Mając więcej niż 3 grup obiektów blob lub przekazywania w tym samym czasie plików może powodować błędy.</span><span class="sxs-lookup"><span data-stu-id="a59bf-247">Having more than 3 groups of blobs or files uploading at the same time may cause errors.</span></span>

<span data-ttu-id="a59bf-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="a59bf-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="a59bf-249">Wersja 0.8.7</span><span class="sxs-lookup"><span data-stu-id="a59bf-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="a59bf-250">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-250">New</span></span>

* <span data-ttu-id="a59bf-251">Można wybrać sposób rozwiązywania konfliktów na początku sesji aktualizacji, pobieranie lub kopiowanie w oknie działań</span><span class="sxs-lookup"><span data-stu-id="a59bf-251">You can choose how to resolve conflicts at the beginning of an update, download or copy session in the Activities window</span></span>
* <span data-ttu-id="a59bf-252">Umieść kursor nad kartę, aby wyświetlić pełną ścieżkę zasobów pamięci masowej</span><span class="sxs-lookup"><span data-stu-id="a59bf-252">Hover over a tab to see the full path of the storage resource</span></span>
* <span data-ttu-id="a59bf-253">Po kliknięciu na karcie synchronizacji z lokalizacji, w okienku nawigacji po lewej stronie</span><span class="sxs-lookup"><span data-stu-id="a59bf-253">When you click on a tab, it synchronizes with its location in the left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-254">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-254">Fixes</span></span>

* <span data-ttu-id="a59bf-255">Stały: Eksploratora usługi Storage jest teraz zaufanych aplikacji dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="a59bf-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="a59bf-256">Stały: Ubuntu 14.04 jest ponownie obsługiwane</span><span class="sxs-lookup"><span data-stu-id="a59bf-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="a59bf-257">Stały: Czasami Dodaj konto interfejsu użytkownika miga podczas ładowania subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a59bf-257">Fixed: Sometimes the add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="a59bf-258">Stały: Czasami nie wszystkie zasoby magazynu zostały wymienione w okienku nawigacji po lewej stronie</span><span class="sxs-lookup"><span data-stu-id="a59bf-258">Fixed: Sometimes not all storage resources were listed in the left side navigation pane</span></span>
* <span data-ttu-id="a59bf-259">Stałe: Okienka akcji czasami wyświetlane akcje pusty</span><span class="sxs-lookup"><span data-stu-id="a59bf-259">Fixed: The action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="a59bf-260">Stały: Rozmiar okna z ostatniej sesji zamkniętego są teraz przechowywane</span><span class="sxs-lookup"><span data-stu-id="a59bf-260">Fixed: The window size from the last closed session is now retained</span></span>
* <span data-ttu-id="a59bf-261">Stały: Możesz otworzyć wiele kart dla tego samego zasobu za pomocą menu kontekstowe</span><span class="sxs-lookup"><span data-stu-id="a59bf-261">Fixed: You can open multiple tabs for the same resource using the context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a59bf-262">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-262">Known Issues</span></span>

* <span data-ttu-id="a59bf-263">Szybki dostęp działa tylko z elementami subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a59bf-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="a59bf-264">Zasobów lokalnych lub dołączonych za pomocą klucza lub tokenu sygnatury dostępu Współdzielonego zasobów nie są obsługiwane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="a59bf-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="a59bf-265">Może zająć w kilka sekund, aby przejść do zasobu docelowego, w zależności od liczby zasobów, musisz mieć szybki dostęp</span><span class="sxs-lookup"><span data-stu-id="a59bf-265">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="a59bf-266">Mając więcej niż 3 grup obiektów blob lub przekazywania w tym samym czasie plików może powodować błędy</span><span class="sxs-lookup"><span data-stu-id="a59bf-266">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="a59bf-267">Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 — po to, może to mieć wpływ na wydajność lub może spowodować nieobsługiwany wyjątek</span><span class="sxs-lookup"><span data-stu-id="a59bf-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="a59bf-268">Po raz pierwszy na macOS przy użyciu Eksploratora magazynu może pojawić się wiele monitów pytania o uprawnienia użytkownika do uzyskania dostępu łańcucha kluczy.</span><span class="sxs-lookup"><span data-stu-id="a59bf-268">For the first time using the Storage Explorer on macOS, you might see multiple prompts asking for user's permission to access keychain.</span></span> <span data-ttu-id="a59bf-269">Zalecamy użycie wybierz zawsze Zezwalaj, monit nie będą widoczne ponownie</span><span class="sxs-lookup"><span data-stu-id="a59bf-269">We suggest you select Always Allow so the prompt won't show up again</span></span>

<span data-ttu-id="a59bf-270">11/18/2016</span><span class="sxs-lookup"><span data-stu-id="a59bf-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="a59bf-271">Wersja 0.8.6</span><span class="sxs-lookup"><span data-stu-id="a59bf-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="a59bf-272">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-272">New</span></span>

* <span data-ttu-id="a59bf-273">Można teraz numer pin najczęściej używane usług szybki dostęp do ułatwienia nawigacji</span><span class="sxs-lookup"><span data-stu-id="a59bf-273">You can now pin most frequently used services to the Quick Access for easy navigation</span></span>
* <span data-ttu-id="a59bf-274">Teraz możesz otworzyć wiele edytorów na różnych kartach.</span><span class="sxs-lookup"><span data-stu-id="a59bf-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="a59bf-275">Jednego kliknięcia, aby otworzyć kartę tymczasowego; Kliknij dwukrotnie, aby otworzyć kartę trwałych. Możesz również kliknąć na karcie tymczasowy, aby stał się na karcie stałe</span><span class="sxs-lookup"><span data-stu-id="a59bf-275">Single click to open a temporary tab; double click to open a permanent tab. You can also click on the temporary tab to make it a permanent tab</span></span>
* <span data-ttu-id="a59bf-276">Wprowadziliśmy zauważalna zmiana wydajności i stabilności ulepszenia przekazywania i pobierania, zwłaszcza w przypadku dużych plików na maszynach fast</span><span class="sxs-lookup"><span data-stu-id="a59bf-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="a59bf-277">Teraz można tworzyć foldery "wirtualne" pusta w kontenerów obiektów blob</span><span class="sxs-lookup"><span data-stu-id="a59bf-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="a59bf-278">Ma ponownie wprowadzono ukierunkowane wyszukiwanie z naszego nowego wyszukiwania podciągu rozszerzonego, teraz są dwie opcje wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="a59bf-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="a59bf-279">Globalne wyszukiwanie — w polu tekstowym wyszukiwania wpisz wyszukiwany termin</span><span class="sxs-lookup"><span data-stu-id="a59bf-279">Global search - just enter a search term into the search textbox</span></span>
    * <span data-ttu-id="a59bf-280">Wyszukiwania zakresowego — kliknij ikonę lupy obok węzła, a następnie dodaj wyszukiwany termin do końca ścieżki, lub kliknij prawym przyciskiem myszy i wybierz polecenie "Wyszukiwania z tutaj"</span><span class="sxs-lookup"><span data-stu-id="a59bf-280">Scoped search - click the magnifying glass icon next to a node, then add a search term to the end of the path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="a59bf-281">Dodano różne kompozycje: jasny (ustawienie domyślne), ciemny, wysoki kontrast czarne i wysoki kontrast biały.</span><span class="sxs-lookup"><span data-stu-id="a59bf-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="a59bf-282">Przejdź do edycji -&gt; kompozycje, aby zmienić preferencje motywów</span><span class="sxs-lookup"><span data-stu-id="a59bf-282">Go to Edit -&gt; Themes to change your theming preference</span></span>
* <span data-ttu-id="a59bf-283">Można zmodyfikować właściwości obiektów Blob i plików</span><span class="sxs-lookup"><span data-stu-id="a59bf-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="a59bf-284">Firma Microsoft obsługuje teraz zakodowanego (base64) i niekodowany kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="a59bf-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="a59bf-285">W systemie Linux, 64-bitowego systemu operacyjnego jest teraz wymagane.</span><span class="sxs-lookup"><span data-stu-id="a59bf-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="a59bf-286">W tej wersji obsługiwany jest tylko 64-bitowych Ubuntu 16.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="a59bf-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="a59bf-287">Zaktualizowaliśmy naszych logo!</span><span class="sxs-lookup"><span data-stu-id="a59bf-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-288">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-288">Fixes</span></span>

* <span data-ttu-id="a59bf-289">Stała: Ekranu zamrożenia problemów</span><span class="sxs-lookup"><span data-stu-id="a59bf-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="a59bf-290">Stały: Zwiększonych zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="a59bf-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="a59bf-291">Stałe: Może być czasami zduplikowane dołączonego konta</span><span class="sxs-lookup"><span data-stu-id="a59bf-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="a59bf-292">Stały: Obiektów blob z niezdefiniowanego typu zawartości można wygenerować wyjątek</span><span class="sxs-lookup"><span data-stu-id="a59bf-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="a59bf-293">Stała: Otwieranie panelu zapytania na pusta tabela nie było możliwe</span><span class="sxs-lookup"><span data-stu-id="a59bf-293">Fixed: Opening the Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="a59bf-294">Stały: Zmienia się usterki podczas wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a59bf-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="a59bf-295">Zwiększona stałym: Liczba zasobów załadowane z 50 do 100 po kliknięciu przycisku "Obciążenia więcej"</span><span class="sxs-lookup"><span data-stu-id="a59bf-295">Fixed: Increased the number of resources loaded from 50 to 100 when clicking "Load More"</span></span>
* <span data-ttu-id="a59bf-296">Stałe: Przy pierwszym uruchomieniu, jeśli konto jest podpisana, możemy teraz wybrać wszystkie subskrypcje dla tego konta domyślnie</span><span class="sxs-lookup"><span data-stu-id="a59bf-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="a59bf-297">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-297">Known Issues</span></span>

* <span data-ttu-id="a59bf-298">Ta wersja Eksploratora magazynu nie działa w Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="a59bf-298">This release of the Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="a59bf-299">Aby otworzyć wiele kart dla tego samego zasobu, nie stale klikaj tego samego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a59bf-299">To open multiple tabs for the same resource, do not continuously click on the same resource.</span></span> <span data-ttu-id="a59bf-300">Kliknij na inny zasób, a następnie wrócić do poprzedniej strony, a następnie kliknij polecenie pierwotnego zasobu, aby otworzyć go ponownie w innej karty</span><span class="sxs-lookup"><span data-stu-id="a59bf-300">Click on another resource and then go back and then click on the original resource to open it again in another tab</span></span> 
* <span data-ttu-id="a59bf-301">Szybki dostęp działa tylko z elementami subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a59bf-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="a59bf-302">Zasobów lokalnych lub dołączonych za pomocą klucza lub tokenu sygnatury dostępu Współdzielonego zasobów nie są obsługiwane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="a59bf-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="a59bf-303">Może zająć w kilka sekund, aby przejść do zasobu docelowego, w zależności od liczby zasobów, musisz mieć szybki dostęp</span><span class="sxs-lookup"><span data-stu-id="a59bf-303">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="a59bf-304">Mając więcej niż 3 grup obiektów blob lub przekazywania w tym samym czasie plików może powodować błędy</span><span class="sxs-lookup"><span data-stu-id="a59bf-304">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="a59bf-305">Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 — po to, może to mieć wpływ na wydajność lub może spowodować nieobsługiwany wyjątek</span><span class="sxs-lookup"><span data-stu-id="a59bf-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="a59bf-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="a59bf-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="a59bf-307">Wersja 0.8.5</span><span class="sxs-lookup"><span data-stu-id="a59bf-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="a59bf-308">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-308">New</span></span>

* <span data-ttu-id="a59bf-309">Klucze generowane przez Portal SAS mogą teraz używać do dołączenia do przechowywania kont i zasobów</span><span class="sxs-lookup"><span data-stu-id="a59bf-309">Can now use Portal-generated SAS keys to attach to Storage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-310">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-310">Fixes</span></span>

* <span data-ttu-id="a59bf-311">Stała: wyścigu podczas wyszukiwania czasami spowodował węzłów stanie nie można rozwijać się</span><span class="sxs-lookup"><span data-stu-id="a59bf-311">Fixed: race condition during search sometimes caused nodes to become non-expandable</span></span>
* <span data-ttu-id="a59bf-312">Stałych: "Użyj protokołu HTTP" nie działa, podczas nawiązywania połączenia z nazwą konta i klucza konta magazynu</span><span class="sxs-lookup"><span data-stu-id="a59bf-312">Fixed: "Use HTTP" doesn't work when connecting to Storage Accounts with account name and key</span></span>
* <span data-ttu-id="a59bf-313">Stały: Klucze SAS (wygenerowany specjalnie portalu te) zwracają błąd "ukośnikiem na końcu"</span><span class="sxs-lookup"><span data-stu-id="a59bf-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="a59bf-314">Stały: Importowanie tabeli problemów</span><span class="sxs-lookup"><span data-stu-id="a59bf-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="a59bf-315">Czasami klucz partycji i klucz wiersza zostały cofnięte</span><span class="sxs-lookup"><span data-stu-id="a59bf-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="a59bf-316">Nie można odczytać "wartości null" kluczy partycji</span><span class="sxs-lookup"><span data-stu-id="a59bf-316">Unable to read "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a59bf-317">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-317">Known Issues</span></span>

* <span data-ttu-id="a59bf-318">Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 -, wydajność może mieć wpływ na</span><span class="sxs-lookup"><span data-stu-id="a59bf-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="a59bf-319">Stos Azure aktualnie nie obsługuje plików, rozwiń pliki w trakcie wyświetli błąd</span><span class="sxs-lookup"><span data-stu-id="a59bf-319">Azure Stack doesn't currently support Files, so trying to expand Files will show an error</span></span>

<span data-ttu-id="a59bf-320">09/12/2016</span><span class="sxs-lookup"><span data-stu-id="a59bf-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="a59bf-321">Wersja 0.8.4</span><span class="sxs-lookup"><span data-stu-id="a59bf-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="a59bf-322">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-322">New</span></span>

* <span data-ttu-id="a59bf-323">Generowanie linki bezpośrednie do kont magazynu, kontenerów, kolejek, tabel lub udziały plików do udostępniania i obsługuje łatwy dostęp do zasobów — Windows i Mac OS</span><span class="sxs-lookup"><span data-stu-id="a59bf-323">Generate direct links to storage accounts, containers, queues, tables, or file shares for sharing and easy access to your resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="a59bf-324">Wyszukaj kontenerów obiektów blob, tabel, kolejek, udziałów plików lub kont magazynu w polu wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="a59bf-324">Search for your blob containers, tables, queues, file shares, or storage accounts from the search box</span></span>
* <span data-ttu-id="a59bf-325">Teraz można pogrupować klauzul w tabeli konstruktora zapytań</span><span class="sxs-lookup"><span data-stu-id="a59bf-325">You can now group clauses in the table query builder</span></span>
* <span data-ttu-id="a59bf-326">Zmień nazwę i kopiowania/wklejania kontenerów obiektów blob, udziałów plików, tabel, obiektów blob, obiektów blob folderów, plików i katalogów z wewnątrz dołączone sygnatury dostępu Współdzielonego konta i kontenerów</span><span class="sxs-lookup"><span data-stu-id="a59bf-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="a59bf-327">Zmiana nazwy i kopiowania obiektu blob kontenery i udziały plików teraz zachować właściwości i metadane</span><span class="sxs-lookup"><span data-stu-id="a59bf-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-328">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-328">Fixes</span></span>

* <span data-ttu-id="a59bf-329">Stały: nie można edytować jednostek tabeli, gdy właściwości boolean lub binarne</span><span class="sxs-lookup"><span data-stu-id="a59bf-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a59bf-330">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-330">Known Issues</span></span>

* <span data-ttu-id="a59bf-331">Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 -, wydajność może mieć wpływ na</span><span class="sxs-lookup"><span data-stu-id="a59bf-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="a59bf-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="a59bf-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="a59bf-333">Wersja 0.8.3</span><span class="sxs-lookup"><span data-stu-id="a59bf-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="a59bf-334">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-334">New</span></span>

* <span data-ttu-id="a59bf-335">Zmień nazwę kontenerów, tabel, udziałów plików</span><span class="sxs-lookup"><span data-stu-id="a59bf-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="a59bf-336">Udoskonalone środowisko konstruktora zapytań</span><span class="sxs-lookup"><span data-stu-id="a59bf-336">Improved Query builder experience</span></span>
* <span data-ttu-id="a59bf-337">Umożliwia zapisywanie i ładowanie zapytań</span><span class="sxs-lookup"><span data-stu-id="a59bf-337">Ability to save and load queries</span></span>
* <span data-ttu-id="a59bf-338">Bezpośrednie łącza do przechowywania kont lub kontenery, kolejek, tabel lub udziały do udostępniania i łatwe uzyskiwanie dostępu do zasobów plików (tylko Windows - macOS obsługuje wkrótce!)</span><span class="sxs-lookup"><span data-stu-id="a59bf-338">Direct links to storage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="a59bf-339">Możliwość zarządzania i skonfigurować zasady CORS</span><span class="sxs-lookup"><span data-stu-id="a59bf-339">Ability to manage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-340">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-340">Fixes</span></span>

* <span data-ttu-id="a59bf-341">Stały: Accounts Microsoft wymagają ponowne uwierzytelnianie co 8 – 12 godzin</span><span class="sxs-lookup"><span data-stu-id="a59bf-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a59bf-342">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-342">Known Issues</span></span>

* <span data-ttu-id="a59bf-343">Czasami interfejsu użytkownika mogą sprawiać wrażenie — maksymalizacja okna pomaga rozwiązać ten problem</span><span class="sxs-lookup"><span data-stu-id="a59bf-343">Sometimes the UI might appear frozen - maximizing the window helps resolve this issue</span></span>
* <span data-ttu-id="a59bf-344">System macOS instalacji może wymagać podniesionego poziomu uprawnień</span><span class="sxs-lookup"><span data-stu-id="a59bf-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="a59bf-345">Panel ustawień konta mogą być wyświetlane konieczne ponowne wprowadzenie poświadczeń, aby filtrować subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a59bf-345">Account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="a59bf-346">Zmiana nazwy udziałów plików, kontenerów obiektów blob i tabele nie zachowuje metadane lub innych właściwości w kontenerze, takie jak przydziału udziału plików, poziom dostępu publicznego lub zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="a59bf-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on the container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="a59bf-347">Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki.</span><span class="sxs-lookup"><span data-stu-id="a59bf-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="a59bf-348">Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy</span><span class="sxs-lookup"><span data-stu-id="a59bf-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="a59bf-349">Kopiowanie lub zmiana nazwy zasobów nie działa w ramach konta dołączone sygnatury dostępu Współdzielonego</span><span class="sxs-lookup"><span data-stu-id="a59bf-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="a59bf-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="a59bf-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="a59bf-351">Wersja 0.8.2</span><span class="sxs-lookup"><span data-stu-id="a59bf-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="a59bf-352">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-352">New</span></span>

* <span data-ttu-id="a59bf-353">Konta magazynu są pogrupowane według subskrypcji; Programowanie magazynu i zasobów dołączonych za pomocą klucza lub SAS są wyświetlane w węźle (lokalny i załączone)</span><span class="sxs-lookup"><span data-stu-id="a59bf-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="a59bf-354">Wyloguj z konta w panelu "Ustawienia konta Azure"</span><span class="sxs-lookup"><span data-stu-id="a59bf-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="a59bf-355">Skonfiguruj ustawienia serwera proxy, aby włączyć i zarządzać nimi logowania</span><span class="sxs-lookup"><span data-stu-id="a59bf-355">Configure proxy settings to enable and manage sign-in</span></span>
* <span data-ttu-id="a59bf-356">Tworzenie i przerwać dzierżawy obiektów blob</span><span class="sxs-lookup"><span data-stu-id="a59bf-356">Create and break blob leases</span></span>
* <span data-ttu-id="a59bf-357">Kontenery Otwórz obiektów blob, kolejek, tabel i pliki z jednym kliknięciem</span><span class="sxs-lookup"><span data-stu-id="a59bf-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-358">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-358">Fixes</span></span>

* <span data-ttu-id="a59bf-359">Stała: dodaje z bibliotekami .NET lub Java wiadomości w kolejce są nie prawidłowo zdekodować z formatu base64</span><span class="sxs-lookup"><span data-stu-id="a59bf-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="a59bf-360">Stały: $metrics tabele nie są wyświetlane w przypadku kont magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="a59bf-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="a59bf-361">Stały: węzeł tabele nie działa dla lokalnej pamięci masowej (Programowanie)</span><span class="sxs-lookup"><span data-stu-id="a59bf-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a59bf-362">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-362">Known Issues</span></span>

* <span data-ttu-id="a59bf-363">System macOS instalacji może wymagać podniesionego poziomu uprawnień</span><span class="sxs-lookup"><span data-stu-id="a59bf-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="a59bf-364">06/15/2016</span><span class="sxs-lookup"><span data-stu-id="a59bf-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="a59bf-365">Wersja 0.8.0</span><span class="sxs-lookup"><span data-stu-id="a59bf-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="a59bf-366">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-366">New</span></span>

* <span data-ttu-id="a59bf-367">Obsługa udziału plików: wyświetlanie, przekazywanie, pobieranie, kopiowania plików i katalogów, identyfikatory URI SAS (Tworzenie i łączenie)</span><span class="sxs-lookup"><span data-stu-id="a59bf-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="a59bf-368">Udoskonalona obsługa połączenie z magazynem z kluczami identyfikatory URI SAS lub konta</span><span class="sxs-lookup"><span data-stu-id="a59bf-368">Improved user experience for connecting to Storage with SAS URIs or account keys</span></span>
* <span data-ttu-id="a59bf-369">Eksportowanie tabeli wyników zapytania</span><span class="sxs-lookup"><span data-stu-id="a59bf-369">Export table query results</span></span>
* <span data-ttu-id="a59bf-370">Zmienianie kolejności kolumn w tabeli i dostosowywania</span><span class="sxs-lookup"><span data-stu-id="a59bf-370">Table column reordering and customization</span></span>
* <span data-ttu-id="a59bf-371">Wyświetlanie $logs kontenerów obiektów blob i tabelach $metrics dla konta magazynu o metryki włączone</span><span class="sxs-lookup"><span data-stu-id="a59bf-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="a59bf-372">Ulepszone eksportowania i importowania zachowanie, zawiera teraz typ wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="a59bf-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-373">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-373">Fixes</span></span>

* <span data-ttu-id="a59bf-374">Stały: przekazanie lub pobranie dużych obiektów blob może spowodować niekompletne przekazywania/pobieranie</span><span class="sxs-lookup"><span data-stu-id="a59bf-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="a59bf-375">Stały: Edycja, dodanie lub zaimportowanie jednostki z wartością liczbową ciągu ("1") przekonwertuje go podwójne</span><span class="sxs-lookup"><span data-stu-id="a59bf-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it to double</span></span>
* <span data-ttu-id="a59bf-376">Stała: Nie można rozwinąć węzła tabeli w środowisku programistycznym lokalnego</span><span class="sxs-lookup"><span data-stu-id="a59bf-376">Fixed: Unable to expand the table node in the local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a59bf-377">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-377">Known Issues</span></span>

* <span data-ttu-id="a59bf-378">$metrics tabele nie są widoczne dla kont magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="a59bf-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="a59bf-379">Wiadomości w kolejce dodać programistycznie mogą nie być wyświetlane prawidłowo, jeśli komunikaty są zakodowane przy użyciu kodowania Base64</span><span class="sxs-lookup"><span data-stu-id="a59bf-379">Queue messages added programmatically may not be displayed correctly if the messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="a59bf-380">05/17/2016</span><span class="sxs-lookup"><span data-stu-id="a59bf-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="a59bf-381">Wersja 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="a59bf-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="a59bf-382">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-382">New</span></span>

* <span data-ttu-id="a59bf-383">Awarie lepszą obsługę błędów dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="a59bf-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-384">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-384">Fixes</span></span>

* <span data-ttu-id="a59bf-385">Usunięte usterki gdzie komunikaty paska informacyjnego czasami nie są wyświetlane podczas logowania były wymagane</span><span class="sxs-lookup"><span data-stu-id="a59bf-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a59bf-386">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-386">Known Issues</span></span>

* <span data-ttu-id="a59bf-387">Tabele: Dodawanie, edytowanie lub importowanie jednostki, która ma właściwość z wartość ambiguously liczbowego, na przykład "1" lub "1.0", a użytkownik próbuje wysłać go jako `Edm.String`, wartość będzie Wróć za pomocą klienta interfejsu API jako Edm.Double</span><span class="sxs-lookup"><span data-stu-id="a59bf-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and the user tries to send it as an `Edm.String`, the value will come back through the client API as an Edm.Double</span></span>

<span data-ttu-id="a59bf-388">03/31/2016</span><span class="sxs-lookup"><span data-stu-id="a59bf-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="a59bf-389">Wersja 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="a59bf-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="a59bf-390">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-390">New</span></span>

* <span data-ttu-id="a59bf-391">Tabela wsparcia: przeglądanie, wyszukiwanie, eksportu, importowania i operacji CRUD dla jednostek</span><span class="sxs-lookup"><span data-stu-id="a59bf-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="a59bf-392">Kolejka pomocy technicznej: przeglądanie, dodawanie dequeueing wiadomości</span><span class="sxs-lookup"><span data-stu-id="a59bf-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="a59bf-393">Generowanie identyfikatorów URI sygnatury dostępu Współdzielonego dla konta magazynu</span><span class="sxs-lookup"><span data-stu-id="a59bf-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="a59bf-394">Łączenie z kont magazynu identyfikatory URI sygnatury dostępu Współdzielonego</span><span class="sxs-lookup"><span data-stu-id="a59bf-394">Connecting to Storage Accounts with SAS URIs</span></span>
* <span data-ttu-id="a59bf-395">Powiadomienia o aktualizacji dla przyszłych aktualizacji do Eksploratora usługi Storage</span><span class="sxs-lookup"><span data-stu-id="a59bf-395">Update notifications for future updates to Storage Explorer</span></span>
* <span data-ttu-id="a59bf-396">Zaktualizowano wygląd i działanie</span><span class="sxs-lookup"><span data-stu-id="a59bf-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-397">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-397">Fixes</span></span>

* <span data-ttu-id="a59bf-398">Ulepszenia wydajności i niezawodności</span><span class="sxs-lookup"><span data-stu-id="a59bf-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="a59bf-399">Znane problemy &amp; środki zaradcze</span><span class="sxs-lookup"><span data-stu-id="a59bf-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="a59bf-400">Pobieranie plików dużych obiektów blob nie działa prawidłowo — zaleca się używanie AzCopy, podczas gdy ten problem można rozwiązać</span><span class="sxs-lookup"><span data-stu-id="a59bf-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="a59bf-401">Poświadczenia konta nie zostaną pobrane ani Jeśli folder macierzysty nie można odnaleźć lub nie można zapisać w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="a59bf-401">Account credentials will not be retrieved nor cached if the home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="a59bf-402">Jeśli firma Microsoft Dodawanie, edytowanie lub importowanie jednostki, która ma właściwość z wartością ambiguously liczbowego, takie jak "1" lub "1.0", a użytkownik próbuje wysłać go jako `Edm.String`, wartość będzie Wróć za pomocą klienta interfejsu API jako Edm.Double</span><span class="sxs-lookup"><span data-stu-id="a59bf-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and the user tries to send it as an `Edm.String`, the value will come back through the client API as an Edm.Double</span></span>
* <span data-ttu-id="a59bf-403">Podczas importowania plików CSV z rekordami wielowierszowe, dane mogą uzyskać kostki lub zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="a59bf-403">When importing CSV files with multiline records, the data may get chopped or scrambled</span></span>

<span data-ttu-id="a59bf-404">02/03/2016</span><span class="sxs-lookup"><span data-stu-id="a59bf-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="a59bf-405">Wersja 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="a59bf-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-406">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-406">Fixes</span></span>

* <span data-ttu-id="a59bf-407">Poprawia ogólną wydajność podczas przekazywanie, pobieranie i kopiowania obiektów blob</span><span class="sxs-lookup"><span data-stu-id="a59bf-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="a59bf-408">01/14/2016</span><span class="sxs-lookup"><span data-stu-id="a59bf-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="a59bf-409">Wersja 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="a59bf-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="a59bf-410">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-410">New</span></span>

* <span data-ttu-id="a59bf-411">Obsługa systemu Linux (parzystość funkcji do systemu OS x)</span><span class="sxs-lookup"><span data-stu-id="a59bf-411">Linux support (parity features to OSX)</span></span>
* <span data-ttu-id="a59bf-412">Dodaj kontenerów obiektów blob z kluczem dostępu sygnatur dostępu Współdzielonego</span><span class="sxs-lookup"><span data-stu-id="a59bf-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="a59bf-413">Dodawanie konta magazynu dla Chin Azure</span><span class="sxs-lookup"><span data-stu-id="a59bf-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="a59bf-414">Dodawanie konta magazynu z niestandardowe punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="a59bf-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="a59bf-415">Otwieranie i wyświetlanie obiektów blob tekst i obraz zawartości</span><span class="sxs-lookup"><span data-stu-id="a59bf-415">Open and view the contents text and picture blobs</span></span>
* <span data-ttu-id="a59bf-416">Wyświetlanie i edytowanie właściwości obiektów blob i metadanych</span><span class="sxs-lookup"><span data-stu-id="a59bf-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="a59bf-417">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a59bf-417">Fixes</span></span>

* <span data-ttu-id="a59bf-418">Stała: przekazywanie i pobieranie dużą liczbę obiektów blob (500 +) może wywoływać aplikacji na ekranie białe</span><span class="sxs-lookup"><span data-stu-id="a59bf-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause the app to have a white screen</span></span> 
* <span data-ttu-id="a59bf-419">Stały: podczas ustawiania poziomu dostępu publicznego kontenera obiektów blob, nowa wartość nie jest aktualizowane do momentu ponownego Ustaw fokus w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="a59bf-419">Fixed: when setting blob container public access level, the new value is not updated until you re-set the focus on the container.</span></span> <span data-ttu-id="a59bf-420">Ponadto okno dialogowe zawsze domyślnie "Brak dostępu publicznego", a nie rzeczywiste bieżącą wartość.</span><span class="sxs-lookup"><span data-stu-id="a59bf-420">Also, the dialog always defaults to "No public access", and not the actual current value.</span></span>
* <span data-ttu-id="a59bf-421">Obsługa lepszej ogólnej klawiatury/ułatwień dostępu i interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="a59bf-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="a59bf-422">Obszar nawigacji historii zawijany, gdy jest długa z białą przestrzenią</span><span class="sxs-lookup"><span data-stu-id="a59bf-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="a59bf-423">Okno dialogowe SAS obsługuje sprawdzania poprawności danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="a59bf-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="a59bf-424">Lokalny magazyn nadal będzie dostępna, nawet jeśli wygasły poświadczenia użytkownika</span><span class="sxs-lookup"><span data-stu-id="a59bf-424">Local storage continues to be available even if user credentials have expired</span></span>
* <span data-ttu-id="a59bf-425">Usunięcie kontenera obiektów blob otwarty Eksplorator obiektów blob po prawej stronie jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="a59bf-425">When an opened blob container is deleted, the blob explorer on the right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a59bf-426">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-426">Known Issues</span></span>

* <span data-ttu-id="a59bf-427">Instalacja systemu Linux wymaga wersji gcc zaktualizowane lub uaktualnione — kroki niezbędne do uaktualnienia jest poniżej:</span><span class="sxs-lookup"><span data-stu-id="a59bf-427">Linux install needs gcc version updated or upgraded – steps to upgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="a59bf-428">11/18/2015</span><span class="sxs-lookup"><span data-stu-id="a59bf-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="a59bf-429">Wersja 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="a59bf-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="a59bf-430">Nowy</span><span class="sxs-lookup"><span data-stu-id="a59bf-430">New</span></span>

* <span data-ttu-id="a59bf-431">System macOS i wersji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a59bf-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="a59bf-432">Zaloguj się do wyświetlania kont magazynu — użyć konta organizacji, Account firmy Microsoft, 2FA itp.</span><span class="sxs-lookup"><span data-stu-id="a59bf-432">Sign in to view your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="a59bf-433">Lokalne działania projektowe magazynu (użyć emulatora magazynu systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="a59bf-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="a59bf-434">Usługa Azure Resource Manager i Model Klasyczny zasobów pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="a59bf-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="a59bf-435">Tworzenie i usuwanie obiektów blob, kolejek i tabel</span><span class="sxs-lookup"><span data-stu-id="a59bf-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="a59bf-436">Wyszukiwanie określonych obiektów blob, kolejek i tabel</span><span class="sxs-lookup"><span data-stu-id="a59bf-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="a59bf-437">Przejrzyj zawartość kontenerów obiektów blob</span><span class="sxs-lookup"><span data-stu-id="a59bf-437">Explore the contents of blob containers</span></span>
* <span data-ttu-id="a59bf-438">Wyświetlanie i przeglądanie katalogów</span><span class="sxs-lookup"><span data-stu-id="a59bf-438">View and navigate through directories</span></span>
* <span data-ttu-id="a59bf-439">Przekazywanie, pobieranie i usuwanie obiektów blob i folderów</span><span class="sxs-lookup"><span data-stu-id="a59bf-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="a59bf-440">Wyświetlanie i edytowanie właściwości obiektów blob i metadanych</span><span class="sxs-lookup"><span data-stu-id="a59bf-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="a59bf-441">Generuj klucze SAS</span><span class="sxs-lookup"><span data-stu-id="a59bf-441">Generate SAS keys</span></span>
* <span data-ttu-id="a59bf-442">Zarządzanie i utworzyć przechowywane zasad dostępu (SAP)</span><span class="sxs-lookup"><span data-stu-id="a59bf-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="a59bf-443">Wyszukaj obiekty BLOB według prefiksu</span><span class="sxs-lookup"><span data-stu-id="a59bf-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="a59bf-444">Przeciągnij n porzucić przekazywanie lub pobieranie plików</span><span class="sxs-lookup"><span data-stu-id="a59bf-444">Drag 'n drop files to upload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a59bf-445">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a59bf-445">Known Issues</span></span>

* <span data-ttu-id="a59bf-446">Po ustawienie poziomu dostępu publicznego kontenera obiektów blob, nowa wartość nie jest aktualizowany, dopóki nie zostanie ponownie ustawiony fokus w kontenerze</span><span class="sxs-lookup"><span data-stu-id="a59bf-446">When setting blob container public access level, the new value is not updated until you re-set the focus on the container</span></span>
* <span data-ttu-id="a59bf-447">Po otwarciu okna dialogowego, aby ustawić poziom dostępu publicznego będzie zawsze wyświetlana "Brak dostępu publicznego" jako domyślne, a nie rzeczywiste bieżącą wartość</span><span class="sxs-lookup"><span data-stu-id="a59bf-447">When you open the dialog to set the public access level, it always shows "No public access" as the default, and not the actual current value</span></span>
* <span data-ttu-id="a59bf-448">Nie można zmienić nazwy pobrany obiektów blob</span><span class="sxs-lookup"><span data-stu-id="a59bf-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="a59bf-449">Wpisy dziennika aktywności będą czasami "zatrzymywane" w toku stanu, gdy wystąpi błąd i nie jest wyświetlany błąd</span><span class="sxs-lookup"><span data-stu-id="a59bf-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and the error is not displayed</span></span>
* <span data-ttu-id="a59bf-450">Czasami awarii lub włącza całkowicie biały podczas próby przekazywanie lub pobieranie dużą liczbę obiektów blob</span><span class="sxs-lookup"><span data-stu-id="a59bf-450">Sometimes crashes or turns completely white when trying to upload or download a large number of blobs</span></span>
* <span data-ttu-id="a59bf-451">Czasami anulowanie operacji kopiowania nie działa</span><span class="sxs-lookup"><span data-stu-id="a59bf-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="a59bf-452">Podczas tworzenia kontenera (tabeli-obiekt blob/kolejki), jeśli dane wejściowe nieprawidłową nazwę i przejść do tworzenia drugiego, w ramach typu innego kontenera nie można ustawić fokusu na nowy typ</span><span class="sxs-lookup"><span data-stu-id="a59bf-452">During creating a container (blob/queue/table), if you input an invalid name and proceed to create another under a different container type you cannot set focus on the new type</span></span>
* <span data-ttu-id="a59bf-453">Nie można utworzyć nowego folderu, lub zmień nazwę folderu</span><span class="sxs-lookup"><span data-stu-id="a59bf-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md