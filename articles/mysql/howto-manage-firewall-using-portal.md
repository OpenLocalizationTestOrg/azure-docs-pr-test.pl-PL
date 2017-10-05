---
title: "Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu portalu Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 33198e5a6e11df2db3a17fc96a0b3cd4b1a284e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="02e62-103">Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="02e62-103">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="02e62-104">Reguły zapory poziomu serwera umożliwiają administratorom dostęp do bazy danych Azure MySQL serwera z określonego adresu IP lub zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="02e62-104">Server-level firewall rules enable administrators to access an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="02e62-105">Tworzenie reguły zapory na poziomie serwera w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="02e62-105">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="02e62-106">W bloku serwera MySQL, w obszarze Ustawienia kliknij pozycję **zabezpieczenia połączeń** aby otworzyć blok połączenia zabezpieczeń bazy danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="02e62-106">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Portal Azure — kliknij przycisk Zabezpieczenia połączeń](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="02e62-108">Kliknij przycisk **dodać Moje IP** na pasku narzędzi, aby utworzyć regułę przy użyciu adresu IP komputera, jako widocznego w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="02e62-108">Click **Add My IP** on the toolbar to create a rule with the IP address of your computer, as perceived by the Azure system.</span></span>

   ![Portal Azure — kliknij przycisk Dodaj mój adres IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="02e62-110">Zweryfikuj swój adres IP przed zapisaniem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="02e62-110">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="02e62-111">W niektórych sytuacjach adres IP uwzględniony przez Azure portal różni się od adresu IP, używana podczas uzyskiwania dostępu do Internetu i serwery usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="02e62-111">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="02e62-112">Dlatego może być konieczne zmiany Start IP i końcowemu adresowi IP, aby funkcja reguły zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="02e62-112">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>

   <span data-ttu-id="02e62-113">Użyj aparatu wyszukiwania lub innego narzędzia online w celu sprawdzenia adresu IP (na przykład, wyszukaj "co to jest adresu IP").</span><span class="sxs-lookup"><span data-stu-id="02e62-113">Use a search engine or other online tool to check your own IP address (for example, search "what is my IP address").</span></span>

   ![Bing w celu przedstawienia Moje IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="02e62-115">Dodaj dodatkowy adres zakresów.</span><span class="sxs-lookup"><span data-stu-id="02e62-115">Add additional address ranges.</span></span> <span data-ttu-id="02e62-116">W zasadach zapory MySQL bazą danych Azure można określić pojedynczy adres IP lub zakresu adresów.</span><span class="sxs-lookup"><span data-stu-id="02e62-116">In the rules for the Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="02e62-117">Jeśli chcesz ograniczyć regułę jeden pojedynczy adres IP wpisz ten sam adres w polu Start IP i końcowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="02e62-117">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="02e62-118">Otwarcie zapory umożliwia Administratorzy i użytkownicy mogą uzyskać dostępu do dowolnej bazy danych na serwerze MySQL, do których mają prawidłowe poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="02e62-118">Opening the firewall enables administrators and users to access any database on the MySQL server to which they have valid credentials.</span></span>

   ![<span data-ttu-id="02e62-119">Portal Azure — reguły zapory</span><span class="sxs-lookup"><span data-stu-id="02e62-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="02e62-120">Kliknij przycisk **zapisać** na pasku narzędzi, aby zapisać tę regułę zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="02e62-120">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="02e62-121">Poczekaj na potwierdzenie pomyślnego aktualizacji reguł zapory.</span><span class="sxs-lookup"><span data-stu-id="02e62-121">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

   ![Portal Azure — kliknij przycisk Zapisz](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="02e62-123">Zarządzanie istniejącymi regułami zapory na poziomie serwera przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="02e62-123">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="02e62-124">Powtórz kroki, aby zarządzać regułami zapory.</span><span class="sxs-lookup"><span data-stu-id="02e62-124">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="02e62-125">Aby dodać bieżący komputer, kliknij przycisk **+ Dodaj adres IP Moje**.</span><span class="sxs-lookup"><span data-stu-id="02e62-125">To add the current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="02e62-126">Aby dodać dodatkowe adresy IP, wpisz w **Nazwa reguły**, **START IP**, i **KOŃCOWEMU adresowi IP**.</span><span class="sxs-lookup"><span data-stu-id="02e62-126">To add additional IP addresses, type in the **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="02e62-127">Aby zmodyfikować istniejącą regułę, kliknij dowolne pole w regule i wprowadź zmiany.</span><span class="sxs-lookup"><span data-stu-id="02e62-127">To modify an existing rule, click any of the fields in the rule and modify.</span></span>
* <span data-ttu-id="02e62-128">Aby usunąć istniejącą regułę, kliknij przycisk wielokropka [...], a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="02e62-128">To delete an existing rule, click the ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="02e62-129">Kliknij przycisk **Zapisz**, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="02e62-129">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02e62-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02e62-130">Next steps</span></span>
- <span data-ttu-id="02e62-131">Aby uzyskać pomoc w nawiązywania połączenia z bazą danych Azure dla serwera MySQL, [biblioteki połączeń dla bazy danych Azure dla programu MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="02e62-131">For help in connecting to an Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
