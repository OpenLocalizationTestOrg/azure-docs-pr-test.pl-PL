---
title: Przywracanie serwera w bazie danych systemu Azure dla PostgreSQL | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób przywracania serwera w bazie danych Azure dla PostgreSQL przy użyciu portalu Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: 3fbdb7741481bd3620466c3489d3609f9ea6961f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="caff8-103">Sposób wykonywania kopii zapasowej i przywracania serwera w bazie danych Azure dla PostgreSQL przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="caff8-103">How To Backup and Restore a server in Azure Database for PostgreSQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="caff8-104">Kopia zapasowa jest wykonywana automatycznie</span><span class="sxs-lookup"><span data-stu-id="caff8-104">Backup happens Automatically</span></span>
<span data-ttu-id="caff8-105">W przypadku używania bazy danych platformy Azure dla PostgreSQL, usługa bazy danych automatycznie tworzy kopię zapasową usługi co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="caff8-105">When using Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="caff8-106">Kopie zapasowe są dostępne przez 7 dni, korzystając z warstwy podstawowej i 35 dni po użyciu warstwy standardowa.</span><span class="sxs-lookup"><span data-stu-id="caff8-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="caff8-107">Aby uzyskać więcej informacji, zobacz [bazą danych Azure dla warstwy usług PostgreSQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="caff8-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="caff8-108">Tej funkcji automatycznego tworzenia kopii zapasowej można przywrócić serwer i wszystkie jej baz danych do nowego serwera do wcześniejszego punktu w stanu.</span><span class="sxs-lookup"><span data-stu-id="caff8-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="caff8-109">Przywracanie w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="caff8-109">Restore in the Azure portal</span></span>
<span data-ttu-id="caff8-110">Bazy danych platformy Azure dla PostgreSQL służy do przywrócenia serwera do punktu w czasie, a do z uprawnieniami do nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="caff8-110">Azure Database for PostgreSQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="caff8-111">Aby odzyskać dane, można użyć tego nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="caff8-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="caff8-112">Na przykład jeśli przypadkowo tabeli w południe dzisiaj, można przywrócenie na czas bezpośrednio przed południe i pobieranie Brak tabeli i danych z tej kopii nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="caff8-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="caff8-113">Poniższe kroki przywrócenie serwera próbki do punktu w czasie:</span><span class="sxs-lookup"><span data-stu-id="caff8-113">The following steps restore the sample server to a point in time:</span></span>
1. <span data-ttu-id="caff8-114">Zaloguj się do [portalu Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="caff8-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="caff8-115">Zlokalizuj PostgreSQL serwera bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="caff8-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="caff8-116">W portalu Azure kliknij **wszystkie zasoby** z menu po lewej stronie i wpisz nazwę, taką jak **mypgserver 20170401**, aby wyszukać istniejącego serwera.</span><span class="sxs-lookup"><span data-stu-id="caff8-116">In the Azure portal, click **All Resources** from the left-hand menu and type in the name, such as **mypgserver-20170401**, to search for your existing server.</span></span> <span data-ttu-id="caff8-117">Kliknij nazwę serwera wyświetlaną w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="caff8-117">Click the server name listed in the search result.</span></span> <span data-ttu-id="caff8-118">Zostanie otwarta strona **Przegląd**, która zawiera dalsze opcje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="caff8-118">The **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Portal Azure — Wyszukaj, aby zlokalizować serwera](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="caff8-120">W górnej części bloku Omówienie serwera, kliknij przycisk **przywrócić** na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="caff8-120">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="caff8-121">Zostanie otwarty blok przywracania.</span><span class="sxs-lookup"><span data-stu-id="caff8-121">The Restore blade opens.</span></span>

   ![Bazy danych platformy Azure dla przycisku PostgreSQL — Przegląd — przywracania](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="caff8-123">Wypełnij formularz przywracania wymagane informacje:</span><span class="sxs-lookup"><span data-stu-id="caff8-123">Fill out the Restore form with the required information:</span></span>

   ![<span data-ttu-id="caff8-124">Bazy danych platformy Azure dla PostgreSQL — informacji dotyczące przywracania</span><span class="sxs-lookup"><span data-stu-id="caff8-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="caff8-125">**Punkt przywracania**: Wybierz w momencie po serwer został zmieniony</span><span class="sxs-lookup"><span data-stu-id="caff8-125">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="caff8-126">**Serwer docelowy**: Podaj nową nazwę serwera mają zostać przywrócone</span><span class="sxs-lookup"><span data-stu-id="caff8-126">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="caff8-127">**Lokalizacja**: nie można wybrać region, domyślnie jest taki sam jak serwer źródłowy</span><span class="sxs-lookup"><span data-stu-id="caff8-127">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="caff8-128">**Warstwa cenowa**: nie można zmienić tę wartość podczas przywracania serwera.</span><span class="sxs-lookup"><span data-stu-id="caff8-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="caff8-129">Jest taki sam jak serwer źródłowy.</span><span class="sxs-lookup"><span data-stu-id="caff8-129">It is same as the source server.</span></span> 

5. <span data-ttu-id="caff8-130">Kliknij przycisk **OK** do przywrócenia serwera, aby wykonać przywracanie do punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="caff8-130">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="caff8-131">Po zakończeniu przywracania, zlokalizuj nowy serwer, który jest tworzony w celu sprawdzenia, czy dane została przywrócona, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="caff8-131">Once the restore finishes, locate the new server that is created to verify the data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="caff8-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="caff8-132">Next steps</span></span>
- [<span data-ttu-id="caff8-133">Biblioteki połączeń dla bazy danych Azure dla PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="caff8-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
