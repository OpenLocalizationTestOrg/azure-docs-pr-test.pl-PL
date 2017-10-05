---
title: Przywracanie serwera w bazie danych systemu Azure dla programu MySQL | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób przywracania serwera w bazie danych Azure dla programu MySQL przy użyciu portalu Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a><span data-ttu-id="12acc-103">Jak wykonywanie kopii zapasowych i przywracania serwera w bazie danych Azure dla programu MySQL przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="12acc-103">How To Backup and Restore a server in Azure Database for MySQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="12acc-104">Kopia zapasowa jest wykonywana automatycznie</span><span class="sxs-lookup"><span data-stu-id="12acc-104">Backup happens Automatically</span></span>
<span data-ttu-id="12acc-105">Korzystając z bazy danych platformy Azure dla programu MySQL, usługa bazy danych automatycznie sprawia, że usługa Kopia zapasowa co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="12acc-105">When using Azure Database for MySQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="12acc-106">Kopie zapasowe są dostępne przez 7 dni, korzystając z warstwy podstawowej i 35 dni po użyciu warstwy standardowa.</span><span class="sxs-lookup"><span data-stu-id="12acc-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="12acc-107">Aby uzyskać więcej informacji, zobacz [bazą danych Azure dla warstwy usługi MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="12acc-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="12acc-108">Tej funkcji automatycznego tworzenia kopii zapasowej można przywrócić serwer i wszystkie jej baz danych do nowego serwera do wcześniejszego punktu w stanu.</span><span class="sxs-lookup"><span data-stu-id="12acc-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="12acc-109">Przywracanie w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="12acc-109">Restore in the Azure portal</span></span>
<span data-ttu-id="12acc-110">Bazy danych platformy Azure dla programu MySQL służy do przywrócenia serwera do punktu w czasie, a do z uprawnieniami do nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="12acc-110">Azure Database for MySQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="12acc-111">Aby odzyskać dane, można użyć tego nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="12acc-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="12acc-112">Na przykład jeśli przypadkowo tabeli w południe dzisiaj, można przywrócenie na czas bezpośrednio przed południe i pobieranie Brak tabeli i danych z tej kopii nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="12acc-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="12acc-113">Poniższe kroki przywrócenie serwera próbki do punktu w czasie:</span><span class="sxs-lookup"><span data-stu-id="12acc-113">The following steps restore the sample server to a point in time:</span></span>

1. <span data-ttu-id="12acc-114">Zaloguj się do [portalu Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="12acc-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="12acc-115">Zlokalizuj bazy danych Azure, aby serwer MySQL.</span><span class="sxs-lookup"><span data-stu-id="12acc-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="12acc-116">W okienku po lewej stronie wybierz **wszystkie zasoby**, następnie wybierz serwer z listy.</span><span class="sxs-lookup"><span data-stu-id="12acc-116">In the left pane, select **All resources**, then select your server from the list.</span></span>

3.  <span data-ttu-id="12acc-117">W górnej części bloku Omówienie serwera, kliknij przycisk **przywrócić** na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="12acc-117">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="12acc-118">Zostanie otwarty blok przywracania.</span><span class="sxs-lookup"><span data-stu-id="12acc-118">The Restore blade opens.</span></span>
<span data-ttu-id="12acc-119">![Kliknij przycisk przywracania](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="12acc-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="12acc-120">Wypełnij formularz przywracania wymagane informacje:</span><span class="sxs-lookup"><span data-stu-id="12acc-120">Fill out the Restore form with the required information:</span></span>

- <span data-ttu-id="12acc-121">**(UTC) punkt przywracania**: za pomocą selektora daty i czasu selektora, wybierz w momencie przywrócić.</span><span class="sxs-lookup"><span data-stu-id="12acc-121">**Restore point (UTC)**: Using the Date picker and time picker, select a point-in-time to restore to.</span></span> <span data-ttu-id="12acc-122">Określona godzina jest w formacie UTC, więc prawdopodobnie trzeba przekonwertować czasu lokalnego w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="12acc-122">The time specified is in UTC format, so you likely need to convert the local time into UTC.</span></span>
- <span data-ttu-id="12acc-123">**Przywracanie do nowego serwera**: Podaj nową nazwę serwera do istniejącego serwera do przywrócenia.</span><span class="sxs-lookup"><span data-stu-id="12acc-123">**Restore to new server**: Provide a new server name to restore the existing server into.</span></span>
- <span data-ttu-id="12acc-124">**Lokalizacja**: wybór obszaru automatycznie wypełnia obszaru serwera źródłowego i nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="12acc-124">**Location**: The region choice automatically populates with the source server region, and cannot be changed.</span></span>
- <span data-ttu-id="12acc-125">**Warstwa cenowa**: wybór warstwy cenowej automatycznie wypełnia tej samej warstwie cenowej co serwer źródłowy i nie można ich tutaj zmienić.</span><span class="sxs-lookup"><span data-stu-id="12acc-125">**Pricing tier**: The pricing tier choice automatically populates with the same pricing tier as the source server, and cannot be changed here.</span></span> 
<span data-ttu-id="12acc-126">![Przywracanie PITR](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="12acc-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="12acc-127">Kliknij przycisk **OK** do przywrócenia serwera, aby wykonać przywracanie do punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="12acc-127">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="12acc-128">Po zakończeniu przywracania, zlokalizuj nowy serwer, który został utworzony w celu sprawdzenia, czy zostały przywrócone baz danych, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="12acc-128">After the restore finishes, locate the new server that was created to verify the databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12acc-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="12acc-129">Next steps</span></span>
- [<span data-ttu-id="12acc-130">Biblioteki połączeń dla bazy danych Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="12acc-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)