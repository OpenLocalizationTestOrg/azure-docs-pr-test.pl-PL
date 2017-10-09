---
title: "aaaUsing Eksploratora usługi Storage (wersja zapoznawcza) z usługą Magazyn plików Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Dowiedz się, jak toouse toowork Eksploratora usługi Storage (wersja zapoznawcza) z plików, udziały i pliki."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="66d38-103">Korzystanie z programu Storage Explorer (wersja zapoznawcza) za pośrednictwem usługi Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="66d38-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="66d38-104">Plik Azure magazynu znajduje się, że usługa, która umożliwia pliku udziałów w chmurze hello przy użyciu hello standardowego protokołu bloku komunikatów serwera (SMB).</span><span class="sxs-lookup"><span data-stu-id="66d38-104">Azure File storage is a service that offers file shares in hello cloud using hello standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="66d38-105">Obsługiwane są wersje 2.1 i 3.0 protokołu SMB.</span><span class="sxs-lookup"><span data-stu-id="66d38-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="66d38-106">Magazyn plików Azure można migrować starsze aplikacje korzystające z tooAzure udziały plików szybko i bez kosztownych modyfikacji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="66d38-106">With Azure File storage, you can migrate legacy applications that rely on file shares tooAzure quickly and without costly rewrites.</span></span> <span data-ttu-id="66d38-107">Możesz użyć pliku magazynu tooexpose danych publicznie toohello world lub toostore danych aplikacji prywatnie.</span><span class="sxs-lookup"><span data-stu-id="66d38-107">You can use File storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="66d38-108">W tym artykule dowiesz się, jak toouse toowork Eksploratora usługi Storage (wersja zapoznawcza) z plików, udziały i pliki.</span><span class="sxs-lookup"><span data-stu-id="66d38-108">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66d38-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="66d38-109">Prerequisites</span></span>

<span data-ttu-id="66d38-110">toocomplete hello kroki opisane w tym artykule, będą potrzebne następujące hello:</span><span class="sxs-lookup"><span data-stu-id="66d38-110">toocomplete hello steps in this article, you'll need hello following:</span></span>

- [<span data-ttu-id="66d38-111">Pobieranie i instalowanie Eksploratora usługi Storage (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="66d38-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="66d38-112">Połącz tooa kontem magazynu platformy Azure lub usługi</span><span class="sxs-lookup"><span data-stu-id="66d38-112">Connect tooa Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="66d38-113">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="66d38-113">Create a File Share</span></span>

<span data-ttu-id="66d38-114">Wszystkie pliki muszą znajdować się w udziale plików, który jest po prostu logiczną grupą plików.</span><span class="sxs-lookup"><span data-stu-id="66d38-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="66d38-115">Konto może zawierać nieograniczoną liczbę udziałów plików, a każdy udział może obejmować nieograniczoną liczbę plików.</span><span class="sxs-lookup"><span data-stu-id="66d38-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="66d38-116">Witaj następujące kroki pokazują, jak toocreate, udostępniania plików, w ramach Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="66d38-116">hello following steps illustrate how toocreate a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="66d38-117">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="66d38-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="66d38-118">W okienku po lewej stronie hello rozwiń hello konta magazynu w ramach którego ma zostać hello toocreate udziału plików</span><span class="sxs-lookup"><span data-stu-id="66d38-118">In hello left pane, expand hello storage account within which you wish toocreate hello File Share</span></span>

3. <span data-ttu-id="66d38-119">Kliknij prawym przyciskiem myszy **udziałów plików**i z menu kontekstowego hello — wybierz pozycję **Utwórz udział plików**.</span><span class="sxs-lookup"><span data-stu-id="66d38-119">Right-click **File Shares**, and - from hello context menu - select **Create File Share**.</span></span>

    ![Tworzenie udziału plików](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="66d38-121">Pole tekstowe pojawi się poniżej hello **udziałów plików** folderu.</span><span class="sxs-lookup"><span data-stu-id="66d38-121">A text box will appear below hello **File Shares** folder.</span></span> <span data-ttu-id="66d38-122">Wprowadź nazwę hello udziału plików.</span><span class="sxs-lookup"><span data-stu-id="66d38-122">Enter hello name for your file share.</span></span> <span data-ttu-id="66d38-123">Zobacz hello [udostępnianie reguły nazewnictwa](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) sekcja zawiera listę reguł i ograniczenia dotyczące nazewnictwa udziałów plików.</span><span class="sxs-lookup"><span data-stu-id="66d38-123">See hello [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Nazewnictwo hello udziału](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="66d38-125">Naciśnij klawisz **Enter** podczas done toocreate hello udziału plików lub **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="66d38-125">Press **Enter** when done toocreate hello file share, or **Esc** toocancel.</span></span> <span data-ttu-id="66d38-126">Po pomyślnie utworzono udział plików hello, będzie on wyświetlany w obszarze hello **udziałów plików** folder hello wybranego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="66d38-126">Once hello file share has been successfully created, it will be displayed under hello **File Shares** folder for hello selected storage account.</span></span>

    ![Witaj nowego udziału.](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="66d38-128">Wyświetlanie zawartości udziału plików</span><span class="sxs-lookup"><span data-stu-id="66d38-128">View a file share's contents</span></span>

<span data-ttu-id="66d38-129">Udziały plików zawierają pliki i foldery (które mogą również zawierać pliki).</span><span class="sxs-lookup"><span data-stu-id="66d38-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="66d38-130">Hello następujące kroki ilustrują sposób udostępnienia tooview hello zawartości pliku w Eksploratora usługi Storage (wersja zapoznawcza): +</span><span class="sxs-lookup"><span data-stu-id="66d38-130">hello following steps illustrate how tooview hello contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="66d38-131">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="66d38-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="66d38-132">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello udziału plików mają tooview.</span><span class="sxs-lookup"><span data-stu-id="66d38-132">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="66d38-133">Rozwiń konto magazynu hello **udziałów plików**.</span><span class="sxs-lookup"><span data-stu-id="66d38-133">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="66d38-134">Udział plików kliknij prawym przyciskiem myszy hello konieczność tooview i — wybierz z menu kontekstowego hello - **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="66d38-134">Right-click hello file share you wish tooview, and - from hello context menu - select **Open**.</span></span> <span data-ttu-id="66d38-135">Można także kliknąć dwukrotnie hello udziału plików mają tooview.</span><span class="sxs-lookup"><span data-stu-id="66d38-135">You can also double-click hello file share you wish tooview.</span></span>

    ![Otwieranie udziału](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="66d38-137">Witaj głównego okienku zostaną wyświetlone udziału plików hello zawartość.</span><span class="sxs-lookup"><span data-stu-id="66d38-137">hello main pane will display hello file share's contents.</span></span>
    
    ![Witaj udziału zawartości](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="66d38-139">Usuwanie udziału plików</span><span class="sxs-lookup"><span data-stu-id="66d38-139">Delete a file share</span></span>

<span data-ttu-id="66d38-140">Udziały plików można łatwo tworzyć i usuwać.</span><span class="sxs-lookup"><span data-stu-id="66d38-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="66d38-141">(toosee jak toodelete poszczególnych plików, można znaleźć w sekcji toohello [zarządzania plikami w udziale plików](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="66d38-141">(toosee how toodelete individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="66d38-142">następujące kroki Hello ilustrują sposób toodelete, udostępniania plików, w ramach Eksploratora usługi Storage (wersja zapoznawcza):</span><span class="sxs-lookup"><span data-stu-id="66d38-142">hello following steps illustrate how toodelete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="66d38-143">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="66d38-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="66d38-144">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello udziału plików mają tooview.</span><span class="sxs-lookup"><span data-stu-id="66d38-144">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="66d38-145">Rozwiń konto magazynu hello **udziałów plików**.</span><span class="sxs-lookup"><span data-stu-id="66d38-145">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="66d38-146">Udział plików kliknij prawym przyciskiem myszy hello konieczność toodelete i — wybierz z menu kontekstowego hello - **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="66d38-146">Right-click hello file share you wish toodelete, and - from hello context menu - select **Delete**.</span></span> <span data-ttu-id="66d38-147">Można również nacisnąć **usunąć** toodelete hello aktualnie wybranego pliku udziału.</span><span class="sxs-lookup"><span data-stu-id="66d38-147">You can also press **Delete** toodelete hello currently selected file share.</span></span>

    ![Usuwanie](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="66d38-149">Wybierz **tak** toohello okno dialogowe potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="66d38-149">Select **Yes** toohello confirmation dialog.</span></span>
    
    ![Okno dialogowe potwierdzenia](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="66d38-151">Kopiowanie udziału plików</span><span class="sxs-lookup"><span data-stu-id="66d38-151">Copy a file share</span></span>

<span data-ttu-id="66d38-152">Eksplorator usługi Storage (wersja zapoznawcza) umożliwia toocopy Schowek toohello udziału pliku, a następnie wklej tego udziału pliku do innego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="66d38-152">Storage Explorer (Preview) enables you toocopy a file share toohello clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="66d38-153">(toosee jak toocopy poszczególnych plików, można znaleźć w sekcji toohello [zarządzania plikami w udziale plików](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="66d38-153">(toosee how toocopy individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="66d38-154">Witaj następujące kroki pokazują, jak udostępnić toocopy plik z jednym tooanother konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="66d38-154">hello following steps illustrate how toocopy a file share from one storage account tooanother.</span></span>

1. <span data-ttu-id="66d38-155">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="66d38-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="66d38-156">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello udziału plików mają toocopy.</span><span class="sxs-lookup"><span data-stu-id="66d38-156">In hello left pane, expand hello storage account containing hello file share you wish toocopy.</span></span>

3. <span data-ttu-id="66d38-157">Rozwiń konto magazynu hello **udziałów plików**.</span><span class="sxs-lookup"><span data-stu-id="66d38-157">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="66d38-158">Udział plików kliknij prawym przyciskiem myszy hello konieczność toocopy i — wybierz z menu kontekstowego hello - **udział plików kopii**.</span><span class="sxs-lookup"><span data-stu-id="66d38-158">Right-click hello file share you wish toocopy, and - from hello context menu - select **Copy File Share**.</span></span>

    ![Kopiowanie udziału plików](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="66d38-160">Kliknij prawym przyciskiem myszy konto magazynu Witaj "wartość", do którego chcesz udziału plików hello toopaste, a — wybierz z menu kontekstowego hello - **udział plików Wklej**.</span><span class="sxs-lookup"><span data-stu-id="66d38-160">Right-click hello desired "target" storage account into which you want toopaste hello file share, and - from hello context menu - select **Paste File Share**.</span></span>

    ![Wklejanie udziału plików](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a><span data-ttu-id="66d38-162">Pobierz hello sygnatury dostępu Współdzielonego dla udziału plików</span><span class="sxs-lookup"><span data-stu-id="66d38-162">Get hello SAS for a file share</span></span>

<span data-ttu-id="66d38-163">A [sygnatury dostępu współdzielonego (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) zapewnia dostęp delegowany tooresources na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="66d38-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="66d38-164">Oznacza to, że można udzielać się, że klient ograniczone uprawnienia tooobjects na koncie magazynu w określonym przedziale czasu i z określonym zestawem uprawnień, bez konieczności tooshare klucze dostępu do Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="66d38-164">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span>

<span data-ttu-id="66d38-165">Witaj poniższe kroki przedstawiają sposób toocreate sygnatury dostępu Współdzielonego dla pliku udziału: +</span><span class="sxs-lookup"><span data-stu-id="66d38-165">hello following steps illustrate how toocreate a SAS for a file share:+</span></span>

1. <span data-ttu-id="66d38-166">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="66d38-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="66d38-167">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello udziału plików, dla którego chcesz tooget sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="66d38-167">In hello left pane, expand hello storage account containing hello file share for which you wish tooget a SAS.</span></span>

3. <span data-ttu-id="66d38-168">Rozwiń konto magazynu hello **udziałów plików**.</span><span class="sxs-lookup"><span data-stu-id="66d38-168">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="66d38-169">Kliknij prawym przyciskiem myszy hello udziału żądanego pliku i z menu kontekstowego hello — wybierz pozycję **Uzyskaj sygnaturę dostępu współdzielonego**.</span><span class="sxs-lookup"><span data-stu-id="66d38-169">Right-click hello desired file share, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

    ![Uzyskiwanie sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="66d38-171">W hello **sygnatura dostępu współdzielonego** okna dialogowego, określ hello zasad, daty rozpoczęcia i wygaśnięcia, strefy czasowej, a dla zasobu hello poziomy dostępu.</span><span class="sxs-lookup"><span data-stu-id="66d38-171">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

    ![Okno dialogowe sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="66d38-173">Po zakończeniu określenie opcji SAS hello wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="66d38-173">When you're finished specifying hello SAS options, select **Create**.</span></span>

7. <span data-ttu-id="66d38-174">Drugi **sygnatura dostępu współdzielonego** okna dialogowego zostanie następnie wyświetlona, że listy hello udziału plików wraz z adresu URL hello i QueryStrings można użyć tooaccess hello zasobów magazynu.</span><span class="sxs-lookup"><span data-stu-id="66d38-174">A second **Shared Access Signature** dialog will then display that lists hello file share along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span> <span data-ttu-id="66d38-175">Wybierz **kopiowania** dalej toohello adres URL ma toocopy toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="66d38-175">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>
    
    ![Drugie okno dialogowe Sygnatura dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="66d38-177">Po zakończeniu wybierz pozycję **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="66d38-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="66d38-178">Zarządzanie zasadami dostępu dla udziału plików</span><span class="sxs-lookup"><span data-stu-id="66d38-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="66d38-179">Witaj poniższe kroki przedstawiają sposób toomanage (Dodaj i Usuń) zasady dla udziału plików dostępu: +.</span><span class="sxs-lookup"><span data-stu-id="66d38-179">hello following steps illustrate how toomanage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="66d38-180">Zasady dostępu Hello jest używane do tworzenia adresów URL SAS za pośrednictwem której osoby mogą używać hello tooaccess zasobu magazynu plików w zdefiniowanym okresie.</span><span class="sxs-lookup"><span data-stu-id="66d38-180">hello Access Policies is used for creating SAS URLs through which people can use tooaccess hello Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="66d38-181">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="66d38-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="66d38-182">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające udziału plików hello zasad dostępu, którego chcesz toomanage.</span><span class="sxs-lookup"><span data-stu-id="66d38-182">In hello left pane, expand hello storage account containing hello file share whose access policies you wish toomanage.</span></span>

3. <span data-ttu-id="66d38-183">Rozwiń konto magazynu hello **udziałów plików**.</span><span class="sxs-lookup"><span data-stu-id="66d38-183">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="66d38-184">Wybierz udział żądanego pliku hello i — wybierz z menu kontekstowego hello - **Zarządzanie zasadami dostępu**.</span><span class="sxs-lookup"><span data-stu-id="66d38-184">Select hello desired file share, and - from hello context menu - select **Manage Access Policies**.</span></span>

    ![Menu kontekstowe Zarządzanie zasadami dostępu](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="66d38-186">Witaj **zasady dostępu** okno dialogowe wyświetla wszystkie zasady dostępu dla udziału plików wybranych hello już utworzony.</span><span class="sxs-lookup"><span data-stu-id="66d38-186">hello **Access Policies** dialog will list any access policies already created for hello selected file share.</span></span>
    
    ![Zasady dostępu](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="66d38-188">Wykonaj następujące kroki w zależności od zadania zarządzania zasadami dostępu hello:</span><span class="sxs-lookup"><span data-stu-id="66d38-188">Follow these steps depending on hello access policy management task:</span></span>
    
    - <span data-ttu-id="66d38-189">**Dodawanie nowych zasad dostępu** — wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="66d38-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="66d38-190">Wygenerowany hello **zasady dostępu** hello nowo dodanych do wyświetlenia okna dialogowego dostęp zasad (przy użyciu ustawień domyślnych).</span><span class="sxs-lookup"><span data-stu-id="66d38-190">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="66d38-191">**Edytowanie zasad dostępu** — wykonaj wszystkie żądane operacje edycji, a następnie wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="66d38-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="66d38-192">**Usuń zasady dostępu** — wybierz tę opcję **Usuń** dalej toohello zasady dostępu mają tooremove.</span><span class="sxs-lookup"><span data-stu-id="66d38-192">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

7. <span data-ttu-id="66d38-193">Utwórz nowy adres URL sygnatury dostępu Współdzielonego przy użyciu hello utworzoną wcześniej zasad dostępu:</span><span class="sxs-lookup"><span data-stu-id="66d38-193">Create a new SAS URL using hello Access Policy you created earlier:</span></span>
    
    ![Pobieranie sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nazwa i właściwości sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="66d38-196">Zarządzanie plikami w udziale plików</span><span class="sxs-lookup"><span data-stu-id="66d38-196">Managing files in a file share</span></span>

<span data-ttu-id="66d38-197">Po utworzeniu udziału plików można przekazać pliku toothat udziału plików, Pobierz plik tooyour komputera lokalnego, otwórz plik na komputerze lokalnym i wiele innych.</span><span class="sxs-lookup"><span data-stu-id="66d38-197">Once you've created a file share, you can upload a file toothat file share, download a file tooyour local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="66d38-198">Witaj poniższe kroki przedstawiają jak udostępnić toomanage hello plików (i foldery) w pliku.</span><span class="sxs-lookup"><span data-stu-id="66d38-198">hello following steps illustrate how toomanage hello files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="66d38-199">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="66d38-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="66d38-200">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello udziału plików mają toomanage.</span><span class="sxs-lookup"><span data-stu-id="66d38-200">In hello left pane, expand hello storage account containing hello file share you wish toomanage.</span></span>

3.  <span data-ttu-id="66d38-201">Rozwiń konto magazynu hello **udziałów plików**.</span><span class="sxs-lookup"><span data-stu-id="66d38-201">Expand hello storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="66d38-202">Kliknij dwukrotnie hello udziału plików mają tooview.</span><span class="sxs-lookup"><span data-stu-id="66d38-202">Double-click hello file share you wish tooview.</span></span>

5.  <span data-ttu-id="66d38-203">Witaj głównego okienku zostaną wyświetlone udziału plików hello zawartość.</span><span class="sxs-lookup"><span data-stu-id="66d38-203">hello main pane will display hello file share's contents.</span></span>

    ![Witaj udziału zawartości](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="66d38-205">Witaj głównego okienku zostaną wyświetlone udziału plików hello zawartość.</span><span class="sxs-lookup"><span data-stu-id="66d38-205">hello main pane will display hello file share's contents.</span></span>

7.  <span data-ttu-id="66d38-206">Wykonaj następujące kroki w zależności od zadania hello mają tooperform:</span><span class="sxs-lookup"><span data-stu-id="66d38-206">Follow these steps depending on hello task you wish tooperform:</span></span>

    - <span data-ttu-id="66d38-207">**Przekaż udziału plików tooa plików**</span><span class="sxs-lookup"><span data-stu-id="66d38-207">**Upload files tooa file share**</span></span>

        <span data-ttu-id="66d38-208">a.</span><span class="sxs-lookup"><span data-stu-id="66d38-208">a.</span></span>  <span data-ttu-id="66d38-209">W okienku głównym hello narzędzi, wybierz **przekazać**, a następnie **Przekaż** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="66d38-209">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Przekazywanie plików](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="66d38-211">b.</span><span class="sxs-lookup"><span data-stu-id="66d38-211">b.</span></span> <span data-ttu-id="66d38-212">W hello **przekazać pliki** okno dialogowe, wybierz hello wielokropka (**...** ) przycisku po prawej stronie powitania hello **pliki** tooselect hello pliki mają tooupload polu tekstowym.</span><span class="sxs-lookup"><span data-stu-id="66d38-212">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Dodawanie plików](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="66d38-214">c.</span><span class="sxs-lookup"><span data-stu-id="66d38-214">c.</span></span> <span data-ttu-id="66d38-215">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="66d38-215">Select **Upload**.</span></span>

    - <span data-ttu-id="66d38-216">**Przekaż udziału plików tooa folderu**</span><span class="sxs-lookup"><span data-stu-id="66d38-216">**Upload a folder tooa file share**</span></span>
        
        <span data-ttu-id="66d38-217">a.</span><span class="sxs-lookup"><span data-stu-id="66d38-217">a.</span></span> <span data-ttu-id="66d38-218">Na pasku narzędzi w okienku głównym hello, wybierz **przekazać**, a następnie **przekazać folderu** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="66d38-218">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menu Przekaż folder](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="66d38-220">b.</span><span class="sxs-lookup"><span data-stu-id="66d38-220">b.</span></span> <span data-ttu-id="66d38-221">W hello **folder przekazywania** okno dialogowe, wybierz hello wielokropka (**...** ) przycisku po prawej stronie powitania hello **folderu** tekst pola tooselect hello folder zawartości, którego chcesz tooupload.</span><span class="sxs-lookup"><span data-stu-id="66d38-221">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        <span data-ttu-id="66d38-222">c.</span><span class="sxs-lookup"><span data-stu-id="66d38-222">c.</span></span> <span data-ttu-id="66d38-223">Opcjonalnie określ folder docelowy, w których hello zostanie przekazany zawartość wybranego folderu.</span><span class="sxs-lookup"><span data-stu-id="66d38-223">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="66d38-224">Witaj, folder docelowy nie istnieje, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="66d38-224">If hello target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="66d38-225">d.</span><span class="sxs-lookup"><span data-stu-id="66d38-225">d.</span></span> <span data-ttu-id="66d38-226">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="66d38-226">Select **Upload**.</span></span>

    - <span data-ttu-id="66d38-227">**Pobierz plik tooyour komputera lokalnego**</span><span class="sxs-lookup"><span data-stu-id="66d38-227">**Download a file tooyour local computer**</span></span>
        
        <span data-ttu-id="66d38-228">a.</span><span class="sxs-lookup"><span data-stu-id="66d38-228">a.</span></span> <span data-ttu-id="66d38-229">Wybierz plik hello mają toodownload.</span><span class="sxs-lookup"><span data-stu-id="66d38-229">Select hello file you wish toodownload.</span></span>
        
        <span data-ttu-id="66d38-230">b.</span><span class="sxs-lookup"><span data-stu-id="66d38-230">b.</span></span> <span data-ttu-id="66d38-231">W okienku głównym hello narzędzi wybierz **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="66d38-231">On hello main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="66d38-232">c.</span><span class="sxs-lookup"><span data-stu-id="66d38-232">c.</span></span> <span data-ttu-id="66d38-233">W hello **Określ, gdzie toosave hello pobrany plik** okna dialogowego, określ hello lokalizację pliku hello pobrane i hello nazwę mają toogive go.</span><span class="sxs-lookup"><span data-stu-id="66d38-233">In hello **Specify where toosave hello downloaded file** dialog, specify hello location where you want hello file downloaded, and hello name you wish toogive it.</span></span>

        <span data-ttu-id="66d38-234">d.</span><span class="sxs-lookup"><span data-stu-id="66d38-234">d.</span></span> <span data-ttu-id="66d38-235">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="66d38-235">Select **Save**.</span></span>

    - <span data-ttu-id="66d38-236">**Otwieranie pliku na komputerze lokalnym**</span><span class="sxs-lookup"><span data-stu-id="66d38-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="66d38-237">a.</span><span class="sxs-lookup"><span data-stu-id="66d38-237">a.</span></span>  <span data-ttu-id="66d38-238">Wybierz plik hello mają tooopen.</span><span class="sxs-lookup"><span data-stu-id="66d38-238">Select hello file you wish tooopen.</span></span>
        
        <span data-ttu-id="66d38-239">b.</span><span class="sxs-lookup"><span data-stu-id="66d38-239">b.</span></span>  <span data-ttu-id="66d38-240">W okienku głównym hello narzędzi wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="66d38-240">On hello main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="66d38-241">c.</span><span class="sxs-lookup"><span data-stu-id="66d38-241">c.</span></span>  <span data-ttu-id="66d38-242">Plik Hello zostaną pobrane i otworzyć przy użyciu aplikacji hello skojarzonej z hello podstawowy typ pliku.</span><span class="sxs-lookup"><span data-stu-id="66d38-242">hello file will be downloaded and opened using hello application associated with hello file's underlying file type.</span></span>

    - <span data-ttu-id="66d38-243">**Skopiuj plik toohello Schowka**</span><span class="sxs-lookup"><span data-stu-id="66d38-243">**Copy a file toohello clipboard**</span></span>

        <span data-ttu-id="66d38-244">a.</span><span class="sxs-lookup"><span data-stu-id="66d38-244">a.</span></span> <span data-ttu-id="66d38-245">Wybierz plik hello mają toocopy.</span><span class="sxs-lookup"><span data-stu-id="66d38-245">Select hello file you wish toocopy.</span></span>

        <span data-ttu-id="66d38-246">b.</span><span class="sxs-lookup"><span data-stu-id="66d38-246">b.</span></span> <span data-ttu-id="66d38-247">W okienku głównym hello narzędzi wybierz **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="66d38-247">On hello main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="66d38-248">c.</span><span class="sxs-lookup"><span data-stu-id="66d38-248">c.</span></span> <span data-ttu-id="66d38-249">W okienku po lewej stronie powitania, przejdź do udziału plików tooanother i kliknij ją dwukrotnie tooview w okienku głównym hello.</span><span class="sxs-lookup"><span data-stu-id="66d38-249">In hello left pane, navigate tooanother file share, and double-click it tooview it in hello main pane.</span></span>

        <span data-ttu-id="66d38-250">d.</span><span class="sxs-lookup"><span data-stu-id="66d38-250">d.</span></span> <span data-ttu-id="66d38-251">W okienku głównym hello narzędzi wybierz **Wklej** toocreate kopię pliku hello.</span><span class="sxs-lookup"><span data-stu-id="66d38-251">On hello main pane's toolbar, select **Paste** toocreate a copy of hello file.</span></span>

    - <span data-ttu-id="66d38-252">**Usuwanie pliku**</span><span class="sxs-lookup"><span data-stu-id="66d38-252">**Delete a file**</span></span>

        <span data-ttu-id="66d38-253">a.</span><span class="sxs-lookup"><span data-stu-id="66d38-253">a.</span></span> <span data-ttu-id="66d38-254">Wybierz plik hello mają toodelete.</span><span class="sxs-lookup"><span data-stu-id="66d38-254">Select hello file you wish toodelete.</span></span>

        <span data-ttu-id="66d38-255">b.</span><span class="sxs-lookup"><span data-stu-id="66d38-255">b.</span></span> <span data-ttu-id="66d38-256">W okienku głównym hello narzędzi wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="66d38-256">On hello main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="66d38-257">c.</span><span class="sxs-lookup"><span data-stu-id="66d38-257">c.</span></span> <span data-ttu-id="66d38-258">Wybierz **tak** toohello okno dialogowe potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="66d38-258">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66d38-259">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="66d38-259">Next steps</span></span>

- <span data-ttu-id="66d38-260">Widok hello [najnowsze informacje o wersji Eksploratora usługi Storage (wersja zapoznawcza) i filmy wideo](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="66d38-260">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="66d38-261">Dowiedz się, jak za[tworzenie aplikacji przy użyciu Azure blob, tabel, kolejek i plików](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="66d38-261">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
