---
title: 'Witryna Azure Portal: tworzenie bazy danych SQL | Microsoft Docs'
description: "Dowiedz się, jak toocreate serwera logicznego SQL Database, regułę zapory poziomu serwera i bazy danych w hello portalu Azure. Dowiesz się też tooquery bazy danych Azure SQL przy użyciu hello portalu Azure."
keywords: "samouczek usługi sql database, tworzenie bazy danych sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: d30352d834f2007e0b6b3eabfc3c108c61479b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-database-in-hello-azure-portal"></a><span data-ttu-id="3f51b-105">Tworzenie bazy danych Azure SQL w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="3f51b-105">Create an Azure SQL database in hello Azure portal</span></span>

<span data-ttu-id="3f51b-106">Ten samouczek szybki start przedstawiono sposób toocreate SQL bazy danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3f51b-106">This quick start tutorial walks through how toocreate a SQL database in Azure.</span></span> <span data-ttu-id="3f51b-107">Bazy danych SQL Azure jest "bazy danych jako — usługa" oferty, które umożliwia toorun i skali wysokiej dostępności bazy danych SQL Server w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="3f51b-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you toorun and scale highly available SQL Server databases in hello cloud.</span></span> <span data-ttu-id="3f51b-108">To szybki start przedstawia sposób uruchamiania tooget przez utworzenie bazy danych SQL przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3f51b-108">This quick start shows you how tooget started by creating a SQL database using hello Azure portal.</span></span>

<span data-ttu-id="3f51b-109">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.</span><span class="sxs-lookup"><span data-stu-id="3f51b-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="3f51b-110">Zaloguj się za toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3f51b-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="3f51b-111">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3f51b-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="3f51b-112">Tworzenie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="3f51b-112">Create a SQL database</span></span>

<span data-ttu-id="3f51b-113">Baza danych Azure SQL jest tworzona ze zdefiniowanym zestawem [zasobów obliczeniowych i przechowywania](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="3f51b-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="3f51b-114">Witaj baza danych została utworzona w ramach [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) i [serwera logicznego bazy danych SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="3f51b-114">hello database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="3f51b-115">Wykonaj te kroki toocreate zawierający hello Adventure Works LT przykładowych danych bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="3f51b-115">Follow these steps toocreate a SQL database containing hello Adventure Works LT sample data.</span></span> 

1. <span data-ttu-id="3f51b-116">Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3f51b-116">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="3f51b-117">Wybierz **baz danych** z hello **nowy** i wybrać opcję **bazy danych SQL** z hello **baz danych** strony.</span><span class="sxs-lookup"><span data-stu-id="3f51b-117">Select **Databases** from hello **New** page, and select **SQL Database** from hello **Databases** page.</span></span>

   ![tworzenie bazy danych 1](./media/sql-database-get-started-portal/create-database-1.png)

3. <span data-ttu-id="3f51b-119">Wypełnianie hello bazy danych SQL formularza z hello następujących informacji, jak pokazano na powitania poprzedzających obrazu:</span><span class="sxs-lookup"><span data-stu-id="3f51b-119">Fill out hello SQL Database form with hello following information, as shown on hello preceding image:</span></span>   

   | <span data-ttu-id="3f51b-120">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="3f51b-120">Setting</span></span>       | <span data-ttu-id="3f51b-121">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="3f51b-121">Suggested value</span></span> | <span data-ttu-id="3f51b-122">Opis</span><span class="sxs-lookup"><span data-stu-id="3f51b-122">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="3f51b-123">**Nazwa bazy danych**</span><span class="sxs-lookup"><span data-stu-id="3f51b-123">**Database name**</span></span> | <span data-ttu-id="3f51b-124">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="3f51b-124">mySampleDatabase</span></span> | <span data-ttu-id="3f51b-125">Prawidłowe nazwy baz danych opisano w artykule [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identyfikatory baz danych).</span><span class="sxs-lookup"><span data-stu-id="3f51b-125">For valid database names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="3f51b-126">**Subskrypcja**</span><span class="sxs-lookup"><span data-stu-id="3f51b-126">**Subscription**</span></span> | <span data-ttu-id="3f51b-127">Twoja subskrypcja</span><span class="sxs-lookup"><span data-stu-id="3f51b-127">Your subscription</span></span>  | <span data-ttu-id="3f51b-128">Aby uzyskać szczegółowe informacje o subskrypcjach, zobacz [Subskrypcje](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="3f51b-128">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="3f51b-129">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="3f51b-129">**Resource group**</span></span>  | <span data-ttu-id="3f51b-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3f51b-130">myResourceGroup</span></span> | <span data-ttu-id="3f51b-131">Prawidłowe nazwy grup zasobów opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa).</span><span class="sxs-lookup"><span data-stu-id="3f51b-131">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="3f51b-132">**Źródło źródła**</span><span class="sxs-lookup"><span data-stu-id="3f51b-132">**Source source**</span></span> | <span data-ttu-id="3f51b-133">Próbka (AdventureWorksLT)</span><span class="sxs-lookup"><span data-stu-id="3f51b-133">Sample (AdventureWorksLT)</span></span> | <span data-ttu-id="3f51b-134">Ładuje hello AdventureWorksLT schemat i dane do nowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="3f51b-134">Loads hello AdventureWorksLT schema and data into your new database</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="3f51b-135">Musisz wybrać hello przykładowej bazy danych w tym formularzu, ponieważ jest on używany w hello pozostałą część tej szybki start.</span><span class="sxs-lookup"><span data-stu-id="3f51b-135">You must select hello sample database on this form because it is used in hello remainder of this quick start.</span></span>
   > 

4. <span data-ttu-id="3f51b-136">W obszarze **serwera**, kliknij przycisk **Skonfiguruj wymagane ustawienia** i wypełnij hello programu SQL server (serwer logiczny) formularza z hello następujących informacji, jak pokazano na powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="3f51b-136">Under **Server**, click **Configure required settings** and fill out hello SQL server (logical server) form with hello following information, as shown on hello following image:</span></span>   

   | <span data-ttu-id="3f51b-137">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="3f51b-137">Setting</span></span>       | <span data-ttu-id="3f51b-138">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="3f51b-138">Suggested value</span></span> | <span data-ttu-id="3f51b-139">Opis</span><span class="sxs-lookup"><span data-stu-id="3f51b-139">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="3f51b-140">**Nazwa serwera**</span><span class="sxs-lookup"><span data-stu-id="3f51b-140">**Server name**</span></span> | <span data-ttu-id="3f51b-141">Dowolna nazwa unikatowa w skali globalnej</span><span class="sxs-lookup"><span data-stu-id="3f51b-141">Any globally unique name</span></span> | <span data-ttu-id="3f51b-142">Prawidłowe nazwy serwera opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa).</span><span class="sxs-lookup"><span data-stu-id="3f51b-142">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="3f51b-143">**Identyfikator logowania administratora serwera**</span><span class="sxs-lookup"><span data-stu-id="3f51b-143">**Server admin login**</span></span> | <span data-ttu-id="3f51b-144">Dowolna prawidłowa nazwa</span><span class="sxs-lookup"><span data-stu-id="3f51b-144">Any valid name</span></span> | <span data-ttu-id="3f51b-145">Prawidłowe nazwy identyfikatorów logowania opisano w artykule [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identyfikatory baz danych).</span><span class="sxs-lookup"><span data-stu-id="3f51b-145">For valid login names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="3f51b-146">**Hasło**</span><span class="sxs-lookup"><span data-stu-id="3f51b-146">**Password**</span></span> | <span data-ttu-id="3f51b-147">Dowolne prawidłowe hasło</span><span class="sxs-lookup"><span data-stu-id="3f51b-147">Any valid password</span></span> | <span data-ttu-id="3f51b-148">Hasło musi mieć co najmniej 8 znaków i musi zawierać znaki z trzech z następujących kategorii hello: wielkich liter, małych liter, cyfr i i znaki inne niż alfanumeryczne.</span><span class="sxs-lookup"><span data-stu-id="3f51b-148">Your password must have at least 8 characters and must contain characters from three of hello following categories: upper case characters, lower case characters, numbers, and and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="3f51b-149">**Subskrypcja**</span><span class="sxs-lookup"><span data-stu-id="3f51b-149">**Subscription**</span></span> | <span data-ttu-id="3f51b-150">Twoja subskrypcja</span><span class="sxs-lookup"><span data-stu-id="3f51b-150">Your subscription</span></span> | <span data-ttu-id="3f51b-151">Aby uzyskać szczegółowe informacje o subskrypcjach, zobacz [Subskrypcje](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="3f51b-151">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="3f51b-152">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="3f51b-152">**Resource group**</span></span> | <span data-ttu-id="3f51b-153">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3f51b-153">myResourceGroup</span></span> | <span data-ttu-id="3f51b-154">Prawidłowe nazwy grup zasobów opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa).</span><span class="sxs-lookup"><span data-stu-id="3f51b-154">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="3f51b-155">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="3f51b-155">**Location**</span></span> | <span data-ttu-id="3f51b-156">Dowolna prawidłowa lokalizacja</span><span class="sxs-lookup"><span data-stu-id="3f51b-156">Any valid location</span></span> | <span data-ttu-id="3f51b-157">Aby uzyskać informacje na temat regionów, zobacz temat [Regiony systemu Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="3f51b-157">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="3f51b-158">Hello identyfikator logowania administratora serwera i hasło, które są określone w tym miejscu są wymagane toolog Server toohello i jej baz danych w dalszej części tego szybki start.</span><span class="sxs-lookup"><span data-stu-id="3f51b-158">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="3f51b-159">Zapamiętaj lub zapisz te informacje do wykorzystania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="3f51b-159">Remember or record this information for later use.</span></span> 
   >  

   ![tworzenie serwera bazy danych](./media/sql-database-get-started-portal/create-database-server.png)

5. <span data-ttu-id="3f51b-161">Po wypełnieniu formularza powitania kliknij **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="3f51b-161">When you have completed hello form, click **Select**.</span></span>

6. <span data-ttu-id="3f51b-162">Kliknij przycisk **warstwa cenowa** toospecify hello warstwę i poziom wydajności usługi dla nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3f51b-162">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="3f51b-163">Użyj hello suwaka tooselect **20 jednostek Dtu** i **250** GB miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="3f51b-163">Use hello slider tooselect **20 DTUs** and **250** GB of storage.</span></span> <span data-ttu-id="3f51b-164">Aby uzyskać więcej informacji o jednostkach DTU, zobacz [Co to jest jednostka DTU?](sql-database-what-is-a-dtu.md).</span><span class="sxs-lookup"><span data-stu-id="3f51b-164">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span></span>

   ![tworzenie bazy danych s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. <span data-ttu-id="3f51b-166">Po hello wybranych jednostek Dtu, kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="3f51b-166">After selected hello amount of DTUs, click **Apply**.</span></span>  

8. <span data-ttu-id="3f51b-167">Teraz, zostały ukończone hello formularz bazy danych SQL, kliknij przycisk **Utwórz** tooprovision hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="3f51b-167">Now that you have completed hello SQL Database form, click **Create** tooprovision hello database.</span></span> <span data-ttu-id="3f51b-168">Aprowizacja zajmuje kilka minut.</span><span class="sxs-lookup"><span data-stu-id="3f51b-168">Provisioning takes a few minutes.</span></span> 

9. <span data-ttu-id="3f51b-169">Na pasku narzędzi hello, kliknij przycisk **powiadomienia** procesu wdrażania hello toomonitor.</span><span class="sxs-lookup"><span data-stu-id="3f51b-169">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>

   ![powiadomienie](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="3f51b-171">Tworzenie reguły zapory na poziomie serwera</span><span class="sxs-lookup"><span data-stu-id="3f51b-171">Create a server-level firewall rule</span></span>

<span data-ttu-id="3f51b-172">Hello usługi baza danych SQL tworzy zapory na poziomie hello server — które uniemożliwiają połączenie serwera toohello lub żadnych baz danych na serwerze hello, chyba że tooopen hello zapory dla określonych adresów IP jest tworzona reguła zapory aplikacji zewnętrznych i narzędzia.</span><span class="sxs-lookup"><span data-stu-id="3f51b-172">hello SQL Database service creates a firewall at hello server-level that prevents external applications and tools from connecting toohello server or any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> <span data-ttu-id="3f51b-173">Wykonaj te kroki toocreate [regułę zapory poziomu serwera bazy danych SQL](sql-database-firewall-configure.md) dla adresów IP klienta i włączyć łączność zewnętrzną przez zaporę bazy danych SQL hello tylko adresu IP.</span><span class="sxs-lookup"><span data-stu-id="3f51b-173">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through hello SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="3f51b-174">Usługa SQL Database nawiązuje komunikację na porcie 1433.</span><span class="sxs-lookup"><span data-stu-id="3f51b-174">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="3f51b-175">Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 1433 może nie być dozwolone przez zaporę w sieci.</span><span class="sxs-lookup"><span data-stu-id="3f51b-175">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="3f51b-176">Jeśli tak, nie można połączyć tooyour serwera bazy danych SQL Azure, chyba że dział IT otwiera port 1433.</span><span class="sxs-lookup"><span data-stu-id="3f51b-176">If so, you cannot connect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="3f51b-177">Po zakończeniu wdrażania hello, kliknij przycisk **baz danych SQL** z menu po lewej stronie powitania, a następnie kliknij przycisk **mySampleDatabase** na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="3f51b-177">After hello deployment completes, click **SQL databases** from hello left-hand menu and then click **mySampleDatabase** on hello **SQL databases** page.</span></span> <span data-ttu-id="3f51b-178">Witaj strona przeglądu otwartym bazy danych przedstawiający hello w pełni kwalifikowana nazwa serwera (takich jak **mynewserver20170313.database.windows.net**) i udostępnia opcje dla dalszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3f51b-178">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="3f51b-179">Skopiuj tę w pełni kwalifikowaną nazwę serwera do użycia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="3f51b-179">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3f51b-180">Należy to pełna nazwa tooconnect tooyour serwera i jego baz danych w kolejnych Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="3f51b-180">You need this fully qualified server name tooconnect tooyour server and its databases in subsequent quick starts.</span></span>
   > 

   ![nazwa serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="3f51b-182">Kliknij przycisk **ustawić Zapora serwera** na powitania narzędzi, jak pokazano na poprzedniej ilustracji hello.</span><span class="sxs-lookup"><span data-stu-id="3f51b-182">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="3f51b-183">Witaj **ustawienia zapory** zostanie otwarta strona hello bazy danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3f51b-183">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

   ![reguła zapory serwera](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. <span data-ttu-id="3f51b-185">Kliknij przycisk **Dodaj adres IP klienta** na powitania narzędzi tooadd IP bieżący adres tooa nowej reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="3f51b-185">Click **Add client IP** on hello toolbar tooadd your current IP address tooa new firewall rule.</span></span> <span data-ttu-id="3f51b-186">Reguła zapory może otworzyć port 1433 dla pojedynczego adresu IP lub zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="3f51b-186">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="3f51b-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="3f51b-187">Click **Save**.</span></span> <span data-ttu-id="3f51b-188">Dla bieżącego adresu IP otwierania portu 1433 na serwerze logicznym hello tworzona jest reguła zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="3f51b-188">A server-level firewall rule is created for your current IP address opening port 1433 on hello logical server.</span></span>

   ![ustawianie reguły zapory serwera](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="3f51b-190">Kliknij przycisk **OK** , a następnie zamknij hello **ustawienia zapory** strony.</span><span class="sxs-lookup"><span data-stu-id="3f51b-190">Click **OK** and then close hello **Firewall settings** page.</span></span>

<span data-ttu-id="3f51b-191">Teraz można podłączyć toohello bazy danych programu SQL server i bazy danych przy użyciu programu SQL Server Management Studio lub inne narzędzie do dowolnego z tego adresu IP przy użyciu konta administratora serwera hello utworzone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="3f51b-191">You can now connect toohello SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using hello server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f51b-192">Domyślnie dostęp za pośrednictwem zapory bazy danych SQL hello jest włączona dla wszystkich usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3f51b-192">By default, access through hello SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="3f51b-193">Kliknij przycisk **OFF** na toodisable tej strony dla wszystkich usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3f51b-193">Click **OFF** on this page toodisable for all Azure services.</span></span>
>

## <a name="query-hello-sql-database"></a><span data-ttu-id="3f51b-194">Baza danych SQL hello zapytania</span><span class="sxs-lookup"><span data-stu-id="3f51b-194">Query hello SQL database</span></span>

<span data-ttu-id="3f51b-195">Teraz, po utworzeniu przykładowej bazy danych na platformie Azure, umożliwia narzędzie hello wbudowaną kwerendę w hello Azure tooconfirm portalu, że możesz połączyć dane hello toohello bazy danych i zapytania.</span><span class="sxs-lookup"><span data-stu-id="3f51b-195">Now that you have created a sample database in Azure, let’s use hello built-in query tool within hello Azure portal tooconfirm that you can connect toohello database and query hello data.</span></span> 

1. <span data-ttu-id="3f51b-196">Na stronie Baza danych SQL hello bazy danych, kliknij przycisk **narzędzia** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="3f51b-196">On hello SQL Database page for your database, click **Tools** on hello toolbar.</span></span> <span data-ttu-id="3f51b-197">Witaj **narzędzia** zostanie otwarta strona.</span><span class="sxs-lookup"><span data-stu-id="3f51b-197">hello **Tools** page opens.</span></span>

   ![menu narzędzi](./media/sql-database-get-started-portal/tools-menu.png) 

2. <span data-ttu-id="3f51b-199">Kliknij przycisk **edytora zapytań (wersja zapoznawcza)**, kliknij hello **Podgląd warunki** pole wyboru, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f51b-199">Click **Query editor (preview)**, click hello **Preview terms** checkbox, and then click **OK**.</span></span> <span data-ttu-id="3f51b-200">zostanie otwarta strona Edytor zapytań Hello.</span><span class="sxs-lookup"><span data-stu-id="3f51b-200">hello Query editor page opens.</span></span>

3. <span data-ttu-id="3f51b-201">Kliknij przycisk **logowania** , a następnie po wyświetleniu monitu wybierz **uwierzytelniania programu SQL server** , a następnie podaj identyfikator logowania administratora serwera hello i hasła, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="3f51b-201">Click **Login** and then, when prompted, select **SQL server authentication** and then provide hello server admin login and password that you created earlier.</span></span>

   ![logowanie](./media/sql-database-get-started-portal/login.png) 

4. <span data-ttu-id="3f51b-203">Kliknij przycisk **OK** toolog w.</span><span class="sxs-lookup"><span data-stu-id="3f51b-203">Click **OK** toolog in.</span></span>

5. <span data-ttu-id="3f51b-204">Po uwierzytelnieniu użytkownik typu hello następujące zapytanie w okienku edytora zapytań hello.</span><span class="sxs-lookup"><span data-stu-id="3f51b-204">After you are authenticated, type hello following query in hello query editor pane.</span></span>

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. <span data-ttu-id="3f51b-205">Kliknij przycisk **Uruchom** , a następnie przejrzyj wyniki zapytania hello w hello **wyniki** okienka.</span><span class="sxs-lookup"><span data-stu-id="3f51b-205">Click **Run** and then review hello query results in hello **Results** pane.</span></span>

   ![wyniki edytora zapytań](./media/sql-database-get-started-portal/query-editor-results.png)

7. <span data-ttu-id="3f51b-207">Zamknij hello **edytora zapytań** strony i hello **narzędzia** strony.</span><span class="sxs-lookup"><span data-stu-id="3f51b-207">Close hello **Query editor** page and hello **Tools** page.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="3f51b-208">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="3f51b-208">Clean up resources</span></span>

<span data-ttu-id="3f51b-209">Jeśli nie potrzebujesz tych zasobów innym Szybki Start/samouczek (zobacz [następne kroki](#next-steps)), można je usunąć, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="3f51b-209">If you don't need these resources for another quickstart/tutorial (see [Next steps](#next-steps)), you can delete them by doing hello following:</span></span>


1. <span data-ttu-id="3f51b-210">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** , a następnie kliknij przycisk **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="3f51b-210">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span> 
2. <span data-ttu-id="3f51b-211">Na stronie grupy zasobów, kliknij przycisk **usunąć**, typ **myResourceGroup** w hello pola tekstowego, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="3f51b-211">On your resource group page, click **Delete**, type **myResourceGroup** in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f51b-212">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f51b-212">Next steps</span></span>

<span data-ttu-id="3f51b-213">Teraz, gdy już masz bazę danych, możesz nawiązać z nią połączenie i uruchamiać zapytania za pomocą ulubionych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="3f51b-213">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="3f51b-214">Dowiedz się więcej, wybierając narzędzie poniżej:</span><span class="sxs-lookup"><span data-stu-id="3f51b-214">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="3f51b-215">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="3f51b-215">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="3f51b-216">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3f51b-216">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="3f51b-217">.NET</span><span class="sxs-lookup"><span data-stu-id="3f51b-217">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="3f51b-218">PHP</span><span class="sxs-lookup"><span data-stu-id="3f51b-218">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="3f51b-219">Node.js</span><span class="sxs-lookup"><span data-stu-id="3f51b-219">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="3f51b-220">Java</span><span class="sxs-lookup"><span data-stu-id="3f51b-220">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="3f51b-221">Python</span><span class="sxs-lookup"><span data-stu-id="3f51b-221">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="3f51b-222">Ruby</span><span class="sxs-lookup"><span data-stu-id="3f51b-222">Ruby</span></span>](sql-database-connect-query-ruby.md)
