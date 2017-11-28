---
title: "aaaDesign pierwszą bazę danych Azure SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się toodesign pierwszą bazę danych Azure SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 65f0a1594cbdda7480abf32a847266a073e7560d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-sql-database"></a><span data-ttu-id="ebde0-103">Projektowanie pierwszą bazę danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="ebde0-103">Design your first Azure SQL database</span></span>

<span data-ttu-id="ebde0-104">Baza danych SQL Azure to relacyjnej bazy danych — jako a usługa (DBaaS) w hello Microsoft Cloud ("Azure").</span><span class="sxs-lookup"><span data-stu-id="ebde0-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="ebde0-105">Z tego samouczka, dowiesz się, jak toouse hello portalu Azure i [programu SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) do:</span><span class="sxs-lookup"><span data-stu-id="ebde0-105">In this tutorial, you learn how toouse hello Azure portal and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ebde0-106">Utwórz bazę danych w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ebde0-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="ebde0-107">Skonfiguruj regułę zapory poziomu serwera w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ebde0-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="ebde0-108">Połączenie bazy danych toohello z SSMS</span><span class="sxs-lookup"><span data-stu-id="ebde0-108">Connect toohello database with SSMS</span></span>
> * <span data-ttu-id="ebde0-109">Tworzenie tabel z SSMS</span><span class="sxs-lookup"><span data-stu-id="ebde0-109">Create tables with SSMS</span></span>
> * <span data-ttu-id="ebde0-110">Danych ładowania zbiorczego, za pomocą narzędzia BCP</span><span class="sxs-lookup"><span data-stu-id="ebde0-110">Bulk load data with BCP</span></span>
> * <span data-ttu-id="ebde0-111">Zapytanie danych z narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="ebde0-111">Query that data with SSMS</span></span>
> * <span data-ttu-id="ebde0-112">Przywróć poprzednie tooa bazy danych hello [punktu w czasie przywracania](sql-database-recovery-using-backups.md#point-in-time-restore) w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ebde0-112">Restore hello database tooa previous [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) in hello Azure portal</span></span>

<span data-ttu-id="ebde0-113">Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="ebde0-113">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebde0-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ebde0-114">Prerequisites</span></span>

<span data-ttu-id="ebde0-115">toocomplete tego samouczka, upewnij się, że została zainstalowana:</span><span class="sxs-lookup"><span data-stu-id="ebde0-115">toocomplete this tutorial, make sure you have installed:</span></span>
- <span data-ttu-id="ebde0-116">Witaj najnowsza wersja [programu SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="ebde0-116">hello newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span></span>
- <span data-ttu-id="ebde0-117">Witaj najnowsza wersja [BCP i SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span><span class="sxs-lookup"><span data-stu-id="ebde0-117">hello newest version of [BCP and SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="ebde0-118">Zaloguj się za toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ebde0-118">Log in toohello Azure portal</span></span>

<span data-ttu-id="ebde0-119">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ebde0-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="ebde0-120">Utwórz pustą bazę danych SQL</span><span class="sxs-lookup"><span data-stu-id="ebde0-120">Create a blank SQL database</span></span>

<span data-ttu-id="ebde0-121">Baza danych Azure SQL jest tworzona ze zdefiniowanym zestawem [zasobów obliczeniowych i przechowywania](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="ebde0-121">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="ebde0-122">Witaj baza danych została utworzona w ramach [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) i [serwera logicznego bazy danych SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="ebde0-122">hello database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="ebde0-123">Wykonaj te kroki toocreate pustej bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="ebde0-123">Follow these steps toocreate a blank SQL database.</span></span> 

1. <span data-ttu-id="ebde0-124">Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ebde0-124">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="ebde0-125">Wybierz **baz danych** z hello **nowy** i wybrać opcję **bazy danych SQL** z hello **baz danych** strony.</span><span class="sxs-lookup"><span data-stu-id="ebde0-125">Select **Databases** from hello **New** page, and select **SQL Database** from hello **Databases** page.</span></span> 

   ![Tworzenie bazy danych puste](./media/sql-database-design-first-database/create-empty-database.png)

3. <span data-ttu-id="ebde0-127">Wypełnianie hello bazy danych SQL formularza z hello następujących informacji, jak pokazano na powitania poprzedzających obrazu:</span><span class="sxs-lookup"><span data-stu-id="ebde0-127">Fill out hello SQL Database form with hello following information, as shown on hello preceding image:</span></span>   

   | <span data-ttu-id="ebde0-128">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="ebde0-128">Setting</span></span>       | <span data-ttu-id="ebde0-129">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="ebde0-129">Suggested value</span></span> | <span data-ttu-id="ebde0-130">Opis</span><span class="sxs-lookup"><span data-stu-id="ebde0-130">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="ebde0-131">**Nazwa bazy danych**</span><span class="sxs-lookup"><span data-stu-id="ebde0-131">**Database name**</span></span> | <span data-ttu-id="ebde0-132">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="ebde0-132">mySampleDatabase</span></span> | <span data-ttu-id="ebde0-133">Prawidłowe nazwy baz danych opisano w artykule [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identyfikatory baz danych).</span><span class="sxs-lookup"><span data-stu-id="ebde0-133">For valid database names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="ebde0-134">**Subskrypcja**</span><span class="sxs-lookup"><span data-stu-id="ebde0-134">**Subscription**</span></span> | <span data-ttu-id="ebde0-135">Twoja subskrypcja</span><span class="sxs-lookup"><span data-stu-id="ebde0-135">Your subscription</span></span>  | <span data-ttu-id="ebde0-136">Aby uzyskać szczegółowe informacje o subskrypcjach, zobacz [Subskrypcje](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="ebde0-136">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="ebde0-137">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="ebde0-137">**Resource group**</span></span> | <span data-ttu-id="ebde0-138">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ebde0-138">myResourceGroup</span></span> | <span data-ttu-id="ebde0-139">Prawidłowe nazwy grup zasobów opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa).</span><span class="sxs-lookup"><span data-stu-id="ebde0-139">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="ebde0-140">**Wybierz źródło**</span><span class="sxs-lookup"><span data-stu-id="ebde0-140">**Select source**</span></span> | <span data-ttu-id="ebde0-141">Pusta baza danych</span><span class="sxs-lookup"><span data-stu-id="ebde0-141">Blank database</span></span> | <span data-ttu-id="ebde0-142">Określa, czy można utworzyć pustej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ebde0-142">Specifies that a blank database should be created.</span></span> |

4. <span data-ttu-id="ebde0-143">Kliknij przycisk **serwera** toocreate i skonfiguruj nowy serwer dla nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ebde0-143">Click **Server** toocreate and configure a new server for your new database.</span></span> <span data-ttu-id="ebde0-144">Wypełnianie hello **nowy formularz serwera** z hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ebde0-144">Fill out hello **New server form** with hello following information:</span></span> 

   | <span data-ttu-id="ebde0-145">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="ebde0-145">Setting</span></span>       | <span data-ttu-id="ebde0-146">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="ebde0-146">Suggested value</span></span> | <span data-ttu-id="ebde0-147">Opis</span><span class="sxs-lookup"><span data-stu-id="ebde0-147">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="ebde0-148">**Nazwa serwera**</span><span class="sxs-lookup"><span data-stu-id="ebde0-148">**Server name**</span></span> | <span data-ttu-id="ebde0-149">Dowolna nazwa unikatowa w skali globalnej</span><span class="sxs-lookup"><span data-stu-id="ebde0-149">Any globally unique name</span></span> | <span data-ttu-id="ebde0-150">Prawidłowe nazwy serwera opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa).</span><span class="sxs-lookup"><span data-stu-id="ebde0-150">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="ebde0-151">**Identyfikator logowania administratora serwera**</span><span class="sxs-lookup"><span data-stu-id="ebde0-151">**Server admin login**</span></span> | <span data-ttu-id="ebde0-152">Dowolna prawidłowa nazwa</span><span class="sxs-lookup"><span data-stu-id="ebde0-152">Any valid name</span></span> | <span data-ttu-id="ebde0-153">Prawidłowe nazwy identyfikatorów logowania opisano w artykule [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identyfikatory baz danych).</span><span class="sxs-lookup"><span data-stu-id="ebde0-153">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span>|
   | <span data-ttu-id="ebde0-154">**Hasło**</span><span class="sxs-lookup"><span data-stu-id="ebde0-154">**Password**</span></span> | <span data-ttu-id="ebde0-155">Dowolne prawidłowe hasło</span><span class="sxs-lookup"><span data-stu-id="ebde0-155">Any valid password</span></span> | <span data-ttu-id="ebde0-156">Hasło musi mieć co najmniej 8 znaków i musi zawierać znaki z trzech z następujących kategorii hello: wielkich liter, małych liter, cyfr i znaków innych niż alfanumeryczne.</span><span class="sxs-lookup"><span data-stu-id="ebde0-156">Your password must have at least 8 characters and must contain characters from three of hello following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="ebde0-157">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="ebde0-157">**Location**</span></span> | <span data-ttu-id="ebde0-158">Dowolna prawidłowa lokalizacja</span><span class="sxs-lookup"><span data-stu-id="ebde0-158">Any valid location</span></span> | <span data-ttu-id="ebde0-159">Aby uzyskać informacje na temat regionów, zobacz temat [Regiony systemu Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="ebde0-159">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![tworzenie serwera bazy danych](./media//sql-database-design-first-database/create-database-server.png)

5. <span data-ttu-id="ebde0-161">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="ebde0-161">Click **Select**.</span></span>

6. <span data-ttu-id="ebde0-162">Kliknij przycisk **warstwa cenowa** toospecify hello warstwę i poziom wydajności usługi dla nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ebde0-162">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="ebde0-163">W tym samouczku, wybierz **20 jednostek Dtu** i **250** GB miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="ebde0-163">For this tutorial, select **20 DTUs** and **250** GB of storage.</span></span>

   ![tworzenie bazy danych s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. <span data-ttu-id="ebde0-165">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="ebde0-165">Click **Apply**.</span></span>  

8. <span data-ttu-id="ebde0-166">Wybierz **sortowania** dla hello pustej bazy danych (w tym samouczku, wartość domyślna używana hello).</span><span class="sxs-lookup"><span data-stu-id="ebde0-166">Select a **collation** for hello blank database (for this tutorial, use hello default value).</span></span> <span data-ttu-id="ebde0-167">Aby uzyskać więcej informacji na temat sortowań zobacz [sortowania](https://docs.microsoft.com/sql/t-sql/statements/collations)</span><span class="sxs-lookup"><span data-stu-id="ebde0-167">For more information about collations, see [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations)</span></span>

9. <span data-ttu-id="ebde0-168">Kliknij przycisk **Utwórz** tooprovision hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="ebde0-168">Click **Create** tooprovision hello database.</span></span> <span data-ttu-id="ebde0-169">Inicjowanie obsługi administracyjnej ma o toocomplete minutę i pół.</span><span class="sxs-lookup"><span data-stu-id="ebde0-169">Provisioning takes about a minute and a half toocomplete.</span></span> 

10. <span data-ttu-id="ebde0-170">Na pasku narzędzi hello, kliknij przycisk **powiadomienia** procesu wdrażania hello toomonitor.</span><span class="sxs-lookup"><span data-stu-id="ebde0-170">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>

   ![powiadomienie](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="ebde0-172">Tworzenie reguły zapory na poziomie serwera</span><span class="sxs-lookup"><span data-stu-id="ebde0-172">Create a server-level firewall rule</span></span>

<span data-ttu-id="ebde0-173">Hello usługi baza danych SQL tworzy zapory na poziomie hello server — które uniemożliwiają połączenie serwera toohello lub żadnych baz danych na serwerze hello, chyba że tooopen hello zapory dla określonych adresów IP jest tworzona reguła zapory aplikacji zewnętrznych i narzędzia.</span><span class="sxs-lookup"><span data-stu-id="ebde0-173">hello SQL Database service creates a firewall at hello server-level that prevents external applications and tools from connecting toohello server or any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> <span data-ttu-id="ebde0-174">Wykonaj te kroki toocreate [regułę zapory poziomu serwera bazy danych SQL](sql-database-firewall-configure.md) dla adresów IP klienta i włączyć łączność zewnętrzną przez zaporę bazy danych SQL hello tylko adresu IP.</span><span class="sxs-lookup"><span data-stu-id="ebde0-174">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through hello SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="ebde0-175">Usługa SQL Database nawiązuje komunikację na porcie 1433.</span><span class="sxs-lookup"><span data-stu-id="ebde0-175">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="ebde0-176">Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 1433 może nie być dozwolone przez zaporę w sieci.</span><span class="sxs-lookup"><span data-stu-id="ebde0-176">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="ebde0-177">Jeśli tak, nie można połączyć tooyour serwera bazy danych SQL Azure, chyba że dział IT otwiera port 1433.</span><span class="sxs-lookup"><span data-stu-id="ebde0-177">If so, you cannot connect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="ebde0-178">Po zakończeniu wdrażania hello, kliknij przycisk **baz danych SQL** z menu po lewej stronie powitania, a następnie kliknij przycisk **mySampleDatabase** na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="ebde0-178">After hello deployment completes, click **SQL databases** from hello left-hand menu and then click **mySampleDatabase** on hello **SQL databases** page.</span></span> <span data-ttu-id="ebde0-179">Witaj strona przeglądu otwartym bazy danych przedstawiający hello w pełni kwalifikowana nazwa serwera (takich jak **mynewserver20170313.database.windows.net**) i udostępnia opcje dla dalszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ebde0-179">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="ebde0-180">Skopiuj tę w pełni kwalifikowaną nazwę serwera do użycia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="ebde0-180">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ebde0-181">Należy to pełna nazwa tooconnect tooyour serwera i jego baz danych w kolejnych Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="ebde0-181">You need this fully qualified server name tooconnect tooyour server and its databases in subsequent quick starts.</span></span>
   > 

   ![nazwa serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="ebde0-183">Kliknij przycisk **ustawić Zapora serwera** na powitania narzędzi, jak pokazano na poprzedniej ilustracji hello.</span><span class="sxs-lookup"><span data-stu-id="ebde0-183">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="ebde0-184">Witaj **ustawienia zapory** zostanie otwarta strona hello bazy danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ebde0-184">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

   ![reguła zapory serwera](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. <span data-ttu-id="ebde0-186">Kliknij przycisk **Dodaj adres IP klienta** na powitania narzędzi tooadd IP bieżący adres tooa nowej reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="ebde0-186">Click **Add client IP** on hello toolbar tooadd your current IP address tooa new firewall rule.</span></span> <span data-ttu-id="ebde0-187">Reguła zapory może otworzyć port 1433 dla pojedynczego adresu IP lub zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="ebde0-187">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="ebde0-188">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ebde0-188">Click **Save**.</span></span> <span data-ttu-id="ebde0-189">Dla bieżącego adresu IP otwierania portu 1433 na serwerze logicznym hello tworzona jest reguła zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="ebde0-189">A server-level firewall rule is created for your current IP address opening port 1433 on hello logical server.</span></span>

   ![ustawianie reguły zapory serwera](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="ebde0-191">Kliknij przycisk **OK** , a następnie zamknij hello **ustawienia zapory** strony.</span><span class="sxs-lookup"><span data-stu-id="ebde0-191">Click **OK** and then close hello **Firewall settings** page.</span></span>

<span data-ttu-id="ebde0-192">Teraz można podłączyć toohello bazy danych programu SQL server i bazy danych przy użyciu programu SQL Server Management Studio lub inne narzędzie do dowolnego z tego adresu IP przy użyciu konta administratora serwera hello utworzone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ebde0-192">You can now connect toohello SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using hello server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ebde0-193">Domyślnie dostęp za pośrednictwem zapory bazy danych SQL hello jest włączona dla wszystkich usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ebde0-193">By default, access through hello SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="ebde0-194">Kliknij przycisk **OFF** na toodisable tej strony dla wszystkich usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ebde0-194">Click **OFF** on this page toodisable for all Azure services.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="ebde0-195">Informacje o połączeniu z serwerem SQL</span><span class="sxs-lookup"><span data-stu-id="ebde0-195">SQL server connection information</span></span>

<span data-ttu-id="ebde0-196">Pobierz hello pełni kwalifikowaną nazwę serwera dla serwera bazy danych SQL Azure w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ebde0-196">Get hello fully qualified server name for your Azure SQL Database server in hello Azure portal.</span></span> <span data-ttu-id="ebde0-197">Możesz użyć hello pełną nazwę tooconnect tooyour serwera przy użyciu programu SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="ebde0-197">You use hello fully qualified server name tooconnect tooyour server using SQL Server Management Studio.</span></span>

1. <span data-ttu-id="ebde0-198">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ebde0-198">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ebde0-199">Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="ebde0-199">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="ebde0-200">W hello **Essentials** okienka w hello strony portalu systemu Azure dla bazy danych, Znajdź, a następnie skopiuj hello **nazwy serwera**.</span><span class="sxs-lookup"><span data-stu-id="ebde0-200">In hello **Essentials** pane in hello Azure portal page for your database, locate and then copy hello **Server name**.</span></span>

   ![informacje o połączeniu](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="ebde0-202">Połączenie bazy danych toohello z SSMS</span><span class="sxs-lookup"><span data-stu-id="ebde0-202">Connect toohello database with SSMS</span></span>

<span data-ttu-id="ebde0-203">Użyj [programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish serwer bazy danych SQL Azure tooyour połączenia.</span><span class="sxs-lookup"><span data-stu-id="ebde0-203">Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish a connection tooyour Azure SQL Database server.</span></span>

1. <span data-ttu-id="ebde0-204">Otwórz program SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="ebde0-204">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="ebde0-205">W hello **połączyć tooServer** okna dialogowego wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ebde0-205">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>

   | <span data-ttu-id="ebde0-206">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="ebde0-206">Setting</span></span>       | <span data-ttu-id="ebde0-207">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="ebde0-207">Suggested value</span></span> | <span data-ttu-id="ebde0-208">Opis</span><span class="sxs-lookup"><span data-stu-id="ebde0-208">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="ebde0-209">Typ serwera</span><span class="sxs-lookup"><span data-stu-id="ebde0-209">Server type</span></span> | <span data-ttu-id="ebde0-210">Aparat bazy danych</span><span class="sxs-lookup"><span data-stu-id="ebde0-210">Database engine</span></span> | <span data-ttu-id="ebde0-211">Ta wartość jest wymagana</span><span class="sxs-lookup"><span data-stu-id="ebde0-211">This value is required</span></span> |
   | <span data-ttu-id="ebde0-212">Nazwa serwera</span><span class="sxs-lookup"><span data-stu-id="ebde0-212">Server name</span></span> | <span data-ttu-id="ebde0-213">Nazwa FQDN serwera Hello</span><span class="sxs-lookup"><span data-stu-id="ebde0-213">hello fully qualified server name</span></span> | <span data-ttu-id="ebde0-214">Witaj nazwa powinna być podobny do następującego: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="ebde0-214">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="ebde0-215">Authentication</span><span class="sxs-lookup"><span data-stu-id="ebde0-215">Authentication</span></span> | <span data-ttu-id="ebde0-216">Uwierzytelnianie programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="ebde0-216">SQL Server Authentication</span></span> | <span data-ttu-id="ebde0-217">Uwierzytelnianie programu SQL jest typ uwierzytelniania tylko hello ma został skonfigurowany w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ebde0-217">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="ebde0-218">Login</span><span class="sxs-lookup"><span data-stu-id="ebde0-218">Login</span></span> | <span data-ttu-id="ebde0-219">konto administratora powitania serwera</span><span class="sxs-lookup"><span data-stu-id="ebde0-219">hello server admin account</span></span> | <span data-ttu-id="ebde0-220">To konto hello określone podczas tworzenia powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="ebde0-220">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="ebde0-221">Hasło</span><span class="sxs-lookup"><span data-stu-id="ebde0-221">Password</span></span> | <span data-ttu-id="ebde0-222">Witaj hasło do konta administratora serwera</span><span class="sxs-lookup"><span data-stu-id="ebde0-222">hello password for your server admin account</span></span> | <span data-ttu-id="ebde0-223">Jest to hasło hello określone podczas tworzenia powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="ebde0-223">This is hello password that you specified when you created hello server.</span></span> |

   ![Połącz tooserver](./media/sql-database-connect-query-ssms/connect.png)

3. <span data-ttu-id="ebde0-225">Kliknij przycisk **opcje** w hello **połączyć tooserver** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="ebde0-225">Click **Options** in hello **Connect tooserver** dialog box.</span></span> <span data-ttu-id="ebde0-226">W hello **połączyć toodatabase** wprowadź **mySampleDatabase** tooconnect toothis w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="ebde0-226">In hello **Connect toodatabase** section, enter **mySampleDatabase** tooconnect toothis database.</span></span>

   ![Połącz toodb na serwerze](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="ebde0-228">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="ebde0-228">Click **Connect**.</span></span> <span data-ttu-id="ebde0-229">Okno Eksploratora obiektów Hello zostanie otwarty w programie SSMS.</span><span class="sxs-lookup"><span data-stu-id="ebde0-229">hello Object Explorer window opens in SSMS.</span></span> 

5. <span data-ttu-id="ebde0-230">W Eksploratorze obiektów rozwiń **baz danych** , a następnie rozwiń węzeł **mySampleDatabase** tooview hello obiektów hello przykładowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ebde0-230">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** tooview hello objects in hello sample database.</span></span>

   ![Obiekty bazy danych](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="ebde0-232">Tworzenie tabel w bazie danych hello</span><span class="sxs-lookup"><span data-stu-id="ebde0-232">Create tables in hello database</span></span> 

<span data-ttu-id="ebde0-233">Tworzenie schematu bazy danych z czterech tabel, które system zarządzania uczniów uczelni przy użyciu modelu [języka Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span><span class="sxs-lookup"><span data-stu-id="ebde0-233">Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span></span>

- <span data-ttu-id="ebde0-234">Osoby</span><span class="sxs-lookup"><span data-stu-id="ebde0-234">Person</span></span>
- <span data-ttu-id="ebde0-235">Plan</span><span class="sxs-lookup"><span data-stu-id="ebde0-235">Course</span></span>
- <span data-ttu-id="ebde0-236">Dla użytkowników domowych</span><span class="sxs-lookup"><span data-stu-id="ebde0-236">Student</span></span>
- <span data-ttu-id="ebde0-237">System zarządzania uczniów uczelni modelu karty kredytowej</span><span class="sxs-lookup"><span data-stu-id="ebde0-237">Credit that model a student management system for universities</span></span>

<span data-ttu-id="ebde0-238">Witaj poniższym diagramie przedstawiono sposób następujące tabele są powiązane tooeach innych.</span><span class="sxs-lookup"><span data-stu-id="ebde0-238">hello following diagram shows how these tables are related tooeach other.</span></span> <span data-ttu-id="ebde0-239">Niektóre z tych tabel odwoływać się do kolumn w innych tabelach.</span><span class="sxs-lookup"><span data-stu-id="ebde0-239">Some of these tables reference columns in other tables.</span></span> <span data-ttu-id="ebde0-240">Na przykład hello uczniów tabeli odwołuje hello **PersonId** kolumny hello **osoby** tabeli.</span><span class="sxs-lookup"><span data-stu-id="ebde0-240">For example, hello Student table references hello **PersonId** column of hello **Person** table.</span></span> <span data-ttu-id="ebde0-241">Diagram toounderstand hello badań, jak hello tabele w tym samouczku są powiązane tooone innego.</span><span class="sxs-lookup"><span data-stu-id="ebde0-241">Study hello diagram toounderstand how hello tables in this tutorial are related tooone another.</span></span> <span data-ttu-id="ebde0-242">Dla omówiono sposób toocreate tabele skuteczne bazy danych, zobacz [tworzenia tabel bazy danych skuteczne](https://msdn.microsoft.com/library/cc505842.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebde0-242">For an in-depth look at how toocreate effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx).</span></span> <span data-ttu-id="ebde0-243">Aby uzyskać informacje dotyczące wybierania typów danych, zobacz [typy danych](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="ebde0-243">For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span></span>

> [!NOTE]
> <span data-ttu-id="ebde0-244">Można również użyć hello [projektanta tabel w programie SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate i projektowanie tabelach.</span><span class="sxs-lookup"><span data-stu-id="ebde0-244">You can also use hello [table designer in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate and design your tables.</span></span> 

![Relacje między tabelami](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. <span data-ttu-id="ebde0-246">W Eksploratorze obiektów kliknij prawym przyciskiem myszy pozycję **mySampleDatabase** i kliknij opcję **Nowe zapytanie**.</span><span class="sxs-lookup"><span data-stu-id="ebde0-246">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="ebde0-247">Puste zapytanie zostanie otwarte okno czyli tooyour połączenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ebde0-247">A blank query window opens that is connected tooyour database.</span></span>

2. <span data-ttu-id="ebde0-248">W oknie zapytania hello wykonaj hello następującego zapytania toocreate cztery tabel bazy danych:</span><span class="sxs-lookup"><span data-stu-id="ebde0-248">In hello query window, execute hello following query toocreate four tables in your database:</span></span> 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![Tworzenie tabel](./media/sql-database-design-first-database/create-tables.png)

3. <span data-ttu-id="ebde0-250">Rozwiń węzeł "tabele" hello w hello programu SQL Server Management Studio obiektu explorer toosee hello tabele, które utworzono.</span><span class="sxs-lookup"><span data-stu-id="ebde0-250">Expand hello 'tables' node in hello SQL Server Management Studio Object explorer toosee hello tables you created.</span></span>

   ![tabele utworzone w programie ssms](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="ebde0-252">Ładowanie danych do tabel hello</span><span class="sxs-lookup"><span data-stu-id="ebde0-252">Load data into hello tables</span></span>

1. <span data-ttu-id="ebde0-253">Utwórz folder o nazwie **SampleTableData** pliki do pobrania folderu toostore przykładowych danych bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ebde0-253">Create a folder called **SampleTableData** in your Downloads folder toostore sample data for your database.</span></span> 

2. <span data-ttu-id="ebde0-254">Kliknij prawym przyciskiem myszy hello następujące łącza i zapisać je w hello **SampleTableData** folderu.</span><span class="sxs-lookup"><span data-stu-id="ebde0-254">Right-click hello following links and save them into hello **SampleTableData** folder.</span></span> 

   - [<span data-ttu-id="ebde0-255">SampleCourseData</span><span class="sxs-lookup"><span data-stu-id="ebde0-255">SampleCourseData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [<span data-ttu-id="ebde0-256">SamplePersonData</span><span class="sxs-lookup"><span data-stu-id="ebde0-256">SamplePersonData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [<span data-ttu-id="ebde0-257">SampleStudentData</span><span class="sxs-lookup"><span data-stu-id="ebde0-257">SampleStudentData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [<span data-ttu-id="ebde0-258">SampleCreditData</span><span class="sxs-lookup"><span data-stu-id="ebde0-258">SampleCreditData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. <span data-ttu-id="ebde0-259">Otwórz okno wiersza polecenia i przejdź do folderu SampleTableData toohello.</span><span class="sxs-lookup"><span data-stu-id="ebde0-259">Open a command prompt window and navigate toohello SampleTableData folder.</span></span>

4. <span data-ttu-id="ebde0-260">Wykonaj następujące polecenia tooinsert przykładowych danych do tabel hello, zastępując wartości hello hello **ServerName**, **DatabaseName**, **UserName**i **Hasło** hello wartościami dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="ebde0-260">Execute hello following commands tooinsert sample data into hello tables replacing hello values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with hello values for your environment.</span></span>
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

<span data-ttu-id="ebde0-261">Teraz załadowano przykładowych danych do tabel hello, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ebde0-261">You have now loaded sample data into hello tables you created earlier.</span></span>

## <a name="query-data"></a><span data-ttu-id="ebde0-262">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="ebde0-262">Query data</span></span>

<span data-ttu-id="ebde0-263">Wykonanie poniższych informacji tooretrieve zapytania z tabel bazy danych hello hello.</span><span class="sxs-lookup"><span data-stu-id="ebde0-263">Execute hello following queries tooretrieve information from hello database tables.</span></span> <span data-ttu-id="ebde0-264">Zobacz [Pisanie zapytań SQL](https://technet.microsoft.com/library/bb264565.aspx) toolearn więcej informacji na temat Pisanie zapytań SQL.</span><span class="sxs-lookup"><span data-stu-id="ebde0-264">See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) toolearn more about writing SQL queries.</span></span> <span data-ttu-id="ebde0-265">Pierwsza kwerenda Hello łączy wszystkie cztery tabele toofind przez wszystkich studentów hello nauczanych przez "Dominick Pope" które mają wyższe niż 75% stopnia w swojej klasie.</span><span class="sxs-lookup"><span data-stu-id="ebde0-265">hello first query joins all four tables toofind all hello students taught by 'Dominick Pope' who have a grade higher than 75% in his class.</span></span> <span data-ttu-id="ebde0-266">Witaj drugiego zapytania wszystkie cztery między tabelami i wyszukuje wszystkich kursów, w których kiedykolwiek zarejestrował "Noe Coleman".</span><span class="sxs-lookup"><span data-stu-id="ebde0-266">hello second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.</span></span>

1. <span data-ttu-id="ebde0-267">W oknie zapytania SQL Server Management Studio wykonaj następujące kwerendy hello:</span><span class="sxs-lookup"><span data-stu-id="ebde0-267">In a SQL Server Management Studio query window, execute hello following query:</span></span>

   ```sql 
   -- Find hello students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. <span data-ttu-id="ebde0-268">W oknie zapytania SQL Server Management Studio wykonaj następujące zapytanie:</span><span class="sxs-lookup"><span data-stu-id="ebde0-268">In a SQL Server Management Studio query window, execute following query:</span></span>

   ```sql
   -- Find all hello courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="ebde0-269">Przywracanie bazy danych tooa poprzedniego punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="ebde0-269">Restore a database tooa previous point in time</span></span>

<span data-ttu-id="ebde0-270">Załóżmy, że przypadkowo usunięto tabelę.</span><span class="sxs-lookup"><span data-stu-id="ebde0-270">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="ebde0-271">Jest to coś, co nie można łatwo odzyskać z.</span><span class="sxs-lookup"><span data-stu-id="ebde0-271">This is something you cannot easily recover from.</span></span> <span data-ttu-id="ebde0-272">Bazy danych SQL Azure pozwala toogo tooany zapasowego punktu w czasie w hello ostatnio zapasowej too35 dni i przywrócić ten punkt w czasie tooa nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ebde0-272">Azure SQL Database allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new database.</span></span> <span data-ttu-id="ebde0-273">Możesz to toorecover bazy danych usunięte dane.</span><span class="sxs-lookup"><span data-stu-id="ebde0-273">You can you this database toorecover your deleted data.</span></span> <span data-ttu-id="ebde0-274">Hello następujące kroki hello przykładowej bazy danych tooa punktu przywracania przed dodaniem hello tabel.</span><span class="sxs-lookup"><span data-stu-id="ebde0-274">hello following steps restore hello sample database tooa point before hello tables were added.</span></span>

1. <span data-ttu-id="ebde0-275">Na stronie Baza danych SQL hello bazy danych, kliknij przycisk **przywrócić** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="ebde0-275">On hello SQL Database page for your database, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="ebde0-276">Witaj **przywrócić** zostanie otwarta strona.</span><span class="sxs-lookup"><span data-stu-id="ebde0-276">hello **Restore** page opens.</span></span>

   ![Przywracanie](./media/sql-database-design-first-database/restore.png)

2. <span data-ttu-id="ebde0-278">Wypełnianie hello **przywrócić** formularza hello wymagane informacje:</span><span class="sxs-lookup"><span data-stu-id="ebde0-278">Fill out hello **Restore** form with hello required information:</span></span>
    * <span data-ttu-id="ebde0-279">Nazwa bazy danych: podaj nazwę bazy danych</span><span class="sxs-lookup"><span data-stu-id="ebde0-279">Database name: Provide a database name</span></span> 
    * <span data-ttu-id="ebde0-280">W momencie: Wybierz hello **w momencie** kartę w formularzu przywracania hello</span><span class="sxs-lookup"><span data-stu-id="ebde0-280">Point-in-time: Select hello **Point-in-time** tab on hello Restore form</span></span> 
    * <span data-ttu-id="ebde0-281">Punkt przywracania: Wybierz godzinę, która występuje przed zmianą hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="ebde0-281">Restore point: Select a time that occurs before hello database was changed</span></span>
    * <span data-ttu-id="ebde0-282">Serwer docelowy: nie można zmienić tę wartość podczas przywracania bazy danych</span><span class="sxs-lookup"><span data-stu-id="ebde0-282">Target server: You cannot change this value when restoring a database</span></span> 
    * <span data-ttu-id="ebde0-283">Elastyczna pula baz danych: Wybierz **None**</span><span class="sxs-lookup"><span data-stu-id="ebde0-283">Elastic database pool: Select **None**</span></span>  
    * <span data-ttu-id="ebde0-284">Warstwa cenowa: Wybierz **20 jednostek Dtu** i **250 GB** magazynu.</span><span class="sxs-lookup"><span data-stu-id="ebde0-284">Pricing tier: Select **20 DTUs** and **250 GB** of storage.</span></span>

   ![punkt przywracania](./media/sql-database-design-first-database/restore-point.png)

3. <span data-ttu-id="ebde0-286">Kliknij przycisk **OK** toorestore hello bazy danych za[tooa punktu przywracania w czasie](sql-database-recovery-using-backups.md#point-in-time-restore) przed dodaniem hello tabel.</span><span class="sxs-lookup"><span data-stu-id="ebde0-286">Click **OK** toorestore hello database too[restore tooa point in time](sql-database-recovery-using-backups.md#point-in-time-restore) before hello tables were added.</span></span> <span data-ttu-id="ebde0-287">Przywracanie bazy danych tooa innego punktu w czasie tworzy duplikat bazy danych w hello tym samym serwerze co hello oryginalnej bazy danych lub nowszym hello punktu w czasie określisz, tak długo, jak jest w okresie przechowywania powitania dla Twojego [warstwy usług](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="ebde0-287">Restoring a database tooa different point in time creates a duplicate database in hello same server as hello original database as of hello point in time you specify, as long as it is within hello retention period for your [service tier](sql-database-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebde0-288">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ebde0-288">Next Steps</span></span> 
<span data-ttu-id="ebde0-289">W tym samouczku przedstawiono bazy danych podstawowych zadań takich jak utworzyć bazę danych i tabele, załadować zapytania na danych i przywrócić hello bazy danych tooa wcześniejszego punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="ebde0-289">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="ebde0-290">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="ebde0-290">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="ebde0-291">Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="ebde0-291">Create a database</span></span>
> * <span data-ttu-id="ebde0-292">Konfigurowanie reguł zapory</span><span class="sxs-lookup"><span data-stu-id="ebde0-292">Set up a firewall rule</span></span>
> * <span data-ttu-id="ebde0-293">Połączenia bazy danych toohello z [programu SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span><span class="sxs-lookup"><span data-stu-id="ebde0-293">Connect toohello database with [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span></span>
> * <span data-ttu-id="ebde0-294">Tworzenie tabel</span><span class="sxs-lookup"><span data-stu-id="ebde0-294">Create tables</span></span>
> * <span data-ttu-id="ebde0-295">Danych ładowania zbiorczego</span><span class="sxs-lookup"><span data-stu-id="ebde0-295">Bulk load data</span></span>
> * <span data-ttu-id="ebde0-296">Dane zapytania</span><span class="sxs-lookup"><span data-stu-id="ebde0-296">Query that data</span></span>
> * <span data-ttu-id="ebde0-297">Przywracanie bazy danych hello tooa poprzedniego punktu w czasie przy użyciu bazy danych SQL [punktu w czasie przywracania](sql-database-recovery-using-backups.md#point-in-time-restore) możliwości</span><span class="sxs-lookup"><span data-stu-id="ebde0-297">Restore hello database tooa previous point in time using SQL Database [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) capabilities</span></span>

<span data-ttu-id="ebde0-298">Przejdź dalej toolearn samouczka toohello o projektowaniu bazy danych przy użyciu programu Visual Studio i C#.</span><span class="sxs-lookup"><span data-stu-id="ebde0-298">Advance toohello next tutorial toolearn about designing a database using Visual Studio and C#.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="ebde0-299">Projekt bazy danych Azure SQL i Połącz z C# i ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ebde0-299">Design an Azure SQL database and connect with C# and ADO.NET</span></span>](sql-database-design-first-database-csharp.md)
