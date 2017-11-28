---
title: "aaaCreate i zarządzania nimi Azure bazy danych MySQL reguł zapory przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu hello portalu Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="02328-103">Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="02328-103">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="02328-104">Reguły zapory poziomu serwera Włącz tooaccess administratorów bazy danych Azure MySQL serwera z określonego adresu IP lub zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="02328-104">Server-level firewall rules enable administrators tooaccess an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="02328-105">Utworzyć regułę zapory poziomu serwera w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="02328-105">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="02328-106">W bloku serwera MySQL hello, w obszarze Ustawienia kliknij pozycję **zabezpieczenia połączeń** tooopen hello zabezpieczenia połączeń bloku hello Azure bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="02328-106">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Portal Azure — kliknij przycisk Zabezpieczenia połączeń](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="02328-108">Kliknij przycisk **dodać Moje IP** na powitania narzędzi toocreate reguły hello adresu IP komputera, ponieważ postrzegane przez hello systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="02328-108">Click **Add My IP** on hello toolbar toocreate a rule with hello IP address of your computer, as perceived by hello Azure system.</span></span>

   ![Portal Azure — kliknij przycisk Dodaj mój adres IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="02328-110">Zweryfikuj swój adres IP przed zapisaniem konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="02328-110">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="02328-111">W niektórych sytuacjach adres IP hello uwzględniony przez Azure portal różni się od hello adres IP używany podczas uzyskiwania dostępu do hello internet i serwerach Azure.</span><span class="sxs-lookup"><span data-stu-id="02328-111">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="02328-112">Dlatego może być konieczne toochange hello Start adresów IP i końcowemu adresowi IP toomake hello funkcja reguły zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="02328-112">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>

   <span data-ttu-id="02328-113">Użyj aparatu wyszukiwania lub inne narzędzia online toocheck adresu IP (na przykład, wyszukaj "co to jest adresu IP").</span><span class="sxs-lookup"><span data-stu-id="02328-113">Use a search engine or other online tool toocheck your own IP address (for example, search "what is my IP address").</span></span>

   ![Bing w celu przedstawienia Moje IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="02328-115">Dodaj dodatkowy adres zakresów.</span><span class="sxs-lookup"><span data-stu-id="02328-115">Add additional address ranges.</span></span> <span data-ttu-id="02328-116">W zasadach hello hello Azure bazy danych MySQL zapory można określić pojedynczy adres IP lub zakresu adresów.</span><span class="sxs-lookup"><span data-stu-id="02328-116">In hello rules for hello Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="02328-117">Jeśli chcesz toolimit hello reguły tooone pojedynczy adres IP, typ hello sam adres w polu hello Start IP i końcowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="02328-117">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="02328-118">Otwarcie zapory hello umożliwia administratorom i użytkownikom tooaccess wszystkie bazy danych na powitania MySQL serwera toowhich mają prawidłowe poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="02328-118">Opening hello firewall enables administrators and users tooaccess any database on hello MySQL server toowhich they have valid credentials.</span></span>

   ![<span data-ttu-id="02328-119">Portal Azure — reguły zapory</span><span class="sxs-lookup"><span data-stu-id="02328-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="02328-120">Kliknij przycisk **zapisać** na hello toosave narzędzi tę regułę zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="02328-120">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="02328-121">Poczekaj, aż hello potwierdzenie, że reguły zapory toohello aktualizacji hello zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="02328-121">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

   ![Portal Azure — kliknij przycisk Zapisz](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="02328-123">Zarządzanie istniejącej reguły zapory poziomu serwera za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="02328-123">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="02328-124">Powtórz reguły zapory hello hello kroki toomanage.</span><span class="sxs-lookup"><span data-stu-id="02328-124">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="02328-125">tooadd hello bieżącego komputera, kliknij przycisk **+ Dodaj adres IP Moje**.</span><span class="sxs-lookup"><span data-stu-id="02328-125">tooadd hello current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="02328-126">tooadd dodatkowe adresy IP, wpisz w hello **Nazwa reguły**, **START IP**, i **KOŃCOWEMU adresowi IP**.</span><span class="sxs-lookup"><span data-stu-id="02328-126">tooadd additional IP addresses, type in hello **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="02328-127">toomodify istniejącą regułę, kliknij polach hello w regule hello i modyfikować.</span><span class="sxs-lookup"><span data-stu-id="02328-127">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span>
* <span data-ttu-id="02328-128">toodelete istniejącą regułę, kliknij przycisk wielokropka hello [...], a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="02328-128">toodelete an existing rule, click hello ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="02328-129">Kliknij przycisk **zapisać** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="02328-129">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02328-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02328-130">Next steps</span></span>
- <span data-ttu-id="02328-131">Aby uzyskać pomoc w łączenie tooan Azure bazy danych MySQL serwera, zobacz [biblioteki połączeń dla bazy danych Azure dla programu MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="02328-131">For help in connecting tooan Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
