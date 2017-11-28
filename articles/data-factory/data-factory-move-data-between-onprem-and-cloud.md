---
title: "Przenoszenie danych - brama zarządzania danymi | Dokumentacja firmy Microsoft"
description: "Skonfiguruj bramę danych do przenoszenia danych między firmą i chmurą. Użyj bramy zarządzania danymi w fabryce danych Azure, aby przenieść dane."
keywords: "Brama danych, integracja danych przenoszenia danych, poświadczeń bramy"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 565091e24a8c0009793e2e2365fb95013cad5028
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-between-on-premises-sources-and-the-cloud-with-data-management-gateway"></a><span data-ttu-id="91ac4-105">Przenoszenie danych między lokalnych źródeł i w chmurze z brama zarządzania danymi</span><span class="sxs-lookup"><span data-stu-id="91ac4-105">Move data between on-premises sources and the cloud with Data Management Gateway</span></span>
<span data-ttu-id="91ac4-106">Ten artykuł zawiera omówienie integrację danych lokalnych magazynów danych i magazyny danych chmury przy użyciu fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="91ac4-107">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu i innych danych fabryki podstawowe pojęcia dotyczące artykułów: [zestawów danych](data-factory-create-datasets.md) i [potoki](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="91ac4-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="91ac4-108">Brama zarządzania danymi</span><span class="sxs-lookup"><span data-stu-id="91ac4-108">Data Management Gateway</span></span>
<span data-ttu-id="91ac4-109">Brama zarządzania danymi należy zainstalować na komputerze lokalnym umożliwia przenoszenie danych z lokalnego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-109">You must install Data Management Gateway on your on-premises machine to enable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="91ac4-110">Bramę można zainstalować na tym samym komputerze co magazyn danych lub na innym komputerze tak długo, jak bramy można nawiązać połączenia z magazynem danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-110">The gateway can be installed on the same machine as the data store or on a different machine as long as the gateway can connect to the data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91ac4-111">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="91ac4-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="91ac4-112">Poniższe wskazówki opisano tworzenie fabryki danych z potok, który przenosi dane z lokalnymi **programu SQL Server** bazy danych do magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="91ac4-112">The following walkthrough shows you how to create a data factory with a pipeline that moves data from an on-premises **SQL Server** database to an Azure blob storage.</span></span> <span data-ttu-id="91ac4-113">W ramach tego przewodnika zainstalujesz i skonfigurujesz bramę zarządzania danymi na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="91ac4-113">As part of the walkthrough, you install and configure the Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-to-cloud"></a><span data-ttu-id="91ac4-114">Wskazówki: kopiowanie danych lokalnych do chmury</span><span class="sxs-lookup"><span data-stu-id="91ac4-114">Walkthrough: copy on-premises data to cloud</span></span>
<span data-ttu-id="91ac4-115">W tym przewodniku możesz wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="91ac4-115">In this walkthrough you do the following steps:</span></span> 

1. <span data-ttu-id="91ac4-116">Tworzenie fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-116">Create a data factory.</span></span>
2. <span data-ttu-id="91ac4-117">Tworzenie bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="91ac4-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="91ac4-118">Tworzenie połączonej usługi dla źródłowy i odbiorczy magazynów danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="91ac4-119">Tworzenie zestawów danych do reprezentowania danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-119">Create datasets to represent input and output data.</span></span>
5. <span data-ttu-id="91ac4-120">Utworzyć potok z działaniem kopiowania przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-120">Create a pipeline with a copy activity to move the data.</span></span>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="91ac4-121">Wymagania wstępne dotyczące samouczka</span><span class="sxs-lookup"><span data-stu-id="91ac4-121">Prerequisites for the tutorial</span></span>
<span data-ttu-id="91ac4-122">Przed rozpoczęciem tego przewodnika, musi mieć następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="91ac4-122">Before you begin this walkthrough, you must have the following prerequisites:</span></span>

* <span data-ttu-id="91ac4-123">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-123">**Azure subscription**.</span></span>  <span data-ttu-id="91ac4-124">Jeśli nie masz subskrypcji, możesz utworzyć konto bezpłatnej wersji próbnej w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="91ac4-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="91ac4-125">Zobacz [bezpłatnej wersji próbnej](http://azure.microsoft.com/pricing/free-trial/) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="91ac4-125">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="91ac4-126">**Konto magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-126">**Azure Storage Account**.</span></span> <span data-ttu-id="91ac4-127">Użyj magazynu obiektów blob jako **docelowego/ujście** magazynu danych, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="91ac4-127">You use the blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="91ac4-128">Jeśli nie masz konta magazynu platformy Azure, zobacz [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykułu kroki go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="91ac4-128">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="91ac4-129">**Program SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-129">**SQL Server**.</span></span> <span data-ttu-id="91ac4-130">Użyj bazy danych programu SQL Server lokalnego jako **źródła** magazynu danych, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="91ac4-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="91ac4-131">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="91ac4-131">Create data factory</span></span>
<span data-ttu-id="91ac4-132">W tym kroku, użyj portalu Azure można utworzyć wystąpienia fabryki danych Azure o nazwie **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-132">In this step, you use the Azure portal to create an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="91ac4-133">Zaloguj się do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91ac4-133">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="91ac4-134">Kliknij przycisk **+ nowy**, kliknij przycisk **analizy i analiza**i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Nowy-> Fabryka danych](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="91ac4-136">W **nowa fabryka danych** wprowadź **ADFTutorialOnPremDF** dla nazwy.</span><span class="sxs-lookup"><span data-stu-id="91ac4-136">In the **New data factory** page, enter **ADFTutorialOnPremDF** for the Name.</span></span>

    ![Dodawanie do tablicy startowej](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="91ac4-138">Nazwa fabryki danych Azure musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="91ac4-138">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="91ac4-139">Jeśli zostanie wyświetlony błąd: **nazwa fabryki danych "ADFTutorialOnPremDF" nie jest dostępna**, Zmień nazwę fabryki danych (na przykład yournameADFTutorialOnPremDF) i spróbuj ponownie utworzyć.</span><span class="sxs-lookup"><span data-stu-id="91ac4-139">If you receive the error: **Data factory name “ADFTutorialOnPremDF” is not available**, change the name of the data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="91ac4-140">Użyj tej nazwy, zamiast ADFTutorialOnPremDF podczas wykonywania pozostałych czynności w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="91ac4-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="91ac4-141">W przyszłości nazwa fabryki danych może zostać zarejestrowana jako nazwa **DNS**, a wówczas stanie się widoczna publicznie.</span><span class="sxs-lookup"><span data-stu-id="91ac4-141">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="91ac4-142">Wybierz **subskrypcję Azure**, w ramach której chcesz utworzyć fabrykę danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-142">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="91ac4-143">Wybierz istniejącą **grupę zasobów** lub utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="91ac4-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="91ac4-144">Samouczek, Utwórz grupę zasobów o nazwie: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-144">For the tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="91ac4-145">Kliknij przycisk **Utwórz** na **nowa fabryka danych** strony.</span><span class="sxs-lookup"><span data-stu-id="91ac4-145">Click **Create** on the **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="91ac4-146">Aby utworzyć wystąpienia usługi Data Factory, użytkownik musi być członkiem roli [współautora usługi Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) na poziomie subskrypcji/grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="91ac4-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="91ac4-147">Po zakończeniu tworzenia zobacz **fabryki danych** strony, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="91ac4-147">After creation is complete, you see the **Data Factory** page as shown in the following image:</span></span>

   ![Strona główna fabryki danych](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="91ac4-149">Tworzenie bramy</span><span class="sxs-lookup"><span data-stu-id="91ac4-149">Create gateway</span></span>
1. <span data-ttu-id="91ac4-150">W **fabryki danych** kliknij przycisk **tworzenie i wdrażanie** Kafelek, aby uruchomić **edytor** dla fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-150">In the **Data Factory** page, click **Author and deploy** tile to launch the **Editor** for the data factory.</span></span>

    ![Kafelek Utwórz i wdróż](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="91ac4-152">W edytorze fabryki danych, kliknij polecenie **... Więcej** na pasku narzędzi, a następnie kliknij przycisk **nowej bramy danych**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-152">In the Data Factory Editor, click **... More** on the toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="91ac4-153">Alternatywnie możesz kliknąć prawym przyciskiem myszy **bram danych** w widoku drzewa, a następnie kliknij przycisk **nowej bramy danych**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-153">Alternatively, you can right-click **Data Gateways** in the tree view, and click **New data gateway**.</span></span>

   ![Nową bramę danych na pasku narzędzi](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="91ac4-155">W **Utwórz** wprowadź **adftutorialgateway** dla **nazwa**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-155">In the **Create** page, enter **adftutorialgateway** for the **name**, and click **OK**.</span></span>     

    ![Utwórz stronę bramy](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="91ac4-157">W tym przewodniku utworzysz logicznej bramy z tylko jednym węzłem (komputera lokalnego systemu Windows).</span><span class="sxs-lookup"><span data-stu-id="91ac4-157">In this walkthrough, you create the logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="91ac4-158">Możesz skalować w poziomie bramy zarządzania danymi można skojarzyć wielu lokalnymi maszynami z bramą.</span><span class="sxs-lookup"><span data-stu-id="91ac4-158">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="91ac4-159">Możesz skalować w górę zwiększając liczbę zadań przepływu danych, które można uruchomić jednocześnie w węźle.</span><span class="sxs-lookup"><span data-stu-id="91ac4-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="91ac4-160">Ta funkcja jest również dostępny do logicznego bramy z jednego węzła.</span><span class="sxs-lookup"><span data-stu-id="91ac4-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="91ac4-161">Zobacz [skalowanie brama zarządzania danymi w fabryce danych Azure](data-factory-data-management-gateway-high-availability-scalability.md) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="91ac4-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="91ac4-162">W **Konfiguruj** kliknij przycisk **Zainstaluj bezpośrednio na tym komputerze**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-162">In the **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="91ac4-163">Ta akcja spowoduje pobranie pakietu instalacyjnego bramy, instaluje konfiguruje i rejestruje bramy na komputerze.</span><span class="sxs-lookup"><span data-stu-id="91ac4-163">This action downloads the installation package for the gateway, installs, configures, and registers the gateway on the computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="91ac4-164">Użyj programu Internet Explorer lub przeglądarki sieci web zgodne Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="91ac4-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="91ac4-165">Jeśli używasz przeglądarki Chrome, przejdź do [sklepu internetowego Chrome](https://chrome.google.com/webstore/), wyszukaj słowo kluczowe „ClickOnce”, wybierz jedno z rozszerzeń ClickOnce i je zainstaluj.</span><span class="sxs-lookup"><span data-stu-id="91ac4-165">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="91ac4-166">Wykonaj te same czynności dla przeglądarki Firefox (Instalowanie dodatku).</span><span class="sxs-lookup"><span data-stu-id="91ac4-166">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="91ac4-167">Kliknij przycisk **Otwórz Menu** przycisk na pasku narzędzi (**trzy poziome linie** w prawym górnym rogu), kliknij przycisk **dodatki**, wyszukaj ze słowem kluczowym "ClickOnce", wybierz jedną z Rozszerzenia ClickOnce, a następnie zainstaluj go.</span><span class="sxs-lookup"><span data-stu-id="91ac4-167">Click **Open Menu** button on the toolbar (**three horizontal lines** in the top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Brama — Konfigurowanie strony](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="91ac4-169">W ten sposób jest najprostszym sposobem (jednym kliknięciem), aby pobrać, zainstalować, skonfigurować i zarejestrować bramę w jeden pojedynczy krok.</span><span class="sxs-lookup"><span data-stu-id="91ac4-169">This way is the easiest way (one-click) to download, install, configure, and register the gateway in one single step.</span></span> <span data-ttu-id="91ac4-170">Widać **Menedżera konfiguracji bramy zarządzania danymi firmy Microsoft** aplikacja jest zainstalowana na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="91ac4-170">You can see the **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="91ac4-171">Możesz również znaleźć pliku wykonywalnego **ConfigManager.exe** w folderze: **C:\Program Files\Microsoft danych zarządzania Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-171">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="91ac4-172">Można również pobrać i zainstalować bramę ręcznie przy użyciu łącza na tej stronie i zarejestrowanie go za pomocą klucza wyświetlany w **nowy klucz** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="91ac4-172">You can also download and install gateway manually by using the links in this page and register it using the key shown in the **NEW KEY** text box.</span></span>

    <span data-ttu-id="91ac4-173">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu wszystkie szczegóły dotyczące bramy.</span><span class="sxs-lookup"><span data-stu-id="91ac4-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="91ac4-174">Musi być administratorem na komputerze lokalnym do instalowania i konfigurowania bramy zarządzania danymi pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="91ac4-174">You must be an administrator on the local computer to install and configure the Data Management Gateway successfully.</span></span> <span data-ttu-id="91ac4-175">Można dodać użytkowników do **użytkownicy bramy zarządzania danymi** lokalnej grupy systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="91ac4-175">You can add additional users to the **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="91ac4-176">Członkowie tej grupy można użyć narzędzia Menedżera konfiguracji bramy zarządzania danymi, aby skonfigurować bramę.</span><span class="sxs-lookup"><span data-stu-id="91ac4-176">The members of this group can use the Data Management Gateway Configuration Manager tool to configure the gateway.</span></span>
   >
   >
5. <span data-ttu-id="91ac4-177">Poczekaj kilka minut lub poczekaj, aż zostanie wyświetlony następujący komunikat powiadomienia:</span><span class="sxs-lookup"><span data-stu-id="91ac4-177">Wait for a couple of minutes or wait until you see the following notification message:</span></span>

    ![Pomyślnie zainstalowano bramy](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="91ac4-179">Uruchom **Menedżera konfiguracji bramy zarządzania danymi** aplikacji na komputerze.</span><span class="sxs-lookup"><span data-stu-id="91ac4-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="91ac4-180">W **wyszukiwania** wpisz **brama zarządzania danymi** można uzyskać dostępu do tego narzędzia.</span><span class="sxs-lookup"><span data-stu-id="91ac4-180">In the **Search** window, type **Data Management Gateway** to access this utility.</span></span> <span data-ttu-id="91ac4-181">Możesz również znaleźć pliku wykonywalnego **ConfigManager.exe** w folderze: **C:\Program Files\Microsoft danych zarządzania Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="91ac4-181">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Menedżer konfiguracji bramy](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="91ac4-183">Upewnij się, że widoczny `adftutorialgateway is connected to the cloud service` wiadomości.</span><span class="sxs-lookup"><span data-stu-id="91ac4-183">Confirm that you see `adftutorialgateway is connected to the cloud service` message.</span></span> <span data-ttu-id="91ac4-184">Pasek Wyświetla dolnej stanu **podłączone do usługi w chmurze** wraz z **zielony znacznik wyboru**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-184">The status bar the bottom displays **Connected to the cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="91ac4-185">Na **Home** karcie, możesz również wykonać następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="91ac4-185">On the **Home** tab, you can also do the following operations:</span></span>

   * <span data-ttu-id="91ac4-186">**Zarejestruj** bramy przy użyciu klucza z portalu Azure za pomocą przycisku Zarejestruj.</span><span class="sxs-lookup"><span data-stu-id="91ac4-186">**Register** a gateway with a key from the Azure portal by using the Register button.</span></span>
   * <span data-ttu-id="91ac4-187">**Zatrzymaj** usługa hosta bramy zarządzania danymi na komputerze bramy.</span><span class="sxs-lookup"><span data-stu-id="91ac4-187">**Stop** the Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="91ac4-188">**Zaplanuj aktualizacje** do zainstalowania w określonym czasie dnia.</span><span class="sxs-lookup"><span data-stu-id="91ac4-188">**Schedule updates** to be installed at a specific time of the day.</span></span>
   * <span data-ttu-id="91ac4-189">Widoku, gdy brama została **ostatniej aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-189">View when the gateway was **last updated**.</span></span>
   * <span data-ttu-id="91ac4-190">Określ czas, w którym można zainstalować aktualizacji z bramą.</span><span class="sxs-lookup"><span data-stu-id="91ac4-190">Specify time at which an update to the gateway can be installed.</span></span>
8. <span data-ttu-id="91ac4-191">Przełącz się do **ustawienia** kartę. Certyfikatu podanego w **certyfikatu** sekcja jest używana do szyfrowania/odszyfrowywania poświadczeń magazynu danych lokalnych, określonym przez użytkownika w portalu.</span><span class="sxs-lookup"><span data-stu-id="91ac4-191">Switch to the **Settings** tab. The certificate specified in the **Certificate** section is used to encrypt/decrypt credentials for the on-premises data store that you specify on the portal.</span></span> <span data-ttu-id="91ac4-192">(opcjonalnie) Kliknij przycisk **zmiany** zamiast tego użyć własnego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="91ac4-192">(optional) Click **Change** to use your own certificate instead.</span></span> <span data-ttu-id="91ac4-193">Domyślnie bramy, używa certyfikatu, który został wygenerowany automatycznie przez usługę fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-193">By default, the gateway uses the certificate that is auto-generated by the Data Factory service.</span></span>

    ![Konfiguracja certyfikatu bramy](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="91ac4-195">Możesz również wykonać następujące czynności na **ustawienia** karty:</span><span class="sxs-lookup"><span data-stu-id="91ac4-195">You can also do the following actions on the **Settings** tab:</span></span>

   * <span data-ttu-id="91ac4-196">Umożliwia wyświetlanie i wyeksportuj certyfikat używany przez bramę.</span><span class="sxs-lookup"><span data-stu-id="91ac4-196">View or export the certificate being used by the gateway.</span></span>
   * <span data-ttu-id="91ac4-197">Zmień punkt końcowy HTTPS używany przez bramę.</span><span class="sxs-lookup"><span data-stu-id="91ac4-197">Change the HTTPS endpoint used by the gateway.</span></span>    
   * <span data-ttu-id="91ac4-198">Ustaw serwer proxy HTTP do użycia przez bramę.</span><span class="sxs-lookup"><span data-stu-id="91ac4-198">Set an HTTP proxy to be used by the gateway.</span></span>     
9. <span data-ttu-id="91ac4-199">(opcjonalnie) Przełącz się do **diagnostyki** karcie wyboru **Włącz pełne rejestrowanie** opcję, jeśli chcesz włączyć pełne rejestrowanie, służącego do rozwiązywania problemów z bramą.</span><span class="sxs-lookup"><span data-stu-id="91ac4-199">(optional) Switch to the **Diagnostics** tab, check the **Enable verbose logging** option if you want to enable verbose logging that you can use to troubleshoot any issues with the gateway.</span></span> <span data-ttu-id="91ac4-200">Rejestrowanie informacji można znaleźć w **Podgląd zdarzeń** w obszarze **Dzienniki aplikacji i usług** -> **brama zarządzania danymi** węzła.</span><span class="sxs-lookup"><span data-stu-id="91ac4-200">The logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Karta diagnostyki](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="91ac4-202">Można również wykonywać następujące czynności w **diagnostyki** karty:</span><span class="sxs-lookup"><span data-stu-id="91ac4-202">You can also perform the following actions in the **Diagnostics** tab:</span></span>

   * <span data-ttu-id="91ac4-203">Użyj **Testuj połączenie** sekcji do lokalnego źródła danych przy użyciu bramy.</span><span class="sxs-lookup"><span data-stu-id="91ac4-203">Use **Test Connection** section to an on-premises data source using the gateway.</span></span>
   * <span data-ttu-id="91ac4-204">Kliknij przycisk **Wyświetl dzienniki** Aby wyświetlić dziennik brama zarządzania danymi w oknie Podgląd zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="91ac4-204">Click **View Logs** to see the Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="91ac4-205">Kliknij przycisk **Wyślij dzienniki** można przekazać do firmy Microsoft w celu ułatwienia rozwiązywania problemów z problemów związanych z pliku zip z dziennikami ostatnich siedmiu dni.</span><span class="sxs-lookup"><span data-stu-id="91ac4-205">Click **Send Logs** to upload a zip file with logs of last seven days to Microsoft to facilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="91ac4-206">Na **diagnostyki** karcie **Testuj połączenie** zaznacz **SqlServer** dla typu źródła danych, wprowadź nazwę serwera bazy danych, nazwę bazy danych, Określ typ uwierzytelniania, wprowadź nazwę użytkownika i hasło, a następnie kliknij przycisk **Test** Aby sprawdzić, czy brama można połączyć z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-206">On the **Diagnostics** tab, in the **Test Connection** section, select **SqlServer** for the type of the data store, enter the name of the database server, name of the database, specify authentication type, enter user name, and password, and click **Test** to test whether the gateway can connect to the database.</span></span>
11. <span data-ttu-id="91ac4-207">Przełącz się do przeglądarki sieci web, a w **portalu Azure**, kliknij przycisk **OK** na **Konfiguruj** strony, a następnie na **nowej bramy danych** strony.</span><span class="sxs-lookup"><span data-stu-id="91ac4-207">Switch to the web browser, and in the **Azure portal**, click **OK** on the **Configure** page and then on the **New data gateway** page.</span></span>
12. <span data-ttu-id="91ac4-208">Powinny pojawić się **adftutorialgateway** w obszarze **bram danych** w widoku drzewa po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="91ac4-208">You should see **adftutorialgateway** under **Data Gateways** in the tree view on the left.</span></span>  <span data-ttu-id="91ac4-209">Jeśli klikniesz przycisk, powinna zostać wyświetlona skojarzone JSON.</span><span class="sxs-lookup"><span data-stu-id="91ac4-209">If you click it, you should see the associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="91ac4-210">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="91ac4-210">Create linked services</span></span>
<span data-ttu-id="91ac4-211">W tym kroku, Utwórz dwie połączonej usługi: **AzureStorageLinkedService** i **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="91ac4-212">**SqlServerLinkedService** łączy lokalną bazą danych programu SQL Server i **AzureStorageLinkedService** połączonej usługi łączy magazynu obiektów blob platformy Azure z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-212">The **SqlServerLinkedService** links an on-premises SQL Server database and the **AzureStorageLinkedService** linked service links an Azure blob store to the data factory.</span></span> <span data-ttu-id="91ac4-213">Możesz utworzyć potok w dalszej części tego przewodnika, który kopiuje dane z lokalną bazą danych programu SQL Server do magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="91ac4-213">You create a pipeline later in this walkthrough that copies data from the on-premises SQL Server database to the Azure blob store.</span></span>

#### <a name="add-a-linked-service-to-an-on-premises-sql-server-database"></a><span data-ttu-id="91ac4-214">Dodaj połączonej usługi do lokalnej bazy danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="91ac4-214">Add a linked service to an on-premises SQL Server database</span></span>
1. <span data-ttu-id="91ac4-215">W **Edytor fabryki danych**, kliknij przycisk **nowy magazyn danych** na pasku narzędzi i wybierz **programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-215">In the **Data Factory Editor**, click **New data store** on the toolbar and select **SQL Server**.</span></span>

   ![Nowa usługa SQL Server połączone](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="91ac4-217">W **edytora JSON** po prawej stronie, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="91ac4-217">In the **JSON editor** on the right, do the following steps:</span></span>

   1. <span data-ttu-id="91ac4-218">Aby uzyskać **gatewayName**, określ **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-218">For the **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="91ac4-219">W **connectionString**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="91ac4-219">In the **connectionString**, do the following steps:</span></span>    

      1. <span data-ttu-id="91ac4-220">Aby uzyskać **servername**, wprowadź nazwę serwera, który jest hostem bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="91ac4-220">For **servername**, enter the name of the server that hosts the SQL Server database.</span></span>
      2. <span data-ttu-id="91ac4-221">Aby uzyskać **databasename**, wprowadź nazwę bazy danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-221">For **databasename**, enter the name of the database.</span></span>
      3. <span data-ttu-id="91ac4-222">Kliknij przycisk **Szyfruj** przycisk na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="91ac4-222">Click **Encrypt** button on the toolbar.</span></span> <span data-ttu-id="91ac4-223">Zostanie wyświetlony aplikacji Menedżera poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="91ac4-223">You see the Credentials Manager application.</span></span>

         ![Aplikacja Menedżera poświadczeń](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="91ac4-225">W **ustawienie poświadczeń** okno dialogowe, określ typ uwierzytelniania, nazwę użytkownika i hasło, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-225">In the **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="91ac4-226">Jeśli połączenie zostanie nawiązane, zaszyfrowane poświadczenia są przechowywane w formacie JSON i zamyka okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="91ac4-226">If the connection is successful, the encrypted credentials are stored in the JSON and the dialog box closes.</span></span>
      5. <span data-ttu-id="91ac4-227">Zamknij kartę puste przeglądarki, który uruchomić okno dialogowe, jeśli nie zostaną automatycznie zamknięte i wrócić na kartę przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="91ac4-227">Close the empty browser tab that launched the dialog box if it is not automatically closed and get back to the tab with the Azure portal.</span></span>

         <span data-ttu-id="91ac4-228">Na komputerze bramy te poświadczenia są **zaszyfrowanych** przy użyciu certyfikatu, który jest właścicielem usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-228">On the gateway machine, these credentials are **encrypted** by using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="91ac4-229">Jeśli chcesz używać certyfikatu, który jest skojarzony z brama zarządzania danymi w zamian, zobacz [ustawić poświadczenia bezpiecznie](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="91ac4-229">If you want to use the certificate that is associated with the Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="91ac4-230">Kliknij przycisk **Wdróż** na pasku poleceń do wdrożenia programu SQL Server połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="91ac4-230">Click **Deploy** on the command bar to deploy the SQL Server linked service.</span></span> <span data-ttu-id="91ac4-231">Powinny pojawić się połączonej usługi w widoku drzewa.</span><span class="sxs-lookup"><span data-stu-id="91ac4-231">You should see the linked service in the tree view.</span></span>

      ![Usługi SQL Server połączone w widoku drzewa](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="91ac4-233">Dodaj połączonej usługi dla konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="91ac4-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="91ac4-234">W **Edytor fabryki danych**, kliknij przycisk **nowy magazyn danych** na pasku poleceń i kliknij przycisk **magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-234">In the **Data Factory Editor**, click **New data store** on the command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="91ac4-235">Wprowadź nazwę konta magazynu Azure dla **nazwa konta**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-235">Enter the name of your Azure storage account for the **Account name**.</span></span>
3. <span data-ttu-id="91ac4-236">Wprowadź klucz konta magazynu Azure dla **klucz konta**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-236">Enter the key for your Azure storage account for the **Account key**.</span></span>
4. <span data-ttu-id="91ac4-237">Kliknij przycisk **Wdróż** wdrażania **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-237">Click **Deploy** to deploy the **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="91ac4-238">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="91ac4-238">Create datasets</span></span>
<span data-ttu-id="91ac4-239">W tym kroku Tworzenie danych wejściowych i wyjściowych zestawów danych, które zawierają dane wejściowe i wyjściowe dla operacji kopiowania (bazy danych serwera SQL lokalnymi = > magazynu obiektów blob platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="91ac4-239">In this step, you create input and output datasets that represent input and output data for the copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="91ac4-240">Przed utworzeniem zestawów danych, wykonaj następujące czynności (szczegółowy opis kroków następuje listy):</span><span class="sxs-lookup"><span data-stu-id="91ac4-240">Before creating datasets, do the following steps (detailed steps follows the list):</span></span>

* <span data-ttu-id="91ac4-241">Tworzenie tabeli o nazwie **pustych elementów** w bazie danych serwera SQL dodany jako połączonej usługi z fabryką danych i Wstaw kilka przykładowych wpisów do tabeli.</span><span class="sxs-lookup"><span data-stu-id="91ac4-241">Create a table named **emp** in the SQL Server Database you added as a linked service to the data factory and insert a couple of sample entries into the table.</span></span>
* <span data-ttu-id="91ac4-242">Tworzenie kontenera obiektów blob o nazwie **adftutorial** na platformie Azure blob konta magazynu dodany jako połączonej usługi z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-242">Create a blob container named **adftutorial** in the Azure blob storage account you added as a linked service to the data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-the-tutorial"></a><span data-ttu-id="91ac4-243">Przygotowanie lokalnego programu SQL Server dla tego samouczka</span><span class="sxs-lookup"><span data-stu-id="91ac4-243">Prepare On-premises SQL Server for the tutorial</span></span>
1. <span data-ttu-id="91ac4-244">Określona dla lokalnej bazy danych programu SQL Server połączone usługi (**SqlServerLinkedService**), użyj następującego skryptu SQL do tworzenia **pustych elementów** tabeli w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-244">In the database you specified for the on-premises SQL Server linked service (**SqlServerLinkedService**), use the following SQL script to create the **emp** table in the database.</span></span>

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. <span data-ttu-id="91ac4-245">Niektóre przykładowe wstawiania w tabeli:</span><span class="sxs-lookup"><span data-stu-id="91ac4-245">Insert some sample into the table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="91ac4-246">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="91ac4-246">Create input dataset</span></span>

1. <span data-ttu-id="91ac4-247">W **Edytorze fabryki danych** kliknij opcję **... Więcej**, kliknij przycisk **nowy zestaw danych** na pasku poleceń, a następnie kliknij **tabeli programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-247">In the **Data Factory Editor**, click **... More**, click **New dataset** on the command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="91ac4-248">Zastąp dane JSON w okienku po prawej stronie następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="91ac4-248">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   <span data-ttu-id="91ac4-249">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="91ac4-249">Note the following points:</span></span>

   * <span data-ttu-id="91ac4-250">**Typ** ustawiono **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-250">**type** is set to **SqlServerTable**.</span></span>
   * <span data-ttu-id="91ac4-251">**tableName** ustawiono **pustych elementów**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-251">**tableName** is set to **emp**.</span></span>
   * <span data-ttu-id="91ac4-252">**linkedServiceName** ustawiono **SqlServerLinkedService** (tej połączonej usługi ma utworzone we wcześniejszej części tego przewodnika.).</span><span class="sxs-lookup"><span data-stu-id="91ac4-252">**linkedServiceName** is set to **SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="91ac4-253">Wejściowy zestaw danych nie jest generowany przez inny potok w fabryce danych Azure, należy ustawić **zewnętrznych** do **true**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** to **true**.</span></span> <span data-ttu-id="91ac4-254">Wskazuje on, że dane wejściowe jest generowany zewnętrzne względem usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="91ac4-254">It denotes the input data is produced external to the Azure Data Factory service.</span></span> <span data-ttu-id="91ac4-255">Opcjonalnie można określić żadnych zasad danych zewnętrznych przy użyciu **externalData** element **zasad** sekcji.</span><span class="sxs-lookup"><span data-stu-id="91ac4-255">You can optionally specify any external data policies using the **externalData** element in the **Policy** section.</span></span>    

   <span data-ttu-id="91ac4-256">Zobacz [przenoszenie danych do/z programu SQL Server](data-factory-sqlserver-connector.md) szczegółowe informacje na temat właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="91ac4-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="91ac4-257">Kliknij przycisk **Wdróż** na pasku poleceń, aby wdrożyć zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-257">Click **Deploy** on the command bar to deploy the dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="91ac4-258">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="91ac4-258">Create output dataset</span></span>

1. <span data-ttu-id="91ac4-259">W **Edytor fabryki danych**, kliknij przycisk **nowy zestaw danych** na pasku poleceń, a następnie kliknij **magazynu obiektów Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-259">In the **Data Factory Editor**, click **New dataset** on the command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="91ac4-260">Zastąp dane JSON w okienku po prawej stronie następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="91ac4-260">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   <span data-ttu-id="91ac4-261">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="91ac4-261">Note the following points:</span></span>

   * <span data-ttu-id="91ac4-262">**Typ** ustawiono **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-262">**type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="91ac4-263">**linkedServiceName** ustawiono **AzureStorageLinkedService** (w kroku 2 została utworzona tej połączonej usługi).</span><span class="sxs-lookup"><span data-stu-id="91ac4-263">**linkedServiceName** is set to **AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="91ac4-264">**folderPath** ustawiono **adftutorial/outfromonpremdf** gdzie outfromonpremdf to folder, w kontenerze adftutorial.</span><span class="sxs-lookup"><span data-stu-id="91ac4-264">**folderPath** is set to **adftutorial/outfromonpremdf** where outfromonpremdf is the folder in the adftutorial container.</span></span> <span data-ttu-id="91ac4-265">Utwórz **adftutorial** kontener, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="91ac4-265">Create the **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="91ac4-266">Parametr **availability** (dostępność) został ustawiony na wartość **hourly** (co godzinę) (parametr **frequency** [częstotliwość] został ustawiony na **hour** [godzinę], a **interval** [interwał] został ustawiony na wartość **1**).</span><span class="sxs-lookup"><span data-stu-id="91ac4-266">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span></span>  <span data-ttu-id="91ac4-267">Usługi fabryka danych generuje wycinek danych wyjściowych, co godzinę w **pustych elementów** tabeli w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="91ac4-267">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL Database.</span></span>

   <span data-ttu-id="91ac4-268">Jeśli nie określisz **fileName** dla **tabeli wyników**, wygenerowanych plików w **folderPath** są nazywane w następującym formacie: danych.<Guid>. txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="91ac4-268">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="91ac4-269">Aby ustawić **folderPath** i **fileName** dynamicznie na podstawie **SliceStart** czasu, użyj właściwości partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="91ac4-269">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the partitionedBy property.</span></span> <span data-ttu-id="91ac4-270">W poniższym przykładzie parametr folderPath używa elementów Year, Month i Day z parametru SliceStart (czas rozpoczęcia przetwarzania wycinka), a parametr fileName używa elementu Hour z parametru SliceStart.</span><span class="sxs-lookup"><span data-stu-id="91ac4-270">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="91ac4-271">Na przykład jeśli wycinek jest generowany dla czasu 2014-10-20T08:00:00, parametr folderName zostaje ustawiony na wikidatagateway/wikisampledataout/2014/10/20, a parametr fileName zostaje ustawiony na wartość 08.csv.</span><span class="sxs-lookup"><span data-stu-id="91ac4-271">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span></span>

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    <span data-ttu-id="91ac4-272">Zobacz [przenoszenie danych do/z magazynu obiektów Blob Azure](data-factory-azure-blob-connector.md) szczegółowe informacje na temat właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="91ac4-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="91ac4-273">Kliknij przycisk **Wdróż** na pasku poleceń, aby wdrożyć zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-273">Click **Deploy** on the command bar to deploy the dataset.</span></span> <span data-ttu-id="91ac4-274">Upewnij się, że widoczne oba zestawy danych w widoku drzewa.</span><span class="sxs-lookup"><span data-stu-id="91ac4-274">Confirm that you see both the datasets in the tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="91ac4-275">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="91ac4-275">Create pipeline</span></span>
<span data-ttu-id="91ac4-276">W tym kroku utworzysz **potoku** z jednym **działanie kopiowania** używającą **EmpOnPremSQLTable** jako dane wejściowe i **OutputBlobTable** jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="91ac4-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="91ac4-277">Kliknij w Edytor fabryki danych **... Więcej** i **Nowy potok**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="91ac4-278">Zastąp dane JSON w okienku po prawej stronie następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="91ac4-278">Replace the JSON in the right pane with the following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL to Azure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server to blob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > <span data-ttu-id="91ac4-279">Zastąp wartość właściwości **start** datą bieżącą, a wartość **end** datą jutrzejszą.</span><span class="sxs-lookup"><span data-stu-id="91ac4-279">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span>
   >
   >

   <span data-ttu-id="91ac4-280">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="91ac4-280">Note the following points:</span></span>

   * <span data-ttu-id="91ac4-281">W sekcji działania jest działanie tylko których **typu** ustawiono **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-281">In the activities section, there is only activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="91ac4-282">**Dane wejściowe** dla działania jest ustawiony na **EmpOnPremSQLTable** i **dane wyjściowe** dla działania jest ustawiony na **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-282">**Input** for the activity is set to **EmpOnPremSQLTable** and **output** for the activity is set to **OutputBlobTable**.</span></span>
   * <span data-ttu-id="91ac4-283">W **typeProperties** sekcji **SqlSource** jest określony jako **typ źródła** i ** BlobSink ** jest określony jako **typu sink**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-283">In the **typeProperties** section, **SqlSource** is specified as the **source type** and **BlobSink **is specified as the **sink type**.</span></span>
   * <span data-ttu-id="91ac4-284">Zapytanie SQL `select * from emp` określono **sqlReaderQuery** właściwość **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-284">SQL query `select * from emp` is specified for the **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="91ac4-285">Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="91ac4-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="91ac4-286">Na przykład: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="91ac4-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="91ac4-287">Czas **end** jest opcjonalny, ale w tym samouczku zostanie użyty.</span><span class="sxs-lookup"><span data-stu-id="91ac4-287">The **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="91ac4-288">Jeśli nie określisz wartości dla właściwości **end**, zostanie ona obliczona jako „**czas rozpoczęcia + 48 godzin**”.</span><span class="sxs-lookup"><span data-stu-id="91ac4-288">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="91ac4-289">Aby uruchomić potok bezterminowo, określ **9/9/9999** jako wartość dla właściwości **end**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-289">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span></span>

   <span data-ttu-id="91ac4-290">Czas trwania przetwarzania wycinków danych na podstawie definiowania **dostępności** właściwości, które zostały zdefiniowane dla każdego zestawu danych z fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="91ac4-290">You are defining the time duration in which the data slices are processed based on the **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="91ac4-291">W tym przykładzie występują 24 wycinki danych, ponieważ poszczególne wycinki są generowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="91ac4-291">In the example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="91ac4-292">Kliknij przycisk **Wdróż** na pasku poleceń, aby wdrożyć zestawu danych (tabela jest prostokątny zestawu danych).</span><span class="sxs-lookup"><span data-stu-id="91ac4-292">Click **Deploy** on the command bar to deploy the dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="91ac4-293">Upewnij się, że potok zostaną wyświetlone w widoku drzewa w **potoki** węzła.</span><span class="sxs-lookup"><span data-stu-id="91ac4-293">Confirm that the pipeline shows up in the tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="91ac4-294">Teraz, kliknij przycisk **X** dwa razy, aby zamknąć stronę, aby wrócić do **fabryki danych** dla strony **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-294">Now, click **X** twice to close the page to get back to the **Data Factory** page for the **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="91ac4-295">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="91ac4-295">**Congratulations!**</span></span> <span data-ttu-id="91ac4-296">Pomyślnie utworzono fabryki danych Azure, połączone usługi, zestawy danych i potoku i zaplanowane potoku.</span><span class="sxs-lookup"><span data-stu-id="91ac4-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled the pipeline.</span></span>

#### <a name="view-the-data-factory-in-a-diagram-view"></a><span data-ttu-id="91ac4-297">Wyświetlanie fabryki danych w widoku diagramu</span><span class="sxs-lookup"><span data-stu-id="91ac4-297">View the data factory in a Diagram View</span></span>
1. <span data-ttu-id="91ac4-298">W **portalu Azure**, kliknij przycisk **Diagram** Kafelek na stronie głównej **ADFTutorialOnPremDF** fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-298">In the **Azure portal**, click **Diagram** tile on the home page for the **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="91ac4-299">:</span><span class="sxs-lookup"><span data-stu-id="91ac4-299">:</span></span>

    ![Diagram łącza](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="91ac4-301">Powinien zostać wyświetlony diagram podobny do tego na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="91ac4-301">You should see the diagram similar to the following image:</span></span>

    ![Widok diagramu](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="91ac4-303">Można powiększać, pomniejszyć, powiększenie do 100%, powiększenia do dopasowania, automatycznie rozmieszczaj potoki i zestawów danych i Pokaż elementy powiązane informacje (wyróżnia elementy nadrzędne i podrzędne wybranego elementu).</span><span class="sxs-lookup"><span data-stu-id="91ac4-303">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="91ac4-304">Możesz kliknąć dwukrotnie (dataset wejścia/wyjścia lub potoku), aby wyświetlić właściwości dla tego obiektu.</span><span class="sxs-lookup"><span data-stu-id="91ac4-304">You can double-click an object (input/output dataset or pipeline) to see properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="91ac4-305">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="91ac4-305">Monitor pipeline</span></span>
<span data-ttu-id="91ac4-306">W tym kroku opisano użycie witryny Azure Portal do monitorowania tego, co dzieje się w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="91ac4-306">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="91ac4-307">Do monitorowania zestawów danych i potoków można również używać poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91ac4-307">You can also use PowerShell cmdlets to monitor datasets and pipelines.</span></span> <span data-ttu-id="91ac4-308">Aby uzyskać szczegółowe informacje o monitorowaniu, zobacz [monitorować i zarządzać potoki](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="91ac4-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="91ac4-309">Na diagramie, kliknij dwukrotnie **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-309">In the diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Wycinki EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="91ac4-311">Zwróć uwagę, że wszystkie dane wycinków zapasowej znajdują się w **gotowe** stanu, ponieważ czas trwania procesu (czas rozpoczęcia do czasu zakończenia) przypada w przeszłości.</span><span class="sxs-lookup"><span data-stu-id="91ac4-311">Notice that all the data slices up are in **Ready** state because the pipeline duration (start time to end time) is in the past.</span></span> <span data-ttu-id="91ac4-312">Jest również wstawieniu danych w bazie danych programu SQL Server i jest cały czas.</span><span class="sxs-lookup"><span data-stu-id="91ac4-312">It is also because you have inserted the data in the SQL Server database and it is there all the time.</span></span> <span data-ttu-id="91ac4-313">Upewnij się, że brak wycinków widoczne w **wycinków Problem** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="91ac4-313">Confirm that no slices show up in the **Problem slices** section at the bottom.</span></span> <span data-ttu-id="91ac4-314">Aby wyświetlić wszystkie fragmenty, kliknij przycisk **Zobacz więcej** w dolnej części listy wycinków.</span><span class="sxs-lookup"><span data-stu-id="91ac4-314">To view all the slices, click **See More** at the bottom of the list of slices.</span></span>
3. <span data-ttu-id="91ac4-315">Teraz, w **zestawów danych** kliknij przycisk **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-315">Now, In the **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Wycinki OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="91ac4-317">Kliknij wycinek żadnych danych z listy i powinna zostać wyświetlona **wycinka danych** strony.</span><span class="sxs-lookup"><span data-stu-id="91ac4-317">Click any data slice from the list and you should see the **Data Slice** page.</span></span> <span data-ttu-id="91ac4-318">Zobaczysz, że działanie jest uruchomione wycinka.</span><span class="sxs-lookup"><span data-stu-id="91ac4-318">You see activity runs for the slice.</span></span> <span data-ttu-id="91ac4-319">Użytkownik widzi tylko jedno działanie Uruchom zwykle.</span><span class="sxs-lookup"><span data-stu-id="91ac4-319">You see only one activity run usually.</span></span>  

    ![Blok wycinek danych](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="91ac4-321">Jeśli wycinek nie znajduje się w stanie **Gotowe**, możesz wyświetlić wycinki strumienia wychodzącego, które nie są w stanie Gotowe i blokują wykonanie bieżącego wycinka na liście **Niegotowe wycinki strumienia wychodzącego**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-321">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="91ac4-322">Kliknij przycisk **uruchamiania działania** z listy na dole, aby wyświetlić **szczegóły uruchomienia działania**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-322">Click the **activity run** from the list at the bottom to see **activity run details**.</span></span>

   ![Strona szczegółów uruchomienia działania](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="91ac4-324">Zobaczysz informacje, takie jak przepustowość, czas trwania i bramy używany do transferu danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-324">You would see information such as throughput, duration, and the gateway used to transfer the data.</span></span>
6. <span data-ttu-id="91ac4-325">Kliknij przycisk **X** zamknąć wszystkie strony, dopóki</span><span class="sxs-lookup"><span data-stu-id="91ac4-325">Click **X** to close all the pages until you</span></span>
7. <span data-ttu-id="91ac4-326">Wróć do strony głównej **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="91ac4-326">get back to the home page for the **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="91ac4-327">(opcjonalnie) Kliknij przycisk **potoki**, kliknij przycisk **ADFTutorialOnPremDF**oraz szczegółowy tabel wejściowych (**zużyto**) lub wyjściowych zestawów danych (**produkcji**).</span><span class="sxs-lookup"><span data-stu-id="91ac4-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="91ac4-328">Użyj narzędzia takiego jak [Eksploratora usługi Storage Microsoft](http://storageexplorer.com/) Aby sprawdzić, czy obiekt blob/plik został utworzony dla każdej godziny.</span><span class="sxs-lookup"><span data-stu-id="91ac4-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to verify that a blob/file is created for each hour.</span></span>

   ![Eksplorator usługi Azure Storage](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="91ac4-330">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91ac4-330">Next steps</span></span>
* <span data-ttu-id="91ac4-331">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykuł, aby wszystkie szczegółowe informacje o brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="91ac4-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the Data Management Gateway.</span></span>
* <span data-ttu-id="91ac4-332">Zobacz [skopiować dane z obiektu Blob Azure do usługi Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Aby dowiedzieć się więcej o sposobie używania działania kopiowania do przenoszenia danych z magazynu danych źródła do ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="91ac4-332">See [Copy data from Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to learn about how to use Copy Activity to move data from a source data store to a sink data store.</span></span>
