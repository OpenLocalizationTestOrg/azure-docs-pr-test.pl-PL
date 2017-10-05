---
title: "Tworzenie i zarządzanie Azure bazy danych dla serwera MySQL przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak szybko utworzyć nową bazę danych Azure dla serwera MySQL i zarządzanie serwerem przy użyciu portalu Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4605518b6955d9943e76c25df2d4105a6a94433d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="b0856-103">Tworzenie i zarządzanie Azure bazy danych dla serwera MySQL przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b0856-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="b0856-104">W tym artykule opisano, jak szybko utworzyć nową bazę danych Azure dla serwera MySQL i zarządzanie serwerem przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b0856-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage the server using the Azure Portal.</span></span> <span data-ttu-id="b0856-105">Zarządzanie serwerem obejmuje wyświetlanie szczegółów serwera & bazy danych, resetowanie hasła i usunięcie serwera.</span><span class="sxs-lookup"><span data-stu-id="b0856-105">Server management includes viewing server details & databases, resetting password and deleting the server.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="b0856-106">Logowanie do witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b0856-106">Log in to the Azure portal</span></span>
<span data-ttu-id="b0856-107">Zaloguj się do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b0856-107">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="b0856-108">Tworzenie serwera usługi Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="b0856-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="b0856-109">Wykonaj następujące kroki, aby utworzyć bazę danych Azure MySQL serwera o nazwie "mysqlserver4demo"</span><span class="sxs-lookup"><span data-stu-id="b0856-109">Follow these steps to create an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="b0856-110">Kliknij przycisk 1 **nowy** znaleziono przycisku w lewym górnym rogu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b0856-110">1- Click **New** button found on the upper left-hand corner of the Azure portal.</span></span>

<span data-ttu-id="b0856-111">Wybierz opcję 2 **baz danych** z nowej strony, a następnie wybierz **bazy danych Azure dla programu MySQL** ze strony baz danych.</span><span class="sxs-lookup"><span data-stu-id="b0856-111">2- Select **Databases** from the New page, and select **Azure Database for MySQL** from the Databases page.</span></span>

> <span data-ttu-id="b0856-112">Baza danych Azure dla serwera MySQL jest tworzony z zdefiniowanego zestawu [obliczeniowej i pamięci masowej](./concepts-compute-unit-and-storage.md) zasobów.</span><span class="sxs-lookup"><span data-stu-id="b0856-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="b0856-113">Baza danych została utworzona w ramach grupy zasobów platformy Azure i w bazie danych Azure dla serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="b0856-113">The database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![Utwórz nowy serwera](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="b0856-115">3 - Wypełnianie bazy danych Azure MySQL formularza z następującymi informacjami:</span><span class="sxs-lookup"><span data-stu-id="b0856-115">3- Fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="b0856-116">**Pole formularza**</span><span class="sxs-lookup"><span data-stu-id="b0856-116">**Form Field**</span></span> | <span data-ttu-id="b0856-117">**Opis pola**</span><span class="sxs-lookup"><span data-stu-id="b0856-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="b0856-118">*Nazwa serwera*</span><span class="sxs-lookup"><span data-stu-id="b0856-118">*Server name*</span></span> | <span data-ttu-id="b0856-119">Azure mysql (nazwa serwera jest globalnie unikatowa)</span><span class="sxs-lookup"><span data-stu-id="b0856-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="b0856-120">*Subskrypcja*</span><span class="sxs-lookup"><span data-stu-id="b0856-120">*Subscription*</span></span> | <span data-ttu-id="b0856-121">MySQLaaS (wybierz z listy rozwijanej)</span><span class="sxs-lookup"><span data-stu-id="b0856-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="b0856-122">*Grupa zasobów*</span><span class="sxs-lookup"><span data-stu-id="b0856-122">*Resource group*</span></span> | <span data-ttu-id="b0856-123">myresource (Utwórz nową grupę zasobów lub użyć istniejącego)</span><span class="sxs-lookup"><span data-stu-id="b0856-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="b0856-124">*Identyfikator logowania administratora serwera*</span><span class="sxs-lookup"><span data-stu-id="b0856-124">*Server admin login*</span></span> | <span data-ttu-id="b0856-125">myadmin (skonfiguruj nazwę konta administratora)</span><span class="sxs-lookup"><span data-stu-id="b0856-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="b0856-126">*Hasło*</span><span class="sxs-lookup"><span data-stu-id="b0856-126">*Password*</span></span> | <span data-ttu-id="b0856-127">ustawienia hasła do konta administratora</span><span class="sxs-lookup"><span data-stu-id="b0856-127">setup admin account password</span></span> |
| <span data-ttu-id="b0856-128">*Potwierdź hasło*</span><span class="sxs-lookup"><span data-stu-id="b0856-128">*Confirm password*</span></span> | <span data-ttu-id="b0856-129">potwierdź hasło konta administratora</span><span class="sxs-lookup"><span data-stu-id="b0856-129">confirm admin account password</span></span> |
| <span data-ttu-id="b0856-130">*Lokalizacja*</span><span class="sxs-lookup"><span data-stu-id="b0856-130">*Location*</span></span> | <span data-ttu-id="b0856-131">Europa Północna (wybór między Europa Północna, Europa i zachodnie stany USA)</span><span class="sxs-lookup"><span data-stu-id="b0856-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="b0856-132">*Wersja*</span><span class="sxs-lookup"><span data-stu-id="b0856-132">*Version*</span></span> | <span data-ttu-id="b0856-133">5.6 (Wybierz bazy danych Azure w wersji server MySQL)</span><span class="sxs-lookup"><span data-stu-id="b0856-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="b0856-134">Kliknij przycisk 4 **warstwa cenowa** umożliwia określenie poziomu wydajności i warstwy usługi dla nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="b0856-134">4- Click **Pricing tier** to specify the service tier and performance level for your new server.</span></span> <span data-ttu-id="b0856-135">Obliczenia bazy danych od 50 do 100 w warstwie podstawowa, 100 i 200 w warstwie standardowa, można skonfigurować jednostki i Magazyn można dodać zależności od uwzględniona ilość.</span><span class="sxs-lookup"><span data-stu-id="b0856-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="b0856-136">Ten przewodnik Porada umożliwia wybierz 50 Jednostka obliczeniowa i 50GB.</span><span class="sxs-lookup"><span data-stu-id="b0856-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="b0856-137">Kliknij przycisk **OK** Aby zapisać wybrane opcje.</span><span class="sxs-lookup"><span data-stu-id="b0856-137">Click **OK** to save your selection.</span></span>
<span data-ttu-id="b0856-138">![Utwórz server--warstwy cenowej](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="b0856-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="b0856-139">Kliknij przycisk 5 **Utwórz** do udostępnienia serwera.</span><span class="sxs-lookup"><span data-stu-id="b0856-139">5- Click **Create** to provision the server.</span></span> <span data-ttu-id="b0856-140">Aprowizacja zajmuje kilka minut.</span><span class="sxs-lookup"><span data-stu-id="b0856-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="b0856-141">Zaznacz opcję **Przypnij do pulpitu nawigacyjnego**, aby łatwo śledzić wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b0856-141">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="b0856-142">Mimo że maksymalnie 1000GB w warstwie podstawowa i 10000 w warstwie standardowa będą obsługiwane dla magazynu, dla publicznej wersji zapoznawczej, pamięci masowej, jest ona nadal maksymalnie 1000GB tymczasowo.</span><span class="sxs-lookup"><span data-stu-id="b0856-142">Although up to 1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, the maximum storage is still limited to 1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="b0856-143">Aktualizacja bazy danych Azure dla serwera MySQL</span><span class="sxs-lookup"><span data-stu-id="b0856-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="b0856-144">Po udostępnieniu nowego serwera użytkownik ma 2 opcje do edycji istniejącego serwera: resetowanie hasła administratora lub skalowania w górę/dół serwera, zmieniając jednostki obliczeń.</span><span class="sxs-lookup"><span data-stu-id="b0856-144">After new server is provisioned, user has 2 options to edit an existing server: reset administrator password or scale up/down the server by changing the compute-units.</span></span>

### <a name="change-the-administrator-user-password"></a><span data-ttu-id="b0856-145">Zmień hasło użytkownika administratora</span><span class="sxs-lookup"><span data-stu-id="b0856-145">Change the administrator user password</span></span>
<span data-ttu-id="b0856-146">1 — na serwerze **omówienie** bloku, kliknij przycisk **resetowania hasła** do wypełnienia okna wprowadzania i potwierdzenie hasła.</span><span class="sxs-lookup"><span data-stu-id="b0856-146">1- On the server **Overview** blade, click **Reset password** to populate a password input and confirmation window.</span></span>

<span data-ttu-id="b0856-147">2 — wprowadź nowe hasło i Potwierdź hasło w oknie, jak pokazano poniżej: ![resetowania hasła](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="b0856-147">2- Enter new password and confirm the password in the window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="b0856-148">Kliknij 3 **OK** można zapisać nowego hasła.</span><span class="sxs-lookup"><span data-stu-id="b0856-148">3- Click **OK** to save the new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="b0856-149">Skalowanie w górę/dół zmieniając obliczeniowe jednostki</span><span class="sxs-lookup"><span data-stu-id="b0856-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="b0856-150">1 — w bloku serwera w obszarze **ustawienia**, kliknij przycisk **warstwa cenowa** aby otworzyć blok warstwa cenowa Azure bazy danych MySQL serwera.</span><span class="sxs-lookup"><span data-stu-id="b0856-150">1- On the server blade, under **Settings**, click **Pricing tier** to open the Pricing tier blade for the Azure Database for MySQL server.</span></span>

<span data-ttu-id="b0856-151">2-wykonaj krok 4 w **utworzenia bazy danych MySQL serwera Azure** zmiany obliczeniowe jednostki w tej samej warstwie cenowej.</span><span class="sxs-lookup"><span data-stu-id="b0856-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** to change Compute Units in the same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="b0856-152">Usuwanie bazy danych Azure dla serwera MySQL</span><span class="sxs-lookup"><span data-stu-id="b0856-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="b0856-153">1 — na serwerze **omówienie** bloku, kliknij przycisk **usunąć** przycisku polecenia, aby otworzyć blok potwierdzający usunięcie.</span><span class="sxs-lookup"><span data-stu-id="b0856-153">1- On the server **Overview** blade, click **Delete** command button to open the Deleting confirmation blade.</span></span>

<span data-ttu-id="b0856-154">2 — wpisz prawidłową nazwę serwera w polu wejściowym bloku o potwierdzenie dwa razy.</span><span class="sxs-lookup"><span data-stu-id="b0856-154">2- Type the correct server name in input box of the blade for double confirmation.</span></span>

<span data-ttu-id="b0856-155">Kliknij 3 **usunąć** przycisk ponownie, aby potwierdzić usunięcie akcji i poczekaj, aż "Usuwanie sukces" popup na pasku powiadomień.</span><span class="sxs-lookup"><span data-stu-id="b0856-155">3- Click **Delete** button again to confirm deleting action and wait for “Deleting success” popup on the notification bar.</span></span>

## <a name="list-the-azure-database-for-mysql-databases"></a><span data-ttu-id="b0856-156">Lista Azure bazy danych dla baz danych MySQL</span><span class="sxs-lookup"><span data-stu-id="b0856-156">List the Azure Database for MySQL databases</span></span>
<span data-ttu-id="b0856-157">Na serwerze **omówienie** bloku, przewiń w dół, aż zostanie wyświetlony Kafelek na dole bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b0856-157">On the server **Overview** blade, scroll down until you see the database tile on the bottom.</span></span> <span data-ttu-id="b0856-158">Wszystkie bazy danych będzie wyświetlane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="b0856-158">All the databases will be listed in the table.</span></span> <span data-ttu-id="b0856-159">Kliknij przycisk **usunąć** przycisku polecenia, aby otworzyć blok potwierdzający usunięcie.</span><span class="sxs-lookup"><span data-stu-id="b0856-159">click **Delete** command button to open the Deleting confirmation blade.</span></span>

![Pokaż-baz danych](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="b0856-161">Pokaż szczegóły bazy danych MySQL serwera Azure</span><span class="sxs-lookup"><span data-stu-id="b0856-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="b0856-162">Kliknij przycisk **właściwości** w obszarze **ustawienia** na serwerze zostanie otwarty blok **właściwości** bloku.</span><span class="sxs-lookup"><span data-stu-id="b0856-162">Click **Properties** under **Settings** on the server blade will open the **Properties** blade.</span></span> <span data-ttu-id="b0856-163">Następnie można wyświetlić wszystkie szczegółowe informacje o serwerze.</span><span class="sxs-lookup"><span data-stu-id="b0856-163">Then you can view all detailed information about the server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0856-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b0856-164">Next steps</span></span>

[<span data-ttu-id="b0856-165">Szybki Start: Tworzenie bazy danych platformy Azure dla serwera MySQL przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b0856-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
