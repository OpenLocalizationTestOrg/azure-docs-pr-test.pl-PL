---
title: "aaaManage zasobów magazynu obiektów Blob Azure przy użyciu Eksploratora usługi Storage (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Zarządzanie kontenerów obiektów Blob platformy Azure i obiektów blob z Eksploratora usługi Storage (wersja zapoznawcza)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="7c6ab-103">Zarządzanie zasobami magazynu obiektów Blob Azure za pomocą Eksploratora usługi Storage (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="7c6ab-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="7c6ab-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7c6ab-104">Overview</span></span>
<span data-ttu-id="7c6ab-105">[Magazyn obiektów Blob Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) to usługa do przechowywania dużych ilości danych bez struktury, takich jak dane tekstowe lub binarne, który można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span>
<span data-ttu-id="7c6ab-106">Możesz użyć danych tooexpose magazynu obiektów Blob publicznie toohello world lub toostore danych aplikacji prywatnie.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-106">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="7c6ab-107">W tym artykule dowiesz się, jak toouse toowork Eksploratora usługi Storage (wersja zapoznawcza) z obiektu blob kontenerów i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-107">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c6ab-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7c6ab-108">Prerequisites</span></span>
<span data-ttu-id="7c6ab-109">toocomplete hello kroki opisane w tym artykule, będą potrzebne następujące hello:</span><span class="sxs-lookup"><span data-stu-id="7c6ab-109">toocomplete hello steps in this article, you'll need hello following:</span></span>

* [<span data-ttu-id="7c6ab-110">Pobieranie i instalowanie Eksploratora usługi Storage (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="7c6ab-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="7c6ab-111">Połącz tooa kontem magazynu platformy Azure lub usługi</span><span class="sxs-lookup"><span data-stu-id="7c6ab-111">Connect tooa Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="7c6ab-112">Tworzenie kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="7c6ab-112">Create a blob container</span></span>
<span data-ttu-id="7c6ab-113">Wszystkie obiekty BLOB muszą znajdować się w kontenerze obiektów blob to po prostu logiczne grupowanie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="7c6ab-114">Konto może zawierać nieograniczoną liczbę kontenerów, a każdy kontener może przechowywać nieograniczoną liczbę obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="7c6ab-115">Witaj poniższe kroki przedstawiają sposób toocreate kontener obiektów blob w ramach Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-115">hello following steps illustrate how toocreate a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="7c6ab-116">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="7c6ab-117">W okienku po lewej stronie powitania rozwiń hello konta magazynu w ramach którego ma zostać kontenera obiektów blob hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-117">In hello left pane, expand hello storage account within which you wish toocreate hello blob container.</span></span>
3. <span data-ttu-id="7c6ab-118">Kliknij prawym przyciskiem myszy **kontenerów obiektów Blob**i z menu kontekstowego hello — wybierz pozycję **Tworzenie kontenera obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-118">Right-click **Blob Containers**, and - from hello context menu - select **Create Blob Container**.</span></span>

   ![Tworzenie menu kontekstowe kontenerów obiektów blob][0]
4. <span data-ttu-id="7c6ab-120">Pole tekstowe pojawi się poniżej hello **kontenerów obiektów Blob** folderu.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-120">A text box will appear below hello **Blob Containers** folder.</span></span> <span data-ttu-id="7c6ab-121">Wprowadź nazwę hello kontenerze obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-121">Enter hello name for your blob container.</span></span> <span data-ttu-id="7c6ab-122">Zobacz hello [reguły nazewnictwa kontenera](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) sekcja zawiera listę reguł i ograniczenia dotyczące nazewnictwa kontenerów obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-122">See hello [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Tworzenie pola tekstowego kontenerów obiektów Blob][1]
5. <span data-ttu-id="7c6ab-124">Naciśnij klawisz **Enter** po zakończeniu toocreate kontenera obiektów blob hello, lub **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-124">Press **Enter** when done toocreate hello blob container, or **Esc** toocancel.</span></span> <span data-ttu-id="7c6ab-125">Po pomyślnym utworzeniu kontenera obiektów blob hello będzie wyświetlana w obszarze hello **kontenerów obiektów Blob** folder hello wybranego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-125">Once hello blob container has been successfully created, it will be displayed under hello **Blob Containers** folder for hello selected storage account.</span></span>

   ![Utworzyć kontener obiektów blob][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="7c6ab-127">Wyświetlanie zawartości kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="7c6ab-127">View a blob container's contents</span></span>
<span data-ttu-id="7c6ab-128">Kontenerów obiektów blob zawiera obiekty BLOB i folderów (które może również zawierać obiektów blob).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="7c6ab-129">Witaj poniższe kroki przedstawiają sposób zawartość hello tooview kontenera obiektów blob w ramach Eksploratora usługi Storage (wersja zapoznawcza):</span><span class="sxs-lookup"><span data-stu-id="7c6ab-129">hello following steps illustrate how tooview hello contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="7c6ab-130">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="7c6ab-131">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello kontenera obiektów blob mają tooview.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-131">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="7c6ab-132">Rozwiń konto magazynu hello **kontenerów obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-132">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="7c6ab-133">Kontener obiektów blob powitania kliknij prawym przyciskiem myszy konieczność tooview i — wybierz z menu kontekstowego hello - **Otwórz Edytor kontenera obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-133">Right-click hello blob container you wish tooview, and - from hello context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="7c6ab-134">Możesz również kliknąć dwukrotnie hello kontenera obiektów blob mają tooview.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-134">You can also double-click hello blob container you wish tooview.</span></span>

   ![Menu kontekstowe edytora kontenera obiektów blob Otwórz][19]
5. <span data-ttu-id="7c6ab-136">Witaj głównego okienku zostaną wyświetlone kontenera obiektów blob hello zawartość.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-136">hello main pane will display hello blob container's contents.</span></span>

   ![Edytor kontenera obiektów blob][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="7c6ab-138">Usunięcie kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="7c6ab-138">Delete a blob container</span></span>
<span data-ttu-id="7c6ab-139">Kontenerów obiektów blob można łatwo tworzyć i usunięte zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="7c6ab-140">(toosee jak toodelete poszczególne obiekty BLOB, można znaleźć w sekcji toohello [Zarządzanie obiekty BLOB w kontenerze obiektów blob](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="7c6ab-140">(toosee how toodelete individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="7c6ab-141">Witaj poniższe kroki przedstawiają sposób toodelete kontener obiektów blob w ramach Eksploratora usługi Storage (wersja zapoznawcza):</span><span class="sxs-lookup"><span data-stu-id="7c6ab-141">hello following steps illustrate how toodelete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="7c6ab-142">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="7c6ab-143">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello kontenera obiektów blob mają tooview.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-143">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="7c6ab-144">Rozwiń konto magazynu hello **kontenerów obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-144">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="7c6ab-145">Kontener obiektów blob powitania kliknij prawym przyciskiem myszy konieczność toodelete i — wybierz z menu kontekstowego hello - **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-145">Right-click hello blob container you wish toodelete, and - from hello context menu - select **Delete**.</span></span>
   <span data-ttu-id="7c6ab-146">Można również nacisnąć **usunąć** toodelete hello aktualnie zaznaczonego obiektu blob kontenera.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-146">You can also press **Delete** toodelete hello currently selected blob container.</span></span>

   ![Usuwanie menu kontekstowe kontenera obiektów blob][4]
5. <span data-ttu-id="7c6ab-148">Wybierz **tak** toohello okno dialogowe potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-148">Select **Yes** toohello confirmation dialog.</span></span>

   ![Usuwanie obiektów blob kontenera potwierdzenia][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="7c6ab-150">Skopiuj kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="7c6ab-150">Copy a blob container</span></span>
<span data-ttu-id="7c6ab-151">Eksplorator usługi Storage (wersja zapoznawcza) umożliwia toocopy Schowek toohello kontenera obiektów blob, a następnie wklej, który kontenera obiektów blob na innym koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-151">Storage Explorer (Preview) enables you toocopy a blob container toohello clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="7c6ab-152">(toosee jak toocopy poszczególne obiekty BLOB, można znaleźć w sekcji toohello [Zarządzanie obiekty BLOB w kontenerze obiektów blob](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="7c6ab-152">(toosee how toocopy individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="7c6ab-153">Witaj następujące kroki pokazują, jak toocopy kontenera obiektów blob z jednego magazynu konta tooanother.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-153">hello following steps illustrate how toocopy a blob container from one storage account tooanother.</span></span>

1. <span data-ttu-id="7c6ab-154">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="7c6ab-155">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello kontenera obiektów blob mają toocopy.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-155">In hello left pane, expand hello storage account containing hello blob container you wish toocopy.</span></span>
3. <span data-ttu-id="7c6ab-156">Rozwiń konto magazynu hello **kontenerów obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-156">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="7c6ab-157">Kontener obiektów blob powitania kliknij prawym przyciskiem myszy konieczność toocopy i — wybierz z menu kontekstowego hello - **kontenera obiektów Blob kopii**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-157">Right-click hello blob container you wish toocopy, and - from hello context menu - select **Copy Blob Container**.</span></span>

   ![Kopiowanie menu kontekstowe kontenera obiektów blob][6]
5. <span data-ttu-id="7c6ab-159">Kliknij prawym przyciskiem myszy konto magazynu Witaj "wartość", do którego chcesz kontenera obiektów blob hello toopaste, a - z menu kontekstowego hello — wybierz **kontenera obiektów Blob Wklej**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-159">Right-click hello desired "target" storage account into which you want toopaste hello blob container, and - from hello context menu - select **Paste Blob Container**.</span></span>

   ![Menu kontekstowe kontenera obiektów blob wklejania][7]

## <a name="get-hello-sas-for-a-blob-container"></a><span data-ttu-id="7c6ab-161">Pobierz hello SAS dla kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="7c6ab-161">Get hello SAS for a blob container</span></span>
<span data-ttu-id="7c6ab-162">A [sygnatury dostępu współdzielonego (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) zapewnia dostęp delegowany tooresources na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access tooresources in your storage account.</span></span>
<span data-ttu-id="7c6ab-163">Oznacza to, że można udzielać się, że klient ograniczone uprawnienia tooobjects na koncie magazynu w określonym przedziale czasu i z określonym zestawem uprawnień, bez konieczności udostępniania kluczy dostępu konta.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-163">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="7c6ab-164">Witaj poniższe kroki przedstawiają sposób toocreate sygnatury dostępu Współdzielonego dla kontenera obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="7c6ab-164">hello following steps illustrate how toocreate a SAS for a blob container:</span></span>

1. <span data-ttu-id="7c6ab-165">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="7c6ab-166">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello kontenera obiektów blob, dla którego chcesz tooget sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-166">In hello left pane, expand hello storage account containing hello blob container for which you wish tooget a SAS.</span></span>
3. <span data-ttu-id="7c6ab-167">Rozwiń konto magazynu hello **kontenerów obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-167">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="7c6ab-168">Kliknij prawym przyciskiem myszy kontener obiektów blob żądaną hello i — wybierz z menu kontekstowego hello - **Uzyskaj sygnaturę dostępu współdzielonego**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-168">Right-click hello desired blob container, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

   ![Uzyskiwanie sygnatury dostępu Współdzielonego menu kontekstowe][8]
5. <span data-ttu-id="7c6ab-170">W hello **sygnatura dostępu współdzielonego** okna dialogowego, określ hello zasad, daty rozpoczęcia i wygaśnięcia, strefy czasowej, a dla zasobu hello poziomy dostępu.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-170">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

   ![Opcje SAS][9]
6. <span data-ttu-id="7c6ab-172">Po zakończeniu określenie opcji SAS hello wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-172">When you're finished specifying hello SAS options, select **Create**.</span></span>
7. <span data-ttu-id="7c6ab-173">Drugi **sygnatura dostępu współdzielonego** okna dialogowego zostanie następnie wyświetlona, że listy hello kontenera obiektów blob oraz adres URL hello i QueryStrings można użyć tooaccess hello zasobów magazynu.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-173">A second **Shared Access Signature** dialog will then display that lists hello blob container along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span>
   <span data-ttu-id="7c6ab-174">Wybierz **kopiowania** dalej toohello adres URL ma toocopy toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-174">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>

   ![Skopiuj adresy URL SAS][10]
8. <span data-ttu-id="7c6ab-176">Po zakończeniu wybierz pozycję **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="7c6ab-177">Zarządzanie zasadami dostępu do kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="7c6ab-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="7c6ab-178">Witaj poniższe kroki przedstawiają sposób toomanage (Dodaj i Usuń) zasady dla kontenera obiektów blob dostępu:</span><span class="sxs-lookup"><span data-stu-id="7c6ab-178">hello following steps illustrate how toomanage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="7c6ab-179">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="7c6ab-180">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające kontenera obiektów blob hello zasad dostępu, którego chcesz toomanage.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-180">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="7c6ab-181">Rozwiń konto magazynu hello **kontenerów obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-181">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="7c6ab-182">Wybierz kontener obiektów blob żądaną hello i — wybierz z menu kontekstowego hello - **Zarządzanie zasadami dostępu**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-182">Select hello desired blob container, and - from hello context menu - select **Manage Access Policies**.</span></span>

   ![Menu kontekstowe Zarządzanie zasadami dostępu][11]
5. <span data-ttu-id="7c6ab-184">Witaj **zasady dostępu** okno dialogowe wyświetla wszystkie zasady dostępu dla kontenera obiektów blob wybranego hello już utworzone.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-184">hello **Access Policies** dialog will list any access policies already created for hello selected blob container.</span></span>

   ![Opcje zasad dostępu][12]        
6. <span data-ttu-id="7c6ab-186">Wykonaj następujące kroki w zależności od zadania zarządzania zasadami dostępu hello:</span><span class="sxs-lookup"><span data-stu-id="7c6ab-186">Follow these steps depending on hello access policy management task:</span></span>

   * <span data-ttu-id="7c6ab-187">**Dodawanie nowych zasad dostępu** — wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="7c6ab-188">Wygenerowany hello **zasady dostępu** hello nowo dodanych do wyświetlenia okna dialogowego dostęp zasad (przy użyciu ustawień domyślnych).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-188">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="7c6ab-189">**Edytowanie zasad dostępu** — wprowadź żądane zmiany i wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="7c6ab-190">**Usuń zasady dostępu** — wybierz tę opcję **Usuń** dalej toohello zasady dostępu mają tooremove.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-190">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

## <a name="set-hello-public-access-level-for-a-blob-container"></a><span data-ttu-id="7c6ab-191">Ustaw hello poziom dostępu publicznego kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="7c6ab-191">Set hello Public Access Level for a blob container</span></span>
<span data-ttu-id="7c6ab-192">Domyślnie każdy kontener obiektów blob jest ustawiona zbyt "Brak dostępu publicznego".</span><span class="sxs-lookup"><span data-stu-id="7c6ab-192">By default, every blob container is set too"No public access".</span></span>

<span data-ttu-id="7c6ab-193">Hello poniższe kroki przedstawiają sposób toospecify publiczny dostęp do poziomu kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-193">hello following steps illustrate how toospecify a public access level for a blob container.</span></span>

1. <span data-ttu-id="7c6ab-194">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="7c6ab-195">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające kontenera obiektów blob hello zasad dostępu, którego chcesz toomanage.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-195">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="7c6ab-196">Rozwiń konto magazynu hello **kontenerów obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-196">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="7c6ab-197">Wybierz kontener obiektów blob żądaną hello i — wybierz z menu kontekstowego hello - **Ustaw poziom dostępu publicznego**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-197">Select hello desired blob container, and - from hello context menu - select **Set Public Access Level**.</span></span>

   ![Menu kontekstowe poziomu dostępu publicznego zestawu][13]
5. <span data-ttu-id="7c6ab-199">W hello **Ustaw poziom dostępu publicznego kontenera** okna dialogowego, określ hello żądany poziom dostępu.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-199">In hello **Set Container Public Access Level** dialog, specify hello desired access level.</span></span>

   ![Ustaw opcje poziomu dostępu publicznego][14]
6. <span data-ttu-id="7c6ab-201">Wybierz przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="7c6ab-202">Zarządzanie obiekty BLOB w kontenerze obiektów blob</span><span class="sxs-lookup"><span data-stu-id="7c6ab-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="7c6ab-203">Po utworzeniu kontenera obiektów blob można przekazać kontenera obiektów blob toothat obiektów blob, Pobierz komputera lokalnego tooyour obiektów blob, otwórz obiektu blob na komputerze lokalnym i wiele innych.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-203">Once you've created a blob container, you can upload a blob toothat blob container, download a blob tooyour local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="7c6ab-204">Witaj następujące kroki pokazują, jak toomanage hello obiektów blob (i foldery) w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-204">hello following steps illustrate how toomanage hello blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="7c6ab-205">Otwórz Eksploratora usługi Storage (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="7c6ab-206">W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello kontenera obiektów blob mają toomanage.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-206">In hello left pane, expand hello storage account containing hello blob container you wish toomanage.</span></span>
3. <span data-ttu-id="7c6ab-207">Rozwiń konto magazynu hello **kontenerów obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-207">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="7c6ab-208">Kliknij dwukrotnie hello kontenera obiektów blob mają tooview.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-208">Double-click hello blob container you wish tooview.</span></span>
5. <span data-ttu-id="7c6ab-209">Witaj głównego okienku zostaną wyświetlone kontenera obiektów blob hello zawartość.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-209">hello main pane will display hello blob container's contents.</span></span>

   ![Widok kontenera obiektów blob][3]
6. <span data-ttu-id="7c6ab-211">Witaj głównego okienku zostaną wyświetlone kontenera obiektów blob hello zawartość.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-211">hello main pane will display hello blob container's contents.</span></span>
7. <span data-ttu-id="7c6ab-212">Wykonaj następujące kroki w zależności od zadania hello mają tooperform:</span><span class="sxs-lookup"><span data-stu-id="7c6ab-212">Follow these steps depending on hello task you wish tooperform:</span></span>

   * <span data-ttu-id="7c6ab-213">**Przekaż kontenera obiektów blob tooa plików**</span><span class="sxs-lookup"><span data-stu-id="7c6ab-213">**Upload files tooa blob container**</span></span>

     1. <span data-ttu-id="7c6ab-214">W okienku głównym hello narzędzi, wybierz **przekazać**, a następnie **Przekaż** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-214">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Przekazywanie plików menu][15]
     2. <span data-ttu-id="7c6ab-216">W hello **przekazać pliki** okno dialogowe, wybierz hello wielokropka (**...** ) przycisku po prawej stronie powitania hello **pliki** tooselect hello pliki mają tooupload polu tekstowym.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-216">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Przekazywanie plików opcje][16]
     3. <span data-ttu-id="7c6ab-218">Określ typ hello **typu obiektu Blob**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-218">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="7c6ab-219">Artykuł Hello [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) wyjaśniono hello różnice między hello różnych typów obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-219">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="7c6ab-220">Opcjonalnie określ folder docelowy, do którego zostanie przekazany hello wybranych plików.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-220">Optionally, specify a target folder into which hello selected file(s) will be uploaded.</span></span> <span data-ttu-id="7c6ab-221">Witaj, folder docelowy nie istnieje, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-221">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="7c6ab-222">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-222">Select **Upload**.</span></span>
   * <span data-ttu-id="7c6ab-223">**Przekaż kontenera obiektów blob tooa folderu**</span><span class="sxs-lookup"><span data-stu-id="7c6ab-223">**Upload a folder tooa blob container**</span></span>

     1. <span data-ttu-id="7c6ab-224">Na pasku narzędzi w okienku głównym hello, wybierz **przekazać**, a następnie **przekazać folderu** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-224">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menu Przekaż folder][17]
     2. <span data-ttu-id="7c6ab-226">W hello **folder przekazywania** okno dialogowe, wybierz hello wielokropka (**...** ) przycisku po prawej stronie powitania hello **folderu** tekst pola tooselect hello folder zawartości, którego chcesz tooupload.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-226">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        ![Przekaż Opcje folderów][18]
     3. <span data-ttu-id="7c6ab-228">Określ typ hello **typu obiektu Blob**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-228">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="7c6ab-229">Artykuł Hello [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) wyjaśniono hello różnice między hello różnych typów obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-229">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="7c6ab-230">Opcjonalnie określ folder docelowy, w których hello zostanie przekazany zawartość wybranego folderu.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-230">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="7c6ab-231">Witaj, folder docelowy nie istnieje, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-231">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="7c6ab-232">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-232">Select **Upload**.</span></span>
   * <span data-ttu-id="7c6ab-233">**Pobieranie obiektu blob tooyour komputera lokalnego**</span><span class="sxs-lookup"><span data-stu-id="7c6ab-233">**Download a blob tooyour local computer**</span></span>

     1. <span data-ttu-id="7c6ab-234">Wybierz hello obiektu blob mają toodownload.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-234">Select hello blob you wish toodownload.</span></span>
     2. <span data-ttu-id="7c6ab-235">W okienku głównym hello narzędzi wybierz **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-235">On hello main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="7c6ab-236">W hello **Określ, którego toosave hello pobrany obiekt blob** okna dialogowego, określ hello lokalizacji obiektu blob hello pobrane i hello nazwę mają toogive go.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-236">In hello **Specify where toosave hello downloaded blob** dialog, specify hello location where you want hello blob downloaded, and hello name you wish toogive it.</span></span>  
     4. <span data-ttu-id="7c6ab-237">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-237">Select **Save**.</span></span>
   * <span data-ttu-id="7c6ab-238">**Otwórz obiektu blob na komputerze lokalnym**</span><span class="sxs-lookup"><span data-stu-id="7c6ab-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="7c6ab-239">Wybierz hello obiektu blob mają tooopen.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-239">Select hello blob you wish tooopen.</span></span>
     2. <span data-ttu-id="7c6ab-240">W okienku głównym hello narzędzi wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-240">On hello main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="7c6ab-241">Obiekt blob Hello zostaną pobrane i otwarty aplikacji hello skojarzone z typem bazowym pliku hello blob.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-241">hello blob will be downloaded and opened using hello application associated with hello blob's underlying file type.</span></span>
   * <span data-ttu-id="7c6ab-242">**Kopiuj do Schowka toohello obiektów blob**</span><span class="sxs-lookup"><span data-stu-id="7c6ab-242">**Copy a blob toohello clipboard**</span></span>

     1. <span data-ttu-id="7c6ab-243">Wybierz hello obiektu blob mają toocopy.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-243">Select hello blob you wish toocopy.</span></span>
     2. <span data-ttu-id="7c6ab-244">W okienku głównym hello narzędzi wybierz **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-244">On hello main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="7c6ab-245">W okienku po lewej stronie powitania, przejdź do kontenera obiektów blob tooanother i kliknij ją dwukrotnie tooview w okienku głównym hello.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-245">In hello left pane, navigate tooanother blob container, and double-click it tooview it in hello main pane.</span></span>
     4. <span data-ttu-id="7c6ab-246">W okienku głównym hello narzędzi wybierz **Wklej** toocreate kopię hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-246">On hello main pane's toolbar, select **Paste** toocreate a copy of hello blob.</span></span>
   * <span data-ttu-id="7c6ab-247">**Usuwanie obiektu blob**</span><span class="sxs-lookup"><span data-stu-id="7c6ab-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="7c6ab-248">Wybierz hello obiektu blob mają toodelete.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-248">Select hello blob you wish toodelete.</span></span>
     2. <span data-ttu-id="7c6ab-249">W okienku głównym hello narzędzi wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-249">On hello main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="7c6ab-250">Wybierz **tak** toohello okno dialogowe potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="7c6ab-250">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c6ab-251">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c6ab-251">Next steps</span></span>
* <span data-ttu-id="7c6ab-252">Widok hello [najnowsze informacje o wersji Eksploratora usługi Storage (wersja zapoznawcza) i filmy wideo](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-252">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="7c6ab-253">Dowiedz się, jak za[tworzenie aplikacji przy użyciu Azure blob, tabel, kolejek i plików](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="7c6ab-253">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
