---
title: "wprowadzenie do usługi Azure Data Lake Store tooget interfejsu aaaUse 2.0 wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj wiersza polecenia platformy Azure i platform 2.0 toocreate konto usługi Data Lake Store i wykonywać podstawowe operacje"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="42ead-103">Rozpoczynanie pracy z usługą Azure Data Lake Store za pomocą interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="42ead-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="42ead-104">Portal</span><span class="sxs-lookup"><span data-stu-id="42ead-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="42ead-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="42ead-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="42ead-106">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="42ead-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="42ead-107">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="42ead-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="42ead-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="42ead-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="42ead-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="42ead-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="42ead-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="42ead-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="42ead-111">Python</span><span class="sxs-lookup"><span data-stu-id="42ead-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="42ead-112">Dowiedz się, jak toocreate toouse Azure CLI 2.0 Azure Data Lake przechowywać konto i wykonywać podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych, usuwanie konta itp. Aby uzyskać więcej informacji o usłudze Data Lake Store, zobacz [Omówienie usługi Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="42ead-112">Learn how toouse Azure CLI 2.0 toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="42ead-113">Hello Azure CLI 2.0 jest nowe środowisko wiersza polecenia platformy Azure do zarządzania zasobami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="42ead-113">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="42ead-114">Można go używać w systemach macOS, Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="42ead-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="42ead-115">Aby uzyskać więcej informacji, zobacz [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview) (Przegląd interfejsu wiersza polecenia platformy Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="42ead-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="42ead-116">Można również sprawdzić hello [odwołanie do usługi Azure Data Lake magazynu interfejsu wiersza polecenia 2.0](https://docs.microsoft.com/cli/azure/dls) pełną listę poleceń i składni.</span><span class="sxs-lookup"><span data-stu-id="42ead-116">You can also look at hello [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="42ead-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="42ead-117">Prerequisites</span></span>
<span data-ttu-id="42ead-118">Przed rozpoczęciem tego artykułu, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="42ead-118">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="42ead-119">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="42ead-119">**An Azure subscription**.</span></span> <span data-ttu-id="42ead-120">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42ead-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="42ead-121">**Interfejs wiersza polecenia platformy Azure 2.0** — instrukcje znajdują się w artykule [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Instalowanie interfejsu wiersza polecenia platformy Azure w wersji 2.0).</span><span class="sxs-lookup"><span data-stu-id="42ead-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="42ead-122">Authentication</span><span class="sxs-lookup"><span data-stu-id="42ead-122">Authentication</span></span>

<span data-ttu-id="42ead-123">W tym artykule użyto prostszej metody uwierzytelniania w usłudze Data Lake Store, w przypadku której logujesz się jako użytkownik końcowy.</span><span class="sxs-lookup"><span data-stu-id="42ead-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="42ead-124">następnie podlega Hello dostępu poziomu tooData Lake Store konta i system plików poziom dostępu hello hello zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="42ead-124">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="42ead-125">Istnieją inne podejścia jako dobrze tooauthenticate z usługi Data Lake Store, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="42ead-125">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="42ead-126">Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniania użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [do usługi uwierzytelniania](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="42ead-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="42ead-127">Zaloguj się za tooyour subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="42ead-127">Log in tooyour Azure subscription</span></span>

1. <span data-ttu-id="42ead-128">Zaloguj się do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="42ead-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="42ead-129">Otrzymasz toouse kodu w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="42ead-129">You get a code toouse in hello next step.</span></span> <span data-ttu-id="42ead-130">Użyj https://aka.ms/devicelogin strony sieci web przeglądarce tooopen hello, a następnie wprowadź hello tooauthenticate kodu.</span><span class="sxs-lookup"><span data-stu-id="42ead-130">Use a web browser tooopen hello page https://aka.ms/devicelogin and enter hello code tooauthenticate.</span></span> <span data-ttu-id="42ead-131">Jesteś zostanie wyświetlony monit o toolog przy użyciu poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="42ead-131">You are prompted toolog in using your credentials.</span></span>

2. <span data-ttu-id="42ead-132">Po zalogowaniu hello okno wyświetla wszystkie hello subskrypcji platformy Azure, które są skojarzone z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="42ead-132">Once you log in, hello window lists all hello Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="42ead-133">Użyj hello następujące polecenia toouse określonej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="42ead-133">Use hello following command toouse a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="42ead-134">Tworzenie konta usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="42ead-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="42ead-135">Utwórz nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="42ead-135">Create a new resource group.</span></span> <span data-ttu-id="42ead-136">W hello następujące polecenia podaj hello ma toouse wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="42ead-136">In hello following command, provide hello parameter values you want toouse.</span></span> <span data-ttu-id="42ead-137">Jeśli nazwa lokalizacji hello zawiera spacje, umieść ją w cudzysłowie.</span><span class="sxs-lookup"><span data-stu-id="42ead-137">If hello location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="42ead-138">Na przykład „Wschodnie stany USA 2”.</span><span class="sxs-lookup"><span data-stu-id="42ead-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="42ead-139">Tworzenie konta usługi Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="42ead-139">Create hello Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="42ead-140">Tworzenie folderów w ramach konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="42ead-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="42ead-141">Można tworzyć foldery w toomanage konta użytkownika usługi Azure Data Lake Store i przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="42ead-141">You can create folders under your Azure Data Lake Store account toomanage and store data.</span></span> <span data-ttu-id="42ead-142">Witaj Użyj następującego polecenia toocreate folder o nazwie **mojnowyfolder** w głównym hello hello usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="42ead-142">Use hello following command toocreate a folder called **mynewfolder** at hello root of hello Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="42ead-143">Witaj `--folder` parametru zapewnia, że polecenie hello tworzy folder.</span><span class="sxs-lookup"><span data-stu-id="42ead-143">hello `--folder` parameter ensures that hello command creates a folder.</span></span> <span data-ttu-id="42ead-144">Jeśli ten parametr nie jest obecny, hello polecenie tworzy pusty plik o nazwie mojnowyfolder w katalogu głównym hello hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="42ead-144">If this parameter is not present, hello command creates an empty file called mynewfolder at hello root of hello Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a><span data-ttu-id="42ead-145">Przekaż konto usługi Data Lake Store tooa danych</span><span class="sxs-lookup"><span data-stu-id="42ead-145">Upload data tooa Data Lake Store account</span></span>

<span data-ttu-id="42ead-146">Możesz przekazać dane tooData Lake Store bezpośrednio hello tooa lub na poziomie folderu głównego utworzonego w ramach konta hello.</span><span class="sxs-lookup"><span data-stu-id="42ead-146">You can upload data tooData Lake Store directly at hello root level or tooa folder that you created within hello account.</span></span> <span data-ttu-id="42ead-147">Witaj poniższe fragmenty kodu przedstawiają sposób tooupload folderu toohello niektóre przykładowe dane (**mojnowyfolder**) został utworzony w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="42ead-147">hello snippets below demonstrate how tooupload some sample data toohello folder (**mynewfolder**) you created in hello previous section.</span></span>

<span data-ttu-id="42ead-148">Jeśli szukasz niektórych tooupload dane przykładowe, możesz pobrać hello **Ambulance Data** folderu z hello [repozytorium Git programu Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="42ead-148">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="42ead-149">Pobierz plik hello i zapisz go w katalogu lokalnym na komputerze, na przykład C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="42ead-149">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="42ead-150">Dla lokalizacji docelowej hello należy określić pełną ścieżkę hello, łącznie z nazwą pliku hello.</span><span class="sxs-lookup"><span data-stu-id="42ead-150">For hello destination, you must specify hello complete path including hello file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="42ead-151">Wyświetlanie listy plików w ramach konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="42ead-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="42ead-152">Użyj hello następujące polecenia toolist hello pliki w ramach konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="42ead-152">Use hello following command toolist hello files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="42ead-153">Hello dane wyjściowe powinny być podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="42ead-153">hello output of this should be similar toohello following:</span></span>

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="42ead-154">Zmienianie nazwy, pobieranie i usuwanie danych z konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="42ead-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="42ead-155">**toorename pliku**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="42ead-155">**toorename a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="42ead-156">**toodownload pliku**, użyj następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="42ead-156">**toodownload a file**, use hello following command.</span></span> <span data-ttu-id="42ead-157">Upewnij się, że ścieżka docelowa hello już istnieje.</span><span class="sxs-lookup"><span data-stu-id="42ead-157">Make sure hello destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="42ead-158">polecenie Hello tworzy folder docelowy hello, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="42ead-158">hello command creates hello destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="42ead-159">**toodelete pliku**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="42ead-159">**toodelete a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="42ead-160">Jeśli chcesz, aby toodelete hello folder **mojnowyfolder** i plik hello **vehicle1_09142014_copy.csv** razem w jedno polecenie, użyj hello--recurse parametru</span><span class="sxs-lookup"><span data-stu-id="42ead-160">If you want toodelete hello folder **mynewfolder** and hello file **vehicle1_09142014_copy.csv** together in one command, use hello --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="42ead-161">Praca z uprawnieniami i listami kontroli dostępu dla konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="42ead-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="42ead-162">W tej sekcji opisano sposób toomanage listy kontroli dostępu i uprawnień przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="42ead-162">In this section you learn about how toomanage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="42ead-163">Szczegółowe omówienie sposobu implementacji list ACL w usłudze Azure Data Lake Store znajduje się w artykule [Kontrola dostępu w usłudze Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="42ead-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="42ead-164">**Właściciel hello tooupdate plik lub folder**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="42ead-164">**tooupdate hello owner of a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="42ead-165">**tooupdate hello uprawnienia do pliku/folderu**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="42ead-165">**tooupdate hello permissions for a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="42ead-166">**Witaj tooget listy ACL dla danej ścieżki**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="42ead-166">**tooget hello ACLs for a given path**, use hello following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="42ead-167">Hello dane wyjściowe powinny być podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="42ead-167">hello output should be similar toohello following:</span></span>

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* <span data-ttu-id="42ead-168">**tooset wpis dla listy ACL**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="42ead-168">**tooset an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="42ead-169">**tooremove wpis dla listy ACL**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="42ead-169">**tooremove an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="42ead-170">**tooremove cały domyślnej listy ACL**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="42ead-170">**tooremove an entire default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="42ead-171">**tooremove cały ACL innych niż domyślne**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="42ead-171">**tooremove an entire non-default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="42ead-172">Usuwanie konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="42ead-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="42ead-173">Użyj następującego polecenia toodelete konto usługi Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="42ead-173">Use hello following command toodelete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="42ead-174">Po wyświetleniu monitu wprowadź **Y** toodelete hello konta.</span><span class="sxs-lookup"><span data-stu-id="42ead-174">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42ead-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42ead-175">Next steps</span></span>

* [<span data-ttu-id="42ead-176">Informacje o interfejsie wiersza polecenia usługi Azure Data Lake Store 2.0</span><span class="sxs-lookup"><span data-stu-id="42ead-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="42ead-177">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="42ead-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="42ead-178">Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="42ead-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="42ead-179">Korzystanie z usługi Azure HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="42ead-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
