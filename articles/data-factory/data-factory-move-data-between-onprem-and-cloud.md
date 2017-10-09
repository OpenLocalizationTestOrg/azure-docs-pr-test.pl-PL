---
title: "dane aaaMove — brama zarządzania danymi | Dokumentacja firmy Microsoft"
description: "Konfigurowanie danych toomove bramy danych między lokalnymi i hello chmury. Użyj bramy zarządzania danymi w fabryce danych Azure toomove danych."
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
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a><span data-ttu-id="b55dd-105">Przenoszenie danych między lokalnych źródeł i w chmurze hello z brama zarządzania danymi</span><span class="sxs-lookup"><span data-stu-id="b55dd-105">Move data between on-premises sources and hello cloud with Data Management Gateway</span></span>
<span data-ttu-id="b55dd-106">Ten artykuł zawiera omówienie integrację danych lokalnych magazynów danych i magazyny danych chmury przy użyciu fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="b55dd-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="b55dd-107">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu i innych danych fabryki podstawowe pojęcia dotyczące artykułów: [zestawów danych](data-factory-create-datasets.md) i [potoki](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="b55dd-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="b55dd-108">Brama zarządzania danymi</span><span class="sxs-lookup"><span data-stu-id="b55dd-108">Data Management Gateway</span></span>
<span data-ttu-id="b55dd-109">Brama zarządzania danymi należy zainstalować na Twojej tooenable maszyny lokalnej przenoszenia danych z lokalnego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="b55dd-109">You must install Data Management Gateway on your on-premises machine tooenable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="b55dd-110">Brama Hello może zostać zainstalowana na powitania, które same komputera jako magazynu danych hello lub na innym komputerze, tak długo, jak brama hello można połączyć z usługą Magazyn danych toohello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-110">hello gateway can be installed on hello same machine as hello data store or on a different machine as long as hello gateway can connect toohello data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b55dd-111">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="b55dd-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="b55dd-112">Witaj następujące przewodniku zademonstrowano, jak toocreate fabryki danych z potok, który przenosi dane z lokalnymi **programu SQL Server** bazy danych magazynu obiektów blob Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="b55dd-112">hello following walkthrough shows you how toocreate a data factory with a pipeline that moves data from an on-premises **SQL Server** database tooan Azure blob storage.</span></span> <span data-ttu-id="b55dd-113">W ramach hello wskazówki zainstalowaniu i skonfigurowaniu hello brama zarządzania danymi na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b55dd-113">As part of hello walkthrough, you install and configure hello Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-toocloud"></a><span data-ttu-id="b55dd-114">Wskazówki: kopiowanie lokalnych danych toocloud</span><span class="sxs-lookup"><span data-stu-id="b55dd-114">Walkthrough: copy on-premises data toocloud</span></span>
<span data-ttu-id="b55dd-115">W tym przewodniku hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b55dd-115">In this walkthrough you do hello following steps:</span></span> 

1. <span data-ttu-id="b55dd-116">Tworzenie fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="b55dd-116">Create a data factory.</span></span>
2. <span data-ttu-id="b55dd-117">Tworzenie bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="b55dd-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="b55dd-118">Tworzenie połączonej usługi dla źródłowy i odbiorczy magazynów danych.</span><span class="sxs-lookup"><span data-stu-id="b55dd-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="b55dd-119">Utwórz dane wejściowe toorepresent zestawów danych i dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="b55dd-119">Create datasets toorepresent input and output data.</span></span>
5. <span data-ttu-id="b55dd-120">Utworzyć potok z danych hello toomove działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="b55dd-120">Create a pipeline with a copy activity toomove hello data.</span></span>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="b55dd-121">Wymagania wstępne dotyczące samouczka hello</span><span class="sxs-lookup"><span data-stu-id="b55dd-121">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="b55dd-122">Przed rozpoczęciem tego przewodnika, musi mieć hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="b55dd-122">Before you begin this walkthrough, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="b55dd-123">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-123">**Azure subscription**.</span></span>  <span data-ttu-id="b55dd-124">Jeśli nie masz subskrypcji, możesz utworzyć konto bezpłatnej wersji próbnej w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="b55dd-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b55dd-125">Zobacz hello [bezpłatnej wersji próbnej](http://azure.microsoft.com/pricing/free-trial/) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="b55dd-125">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="b55dd-126">**Konto magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-126">**Azure Storage Account**.</span></span> <span data-ttu-id="b55dd-127">Użyj magazynu obiektów blob hello **docelowego/ujście** magazynu danych, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b55dd-127">You use hello blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="b55dd-128">Jeśli nie masz konta magazynu platformy Azure, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykuł, aby toocreate kroki, jeden.</span><span class="sxs-lookup"><span data-stu-id="b55dd-128">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="b55dd-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-129">**SQL Server**.</span></span> <span data-ttu-id="b55dd-130">Użyj lokalnej bazy danych programu SQL Server jako **źródła** magazynu danych w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b55dd-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="b55dd-131">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="b55dd-131">Create data factory</span></span>
<span data-ttu-id="b55dd-132">W tym kroku użyjesz hello Azure toocreate portalu o nazwie wystąpienia fabryki danych Azure **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-132">In this step, you use hello Azure portal toocreate an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="b55dd-133">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b55dd-133">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b55dd-134">Kliknij przycisk **+ nowy**, kliknij przycisk **analizy i analiza**i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Nowy-> Fabryka danych](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="b55dd-136">W hello **nowa fabryka danych** wprowadź **ADFTutorialOnPremDF** dla hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="b55dd-136">In hello **New data factory** page, enter **ADFTutorialOnPremDF** for hello Name.</span></span>

    ![Dodaj tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="b55dd-138">Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="b55dd-138">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="b55dd-139">Jeśli wystąpi błąd hello: **nazwa fabryki danych "ADFTutorialOnPremDF" nie jest dostępna**, Zmień nazwę hello hello fabryki danych (na przykład yournameADFTutorialOnPremDF) i spróbuj ponownie utworzyć.</span><span class="sxs-lookup"><span data-stu-id="b55dd-139">If you receive hello error: **Data factory name “ADFTutorialOnPremDF” is not available**, change hello name of hello data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="b55dd-140">Użyj tej nazwy, zamiast ADFTutorialOnPremDF podczas wykonywania pozostałych czynności w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b55dd-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="b55dd-141">Nazwa fabryki danych hello Hello może zostać zarejestrowana jako **DNS** nazwy w przyszłości hello i dlatego stać się publicznie widoczna.</span><span class="sxs-lookup"><span data-stu-id="b55dd-141">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="b55dd-142">Wybierz hello **subskrypcji platformy Azure** miejscu toobe fabryki danych hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="b55dd-142">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="b55dd-143">Wybierz istniejącą **grupę zasobów** lub utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="b55dd-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="b55dd-144">Samouczek hello, Utwórz grupę zasobów o nazwie: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-144">For hello tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="b55dd-145">Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** strony.</span><span class="sxs-lookup"><span data-stu-id="b55dd-145">Click **Create** on hello **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b55dd-146">toocreate wystąpienia fabryki danych, musi być członkiem hello [współautora fabryki danych](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) roli na poziomie grupy zasobów subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="b55dd-147">Po zakończeniu tworzenia Zobacz hello **fabryki danych** strony, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="b55dd-147">After creation is complete, you see hello **Data Factory** page as shown in hello following image:</span></span>

   ![Strona główna fabryki danych](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="b55dd-149">Tworzenie bramy</span><span class="sxs-lookup"><span data-stu-id="b55dd-149">Create gateway</span></span>
1. <span data-ttu-id="b55dd-150">W hello **fabryki danych** kliknij przycisk **tworzenie i wdrażanie** hello toolaunch kafelka **edytora** hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="b55dd-150">In hello **Data Factory** page, click **Author and deploy** tile toolaunch hello **Editor** for hello data factory.</span></span>

    ![Kafelek Utwórz i wdróż](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="b55dd-152">W hello Edytor fabryki danych, kliknij przycisk **... Więcej** na hello narzędzi, a następnie kliknij przycisk **nowej bramy danych**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-152">In hello Data Factory Editor, click **... More** on hello toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="b55dd-153">Alternatywnie możesz kliknąć prawym przyciskiem myszy **bram danych** w hello widok drzewa i kliknij przycisk **nowej bramy danych**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-153">Alternatively, you can right-click **Data Gateways** in hello tree view, and click **New data gateway**.</span></span>

   ![Nową bramę danych na pasku narzędzi](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="b55dd-155">W hello **Utwórz** wprowadź **adftutorialgateway** dla hello **nazwa**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-155">In hello **Create** page, enter **adftutorialgateway** for hello **name**, and click **OK**.</span></span>     

    ![Utwórz stronę bramy](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="b55dd-157">W tym przewodniku należy utworzyć bramę logicznej hello z tylko jeden węzeł (komputera lokalnego systemu Windows).</span><span class="sxs-lookup"><span data-stu-id="b55dd-157">In this walkthrough, you create hello logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="b55dd-158">Możesz skalować w poziomie bramy zarządzania danymi hello bramy można skojarzyć wielu komputerach lokalnych.</span><span class="sxs-lookup"><span data-stu-id="b55dd-158">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="b55dd-159">Możesz skalować w górę zwiększając liczbę zadań przepływu danych, które można uruchomić jednocześnie w węźle.</span><span class="sxs-lookup"><span data-stu-id="b55dd-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="b55dd-160">Ta funkcja jest również dostępny do logicznego bramy z jednego węzła.</span><span class="sxs-lookup"><span data-stu-id="b55dd-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="b55dd-161">Zobacz [skalowanie brama zarządzania danymi w fabryce danych Azure](data-factory-data-management-gateway-high-availability-scalability.md) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="b55dd-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="b55dd-162">W hello **Konfiguruj** kliknij przycisk **Zainstaluj bezpośrednio na tym komputerze**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-162">In hello **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="b55dd-163">Ta akcja pobiera hello pakiet instalacyjny bramy hello, instaluje konfiguruje i rejestruje hello bramę na komputerze hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-163">This action downloads hello installation package for hello gateway, installs, configures, and registers hello gateway on hello computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="b55dd-164">Użyj programu Internet Explorer lub przeglądarki sieci web zgodne Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="b55dd-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="b55dd-165">Jeśli używasz programu Chrome, przejdź toohello [sklepu Chrome web store](https://chrome.google.com/webstore/), wyszukaj ze słowem kluczowym "ClickOnce", wybierz jedno z rozszerzeń ClickOnce hello i zainstaluj go.</span><span class="sxs-lookup"><span data-stu-id="b55dd-165">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="b55dd-166">Witaj tego samego dla przeglądarki Firefox (Instalowanie dodatku).</span><span class="sxs-lookup"><span data-stu-id="b55dd-166">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="b55dd-167">Kliknij przycisk **Otwórz Menu** przycisk na pasku narzędzi hello (**trzy poziome linie** w hello prawym górnym rogu), kliknij przycisk **dodatki**, wyszukaj ze słowem kluczowym "ClickOnce", wybierz jedną z hello Rozszerzenia ClickOnce, a następnie zainstaluj go.</span><span class="sxs-lookup"><span data-stu-id="b55dd-167">Click **Open Menu** button on hello toolbar (**three horizontal lines** in hello top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Brama — Konfigurowanie strony](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="b55dd-169">W ten sposób jest hello Najprostszym sposobem (jednym kliknięciem) toodownload, zainstalować, skonfigurować i zarejestrować bramę hello w jeden pojedynczy krok.</span><span class="sxs-lookup"><span data-stu-id="b55dd-169">This way is hello easiest way (one-click) toodownload, install, configure, and register hello gateway in one single step.</span></span> <span data-ttu-id="b55dd-170">Zostanie wyświetlony hello **Menedżera konfiguracji bramy zarządzania danymi firmy Microsoft** aplikacja jest zainstalowana na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b55dd-170">You can see hello **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="b55dd-171">Możesz również znaleźć hello wykonywalnego **ConfigManager.exe** w folderze hello: **C:\Program Files\Microsoft danych zarządzania Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-171">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="b55dd-172">Można również pobrać i zainstalować bramę ręcznie przy użyciu łącza hello na tej stronie i zarejestrowanie go za pomocą klucza hello pokazano hello **nowy klucz** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="b55dd-172">You can also download and install gateway manually by using hello links in this page and register it using hello key shown in hello **NEW KEY** text box.</span></span>

    <span data-ttu-id="b55dd-173">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu dla wszystkich hello szczegółowe informacje o hello bramy.</span><span class="sxs-lookup"><span data-stu-id="b55dd-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b55dd-174">Należy mieć uprawnienia administratora na powitania tooinstall komputera lokalnego i pomyślnie skonfigurować hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="b55dd-174">You must be an administrator on hello local computer tooinstall and configure hello Data Management Gateway successfully.</span></span> <span data-ttu-id="b55dd-175">Możesz dodać kolejnych użytkowników toohello **użytkownicy bramy zarządzania danymi** lokalnej grupy systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="b55dd-175">You can add additional users toohello **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="b55dd-176">Witaj członkami tej grupy można użyć hello Menedżera konfiguracji bramy zarządzania danymi narzędzia tooconfigure hello bramy.</span><span class="sxs-lookup"><span data-stu-id="b55dd-176">hello members of this group can use hello Data Management Gateway Configuration Manager tool tooconfigure hello gateway.</span></span>
   >
   >
5. <span data-ttu-id="b55dd-177">Poczekaj kilka minut lub poczekaj na wyświetlenie hello następującego komunikatu powiadomienia:</span><span class="sxs-lookup"><span data-stu-id="b55dd-177">Wait for a couple of minutes or wait until you see hello following notification message:</span></span>

    ![Pomyślnie zainstalowano bramy](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="b55dd-179">Uruchom **Menedżera konfiguracji bramy zarządzania danymi** aplikacji na komputerze.</span><span class="sxs-lookup"><span data-stu-id="b55dd-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="b55dd-180">W hello **wyszukiwania** wpisz **brama zarządzania danymi** tooaccess tego narzędzia.</span><span class="sxs-lookup"><span data-stu-id="b55dd-180">In hello **Search** window, type **Data Management Gateway** tooaccess this utility.</span></span> <span data-ttu-id="b55dd-181">Możesz również znaleźć hello wykonywalnego **ConfigManager.exe** w folderze hello: **C:\Program Files\Microsoft danych zarządzania Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="b55dd-181">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Menedżer konfiguracji bramy](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="b55dd-183">Upewnij się, że widoczny `adftutorialgateway is connected toohello cloud service` wiadomości.</span><span class="sxs-lookup"><span data-stu-id="b55dd-183">Confirm that you see `adftutorialgateway is connected toohello cloud service` message.</span></span> <span data-ttu-id="b55dd-184">Witaj pasek Wyświetla dolnej hello stanu **połączona usługa w chmurze toohello** wraz z **zielony znacznik wyboru**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-184">hello status bar hello bottom displays **Connected toohello cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="b55dd-185">Na powitania **Home** karcie, możesz również wykonać hello następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="b55dd-185">On hello **Home** tab, you can also do hello following operations:</span></span>

   * <span data-ttu-id="b55dd-186">**Zarejestruj** bramy przy użyciu klucza z portalu Azure za pomocą przycisku Zarejestruj hello hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-186">**Register** a gateway with a key from hello Azure portal by using hello Register button.</span></span>
   * <span data-ttu-id="b55dd-187">**Zatrzymaj** hello danych usługa hosta bramy zarządzania na komputerze bramy.</span><span class="sxs-lookup"><span data-stu-id="b55dd-187">**Stop** hello Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="b55dd-188">**Zaplanuj aktualizacje** toobe zainstalowany w określonym czasie hello dnia.</span><span class="sxs-lookup"><span data-stu-id="b55dd-188">**Schedule updates** toobe installed at a specific time of hello day.</span></span>
   * <span data-ttu-id="b55dd-189">Widoku, gdy został bramy hello **ostatniej aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-189">View when hello gateway was **last updated**.</span></span>
   * <span data-ttu-id="b55dd-190">Określ czas, w którym można zainstalować bramę toohello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="b55dd-190">Specify time at which an update toohello gateway can be installed.</span></span>
8. <span data-ttu-id="b55dd-191">Przełącz toohello **ustawienia** kartę hello certyfikatu podanego w hello **certyfikatu** sekcja jest używane tooencrypt/odszyfrowywania poświadczenia dla magazynu danych lokalnych hello określoną na powitania portalu.</span><span class="sxs-lookup"><span data-stu-id="b55dd-191">Switch toohello **Settings** tab. hello certificate specified in hello **Certificate** section is used tooencrypt/decrypt credentials for hello on-premises data store that you specify on hello portal.</span></span> <span data-ttu-id="b55dd-192">(opcjonalnie) Kliknij przycisk **zmiany** toouse własnego certyfikatu zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="b55dd-192">(optional) Click **Change** toouse your own certificate instead.</span></span> <span data-ttu-id="b55dd-193">Domyślnie przy użyciu brama hello hello certyfikatu, który został wygenerowany automatycznie przez hello usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="b55dd-193">By default, hello gateway uses hello certificate that is auto-generated by hello Data Factory service.</span></span>

    ![Konfiguracja certyfikatu bramy](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="b55dd-195">Możesz również wykonać hello następujących czynności na powitania **ustawienia** karty:</span><span class="sxs-lookup"><span data-stu-id="b55dd-195">You can also do hello following actions on hello **Settings** tab:</span></span>

   * <span data-ttu-id="b55dd-196">Wyświetl lub wyeksportować certyfikat hello jest używany przez bramę hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-196">View or export hello certificate being used by hello gateway.</span></span>
   * <span data-ttu-id="b55dd-197">Zmień punkt końcowy HTTPS hello używany przez bramę hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-197">Change hello HTTPS endpoint used by hello gateway.</span></span>    
   * <span data-ttu-id="b55dd-198">Ustaw toobe serwera proxy HTTP używany przez bramę hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-198">Set an HTTP proxy toobe used by hello gateway.</span></span>     
9. <span data-ttu-id="b55dd-199">(opcjonalnie) Przełącz toohello **diagnostyki** pozycję Sprawdź hello **Włącz pełne rejestrowanie** opcję, jeśli chcesz tooenable pełne rejestrowanie, której można tootroubleshoot wszelkie problemy z bramą hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-199">(optional) Switch toohello **Diagnostics** tab, check hello **Enable verbose logging** option if you want tooenable verbose logging that you can use tootroubleshoot any issues with hello gateway.</span></span> <span data-ttu-id="b55dd-200">Witaj rejestrowane informacje znajdują się w **Podgląd zdarzeń** w obszarze **Dzienniki aplikacji i usług** -> **brama zarządzania danymi** węzła.</span><span class="sxs-lookup"><span data-stu-id="b55dd-200">hello logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Karta diagnostyki](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="b55dd-202">Można również wykonać następujące akcje w hello hello **diagnostyki** karty:</span><span class="sxs-lookup"><span data-stu-id="b55dd-202">You can also perform hello following actions in hello **Diagnostics** tab:</span></span>

   * <span data-ttu-id="b55dd-203">Użyj **Testuj połączenie** sekcji tooan lokalnego źródła danych przy użyciu bramy hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-203">Use **Test Connection** section tooan on-premises data source using hello gateway.</span></span>
   * <span data-ttu-id="b55dd-204">Kliknij przycisk **Wyświetl dzienniki** hello toosee brama zarządzania danymi logowania w oknie Podgląd zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b55dd-204">Click **View Logs** toosee hello Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="b55dd-205">Kliknij przycisk **Wyślij dzienniki** tooupload z dziennikami z ostatnich siedmiu dni tooMicrosoft toofacilitate rozwiązywania problemów z problemów związanych z pliku zip.</span><span class="sxs-lookup"><span data-stu-id="b55dd-205">Click **Send Logs** tooupload a zip file with logs of last seven days tooMicrosoft toofacilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="b55dd-206">Na powitania **diagnostyki** na karcie hello **Testuj połączenie** zaznacz **SqlServer** hello typu danych hello przechowywania, wprowadź nazwę hello powitania serwera bazy danych, nazwę Witaj bazy danych, określ typ uwierzytelniania, wprowadź nazwę użytkownika i hasło i kliknij przycisk **testu** tootest czy brama hello można połączyć z usługą toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b55dd-206">On hello **Diagnostics** tab, in hello **Test Connection** section, select **SqlServer** for hello type of hello data store, enter hello name of hello database server, name of hello database, specify authentication type, enter user name, and password, and click **Test** tootest whether hello gateway can connect toohello database.</span></span>
11. <span data-ttu-id="b55dd-207">Przełącznik toohello przeglądarki sieci web w hello **portalu Azure**, kliknij przycisk **OK** na powitania **Konfiguruj** strony, a następnie na powitania **nowej bramy danych** Strona.</span><span class="sxs-lookup"><span data-stu-id="b55dd-207">Switch toohello web browser, and in hello **Azure portal**, click **OK** on hello **Configure** page and then on hello **New data gateway** page.</span></span>
12. <span data-ttu-id="b55dd-208">Powinny pojawić się **adftutorialgateway** w obszarze **bram danych** w widoku drzewa hello powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="b55dd-208">You should see **adftutorialgateway** under **Data Gateways** in hello tree view on hello left.</span></span>  <span data-ttu-id="b55dd-209">Jeśli klikniesz przycisk, powinien pojawić się hello skojarzone JSON.</span><span class="sxs-lookup"><span data-stu-id="b55dd-209">If you click it, you should see hello associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="b55dd-210">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="b55dd-210">Create linked services</span></span>
<span data-ttu-id="b55dd-211">W tym kroku, Utwórz dwie połączonej usługi: **AzureStorageLinkedService** i **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="b55dd-212">Witaj **SqlServerLinkedService** łączy lokalną bazą danych programu SQL Server i hello **AzureStorageLinkedService** połączonej usługi łączy fabrykę danych toohello magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b55dd-212">hello **SqlServerLinkedService** links an on-premises SQL Server database and hello **AzureStorageLinkedService** linked service links an Azure blob store toohello data factory.</span></span> <span data-ttu-id="b55dd-213">W dalszej części tego przewodnika, który kopiuje dane z magazynu obiektów blob platformy Azure toohello bazy danych w programu SQL Server lokalne hello jest utworzyć potok.</span><span class="sxs-lookup"><span data-stu-id="b55dd-213">You create a pipeline later in this walkthrough that copies data from hello on-premises SQL Server database toohello Azure blob store.</span></span>

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a><span data-ttu-id="b55dd-214">Dodawanie bazy danych programu SQL Server połączonej usługi tooan lokalnej</span><span class="sxs-lookup"><span data-stu-id="b55dd-214">Add a linked service tooan on-premises SQL Server database</span></span>
1. <span data-ttu-id="b55dd-215">W hello **Edytor fabryki danych**, kliknij przycisk **nowy magazyn danych** na powitania narzędzi i wybierz **programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-215">In hello **Data Factory Editor**, click **New data store** on hello toolbar and select **SQL Server**.</span></span>

   ![Nowa usługa SQL Server połączone](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="b55dd-217">W hello **edytora JSON** na powitania prawo, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b55dd-217">In hello **JSON editor** on hello right, do hello following steps:</span></span>

   1. <span data-ttu-id="b55dd-218">Dla hello **gatewayName**, określ **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-218">For hello **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="b55dd-219">W hello **connectionString**, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b55dd-219">In hello **connectionString**, do hello following steps:</span></span>    

      1. <span data-ttu-id="b55dd-220">Aby uzyskać **servername**, wprowadź nazwę hello powitania serwera, który hostuje hello bazy danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b55dd-220">For **servername**, enter hello name of hello server that hosts hello SQL Server database.</span></span>
      2. <span data-ttu-id="b55dd-221">Aby uzyskać **databasename**, wprowadź nazwę hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b55dd-221">For **databasename**, enter hello name of hello database.</span></span>
      3. <span data-ttu-id="b55dd-222">Kliknij przycisk **Szyfruj** przycisk na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="b55dd-222">Click **Encrypt** button on hello toolbar.</span></span> <span data-ttu-id="b55dd-223">Zostanie wyświetlony hello aplikacji Menedżera poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="b55dd-223">You see hello Credentials Manager application.</span></span>

         ![Aplikacja Menedżera poświadczeń](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="b55dd-225">W hello **ustawienie poświadczeń** okno dialogowe, określ typ uwierzytelniania, nazwę użytkownika i hasło, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-225">In hello **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="b55dd-226">W przypadku pomyślnego nawiązania połączenia hello hello zaszyfrowane poświadczenia są przechowywane w hello JSON i zamyka okno dialogowe hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-226">If hello connection is successful, hello encrypted credentials are stored in hello JSON and hello dialog box closes.</span></span>
      5. <span data-ttu-id="b55dd-227">Zamknij kartę puste przeglądarki hello uruchomić okno dialogowe hello, jeśli nie zostaną automatycznie zamknięte i wrócić toohello kartę hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b55dd-227">Close hello empty browser tab that launched hello dialog box if it is not automatically closed and get back toohello tab with hello Azure portal.</span></span>

         <span data-ttu-id="b55dd-228">Na komputerze bramy hello, te poświadczenia są **zaszyfrowanych** za pomocą certyfikatu, który hello fabryki danych jest właścicielem usługi.</span><span class="sxs-lookup"><span data-stu-id="b55dd-228">On hello gateway machine, these credentials are **encrypted** by using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="b55dd-229">Jeśli chcesz toouse hello certyfikatu, który jest skojarzony z hello brama zarządzania danymi zamiast tego zobacz [bezpiecznie ustawić poświadczenia](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="b55dd-229">If you want toouse hello certificate that is associated with hello Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="b55dd-230">Kliknij przycisk **Wdróż** na pasku hello toodeploy usługi SQL Server połączone poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-230">Click **Deploy** on hello command bar toodeploy hello SQL Server linked service.</span></span> <span data-ttu-id="b55dd-231">Usługa hello połączone w widoku drzewa hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="b55dd-231">You should see hello linked service in hello tree view.</span></span>

      ![Usługi SQL Server połączone w widoku drzewa hello](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="b55dd-233">Dodaj połączonej usługi dla konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b55dd-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="b55dd-234">W hello **Edytor fabryki danych**, kliknij przycisk **nowy magazyn danych** hello pasek poleceń i kliknij przycisk **magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-234">In hello **Data Factory Editor**, click **New data store** on hello command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="b55dd-235">Wprowadź nazwę hello konta magazynu Azure hello **nazwa konta**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-235">Enter hello name of your Azure storage account for hello **Account name**.</span></span>
3. <span data-ttu-id="b55dd-236">Wprowadź klucz powitania dla konta magazynu Azure hello **klucz konta**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-236">Enter hello key for your Azure storage account for hello **Account key**.</span></span>
4. <span data-ttu-id="b55dd-237">Kliknij przycisk **Wdróż** toodeploy hello **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-237">Click **Deploy** toodeploy hello **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="b55dd-238">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="b55dd-238">Create datasets</span></span>
<span data-ttu-id="b55dd-239">W tym kroku Tworzenie danych wejściowych i wyjściowych zestawów danych, które zawierają dane wejściowe i wyjściowe dla operacji kopiowania hello (bazy danych serwera SQL lokalnymi = > magazynu obiektów blob platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="b55dd-239">In this step, you create input and output datasets that represent input and output data for hello copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="b55dd-240">Przed utworzeniem zestawów danych, hello następujące kroki (szczegółowy opis kroków następująca liście hello):</span><span class="sxs-lookup"><span data-stu-id="b55dd-240">Before creating datasets, do hello following steps (detailed steps follows hello list):</span></span>

* <span data-ttu-id="b55dd-241">Tworzenie tabeli o nazwie **pustych elementów** w hello dodany jako fabryki danych toohello połączonej usługi bazy danych serwera SQL i Wstaw kilka przykładowych wpisów do tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-241">Create a table named **emp** in hello SQL Server Database you added as a linked service toohello data factory and insert a couple of sample entries into hello table.</span></span>
* <span data-ttu-id="b55dd-242">Tworzenie kontenera obiektów blob o nazwie **adftutorial** w hello Azure blob dodany jako połączonej usługi fabryki danych toohello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="b55dd-242">Create a blob container named **adftutorial** in hello Azure blob storage account you added as a linked service toohello data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a><span data-ttu-id="b55dd-243">Przygotowanie lokalnego programu SQL Server w samouczku hello</span><span class="sxs-lookup"><span data-stu-id="b55dd-243">Prepare On-premises SQL Server for hello tutorial</span></span>
1. <span data-ttu-id="b55dd-244">W bazie danych hello określony dla hello lokalnego programu SQL Server połączone usługi (**SqlServerLinkedService**), użyj powitania po hello toocreate skryptu SQL **pustych elementów** tabeli w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-244">In hello database you specified for hello on-premises SQL Server linked service (**SqlServerLinkedService**), use hello following SQL script toocreate hello **emp** table in hello database.</span></span>

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
2. <span data-ttu-id="b55dd-245">Wstaw niektóre przykładowe do tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="b55dd-245">Insert some sample into hello table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="b55dd-246">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="b55dd-246">Create input dataset</span></span>

1. <span data-ttu-id="b55dd-247">W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej**, kliknij przycisk **nowy zestaw danych** hello pasek poleceń i kliknij przycisk **tabeli programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-247">In hello **Data Factory Editor**, click **... More**, click **New dataset** on hello command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="b55dd-248">Zastąp hello JSON w okienku po prawej stronie powitania hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="b55dd-248">Replace hello JSON in hello right pane with hello following text:</span></span>

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
   <span data-ttu-id="b55dd-249">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="b55dd-249">Note hello following points:</span></span>

   * <span data-ttu-id="b55dd-250">**Typ** ustawiono zbyt**SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-250">**type** is set too**SqlServerTable**.</span></span>
   * <span data-ttu-id="b55dd-251">**tableName** ustawiono zbyt**pustych elementów**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-251">**tableName** is set too**emp**.</span></span>
   * <span data-ttu-id="b55dd-252">**linkedServiceName** ustawiono zbyt**SqlServerLinkedService** (tej połączonej usługi ma utworzone we wcześniejszej części tego przewodnika.).</span><span class="sxs-lookup"><span data-stu-id="b55dd-252">**linkedServiceName** is set too**SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="b55dd-253">Wejściowy zestaw danych nie jest generowany przez inny potok w fabryce danych Azure, należy ustawić **zewnętrznych** za**true**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** too**true**.</span></span> <span data-ttu-id="b55dd-254">Wskazuje on, że hello danych wejściowych jest także toohello zewnętrznej usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="b55dd-254">It denotes hello input data is produced external toohello Azure Data Factory service.</span></span> <span data-ttu-id="b55dd-255">Opcjonalnie można określić żadnych zasad danych zewnętrznych przy użyciu hello **externalData** element hello **zasad** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b55dd-255">You can optionally specify any external data policies using hello **externalData** element in hello **Policy** section.</span></span>    

   <span data-ttu-id="b55dd-256">Zobacz [przenoszenie danych do/z programu SQL Server](data-factory-sqlserver-connector.md) szczegółowe informacje na temat właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="b55dd-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="b55dd-257">Kliknij przycisk **Wdróż** polecenie hello paska toodeploy hello dataset.</span><span class="sxs-lookup"><span data-stu-id="b55dd-257">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="b55dd-258">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="b55dd-258">Create output dataset</span></span>

1. <span data-ttu-id="b55dd-259">W hello **Edytor fabryki danych**, kliknij przycisk **nowy zestaw danych** hello pasek poleceń i kliknij przycisk **magazynu obiektów Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-259">In hello **Data Factory Editor**, click **New dataset** on hello command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="b55dd-260">Zastąp hello JSON w okienku po prawej stronie powitania hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="b55dd-260">Replace hello JSON in hello right pane with hello following text:</span></span>

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
   <span data-ttu-id="b55dd-261">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="b55dd-261">Note hello following points:</span></span>

   * <span data-ttu-id="b55dd-262">**Typ** ustawiono zbyt**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-262">**type** is set too**AzureBlob**.</span></span>
   * <span data-ttu-id="b55dd-263">**linkedServiceName** ustawiono zbyt**AzureStorageLinkedService** (w kroku 2 została utworzona tej połączonej usługi).</span><span class="sxs-lookup"><span data-stu-id="b55dd-263">**linkedServiceName** is set too**AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="b55dd-264">**folderPath** ustawiono zbyt**adftutorial/outfromonpremdf** gdzie outfromonpremdf jest hello w kontenerze adftutorial hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-264">**folderPath** is set too**adftutorial/outfromonpremdf** where outfromonpremdf is hello folder in hello adftutorial container.</span></span> <span data-ttu-id="b55dd-265">Utwórz hello **adftutorial** kontener, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="b55dd-265">Create hello **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="b55dd-266">Hello **dostępności** ustawiono zbyt**co godzinę** (**częstotliwość** ustawić także**godzina** i **interwał** ustawić także **1**).</span><span class="sxs-lookup"><span data-stu-id="b55dd-266">hello **availability** is set too**hourly** (**frequency** set too**hour** and **interval** set too**1**).</span></span>  <span data-ttu-id="b55dd-267">Witaj usługi fabryka danych generuje wycinek danych wyjściowych co godzinę w hello **pustych elementów** tabeli w hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b55dd-267">hello Data Factory service generates an output data slice every hour in hello **emp** table in hello Azure SQL Database.</span></span>

   <span data-ttu-id="b55dd-268">Jeśli nie określisz **fileName** dla **tabeli wyników**, hello wygenerowanych plików w hello **folderPath** mają nazwy w hello następującego formatu: danych.<Guid>. txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="b55dd-268">If you do not specify a **fileName** for an **output table**, hello generated files in hello **folderPath** are named in hello following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="b55dd-269">tooset **folderPath** i **fileName** dynamicznie w oparciu hello **SliceStart** czasu, użyj właściwości partitionedBy hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-269">tooset **folderPath** and **fileName** dynamically based on hello **SliceStart** time, use hello partitionedBy property.</span></span> <span data-ttu-id="b55dd-270">W hello poniższy przykład, folderPath korzysta rok, miesiąc i dzień z hello SliceStart (czas rozpoczęcia przetwarzania wycinka hello), a nazwa pliku godzinę z hello SliceStart.</span><span class="sxs-lookup"><span data-stu-id="b55dd-270">In hello following example, folderPath uses Year, Month, and Day from hello SliceStart (start time of hello slice being processed) and fileName uses Hour from hello SliceStart.</span></span> <span data-ttu-id="b55dd-271">Na przykład, jeśli wycinek jest tworzonym dla 2014-10-20T08:00:00, nazwa_folderu hello ustawiono toowikidatagateway/wikisampledataout/2014/10/20 i hello fileName ustawiono too08.csv.</span><span class="sxs-lookup"><span data-stu-id="b55dd-271">For example, if a slice is being produced for 2014-10-20T08:00:00, hello folderName is set toowikidatagateway/wikisampledataout/2014/10/20 and hello fileName is set too08.csv.</span></span>

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

    <span data-ttu-id="b55dd-272">Zobacz [przenoszenie danych do/z magazynu obiektów Blob Azure](data-factory-azure-blob-connector.md) szczegółowe informacje na temat właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="b55dd-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="b55dd-273">Kliknij przycisk **Wdróż** polecenie hello paska toodeploy hello dataset.</span><span class="sxs-lookup"><span data-stu-id="b55dd-273">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span> <span data-ttu-id="b55dd-274">Upewnij się, że oba zestawy danych hello w widoku drzewa hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="b55dd-274">Confirm that you see both hello datasets in hello tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="b55dd-275">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="b55dd-275">Create pipeline</span></span>
<span data-ttu-id="b55dd-276">W tym kroku utworzysz **potoku** z jednym **działanie kopiowania** używającą **EmpOnPremSQLTable** jako dane wejściowe i **OutputBlobTable** jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="b55dd-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="b55dd-277">Kliknij w Edytor fabryki danych **... Więcej** i **Nowy potok**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="b55dd-278">Zastąp hello JSON w okienku po prawej stronie powitania hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="b55dd-278">Replace hello JSON in hello right pane with hello following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
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
   > <span data-ttu-id="b55dd-279">Zastąp wartość hello hello **start** właściwość o hello bieżącego dnia i **zakończenia** wartości z hello następnego dnia.</span><span class="sxs-lookup"><span data-stu-id="b55dd-279">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span>
   >
   >

   <span data-ttu-id="b55dd-280">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="b55dd-280">Note hello following points:</span></span>

   * <span data-ttu-id="b55dd-281">W sekcji działania hello jest tylko działania którego **typu** ustawiono zbyt**kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-281">In hello activities section, there is only activity whose **type** is set too**Copy**.</span></span>
   * <span data-ttu-id="b55dd-282">**Dane wejściowe** dla działania hello jest ustawiony za**EmpOnPremSQLTable** i **dane wyjściowe** dla działania hello jest ustawiony za**OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-282">**Input** for hello activity is set too**EmpOnPremSQLTable** and **output** for hello activity is set too**OutputBlobTable**.</span></span>
   * <span data-ttu-id="b55dd-283">W hello **typeProperties** sekcji **SqlSource** jest określony jako hello **typ źródła** i ** BlobSink ** jest określony jako hello **sink typu**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-283">In hello **typeProperties** section, **SqlSource** is specified as hello **source type** and **BlobSink **is specified as hello **sink type**.</span></span>
   * <span data-ttu-id="b55dd-284">Zapytanie SQL `select * from emp` określono hello **sqlReaderQuery** właściwość **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-284">SQL query `select * from emp` is specified for hello **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="b55dd-285">Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="b55dd-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="b55dd-286">Na przykład: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="b55dd-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="b55dd-287">Witaj **zakończenia** czasu jest opcjonalne, ale możemy użyć w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b55dd-287">hello **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="b55dd-288">Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin**".</span><span class="sxs-lookup"><span data-stu-id="b55dd-288">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="b55dd-289">potok hello toorun przez czas nieokreślony, określ **9/9/9999** jako wartość hello hello **zakończenia** właściwości.</span><span class="sxs-lookup"><span data-stu-id="b55dd-289">toorun hello pipeline indefinitely, specify **9/9/9999** as hello value for hello **end** property.</span></span>

   <span data-ttu-id="b55dd-290">Definiujesz hello czas trwania w których hello są przetwarzane wycinków danych oparte na powitania **dostępności** właściwości, które zostały zdefiniowane dla każdego zestawu danych z fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="b55dd-290">You are defining hello time duration in which hello data slices are processed based on hello **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="b55dd-291">Przykład Witaj istnieją 24 wycinków danych jak każdy wycinek danych jest tworzone co godzinę.</span><span class="sxs-lookup"><span data-stu-id="b55dd-291">In hello example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="b55dd-292">Kliknij przycisk **Wdróż** na pasku toodeploy hello dataset poleceń hello (tabela jest prostokątny zestawu danych).</span><span class="sxs-lookup"><span data-stu-id="b55dd-292">Click **Deploy** on hello command bar toodeploy hello dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="b55dd-293">Potwierdzenie tego potoku hello zostaną wyświetlone w widoku drzewa hello w **potoki** węzła.</span><span class="sxs-lookup"><span data-stu-id="b55dd-293">Confirm that hello pipeline shows up in hello tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="b55dd-294">Teraz, kliknij przycisk **X** dwukrotnie tooclose hello strony tooget wstecz toohello **fabryki danych** stronę hello **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-294">Now, click **X** twice tooclose hello page tooget back toohello **Data Factory** page for hello **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="b55dd-295">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="b55dd-295">**Congratulations!**</span></span> <span data-ttu-id="b55dd-296">Pomyślnie utworzono fabryki danych Azure, połączone usługi, zestawów danych oraz potoku i zaplanowane hello potoku.</span><span class="sxs-lookup"><span data-stu-id="b55dd-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled hello pipeline.</span></span>

#### <a name="view-hello-data-factory-in-a-diagram-view"></a><span data-ttu-id="b55dd-297">Fabryka danych hello widoku w widoku diagramu</span><span class="sxs-lookup"><span data-stu-id="b55dd-297">View hello data factory in a Diagram View</span></span>
1. <span data-ttu-id="b55dd-298">W hello **portalu Azure**, kliknij przycisk **Diagram** kafelka na stronie głównej hello hello **ADFTutorialOnPremDF** fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="b55dd-298">In hello **Azure portal**, click **Diagram** tile on hello home page for hello **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="b55dd-299">:</span><span class="sxs-lookup"><span data-stu-id="b55dd-299">:</span></span>

    ![Diagram łącza](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="b55dd-301">Powinny pojawić się toohello podobne diagram powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="b55dd-301">You should see hello diagram similar toohello following image:</span></span>

    ![Widok diagramu](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="b55dd-303">Powiększ, pomniejszyć powiększenia too100%, toofit powiększenia, automatycznie potoki pozycji i zestawów danych i Pokaż elementy powiązane informacje (wyróżnia elementy nadrzędne i podrzędne wybranego elementu).</span><span class="sxs-lookup"><span data-stu-id="b55dd-303">You can zoom in, zoom out, zoom too100%, zoom toofit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="b55dd-304">Możesz kliknąć dwukrotnie właściwości toosee obiektu (dataset wejścia/wyjścia lub potoku) dla niego.</span><span class="sxs-lookup"><span data-stu-id="b55dd-304">You can double-click an object (input/output dataset or pipeline) toosee properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="b55dd-305">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="b55dd-305">Monitor pipeline</span></span>
<span data-ttu-id="b55dd-306">W tym kroku użyjesz hello Azure toomonitor portalu, co się dzieje w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="b55dd-306">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="b55dd-307">Można również użyć zestawy danych toomonitor poleceń cmdlet programu PowerShell i potoki.</span><span class="sxs-lookup"><span data-stu-id="b55dd-307">You can also use PowerShell cmdlets toomonitor datasets and pipelines.</span></span> <span data-ttu-id="b55dd-308">Aby uzyskać szczegółowe informacje o monitorowaniu, zobacz [monitorować i zarządzać potoki](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="b55dd-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="b55dd-309">Na diagramie powitania kliknij dwukrotnie **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-309">In hello diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Wycinki EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="b55dd-311">Należy zauważyć, że wszystkie dane hello wycinków zapasowej znajdują się w **gotowe** stanu, ponieważ czas trwania potoku hello (czas rozpoczęcia czasu tooend) jest w przeszłości hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-311">Notice that all hello data slices up are in **Ready** state because hello pipeline duration (start time tooend time) is in hello past.</span></span> <span data-ttu-id="b55dd-312">To również, że wstawiono hello danych w bazie danych programu SQL Server hello i będzie cały czas hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-312">It is also because you have inserted hello data in hello SQL Server database and it is there all hello time.</span></span> <span data-ttu-id="b55dd-313">Upewnij się, że brak wycinków widoczne w hello **wycinków Problem** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-313">Confirm that no slices show up in hello **Problem slices** section at hello bottom.</span></span> <span data-ttu-id="b55dd-314">tooview wszystkie fragmenty hello, kliknij przycisk **Zobacz więcej** u dołu listy hello wycinków hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-314">tooview all hello slices, click **See More** at hello bottom of hello list of slices.</span></span>
3. <span data-ttu-id="b55dd-315">Teraz, w hello **zestawów danych** kliknij przycisk **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-315">Now, In hello **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Wycinki OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="b55dd-317">Kliknij wycinek żadnych danych z listy hello i powinna zostać wyświetlona hello **wycinka danych** strony.</span><span class="sxs-lookup"><span data-stu-id="b55dd-317">Click any data slice from hello list and you should see hello **Data Slice** page.</span></span> <span data-ttu-id="b55dd-318">Widać, że działanie jest uruchomione wycinek hello.</span><span class="sxs-lookup"><span data-stu-id="b55dd-318">You see activity runs for hello slice.</span></span> <span data-ttu-id="b55dd-319">Użytkownik widzi tylko jedno działanie Uruchom zwykle.</span><span class="sxs-lookup"><span data-stu-id="b55dd-319">You see only one activity run usually.</span></span>  

    ![Blok wycinek danych](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="b55dd-321">Jeśli hello wycinka nie jest hello **gotowe** stanu, można zobaczyć hello niegotowe wycinki strumienia wychodzącego nie jest gotowa i blokuje hello bieżący fragment wykonywanie w hello **wycinków strumienia wychodzącego, które nie są gotowe** listy.</span><span class="sxs-lookup"><span data-stu-id="b55dd-321">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="b55dd-322">Kliknij przycisk hello **uruchamiania działania** z listy hello na powitania dolnej toosee **szczegóły uruchomienia działania**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-322">Click hello **activity run** from hello list at hello bottom toosee **activity run details**.</span></span>

   ![Strona szczegółów uruchomienia działania](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="b55dd-324">Zobaczysz informacje, takie jak przepustowość, czas trwania i brama hello użyty tootransfer hello danych.</span><span class="sxs-lookup"><span data-stu-id="b55dd-324">You would see information such as throughput, duration, and hello gateway used tootransfer hello data.</span></span>
6. <span data-ttu-id="b55dd-325">Kliknij przycisk **X** tooclose wszystkie hello aż do strony</span><span class="sxs-lookup"><span data-stu-id="b55dd-325">Click **X** tooclose all hello pages until you</span></span>
7. <span data-ttu-id="b55dd-326">wrócić toohello strony głównej dla hello **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-326">get back toohello home page for hello **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="b55dd-327">(opcjonalnie) Kliknij przycisk **potoki**, kliknij przycisk **ADFTutorialOnPremDF**oraz szczegółowy tabel wejściowych (**zużyto**) lub wyjściowych zestawów danych (**produkcji**).</span><span class="sxs-lookup"><span data-stu-id="b55dd-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="b55dd-328">Użyj narzędzia takiego jak [Eksploratora usługi Storage Microsoft](http://storageexplorer.com/) tooverify utworzony obiekt blob/plik dla każdej godziny.</span><span class="sxs-lookup"><span data-stu-id="b55dd-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) tooverify that a blob/file is created for each hour.</span></span>

   ![Eksplorator usługi Azure Storage](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="b55dd-330">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b55dd-330">Next steps</span></span>
* <span data-ttu-id="b55dd-331">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu dla wszystkich hello szczegółowe informacje o hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="b55dd-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello Data Management Gateway.</span></span>
* <span data-ttu-id="b55dd-332">Zobacz [kopiowanie danych z obiektu Blob Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn o jak toouse działanie kopiowania toomove danych ze źródła danych przechowywane tooa ujście danych magazynu.</span><span class="sxs-lookup"><span data-stu-id="b55dd-332">See [Copy data from Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn about how toouse Copy Activity toomove data from a source data store tooa sink data store.</span></span>
