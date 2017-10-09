---
title: tooRestore aaaHow serwera w bazie danych Azure dla programu MySQL | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób toorestore serwera w bazie danych Azure poświęcone MySQL hello portalu Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a><span data-ttu-id="44d4c-103">Jak tooBackup i przywracania serwera w bazie danych Azure poświęcone MySQL hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="44d4c-103">How tooBackup and Restore a server in Azure Database for MySQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="44d4c-104">Kopia zapasowa jest wykonywana automatycznie</span><span class="sxs-lookup"><span data-stu-id="44d4c-104">Backup happens Automatically</span></span>
<span data-ttu-id="44d4c-105">Korzystając z bazy danych platformy Azure dla programu MySQL, hello bazy danych usługi automatycznie tworzy kopię zapasową usługi hello co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="44d4c-105">When using Azure Database for MySQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="44d4c-106">kopie zapasowe Hello są dostępne przez 7 dni, korzystając z warstwy podstawowej i 35 dni po użyciu warstwy standardowa.</span><span class="sxs-lookup"><span data-stu-id="44d4c-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="44d4c-107">Aby uzyskać więcej informacji, zobacz [bazą danych Azure dla warstwy usługi MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="44d4c-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="44d4c-108">Tej funkcji automatycznego tworzenia kopii zapasowej można przywrócić powitania serwera i wszystkich jego baz danych do nowego serwera tooan wcześniej punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="44d4c-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="44d4c-109">Przywracanie w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="44d4c-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="44d4c-110">Bazy danych platformy Azure dla programu MySQL pozwala toorestore powitania serwera zapasowego tooa punktu w czasie, do nowej kopii tooa powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="44d4c-110">Azure Database for MySQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="44d4c-111">Ten nowy toorecover serwera można użyć danych.</span><span class="sxs-lookup"><span data-stu-id="44d4c-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="44d4c-112">Na przykład jeśli tabela została przypadkowo porzucony w południe dzisiaj, można przywrócenie czasu toohello tuż przed południe i pobrać hello Brak tabeli i danych z tej nowej kopii powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="44d4c-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="44d4c-113">Witaj następujące kroki hello przykładowy serwer tooa punkt przywracania w czasie:</span><span class="sxs-lookup"><span data-stu-id="44d4c-113">hello following steps restore hello sample server tooa point in time:</span></span>

1. <span data-ttu-id="44d4c-114">Zaloguj się na powitania [portalu Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="44d4c-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="44d4c-115">Zlokalizuj bazy danych Azure, aby serwer MySQL.</span><span class="sxs-lookup"><span data-stu-id="44d4c-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="44d4c-116">Wybierz w okienku po lewej stronie powitania **wszystkie zasoby**, następnie wybierz serwer z listy hello.</span><span class="sxs-lookup"><span data-stu-id="44d4c-116">In hello left pane, select **All resources**, then select your server from hello list.</span></span>

3.  <span data-ttu-id="44d4c-117">U góry hello powitania serwera omówienie bloku, kliknij przycisk **przywrócić** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="44d4c-117">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="44d4c-118">zostanie otwarty blok przywracania Hello.</span><span class="sxs-lookup"><span data-stu-id="44d4c-118">hello Restore blade opens.</span></span>
<span data-ttu-id="44d4c-119">![Kliknij przycisk przywracania](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="44d4c-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="44d4c-120">Wypełnij formularz przywracania hello hello wymagane informacje:</span><span class="sxs-lookup"><span data-stu-id="44d4c-120">Fill out hello Restore form with hello required information:</span></span>

- <span data-ttu-id="44d4c-121">**(UTC) punkt przywracania**: za pomocą selektora czasu i hello wyboru daty, wybierz toorestore punktu w czasie, aby.</span><span class="sxs-lookup"><span data-stu-id="44d4c-121">**Restore point (UTC)**: Using hello Date picker and time picker, select a point-in-time toorestore to.</span></span> <span data-ttu-id="44d4c-122">określona godzina Hello jest w formacie UTC, warto prawdopodobnie tooconvert hello lokalnego czasu w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="44d4c-122">hello time specified is in UTC format, so you likely need tooconvert hello local time into UTC.</span></span>
- <span data-ttu-id="44d4c-123">**Przywracanie serwera toonew**: Podaj nazwę toorestore hello istniejącego serwera do nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="44d4c-123">**Restore toonew server**: Provide a new server name toorestore hello existing server into.</span></span>
- <span data-ttu-id="44d4c-124">**Lokalizacja**: wybór obszaru hello automatycznie wypełnia hello źródłowego serwera regionu i nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="44d4c-124">**Location**: hello region choice automatically populates with hello source server region, and cannot be changed.</span></span>
- <span data-ttu-id="44d4c-125">**Warstwa cenowa**: hello cennik wybór warstwy automatycznie wypełnia hello takie same ceny warstwy jako powitania serwera źródłowego i nie można ich tutaj zmienić.</span><span class="sxs-lookup"><span data-stu-id="44d4c-125">**Pricing tier**: hello pricing tier choice automatically populates with hello same pricing tier as hello source server, and cannot be changed here.</span></span> 
<span data-ttu-id="44d4c-126">![Przywracanie PITR](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="44d4c-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="44d4c-127">Kliknij przycisk **OK** toorestore powitania serwera toorestore tooa punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="44d4c-127">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="44d4c-128">Po zakończeniu przywracania hello zlokalizować hello nowy serwer, który został utworzony powitalne tooverify baz danych zostały przywrócone zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="44d4c-128">After hello restore finishes, locate hello new server that was created tooverify hello databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44d4c-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="44d4c-129">Next steps</span></span>
- [<span data-ttu-id="44d4c-130">Biblioteki połączeń dla bazy danych Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="44d4c-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)