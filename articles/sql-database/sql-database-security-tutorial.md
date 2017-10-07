---
title: aaaSecure bazy danych Azure SQL | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o toosecure techniki i funkcje bazy danych Azure SQL."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="5a478-103">Zabezpieczenia bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="5a478-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="5a478-104">Baza danych SQL zabezpiecza dane poprzez ograniczenie przy użyciu reguł zapory, wymagających tooprove użytkowników, tożsamości i autoryzacji toodata za pośrednictwem członkostwa na podstawie ról i uprawnień, a także za pomocą mechanizmów uwierzytelniania tooyour dostępu do bazy danych zabezpieczenia na poziomie wiersza i maskowania danych dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="5a478-104">SQL Database secures your data by limiting access tooyour database using firewall rules, authentication mechanisms requiring users tooprove their identity, and authorization toodata through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="5a478-105">Można zwiększyć hello ochrony bazy danych przed złośliwymi użytkownikami lub nieautoryzowanego dostępu, wystarczy kilka prostych kroków.</span><span class="sxs-lookup"><span data-stu-id="5a478-105">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="5a478-106">W tym samouczku dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="5a478-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5a478-107">Konfigurowanie reguł zapory poziomu serwera dla serwera w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5a478-107">Set up server-level firewall rules for your server in hello Azure portal</span></span>
> * <span data-ttu-id="5a478-108">Konfigurowanie reguł zapory na poziomie bazy danych dla bazy danych przy użyciu narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="5a478-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="5a478-109">Połącz tooyour bazy danych przy użyciu ciągu bezpiecznego połączenia</span><span class="sxs-lookup"><span data-stu-id="5a478-109">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="5a478-110">Zarządzanie dostępem użytkowników</span><span class="sxs-lookup"><span data-stu-id="5a478-110">Manage user access</span></span>
> * <span data-ttu-id="5a478-111">Ochrona danych za pomocą szyfrowania</span><span class="sxs-lookup"><span data-stu-id="5a478-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="5a478-112">Włączanie inspekcji bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="5a478-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="5a478-113">Włączyć wykrywanie zagrożeń bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="5a478-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="5a478-114">Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="5a478-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a478-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5a478-115">Prerequisites</span></span>

<span data-ttu-id="5a478-116">toocomplete tego samouczka, upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="5a478-116">toocomplete this tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="5a478-117">Hello zainstalowana najnowsza wersja [programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="5a478-117">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="5a478-118">Zainstalowany program Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="5a478-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="5a478-119">Utworzone usługi Azure SQL server i bazy danych — zobacz [tworzenie bazy danych Azure SQL w portalu Azure hello](sql-database-get-started-portal.md), [tworzenia pojedynczej bazy danych Azure SQL przy użyciu interfejsu wiersza polecenia Azure hello](sql-database-get-started-cli.md), i [Utwórz pojedynczy SQL Azure bazy danych przy użyciu programu PowerShell](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5a478-119">Created an Azure SQL server and database - See [Create an Azure SQL database in hello Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using hello Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="5a478-120">Zaloguj się za toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5a478-120">Log in toohello Azure portal</span></span>

<span data-ttu-id="5a478-121">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5a478-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="5a478-122">Utworzyć regułę zapory poziomu serwera w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5a478-122">Create a server-level firewall rule in hello Azure portal</span></span>

<span data-ttu-id="5a478-123">Baz danych są chronione przez zaporę Windows na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5a478-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="5a478-124">Domyślnie wszystkie połączenia toohello serwera i hello bazy danych wewnątrz powitania serwera są odrzucane, z wyjątkiem połączeń z innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="5a478-124">By default, all connections toohello server and hello databases inside hello server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="5a478-125">Aby uzyskać więcej informacji, zobacz [reguły zapory poziomu serwera i bazy danych na poziomie bazy danych SQL Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5a478-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="5a478-126">Najbezpieczniejszą konfigurację Hello jest tooset tooOFF "Zezwalaj na dostęp do usług tooAzure".</span><span class="sxs-lookup"><span data-stu-id="5a478-126">hello most secure configuration is tooset 'Allow access tooAzure services' tooOFF.</span></span> <span data-ttu-id="5a478-127">Jeśli potrzebujesz tooconnect toohello z bazy danych z maszyny Wirtualnej platformy Azure lub usługę w chmurze, należy utworzyć [zastrzeżonego adresu IP](../virtual-network/virtual-networks-reserved-public-ip.md) i umożliwiają tylko hello zastrzeżone IP address dostęp przez zaporę Windows hello.</span><span class="sxs-lookup"><span data-stu-id="5a478-127">If you need tooconnect toohello database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only hello reserved IP address access through hello firewall.</span></span> 

<span data-ttu-id="5a478-128">Wykonaj te kroki toocreate [regułę zapory poziomu serwera bazy danych SQL](sql-database-firewall-configure.md) dla połączeń tooallow serwera z określonego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="5a478-128">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server tooallow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="5a478-129">Po utworzeniu przykładowej bazy danych na platformie Azure przy użyciu jednej z poprzednich samouczki hello lub poradniki Szybki Start i są wykonywania tego samouczka na komputerze z hello tego samego adresu IP jego znajdował się, gdy udał przez te samouczki, można pominąć ten krok jako będą mieć utworzone reguły zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="5a478-129">If you have created a sample database in Azure using one of hello previous tutorials or quickstarts and are performing this tutorial on a computer with hello same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="5a478-130">Kliknij przycisk **baz danych SQL** z hello lewym menu kliknij hello bazy danych i chcesz tooconfigure reguły zapory powitania dla na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="5a478-130">Click **SQL databases** from hello left-hand menu and click hello database you would like tooconfigure hello firewall rule for on hello **SQL databases** page.</span></span> <span data-ttu-id="5a478-131">Witaj strona przeglądu otwartym bazy danych przedstawiający hello w pełni kwalifikowana nazwa serwera (takich jak **mynewserver 20170313.database.windows.net**) i udostępnia opcje dla dalszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5a478-131">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![reguła zapory serwera](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="5a478-133">Kliknij przycisk **ustawić Zapora serwera** na powitania narzędzi, jak pokazano na poprzedniej ilustracji hello.</span><span class="sxs-lookup"><span data-stu-id="5a478-133">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="5a478-134">Witaj **ustawienia zapory** zostanie otwarta strona hello bazy danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5a478-134">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="5a478-135">Kliknij przycisk **Dodaj adres IP klienta** na hello narzędzi tooadd hello publiczny adres IP portalu toohello podłączonego komputera hello z lub ręcznie wprowadzić hello reguły zapory, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5a478-135">Click **Add client IP** on hello toolbar tooadd hello public IP address of hello computer connected toohello portal with or enter hello firewall rule manually and then click **Save**.</span></span>

      ![ustawianie reguły zapory serwera](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="5a478-137">Kliknij przycisk **OK** , a następnie kliknij przycisk hello **X** tooclose hello **ustawienia zapory** strony.</span><span class="sxs-lookup"><span data-stu-id="5a478-137">Click **OK** and then click hello **X** tooclose hello **Firewall settings** page.</span></span>

<span data-ttu-id="5a478-138">Teraz możesz połączyć tooany powitania serwera bazy danych z hello określony adres IP lub zakres adresów IP.</span><span class="sxs-lookup"><span data-stu-id="5a478-138">You can now connect tooany database in hello server with hello specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="5a478-139">Usługa SQL Database nawiązuje komunikację na porcie 1433.</span><span class="sxs-lookup"><span data-stu-id="5a478-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="5a478-140">Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 1433 może nie być dozwolone przez zaporę w sieci.</span><span class="sxs-lookup"><span data-stu-id="5a478-140">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="5a478-141">Jeśli tak, nie będzie serwera bazy danych SQL Azure tooyour stanie tooconnect, chyba że dział IT otwiera port 1433.</span><span class="sxs-lookup"><span data-stu-id="5a478-141">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="5a478-142">Utworzyć regułę zapory poziomu bazy danych przy użyciu narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="5a478-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="5a478-143">Reguły zapory poziomu bazy danych pozwalają toocreate ustawienia innej zapory dla różnych baz danych w ramach hello tej samej logicznej zapory serwera i toocreate reguł, które można przenosić — co oznacza, że należy wykonać hello bazy danych, podczas [trybu failover ](sql-database-geo-replication-overview.md) zamiast przechowywane na powitania serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="5a478-143">Database-level firewall rules enable you toocreate different firewall settings for different databases within hello same logical server and toocreate firewall rules that are portable - meaning that they follow hello database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on hello SQL server.</span></span> <span data-ttu-id="5a478-144">Reguły zapory poziomu bazy danych może być skonfigurowany za pomocą instrukcji języka Transact-SQL lub tylko po skonfigurowaniu hello pierwszą regułę zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="5a478-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured hello first server-level firewall rule.</span></span> <span data-ttu-id="5a478-145">Aby uzyskać więcej informacji, zobacz [reguły zapory poziomu serwera i bazy danych na poziomie bazy danych SQL Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5a478-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="5a478-146">Wykonuje te czynności toocreate reguły zapory dotyczące bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5a478-146">Follows these steps toocreate a database-specific firewall rule.</span></span>

1. <span data-ttu-id="5a478-147">Połącz tooyour bazy danych, na przykład za pomocą [programu SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="5a478-147">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="5a478-148">W Eksploratorze obiektów kliknij prawym przyciskiem myszy hello bazy danych ma tooadd reguły dla zapory i kliknij przycisk **nowe zapytanie**.</span><span class="sxs-lookup"><span data-stu-id="5a478-148">In Object Explorer, right-click on hello database you want tooadd a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="5a478-149">Puste zapytanie zostanie otwarte okno czyli tooyour połączenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5a478-149">A blank query window opens that is connected tooyour database.</span></span>

3. <span data-ttu-id="5a478-150">W oknie zapytania hello zmodyfikować hello IP address tooyour publicznego adresu IP, a następnie wykonaj hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="5a478-150">In hello query window, modify hello IP address tooyour public IP address and then execute hello following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="5a478-151">Na pasku narzędzi hello, kliknij przycisk **Execute** reguły zapory hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5a478-151">On hello toolbar, click **Execute** toocreate hello firewall rule.</span></span>

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a><span data-ttu-id="5a478-152">Wyświetl jak tooconnect tooyour aplikacji bazy danych przy użyciu ciągu bezpiecznego połączenia</span><span class="sxs-lookup"><span data-stu-id="5a478-152">View how tooconnect an application tooyour database using a secure connection string</span></span>

<span data-ttu-id="5a478-153">tooensure bezpiecznego zaszyfrowanego połączenia między aplikacji klienckiej i bazy danych SQL, ciąg połączenia hello ma toobe skonfigurowany tak, aby:</span><span class="sxs-lookup"><span data-stu-id="5a478-153">tooensure a secure, encrypted connection between a client application and SQL Database, hello connection string has toobe configured to:</span></span>

- <span data-ttu-id="5a478-154">Żądanie połączenia szyfrowanego i</span><span class="sxs-lookup"><span data-stu-id="5a478-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="5a478-155">toonot zaufania hello certyfikatu serwera.</span><span class="sxs-lookup"><span data-stu-id="5a478-155">toonot trust hello server certificate.</span></span> 

<span data-ttu-id="5a478-156">Ustanawia połączenie przy użyciu zabezpieczeń TLS (Transport Layer) i zmniejsza zagrożenie hello man-in--middle.</span><span class="sxs-lookup"><span data-stu-id="5a478-156">This establishes a connection using Transport Layer Security (TLS) and reduces hello risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="5a478-157">Można uzyskać poprawnie skonfigurowane parametry połączenia bazy danych SQL, aby obsługiwany klient sterowniki z hello portalu Azure pokazany dla ADO.net w tym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="5a478-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from hello Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="5a478-158">Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="5a478-158">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span>

2. <span data-ttu-id="5a478-159">Na powitania **omówienie** stron dla bazy danych, kliknij przycisk **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="5a478-159">On hello **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="5a478-160">Przejrzyj hello pełną **ADO.NET** parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="5a478-160">Review hello complete **ADO.NET** connection string.</span></span>

    ![Parametry połączenia sterownika ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="5a478-162">Tworzenie bazy danych użytkowników</span><span class="sxs-lookup"><span data-stu-id="5a478-162">Creating database users</span></span>

<span data-ttu-id="5a478-163">Przed utworzeniem żadnych użytkowników, należy najpierw wybrać jedną z dwóch typów uwierzytelniania obsługiwanych przez bazę danych SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="5a478-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="5a478-164">**Uwierzytelnianie SQL**, który używa nazwy użytkownika i hasła do logowania i użytkowników, którzy są prawidłowe tylko w hello kontekst określonej bazy danych w ramach serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="5a478-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in hello context of a specific database within a logical server.</span></span> 

<span data-ttu-id="5a478-165">**Uwierzytelniania usługi Azure Active Directory**, który używa tożsamości zarządzanych przez usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5a478-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="5a478-166">Jeśli chcesz, aby toouse [usługi Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate w bazie danych SQL, musi istnieć wypełnione usługi Azure Active Directory, zanim będzie można kontynuować.</span><span class="sxs-lookup"><span data-stu-id="5a478-166">If you want toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="5a478-167">Wykonaj te kroki toocreate użytkownika za pomocą uwierzytelniania SQL:</span><span class="sxs-lookup"><span data-stu-id="5a478-167">Follow these steps toocreate a user using SQL Authentication:</span></span>

1. <span data-ttu-id="5a478-168">Połącz tooyour bazy danych, na przykład za pomocą [programu SQL Server Management Studio](./sql-database-connect-query-ssms.md) przy użyciu poświadczeń administratora serwera.</span><span class="sxs-lookup"><span data-stu-id="5a478-168">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="5a478-169">W Eksploratorze obiektów kliknij prawym przyciskiem myszy hello bazę danych tooadd nowego użytkownika na kliknij **nowe zapytanie**.</span><span class="sxs-lookup"><span data-stu-id="5a478-169">In Object Explorer, right-click on hello database you want tooadd a new user on and click **New Query**.</span></span> <span data-ttu-id="5a478-170">Puste zapytanie zostanie otwarte okno czyli połączonych toohello wybranej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5a478-170">A blank query window opens that is connected toohello selected database.</span></span>

3. <span data-ttu-id="5a478-171">W oknie zapytania hello wprowadź hello następujące zapytanie:</span><span class="sxs-lookup"><span data-stu-id="5a478-171">In hello query window, enter hello following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="5a478-172">Na pasku narzędzi hello, kliknij przycisk **Execute** toocreate hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5a478-172">On hello toolbar, click **Execute** toocreate hello user.</span></span>

5. <span data-ttu-id="5a478-173">Domyślnie program hello użytkownika połączenie toohello bazy danych, ale nie ma uprawnienia zapisu lub tooread danych.</span><span class="sxs-lookup"><span data-stu-id="5a478-173">By default, hello user can connect toohello database, but has no permissions tooread or write data.</span></span> <span data-ttu-id="5a478-174">toogrant toohello te uprawnienia nowo utworzony użytkownik, wykonaj następujące dwa polecenia w nowym oknie zapytania hello</span><span class="sxs-lookup"><span data-stu-id="5a478-174">toogrant these permissions toohello newly created user, execute hello following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="5a478-175">Jest najlepszym toocreate praktyki te konta bez uprawnień administratora na powitania bazy danych tooconnect poziomu tooyour bazy danych, chyba że potrzebne tooexecute administratora zadania, takie jak tworzenie nowych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5a478-175">It is best practice toocreate these non-administrator accounts at hello database level tooconnect tooyour database unless you need tooexecute administrator tasks like creating new users.</span></span> <span data-ttu-id="5a478-176">Zapoznaj się z tematem hello [samouczek usługi Azure Active Directory](./sql-database-aad-authentication-configure.md) na temat tooauthenticate przy użyciu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5a478-176">Please review hello [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how tooauthenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="5a478-177">Ochrona danych za pomocą szyfrowania</span><span class="sxs-lookup"><span data-stu-id="5a478-177">Protect your data with encryption</span></span>

<span data-ttu-id="5a478-178">Azure SQL Database przezroczystego szyfrowania danych (funkcji TDE) automatycznie szyfruje dane przechowywane, bez konieczności wprowadzania żadnych zmian toohello podczas uzyskiwania dostępu do hello zaszyfrowanych bazy danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5a478-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes toohello application accessing hello encrypted database.</span></span> <span data-ttu-id="5a478-179">W przypadku nowo utworzonego baz danych funkcji TDE jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="5a478-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="5a478-180">tooenable funkcji TDE dla bazy danych lub tooverify, który funkcji TDE jest włączone, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5a478-180">tooenable TDE for your database or tooverify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="5a478-181">Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="5a478-181">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="5a478-182">Polecenie **przezroczystego szyfrowania danych** strony konfiguracji hello tooopen dla funkcji TDE.</span><span class="sxs-lookup"><span data-stu-id="5a478-182">Click on **Transparent data encryption** tooopen hello configuration page for TDE.</span></span>

    ![Przezroczyste szyfrowanie danych](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="5a478-184">W razie potrzeby ustaw **szyfrowanie danych** tooON i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5a478-184">If necessary, set **Data encryption** tooON and click **Save**.</span></span>

<span data-ttu-id="5a478-185">proces szyfrowania Hello jest uruchamiany w tle hello.</span><span class="sxs-lookup"><span data-stu-id="5a478-185">hello encryption process starts in hello background.</span></span> <span data-ttu-id="5a478-186">Możesz monitorować postęp hello przy użyciu połączenia bazy danych tooSQL [programu SQL Server Management Studio](./sql-database-connect-query-ssms.md) badając kolumny encryption_state hello hello `sys.dm_database_encryption_keys` widoku.</span><span class="sxs-lookup"><span data-stu-id="5a478-186">You can monitor hello progress by connecting tooSQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying hello encryption_state column of hello `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="5a478-187">Włączanie inspekcji bazy danych SQL, w razie potrzeby</span><span class="sxs-lookup"><span data-stu-id="5a478-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="5a478-188">Usługa Azure SQL Database Auditing śledzi zdarzenia bazy danych i zapisuje je tooan dziennik inspekcji na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="5a478-188">Azure SQL Database Auditing tracks database events and writes them tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="5a478-189">Inspekcja pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą wskazywać potencjalne naruszenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5a478-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="5a478-190">Wykonaj te kroki toocreate domyślne zasady inspekcji bazy danych SQL:</span><span class="sxs-lookup"><span data-stu-id="5a478-190">Follow these steps toocreate a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="5a478-191">Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="5a478-191">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="5a478-192">W bloku ustawienia hello, wybierz **Inspekcja i wykrywanie zagrożeń**.</span><span class="sxs-lookup"><span data-stu-id="5a478-192">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="5a478-193">Powiadomienie, że inspekcję na poziomie serwera jest diabled i że istnieje **wyświetlić ustawienia serwera** łącze pozwala tooview lub zmodyfikować ustawienia inspekcji serwera hello w tym kontekście.</span><span class="sxs-lookup"><span data-stu-id="5a478-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you tooview or modify hello server auditing settings from this context.</span></span>

    ![Inspekcja bloku](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="5a478-195">Jeśli wolisz tooenable inspekcji typu (lub lokalizacji?) inne niż hello określona na poziomie serwera hello, Włącz **ON** inspekcji i wybierz polecenie hello **obiektu Blob** typu inspekcji.</span><span class="sxs-lookup"><span data-stu-id="5a478-195">If you prefer tooenable an Audit type (or location?) different from hello one specified at hello server level, turn **ON** Auditing, and choose hello **Blob** Auditing Type.</span></span> <span data-ttu-id="5a478-196">Po włączeniu inspekcji obiektu Blob serwera inspekcji bazy danych skonfigurowane hello będą istniały równolegle powitania serwera obiektu Blob inspekcji.</span><span class="sxs-lookup"><span data-stu-id="5a478-196">If server Blob auditing is enabled, hello database configured audit will exist side by side with hello server Blob audit.</span></span>

    ![Włączanie inspekcji](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="5a478-198">Wybierz **szczegóły magazynu** hello tooopen bloku magazynu dzienników inspekcji.</span><span class="sxs-lookup"><span data-stu-id="5a478-198">Select **Storage Details** tooopen hello Audit Logs Storage Blade.</span></span> <span data-ttu-id="5a478-199">Wybierz hello kontem magazynu platformy Azure, gdzie zostaną zapisane dzienniki i hello okres przechowywania, po którym hello będą usuwane stare dzienniki, następnie kliknij przycisk **OK** u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5a478-199">Select hello Azure storage account where logs will be saved, and hello retention period, after which hello old logs will be deleted, then click **OK** at hello bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="5a478-200">Użyj hello samo konto magazynu dla wszystkich hello tooget inspekcji bazy danych maksymalne wykorzystanie możliwości inspekcji hello raporty szablonów.</span><span class="sxs-lookup"><span data-stu-id="5a478-200">Use hello same storage account for all audited databases tooget hello most out of hello auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="5a478-201">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5a478-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a478-202">Jeśli chcesz toocustomize hello inspekcji zdarzeń, można to zrobić za pomocą programu PowerShell lub interfejsu API REST — Zobacz hello [automatyzacji (programu PowerShell / interfejsu API REST)](sql-database-auditing.md#subheading-7) sekcji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="5a478-202">If you want toocustomize hello audited events, you can do this via PowerShell or REST API - see hello [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="5a478-203">Włączyć wykrywanie zagrożeń bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="5a478-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="5a478-204">Wykrywanie zagrożeń udostępnia nową warstwę zabezpieczeń, co umożliwia klientom toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania, zapewniając alerty zabezpieczeń w nietypowych działań.</span><span class="sxs-lookup"><span data-stu-id="5a478-204">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="5a478-205">Użytkownicy mogą eksplorować hello zdarzenia podejrzane przy użyciu toodetermine inspekcji bazy danych SQL, jeśli wynikiem próby tooaccess, naruszenia lub wykorzystania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="5a478-205">Users can explore hello suspicious events using SQL Database Auditing toodetermine if they result from an attempt tooaccess, breach or exploit data in hello database.</span></span> <span data-ttu-id="5a478-206">Wykrywanie zagrożeń umożliwia proste tooaddress potencjalne zagrożenia toohello bazy danych bez toobe potrzeby hello ekspert zabezpieczeń lub zarządzać zabezpieczeniami zaawansowanymi, monitorowanie systemów.</span><span class="sxs-lookup"><span data-stu-id="5a478-206">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="5a478-207">Na przykład wykrywanie zagrożeń wykrywa niektóre działania nietypowych bazy danych, które wskazują potencjalne prób iniekcji kodu SQL.</span><span class="sxs-lookup"><span data-stu-id="5a478-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="5a478-208">Iniekcja kodu SQL jest jednym z hello typowych problemów sieci Web aplikacji zabezpieczeń na powitania internetowe, aplikacje używane tooattack opartych na danych.</span><span class="sxs-lookup"><span data-stu-id="5a478-208">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="5a478-209">Osoby atakujące korzystać z aplikacji tooinject luk w zabezpieczeniach złośliwego instrukcji SQL do pola wejścia aplikacji, naruszenia i modyfikacji danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="5a478-209">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

1. <span data-ttu-id="5a478-210">Przejdź bloku konfiguracji toohello hello ma toomonitor bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="5a478-210">Navigate toohello configuration blade of hello SQL database you want toomonitor.</span></span> <span data-ttu-id="5a478-211">W bloku ustawienia hello, wybierz **Inspekcja i wykrywanie zagrożeń**.</span><span class="sxs-lookup"><span data-stu-id="5a478-211">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Okienko nawigacji](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="5a478-213">W hello **Inspekcja i wykrywanie zagrożeń** Włącz bloku konfiguracji **ON** inspekcji, które będzie wyświetlane ustawienia wykrywania zagrożeń hello.</span><span class="sxs-lookup"><span data-stu-id="5a478-213">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello threat detection settings.</span></span>

3. <span data-ttu-id="5a478-214">Włącz **ON** wykrywanie zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="5a478-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="5a478-215">Skonfiguruj listę hello wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowe działania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5a478-215">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="5a478-216">Kliknij przycisk **zapisać** w hello **Inspekcja i wykrywanie zagrożeń** toosave bloku hello nowych lub zaktualizowanych inspekcji i zagrożeń zasady wykrywania.</span><span class="sxs-lookup"><span data-stu-id="5a478-216">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection policy.</span></span>

    ![Okienko nawigacji](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="5a478-218">W przypadku wykrycia są nietypowe działania bazy danych, otrzymasz wiadomość e-mail z powiadomieniem po wykryciu nietypowe działania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5a478-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="5a478-219">e-mail Hello dostarcza informacji o zdarzeń zabezpieczeń podejrzane hello tym rodzaj hello hello nietypowych działań, nazwa bazy danych, server name i hello czas trwania zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="5a478-219">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="5a478-220">Ponadto zawierają informacje dotyczące możliwe przyczyny i zalecane akcje tooinvestigate i ograniczyć hello potencjalne zagrożenie toohello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="5a478-220">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span> <span data-ttu-id="5a478-221">dalej przeszukiwania kroki Hello, przez jaki toodo użytkownik powinien otrzymywać wiadomości e-mail:</span><span class="sxs-lookup"><span data-stu-id="5a478-221">hello next steps walk you through what toodo should you receive such an email:</span></span>

    ![Wykrywanie zagrożeń w wiadomości e-mail](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="5a478-223">W wiadomości powitania kliknij hello **dziennik inspekcji SQL Azure** łącza, co spowoduje uruchomienie hello portalu Azure i wyświetlić odpowiednie rekordy hello wokół czasu hello hello podejrzane zdarzenia inspekcji.</span><span class="sxs-lookup"><span data-stu-id="5a478-223">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure portal and show hello relevant auditing records around hello time of hello suspicious event.</span></span>

    ![Rekordy inspekcji](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="5a478-225">Polecenie tooview rekordów inspekcji hello więcej szczegółów na powitania bazy danych podejrzane działania, takie jak instrukcji SQL, Niepowodzenie IP Przyczyna i klienta.</span><span class="sxs-lookup"><span data-stu-id="5a478-225">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Szczegóły rekordu](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="5a478-227">W bloku rekordów inspekcji powitania kliknij **Otwórz w programie Excel** tooopen wstępnie skonfigurowane w programie excel tooimport szablonu i wykonywania dokładniejszej analizy dziennika inspekcji hello wokół czasu hello hello podejrzane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="5a478-227">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5a478-228">W programu Excel 2010 lub nowszej, dodatku Power Query i hello **szybkie łączenie** ustawienie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="5a478-228">In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required.</span></span>

    ![Otwarte rekordy w programie Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="5a478-230">Witaj tooconfigure **szybkie łączenie** ustawienie - hello **dodatku POWER QUERY** karty wstążki, wybierz opcję **opcje** toodisplay hello opcje w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="5a478-230">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="5a478-231">Zaznacz hello sekcji prywatności i wybierz opcję drugi hello — "Ignoruj hello poziomów prywatności i potencjalne poprawianie wydajności":</span><span class="sxs-lookup"><span data-stu-id="5a478-231">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>

    ![Łączenie programu Excel fast](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="5a478-233">tooload dzienników inspekcji SQL, upewnij się, że parametry hello na karcie Ustawienia hello są poprawnie ustawione i wybierz wstążki "Dane" hello i kliknij przycisk "Odśwież wszystko" hello.</span><span class="sxs-lookup"><span data-stu-id="5a478-233">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>

    ![Parametry programu Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="5a478-235">Witaj wyniki są wyświetlane na powitania **dzienników inspekcji SQL** arkusza, co pozwala toorun dokładniejszej analizy hello nietypowych działań, które zostały wykryte i ograniczyć wpływ hello hello zdarzeń zabezpieczeń w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5a478-235">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5a478-236">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5a478-236">Next steps</span></span>
<span data-ttu-id="5a478-237">Można zwiększyć hello ochrony bazy danych przed złośliwymi użytkownikami lub nieautoryzowanego dostępu, wystarczy kilka prostych kroków.</span><span class="sxs-lookup"><span data-stu-id="5a478-237">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="5a478-238">W tym samouczku dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="5a478-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5a478-239">Konfigurowanie reguł zapory serwera i lub bazy danych</span><span class="sxs-lookup"><span data-stu-id="5a478-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="5a478-240">Połącz tooyour bazy danych przy użyciu ciągu bezpiecznego połączenia</span><span class="sxs-lookup"><span data-stu-id="5a478-240">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="5a478-241">Zarządzanie dostępem użytkowników</span><span class="sxs-lookup"><span data-stu-id="5a478-241">Manage user access</span></span>
> * <span data-ttu-id="5a478-242">Ochrona danych za pomocą szyfrowania</span><span class="sxs-lookup"><span data-stu-id="5a478-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="5a478-243">Włączanie inspekcji bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="5a478-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="5a478-244">Włączyć wykrywanie zagrożeń bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="5a478-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="5a478-245">Podnoszenie wydajności usługi SQL Database</span><span class="sxs-lookup"><span data-stu-id="5a478-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

