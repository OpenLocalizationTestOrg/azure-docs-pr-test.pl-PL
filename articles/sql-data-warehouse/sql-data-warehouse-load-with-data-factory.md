---
title: "aaaLoad danych do usługi Azure SQL Data Warehouse — fabryki danych | Dokumentacja firmy Microsoft"
description: "W tym samouczku ładuje dane do usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure i korzysta z bazy danych programu SQL Server jako hello źródła danych."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="bca00-103">Ładowanie danych do usługi SQL Data Warehouse z fabryką danych</span><span class="sxs-lookup"><span data-stu-id="bca00-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="bca00-104">Fabryka danych Azure tooload danych można użyć do magazynu danych SQL Azure za pomocą dowolnego hello [obsługiwane magazyny danych źródła](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="bca00-104">You can use Azure Data Factory tooload data into Azure SQL Data Warehouse from any of hello [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="bca00-105">Na przykład można ładowania danych z bazy danych Azure SQL lub z bazą danych programu Oracle do magazynu danych SQL przy użyciu fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="bca00-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="bca00-106">Samouczek, w tym artykule przedstawiono sposób tooload danych z lokalnego serwera SQL bazy danych do magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="bca00-106">Tutorial in this article shows you how tooload data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="bca00-107">**Szacowanie czasu**: tego samouczka trwa około 10 – 15 minut toocomplete, po spełnieniu wymagań wstępnych hello.</span><span class="sxs-lookup"><span data-stu-id="bca00-107">**Time estimate**: This tutorial takes about 10-15 minutes toocomplete once hello prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bca00-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bca00-108">Prerequisites</span></span>

- <span data-ttu-id="bca00-109">Należy **bazy danych programu SQL Server** z tabel zawierających dane hello toobe kopiowane toohello usługi SQL data warehouse.</span><span class="sxs-lookup"><span data-stu-id="bca00-109">You need a **SQL Server database** with tables that contain hello data toobe copied over toohello SQL data warehouse.</span></span>  

- <span data-ttu-id="bca00-110">Należy online **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="bca00-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="bca00-111">Jeśli nie masz już magazyn danych, Dowiedz się, jak za[Utwórz magazyn danych SQL Azure](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="bca00-111">If you do not already have a data warehouse, learn how too[Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="bca00-112">Należy **konta magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="bca00-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="bca00-113">Jeśli nie masz już konto magazynu, Dowiedz się, jak za[Utwórz konto magazynu](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="bca00-113">If you do not already have a storage account, learn how too[Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="bca00-114">Aby uzyskać najlepszą wydajność, Znajdź konto magazynu hello i hello magazynu danych w hello sam region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bca00-114">For best performance, locate hello storage account and hello data warehouse in hello same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="bca00-115">Skonfiguruj fabryki danych</span><span class="sxs-lookup"><span data-stu-id="bca00-115">Configure a data factory</span></span>
1. <span data-ttu-id="bca00-116">Zaloguj się za toohello [portalu Azure][].</span><span class="sxs-lookup"><span data-stu-id="bca00-116">Log in toohello [Azure portal][].</span></span>
2. <span data-ttu-id="bca00-117">Znajdź magazynu danych i kliknij przycisk tooopen go.</span><span class="sxs-lookup"><span data-stu-id="bca00-117">Locate your data warehouse and click tooopen it.</span></span>
3. <span data-ttu-id="bca00-118">W głównym bloku hello kliknij **danych obciążenia** > **fabryki danych Azure**.</span><span class="sxs-lookup"><span data-stu-id="bca00-118">In hello main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Uruchom Kreatora ładowanie danych](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="bca00-120">Jeśli nie ma fabryki danych w ramach subskrypcji platformy Azure, zobacz **nowa fabryka danych** okno dialogowe w osobnej karcie hello przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="bca00-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of hello browser.</span></span> <span data-ttu-id="bca00-121">Wypełnij hello wymagane informacje, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bca00-121">Fill in hello requested information, and click **Create**.</span></span> <span data-ttu-id="bca00-122">Po utworzeniu fabryki danych hello hello **nowa fabryka danych** okno dialogowe zostanie zamknięte i zostanie wyświetlony hello **fabryki danych wybierz** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="bca00-122">After hello data factory is created, hello **New Data Factory** dialog box closes, and you see hello **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="bca00-123">Jeśli masz co najmniej jeden fabryki danych znajdujących się w hello subskrypcji platformy Azure, zobacz hello **fabryki danych wybierz** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="bca00-123">If you have one or more data factories already in hello Azure subscription, you see hello **Select Data Factory** dialog box.</span></span> <span data-ttu-id="bca00-124">W tym oknie można wybrać istniejącą fabrykę danych lub kliknij przycisk **Utwórz nowy fabryki danych** toocreate nowy.</span><span class="sxs-lookup"><span data-stu-id="bca00-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** toocreate a new one.</span></span>

    ![Konfigurowanie usługi fabryka danych](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="bca00-126">W hello **fabryki danych wybierz** okno dialogowe, hello **ładowanie danych** opcja jest domyślnie zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="bca00-126">In hello **Select Data Factory** dialog box, hello **Load data** option is selected by default.</span></span> <span data-ttu-id="bca00-127">Kliknij przycisk **dalej** toostart Tworzenie danych podczas ładowania zadania.</span><span class="sxs-lookup"><span data-stu-id="bca00-127">Click **Next** toostart creating a data loading task.</span></span>

## <a name="configure-hello-data-factory-properties"></a><span data-ttu-id="bca00-128">Skonfiguruj właściwości fabryki danych hello</span><span class="sxs-lookup"><span data-stu-id="bca00-128">Configure hello data factory properties</span></span>
<span data-ttu-id="bca00-129">Po utworzeniu fabryki danych hello następnym krokiem jest danych hello tooconfigure ładowania harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="bca00-129">Now that you have created a data factory, hello next step is tooconfigure hello data loading schedule.</span></span>

1. <span data-ttu-id="bca00-130">Aby uzyskać **Nazwa zadania**, wprowadź **DWLoadData fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="bca00-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="bca00-131">Użyj domyślnej hello **uruchom raz teraz** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="bca00-131">Use hello default **Run once now** option, click **Next**.</span></span>

    ![Skonfiguruj harmonogram obciążenia](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a><span data-ttu-id="bca00-133">Konfigurowanie magazynu danych źródła hello i bramy</span><span class="sxs-lookup"><span data-stu-id="bca00-133">Configure hello source data store and gateway</span></span>
<span data-ttu-id="bca00-134">Teraz nakaż fabryki danych o hello: lokalną bazą danych programu SQL Server z którego mają zostać tooload danych.</span><span class="sxs-lookup"><span data-stu-id="bca00-134">Now you tell Data Factory about hello on-premises SQL Server database from which you want tooload data.</span></span>

1. <span data-ttu-id="bca00-135">Wybierz **programu SQL Server** z hello obsługiwane źródła danych przechowywane w katalogu, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="bca00-135">Choose **SQL Server** from hello supported source data store catalog, and click **Next**.</span></span>

    ![Wybierz źródło programu SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="bca00-137">A **Określ hello lokalną bazą danych programu SQL Server** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="bca00-137">A **Specify hello on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="bca00-138">Witaj najpierw **nazwa połączenia** pole jest wypełniane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="bca00-138">hello first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="bca00-139">drugie pole Hello poprosi o podanie nazwy hello hello **bramy**.</span><span class="sxs-lookup"><span data-stu-id="bca00-139">hello second field asks for hello name of hello **Gateway**.</span></span> <span data-ttu-id="bca00-140">Jeśli korzystasz z istniejącą fabrykę danych, która ma już bramy, można użyć ponownie hello bramy, wybierając ją z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="bca00-140">If you are using an existing data factory that already has a gateway, you can reuse hello gateway by selecting it from hello drop-down list.</span></span> <span data-ttu-id="bca00-141">Kliknij przycisk hello **Tworzenie bramy** link toocreate brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="bca00-141">Click hello **Create Gateway** link toocreate a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="bca00-142">Jeśli Magazyn hello źródła danych działa lokalnie lub w maszynie wirtualnej platformy Azure IaaS, jest wymagana brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="bca00-142">If hello source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="bca00-143">Brama ma relację 1-1 z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="bca00-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="bca00-144">Nie można użyć z innego fabryki danych, ale mogą służyć przez wiele danych podczas ładowania zadania związane z w hello tej samej fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="bca00-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in hello same data factory.</span></span> <span data-ttu-id="bca00-145">Brama może być magazyny danych toomultiple tooconnect używanych podczas uruchamiania zadania ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="bca00-145">A gateway can be used tooconnect toomultiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="bca00-146">Aby uzyskać szczegółowe informacje na temat bramy hello, zobacz [brama zarządzania danymi](../data-factory/data-factory-data-management-gateway.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="bca00-146">For detailed information about hello gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="bca00-147">A **Tworzenie bramy** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="bca00-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="bca00-148">Wprowadź nazwę, **GatewayForDWLoading**i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bca00-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="bca00-149">A **konfigurowania bramy** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="bca00-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="bca00-150">Kliknij przycisk **uruchamiania instalacji ekspresowej na tym komputerze** tooautomatically pobierania, zainstaluj i zarejestruj bramę zarządzania danymi na bieżącym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bca00-150">Click **Launch express setup on this computer** tooautomatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="bca00-151">Witaj postęp jest wyświetlany w oknie podręcznym.</span><span class="sxs-lookup"><span data-stu-id="bca00-151">hello progress is shown in a pop-up window.</span></span> <span data-ttu-id="bca00-152">Jeśli maszyna hello nie można połączyć toohello magazynu danych, możesz ręcznie [pobieranie i instalowanie bramy hello](https://www.microsoft.com/download/details.aspx?id=39717) na komputerze, na którym można połączyć toohello danych przechowywania, a następnie użyj hello tooregister klucza.</span><span class="sxs-lookup"><span data-stu-id="bca00-152">If hello machine cannot connect toohello data store, you can manually [download and install hello gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect toohello data store, and then use hello key tooregister.</span></span>
    > [!NOTE]
    > <span data-ttu-id="bca00-153">Instalacja ekspresowa Hello natywnie współpracuje z Microsoft Edge i przeglądarki Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="bca00-153">hello express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="bca00-154">Jeśli używasz przeglądarki Google Chrome, należy najpierw zainstalować rozszerzenie ClickOnce hello ze sklepu Chrome web store.</span><span class="sxs-lookup"><span data-stu-id="bca00-154">If you are using Google Chrome, first install hello ClickOnce extension from Chrome web store.</span></span>

    ![Uruchamianie instalacji ekspresowej](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="bca00-156">Poczekaj, aż toocomplete instalacji bramy hello.</span><span class="sxs-lookup"><span data-stu-id="bca00-156">Wait for hello gateway setup toocomplete.</span></span> <span data-ttu-id="bca00-157">Po hello bramy zostało pomyślnie zarejestrowane i jest w trybie online, zamyka okno podręczne hello i nową bramę hello jest wyświetlana w polu Brama hello.</span><span class="sxs-lookup"><span data-stu-id="bca00-157">Once hello gateway is successfully registered and is online, hello pop-up window closes and hello new gateway appears in hello gateway field.</span></span> <span data-ttu-id="bca00-158">Następnie wypełnij hello rest wymagane pola w następujący sposób, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="bca00-158">Then fill in hello rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="bca00-159">**Nazwa serwera**: Nazwa hello lokalnego programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bca00-159">**Server name**: Name of hello on-premises SQL Server.</span></span>
    - <span data-ttu-id="bca00-160">**Nazwa bazy danych**: baza danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bca00-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="bca00-161">**Poświadczeń szyfrowania**: Użyj domyślnej hello "przez przeglądarkę sieci web".</span><span class="sxs-lookup"><span data-stu-id="bca00-161">**Credential encryption**: Use hello default "By web browser".</span></span>
    - <span data-ttu-id="bca00-162">**Typ uwierzytelniania**: Wybierz typ hello używasz uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="bca00-162">**Authentication type**: Choose hello type of authentication you are using.</span></span>
    - <span data-ttu-id="bca00-163">**Nazwa użytkownika** i **hasło**: Wprowadź hello nazwy użytkownika i hasła dla użytkownika, który ma uprawnienia toocopy hello danych.</span><span class="sxs-lookup"><span data-stu-id="bca00-163">**User name** and **password**: Enter hello user name and password for a user who has permission toocopy hello data.</span></span>

    ![Uruchamianie instalacji ekspresowej](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="bca00-165">Witaj następnym krokiem jest toochoose hello tabele, z których dane hello toocopy.</span><span class="sxs-lookup"><span data-stu-id="bca00-165">hello next step is toochoose hello tables from which toocopy hello data.</span></span> <span data-ttu-id="bca00-166">Tabele hello można filtrować przy użyciu słów kluczowych.</span><span class="sxs-lookup"><span data-stu-id="bca00-166">You can filter hello tables by using keywords.</span></span> <span data-ttu-id="bca00-167">I można wyświetlić podgląd danych i tabeli schematu hello w hello dolny panel.</span><span class="sxs-lookup"><span data-stu-id="bca00-167">And you can preview hello data and table schema in hello bottom panel.</span></span> <span data-ttu-id="bca00-168">Po zakończeniu wybór, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="bca00-168">After you finish your selection, click **Next**.</span></span>

    ![Wybór tabel](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a><span data-ttu-id="bca00-170">Skonfigurowane miejsce docelowe hello, Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="bca00-170">Configure hello destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="bca00-171">Teraz nakaż fabryki danych o hello informacji o lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="bca00-171">Now you tell Data Factory about hello destination information.</span></span>

1. <span data-ttu-id="bca00-172">Informacje o połączeniu magazyn danych SQL jest wypełniane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="bca00-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="bca00-173">Wprowadź hasło hello hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bca00-173">Enter hello password for hello user name.</span></span> <span data-ttu-id="bca00-174">i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="bca00-174">and click **Next**.</span></span>

    ![Skonfigurowane miejsce docelowe](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="bca00-176">Mapowania tabeli inteligentnego wyświetlany jest mapowany na podstawie tabeli nazw tabel toodestination źródeł.</span><span class="sxs-lookup"><span data-stu-id="bca00-176">An intelligent table mapping appears that maps source toodestination tables based on table names.</span></span> <span data-ttu-id="bca00-177">Jeśli hello tabela nie istnieje w docelowym hello, domyślnie ADF utworzy po jednym z hello samej nazwie (dotyczy to tooSQL serwera lub bazy danych SQL Azure jako źródła).</span><span class="sxs-lookup"><span data-stu-id="bca00-177">If hello table does not exist in hello destination, by default ADF will create one with hello same name (this applies tooSQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="bca00-178">Możesz również toomap tooan istniejącej tabeli.</span><span class="sxs-lookup"><span data-stu-id="bca00-178">You can also choose toomap tooan existing table.</span></span> <span data-ttu-id="bca00-179">Przejrzyj i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="bca00-179">Review and click **Next**.</span></span>

    ![Mapowanie tabel](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="bca00-181">Przejrzyj hello mapowanie schematu i odszukaj ostrzeżeń i komunikatów o błędach.</span><span class="sxs-lookup"><span data-stu-id="bca00-181">Review hello schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="bca00-182">Mapowanie inteligentnego jest oparta na nazwę kolumny.</span><span class="sxs-lookup"><span data-stu-id="bca00-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="bca00-183">W przypadku konwersji typu nieobsługiwanych danych między kolumną hello źródłowym i docelowym, zostanie wyświetlony komunikat o błędzie obok odpowiedniej tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="bca00-183">If there is an unsupported data type conversion between hello source and destination column, you see an error message alongside hello corresponding table.</span></span> <span data-ttu-id="bca00-184">Jeśli wybierzesz toolet fabryka danych automatycznie Tworzenie tabel hello, konwersja typu danych właściwe może się tak zdarzyć w razie potrzeby toofix hello niezgodności między magazynami źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="bca00-184">If you choose toolet Data Factory auto create hello tables, proper data type conversion may happen if needed toofix hello incompatibility between source and destination stores.</span></span>

    ![Mapowanie schematu](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="bca00-186">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="bca00-186">Click **Next**.</span></span>

## <a name="configure-hello-performance-settings"></a><span data-ttu-id="bca00-187">Skonfigurowanie ustawień wydajności hello</span><span class="sxs-lookup"><span data-stu-id="bca00-187">Configure hello performance settings</span></span>
<span data-ttu-id="bca00-188">W konfiguracji wydajności hello, skonfiguruj konta magazynu platformy Azure używana do przemieszczania danych hello przed załadowaniem do usługi SQL Data Warehouse performantly przy użyciu [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="bca00-188">In hello Performance configurations, you configure an Azure storage account used for staging hello data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="bca00-189">Po wykonaniu czynności kopiowania hello hello tymczasowe dane w magazynie zostaną wyczyszczone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="bca00-189">After hello copy is done, hello interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="bca00-190">Wybierz istniejące konto magazynu Azure, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="bca00-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Skonfiguruj tymczasowych obiektów blob](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a><span data-ttu-id="bca00-192">Przejrzyj podsumowanie i wdrażanie hello potoku</span><span class="sxs-lookup"><span data-stu-id="bca00-192">Review summary information and deploy hello pipeline</span></span>

<span data-ttu-id="bca00-193">Należy przejrzeć konfigurację hello i kliknij przycisk **Zakończ** przycisk toodeploy hello potoku.</span><span class="sxs-lookup"><span data-stu-id="bca00-193">Review hello configuration and click **Finish** button toodeploy hello pipeline.</span></span>

![Wdrażanie usługi fabryka danych](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="bca00-195">Trwa ładowanie danych monitora</span><span class="sxs-lookup"><span data-stu-id="bca00-195">Monitor data loading progress</span></span>

<span data-ttu-id="bca00-196">Można wyświetlić postęp wdrażania hello i powoduje hello **wdrożenia** strony.</span><span class="sxs-lookup"><span data-stu-id="bca00-196">You can see hello deployment progress and results in hello **Deployment** page.</span></span>

1. <span data-ttu-id="bca00-197">Po ukończeniu wdrażania hello, kliknij łącze hello **kliknij tutaj potoku kopiowania toomonitor** danych toomonitor postępu ładowania.</span><span class="sxs-lookup"><span data-stu-id="bca00-197">Once hello deployment is done, click hello link that says **Click here toomonitor copy pipeline** toomonitor data loading progress.</span></span>

    ![Monitorowanie potoku](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="bca00-199">nowo utworzona Hello **DWLoadData fromSQLServer** potoku podczas ładowania danych zostanie automatycznie wybrany z lewym hello **Eksploratora zasobów**.</span><span class="sxs-lookup"><span data-stu-id="bca00-199">hello newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from hello left-hand **Resource Explorer**.</span></span>

    ![Widok procesu](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="bca00-201">Kliknij przycisk potokiem hello w środku hello hello toosee panelu szczegółowy stan dla każdej tabeli, która mapuje tooan działania.</span><span class="sxs-lookup"><span data-stu-id="bca00-201">Click into hello pipeline in hello middle panel toosee hello detailed status for each table that maps tooan Activity.</span></span>

    ![Widok tabeli działania](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="bca00-203">Kliknij dalej do działania i zostaną wyświetlone dane hello ładowania szczegółów prawym panelu hello, takich jak rozmiar danych, wiersze, przepływności, itp.</span><span class="sxs-lookup"><span data-stu-id="bca00-203">Further click into an activity and you see hello data loading details in hello right panel including data size, rows, throughput, etc.</span></span>

    ![Wyświetl szczegóły działania tabeli](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="bca00-205">toolaunch tego monitorowania widoku nowsze, przejdź do pozycji tooyour magazyn danych SQL, kliknij przycisk **danych obciążenia > fabryki danych Azure**, wybierz fabryką i wybierz **monitorowanie istniejących podczas ładowania zadania**.</span><span class="sxs-lookup"><span data-stu-id="bca00-205">toolaunch this monitoring view later, go tooyour SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bca00-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bca00-206">Next steps</span></span>

<span data-ttu-id="bca00-207">toomigrate Twojego tooSQL bazy danych magazynu danych, zobacz [Omówienie migracji](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="bca00-207">toomigrate your database tooSQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="bca00-208">toolearn więcej informacji na temat fabryki danych Azure i jego możliwości przepływu danych, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="bca00-208">toolearn more about Azure Data Factory and its data movement capabilities, see hello following articles:</span></span>

- [<span data-ttu-id="bca00-209">Wprowadzenie tooAzure fabryki danych</span><span class="sxs-lookup"><span data-stu-id="bca00-209">Introduction tooAzure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="bca00-210">Przenoszenie danych za pomocą działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="bca00-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="bca00-211">Przenieś tooand danych z magazynu danych SQL Azure przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="bca00-211">Move data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="bca00-212">tooexplore danych w usłudze SQL Data Warehouse, zobacz hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="bca00-212">tooexplore your data in SQL Data Warehouse, see hello following articles:</span></span>

- [<span data-ttu-id="bca00-213">Połączenie tooSQL magazynu danych z programu Visual Studio i narzędzi SSDT</span><span class="sxs-lookup"><span data-stu-id="bca00-213">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="bca00-214">[Visual danych za pomocą usługi Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="bca00-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[portalu Azure]: https://portal.azure.com
