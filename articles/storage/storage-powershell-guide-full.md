---
title: "Używanie programu Azure PowerShell z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć i zarządzać kontami magazynu; przy użyciu poleceń cmdlet programu Azure PowerShell dla usługi Azure Storage Praca z obiektów blob, tabel, kolejek i plików. Konfigurowanie i zapytania analityka magazynu, a następnie utwórz sygnatur dostępu współdzielonego."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 51e3e93ebedd31370857e61a00139294bcee9237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="22a3f-103">Używanie programu Azure PowerShell z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="22a3f-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="22a3f-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="22a3f-104">Overview</span></span>
<span data-ttu-id="22a3f-105">Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet do zarządzania za pomocą środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a3f-105">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="22a3f-106">Jest to język skryptów i powłoka wiersza polecenia oparta na zadaniach zaprojektowana pod kątem administrowania systemem.</span><span class="sxs-lookup"><span data-stu-id="22a3f-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="22a3f-107">Przy użyciu programu PowerShell można łatwo kontrolować i automatyzować administrowanie Azure usługi i aplikacje.</span><span class="sxs-lookup"><span data-stu-id="22a3f-107">With PowerShell, you can easily control and automate the administration of your Azure services and applications.</span></span> <span data-ttu-id="22a3f-108">Na przykład służy poleceń cmdlet do wykonania tych samych czynności, które można wykonywać za pomocą [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22a3f-108">For example, you can use the cmdlets to perform the same tasks that you can perform through the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="22a3f-109">W tym przewodniku, możemy Eksploruj sposób użycia [polecenia cmdlet usługi Azure Storage](/powershell/module/azurerm.storage/#storage) do wykonywania różnych zadań programowania i administracji z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="22a3f-109">In this guide, we'll explore how to use the [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) to perform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="22a3f-110">W tym przewodniku założono, że przy użyciu doświadczenie [usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/) i [programu Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="22a3f-111">Przewodnik udostępnia wiele skryptów do zaprezentowania użycia programu PowerShell z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="22a3f-111">The guide provides a number of scripts to demonstrate the usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="22a3f-112">Należy zaktualizować zmienne skryptu na podstawie konfiguracji przed uruchomieniem każdego skryptu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-112">You should update the script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="22a3f-113">Pierwsza sekcja, w tym przewodniku zapewnia szybkiego dostępu w usłudze Azure Storage i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a3f-113">The first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="22a3f-114">Aby uzyskać szczegółowe informacje i instrukcje, Rozpocznij od [wymagań wstępnych dotyczących używania programu Azure PowerShell z usługą Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="22a3f-114">For detailed information and instructions, start from the [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="22a3f-115">Wprowadzenie do korzystania z usługi Azure Storage i programu PowerShell w ciągu 5 minut</span><span class="sxs-lookup"><span data-stu-id="22a3f-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="22a3f-116">W tej sekcji przedstawiono sposób uzyskać dostępu do usługi Azure Storage za pomocą programu PowerShell w ciągu 5 minut.</span><span class="sxs-lookup"><span data-stu-id="22a3f-116">This section shows you how to access Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="22a3f-117">**Jesteś nowym użytkownikiem usługi Azure:** subskrypcji Microsoft Azure i konta Microsoft skojarzonego z jego subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="22a3f-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="22a3f-118">Aby uzyskać informacje na temat opcji zakupu platformy Azure, zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/), [opcjami zakupu](https://azure.microsoft.com/pricing/purchase-options/), i [oferty Członkowskie](https://azure.microsoft.com/pricing/member-offers/) (dla członków MSDN, Microsoft Partner Network, BizSpark i innych programów firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="22a3f-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="22a3f-119">Zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) uzyskać więcej informacji o subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="22a3f-120">**Po utworzeniu subskrypcji Microsoft Azure i konto:**</span><span class="sxs-lookup"><span data-stu-id="22a3f-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="22a3f-121">Pobierz i zainstaluj najnowszą [programu Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="22a3f-121">Download and install the latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="22a3f-122">Start środowisko systemu Windows PowerShell zintegrowane skryptów (ISE): W komputerze lokalnym, przejdź do **Start** menu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go to the **Start** menu.</span></span> <span data-ttu-id="22a3f-123">Typ **narzędzia administracyjne** i kliknij go uruchomić.</span><span class="sxs-lookup"><span data-stu-id="22a3f-123">Type **Administrative Tools** and click to run it.</span></span> <span data-ttu-id="22a3f-124">W **narzędzia administracyjne** okna, kliknij prawym przyciskiem myszy **programu Windows PowerShell ISE**, kliknij przycisk **Uruchom jako Administrator**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-124">In the **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="22a3f-125">W **programu Windows PowerShell ISE**, kliknij przycisk **pliku** > **nowy** Aby utworzyć nowy plik skryptu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-125">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="22a3f-126">Teraz przedstawimy prostego skryptu, który pokazuje podstawowych poleceń programu PowerShell dostęp do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-126">Now, we'll give you a simple script that shows basic PowerShell commands to access Azure Storage.</span></span> <span data-ttu-id="22a3f-127">Skrypt najpierw poprosi Azure poświadczenia konta, aby dodać Azure konta lokalnego środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a3f-127">The script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment.</span></span> <span data-ttu-id="22a3f-128">Następnie skrypt ustawiania domyślnych subskrypcji platformy Azure i Utwórz nowe konto magazynu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-128">Then, the script will set the default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="22a3f-129">Następnie skrypt utworzyć nowy kontener w tym nowe konto magazynu i przekazać istniejący plik obrazu (blob) do tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="22a3f-129">Next, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="22a3f-130">Po skrypt znajduje się lista wszystkich obiektów blob w tym kontenerze, utworzy nowy katalog docelowy w komputerze lokalnym i pobranie pliku obrazu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-130">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>
5. <span data-ttu-id="22a3f-131">W poniższej sekcji kodu, wybierz skrypt między uwagi **#begin** i **#end**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-131">In the following code section, select the script between the remarks **#begin** and **#end**.</span></span> <span data-ttu-id="22a3f-132">Naciśnij klawisze CTRL + C, aby skopiować go do Schowka.</span><span class="sxs-lookup"><span data-stu-id="22a3f-132">Press CTRL+C to copy it to the clipboard.</span></span>

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from the container:
    # Get a reference to a list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create the destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into the local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="22a3f-133">W **programu Windows PowerShell ISE**, naciśnij klawisze CTRL + V, aby skopiować skrypt.</span><span class="sxs-lookup"><span data-stu-id="22a3f-133">In **Windows PowerShell ISE**, press CTRL+V to copy the script.</span></span> <span data-ttu-id="22a3f-134">Kliknij przycisk **pliku** > **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-134">Click **File** > **Save**.</span></span> <span data-ttu-id="22a3f-135">W **Zapisz jako** oknie dialogowym wpisz nazwę pliku skryptu, takie jak "mystoragescript."</span><span class="sxs-lookup"><span data-stu-id="22a3f-135">In the **Save As** dialog window, type the name of the script file, such as "mystoragescript."</span></span> <span data-ttu-id="22a3f-136">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-136">Click **Save**.</span></span>
7. <span data-ttu-id="22a3f-137">Teraz musisz zaktualizować zmienne skryptu na podstawie własnych ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-137">Now, you need to update the script variables based on your configuration settings.</span></span> <span data-ttu-id="22a3f-138">Należy zaktualizować **$SubscriptionName** zmiennej przy użyciu posiadanej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-138">You must update the **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="22a3f-139">Można zachować zmienne określone w skrypcie lub zaktualizuj je zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="22a3f-139">You can keep the other variables as specified in the script or update them as you wish.</span></span>
   
   * <span data-ttu-id="22a3f-140">**$SubscriptionName:** należy zaktualizować tę zmienną z własną nazwę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="22a3f-141">Wykonaj jedną z następujących trzech sposobów, aby zlokalizować nazwę Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="22a3f-141">Follow one of the following three ways to locate the name of your subscription:</span></span>
     
    <span data-ttu-id="22a3f-142">a.</span><span class="sxs-lookup"><span data-stu-id="22a3f-142">a.</span></span> <span data-ttu-id="22a3f-143">W **programu Windows PowerShell ISE**, kliknij przycisk **pliku** > **nowy** Aby utworzyć nowy plik skryptu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-143">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span> <span data-ttu-id="22a3f-144">Skopiuj poniższy skrypt do nowego pliku skryptu, a następnie kliknij przycisk **debugowania** > **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-144">Copy the following script to the new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="22a3f-145">Poniższy skrypt najpierw poprosi Azure poświadczenia konta, aby dodać Azure konta lokalnego środowiska PowerShell, a następnie wyświetlić wszystkie subskrypcje, które są podłączone do lokalnej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a3f-145">The following script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment and then show all the subscriptions that are connected to the local PowerShell session.</span></span> <span data-ttu-id="22a3f-146">Zanotuj nazwę subskrypcji, która ma być używany podczas korzystania z tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="22a3f-146">Take a note of the name of the subscription that you want to use while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="22a3f-147">b.</span><span class="sxs-lookup"><span data-stu-id="22a3f-147">b.</span></span> <span data-ttu-id="22a3f-148">Aby znaleźć i skopiować nazwę subskrypcji w [portalu Azure](https://portal.azure.com), w menu centralnym po lewej stronie kliknij **subskrypcje**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-148">To locate and copy your subscription name in the [Azure portal](https://portal.azure.com), in the Hub menu on the left, click **Subscriptions**.</span></span> <span data-ttu-id="22a3f-149">Skopiuj nazwę subskrypcji, która ma być używany podczas uruchamiania skryptów w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="22a3f-149">Copy the name of subscription that you want to use while running the scripts in this guide.</span></span>
     
     ![Azure Portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="22a3f-151">c.</span><span class="sxs-lookup"><span data-stu-id="22a3f-151">c.</span></span> <span data-ttu-id="22a3f-152">Aby znaleźć i skopiować nazwę subskrypcji w [klasycznego portalu Azure](https://manage.windowsazure.com/), przewiń w dół i kliknij przycisk **ustawienia** po lewej stronie portalu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-152">To locate and copy your subscription name in the [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on the left side of the portal.</span></span> <span data-ttu-id="22a3f-153">Kliknij przycisk **subskrypcje** umożliwia wyświetlenie listy subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-153">Click **Subscriptions** to see a list of your subscriptions.</span></span> <span data-ttu-id="22a3f-154">Skopiuj nazwę subskrypcji, która ma być używany podczas uruchamiania skryptów podane w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="22a3f-154">Copy the name of subscription that you want to use while running the scripts given in this guide.</span></span>
     
     ![klasyczny portal Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="22a3f-156">**$StorageAccountName:** użyć nazwy podanej w skrypcie lub wprowadź nową nazwę dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-156">**$StorageAccountName:** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="22a3f-157">**Ważne:** nazwę konta magazynu musi być unikatowa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-157">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="22a3f-158">Musi być pisane małymi literami, zbyt!</span><span class="sxs-lookup"><span data-stu-id="22a3f-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="22a3f-159">**$Location:** Użyj danego "zachodnie stany USA" w skrypcie lub wybierz inne lokalizacje Azure, takich jak wschodnie stany USA, Europa Północna, Europa i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="22a3f-159">**$Location:** Use the given "West US" in the script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="22a3f-160">**$ContainerName:** użyć nazwy podanej w skrypcie lub wprowadź nową nazwę dla Twojego kontenera.</span><span class="sxs-lookup"><span data-stu-id="22a3f-160">**$ContainerName:** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="22a3f-161">**$ImageToUpload:** wprowadź ścieżkę do obrazu na komputerze lokalnym, takich jak: "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="22a3f-161">**$ImageToUpload:** Enter a path to a picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="22a3f-162">**$DestinationFolder:** wprowadź ścieżkę do katalogu lokalnego do przechowywania pliki pobierane z usługi Azure Storage, takich jak: "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="22a3f-162">**$DestinationFolder:** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="22a3f-163">Po zaktualizowaniu zmienne skryptu w pliku "mystoragescript.ps1", kliknij przycisk **pliku** > **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-163">After updating the script variables in the "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="22a3f-164">Następnie kliknij przycisk **debugowania** > **Uruchom** lub naciśnij klawisz **F5** do uruchomienia skryptu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-164">Then, click **Debug** > **Run** or press **F5** to run the script.</span></span>  

<span data-ttu-id="22a3f-165">Po uruchomieniu skryptu, ma lokalne miejsce docelowe folder, który zawiera plik pobrany obraz.</span><span class="sxs-lookup"><span data-stu-id="22a3f-165">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="22a3f-166">Poniższy zrzut ekranu przedstawia przykład danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="22a3f-166">The following screenshot shows an example output:</span></span>

![Pobieranie obiektów blob](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="22a3f-168">W sekcji "Wprowadzenie do magazynu Azure i programu PowerShell w ciągu 5 minut" zapewnić szybkie wprowadzenie dotyczące sposobu używania programu Azure PowerShell z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="22a3f-168">The "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how to use Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="22a3f-169">Aby uzyskać szczegółowe informacje i instrukcje, firma Microsoft zachęca do odczytu w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="22a3f-169">For detailed information and instructions, we encourage you to read the following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="22a3f-170">Wymagania wstępne dotyczące korzystania z programu Azure PowerShell z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="22a3f-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="22a3f-171">Potrzebujesz subskrypcji platformy Azure i konta, aby uruchomić polecenia cmdlet programu PowerShell podane w tym przewodniku, jak opisano powyżej.</span><span class="sxs-lookup"><span data-stu-id="22a3f-171">You need an Azure subscription and account to run the PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="22a3f-172">Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet do zarządzania za pomocą środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a3f-172">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="22a3f-173">Aby uzyskać informacje na temat instalowania i konfigurowania programu Azure PowerShell, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="22a3f-173">For information on installing and setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="22a3f-174">Zaleca się pobrać i zainstalować lub uaktualnić moduł Azure PowerShell najnowsze przed rozpoczęciem korzystania z tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="22a3f-174">We recommend that you download and install or upgrade to the latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="22a3f-175">Można uruchomić polecenia cmdlet w konsoli środowiska Windows PowerShell standard lub Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="22a3f-175">You can run the cmdlets in the standard Windows PowerShell console or the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="22a3f-176">Na przykład, aby otworzyć **programu Windows PowerShell ISE**, przejdź do Start menu, wpisz narzędzia administracyjne i kliknij, aby go uruchomić.</span><span class="sxs-lookup"><span data-stu-id="22a3f-176">For example, to open **Windows PowerShell ISE**, go to the Start menu, type Administrative Tools and click to run it.</span></span> <span data-ttu-id="22a3f-177">W oknie Narzędzia administracyjne kliknij prawym przyciskiem myszy program Windows PowerShell ISE, kliknij polecenie Uruchom jako Administrator.</span><span class="sxs-lookup"><span data-stu-id="22a3f-177">In the Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-to-manage-storage-accounts-in-azure"></a><span data-ttu-id="22a3f-178">Jak zarządzać kontami magazynu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="22a3f-178">How to manage storage accounts in Azure</span></span>

<span data-ttu-id="22a3f-179">Spójrzmy na zarządzanie kontami magazynu na platformie Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="22a3f-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-to-set-a-default-azure-subscription"></a><span data-ttu-id="22a3f-180">Jak ustawić domyślnego subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22a3f-180">How to set a default Azure subscription</span></span>
<span data-ttu-id="22a3f-181">Aby zarządzać magazynem Azure przy użyciu programu Azure PowerShell, należy uwierzytelnić środowiskiem klienta na platformie Azure przy użyciu uwierzytelniania usługi Azure Active Directory lub uwierzytelniania opartego na certyfikatach.</span><span class="sxs-lookup"><span data-stu-id="22a3f-181">To manage Azure Storage using Azure PowerShell, you need to authenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="22a3f-182">Aby uzyskać szczegółowe informacje, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) samouczka.</span><span class="sxs-lookup"><span data-stu-id="22a3f-182">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="22a3f-183">W tym przewodniku korzysta z uwierzytelniania usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22a3f-183">This guide uses the Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="22a3f-184">W środowisku Windows PowerShell ISE, wpisz następujące polecenie, aby dodać Azure konta lokalnego środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="22a3f-184">In Windows PowerShell ISE, type the following command to add your Azure account to the local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="22a3f-185">W oknie "Logowania w celu Microsoft Azure" wpisz adres e-mail i hasło skojarzone z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="22a3f-185">In the "Sign in to Microsoft Azure" window, type the email address and password associated with your account.</span></span> <span data-ttu-id="22a3f-186">Nastąpi uwierzytelnienie i zapisanie informacji o poświadczeniach na platformie Azure, a następnie zamknięcie okna.</span><span class="sxs-lookup"><span data-stu-id="22a3f-186">Azure authenticates and saves the credential information, and then closes the window.</span></span>

3. <span data-ttu-id="22a3f-187">Następnie uruchom następujące polecenie, aby wyświetlić konta platformy Azure w lokalnym środowisku PowerShell i sprawdź, czy Twoje konto jest wyświetlane:</span><span class="sxs-lookup"><span data-stu-id="22a3f-187">Next, run the following command to view the Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="22a3f-188">Następnie uruchom następujące polecenie cmdlet, aby wyświetlić wszystkie subskrypcje, które są podłączone do lokalnej sesji programu PowerShell i sprawdź, czy subskrypcja jest wyświetlane:</span><span class="sxs-lookup"><span data-stu-id="22a3f-188">Then, run the following cmdlet to view all the subscriptions that are connected to the local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="22a3f-189">Aby ustawić domyślnego subskrypcji platformy Azure, uruchom polecenie cmdlet AzureSubscription wybierz:</span><span class="sxs-lookup"><span data-stu-id="22a3f-189">To set a default Azure subscription, run the Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="22a3f-190">Sprawdź nazwę subskrypcji domyślne przy użyciu polecenia cmdlet Get-AzureSubscription:</span><span class="sxs-lookup"><span data-stu-id="22a3f-190">Verify the name of the default subscription by running the Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="22a3f-191">Aby wyświetlić wszystkie dostępne polecenia cmdlet programu PowerShell dla usługi Azure Storage, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="22a3f-191">To see all the available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a><span data-ttu-id="22a3f-192">Jak utworzyć nowe konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="22a3f-192">How to create a new Azure storage account</span></span>
<span data-ttu-id="22a3f-193">Aby korzystać z magazynu Azure, konieczne będzie konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-193">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="22a3f-194">Po skonfigurowaniu komputera do nawiązania połączenia subskrypcji, można utworzyć nowe konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-194">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

1. <span data-ttu-id="22a3f-195">Uruchom polecenie cmdlet Get-AzureLocation do znajdowania lokalizacji datacenter dostępne:</span><span class="sxs-lookup"><span data-stu-id="22a3f-195">Run the Get-AzureLocation cmdlet to find all the available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="22a3f-196">Następnie uruchom polecenie cmdlet New-AzureStorageAccount Aby utworzyć nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-196">Next, run the New-AzureStorageAccount cmdlet to create a new storage account.</span></span> <span data-ttu-id="22a3f-197">Poniższy przykład tworzy nowe konto magazynu w centrum danych "Zachodnie stany USA".</span><span class="sxs-lookup"><span data-stu-id="22a3f-197">The following example creates a new storage account in the "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="22a3f-198">Nazwa konta magazynu musi być unikatowa w obrębie platformy Azure i muszą być małymi literami.</span><span class="sxs-lookup"><span data-stu-id="22a3f-198">The name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="22a3f-199">Ograniczenia i konwencje nazewnictwa, zobacz [o kontach magazynu Azure](storage-create-storage-account.md) i [nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a><span data-ttu-id="22a3f-200">Jak ustawić domyślnego konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22a3f-200">How to set a default Azure storage account</span></span>
<span data-ttu-id="22a3f-201">Może mieć wielu kont magazynu w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="22a3f-202">Można wybrać jedną z nich i ustawić go jako domyślne konto magazynu dla wszystkich poleceń magazynu w tej samej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a3f-202">You can choose one of them and set it as the default storage account for all the storage commands in the same PowerShell session.</span></span> <span data-ttu-id="22a3f-203">Umożliwia to uruchamianie poleceń programu Azure PowerShell magazynu bez jawne określenie kontekst magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-203">This enables you to run the Azure PowerShell storage commands without specifying the storage context explicitly.</span></span>

1. <span data-ttu-id="22a3f-204">Aby skonfigurować domyślne konto magazynu dla Twojej subskrypcji, można uruchomić polecenie cmdlet Set-AzureSubscription.</span><span class="sxs-lookup"><span data-stu-id="22a3f-204">To set a default storage account for your subscription, you can run the Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="22a3f-205">Następnie uruchom polecenie cmdlet Get-AzureSubscription, aby sprawdzić, czy konto magazynu jest skojarzony z domyślnego konta subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-205">Next, run the Get-AzureSubscription cmdlet to verify that the storage account is associated with your default subscription account.</span></span> <span data-ttu-id="22a3f-206">To polecenie zwraca właściwości subskrypcji w bieżącej subskrypcji, w tym konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-206">This command returns the subscription properties on the current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="22a3f-207">Jak wyświetlić wszystkie konta magazynu Azure w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="22a3f-207">How to list all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="22a3f-208">Każda subskrypcja platformy Azure może mieć maksymalnie 100 kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-208">Each Azure subscription can have up to 100 storage accounts.</span></span> <span data-ttu-id="22a3f-209">Aby uzyskać najbardziej aktualne informacje dotyczące limity, zobacz [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="22a3f-209">For the most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="22a3f-210">Uruchom następujące polecenie cmdlet, aby znaleźć nazwę i stanu kont magazynu w bieżącej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="22a3f-210">Run the following cmdlet to find out the name and status of the storage accounts in the current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a><span data-ttu-id="22a3f-211">Jak utworzyć kontekst magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="22a3f-211">How to create an Azure storage context</span></span>
<span data-ttu-id="22a3f-212">Kontekst magazynu platformy Azure jest obiektu w programie PowerShell, aby hermetyzować poświadczeń magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-212">Azure storage context is an object in PowerShell to encapsulate the storage credentials.</span></span> <span data-ttu-id="22a3f-213">Przy użyciu kontekst magazynu podczas uruchamiania wszystkie kolejne polecenia cmdlet umożliwia uwierzytelnić żądania bez jawne określenie konta magazynu i klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-213">Using a storage context while running any subsequent cmdlet enables you to authenticate your request without specifying the storage account and its access key explicitly.</span></span> <span data-ttu-id="22a3f-214">Kontekst magazynu można utworzyć na wiele sposobów, na przykład za pomocą magazynu konta nazwy i klucza dostępu, token sygnatury dostępu Współdzielonego dostępu współdzielonego, parametry połączenia lub anonimowych.</span><span class="sxs-lookup"><span data-stu-id="22a3f-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="22a3f-215">Aby uzyskać więcej informacji, zobacz [AzureStorageContext nowy](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="22a3f-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="22a3f-216">Użyj jednej z następujących trzech sposobów, aby utworzyć kontekst magazynu:</span><span class="sxs-lookup"><span data-stu-id="22a3f-216">Use one of the following three ways to create a storage context:</span></span>

* <span data-ttu-id="22a3f-217">Uruchom [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) polecenia cmdlet, aby dowiedzieć się, podstawowy klucz dostępu dla konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-217">Run the [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet to find out the primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="22a3f-218">Następnie wywołaj [AzureStorageContext nowy](/powershell/module/azure.storage/new-azurestoragecontext) polecenia cmdlet można utworzyć kontekstu magazynu:</span><span class="sxs-lookup"><span data-stu-id="22a3f-218">Next, call the [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet to create a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="22a3f-219">Generowanie tokenu sygnatury dostępu współdzielonego dla kontenera magazynu systemu Azure i przy jego użyciu można utworzyć kontekstu magazynu:</span><span class="sxs-lookup"><span data-stu-id="22a3f-219">Generate a shared access signature token for an Azure storage container and use it to create a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="22a3f-220">Aby uzyskać więcej informacji, zobacz [AzureStorageContainerSASToken nowy](/powershell/module/azure.storage/new-azurestoragecontainersastoken) i [przy użyciu dostępu sygnatur dostępu Współdzielonego](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="22a3f-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="22a3f-221">W niektórych przypadkach możesz określić punktów końcowych usługi podczas tworzenia nowego kontekst magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-221">In some cases, you may want to specify the service endpoints when you create a new storage context.</span></span> <span data-ttu-id="22a3f-222">Może to być konieczne, gdy niestandardowej nazwy domeny dla konta magazynu zostały zarejestrowane w usłudze obiektów Blob lub chcesz używać do uzyskiwania dostępu do zasobów magazynu sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="22a3f-222">This might be necessary when you have registered a custom domain name for your storage account with the Blob service or you want to use a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="22a3f-223">W parametrach połączenia ustawiono punktów końcowych usługi i go użyć do utworzenia nowego kontekst magazynu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="22a3f-223">Set the service endpoints in a connection string and use it to create a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="22a3f-224">Aby uzyskać więcej informacji na temat konfigurowania parametrów połączenia magazynu, zobacz [Konfigurowanie parametrów połączenia](storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="22a3f-224">For more information on how to configure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="22a3f-225">Teraz, skonfiguruj komputer i przedstawiono sposób zarządzać subskrypcjami i konta magazynu przy użyciu programu Azure PowerShell, przejdź do następnej sekcji, aby dowiedzieć się, jak zarządzać obiekty BLOB platformy Azure i migawki obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="22a3f-225">Now that you have set up your computer and learned how to manage subscriptions and storage accounts using Azure PowerShell, go to the next section to learn how to manage Azure blobs and blob snapshots.</span></span>

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="22a3f-226">Jak pobrać i ponowne generowanie kluczy magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="22a3f-226">How to retrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="22a3f-227">Konto magazynu Azure ma dwa klucze konta.</span><span class="sxs-lookup"><span data-stu-id="22a3f-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="22a3f-228">Następujące polecenie cmdlet służy do pobierania kluczy.</span><span class="sxs-lookup"><span data-stu-id="22a3f-228">You can use the following cmdlet to retrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="22a3f-229">Użyj następującego polecenia cmdlet można pobrać określonego klucza.</span><span class="sxs-lookup"><span data-stu-id="22a3f-229">Use the following cmdlet to retrieve a specific key.</span></span> <span data-ttu-id="22a3f-230">Prawidłowe wartości to podstawowe i pomocnicze.</span><span class="sxs-lookup"><span data-stu-id="22a3f-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="22a3f-231">Jeśli chcesz ponownie wygenerować klucze, użyj następującego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-231">If you would like to regenerate your keys, use the following cmdlet.</span></span> <span data-ttu-id="22a3f-232">Prawidłowe wartości właściwości KeyType - to "Primary" i "Secondary"</span><span class="sxs-lookup"><span data-stu-id="22a3f-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a><span data-ttu-id="22a3f-233">Jak zarządzać obiekty BLOB platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22a3f-233">How to manage Azure blobs</span></span>
<span data-ttu-id="22a3f-234">Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, takich jak dane tekstowe lub binarne, którego mogą uzyskać dostęp z dowolnego miejsca na świecie za pośrednictwem protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="22a3f-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="22a3f-235">W tej sekcji założono, że znasz już pojęcia dotyczące usługi magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-235">This section assumes that you are already familiar with the Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="22a3f-236">Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md) i [pojęcia dotyczące usługi Blob](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-to-create-a-container"></a><span data-ttu-id="22a3f-237">Jak utworzyć kontener</span><span class="sxs-lookup"><span data-stu-id="22a3f-237">How to create a container</span></span>
<span data-ttu-id="22a3f-238">Każdy obiekt blob w magazynie Azure musi być w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="22a3f-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="22a3f-239">Można utworzyć kontener prywatnego za pomocą polecenia cmdlet New-AzureStorageContainer:</span><span class="sxs-lookup"><span data-stu-id="22a3f-239">You can create a private container using the New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="22a3f-240">Istnieją trzy poziomy anonimowy dostęp do odczytu: **poza**, **obiektu Blob**, i **kontenera**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="22a3f-241">Aby uniemożliwić dostęp anonimowy do obiektów blob, ustaw dla parametru uprawnienia **poza**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-241">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="22a3f-242">Domyślnie nowy kontener jest prywatny i jest możliwy tylko przez właściciela konta.</span><span class="sxs-lookup"><span data-stu-id="22a3f-242">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="22a3f-243">Umożliwia anonimowego publiczny dostęp do odczytu do zasobów obiektów blob, ale nie do metadanych kontenera lub listę obiektów blob w kontenerze, ustaw uprawnienia dla parametru **obiektu Blob**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-243">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="22a3f-244">Umożliwia pełną publiczny dostęp do odczytu do zasobów, metadanych kontenera i listę obiektów blob w kontenerze obiektu blob, ustaw dla parametru uprawnienia **kontenera**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-244">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="22a3f-245">Aby uzyskać więcej informacji, zobacz [Zarządzanie anonimowy dostęp do odczytu do kontenerów i obiektów blob](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="22a3f-245">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="22a3f-246">Jak przekazać obiekt blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="22a3f-246">How to upload a blob into a container</span></span>
<span data-ttu-id="22a3f-247">Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="22a3f-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="22a3f-248">Aby uzyskać więcej informacji, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="22a3f-249">Aby przekazać obiektów blob w kontenerze, można użyć [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-249">To upload blobs in to a container, you can use the [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="22a3f-250">Domyślnie to polecenie operacji przekazywania plików lokalnych do blokowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="22a3f-250">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="22a3f-251">Aby określić typ obiektu blob, można użyć parametru - BlobType.</span><span class="sxs-lookup"><span data-stu-id="22a3f-251">To specify the type for the blob, you can use the -BlobType parameter.</span></span>

<span data-ttu-id="22a3f-252">W poniższym przykładzie uruchamiane [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) polecenia cmdlet, aby pobrać wszystkie pliki w określonym folderze, a następnie przekazuje je do następnego polecenia cmdlet, za pomocą operatora potoku.</span><span class="sxs-lookup"><span data-stu-id="22a3f-252">The following example runs the [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet to get all the files in the specified folder, and then passes them to the next cmdlet by using the pipeline operator.</span></span> <span data-ttu-id="22a3f-253">[Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) polecenia cmdlet przekazuje lokalnych plików z kontenera:</span><span class="sxs-lookup"><span data-stu-id="22a3f-253">The [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads the local files to your container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a><span data-ttu-id="22a3f-254">Jak pobrać obiekty BLOB z kontenera</span><span class="sxs-lookup"><span data-stu-id="22a3f-254">How to download blobs from a container</span></span>
<span data-ttu-id="22a3f-255">W poniższym przykładzie pokazano, jak pobrać obiekty BLOB z kontenera.</span><span class="sxs-lookup"><span data-stu-id="22a3f-255">The following example demonstrates how to download blobs from a container.</span></span> <span data-ttu-id="22a3f-256">Przykład najpierw nawiąże połączenie z magazynem Azure przy użyciu kontekstu konta magazynu, w tym nazwę konta magazynu i jego podstawowy klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-256">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its primary access key.</span></span> <span data-ttu-id="22a3f-257">Następnie pobiera odwołanie obiektu blob przy użyciu przykładzie [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-257">Then, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="22a3f-258">Następnie w przykładzie użyto [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) polecenia cmdlet, aby pobierać obiekty BLOB do folderu docelowego lokalnego.</span><span class="sxs-lookup"><span data-stu-id="22a3f-258">Next, the example uses the [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet to download blobs into the local destination folder.</span></span>

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a><span data-ttu-id="22a3f-259">Kopiowanie obiektów blob z jeden kontener magazynu do innego</span><span class="sxs-lookup"><span data-stu-id="22a3f-259">How to copy blobs from one storage container to another</span></span>
<span data-ttu-id="22a3f-260">Asynchronicznie należy skopiować obiekty BLOB na kontach magazynu i regionów.</span><span class="sxs-lookup"><span data-stu-id="22a3f-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="22a3f-261">W poniższym przykładzie pokazano sposób kopiowania obiektów blob z jeden kontener magazynu do innego w dwóch różnych kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-261">The following example demonstrates how to copy blobs from one storage container to another in two different storage accounts.</span></span> <span data-ttu-id="22a3f-262">Przykład najpierw ustawia zmienne dla konta magazynu źródłowego i docelowego, a następnie tworzy kontekst magazynu dla poszczególnych kont.</span><span class="sxs-lookup"><span data-stu-id="22a3f-262">The example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="22a3f-263">Następnie przykładowy kod kopiuje obiekty BLOB w kontenerze źródła do kontenera docelowego przy użyciu [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-263">Next, the example copies blobs from the source container to the destination container using the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="22a3f-264">W przykładzie założono, że konta magazynu źródłowego i docelowego i kontenerów już istnieje.</span><span class="sxs-lookup"><span data-stu-id="22a3f-264">The example assumes that the source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="22a3f-265">Należy pamiętać, że w tym przykładzie wykonuje asynchroniczne kopiowania.</span><span class="sxs-lookup"><span data-stu-id="22a3f-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="22a3f-266">Można monitorować stan poszczególnych kopii uruchamiając [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-266">You can monitor the status of each copy by running the [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-to-copy-blobs-from-a-secondary-location"></a><span data-ttu-id="22a3f-267">Kopiowanie obiektów blob z lokalizacji dodatkowej</span><span class="sxs-lookup"><span data-stu-id="22a3f-267">How to copy blobs from a secondary location</span></span>
<span data-ttu-id="22a3f-268">Obiekty BLOB można skopiować z lokalizacji dodatkowej RA-GRS włączone konta.</span><span class="sxs-lookup"><span data-stu-id="22a3f-268">You can copy blobs from the secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a><span data-ttu-id="22a3f-269">Jak usunąć obiektu blob</span><span class="sxs-lookup"><span data-stu-id="22a3f-269">How to delete a blob</span></span>
<span data-ttu-id="22a3f-270">Aby usunąć obiekt blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać polecenie cmdlet Remove-AzureStorageBlob na nim.</span><span class="sxs-lookup"><span data-stu-id="22a3f-270">To delete a blob, first get a blob reference and then call the Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="22a3f-271">Poniższy przykład powoduje usunięcie wszystkich obiektów blob w danym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="22a3f-271">The following example deletes all the blobs in a given container.</span></span> <span data-ttu-id="22a3f-272">Przykład najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-272">The example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="22a3f-273">Następnie pobiera odwołanie obiektu blob przy użyciu przykładzie [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet i uruchamia [AzureStorageBlob Usuń](/powershell/module/azure.storage/remove-azurestorageblob) polecenia cmdlet, aby usunąć obiekty BLOB z kontenera w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-273">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet to remove blobs from a container in Azure storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a><span data-ttu-id="22a3f-274">Jak zarządzać migawki obiektu blob systemu Azure</span><span class="sxs-lookup"><span data-stu-id="22a3f-274">How to manage Azure blob snapshots</span></span>
<span data-ttu-id="22a3f-275">Azure umożliwia tworzenie migawki obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="22a3f-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="22a3f-276">Migawka jest tylko do odczytu wersji obiektu blob, która jest wykonywana w punkcie w czasie.</span><span class="sxs-lookup"><span data-stu-id="22a3f-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="22a3f-277">Po utworzeniu migawki, to można można odczytać, kopiowane, lub usunięte, ale nie został zmodyfikowany.</span><span class="sxs-lookup"><span data-stu-id="22a3f-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="22a3f-278">Migawki umożliwiają tworzenie kopii zapasowej obiektu blob, pojawiającą się w chwili.</span><span class="sxs-lookup"><span data-stu-id="22a3f-278">Snapshots provide a way to back up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="22a3f-279">Aby uzyskać więcej informacji, zobacz [tworzenia migawki obiektu Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-to-create-a-blob-snapshot"></a><span data-ttu-id="22a3f-280">Tworzenie migawki obiektu blob</span><span class="sxs-lookup"><span data-stu-id="22a3f-280">How to create a blob snapshot</span></span>
<span data-ttu-id="22a3f-281">Aby utworzyć snaphot obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać `ICloudBlob.CreateSnapshot` dla niego metodę.</span><span class="sxs-lookup"><span data-stu-id="22a3f-281">To create a snaphot of a blob, first get a blob reference and then call the `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="22a3f-282">Poniższy przykład najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-282">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="22a3f-283">Następnie pobiera odwołanie obiektu blob przy użyciu przykładzie [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet i uruchamia [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) metodę w celu utworzenia migawki.</span><span class="sxs-lookup"><span data-stu-id="22a3f-283">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a><span data-ttu-id="22a3f-284">Sposób wyświetlania migawki obiektu blob</span><span class="sxs-lookup"><span data-stu-id="22a3f-284">How to list a blob's snapshots</span></span>
<span data-ttu-id="22a3f-285">Można utworzyć dowolną liczbę migawek do obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="22a3f-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="22a3f-286">Można wyświetlić listę migawki skojarzone z z obiektu blob do śledzenia sieci bieżącej migawki.</span><span class="sxs-lookup"><span data-stu-id="22a3f-286">You can list the snapshots associated with your blob to track your current snapshots.</span></span> <span data-ttu-id="22a3f-287">W poniższym przykładzie użyto wstępnie zdefiniowanych obiektów blob i wywołania [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet, aby wyświetlić listę migawki tego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="22a3f-287">The following example uses a predefined blob and calls the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet to list the snapshots of that blob.</span></span>  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a><span data-ttu-id="22a3f-288">Jak skopiować migawki obiektu blob</span><span class="sxs-lookup"><span data-stu-id="22a3f-288">How to copy a snapshot of a blob</span></span>
<span data-ttu-id="22a3f-289">Możesz skopiować migawki obiektu blob do przywrócenia migawki.</span><span class="sxs-lookup"><span data-stu-id="22a3f-289">You can copy a snapshot of a blob to restore the snapshot.</span></span> <span data-ttu-id="22a3f-290">Aby uzyskać szczegółowe informacje i ograniczenia, zobacz [tworzenia migawki obiektu Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="22a3f-291">Poniższy przykład najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-291">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="22a3f-292">Następnie w przykładzie zdefiniowano zmienne nazwa kontenera i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="22a3f-292">Next, the example defines the container and blob name variables.</span></span> <span data-ttu-id="22a3f-293">Przykład pobiera odwołanie obiektu blob przy użyciu [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet i uruchamia [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) metodę w celu utworzenia migawki.</span><span class="sxs-lookup"><span data-stu-id="22a3f-293">The example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span> <span data-ttu-id="22a3f-294">Następnie, w przykładzie uruchamiane są [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) polecenia cmdlet można skopiować migawki obiektu blob przy użyciu obiektu ICloudBlob dla źródłowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="22a3f-294">Then, the example runs the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet to copy the snapshot of a blob using the ICloudBlob object for the source blob.</span></span> <span data-ttu-id="22a3f-295">Należy zaktualizować zmienne na podstawie konfiguracji przed uruchomieniem w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="22a3f-295">Be sure to update the variables based on your configuration before running the example.</span></span> <span data-ttu-id="22a3f-296">Należy pamiętać, że w poniższym przykładzie założono, że źródłowy i docelowy kontenery i źródłowego obiektu blob już istnieje.</span><span class="sxs-lookup"><span data-stu-id="22a3f-296">Note that the following example assumes that the source and destination containers, and the source blob already exist.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="22a3f-297">Teraz, kiedy znasz sposobu zarządzania obiekty BLOB platformy Azure i obiektów blob migawki przy użyciu programu Azure PowerShell, przejdź do następnej sekcji, aby dowiedzieć się, jak zarządzać tabel, kolejek i plików.</span><span class="sxs-lookup"><span data-stu-id="22a3f-297">Now that you have learned how to manage Azure blobs and blob snapshots with Azure PowerShell, go to the next section to learn how to manage tables, queues, and files.</span></span>

## <a name="how-to-manage-azure-tables-and-table-entities"></a><span data-ttu-id="22a3f-298">Jak zarządzać tabelach platformy Azure i jednostek tabeli</span><span class="sxs-lookup"><span data-stu-id="22a3f-298">How to manage Azure tables and table entities</span></span>
<span data-ttu-id="22a3f-299">Azure usługi Magazyn tabel jest magazynem danych NoSQL, która służy do przechowywania i zapytań dotyczących dużych zestawów strukturalnych danych nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="22a3f-299">Azure Table storage service is a NoSQL datastore, which you can use to store and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="22a3f-300">Główne składniki usługi są tabele, jednostki i właściwości.</span><span class="sxs-lookup"><span data-stu-id="22a3f-300">The main components of the service are tables, entities, and properties.</span></span> <span data-ttu-id="22a3f-301">Tabela jest kolekcji jednostek.</span><span class="sxs-lookup"><span data-stu-id="22a3f-301">A table is a collection of entities.</span></span> <span data-ttu-id="22a3f-302">Jednostka jest zbiór właściwości.</span><span class="sxs-lookup"><span data-stu-id="22a3f-302">An entity is a set of properties.</span></span> <span data-ttu-id="22a3f-303">Każdy obiekt może mieć maksymalnie 252 właściwości, które są wszystkie pary nazwa wartość.</span><span class="sxs-lookup"><span data-stu-id="22a3f-303">Each entity can have up to 252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="22a3f-304">W tej sekcji założono, że znasz już pojęcia dotyczące usługi Magazyn tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-304">This section assumes that you are already familiar with the Azure Table Storage Service concepts.</span></span> <span data-ttu-id="22a3f-305">Aby uzyskać szczegółowe informacje, zobacz [opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx) i [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="22a3f-305">For detailed information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="22a3f-306">W poniższych podsekcjach dowiesz się, jak zarządzać usługą magazynu tabel Azure przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a3f-306">In the following subsections, you'll learn how to manage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="22a3f-307">Omówione scenariusze obejmują **tworzenie**, **usuwanie**, i **pobierania** **tabel**, jak również **Dodawanie**, **badania**, i **usuwania jednostek tabeli**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-307">The scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-to-create-a-table"></a><span data-ttu-id="22a3f-308">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="22a3f-308">How to create a table</span></span>
<span data-ttu-id="22a3f-309">Każda tabela musi znajdować się na koncie magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="22a3f-310">Poniższy przykład przedstawia sposób tworzenia tabeli w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="22a3f-310">The following example demonstrates how to create a table in Azure Storage.</span></span> <span data-ttu-id="22a3f-311">Przykład najpierw nawiąże połączenie z usługi Azure Storage przy użyciu kontekstu konta magazynu, która zawiera nazwę konta magazynu i klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-311">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="22a3f-312">Następnie używa [AzureStorageTable nowy](/powershell/module/azure.storage/new-azurestoragetable) polecenia cmdlet, aby utworzyć tabelę w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="22a3f-312">Next, it uses the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet to create a table in Azure Storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a><span data-ttu-id="22a3f-313">Jak pobrać tabeli</span><span class="sxs-lookup"><span data-stu-id="22a3f-313">How to retrieve a table</span></span>
<span data-ttu-id="22a3f-314">Można zbadać i pobrać jednego lub wszystkich tabel na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="22a3f-315">W poniższym przykładzie pokazano, jak pobrać danej tabeli za pomocą [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-315">The following example demonstrates how to retrieve a given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="22a3f-316">Wywołanie polecenia cmdlet Get-AzureStorageTable bez żadnych parametrów, pobiera wszystkie tabele magazynu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-316">If you call the Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-to-delete-a-table"></a><span data-ttu-id="22a3f-317">Sposób usuwania tabeli</span><span class="sxs-lookup"><span data-stu-id="22a3f-317">How to delete a table</span></span>
<span data-ttu-id="22a3f-318">Z konta magazynu można usunąć tabeli, za pomocą [AzureStorageTable Usuń](/powershell/module/azure.storage/remove-azurestoragetable) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-318">You can delete a table from a storage account by using the [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a><span data-ttu-id="22a3f-319">Jak zarządzać jednostek tabeli</span><span class="sxs-lookup"><span data-stu-id="22a3f-319">How to manage table entities</span></span>
<span data-ttu-id="22a3f-320">Obecnie programu Azure PowerShell nie udostępnia polecenia cmdlet do zarządzania jednostek tabeli bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="22a3f-320">Currently, Azure PowerShell does not provide cmdlets to manage table entities directly.</span></span> <span data-ttu-id="22a3f-321">Aby wykonywać operacje na jednostkach tabeli, można użyć klasy podane w [biblioteki klienta magazynu Azure dla platformy .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-321">To perform operations on table entities, you can use the classes given in the [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-to-add-table-entities"></a><span data-ttu-id="22a3f-322">Jak dodać jednostek tabeli</span><span class="sxs-lookup"><span data-stu-id="22a3f-322">How to add table entities</span></span>
<span data-ttu-id="22a3f-323">Aby dodać jednostkę do tabeli, należy najpierw utworzyć obiekt, który definiuje właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="22a3f-323">To add an entity to a table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="22a3f-324">Jednostka może mieć maksymalnie 255 właściwości, w tym 3 Właściwości systemowe: **PartitionKey**, **RowKey**, i **sygnatury czasowej**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-324">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="22a3f-325">Jest odpowiedzialny za wstawiania i aktualizowania wartości **PartitionKey** i **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-325">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="22a3f-326">Serwer zarządza wartością **sygnatury czasowej**, która nie może być modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="22a3f-326">The server manages the value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="22a3f-327">Razem **PartitionKey** i **RowKey** jednoznacznie zidentyfikować każdej jednostki w tabeli.</span><span class="sxs-lookup"><span data-stu-id="22a3f-327">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="22a3f-328">**PartitionKey**: Określa jednostki przechowywanego w partycji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-328">**PartitionKey**: Determines the partition that the entity is stored in.</span></span>
* <span data-ttu-id="22a3f-329">**RowKey**: unikatowo identyfikuje jednostek w partycji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-329">**RowKey**: Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="22a3f-330">Można zdefiniować maksymalnie 252 właściwości niestandardowych dla jednostki.</span><span class="sxs-lookup"><span data-stu-id="22a3f-330">You may define up to 252 custom properties for an entity.</span></span> <span data-ttu-id="22a3f-331">Aby uzyskać więcej informacji, zobacz [opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-331">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="22a3f-332">W poniższym przykładzie pokazano, jak dodać jednostek do tabeli.</span><span class="sxs-lookup"><span data-stu-id="22a3f-332">The following example demonstrates how to add entities to a table.</span></span> <span data-ttu-id="22a3f-333">W przykładzie przedstawiono sposób pobierania tabeli pracowników i Dodaj do niej kilku jednostek.</span><span class="sxs-lookup"><span data-stu-id="22a3f-333">The example shows how to retrieve the employee table and add several entities into it.</span></span> <span data-ttu-id="22a3f-334">Najpierw nawiązaniem połączenia z magazynem Azure przy użyciu kontekstu konta magazynu, która zawiera nazwę konta magazynu i klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-334">First, it establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="22a3f-335">Następnie pobiera przy użyciu danej tabeli [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-335">Next, it retrieves the given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="22a3f-336">Jeśli tabela nie istnieje, [AzureStorageTable nowy](/powershell/module/azure.storage/new-azurestoragetable) polecenia cmdlet służy do tworzenia tabeli w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="22a3f-336">If the table does not exist, the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used to create a table in Azure Storage.</span></span> <span data-ttu-id="22a3f-337">Następnie w przykładzie zdefiniowano niestandardowe funkcji Dodaj jednostki do Dodaj jednostki do tabeli, określając każdej jednostki partycji i klucz wiersza.</span><span class="sxs-lookup"><span data-stu-id="22a3f-337">Next, the example defines a custom function Add-Entity to add entities to the table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="22a3f-338">Wywołania funkcji jednostki Dodaj [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet na [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) klasy w celu utworzenia obiektu jednostki.</span><span class="sxs-lookup"><span data-stu-id="22a3f-338">The Add-Entity function calls the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class to create an entity object.</span></span> <span data-ttu-id="22a3f-339">Później, przykład wywołuje [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) metody dla tego obiektu jednostki, aby dodać go do tabeli.</span><span class="sxs-lookup"><span data-stu-id="22a3f-339">Later, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object to add it to a table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity to a table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a><span data-ttu-id="22a3f-340">Jak wykonać zapytanie dotyczące jednostek tabeli</span><span class="sxs-lookup"><span data-stu-id="22a3f-340">How to query table entities</span></span>
<span data-ttu-id="22a3f-341">Aby sprawdzić tabelę, użyj [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="22a3f-341">To query a table, use the [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="22a3f-342">W poniższym przykładzie założono, zostały już uruchomiono skrypt podanych w sposobu, w jaki można dodać jednostki części tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="22a3f-342">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="22a3f-343">Przykład najpierw nawiąże połączenie z magazynem Azure przy użyciu kontekst magazynu, który zawiera nazwę konta magazynu i klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-343">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="22a3f-344">Następnie próbuje pobrać za pomocą tabeli utworzonej wcześniej "pracownicy" [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-344">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="22a3f-345">Wywoływanie [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet w klasie Microsoft.WindowsAzure.Storage.Table.TableQuery tworzy nowy obiekt zapytania.</span><span class="sxs-lookup"><span data-stu-id="22a3f-345">Calling the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="22a3f-346">Przykład szuka obiektów, które mają kolumnę 'ID', którego wartość wynosi 1, ponieważ określony w filtrze ciągu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-346">The example looks for the entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="22a3f-347">Aby uzyskać szczegółowe informacje, zobacz [badania tabel i jednostek](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="22a3f-348">Po uruchomieniu to zapytanie zwraca wszystkich jednostek spełniających kryteria filtrowania.</span><span class="sxs-lookup"><span data-stu-id="22a3f-348">When you run this query, it returns all entities that match the filter criteria.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a><span data-ttu-id="22a3f-349">Sposób usuwania jednostek tabeli</span><span class="sxs-lookup"><span data-stu-id="22a3f-349">How to delete table entities</span></span>
<span data-ttu-id="22a3f-350">Można usunąć jednostki przy użyciu jego kluczy partycji i wiersza.</span><span class="sxs-lookup"><span data-stu-id="22a3f-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="22a3f-351">W poniższym przykładzie założono, zostały już uruchomiono skrypt podanych w sposobu, w jaki można dodać jednostki części tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="22a3f-351">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="22a3f-352">Przykład najpierw nawiąże połączenie z magazynem Azure przy użyciu kontekst magazynu, który zawiera nazwę konta magazynu i klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-352">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="22a3f-353">Następnie próbuje pobrać za pomocą tabeli utworzonej wcześniej "pracownicy" [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-353">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="22a3f-354">Jeśli tabela istnieje, [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) metody do pobierania jednostki na podstawie jego wartości klucza partycji i wiersza.</span><span class="sxs-lookup"><span data-stu-id="22a3f-354">If the table exists, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method to retrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="22a3f-355">Przekazuj jednostki do [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="22a3f-355">Then, pass the entity to the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method to delete.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a><span data-ttu-id="22a3f-356">Jak zarządzać kolejek platformy Azure i wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="22a3f-356">How to manage Azure queues and queue messages</span></span>
<span data-ttu-id="22a3f-357">Azure Queue Storage to usługa do przechowywania dużej liczby komunikatów, do której można uzyskać dostęp z dowolnego miejsca na świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="22a3f-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="22a3f-358">W tej sekcji założono, że znasz już pojęcia dotyczące usługi magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-358">This section assumes that you are already familiar with the Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="22a3f-359">Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="22a3f-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="22a3f-360">W tej sekcji opisano sposób zarządzania usługą magazynu kolejek Azure przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a3f-360">This section will show you how to manage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="22a3f-361">Omówione scenariusze obejmują **wstawianie** i **usuwanie** kolejki komunikatów, a także **tworzenie**, **usuwanie**, i **pobierania kolejek**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-361">The scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-to-create-a-queue"></a><span data-ttu-id="22a3f-362">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="22a3f-362">How to create a queue</span></span>
<span data-ttu-id="22a3f-363">Poniższy przykład najpierw nawiąże połączenie z usługi Azure Storage przy użyciu kontekstu konta magazynu, która zawiera nazwę konta magazynu i klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-363">The following example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="22a3f-364">Następnie wywołuje [AzureStorageQueue nowy](/powershell/module/azure.storage/new-azurestoragequeue) polecenia cmdlet, aby utworzyć kolejkę o nazwie "queuename".</span><span class="sxs-lookup"><span data-stu-id="22a3f-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet to create a queue named 'queuename'.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="22a3f-365">Aby uzyskać informacji na temat konwencji nazewnictwa dla usługi kolejek platformy Azure, zobacz [nazewnictwo kolejek i metadanych](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-to-retrieve-a-queue"></a><span data-ttu-id="22a3f-366">Jak pobrać kolejki</span><span class="sxs-lookup"><span data-stu-id="22a3f-366">How to retrieve a queue</span></span>
<span data-ttu-id="22a3f-367">Można zbadać i pobrać określonej kolejki, a także listę wszystkich kolejek na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-367">You can query and retrieve a specific queue or a list of all the queues in a Storage account.</span></span> <span data-ttu-id="22a3f-368">W poniższym przykładzie pokazano, jak pobrać przy użyciu określonej kolejki [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-368">The following example demonstrates how to retrieve a specified queue using the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="22a3f-369">Jeśli należy wywołać [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) polecenia cmdlet bez parametrów, pobiera listę wszystkich kolejek.</span><span class="sxs-lookup"><span data-stu-id="22a3f-369">If you call the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all the queues.</span></span>

### <a name="how-to-delete-a-queue"></a><span data-ttu-id="22a3f-370">Sposób usuwania kolejki</span><span class="sxs-lookup"><span data-stu-id="22a3f-370">How to delete a queue</span></span>
<span data-ttu-id="22a3f-371">Aby usunąć kolejkę i wszystkie zawarte w niej komunikaty, wywołaj polecenie cmdlet Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="22a3f-371">To delete a queue and all the messages contained in it, call the Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="22a3f-372">Poniższy przykład pokazuje, jak można usunąć za pomocą polecenia cmdlet Remove-AzureStorageQueue określonej kolejki.</span><span class="sxs-lookup"><span data-stu-id="22a3f-372">The following example shows how to delete a specified queue using the Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="22a3f-373">Jak można wstawić komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="22a3f-373">How to insert a message into a queue</span></span>
<span data-ttu-id="22a3f-374">Aby wstawić komunikat do istniejącej kolejki, najpierw utwórz nowe wystąpienie klasy [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="22a3f-374">To insert a message into an existing queue, first create a new instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="22a3f-375">Następnie wywołaj metodę [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-375">Next, call the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="22a3f-376">CloudQueueMessage można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="22a3f-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="22a3f-377">W poniższym przykładzie pokazano, jak dodać wiadomości do kolejki.</span><span class="sxs-lookup"><span data-stu-id="22a3f-377">The following example demonstrates how to add message to a queue.</span></span> <span data-ttu-id="22a3f-378">Przykład najpierw nawiąże połączenie z usługi Azure Storage przy użyciu kontekstu konta magazynu, która zawiera nazwę konta magazynu i klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-378">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="22a3f-379">Następnie pobiera przy użyciu określonej kolejki [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22a3f-379">Next, it retrieves the specified queue using the [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="22a3f-380">Jeśli kolejka istnieje, [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet służy do tworzenia wystąpienia [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="22a3f-380">If the queue exists, the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used to create an instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="22a3f-381">Później, przykład wywołuje [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) metody w tym obiekcie komunikat, aby dodać je do kolejki.</span><span class="sxs-lookup"><span data-stu-id="22a3f-381">Later, the example calls the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object to add it to a queue.</span></span> <span data-ttu-id="22a3f-382">Oto kod, który pobiera kolejki i wstawia komunikat "MessageInfo":</span><span class="sxs-lookup"><span data-stu-id="22a3f-382">Here is code which retrieves a queue and inserts the message 'MessageInfo':</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a><span data-ttu-id="22a3f-383">Jak cofnąć kolejka kolejnego komunikatu</span><span class="sxs-lookup"><span data-stu-id="22a3f-383">How to de-queue at the next message</span></span>
<span data-ttu-id="22a3f-384">Twój kod usuwa komunikat z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="22a3f-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="22a3f-385">Podczas wywoływania [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) metody, otrzymasz następnej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="22a3f-385">When you call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get the next message in a queue.</span></span> <span data-ttu-id="22a3f-386">Komunikat zwrócony z funkcji **GetMessage** staje się niewidoczny dla innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="22a3f-386">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="22a3f-387">Aby zakończyć usuwanie komunikatu z kolejki, musisz również wywołać [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="22a3f-387">To finish removing the message from the queue, you must also call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="22a3f-388">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie będzie w stanie przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu będzie w stanie uzyskać ten sam komunikat i ponowić próbę.</span><span class="sxs-lookup"><span data-stu-id="22a3f-388">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="22a3f-389">Twój kod wywołuje funkcję **DeleteMessage** natychmiast po przetworzeniu komunikatu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-389">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a><span data-ttu-id="22a3f-390">Jak zarządzać udziały plików platformy Azure i plików</span><span class="sxs-lookup"><span data-stu-id="22a3f-390">How to manage Azure file shares and files</span></span>
<span data-ttu-id="22a3f-391">Magazyn plików Azure oferuje współużytkowany magazyn dla aplikacji używających standardowego protokołu SMB.</span><span class="sxs-lookup"><span data-stu-id="22a3f-391">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="22a3f-392">Maszyny wirtualne Microsoft Azure i usługi w chmurze mogą udostępniać dane między składnikami aplikacji za pośrednictwem zainstalowanych udziałów i aplikacji lokalnych mają dostęp do danych plików w udziale za pośrednictwem programu Azure PowerShell lub interfejsu API magazynu plików.</span><span class="sxs-lookup"><span data-stu-id="22a3f-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via the File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="22a3f-393">Aby uzyskać więcej informacji dotyczących usługi Magazyn plików Azure, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](storage-dotnet-how-to-use-files.md) i [interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-to-set-and-query-storage-analytics"></a><span data-ttu-id="22a3f-394">Jak ustawić i analiza magazynu zapytań</span><span class="sxs-lookup"><span data-stu-id="22a3f-394">How to set and query storage analytics</span></span>
<span data-ttu-id="22a3f-395">Można użyć [analityka magazynu Azure](storage-analytics.md) zbieranie metryk dla kont magazynu Azure i rejestrowanie danych dotyczących żądania wysyłane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-395">You can use [Azure Storage Analytics](storage-analytics.md) to collect metrics for your Azure storage accounts and log data about requests sent to your storage account.</span></span> <span data-ttu-id="22a3f-396">Metryki magazynu służy do monitorowania prawidłowości konta magazynu i magazynu rejestrowania do diagnozowania i rozwiązywania problemów z kontem magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-396">You can use storage metrics to monitor the health of a storage account, and storage logging to diagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="22a3f-397">Istnieje możliwość skonfigurowania monitorowania przy użyciu portalu Azure lub programu Windows PowerShell, albo programowo z użyciem biblioteki klienta usługi storage.</span><span class="sxs-lookup"><span data-stu-id="22a3f-397">You can configure monitoring using the Azure portal or Windows PowerShell, or programmatically using the storage client library.</span></span> <span data-ttu-id="22a3f-398">Rejestrowanie magazynu wykonywany po stronie serwera i umożliwia utworzenie rekordów szczegółów dla żądań pomyślnie i niepomyślnie na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-398">Storage logging happens server-side and enables you to record details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="22a3f-399">Dzienniki te umożliwiają szczegóły odczytu, zapisu i usuwania działań przed tabel, kolejek i obiektów blob, a także przyczyny żądań zakończonych niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="22a3f-399">These logs enable you to see details of read, write, and delete operations against your tables, queues, and blobs as well as the reasons for failed requests.</span></span>

<span data-ttu-id="22a3f-400">Aby dowiedzieć się, jak włączyć i wyświetlania metryk magazynu danych przy użyciu programu PowerShell, zobacz [jak włączyć metryki magazynu przy użyciu programu PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="22a3f-400">To learn how to enable and view Storage Metrics data using PowerShell, see [How to enable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="22a3f-401">Aby dowiedzieć się, jak włączyć i pobrać rejestrowania magazynu danych przy użyciu programu PowerShell, zobacz [jak włączyć rejestrowanie magazynu przy użyciu programu PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) i [znajdowanie rejestrowania magazynu danych dziennika](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="22a3f-401">To learn how to enable and retrieve Storage Logging data using PowerShell, see [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="22a3f-402">Aby uzyskać szczegółowe informacje dotyczące rozwiązywania problemów z magazynowaniem za pomocą metryki magazynu i rejestrowanie magazynu, zobacz [monitorowanie, diagnozowanie i rozwiązywanie problemów z programem Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="22a3f-402">For detailed information on using Storage Metrics and Storage Logging to troubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="22a3f-403">Jak zarządzać dostępu sygnatury dostępu Współdzielonego i przechowywane zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="22a3f-403">How to manage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="22a3f-404">Sygnatury dostępu współdzielonego są ważnym elementem modelu zabezpieczeń dla dowolnej aplikacji przy użyciu usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="22a3f-404">Shared access signatures are an important part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="22a3f-405">Są one przydatne zapewniające dostęp jest ograniczony do konta magazynu do klientów, które nie powinny mieć klucz konta.</span><span class="sxs-lookup"><span data-stu-id="22a3f-405">They are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="22a3f-406">Domyślnie obiekty BLOB, tabel i kolejek w ramach tego konta może uzyskiwać dostęp tylko właściciel konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-406">By default, only the owner of the storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="22a3f-407">Jeśli daną usługą lub aplikacją musi udostępniać tych zasobów innym klientom bez udostępniania klucz dostępu, dostępne są trzy opcje:</span><span class="sxs-lookup"><span data-stu-id="22a3f-407">If your service or application needs to make these resources available to other clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="22a3f-408">Ustaw uprawnienia kontenera, aby zezwolić na anonimowy dostęp do odczytu do kontenera i jego obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="22a3f-408">Set a container's permissions to permit anonymous read access to the container and its blobs.</span></span> <span data-ttu-id="22a3f-409">Jest to niedozwolone dla tabel lub kolejek.</span><span class="sxs-lookup"><span data-stu-id="22a3f-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="22a3f-410">Użyj sygnatury dostępu współdzielonego, że przyznaje ograniczone prawa dostępu do kontenerów, obiektów blob, kolejek i tabel dla określonego interwału.</span><span class="sxs-lookup"><span data-stu-id="22a3f-410">Use a shared access signature that grants restricted access rights to containers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="22a3f-411">Zasady dostępu do przechowywanych umożliwia uzyskanie dodatkowy poziom kontroli nad sygnatur dostępu współdzielonego dla kontenera lub jego obiektów blob, kolejki lub tabeli.</span><span class="sxs-lookup"><span data-stu-id="22a3f-411">Use a stored access policy to obtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="22a3f-412">Zasady dostępu przechowywanych umożliwia zmianę godziny rozpoczęcia, czas wygaśnięcia lub uprawnienia dla podpisu lub odwołać go po nim został wystawiony.</span><span class="sxs-lookup"><span data-stu-id="22a3f-412">The stored access policy allows you to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.</span></span>

<span data-ttu-id="22a3f-413">Sygnatury dostępu współdzielonego, można w jednym z dwóch formach:</span><span class="sxs-lookup"><span data-stu-id="22a3f-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="22a3f-414">**Ad hoc SAS**: podczas tworzenia ad hoc SAS, godzina rozpoczęcia, czas wygaśnięcia i uprawnienia dla sygnatury dostępu Współdzielonego są określone w identyfikatorze URI sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="22a3f-414">**Ad hoc SAS**: When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span> <span data-ttu-id="22a3f-415">Ten typ sygnatury dostępu Współdzielonego może zostać utworzony w kontenerze, obiektów blob, tabeli lub kolejki i jest z systemem innym niż odwoływalny.</span><span class="sxs-lookup"><span data-stu-id="22a3f-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="22a3f-416">**Sygnatury dostępu Współdzielonego z zasadami dostępu do przechowywanych**: zasady dostępu do przechowywanych jest zdefiniowany w kontenerze zasobu kontenera obiektów blob, tabel lub kolejek — i służy do zarządzania ograniczeniami dla jednego lub więcej sygnatur dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="22a3f-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="22a3f-417">Po skojarzeniu sygnatury dostępu Współdzielonego za pomocą zasad dostępu przechowywane, sygnatury dostępu Współdzielonego dziedziczy ograniczenia — czas rozpoczęcia, czas wygaśnięcia i uprawnienia - zdefiniowane zasady dostępu przechowywane.</span><span class="sxs-lookup"><span data-stu-id="22a3f-417">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span> <span data-ttu-id="22a3f-418">Ten typ sygnatury dostępu Współdzielonego jest odwoływalny.</span><span class="sxs-lookup"><span data-stu-id="22a3f-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="22a3f-419">Aby uzyskać więcej informacji, zobacz [przy użyciu dostępu sygnatur dostępu Współdzielonego](storage-dotnet-shared-access-signature-part-1.md) i [Zarządzanie anonimowy dostęp do odczytu do kontenerów i obiektów blob](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="22a3f-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="22a3f-420">W kolejnych sekcjach dowiesz się, jak utworzyć zasady dostępu współdzielonego podpisu tokenu i przechowywane dostęp do tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-420">In the next sections, you will learn how to create a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="22a3f-421">Program Azure PowerShell udostępnia podobne polecenia cmdlet dla kontenerów, obiektów blob i kolejek oraz.</span><span class="sxs-lookup"><span data-stu-id="22a3f-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="22a3f-422">Aby uruchomić skrypty w tej sekcji, Pobierz [Azure PowerShell w wersji 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="22a3f-422">To run the scripts in this section, download the [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="22a3f-423">Jak utworzyć token sygnatura dostępu współdzielonego opartych na zasadach</span><span class="sxs-lookup"><span data-stu-id="22a3f-423">How to create a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="22a3f-424">Aby utworzyć nowe zasady dostępu do przechowywanych, należy użyć polecenia cmdlet New-AzureStorageTableStoredAccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="22a3f-424">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy.</span></span> <span data-ttu-id="22a3f-425">Następnie wywołaj metodę [AzureStorageTableSASToken nowy](/powershell/module/azure.storage/new-azurestoragetablesastoken) , aby utworzyć nowy token podpisu na podstawie zasad dostępu współdzielonego dla tabeli magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-425">Then, call the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="22a3f-426">Jak utworzyć token ad hoc sygnatura dostępu współdzielonego (z systemem innym niż — odwoływalny)</span><span class="sxs-lookup"><span data-stu-id="22a3f-426">How to create an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="22a3f-427">Użyj [AzureStorageTableSASToken nowy](/powershell/module/azure.storage/new-azurestoragetablesastoken) , aby utworzyć nowy ad hoc (z systemem innym niż — odwoływalny) Sygnatura dostępu współdzielonego token dla tabeli magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="22a3f-427">Use the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a><span data-ttu-id="22a3f-428">Tworzenie zasad dostępu przechowywane</span><span class="sxs-lookup"><span data-stu-id="22a3f-428">How to create a stored access policy</span></span>
<span data-ttu-id="22a3f-429">Utwórz nowe zasady dostępu do przechowywanych dla tabeli usługi Azure Storage za pomocą polecenia cmdlet New-AzureStorageTableStoredAccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="22a3f-429">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a><span data-ttu-id="22a3f-430">Jak zaktualizować zasad dostępu przechowywane</span><span class="sxs-lookup"><span data-stu-id="22a3f-430">How to update a stored access policy</span></span>
<span data-ttu-id="22a3f-431">Za pomocą polecenia cmdlet Set-AzureStorageTableStoredAccessPolicy zaktualizować istniejące zasady dostępu do przechowywanych dla tabeli magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="22a3f-431">Use the Set-AzureStorageTableStoredAccessPolicy cmdlet to update an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a><span data-ttu-id="22a3f-432">Jak usunąć zasadę przechowywanych dostępu</span><span class="sxs-lookup"><span data-stu-id="22a3f-432">How to delete a stored access policy</span></span>
<span data-ttu-id="22a3f-433">Aby usunąć zasady dostępu przechowywane w tabeli magazynu Azure, użyj polecenia cmdlet Remove-AzureStorageTableStoredAccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="22a3f-433">Use the Remove-AzureStorageTableStoredAccessPolicy cmdlet to delete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="22a3f-434">Jak używać magazynu Azure dla instytucji rządowych USA i Chińskiej wersji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22a3f-434">How to use Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="22a3f-435">Środowiska platformy Azure jest niezależnie od wdrożenia programu Microsoft Azure, takich jak [Azure dla instytucji rządowych USA administracji](https://azure.microsoft.com/features/gov/), [AzureCloud globalne Azure](https://portal.azure.com), i [AzureChinaCloud dla platformy Azure obsługiwane przez 21Vianet w Chinach](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="22a3f-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="22a3f-436">Można wdrażać nowe środowisk Azure dla instytucji rządowych USA i Chińskiej wersji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22a3f-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="22a3f-437">Aby używać usługi Azure Storage z AzureChinaCloud, musisz utworzyć kontekst magazynu, który jest skojarzony z AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="22a3f-437">To use Azure Storage with AzureChinaCloud, you need to create a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="22a3f-438">Wykonaj następujące kroki, które ułatwią rozpoczęcie pracy:</span><span class="sxs-lookup"><span data-stu-id="22a3f-438">Follow these steps to get you started:</span></span>

1. <span data-ttu-id="22a3f-439">Uruchom [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) polecenia cmdlet, aby wyświetlić dostępne środowisk Azure:</span><span class="sxs-lookup"><span data-stu-id="22a3f-439">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="22a3f-440">Dodaj konto chińskiej wersji platformy Azure do środowiska Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="22a3f-440">Add an Azure China account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="22a3f-441">Tworzenie magazynu kontekstu konta AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="22a3f-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="22a3f-442">Aby używać magazynu Azure z [stany USA Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), należy zdefiniować nowe środowisko i następnie tworzy nowy kontekst magazynu z tym środowiskiem:</span><span class="sxs-lookup"><span data-stu-id="22a3f-442">To use Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="22a3f-443">Uruchom [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) polecenia cmdlet, aby wyświetlić dostępne środowisk Azure:</span><span class="sxs-lookup"><span data-stu-id="22a3f-443">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="22a3f-444">Dodaj konto Azure instytucji rządowych Stanów Zjednoczonych do środowiska Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="22a3f-444">Add an Azure US Government account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="22a3f-445">Tworzenie magazynu kontekstu konta AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="22a3f-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="22a3f-446">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="22a3f-446">For more information, see:</span></span>

* <span data-ttu-id="22a3f-447">[Przewodnik dewelopera usługi Microsoft Azure dla instytucji rządowych](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="22a3f-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="22a3f-448">Omówienie różnic podczas tworzenia aplikacji w usłudze Chin</span><span class="sxs-lookup"><span data-stu-id="22a3f-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="22a3f-449">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22a3f-449">Next Steps</span></span>
<span data-ttu-id="22a3f-450">W tym przewodniku kiedy znasz już sposobu zarządzania usługi Azure Storage przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a3f-450">In this guide, you've learned how to manage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="22a3f-451">Poniżej przedstawiono niektóre pokrewne artykuły i zasoby dowiedzieć się więcej o nich.</span><span class="sxs-lookup"><span data-stu-id="22a3f-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="22a3f-452">Dokumentacja usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="22a3f-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="22a3f-453">Polecenia cmdlet programu PowerShell usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="22a3f-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="22a3f-454">Dokumentacja programu PowerShell systemu Windows</span><span class="sxs-lookup"><span data-stu-id="22a3f-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
