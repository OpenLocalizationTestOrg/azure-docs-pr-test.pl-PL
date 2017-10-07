---
title: "aaaCreate i zarządzanie bazą danych Azure PostgreSQL reguł zapory przy użyciu portalu Azure hello | Dokumentacja firmy Microsoft"
description: "Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu hello portalu Azure"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="42303-103">Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="42303-103">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="42303-104">Reguły zapory poziomu serwera włączyć tooaccess administratorów bazy danych Azure PostgreSQL serwera z określonego adresu IP lub zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="42303-104">Server-level firewall rules enable administrators tooaccess an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="42303-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="42303-105">Prerequisites</span></span>
<span data-ttu-id="42303-106">toostep za pośrednictwem tego jak tooguide, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="42303-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="42303-107">Serwer [utworzenia bazy danych Azure dla PostgreSQL](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="42303-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="42303-108">Utworzyć regułę zapory poziomu serwera w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="42303-108">Create a server-level firewall rule in hello Azure portal</span></span>
1. <span data-ttu-id="42303-109">W bloku serwera PostgreSQL hello, w obszarze Ustawienia kliknij pozycję **zabezpieczenia połączeń** tooopen hello zabezpieczenia połączeń bloku hello Azure bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="42303-109">On hello PostgreSQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for PostgreSQL.</span></span>

  ![Portal Azure — kliknij przycisk Zabezpieczenia połączeń](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="42303-111">Kliknij przycisk **dodać Moje IP** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="42303-111">Click **Add My IP** on hello toolbar.</span></span> <span data-ttu-id="42303-112">Spowoduje to utworzenie reguły automatycznie hello adresu IP komputera, jako postrzegana przez hello systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="42303-112">This will create a rule automatically with hello IP address of your computer, as perceived by hello Azure system.</span></span>

  ![Portal Azure — kliknij przycisk Dodaj mój adres IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="42303-114">Zweryfikuj swój adres IP przed zapisaniem konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="42303-114">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="42303-115">W niektórych sytuacjach adres IP hello uwzględniony przez Azure portal różni się od hello adres IP używany podczas uzyskiwania dostępu do hello internet i serwerach Azure.</span><span class="sxs-lookup"><span data-stu-id="42303-115">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="42303-116">Dlatego może być konieczne toochange hello Start adresów IP i końcowemu adresowi IP toomake hello funkcja reguły zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="42303-116">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>
<span data-ttu-id="42303-117">Użyj aparatu wyszukiwania lub inne narzędzia online toocheck własnego adresu IP (na przykład wyszukiwania usługi Bing "co to jest IP Moje").</span><span class="sxs-lookup"><span data-stu-id="42303-117">Use a search engine or other online tool toocheck your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Co to jest Mój IP wyszukiwania usługi Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="42303-119">Dodaj dodatkowy adres zakresów.</span><span class="sxs-lookup"><span data-stu-id="42303-119">Add additional address ranges.</span></span> <span data-ttu-id="42303-120">W zasadach hello hello Azure bazy danych PostgreSQL zapory można określić pojedynczy adres IP lub zakresu adresów.</span><span class="sxs-lookup"><span data-stu-id="42303-120">In hello rules for hello Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="42303-121">Jeśli chcesz toolimit hello reguły tooone pojedynczy adres IP, typ hello sam adres w polu hello Start IP i końcowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="42303-121">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="42303-122">Otwarcie zapory hello umożliwia administratorom i użytkownikom toologin tooany bazy danych na powitania toowhich serwera PostgreSQL mają prawidłowe poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="42303-122">Opening hello firewall enables administrators and users toologin tooany database on hello PostgreSQL server toowhich they have valid credentials.</span></span>

  ![<span data-ttu-id="42303-123">Portal Azure — reguły zapory</span><span class="sxs-lookup"><span data-stu-id="42303-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="42303-124">Kliknij przycisk **zapisać** na hello toosave narzędzi tę regułę zapory poziomu serwera.</span><span class="sxs-lookup"><span data-stu-id="42303-124">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="42303-125">Poczekaj, aż hello potwierdzenie, że reguły zapory toohello aktualizacji hello zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="42303-125">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

  ![Portal Azure — kliknij przycisk Zapisz](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="42303-127">Zarządzanie istniejącej reguły zapory poziomu serwera za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="42303-127">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="42303-128">Powtórz reguły zapory hello hello kroki toomanage.</span><span class="sxs-lookup"><span data-stu-id="42303-128">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="42303-129">tooadd hello bieżącego komputera, kliknij przycisk hello zbyt + **dodać Moje IP**.</span><span class="sxs-lookup"><span data-stu-id="42303-129">tooadd hello current computer, click hello button too+ **Add My IP**.</span></span> <span data-ttu-id="42303-130">Kliknij przycisk **zapisać** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="42303-130">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="42303-131">tooadd dodatkowe adresy IP, wpisz w hello nazwę reguły, początkowy adres IP i końcowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="42303-131">tooadd additional IP addresses, type in hello Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="42303-132">Kliknij przycisk **zapisać** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="42303-132">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="42303-133">toomodify istniejącą regułę, kliknij polach hello w regule hello i modyfikować.</span><span class="sxs-lookup"><span data-stu-id="42303-133">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span> <span data-ttu-id="42303-134">Kliknij przycisk **zapisać** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="42303-134">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="42303-135">toodelete istniejącą regułę, kliknij przycisk wielokropka hello [...] i kliknij przycisk Usuń Usuń hello reguły.</span><span class="sxs-lookup"><span data-stu-id="42303-135">toodelete an existing rule, click hello ellipsis […] and click Delete remove hello rule.</span></span> <span data-ttu-id="42303-136">Kliknij przycisk **zapisać** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="42303-136">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42303-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42303-137">Next steps</span></span>
- <span data-ttu-id="42303-138">Podobnie można utworzyć skrypty zbyt[tworzenie i zarządzanie bazą danych Azure PostgreSQL reguł zapory przy użyciu wiersza polecenia platformy Azure](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="42303-138">Similarly, you can script too[Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="42303-139">Aby uzyskać pomoc w łączenie tooan Azure bazy danych dla serwera PostgreSQL, [biblioteki połączeń dla bazy danych Azure dla PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="42303-139">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
