---
title: "Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu portalu Azure"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 20ac1392949a6f604e68d984cb50273b61051037
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="a159c-103">Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a159c-103">Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="a159c-104">Reguły zapory poziomu serwera umożliwiają administratorom dostęp do bazy danych Azure PostgreSQL serwera z określonego adresu IP lub zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="a159c-104">Server-level firewall rules enable administrators to access an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a159c-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a159c-105">Prerequisites</span></span>
<span data-ttu-id="a159c-106">Do wykonania kroków opisanych ten przewodnik, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="a159c-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="a159c-107">Serwer [utworzenia bazy danych Azure dla PostgreSQL](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a159c-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="a159c-108">Tworzenie reguły zapory na poziomie serwera w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a159c-108">Create a server-level firewall rule in the Azure portal</span></span>
1. <span data-ttu-id="a159c-109">W bloku serwera PostgreSQL, w obszarze Ustawienia kliknij pozycję **zabezpieczenia połączeń** aby otworzyć blok połączenia zabezpieczeń bazy danych Azure dla PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a159c-109">On the PostgreSQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for PostgreSQL.</span></span>

  ![Portal Azure — kliknij przycisk Zabezpieczenia połączeń](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="a159c-111">Kliknij przycisk **dodać Moje IP** na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="a159c-111">Click **Add My IP** on the toolbar.</span></span> <span data-ttu-id="a159c-112">Spowoduje to utworzenie reguły automatycznie przy użyciu adresu IP komputera, jako widocznego w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="a159c-112">This will create a rule automatically with the IP address of your computer, as perceived by the Azure system.</span></span>

  ![Portal Azure — kliknij przycisk Dodaj mój adres IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="a159c-114">Zweryfikuj swój adres IP przed zapisaniem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a159c-114">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="a159c-115">W niektórych sytuacjach adres IP uwzględniony przez Azure portal różni się od adresu IP, używana podczas uzyskiwania dostępu do Internetu i serwery usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="a159c-115">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="a159c-116">Dlatego może być konieczne zmiany Start IP i końcowemu adresowi IP, aby funkcja reguły zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="a159c-116">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>
<span data-ttu-id="a159c-117">Użyj aparatu wyszukiwania lub innego narzędzia online, aby sprawdzić własnego adresu IP (na przykład wyszukiwania usługi Bing "co to jest IP Moje").</span><span class="sxs-lookup"><span data-stu-id="a159c-117">Use a search engine or other online tool to check your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Co to jest Mój IP wyszukiwania usługi Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="a159c-119">Dodaj dodatkowy adres zakresów.</span><span class="sxs-lookup"><span data-stu-id="a159c-119">Add additional address ranges.</span></span> <span data-ttu-id="a159c-120">W zasadach zapory PostgreSQL bazą danych Azure można określić pojedynczy adres IP lub zakresu adresów.</span><span class="sxs-lookup"><span data-stu-id="a159c-120">In the rules for the Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="a159c-121">Jeśli chcesz ograniczyć regułę jeden pojedynczy adres IP wpisz ten sam adres w polu Start IP i końcowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="a159c-121">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="a159c-122">Otwarcie zapory umożliwia administratorom i użytkownikom do dowolnej bazy danych na serwerze PostgreSQL, do którego mają prawidłowe poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="a159c-122">Opening the firewall enables administrators and users to login to any database on the PostgreSQL server to which they have valid credentials.</span></span>

  ![<span data-ttu-id="a159c-123">Portal Azure — reguły zapory</span><span class="sxs-lookup"><span data-stu-id="a159c-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="a159c-124">Kliknij przycisk **zapisać** na pasku narzędzi, aby zapisać tę regułę zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="a159c-124">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="a159c-125">Poczekaj na potwierdzenie pomyślnego aktualizacji reguł zapory.</span><span class="sxs-lookup"><span data-stu-id="a159c-125">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

  ![Portal Azure — kliknij przycisk Zapisz](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="a159c-127">Zarządzanie istniejącymi regułami zapory na poziomie serwera przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a159c-127">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="a159c-128">Powtórz kroki, aby zarządzać regułami zapory.</span><span class="sxs-lookup"><span data-stu-id="a159c-128">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="a159c-129">Aby dodać bieżący komputer, kliknij przycisk + **dodać Moje IP**.</span><span class="sxs-lookup"><span data-stu-id="a159c-129">To add the current computer, click the button to + **Add My IP**.</span></span> <span data-ttu-id="a159c-130">Kliknij przycisk **Zapisz**, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="a159c-130">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="a159c-131">Aby dodać kolejne adresy IP, wpisz nazwę reguły, początkowy adres IP i końcowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="a159c-131">To add additional IP addresses, type in the Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="a159c-132">Kliknij przycisk **Zapisz**, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="a159c-132">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="a159c-133">Aby zmodyfikować istniejącą regułę, kliknij dowolne pole w regule i wprowadź zmiany.</span><span class="sxs-lookup"><span data-stu-id="a159c-133">To modify an existing rule, click any of the fields in the rule and modify.</span></span> <span data-ttu-id="a159c-134">Kliknij przycisk **Zapisz**, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="a159c-134">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="a159c-135">Aby usunąć istniejącą regułę, kliknij przycisk wielokropka [...] i kliknij przycisk Usuń, Usuń regułę.</span><span class="sxs-lookup"><span data-stu-id="a159c-135">To delete an existing rule, click the ellipsis […] and click Delete remove the rule.</span></span> <span data-ttu-id="a159c-136">Kliknij przycisk **Zapisz**, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="a159c-136">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a159c-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a159c-137">Next steps</span></span>
- <span data-ttu-id="a159c-138">Podobnie można utworzyć skrypty do [tworzenie i zarządzanie bazą danych Azure PostgreSQL reguł zapory przy użyciu wiersza polecenia platformy Azure](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a159c-138">Similarly, you can script to [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="a159c-139">Aby uzyskać pomoc w połączeniu z bazą danych PostgreSQL serwera Azure, zobacz [biblioteki połączeń dla bazy danych Azure dla PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="a159c-139">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
