---
title: "aaaConfigure zabezpieczeń bazy danych SQL Azure dla odzyskiwania po awarii | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano zagadnienia dotyczące zabezpieczeń dotyczące konfigurowania i zarządzania zabezpieczeniami po Przywracanie bazy danych lub serwera pomocniczego tooa trybu failover w przypadku hello awarii centrum danych lub innych po awarii"
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="be9b1-103">Konfigurowanie i zarządzanie nimi zabezpieczenia bazy danych SQL Azure geograficzne lub trybu failover</span><span class="sxs-lookup"><span data-stu-id="be9b1-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="be9b1-104">[Aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) jest teraz dostępna dla wszystkich baz danych w warstwach wszystkich usług.</span><span class="sxs-lookup"><span data-stu-id="be9b1-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="be9b1-105">Przegląd wymagań uwierzytelniania dla odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="be9b1-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="be9b1-106">W tym temacie opisano hello uwierzytelniania wymogi tooconfigure i kontroli [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) i hello kroki wymagane tooset użytkownika dostępu toohello pomocniczej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="be9b1-106">This topic describes hello authentication requirements tooconfigure and control [active geo-replication](sql-database-geo-replication-overview.md) and hello steps required tooset up user access toohello secondary database.</span></span> <span data-ttu-id="be9b1-107">Opisano również sposób włączenia odzyskanej bazy danych programu access toohello po użyciu [geograficzne](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="be9b1-107">It also describes how enable access toohello recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="be9b1-108">Aby uzyskać więcej informacji na temat opcji odzyskiwania, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="be9b1-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="be9b1-109">Odzyskiwanie po awarii z zawartych użytkowników</span><span class="sxs-lookup"><span data-stu-id="be9b1-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="be9b1-110">W przeciwieństwie do tradycyjnych użytkowników, które muszą być mapowane toologins w bazie danych master hello, zawartego użytkownika zarządza całkowicie hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="be9b1-110">Unlike traditional users, which must be mapped toologins in hello master database, a contained user is managed completely by hello database itself.</span></span> <span data-ttu-id="be9b1-111">Ma to dwie korzyści.</span><span class="sxs-lookup"><span data-stu-id="be9b1-111">This has two benefits.</span></span> <span data-ttu-id="be9b1-112">W przypadku odzyskiwania po awarii hello hello użytkownicy nadal tooconnect toohello nowe głównej bazy danych lub hello odzyskane przy użyciu przywracaniem geograficznym bez przeprowadzania dodatkowej konfiguracji, ponieważ użytkownicy hello zarządza hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="be9b1-112">In hello disaster recovery scenario, hello users can continue tooconnect toohello new primary database or hello database recovered using geo-restore without any additional configuration, because hello database manages hello users.</span></span> <span data-ttu-id="be9b1-113">Istnieją również potencjalne skalowalności i wydajności korzysta z tej konfiguracji z punktu widzenia logowania.</span><span class="sxs-lookup"><span data-stu-id="be9b1-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="be9b1-114">Aby uzyskać więcej informacji, zobacz artykuł [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx) (Użytkownicy zawartej bazy danych — tworzenie przenośnej bazy danych).</span><span class="sxs-lookup"><span data-stu-id="be9b1-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="be9b1-115">optymalne rozwiązania w zakresie głównym Hello jest zarządzanie hello proces odzyskiwania po awarii na dużą skalę trudniejsza.</span><span class="sxs-lookup"><span data-stu-id="be9b1-115">hello main trade-off is that managing hello disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="be9b1-116">Jeśli masz wiele baz danych tego powitalne Użyj zawartych w tej samej logowania, obsługa przy użyciu poświadczeń hello użytkowników w wielu baz danych może odwrócić hello zalet zawartych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="be9b1-116">When you have multiple databases that use hello same login, maintaining hello credentials using contained users in multiple databases may negate hello benefits of contained users.</span></span> <span data-ttu-id="be9b1-117">Na przykład hello obrotu zasady haseł wymagają że można wprowadzać zmian stale w wielu baz danych, zamiast zmiany hasła hello logowania hello raz w bazie danych master hello.</span><span class="sxs-lookup"><span data-stu-id="be9b1-117">For example, hello password rotation policy requires that changes be made consistently in multiple databases rather than changing hello password for hello login once in hello master database.</span></span> <span data-ttu-id="be9b1-118">Z tego powodu, jeśli masz wiele baz danych tego hello Użyj tej samej nazwy użytkownika i hasła, używanie zawartych użytkowników nie jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="be9b1-118">For this reason, if you have multiple databases that use hello same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-tooconfigure-logins-and-users"></a><span data-ttu-id="be9b1-119">Jak tooconfigure logowania i użytkowników</span><span class="sxs-lookup"><span data-stu-id="be9b1-119">How tooconfigure logins and users</span></span>
<span data-ttu-id="be9b1-120">Jeśli używasz logowania i użytkowników (zamiast zawartych użytkowników), należy wykonać dodatkowe kroki tooinsure hello, że istnieje w tej samej nazwy logowania w bazie danych master hello.</span><span class="sxs-lookup"><span data-stu-id="be9b1-120">If you are using logins and users (rather than contained users), you must take extra steps tooinsure that hello same logins exist in hello master database.</span></span> <span data-ttu-id="be9b1-121">Witaj poniższych sekcjach podano hello zagadnienia związane i dodatkowe kroki.</span><span class="sxs-lookup"><span data-stu-id="be9b1-121">hello following sections outline hello steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a><span data-ttu-id="be9b1-122">Konfigurowanie dostępu tooa dodatkowej lub odzyskanej bazy danych użytkowników</span><span class="sxs-lookup"><span data-stu-id="be9b1-122">Set up user access tooa secondary or recovered database</span></span>
<span data-ttu-id="be9b1-123">Aby hello dodatkowej bazy danych toobe można używać tylko do odczytu dodatkowej i baza danych tooensure właściwy dostęp toohello nowe głównej bazy danych lub hello odzyskane przy użyciu przywracaniem geograficznym hello wzorca bazy danych serwera obiektów docelowych hello musi mieć hello Konfiguracja zabezpieczeń odpowiednich na miejscu przed hello odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="be9b1-123">In order for hello secondary database toobe usable as a read-only secondary database, and tooensure proper access toohello new primary database or hello database recovered using geo-restore, hello master database of hello target server must have hello appropriate security configuration in place before hello recovery.</span></span>

<span data-ttu-id="be9b1-124">Witaj określonych uprawnień dla każdego kroku są opisane w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="be9b1-124">hello specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="be9b1-125">Przygotowywanie tooa dostępu użytkownika pomocniczy — replikacja geograficzna należy wykonać w ramach konfigurowania — replikacja geograficzna.</span><span class="sxs-lookup"><span data-stu-id="be9b1-125">Preparing user access tooa geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="be9b1-126">Przygotowywanie bazy danych toohello przywrócone z magazynu geograficznie dostępu użytkowników, należy wykonać w dowolnej chwili, gdy hello oryginalny serwer jest w trybie online (np. w ramach hello DR Przechodzenie do szczegółów).</span><span class="sxs-lookup"><span data-stu-id="be9b1-126">Preparing user access toohello geo-restored databases should be performed at any time when hello original server is online (e.g. as part of hello DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="be9b1-127">Jeśli nie zostanie over lub geograficzne serwer tooa, który nie ma poprawnego skonfigurowania logowania tooit dostępu będzie kontem administratora serwera toohello ograniczone.</span><span class="sxs-lookup"><span data-stu-id="be9b1-127">If you fail over or geo-restore tooa server that does not have properly configured logins, access tooit will be limited toohello server admin account.</span></span>
> 
> 

<span data-ttu-id="be9b1-128">Konfigurowanie logowania na serwerze docelowym hello obejmuje trzy kroki przedstawione poniżej:</span><span class="sxs-lookup"><span data-stu-id="be9b1-128">Setting up logins on hello target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a><span data-ttu-id="be9b1-129">1. Określ nazwy logowania z podstawowej bazy danych programu access toohello:</span><span class="sxs-lookup"><span data-stu-id="be9b1-129">1. Determine logins with access toohello primary database:</span></span>
<span data-ttu-id="be9b1-130">pierwszym krokiem procesu hello Hello jest toodetermine logowania, które musi zostać skopiowane na serwer docelowy hello.</span><span class="sxs-lookup"><span data-stu-id="be9b1-130">hello first step of hello process is toodetermine which logins must be duplicated on hello target server.</span></span> <span data-ttu-id="be9b1-131">Jest to realizowane przy użyciu pary instrukcji "SELECT", co w hello logicznej głównej bazy danych na serwerze źródłowym hello i w hello głównej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="be9b1-131">This is accomplished with a pair of SELECT statements, one in hello logical master database on hello source server and one in hello primary database itself.</span></span>

<span data-ttu-id="be9b1-132">Witaj tylko administrator serwera lub członek hello **LoginManager** roli serwera można określić hello logowania na serwerze źródłowym hello, powitania po instrukcji SELECT.</span><span class="sxs-lookup"><span data-stu-id="be9b1-132">Only hello server admin or a member of hello **LoginManager** server role can determine hello logins on hello source server with hello following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="be9b1-133">Tylko członek roli bazy danych db_owner hello, hello użytkownika dbo lub administratorem serwera, można określić wszystkich podmiotów użytkownika bazy danych hello w hello podstawowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="be9b1-133">Only a member of hello db_owner database role, hello dbo user, or server admin, can determine all of hello database user principals in hello primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a><span data-ttu-id="be9b1-134">2. Znajdź hello identyfikatora SID dla logowania hello w kroku 1:</span><span class="sxs-lookup"><span data-stu-id="be9b1-134">2. Find hello SID for hello logins identified in step 1:</span></span>
<span data-ttu-id="be9b1-135">Na podstawie porównania ilości danych wyjściowych hello hello zapytań z poprzedniej sekcji hello i hello pasujące identyfikatory SID, możesz mapować powitania serwera logowania toodatabase użytkownika.</span><span class="sxs-lookup"><span data-stu-id="be9b1-135">By comparing hello output of hello queries from hello previous section and matching hello SIDs, you can map hello server login toodatabase user.</span></span> <span data-ttu-id="be9b1-136">Nazwy logowania, w których użytkownik bazy danych ze zgodnym identyfikatorem SID ma toothat dostępu użytkownika do bazy danych jako główny użytkownik bazy danych.</span><span class="sxs-lookup"><span data-stu-id="be9b1-136">Logins that have a database user with a matching SID have user access toothat database as that database user principal.</span></span> 

<span data-ttu-id="be9b1-137">Witaj następujące zapytanie może być używane toosee wszystkich podmiotów zabezpieczeń użytkownika hello i ich identyfikatorów SID w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="be9b1-137">hello following query can be used toosee all of hello user principals and their SIDs in a database.</span></span> <span data-ttu-id="be9b1-138">Tylko członek hello db_owner bazy danych roli lub serwera administracyjnego można uruchomić tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="be9b1-138">Only a member of hello db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="be9b1-139">Witaj **INFORMATION_SCHEMA** i **sys** użytkownicy mają *NULL* identyfikatorów SID i hello **gościa** identyfikator SID jest **0x00**.</span><span class="sxs-lookup"><span data-stu-id="be9b1-139">hello **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and hello **guest** SID is **0x00**.</span></span> <span data-ttu-id="be9b1-140">Witaj **dbo** identyfikator SID może rozpoczynać się *0x01060000000001648000000000048454*, jeśli hello twórcy bazy danych serwera Witaj, Administratorze zamiast członkiem **dbmanager:**.</span><span class="sxs-lookup"><span data-stu-id="be9b1-140">hello **dbo** SID may start with *0x01060000000001648000000000048454*, if hello database creator was hello server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a><span data-ttu-id="be9b1-141">3. Tworzenie identyfikatorów logowania hello na serwerze docelowym hello:</span><span class="sxs-lookup"><span data-stu-id="be9b1-141">3. Create hello logins on hello target server:</span></span>
<span data-ttu-id="be9b1-142">Hello ostatnim krokiem jest serwer docelowy toohello toogo lub serwerów i generować hello logowania z hello odpowiednie identyfikatory SID.</span><span class="sxs-lookup"><span data-stu-id="be9b1-142">hello last step is toogo toohello target server, or servers, and generate hello logins with hello appropriate SIDs.</span></span> <span data-ttu-id="be9b1-143">Witaj podstawowa ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="be9b1-143">hello basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="be9b1-144">Jeśli chcesz toohello dostępu użytkownika toogrant dodatkowej, ale nie toohello podstawowe, możesz to zrobić, zmieniając hello dane logowania użytkownika na serwerze podstawowym hello przy użyciu składni hello.</span><span class="sxs-lookup"><span data-stu-id="be9b1-144">If you want toogrant user access toohello secondary, but not toohello primary, you can do that by altering hello user login on hello primary server by using hello following syntax.</span></span>
> 
> <span data-ttu-id="be9b1-145">ALTER LOGIN <login name> WYŁĄCZ</span><span class="sxs-lookup"><span data-stu-id="be9b1-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="be9b1-146">Wyłącz nie powoduje zmiany hasła hello, włączyć go zawsze, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="be9b1-146">DISABLE doesn’t change hello password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="be9b1-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be9b1-147">Next steps</span></span>
* <span data-ttu-id="be9b1-148">Aby uzyskać więcej informacji na temat zarządzania dostęp do bazy danych i logowania do, zobacz [zabezpieczeń bazy danych SQL: Zarządzanie zabezpieczeniami dostępu i nazwy logowania bazy danych](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="be9b1-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="be9b1-149">Aby uzyskać więcej informacji dotyczących użytkowników zawartej bazy danych, zobacz [zawarte bazy danych użytkowników — co Twojej bazy danych przenośne](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="be9b1-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="be9b1-150">Aby uzyskać informacje o użyciu i skonfigurowaniu aktywna replikacja geograficzna, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="be9b1-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="be9b1-151">Informacje o korzystaniu z przywracaniem geograficznym, zobacz [geograficzne](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="be9b1-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

