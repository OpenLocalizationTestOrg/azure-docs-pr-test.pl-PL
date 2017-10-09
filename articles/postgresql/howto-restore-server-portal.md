---
title: Jak tooRestore serwera w bazie danych Azure PostgreSQL | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób toorestore serwera w bazie danych Azure poświęcone PostgreSQL hello portalu Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="dad4b-103">Jak tooBackup i przywracania serwera w bazie danych Azure poświęcone PostgreSQL hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="dad4b-103">How tooBackup and Restore a server in Azure Database for PostgreSQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="dad4b-104">Kopia zapasowa jest wykonywana automatycznie</span><span class="sxs-lookup"><span data-stu-id="dad4b-104">Backup happens Automatically</span></span>
<span data-ttu-id="dad4b-105">Korzystając z bazy danych Azure PostgreSQL, hello bazy danych usługi automatycznie tworzy kopię zapasową usługi hello co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="dad4b-105">When using Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="dad4b-106">kopie zapasowe Hello są dostępne przez 7 dni, korzystając z warstwy podstawowej i 35 dni po użyciu warstwy standardowa.</span><span class="sxs-lookup"><span data-stu-id="dad4b-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="dad4b-107">Aby uzyskać więcej informacji, zobacz [bazą danych Azure dla warstwy usług PostgreSQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="dad4b-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="dad4b-108">Tej funkcji automatycznego tworzenia kopii zapasowej można przywrócić powitania serwera i wszystkich jego baz danych do nowego serwera tooan wcześniej punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="dad4b-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="dad4b-109">Przywracanie w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="dad4b-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="dad4b-110">Bazy danych platformy Azure dla PostgreSQL pozwala toorestore powitania serwera zapasowego tooa punktu w czasie, do nowej kopii tooa powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="dad4b-110">Azure Database for PostgreSQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="dad4b-111">Ten nowy toorecover serwera można użyć danych.</span><span class="sxs-lookup"><span data-stu-id="dad4b-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="dad4b-112">Na przykład jeśli tabela została przypadkowo porzucony w południe dzisiaj, można przywrócenie czasu toohello tuż przed południe i pobrać hello Brak tabeli i danych z tej nowej kopii powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="dad4b-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="dad4b-113">Witaj następujące kroki hello przykładowy serwer tooa punkt przywracania w czasie:</span><span class="sxs-lookup"><span data-stu-id="dad4b-113">hello following steps restore hello sample server tooa point in time:</span></span>
1. <span data-ttu-id="dad4b-114">Zaloguj się na powitania [portalu Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="dad4b-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="dad4b-115">Zlokalizuj PostgreSQL serwera bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="dad4b-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="dad4b-116">W portalu Azure hello, kliknij przycisk **wszystkie zasoby** z menu po lewej stronie powitania i wpisz nazwę hello, takich jak **mypgserver 20170401**, toosearch dla istniejącego serwera.</span><span class="sxs-lookup"><span data-stu-id="dad4b-116">In hello Azure portal, click **All Resources** from hello left-hand menu and type in hello name, such as **mypgserver-20170401**, toosearch for your existing server.</span></span> <span data-ttu-id="dad4b-117">Kliknij nazwę serwera hello hello wynik wyszukiwania na liście.</span><span class="sxs-lookup"><span data-stu-id="dad4b-117">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="dad4b-118">Witaj **omówienie** strony dla serwera zostanie otwarty i udostępnia opcje dla dalszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dad4b-118">hello **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Portal Azure — wyszukiwanie toolocate serwera](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="dad4b-120">U góry hello powitania serwera omówienie bloku, kliknij przycisk **przywrócić** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="dad4b-120">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="dad4b-121">zostanie otwarty blok przywracania Hello.</span><span class="sxs-lookup"><span data-stu-id="dad4b-121">hello Restore blade opens.</span></span>

   ![Bazy danych platformy Azure dla przycisku PostgreSQL — Przegląd — przywracania](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="dad4b-123">Wypełnij formularz przywracania hello hello wymagane informacje:</span><span class="sxs-lookup"><span data-stu-id="dad4b-123">Fill out hello Restore form with hello required information:</span></span>

   ![<span data-ttu-id="dad4b-124">Bazy danych platformy Azure dla PostgreSQL — informacji dotyczące przywracania</span><span class="sxs-lookup"><span data-stu-id="dad4b-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="dad4b-125">**Punkt przywracania**: Wybierz w momencie po hello serwer został zmieniony</span><span class="sxs-lookup"><span data-stu-id="dad4b-125">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="dad4b-126">**Serwer docelowy**: Podaj nową nazwę serwera ma toorestore do</span><span class="sxs-lookup"><span data-stu-id="dad4b-126">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="dad4b-127">**Lokalizacja**: nie można wybrać hello region, domyślnie jest taka sama jak powitania serwera źródłowego</span><span class="sxs-lookup"><span data-stu-id="dad4b-127">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="dad4b-128">**Warstwa cenowa**: nie można zmienić tę wartość podczas przywracania serwera.</span><span class="sxs-lookup"><span data-stu-id="dad4b-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="dad4b-129">Jest taki sam jak powitania serwera źródłowego.</span><span class="sxs-lookup"><span data-stu-id="dad4b-129">It is same as hello source server.</span></span> 

5. <span data-ttu-id="dad4b-130">Kliknij przycisk **OK** toorestore powitania serwera toorestore tooa punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="dad4b-130">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="dad4b-131">Po zakończeniu przywracania hello zlokalizować hello nowy serwer, który jest tworzony powitalne tooverify danych zostało przywrócone, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="dad4b-131">Once hello restore finishes, locate hello new server that is created tooverify hello data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dad4b-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dad4b-132">Next steps</span></span>
- [<span data-ttu-id="dad4b-133">Biblioteki połączeń dla bazy danych Azure dla PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="dad4b-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
