---
title: "Rozpoczynanie pracy aaaAzure SQL Data Warehouse — samouczek | Dokumentacja firmy Microsoft"
description: "W tym samouczku jest przedstawienie sposobu tooprovision i ładowanie danych do usługi Azure SQL Data Warehouse. Dowiesz się hello podstawy dotyczące skalowania, wstrzymywanie i dostrajania."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="f602f-104">Rozpoczynanie pracy z usługą SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f602f-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="f602f-105">Ten samouczek pokazuje, jak tooprovision i ładowanie danych do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f602f-105">This tutorial shows how tooprovision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f602f-106">Dowiesz się hello podstawy dotyczące skalowania, wstrzymywanie i dostrajania.</span><span class="sxs-lookup"><span data-stu-id="f602f-106">You’ll also learn hello basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="f602f-107">Po zakończeniu, należy być gotowe tooquery i Eksploruj magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="f602f-107">When you’re finished, you’ll be ready tooquery and explore your data warehouse.</span></span>

<span data-ttu-id="f602f-108">**Szacowany czas toocomplete:** jest na trasie samouczek z przykładowy kod, który toocomplete około 30 minut po hello wymagania wstępne zostały spełnione.</span><span class="sxs-lookup"><span data-stu-id="f602f-108">**Estimated time toocomplete:** This is an end-to-end tutorial with example code that takes about 30 minutes toocomplete once you have met hello prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f602f-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f602f-109">Prerequisites</span></span>

<span data-ttu-id="f602f-110">Hello samouczka przyjęto założenie, że czytelnik zna podstawowe pojęcia dotyczące usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f602f-110">hello tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="f602f-111">Wprowadzenie można znaleźć na stronie [Co to jest usługa SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="f602f-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="f602f-112">Utwórz konto na platformie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f602f-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="f602f-113">Jeśli nie masz już konto Microsoft Azure, należy toosign dla jednego toouse tej usługi.</span><span class="sxs-lookup"><span data-stu-id="f602f-113">If you don't already have a Microsoft Azure account, you need toosign up for one toouse this service.</span></span> <span data-ttu-id="f602f-114">Jeśli masz już konto platformy Azure, pomiń ten krok.</span><span class="sxs-lookup"><span data-stu-id="f602f-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="f602f-115">Przejdź do strony konta toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="f602f-115">Navigate toohello account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="f602f-116">Utwórz bezpłatne konto platformy Azure lub zakup konto.</span><span class="sxs-lookup"><span data-stu-id="f602f-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="f602f-117">Postępuj zgodnie z instrukcjami hello</span><span class="sxs-lookup"><span data-stu-id="f602f-117">Follow hello instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="f602f-118">Instalowanie odpowiednich sterowników i narzędzi klienta SQL</span><span class="sxs-lookup"><span data-stu-id="f602f-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="f602f-119">Większość narzędzi klienta SQL mogą łączyć się z tooSQL hurtowni danych przy użyciu JDBC, ODBC lub ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="f602f-119">Most SQL client tools can connect tooSQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="f602f-120">Powodu toohello dużej liczby funkcje T-SQL, które obsługuje magazyn danych SQL niektóre aplikacje klienckie nie są całkowicie zgodne z usługą Magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="f602f-120">Due toohello large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="f602f-121">Jeśli używasz systemu operacyjnego Windows, zalecamy użycie programu [Visual Studio] lub [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="f602f-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="f602f-122">Tworzenie bazy danych w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f602f-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="f602f-123">Magazyn danych SQL Data Warehouse to specjalny typ bazy danych zaprojektowany z myślą o masowym przetwarzaniu równoległym.</span><span class="sxs-lookup"><span data-stu-id="f602f-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="f602f-124">Baza danych Hello są rozproszone na wielu węzłach i przetwarza zapytania równolegle.</span><span class="sxs-lookup"><span data-stu-id="f602f-124">hello database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="f602f-125">Magazyn danych SQL ma węzeł kontrolny, będąca aranżacją hello działania wszystkich węzłów hello.</span><span class="sxs-lookup"><span data-stu-id="f602f-125">SQL Data Warehouse has a control node that orchestrates hello activities of all hello nodes.</span></span> <span data-ttu-id="f602f-126">Witaj w poszczególnych węzłach dane wykorzystywane toomanage bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="f602f-126">hello nodes themselves use SQL Database toomanage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="f602f-127">Utworzenie bazy danych w usłudze SQL Data Warehouse może skutkować powstaniem nowej usługi płatnej.</span><span class="sxs-lookup"><span data-stu-id="f602f-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="f602f-128">Aby uzyskać więcej informacji, zobacz [Cennik usługi SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="f602f-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="f602f-129">Tworzenie magazynu danych</span><span class="sxs-lookup"><span data-stu-id="f602f-129">Create a data warehouse</span></span>

1. <span data-ttu-id="f602f-130">Zaloguj się na powitania [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f602f-130">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f602f-131">Kliknij pozycję **Nowy** > **Bazy danych** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="f602f-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="f602f-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="f602f-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="f602f-133">Wypełnij szczegóły dotyczące wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f602f-133">Fill out deployment details</span></span>

    <span data-ttu-id="f602f-134">**Nazwa bazy danych**: wybierz dowolną.</span><span class="sxs-lookup"><span data-stu-id="f602f-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="f602f-135">Jeśli masz wiele magazynów danych, zaleca się nazwy zawierają szczegółowe informacje, takie jak hello regionu, środowisko, na przykład *mydw westus-1-test*.</span><span class="sxs-lookup"><span data-stu-id="f602f-135">If you have multiple data warehouses, we recommend your names include details such as hello region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="f602f-136">**Subskrypcja**: Twoja subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f602f-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="f602f-137">**Grupa zasobów**: utwórz grupę zasobów lub użyj istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="f602f-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="f602f-138">Grupy zasobów są przydatne w przypadku administrowania zasobami, co obejmuje na przykład wyznaczanie zakresu kontroli dostępu i wdrażanie oparte na szablonach.</span><span class="sxs-lookup"><span data-stu-id="f602f-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="f602f-139">Więcej o grupach zasobów platformy Azure i najlepszych praktykach możesz dowiedzieć się [tutaj](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span><span class="sxs-lookup"><span data-stu-id="f602f-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="f602f-140">**Źródło**: pusta baza danych</span><span class="sxs-lookup"><span data-stu-id="f602f-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="f602f-141">**Serwer**: serwer hello wybierz utworzony w [wymagania wstępne].</span><span class="sxs-lookup"><span data-stu-id="f602f-141">**Server**: Select hello server you created in [Prerequisites].</span></span>

    <span data-ttu-id="f602f-142">**Sortowanie**: pozostaw hello domyślnego sortowania SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="f602f-142">**Collation**: Leave hello default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="f602f-143">**Wybierz wydajności**: zalecamy Rozpoczynanie od hello 400DWU standardowa.</span><span class="sxs-lookup"><span data-stu-id="f602f-143">**Select performance**: We recommend starting with hello standard 400DWU.</span></span>

4. <span data-ttu-id="f602f-144">Wybierz **toodashboard numeru Pin** ![tooDashboard numeru Pin](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="f602f-144">Choose **Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="f602f-145">Zaczekaj i poczekaj, aż Twoje toodeploy magazynu danych!</span><span class="sxs-lookup"><span data-stu-id="f602f-145">Sit back and wait for your data warehouse toodeploy!</span></span> <span data-ttu-id="f602f-146">Jest zjawiskiem tootake tego procesu kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f602f-146">It's normal for this process tootake several minutes.</span></span> <span data-ttu-id="f602f-147">Hello portal powiadamia użytkownika, gdy magazyn danych jest gotowy toouse.</span><span class="sxs-lookup"><span data-stu-id="f602f-147">hello portal notifies you when your data warehouse is ready toouse.</span></span> 

## <a name="connect-toosql-data-warehouse"></a><span data-ttu-id="f602f-148">Połącz tooSQL magazynu danych</span><span class="sxs-lookup"><span data-stu-id="f602f-148">Connect tooSQL Data Warehouse</span></span>

<span data-ttu-id="f602f-149">W tym samouczku korzysta z magazynu danych programu SQL Server Management Studio (SSMS) tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="f602f-149">This tutorial uses SQL Server Management Studio (SSMS) tooconnect toohello data warehouse.</span></span> <span data-ttu-id="f602f-150">Możesz połączyć tooSQL hurtowni danych za pośrednictwem obsługiwanych łączników: ADO.NET, JDBC ODBC i PHP.</span><span class="sxs-lookup"><span data-stu-id="f602f-150">You can connect tooSQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="f602f-151">W przypadku narzędzi nieobsługiwanych przez firmę Microsoft funkcjonalność może być ograniczona.</span><span class="sxs-lookup"><span data-stu-id="f602f-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="f602f-152">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="f602f-152">Get connection information</span></span>

<span data-ttu-id="f602f-153">Magazyn danych tooyour tooconnect, należy tooconnect za pośrednictwem powitania serwera logicznego SQL utworzony w [wymagania wstępne].</span><span class="sxs-lookup"><span data-stu-id="f602f-153">tooconnect tooyour data warehouse, you need tooconnect through hello logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="f602f-154">Wybierz magazyn danych z pulpitu nawigacyjnego hello lub wyszukaj go w Twoich zasobów.</span><span class="sxs-lookup"><span data-stu-id="f602f-154">Select your data warehouse from hello dashboard or search for it in your resources.</span></span>

    ![Pulpit nawigacyjny usługi SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="f602f-156">Znajdź pełną nazwę serwera logicznego SQL hello hello.</span><span class="sxs-lookup"><span data-stu-id="f602f-156">Find hello full name for hello logical SQL server.</span></span>

    ![Wybieranie nazwy serwera](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="f602f-158">Otwórz SSMS i użyj obiektu explorer tooconnect toothis serwera przy użyciu poświadczeń administratora serwera na powitania utworzony w [wymagania wstępne]</span><span class="sxs-lookup"><span data-stu-id="f602f-158">Open SSMS and use object explorer tooconnect toothis server using hello server admin credentials you created in [Prerequisites]</span></span>

    ![Nawiązywanie połączenia z programem SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="f602f-160">Jeśli wszystko przebiegnie poprawnie, powinno być teraz połączonych tooyour logicznego programu SQL server.</span><span class="sxs-lookup"><span data-stu-id="f602f-160">If all goes correctly, you should now be connected tooyour logical SQL server.</span></span> <span data-ttu-id="f602f-161">Ponieważ użytkownik zalogowany jako administrator serwera Witaj, możesz połączyć tooany bazy danych obsługiwanych przez serwer hello, w tym hello bazy danych master.</span><span class="sxs-lookup"><span data-stu-id="f602f-161">Since you logged in as hello server admin, you can connect tooany database hosted by hello server, including hello master database.</span></span> 

<span data-ttu-id="f602f-162">Istnieje tylko jeden serwer, konto administratora i ma hello większość uprawnień przez dowolnego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f602f-162">There is only one server admin account and it has hello most privileges of any user.</span></span> <span data-ttu-id="f602f-163">Należy zachować ostrożność nie tooallow zbyt wiele osób w organizacji hasło administratora hello tooknow.</span><span class="sxs-lookup"><span data-stu-id="f602f-163">Be careful not tooallow too many people in your organization tooknow hello admin password.</span></span> 

<span data-ttu-id="f602f-164">Możesz również mieć konto administratora usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f602f-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="f602f-165">Firma Microsoft nie udostępniają hello tutaj.</span><span class="sxs-lookup"><span data-stu-id="f602f-165">We don't provide hello details here.</span></span> <span data-ttu-id="f602f-166">Jeśli chcesz toolearn więcej informacji na temat przy użyciu uwierzytelniania usługi Azure Active Directory, zobacz [uwierzytelniania usługi Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="f602f-166">If you want toolearn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="f602f-167">Następnym tematem jest tworzenie dodatkowych kont logowania i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f602f-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="f602f-168">Tworzenie użytkownika bazy danych</span><span class="sxs-lookup"><span data-stu-id="f602f-168">Create a database user</span></span>

<span data-ttu-id="f602f-169">W tym kroku utworzysz tooaccess konta użytkownika magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="f602f-169">In this step, you create a user account tooaccess your data warehouse.</span></span> <span data-ttu-id="f602f-170">Możemy również przedstawiają sposób toogive tego użytkownika hello możliwości toorun zapytania dużą ilość pamięci i zasobów Procesora.</span><span class="sxs-lookup"><span data-stu-id="f602f-170">We also show you how toogive that user hello ability toorun queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a><span data-ttu-id="f602f-171">Uwagi dotyczące klasy zasobu przydzielania zasobów tooqueries</span><span class="sxs-lookup"><span data-stu-id="f602f-171">Notes about resource classes for allocating resources tooqueries</span></span>

- <span data-ttu-id="f602f-172">tookeep danych bezpieczne, nie używaj powitania serwera admin toorun zapytania na produkcyjnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="f602f-172">tookeep your data safe, don't use hello server admin toorun queries on your production databases.</span></span> <span data-ttu-id="f602f-173">Ma hello większości uprawnienia każdego użytkownika i przy jego użyciu tooperform operacji na danych użytkownika umieszcza dane na ryzyko.</span><span class="sxs-lookup"><span data-stu-id="f602f-173">It has hello most privileges of any user and using it tooperform operations on user data puts your data at risk.</span></span> <span data-ttu-id="f602f-174">Ponadto ponieważ Witaj, Administratorze server jest przeznaczona tooperform operacji zarządzania, uruchamia operacje, przy użyciu tylko małych alokacji pamięci i zasobów procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="f602f-174">Also, since hello server admin is meant tooperform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="f602f-175">Usługi SQL Data Warehouse używa ról wstępnie zdefiniowanych bazy danych, o nazwie klasy zasobu, tooallocate różnych ilości pamięci, zasobów Procesora i toousers miejsc współbieżności.</span><span class="sxs-lookup"><span data-stu-id="f602f-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, tooallocate different amounts of memory, CPU resources, and concurrency slots toousers.</span></span> <span data-ttu-id="f602f-176">Każdy użytkownik może należeć tooa klasy mały, Średni, duża lub bardzo duży zasób.</span><span class="sxs-lookup"><span data-stu-id="f602f-176">Each user can belong tooa small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="f602f-177">Witaj klasy zasobów użytkownika określa hello zasobów hello użytkownik ma toorun zapytań i załaduj operacji.</span><span class="sxs-lookup"><span data-stu-id="f602f-177">hello user's resource class determines hello resources hello user has toorun queries and load operations.</span></span>

- <span data-ttu-id="f602f-178">Kompresja danych optymalną hello użytkownika może być wymagane tooload duże lub alokacji zasobów bardzo duża.</span><span class="sxs-lookup"><span data-stu-id="f602f-178">For optimal data compression, hello user may need tooload with large or extra large resource allocations.</span></span> <span data-ttu-id="f602f-179">Więcej o klasach zasobów może dowiedzieć się [tutaj](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span><span class="sxs-lookup"><span data-stu-id="f602f-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="f602f-180">Tworzenie konta z możliwością sterowania bazą danych</span><span class="sxs-lookup"><span data-stu-id="f602f-180">Create an account that can control a database</span></span>

<span data-ttu-id="f602f-181">Ponieważ użytkownik jest zalogowany w hello administratora serwera ma uprawnienia logowania toocreate i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f602f-181">Since you are currently logged in as hello server admin you have permissions toocreate logins and users.</span></span>

1. <span data-ttu-id="f602f-182">Za pomocą programu SSMS lub innego klienta zapytań otwórz nowe zapytanie dotyczące bazy danych **master**.</span><span class="sxs-lookup"><span data-stu-id="f602f-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Nowe zapytanie w bazie danych master Master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nowe zapytanie w bazie danych master Master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="f602f-185">W oknie zapytania hello Uruchom to toocreate polecenia T-SQL o nazwie MedRCLogin logowania i użytkownika o nazwie LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="f602f-185">In hello query window, run this T-SQL command toocreate a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="f602f-186">Tę nazwę logowania można połączyć toohello logicznego programu SQL server.</span><span class="sxs-lookup"><span data-stu-id="f602f-186">This login can connect toohello logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="f602f-187">Teraz zapytanie hello *bazy danych magazynu danych SQL*, utworzyć użytkownika bazy danych na podstawie hello utworzony tooaccess logowania i wykonywania operacji na powitania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f602f-187">Now querying hello *SQL Data Warehouse database*, create a database user based on hello login you created tooaccess and perform operations on hello database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="f602f-188">Nadaj hello użytkownika kontroli uprawnień toohello baza danych o nazwie NYT.</span><span class="sxs-lookup"><span data-stu-id="f602f-188">Give hello database user control permissions toohello database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="f602f-189">Jeśli nazwa bazy danych ma łączników, należy się toowrap go w nawiasach!</span><span class="sxs-lookup"><span data-stu-id="f602f-189">If your database name has hyphens in it, be sure toowrap it in brackets!</span></span> 
    >

### <a name="give-hello-user-medium-resource-allocations"></a><span data-ttu-id="f602f-190">Nadaj alokacji zasobów średnia użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="f602f-190">Give hello user medium resource allocations</span></span>

1. <span data-ttu-id="f602f-191">Uruchom ten toomake polecenia T-SQL it, a element członkowski klasy hello średnia zasobu, która jest wywoływana mediumrc.</span><span class="sxs-lookup"><span data-stu-id="f602f-191">Run this T-SQL command toomake it a member of hello medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="f602f-192">Kliknij przycisk [tutaj](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn więcej informacji na temat klas współbieżności i zasobów!</span><span class="sxs-lookup"><span data-stu-id="f602f-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="f602f-193">Połącz z nowymi poświadczeniami hello toohello serwera logicznego</span><span class="sxs-lookup"><span data-stu-id="f602f-193">Connect toohello logical server with hello new credentials</span></span>

    ![Zaloguj się za pomocą nowego identyfikatora logowania](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="f602f-195">Ładowanie danych usługi Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="f602f-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="f602f-196">Wszystko jest teraz gotowy tooload danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="f602f-196">You are now ready tooload data into your data warehouse.</span></span> <span data-ttu-id="f602f-197">W tym kroku przedstawiono sposób obiektu blob tooload nowego Jorku taksówki cab danych z publicznej usługi Azure storage.</span><span class="sxs-lookup"><span data-stu-id="f602f-197">This step shows you how tooload New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="f602f-198">Typowa tooload danych do usługi SQL Data Warehouse jest toofirst przenieść magazyn obiektów blob tooAzure danych hello, a następnie załadować go do magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="f602f-198">A common way tooload data into SQL Data Warehouse is toofirst move hello data tooAzure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="f602f-199">toomake on toounderstand łatwiejszy sposób tooload, mamy danych pliku cab taksówki Nowy Jork już hostowana w obiekcie blob magazynu Azure publicznego.</span><span class="sxs-lookup"><span data-stu-id="f602f-199">toomake it easier toounderstand how tooload, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="f602f-200">Do użytku w przyszłości, toolearn jak tooget Twojego tooAzure danych obiektu blob magazynu lub tooload go bezpośrednio ze źródła do usługi SQL Data Warehouse, zobacz hello [omówienie ładowania](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="f602f-200">For future reference, toolearn how tooget your data tooAzure blob storage or tooload it directly from your source into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="f602f-201">Definiowanie danych zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="f602f-201">Define external data</span></span>

1. <span data-ttu-id="f602f-202">Utwórz klucz główny.</span><span class="sxs-lookup"><span data-stu-id="f602f-202">Create a master key.</span></span> <span data-ttu-id="f602f-203">Wystarczy toocreate klucz główny raz na bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f602f-203">You only need toocreate a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="f602f-204">Zdefiniuj lokalizację hello hello obiektów blob platformy Azure, zawierający dane pliku cab taksówki hello.</span><span class="sxs-lookup"><span data-stu-id="f602f-204">Define hello location of hello Azure blob that contains hello taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="f602f-205">Zdefiniuj hello formatów plików zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="f602f-205">Define hello external file formats</span></span>

    <span data-ttu-id="f602f-206">Witaj ```CREATE EXTERNAL FILE FORMAT``` polecenie jest toospecify używany format plików, które zawierają hello danych zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="f602f-206">hello ```CREATE EXTERNAL FILE FORMAT``` command is used toospecify the format of files that contain hello external data.</span></span> <span data-ttu-id="f602f-207">Zawierają one tekst rozdzielony znakami nazywanymi ogranicznikami.</span><span class="sxs-lookup"><span data-stu-id="f602f-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="f602f-208">Dla celów demonstracyjnych hello taksówki cab dane są przechowywane, zarówno jako nieskompresowanych danych, jak i jako dane skompresowane gzip.</span><span class="sxs-lookup"><span data-stu-id="f602f-208">For demonstration purposes, hello taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="f602f-209">Uruchom te polecenia T-SQL toodefine dwóch różnych formatach: nieskompresowane i skompresowane.</span><span class="sxs-lookup"><span data-stu-id="f602f-209">Run these T-SQL commands toodefine two different formats: uncompressed and compressed.</span></span>

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  <span data-ttu-id="f602f-210">Utwórz schemat dla formatu plików zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="f602f-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="f602f-211">Utwórz hello tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="f602f-211">Create hello external tables.</span></span> <span data-ttu-id="f602f-212">Te tabele odwołują się do danych przechowywanych w usłudze Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f602f-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="f602f-213">Uruchom następujące toocreate polecenia T-SQL hello kilku tabel zewnętrznych, że wszystkie punktu toohello obiektów blob platformy Azure zdefiniowanego wcześniej w naszym zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="f602f-213">Run hello following T-SQL commands toocreate several external tables that all point toohello Azure blob we defined previously in our external data source.</span></span>

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a><span data-ttu-id="f602f-214">Importuj dane hello z magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f602f-214">Import hello data from Azure blob storage.</span></span>

<span data-ttu-id="f602f-215">Usługa SQL Data Warehouse obsługuje kluczową instrukcję o nazwie CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="f602f-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="f602f-216">Ta instrukcja tworzy nową tabelę na podstawie wyników hello instrukcji select.</span><span class="sxs-lookup"><span data-stu-id="f602f-216">This statement creates a new table based on hello results of a select statement.</span></span> <span data-ttu-id="f602f-217">Witaj nowa tabela zawiera hello tej samej kolumny i typy danych jak wyniki hello hello wybierz instrukcji.</span><span class="sxs-lookup"><span data-stu-id="f602f-217">hello new table has hello same columns and data types as hello results of hello select statement.</span></span>  <span data-ttu-id="f602f-218">To są dane tooimport elegancki sposób z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f602f-218">This is an elegant way tooimport data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="f602f-219">Uruchom ten skrypt tooimport danych.</span><span class="sxs-lookup"><span data-stu-id="f602f-219">Run this script tooimport your data.</span></span>

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. <span data-ttu-id="f602f-220">Wyświetlaj dane podczas ładowania.</span><span class="sxs-lookup"><span data-stu-id="f602f-220">View your data as it loads.</span></span>

   <span data-ttu-id="f602f-221">Ładowane jest kilka gigabajtów danych, które są kompresowane do wysoce wydajnych indeksów magazynu kolumn klastra.</span><span class="sxs-lookup"><span data-stu-id="f602f-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="f602f-222">Uruchom następujące zapytanie, które korzysta z dynamicznego zarządzania widoków (widoków DMV) tooshow hello stan obciążenia hello hello.</span><span class="sxs-lookup"><span data-stu-id="f602f-222">Run hello following query that uses a dynamic management views (DMVs) tooshow hello status of hello load.</span></span> <span data-ttu-id="f602f-223">Po uruchomieniu kwerendy hello, wystarczy pobrać kawy i popcorn podczas SQL Data Warehouse nie niektórych lifting ciężki.</span><span class="sxs-lookup"><span data-stu-id="f602f-223">After starting hello query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. <span data-ttu-id="f602f-224">Wyświetl wszystkie zapytania systemowe.</span><span class="sxs-lookup"><span data-stu-id="f602f-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="f602f-225">Korzystaj z danych poprawnie załadowanych do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f602f-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Wyświetl załadowane dane](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="f602f-227">Zwiększanie wydajności zapytań</span><span class="sxs-lookup"><span data-stu-id="f602f-227">Improve query performance</span></span>

<span data-ttu-id="f602f-228">Istnieje kilka sposobów tooimprove kwerendy wydajności i tooachieve hello szybkich wydajność usługi SQL Data Warehouse jest zaprojektowany tooprovide.</span><span class="sxs-lookup"><span data-stu-id="f602f-228">There are several ways tooimprove query performance and tooachieve hello high-speed performance that SQL Data Warehouse is designed tooprovide.</span></span>  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a><span data-ttu-id="f602f-229">Zobacz efekt hello skalowanie na wydajność zapytań</span><span class="sxs-lookup"><span data-stu-id="f602f-229">See hello effect of scaling on query performance</span></span> 

<span data-ttu-id="f602f-230">Wydajność zapytania jednokierunkowej tooimprove jest tooscale zasobów, zmieniając poziom usług DWU hello magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="f602f-230">One way tooimprove query performance is tooscale resources by changing hello DWU service level for your data warehouse.</span></span> <span data-ttu-id="f602f-231">Poszczególne poziomy usług są coraz droższe, ale w dowolnej chwili można przeprowadzić skalowanie w dół lub wstrzymać zasoby.</span><span class="sxs-lookup"><span data-stu-id="f602f-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="f602f-232">W tym kroku wykonywane jest porównanie wydajności dla dwóch różnych ustawień jednostek DWU.</span><span class="sxs-lookup"><span data-stu-id="f602f-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="f602f-233">Najpierw Przeprowadź skalowanie hello zmiany rozmiaru w dół too100 DWU, więc można pobrać informacje o tym, jak jeden węzeł obliczeń może wykonywać samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="f602f-233">First, let's scale hello sizing down too100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="f602f-234">Przejdź toohello portalu i wybierz polecenie SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f602f-234">Go toohello portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="f602f-235">W bloku usługi SQL Data Warehouse hello wybierz skali.</span><span class="sxs-lookup"><span data-stu-id="f602f-235">Select scale in hello SQL Data Warehouse blade.</span></span> 

    ![Skalowanie usługi SQL Data Warehouse z poziomu portalu](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="f602f-237">Dół wydajności hello paska too100 DWU i kliknij przycisk Zapisz.</span><span class="sxs-lookup"><span data-stu-id="f602f-237">Scale down hello performance bar too100 DWU and hit save.</span></span>

    ![Skaluj i zapisz](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="f602f-239">Poczekaj, aż Twoje toofinish operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="f602f-239">Wait for your scale operation toofinish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f602f-240">Zapytania nie można uruchomić podczas zmiany hello skali.</span><span class="sxs-lookup"><span data-stu-id="f602f-240">Queries cannot run while changing hello scale.</span></span> <span data-ttu-id="f602f-241">Skalowanie powoduje **skasowanie** aktualnie uruchomionych zapytań.</span><span class="sxs-lookup"><span data-stu-id="f602f-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="f602f-242">Można uruchomić je ponownie, po zakończeniu operacji hello.</span><span class="sxs-lookup"><span data-stu-id="f602f-242">You can restart them when hello operation is finished.</span></span>
    >
    
5. <span data-ttu-id="f602f-243">Wykonaj operację skanowania na powitania podróży danych, wybierając hello top milionów wpisy dla wszystkich kolumn hello.</span><span class="sxs-lookup"><span data-stu-id="f602f-243">Do a scan operation on hello trip data, selecting hello top million entries for all hello columns.</span></span> <span data-ttu-id="f602f-244">Jeśli używasz wczesny toomove szybko, możesz tooselect wolnego mniej wierszy.</span><span class="sxs-lookup"><span data-stu-id="f602f-244">If you're eager toomove on quickly, feel free tooselect fewer rows.</span></span> <span data-ttu-id="f602f-245">Zwróć uwagę na powitania czas toorun tej operacji.</span><span class="sxs-lookup"><span data-stu-id="f602f-245">Take note of hello time it takes toorun this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="f602f-246">Skalować dane kopii too400 DWU.</span><span class="sxs-lookup"><span data-stu-id="f602f-246">Scale your data warehouse back too400 DWU.</span></span> <span data-ttu-id="f602f-247">Należy pamiętać, że w każdym 100 DWU polega na dodaniu innego tooyour węzła obliczeń magazyn danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f602f-247">Remember, each 100 DWU is adding another compute node tooyour Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="f602f-248">Ponownie uruchom zapytanie Witaj!</span><span class="sxs-lookup"><span data-stu-id="f602f-248">Run hello query again!</span></span> <span data-ttu-id="f602f-249">Powinna być zauważalna istotna różnica.</span><span class="sxs-lookup"><span data-stu-id="f602f-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="f602f-250">Ponieważ hello zapytanie zwraca dużą ilość danych, dostępnej przepustowości hello maszyny hello uruchomionej SSMS może być wąskie gardło.</span><span class="sxs-lookup"><span data-stu-id="f602f-250">Because hello query returns a lot of data, hello bandwidth availability of hello machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="f602f-251">Może to spowodować, że użytkownik nie odczuje jakiegokolwiek zwiększenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="f602f-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="f602f-252">Usługa SQL Data Warehouse korzysta bowiem z masowego przetwarzania równoległego.</span><span class="sxs-lookup"><span data-stu-id="f602f-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="f602f-253">Zapytania, które skanowania ani wykonywać funkcje analityczne na miliony wierszy wystąpić hello true możliwości usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f602f-253">Queries that scan or perform analytic functions on millions of rows experience hello true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a><span data-ttu-id="f602f-254">Zobaczyć efekt hello statystyk na wydajność zapytań</span><span class="sxs-lookup"><span data-stu-id="f602f-254">See hello effect of statistics on query performance</span></span>

1. <span data-ttu-id="f602f-255">Uruchom zapytanie, że sprzężenia hello tabeli danych z tabeli podróży hello</span><span class="sxs-lookup"><span data-stu-id="f602f-255">Run a query that joins hello Date table with hello Trip table</span></span>

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    <span data-ttu-id="f602f-256">To zapytanie zajmie trochę czasu, ponieważ Magazyn danych SQL ma tooshuffle danych, zanim można wykonywać hello sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="f602f-256">This query takes a while because SQL Data Warehouse has tooshuffle data before it can perform hello join.</span></span> <span data-ttu-id="f602f-257">Sprzężenia nie ma danych tooshuffle, jeśli są one zaprojektowane toojoin danych hello jest rozpowszechniana tak samo.</span><span class="sxs-lookup"><span data-stu-id="f602f-257">Joins do not have tooshuffle data if they are designed toojoin data in hello same way it is distributed.</span></span> <span data-ttu-id="f602f-258">Jest to nieco skomplikowane.</span><span class="sxs-lookup"><span data-stu-id="f602f-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="f602f-259">Przychodzi tu z pomocą statystyka.</span><span class="sxs-lookup"><span data-stu-id="f602f-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="f602f-260">Uruchom statystyki toocreate tej instrukcji na powitania kolumn sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="f602f-260">Run this statement toocreate statistics on hello join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="f602f-261">Usługa SQL Data Warehouse nie zarządza statystykami automatycznie.</span><span class="sxs-lookup"><span data-stu-id="f602f-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="f602f-262">Statystyki są istotne w przypadku wydajności zapytań i zdecydowanie zalecane jest ich tworzenie i aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="f602f-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="f602f-263">**Możesz uzyskać hello największe korzyści uzyskanie statystyki do kolumn uczestniczących w sprzężeniu, kolumn używanych w hello klauzuli i kolumny wykrytych GROUP BY.**</span><span class="sxs-lookup"><span data-stu-id="f602f-263">**You gain hello most benefit by having statistics on columns involved in joins, columns used in hello WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="f602f-264">Ponownie uruchom zapytanie hello z wymagań wstępnych i sprawdź wszystkie problemy dotyczące różnic wydajności.</span><span class="sxs-lookup"><span data-stu-id="f602f-264">Run hello query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="f602f-265">Podczas hello różnic w wydajności zapytania nie zostanie jako radykalne jako skalowanie, można zauważyć, przyspieszyć.</span><span class="sxs-lookup"><span data-stu-id="f602f-265">While hello differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f602f-266">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f602f-266">Next steps</span></span>

<span data-ttu-id="f602f-267">Jest teraz gotowy tooquery i eksplorowanie.</span><span class="sxs-lookup"><span data-stu-id="f602f-267">You're now ready tooquery and explore.</span></span> <span data-ttu-id="f602f-268">Zapoznaj się z naszymi najlepszymi praktykami i poradami.</span><span class="sxs-lookup"><span data-stu-id="f602f-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="f602f-269">Gdy wszystko będzie gotowe poszukiwania dzień hello, upewnij się, że toopause wystąpienia!</span><span class="sxs-lookup"><span data-stu-id="f602f-269">If you're done exploring for hello day, make sure toopause your instance!</span></span> <span data-ttu-id="f602f-270">W środowisku produkcyjnym, może występować znaczne oszczędności wstrzymywania i skalowanie toomeet potrzeb biznesowych.</span><span class="sxs-lookup"><span data-stu-id="f602f-270">In production, you can experience enormous savings by pausing and scaling toomeet your business needs.</span></span>

![Wstrzymaj](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="f602f-272">Przydatne zasoby</span><span class="sxs-lookup"><span data-stu-id="f602f-272">Useful readings</span></span>

<span data-ttu-id="f602f-273">[Współbieżność i zarządzanie obciążeniami][]</span><span class="sxs-lookup"><span data-stu-id="f602f-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="f602f-274">[Najlepsze praktyki dotyczące korzystania z usługi Azure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="f602f-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="f602f-275">[Monitorowanie zapytań][]</span><span class="sxs-lookup"><span data-stu-id="f602f-275">[Query Monitoring][]</span></span>

<span data-ttu-id="f602f-276">[10 najlepszych praktyk dotyczących tworzenia relacyjnego magazynu danych w dużej skali][]</span><span class="sxs-lookup"><span data-stu-id="f602f-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="f602f-277">[Migrowanie danych tooAzure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="f602f-277">[Migrating Data tooAzure SQL Data Warehouse][]</span></span>

[Współbieżność i zarządzanie obciążeniami]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Najlepsze praktyki dotyczące korzystania z usługi Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Monitorowanie zapytań]: sql-data-warehouse-manage-monitor.md
[10 najlepszych praktyk dotyczących tworzenia relacyjnego magazynu danych w dużej skali]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[Migrowanie danych tooAzure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[wymagania wstępne]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
