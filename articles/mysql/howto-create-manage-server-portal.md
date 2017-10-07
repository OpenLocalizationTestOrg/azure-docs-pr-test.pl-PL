---
title: "aaaCreate i zarządzanie bazą danych Azure dla serwera MySQL przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak szybko utworzyć nową bazę danych Azure MySQL serwera i zarządzanie serwerem hello za pomocą hello portalu Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="4afff-103">Tworzenie i zarządzanie Azure bazy danych dla serwera MySQL przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4afff-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="4afff-104">W tym artykule opisano, jak szybko utworzyć nową bazę danych Azure MySQL serwera i zarządzanie serwerem hello za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4afff-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage hello server using hello Azure Portal.</span></span> <span data-ttu-id="4afff-105">Zarządzanie serwerem obejmuje wyświetlanie szczegółów serwera & bazy danych, resetowanie hasła i usuwanie powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="4afff-105">Server management includes viewing server details & databases, resetting password and deleting hello server.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="4afff-106">Zaloguj się za toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4afff-106">Log in toohello Azure portal</span></span>
<span data-ttu-id="4afff-107">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4afff-107">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="4afff-108">Tworzenie serwera usługi Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="4afff-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="4afff-109">Wykonaj te kroki toocreate bazy danych Azure programu MySQL serwer o nazwie "mysqlserver4demo"</span><span class="sxs-lookup"><span data-stu-id="4afff-109">Follow these steps toocreate an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="4afff-110">Kliknij przycisk 1 **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4afff-110">1- Click **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

<span data-ttu-id="4afff-111">Wybierz opcję 2 **baz danych** z hello nowej strony, a następnie wybierz **bazy danych Azure dla programu MySQL** ze strony baz danych hello.</span><span class="sxs-lookup"><span data-stu-id="4afff-111">2- Select **Databases** from hello New page, and select **Azure Database for MySQL** from hello Databases page.</span></span>

> <span data-ttu-id="4afff-112">Baza danych Azure dla serwera MySQL jest tworzony z zdefiniowanego zestawu [obliczeniowej i pamięci masowej](./concepts-compute-unit-and-storage.md) zasobów.</span><span class="sxs-lookup"><span data-stu-id="4afff-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="4afff-113">Witaj baza danych została utworzona, w ramach grupy zasobów platformy Azure i w bazie danych Azure dla serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="4afff-113">hello database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![Utwórz nowy serwera](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="4afff-115">3 - wypełnić hello Azure bazy danych MySQL formularza z hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="4afff-115">3- Fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="4afff-116">**Pole formularza**</span><span class="sxs-lookup"><span data-stu-id="4afff-116">**Form Field**</span></span> | <span data-ttu-id="4afff-117">**Opis pola**</span><span class="sxs-lookup"><span data-stu-id="4afff-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="4afff-118">*Nazwa serwera*</span><span class="sxs-lookup"><span data-stu-id="4afff-118">*Server name*</span></span> | <span data-ttu-id="4afff-119">Azure mysql (nazwa serwera jest globalnie unikatowa)</span><span class="sxs-lookup"><span data-stu-id="4afff-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="4afff-120">*Subskrypcja*</span><span class="sxs-lookup"><span data-stu-id="4afff-120">*Subscription*</span></span> | <span data-ttu-id="4afff-121">MySQLaaS (wybierz z listy rozwijanej)</span><span class="sxs-lookup"><span data-stu-id="4afff-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="4afff-122">*Grupa zasobów*</span><span class="sxs-lookup"><span data-stu-id="4afff-122">*Resource group*</span></span> | <span data-ttu-id="4afff-123">myresource (Utwórz nową grupę zasobów lub użyć istniejącego)</span><span class="sxs-lookup"><span data-stu-id="4afff-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="4afff-124">*Identyfikator logowania administratora serwera*</span><span class="sxs-lookup"><span data-stu-id="4afff-124">*Server admin login*</span></span> | <span data-ttu-id="4afff-125">myadmin (skonfiguruj nazwę konta administratora)</span><span class="sxs-lookup"><span data-stu-id="4afff-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="4afff-126">*Hasło*</span><span class="sxs-lookup"><span data-stu-id="4afff-126">*Password*</span></span> | <span data-ttu-id="4afff-127">ustawienia hasła do konta administratora</span><span class="sxs-lookup"><span data-stu-id="4afff-127">setup admin account password</span></span> |
| <span data-ttu-id="4afff-128">*Potwierdź hasło*</span><span class="sxs-lookup"><span data-stu-id="4afff-128">*Confirm password*</span></span> | <span data-ttu-id="4afff-129">potwierdź hasło konta administratora</span><span class="sxs-lookup"><span data-stu-id="4afff-129">confirm admin account password</span></span> |
| <span data-ttu-id="4afff-130">*Lokalizacja*</span><span class="sxs-lookup"><span data-stu-id="4afff-130">*Location*</span></span> | <span data-ttu-id="4afff-131">Europa Północna (wybór między Europa Północna, Europa i zachodnie stany USA)</span><span class="sxs-lookup"><span data-stu-id="4afff-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="4afff-132">*Wersja*</span><span class="sxs-lookup"><span data-stu-id="4afff-132">*Version*</span></span> | <span data-ttu-id="4afff-133">5.6 (Wybierz bazy danych Azure w wersji server MySQL)</span><span class="sxs-lookup"><span data-stu-id="4afff-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="4afff-134">Kliknij przycisk 4 **warstwa cenowa** toospecify hello warstwę i poziom wydajności usługi dla nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="4afff-134">4- Click **Pricing tier** toospecify hello service tier and performance level for your new server.</span></span> <span data-ttu-id="4afff-135">Obliczenia bazy danych od 50 do 100 w warstwie podstawowa, 100 i 200 w warstwie standardowa, można skonfigurować jednostki i Magazyn można dodać zależności od uwzględniona ilość.</span><span class="sxs-lookup"><span data-stu-id="4afff-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="4afff-136">Ten przewodnik Porada umożliwia wybierz 50 Jednostka obliczeniowa i 50GB.</span><span class="sxs-lookup"><span data-stu-id="4afff-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="4afff-137">Kliknij przycisk **OK** toosave wybór.</span><span class="sxs-lookup"><span data-stu-id="4afff-137">Click **OK** toosave your selection.</span></span>
<span data-ttu-id="4afff-138">![Utwórz server--warstwy cenowej](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="4afff-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="4afff-139">Kliknij przycisk 5 **Utwórz** tooprovision powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="4afff-139">5- Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="4afff-140">Aprowizacja zajmuje kilka minut.</span><span class="sxs-lookup"><span data-stu-id="4afff-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="4afff-141">Sprawdź hello **toodashboard numeru Pin** opcji tooallow łatwe monitorowanie wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="4afff-141">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="4afff-142">Mimo że too1000GB w warstwie podstawowa i 10000GB w standardzie warstwy będą obsługiwane dla magazynu, dla publicznej wersji zapoznawczej, pamięci masowej hello jest tymczasowo too1000GB nadal ograniczone.</span><span class="sxs-lookup"><span data-stu-id="4afff-142">Although up too1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, hello maximum storage is still limited too1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="4afff-143">Aktualizacja bazy danych Azure dla serwera MySQL</span><span class="sxs-lookup"><span data-stu-id="4afff-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="4afff-144">Po udostępnieniu nowego serwera użytkownik ma 2 tooedit opcje istniejącego serwera: resetowanie hasła administratora lub skalowania w górę/dół powitania serwera, zmieniając hello obliczeń jednostki.</span><span class="sxs-lookup"><span data-stu-id="4afff-144">After new server is provisioned, user has 2 options tooedit an existing server: reset administrator password or scale up/down hello server by changing hello compute-units.</span></span>

### <a name="change-hello-administrator-user-password"></a><span data-ttu-id="4afff-145">Zmienianie hasła użytkownika administratora hello</span><span class="sxs-lookup"><span data-stu-id="4afff-145">Change hello administrator user password</span></span>
<span data-ttu-id="4afff-146">1 — na serwerze hello **omówienie** bloku, kliknij przycisk **resetowania hasła** toopopulate okna wprowadzania i potwierdzenie hasła.</span><span class="sxs-lookup"><span data-stu-id="4afff-146">1- On hello server **Overview** blade, click **Reset password** toopopulate a password input and confirmation window.</span></span>

<span data-ttu-id="4afff-147">2 — wprowadź nowe hasło i potwierdzenie hasła hello w oknie hello zgodnie z poniższymi instrukcjami: ![resetowania hasła](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="4afff-147">2- Enter new password and confirm hello password in hello window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="4afff-148">Kliknij 3 **OK** toosave hello nowe hasło.</span><span class="sxs-lookup"><span data-stu-id="4afff-148">3- Click **OK** toosave hello new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="4afff-149">Skalowanie w górę/dół zmieniając obliczeniowe jednostki</span><span class="sxs-lookup"><span data-stu-id="4afff-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="4afff-150">1 - na powitania serwera bloku w obszarze **ustawienia**, kliknij przycisk **warstwa cenowa** bloku warstwa cenowa tooopen hello, hello Azure bazy danych dla serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="4afff-150">1- On hello server blade, under **Settings**, click **Pricing tier** tooopen hello Pricing tier blade for hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="4afff-151">2-wykonaj krok 4 w **utworzenia bazy danych MySQL serwera Azure** toochange obliczeniowe jednostki w hello samą warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="4afff-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** toochange Compute Units in hello same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="4afff-152">Usuwanie bazy danych Azure dla serwera MySQL</span><span class="sxs-lookup"><span data-stu-id="4afff-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="4afff-153">1 - na powitania serwera **omówienie** bloku, kliknij przycisk **usunąć** polecenia przycisk tooopen hello usunięcie potwierdzenie bloku.</span><span class="sxs-lookup"><span data-stu-id="4afff-153">1- On hello server **Overview** blade, click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

<span data-ttu-id="4afff-154">Typ 2 hello poprawną nazwę serwera w polu wejściowym hello bloku o potwierdzenie dwa razy.</span><span class="sxs-lookup"><span data-stu-id="4afff-154">2- Type hello correct server name in input box of hello blade for double confirmation.</span></span>

<span data-ttu-id="4afff-155">Kliknij 3 **usunąć** ponownie przycisk usuwania akcji tooconfirm i poczekaj "Usuwanie sukces" popup na powitania pasek powiadomień.</span><span class="sxs-lookup"><span data-stu-id="4afff-155">3- Click **Delete** button again tooconfirm deleting action and wait for “Deleting success” popup on hello notification bar.</span></span>

## <a name="list-hello-azure-database-for-mysql-databases"></a><span data-ttu-id="4afff-156">Lista hello Azure bazy danych dla baz danych MySQL</span><span class="sxs-lookup"><span data-stu-id="4afff-156">List hello Azure Database for MySQL databases</span></span>
<span data-ttu-id="4afff-157">Na serwerze hello **omówienie** bloku, przewiń w dół, aż zostanie wyświetlony hello bazy danych kafelka na dole hello.</span><span class="sxs-lookup"><span data-stu-id="4afff-157">On hello server **Overview** blade, scroll down until you see hello database tile on hello bottom.</span></span> <span data-ttu-id="4afff-158">Wszystkie hello bazy danych będzie wyświetlane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4afff-158">All hello databases will be listed in hello table.</span></span> <span data-ttu-id="4afff-159">Kliknij przycisk **usunąć** polecenia przycisk tooopen hello usunięcie potwierdzenie bloku.</span><span class="sxs-lookup"><span data-stu-id="4afff-159">click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

![Pokaż-baz danych](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="4afff-161">Pokaż szczegóły bazy danych MySQL serwera Azure</span><span class="sxs-lookup"><span data-stu-id="4afff-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="4afff-162">Kliknij przycisk **właściwości** w obszarze **ustawienia** na powitania serwera zostanie otwarty hello blok **właściwości** bloku.</span><span class="sxs-lookup"><span data-stu-id="4afff-162">Click **Properties** under **Settings** on hello server blade will open hello **Properties** blade.</span></span> <span data-ttu-id="4afff-163">Następnie można wyświetlić wszystkie szczegółowe informacje o serwerze hello.</span><span class="sxs-lookup"><span data-stu-id="4afff-163">Then you can view all detailed information about hello server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4afff-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4afff-164">Next steps</span></span>

[<span data-ttu-id="4afff-165">Szybki Start: Tworzenie bazy danych platformy Azure dla serwera MySQL przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4afff-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
