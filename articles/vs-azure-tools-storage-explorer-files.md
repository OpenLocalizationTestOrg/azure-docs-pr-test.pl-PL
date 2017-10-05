---
title: "Korzystanie z programu Storage Explorer (wersja zapoznawcza) za pośrednictwem usługi Azure File Storage | Microsoft Docs"
description: "Dowiedz się, jak korzystać z programu Storage Explorer (wersja zapoznawcza) w celu pracy z udziałami plików i plikami."
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
ms.openlocfilehash: 964691758254531cb92a5b1cbe055ef61d25dba8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="95157-103">Korzystanie z programu Storage Explorer (wersja zapoznawcza) za pośrednictwem usługi Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="95157-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="95157-104">Azure File Storage to usługa, która umożliwia korzystanie z udziałów plików w chmurze przy użyciu standardowego protokołu bloku komunikatów serwera (SMB, Server Message Block).</span><span class="sxs-lookup"><span data-stu-id="95157-104">Azure File storage is a service that offers file shares in the cloud using the standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="95157-105">Obsługiwane są wersje 2.1 i 3.0 protokołu SMB.</span><span class="sxs-lookup"><span data-stu-id="95157-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="95157-106">W usłudze Magazyn plików Azure można migrować starsze aplikacje korzystające z udziałów plików na platformę Azure szybko i bez kosztownych modyfikacji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="95157-106">With Azure File storage, you can migrate legacy applications that rely on file shares to Azure quickly and without costly rewrites.</span></span> <span data-ttu-id="95157-107">Usługa File Storage może być używana do udostępniania danych publicznie lub do przechowywania danych aplikacji prywatnie.</span><span class="sxs-lookup"><span data-stu-id="95157-107">You can use File storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="95157-108">Ten artykuł zawiera informacje dotyczące sposobu korzystania z programu Storage Explorer (wersja zapoznawcza) w celu pracy z udziałami plików i plikami.</span><span class="sxs-lookup"><span data-stu-id="95157-108">In this article, you'll learn how to use Storage Explorer (Preview) to work with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95157-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="95157-109">Prerequisites</span></span>

<span data-ttu-id="95157-110">Do wykonania kroków opisanych w tym artykule konieczne jest wykonanie kroków znajdujących się w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="95157-110">To complete the steps in this article, you'll need the following:</span></span>

- [<span data-ttu-id="95157-111">Pobieranie i instalowanie Eksploratora usługi Storage (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="95157-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="95157-112">Łączenie się z usługą lub kontem magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="95157-112">Connect to a Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="95157-113">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="95157-113">Create a File Share</span></span>

<span data-ttu-id="95157-114">Wszystkie pliki muszą znajdować się w udziale plików, który jest po prostu logiczną grupą plików.</span><span class="sxs-lookup"><span data-stu-id="95157-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="95157-115">Konto może zawierać nieograniczoną liczbę udziałów plików, a każdy udział może obejmować nieograniczoną liczbę plików.</span><span class="sxs-lookup"><span data-stu-id="95157-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="95157-116">Poniższe kroki ilustrują tworzenie udziału plików w programie Storage Explorer (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="95157-116">The following steps illustrate how to create a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="95157-117">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="95157-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="95157-118">W okienku po lewej stronie rozwiń konto magazynu, w którym chcesz utworzyć udział plików</span><span class="sxs-lookup"><span data-stu-id="95157-118">In the left pane, expand the storage account within which you wish to create the File Share</span></span>

3. <span data-ttu-id="95157-119">Kliknij prawym przyciskiem myszy pozycję **Udziały plików**, a następnie z menu kontekstowego wybierz pozycję **Utwórz udział plików**.</span><span class="sxs-lookup"><span data-stu-id="95157-119">Right-click **File Shares**, and - from the context menu - select **Create File Share**.</span></span>

    ![Tworzenie udziału plików](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="95157-121">Poniżej folderu **Udziały plików** zostanie wyświetlone pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="95157-121">A text box will appear below the **File Shares** folder.</span></span> <span data-ttu-id="95157-122">Wprowadź nazwę udziału plików.</span><span class="sxs-lookup"><span data-stu-id="95157-122">Enter the name for your file share.</span></span> <span data-ttu-id="95157-123">Lista reguł i ograniczeń dotyczących nazewnictwa udziałów plików znajduje się w sekcji [Reguły nazewnictwa udziałów](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container).</span><span class="sxs-lookup"><span data-stu-id="95157-123">See the [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Nazywanie udziału](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="95157-125">Naciśnij klawisz **Enter** po zakończeniu tworzenia udziału plików lub klawisz **Esc**, aby anulować.</span><span class="sxs-lookup"><span data-stu-id="95157-125">Press **Enter** when done to create the file share, or **Esc** to cancel.</span></span> <span data-ttu-id="95157-126">Po pomyślnym utworzeniu udział plików zostanie wyświetlony w folderze **Udziały plików** dla wybranego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="95157-126">Once the file share has been successfully created, it will be displayed under the **File Shares** folder for the selected storage account.</span></span>

    ![Nowy udział](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="95157-128">Wyświetlanie zawartości udziału plików</span><span class="sxs-lookup"><span data-stu-id="95157-128">View a file share's contents</span></span>

<span data-ttu-id="95157-129">Udziały plików zawierają pliki i foldery (które mogą również zawierać pliki).</span><span class="sxs-lookup"><span data-stu-id="95157-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="95157-130">Poniższe kroki ilustrują wyświetlanie zawartości udziału plików w programie Storage Explorer (wersja zapoznawcza):</span><span class="sxs-lookup"><span data-stu-id="95157-130">The following steps illustrate how to view the contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="95157-131">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="95157-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="95157-132">W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, który chcesz wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="95157-132">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="95157-133">Rozwiń pozycję **Udziały plików** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="95157-133">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="95157-134">Kliknij prawym przyciskiem myszy udział plików, który chcesz wyświetlić, a następnie z menu kontekstowego wybierz pozycję **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="95157-134">Right-click the file share you wish to view, and - from the context menu - select **Open**.</span></span> <span data-ttu-id="95157-135">Możesz także kliknąć dwukrotnie udział plików, który chcesz wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="95157-135">You can also double-click the file share you wish to view.</span></span>

    ![Otwieranie udziału](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="95157-137">W okienku głównym zostanie wyświetlona zawartość udziału plików.</span><span class="sxs-lookup"><span data-stu-id="95157-137">The main pane will display the file share's contents.</span></span>
    
    ![Zawartość udziału](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="95157-139">Usuwanie udziału plików</span><span class="sxs-lookup"><span data-stu-id="95157-139">Delete a file share</span></span>

<span data-ttu-id="95157-140">Udziały plików można łatwo tworzyć i usuwać.</span><span class="sxs-lookup"><span data-stu-id="95157-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="95157-141">Informacje na temat sposobu usuwania pojedynczych plików zawiera sekcja [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) (Zarządzanie plikami w udziale plików).</span><span class="sxs-lookup"><span data-stu-id="95157-141">(To see how to delete individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="95157-142">Poniższe kroki ilustrują usuwanie udziału plików w programie Storage Explorer (wersja zapoznawcza):</span><span class="sxs-lookup"><span data-stu-id="95157-142">The following steps illustrate how to delete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="95157-143">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="95157-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="95157-144">W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, który chcesz wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="95157-144">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="95157-145">Rozwiń pozycję **Udziały plików** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="95157-145">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="95157-146">Kliknij prawym przyciskiem myszy udział plików, który chcesz usunąć, a następnie z menu kontekstowego wybierz pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="95157-146">Right-click the file share you wish to delete, and - from the context menu - select **Delete**.</span></span> <span data-ttu-id="95157-147">Możesz również nacisnąć klawisz **Delete**, aby usunąć aktualnie wybrany udział plików.</span><span class="sxs-lookup"><span data-stu-id="95157-147">You can also press **Delete** to delete the currently selected file share.</span></span>

    ![Usuwanie](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="95157-149">Wybierz pozycję **Tak** w oknie dialogowym potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="95157-149">Select **Yes** to the confirmation dialog.</span></span>
    
    ![Okno dialogowe potwierdzenia](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="95157-151">Kopiowanie udziału plików</span><span class="sxs-lookup"><span data-stu-id="95157-151">Copy a file share</span></span>

<span data-ttu-id="95157-152">Program Storage Explorer (wersja zapoznawcza) umożliwia kopiowanie udziału pliku do schowka, a następnie wklejanie go do innego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="95157-152">Storage Explorer (Preview) enables you to copy a file share to the clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="95157-153">Informacje na temat sposobu kopiowania pojedynczych plików zawiera sekcja [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) (Zarządzanie plikami w udziale plików).</span><span class="sxs-lookup"><span data-stu-id="95157-153">(To see how to copy individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="95157-154">Poniższe kroki ilustrują kopiowanie udziału plików z jednego konta magazynu do innego.</span><span class="sxs-lookup"><span data-stu-id="95157-154">The following steps illustrate how to copy a file share from one storage account to another.</span></span>

1. <span data-ttu-id="95157-155">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="95157-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="95157-156">W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, który chcesz skopiować.</span><span class="sxs-lookup"><span data-stu-id="95157-156">In the left pane, expand the storage account containing the file share you wish to copy.</span></span>

3. <span data-ttu-id="95157-157">Rozwiń pozycję **Udziały plików** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="95157-157">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="95157-158">Kliknij prawym przyciskiem myszy udział plików, który chcesz skopiować, a następnie z menu kontekstowego wybierz pozycję **Kopiuj udział plików**.</span><span class="sxs-lookup"><span data-stu-id="95157-158">Right-click the file share you wish to copy, and - from the context menu - select **Copy File Share**.</span></span>

    ![Kopiowanie udziału plików](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="95157-160">Kliknij prawym przyciskiem myszy żądane „docelowe” konto magazynu, do którego chcesz wkleić udział plików, a następnie z menu kontekstowego wybierz pozycję **Wklej udział plików**.</span><span class="sxs-lookup"><span data-stu-id="95157-160">Right-click the desired "target" storage account into which you want to paste the file share, and - from the context menu - select **Paste File Share**.</span></span>

    ![Wklejanie udziału plików](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-the-sas-for-a-file-share"></a><span data-ttu-id="95157-162">Uzyskiwanie sygnatury dostępu współdzielonego dla udziału plików</span><span class="sxs-lookup"><span data-stu-id="95157-162">Get the SAS for a file share</span></span>

<span data-ttu-id="95157-163">[Sygnatura dostępu współdzielonego (SAS, shared access signature)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) zapewnia delegowany dostęp do zasobów w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="95157-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="95157-164">Oznacza to, że możliwe jest przyznanie klientowi ograniczonych uprawnień do obiektów w ramach konta magazynu na określony czas i z określonym zestawem uprawnień bez konieczności udostępniania kluczy dostępu do konta.</span><span class="sxs-lookup"><span data-stu-id="95157-164">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="95157-165">Poniższe kroki ilustrują tworzenie sygnatury dostępu współdzielonego dla udziału plików:</span><span class="sxs-lookup"><span data-stu-id="95157-165">The following steps illustrate how to create a SAS for a file share:+</span></span>

1. <span data-ttu-id="95157-166">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="95157-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="95157-167">W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, dla którego ma zostać uzyskana sygnatura dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="95157-167">In the left pane, expand the storage account containing the file share for which you wish to get a SAS.</span></span>

3. <span data-ttu-id="95157-168">Rozwiń pozycję **Udziały plików** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="95157-168">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="95157-169">Kliknij prawym przyciskiem myszy żądany udział plików, a następnie z menu kontekstowego wybierz pozycję **Uzyskaj sygnaturę dostępu współdzielonego**.</span><span class="sxs-lookup"><span data-stu-id="95157-169">Right-click the desired file share, and - from the context menu - select **Get Shared Access Signature**.</span></span>

    ![Uzyskiwanie sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="95157-171">W oknie dialogowym **Sygnatura dostępu współdzielonego** określ zasady, daty rozpoczęcia i wygaśnięcia, strefę czasową oraz poziomy dostępu dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="95157-171">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

    ![Okno dialogowe sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="95157-173">Po zakończeniu określania opcji sygnatury dostępu współdzielonego wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="95157-173">When you're finished specifying the SAS options, select **Create**.</span></span>

7. <span data-ttu-id="95157-174">Zostanie wyświetlone drugie okno dialogowe **Sygnatura dostępu współdzielonego** zawierające listę udziałów plików wraz z adresami URL i ciągami zapytań umożliwiającymi dostęp do zasobu magazynu.</span><span class="sxs-lookup"><span data-stu-id="95157-174">A second **Shared Access Signature** dialog will then display that lists the file share along with the URL and QueryStrings you can use to access the storage resource.</span></span> <span data-ttu-id="95157-175">Wybierz pozycję **Kopiuj** obok adres URL, który chcesz skopiować do schowka.</span><span class="sxs-lookup"><span data-stu-id="95157-175">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>
    
    ![Drugie okno dialogowe Sygnatura dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="95157-177">Po zakończeniu wybierz pozycję **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="95157-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="95157-178">Zarządzanie zasadami dostępu dla udziału plików</span><span class="sxs-lookup"><span data-stu-id="95157-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="95157-179">Poniższe kroki ilustrują zarządzanie (dodawanie i usuwanie) zasadami dostępu dla udziału plików.</span><span class="sxs-lookup"><span data-stu-id="95157-179">The following steps illustrate how to manage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="95157-180">Zasady dostępu są używane do tworzenia adresów URL sygnatur dostępu współdzielonego, za pomocą których użytkownicy mogą uzyskiwać dostęp do zasobów pliku magazynu przez zdefiniowany okres.</span><span class="sxs-lookup"><span data-stu-id="95157-180">The Access Policies is used for creating SAS URLs through which people can use to access the Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="95157-181">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="95157-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="95157-182">W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, którego zasadami dostępu chcesz zarządzać.</span><span class="sxs-lookup"><span data-stu-id="95157-182">In the left pane, expand the storage account containing the file share whose access policies you wish to manage.</span></span>

3. <span data-ttu-id="95157-183">Rozwiń pozycję **Udziały plików** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="95157-183">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="95157-184">Wybierz żądany udział plików, a następnie z menu kontekstowego wybierz pozycję **Zarządzaj zasadami dostępu**.</span><span class="sxs-lookup"><span data-stu-id="95157-184">Select the desired file share, and - from the context menu - select **Manage Access Policies**.</span></span>

    ![Menu kontekstowe Zarządzanie zasadami dostępu](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="95157-186">W oknie dialogowym **Zasady dostępu** zostanie wyświetlona lista wszystkich zasad dostępu, które zostały już utworzone dla wybranego udziału plików.</span><span class="sxs-lookup"><span data-stu-id="95157-186">The **Access Policies** dialog will list any access policies already created for the selected file share.</span></span>
    
    ![Zasady dostępu](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="95157-188">Wykonaj następujące kroki w zależności od zadania zarządzania zasadami dostępu:</span><span class="sxs-lookup"><span data-stu-id="95157-188">Follow these steps depending on the access policy management task:</span></span>
    
    - <span data-ttu-id="95157-189">**Dodawanie nowych zasad dostępu** — wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="95157-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="95157-190">Po wygenerowaniu w oknie dialogowym **Zasady dostępu** będą wyświetlane nowo dodane zasady dostępu (przy użyciu ustawień domyślnych).</span><span class="sxs-lookup"><span data-stu-id="95157-190">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="95157-191">**Edytowanie zasad dostępu** — wykonaj wszystkie żądane operacje edycji, a następnie wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="95157-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="95157-192">**Usuwanie zasad dostępu** — wybierz pozycję **Usuń** obok zasad dostępu, które chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="95157-192">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

7. <span data-ttu-id="95157-193">Utwórz nowy adres URL sygnatury dostępu współdzielonego za pomocą utworzonych wcześniej zasad dostępu:</span><span class="sxs-lookup"><span data-stu-id="95157-193">Create a new SAS URL using the Access Policy you created earlier:</span></span>
    
    ![Pobieranie sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nazwa i właściwości sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="95157-196">Zarządzanie plikami w udziale plików</span><span class="sxs-lookup"><span data-stu-id="95157-196">Managing files in a file share</span></span>

<span data-ttu-id="95157-197">Po utworzeniu udziału plików można do niego przekazać plik, pobrać plik na komputer lokalny, otworzyć plik na komputerze lokalnym i wykonać wiele innych operacji.</span><span class="sxs-lookup"><span data-stu-id="95157-197">Once you've created a file share, you can upload a file to that file share, download a file to your local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="95157-198">Poniższe kroki ilustrują zarządzanie plikami (i folderami) w udziale plików.</span><span class="sxs-lookup"><span data-stu-id="95157-198">The following steps illustrate how to manage the files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="95157-199">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="95157-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="95157-200">W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, którym chcesz zarządzać.</span><span class="sxs-lookup"><span data-stu-id="95157-200">In the left pane, expand the storage account containing the file share you wish to manage.</span></span>

3.  <span data-ttu-id="95157-201">Rozwiń pozycję **Udziały plików** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="95157-201">Expand the storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="95157-202">Dwukrotnie kliknij udział plików, który chcesz wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="95157-202">Double-click the file share you wish to view.</span></span>

5.  <span data-ttu-id="95157-203">W okienku głównym zostanie wyświetlona zawartość udziału plików.</span><span class="sxs-lookup"><span data-stu-id="95157-203">The main pane will display the file share's contents.</span></span>

    ![Zawartość udziału](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="95157-205">W okienku głównym zostanie wyświetlona zawartość udziału plików.</span><span class="sxs-lookup"><span data-stu-id="95157-205">The main pane will display the file share's contents.</span></span>

7.  <span data-ttu-id="95157-206">Wykonaj następujące kroki w zależności od zadania, które chcesz wykonać:</span><span class="sxs-lookup"><span data-stu-id="95157-206">Follow these steps depending on the task you wish to perform:</span></span>

    - <span data-ttu-id="95157-207">**Przekazywanie plików do udziału plików**</span><span class="sxs-lookup"><span data-stu-id="95157-207">**Upload files to a file share**</span></span>

        <span data-ttu-id="95157-208">a.</span><span class="sxs-lookup"><span data-stu-id="95157-208">a.</span></span>  <span data-ttu-id="95157-209">Na pasku narzędzi okienka głównego wybierz pozycję **Przekaż**, a następnie z menu rozwijanego wybierz pozycję **Przekaż pliki**.</span><span class="sxs-lookup"><span data-stu-id="95157-209">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![Przekazywanie plików](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="95157-211">b.</span><span class="sxs-lookup"><span data-stu-id="95157-211">b.</span></span> <span data-ttu-id="95157-212">W oknie dialogowym **Przekazywanie plików** wybierz przycisk wielokropka (**...**) po prawej stronie pola tekstowego **Pliki**, aby wybrać pliki do przekazania.</span><span class="sxs-lookup"><span data-stu-id="95157-212">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![Dodawanie plików](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="95157-214">c.</span><span class="sxs-lookup"><span data-stu-id="95157-214">c.</span></span> <span data-ttu-id="95157-215">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="95157-215">Select **Upload**.</span></span>

    - <span data-ttu-id="95157-216">**Przekazywanie folderu do udziału plików**</span><span class="sxs-lookup"><span data-stu-id="95157-216">**Upload a folder to a file share**</span></span>
        
        <span data-ttu-id="95157-217">a.</span><span class="sxs-lookup"><span data-stu-id="95157-217">a.</span></span> <span data-ttu-id="95157-218">Na pasku narzędzi okienka głównego wybierz pozycję **Przekaż**, a następnie z menu rozwijanego wybierz pozycję **Przekaż folder**.</span><span class="sxs-lookup"><span data-stu-id="95157-218">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![Menu Przekaż folder](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="95157-220">b.</span><span class="sxs-lookup"><span data-stu-id="95157-220">b.</span></span> <span data-ttu-id="95157-221">W oknie dialogowym **Przekazywanie folderu** wybierz przycisk wielokropka (**...**) po prawej stronie pola tekstowego **Folder**, aby wybrać folder, którego zawartość chcesz przekazać.</span><span class="sxs-lookup"><span data-stu-id="95157-221">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        <span data-ttu-id="95157-222">c.</span><span class="sxs-lookup"><span data-stu-id="95157-222">c.</span></span> <span data-ttu-id="95157-223">Opcjonalnie określ folder docelowy, do którego zawartość wybranego folderu zostanie przekazana.</span><span class="sxs-lookup"><span data-stu-id="95157-223">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="95157-224">Jeśli folder docelowy nie istnieje, zostanie on utworzony.</span><span class="sxs-lookup"><span data-stu-id="95157-224">If the target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="95157-225">d.</span><span class="sxs-lookup"><span data-stu-id="95157-225">d.</span></span> <span data-ttu-id="95157-226">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="95157-226">Select **Upload**.</span></span>

    - <span data-ttu-id="95157-227">**Pobieranie pliku na komputer lokalny**</span><span class="sxs-lookup"><span data-stu-id="95157-227">**Download a file to your local computer**</span></span>
        
        <span data-ttu-id="95157-228">a.</span><span class="sxs-lookup"><span data-stu-id="95157-228">a.</span></span> <span data-ttu-id="95157-229">Wybierz plik, który chcesz pobrać.</span><span class="sxs-lookup"><span data-stu-id="95157-229">Select the file you wish to download.</span></span>
        
        <span data-ttu-id="95157-230">b.</span><span class="sxs-lookup"><span data-stu-id="95157-230">b.</span></span> <span data-ttu-id="95157-231">Na pasku narzędzi okienka głównego wybierz pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="95157-231">On the main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="95157-232">c.</span><span class="sxs-lookup"><span data-stu-id="95157-232">c.</span></span> <span data-ttu-id="95157-233">W oknie dialogowym **Określanie lokalizacji, w której zapisać pobrany plik** określ lokalizację, w której ma zostać zapisany pobrany plik, oraz nazwę tego pliku.</span><span class="sxs-lookup"><span data-stu-id="95157-233">In the **Specify where to save the downloaded file** dialog, specify the location where you want the file downloaded, and the name you wish to give it.</span></span>

        <span data-ttu-id="95157-234">d.</span><span class="sxs-lookup"><span data-stu-id="95157-234">d.</span></span> <span data-ttu-id="95157-235">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="95157-235">Select **Save**.</span></span>

    - <span data-ttu-id="95157-236">**Otwieranie pliku na komputerze lokalnym**</span><span class="sxs-lookup"><span data-stu-id="95157-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="95157-237">a.</span><span class="sxs-lookup"><span data-stu-id="95157-237">a.</span></span>  <span data-ttu-id="95157-238">Wybierz plik, który chcesz otworzyć.</span><span class="sxs-lookup"><span data-stu-id="95157-238">Select the file you wish to open.</span></span>
        
        <span data-ttu-id="95157-239">b.</span><span class="sxs-lookup"><span data-stu-id="95157-239">b.</span></span>  <span data-ttu-id="95157-240">Na pasku narzędzi okienka głównego wybierz pozycję **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="95157-240">On the main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="95157-241">c.</span><span class="sxs-lookup"><span data-stu-id="95157-241">c.</span></span>  <span data-ttu-id="95157-242">Plik zostanie pobrany i otwarty przy użyciu aplikacji skojarzonej z typem pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="95157-242">The file will be downloaded and opened using the application associated with the file's underlying file type.</span></span>

    - <span data-ttu-id="95157-243">**Kopiowanie pliku do Schowka**</span><span class="sxs-lookup"><span data-stu-id="95157-243">**Copy a file to the clipboard**</span></span>

        <span data-ttu-id="95157-244">a.</span><span class="sxs-lookup"><span data-stu-id="95157-244">a.</span></span> <span data-ttu-id="95157-245">Wybierz plik, który chcesz skopiować.</span><span class="sxs-lookup"><span data-stu-id="95157-245">Select the file you wish to copy.</span></span>

        <span data-ttu-id="95157-246">b.</span><span class="sxs-lookup"><span data-stu-id="95157-246">b.</span></span> <span data-ttu-id="95157-247">Na pasku narzędzi okienka głównego wybierz pozycję **Kopiuj**.</span><span class="sxs-lookup"><span data-stu-id="95157-247">On the main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="95157-248">c.</span><span class="sxs-lookup"><span data-stu-id="95157-248">c.</span></span> <span data-ttu-id="95157-249">W lewym okienku przejdź do innego udziału plików i kliknij go dwukrotnie, aby wyświetlić go w okienku głównym.</span><span class="sxs-lookup"><span data-stu-id="95157-249">In the left pane, navigate to another file share, and double-click it to view it in the main pane.</span></span>

        <span data-ttu-id="95157-250">d.</span><span class="sxs-lookup"><span data-stu-id="95157-250">d.</span></span> <span data-ttu-id="95157-251">Na pasku narzędzi okienka głównego wybierz pozycję **Wklej**, aby utworzyć kopię pliku.</span><span class="sxs-lookup"><span data-stu-id="95157-251">On the main pane's toolbar, select **Paste** to create a copy of the file.</span></span>

    - <span data-ttu-id="95157-252">**Usuwanie pliku**</span><span class="sxs-lookup"><span data-stu-id="95157-252">**Delete a file**</span></span>

        <span data-ttu-id="95157-253">a.</span><span class="sxs-lookup"><span data-stu-id="95157-253">a.</span></span> <span data-ttu-id="95157-254">Wybierz plik, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="95157-254">Select the file you wish to delete.</span></span>

        <span data-ttu-id="95157-255">b.</span><span class="sxs-lookup"><span data-stu-id="95157-255">b.</span></span> <span data-ttu-id="95157-256">Na pasku narzędzi okienka głównego wybierz pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="95157-256">On the main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="95157-257">c.</span><span class="sxs-lookup"><span data-stu-id="95157-257">c.</span></span> <span data-ttu-id="95157-258">Wybierz pozycję **Tak** w oknie dialogowym potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="95157-258">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95157-259">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95157-259">Next steps</span></span>

- <span data-ttu-id="95157-260">Zobacz [najnowsze informacje o wersji i filmy wideo dotyczące programu Storage Explorer (wersja zapoznawcza)](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="95157-260">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="95157-261">Dowiedz się, jak [tworzyć aplikacje przy użyciu obiektów Blob, tabel, kolejek i plików platformy Azure](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="95157-261">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
