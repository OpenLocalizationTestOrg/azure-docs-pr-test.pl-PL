---
title: "Witaj aaaUsing 2.0 interfejsu wiersza polecenia platformy Azure z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello interfejsu wiersza polecenia platformy Azure (Azure CLI) 2.0, o toocreate magazynu Azure i zarządzanie kontami magazynu i pracować z plikami i obiekty BLOB platformy Azure. Hello Azure CLI 2.0 to narzędzie i platform napisanych w języku Python."
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
ms.openlocfilehash: 14e6eb0c913676380c90a72563276245e7f08aa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a><span data-ttu-id="f65c0-104">Przy użyciu hello 2.0 interfejsu wiersza polecenia platformy Azure z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f65c0-104">Using hello Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="f65c0-105">Hello open source, 2.0 interfejsu wiersza polecenia platformy Azure i platform udostępnia zestaw poleceń do pracy z hello platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f65c0-105">hello open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with hello Azure platform.</span></span> <span data-ttu-id="f65c0-106">Zapewnia znacznie hello tę samą funkcjonalność znalezione w hello [portalu Azure](https://portal.azure.com), w tym dostęp do zaawansowanych danych.</span><span class="sxs-lookup"><span data-stu-id="f65c0-106">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="f65c0-107">W tym przewodniku zostanie przedstawiony zostanie sposób toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform kilka zadań, Praca z zasobów na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="f65c0-107">In this guide, we show you how toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="f65c0-108">Zaleca się pobrać i zainstalować lub uaktualnić toohello najnowszą wersję hello 2.0 interfejsu wiersza polecenia przed rozpoczęciem korzystania z tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="f65c0-108">We recommend that you download and install or upgrade toohello latest version of hello CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="f65c0-109">Przykłady Hello w przewodniku hello założono użycie hello hello powłoki Bash na Ubuntu, ale innych platform, należy wykonać podobnie.</span><span class="sxs-lookup"><span data-stu-id="f65c0-109">hello examples in hello guide assume hello use of hello Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="f65c0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f65c0-110">Prerequisites</span></span>
<span data-ttu-id="f65c0-111">W tym przewodniku założono, że rozumiesz hello podstawowych pojęciach dotyczących usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f65c0-111">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="f65c0-112">Przyjęto założenie, że jesteś toosatisfy stanie hello tworzenie wymagania dotyczące konta określonych poniżej platformy Azure i hello usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="f65c0-112">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="f65c0-113">Konta</span><span class="sxs-lookup"><span data-stu-id="f65c0-113">Accounts</span></span>
* <span data-ttu-id="f65c0-114">**Konto platformy Azure**: Jeśli nie masz już subskrypcję platformy Azure, [utworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f65c0-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="f65c0-115">**Konto magazynu**: zobacz sekcję [Tworzenie konta magazynu](storage-create-storage-account.md#create-a-storage-account) w temacie [Informacje o kontach magazynu Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f65c0-115">**Storage account**: See [Create a storage account](storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](storage-create-storage-account.md).</span></span>

### <a name="install-hello-azure-cli-20"></a><span data-ttu-id="f65c0-116">Zainstaluj hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f65c0-116">Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="f65c0-117">Pobierz i zainstaluj hello Azure CLI 2.0, wykonując instrukcje hello opisane w temacie [zainstalować Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f65c0-117">Download and install hello Azure CLI 2.0 by following hello instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="f65c0-118">Jeśli masz problemy z instalacją hello, zapoznaj się hello [Rozwiązywanie problemów z instalacji](/cli/azure/install-az-cli2#installation-troubleshooting) części artykułu hello i hello [zainstalować Rozwiązywanie problemów z](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) przewodnik w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="f65c0-118">If you have trouble with hello installation, check out hello [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of hello article, and hello [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-hello-cli"></a><span data-ttu-id="f65c0-119">Praca z hello interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="f65c0-119">Working with hello CLI</span></span>

<span data-ttu-id="f65c0-120">Po zainstalowaniu hello interfejsu wiersza polecenia, można użyć hello `az` polecenia w poleceniach wiersza polecenia platformy Azure hello tooaccess interfejsu wiersza polecenia (Bash, Terminal wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="f65c0-120">Once you've installed hello CLI, you can use hello `az` command in your command-line interface (Bash, Terminal, Command Prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="f65c0-121">Typ hello `az` toosee polecenia pełną listę poleceń podstawowej hello (hello następujące przykładowe dane wyjściowe zostały obcięte):</span><span class="sxs-lookup"><span data-stu-id="f65c0-121">Type hello `az` command toosee a full list of hello base commands (hello following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="f65c0-122">W interfejsie wiersza polecenia, wykonaj polecenie hello `az storage --help` toolist hello `storage` polecenia podgrup.</span><span class="sxs-lookup"><span data-stu-id="f65c0-122">In your command-line interface, execute hello command `az storage --help` toolist hello `storage` command subgroups.</span></span> <span data-ttu-id="f65c0-123">opisy Hello podgrupy hello omówiono hello powitalne funkcji interfejsu wiersza polecenia Azure zapewnia do pracy z zasobami magazynu.</span><span class="sxs-lookup"><span data-stu-id="f65c0-123">hello descriptions of hello subgroups provide an overview of hello functionality hello Azure CLI provides for working with your storage resources.</span></span>

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
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a><span data-ttu-id="f65c0-124">Połącz hello CLI tooyour subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f65c0-124">Connect hello CLI tooyour Azure subscription</span></span>

<span data-ttu-id="f65c0-125">toowork hello zasobów w Twojej subskrypcji platformy Azure, musisz najpierw zalogować się tooyour konto platformy Azure z `az login`.</span><span class="sxs-lookup"><span data-stu-id="f65c0-125">toowork with hello resources in your Azure subscription, you must first log in tooyour Azure account with `az login`.</span></span> <span data-ttu-id="f65c0-126">Istnieje kilka metod, które możesz zalogować się:</span><span class="sxs-lookup"><span data-stu-id="f65c0-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="f65c0-127">**Logowanie interakcyjne**:`az login`</span><span class="sxs-lookup"><span data-stu-id="f65c0-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="f65c0-128">**Zaloguj się przy użyciu nazwy użytkownika i hasła**:`az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="f65c0-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="f65c0-129">To nie działa z konta Microsoft lub konta, które korzystają z uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="f65c0-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="f65c0-130">**Zaloguj się przy użyciu nazwy głównej usługi**:`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="f65c0-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="f65c0-131">Azure CLI 2.0 przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f65c0-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="f65c0-132">Następnie będzie pracujemy ze skryptem małych powłoki, który wystawia kilka podstawowych toointeract poleceń Azure CLI 2.0 z zasobami magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f65c0-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands toointeract with Azure Storage resources.</span></span> <span data-ttu-id="f65c0-133">skrypt Hello najpierw tworzy nowy kontener na koncie magazynu, a następnie przekazuje istniejącego kontenera toothat pliku (jako obiektu blob).</span><span class="sxs-lookup"><span data-stu-id="f65c0-133">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container.</span></span> <span data-ttu-id="f65c0-134">Wyświetla listę wszystkich obiektów blob w kontenerze hello, a na koniec pobiera hello pliku tooa docelowego na komputerze lokalnym, który określisz.</span><span class="sxs-lookup"><span data-stu-id="f65c0-134">It then lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="f65c0-135">**Skonfiguruj i uruchom skrypt hello**</span><span class="sxs-lookup"><span data-stu-id="f65c0-135">**Configure and run hello script**</span></span>

1. <span data-ttu-id="f65c0-136">Otwórz w ulubionym edytorze tekstów, a następnie skopiuj i Wklej hello poprzedzających skrypt do edytora hello.</span><span class="sxs-lookup"><span data-stu-id="f65c0-136">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>

2. <span data-ttu-id="f65c0-137">Następnie zaktualizuj tooreflect zmienne skryptu hello ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f65c0-137">Next, update hello script's variables tooreflect your configuration settings.</span></span> <span data-ttu-id="f65c0-138">Zastąp następujące wartości określonych hello:</span><span class="sxs-lookup"><span data-stu-id="f65c0-138">Replace hello following values as specified:</span></span>

   * <span data-ttu-id="f65c0-139">**\<storage_account_name\>**  hello nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f65c0-139">**\<storage_account_name\>** hello name of your storage account.</span></span>
   * <span data-ttu-id="f65c0-140">**\<storage_account_key\>**  hello klucz podstawowy lub pomocniczy dostępu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f65c0-140">**\<storage_account_key\>** hello primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="f65c0-141">**\<container_name\>**  nazwę hello nowy kontener toocreate, takie jak "azure-cli — próbki container".</span><span class="sxs-lookup"><span data-stu-id="f65c0-141">**\<container_name\>** A name hello new container toocreate, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="f65c0-142">**\<blob_name\>**  nazwę hello docelowego obiektu blob w kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="f65c0-142">**\<blob_name\>** A name for hello destination blob in hello container.</span></span>
   * <span data-ttu-id="f65c0-143">**\<file_to_upload\>**  hello ścieżki pliku toosmall na komputerze lokalnym, takich jak "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="f65c0-143">**\<file_to_upload\>** hello path toosmall file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="f65c0-144">**\<destination_file\>**  hello ścieżkę pliku docelowego, takich jak "~ / downloadedImage.png".</span><span class="sxs-lookup"><span data-stu-id="f65c0-144">**\<destination_file\>** hello destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="f65c0-145">Po zaktualizowaniu zmienne niezbędne hello zapisać skrypt hello, a następnie zamknij Edytor.</span><span class="sxs-lookup"><span data-stu-id="f65c0-145">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="f65c0-146">Następne kroki Hello założono nazwanego skryptu **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="f65c0-146">hello next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="f65c0-147">Oznacz hello skrypt jako plik wykonywalny, w razie potrzeby:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="f65c0-147">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="f65c0-148">Uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="f65c0-148">Execute hello script.</span></span> <span data-ttu-id="f65c0-149">Na przykład w Bash:`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="f65c0-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="f65c0-150">Należy znaleźć dane wyjściowe podobne toohello w następujących tematach i hello  **\<destination_file\>**  określone w hello skryptu powinny pojawiać się na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="f65c0-150">You should see output similar toohello following, and hello **\<destination_file\>** you specified in hello script should appear on your local computer.</span></span>

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="f65c0-151">Witaj Powyższy wynik znajduje się w **tabeli** format.</span><span class="sxs-lookup"><span data-stu-id="f65c0-151">hello preceding output is in **table** format.</span></span> <span data-ttu-id="f65c0-152">Można określić wyjściowy, który format toouse określając hello `--output` argument w poleceniach interfejsu wiersza polecenia lub ustaw ją za pomocą `az configure`.</span><span class="sxs-lookup"><span data-stu-id="f65c0-152">You can specify which output format toouse by specifying hello `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="f65c0-153">Zarządzanie kontami magazynu</span><span class="sxs-lookup"><span data-stu-id="f65c0-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="f65c0-154">Utwórz nowe konto magazynu</span><span class="sxs-lookup"><span data-stu-id="f65c0-154">Create a new storage account</span></span>
<span data-ttu-id="f65c0-155">toouse magazynu Azure, musisz mieć konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="f65c0-155">toouse Azure Storage, you need a storage account.</span></span> <span data-ttu-id="f65c0-156">Można utworzyć nowe konto magazynu Azure, po skonfigurowaniu komputera za[połączenia subskrypcji tooyour](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="f65c0-156">You can create a new Azure Storage account after you've configured your computer too[connect tooyour subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="f65c0-157">`--location`[Wymagane]: lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="f65c0-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="f65c0-158">Na przykład "zachodnie stany USA".</span><span class="sxs-lookup"><span data-stu-id="f65c0-158">For example, "West US".</span></span>
* <span data-ttu-id="f65c0-159">`--name`[Wymagane]: Nazwa konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="f65c0-159">`--name` [Required]: hello storage account name.</span></span> <span data-ttu-id="f65c0-160">Witaj nazwa musi składać się z 3 znaków too24 i używaj tylko małych znaków alfanumerycznych.</span><span class="sxs-lookup"><span data-stu-id="f65c0-160">hello name must be 3 too24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="f65c0-161">`--resource-group`[Wymagane]: Nazwa grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="f65c0-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="f65c0-162">`--sku`[Wymagane]: hello konta magazynu wersji.</span><span class="sxs-lookup"><span data-stu-id="f65c0-162">`--sku` [Required]: hello storage account SKU.</span></span> <span data-ttu-id="f65c0-163">Dozwolone wartości:</span><span class="sxs-lookup"><span data-stu-id="f65c0-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="f65c0-164">Ustaw zmienne środowiskowe domyślne konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="f65c0-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="f65c0-165">Może mieć wielu kont magazynu w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f65c0-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="f65c0-166">tooselect jeden z nich polecenia toouse dla wszystkich kolejnych magazynu, można ustawić zmienne środowiskowe:</span><span class="sxs-lookup"><span data-stu-id="f65c0-166">tooselect one of them toouse for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="f65c0-167">Inny sposób tooset domyślne konto magazynu jest przy użyciu ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="f65c0-167">Another way tooset a default storage account is by using a connection string.</span></span> <span data-ttu-id="f65c0-168">Najpierw pobierz hello ciągu połączenia za pomocą hello `show-connection-string` polecenia:</span><span class="sxs-lookup"><span data-stu-id="f65c0-168">First, get hello connection string with hello `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="f65c0-169">Następnie hello kopiowania danych wyjściowych ciąg połączenia i ustaw hello `AZURE_STORAGE_CONNECTION_STRING` zmiennej środowiskowej (może być konieczne w cudzysłów ciągu połączenia hello tooenclose):</span><span class="sxs-lookup"><span data-stu-id="f65c0-169">Then copy hello output connection string and set hello `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need tooenclose hello connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="f65c0-170">Wszystkie przykłady w hello następujące sekcje w tym artykule założono, że ustawiono hello `AZURE_STORAGE_ACCOUNT` i `AZURE_STORAGE_ACCESS_KEY` zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="f65c0-170">All examples in hello following sections of this article assume that you've set hello `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="f65c0-171">Tworzenie i zarządzanie nimi obiektów blob</span><span class="sxs-lookup"><span data-stu-id="f65c0-171">Create and manage blobs</span></span>
<span data-ttu-id="f65c0-172">Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, takich jak dane tekstowe lub binarne, który można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f65c0-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="f65c0-173">W tej sekcji założono, że znasz już pojęcia dotyczące magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f65c0-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="f65c0-174">Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../blobs/storage-dotnet-how-to-use-blobs.md) i [pojęcia dotyczące usługi Blob](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="f65c0-174">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="f65c0-175">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="f65c0-175">Create a container</span></span>
<span data-ttu-id="f65c0-176">Każdy obiekt blob w magazynie Azure musi być w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="f65c0-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="f65c0-177">Kontener można utworzyć przy użyciu hello `az storage container create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="f65c0-177">You can create a container by using hello `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="f65c0-178">Można ustawić jedną z trzech poziomów dostępu do odczytu dla nowego kontenera, określając hello opcjonalne `--public-access` argumentu:</span><span class="sxs-lookup"><span data-stu-id="f65c0-178">You can set one of three levels of read access for a new container by specifying hello optional  `--public-access` argument:</span></span>

* <span data-ttu-id="f65c0-179">`off`(domyślnie): dane w kontenerze są prywatne toohello właściciela konta.</span><span class="sxs-lookup"><span data-stu-id="f65c0-179">`off` (default): Container data is private toohello account owner.</span></span>
* <span data-ttu-id="f65c0-180">`blob`: Publiczny dostęp do odczytu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f65c0-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="f65c0-181">`container`: Odczyt publiczny i listy dostępu toohello całego kontenera.</span><span class="sxs-lookup"><span data-stu-id="f65c0-181">`container`: Public read and list access toohello entire container.</span></span>

<span data-ttu-id="f65c0-182">Aby uzyskać więcej informacji, zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f65c0-182">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-tooa-container"></a><span data-ttu-id="f65c0-183">Przekaż tooa kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="f65c0-183">Upload a blob tooa container</span></span>
<span data-ttu-id="f65c0-184">Azure Blob storage obsługuje blok, Dołącz i stronicowe.</span><span class="sxs-lookup"><span data-stu-id="f65c0-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="f65c0-185">Przekazywanie obiektów blob kontenera tooa przy użyciu hello `blob upload` polecenia:</span><span class="sxs-lookup"><span data-stu-id="f65c0-185">Upload blobs tooa container by using hello `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="f65c0-186">Domyślnie program hello `blob upload` polecenia przekazuje obiekty BLOB toopage pliki *.vhd lub blokowych obiektów blob w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="f65c0-186">By default, hello `blob upload` command uploads *.vhd files toopage blobs, or block blobs otherwise.</span></span> <span data-ttu-id="f65c0-187">toospecify innego typu kiedy przekazywanie obiektu blob, możesz użyć hello `--type` argumentu--dozwolone wartości są `append`, `block`, i `page`.</span><span class="sxs-lookup"><span data-stu-id="f65c0-187">toospecify another type when you upload a blob, you can use hello `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="f65c0-188">Aby uzyskać więcej informacji o typach inny obiektu blob hello, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="f65c0-188">For more information on hello different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="f65c0-189">Pobieranie obiektu blob z kontenera</span><span class="sxs-lookup"><span data-stu-id="f65c0-189">Download a blob from a container</span></span>
<span data-ttu-id="f65c0-190">W tym przykładzie pokazano, jak toodownload obiektu blob z kontenera:</span><span class="sxs-lookup"><span data-stu-id="f65c0-190">This example demonstrates how toodownload a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="f65c0-191">Lista hello BLOB w kontenerze</span><span class="sxs-lookup"><span data-stu-id="f65c0-191">List hello blobs in a container</span></span>

<span data-ttu-id="f65c0-192">Wyświetlanie obiektów blob hello w kontenerze o hello [az magazynu obiektów blob listy](/cli/azure/storage/blob#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="f65c0-192">List hello blobs in a container with hello [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="f65c0-193">Kopiowanie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="f65c0-193">Copy blobs</span></span>
<span data-ttu-id="f65c0-194">Można asynchronicznie kopiować obiekty blob w obrębie konta magazynu i regionu lub między różnymi kontami magazynu i regionami.</span><span class="sxs-lookup"><span data-stu-id="f65c0-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="f65c0-195">Witaj poniższym przykładzie pokazano, jak obiekty BLOB toocopy z jednego magazynu konta tooanother.</span><span class="sxs-lookup"><span data-stu-id="f65c0-195">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="f65c0-196">Najpierw utworzymy kontenera na koncie magazynu źródłowego hello, określając publiczny dostęp do odczytu do jego obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f65c0-196">We first create a container in hello source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="f65c0-197">Następnie możemy przekazać kontenera toohello plików, a na końcu obiektu blob hello kopiowania z tego kontenera do kontenera na koncie magazynu docelowego hello.</span><span class="sxs-lookup"><span data-stu-id="f65c0-197">Next, we upload a file toohello container, and finally, copy hello blob from that container into a container in hello destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="f65c0-198">W hello powyżej przykładzie hello docelowy kontener musi już istnieć w hello konto magazynu docelowego dla toosucceed operacji kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="f65c0-198">In hello above example, hello destination container must already exist in hello destination storage account for hello copy operation toosucceed.</span></span> <span data-ttu-id="f65c0-199">Ponadto hello źródłowego obiektu blob określone w hello `--source-uri` argument musi zawierać token sygnatury dostępu Współdzielonego dostępu współdzielonego, albo być dostępny publicznie, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="f65c0-199">Additionally, hello source blob specified in hello `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="f65c0-200">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="f65c0-200">Delete a blob</span></span>
<span data-ttu-id="f65c0-201">toodelete obiektu blob, użyj hello `blob delete` polecenia:</span><span class="sxs-lookup"><span data-stu-id="f65c0-201">toodelete a blob, use hello `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="f65c0-202">Tworzenie i Zarządzanie udziałami plików</span><span class="sxs-lookup"><span data-stu-id="f65c0-202">Create and manage file shares</span></span>
<span data-ttu-id="f65c0-203">Magazyn plików Azure oferuje współużytkowany magazyn dla aplikacji używających protokołu bloku komunikatów serwera (SMB) hello.</span><span class="sxs-lookup"><span data-stu-id="f65c0-203">Azure File storage offers shared storage for applications using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="f65c0-204">Maszyny wirtualne Microsoft Azure i usługi w chmurze, a także aplikacje lokalne mogą udostępniać dane za pośrednictwem zainstalowanych udziałów.</span><span class="sxs-lookup"><span data-stu-id="f65c0-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="f65c0-205">Możesz zarządzać udziałami plików i danych plików za pośrednictwem hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f65c0-205">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="f65c0-206">Aby uzyskać więcej informacji dotyczących usługi Magazyn plików Azure, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../storage-dotnet-how-to-use-files.md) lub [jak toouse magazyn plików Azure z systemem Linux](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f65c0-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="f65c0-207">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="f65c0-207">Create a file share</span></span>
<span data-ttu-id="f65c0-208">Udział plików Azure jest udziałem plików SMB na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f65c0-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="f65c0-209">Wszystkie pliki i katalogi, należy utworzyć w udziale plików.</span><span class="sxs-lookup"><span data-stu-id="f65c0-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="f65c0-210">Konto może zawierać nieograniczoną liczbę udziałów, a udział może przechowywać nieograniczoną liczbę plików w górę toohello limity pojemności konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="f65c0-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="f65c0-211">Witaj poniższy przykład tworzy udział plików o nazwie **moj_udzial**.</span><span class="sxs-lookup"><span data-stu-id="f65c0-211">hello following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="f65c0-212">Tworzenie katalogu</span><span class="sxs-lookup"><span data-stu-id="f65c0-212">Create a directory</span></span>
<span data-ttu-id="f65c0-213">Katalog udostępnia strukturę hierarchiczną w udziale plików na platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="f65c0-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="f65c0-214">Witaj poniższy przykład tworzy katalog o nazwie **myDir** w hello udziału plików.</span><span class="sxs-lookup"><span data-stu-id="f65c0-214">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="f65c0-215">Ścieżki katalogu może zawierać wiele poziomów, na przykład **katalog1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="f65c0-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="f65c0-216">Należy jednak upewnij się, że wszystkie katalogi nadrzędne istnieć przed utworzeniem podkatalogu.</span><span class="sxs-lookup"><span data-stu-id="f65c0-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="f65c0-217">Na przykład dla ścieżki **katalog1/dir2**, należy najpierw utworzyć katalog **katalog1**, następnie utwórz katalog **dir2**.</span><span class="sxs-lookup"><span data-stu-id="f65c0-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-tooa-share"></a><span data-ttu-id="f65c0-218">Przekaż udziału tooa pliku lokalnego</span><span class="sxs-lookup"><span data-stu-id="f65c0-218">Upload a local file tooa share</span></span>
<span data-ttu-id="f65c0-219">Witaj poniższym przykładzie plik zostanie przekazany z **~/temp/samplefile.txt** tooroot hello **moj_udzial** udziału plików.</span><span class="sxs-lookup"><span data-stu-id="f65c0-219">hello following example uploads a file from **~/temp/samplefile.txt** tooroot of hello **myshare** file share.</span></span> <span data-ttu-id="f65c0-220">Witaj `--source` argument określa hello istniejących tooupload pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f65c0-220">hello `--source` argument specifies hello existing local file tooupload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="f65c0-221">Podobnie jak w przypadku tworzenia katalogu, można określić ścieżkę katalogu w ramach hello udziału tooupload hello tooan istniejącego katalogu pliku w udziale hello:</span><span class="sxs-lookup"><span data-stu-id="f65c0-221">As with directory creation, you can specify a directory path within hello share tooupload hello file tooan existing directory within hello share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="f65c0-222">Plik w udziale hello można się too1 TB rozmiar.</span><span class="sxs-lookup"><span data-stu-id="f65c0-222">A file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-a-share"></a><span data-ttu-id="f65c0-223">Wyświetlanie listy plików hello w udziale</span><span class="sxs-lookup"><span data-stu-id="f65c0-223">List hello files in a share</span></span>
<span data-ttu-id="f65c0-224">Można wyświetlić listę plików i katalogów w udziale, za pomocą hello `az storage file list` polecenia:</span><span class="sxs-lookup"><span data-stu-id="f65c0-224">You can list files and directories in a share by using hello `az storage file list` command:</span></span>

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="f65c0-225">Kopiowanie plików</span><span class="sxs-lookup"><span data-stu-id="f65c0-225">Copy files</span></span>      
<span data-ttu-id="f65c0-226">Można skopiować pliku tooanother, obiektu blob tooa pliku lub pliku tooa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f65c0-226">You can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="f65c0-227">Na przykład toocopy katalogu tooa plików w różnych udziału:</span><span class="sxs-lookup"><span data-stu-id="f65c0-227">For example, toocopy a file tooa directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="f65c0-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f65c0-228">Next steps</span></span>
<span data-ttu-id="f65c0-229">Poniżej przedstawiono dodatkowe zasoby dowiedzieć się więcej o pracy z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f65c0-229">Here are some additional resources for learning more about working with hello Azure CLI 2.0.</span></span>

* [<span data-ttu-id="f65c0-230">Wprowadzenie do usługi Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f65c0-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="f65c0-231">Dokumentacja poleceń interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f65c0-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="f65c0-232">Azure CLI 2.0 w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="f65c0-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
