---
title: "wprowadzenie do usługi Azure Data Lake Store aaaUse tooget programu PowerShell | Dokumentacja firmy Microsoft"
description: "Użyj programu Azure PowerShell toocreate konto usługi Data Lake Store i wykonywać podstawowe operacje"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="a582d-103">Rozpoczynanie pracy z usługą Azure Data Lake Store przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a582d-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a582d-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a582d-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="a582d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a582d-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="a582d-106">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="a582d-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="a582d-107">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="a582d-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="a582d-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="a582d-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="a582d-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a582d-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="a582d-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="a582d-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="a582d-111">Python</span><span class="sxs-lookup"><span data-stu-id="a582d-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="a582d-112">Dowiedz się, jak toouse toocreate programu Azure PowerShell usługi Azure Data Lake przechowywać konto i wykonywać podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych, usuwanie konta itp. Aby uzyskać więcej informacji o usłudze Data Lake Store, zobacz [Omówienie usługi Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a582d-112">Learn how toouse Azure PowerShell toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a582d-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a582d-113">Prerequisites</span></span>
<span data-ttu-id="a582d-114">Przed rozpoczęciem tego samouczka wymagane są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="a582d-114">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="a582d-115">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="a582d-115">**An Azure subscription**.</span></span> <span data-ttu-id="a582d-116">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a582d-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a582d-117">**Program Azure PowerShell 1.0 lub nowszy**.</span><span class="sxs-lookup"><span data-stu-id="a582d-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="a582d-118">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a582d-118">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="a582d-119">Authentication</span><span class="sxs-lookup"><span data-stu-id="a582d-119">Authentication</span></span>
<span data-ttu-id="a582d-120">W tym artykule używa prostsze uwierzytelniania z Data Lake Store, na którym są tooenter zostanie wyświetlony monit o poświadczenia konta Azure.</span><span class="sxs-lookup"><span data-stu-id="a582d-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="a582d-121">następnie podlega Hello dostępu poziomu tooData Lake Store konta i system plików poziom dostępu hello hello zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a582d-121">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="a582d-122">Istnieją inne podejścia jako dobrze tooauthenticate z usługi Data Lake Store, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="a582d-122">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="a582d-123">Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniania użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [do usługi uwierzytelniania](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a582d-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="a582d-124">Tworzenie konta usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a582d-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="a582d-125">Na pulpicie otwórz nowe okno programu Windows PowerShell, wprowadź powitania po toolog fragment w tooyour konto platformy Azure, ustawione hello subskrypcję i zarejestruj dostawcę usługi Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="a582d-125">From your desktop, open a new Windows PowerShell window, and enter hello following snippet toolog in tooyour Azure account, set hello subscription, and register hello Data Lake Store provider.</span></span> <span data-ttu-id="a582d-126">Gdy zostanie wyświetlony monit o toolog, upewnij się, że logujesz się jako jeden hello/właścicieli subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="a582d-126">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="a582d-127">Konto usługi Azure Data Lake Store jest skojarzone z grupą zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a582d-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="a582d-128">Rozpocznij od utworzenia grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a582d-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="a582d-129">![Tworzenie grupy zasobów platformy Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Tworzenie grupy zasobów platformy Azure")</span><span class="sxs-lookup"><span data-stu-id="a582d-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="a582d-130">Utwórz konto usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a582d-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="a582d-131">Nazwa Hello musi zawierać tylko małe litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="a582d-131">hello name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="a582d-132">![Tworzenie konta usługi Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Tworzenie konta usługi Azure Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="a582d-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="a582d-133">Sprawdź, czy hello konto zostało utworzone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a582d-133">Verify that hello account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="a582d-134">Witaj output powinna to być **True**.</span><span class="sxs-lookup"><span data-stu-id="a582d-134">hello output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="a582d-135">Tworzenie struktur katalogów w usłudze Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a582d-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="a582d-136">Można tworzyć katalogi w obszarze toomanage konta użytkownika usługi Azure Data Lake Store i przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="a582d-136">You can create directories under your Azure Data Lake Store account toomanage and store data.</span></span>

1. <span data-ttu-id="a582d-137">Określ katalog główny.</span><span class="sxs-lookup"><span data-stu-id="a582d-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="a582d-138">Utwórz nowy katalog o nazwie **mynewdirectory** w katalogu głównym określonej hello.</span><span class="sxs-lookup"><span data-stu-id="a582d-138">Create a new directory called **mynewdirectory** under hello specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="a582d-139">Sprawdź, czy ten hello nowy katalog został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a582d-139">Verify that hello new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="a582d-140">Go powinny być widoczne dane wyjściowe podobne hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a582d-140">It should show an output like hello following:</span></span>

    <span data-ttu-id="a582d-141">![Weryfikowanie katalogu](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Weryfikowanie katalogu")</span><span class="sxs-lookup"><span data-stu-id="a582d-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-tooyour-azure-data-lake-store"></a><span data-ttu-id="a582d-142">Przekazywanie danych tooyour Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a582d-142">Upload data tooyour Azure Data Lake Store</span></span>
<span data-ttu-id="a582d-143">Możesz przekazać sklepu Lake tooData danych bezpośrednio na powitania tooa lub na poziomie katalogu utworzonego w ramach konta hello.</span><span class="sxs-lookup"><span data-stu-id="a582d-143">You can upload your data tooData Lake Store directly at hello root level or tooa directory that you created within hello account.</span></span> <span data-ttu-id="a582d-144">Witaj poniższe fragmenty kodu przedstawiają sposób tooupload niektóre przykładowe dane toohello katalogu (**mynewdirectory**) utworzonego w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="a582d-144">hello snippets below demonstrate how tooupload some sample data toohello directory (**mynewdirectory**) you created in hello previous section.</span></span>

<span data-ttu-id="a582d-145">Jeśli szukasz niektórych tooupload dane przykładowe, możesz pobrać hello **Ambulance Data** folderu z hello [repozytorium Git programu Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="a582d-145">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="a582d-146">Pobierz plik hello i zapisz go w katalogu lokalnym na komputerze, na przykład C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="a582d-146">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="a582d-147">Zmienianie nazwy, pobieranie i usuwanie danych z usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a582d-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="a582d-148">toorename pliku hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a582d-148">toorename a file, use hello following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="a582d-149">toodownload pliku hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a582d-149">toodownload a file, use hello following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="a582d-150">toodelete pliku hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a582d-150">toodelete a file, use hello following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="a582d-151">Po wyświetleniu monitu wprowadź **Y** toodelete hello elementu.</span><span class="sxs-lookup"><span data-stu-id="a582d-151">When prompted, enter **Y** toodelete hello item.</span></span> <span data-ttu-id="a582d-152">Jeśli masz więcej niż jeden plik toodelete, musisz podać wszystkie ścieżki hello rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="a582d-152">If you have more than one file toodelete, you can provide all hello paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="a582d-153">Usuwanie konta usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a582d-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="a582d-154">Użyj następującego polecenia toodelete hello Twoje konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a582d-154">Use hello following command toodelete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="a582d-155">Po wyświetleniu monitu wprowadź **Y** toodelete hello konta.</span><span class="sxs-lookup"><span data-stu-id="a582d-155">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="a582d-156">Wskazówki dotyczące wydajności podczas korzystania z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a582d-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="a582d-157">Poniżej przedstawiono hello najważniejszych ustawień, które mogą być tooget Zaczekaj hello najlepszą wydajność podczas korzystania z usługi Data Lake Store toowork środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a582d-157">Below are hello most important settings that can be tuned tooget hello best performance while using PowerShell toowork with Data Lake Store:</span></span>

| <span data-ttu-id="a582d-158">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a582d-158">Property</span></span>            | <span data-ttu-id="a582d-159">Domyślne</span><span class="sxs-lookup"><span data-stu-id="a582d-159">Default</span></span> | <span data-ttu-id="a582d-160">Opis</span><span class="sxs-lookup"><span data-stu-id="a582d-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="a582d-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="a582d-161">PerFileThreadCount</span></span>  | <span data-ttu-id="a582d-162">10</span><span class="sxs-lookup"><span data-stu-id="a582d-162">10</span></span>      | <span data-ttu-id="a582d-163">Ten parametr umożliwia toochoose hello liczbę równoległych wątków przekazanie lub pobranie każdego pliku.</span><span class="sxs-lookup"><span data-stu-id="a582d-163">This parameter enables you toochoose hello number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="a582d-164">Liczba ta reprezentuje hello max wątków, które mogą być przydzielone dla każdego pliku, ale może zostać mniej wątków w zależności od danego scenariusza (np. podczas przekazywania pliku o rozmiarze 1 KB, otrzymasz jeden wątek, nawet jeśli poprosić o 20 wątków).</span><span class="sxs-lookup"><span data-stu-id="a582d-164">This number represents hello max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="a582d-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="a582d-165">ConcurrentFileCount</span></span> | <span data-ttu-id="a582d-166">10</span><span class="sxs-lookup"><span data-stu-id="a582d-166">10</span></span>      | <span data-ttu-id="a582d-167">Ten parametr jest przeznaczony konkretnie na potrzeby przekazywania lub pobierania folderów.</span><span class="sxs-lookup"><span data-stu-id="a582d-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="a582d-168">Ten parametr określa liczbę hello równoczesnych plików, które można przekazać lub pobrać.</span><span class="sxs-lookup"><span data-stu-id="a582d-168">This parameter determines hello number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="a582d-169">Liczba ta reprezentuje hello maksymalną liczbę równoczesnych plików, które można przekazać lub pobrana w tym samym czasie, ale może zostać mniej współbieżności, w zależności od danego scenariusza (np. można przekazać dwóch plików, otrzymasz dwa przekazywania plików jednoczesnych, nawet wtedy, gdy na żądanie użytkownika 15).</span><span class="sxs-lookup"><span data-stu-id="a582d-169">This number represents hello maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="a582d-170">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="a582d-170">**Example**</span></span>

<span data-ttu-id="a582d-171">To polecenie pobiera pliki z dysku lokalnego użytkownika toohello Azure Data Lake Store za pomocą 20 wątków na plik i 100 równoczesnych pliki.</span><span class="sxs-lookup"><span data-stu-id="a582d-171">This command downloads files from Azure Data Lake Store toohello user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a><span data-ttu-id="a582d-172">Jak ustalić hello tooset wartości dla parametrów?</span><span class="sxs-lookup"><span data-stu-id="a582d-172">How do I determine hello value tooset for these parameters?</span></span>

<span data-ttu-id="a582d-173">Oto kilka użytecznych wskazówek.</span><span class="sxs-lookup"><span data-stu-id="a582d-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="a582d-174">**Krok 1: Określanie liczby całkowitej wątku hello** — należy zacząć od obliczania hello wątku łączna liczba toouse.</span><span class="sxs-lookup"><span data-stu-id="a582d-174">**Step 1: Determine hello total thread count** - You should start by calculating hello total thread count toouse.</span></span> <span data-ttu-id="a582d-175">Zasadniczo powinno się używać 6 wątków na każdy rdzeń fizyczny.</span><span class="sxs-lookup"><span data-stu-id="a582d-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="a582d-176">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="a582d-176">**Example**</span></span>

    <span data-ttu-id="a582d-177">Przy założeniu, że używasz hello PowerShell poleceń z D14 maszyny Wirtualnej, która ma 16 rdzeni</span><span class="sxs-lookup"><span data-stu-id="a582d-177">Assuming you are running hello PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="a582d-178">**Krok 2: Oblicz PerFileThreadCount** -możemy obliczyć naszych PerFileThreadCount na podstawie rozmiaru hello hello plików.</span><span class="sxs-lookup"><span data-stu-id="a582d-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on hello size of hello files.</span></span> <span data-ttu-id="a582d-179">Pliki mniejsze niż 2,5 GB jest toochange nie konieczności tego parametru, ponieważ domyślny hello 10 jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="a582d-179">For files smaller than 2.5GB, there is no need toochange this parameter because hello default of 10 is sufficient.</span></span> <span data-ttu-id="a582d-180">W przypadku plików większych niż 2,5 GB należy użyć 10 wątków jako podstawa hello hello pierwszy 2,5 GB i Dodaj 1 wątków dla każdego dodatkowego zwiększenia 256 MB rozmiaru pliku.</span><span class="sxs-lookup"><span data-stu-id="a582d-180">For files larger than 2.5GB, you should use 10 threads as hello base for hello first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="a582d-181">Podczas kopiowania folderu zawierającego pliki o szerokim zakresie rozmiarów warto podzielić je na grupy złożone z plików o podobnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="a582d-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="a582d-182">Różne rozmiary plików mogą spowodować utratę optymalnej wydajności.</span><span class="sxs-lookup"><span data-stu-id="a582d-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="a582d-183">Jeśli nie jest możliwe toogroup podobne rozmiary plików, należy ustawić PerFileThreadCount oparte na powitania największy rozmiar pliku.</span><span class="sxs-lookup"><span data-stu-id="a582d-183">If that's not possible toogroup similar file sizes, you should set PerFileThreadCount based on hello largest file size.</span></span>

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="a582d-184">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="a582d-184">**Example**</span></span>

    <span data-ttu-id="a582d-185">Zakładając, że masz 100 plików od too10GB 1 GB, używamy hello 10 GB, jak hello największy rozmiar dla równanie, które będzie odczytywać podobnie następującej hello pliku.</span><span class="sxs-lookup"><span data-stu-id="a582d-185">Assuming you have 100 files ranging from 1GB too10GB, we use hello 10GB as hello largest file size for equation, which would read like hello following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="a582d-186">**Krok 3: Oblicz ConcurrentFilecount** — liczba całkowita liczba wątków hello użycia i PerFileThreadCount toocalculate ConcurrentFileCount oparte na powitania po równości.</span><span class="sxs-lookup"><span data-stu-id="a582d-186">**Step 3: Calculate ConcurrentFilecount** - Use hello total thread count and PerFileThreadCount toocalculate ConcurrentFileCount based on hello following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="a582d-187">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="a582d-187">**Example**</span></span>

    <span data-ttu-id="a582d-188">Na podstawie wartości przykład hello, który był używany firma Microsoft</span><span class="sxs-lookup"><span data-stu-id="a582d-188">Based on hello example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="a582d-189">Tak **ConcurrentFileCount** jest **2.4**, które firma Microsoft może zaokrąglania zbyt**2**.</span><span class="sxs-lookup"><span data-stu-id="a582d-189">So, **ConcurrentFileCount** is **2.4**, which we can round off too**2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="a582d-190">Dalsze dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="a582d-190">Further tuning</span></span>

<span data-ttu-id="a582d-191">Mogą być wymagane dodatkowe dostrajania, ponieważ istnieje szereg toowork rozmiary plików z.</span><span class="sxs-lookup"><span data-stu-id="a582d-191">You might require further tuning because there is a range of file sizes toowork with.</span></span> <span data-ttu-id="a582d-192">Witaj powyżej obliczania sprawdza się, gdy wszystkie lub większość plików hello są większe i bliżej toohello zakresu 10GB.</span><span class="sxs-lookup"><span data-stu-id="a582d-192">hello above calculation works well if all or most of hello files are larger and closer toohello 10GB range.</span></span> <span data-ttu-id="a582d-193">Jeśli natomiast istnieje wiele różnych rozmiarów plików, z czego wiele plików jest mniejszych, można zmniejszyć wartość parametru PerFileThreadCount.</span><span class="sxs-lookup"><span data-stu-id="a582d-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="a582d-194">Dzięki zmniejszeniu hello PerFileThreadCount, firma Microsoft może zwiększyć ConcurrentFileCount.</span><span class="sxs-lookup"><span data-stu-id="a582d-194">By reducing hello PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="a582d-195">Tak Jeśli przyjęto założenie, że większość naszego plików są mniejsze hello 5GB zakresu, możemy ponownie wykonaj naszych obliczenia:</span><span class="sxs-lookup"><span data-stu-id="a582d-195">So, if we assume that most of our files are smaller in hello 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="a582d-196">Tak **ConcurrentFileCount** będzie teraz 96/20, czyli 4.8 zaokrąglana zbyt**4**.</span><span class="sxs-lookup"><span data-stu-id="a582d-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off too**4**.</span></span>

<span data-ttu-id="a582d-197">Można kontynuować tootune te ustawienia, zmieniając hello **PerFileThreadCount** górę i w dół w zależności od hello dystrybucji Twojej rozmiary plików.</span><span class="sxs-lookup"><span data-stu-id="a582d-197">You can continue tootune these settings by changing hello **PerFileThreadCount** up and down depending on hello distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="a582d-198">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="a582d-198">Limitation</span></span>

* <span data-ttu-id="a582d-199">**Liczba plików jest mniejsza niż ConcurrentFileCount**: Jeśli hello liczby plików podczas przekazywania jest mniejszy niż hello **ConcurrentFileCount** obliczane, a następnie należy zmniejszyć  **ConcurrentFileCount** toobe toohello równy liczby plików.</span><span class="sxs-lookup"><span data-stu-id="a582d-199">**Number of files is less than ConcurrentFileCount**: If hello number of files you are uploading is smaller than hello **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** toobe equal toohello number of files.</span></span> <span data-ttu-id="a582d-200">Można użyć dowolnego pozostałych tooincrease wątków **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="a582d-200">You can use any remaining threads tooincrease **PerFileThreadCount**.</span></span>

* <span data-ttu-id="a582d-201">**Zbyt wiele wątków**: Jeśli zwiększysz wątku liczba zbyt dużo bez zwiększania rozmiar klastra, należy uruchomić hello ryzyko pogorszenie wydajności.</span><span class="sxs-lookup"><span data-stu-id="a582d-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run hello risk of degraded performance.</span></span> <span data-ttu-id="a582d-202">Może być rywalizacji problemy podczas przełączania kontekstu na powitania procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="a582d-202">There can be contention issues when context-switching on hello CPU.</span></span>

* <span data-ttu-id="a582d-203">**Za mało współbieżności**: Jeśli nie wystarcza hello współbieżności, a następnie klastra jest za mały.</span><span class="sxs-lookup"><span data-stu-id="a582d-203">**Insufficient concurrency**: If hello concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="a582d-204">Można zwiększyć hello liczby węzłów w klastrze, który będzie zawierać więcej współbieżności.</span><span class="sxs-lookup"><span data-stu-id="a582d-204">You can increase hello number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="a582d-205">**Błędy ograniczania przepływności**: błędy ograniczania przepływności mogą wystąpić wówczas, gdy współbieżność jest zbyt wysoka.</span><span class="sxs-lookup"><span data-stu-id="a582d-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="a582d-206">Jeśli widzisz ograniczania błędy, możesz zmniejszają hello lub skontaktuj się z nami.</span><span class="sxs-lookup"><span data-stu-id="a582d-206">If you are seeing throttling errors, you should either reduce hello concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a582d-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a582d-207">Next steps</span></span>
* [<span data-ttu-id="a582d-208">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a582d-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="a582d-209">Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a582d-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="a582d-210">Korzystanie z usługi Azure HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a582d-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

