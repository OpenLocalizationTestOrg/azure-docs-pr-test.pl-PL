---
title: "aaaConnect istniejącej usługi aplikacji Azure tooAzure bazy danych dla programu MySQL | Dokumentacja firmy Microsoft"
description: "Instrukcje dotyczące sposób łączenia tooproperly tooAzure usłudze Azure App Service istniejącej bazy danych dla programu MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a><span data-ttu-id="d2b51-103">Połącz istniejące usługi Azure App Service tooAzure bazy danych MySQL serwera</span><span class="sxs-lookup"><span data-stu-id="d2b51-103">Connect an existing Azure App Service tooAzure Database for MySQL server</span></span>
<span data-ttu-id="d2b51-104">W tym dokumencie opisano sposób tooconnect istniejących tooyour usłudze Azure App Service MySQL serwera bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b51-104">This document explains how tooconnect an existing Azure App Service tooyour Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d2b51-105">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="d2b51-105">Before you begin</span></span>
<span data-ttu-id="d2b51-106">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2b51-106">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d2b51-107">Utwórz bazę danych Azure dla serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="d2b51-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="d2b51-108">Aby uzyskać więcej informacji, zobacz zbyt[jak toocreate Azure bazy danych MySQL serwera z portalu](quickstart-create-mysql-server-database-using-azure-portal.md) lub [jak toocreate Azure bazy danych MySQL serwera przy użyciu interfejsu wiersza polecenia](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d2b51-108">For details, refer too[How toocreate Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How toocreate Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="d2b51-109">Obecnie istnieją dwa dostęp tooenable rozwiązań z usługi aplikacji Azure tooan bazy danych Azure dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="d2b51-109">Currently there are two solutions tooenable access from an Azure App Service tooan Azure Database for MySQL.</span></span> <span data-ttu-id="d2b51-110">Oba rozwiązania wymagają konfigurowania reguł zapory na poziomie serwera.</span><span class="sxs-lookup"><span data-stu-id="d2b51-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a><span data-ttu-id="d2b51-111">Rozwiązanie 1 — Tworzenie tooallow reguły zapory wszystkich adresów IP</span><span class="sxs-lookup"><span data-stu-id="d2b51-111">Solution 1 - Create a firewall rule tooallow all IPs</span></span>
<span data-ttu-id="d2b51-112">Bazy danych platformy Azure dla programu MySQL zapewnia zabezpieczenia dostępu przy użyciu tooprotect zapory danych.</span><span class="sxs-lookup"><span data-stu-id="d2b51-112">Azure Database for MySQL provides access security using a firewall tooprotect your data.</span></span> <span data-ttu-id="d2b51-113">Gdy łączących się z usługi aplikacji Azure tooAzure bazy danych MySQL serwera, należy pamiętać, że hello wychodzących adresów IP z usługi aplikacji są dynamiczne charakter.</span><span class="sxs-lookup"><span data-stu-id="d2b51-113">When connecting from an Azure App Service tooAzure Database for MySQL server, keep in mind that hello outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="d2b51-114">dostępność hello tooensure usłudze Azure App Service, firma Microsoft zaleca używanie tego rozwiązania tooallow wszystkich adresów IP.</span><span class="sxs-lookup"><span data-stu-id="d2b51-114">tooensure hello availability of your Azure App Service, we recommend using this solution tooallow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="d2b51-115">Firma Microsoft współpracuje dla długoterminowego tooavoid rozwiązanie umożliwiający wszystkie adresy IP dla usług Azure tooconnect tooAzure bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="d2b51-115">Microsoft is working for a long-term solution tooavoid allowing all IPs for Azure services tooconnect tooAzure Database for MySQL.</span></span>

1. <span data-ttu-id="d2b51-116">W bloku serwera MySQL hello, w obszarze Ustawienia kliknij pozycję **zabezpieczenia połączeń** tooopen hello zabezpieczenia połączeń bloku hello Azure bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="d2b51-116">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Portal Azure — kliknij przycisk Zabezpieczenia połączeń](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="d2b51-118">Wprowadź **Nazwa reguły**, **ustawiony POCZĄTKOWY adres IP**, i **KOŃCOWEMU adresowi IP**.</span><span class="sxs-lookup"><span data-stu-id="d2b51-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="d2b51-119">Następnie kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="d2b51-119">Then click **Save**.</span></span>
   - <span data-ttu-id="d2b51-120">Nazwa reguły: Zezwalaj-All-adresów IP</span><span class="sxs-lookup"><span data-stu-id="d2b51-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="d2b51-121">Uruchom IP: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="d2b51-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="d2b51-122">Zakończenie IP: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="d2b51-122">End IP: 255.255.255.255</span></span>

   ![Portal Azure — Dodaj wszystkie adresy IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a><span data-ttu-id="d2b51-124">Rozwiązanie 2 — Tworzenie Zapora tooexplicitly reguły Zezwalaj wychodzących adresów IP</span><span class="sxs-lookup"><span data-stu-id="d2b51-124">Solution 2 - Create a firewall rule tooexplicitly allow outbound IPs</span></span>
<span data-ttu-id="d2b51-125">Można jawnie dodać wszystkie hello wychodzących adresów IP z usługi aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b51-125">You can explicitly add all hello outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="d2b51-126">W bloku właściwości usługi aplikacji hello, wyświetlanie użytkownika **WYCHODZĄCY adres IP**.</span><span class="sxs-lookup"><span data-stu-id="d2b51-126">On hello App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Portal Azure — widok wychodzących adresów IP](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="d2b51-128">W bloku zabezpieczeń połączenia MySQL hello Dodaj wychodzących adresów IP pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="d2b51-128">On hello MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Portal Azure — Dodaj jawne adresów IP](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="d2b51-130">Należy pamiętać, zbyt**zapisać** reguł zapory.</span><span class="sxs-lookup"><span data-stu-id="d2b51-130">Remember too**Save** your firewall rules.</span></span>

<span data-ttu-id="d2b51-131">Chociaż hello Azure App service próbuje stała adresy IP tookeep wraz z upływem czasu, istnieją przypadki, w którym może zmienić hello adresów IP.</span><span class="sxs-lookup"><span data-stu-id="d2b51-131">Though hello Azure App service attempts tookeep IP addresses constant over time, there are cases where hello IP addresses may change.</span></span> <span data-ttu-id="d2b51-132">Na przykład gdy hello odtwarza aplikacji występuje operacji skalowania lub dodania nowych maszyn w danych Azure regionalnych centrach tooincrease hello pojemności.</span><span class="sxs-lookup"><span data-stu-id="d2b51-132">For example, when hello app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers tooincrease hello capacity.</span></span> <span data-ttu-id="d2b51-133">Podczas zmiany adresów hello IP, aplikacja hello można przestój w przypadku hello nie można już połączyć toohello MySQL serwera.</span><span class="sxs-lookup"><span data-stu-id="d2b51-133">When hello IP addresses change, hello app could experience downtime in hello event it can no longer connect toohello MySQL server.</span></span> <span data-ttu-id="d2b51-134">W przypadku wybrania jednej hello poprzedzających rozwiązania należy wziąć pod uwagę tej możliwości.</span><span class="sxs-lookup"><span data-stu-id="d2b51-134">Consider this potential when choosing one of hello preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="d2b51-135">Konfiguracja protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="d2b51-135">SSL configuration</span></span>
<span data-ttu-id="d2b51-136">Bazy danych platformy Azure dla programu MySQL jest domyślnie włączony protokół SSL.</span><span class="sxs-lookup"><span data-stu-id="d2b51-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="d2b51-137">Jeśli aplikacja nie używa protokołu SSL tooconnect toohello w bazie danych, należy toodisable SSL na serwerze MySQL.</span><span class="sxs-lookup"><span data-stu-id="d2b51-137">If your application is not using SSL tooconnect toohello database, then you need toodisable SSL on MySQL server.</span></span> <span data-ttu-id="d2b51-138">Aby uzyskać więcej informacji na temat protokołu SSL, zobacz tooconfigure [przy użyciu protokołu SSL z bazą danych Azure dla programu MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="d2b51-138">For details on how tooconfigure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2b51-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d2b51-139">Next steps</span></span>
<span data-ttu-id="d2b51-140">Aby uzyskać więcej informacji dotyczących parametrów połączenia, można znaleźć zbyt[parametry połączenia](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="d2b51-140">For more information about connection strings, refer too[Connection Strings](howto-connection-string.md).</span></span>
