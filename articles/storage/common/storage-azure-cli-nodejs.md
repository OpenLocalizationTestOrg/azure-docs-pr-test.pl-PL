---
title: "Witaj aaaUsing 1.0 interfejsu wiersza polecenia platformy Azure z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello interfejsu wiersza polecenia platformy Azure (Azure CLI) 1.0, z toocreate magazynu Azure i zarządzać kontami magazynu i pracować z plikami i obiekty BLOB platformy Azure. Hello Azure CLI jest narzędziem do wielu platform"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 25e459403dde631741403c8722ed07beafac35c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a><span data-ttu-id="f1b67-104">Przy użyciu hello Azure CLI 1.0 z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f1b67-104">Using hello Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="f1b67-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f1b67-105">Overview</span></span>

<span data-ttu-id="f1b67-106">Hello wiersza polecenia platformy Azure oferuje zestaw typu open source, obsługujący wiele platform polecenia dotyczące pracy z hello platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b67-106">hello Azure CLI provides a set of open source, cross-platform commands for working with hello Azure Platform.</span></span> <span data-ttu-id="f1b67-107">Zapewnia znacznie hello tę samą funkcjonalność znalezione w hello [portalu Azure](https://portal.azure.com) danych oraz jak sformatowanego dostęp do funkcji.</span><span class="sxs-lookup"><span data-stu-id="f1b67-107">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="f1b67-108">W tym przewodniku, firma Microsoft będzie Eksploruj jak toouse [interfejsu wiersza polecenia platformy Azure (Azure CLI)](../../cli-install-nodejs.md) tooperform różnych zadań programowania i administracji z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f1b67-108">In this guide, we'll explore how toouse [Azure Command-Line Interface (Azure CLI)](../../cli-install-nodejs.md) tooperform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="f1b67-109">Zalecamy, aby pobrać i zainstalować lub uaktualnić toohello najnowsze wiersza polecenia platformy Azure, przed rozpoczęciem korzystania z tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="f1b67-109">We recommend that you download and install or upgrade toohello latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="f1b67-110">W tym przewodniku założono, że rozumiesz hello podstawowych pojęciach dotyczących usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f1b67-110">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="f1b67-111">Przewodnik Hello zawiera liczby skryptów toodemonstrate użycie hello hello wiersza polecenia platformy Azure z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f1b67-111">hello guide provides a number of scripts toodemonstrate hello usage of hello Azure CLI with Azure Storage.</span></span> <span data-ttu-id="f1b67-112">Należy się tooupdate hello zmienne skryptu na podstawie konfiguracji przed uruchomieniem każdego skryptu.</span><span class="sxs-lookup"><span data-stu-id="f1b67-112">Be sure tooupdate hello script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="f1b67-113">Przewodnik Hello przedstawiono przykłady poleceń i skryptów wiersza polecenia platformy Azure hello klasycznych kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="f1b67-113">hello guide provides hello Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="f1b67-114">Zobacz [hello Using Azure CLI for Mac, Linux i Windows z usługą Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) dla polecenia wiersza polecenia platformy Azure dla Menedżera zasobów konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f1b67-114">See [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a><span data-ttu-id="f1b67-115">Wprowadzenie do usługi Azure Storage i hello wiersza polecenia platformy Azure w ciągu 5 minut</span><span class="sxs-lookup"><span data-stu-id="f1b67-115">Get started with Azure Storage and hello Azure CLI in 5 minutes</span></span>
<span data-ttu-id="f1b67-116">W tym przewodniku używa Ubuntu przykłady, ale innych platform systemu operacyjnego należy wykonać w podobny sposób.</span><span class="sxs-lookup"><span data-stu-id="f1b67-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="f1b67-117">**Nowe tooAzure:** subskrypcji Microsoft Azure i konta Microsoft skojarzonego z jego subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="f1b67-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="f1b67-118">Aby uzyskać informacje na temat opcji zakupu platformy Azure, zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/), [opcjami zakupu](https://azure.microsoft.com/pricing/purchase-options/), i [oferty Członkowskie](https://azure.microsoft.com/pricing/member-offers/) (dla członków MSDN, Microsoft Partner Network, BizSpark i innych programów firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="f1b67-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="f1b67-119">Zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) uzyskać więcej informacji o subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b67-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="f1b67-120">**Po utworzeniu subskrypcji Microsoft Azure i konto:**</span><span class="sxs-lookup"><span data-stu-id="f1b67-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="f1b67-121">Pobierz i zainstaluj hello wiersza polecenia platformy Azure, postępując zgodnie z instrukcjami hello opisane w [hello instalowanie interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f1b67-121">Download and install hello Azure CLI following hello instructions outlined in [Install hello Azure CLI](../../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="f1b67-122">Po hello wiersza polecenia platformy Azure został zainstalowany, będzie możliwe toouse hello azure polecenie z poleceń Azure CLI hello tooaccess interfejsu wiersza polecenia (Bash, terminali, wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="f1b67-122">Once hello Azure CLI has been installed, you will be able toouse hello azure command from your command-line interface (Bash, Terminal, Command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="f1b67-123">Typ hello _azure_ polecenia i powinna zostać wyświetlona hello następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="f1b67-123">Type hello _azure_ command and you should see hello following output.</span></span>

    ![Dane wyjściowe polecenia platformy Azure](./media/storage-azure-cli/azure_command.png)   
3. <span data-ttu-id="f1b67-125">W hello interfejsu wiersza polecenia, wpisz `azure storage` toolist całe hello polecenia magazynu azure i uzyskać pierwszy wrażenie Witaj Witaj funkcje interfejsu wiersza polecenia Azure udostępnia.</span><span class="sxs-lookup"><span data-stu-id="f1b67-125">In hello command-line interface, type `azure storage` toolist out all hello azure storage commands and get a first impression of hello functionalities hello Azure CLI provides.</span></span> <span data-ttu-id="f1b67-126">Możesz wpisać nazwę polecenia z **-h** parametru (na przykład `azure storage share create -h`) toosee szczegóły składni polecenia.</span><span class="sxs-lookup"><span data-stu-id="f1b67-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) toosee details of command syntax.</span></span>
4. <span data-ttu-id="f1b67-127">Teraz przedstawimy prosty skrypt, który zawiera podstawowe tooaccess polecenia interfejsu wiersza polecenia Azure usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f1b67-127">Now, we'll give you a simple script that shows basic Azure CLI commands tooaccess Azure Storage.</span></span> <span data-ttu-id="f1b67-128">skrypt Hello najpierw zapyta tooset dwie zmienne dla konta magazynu i klucza.</span><span class="sxs-lookup"><span data-stu-id="f1b67-128">hello script will first ask you tooset two variables for your storage account and key.</span></span> <span data-ttu-id="f1b67-129">Następnie skryptu hello utworzyć nowy kontener w tym nowe konto magazynu i przekaż istniejącego kontenera toothat obrazu pliku (blob).</span><span class="sxs-lookup"><span data-stu-id="f1b67-129">Then, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="f1b67-130">Po skryptu hello znajduje się lista wszystkich obiektów blob w tym kontenerze, pobierze hello obrazu pliku toohello katalog docelowy która istnieje na komputerze lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="f1b67-130">After hello script lists all blobs in that container, it will download hello image file toohello destination directory which exists on hello local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="f1b67-131">W komputerze lokalnym Otwórz w edytorze tekstów preferowanych (vim na przykład).</span><span class="sxs-lookup"><span data-stu-id="f1b67-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="f1b67-132">Typ hello powyżej skrypt do edytora tekstu.</span><span class="sxs-lookup"><span data-stu-id="f1b67-132">Type hello above script into your text editor.</span></span>
6. <span data-ttu-id="f1b67-133">Teraz należy zmienne skryptu hello tooupdate na podstawie własnych ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f1b67-133">Now, you need tooupdate hello script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="f1b67-134">**< Storage_account_name >** Użyj hello otrzymuje nazwę w skrypcie hello, lub wprowadź nową nazwę dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f1b67-134">**<storage_account_name>** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="f1b67-135">**Ważne:** hello nazwa konta magazynu hello musi być unikatowa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b67-135">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="f1b67-136">Musi być pisane małymi literami, zbyt!</span><span class="sxs-lookup"><span data-stu-id="f1b67-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="f1b67-137">**< storage_account_key >** hello klucz dostępu konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f1b67-137">**<storage_account_key>** hello access key of your storage account.</span></span>
   * <span data-ttu-id="f1b67-138">**< Container_name >** Użyj hello otrzymuje nazwę w skrypcie hello lub wprowadź nową nazwę dla Twojego kontenera.</span><span class="sxs-lookup"><span data-stu-id="f1b67-138">**<container_name>** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="f1b67-139">**< Image_to_upload >** wprowadź obraz tooa ścieżkę na komputerze lokalnym, na przykład: "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="f1b67-139">**<image_to_upload>** Enter a path tooa picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="f1b67-140">**< Destination_folder >** wprowadź ścieżkę tooa katalogu lokalnego toostore pliki pobierane z usługi Magazyn Azure, takich jak: "~/downloadImages".</span><span class="sxs-lookup"><span data-stu-id="f1b67-140">**<destination_folder>** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="f1b67-141">Po zaktualizowaniu hello niezbędne zmiennych w vim naciśnij kombinacje klawiszy `ESC`, `:`, `wq!` toosave hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="f1b67-141">After you've updated hello necessary variables in vim, press key combinations `ESC`, `:`, `wq!` toosave hello script.</span></span>
8. <span data-ttu-id="f1b67-142">toorun ten skrypt, po prostu typu hello nazwę pliku skryptu w konsoli bash hello.</span><span class="sxs-lookup"><span data-stu-id="f1b67-142">toorun this script, simply type hello script file name in hello bash console.</span></span> <span data-ttu-id="f1b67-143">Po uruchomieniu tego skryptu, ma lokalne miejsce docelowe folder, który zawiera hello pobrany plik obrazu.</span><span class="sxs-lookup"><span data-stu-id="f1b67-143">After this script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="f1b67-144">powitania po zrzut ekranu przedstawia przykład danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="f1b67-144">hello following screenshot shows an example output:</span></span>

<span data-ttu-id="f1b67-145">Po uruchomieniu skryptu hello powinien mieć folderu lokalne miejsce docelowe, który zawiera hello pobrany plik obrazu.</span><span class="sxs-lookup"><span data-stu-id="f1b67-145">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-hello-azure-cli"></a><span data-ttu-id="f1b67-146">Zarządzanie kontami magazynu z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f1b67-146">Manage storage accounts with hello Azure CLI</span></span>
### <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="f1b67-147">Połącz tooyour subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f1b67-147">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="f1b67-148">Większość poleceń magazynu hello będzie działać bez subskrypcji platformy Azure, ale zalecamy tooconnect tooyour subskrypcji z hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b67-148">While most of hello storage commands will work without an Azure subscription, we recommend you tooconnect tooyour subscription from hello Azure CLI.</span></span> <span data-ttu-id="f1b67-149">tooconfigure hello Azure CLI toowork w ramach subskrypcji, wykonaj kroki hello w [połączyć tooan subskrypcji platformy Azure z hello Azure CLI](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f1b67-149">tooconfigure hello Azure CLI toowork with your subscription, follow hello steps in [Connect tooan Azure subscription from hello Azure CLI](../../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="f1b67-150">Utwórz nowe konto magazynu</span><span class="sxs-lookup"><span data-stu-id="f1b67-150">Create a new storage account</span></span>
<span data-ttu-id="f1b67-151">toouse magazynu Azure, konieczne będzie konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="f1b67-151">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="f1b67-152">Po skonfigurowaniu subskrypcji tooyour tooconnect komputera, można utworzyć nowe konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b67-152">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="f1b67-153">Nazwa Hello konta magazynu musi mieć od 3 do 24 znaków i korzystać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="f1b67-153">hello name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="f1b67-154">Ustaw domyślnego konta magazynu Azure w zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="f1b67-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="f1b67-155">Może mieć wielu kont magazynu w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f1b67-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="f1b67-156">Można wybrać jedną z nich i ustaw go w hello zmiennych środowiskowych dla wszystkich magazynu hello polecenia w hello sam sesji.</span><span class="sxs-lookup"><span data-stu-id="f1b67-156">You can choose one of them and set it in hello environment variables for all hello storage commands in hello same session.</span></span> <span data-ttu-id="f1b67-157">Dzięki temu toorun hello Azure CLI magazynu polecenia bez określania magazynu hello konta i klucz jawnie.</span><span class="sxs-lookup"><span data-stu-id="f1b67-157">This enables you toorun hello Azure CLI storage commands without specifying hello storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="f1b67-158">Inny sposób tooset domyślne konto magazynu jest przy użyciu parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="f1b67-158">Another way tooset a default storage account is using connection string.</span></span> <span data-ttu-id="f1b67-159">Po pierwsze uzyskać hello parametry połączenia za pomocą polecenia:</span><span class="sxs-lookup"><span data-stu-id="f1b67-159">Firstly get hello connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="f1b67-160">Następnie skopiuj parametry połączenia danych wyjściowych hello i ustaw zmienną tooenvironment:</span><span class="sxs-lookup"><span data-stu-id="f1b67-160">Then copy hello output connection string and set it tooenvironment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="f1b67-161">Tworzenie i zarządzanie nimi obiektów blob</span><span class="sxs-lookup"><span data-stu-id="f1b67-161">Create and manage blobs</span></span>
<span data-ttu-id="f1b67-162">Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, takich jak dane tekstowe lub binarne, który można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f1b67-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="f1b67-163">W tej sekcji założono, że znasz już pojęcia dotyczące magazynu obiektów Blob platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f1b67-163">This section assumes that you are already familiar with hello Azure Blob storage concepts.</span></span> <span data-ttu-id="f1b67-164">Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../blobs/storage-dotnet-how-to-use-blobs.md) i [pojęcia dotyczące usługi Blob](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1b67-164">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="f1b67-165">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="f1b67-165">Create a container</span></span>
<span data-ttu-id="f1b67-166">Każdy obiekt blob w magazynie Azure musi być w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="f1b67-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="f1b67-167">Możesz utworzyć kontener prywatnego przy użyciu hello `azure storage container create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="f1b67-167">You can create a private container using hello `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="f1b67-168">Istnieją trzy poziomy anonimowy dostęp do odczytu: **poza**, **obiektu Blob**, i **kontenera**.</span><span class="sxs-lookup"><span data-stu-id="f1b67-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="f1b67-169">tooprevent anonimowego dostępu zbyt tooblobs, parametr uprawnienia hello zestawu**poza**.</span><span class="sxs-lookup"><span data-stu-id="f1b67-169">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="f1b67-170">Domyślnie nowy kontener hello jest prywatny i jest możliwy tylko przez właściciela konta hello.</span><span class="sxs-lookup"><span data-stu-id="f1b67-170">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="f1b67-171">odczytu tooallow publicznego anonimowy dostęp do zasobów tooblob, ale nie toocontainer metadanych lub toohello listę obiektów blob w kontenerze hello, ustaw parametr uprawnienia hello zbyt**obiektu Blob**.</span><span class="sxs-lookup"><span data-stu-id="f1b67-171">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="f1b67-172">tooallow publicznego Pełny odczyt dostęp do zasobów tooblob metadanych kontenera i hello listę obiektów blob w kontenerze hello, ustaw parametr uprawnienia hello zbyt**kontenera**.</span><span class="sxs-lookup"><span data-stu-id="f1b67-172">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="f1b67-173">Aby uzyskać więcej informacji, zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f1b67-173">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="f1b67-174">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="f1b67-174">Upload a blob into a container</span></span>
<span data-ttu-id="f1b67-175">Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="f1b67-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="f1b67-176">Aby uzyskać więcej informacji, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1b67-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="f1b67-177">tooupload obiekty BLOB w kontenerze tooa, można użyć hello `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="f1b67-177">tooupload blobs in tooa container, you can use hello `azure storage blob upload`.</span></span> <span data-ttu-id="f1b67-178">Domyślnie to polecenie wysyła hello lokalne pliki tooa — obiekt blob blokowy.</span><span class="sxs-lookup"><span data-stu-id="f1b67-178">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="f1b67-179">Typ hello toospecify hello obiektu blob, można użyć hello `--blobtype` parametru.</span><span class="sxs-lookup"><span data-stu-id="f1b67-179">toospecify hello type for hello blob, you can use hello `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="f1b67-180">Pobierać obiekty BLOB z kontenera</span><span class="sxs-lookup"><span data-stu-id="f1b67-180">Download blobs from a container</span></span>
<span data-ttu-id="f1b67-181">Witaj poniższy przykład pokazuje, jak toodownload obiektów blob z kontenera.</span><span class="sxs-lookup"><span data-stu-id="f1b67-181">hello following example demonstrates how toodownload blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="f1b67-182">Kopiowanie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="f1b67-182">Copy blobs</span></span>
<span data-ttu-id="f1b67-183">Można asynchronicznie kopiować obiekty blob w obrębie konta magazynu i regionu lub między różnymi kontami magazynu i regionami.</span><span class="sxs-lookup"><span data-stu-id="f1b67-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="f1b67-184">Witaj poniższym przykładzie pokazano, jak obiekty BLOB toocopy z jednego magazynu konta tooanother.</span><span class="sxs-lookup"><span data-stu-id="f1b67-184">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="f1b67-185">W tym przykładzie tworzymy kontenera, w których obiekty BLOB są publicznie, anonimowo dostępny.</span><span class="sxs-lookup"><span data-stu-id="f1b67-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="f1b67-186">W tym przykładzie wykonuje asynchroniczne kopiowania.</span><span class="sxs-lookup"><span data-stu-id="f1b67-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="f1b67-187">Możesz monitorować stan hello każdej operacji kopiowania, uruchamiając hello `azure storage blob copy show` operacji.</span><span class="sxs-lookup"><span data-stu-id="f1b67-187">You can monitor hello status of each copy operation by running hello `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="f1b67-188">Należy pamiętać, że hello źródłowy adres URL podany dla operacji kopiowania hello musi być dostępny publicznie albo obejmuje tokenu sygnatury dostępu Współdzielonego (sygnatury dostępu współdzielonego).</span><span class="sxs-lookup"><span data-stu-id="f1b67-188">Note that hello source URL provided for hello copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="f1b67-189">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="f1b67-189">Delete a blob</span></span>
<span data-ttu-id="f1b67-190">toodelete obiektu blob, użyj hello poniżej polecenia:</span><span class="sxs-lookup"><span data-stu-id="f1b67-190">toodelete a blob, use hello below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="f1b67-191">Tworzenie i Zarządzanie udziałami plików</span><span class="sxs-lookup"><span data-stu-id="f1b67-191">Create and manage file shares</span></span>
<span data-ttu-id="f1b67-192">Magazyn plików Azure oferuje współużytkowany magazyn dla aplikacji używających standardowego protokołu SMB hello.</span><span class="sxs-lookup"><span data-stu-id="f1b67-192">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="f1b67-193">Maszyny wirtualne Microsoft Azure i usługi w chmurze, a także aplikacje lokalne mogą udostępniać dane za pośrednictwem zainstalowanych udziałów.</span><span class="sxs-lookup"><span data-stu-id="f1b67-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="f1b67-194">Możesz zarządzać udziałami plików i danych plików za pośrednictwem hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f1b67-194">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="f1b67-195">Aby uzyskać więcej informacji dotyczących usługi Magazyn plików Azure, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../storage-dotnet-how-to-use-files.md) lub [jak toouse magazyn plików Azure z systemem Linux](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f1b67-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="f1b67-196">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="f1b67-196">Create a file share</span></span>
<span data-ttu-id="f1b67-197">Udział plików Azure jest udziałem plików SMB na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b67-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="f1b67-198">Wszystkie pliki i katalogi, należy utworzyć w udziale plików.</span><span class="sxs-lookup"><span data-stu-id="f1b67-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="f1b67-199">Konto może zawierać nieograniczoną liczbę udziałów, a udział może przechowywać nieograniczoną liczbę plików w górę toohello limity pojemności konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="f1b67-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="f1b67-200">Witaj poniższy przykład tworzy udział plików o nazwie **moj_udzial**.</span><span class="sxs-lookup"><span data-stu-id="f1b67-200">hello following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="f1b67-201">Tworzenie katalogu</span><span class="sxs-lookup"><span data-stu-id="f1b67-201">Create a directory</span></span>
<span data-ttu-id="f1b67-202">Katalog udostępnia opcjonalne strukturę hierarchiczną do udziału plików na platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b67-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="f1b67-203">Witaj poniższy przykład tworzy katalog o nazwie **myDir** w hello udziału plików.</span><span class="sxs-lookup"><span data-stu-id="f1b67-203">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="f1b67-204">Należy pamiętać, że ścieżki katalogu może zawierać wiele poziomów *np.*, **/ b**.</span><span class="sxs-lookup"><span data-stu-id="f1b67-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="f1b67-205">Należy jednak upewnij się, że istnieją wszystkie katalogi nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="f1b67-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="f1b67-206">Na przykład dla ścieżki **/ b**, należy utworzyć katalog **** najpierw utwórz katalog **b**.</span><span class="sxs-lookup"><span data-stu-id="f1b67-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-toodirectory"></a><span data-ttu-id="f1b67-207">Przekaż toodirectory pliku lokalnego</span><span class="sxs-lookup"><span data-stu-id="f1b67-207">Upload a local file toodirectory</span></span>
<span data-ttu-id="f1b67-208">Witaj poniższym przykładzie plik zostanie przekazany z **~/temp/samplefile.txt** toohello **myDir** katalogu.</span><span class="sxs-lookup"><span data-stu-id="f1b67-208">hello following example uploads a file from **~/temp/samplefile.txt** toohello **myDir** directory.</span></span> <span data-ttu-id="f1b67-209">Edytuj hello ścieżkę pliku tak, aby wskazywało tooa prawidłowy plik na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="f1b67-209">Edit hello file path so that it points tooa valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="f1b67-210">Należy pamiętać, że plik w udziale hello może być zapasowej TB too1 rozmiar.</span><span class="sxs-lookup"><span data-stu-id="f1b67-210">Note that a file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-hello-share-root-or-directory"></a><span data-ttu-id="f1b67-211">Wyświetlanie listy plików hello w katalogu głównego udziału hello lub katalogu</span><span class="sxs-lookup"><span data-stu-id="f1b67-211">List hello files in hello share root or directory</span></span>
<span data-ttu-id="f1b67-212">Możesz wyświetlić listę hello pliki i podkatalogi w katalogu głównego udziału lub w katalogu przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f1b67-212">You can list hello files and subdirectories in a share root or a directory using hello following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="f1b67-213">Należy pamiętać, że podana nazwa katalogu hello jest opcjonalny w przypadku hello listę operacji.</span><span class="sxs-lookup"><span data-stu-id="f1b67-213">Note that hello directory name is optional for hello listing operation.</span></span> <span data-ttu-id="f1b67-214">Pominięcie hello polecenie wyświetla listę hello zawartość katalogu głównego hello hello udziału.</span><span class="sxs-lookup"><span data-stu-id="f1b67-214">If omitted, hello command lists hello contents of hello root directory of hello share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="f1b67-215">Kopiowanie plików</span><span class="sxs-lookup"><span data-stu-id="f1b67-215">Copy files</span></span>
<span data-ttu-id="f1b67-216">Począwszy od wersji 0.9.8 wiersza polecenia platformy Azure, można skopiować pliku tooanother, obiektu blob tooa pliku lub pliku tooa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f1b67-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="f1b67-217">Poniżej przedstawiamy, jak tooperform je skopiować operacji za pomocą polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f1b67-217">Below we demonstrate how tooperform these copy operations using CLI commands.</span></span> <span data-ttu-id="f1b67-218">toocopy nowy katalog toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="f1b67-218">toocopy a file toohello new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="f1b67-219">toocopy katalogu plików tooa obiektu blob:</span><span class="sxs-lookup"><span data-stu-id="f1b67-219">toocopy a blob tooa file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="f1b67-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f1b67-220">Next Steps</span></span>

<span data-ttu-id="f1b67-221">Dokumentacja poleceń Azure 1.0 interfejsu wiersza polecenia można znaleźć do pracy z zasobami magazynu w tym miejscu:</span><span class="sxs-lookup"><span data-stu-id="f1b67-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="f1b67-222">Azure polecenia interfejsu wiersza polecenia w trybie Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="f1b67-222">Azure CLI commands in Resource Manager mode</span></span>](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="f1b67-223">Azure polecenia interfejsu wiersza polecenia w trybie zarządzania usługami Azure</span><span class="sxs-lookup"><span data-stu-id="f1b67-223">Azure CLI commands in Azure Service Management mode</span></span>](../../cli-install-nodejs.md)

<span data-ttu-id="f1b67-224">Również chcesz tootry hello [Azure CLI 2.0](../storage-azure-cli.md), naszych CLI generacji napisane w języku Python, do użycia z modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="f1b67-224">You may also like tootry hello [Azure CLI 2.0](../storage-azure-cli.md), our next-generation CLI written in Python, for use with hello Resource Manager deployment model.</span></span>
