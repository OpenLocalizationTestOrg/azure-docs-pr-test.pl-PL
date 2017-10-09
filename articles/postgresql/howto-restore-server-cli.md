---
title: Jak tooback zapasowych i przywracania serwera w bazie danych Azure dla PostgreSQL | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooback zapasowej i przywracanie serwera w bazie danych Azure PostgreSQL przy użyciu hello wiersza polecenia platformy Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a><span data-ttu-id="2bac0-103">Jak tooback zapasowej i przywracanie serwera w bazie danych Azure PostgreSQL przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2bac0-103">How tooback up and restore a server in Azure Database for PostgreSQL by using hello Azure CLI</span></span>

<span data-ttu-id="2bac0-104">Użyj bazy danych platformy Azure dla toorestore PostgreSQL tooan bazy danych serwera wcześniejszą datę, która jest liczony od 7 dni too35.</span><span class="sxs-lookup"><span data-stu-id="2bac0-104">Use Azure Database for PostgreSQL toorestore a server database tooan earlier date that spans from 7 too35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bac0-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2bac0-105">Prerequisites</span></span>
<span data-ttu-id="2bac0-106">toocomplete to tooguide jak należy:</span><span class="sxs-lookup"><span data-stu-id="2bac0-106">toocomplete this how-tooguide, you need:</span></span>
- <span data-ttu-id="2bac0-107">[Bazy danych Azure PostgreSQL serwera i bazy danych](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2bac0-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="2bac0-108">Jeśli został zainstalowany, użyj hello Azure CLI lokalnie to tooguide jak wymaga użycia interfejsu wiersza polecenia Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="2bac0-108">If you install and use hello Azure CLI locally, this how-tooguide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2bac0-109">Wprowadź tooconfirm hello wersji, w wierszu polecenia interfejsu wiersza polecenia Azure hello `az --version`.</span><span class="sxs-lookup"><span data-stu-id="2bac0-109">tooconfirm hello version, at hello Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="2bac0-110">tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2bac0-110">tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="2bac0-111">Tworzenie kopii zapasowej odbywa się automatycznie</span><span class="sxs-lookup"><span data-stu-id="2bac0-111">Back up happens automatically</span></span>
<span data-ttu-id="2bac0-112">Gdy używasz bazy danych Azure PostgreSQL, hello bazy danych usługi automatycznie sprawia, że kopia zapasowa usługi hello co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="2bac0-112">When you use Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="2bac0-113">Dla warstwy Basic kopie zapasowe hello są dostępne przez 7 dni.</span><span class="sxs-lookup"><span data-stu-id="2bac0-113">For Basic Tier, hello backups are available for 7 days.</span></span> <span data-ttu-id="2bac0-114">Dla warstwy standardowa kopie zapasowe hello są dostępne dla 35 dni.</span><span class="sxs-lookup"><span data-stu-id="2bac0-114">For Standard Tier, hello backups are available for 35 days.</span></span> <span data-ttu-id="2bac0-115">Aby uzyskać więcej informacji, zobacz [bazą danych Azure dla PostgreSQL warstw cenowych](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="2bac0-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="2bac0-116">Z automatycznej funkcji Kopia zapasowa można przywrócić wcześniejszą datę powitania serwera i jego tooan baz danych lub punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="2bac0-116">With this automatic backup feature, you can restore hello server and its databases tooan earlier date, or point in time.</span></span>

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a><span data-ttu-id="2bac0-117">Przywracanie bazy danych tooa poprzedniego punktu w czasie przy użyciu interfejsu wiersza polecenia Azure hello</span><span class="sxs-lookup"><span data-stu-id="2bac0-117">Restore a database tooa previous point in time by using hello Azure CLI</span></span>
<span data-ttu-id="2bac0-118">Na użytek bazy danych Azure PostgreSQL toorestore powitania serwera tooa wcześniejszego punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="2bac0-118">Use Azure Database for PostgreSQL toorestore hello server tooa previous point in time.</span></span> <span data-ttu-id="2bac0-119">Hello przywrócić dane są kopiowane tooa nowy serwer, a hello istniejącego serwera pozostanie niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="2bac0-119">hello restored data is copied tooa new server, and hello existing server is left as is.</span></span> <span data-ttu-id="2bac0-120">Na przykład w tabeli jest przypadkowo usunięte w południe dzisiaj, można przywrócić czasu toohello tuż przed południe.</span><span class="sxs-lookup"><span data-stu-id="2bac0-120">For example, if a table is accidentally dropped at noon today, you can restore toohello time just before noon.</span></span> <span data-ttu-id="2bac0-121">Następnie można pobrać hello Brak tabeli i danych z hello przywrócić kopię powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="2bac0-121">Then, you can retrieve hello missing table and data from hello restored copy of hello server.</span></span> 

<span data-ttu-id="2bac0-122">toorestore powitania serwera, użyj hello Azure CLI [przywracania serwera postgres az](/cli/azure/postgres/server#restore) polecenia.</span><span class="sxs-lookup"><span data-stu-id="2bac0-122">toorestore hello server, use hello Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-hello-restore-command"></a><span data-ttu-id="2bac0-123">Uruchom polecenie restore hello</span><span class="sxs-lookup"><span data-stu-id="2bac0-123">Run hello restore command</span></span>

<span data-ttu-id="2bac0-124">toorestore powitania serwera, w wierszu polecenia interfejsu wiersza polecenia Azure hello, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2bac0-124">toorestore hello server, at hello Azure CLI command prompt, enter hello following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="2bac0-125">Witaj `az postgres server restore` polecenie wymaga hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="2bac0-125">hello `az postgres server restore` command requires hello following parameters:</span></span>
| <span data-ttu-id="2bac0-126">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="2bac0-126">Setting</span></span> | <span data-ttu-id="2bac0-127">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="2bac0-127">Suggested value</span></span> | <span data-ttu-id="2bac0-128">Opis</span><span class="sxs-lookup"><span data-stu-id="2bac0-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="2bac0-129">grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="2bac0-129">resource-group</span></span> |  <span data-ttu-id="2bac0-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2bac0-130">myResourceGroup</span></span> |  <span data-ttu-id="2bac0-131">Grupy zasobów, gdy istnieje powitania serwera źródłowego.</span><span class="sxs-lookup"><span data-stu-id="2bac0-131">The resource group where hello source server exists.</span></span>  |
| <span data-ttu-id="2bac0-132">name</span><span class="sxs-lookup"><span data-stu-id="2bac0-132">name</span></span> | <span data-ttu-id="2bac0-133">przywrócona mypgserver</span><span class="sxs-lookup"><span data-stu-id="2bac0-133">mypgserver-restored</span></span> | <span data-ttu-id="2bac0-134">Nazwa Hello hello nowy serwer, który jest tworzony przez polecenie restore hello.</span><span class="sxs-lookup"><span data-stu-id="2bac0-134">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="2bac0-135">Przywracanie punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="2bac0-135">restore-point-in-time</span></span> | <span data-ttu-id="2bac0-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="2bac0-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="2bac0-137">Wybieranie punktu w czasie toorestore do.</span><span class="sxs-lookup"><span data-stu-id="2bac0-137">Select a point in time toorestore to.</span></span> <span data-ttu-id="2bac0-138">Ta data i godzina musi należeć powitania serwera źródłowego kopii zapasowych okresu przechowywania.</span><span class="sxs-lookup"><span data-stu-id="2bac0-138">This date and time must be within hello source server's back up retention period.</span></span> <span data-ttu-id="2bac0-139">Użyj hello ISO8601 format daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="2bac0-139">Use hello ISO8601 date and time format.</span></span> <span data-ttu-id="2bac0-140">Na przykład można własnej lokalnej strefie czasowej, takich jak `2017-04-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="2bac0-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="2bac0-141">Można również użyć hello sformatować UTC Zulu, na przykład `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="2bac0-141">You can also use hello UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="2bac0-142">Serwer źródłowy</span><span class="sxs-lookup"><span data-stu-id="2bac0-142">source-server</span></span> | <span data-ttu-id="2bac0-143">mypgserver 20170401</span><span class="sxs-lookup"><span data-stu-id="2bac0-143">mypgserver-20170401</span></span> | <span data-ttu-id="2bac0-144">Witaj, nazwa lub identyfikator toorestore serwera źródłowego hello z.</span><span class="sxs-lookup"><span data-stu-id="2bac0-144">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="2bac0-145">Po przywróceniu tooan serwera wcześniejszego punktu w czasie, jest tworzony nowy serwer.</span><span class="sxs-lookup"><span data-stu-id="2bac0-145">When you restore a server tooan earlier point in time, a new server is created.</span></span> <span data-ttu-id="2bac0-146">Witaj oryginalnego określić serwer i jej baz danych z hello punktu w czasie są kopiowane toohello nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="2bac0-146">hello original server and its databases from hello specified point in time are copied toohello new server.</span></span>

<span data-ttu-id="2bac0-147">wartości warstwy Hello lokalizacji i cenach dla serwera hello przywrócić pozostają hello sam jako hello oryginalny serwer.</span><span class="sxs-lookup"><span data-stu-id="2bac0-147">hello location and pricing tier values for hello restored server remain hello same as hello original server.</span></span> 

<span data-ttu-id="2bac0-148">Witaj `az postgres server restore` polecenie jest synchroniczne.</span><span class="sxs-lookup"><span data-stu-id="2bac0-148">hello `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="2bac0-149">Po przywróceniu serwera hello umożliwia ponownie toorepeat hello proces dla różnych punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="2bac0-149">After hello server is restored, you can use it again toorepeat hello process for a different point in time.</span></span> 

<span data-ttu-id="2bac0-150">Po hello zakończenie procesu przywracania, Znajdź hello nowego serwera i sprawdź, czy dane hello są przywracane zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="2bac0-150">After hello restore process finishes, locate hello new server and verify that hello data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bac0-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2bac0-151">Next steps</span></span>
[<span data-ttu-id="2bac0-152">Biblioteki połączeń dla bazy danych Azure dla PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2bac0-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
