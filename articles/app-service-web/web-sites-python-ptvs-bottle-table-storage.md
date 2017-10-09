---
title: "aaaBottle i Azure Table Storage na platformie Azure za pomocą narzędzia Python Tools 2.2 for Visual Studio"
description: "Dowiedz się, jak toouse hello narzędzi Python Tools dla Visual Studio toocreate aplikacji Bottle, która przechowuje dane w magazynie tabel platformy Azure i wdrażanie tooAzure aplikacji sieci web hello aplikacji usługi sieci Web aplikacji."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="1820d-103">Bottle i magazynu tabel platformy Azure na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1820d-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="1820d-104">W tym samouczku użyjemy [narzędzi Python Tools for Visual Studio] toocreate prostą sonduje aplikacji sieci web przy użyciu jednej z hello PTVS przykładowe szablony.</span><span class="sxs-lookup"><span data-stu-id="1820d-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="1820d-105">W tym samouczku jest również dostępny jako [wideo](https://www.youtube.com/watch?v=GJXDGaEPy94).</span><span class="sxs-lookup"><span data-stu-id="1820d-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="1820d-106">aplikacji sieci web sond Hello definiuje abstrakcję do repozytorium, więc można łatwo przełączać się między różnymi typami repozytoriów (w pamięci, magazynu tabel Azure, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="1820d-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="1820d-107">Dowiesz się, jak konto toocreate magazynu Azure, jak tooconfigure hello toouse aplikacji sieci web Azure Table Storage i jak toopublish hello aplikacji sieci web zbyt[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="1820d-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="1820d-108">Zobacz hello [Centrum deweloperów języka Python] więcej artykułów o programowaniu aplikacji sieci Web usługi aplikacji Azure z narzędziami PTVS przy użyciu Bottle, Flask i Django oraz sieci web z usługami bazy danych MongoDB, Magazyn tabel Azure, MySQL i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="1820d-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="1820d-109">Gdy ten artykuł dotyczy usługi App Service, hello kroki są podobne do programowania [usługi w chmurze Azure].</span><span class="sxs-lookup"><span data-stu-id="1820d-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1820d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1820d-110">Prerequisites</span></span>
* <span data-ttu-id="1820d-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="1820d-111">Visual Studio 2015</span></span>
* <span data-ttu-id="1820d-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="1820d-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="1820d-113">[Python Tools 2.2 for Visual Studio przykładów VSIX]</span><span class="sxs-lookup"><span data-stu-id="1820d-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="1820d-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="1820d-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="1820d-115">[32-bitowe środowisko Python w wersji 2.7] lub [32-bitowe środowisko Python w wersji 3.4]</span><span class="sxs-lookup"><span data-stu-id="1820d-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="1820d-116">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="1820d-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1820d-117">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="1820d-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="1820d-118">Utwórz hello projektu</span><span class="sxs-lookup"><span data-stu-id="1820d-118">Create hello Project</span></span>
<span data-ttu-id="1820d-119">W tej sekcji utworzymy projektu programu Visual Studio przy użyciu przykładowego szablonu.</span><span class="sxs-lookup"><span data-stu-id="1820d-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="1820d-120">Firma Microsoft będzie utworzyć środowisko wirtualne i zainstalujesz wymagane pakiety.</span><span class="sxs-lookup"><span data-stu-id="1820d-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="1820d-121">Następnie zostanie uruchomiony aplikacji hello lokalnie za pomocą hello domyślne w pamięci repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1820d-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="1820d-122">W programie Visual Studio wybierz pozycje **Plik**, **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="1820d-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="1820d-123">Szablony projektu z hello Hello [Python Tools 2.2 for Visual Studio przykładów VSIX] są dostępne w ramach **Python**, **przykłady**.</span><span class="sxs-lookup"><span data-stu-id="1820d-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="1820d-124">Wybierz **projektu sieci Web Bottle sond** i kliknij przycisk OK toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="1820d-124">Select **Polls Bottle Web Project** and click OK toocreate hello project.</span></span>
   
     ![Okno dialogowe Nowy projekt](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="1820d-126">Pakiety zewnętrzne zostanie wyświetlony monit o tooinstall będzie.</span><span class="sxs-lookup"><span data-stu-id="1820d-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="1820d-127">Wybierz pozycję **Zainstaluj w środowisku wirtualnym**.</span><span class="sxs-lookup"><span data-stu-id="1820d-127">Select **Install into a virtual environment**.</span></span>
   
     ![Okno dialogowe Pakiety zewnętrzne](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="1820d-129">Wybierz **Python 2.7** lub **języka Python 3.4** jako podstawowy interpreter hello.</span><span class="sxs-lookup"><span data-stu-id="1820d-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Okno dialogowe Dodawanie środowiska wirtualnego](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="1820d-131">Upewnij się, że aplikacja hello działa, naciskając `F5`.</span><span class="sxs-lookup"><span data-stu-id="1820d-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="1820d-132">Domyślnie aplikacja hello używa repozytorium w pamięci, które nie wymaga żadnej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1820d-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="1820d-133">Wszystkie dane zostaną utracone, gdy serwer sieci web hello jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="1820d-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="1820d-134">Kliknij przycisk **tworzenie przykładowej ankiety**, kliknij ankietę i Zagłosuj.</span><span class="sxs-lookup"><span data-stu-id="1820d-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="1820d-136">Utwórz konto magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1820d-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="1820d-137">operacje magazynu toouse, potrzebne jest konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="1820d-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="1820d-138">Można utworzyć konta magazynu, wykonując następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="1820d-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="1820d-139">Zaloguj się do hello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1820d-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1820d-140">Kliknij przycisk hello **nowy** ikony na górze hello rogu hello portalu, kliknij przycisk **dane i magazyn** > **konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="1820d-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="1820d-141">Kliknij przycisk hello **Utwórz** przycisk, a następnie nadaj unikatową nazwę konta magazynu hello i utworzyć nową [grupy zasobów](../azure-resource-manager/resource-group-overview.md) dla niego.</span><span class="sxs-lookup"><span data-stu-id="1820d-141">Click hello **Create** button, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Szybkie tworzenie](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="1820d-143">Po utworzeniu konta magazynu hello hello **powiadomienia** przycisk będzie flash zielona **Powodzenie** i bloku konto magazynu hello jest otwarty tooshow należy toohello nowy zasób grupy utworzony.</span><span class="sxs-lookup"><span data-stu-id="1820d-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="1820d-144">Kliknij przycisk hello **klucze dostępu** część w bloku konto magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="1820d-144">Click hello **Access keys** part in hello storage account's blade.</span></span> <span data-ttu-id="1820d-145">Zanotuj nazwę konta hello i klucz1.</span><span class="sxs-lookup"><span data-stu-id="1820d-145">Take note of hello account name and key1.</span></span>
   
      ![Klucze](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="1820d-147">Projekt w następnej sekcji hello są wymagane tooconfigure tej informacji.</span><span class="sxs-lookup"><span data-stu-id="1820d-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="1820d-148">Skonfiguruj hello projektu</span><span class="sxs-lookup"><span data-stu-id="1820d-148">Configure hello Project</span></span>
<span data-ttu-id="1820d-149">W tej sekcji skonfigurujemy naszej aplikacji toouse hello konta magazynu, którą właśnie utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="1820d-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="1820d-150">Następnie aplikacja hello zostanie uruchomiony lokalnie.</span><span class="sxs-lookup"><span data-stu-id="1820d-150">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="1820d-151">W programie Visual Studio, kliknij prawym przyciskiem myszy węzeł projektu w Eksploratorze rozwiązań i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="1820d-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="1820d-152">Polecenie hello **debugowania** kartę.</span><span class="sxs-lookup"><span data-stu-id="1820d-152">Click on hello **Debug** tab.</span></span>
   
     ![Ustawienia debugowania projektu](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="1820d-154">Ustaw wartości hello wymagane przez aplikację hello w zmiennych środowiskowych **polecenia Debug serwera**, **środowiska**.</span><span class="sxs-lookup"><span data-stu-id="1820d-154">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="1820d-155">Spowoduje to ustawienie zmiennych środowiskowych hello podczas możesz **Rozpocznij debugowanie**.</span><span class="sxs-lookup"><span data-stu-id="1820d-155">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="1820d-156">Toobe zmienne hello ustawić podczas możesz **uruchomić bez debugowania**, hello zestaw takie same wartości w obszarze **uruchamiania polecenia serwera** również.</span><span class="sxs-lookup"><span data-stu-id="1820d-156">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="1820d-157">Alternatywnie można zdefiniować zmienne środowiskowe za pomocą Panelu sterowania systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="1820d-157">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="1820d-158">Jest lepszym rozwiązaniem, jeśli chcesz tooavoid przechowywania poświadczeń w kodzie źródłowym / pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="1820d-158">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="1820d-159">Należy pamiętać, że konieczne będzie toorestart programu Visual Studio dla nowego środowiska hello wartości toobe toohello dostępnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1820d-159">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="1820d-160">Kod Hello implementuje repozytorium Azure Table Storage hello jest **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="1820d-160">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="1820d-161">Zobacz hello [dokumentacji] Aby uzyskać więcej informacji na temat toouse usługi tabel w języku Python.</span><span class="sxs-lookup"><span data-stu-id="1820d-161">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="1820d-162">Uruchamianie aplikacji hello z `F5`.</span><span class="sxs-lookup"><span data-stu-id="1820d-162">Run hello application with `F5`.</span></span> <span data-ttu-id="1820d-163">Ankieta utworzona za pomocą **tworzenie przykładowej ankiety** i hello dane przesłane podczas głosowania zostaną zserializowane w magazynu tabel platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1820d-163">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1820d-164">Hello środowiska wirtualnego Python 2.7 może spowodować wyjątek podziału w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1820d-164">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="1820d-165">Naciśnij klawisz `F5` toocontinue ładowania hello projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="1820d-165">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="1820d-166">Przeglądaj toohello **o** tooverify strony, która aplikacja hello używa hello **Azure Table Storage** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1820d-166">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="1820d-168">Eksploruj hello Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="1820d-168">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="1820d-169">Jest łatwy tooview i edytowanie tabel do przechowywania Eksploratorze chmury w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1820d-169">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="1820d-170">W tej sekcji użyjemy Eksploratora serwera tooview hello zawartość tabel aplikacji hello ankiety.</span><span class="sxs-lookup"><span data-stu-id="1820d-170">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="1820d-171">Wymaga to Microsoft Azure Tools toobe zainstalowane, które są dostępne jako część hello [zestawu Azure SDK dla platformy .NET].</span><span class="sxs-lookup"><span data-stu-id="1820d-171">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="1820d-172">Otwórz **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="1820d-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="1820d-173">Rozwiń węzeł **kont magazynu**, konta magazynu, następnie **tabel**.</span><span class="sxs-lookup"><span data-stu-id="1820d-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Eksplorator chmury](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="1820d-175">Kliknij dwukrotnie hello **sond** lub **opcji** tabeli tooview hello zawartości tabeli hello w oknie dokumentu, a także dodawanie/usuwanie/edytowanie jednostek.</span><span class="sxs-lookup"><span data-stu-id="1820d-175">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Wyniki zapytania w tabeli](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="1820d-177">Publikowanie tooAzure aplikacji sieci web hello usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="1820d-177">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="1820d-178">Hello Azure .NET SDK udostępnia toodeploy łatwy sposób tooAzure aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1820d-178">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="1820d-179">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="1820d-179">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Okno dialogowe Publikowanie w sieci Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="1820d-181">Kliknij pozycję **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="1820d-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="1820d-182">Polecenie **nowy** toocreate nowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1820d-182">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="1820d-183">Wypełnij następujące pola hello i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1820d-183">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="1820d-184">**Nazwa aplikacji sieci Web**</span><span class="sxs-lookup"><span data-stu-id="1820d-184">**Web App name**</span></span>
   * <span data-ttu-id="1820d-185">**Plan usługi App Service**</span><span class="sxs-lookup"><span data-stu-id="1820d-185">**App Service plan**</span></span>
   * <span data-ttu-id="1820d-186">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="1820d-186">**Resource group**</span></span>
   * <span data-ttu-id="1820d-187">**Region**</span><span class="sxs-lookup"><span data-stu-id="1820d-187">**Region**</span></span>
   * <span data-ttu-id="1820d-188">Pozostaw **serwera bazy danych** ustawić także**bazy danych**</span><span class="sxs-lookup"><span data-stu-id="1820d-188">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="1820d-189">Zaakceptuj wszystkie inne ustawienia domyślne i kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="1820d-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="1820d-190">Przeglądarki sieci web zostanie otwarty toohello opublikowana aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="1820d-190">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="1820d-191">Jeśli przeglądania toohello o stronie zostanie wyświetlone, korzysta z hello **w pamięci** repozytorium, nie hello **Azure Table Storage** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1820d-191">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="1820d-192">Jest to spowodowane hello zmienne środowiskowe nie są ustawione na powitania wystąpienia aplikacji sieci Web w usłudze Azure App Service, więc używa hello domyślne wartości podanych w tym **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="1820d-192">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="1820d-193">Skonfiguruj hello wystąpienie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="1820d-193">Configure hello Web Apps instance</span></span>
<span data-ttu-id="1820d-194">W tej sekcji skonfigurujemy zmiennych środowiskowych dla hello wystąpienia aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1820d-194">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="1820d-195">W [portalu Azure], otwarcie bloku aplikacji sieci web hello klikając **Przeglądaj** > **usługi aplikacji** > Nazwa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1820d-195">In [Azure Portal], open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="1820d-196">W bloku aplikacja sieci web, kliknij przycisk **wszystkie ustawienia**, następnie kliknij przycisk **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="1820d-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="1820d-197">Przewiń w dół toohello **ustawień aplikacji** sekcji i ustawiać wartości hello **REPOZYTORIUM\_nazwa**, **MAGAZYNU\_nazwa** i  **Magazyn\_klucza** zgodnie z opisem w hello **projektu hello Konfiguruj** powyższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1820d-197">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![Ustawienia aplikacji](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="1820d-199">Kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1820d-199">Click on **Save**.</span></span> <span data-ttu-id="1820d-200">Po otrzymaniu powiadomienia hello czy hello zmiany zostały zastosowane, kliknij **Przeglądaj** z głównego bloku aplikacja sieci Web hello.</span><span class="sxs-lookup"><span data-stu-id="1820d-200">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="1820d-201">Powinny pojawić się pracy aplikacji sieci web hello zgodnie z oczekiwaniami, za pomocą hello **Azure Table Storage** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1820d-201">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="1820d-202">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1820d-202">Congratulations!</span></span>
   
     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="1820d-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1820d-204">Next steps</span></span>
<span data-ttu-id="1820d-205">Wykonaj te toolearn łącza więcej informacji na temat narzędzi Python Tools for Visual Studio, Bottle i Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="1820d-205">Follow these links toolearn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="1820d-206">[Dokumentacja narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="1820d-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="1820d-207">[Projekty sieci Web]</span><span class="sxs-lookup"><span data-stu-id="1820d-207">[Web Projects]</span></span>
  * <span data-ttu-id="1820d-208">[Projekty usługi w chmurze]</span><span class="sxs-lookup"><span data-stu-id="1820d-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="1820d-209">[Debugowanie zdalne na platformie Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="1820d-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="1820d-210">[Dokumentacja bottle]</span><span class="sxs-lookup"><span data-stu-id="1820d-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="1820d-211">[Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="1820d-211">[Azure Storage]</span></span>
* <span data-ttu-id="1820d-212">[Zestaw Azure SDK dla środowiska Python]</span><span class="sxs-lookup"><span data-stu-id="1820d-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="1820d-213">[Jak tooUse hello usługi Magazyn tabel w języku Python]</span><span class="sxs-lookup"><span data-stu-id="1820d-213">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="1820d-214">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="1820d-214">What's changed</span></span>
* <span data-ttu-id="1820d-215">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="1820d-215">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centrum deweloperów języka Python]: /develop/python/
[usługi w chmurze Azure]: ../cloud-services/cloud-services-python-ptvs.md
[dokumentacji]:../cosmos-db/table-storage-how-to-use-python.md
[Jak tooUse hello usługi Magazyn tabel w języku Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[portalu Azure]: https://portal.azure.com
[zestawu Azure SDK dla platformy .NET]: http://azure.microsoft.com/downloads/
[narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Python Tools 2.2 for Visual Studio przykładów VSIX]: http://go.microsoft.com/fwlink/?LinkId=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[32-bitowe środowisko Python w wersji 2.7]: http://go.microsoft.com/fwlink/?LinkId=517190
[32-bitowe środowisko Python w wersji 3.4]: http://go.microsoft.com/fwlink/?LinkId=517191
[Dokumentacja narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Dokumentacja bottle]: http://bottlepy.org/docs/dev/index.html
[Debugowanie zdalne na platformie Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projekty sieci Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projekty usługi w chmurze]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Storage]: http://azure.microsoft.com/documentation/services/storage/
[Zestaw Azure SDK dla środowiska Python]: https://github.com/Azure/azure-sdk-for-python
