---
title: "Rozpoczynanie pracy z usługą Azure Data Lake Store przy użyciu interfejsu wiersza polecenia platformy Azure 2.0 | Microsoft Docs"
description: "Korzystanie z międzyplatformowego wiersza polecenia platformy Azure 2.0 w celu utworzenia konta usługi Data Lake Store i wykonywania podstawowych operacji"
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
ms.openlocfilehash: ed78d25f2bac0a9996f1796ee503f31a36940977
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="4c25d-103">Rozpoczynanie pracy z usługą Azure Data Lake Store za pomocą interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4c25d-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c25d-104">Portal</span><span class="sxs-lookup"><span data-stu-id="4c25d-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="4c25d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c25d-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="4c25d-106">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="4c25d-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="4c25d-107">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="4c25d-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="4c25d-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="4c25d-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="4c25d-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4c25d-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="4c25d-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="4c25d-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="4c25d-111">Python</span><span class="sxs-lookup"><span data-stu-id="4c25d-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="4c25d-112">Dowiedz się, jak przy użyciu interfejsu wiersza polecenia platformy Azure 2.0 utworzyć konto usługi Azure Data Lake Store i wykonywać podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych, usuwanie konta itp. Aby uzyskać więcej informacji o usłudze Data Lake Store, zobacz [Omówienie usługi Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c25d-112">Learn how to use Azure CLI 2.0 to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="4c25d-113">Interfejs wiersza polecenia platformy Azure 2.0 to nowe środowisko wiersza polecenia platformy Azure do zarządzania jej zasobami.</span><span class="sxs-lookup"><span data-stu-id="4c25d-113">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="4c25d-114">Można go używać w systemach macOS, Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="4c25d-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="4c25d-115">Aby uzyskać więcej informacji, zobacz [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview) (Przegląd interfejsu wiersza polecenia platformy Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="4c25d-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="4c25d-116">Aby wyświetlić pełną listę poleceń i składnię, zobacz artykuł [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) (Informacje o interfejsie wiersza polecenia usługi Azure Data Lake Store 2.0).</span><span class="sxs-lookup"><span data-stu-id="4c25d-116">You can also look at the [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4c25d-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4c25d-117">Prerequisites</span></span>
<span data-ttu-id="4c25d-118">Przed rozpoczęciem korzystania z informacji zawartych w tym artykule należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="4c25d-118">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="4c25d-119">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="4c25d-119">**An Azure subscription**.</span></span> <span data-ttu-id="4c25d-120">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c25d-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="4c25d-121">**Interfejs wiersza polecenia platformy Azure 2.0** — instrukcje znajdują się w artykule [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Instalowanie interfejsu wiersza polecenia platformy Azure w wersji 2.0).</span><span class="sxs-lookup"><span data-stu-id="4c25d-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="4c25d-122">Authentication</span><span class="sxs-lookup"><span data-stu-id="4c25d-122">Authentication</span></span>

<span data-ttu-id="4c25d-123">W tym artykule użyto prostszej metody uwierzytelniania w usłudze Data Lake Store, w przypadku której logujesz się jako użytkownik końcowy.</span><span class="sxs-lookup"><span data-stu-id="4c25d-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="4c25d-124">Poziom dostępu do konta i systemu plików usługi Data Lake Store jest określany przez poziom dostępu zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4c25d-124">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="4c25d-125">Istnieją jednak inne metody uwierzytelniania w usłudze Data Lake Store: **uwierzytelnianie użytkowników końcowych** i **uwierzytelnianie między usługami**.</span><span class="sxs-lookup"><span data-stu-id="4c25d-125">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="4c25d-126">Aby uzyskać instrukcje i więcej informacji na temat uwierzytelniania, zobacz [Uwierzytelnianie użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [Uwierzytelnianie między usługami](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="4c25d-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="4c25d-127">Logowanie się do subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4c25d-127">Log in to your Azure subscription</span></span>

1. <span data-ttu-id="4c25d-128">Zaloguj się do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4c25d-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="4c25d-129">Uzyskasz kod do użycia w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="4c25d-129">You get a code to use in the next step.</span></span> <span data-ttu-id="4c25d-130">Użyj przeglądarki sieci Web, aby otworzyć stronę https://aka.ms/devicelogin, i wprowadź kod w celu uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="4c25d-130">Use a web browser to open the page https://aka.ms/devicelogin and enter the code to authenticate.</span></span> <span data-ttu-id="4c25d-131">Zostanie wyświetlony monit o zalogowanie się przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="4c25d-131">You are prompted to log in using your credentials.</span></span>

2. <span data-ttu-id="4c25d-132">Po zalogowaniu w oknie zostanie wyświetlona lista wszystkich subskrypcji platformy Azure, które są skojarzone z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="4c25d-132">Once you log in, the window lists all the Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="4c25d-133">Za pomocą następującego polecenia użyj konkretnej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4c25d-133">Use the following command to use a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="4c25d-134">Tworzenie konta usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4c25d-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="4c25d-135">Utwórz nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="4c25d-135">Create a new resource group.</span></span> <span data-ttu-id="4c25d-136">W poniższym poleceniu podaj wartości parametrów, których chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="4c25d-136">In the following command, provide the parameter values you want to use.</span></span> <span data-ttu-id="4c25d-137">Jeśli nazwa lokalizacji zawiera spacje, umieść ją w cudzysłowie.</span><span class="sxs-lookup"><span data-stu-id="4c25d-137">If the location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="4c25d-138">Na przykład „Wschodnie stany USA 2”.</span><span class="sxs-lookup"><span data-stu-id="4c25d-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="4c25d-139">Utwórz konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c25d-139">Create the Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="4c25d-140">Tworzenie folderów w ramach konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4c25d-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="4c25d-141">Na koncie usługi Azure Data Lake Store można tworzyć foldery w celu przechowywania danych i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="4c25d-141">You can create folders under your Azure Data Lake Store account to manage and store data.</span></span> <span data-ttu-id="4c25d-142">Za pomocą następującego polecenia utwórz folder o nazwie **mojnowyfolder** w katalogu głównym usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c25d-142">Use the following command to create a folder called **mynewfolder** at the root of the Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="4c25d-143">Parametr `--folder` gwarantuje, że polecenie utworzy folder.</span><span class="sxs-lookup"><span data-stu-id="4c25d-143">The `--folder` parameter ensures that the command creates a folder.</span></span> <span data-ttu-id="4c25d-144">Jeśli ten parametr zostanie pominięty, polecenie utworzy w katalogu głównym konta usługi Data Lake Store pusty plik o nazwie mojnowyfolder.</span><span class="sxs-lookup"><span data-stu-id="4c25d-144">If this parameter is not present, the command creates an empty file called mynewfolder at the root of the Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-to-a-data-lake-store-account"></a><span data-ttu-id="4c25d-145">Przekazywanie danych do konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4c25d-145">Upload data to a Data Lake Store account</span></span>

<span data-ttu-id="4c25d-146">Dane można przekazywać do konta usługi Data Lake Store bezpośrednio do katalogu głównego lub do folderu utworzonego w ramach konta.</span><span class="sxs-lookup"><span data-stu-id="4c25d-146">You can upload data to Data Lake Store directly at the root level or to a folder that you created within the account.</span></span> <span data-ttu-id="4c25d-147">Poniższe fragmenty kodu przedstawiają sposób przekazywania przykładowych danych do folderu (**mojnowyfolder**), który został utworzony w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="4c25d-147">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span></span>

<span data-ttu-id="4c25d-148">Jeśli szukasz przykładowych danych do przekazania, możesz pobrać folder **Ambulance Data** z [repozytorium Git usługi Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="4c25d-148">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="4c25d-149">Pobierz plik i zapisz go w katalogu lokalnym na komputerze, na przykład C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="4c25d-149">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="4c25d-150">W przypadku podawania miejsca docelowego należy określić pełną ścieżkę, łącznie z nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="4c25d-150">For the destination, you must specify the complete path including the file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="4c25d-151">Wyświetlanie listy plików w ramach konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4c25d-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="4c25d-152">Użyj poniższego polecenia, aby wyświetlić listę plików na koncie usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c25d-152">Use the following command to list the files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="4c25d-153">Dane wyjściowe będą mieć postać podobną do następującej:</span><span class="sxs-lookup"><span data-stu-id="4c25d-153">The output of this should be similar to the following:</span></span>

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="4c25d-154">Zmienianie nazwy, pobieranie i usuwanie danych z konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4c25d-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="4c25d-155">**Aby zmienić nazwę pliku**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4c25d-155">**To rename a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="4c25d-156">**Aby pobrać plik**, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="4c25d-156">**To download a file**, use the following command.</span></span> <span data-ttu-id="4c25d-157">Upewnij się, że ścieżka docelowa już istnieje.</span><span class="sxs-lookup"><span data-stu-id="4c25d-157">Make sure the destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="4c25d-158">Polecenie tworzy folder docelowy, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="4c25d-158">The command creates the destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="4c25d-159">**Aby usunąć plik**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4c25d-159">**To delete a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="4c25d-160">Jeśli chcesz usunąć folder **mojnowyfolder** i plik **vehicle1_09142014_copy.csv** za pomocą jednego polecenia, użyj parametru --recurse</span><span class="sxs-lookup"><span data-stu-id="4c25d-160">If you want to delete the folder **mynewfolder** and the file **vehicle1_09142014_copy.csv** together in one command, use the --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="4c25d-161">Praca z uprawnieniami i listami kontroli dostępu dla konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4c25d-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="4c25d-162">W tej sekcji zawarto informacje o sposobie zarządzania listami kontroli dostępu (ACL) i uprawnieniami przy użyciu interfejsu wiersza polecenia platformy Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="4c25d-162">In this section you learn about how to manage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="4c25d-163">Szczegółowe omówienie sposobu implementacji list ACL w usłudze Azure Data Lake Store znajduje się w artykule [Kontrola dostępu w usłudze Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="4c25d-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="4c25d-164">**Aby zaktualizować właściciela pliku/folderu**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4c25d-164">**To update the owner of a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="4c25d-165">**Aby zaktualizować uprawnienia do pliku/folderu**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4c25d-165">**To update the permissions for a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="4c25d-166">**Aby uzyskać listy ACL dla danej ścieżki**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4c25d-166">**To get the ACLs for a given path**, use the following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="4c25d-167">Dane wyjściowe będą podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="4c25d-167">The output should be similar to the following:</span></span>

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

* <span data-ttu-id="4c25d-168">**Aby ustawić pozycję listy ACL**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4c25d-168">**To set an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="4c25d-169">**Aby usunąć pozycję z listy ACL**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4c25d-169">**To remove an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="4c25d-170">**Aby usunąć całą domyślną listę ACL**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4c25d-170">**To remove an entire default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="4c25d-171">**Aby usunąć całą inną niż domyślną listę ACL**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4c25d-171">**To remove an entire non-default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="4c25d-172">Usuwanie konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4c25d-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="4c25d-173">Użyj poniższego polecenia, aby usunąć konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c25d-173">Use the following command to delete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="4c25d-174">Po wyświetleniu monitu wpisz **Y**, aby usunąć konto.</span><span class="sxs-lookup"><span data-stu-id="4c25d-174">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c25d-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4c25d-175">Next steps</span></span>

* [<span data-ttu-id="4c25d-176">Informacje o interfejsie wiersza polecenia usługi Azure Data Lake Store 2.0</span><span class="sxs-lookup"><span data-stu-id="4c25d-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="4c25d-177">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4c25d-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="4c25d-178">Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4c25d-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="4c25d-179">Korzystanie z usługi Azure HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4c25d-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
