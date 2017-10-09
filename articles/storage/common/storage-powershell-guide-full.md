---
title: "aaaUsing programu Azure PowerShell z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello poleceń cmdlet programu Azure PowerShell dla usługi Azure Storage toocreate i zarządzanie kontami magazynu; Praca z obiektów blob, tabel, kolejek i plików. Konfigurowanie i zapytania analityka magazynu, a następnie utwórz sygnatur dostępu współdzielonego."
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
ms.openlocfilehash: 17d638e741911ceafb9777d5c2fce7bfe533e50c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="8133b-103">Używanie programu Azure PowerShell z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8133b-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="8133b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8133b-104">Overview</span></span>
<span data-ttu-id="8133b-105">Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet toomanage Azure za pomocą programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8133b-105">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="8133b-106">Jest to język skryptów i powłoka wiersza polecenia oparta na zadaniach zaprojektowana pod kątem administrowania systemem.</span><span class="sxs-lookup"><span data-stu-id="8133b-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="8133b-107">Przy użyciu programu PowerShell można łatwo kontrolować i automatyzować administrację hello Azure usługi i aplikacje.</span><span class="sxs-lookup"><span data-stu-id="8133b-107">With PowerShell, you can easily control and automate hello administration of your Azure services and applications.</span></span> <span data-ttu-id="8133b-108">Na przykład można użyć hello tooperform poleceń cmdlet hello same zadania, można wykonać za pomocą hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8133b-108">For example, you can use hello cmdlets tooperform hello same tasks that you can perform through hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="8133b-109">W tym przewodniku, firma Microsoft będzie Eksploruj jak toouse hello [polecenia cmdlet usługi Azure Storage](/powershell/module/azurerm.storage/#storage) tooperform różnych zadań programowania i administracji z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8133b-109">In this guide, we'll explore how toouse hello [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="8133b-110">W tym przewodniku założono, że przy użyciu doświadczenie [usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/) i [programu Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="8133b-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="8133b-111">Przewodnik Hello zawiera liczby skryptów toodemonstrate hello użycia programu PowerShell z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8133b-111">hello guide provides a number of scripts toodemonstrate hello usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="8133b-112">Należy zaktualizować hello zmienne skryptu na podstawie konfiguracji przed uruchomieniem każdego skryptu.</span><span class="sxs-lookup"><span data-stu-id="8133b-112">You should update hello script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="8133b-113">Pierwsza sekcja Hello w tym przewodniku zapewnia szybkiego dostępu w usłudze Azure Storage i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8133b-113">hello first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="8133b-114">Aby uzyskać szczegółowe informacje i instrukcje, Rozpocznij od hello [wymagań wstępnych dotyczących używania programu Azure PowerShell z usługą Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="8133b-114">For detailed information and instructions, start from hello [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="8133b-115">Wprowadzenie do korzystania z usługi Azure Storage i programu PowerShell w ciągu 5 minut</span><span class="sxs-lookup"><span data-stu-id="8133b-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="8133b-116">W tej sekcji opisano sposób tooaccess usługi Azure Storage za pomocą programu PowerShell w ciągu 5 minut.</span><span class="sxs-lookup"><span data-stu-id="8133b-116">This section shows you how tooaccess Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="8133b-117">**Nowe tooAzure:** subskrypcji Microsoft Azure i konta Microsoft skojarzonego z jego subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="8133b-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="8133b-118">Aby uzyskać informacje na temat opcji zakupu platformy Azure, zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/), [opcjami zakupu](https://azure.microsoft.com/pricing/purchase-options/), i [oferty Członkowskie](https://azure.microsoft.com/pricing/member-offers/) (dla członków MSDN, Microsoft Partner Network, BizSpark i innych programów firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="8133b-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="8133b-119">Zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) uzyskać więcej informacji o subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8133b-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="8133b-120">**Po utworzeniu subskrypcji Microsoft Azure i konto:**</span><span class="sxs-lookup"><span data-stu-id="8133b-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="8133b-121">Pobierz i zainstaluj najnowsze hello [programu Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="8133b-121">Download and install hello latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="8133b-122">Start środowisko systemu Windows PowerShell zintegrowane skryptów (ISE): W komputerze lokalnym, przejdź toohello **Start** menu.</span><span class="sxs-lookup"><span data-stu-id="8133b-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go toohello **Start** menu.</span></span> <span data-ttu-id="8133b-123">Typ **narzędzia administracyjne** i kliknij przycisk toorun go.</span><span class="sxs-lookup"><span data-stu-id="8133b-123">Type **Administrative Tools** and click toorun it.</span></span> <span data-ttu-id="8133b-124">W hello **narzędzia administracyjne** okna, kliknij prawym przyciskiem myszy **programu Windows PowerShell ISE**, kliknij przycisk **Uruchom jako Administrator**.</span><span class="sxs-lookup"><span data-stu-id="8133b-124">In hello **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="8133b-125">W **programu Windows PowerShell ISE**, kliknij przycisk **pliku** > **nowy** toocreate nowy plik skryptu.</span><span class="sxs-lookup"><span data-stu-id="8133b-125">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="8133b-126">Teraz przedstawimy prosty skrypt, który zawiera podstawowe tooaccess poleceń programu PowerShell usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8133b-126">Now, we'll give you a simple script that shows basic PowerShell commands tooaccess Azure Storage.</span></span> <span data-ttu-id="8133b-127">skryptu Hello najpierw poprosi użytkownika tooadd poświadczenia konta Azure konta Azure toohello PowerShell środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="8133b-127">hello script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment.</span></span> <span data-ttu-id="8133b-128">Następnie skryptu hello ustawiania domyślnych hello subskrypcji platformy Azure i Utwórz nowe konto magazynu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="8133b-128">Then, hello script will set hello default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="8133b-129">Następnie skryptu hello utworzyć nowy kontener w tym nowe konto magazynu i przekaż istniejącego kontenera toothat obrazu pliku (blob).</span><span class="sxs-lookup"><span data-stu-id="8133b-129">Next, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="8133b-130">Po skryptu hello znajduje się lista wszystkich obiektów blob w tym kontenerze, utworzy nowy katalog docelowy w komputerze lokalnym i Pobierz hello pliku obrazu.</span><span class="sxs-lookup"><span data-stu-id="8133b-130">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>
5. <span data-ttu-id="8133b-131">W następujących sekcji kodu hello, wybierz skrypt hello między uwagi hello **#begin** i **#end**.</span><span class="sxs-lookup"><span data-stu-id="8133b-131">In hello following code section, select hello script between hello remarks **#begin** and **#end**.</span></span> <span data-ttu-id="8133b-132">Naciśnij klawisze CTRL + C toocopy on toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="8133b-132">Press CTRL+C toocopy it toohello clipboard.</span></span>

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
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
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="8133b-133">W **programu Windows PowerShell ISE**, naciśnij klawisze CTRL + V toocopy hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="8133b-133">In **Windows PowerShell ISE**, press CTRL+V toocopy hello script.</span></span> <span data-ttu-id="8133b-134">Kliknij przycisk **pliku** > **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="8133b-134">Click **File** > **Save**.</span></span> <span data-ttu-id="8133b-135">W hello **Zapisz jako** okno dialogowe, nazwa typu hello hello pliku skryptu, takie jak "mystoragescript."</span><span class="sxs-lookup"><span data-stu-id="8133b-135">In hello **Save As** dialog window, type hello name of hello script file, such as "mystoragescript."</span></span> <span data-ttu-id="8133b-136">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8133b-136">Click **Save**.</span></span>
7. <span data-ttu-id="8133b-137">Teraz należy zmienne skryptu hello tooupdate na podstawie własnych ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8133b-137">Now, you need tooupdate hello script variables based on your configuration settings.</span></span> <span data-ttu-id="8133b-138">Należy zaktualizować hello **$SubscriptionName** zmiennej przy użyciu posiadanej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8133b-138">You must update hello **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="8133b-139">Możesz zachować hello inne zmienne określone w skrypcie hello lub zaktualizuj je zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="8133b-139">You can keep hello other variables as specified in hello script or update them as you wish.</span></span>
   
   * <span data-ttu-id="8133b-140">**$SubscriptionName:** należy zaktualizować tę zmienną z własną nazwę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8133b-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="8133b-141">Wykonaj jedną z hello następujące trzy sposoby toolocate hello nazwa Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="8133b-141">Follow one of hello following three ways toolocate hello name of your subscription:</span></span>
     
    <span data-ttu-id="8133b-142">a.</span><span class="sxs-lookup"><span data-stu-id="8133b-142">a.</span></span> <span data-ttu-id="8133b-143">W **programu Windows PowerShell ISE**, kliknij przycisk **pliku** > **nowy** toocreate nowy plik skryptu.</span><span class="sxs-lookup"><span data-stu-id="8133b-143">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span> <span data-ttu-id="8133b-144">Kopia hello następujący skrypt toohello nowy plik skryptu i kliknij przycisk **debugowania** > **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="8133b-144">Copy hello following script toohello new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="8133b-145">Hello poniższy skrypt zostanie najpierw poproś użytkownika tooadd poświadczenia konta Azure konta Azure toohello PowerShell środowisku lokalnym a następnie wyświetlać wszystkie subskrypcje hello, które są połączone toohello lokalnej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8133b-145">hello following script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment and then show all hello subscriptions that are connected toohello local PowerShell session.</span></span> <span data-ttu-id="8133b-146">Zanotuj nazwę hello subskrypcji hello mają toouse podczas korzystania z tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="8133b-146">Take a note of hello name of hello subscription that you want toouse while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="8133b-147">b.</span><span class="sxs-lookup"><span data-stu-id="8133b-147">b.</span></span> <span data-ttu-id="8133b-148">toolocate i skopiuj subskrypcji nazwisko hello [portalu Azure](https://portal.azure.com), w hello menu centralnym na powitania po lewej, kliknij przycisk **subskrypcje**.</span><span class="sxs-lookup"><span data-stu-id="8133b-148">toolocate and copy your subscription name in hello [Azure portal](https://portal.azure.com), in hello Hub menu on hello left, click **Subscriptions**.</span></span> <span data-ttu-id="8133b-149">Skopiuj hello Nazwa subskrypcji mają toouse podczas uruchamiania skryptów hello w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="8133b-149">Copy hello name of subscription that you want toouse while running hello scripts in this guide.</span></span>
     
     ![Azure Portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="8133b-151">c.</span><span class="sxs-lookup"><span data-stu-id="8133b-151">c.</span></span> <span data-ttu-id="8133b-152">toolocate i skopiuj subskrypcji nazwisko hello [klasycznego portalu Azure](https://manage.windowsazure.com/), przewiń w dół i kliknij przycisk **ustawienia** na powitania po lewej stronie portalu hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-152">toolocate and copy your subscription name in hello [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="8133b-153">Kliknij przycisk **subskrypcje** toosee listę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8133b-153">Click **Subscriptions** toosee a list of your subscriptions.</span></span> <span data-ttu-id="8133b-154">Nazwa hello kopii subskrypcji, która ma toouse podczas uruchamiania skryptów hello podane w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="8133b-154">Copy hello name of subscription that you want toouse while running hello scripts given in this guide.</span></span>
     
     ![klasyczny portal Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="8133b-156">**$StorageAccountName:** Użyj hello otrzymuje nazwę w skrypcie hello, lub wprowadź nową nazwę dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-156">**$StorageAccountName:** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="8133b-157">**Ważne:** hello nazwa konta magazynu hello musi być unikatowa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="8133b-157">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="8133b-158">Musi być pisane małymi literami, zbyt!</span><span class="sxs-lookup"><span data-stu-id="8133b-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="8133b-159">**$Location:** użyć hello "Zachodnie stany USA" podany w skrypcie hello lub wybrać innych lokalizacji platformy Azure, takich jak wschodnie stany USA, Europa Północna, Europa i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="8133b-159">**$Location:** Use hello given "West US" in hello script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="8133b-160">**$ContainerName:** Użyj hello otrzymuje nazwę w skrypcie hello lub wprowadź nową nazwę dla Twojego kontenera.</span><span class="sxs-lookup"><span data-stu-id="8133b-160">**$ContainerName:** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="8133b-161">**$ImageToUpload:** wprowadź obraz tooa ścieżkę na komputerze lokalnym, na przykład: "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="8133b-161">**$ImageToUpload:** Enter a path tooa picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="8133b-162">**$DestinationFolder:** wprowadź ścieżkę tooa katalogu lokalnego toostore pliki pobierane z usługi Magazyn Azure, takich jak: "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="8133b-162">**$DestinationFolder:** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="8133b-163">Po zaktualizowaniu hello zmienne skryptu w pliku "mystoragescript.ps1" hello, kliknij przycisk **pliku** > **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="8133b-163">After updating hello script variables in hello "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="8133b-164">Następnie kliknij przycisk **debugowania** > **Uruchom** lub naciśnij klawisz **F5** toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="8133b-164">Then, click **Debug** > **Run** or press **F5** toorun hello script.</span></span>  

<span data-ttu-id="8133b-165">Po uruchomieniu skryptu hello powinien mieć folderu lokalne miejsce docelowe, który zawiera hello pobrany plik obrazu.</span><span class="sxs-lookup"><span data-stu-id="8133b-165">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="8133b-166">powitania po zrzut ekranu przedstawia przykład danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="8133b-166">hello following screenshot shows an example output:</span></span>

![Pobieranie obiektów blob](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="8133b-168">Witaj "Wprowadzenie do magazynu Azure i programu PowerShell w ciągu 5 minut" sekcji podano szybkie wprowadzenie na temat toouse programu Azure PowerShell z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8133b-168">hello "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how toouse Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="8133b-169">Aby uzyskać szczegółowe informacje i instrukcje, firma Microsoft zachęca hello tooread następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="8133b-169">For detailed information and instructions, we encourage you tooread hello following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="8133b-170">Wymagania wstępne dotyczące korzystania z programu Azure PowerShell z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8133b-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="8133b-171">Należy korzystać z platformy Azure i przystąpienie do subskrypcji toorun hello poleceń cmdlet programu PowerShell podane w tym przewodniku, zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="8133b-171">You need an Azure subscription and account toorun hello PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="8133b-172">Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet toomanage Azure za pomocą programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8133b-172">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="8133b-173">Aby uzyskać informacje na temat instalowania i konfigurowania programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8133b-173">For information on installing and setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="8133b-174">Zaleca się pobrać i zainstalować lub uaktualnić najnowsze modułu Azure PowerShell toohello przed rozpoczęciem korzystania z tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="8133b-174">We recommend that you download and install or upgrade toohello latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="8133b-175">Możesz uruchamiać polecenia cmdlet hello w konsoli środowiska Windows PowerShell standardowe hello lub hello Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="8133b-175">You can run hello cmdlets in hello standard Windows PowerShell console or hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="8133b-176">Na przykład tooopen **programu Windows PowerShell ISE**, przejdź do toohello Start menu, wpisz narzędzia administracyjne i kliknij przycisk toorun go.</span><span class="sxs-lookup"><span data-stu-id="8133b-176">For example, tooopen **Windows PowerShell ISE**, go toohello Start menu, type Administrative Tools and click toorun it.</span></span> <span data-ttu-id="8133b-177">W oknie Narzędzia administracyjne hello kliknij prawym przyciskiem myszy program Windows PowerShell ISE, kliknij polecenie Uruchom jako Administrator.</span><span class="sxs-lookup"><span data-stu-id="8133b-177">In hello Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-toomanage-storage-accounts-in-azure"></a><span data-ttu-id="8133b-178">Jak kont magazynu toomanage na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="8133b-178">How toomanage storage accounts in Azure</span></span>

<span data-ttu-id="8133b-179">Spójrzmy na zarządzanie kontami magazynu na platformie Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8133b-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-tooset-a-default-azure-subscription"></a><span data-ttu-id="8133b-180">Jak tooset domyślne subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8133b-180">How tooset a default Azure subscription</span></span>
<span data-ttu-id="8133b-181">toomanage usługi Azure Storage za pomocą programu Azure PowerShell, należy tooauthenticate środowiskiem klienta na platformie Azure przy użyciu uwierzytelniania usługi Azure Active Directory lub uwierzytelniania opartego na certyfikatach.</span><span class="sxs-lookup"><span data-stu-id="8133b-181">toomanage Azure Storage using Azure PowerShell, you need tooauthenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="8133b-182">Aby uzyskać szczegółowe informacje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) samouczka.</span><span class="sxs-lookup"><span data-stu-id="8133b-182">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="8133b-183">W tym przewodniku korzysta z uwierzytelniania usługi Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-183">This guide uses hello Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="8133b-184">W środowisku Windows PowerShell ISE wpisz następujące polecenie tooadd hello konta Azure toohello PowerShell środowisku lokalnym:</span><span class="sxs-lookup"><span data-stu-id="8133b-184">In Windows PowerShell ISE, type hello following command tooadd your Azure account toohello local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="8133b-185">W oknie "Zaloguj się za tooMicrosoft Azure" hello, wpisz adresy e-mail hello i hasło skojarzone z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="8133b-185">In hello "Sign in tooMicrosoft Azure" window, type hello email address and password associated with your account.</span></span> <span data-ttu-id="8133b-186">Azure służy do uwierzytelniania i zapisuje informacji o poświadczeniach hello, a następnie zamyka okno hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-186">Azure authenticates and saves hello credential information, and then closes hello window.</span></span>

3. <span data-ttu-id="8133b-187">Następnie uruchom następujące polecenie tooview hello Azure kont w lokalnym środowisku PowerShell i sprawdź, czy Twoje konto jest wyświetlane hello:</span><span class="sxs-lookup"><span data-stu-id="8133b-187">Next, run hello following command tooview hello Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="8133b-188">Następnie uruchom następujące polecenie cmdlet tooview hello wszystkie subskrypcje hello, które są połączone toohello lokalnej sesji programu PowerShell i sprawdź, czy subskrypcja jest wyświetlane:</span><span class="sxs-lookup"><span data-stu-id="8133b-188">Then, run hello following cmdlet tooview all hello subscriptions that are connected toohello local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="8133b-189">tooset domyślne subskrypcji platformy Azure, uruchom polecenie cmdlet hello AzureSubscription wybierz:</span><span class="sxs-lookup"><span data-stu-id="8133b-189">tooset a default Azure subscription, run hello Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="8133b-190">Sprawdź nazwę hello hello domyślne subskrypcji przy użyciu polecenia cmdlet Get-AzureSubscription hello:</span><span class="sxs-lookup"><span data-stu-id="8133b-190">Verify hello name of hello default subscription by running hello Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="8133b-191">toosee Uruchom wszystkie hello dostępne polecenia cmdlet programu PowerShell dla usługi Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="8133b-191">toosee all hello available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a><span data-ttu-id="8133b-192">Jak toocreate nowe konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="8133b-192">How toocreate a new Azure storage account</span></span>
<span data-ttu-id="8133b-193">toouse magazynu Azure, konieczne będzie konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-193">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="8133b-194">Po skonfigurowaniu subskrypcji tooyour tooconnect komputera, można utworzyć nowe konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8133b-194">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

1. <span data-ttu-id="8133b-195">Uruchom wszystkie lokalizacje dostępne datacenter hello toofind polecenia cmdlet Get-AzureLocation hello:</span><span class="sxs-lookup"><span data-stu-id="8133b-195">Run hello Get-AzureLocation cmdlet toofind all hello available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="8133b-196">Następnie przeprowadź toocreate polecenia cmdlet New-AzureStorageAccount hello nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-196">Next, run hello New-AzureStorageAccount cmdlet toocreate a new storage account.</span></span> <span data-ttu-id="8133b-197">Witaj poniższy przykład tworzy nowe konto magazynu w centrum danych "Zachodnie stany USA" hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-197">hello following example creates a new storage account in hello "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="8133b-198">Hello nazwa konta magazynu musi być unikatowa w obrębie platformy Azure i muszą być małymi literami.</span><span class="sxs-lookup"><span data-stu-id="8133b-198">hello name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="8133b-199">Ograniczenia i konwencje nazewnictwa, zobacz [o kontach magazynu Azure](../storage-create-storage-account.md) i [nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="8133b-199">For naming conventions and restrictions, see [About Azure Storage Accounts](../storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a><span data-ttu-id="8133b-200">Jak tooset domyślne konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="8133b-200">How tooset a default Azure storage account</span></span>
<span data-ttu-id="8133b-201">Może mieć wielu kont magazynu w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8133b-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="8133b-202">Można wybrać jedną z nich i ustaw go jako hello domyślne konto magazynu dla wszystkich hello magazynu polecenia w hello sama sesja programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8133b-202">You can choose one of them and set it as hello default storage account for all hello storage commands in hello same PowerShell session.</span></span> <span data-ttu-id="8133b-203">Dzięki temu możesz toorun hello Azure PowerShell magazynu polecenia bez jawne określenie hello kontekst magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-203">This enables you toorun hello Azure PowerShell storage commands without specifying hello storage context explicitly.</span></span>

1. <span data-ttu-id="8133b-204">tooset domyślne konto magazynu dla Twojej subskrypcji, możesz uruchomić polecenie cmdlet Set-AzureSubscription hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-204">tooset a default storage account for your subscription, you can run hello Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="8133b-205">Następnie przeprowadź tooverify polecenia cmdlet Get-AzureSubscription hello czy konto magazynu hello jest skojarzony z domyślnego konta subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8133b-205">Next, run hello Get-AzureSubscription cmdlet tooverify that hello storage account is associated with your default subscription account.</span></span> <span data-ttu-id="8133b-206">To polecenie zwraca hello właściwości subskrypcji na powitania bieżącej subskrypcji w tym konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-206">This command returns hello subscription properties on hello current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="8133b-207">Jak toolist magazynu Azure wszystkich kont w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8133b-207">How toolist all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="8133b-208">Każda subskrypcja platformy Azure może zawierać maksymalnie too100 kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-208">Each Azure subscription can have up too100 storage accounts.</span></span> <span data-ttu-id="8133b-209">Hello najbardziej aktualne informacje dotyczące limitów znajdują się w temacie [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="8133b-209">For hello most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="8133b-210">Uruchom następujące polecenia cmdlet toofind nazwę hello i stanu kont magazynu hello w bieżącej subskrypcji hello hello:</span><span class="sxs-lookup"><span data-stu-id="8133b-210">Run hello following cmdlet toofind out hello name and status of hello storage accounts in hello current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a><span data-ttu-id="8133b-211">Jak toocreate kontekst magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="8133b-211">How toocreate an Azure storage context</span></span>
<span data-ttu-id="8133b-212">Kontekst magazynu Azure jest obiektem w poświadczenia magazynu hello tooencapsulate programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8133b-212">Azure storage context is an object in PowerShell tooencapsulate hello storage credentials.</span></span> <span data-ttu-id="8133b-213">Używanie kontekst magazynu podczas uruchamiania każdego kolejne polecenia cmdlet umożliwia tooauthenticate możesz żądania bez jawne określenie hello konta magazynu i klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="8133b-213">Using a storage context while running any subsequent cmdlet enables you tooauthenticate your request without specifying hello storage account and its access key explicitly.</span></span> <span data-ttu-id="8133b-214">Kontekst magazynu można utworzyć na wiele sposobów, na przykład za pomocą magazynu konta nazwy i klucza dostępu, token sygnatury dostępu Współdzielonego dostępu współdzielonego, parametry połączenia lub anonimowych.</span><span class="sxs-lookup"><span data-stu-id="8133b-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="8133b-215">Aby uzyskać więcej informacji, zobacz [AzureStorageContext nowy](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="8133b-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="8133b-216">Użyj jednej z następujących trzech sposobów toocreate hello kontekst magazynu:</span><span class="sxs-lookup"><span data-stu-id="8133b-216">Use one of hello following three ways toocreate a storage context:</span></span>

* <span data-ttu-id="8133b-217">Uruchom hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind polecenia cmdlet limit klucz dostępu do magazynu podstawowego hello konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="8133b-217">Run hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind out hello primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="8133b-218">Następnie wywołaj hello [AzureStorageContext nowy](/powershell/module/azure.storage/new-azurestoragecontext) toocreate polecenia cmdlet kontekst magazynu:</span><span class="sxs-lookup"><span data-stu-id="8133b-218">Next, call hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="8133b-219">Generuj token sygnatury dostępu współdzielonego dla kontenera magazynu systemu Azure i korzystać z niego toocreate kontekst magazynu:</span><span class="sxs-lookup"><span data-stu-id="8133b-219">Generate a shared access signature token for an Azure storage container and use it toocreate a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="8133b-220">Aby uzyskać więcej informacji, zobacz [AzureStorageContainerSASToken nowy](/powershell/module/azure.storage/new-azurestoragecontainersastoken) i [przy użyciu dostępu sygnatur dostępu Współdzielonego](../storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="8133b-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="8133b-221">W niektórych przypadkach może być punktów końcowych usługi hello toospecify podczas tworzenia nowego kontekst magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-221">In some cases, you may want toospecify hello service endpoints when you create a new storage context.</span></span> <span data-ttu-id="8133b-222">Może to być konieczne, gdy zarejestrowano niestandardowej nazwy domeny dla konta magazynu z usługą Blob hello lub toouse sygnatury dostępu współdzielonego mają dostęp do zasobów magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-222">This might be necessary when you have registered a custom domain name for your storage account with hello Blob service or you want toouse a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="8133b-223">W parametrach połączenia ustawiono hello punktów końcowych usługi i użyj go toocreate nowy kontekst magazynu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="8133b-223">Set hello service endpoints in a connection string and use it toocreate a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="8133b-224">Aby uzyskać więcej informacji na temat tooconfigure parametry połączenia magazynu, zobacz [Konfigurowanie parametrów połączenia](../storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="8133b-224">For more information on how tooconfigure a storage connection string, see [Configuring Connection Strings](../storage-configure-connection-string.md).</span></span>

<span data-ttu-id="8133b-225">Teraz, możesz skonfigurować komputer i przedstawiono sposób toomanage subskrypcji i kont magazynu przy użyciu programu Azure PowerShell Przejdź dalej toolearn sekcji toohello, jak obiekty BLOB toomanage Azure i migawki obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="8133b-225">Now that you have set up your computer and learned how toomanage subscriptions and storage accounts using Azure PowerShell, go toohello next section toolearn how toomanage Azure blobs and blob snapshots.</span></span>

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="8133b-226">Jak tooretrieve i regenerate klucze magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="8133b-226">How tooretrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="8133b-227">Konto magazynu Azure ma dwa klucze konta.</span><span class="sxs-lookup"><span data-stu-id="8133b-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="8133b-228">Możesz użyć następującego polecenia cmdlet tooretrieve hello klucze.</span><span class="sxs-lookup"><span data-stu-id="8133b-228">You can use hello following cmdlet tooretrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="8133b-229">Użyj następującego polecenia cmdlet tooretrieve określonego klucza hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-229">Use hello following cmdlet tooretrieve a specific key.</span></span> <span data-ttu-id="8133b-230">Prawidłowe wartości to podstawowe i pomocnicze.</span><span class="sxs-lookup"><span data-stu-id="8133b-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="8133b-231">Jeśli chcesz tooregenerate klucze, użyj następującego polecenia cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-231">If you would like tooregenerate your keys, use hello following cmdlet.</span></span> <span data-ttu-id="8133b-232">Prawidłowe wartości właściwości KeyType - to "Primary" i "Secondary"</span><span class="sxs-lookup"><span data-stu-id="8133b-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a><span data-ttu-id="8133b-233">Jak obiekty BLOB toomanage Azure</span><span class="sxs-lookup"><span data-stu-id="8133b-233">How toomanage Azure blobs</span></span>
<span data-ttu-id="8133b-234">Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, takich jak dane tekstowe lub binarne, który można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8133b-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="8133b-235">W tej sekcji założono, że znasz już pojęcia dotyczące usługi magazynu obiektów Blob Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-235">This section assumes that you are already familiar with hello Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="8133b-236">Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob przy użyciu platformy .NET](../blobs/storage-dotnet-how-to-use-blobs.md) i [pojęcia dotyczące usługi Blob](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="8133b-236">For detailed information, see [Get started with Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-toocreate-a-container"></a><span data-ttu-id="8133b-237">Jak toocreate kontenera</span><span class="sxs-lookup"><span data-stu-id="8133b-237">How toocreate a container</span></span>
<span data-ttu-id="8133b-238">Każdy obiekt blob w magazynie Azure musi być w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="8133b-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="8133b-239">Można utworzyć za pomocą polecenia cmdlet hello AzureStorageContainer nowy kontener prywatnych:</span><span class="sxs-lookup"><span data-stu-id="8133b-239">You can create a private container using hello New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="8133b-240">Istnieją trzy poziomy anonimowy dostęp do odczytu: **poza**, **obiektu Blob**, i **kontenera**.</span><span class="sxs-lookup"><span data-stu-id="8133b-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="8133b-241">tooprevent anonimowego dostępu zbyt tooblobs, parametr uprawnienia hello zestawu**poza**.</span><span class="sxs-lookup"><span data-stu-id="8133b-241">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="8133b-242">Domyślnie nowy kontener hello jest prywatny i jest możliwy tylko przez właściciela konta hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-242">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="8133b-243">odczytu tooallow publicznego anonimowy dostęp do zasobów tooblob, ale nie toocontainer metadanych lub toohello listę obiektów blob w kontenerze hello, ustaw parametr uprawnienia hello zbyt**obiektu Blob**.</span><span class="sxs-lookup"><span data-stu-id="8133b-243">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="8133b-244">tooallow publicznego Pełny odczyt dostęp do zasobów tooblob metadanych kontenera i hello listę obiektów blob w kontenerze hello, ustaw parametr uprawnienia hello zbyt**kontenera**.</span><span class="sxs-lookup"><span data-stu-id="8133b-244">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="8133b-245">Aby uzyskać więcej informacji, zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8133b-245">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a><span data-ttu-id="8133b-246">Jak tooupload obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="8133b-246">How tooupload a blob into a container</span></span>
<span data-ttu-id="8133b-247">Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="8133b-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="8133b-248">Aby uzyskać więcej informacji, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="8133b-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="8133b-249">tooupload obiekty BLOB w kontenerze tooa, można użyć hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-249">tooupload blobs in tooa container, you can use hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="8133b-250">Domyślnie to polecenie wysyła hello lokalne pliki tooa — obiekt blob blokowy.</span><span class="sxs-lookup"><span data-stu-id="8133b-250">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="8133b-251">Typ hello toospecify hello obiektu blob, można użyć parametru - BlobType hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-251">toospecify hello type for hello blob, you can use hello -BlobType parameter.</span></span>

<span data-ttu-id="8133b-252">Witaj poniższym przykładzie uruchamiane są hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) tooget polecenia cmdlet hello wszystkie pliki w określonym folderze hello, a następnie przesyła je dalej polecenia cmdlet toohello za pomocą operatora potoku hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-252">hello following example runs hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget all hello files in hello specified folder, and then passes them toohello next cmdlet by using hello pipeline operator.</span></span> <span data-ttu-id="8133b-253">Witaj [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) kontenera tooyour pliki lokalne powitania przekazuje polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8133b-253">hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads hello local files tooyour container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a><span data-ttu-id="8133b-254">Jak toodownload obiektów blob z kontenera</span><span class="sxs-lookup"><span data-stu-id="8133b-254">How toodownload blobs from a container</span></span>
<span data-ttu-id="8133b-255">Witaj poniższy przykład pokazuje, jak toodownload obiektów blob z kontenera.</span><span class="sxs-lookup"><span data-stu-id="8133b-255">hello following example demonstrates how toodownload blobs from a container.</span></span> <span data-ttu-id="8133b-256">przykład Witaj najpierw ustanawia tooAzure połączenia magazynu przy użyciu kontekstu konta magazynu hello, w tym nazwy konta magazynu hello i jego podstawowy klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="8133b-256">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its primary access key.</span></span> <span data-ttu-id="8133b-257">Następnie przykład Witaj pobiera odwołanie do obiektu blob przy użyciu hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-257">Then, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="8133b-258">Następnie przykład Witaj używa hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) obiekty BLOB toodownload polecenia cmdlet do folderu docelowego lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="8133b-258">Next, hello example uses hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs into hello local destination folder.</span></span>

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a><span data-ttu-id="8133b-259">Jak toocopy obiektów blob z jednego tooanother kontenera magazynu</span><span class="sxs-lookup"><span data-stu-id="8133b-259">How toocopy blobs from one storage container tooanother</span></span>
<span data-ttu-id="8133b-260">Asynchronicznie należy skopiować obiekty BLOB na kontach magazynu i regionów.</span><span class="sxs-lookup"><span data-stu-id="8133b-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="8133b-261">Witaj poniższym przykładzie pokazano, jak toocopy obiektów blob z jednego magazynu tooanother kontenera w dwóch różnych kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-261">hello following example demonstrates how toocopy blobs from one storage container tooanother in two different storage accounts.</span></span> <span data-ttu-id="8133b-262">przykład Witaj najpierw ustawia zmienne dla konta magazynu źródłowego i docelowego, a następnie tworzy kontekst magazynu dla poszczególnych kont.</span><span class="sxs-lookup"><span data-stu-id="8133b-262">hello example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="8133b-263">Następnie przykład Witaj kopiuje obiekty BLOB z hello źródła kontenera toohello docelowy kontener przy użyciu hello [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-263">Next, hello example copies blobs from hello source container toohello destination container using hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="8133b-264">przykład Witaj przyjęto założenie, że konta magazynu źródłowego i docelowego hello i kontenery już istnieje.</span><span class="sxs-lookup"><span data-stu-id="8133b-264">hello example assumes that hello source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="8133b-265">Należy pamiętać, że w tym przykładzie wykonuje asynchroniczne kopiowania.</span><span class="sxs-lookup"><span data-stu-id="8133b-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="8133b-266">Możesz monitorować stan hello każdej kopii uruchamiając hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-266">You can monitor hello status of each copy by running hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-toocopy-blobs-from-a-secondary-location"></a><span data-ttu-id="8133b-267">Jak toocopy obiektów blob z lokalizacji dodatkowej</span><span class="sxs-lookup"><span data-stu-id="8133b-267">How toocopy blobs from a secondary location</span></span>
<span data-ttu-id="8133b-268">Obiekty BLOB można skopiować z lokalizacji dodatkowej hello RA-GRS włączone konta.</span><span class="sxs-lookup"><span data-stu-id="8133b-268">You can copy blobs from hello secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a><span data-ttu-id="8133b-269">Jak toodelete obiektu blob</span><span class="sxs-lookup"><span data-stu-id="8133b-269">How toodelete a blob</span></span>
<span data-ttu-id="8133b-270">toodelete obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołaj polecenie cmdlet Remove-AzureStorageBlob hello na nim.</span><span class="sxs-lookup"><span data-stu-id="8133b-270">toodelete a blob, first get a blob reference and then call hello Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="8133b-271">Poniższy przykład Hello usuwa wszystkie hello obiekty BLOB w danym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="8133b-271">hello following example deletes all hello blobs in a given container.</span></span> <span data-ttu-id="8133b-272">przykład Witaj najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-272">hello example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="8133b-273">Następnie przykład Witaj pobiera odwołanie do obiektu blob przy użyciu hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello polecenia cmdlet i działa [AzureStorageBlob Usuń](/powershell/module/azure.storage/remove-azurestorageblob) obiekty BLOB tooremove polecenia cmdlet z kontenera w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="8133b-273">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs from a container in Azure storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a><span data-ttu-id="8133b-274">Jak toomanage Azure blob migawki</span><span class="sxs-lookup"><span data-stu-id="8133b-274">How toomanage Azure blob snapshots</span></span>
<span data-ttu-id="8133b-275">Azure umożliwia tworzenie migawki obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="8133b-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="8133b-276">Migawka jest tylko do odczytu wersji obiektu blob, która jest wykonywana w punkcie w czasie.</span><span class="sxs-lookup"><span data-stu-id="8133b-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="8133b-277">Po utworzeniu migawki, to można można odczytać, kopiowane, lub usunięte, ale nie został zmodyfikowany.</span><span class="sxs-lookup"><span data-stu-id="8133b-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="8133b-278">Migawki zapewniają tooback sposób się obiektu blob znajduje się na chwilę w czasie.</span><span class="sxs-lookup"><span data-stu-id="8133b-278">Snapshots provide a way tooback up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="8133b-279">Aby uzyskać więcej informacji, zobacz [tworzenia migawki obiektu Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="8133b-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-toocreate-a-blob-snapshot"></a><span data-ttu-id="8133b-280">Jak toocreate migawki obiektu blob</span><span class="sxs-lookup"><span data-stu-id="8133b-280">How toocreate a blob snapshot</span></span>
<span data-ttu-id="8133b-281">toocreate snaphot obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać hello `ICloudBlob.CreateSnapshot` dla niego metodę.</span><span class="sxs-lookup"><span data-stu-id="8133b-281">toocreate a snaphot of a blob, first get a blob reference and then call hello `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="8133b-282">Witaj poniższym przykładzie najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-282">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="8133b-283">Następnie przykład Witaj pobiera odwołanie do obiektu blob przy użyciu hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello polecenia cmdlet i działa [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate metody migawki.</span><span class="sxs-lookup"><span data-stu-id="8133b-283">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a><span data-ttu-id="8133b-284">Jak migawki toolist obiektu blob</span><span class="sxs-lookup"><span data-stu-id="8133b-284">How toolist a blob's snapshots</span></span>
<span data-ttu-id="8133b-285">Można utworzyć dowolną liczbę migawek do obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="8133b-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="8133b-286">Możesz wyświetlić listę hello migawki skojarzone z tootrack Twojego obiektu blob z bieżącej migawki.</span><span class="sxs-lookup"><span data-stu-id="8133b-286">You can list hello snapshots associated with your blob tootrack your current snapshots.</span></span> <span data-ttu-id="8133b-287">Witaj poniższym przykładzie użyto wstępnie zdefiniowanych obiektów blob i wywołania hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) migawek hello toolist polecenia cmdlet tego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="8133b-287">hello following example uses a predefined blob and calls hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist hello snapshots of that blob.</span></span>  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a><span data-ttu-id="8133b-288">Jak toocopy migawki obiektu blob</span><span class="sxs-lookup"><span data-stu-id="8133b-288">How toocopy a snapshot of a blob</span></span>
<span data-ttu-id="8133b-289">Możesz skopiować migawki obiektu blob toorestore hello migawki.</span><span class="sxs-lookup"><span data-stu-id="8133b-289">You can copy a snapshot of a blob toorestore hello snapshot.</span></span> <span data-ttu-id="8133b-290">Aby uzyskać szczegółowe informacje i ograniczenia, zobacz [tworzenia migawki obiektu Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="8133b-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="8133b-291">Witaj poniższym przykładzie najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-291">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="8133b-292">Przykład Witaj definiuje następnie hello zmienne nazwa kontenera i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="8133b-292">Next, hello example defines hello container and blob name variables.</span></span> <span data-ttu-id="8133b-293">przykład Witaj pobiera odwołanie do obiektu blob przy użyciu hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello polecenia cmdlet i działa [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate metody migawki.</span><span class="sxs-lookup"><span data-stu-id="8133b-293">hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span> <span data-ttu-id="8133b-294">Następnie przykład Witaj uruchamia hello [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) polecenia cmdlet toocopy hello migawki obiektu blob przy użyciu obiektu ICloudBlob hello na powitania źródłowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="8133b-294">Then, hello example runs hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello snapshot of a blob using hello ICloudBlob object for hello source blob.</span></span> <span data-ttu-id="8133b-295">Należy się, że zmienne hello tooupdate zgodnie z konfiguracją przed uruchomionych przykład Witaj.</span><span class="sxs-lookup"><span data-stu-id="8133b-295">Be sure tooupdate hello variables based on your configuration before running hello example.</span></span> <span data-ttu-id="8133b-296">Należy zauważyć, że ten hello poniższy przykład przyjęto założenie, że hello źródłowego i docelowego kontenery i hello źródłowego obiektu blob już istnieje.</span><span class="sxs-lookup"><span data-stu-id="8133b-296">Note that hello following example assumes that hello source and destination containers, and hello source blob already exist.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="8133b-297">Teraz, gdy uzyskanych jak obiekty BLOB toomanage Azure i obiektów blob migawki przy użyciu programu Azure PowerShell Przejdź toohello dalej toolearn sekcji jak toomanage tabel, kolejek i plików.</span><span class="sxs-lookup"><span data-stu-id="8133b-297">Now that you have learned how toomanage Azure blobs and blob snapshots with Azure PowerShell, go toohello next section toolearn how toomanage tables, queues, and files.</span></span>

## <a name="how-toomanage-azure-tables-and-table-entities"></a><span data-ttu-id="8133b-298">Jak toomanage Azure tabele i tabela jednostek</span><span class="sxs-lookup"><span data-stu-id="8133b-298">How toomanage Azure tables and table entities</span></span>
<span data-ttu-id="8133b-299">Azure usługi Magazyn tabel jest magazynem danych NoSQL, którego można użyć toostore i zapytań dotyczących dużych zestawów strukturalnych danych nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="8133b-299">Azure Table storage service is a NoSQL datastore, which you can use toostore and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="8133b-300">głównymi składnikami usługi hello Hello są tabele, jednostki i właściwości.</span><span class="sxs-lookup"><span data-stu-id="8133b-300">hello main components of hello service are tables, entities, and properties.</span></span> <span data-ttu-id="8133b-301">Tabela jest kolekcji jednostek.</span><span class="sxs-lookup"><span data-stu-id="8133b-301">A table is a collection of entities.</span></span> <span data-ttu-id="8133b-302">Jednostka jest zbiór właściwości.</span><span class="sxs-lookup"><span data-stu-id="8133b-302">An entity is a set of properties.</span></span> <span data-ttu-id="8133b-303">Każdy obiekt może zawierać maksymalnie too252 właściwości, które są wszystkie pary nazwa wartość.</span><span class="sxs-lookup"><span data-stu-id="8133b-303">Each entity can have up too252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="8133b-304">W tej sekcji założono, że znasz już pojęcia dotyczące usługi Magazyn tabel Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-304">This section assumes that you are already familiar with hello Azure Table Storage Service concepts.</span></span> <span data-ttu-id="8133b-305">Aby uzyskać szczegółowe informacje, zobacz [hello opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx) i [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8133b-305">For detailed information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span>

<span data-ttu-id="8133b-306">Następujące podpunkty hello dowiesz się, jak usługa toomanage magazynu tabel Azure przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8133b-306">In hello following subsections, you'll learn how toomanage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="8133b-307">Witaj omówione scenariusze obejmują **tworzenie**, **usuwanie**, i **pobierania** **tabel**, jak również **Dodawanie**, **badania**, i **usuwania jednostek tabeli**.</span><span class="sxs-lookup"><span data-stu-id="8133b-307">hello scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-toocreate-a-table"></a><span data-ttu-id="8133b-308">Jak toocreate tabeli</span><span class="sxs-lookup"><span data-stu-id="8133b-308">How toocreate a table</span></span>
<span data-ttu-id="8133b-309">Każda tabela musi znajdować się na koncie magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8133b-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="8133b-310">Witaj poniższym przykładzie pokazano, jak toocreate tabeli w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8133b-310">hello following example demonstrates how toocreate a table in Azure Storage.</span></span> <span data-ttu-id="8133b-311">przykład Witaj najpierw ustanawia tooAzure połączenia magazynu przy użyciu kontekstu konta magazynu hello, w tym nazwy konta magazynu hello i jego klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="8133b-311">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="8133b-312">Następnie używa hello [AzureStorageTable nowy](/powershell/module/azure.storage/new-azurestoragetable) toocreate polecenia cmdlet tabeli w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8133b-312">Next, it uses hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate a table in Azure Storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a><span data-ttu-id="8133b-313">Jak tooretrieve tabeli</span><span class="sxs-lookup"><span data-stu-id="8133b-313">How tooretrieve a table</span></span>
<span data-ttu-id="8133b-314">Można zbadać i pobrać jednego lub wszystkich tabel na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="8133b-315">Witaj poniższym przykładzie pokazano, jak przy użyciu danej tabeli tooretrieve hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-315">hello following example demonstrates how tooretrieve a given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="8133b-316">Wywołanie polecenia cmdlet Get-AzureStorageTable hello bez żadnych parametrów, pobiera wszystkie tabele magazynu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-316">If you call hello Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-toodelete-a-table"></a><span data-ttu-id="8133b-317">Jak toodelete tabeli</span><span class="sxs-lookup"><span data-stu-id="8133b-317">How toodelete a table</span></span>
<span data-ttu-id="8133b-318">Z konta magazynu można usunąć tabeli, za pomocą hello [AzureStorageTable Usuń](/powershell/module/azure.storage/remove-azurestoragetable) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-318">You can delete a table from a storage account by using hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a><span data-ttu-id="8133b-319">Jak toomanage Tabela jednostek</span><span class="sxs-lookup"><span data-stu-id="8133b-319">How toomanage table entities</span></span>
<span data-ttu-id="8133b-320">Obecnie programu Azure PowerShell nie zapewnia bezpośrednio jednostek tabeli toomanage polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-320">Currently, Azure PowerShell does not provide cmdlets toomanage table entities directly.</span></span> <span data-ttu-id="8133b-321">tooperform operacje na jednostkach tabeli, można użyć klasy hello podany w hello [biblioteki klienta magazynu Azure dla platformy .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="8133b-321">tooperform operations on table entities, you can use hello classes given in hello [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-tooadd-table-entities"></a><span data-ttu-id="8133b-322">Jak tooadd Tabela jednostek</span><span class="sxs-lookup"><span data-stu-id="8133b-322">How tooadd table entities</span></span>
<span data-ttu-id="8133b-323">Tabela tooa jednostek tooadd najpierw utworzyć obiekt, który definiuje właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="8133b-323">tooadd an entity tooa table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="8133b-324">Jednostka może mieć właściwości too255, łącznie z 3 Właściwości systemowe: **PartitionKey**, **RowKey**, i **sygnatury czasowej**.</span><span class="sxs-lookup"><span data-stu-id="8133b-324">An entity can have up too255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="8133b-325">Jest odpowiedzialny za wstawiania i aktualizowania wartości hello **PartitionKey** i **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="8133b-325">You are responsible for inserting and updating hello values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="8133b-326">Hello podlegało zarządzaniu przez serwer wartość hello **sygnatury czasowej**, która nie może być modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="8133b-326">hello server manages hello value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="8133b-327">Razem hello **PartitionKey** i **RowKey** jednoznacznie zidentyfikować każdej jednostki w tabeli.</span><span class="sxs-lookup"><span data-stu-id="8133b-327">Together hello **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="8133b-328">**PartitionKey**: Określa jednostki hello są przechowywane w partycji hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-328">**PartitionKey**: Determines hello partition that hello entity is stored in.</span></span>
* <span data-ttu-id="8133b-329">**RowKey**: unikatowo identyfikuje hello jednostek w partycji hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-329">**RowKey**: Uniquely identifies hello entity within hello partition.</span></span>

<span data-ttu-id="8133b-330">Można zdefiniować niestandardowe właściwości too252 dla jednostki.</span><span class="sxs-lookup"><span data-stu-id="8133b-330">You may define up too252 custom properties for an entity.</span></span> <span data-ttu-id="8133b-331">Aby uzyskać więcej informacji, zobacz [hello opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="8133b-331">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="8133b-332">Witaj poniższym przykładzie pokazano, jak tooadd jednostek tooa tabeli.</span><span class="sxs-lookup"><span data-stu-id="8133b-332">hello following example demonstrates how tooadd entities tooa table.</span></span> <span data-ttu-id="8133b-333">przykład Witaj pokazuje, jak tooretrieve hello tabeli pracowników i dodać kilka podmiotów do niego.</span><span class="sxs-lookup"><span data-stu-id="8133b-333">hello example shows how tooretrieve hello employee table and add several entities into it.</span></span> <span data-ttu-id="8133b-334">Po pierwsze, nawiązaniem połączenia tooAzure magazynu przy użyciu kontekstu konta magazynu hello, w tym nazwy konta magazynu hello i jego klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="8133b-334">First, it establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="8133b-335">Następnie pobiera ona hello podanej tabeli za pomocą hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-335">Next, it retrieves hello given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="8133b-336">Jeśli hello tabela nie istnieje, hello [AzureStorageTable nowy](/powershell/module/azure.storage/new-azurestoragetable) polecenia cmdlet jest używane toocreate tabeli w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8133b-336">If hello table does not exist, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used toocreate a table in Azure Storage.</span></span> <span data-ttu-id="8133b-337">Następnie przykład Witaj definiuje funkcję niestandardowych Dodaj jednostki tooadd jednostek toohello tabeli przez określenie poszczególnych partycji i klucz wiersza.</span><span class="sxs-lookup"><span data-stu-id="8133b-337">Next, hello example defines a custom function Add-Entity tooadd entities toohello table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="8133b-338">Witaj Dodaj jednostki Witaj wywołania funkcji [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet na powitania [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) toocreate klasy do obiektu jednostki.</span><span class="sxs-lookup"><span data-stu-id="8133b-338">hello Add-Entity function calls hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class toocreate an entity object.</span></span> <span data-ttu-id="8133b-339">Później, przykład Witaj wywołuje hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) metody w tym tooadd obiekt jednostki go tooa tabeli.</span><span class="sxs-lookup"><span data-stu-id="8133b-339">Later, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object tooadd it tooa table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
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

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a><span data-ttu-id="8133b-340">Jak tooquery Tabela jednostek</span><span class="sxs-lookup"><span data-stu-id="8133b-340">How tooquery table entities</span></span>
<span data-ttu-id="8133b-341">tooquery tabelę, użyj hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="8133b-341">tooquery a table, use hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="8133b-342">Witaj poniższym przykładzie przyjęto założenie, zostały już uruchomione hello skrypt podanych w hello jak tooadd jednostek części tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="8133b-342">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="8133b-343">przykład Witaj najpierw ustanawia tooAzure połączenia magazynu przy użyciu hello kontekst magazynu, który zawiera nazwy konta magazynu hello i klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="8133b-343">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="8133b-344">Następnie próbuje tabeli hello wcześniej utworzony "pracownicy" tooretrieve przy użyciu hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-344">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="8133b-345">Wywoływanie hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet na powitania klasy Microsoft.WindowsAzure.Storage.Table.TableQuery tworzy nowy obiekt zapytania.</span><span class="sxs-lookup"><span data-stu-id="8133b-345">Calling hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="8133b-346">przykład Witaj szuka hello obiektów, które mają kolumnę 'ID', którego wartość wynosi 1, ponieważ określony w filtrze ciągu.</span><span class="sxs-lookup"><span data-stu-id="8133b-346">hello example looks for hello entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="8133b-347">Aby uzyskać szczegółowe informacje, zobacz [badania tabel i jednostek](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="8133b-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="8133b-348">Po uruchomieniu to zapytanie zwraca wszystkich jednostek spełniających kryteria filtru hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-348">When you run this query, it returns all entities that match hello filter criteria.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a><span data-ttu-id="8133b-349">Jak toodelete Tabela jednostek</span><span class="sxs-lookup"><span data-stu-id="8133b-349">How toodelete table entities</span></span>
<span data-ttu-id="8133b-350">Można usunąć jednostki przy użyciu jego kluczy partycji i wiersza.</span><span class="sxs-lookup"><span data-stu-id="8133b-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="8133b-351">Witaj poniższym przykładzie przyjęto założenie, zostały już uruchomione hello skrypt podanych w hello jak tooadd jednostek części tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="8133b-351">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="8133b-352">przykład Witaj najpierw ustanawia tooAzure połączenia magazynu przy użyciu hello kontekst magazynu, który zawiera nazwy konta magazynu hello i klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="8133b-352">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="8133b-353">Następnie próbuje tabeli hello wcześniej utworzony "pracownicy" tooretrieve przy użyciu hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-353">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="8133b-354">Jeśli istnieje tabela hello, przykład Witaj wywołuje hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve metody jednostki na podstawie jego wartości klucza partycji i wiersza.</span><span class="sxs-lookup"><span data-stu-id="8133b-354">If hello table exists, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method tooretrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="8133b-355">Przekazuj hello jednostki toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete metody.</span><span class="sxs-lookup"><span data-stu-id="8133b-355">Then, pass hello entity toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method toodelete.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a><span data-ttu-id="8133b-356">Jak toomanage Azure kolejki i wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="8133b-356">How toomanage Azure queues and queue messages</span></span>
<span data-ttu-id="8133b-357">Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8133b-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="8133b-358">W tej sekcji założono, że znasz już pojęcia dotyczące usługi magazynu kolejek Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-358">This section assumes that you are already familiar with hello Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="8133b-359">Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](../storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="8133b-359">For detailed information, see [Get started with Azure Queue storage using .NET](../storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="8133b-360">W tej sekcji opisano sposób toomanage magazynu kolejek Azure usługi przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8133b-360">This section will show you how toomanage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="8133b-361">Hello omówione scenariusze obejmują **wstawianie** i **usuwanie** kolejki komunikatów, a także **tworzenie**, **usuwanie**i **pobierania kolejek**.</span><span class="sxs-lookup"><span data-stu-id="8133b-361">hello scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-toocreate-a-queue"></a><span data-ttu-id="8133b-362">Jak toocreate kolejki</span><span class="sxs-lookup"><span data-stu-id="8133b-362">How toocreate a queue</span></span>
<span data-ttu-id="8133b-363">Witaj poniższym przykładzie najpierw ustanawia tooAzure połączenia magazynu przy użyciu kontekstu konta magazynu hello, w tym nazwy konta magazynu hello i jego klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="8133b-363">hello following example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="8133b-364">Następnie wywołuje [AzureStorageQueue nowy](/powershell/module/azure.storage/new-azurestoragequeue) toocreate polecenia cmdlet kolejki o nazwie "queuename".</span><span class="sxs-lookup"><span data-stu-id="8133b-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate a queue named 'queuename'.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="8133b-365">Aby uzyskać informacji na temat konwencji nazewnictwa dla usługi kolejek platformy Azure, zobacz [nazewnictwo kolejek i metadanych](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="8133b-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-tooretrieve-a-queue"></a><span data-ttu-id="8133b-366">Jak tooretrieve kolejki</span><span class="sxs-lookup"><span data-stu-id="8133b-366">How tooretrieve a queue</span></span>
<span data-ttu-id="8133b-367">Można zbadać i pobrać określonej kolejki, a także listę wszystkich kolejek hello na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-367">You can query and retrieve a specific queue or a list of all hello queues in a Storage account.</span></span> <span data-ttu-id="8133b-368">Witaj poniższym przykładzie pokazano, jak przy użyciu określonej kolejki tooretrieve hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-368">hello following example demonstrates how tooretrieve a specified queue using hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="8133b-369">Jeśli wywołujesz hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) polecenia cmdlet bez parametrów, pobiera listę wszystkich kolejek hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-369">If you call hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all hello queues.</span></span>

### <a name="how-toodelete-a-queue"></a><span data-ttu-id="8133b-370">Jak toodelete kolejki</span><span class="sxs-lookup"><span data-stu-id="8133b-370">How toodelete a queue</span></span>
<span data-ttu-id="8133b-371">toodelete kolejkę i wszystkie wiadomości powitania zawartych w nim polecenia cmdlet Remove-AzureStorageQueue hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="8133b-371">toodelete a queue and all hello messages contained in it, call hello Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="8133b-372">Witaj poniższy przykład pokazuje, jak przy użyciu określonej kolejki toodelete hello polecenia cmdlet Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="8133b-372">hello following example shows how toodelete a specified queue using hello Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a><span data-ttu-id="8133b-373">Jak tooinsert wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="8133b-373">How tooinsert a message into a queue</span></span>
<span data-ttu-id="8133b-374">tooinsert komunikat do istniejącej kolejki, najpierw utwórz nowe wystąpienie klasy hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="8133b-374">tooinsert a message into an existing queue, first create a new instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="8133b-375">Następnie wywołaj hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="8133b-375">Next, call hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="8133b-376">CloudQueueMessage można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="8133b-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="8133b-377">Hello poniższy przykład pokazuje, jak tooadd komunikatu tooa kolejki.</span><span class="sxs-lookup"><span data-stu-id="8133b-377">hello following example demonstrates how tooadd message tooa queue.</span></span> <span data-ttu-id="8133b-378">przykład Witaj najpierw ustanawia tooAzure połączenia magazynu przy użyciu kontekstu konta magazynu hello, w tym nazwy konta magazynu hello i jego klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="8133b-378">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="8133b-379">Następnie pobiera ona hello określonej kolejki przy użyciu hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8133b-379">Next, it retrieves hello specified queue using hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="8133b-380">Jeśli hello kolejka istnieje, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet jest używane toocreate wystąpienia hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="8133b-380">If hello queue exists, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used toocreate an instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="8133b-381">Później, przykład Witaj wywołuje hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) metody w tej wiadomości obiektu tooadd go tooa kolejki.</span><span class="sxs-lookup"><span data-stu-id="8133b-381">Later, hello example calls hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object tooadd it tooa queue.</span></span> <span data-ttu-id="8133b-382">Oto kod, który pobiera kolejki i wstawia wiadomości powitania "MessageInfo":</span><span class="sxs-lookup"><span data-stu-id="8133b-382">Here is code which retrieves a queue and inserts hello message 'MessageInfo':</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a><span data-ttu-id="8133b-383">Jak kolejki toode na powitania obok komunikatu</span><span class="sxs-lookup"><span data-stu-id="8133b-383">How toode-queue at hello next message</span></span>
<span data-ttu-id="8133b-384">Twój kod usuwa komunikat z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="8133b-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="8133b-385">Podczas wywoływania hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) metody, otrzymasz hello następnej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="8133b-385">When you call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get hello next message in a queue.</span></span> <span data-ttu-id="8133b-386">Komunikat zwrócony z **GetMessage** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="8133b-386">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="8133b-387">toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="8133b-387">toofinish removing hello message from hello queue, you must also call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="8133b-388">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="8133b-388">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="8133b-389">Twój kod wywołuje **DeleteMessage** natychmiast po przetworzeniu wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-389">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a><span data-ttu-id="8133b-390">Jak toomanage plików na platformę Azure udostępnia i pliki</span><span class="sxs-lookup"><span data-stu-id="8133b-390">How toomanage Azure file shares and files</span></span>
<span data-ttu-id="8133b-391">Magazyn plików Azure oferuje współużytkowany magazyn dla aplikacji używających standardowego protokołu SMB hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-391">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="8133b-392">Maszyny wirtualne Microsoft Azure i usługi w chmurze mogą udostępniać dane między składnikami aplikacji za pośrednictwem zainstalowanych udziałów i lokalnych aplikacji można uzyskać dostępu do danych plików w udziale za pomocą interfejsu API magazynu plików hello lub Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8133b-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via hello File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="8133b-393">Aby uzyskać więcej informacji dotyczących usługi Magazyn plików Azure, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../storage-dotnet-how-to-use-files.md) i [interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="8133b-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-tooset-and-query-storage-analytics"></a><span data-ttu-id="8133b-394">Jak tooset i zapytań analiz magazynu</span><span class="sxs-lookup"><span data-stu-id="8133b-394">How tooset and query storage analytics</span></span>
<span data-ttu-id="8133b-395">Można użyć [analityka magazynu Azure](../storage-analytics.md) toocollect metryki dla konta magazynu platformy Azure i dane dziennika o żądaniach wysyłane tooyour konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-395">You can use [Azure Storage Analytics](../storage-analytics.md) toocollect metrics for your Azure storage accounts and log data about requests sent tooyour storage account.</span></span> <span data-ttu-id="8133b-396">Można użyć magazynu metryki toomonitor hello kondycji konta magazynu oraz magazynu toodiagnose rejestrowania i rozwiązywać problemy z kontem magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-396">You can use storage metrics toomonitor hello health of a storage account, and storage logging toodiagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="8133b-397">Można skonfigurować monitorowanie za pomocą hello portalu Azure lub programu Windows PowerShell, albo programowo z użyciem biblioteki klienta usługi storage hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-397">You can configure monitoring using hello Azure portal or Windows PowerShell, or programmatically using hello storage client library.</span></span> <span data-ttu-id="8133b-398">Rejestrowanie magazynu wykonywany po stronie serwera i umożliwia toorecord szczegóły zarówno udane, jak i nieudane żądania na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-398">Storage logging happens server-side and enables you toorecord details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="8133b-399">Te dzienniki Włącz szczegóły toosee odczytu, zapisu i usuwania operacje z tabel, kolejek i obiektów blob także hello powody żądań zakończonych niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="8133b-399">These logs enable you toosee details of read, write, and delete operations against your tables, queues, and blobs as well as hello reasons for failed requests.</span></span>

<span data-ttu-id="8133b-400">toolearn tooenable i wyświetlanie danych metryk magazynu przy użyciu programu PowerShell, zobacz temat [jak tooenable metryki magazynu przy użyciu programu PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="8133b-400">toolearn how tooenable and view Storage Metrics data using PowerShell, see [How tooenable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="8133b-401">toolearn tooenable i pobrać rejestrowania magazynu danych przy użyciu programu PowerShell, zobacz temat [jak tooenable magazynu rejestrowanie przy użyciu programu PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) i [znajdowanie rejestrowania magazynu danych dziennika](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="8133b-401">toolearn how tooenable and retrieve Storage Logging data using PowerShell, see [How tooenable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="8133b-402">Aby uzyskać szczegółowe informacje na temat używania metryki magazynu i rejestrowania problemów z magazynowaniem tootroubleshoot magazynu, zobacz [monitorowanie, diagnozowanie i rozwiązywanie problemów z programem Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8133b-402">For detailed information on using Storage Metrics and Storage Logging tootroubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="8133b-403">Jak udostępnione toomanage podpis dostępu (SAS) i przechowywane zasady dostępu</span><span class="sxs-lookup"><span data-stu-id="8133b-403">How toomanage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="8133b-404">Sygnatury dostępu współdzielonego są ważnym elementem modelu zabezpieczeń powitania dla dowolnej aplikacji przy użyciu usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8133b-404">Shared access signatures are an important part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="8133b-405">Są one przydatne zapewniające tooclients konta magazynu tooyour ograniczone uprawnienia, które nie powinny mieć hello klucz konta.</span><span class="sxs-lookup"><span data-stu-id="8133b-405">They are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="8133b-406">Domyślnie obiekty BLOB, tabel i kolejek w ramach tego konta może uzyskiwać dostęp tylko jego właściciel hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8133b-406">By default, only hello owner of hello storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="8133b-407">Jeśli daną usługą lub aplikacją musi toomake Ci klienci tooother dostępne zasoby bez udostępniania klucz dostępu, dostępne są trzy opcje:</span><span class="sxs-lookup"><span data-stu-id="8133b-407">If your service or application needs toomake these resources available tooother clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="8133b-408">Ustaw kontenera uprawnienia toopermit anonimowy dostęp do odczytu toohello kontenera i jego obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="8133b-408">Set a container's permissions toopermit anonymous read access toohello container and its blobs.</span></span> <span data-ttu-id="8133b-409">Jest to niedozwolone dla tabel lub kolejek.</span><span class="sxs-lookup"><span data-stu-id="8133b-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="8133b-410">Użyj sygnatury dostępu współdzielonego przyznająca toocontainers praw dostępu ograniczonego, obiekty BLOB, kolejek i tabel dla określonego interwału.</span><span class="sxs-lookup"><span data-stu-id="8133b-410">Use a shared access signature that grants restricted access rights toocontainers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="8133b-411">Użyj tooobtain zasad dostępu do przechowywanych dodatkowy poziom kontroli nad sygnatur dostępu współdzielonego dla kontenera lub jego obiektów blob, kolejki lub tabeli.</span><span class="sxs-lookup"><span data-stu-id="8133b-411">Use a stored access policy tooobtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="8133b-412">Witaj przechowywanych zasada dostępu zezwala na możesz czas rozpoczęcia hello toochange, czas wygaśnięcia lub uprawnień do podpisu, lub toorevoke po nim został wydany.</span><span class="sxs-lookup"><span data-stu-id="8133b-412">hello stored access policy allows you toochange hello start time, expiry time, or permissions for a signature, or toorevoke it after it has been issued.</span></span>

<span data-ttu-id="8133b-413">Sygnatury dostępu współdzielonego, można w jednym z dwóch formach:</span><span class="sxs-lookup"><span data-stu-id="8133b-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="8133b-414">**Ad hoc SAS**: podczas tworzenia sygnatury dostępu Współdzielonego ad hoc, godzina rozpoczęcia hello, czas wygaśnięcia i uprawnienia dla hello SAS są określone na powitania identyfikatora URI połączenia SAS.</span><span class="sxs-lookup"><span data-stu-id="8133b-414">**Ad hoc SAS**: When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span> <span data-ttu-id="8133b-415">Ten typ sygnatury dostępu Współdzielonego może zostać utworzony w kontenerze, obiektów blob, tabeli lub kolejki i jest z systemem innym niż odwoływalny.</span><span class="sxs-lookup"><span data-stu-id="8133b-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="8133b-416">**Sygnatury dostępu Współdzielonego z zasadami dostępu do przechowywanych**: zasady dostępu do przechowywanych jest zdefiniowany w kontenerze zasobu kontenera obiektów blob, tabel lub kolejek — i umożliwia toomanage ograniczenia dla co najmniej jeden sygnatur dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="8133b-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="8133b-417">Po skojarzeniu sygnatury dostępu Współdzielonego za pomocą zasad dostępu przechowywane, hello SAS dziedziczy ograniczenia hello — uprawnienia - zdefiniowane zasady dostępu hello przechowywane, czas wygaśnięcia i godzina rozpoczęcia hello.</span><span class="sxs-lookup"><span data-stu-id="8133b-417">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span> <span data-ttu-id="8133b-418">Ten typ sygnatury dostępu Współdzielonego jest odwoływalny.</span><span class="sxs-lookup"><span data-stu-id="8133b-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="8133b-419">Aby uzyskać więcej informacji, zobacz [przy użyciu dostępu sygnatur dostępu Współdzielonego](../storage-dotnet-shared-access-signature-part-1.md) i [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8133b-419">For more information, see [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="8133b-420">W kolejnych sekcjach hello przedstawiono sposób toocreate zasady dostępu współdzielonego podpisu tokenu i przechowywane dostęp do tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="8133b-420">In hello next sections, you will learn how toocreate a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="8133b-421">Program Azure PowerShell udostępnia podobne polecenia cmdlet dla kontenerów, obiektów blob i kolejek oraz.</span><span class="sxs-lookup"><span data-stu-id="8133b-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="8133b-422">skrypty hello toorun w tej sekcji, Pobierz hello [Azure PowerShell w wersji 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="8133b-422">toorun hello scripts in this section, download hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="8133b-423">Jak token sygnatura dostępu współdzielonego toocreate oparta na zasadach</span><span class="sxs-lookup"><span data-stu-id="8133b-423">How toocreate a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="8133b-424">Użyj toocreate polecenia cmdlet New-AzureStorageTableStoredAccessPolicy hello Nowa zasada dostępu przechowywane.</span><span class="sxs-lookup"><span data-stu-id="8133b-424">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy.</span></span> <span data-ttu-id="8133b-425">Następnie wywołaj metodę hello [AzureStorageTableSASToken nowy](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate polecenia cmdlet nowy token podpisu na podstawie zasad dostępu współdzielonego dla tabeli magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="8133b-425">Then, call hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="8133b-426">Jak toocreate token ad hoc sygnatura dostępu współdzielonego (z systemem innym niż — odwoływalny)</span><span class="sxs-lookup"><span data-stu-id="8133b-426">How toocreate an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="8133b-427">Użyj hello [AzureStorageTableSASToken nowy](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate polecenia cmdlet nowy ad hoc (z systemem innym niż — odwoływalny) Sygnatura dostępu współdzielonego token dla tabeli magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="8133b-427">Use hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a><span data-ttu-id="8133b-428">Jak toocreate zasad dostępu przechowywane</span><span class="sxs-lookup"><span data-stu-id="8133b-428">How toocreate a stored access policy</span></span>
<span data-ttu-id="8133b-429">Użyj hello AzureStorageTableStoredAccessPolicy nowe polecenia cmdlet toocreate Nowa zasada dostępu przechowywanych dla tabeli magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="8133b-429">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a><span data-ttu-id="8133b-430">Jak tooupdate zasad dostępu przechowywane</span><span class="sxs-lookup"><span data-stu-id="8133b-430">How tooupdate a stored access policy</span></span>
<span data-ttu-id="8133b-431">Użyj tooupdate polecenia cmdlet Set-AzureStorageTableStoredAccessPolicy hello istniejących zasad dostępu do przechowywanych dla tabeli magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="8133b-431">Use hello Set-AzureStorageTableStoredAccessPolicy cmdlet tooupdate an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a><span data-ttu-id="8133b-432">Jak toodelete zasad dostępu przechowywane</span><span class="sxs-lookup"><span data-stu-id="8133b-432">How toodelete a stored access policy</span></span>
<span data-ttu-id="8133b-433">Użyj toodelete polecenia cmdlet Remove-AzureStorageTableStoredAccessPolicy hello zasad dostępu do przechowywanych w tabeli magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="8133b-433">Use hello Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="8133b-434">Jak toouse magazynu Azure dla instytucji rządowych USA i Chińskiej wersji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8133b-434">How toouse Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="8133b-435">Środowiska platformy Azure jest niezależnie od wdrożenia programu Microsoft Azure, takich jak [Azure dla instytucji rządowych USA administracji](https://azure.microsoft.com/features/gov/), [AzureCloud globalne Azure](https://portal.azure.com), i [AzureChinaCloud dla platformy Azure obsługiwane przez 21Vianet w Chinach](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="8133b-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="8133b-436">Można wdrażać nowe środowisk Azure dla instytucji rządowych USA i Chińskiej wersji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8133b-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="8133b-437">toouse magazynu Azure z AzureChinaCloud należy toocreate kontekst magazynu, który jest skojarzony z AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="8133b-437">toouse Azure Storage with AzureChinaCloud, you need toocreate a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="8133b-438">Wykonaj te kroki tooget, możesz uruchomić:</span><span class="sxs-lookup"><span data-stu-id="8133b-438">Follow these steps tooget you started:</span></span>

1. <span data-ttu-id="8133b-439">Uruchom hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee polecenia cmdlet hello dostępnego środowiska platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="8133b-439">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="8133b-440">Dodaj tooWindows konta chińskiej wersji platformy Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8133b-440">Add an Azure China account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="8133b-441">Tworzenie magazynu kontekstu konta AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="8133b-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="8133b-442">toouse usługi Azure Storage z [stany USA Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), należy zdefiniować nowe środowisko i następnie tworzy nowy kontekst magazynu z tym środowiskiem:</span><span class="sxs-lookup"><span data-stu-id="8133b-442">toouse Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="8133b-443">Uruchom hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee polecenia cmdlet hello dostępnego środowiska platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="8133b-443">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="8133b-444">Dodaj tooWindows konta Azure instytucji rządowych Stanów Zjednoczonych środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8133b-444">Add an Azure US Government account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="8133b-445">Tworzenie magazynu kontekstu konta AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="8133b-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="8133b-446">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="8133b-446">For more information, see:</span></span>

* <span data-ttu-id="8133b-447">[Przewodnik dewelopera usługi Microsoft Azure dla instytucji rządowych](../../azure-government/documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="8133b-447">[Microsoft Azure Government Developer Guide](../../azure-government/documentation-government-developer-guide.md).</span></span>
* [<span data-ttu-id="8133b-448">Omówienie różnic podczas tworzenia aplikacji w usłudze Chin</span><span class="sxs-lookup"><span data-stu-id="8133b-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="8133b-449">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8133b-449">Next Steps</span></span>
<span data-ttu-id="8133b-450">W tym przewodniku, kiedy znasz już jak toomanage usługi Azure Storage przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8133b-450">In this guide, you've learned how toomanage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="8133b-451">Poniżej przedstawiono niektóre pokrewne artykuły i zasoby dowiedzieć się więcej o nich.</span><span class="sxs-lookup"><span data-stu-id="8133b-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="8133b-452">Dokumentacja usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8133b-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="8133b-453">Polecenia cmdlet programu PowerShell usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8133b-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="8133b-454">Dokumentacja programu PowerShell systemu Windows</span><span class="sxs-lookup"><span data-stu-id="8133b-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
