---
title: "Za pomocą usługi Azure CLI 2.0 z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać interfejsu wiersza polecenia platformy Azure (Azure CLI) 2.0, z usługą Azure Storage, aby utworzyć i zarządzać kontami magazynu i pracy z plikami i obiekty BLOB platformy Azure. Azure CLI 2.0 to narzędzie i platform napisanych w języku Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 6098216f7dd901ea48fb3ab969c7934cc288b247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-20-with-azure-storage"></a><span data-ttu-id="9c622-104">Za pomocą usługi Azure CLI 2.0 z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9c622-104">Using the Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="9c622-105">Open source, obsługujący wiele platform 2.0 interfejsu wiersza polecenia Azure udostępnia zestaw poleceń do pracy z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="9c622-105">The open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with the Azure platform.</span></span> <span data-ttu-id="9c622-106">Zapewnia wiele funkcji w [portalu Azure](https://portal.azure.com), w tym dostęp do zaawansowanych danych.</span><span class="sxs-lookup"><span data-stu-id="9c622-106">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="9c622-107">W tym przewodniku zostanie przedstawiony zostanie sposób użycia [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) wykonać kilka czynności, Praca z zasobów na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c622-107">In this guide, we show you how to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to perform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="9c622-108">Firma Microsoft zaleca, Pobierz i zainstaluj lub uaktualnienie do najnowszej wersji 2.0 interfejsu wiersza polecenia przed przy użyciu tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="9c622-108">We recommend that you download and install or upgrade to the latest version of the CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="9c622-109">Przykłady w podręczniku założono korzystanie z powłoki Bash na Ubuntu, ale innych platform, należy wykonać podobnie.</span><span class="sxs-lookup"><span data-stu-id="9c622-109">The examples in the guide assume the use of the Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="9c622-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9c622-110">Prerequisites</span></span>
<span data-ttu-id="9c622-111">W tym przewodniku założono, że rozumiesz podstawowe pojęcia dotyczące środowiska usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9c622-111">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="9c622-112">Przyjęto założenie, że jesteś w stanie spełnić wymagania dotyczące tworzenia konta, określonych poniżej platformy Azure i usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="9c622-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="9c622-113">Konta</span><span class="sxs-lookup"><span data-stu-id="9c622-113">Accounts</span></span>
* <span data-ttu-id="9c622-114">**Konto platformy Azure**: Jeśli nie masz już subskrypcję platformy Azure, [utworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9c622-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="9c622-115">**Konto magazynu**: zobacz sekcję [Tworzenie konta magazynu](../storage/storage-create-storage-account.md#create-a-storage-account) w temacie [Informacje o kontach magazynu Azure](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9c622-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-the-azure-cli-20"></a><span data-ttu-id="9c622-116">Instalacja interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9c622-116">Install the Azure CLI 2.0</span></span>

<span data-ttu-id="9c622-117">Pobierz i zainstaluj 2.0 interfejsu wiersza polecenia platformy Azure, wykonując czynności opisane w [zainstalować Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="9c622-117">Download and install the Azure CLI 2.0 by following the instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="9c622-118">Jeśli masz problemy z instalacją, zapoznaj się [instalacji Rozwiązywanie problemów z](/cli/azure/install-az-cli2#installation-troubleshooting) sekcji tego artykułu oraz [zainstalować Rozwiązywanie problemów z](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) przewodnik w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="9c622-118">If you have trouble with the installation, check out the [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of the article, and the [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-the-cli"></a><span data-ttu-id="9c622-119">Praca z poziomu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="9c622-119">Working with the CLI</span></span>

<span data-ttu-id="9c622-120">Po zainstalowaniu interfejsu wiersza polecenia, można użyć `az` polecenia w interfejsie wiersza polecenia (Bash, Terminal, wiersza polecenia) do poleceń wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c622-120">Once you've installed the CLI, you can use the `az` command in your command-line interface (Bash, Terminal, Command Prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="9c622-121">Typ `az` polecenie, aby wyświetlić pełną listę poleceń podstawowej (następujące przykładowe dane wyjściowe zostały obcięte):</span><span class="sxs-lookup"><span data-stu-id="9c622-121">Type the `az` command to see a full list of the base commands (the following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome to the cool new Azure CLI!

Here are the base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="9c622-122">W interfejsie wiersza polecenia, wykonaj polecenie `az storage --help` do listy `storage` polecenia podgrup.</span><span class="sxs-lookup"><span data-stu-id="9c622-122">In your command-line interface, execute the command `az storage --help` to list the `storage` command subgroups.</span></span> <span data-ttu-id="9c622-123">Opisy podgrupy, które zawierają omówienie funkcji, który zapewnia wiersza polecenia platformy Azure do pracy z zasobami magazynu.</span><span class="sxs-lookup"><span data-stu-id="9c622-123">The descriptions of the subgroups provide an overview of the functionality the Azure CLI provides for working with your storage resources.</span></span>

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use the standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues to effectively scale applications according to traffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-the-cli-to-your-azure-subscription"></a><span data-ttu-id="9c622-124">Interfejsu wiersza polecenia nawiązać połączenia z subskrypcją platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9c622-124">Connect the CLI to your Azure subscription</span></span>

<span data-ttu-id="9c622-125">Do pracy z zasobami w Twojej subskrypcji platformy Azure, musi najpierw logujesz się do konta platformy Azure z `az login`.</span><span class="sxs-lookup"><span data-stu-id="9c622-125">To work with the resources in your Azure subscription, you must first log in to your Azure account with `az login`.</span></span> <span data-ttu-id="9c622-126">Istnieje kilka metod, które możesz zalogować się:</span><span class="sxs-lookup"><span data-stu-id="9c622-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="9c622-127">**Logowanie interakcyjne**:`az login`</span><span class="sxs-lookup"><span data-stu-id="9c622-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="9c622-128">**Zaloguj się przy użyciu nazwy użytkownika i hasła**:`az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="9c622-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="9c622-129">To nie działa z konta Microsoft lub konta, które korzystają z uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="9c622-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="9c622-130">**Zaloguj się przy użyciu nazwy głównej usługi**:`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="9c622-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="9c622-131">Azure CLI 2.0 przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9c622-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="9c622-132">Następnie będzie pracujemy ze skryptem małych powłoki, który wystawia kilka podstawowych poleceń Azure CLI 2.0 do interakcji z zasobami magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c622-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands to interact with Azure Storage resources.</span></span> <span data-ttu-id="9c622-133">Skrypt najpierw tworzy nowy kontener na koncie magazynu, a następnie przekazuje istniejącego pliku (jako obiektu blob) do tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="9c622-133">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container.</span></span> <span data-ttu-id="9c622-134">Wyświetla listę wszystkich obiektów blob w kontenerze, a na koniec pobierze plik do miejsca docelowego na komputerze lokalnym, który określisz.</span><span class="sxs-lookup"><span data-stu-id="9c622-134">It then lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating the container..."
az storage container create --name $container_name

echo "Uploading the file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing the blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading the file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="9c622-135">**Skonfiguruj i uruchom skrypt**</span><span class="sxs-lookup"><span data-stu-id="9c622-135">**Configure and run the script**</span></span>

1. <span data-ttu-id="9c622-136">Otwórz w ulubionym edytorze tekstów, a następnie skopiuj i Wklej powyższy skrypt w edytorze.</span><span class="sxs-lookup"><span data-stu-id="9c622-136">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>

2. <span data-ttu-id="9c622-137">Następnie zaktualizuj zmienne skryptu, aby odzwierciedlić ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9c622-137">Next, update the script's variables to reflect your configuration settings.</span></span> <span data-ttu-id="9c622-138">Zastąp następujące wartości określonych:</span><span class="sxs-lookup"><span data-stu-id="9c622-138">Replace the following values as specified:</span></span>

   * <span data-ttu-id="9c622-139">**\<storage_account_name\>**  nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="9c622-139">**\<storage_account_name\>** The name of your storage account.</span></span>
   * <span data-ttu-id="9c622-140">**\<storage_account_key\>**  klucz podstawowy lub pomocniczy dostępu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="9c622-140">**\<storage_account_key\>** The primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="9c622-141">**\<container_name\>**  A Nazwa nowego kontenera, aby utworzyć, takie jak "azure-cli — próbki container".</span><span class="sxs-lookup"><span data-stu-id="9c622-141">**\<container_name\>** A name the new container to create, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="9c622-142">**\<blob_name\>**  nazwę docelowego obiektu blob w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="9c622-142">**\<blob_name\>** A name for the destination blob in the container.</span></span>
   * <span data-ttu-id="9c622-143">**\<file_to_upload\>**  ścieżkę do małych plików na komputerze lokalnym, takich jak "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="9c622-143">**\<file_to_upload\>** The path to small file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="9c622-144">**\<destination_file\>**  docelowego pliku ścieżki, takie jak "~ / downloadedImage.png".</span><span class="sxs-lookup"><span data-stu-id="9c622-144">**\<destination_file\>** The destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="9c622-145">Po zaktualizowaniu niezbędne zmienne zapisać skrypt, a następnie zamknij Edytor.</span><span class="sxs-lookup"><span data-stu-id="9c622-145">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="9c622-146">Następnych krokach założono nazwanego skryptu **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="9c622-146">The next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="9c622-147">Należy oznaczyć skrypt jako plik wykonywalny, w razie potrzeby:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="9c622-147">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="9c622-148">Uruchom skrypt.</span><span class="sxs-lookup"><span data-stu-id="9c622-148">Execute the script.</span></span> <span data-ttu-id="9c622-149">Na przykład w Bash:`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="9c622-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="9c622-150">Powinny pojawić się dane wyjściowe podobne do następujących i  **\<destination_file\>**  podana w skrypcie powinien zostać wyświetlony na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="9c622-150">You should see output similar to the following, and the **\<destination_file\>** you specified in the script should appear on your local computer.</span></span>

```
Creating the container...
{
  "created": true
}
Uploading the file...
Percent complete: %100.0
Listing the blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading the file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="9c622-151">Powyższy wynik jest **tabeli** format.</span><span class="sxs-lookup"><span data-stu-id="9c622-151">The preceding output is in **table** format.</span></span> <span data-ttu-id="9c622-152">Można określić formatu do użycia przez określenie wyjściowy, który `--output` argument w poleceniach interfejsu wiersza polecenia lub ustaw ją za pomocą `az configure`.</span><span class="sxs-lookup"><span data-stu-id="9c622-152">You can specify which output format to use by specifying the `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="9c622-153">Zarządzanie kontami magazynu</span><span class="sxs-lookup"><span data-stu-id="9c622-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="9c622-154">Utwórz nowe konto magazynu</span><span class="sxs-lookup"><span data-stu-id="9c622-154">Create a new storage account</span></span>
<span data-ttu-id="9c622-155">Aby móc użyć usługi Azure Storage, musisz mieć konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="9c622-155">To use Azure Storage, you need a storage account.</span></span> <span data-ttu-id="9c622-156">Po skonfigurowaniu komputera, można utworzyć nowe konto magazynu Azure [nawiązać połączenia z subskrypcją](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="9c622-156">You can create a new Azure Storage account after you've configured your computer to [connect to your subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="9c622-157">`--location`[Wymagane]: lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="9c622-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="9c622-158">Na przykład "zachodnie stany USA".</span><span class="sxs-lookup"><span data-stu-id="9c622-158">For example, "West US".</span></span>
* <span data-ttu-id="9c622-159">`--name`[Wymagane]: Nazwa konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="9c622-159">`--name` [Required]: The storage account name.</span></span> <span data-ttu-id="9c622-160">Nazwa musi składać się z 3 do 24 znaków i zawierać tylko małe znaki alfanumeryczne.</span><span class="sxs-lookup"><span data-stu-id="9c622-160">The name must be 3 to 24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="9c622-161">`--resource-group`[Wymagane]: Nazwa grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c622-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="9c622-162">`--sku`[Wymagane]: Konto magazynu wersji.</span><span class="sxs-lookup"><span data-stu-id="9c622-162">`--sku` [Required]: The storage account SKU.</span></span> <span data-ttu-id="9c622-163">Dozwolone wartości:</span><span class="sxs-lookup"><span data-stu-id="9c622-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="9c622-164">Ustaw zmienne środowiskowe domyślne konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="9c622-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="9c622-165">Może mieć wielu kont magazynu w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c622-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="9c622-166">Aby wybrać jeden z nich do użycia dla wszystkich poleceń kolejnych magazynu, można ustawić zmienne środowiskowe:</span><span class="sxs-lookup"><span data-stu-id="9c622-166">To select one of them to use for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="9c622-167">Innym sposobem ustawienia domyślne konto magazynu jest przy użyciu ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="9c622-167">Another way to set a default storage account is by using a connection string.</span></span> <span data-ttu-id="9c622-168">Najpierw należy pobrać ciągu połączenia z `show-connection-string` polecenia:</span><span class="sxs-lookup"><span data-stu-id="9c622-168">First, get the connection string with the `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="9c622-169">Następnie skopiuj parametry połączenia danych wyjściowych i ustaw `AZURE_STORAGE_CONNECTION_STRING` zmiennej środowiskowej (może być konieczne parametry połączenia, należy ująć w cudzysłowy):</span><span class="sxs-lookup"><span data-stu-id="9c622-169">Then copy the output connection string and set the `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need to enclose the connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="9c622-170">Wszystkie przykłady w następujących sekcjach w tym artykule założono, że ustawiono `AZURE_STORAGE_ACCOUNT` i `AZURE_STORAGE_ACCESS_KEY` zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="9c622-170">All examples in the following sections of this article assume that you've set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="9c622-171">Tworzenie i zarządzanie nimi obiektów blob</span><span class="sxs-lookup"><span data-stu-id="9c622-171">Create and manage blobs</span></span>
<span data-ttu-id="9c622-172">Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, takich jak dane tekstowe lub binarne, którego mogą uzyskać dostęp z dowolnego miejsca na świecie za pośrednictwem protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9c622-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="9c622-173">W tej sekcji założono, że znasz już pojęcia dotyczące magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c622-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="9c622-174">Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md) i [pojęcia dotyczące usługi Blob](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="9c622-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="9c622-175">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="9c622-175">Create a container</span></span>
<span data-ttu-id="9c622-176">Każdy obiekt blob w magazynie Azure musi być w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="9c622-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="9c622-177">Kontener można utworzyć przy użyciu `az storage container create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="9c622-177">You can create a container by using the `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="9c622-178">Można ustawić jedną z trzech poziomów dostępu do odczytu dla nowego kontenera, określając opcjonalny `--public-access` argumentu:</span><span class="sxs-lookup"><span data-stu-id="9c622-178">You can set one of three levels of read access for a new container by specifying the optional  `--public-access` argument:</span></span>

* <span data-ttu-id="9c622-179">`off`(domyślnie): dane w kontenerze są prywatne dla właściciela konta.</span><span class="sxs-lookup"><span data-stu-id="9c622-179">`off` (default): Container data is private to the account owner.</span></span>
* <span data-ttu-id="9c622-180">`blob`: Publiczny dostęp do odczytu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="9c622-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="9c622-181">`container`: Publiczny dostęp do odczytu i listy do całego kontenera.</span><span class="sxs-lookup"><span data-stu-id="9c622-181">`container`: Public read and list access to the entire container.</span></span>

<span data-ttu-id="9c622-182">Aby uzyskać więcej informacji, zobacz [Zarządzanie anonimowy dostęp do odczytu do kontenerów i obiektów blob](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="9c622-182">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-to-a-container"></a><span data-ttu-id="9c622-183">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="9c622-183">Upload a blob to a container</span></span>
<span data-ttu-id="9c622-184">Azure Blob storage obsługuje blok, Dołącz i stronicowe.</span><span class="sxs-lookup"><span data-stu-id="9c622-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="9c622-185">Przekaż obiekty BLOB do kontenera za pomocą `blob upload` polecenia:</span><span class="sxs-lookup"><span data-stu-id="9c622-185">Upload blobs to a container by using the `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="9c622-186">Domyślnie `blob upload` polecenie wysyła pliki *.vhd stronicowych obiektów blob lub blokowych obiektów blob w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="9c622-186">By default, the `blob upload` command uploads *.vhd files to page blobs, or block blobs otherwise.</span></span> <span data-ttu-id="9c622-187">Aby określić inny typ podczas ładowania obiektu blob, można użyć `--type` argumentu--dozwolone wartości są `append`, `block`, i `page`.</span><span class="sxs-lookup"><span data-stu-id="9c622-187">To specify another type when you upload a blob, you can use the `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="9c622-188">Aby uzyskać więcej informacji o typach różnych obiektów blob, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="9c622-188">For more information on the different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="9c622-189">Pobieranie obiektu blob z kontenera</span><span class="sxs-lookup"><span data-stu-id="9c622-189">Download a blob from a container</span></span>
<span data-ttu-id="9c622-190">W tym przykładzie pokazano, jak pobrać obiektu blob z kontenera:</span><span class="sxs-lookup"><span data-stu-id="9c622-190">This example demonstrates how to download a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="9c622-191">Wyświetlanie listy obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="9c622-191">List the blobs in a container</span></span>

<span data-ttu-id="9c622-192">Wyświetlanie obiektów blob w kontenerze o [az magazynu obiektów blob listy](/cli/azure/storage/blob#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="9c622-192">List the blobs in a container with the [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="9c622-193">Kopiowanie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="9c622-193">Copy blobs</span></span>
<span data-ttu-id="9c622-194">Można asynchronicznie kopiować obiekty blob w obrębie konta magazynu i regionu lub między różnymi kontami magazynu i regionami.</span><span class="sxs-lookup"><span data-stu-id="9c622-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="9c622-195">W poniższym przykładzie pokazano sposób kopiowania obiektów blob z jednego konta magazynu do innego.</span><span class="sxs-lookup"><span data-stu-id="9c622-195">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="9c622-196">Najpierw trzeba utworzyć kontener na źródłowym koncie magazynu, określając publiczny dostęp do odczytu do jego obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="9c622-196">We first create a container in the source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="9c622-197">Następnie plik zostanie przekazany do kontenera, a potem obiekt blob z tego kontenera zostanie skopiowany do kontenera na docelowym koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="9c622-197">Next, we upload a file to the container, and finally, copy the blob from that container into a container in the destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob to container in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account to destination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="9c622-198">W powyższym przykładzie kontener docelowy musi już istnieć na koncie magazynu docelowy operacji kopiowania powiodła się.</span><span class="sxs-lookup"><span data-stu-id="9c622-198">In the above example, the destination container must already exist in the destination storage account for the copy operation to succeed.</span></span> <span data-ttu-id="9c622-199">Ponadto źródłowy obiekt blob wskazany za pomocą argumentu `--source-uri` musi zawierać token sygnatury dostępu współdzielonego (SAS) albo musi być dostępny publicznie, jak w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="9c622-199">Additionally, the source blob specified in the `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="9c622-200">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="9c622-200">Delete a blob</span></span>
<span data-ttu-id="9c622-201">Aby usunąć obiekt blob, użyj `blob delete` polecenia:</span><span class="sxs-lookup"><span data-stu-id="9c622-201">To delete a blob, use the `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="9c622-202">Tworzenie i Zarządzanie udziałami plików</span><span class="sxs-lookup"><span data-stu-id="9c622-202">Create and manage file shares</span></span>
<span data-ttu-id="9c622-203">Magazyn plików Azure oferuje współużytkowany magazyn dla aplikacji używających protokołu bloku komunikatów serwera (SMB).</span><span class="sxs-lookup"><span data-stu-id="9c622-203">Azure File storage offers shared storage for applications using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="9c622-204">Maszyny wirtualne Microsoft Azure i usługi w chmurze, a także aplikacje lokalne mogą udostępniać dane za pośrednictwem zainstalowanych udziałów.</span><span class="sxs-lookup"><span data-stu-id="9c622-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="9c622-205">Możesz zarządzać udziałami plików i danych plików za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c622-205">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="9c622-206">Aby uzyskać więcej informacji dotyczących usługi Magazyn plików Azure, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](storage-dotnet-how-to-use-files.md) lub [jak używać magazynu plików Azure z systemem Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9c622-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="9c622-207">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="9c622-207">Create a file share</span></span>
<span data-ttu-id="9c622-208">Udział plików Azure jest udziałem plików SMB na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9c622-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="9c622-209">Wszystkie pliki i katalogi, należy utworzyć w udziale plików.</span><span class="sxs-lookup"><span data-stu-id="9c622-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="9c622-210">Konto może zawierać nieograniczoną liczbę udziałów, a udział może przechowywać nieograniczoną liczbę plików do osiągnięcia limitu pojemności konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="9c622-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="9c622-211">Poniższy przykład tworzy udział plików o nazwie **moj_udzial**.</span><span class="sxs-lookup"><span data-stu-id="9c622-211">The following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="9c622-212">Tworzenie katalogu</span><span class="sxs-lookup"><span data-stu-id="9c622-212">Create a directory</span></span>
<span data-ttu-id="9c622-213">Katalog udostępnia strukturę hierarchiczną w udziale plików na platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="9c622-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="9c622-214">Poniższy przykład tworzy katalog o nazwie **myDir** w udziale plików.</span><span class="sxs-lookup"><span data-stu-id="9c622-214">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="9c622-215">Ścieżki katalogu może zawierać wiele poziomów, na przykład **katalog1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="9c622-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="9c622-216">Należy jednak upewnij się, że wszystkie katalogi nadrzędne istnieć przed utworzeniem podkatalogu.</span><span class="sxs-lookup"><span data-stu-id="9c622-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="9c622-217">Na przykład dla ścieżki **katalog1/dir2**, należy najpierw utworzyć katalog **katalog1**, następnie utwórz katalog **dir2**.</span><span class="sxs-lookup"><span data-stu-id="9c622-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-to-a-share"></a><span data-ttu-id="9c622-218">Przekazanie pliku lokalnego do udziału</span><span class="sxs-lookup"><span data-stu-id="9c622-218">Upload a local file to a share</span></span>
<span data-ttu-id="9c622-219">Poniższy przykład przekazuje plik z **~/temp/samplefile.txt** do głównego **moj_udzial** udziału plików.</span><span class="sxs-lookup"><span data-stu-id="9c622-219">The following example uploads a file from **~/temp/samplefile.txt** to root of the **myshare** file share.</span></span> <span data-ttu-id="9c622-220">`--source` Argument określa istniejący plik lokalny do przekazania.</span><span class="sxs-lookup"><span data-stu-id="9c622-220">The `--source` argument specifies the existing local file to upload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="9c622-221">Jako o utworzenie katalogu, można określić ścieżkę katalogu w udziale można przekazać pliku do istniejącego katalogu w obrębie udziału:</span><span class="sxs-lookup"><span data-stu-id="9c622-221">As with directory creation, you can specify a directory path within the share to upload the file to an existing directory within the share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="9c622-222">Plik w udziale może być o rozmiarze do 1 TB.</span><span class="sxs-lookup"><span data-stu-id="9c622-222">A file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-a-share"></a><span data-ttu-id="9c622-223">Lista plików w udziale</span><span class="sxs-lookup"><span data-stu-id="9c622-223">List the files in a share</span></span>
<span data-ttu-id="9c622-224">Można wyświetlić listę plików i katalogów w udziale, przy użyciu `az storage file list` polecenia:</span><span class="sxs-lookup"><span data-stu-id="9c622-224">You can list files and directories in a share by using the `az storage file list` command:</span></span>

```azurecli
# List the files in the root of a share
az storage file list --share-name myshare --output table

# List the files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List the files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="9c622-225">Kopiowanie plików</span><span class="sxs-lookup"><span data-stu-id="9c622-225">Copy files</span></span>      
<span data-ttu-id="9c622-226">Można skopiować pliku do innego pliku, pliki do obiektu blob, obiekty blob do pliku.</span><span class="sxs-lookup"><span data-stu-id="9c622-226">You can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="9c622-227">Na przykład, aby skopiować plik do katalogu w inny udział:</span><span class="sxs-lookup"><span data-stu-id="9c622-227">For example, to copy a file to a directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="9c622-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9c622-228">Next steps</span></span>
<span data-ttu-id="9c622-229">Poniżej przedstawiono dodatkowe zasoby dowiedzieć się więcej o pracy z 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c622-229">Here are some additional resources for learning more about working with the Azure CLI 2.0.</span></span>

* [<span data-ttu-id="9c622-230">Wprowadzenie do usługi Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9c622-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="9c622-231">Dokumentacja poleceń interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9c622-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="9c622-232">Azure CLI 2.0 w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="9c622-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
